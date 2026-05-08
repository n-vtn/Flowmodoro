<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="apple-mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
  <meta name="theme-color" content="#0f172a" />
  <title>Flowmodoro Bank</title>
  <style>
    :root {
      font-family: -apple-system, BlinkMacSystemFont, system-ui, sans-serif;
      background: #020617;
      color: #f8fafc;
    }

    * { box-sizing: border-box; }

    body {
      margin: 0;
      min-height: 100vh;
      padding: 24px;
      background: radial-gradient(circle at top left, #1e293b, #020617 70%);
    }

    .app {
      width: min(1180px, 100%);
      min-height: calc(100vh - 48px);
      margin: 0 auto;
      padding: 28px;
      border-radius: 34px;
      background: rgba(15, 23, 42, 0.92);
      border: 1px solid rgba(148, 163, 184, 0.2);
      box-shadow: 0 24px 90px rgba(0, 0, 0, 0.5);
      display: grid;
      grid-template-rows: auto 1fr;
      gap: 24px;
    }

    header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 20px;
    }

    h1 {
      margin: 0;
      font-size: 38px;
      letter-spacing: -0.05em;
    }

    .subtitle {
      margin: 6px 0 0;
      color: #94a3b8;
      line-height: 1.4;
    }

    .tabs {
      display: flex;
      gap: 10px;
      padding: 6px;
      border-radius: 999px;
      background: rgba(2, 6, 23, 0.55);
      border: 1px solid rgba(148, 163, 184, 0.16);
    }

    .tab {
      border: 0;
      border-radius: 999px;
      padding: 12px 18px;
      color: #cbd5e1;
      background: transparent;
      font-weight: 750;
      cursor: pointer;
    }

    .tab.active {
      background: #f8fafc;
      color: #020617;
    }

    .page { display: none; }
    .page.active { display: block; }

    .dashboard {
      height: 100%;
      display: grid;
      grid-template-columns: 1.2fr 0.8fr;
      gap: 24px;
    }

    .panel {
      border-radius: 30px;
      background: rgba(30, 41, 59, 0.58);
      border: 1px solid rgba(148, 163, 184, 0.15);
      padding: 24px;
    }

    .main-panel {
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      min-height: 560px;
    }

    .status {
      display: inline-flex;
      gap: 8px;
      align-items: center;
      padding: 8px 12px;
      border-radius: 999px;
      background: rgba(148, 163, 184, 0.12);
      color: #cbd5e1;
      font-size: 14px;
      width: fit-content;
    }

    .dot {
      width: 9px;
      height: 9px;
      border-radius: 50%;
      background: #64748b;
    }

    .dot.work { background: #22c55e; }
    .dot.break { background: #38bdf8; }

    .timer {
      text-align: center;
      font-size: clamp(96px, 14vw, 176px);
      font-weight: 850;
      letter-spacing: -0.08em;
      font-variant-numeric: tabular-nums;
      margin: 20px 0;
    }

    .controls {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 12px;
    }

    button, input, select { font: inherit; }

    button {
      border: 0;
      border-radius: 20px;
      padding: 18px 14px;
      color: white;
      font-weight: 800;
      background: #334155;
      cursor: pointer;
    }

    button:active { transform: scale(0.98); }
    button:disabled { opacity: 0.38; cursor: not-allowed; }

    .primary { background: #16a34a; }
    .danger { background: #dc2626; }
    .blue { background: #0284c7; }
    .muted { background: #475569; }
    .wide { grid-column: 1 / -1; }

    .cards {
      display: grid;
      grid-template-columns: 1fr;
      gap: 14px;
      margin-bottom: 18px;
    }

    .card {
      padding: 20px;
      border-radius: 24px;
      background: rgba(15, 23, 42, 0.62);
      border: 1px solid rgba(148, 163, 184, 0.14);
    }

    .label {
      color: #94a3b8;
      font-size: 14px;
      margin-bottom: 8px;
    }

    .value {
      font-size: 38px;
      font-weight: 800;
      letter-spacing: -0.05em;
    }

    .settings {
      display: grid;
      grid-template-columns: 1fr;
      gap: 14px;
      margin-top: 18px;
    }

    label {
      display: block;
      margin-bottom: 8px;
      color: #94a3b8;
      font-size: 14px;
    }

    input, select {
      width: 100%;
      border: 1px solid rgba(148, 163, 184, 0.22);
      border-radius: 18px;
      padding: 16px;
      background: rgba(15, 23, 42, 0.9);
      color: white;
      outline: none;
    }

    .hint {
      margin-top: 18px;
      color: #94a3b8;
      font-size: 14px;
      line-height: 1.5;
    }

    .mini-history {
      margin-top: 20px;
      max-height: 150px;
      overflow: auto;
      font-size: 13px;
      color: #cbd5e1;
    }

    .mini-history div {
      padding: 8px 0;
      border-bottom: 1px solid rgba(148, 163, 184, 0.12);
    }

    .history-page {
      display: grid;
      grid-template-columns: 0.75fr 1.25fr;
      gap: 24px;
      height: 100%;
    }

    .summary-number {
      font-size: 68px;
      font-weight: 850;
      letter-spacing: -0.07em;
      margin: 14px 0 4px;
    }

    .week-chart {
      display: grid;
      grid-template-columns: repeat(7, 1fr);
      gap: 12px;
      height: 430px;
      align-items: end;
      padding-top: 30px;
    }

    .bar-wrap {
      height: 100%;
      display: flex;
      flex-direction: column;
      justify-content: end;
      gap: 10px;
      text-align: center;
    }

    .bar {
      min-height: 8px;
      border-radius: 18px 18px 8px 8px;
      background: linear-gradient(180deg, #38bdf8, #0284c7);
      border: 1px solid rgba(255,255,255,0.16);
    }

    .bar-label {
      color: #cbd5e1;
      font-weight: 750;
      font-size: 14px;
    }

    .bar-time {
      color: #94a3b8;
      font-size: 13px;
      font-variant-numeric: tabular-nums;
    }

    .sessions-list {
      margin-top: 20px;
      max-height: 250px;
      overflow: auto;
      color: #cbd5e1;
      font-size: 14px;
    }

    .sessions-list div {
      display: flex;
      justify-content: space-between;
      gap: 14px;
      padding: 10px 0;
      border-bottom: 1px solid rgba(148, 163, 184, 0.12);
    }

    @media (orientation: portrait) {
      body::before {
        content: "Tourne l’iPad en mode paysage pour une meilleure interface.";
        position: fixed;
        inset: 0;
        z-index: 10;
        display: flex;
        align-items: center;
        justify-content: center;
        padding: 32px;
        text-align: center;
        background: rgba(2, 6, 23, 0.94);
        color: #f8fafc;
        font-size: 24px;
        font-weight: 800;
      }
    }
  </style>
</head>
<body>
  <main class="app">
    <header>
      <div>
        <h1>Flowmodoro</h1>
        <p class="subtitle">Travaille librement, gagne de la pause, garde le surplus en banque.</p>
      </div>
      <nav class="tabs">
        <button id="tabDashboard" class="tab active">Aujourd’hui</button>
        <button id="tabHistory" class="tab">Historique</button>
      </nav>
    </header>

    <section id="dashboardPage" class="page active">
      <div class="dashboard">
        <section class="panel main-panel">
          <div class="status">
            <span id="statusDot" class="dot"></span>
            <span id="statusText">Inactif</span>
          </div>

          <div id="timer" class="timer">00:00</div>

          <div class="controls">
            <button id="startWork" class="primary">▶ Travail</button>
            <button id="stopWork" class="danger" disabled>■ Stop</button>
            <button id="startBreak" class="blue">☕ Pause</button>
            <button id="stopBreak" class="muted" disabled>✓ Fin pause</button>
          </div>
        </section>

        <aside class="panel">
          <section class="cards">
            <div class="card">
              <div class="label">Pause disponible</div>
              <div id="bankValue" class="value">0 min</div>
            </div>
            <div class="card">
              <div class="label">Ratio</div>
              <div id="ratioValue" class="value">5:1</div>
            </div>
            <div class="card">
              <div class="label">Focus aujourd’hui</div>
              <div id="todayFocusValue" class="value">0 min</div>
            </div>
          </section>

          <section class="settings">
            <div>
              <label for="ratio">Ratio travail / pause</label>
              <select id="ratio">
                <option value="1">1:1</option>
                <option value="2">2:1</option>
                <option value="3">3:1</option>
                <option value="4">4:1</option>
                <option value="5">5:1</option>
              </select>
            </div>
            <div>
              <label for="breakMinutes">Pause à prendre</label>
              <input id="breakMinutes" type="number" min="1" step="1" placeholder="minutes" />
            </div>
          </section>

          <section class="controls">
            <button id="enableNotifications" class="blue wide">Activer les notifications</button>
            <button id="reset" class="muted wide">Réinitialiser la banque</button>
          </section>

          <p class="hint">Avec un ratio 5:1, 50 minutes de travail donnent 10 minutes de pause. Tu peux en prendre une partie seulement.</p>
          <div id="history" class="mini-history"></div>
        </aside>
      </div>
    </section>

    <section id="historyPage" class="page">
      <div class="history-page">
        <aside class="panel">
          <div class="label">Focus sur les 7 derniers jours</div>
          <div id="weekTotal" class="summary-number">0h00</div>
          <p class="hint">Cette page additionne uniquement le temps de travail réellement terminé avec le bouton Stop.</p>
          <div id="sessionsList" class="sessions-list"></div>
        </aside>

        <section class="panel">
          <div class="label">Temps de focus par jour</div>
          <div id="weekChart" class="week-chart"></div>
        </section>
      </div>
    </section>
  </main>

  <script>
    const STORAGE_KEY = "flowmodoro-state-v2";

    const defaultState = {
      mode: "idle",
      activePage: "dashboard",
      ratio: 5,
      breakBankSeconds: 0,
      workStart: null,
      breakStart: null,
      plannedBreakSeconds: 0,
      history: [],
      workSessions: []
    };

    let state = loadState();

    const el = {
      tabDashboard: document.getElementById("tabDashboard"),
      tabHistory: document.getElementById("tabHistory"),
      dashboardPage: document.getElementById("dashboardPage"),
      historyPage: document.getElementById("historyPage"),
      statusDot: document.getElementById("statusDot"),
      statusText: document.getElementById("statusText"),
      timer: document.getElementById("timer"),
      bankValue: document.getElementById("bankValue"),
      ratioValue: document.getElementById("ratioValue"),
      todayFocusValue: document.getElementById("todayFocusValue"),
      ratio: document.getElementById("ratio"),
      breakMinutes: document.getElementById("breakMinutes"),
      startWork: document.getElementById("startWork"),
      stopWork: document.getElementById("stopWork"),
      startBreak: document.getElementById("startBreak"),
      stopBreak: document.getElementById("stopBreak"),
      reset: document.getElementById("reset"),
      enableNotifications: document.getElementById("enableNotifications"),
      history: document.getElementById("history"),
      weekTotal: document.getElementById("weekTotal"),
      weekChart: document.getElementById("weekChart"),
      sessionsList: document.getElementById("sessionsList")
    };

    function loadState() {
      const saved = localStorage.getItem(STORAGE_KEY);
      return saved ? { ...defaultState, ...JSON.parse(saved) } : { ...defaultState };
    }

    function saveState() {
      localStorage.setItem(STORAGE_KEY, JSON.stringify(state));
    }

    function now() { return Date.now(); }

    function secondsBetween(startMs, endMs = now()) {
      return Math.max(0, Math.floor((endMs - startMs) / 1000));
    }

    function formatClock(seconds) {
      const total = Math.max(0, Math.floor(seconds));
      const min = Math.floor(total / 60);
      const sec = total % 60;
      return `${String(min).padStart(2, "0")}:${String(sec).padStart(2, "0")}`;
    }

    function formatMinutes(seconds) {
      return `${Math.floor(seconds / 60)} min`;
    }

    function formatHoursMinutes(seconds) {
      const totalMinutes = Math.floor(seconds / 60);
      const h = Math.floor(totalMinutes / 60);
      const m = totalMinutes % 60;
      return `${h}h${String(m).padStart(2, "0")}`;
    }

    function dateKey(ms) {
      const d = new Date(ms);
      const y = d.getFullYear();
      const m = String(d.getMonth() + 1).padStart(2, "0");
      const day = String(d.getDate()).padStart(2, "0");
      return `${y}-${m}-${day}`;
    }

    function shortDayLabel(ms) {
      const d = new Date(ms);
      return d.toLocaleDateString("fr-FR", { weekday: "short" }).replace(".", "");
    }

    function longDateLabel(ms) {
      return new Date(ms).toLocaleDateString("fr-FR", { weekday: "long", day: "numeric", month: "short" });
    }

    function addHistory(text) {
      const time = new Date().toLocaleTimeString("fr-FR", { hour: "2-digit", minute: "2-digit" });
      state.history.unshift(`${time} — ${text}`);
      state.history = state.history.slice(0, 8);
    }

    function setPage(page) {
      state.activePage = page;
      saveState();
      render();
    }

    function startWork() {
      if (state.mode !== "idle") return;
      state.mode = "work";
      state.workStart = now();
      addHistory("Travail démarré");
      saveState();
      render();
    }

    function stopWork() {
      if (state.mode !== "work") return;

      const end = now();
      const workedSeconds = secondsBetween(state.workStart, end);
      const earnedBreakSeconds = Math.floor(workedSeconds / state.ratio);

      state.breakBankSeconds += earnedBreakSeconds;
      state.workSessions.unshift({
        start: state.workStart,
        end,
        seconds: workedSeconds,
        ratio: state.ratio,
        earnedBreakSeconds
      });
      state.workSessions = state.workSessions.slice(0, 300);

      state.mode = "idle";
      state.workStart = null;

      addHistory(`Travail ${formatClock(workedSeconds)} → +${formatMinutes(earnedBreakSeconds)} de pause`);
      saveState();
      render();
    }

    function startBreak() {
      if (state.mode !== "idle") return;

      const requestedMinutes = Number(el.breakMinutes.value);
      if (!requestedMinutes || requestedMinutes <= 0) {
        alert("Choisis une durée de pause en minutes.");
        return;
      }

      const requestedSeconds = Math.floor(requestedMinutes * 60);
      if (requestedSeconds > state.breakBankSeconds) {
        alert("Tu n'as pas assez de pause disponible.");
        return;
      }

      state.mode = "break";
      state.breakStart = now();
      state.plannedBreakSeconds = requestedSeconds;
      addHistory(`Pause démarrée pour ${requestedMinutes} min`);
      saveState();
      render();
    }

    function stopBreak() {
      if (state.mode !== "break") return;

      const usedSeconds = Math.min(secondsBetween(state.breakStart), state.plannedBreakSeconds);
      state.breakBankSeconds = Math.max(0, state.breakBankSeconds - usedSeconds);
      state.mode = "idle";
      state.breakStart = null;
      state.plannedBreakSeconds = 0;

      addHistory(`Pause utilisée : ${formatMinutes(usedSeconds)}`);
      saveState();
      render();
    }

    function updateRatio() {
      if (state.mode !== "idle") {
        alert("Change le ratio quand aucun chrono n'est en cours.");
        el.ratio.value = state.ratio;
        return;
      }
      state.ratio = Number(el.ratio.value);
      addHistory(`Ratio réglé sur ${state.ratio}:1`);
      saveState();
      render();
    }

    async function enableNotifications() {
      if (!("Notification" in window)) {
        alert("Les notifications ne sont pas disponibles dans ce navigateur.");
        return;
      }

      const permission = await Notification.requestPermission();
      if (permission === "granted") {
        notify("Notifications activées", "Je te préviendrai à la fin de tes pauses.");
      } else {
        alert("Notifications refusées. Tu peux les réactiver dans les réglages de Safari/iPadOS.");
      }
    }

    function notify(title, body) {
      if (("Notification" in window) && Notification.permission === "granted") {
        new Notification(title, { body });
      } else {
        alert(`${title}\n\n${body}`);
      }
    }

    function resetBank() {
      if (!confirm("Réinitialiser toute la banque de pause ?")) return;
      state.breakBankSeconds = 0;
      state.mode = "idle";
      state.workStart = null;
      state.breakStart = null;
      state.plannedBreakSeconds = 0;
      addHistory("Banque réinitialisée");
      saveState();
      render();
    }

    function getLastSevenDays() {
      const days = [];
      const today = new Date();
      today.setHours(0, 0, 0, 0);
      for (let i = 6; i >= 0; i--) {
        const d = new Date(today);
        d.setDate(today.getDate() - i);
        days.push({ ms: d.getTime(), key: dateKey(d.getTime()) });
      }
      return days;
    }

    function focusSecondsForDate(key) {
      return state.workSessions
        .filter(session => dateKey(session.end) === key)
        .reduce((sum, session) => sum + session.seconds, 0);
    }

    function renderHistoryPage() {
      const days = getLastSevenDays();
      const data = days.map(day => ({ ...day, seconds: focusSecondsForDate(day.key) }));
      const maxSeconds = Math.max(1, ...data.map(d => d.seconds));
      const total = data.reduce((sum, day) => sum + day.seconds, 0);

      el.weekTotal.textContent = formatHoursMinutes(total);
      el.weekChart.innerHTML = data.map(day => {
        const height = Math.max(2, Math.round((day.seconds / maxSeconds) * 100));
        return `
          <div class="bar-wrap">
            <div class="bar-time">${formatHoursMinutes(day.seconds)}</div>
            <div class="bar" style="height:${height}%"></div>
            <div class="bar-label">${shortDayLabel(day.ms)}</div>
          </div>
        `;
      }).join("");

      const lastSessions = state.workSessions.slice(0, 12);
      el.sessionsList.innerHTML = lastSessions.length
        ? lastSessions.map(session => `
            <div>
              <span>${longDateLabel(session.end)}</span>
              <strong>${formatHoursMinutes(session.seconds)}</strong>
            </div>
          `).join("")
        : `<div>Aucune session terminée pour l’instant.</div>`;
    }

    function render() {
      const showHistory = state.activePage === "history";
      el.tabDashboard.classList.toggle("active", !showHistory);
      el.tabHistory.classList.toggle("active", showHistory);
      el.dashboardPage.classList.toggle("active", !showHistory);
      el.historyPage.classList.toggle("active", showHistory);

      el.ratio.value = state.ratio;
      el.ratioValue.textContent = `${state.ratio}:1`;
      el.bankValue.textContent = formatMinutes(state.breakBankSeconds);
      el.todayFocusValue.textContent = formatMinutes(focusSecondsForDate(dateKey(now())));

      el.statusDot.className = "dot";

      if (state.mode === "work") {
        const elapsed = secondsBetween(state.workStart);
        el.timer.textContent = formatClock(elapsed);
        el.statusText.textContent = "Travail en cours";
        el.statusDot.classList.add("work");
      } else if (state.mode === "break") {
        const elapsed = secondsBetween(state.breakStart);
        const remaining = state.plannedBreakSeconds - elapsed;
        el.timer.textContent = formatClock(remaining);
        el.statusText.textContent = "Pause en cours";
        el.statusDot.classList.add("break");

        if (remaining <= 0) {
          stopBreak();
          notify("Pause terminée", "C’est le moment de reprendre le travail.");
          return;
        }
      } else {
        el.timer.textContent = "00:00";
        el.statusText.textContent = "Inactif";
      }

      el.startWork.disabled = state.mode !== "idle";
      el.stopWork.disabled = state.mode !== "work";
      el.startBreak.disabled = state.mode !== "idle" || state.breakBankSeconds <= 0;
      el.stopBreak.disabled = state.mode !== "break";
      el.ratio.disabled = state.mode !== "idle";

      el.history.innerHTML = state.history.map(item => `<div>${item}</div>`).join("");
      renderHistoryPage();
    }

    el.tabDashboard.addEventListener("click", () => setPage("dashboard"));
    el.tabHistory.addEventListener("click", () => setPage("history"));
    el.startWork.addEventListener("click", startWork);
    el.stopWork.addEventListener("click", stopWork);
    el.startBreak.addEventListener("click", startBreak);
    el.stopBreak.addEventListener("click", stopBreak);
    el.ratio.addEventListener("change", updateRatio);
    el.enableNotifications.addEventListener("click", enableNotifications);
    el.reset.addEventListener("click", resetBank);

    setInterval(render, 1000);
    render();
  </script>
</body>
</html>
