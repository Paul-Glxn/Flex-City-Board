<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Dashboard Team Flex-City</title>
<!-- Minecraft Pixel-Font -->
<link href="https://fonts.googleapis.com/css2?family=Press+Start+2P&display=swap" rel="stylesheet" />
<style>
  /* Grunddesign im Minecraft-Stil */
  body {
    font-family: 'Press Start 2P', cursive;
    background: #3a5218 url('https://i.imgur.com/gkxjzNN.png') repeat;
    color: #e0e0d1;
    margin: 0;
    padding: 2rem 1rem;
    max-width: 900px;
    margin-left: auto;
    margin-right: auto;
    user-select: none;
  }

  /* Scrollbar Minecraft-style */
  ::-webkit-scrollbar {
    width: 8px;
  }
  ::-webkit-scrollbar-track {
    background: #556b2f;
    border-radius: 4px;
  }
  ::-webkit-scrollbar-thumb {
    background: #a2c523;
    border-radius: 4px;
    box-shadow: inset 0 0 5px #698b22;
  }

  h1, h2 {
    color: #80ff00;
    text-shadow: 0 0 10px #a2c523, 0 0 5px #4b690f;
    margin-bottom: 0.5rem;
    position: relative;
  }

  /* Minecraft icon before headers */
  h2::before {
    content: "⛏️ ";
    position: absolute;
    left: -2rem;
    top: 2px;
  }

  p, small {
    font-size: 0.7rem;
    margin-top: 0;
    margin-bottom: 1rem;
    color: #a9d147;
  }

  label {
    display: block;
    margin-top: 1rem;
    font-size: 0.6rem;
    color: #d4e157;
  }

  input, textarea {
    font-family: 'Press Start 2P', cursive;
    font-size: 0.55rem;
    background: #6b8e23;
    border: 2px solid #556b2f;
    border-radius: 4px;
    color: #d4e157;
    padding: 0.7rem;
    margin-top: 0.2rem;
    width: 100%;
    box-sizing: border-box;
    text-shadow: 1px 1px 0 #1b3100;
    transition: border-color 0.3s ease;
  }
  input:focus, textarea:focus {
    border-color: #a2c523;
    outline: none;
  }

  textarea {
    resize: vertical;
    min-height: 80px;
  }

  button {
    margin-top: 1.2rem;
    padding: 0.7rem 1.8rem;
    background: #a2c523;
    border: 3px solid #698b22;
    color: #233d00;
    font-weight: bold;
    cursor: pointer;
    text-shadow: 1px 1px 0 #e7f28e;
    transition: background-color 0.3s ease, box-shadow 0.3s ease;
    position: relative;
  }
  button:hover:not(:disabled) {
    background: #d8f28e;
    color: #2a4200;
    border-color: #4b690f;
    box-shadow: 0 0 10px #a2c523;
  }
  button:disabled {
    background: #76893e;
    border-color: #4b690f;
    color: #556b2f;
    cursor: not-allowed;
    box-shadow: none;
  }

  .info-box {
    background: #4a6a0f;
    padding: 1rem;
    border-radius: 6px;
    margin-top: 1rem;
    color: #c3df4a;
    white-space: pre-wrap;
    box-shadow: inset 0 0 10px #9fd34b;
    max-height: 180px;
    overflow-y: auto;
  }

  .info-item {
    border-bottom: 1px solid #698b22;
    margin-bottom: 0.8rem;
    padding-bottom: 0.5rem;
  }
  .info-item:last-child {
    border-bottom: none;
    margin-bottom: 0;
    padding-bottom: 0;
  }
  .info-title {
    font-weight: bold;
    font-size: 0.65rem;
    color: #bde04c;
    text-shadow: 0 0 6px #a2c523;
    margin-bottom: 0.2rem;
  }
  .info-author {
    font-size: 0.5rem;
    color: #8ca92d;
    margin-top: 0.3rem;
    font-style: italic;
  }

  .error {
    color: #ff6b6b;
    margin-top: 0.5rem;
    font-size: 0.55rem;
  }

  #abmeldungSuccess, #teamInfoSuccess {
    font-size: 0.6rem;
    margin-top: 0.5rem;
    color: #9fff5c;
    text-shadow: 0 0 6px #a2c523;
  }

  small {
    font-size: 0.5rem;
    color: #a5d081;
  }

  hr {
    border: 1px solid #5a8e00;
    margin: 2rem 0;
  }

  /* Loader Spinner */
  .loader {
    border: 3px solid #f3f3f3;
    border-top: 3px solid #a2c523;
    border-radius: 50%;
    width: 16px;
    height: 16px;
    animation: spin 1s linear infinite;
    display: inline-block;
    position: absolute;
    right: 12px;
    top: 50%;
    transform: translateY(-50%);
  }
  @keyframes spin {
    0% { transform: translateY(-50%) rotate(0deg);}
    100% { transform: translateY(-50%) rotate(360deg);}
  }

  /* Responsive */
  @media (max-width: 480px) {
    body {
      padding: 1rem 0.5rem;
    }
    input, textarea, button {
      font-size: 0.5rem;
    }
    h1 {
      font-size: 1.2rem;
    }
    h2 {
      font-size: 1rem;
    }
  }
