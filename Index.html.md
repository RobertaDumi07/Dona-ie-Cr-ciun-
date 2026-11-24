<!DOCTYPE html>  
<html lang="ro">  
<head>  
  <meta charset="UTF-8" />  
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />  
  <title>Poveste de Crăciun — O Mică Dorință din Suflet</title>  
  <style>  
    :root {  
      --pine-dark: #0d2b1d;  
      --pine: #184d32;  
      --red: #b91c1c;  
      --red-bright: #e12d2d;  
      --gold: #f5c542;  
      --gold-dark: #c49216;  
      --snow: #fafafc;  
      --parchment: #fff8e7;  
      --ink: #3e2723;  
    }  
  
    * {  
      box-sizing: border-box;  
      margin: 0;  
      padding: 0;  
    }  
  
    body {  
      min-height: 100vh;  
      font-family: "Segoe UI", Roboto, Helvetica, Arial, sans-serif;  
      background: linear-gradient(180deg, var(--pine-dark) 0%, var(--pine) 100%);  
      color: var(--snow);  
      overflow-x: hidden;  
      position: relative;  
    }  
  
    #snow-canvas {  
      position: fixed;  
      inset: 0;  
      width: 100%;  
      height: 100%;  
      pointer-events: none;  
      z-index: 0;  
    }  
  
    .lights-bar {  
      position: relative;  
      z-index: 2;  
      display: flex;  
      justify-content: space-around;  
      align-items: center;  
      padding: 10px 18px;  
      background: rgba(8, 24, 16, 0.55);  
      border-bottom: 1px solid rgba(245, 197, 66, 0.25);  
    }  
  
    .bulb {  
      width: 13px;  
      height: 17px;  
      border-radius: 50%;  
      animation: glow 1.6s infinite alternate;  
    }  
  
    .bulb:nth-child(4n+1) { background: #ff4d4d; box-shadow: 0 0 12px #ff4d4d; animation-delay: 0s; }  
    .bulb:nth-child(4n+2) { background: var(--gold); box-shadow: 0 0 12px var(--gold); animation-delay: 0.35s; }  
    .bulb:nth-child(4n+3) { background: #48db70; box-shadow: 0 0 12px #48db70; animation-delay: 0.7s; }  
    .bulb:nth-child(4n+4) { background: #5abeff; box-shadow: 0 0 12px #5abeff; animation-delay: 1.05s; }  
  
    @keyframes glow {  
      from { opacity: 0.45; transform: scale(0.92); }  
      to { opacity: 1; transform: scale(1.08); }  
    }  
  
    .app-wrapper {  
      position: relative;  
      z-index: 1;  
      max-width: 900px;  
      margin: 22px auto 40px;  
      padding: 0 16px;  
    }  
  
    .card {  
      background: rgba(11, 36, 24, 0.88);  
      border: 2px solid var(--gold);  
      border-radius: 24px;  
      padding: 28px 26px;  
      box-shadow: 0 18px 40px rgba(0, 0, 0, 0.45);  
      backdrop-filter: blur(6px);  
    }  
  
    .screen {  
      display: none;  
    }  
  
    .screen.active {  
      display: block;  
      animation: fadeIn 0.35s ease;  
    }  
  
    @keyframes fadeIn {  
      from { opacity: 0; transform: translateY(8px); }  
      to { opacity: 1; transform: translateY(0); }  
    }  
  
    h1, h2 {  
      font-family: Georgia, "Times New Roman", serif;  
      color: var(--gold);  
      text-align: center;  
      margin-bottom: 12px;  
    }  
  
    h1 { font-size: clamp(1.6rem, 4vw, 2.25rem); }  
    h2 { font-size: clamp(1.35rem, 3.2vw, 1.85rem); }  
  
    .subtitle {  
      text-align: center;  
      line-height: 1.55;  
      color: var(--snow);  
      margin-bottom: 20px;  
      font-size: 1.02rem;  
    }  
  
    .input-group {  
      max-width: 360px;  
      margin: 0 auto 20px;  
      text-align: center;  
    }  
  
    .input-group label {  
      display: block;  
      color: var(--gold);  
      font-weight: 600;  
      margin-bottom: 8px;  
    }  
  
    input[type="text"] {  
      width: 100%;  
      padding: 12px 14px;  
      border-radius: 14px;  
      border: 2px solid var(--gold);  
      background: #fffbeb;  
      color: #14281e;  
      font-size: 1rem;  
      text-align: center;  
      outline: none;  
    }  
  
    .btn-row {  
      display: flex;  
      flex-wrap: wrap;  
      gap: 12px;  
      justify-content: center;  
      margin-top: 14px;  
    }  
  
    button {  
      border: 1.5px solid var(--gold);  
      border-radius: 16px;  
      padding: 11px 20px;  
      font-size: 0.98rem;  
      font-weight: 700;  
      cursor: pointer;  
      color: var(--snow);  
      transition: transform 0.14s ease, filter 0.14s ease;  
    }  
  
    button:hover:not(:disabled) {  
      transform: translateY(-2px);  
      filter: brightness(1.08);  
    }  
  
    button:disabled {  
      opacity: 0.45;  
      cursor: not-allowed;  
    }  
  
    .btn-red { background: var(--red-bright); }  
    .btn-gold { background: var(--gold-dark); }  
    .btn-green { background: #166534; }  
    .btn-muted { background: #4b5563; }  
  
    /* Joc 1: Prinde cadourile */  
    .game-hud {  
      display: flex;  
      justify-content: space-between;  
      align-items: center;  
      flex-wrap: wrap;  
      gap: 8px;  
      margin-bottom: 10px;  
      font-weight: 700;  
      color: var(--gold);  
    }  
  
    #catch-area {  
      position: relative;  
      width: 100%;  
      height: 360px;  
      background: rgba(8, 25, 17, 0.8);  
      border: 2px solid var(--gold);  
      border-radius: 18px;  
      overflow: hidden;  
      touch-action: none;  
    }  
  
    .sled {  
      position: absolute;  
      bottom: 14px;  
      width: 106px;  
      height: 30px;  
      background: var(--red-bright);  
      border: 2px solid var(--gold);  
      border-radius: 14px;  
      display: flex;  
      align-items: center;  
      justify-content: center;  
      font-size: 0.82rem;  
      font-weight: 700;  
      color: var(--snow);  
      user-select: none;  
    }  
  
    .falling-item {  
      position: absolute;  
      font-size: 1.85rem;  
      user-select: none;  
      line-height: 1;  
    }  
  
    /* Joc 2: Memory */  
    .memory-grid {  
      display: grid;  
      grid-template-columns: repeat(4, 1fr);  
      gap: 12px;  
      max-width: 520px;  
      margin: 14px auto;  
    }  
  
    .memory-card {  
      aspect-ratio: 1 / 1;  
      font-size: 2rem;  
      background: var(--red);  
      border: 2px solid var(--gold);  
      border-radius: 16px;  
      display: flex;  
      align-items: center;  
      justify-content: center;  
      padding: 0;  
    }  
  
    .memory-card.revealed {  
      background: var(--snow);  
      color: var(--pine-dark);  
    }  
  
    .memory-card.matched {  
      background: #dcfce7;  
      color: var(--pine-dark);  
    }  
  
    /* Joc 3: Ghicitoare */  
    .riddle-box {  
      background: rgba(255, 255, 255, 0.06);  
      border-left: 4px solid var(--gold);  
      border-radius: 12px;  
      padding: 18px;  
      margin: 16px auto;  
      max-width: 600px;  
      font-family: Georgia, serif;  
      font-style: italic;  
      font-size: 1.12rem;  
      line-height: 1.6;  
      text-align: center;  
    }  
  
    .feedback {  
      text-align: center;  
      min-height: 24px;  
      margin-top: 12px;  
      font-weight: 700;  
      color: #fde047;  
    }  
  
    /* Scrisoare & Donații */  
    .letter-box {  
      display: none;  
      background: var(--parchment);  
      color: var(--ink);  
      border: 3px solid var(--gold-dark);  
      border-radius: 18px;  
      padding: 20px 22px;  
      margin: 14px auto;  
      max-width: 740px;  
      font-family: Georgia, serif;  
      line-height: 1.55;  
      font-size: 0.98rem;  
      box-shadow: 0 10px 24px rgba(0, 0, 0, 0.35);  
    }  
  
    .letter-box.open {  
      display: block;  
      animation: fadeIn 0.3s ease;  
    }  
  
    .letter-box h3 {  
      color: #991b1b;  
      margin-bottom: 10px;  
      font-size: 1.15rem;  
    }  
  
    .donation-panel {  
      display: none;  
      background: rgba(24, 77, 50, 0.75);  
      border: 1.5px solid var(--gold);  
      border-radius: 18px;  
      padding: 16px;  
      margin: 14px auto 0;  
      max-width: 740px;  
      text-align: center;  
    }  
  
    .donation-panel.visible {  
      display: block;  
      animation: fadeIn 0.3s ease;  
    }  
  
    .iban-row {  
      display: flex;  
      flex-wrap: wrap;  
      gap: 10px;  
      justify-content: center;  
      align-items: center;  
      margin-bottom: 12px;  
    }  
  
    .iban-code {  
      background: #fffbeb;  
      color: #14281e;  
      font-family: Consolas, monospace;  
      font-weight: 700;  
      padding: 9px 14px;  
      border-radius: 12px;  
      border: 2px solid var(--gold);  
      font-size: 0.98rem;  
      letter-spacing: 0.5px;  
    }  
  
    .table-section {  
      margin-top: 22px;  
    }  
  
    .table-wrap {  
      overflow-x: auto;  
      border-radius: 14px;  
      border: 2px solid var(--gold);  
      margin-top: 10px;  
    }  
  
    table {  
      width: 100%;  
      border-collapse: collapse;  
      background: #fffdf5;  
      color: #19231e;  
      font-size: 0.92rem;  
    }  
  
    th {  
      background: var(--gold-dark);  
      color: var(--snow);  
      padding: 10px 12px;  
      text-align: left;  
    }  
  
    td {  
      padding: 9px 12px;  
      border-top: 1px solid #e5e7eb;  
    }  
  </style>  
</head>  
<body>  
  <canvas id="snow-canvas"></canvas>  
  
  <div class="lights-bar" aria-hidden="true">  
    <span class="bulb"></span><span class="bulb"></span><span class="bulb"></span><span class="bulb"></span>  
    <span class="bulb"></span><span class="bulb"></span><span class="bulb"></span><span class="bulb"></span>  
    <span class="bulb"></span><span class="bulb"></span><span class="bulb"></span><span class="bulb"></span>  
  </div>  
  
  <main class="app-wrapper">  
    <!-- ECRAN 0: BUN VENIT + NUME -->  
    <section id="screen-welcome" class="card screen active">  
      <div style="text-align:center; font-size:2.8rem; margin-bottom:8px;">🎄✨🎁</div>  
      <h1>Magia Crăciunului Te Așteaptă!</h1>  
      <p class="subtitle">  
        Spiridușii au pregătit <b>3 mici provocări de iarnă</b> pentru tine.<br />  
        Scrie-ți numele la început ca să știu cine a deschis link-ul!  
      </p>  
      <div class="input-group">  
        <label for="player-name-input">Numele tău:</label>  
        <input id="player-name-input" type="text" placeholder="Ex: Maria, Andrei, Alex..." maxlength="50" />  
      </div>  
      <div class="btn-row">  
        <button class="btn-red" id="btn-start-adventure">✨ Începe Aventura de Crăciun ✨</button>  
      </div>  
    </section>  
  
    <!-- JOCUL 1: PRINDE CADOURILE -->  
    <section id="screen-game1" class="card screen">  
      <h2>Proba 1/3: Prinde Cadourile Spiridușilor!</h2>  
      <div class="game-hud">  
        <span id="g1-player">Jucător: -</span>  
        <span id="g1-score">Cadouri: 0 / 8</span>  
        <span>Evită cărbunii 🪨!</span>  
      </div>  
      <div id="catch-area">  
        <div id="sled" class="sled">🛷 SANIA TA</div>  
      </div>  
      <div class="feedback" id="g1-feedback">Mișcă mouse-ul, degetul sau săgețile ◀ ▶ pentru a prinde 8 cadouri!</div>  
      <div class="btn-row">  
        <button class="btn-gold" id="btn-to-game2" style="display:none;">🎉 Bravo! Mergi la Proba 2 ➔</button>  
      </div>  
    </section>  
  
    <!-- JOCUL 2: MEMORY -->  
    <section id="screen-game2" class="card screen">  
      <h2>Proba 2/3: Memory-ul Spiridușilor</h2>  
      <p class="subtitle" id="g2-status">Găsește toate cele 8 perechi de simboluri de Crăciun!</p>  
      <div class="memory-grid" id="memory-grid"></div>  
      <div class="feedback" id="g2-feedback"></div>  
      <div class="btn-row">  
        <button class="btn-gold" id="btn-to-game3" style="display:none;">🌟 Excelent! Ultima Probă ➔</button>  
      </div>  
    </section>  
  
    <!-- JOCUL 3: GHICITOAREA -->  
    <section id="screen-game3" class="card screen">  
      <h2>Proba 3/3: Ghicitoarea de Iarnă a Spiridușului 🧝‍♂️</h2>  
      <div class="riddle-box">  
        „Nu costă nimic, dar valorează enorm.<br />  
        Încălzește sufletul chiar și în cea mai geroasă noapte de decembrie,<br />  
        iar când o dăruiești cuiva drag, se înmulțește.<br />  
        Ce este?”  
      </div>  
      <div class="btn-row">  
        <button class="btn-green riddle-opt" data-correct="0">🧣 Un fular gros</button>  
        <button class="btn-green riddle-opt" data-correct="1">❤️ Bunătatea și iubirea</button>  
        <button class="btn-green riddle-opt" data-correct="0">🔥 Un foc în sobă</button>  
      </div>  
      <div class="feedback" id="g3-feedback">Alege răspunsul corect pentru a ajunge la marea întrebare!</div>  
      <div class="btn-row">  
        <button class="btn-red" id="btn-to-final" style="display:none;">🎁 Felicitări! Mergi la Marea Întrebare ✨</button>  
      </div>  
    </section>  
  
    <!-- ECRAN FINAL: MAREA ÎNTREBARE + SCRISOARE + DONAȚII + TABEL -->  
    <section id="screen-final" class="card screen">  
      <p class="subtitle" style="color:#a7f3d0; font-weight:700; margin-bottom:6px;">  
        🎉 Felicitări! Ai trecut cu brio toate probele spiridușilor! 🎉  
      </p>  
      <h2>„Îmi donezi și mie cât te lasă sufletul?”</h2>  
  
      <div class="btn-row">  
        <button class="btn-red" id="btn-toggle-letter">✉️ Deschide scrisoarea</button>  
      </div>  
  
      <div id="letter-box" class="letter-box">  
        <h3>Dragul meu prieten / Dragă suflet bun,</h3>  
        <p>  
          Îți scriu aceste rânduri cu toată sinceritatea și emoția Crăciunului.  
          <b>Motivul pentru care te rog să mă ajuți cu o mică donație este că vreau să strâng bani ca să merg de Crăciun la Cernavodă.</b>  
          <b>Vreau să îi fac o surpriză lui Andrei fără ca el să știe</b>, să apar acolo și să îi aduc bucurie chiar de sărbători.  
          Sincer, <b>vreau să fiu și eu fericită de Crăciun</b>, iar cel mai frumos dar pentru mine ar fi să pot ajunge lângă el.  
          <b>Nu vreau niciun cadou</b> material anul acesta — tot ce îmi doresc este acest drum.  
          <b>Măcar 10 lei de la fiecare și sunt mulțumită</b> din toată inima!  
        </p>  
        <p style="margin-top:10px; color:#184d32; font-style:italic;">  
          Îți mulțumesc din suflet că ai citit și că faci parte din această surpriză de Crăciun! 🎄❤️  
        </p>  
      </div>  
  
      <div class="btn-row" style="margin-top:16px;">  
        <button class="btn-red" id="btn-want-donate" disabled>❤️ Da, vreau să donez!</button>  
        <button class="btn-muted" id="btn-no-donate">🙈 Nu donez acum</button>  
        <button class="btn-green" id="btn-think-more">🤔 Mă mai gândesc...</button>  
      </div>  
  
      <div class="feedback" id="final-status">  
        💡 Deschide și citește scrisoarea ca să poți alege cum donezi.  
      </div>  
  
      <div id="donation-panel" class="donation-panel">  
        <div class="iban-row">  
          <span style="color:var(--gold); font-weight:700;">🏦 IBAN:</span>  
          <span class="iban-code" id="iban-text">RO59BRDE240SV87933162400</span>  
          <button class="btn-gold" id="btn-copy-iban">📋 Copiază IBAN</button>  
          <button class="btn-red" id="btn-confirm-iban">💳 Donez prin IBAN</button>  
          <button class="btn-green" id="btn-give-cash">💵 Îți dau cash</button>  
        </div>  
      </div>  
  
      <div class="table-section">  
        <h3 style="color:var(--gold); text-align:center; font-size:1.1rem;">  
          📊 Cine a accesat link-ul și cum a răspuns:  
        </h3>  
        <div class="table-wrap">  
          <table>  
            <thead>  
              <tr>  
                <th>Nume</th>  
                <th>A accesat link-ul</th>  
                <th>Cât a donat / Status</th>  
                <th>Data</th>  
              </tr>  
            </thead>  
            <tbody id="records-tbody"></tbody>  
          </table>  
        </div>  
      </div>  
    </section>  
  </main>  
  
  <script>  
    const MY_IBAN = "RO59BRDE240SV87933162400";  
    const MY_EMAIL = "robertagiriada6@gmail.com";  
    const FORMSPREE_URL = "https://formspree.io/f/xkjrkzbl";  
    const STORAGE_KEY = "craciun_istoric_v1";  
  
    let currentPlayer = "Prieten anonim";  
    let records = loadRecords();  
  
    function loadRecords() {  
      try {  
        const raw = localStorage.getItem(STORAGE_KEY);  
        return raw ? JSON.parse(raw) : [];  
      } catch {  
        return [];  
      }  
    }  
  
    function saveRecords() {  
      try {  
        localStorage.setItem(STORAGE_KEY, JSON.stringify(records));  
      } catch {}  
    }  
  
    function formatNow() {  
      const d = new Date();  
      const pad = n => String(n).padStart(2, "0");  
      return `${pad(d.getDate())}.${pad(d.getMonth() + 1)}.${d.getFullYear()} ${pad(d.getHours())}:${pad(d.getMinutes())}`;  
    }  
  
    function renderTable() {  
      const tbody = document.getElementById("records-tbody");  
      tbody.innerHTML = "";  
      if (records.length === 0) {  
        tbody.innerHTML = `<tr><td colspan="4" style="text-align:center;">Încă nu există intrări salvate pe acest dispozitiv.</td></tr>`;  
        return;  
      }  
      records.forEach(r => {  
        const tr = document.createElement("tr");  
        tr.innerHTML = `  
          <td>${escapeHtml(r.name)}</td>  
          <td>${escapeHtml(r.accessed)}</td>  
          <td><b>${escapeHtml(r.status)}</b></td>  
          <td>${escapeHtml(r.date)}</td>  
        `;  
        tbody.appendChild(tr);  
      });  
    }  
  
    function escapeHtml(str) {  
      return String(str)  
        .replace(/&/g, "&amp;")  
        .replace(/</g, "&lt;")  
        .replace(/>/g, "&gt;")  
        .replace(/"/g, "&quot;");  
    }  
  
    async function sendToFormspree(statusLabel, details) {  
      try {  
        const formData = new URLSearchParams();  
        formData.append("nume", currentPlayer);  
        formData.append("a_accesat_link", "Da");  
        formData.append("status_donatie", statusLabel);  
        formData.append("detalii", details || "");  
        formData.append("iban", MY_IBAN);  
        formData.append("destinatar", MY_EMAIL);  
  
        await fetch(FORMSPREE_URL, {  
          method: "POST",  
          headers: {  
            "Content-Type": "application/x-www-form-urlencoded",  
            "Accept": "application/json"  
          },  
          body: formData.toString()  
        });  
      } catch {  
        // Ignoră erorile de rețea dacă utilizatorul este offline  
      }  
    }  
  
    function setCurrentStatus(statusLabel, details) {  
      if (records.length > 0) {  
        records[records.length - 1].status = statusLabel;  
      } else {  
        records.push({ name: currentPlayer, accessed: "Da", status: statusLabel, date: formatNow() });  
      }  
      saveRecords();  
      renderTable();  
      sendToFormspree(statusLabel, details);  
    }  
  
    function showScreen(id) {  
      document.querySelectorAll(".screen").forEach(s => s.classList.remove("active"));  
      document.getElementById(id).classList.add("active");  
    }  
  
    // Ninsoare pe fundal  
    (function initSnow() {  
      const canvas = document.getElementById("snow-canvas");  
      const ctx = canvas.getContext("2d");  
      let flakes = [];  
  
      function resize() {  
        canvas.width = window.innerWidth;  
        canvas.height = window.innerHeight;  
      }  
      window.addEventListener("resize", resize);  
      resize();  
  
      for (let i = 0; i < 85; i++) {  
        flakes.push({  
          x: Math.random() * canvas.width,  
          y: Math.random() * canvas.height,  
          r: 1.8 + Math.random() * 3.2,  
          vy: 0.7 + Math.random() * 1.6,  
          vx: -0.4 + Math.random() * 0.8  
        });  
      }  
  
      function tick() {  
        ctx.clearRect(0, 0, canvas.width, canvas.height);  
        ctx.fillStyle = "rgba(250, 250, 252, 0.82)";  
        flakes.forEach(f => {  
          f.y += f.vy;  
          f.x += f.vx;  
          if (f.y > canvas.height) { f.y = -8; f.x = Math.random() * canvas.width; }  
          if (f.x < 0) f.x = canvas.width;  
          if (f.x > canvas.width) f.x = 0;  
          ctx.beginPath();  
          ctx.arc(f.x, f.y, f.r, 0, Math.PI * 2);  
          ctx.fill();  
        });  
        requestAnimationFrame(tick);  
      }  
      tick();  
    })();  
  
    // Ecran 0: Start  
    document.getElementById("btn-start-adventure").addEventListener("click", () => {  
      const raw = document.getElementById("player-name-input").value.trim();  
      currentPlayer = raw || "Prieten anonim";  
      const nowStr = formatNow();  
      records.push({  
        name: currentPlayer,  
        accessed: "Da",  
        status: "Încă nu a răspuns (în joc)",  
        date: nowStr  
      });  
      saveRecords();  
      renderTable();  
      sendToFormspree("A accesat link-ul", "A început aventura la " + nowStr);  
      startGame1();  
      showScreen("screen-game1");  
    });  
  
    // Joc 1: Prinde cadourile  
    let g1Timer = null, g1Spawn = null, g1Score = 0, g1Active = false, sledX = 120;  
    const TARGET_SCORE = 8;  
  
    function startGame1() {  
      const area = document.getElementById("catch-area");  
      const sled = document.getElementById("sled");  
      area.querySelectorAll(".falling-item").forEach(el => el.remove());  
  
      g1Score = 0;  
      g1Active = true;  
      sledX = Math.max(10, (area.clientWidth - 106) / 2);  
      sled.style.left = sledX + "px";  
  
      document.getElementById("g1-player").textContent = "Jucător: " + currentPlayer;  
      document.getElementById("g1-score").textContent = `Cadouri: 0 / ${TARGET_SCORE}`;  
      document.getElementById("g1-feedback").textContent = "Prinde 8 cadouri/globuri/stele și evită cărbunii 🪨!";  
      document.getElementById("btn-to-game2").style.display = "none";  
  
      function moveSled(clientX) {  
        const rect = area.getBoundingClientRect();  
        const relX = clientX - rect.left - 53;  
        sledX = Math.max(6, Math.min(area.clientWidth - 112, relX));  
        sled.style.left = sledX + "px";  
      }  
  
      area.onmousemove = e => { if (g1Active) moveSled(e.clientX); };  
      area.ontouchmove = e => {  
        if (g1Active && e.touches.length > 0) {  
          moveSled(e.touches[0].clientX);  
        }  
      };  
  
      clearInterval(g1Spawn);  
      clearInterval(g1Timer);  
  
      g1Spawn = setInterval(() => {  
        if (!g1Active) return;  
        const item = document.createElement("div");  
        item.className = "falling-item";  
        const roll = Math.random();  
        let emoji = "🎁", pts = 1;  
        if (roll < 0.35) { emoji = "🎁"; pts = 1; }  
        else if (roll < 0.65) { emoji = "🔴"; pts = 1; }  
        else if (roll < 0.8) { emoji = "⭐"; pts = 2; }  
        else { emoji = "🪨"; pts = -1; }  
  
        item.textContent = emoji;  
        item.dataset.pts = pts;  
        item.dataset.y = -32;  
        item.style.left = (16 + Math.random() * Math.max(40, area.clientWidth - 56)) + "px";  
        item.style.top = "-32px";  
        area.appendChild(item);  
      }, 720);  
  
      g1Timer = setInterval(() => {  
        if (!g1Active) return;  
        const areaRect = area.getBoundingClientRect();  
        const sledRect = sled.getBoundingClientRect();  
  
        area.querySelectorAll(".falling-item").forEach(item => {  
          let y = parseFloat(item.dataset.y) + 3.4;  
          item.dataset.y = y;  
          item.style.top = y + "px";  
  
          const itemRect = item.getBoundingClientRect();  
          const hit =  
            itemRect.bottom >= sledRect.top &&  
            itemRect.top <= sledRect.bottom &&  
            itemRect.right >= sledRect.left &&  
            itemRect.left <= sledRect.right;  
  
          if (hit) {  
            const pts = parseInt(item.dataset.pts, 10);  
            g1Score = Math.max(0, g1Score + pts);  
            item.remove();  
            document.getElementById("g1-score").textContent = `Cadouri: ${Math.min(g1Score, TARGET_SCORE)} / ${TARGET_SCORE}`;  
  
            if (g1Score >= TARGET_SCORE) {  
              g1Active = false;  
              clearInterval(g1Spawn);  
              clearInterval(g1Timer);  
              document.getElementById("g1-feedback").textContent = "✨ Ai strâns toate cadourile! Treci la Proba 2! ✨";  
              document.getElementById("btn-to-game2").style.display = "inline-block";  
            }  
          } else if (y > areaRect.height + 20) {  
            item.remove();  
          }  
        });  
      }, 25);  
    }  
  
    document.getElementById("btn-to-game2").addEventListener("click", () => {  
      initMemoryGame();  
      showScreen("screen-game2");  
    });  
  
    // Joc 2: Memory  
    function initMemoryGame() {  
      const grid = document.getElementById("memory-grid");  
      grid.innerHTML = "";  
      document.getElementById("g2-feedback").textContent = "";  
      document.getElementById("btn-to-game3").style.display = "none";  
      document.getElementById("g2-status").textContent = "Perechi găsite: 0 / 8";  
  
      const symbols = ["🎄", "🎅", "⛄", "🦌", "🔔", "🕯️", "🍪", "🌟"];  
      const deck = [...symbols, ...symbols].sort(() => Math.random() - 0.5);  
  
      let first = null, second = null, lock = false, matchedPairs = 0;  
  
      deck.forEach(sym => {  
        const btn = document.createElement("button");  
        btn.className = "memory-card";  
        btn.textContent = "❄️";  
        btn.dataset.symbol = sym;  
  
        btn.addEventListener("click", () => {  
          if (lock || btn === first || btn.classList.contains("matched")) return;  
          btn.textContent = sym;  
          btn.classList.add("revealed");  
  
          if (!first) {  
            first = btn;  
          } else {  
            second = btn;  
            lock = true;  
  
            if (first.dataset.symbol === second.dataset.symbol) {  
              first.classList.add("matched");  
              second.classList.add("matched");  
              matchedPairs++;  
              document.getElementById("g2-status").textContent = `Perechi găsite: ${matchedPairs} / 8`;  
              first = null;  
              second = null;  
              lock = false;  
  
              if (matchedPairs === 8) {  
                document.getElementById("g2-feedback").textContent = "🎉 Ai găsit toate perechile de Crăciun!";  
                document.getElementById("btn-to-game3").style.display = "inline-block";  
              }  
            } else {  
              setTimeout(() => {  
                first.textContent = "❄️";  
                second.textContent = "❄️";  
                first.classList.remove("revealed");  
                second.classList.remove("revealed");  
                first = null;  
                second = null;  
                lock = false;  
              }, 650);  
            }  
          }  
        });  
  
        grid.appendChild(btn);  
      });  
    }  
  
    document.getElementById("btn-to-game3").addEventListener("click", () => {  
      showScreen("screen-game3");  
    });  
  
    // Joc 3: Ghicitoarea  
    document.querySelectorAll(".riddle-opt").forEach(btn => {  
      btn.addEventListener("click", () => {  
        const fb = document.getElementById("g3-feedback");  
        if (btn.dataset.correct === "1") {  
          fb.style.color = "#86efac";  
          fb.textContent = "✨ Corect! Ai trecut toate probele spiridușilor! ✨";  
          document.getElementById("btn-to-final").style.display = "inline-block";  
        } else {  
          fb.style.color = "#fdba74";  
          fb.textContent = "❄️ Mai încearcă! Ce încălzește sufletul fără să coste nimic?";  
        }  
      });  
    });  
  
    document.getElementById("btn-to-final").addEventListener("click", () => {  
      renderTable();  
      showScreen("screen-final");  
    });  
  
    // Ecran final: Scrisoare + Răspuns + IBAN / Cash  
    let letterRead = false, shyCount = 0;  
  
    document.getElementById("btn-toggle-letter").addEventListener("click", () => {  
      const box = document.getElementById("letter-box");  
      const btn = document.getElementById("btn-toggle-letter");  
      const opened = box.classList.toggle("open");  
      btn.textContent = opened ? "📭 Închide scrisoarea" : "✉️ Deschide scrisoarea";  
  
      if (!letterRead) {  
        letterRead = true;  
        document.getElementById("btn-want-donate").disabled = false;  
        const st = document.getElementById("final-status");  
        st.style.color = "#fde047";  
        st.textContent = "💌 Acum că ai citit scrisoarea, spune-mi: vrei să donezi?";  
      }  
    });  
  
    document.getElementById("btn-want-donate").addEventListener("click", () => {  
      document.getElementById("donation-panel").classList.add("visible");  
      const st = document.getElementById("final-status");  
      st.style.color = "#86efac";  
      st.textContent = "🎁 Mulțumesc din suflet! Ai mai jos IBAN-ul meu sau butonul «Îți dau cash»:";  
    });  
  
    document.getElementById("btn-copy-iban").addEventListener("click", async () => {  
      try {  
        await navigator.clipboard.writeText(MY_IBAN);  
      } catch {}  
      const st = document.getElementById("final-status");  
      st.style.color = "#86efac";  
      st.textContent = `✅ IBAN-ul ${MY_IBAN} a fost copiat! Apasă «Donez prin IBAN» ca să trecem în tabel.`;  
    });  
  
    document.getElementById("btn-confirm-iban").addEventListener("click", () => {  
      const amount = prompt("Cu ce sumă vrei să contribui prin IBAN (" + MY_IBAN + ")? (ex: 10 lei, 20 lei, 50 lei)", "10 lei");  
      if (amount !== null) {  
        const clean = amount.trim() ? `${amount.trim()} (IBAN)` : "Sumă prin IBAN (nespecificată)";  
        setCurrentStatus(clean, "Donație prin IBAN " + MY_IBAN);  
        const st = document.getElementById("final-status");  
        st.style.color = "#86efac";  
        st.textContent = `🥰 Mulțumesc, ${currentPlayer}! Am notat în tabel: ${clean}.`;  
      }  
    });  
  
    document.getElementById("btn-give-cash").addEventListener("click", () => {  
      const cash = prompt("Cu cât / cum îți dau cash? (opțional)", "10 lei cash");  
      const statusText = (cash && cash.trim()) ? `${cash.trim()} (Cash)` : "Îți dau cash (sumă de stabilit)";  
      setCurrentStatus(statusText, "A ales opțiunea: Îți dau cash");  
      const st = document.getElementById("final-status");  
      st.style.color = "#86efac";  
      st.textContent = `🥰 Mulțumesc, ${currentPlayer}! Am notat în tabel: ${statusText}.`;  
    });  
  
    document.getElementById("btn-no-donate").addEventListener("click", () => {  
      setCurrentStatus("Nu a donat", "A ales «Nu donez acum»");  
      const st = document.getElementById("final-status");  
      st.style.color = "#fde047";  
      st.textContent = `🎄 Îți mulțumesc oricum că ai jucat până la final, ${currentPlayer}!`;  
    });  
  
    document.getElementById("btn-think-more").addEventListener("click", () => {  
      shyCount++;  
      const msgs = [  
        "🎅 Nicio grabă! Scrisoarea rămâne aici dacă te răzgândești.",  
        "✨ Chiar și 10 lei contează enorm pentru surpriza lui Andrei de la Cernavodă!",  
        "❤️ Îți mulțumesc că ai citit cu atenție!"  
      ];  
      const st = document.getElementById("final-status");  
      st.style.color = "#fde047";  
      st.textContent = msgs[(shyCount - 1) % msgs.length];  
      setCurrentStatus("Încă se mai gândește", "A apăsat Mă mai gândesc");  
    });  
  
    renderTable();  
  </script>  
</body>  
</html>  
