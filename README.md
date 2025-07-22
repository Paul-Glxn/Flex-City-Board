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
    background: #3a5218 url('https://i.imgur.com/gkxjzNN.png') repeat; /* Pixel-Kachel (Grasblock) als BG */
    color: #e0e0d1;
    margin: 0;
    padding: 2rem;
    max-width: 800px;
    margin-left: auto;
    margin-right: auto;
    user-select: none;
  }

  h1, h2 {
    color: #80ff00; /* leuchtendes Grasgrün */
    text-shadow: 1px 1px 0 #0b3d00;
    margin-bottom: 0.5rem;
  }

  p {
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
    background: #6b8e23; /* Olivgrün */
    border: 2px solid #556b2f; /* Dunkelgrün */
    border-radius: 4px;
    color: #d4e157;
    padding: 0.7rem;
    margin-top: 0.2rem;
    width: 100%;
    box-sizing: border-box;
    text-shadow: 1px 1px 0 #1b3100;
  }

  textarea {
    resize: vertical;
    min-height: 80px;
  }

  button {
    margin-top: 1.2rem;
    padding: 0.7rem 1.5rem;
    background: #a2c523;
    border: 3px solid #698b22;
    color: #233d00;
    font-weight: bold;
    cursor: pointer;
    text-shadow: 1px 1px 0 #e7f28e;
    transition: background-color 0.3s ease;
  }

  button:hover {
    background: #d8f28e;
    color: #2a4200;
    border-color: #4b690f;
  }

  .info-box {
    background: #4a6a0f;
    padding: 1rem;
    border-radius: 6px;
    margin-top: 1rem;
    color: #c3df4a;
    white-space: pre-wrap;
    box-shadow: inset 0 0 10px #9fd34b;
  }

  .error {
    color: #ff6b6b;
    margin-top: 0.5rem;
    font-size: 0.55rem;
  }

  #abmeldungSuccess, #teamInfoSuccess {
    font-size: 0.6rem;
    margin-top: 0.5rem;
  }

  small {
    font-size: 0.5rem;
    color: #a5d081;
  }

  hr {
    border: 1px solid #5a8e00;
    margin: 2rem 0;
  }
</style>
</head>
<body>

<h1>Dashboard Team Flex-City</h1>
<p>Dies ist das offizielle Dashboard von Flex City</p>

<!-- Abmeldung-Team Forum -->
<section>
  <h2>Abmeldung-Team</h2>
  <form id="abmeldungForm">
    <label for="wer">Wer: <span style="color:#ff4444;">*</span></label>
    <input type="text" id="wer" name="wer" required autocomplete="off" />
    
    <label for="wieLange">Wie lange: <span style="color:#ff4444;">*</span></label>
    <input type="text" id="wieLange" name="wieLange" placeholder="TT.MM.JJ-TT.MM.JJ" pattern="\d{2}\.\d{2}\.\d{2}-\d{2}\.\d{2}\.\d{2}" required autocomplete="off" />
    <small>Format: TT.MM.JJ-TT.MM.JJ</small>

    <label for="grund">Welcher Grund: <span style="color:#ff4444;">*</span> (mindestens 50 Wörter)</label>
    <textarea id="grund" name="grund" minlength="250" required placeholder="Bitte mindestens 50 Wörter eingeben..."></textarea>

    <button type="submit">Abmelden</button>
    <p id="abmeldungError" class="error"></p>
    <p id="abmeldungSuccess" style="color:#9fff5c;"></p>
  </form>
</section>

<hr />

<!-- Team Information -->
<section>
  <h2>TEAM INFORMATION</h2>
  <div id="teamInfoBox" class="info-box">Keine Verfügbar</div>

  <form id="teamInfoForm">
    <label for="ueberschrift">Überschrift: <span style="color:#ff4444;">*</span></label>
    <input type="text" id="ueberschrift" name="ueberschrift" required autocomplete="off" />

    <label for="haupttext">Haupttext: <span style="color:#ff4444;">*</span></label>
    <textarea id="haupttext" name="haupttext" required></textarea>

    <label for="geschriebenVon">Geschrieben von: <span style="color:#ff4444;">*</span></label>
    <input type="text" id="geschriebenVon" name="geschriebenVon" required autocomplete="off" />

    <button type="submit">Informationen absenden</button>
    <p id="teamInfoError" class="error"></p>
    <p id="teamInfoSuccess" style="color:#9fff5c;"></p>
  </form>
</section>

<script>
  // Deine Discord Webhook URLs
  const abmeldungWebhookUrl = "https://discord.com/api/webhooks/1397035955671798033/mcDxMU3kHKNl_9ev-afJ_xGI79vvkfwFIV502e0mB8omEOZ-_zxC6bRjs7RraC-QuLJW";
  const teamInfoWebhookUrl = "https://discord.com/api/webhooks/1397036110651330684/B0DmsHjO2cNtmD426cyLk49ymOXc_2PymjMJRSMpyw0-rwL1MjNVgXj-16uQeQDob3l3";

  function countWords(str) {
    return str.trim().split(/\s+/).length;
  }

  // Abmeldung-Formular
  document.getElementById('abmeldungForm').addEventListener('submit', async function(e) {
    e.preventDefault();
    const wer = this.wer.value.trim();
    const wieLange = this.wieLange.value.trim();
    const grund = this.grund.value.trim();
    const errorEl = document.getElementById('abmeldungError');
    const successEl = document.getElementById('abmeldungSuccess');
    errorEl.textContent = "";
    successEl.textContent = "";

    if(countWords(grund) < 50) {
      errorEl.textContent = "Der Grund muss mindestens 50 Wörter enthalten.";
      return;
    }

    const message = `**Abmeldung-Team**\n**Wer:** ${wer}\n**Wie lange:** ${wieLange}\n**Welcher Grund:**\n${grund}`;

    try {
      const res = await fetch(abmeldungWebhookUrl, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ content: message }),
      });

      if(res.ok){
        successEl.textContent = "Abmeldung wurde erfolgreich gesendet!";
        this.reset();
      } else {
        errorEl.textContent = "Fehler beim Senden an Discord.";
      }
    } catch (err) {
      errorEl.textContent = "Netzwerkfehler beim Senden.";
    }
  });

  // Team Info Formular
  document.getElementById('teamInfoForm').addEventListener('submit', async function(e) {
    e.preventDefault();
    const ueberschrift = this.ueberschrift.value.trim();
    const haupttext = this.haupttext.value.trim();
    const geschriebenVon = this.geschriebenVon.value.trim();
    const errorEl = document.getElementById('teamInfoError');
    const successEl = document.getElementById('teamInfoSuccess');
    errorEl.textContent = "";
    successEl.textContent = "";

    if(!ueberschrift || !haupttext || !geschriebenVon) {
      errorEl.textContent = "Bitte alle Pflichtfelder ausfüllen.";
      return;
    }

    const message = `**TEAM INFORMATION**\n**Überschrift:** ${ueberschrift}\n**Haupttext:**\n${haupttext}\n**Geschrieben von:** ${geschriebenVon}`;

    try {
      const res = await fetch(teamInfoWebhookUrl, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ content: message }),
      });

      if(res.ok){
        successEl.textContent = "Team Information wurde erfolgreich gesendet!";
        this.reset();
        // Zeige die Info im Dashboard an
        document.getElementById('teamInfoBox').textContent = haupttext;
      } else {
        errorEl.textContent = "Fehler beim Senden an Discord.";
      }
    } catch (err) {
      errorEl.textContent = "Netzwerkfehler beim Senden.";
    }
  });
</script>

</body>
</html>