</style>
</head>
<body>

<h1>Dashboard Team Flex-City</h1>
<p>Dies ist das offizielle Dashboard von Flex City</p>

<!-- Abmeldung-Team Forum -->
<section>
  <h2>Abmeldung-Team</h2>
  <form id="abmeldungForm" novalidate>
    <label for="wer">Wer: <span style="color:#ff4444;">*</span></label>
    <input type="text" id="wer" name="wer" required autocomplete="off" />

    <label for="wieLange">Wie lange: <span style="color:#ff4444;">*</span></label>
    <input type="text" id="wieLange" name="wieLange" placeholder="TT.MM.JJ-TT.MM.JJ" pattern="\d{2}\.\d{2}\.\d{2}-\d{2}\.\d{2}\.\d{2}" required autocomplete="off" />
    <small>Format: TT.MM.JJ-TT.MM.JJ</small>

    <label for="grund">Welcher Grund: <span style="color:#ff4444;">*</span> (mindestens 50 Wörter)</label>
    <textarea id="grund" name="grund" minlength="250" required placeholder="Bitte mindestens 50 Wörter eingeben..."></textarea>
    <small><span id="wortZaehler">0</span>/50 Wörter</small>

    <button type="submit">Abmelden</button>
    <p id="abmeldungError" class="error" aria-live="polite"></p>
    <p id="abmeldungSuccess" aria-live="polite"></p>
  </form>
</section>

<hr />

<!-- Team Information -->
<section>
  <h2>TEAM INFORMATION</h2>

  <div id="teamInfoBox" class="info-box" aria-live="polite" aria-label="Team Informationen">
    Keine Verfügbar
  </div>

  <form id="teamInfoForm" novalidate>
    <label for="ueberschrift">Überschrift: <span style="color:#ff4444;">*</span></label>
    <input type="text" id="ueberschrift" name="ueberschrift" autocomplete="off" required />

    <label for="haupttext">Haupttext: <span style="color:#ff4444;">*</span></label>
    <textarea id="haupttext" name="haupttext" required></textarea>

    <label for="geschriebenVon">Geschrieben von: <span style="color:#ff4444;">*</span></label>
    <input type="text" id="geschriebenVon" name="geschriebenVon" autocomplete="off" required />

    <button type="submit">Informationen absenden</button>
    <p id="teamInfoError" class="error" aria-live="polite"></p>
    <p id="teamInfoSuccess" aria-live="polite"></p>
  </form>
</section>

