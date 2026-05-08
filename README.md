<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0, viewport-fit=cover" />
  <meta name="apple-mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
  <meta name="theme-color" content="#020617" />
  <title>Flowmodoro Bank</title>

  <style>
    :root {
      font-family: -apple-system, BlinkMacSystemFont, system-ui, sans-serif;
      background: #020617;
      color: #ffffff;
    }

    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      min-height: 100vh;
      padding: 16px;
      color: #ffffff;
      background: radial-gradient(circle at top left, #1e293b, #020617 70%);
    }

    .app {
      width: min(1320px, 100%);
      min-height: calc(100vh - 32px);
      margin: 0 auto;
      padding: 22px;
      border-radius: 30px;
      background: rgba(15, 23, 42, 0.96);
      border: 1px solid rgba(226, 232, 240, 0.22);
      box-shadow: 0 24px 90px rgba(0, 0, 0, 0.55);
      display: grid;
      grid-template-rows: auto 1fr;
      gap: 18px;
    }

    header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 20px;
    }

    h1 {
      margin: 0;
      font-size: 34px;
      line-height: 1;
      letter-spacing: -0.05em;
      color: #ffffff;
    }

    .subtitle {
      margin: 10px 0 0;
      color: #e2e8f0;
      line-height: 1.35;
      font-size: 17px;
    }

    .tabs {
      display: flex;
      gap: 8px;
      padding: 6px;
      border-radius: 999px;
      background: rgba(2, 6, 23, 0.72);
      border: 1px solid rgba(226, 232, 240, 0.18);
      flex-shrink: 0;
    }

    .tab {
      border: 0;
      border-radius: 999px;
      padding: 13px 24px;
      color: #ffffff;
      background: transparent;
      font-size: 17px;
      font-weight: 800;
      cursor: pointer;
    }

    .tab.active {
      background: #ffffff;
      color: #020617;
    }

    .page {
      display: none;
      height: 100%;
    }

    .page.active {
      display: block;
    }

    .dashboard {
      height: 100%;
      display: grid;
      grid-template-columns: 1.7fr 1fr;
      gap: 18px;
    }

    .panel {
      border-radius: 28px;
      background: rgba(30, 41, 59, 0.72);
      border: 1px solid rgba(226, 232, 240, 0.18);
      padding: 22px;
    }

    .main-panel {
      min-height: 430px;
      display: grid;
      grid-template-rows: auto 1fr auto;
      gap: 12px;
    }

    .status {
      display: inline-flex;
      gap: 8px;
      align-items: center;
      width: fit-content;
      padding: 8px 13px;
      border-radius: 999px;
      background: rgba(226, 232, 240, 0.16);
      color: #ffffff;
      font-size: 15px;
      font-weight: 700;
    }

    .dot {
      width: 9px;
      height: 9px;
      border-radius: 50%;
      background: #cbd5e1;
    }

    .dot.work {
      background: #22c55e;
    }

    .dot.break {
      background: #38bdf8;
    }

    .timer {
      align-self: center;
      text-align: center;
      font-size: clamp(108px, 18vw, 210px);
      font-weight: 900;
      letter-spacing: -0.09em;
      font-variant-numeric: tabular-nums;
      color: #ffffff;
      line-height: 0.95;
      margin: 0;
      text-shadow: 0 8px 40px rgba(255, 255, 255, 0.08);
    }

    .controls {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 12px;
    }

    button,
    input,
    select {
      font: inherit;
    }

    button {
      border: 0;
      border-radius: 18px;
      padding: 16px 14px;
      color: #ffffff;
      font-size: 16px;
      font-weight: 850;
      background: #334155;
      cursor: pointer;
    }

    button:active {
      transform: scale(0.98);
    }

    button:disabled {
      opacity: 0.42;
      cursor: not-allowed;
    }

    .primary {
      background: #16a34a;
    }

    .danger {
      background: #dc2626;
    }

    .blue {
      background: #0284c7;
    }

    .muted {
      background: #475569;
    }

    .wide {
      grid-column: 1 / -1;
    }

    .side-panel {
      display: grid;
      grid-template-rows: auto auto auto 1fr;
      gap: 14px;
      min-height: 430px;
    }

    .cards {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 12px;
    }

    .card {
      padding: 18px;
      border-radius: 22px;
      background: rgba(15, 23, 42, 0.78);
      border: 1px solid rgba(226, 232, 240, 0.16);
      min-height: 118px;
    }

    .label {
      color: #ffffff;
      font-size: 14px;
      font-weight: 750;
      margin-bottom: 8px;
    }

    .value {
      font-size: 34px;
      font-weight: 900;
      letter-spacing: -0.05em;
      color: #ffffff;
      line-height: 1;
    }

    .settings {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 12px;
    }

    label {
      display: block;
      margin-bottom: 8px;
      color: #ffffff;
      font-size: 14px;
      font-weight: 750;
    }

    input,
    select {
      width: 100%;
      border: 1px solid rgba(226, 232, 240, 0.26);
      border-radius: 16px;
      padding: 14px;
      background: rgba(2, 6, 23, 0.76);
      color: #ffffff;
      outline: none;
      font-size: 16px;
    }

    input::placeholder {
      color: #e2e8f0;
      opacity: 0.75;
    }

    .hint {
      margin: 0;
      color: #e2e8f0;
      font-size: 14px;
      line-height: 1.45;
    }

    .mini-history {
      overflow: auto;
      font-size: 13px;
      color: #ffffff;
      min-height: 80px;
      max-height: 130px;
    }

    .mini-history div {
      padding: 8px 0;
      border-bottom: 1px solid rgba(226, 232, 240, 0.14);
    }

    .history-page {
      height: 100%;
      display: grid;
      grid-template-columns: 0.7fr 1.3fr;
      gap: 18px;
    }

    .summary-number {
      font-size: 68px;
      font-weight: 900;
      letter-spacing: -0.07em;
      margin: 10px 0 8px;
      color: #ffffff;
      line-height: 1;
    }

    .week-chart {
      display: grid;
      grid-template-columns: repeat(7, 1fr);
      gap: 12px;
      height: 360px;
      align-items: end;
      padding-top: 20px;
    }

    .bar-wrap {
      height: 100%;
      display: flex;
      flex-direction: column;
      justify-content: end;
      gap: 9px;
      text-align: center;
    }

    .bar {
      min-height: 8px;
      border-radius: 18px 18px 8px 8px;
      background: linear-gradient(180deg, #38bdf8, #0284c7);
      border: 1px solid rgba(255, 255, 255, 0.22);
    }

    .bar-label {
      color: #ffffff;
      font-weight: 850;
      font-size: 14px;
    }

    .bar-time {
      color: #ffffff;
      font-size: 13px;
      font-weight: 750;
      font-variant-numeric: tabular-nums;
    }

    .sessions-list {
      margin-top: 18px;
      max-height: 240px;
      overflow: auto;
      color: #ffffff;
      font-size: 14px;
    }

    .sessions-list div {
      display: flex;
      justify-content: space-between;
      gap: 14px;
      padding: 10px 0;
      border-bottom: 1px solid rgba(226, 232, 240, 0.14);
    }

    .sessions-list strong {
      color: #ffffff;
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
        background: rgba(2, 6, 23, 0.96);
        color: #ffffff;
        font-size: 24px;
        font-weight: 850;
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

        <aside class="panel side-panel">
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
    const STORAGE_KEY = "flowmodoro-state-v3";

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

    function now() {
      return Date.now();
    }

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
      return new Date(ms).toLocaleDateString("fr-FR", {
        weekday: "long",
        day: "numeric",
        month: "short"
      });
    }

    function addHistory(text) {
      const time = new Date().toLocaleTimeString("fr-FR", {
        hour: "2-digit",
        minute: "2-digit"
      });
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
          alert("Pause terminée.");
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
    el.reset.addEventListener("click", resetBank);

    setInterval(render, 1000);
    render();
  </script>
</body>
</html>
