<!DOCTYPE html>
<html lang="de">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Dashboard Team Flex-City</title>
  <style>
    body {
      font-family: sans-serif;
      background: #1e1e1e;
      color: #f5f5f5;
      max-width: 800px;
      margin: 0 auto;
      padding: 2rem;
    }
    h1, h2 {
      color: #9fff5c;
    }
    label {
      display: block;
      margin-top: 1rem;
      font-weight: bold;
    }
    input, textarea {
      width: 100%;
      padding: 0.5rem;
      margin-top: 0.3rem;
      border: 1px solid #ccc;
      border-radius: 4px;
      font-family: inherit;
      background: #2c2c2c;
      color: #fff;
    }
    textarea {
      resize: vertical;
    }
    button {
      margin-top: 1rem;
      padding: 0.6rem 1.2rem;
      background: #9fff5c;
      border: none;
      color: #000;
      font-weight: bold;
      cursor: pointer;
    }
    .info-box {
      background: #333;
      padding: 1rem;
      border-radius: 6px;
      margin-bottom: 2rem;
      box-shadow: inset 0 0 10px #111;
    }
    .error {
      color: #ff6b6b;
      font-size: 0.9rem;
    }
    .success {
      color: #9fff5c;
      font-size: 0.9rem;
    }
    hr {
      border: none;
      border-top: 1px solid #666;
      margin: 2rem 0;
    }
  </style>