<script>
  const abmeldungWebhookUrl = "https://discord.com/api/webhooks/1397035955671798033/mcDxMU3kHKNl_9ev-afJ_xGI79vvkfwFIV502e0mB8omEOZ-_zxC6bRjs7RraC-QuLJW";
  const teamInfoWebhookUrl = "https://discord.com/api/webhooks/1397036110651330684/B0DmsHjO2cNtmD426cyLk49ymOXc_2PymjMJRSMpyw0-rwL1MjNVgXj-16uQeQDob3l3";

  // Word counter for Grund
  const grundField = document.getElementById('grund');
  const wortZaehler = document.getElementById('wortZaehler');

  function countWords(str) {
    return str.trim().split(/\s+/).filter(w => w.length > 0).length;
  }

  grundField.addEventListener('input', () => {
    const words = countWords(grundField.value);
    wortZaehler.textContent = words;
  });

  // Validate date range: TT.MM.JJ-TT.MM.JJ and logical check
  function validateDateRange(value) {
    const regex = /^(\d{2})\.(\d{2})\.(\d{2})-(\d{2})\.(\d{2})\.(\d{2})$/;
    const match = value.match(regex);
    if (!match) return false;
    const [_, sd, sm, sy, ed, em, ey] = match;
    // Parse dates (add 2000 for YY)
    const start = new Date(`20${sy}`, sm - 1, sd);
    const end = new Date(`20${ey}`, em - 1, ed);
    if (isNaN(start.getTime()) || isNaN(end.getTime())) return false;
    return start <= end;
  }

  // Show loader on button
  function toggleButtonLoader(button, show) {
    if (show) {
      button.disabled = true;
      if (!button.querySelector('.loader')) {
        const loader = document.createElement('span');
        loader.className = 'loader';
        button.appendChild(loader);
      }
    } else {
      button.disabled = false;
      const loader = button.querySelector('.loader');
      if (loader) loader.remove();
    }
  }

  // Abmeldung-Formular
  document.getElementById('abmeldungForm').addEventListener('submit', async function(e) {
    e.preventDefault();
    const wer = this.wer.value.trim();
    const wieLange = this.wieLange.value.trim();
    const grund = this.grund.value.trim();
    const errorEl = document.getElementById('abmeldungError');
    const successEl = document.getElementById('abmeldungSuccess');
    const submitBtn = this.querySelector('button[type="submit"]');
    errorEl.textContent = "";
    successEl.textContent = "";

    // Validierungen
    if (!wer) {
      errorEl.textContent = "Bitte 'Wer' angeben.";
      return;
    }
    if (!validateDateRange(wieLange)) {
      errorEl.textContent = "Bitte ein gültiges Datumsformat eingeben (TT.MM.JJ-TT.MM.JJ) und Zeitraum prüfen.";
      return;
    }
    if (countWords(grund) < 50) {
      errorEl.textContent = "Der Grund muss mindestens 50 Wörter enthalten.";
      return;
    }

    const message = `**Abmeldung-Team**\n**Wer:** ${wer}\n**Wie lange:** ${wieLange}\n**Welcher Grund:**\n${grund}`;

    toggleButtonLoader(submitBtn, true);
    try {
      const res = await fetch(abmeldungWebhookUrl, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ content: message }),
      });

      if(res.ok){
        successEl.textContent = "Abmeldung wurde erfolgreich gesendet!";
        this.reset();
        wortZaehler.textContent = "0";
      } else {
        const text = await res.text();
        errorEl.textContent = "Fehler beim Senden an Discord: " + text;
      }
    } catch (err) {
      errorEl.textContent = "Netzwerkfehler beim Senden.";
    } finally {
      toggleButtonLoader(submitBtn, false);
    }
  });

  // Team Infos aus localStorage laden und anzeigen
  const teamInfoBox = document.getElementById('teamInfoBox');

  function loadTeamInfos() {
    const stored = localStorage.getItem('teamInfos');
    if (!stored) {
      teamInfoBox.textContent = "Keine Verfügbar";
      return [];
    }
    try {
      const infos = JSON.parse(stored);
      renderTeamInfos(infos);
      return infos;
    } catch {
      teamInfoBox.textContent = "Keine Verfügbar";
      return [];
    }
  }

  function renderTeamInfos(infos) {
    if (!infos.length) {
      teamInfoBox.textContent = "Keine Verfügbar";
      return;
    }
    teamInfoBox.innerHTML = "";
    infos.slice(0, 3).forEach(info => {
      const div = document.createElement('div');
      div.className = 'info-item';

      const title = document.createElement('div');
      title.className = 'info-title';
      title.textContent = info.ueberschrift;

      const text = document.createElement('div');
      text.style.whiteSpace = 'pre-wrap';
      text.textContent = info.haupttext;

      const author = document.createElement('div');
      author.className = 'info-author';
      author.textContent = `Geschrieben von: ${info.geschriebenVon}`;

      div.appendChild(title);
      div.appendChild(text);
      div.appendChild(author);

      teamInfoBox.appendChild(div);
    });
  }

  // Team Info Formular
  document.getElementById('teamInfoForm').addEventListener('submit', async function(e) {
    e.preventDefault();
    const ueberschrift = this.ueberschrift.value.trim();
    const haupttext = this.haupttext.value.trim();
    const geschriebenVon = this.geschriebenVon.value.trim();
    const errorEl = document.getElementById('teamInfoError');
    const successEl = document.getElementById('teamInfoSuccess');
    const submitBtn = this.querySelector('button[type="submit"]');
    errorEl.textContent = "";
    successEl.textContent = "";

    if(!ueberschrift || !haupttext || !geschriebenVon) {
      errorEl.textContent = "Bitte alle Pflichtfelder ausfüllen.";
      return;
    }

    const message = `**TEAM INFORMATION**\n**Überschrift:** ${ueberschrift}\n**Haupttext:**\n${haupttext}\n**Geschrieben von:** ${geschriebenVon}`;

    toggleButtonLoader(submitBtn, true);
    try {
      const res = await fetch(teamInfoWebhookUrl, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ content: message }),
      });

      if(res.ok){
        successEl.textContent = "Team Information wurde erfolgreich gesendet!";
        // Lokale Speicherung der Infos (max 10 speichern)
        const currentInfos = loadTeamInfos();
        currentInfos.unshift({ ueberschrift, haupttext, geschriebenVon });
        if (currentInfos.length > 10) currentInfos.pop();
        localStorage.setItem('teamInfos', JSON.stringify(currentInfos));
        renderTeamInfos(currentInfos);
        this.reset();
      } else {
        const text = await res.text();
        errorEl.textContent = "Fehler beim Senden an Discord: " + text;
      }
    } catch (err) {
      errorEl.textContent = "Netzwerkfehler beim Senden.";
    } finally {
      toggleButtonLoader(submitBtn, false);
    }
  });

  // Initial Laden der Team Infos
  loadTeamInfos();
</script>

</body>
</html>
