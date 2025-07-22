<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Dashboard Team Flex-City</title>
  <style>
    body {
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
      background-color: #f4f4f4;
      color: #333;
      max-width: 700px;
      margin: 2rem auto;
      padding: 1.5rem;
    }
    h1, h2 {
      color: #2c3e50;
      margin-bottom: 0.5rem;
    }
    label {
      display: block;
      margin-top: 1rem;
      font-weight: 600;
    }
    input, textarea {
      width: 100%;
      padding: 0.6rem;
      margin-top: 0.3rem;
      border: 1px solid #ccc;
      border-radius: 4px;
      font-size: 1rem;
      font-family: inherit;
    }
    textarea {
      resize: vertical;
      min-height: 100px;
    }
    button {
      margin-top: 1.2rem;
      padding: 0.8rem 1.8rem;
      background-color: #3498db;
      color: #fff;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      font-size: 1rem;
      font-weight: 600;
    }
    button:hover {
      background-color: #2980b9;
    }
    .info-box {
      background-color: #fff;
      padding: 1rem;
      margin-top: 1rem;
      border: 1px solid #ccc;
      border-radius: 4px;
      line-height: 1.5;
    }
    .error {
      color: #e74c3c;
      margin-top: 0.5rem;
      font-size: 0.9rem;
    }
    .success {
      color: #27ae60;
      margin-top: 0.5rem;
      font-size: 0.9rem;
    }
    hr {
      margin: 2rem 0;
      border: none;
      border-top: 1px solid #ccc;
    }
  </style>
</head>
<body>

  <h1>Dashboard Team Flex-City</h1>

  <!-- Abmeldung-Team Formular -->
  <section>
    <h2>Abmeldung-Team</h2>
    <form id="abmeldungForm">
      <label for="wer">Wer: *</label>
      <input type="text" id="wer" name="wer" required />

      <label for="wieLange">Wie lange: * (TT.MM.JJ-TT.MM.JJ)</label>
      <input type="text" id="wieLange" name="wieLange" placeholder="TT.MM.JJ-TT.MM.JJ" required />

      <label for="grund">Welcher Grund: * (mind. 50 Wörter)</label>
      <textarea id="grund" name="grund" minlength="250" required></textarea>

      <button type="submit">Abmelden</button>
      <p id="abmeldungError" class="error"></p>
      <p id="abmeldungSuccess" class="success"></p>
    </form>
  </section>

  <hr />

  <!-- Team Information Formular -->
  <section>
    <h2>Team Information</h2>
    <div id="teamInfoBox" class="info-box">Keine Verfügbar</div>

    <form id="teamInfoForm">
      <label for="ueberschrift">Überschrift: *</label>
      <input type="text" id="ueberschrift" name="ueberschrift" required />

      <label for="haupttext">Haupttext: *</label>
      <textarea id="haupttext" name="haupttext" required></textarea>

      <label for="geschriebenVon">Geschrieben von: *</label>
      <input type="text" id="geschriebenVon" name="geschriebenVon" required />

      <button type="submit">Information absenden</button>
      <p id="teamInfoError" class="error"></p>
      <p id="teamInfoSuccess" class="success"></p>
    </form>
  </section>

  <script>
    const abmeldungWebhookUrl = "https://discord.com/api/webhooks/DEINE_ID_1";
    const teamInfoWebhookUrl = "https://discord.com/api/webhooks/DEINE_ID_2";

    function countWords(str) {
      return str.trim().split(/\s+/).filter(w => w).length;
    }

    document.getElementById('abmeldungForm').addEventListener('submit', async function(e) {
      e.preventDefault();
      const errorEl = document.getElementById('abmeldungError');
      const successEl = document.getElementById('abmeldungSuccess');
      errorEl.textContent = '';
      successEl.textContent = '';

      const wer = this.wer.value.trim();
      const wieLange = this.wieLange.value.trim();
      const grund = this.grund.value.trim();

      if (!wer || !wieLange || countWords(grund) < 50) {
        errorEl.textContent = 'Bitte alle Pflichtfelder korrekt ausfüllen.';
        return;
      }

      const message = `**Abmeldung-Team**\nWer: ${wer}\nWie lange: ${wieLange}\nGrund:\n${grund}`;

      try {
        const res = await fetch(abmeldungWebhookUrl, {
          method: 'POST',
          headers: {'Content-Type': 'application/json'},
          body: JSON.stringify({ content: message })
        });
        if (res.ok) {
          successEl.textContent = 'Abmeldung erfolgreich gesendet!';
          this.reset();
        } else {
          errorEl.textContent = 'Fehler beim Senden an Discord.';
        }
      } catch {
        errorEl.textContent = 'Netzwerkfehler beim Senden.';
      }
    });

    document.getElementById('teamInfoForm').addEventListener('submit', async function(e) {
      e.preventDefault();
      const errorEl = document.getElementById('teamInfoError');
      const successEl = document.getElementById('teamInfoSuccess');
      const box = document.getElementById('teamInfoBox');
      errorEl.textContent = '';
      successEl.textContent = '';

      const ueberschrift = this.ueberschrift.value.trim();
      const haupttext = this.haupttext.value.trim();
      const geschriebenVon = this.geschriebenVon.value.trim();

      if (!ueberschrift || !haupttext || !geschriebenVon) {
        errorEl.textContent = 'Bitte alle Felder ausfüllen.';
        return;
      }

      const message = `**TEAM INFORMATION**\nÜberschrift: ${ueberschrift}\nHaupttext:\n${haupttext}\nGeschrieben von: ${geschriebenVon}`;

      try {
        const res = await fetch(teamInfoWebhookUrl, {
          method: 'POST',
          headers: {'Content-Type': 'application/json'},
          body: JSON.stringify({ content: message })
        });
        if (res.ok) {
          successEl.textContent = 'Team‑Info erfolgreich gesendet!';
          box.textContent = haupttext;
          this.reset();
        } else {
          errorEl.textContent = 'Fehler beim Senden an Discord.';
        }
      } catch {
        errorEl.textContent = 'Netzwerkfehler beim Senden.';
      }
    });
  </script>

</body>
</html>