</head>
<body>

  <h1>Dashboard Team Flex-City</h1>
  <p>Dies ist das offizielle Dashboard von Flex City</p>

  <!-- MEETING LIST -->
  <div id="meetingListDisplay" class="info-box">
    📅 <strong>Geplante Meetings:</strong><br />
    <span id="meetingListContent">Keine Meetings eingetragen.</span>
  </div>

  <!-- Abmeldung-Team Formular -->
  <section>
    <h2>Abmeldung-Team</h2>
    <form id="abmeldungForm">
      <label for="wer">Wer: *</label>
      <input type="text" id="wer" name="wer" required autocomplete="off" />
      
      <label for="von">Von: *</label>
      <input type="date" id="von" name="von" required />

      <label for="bis">Bis: *</label>
      <input type="date" id="bis" name="bis" required />

      <label for="grund">Welcher Grund: *</label>
      <textarea id="grund" name="grund" minlength="50" required placeholder="Bitte mindestens 50 Wörter eingeben..."></textarea>

      <button type="submit">Abmelden</button>
      <p id="abmeldungError" class="error"></p>
      <p id="abmeldungSuccess" class="success"></p>
    </form>
  </section>

  <hr />

  <!-- Team Information -->
  <section>
    <h2>Team Information</h2>
    <div id="teamInfoBox" class="info-box">Keine Verfügbar</div>

    <form id="teamInfoForm">
      <label for="ueberschrift">Überschrift: *</label>
      <input type="text" id="ueberschrift" name="ueberschrift" required autocomplete="off" />

      <label for="haupttext">Haupttext: *</label>
      <textarea id="haupttext" name="haupttext" required></textarea>

      <label for="geschriebenVon">Geschrieben von: *</label>
      <input type="text" id="geschriebenVon" name="geschriebenVon" required autocomplete="off" />

      <button type="submit">Informationen absenden</button>
      <p id="teamInfoError" class="error"></p>
      <p id="teamInfoSuccess" class="success"></p>
    </form>
  </section>

  <hr />

  <!-- /MEETINGS/ Formular -->
  <section>
    <h2>/MEETINGS/</h2>
    <form id="meetingForm">
      <label for="meetingDatum">Datum & Uhrzeit: *</label>
      <input type="datetime-local" id="meetingDatum" name="meetingDatum" required />

      <label for="meetingGrund">Grund (Was wird besprochen): *</label>
      <textarea id="meetingGrund" name="meetingGrund" required placeholder="Kurze Beschreibung..."></textarea>

      <label for="meetingLeiter">Leiter des Meetings: *</label>
      <input type="text" id="meetingLeiter" name="meetingLeiter" required autocomplete="off" />

      <button type="submit">Meeting eintragen</button>
      <p id="meetingError" class="error"></p>
      <p id="meetingSuccess" class="success"></p>
    </form>
  </section>

  <script>
    const abmeldungWebhookUrl = "https://discord.com/api/webhooks/1397035955671798033/mcDxMU3kHKNl_9ev-afJ_xGI79vvkfwFIV502e0mB8omEOZ-_zxC6bRjs7RraC-QuLJW";
    const teamInfoWebhookUrl = "https://discord.com/api/webhooks/1397036110651330684/B0DmsHjO2cNtmD426cyLk49ymOXc_2PymjMJRSMpyw0-rwL1MjNVgXj-16uQeQDob3l3";
    const meetingWebhookUrl = "https://discord.com/api/webhooks/1397079732733874309/pUD5fa9i3SblLV6sT2uMMms-hf80xBycKIgl_h8YKy4bZePu6t-_dseR64Fd7ixEVhuX";

    // Abmeldung
    document.getElementById('abmeldungForm').addEventListener('submit', async function(e) {
      e.preventDefault();
      const wer = this.wer.value.trim();
      const von = this.von.value;
      const bis = this.bis.value;
      const grund = this.grund.value.trim();
      const errorEl = document.getElementById('abmeldungError');
      const successEl = document.getElementById('abmeldungSuccess');
      errorEl.textContent = "";
      successEl.textContent = "";

      if (grund.split(/\s+/).length < 50) {
        errorEl.textContent = "Der Grund muss mindestens 50 Wörter enthalten.";
        return;
      }

      const message = `📢 **Abmeldung im Team**\n\n👤 **Wer:** ${wer}\n📅 **Von:** ${von} bis ${bis}\n✏️ **Grund:**\n${grund}`;

      try {
        const res = await fetch(abmeldungWebhookUrl, {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ content: message }),
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

    // Team Info
    document.getElementById('teamInfoForm').addEventListener('submit', async function(e) {
      e.preventDefault();
      const ueberschrift = this.ueberschrift.value.trim();
      const haupttext = this.haupttext.value.trim();
      const geschriebenVon = this.geschriebenVon.value.trim();
      const errorEl = document.getElementById('teamInfoError');
      const successEl = document.getElementById('teamInfoSuccess');
      errorEl.textContent = "";
      successEl.textContent = "";

      const message = `📝 **Team Information**\n\n📌 **${ueberschrift}**\n\n${haupttext}\n\n✍️ *Geschrieben von:* ${geschriebenVon}`;

      try {
        const res = await fetch(teamInfoWebhookUrl, {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ content: message }),
        });

        if (res.ok) {
          successEl.textContent = "Team Information wurde erfolgreich gesendet!";
          document.getElementById('teamInfoBox').textContent = haupttext;
          this.reset();
        } else {
          errorEl.textContent = "Fehler beim Senden an Discord.";
        }
      } catch (err) {
        errorEl.textContent = "Netzwerkfehler beim Senden.";
      }
    });

    // Meetingliste
    function showMeetingList() {
      const list = JSON.parse(localStorage.getItem('meetings') || "[]");
      const display = document.getElementById('meetingListContent');
      if (list.length === 0) {
        display.textContent = "Keine Meetings eingetragen.";
        return;
      }
      display.innerHTML = list.map(m =>
        `- 🕒 ${m.datum} | 📋 ${m.grund} | 👤 ${m.leiter}`
      ).join("<br>");
    }
    showMeetingList();

    // Meeting
    document.getElementById('meetingForm').addEventListener('submit', async function(e) {
      e.preventDefault();

      const datum = this.meetingDatum.value.trim();
      const grund = this.meetingGrund.value.trim();
      const leiter = this.meetingLeiter.value.trim();
      const errorEl = document.getElementById('meetingError');
      const successEl = document.getElementById('meetingSuccess');
      errorEl.textContent = "";
      successEl.textContent = "";

      const message = `📅 **Neues Meeting eingetragen**\n\n🕒 **Wann:** ${datum}\n📋 **Thema:** ${grund}\n👤 **Leiter:** ${leiter}`;

      try {
        const res = await fetch(meetingWebhookUrl, {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ content: message }),
        });

        if (res.ok) {
          successEl.textContent = "Meeting erfolgreich eingetragen!";
          const list = JSON.parse(localStorage.getItem('meetings') || "[]");
          list.push({ datum, grund, leiter });
          localStorage.setItem('meetings', JSON.stringify(list));
          showMeetingList();
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
