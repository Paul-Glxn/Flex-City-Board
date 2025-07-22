<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Dashboard Team Flex-City</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #1e1e1e;
      color: #ffffff;
      max-width: 700px;
      margin: 2rem auto;
      padding: 1rem;
    }
    h1, h2 {
      color: #90ee90;
    }
    form {
      margin-top: 1rem;
      background: #2c2c2c;
      padding: 1rem;
      border-radius: 6px;
    }
    label {
      display: block;
      margin-top: 0.8rem;
      font-weight: bold;
    }
    input, textarea {
      width: 100%;
      padding: 0.6rem;
      margin-top: 0.2rem;
      background: #3a3a3a;
      border: 1px solid #555;
      color: #fff;
      border-radius: 4px;
    }
    button {
      margin-top: 1rem;
      background: #90ee90;
      border: none;
      padding: 0.7rem 1.2rem;
      font-weight: bold;
      cursor: pointer;
      border-radius: 4px;
      color: #000;
    }
    .info-box {
      background: #333;
      padding: 1rem;
      border-radius: 6px;
      margin-top: 1rem;
    }
    .error {
      color: #ff6b6b;
      margin-top: 0.5rem;
    }
    .success {
      color: #9fff5c;
      margin-top: 0.5rem;
    }
  </style>
</head>
<body>

<h1>Dashboard Team Flex-City</h1>

<!-- Abmeldung Formular -->
<section>
  <h2>Abmeldung-Team</h2>
  <form id="abmeldungForm">
    <label for="wer">Wer:</label>
    <input type="text" id="wer" name="wer" required autocomplete="off" />

    <label for="wieLange">Wie lange:</label>
    <input type="text" id="wieLange" name="wieLange" placeholder="TT.MM.JJ - TT.MM.JJ" required autocomplete="off" />

    <label for="grund">Grund (mind. 50 Wörter):</label>
    <textarea id="grund" name="grund" required minlength="250"></textarea>

    <button type="submit">Abmeldung absenden</button>
    <p id="abmeldungError" class="error"></p>
    <p id="abmeldungSuccess" class="success"></p>
  </form>
</section>

<!-- Team Information Formular -->
<section>
  <h2 style="margin-top: 3rem;">Team Information</h2>
  <div id="teamInfoBox" class="info-box">Keine verfügbar</div>

  <form id="teamInfoForm">
    <label for="ueberschrift">Überschrift:</label>
    <input type="text" id="ueberschrift" name="ueberschrift" required autocomplete="off" />

    <label for="haupttext">Haupttext:</label>
    <textarea id="haupttext" name="haupttext" required></textarea>

    <label for="geschriebenVon">Geschrieben von:</label>
    <input type="text" id="geschriebenVon" name="geschriebenVon" required autocomplete="off" />

    <button type="submit">Information absenden</button>
    <p id="teamInfoError" class="error"></p>
    <p id="teamInfoSuccess" class="success"></p>
  </form>
</section>

<script>
  // Webhook-URLs
  const abmeldungWebhookUrl = "https://discord.com/api/webhooks/1397035955671798033/mcDxMU3kHKNl_9ev-afJ_xGI79vvkfwFIV502e0mB8omEOZ-_zxC6bRjs7RraC-QuLJW";
  const teamInfoWebhookUrl = "https://discord.com/api/webhooks/1397036110651330684/B0DmsHjO2cNtmD426cyLk49ymOXc_2PymjMJRSMpyw0-rwL1MjNVgXj-16uQeQDob3l3";

  function countWords(text) {
    return text.trim().split(/\s+/).length;
  }

  // Abmeldung Formular
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

    const message = `📢 **Abmeldung im Team**\n👤 **Wer:** ${wer}\n📅 **Zeitraum:** ${wieLange}\n📝 **Grund:**\n${grund}`;

    try {
      const res = await fetch(abmeldungWebhookUrl, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ content: message }),
      });

      if (res.ok) {
        successEl.textContent = "Abmeldung erfolgreich an Discord gesendet!";
        this.reset();
      } else {
        errorEl.textContent = "Fehler beim Senden an Discord.";
      }
    } catch (err) {
      errorEl.textContent = "Netzwerkfehler beim Senden.";
    }
  });

  // Team Information Formular
  document.getElementById('teamInfoForm').addEventListener('submit', async function(e) {
    e.preventDefault();
    const ueberschrift = this.ueberschrift.value.trim();
    const haupttext = this.haupttext.value.trim();
    const geschriebenVon = this.geschriebenVon.value.trim();
    const errorEl = document.getElementById('teamInfoError');
    const successEl = document.getElementById('teamInfoSuccess');
    errorEl.textContent = "";
    successEl.textContent = "";

    if (!ueberschrift || !haupttext || !geschriebenVon) {
      errorEl.textContent = "Bitte alle Felder ausfüllen.";
      return;
    }

    const message = `📌 **Neue Team-Information**\n📖 **Titel:** ${ueberschrift}\n🗒️ **Text:**\n${haupttext}\n✍️ **Verfasst von:** ${geschriebenVon}`;

    try {
      const res = await fetch(teamInfoWebhookUrl, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ content: message }),
      });

      if (res.ok) {
        successEl.textContent = "Information erfolgreich an Discord gesendet!";
        this.reset();
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
