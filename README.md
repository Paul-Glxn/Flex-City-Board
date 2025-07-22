<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Dashboard Team Flex-City</title>
  <link href="https://fonts.googleapis.com/css2?family=Segoe+UI:wght@400;700&display=swap" rel="stylesheet">
  <style>
    body {
      font-family: 'Segoe UI', sans-serif;
      background-color: #1c1c1c;
      color: #f2f2f2;
      padding: 2rem;
      max-width: 800px;
      margin: 0 auto;
    }

    h1, h2 {
      color: #00ffcc;
      border-bottom: 2px solid #00ffcc;
      padding-bottom: 5px;
    }

    label {
      display: block;
      margin-top: 1rem;
      font-weight: bold;
    }

    input, textarea {
      width: 100%;
      padding: 10px;
      margin-top: 5px;
      background-color: #2a2a2a;
      color: #fff;
      border: 1px solid #555;
      border-radius: 5px;
    }

    button {
      margin-top: 1rem;
      padding: 10px 20px;
      background-color: #00cc88;
      border: none;
      border-radius: 5px;
      color: #000;
      font-weight: bold;
      cursor: pointer;
    }

    button:hover {
      background-color: #00ffaa;
    }

    .error {
      color: #ff6b6b;
      margin-top: 0.5rem;
    }

    .success {
      color: #9fff5c;
      margin-top: 0.5rem;
    }

    .info-box {
      background-color: #2a2a2a;
      padding: 1rem;
      margin-top: 1rem;
      border-left: 4px solid #00ffcc;
    }

    hr {
      border: none;
      border-top: 1px solid #333;
      margin: 2rem 0;
    }
  </style>
</head>
<body>

<h1>Dashboard Team Flex-City</h1>

<section>
  <h2>Abmeldung-Team</h2>
  <form id="abmeldungForm">
    <label for="wer">Wer:</label>
    <input type="text" id="wer" name="wer" required />

    <label for="wieLange">Wie lange (Format: TT.MM.JJ-TT.MM.JJ):</label>
    <input type="text" id="wieLange" name="wieLange" required pattern="\d{2}\.\d{2}\.\d{2}-\d{2}\.\d{2}\.\d{2}" />

    <label for="grund">Grund (min. 50 Wörter):</label>
    <textarea id="grund" name="grund" minlength="250" required></textarea>

    <button type="submit">Abmelden</button>
    <p class="error" id="abmeldungError"></p>
    <p class="success" id="abmeldungSuccess"></p>
  </form>
</section>

<hr />

<section>
  <h2>Team Information</h2>
  <div id="teamInfoBox" class="info-box">Keine Informationen verfügbar.</div>

  <form id="teamInfoForm">
    <label for="ueberschrift">Überschrift:</label>
    <input type="text" id="ueberschrift" name="ueberschrift" required />

    <label for="haupttext">Haupttext:</label>
    <textarea id="haupttext" name="haupttext" required></textarea>

    <label for="geschriebenVon">Geschrieben von:</label>
    <input type="text" id="geschriebenVon" name="geschriebenVon" required />

    <button type="submit">Information absenden</button>
    <p class="error" id="teamInfoError"></p>
    <p class="success" id="teamInfoSuccess"></p>
  </form>
</section>

<script>
  const abmeldungWebhookUrl = "https://discord.com/api/webhooks/1397035955671798033/mcDxMU3kHKNl_9ev-afJ_xGI79vvkfwFIV502e0mB8omEOZ-_zxC6bRjs7RraC-QuLJW";
  const teamInfoWebhookUrl = "https://discord.com/api/webhooks/1397036110651330684/B0DmsHjO2cNtmD426cyLk49ymOXc_2PymjMJRSMpyw0-rwL1MjNVgXj-16uQeQDob3l3";

  function countWords(str) {
    return str.trim().split(/\s+/).length;
  }

  document.getElementById('abmeldungForm').addEventListener('submit', async function(e) {
    e.preventDefault();
    const wer = this.wer.value.trim();
    const wieLange = this.wieLange.value.trim();
    const grund = this.grund.value.trim();

    const errorEl = document.getElementById('abmeldungError');
    const successEl = document.getElementById('abmeldungSuccess');
    errorEl.textContent = "";
    successEl.textContent = "";

    if (countWords(grund) < 50) {
      errorEl.textContent = "Der Grund muss mindestens 50 Wörter enthalten.";
      return;
    }

    const message = `📢 **Abmeldung eines Teammitglieds** 📢\n\n👤 **Wer:** ${wer}\n📅 **Zeitraum:** ${wieLange}\n📝 **Grund:**\n>>> ${grund}`;

    try {
      const res = await fetch(abmeldungWebhookUrl, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ content: message })
      });

      if (res.ok) {
        successEl.textContent = "Abmeldung wurde erfolgreich gesendet!";
        this.reset();
      } else {
        errorEl.textContent = "Fehler beim Senden an Discord.";
      }
    } catch (err) {
      errorEl.textContent = "Netzwerkfehler beim Senden.";
    }
  });

  document.getElementById('teamInfoForm').addEventListener('submit', async function(e) {
    e.preventDefault();
    const ueberschrift = this.ueberschrift.value.trim();
    const haupttext = this.haupttext.value.trim();
    const geschriebenVon = this.geschriebenVon.value.trim();

    const errorEl = document.getElementById('teamInfoError');
    const successEl = document.getElementById('teamInfoSuccess');
    errorEl.textContent = "";
    successEl.textContent = "";

    const message = `📌 **Neue Team-Info**\n\n📖 **${ueberschrift}**\n\n🗒️ >>> ${haupttext}\n\n✍️ Geschrieben von: **${geschriebenVon}**`;

    try {
      const res = await fetch(teamInfoWebhookUrl, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ content: message })
      });

      if (res.ok) {
        successEl.textContent = "Information erfolgreich gesendet!";
        document.getElementById('teamInfoBox').textContent = haupttext;
        this.reset();
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
