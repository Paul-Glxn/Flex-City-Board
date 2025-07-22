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
    h1, h2, h3 {
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
    details {
      margin-top: 1rem;
      background: #2a2a2a;
      padding: 0.5rem;
      border-radius: 4px;
    }
    summary {
      cursor: pointer;
      font-weight: bold;
      color: #9fff5c;
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

  <hr />

  <!-- <ABSTIMMUNG> Formular -->
  <section>
    <h2>&lt;ABSTIMMUNG&gt;</h2>
    <form id="abstimmungForm">
      <label for="abstimmungWas">Abstimmung - (Was soll abgestimmt werden): *</label>
      <textarea id="abstimmungWas" name="abstimmungWas" required placeholder="Thema der Abstimmung..."></textarea>

      <label for="abstimmungZusatz">Zusatz Text (optional):</label>
      <textarea id="abstimmungZusatz" name="abstimmungZusatz" placeholder="Optionaler Zusatztext..."></textarea>

      <button type="submit">Abstimmen</button>
      <p id="abstimmungError" class="error"></p>
      <p id="abstimmungSuccess" class="success"></p>
    </form>
  </section>

  <hr />

  <!-- Kummerkasten -->
  <section>
    <h2>Kummerkasten 📨</h2>
    <p>Teile anonym dein Feedback. Deine Nachricht ist für alle sichtbar.</p>

    <form id="kummerForm">
      <label for="kummerNachricht">Nachricht:</label>
      <textarea id="kummerNachricht" required placeholder="Was möchtest du loswerden? (anonym)"></textarea>
      <button type="submit">Absenden</button>
      <p id="kummerError" class="error"></p>
    </form>

    <hr />
    <h3>📬 Eingegangene Nachrichten:</h3>
    <div id="kummerListe"></div>
  </section>

  <!-- Script -->
  <script>
    const abmeldungWebhookUrl = "DEIN_ABMELDUNG_WEBHOOK";
    const teamInfoWebhookUrl = "DEIN_TEAMINFO_WEBHOOK";
    const meetingWebhookUrl = "DEIN_MEETING_WEBHOOK";
    const abstimmungWebhookUrl = "DEIN_ABSTIMMUNG_WEBHOOK";

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

    // Meetingliste anzeigen
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

    // Meeting eintragen
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

    // Abstimmung
    document.getElementById('abstimmungForm').addEventListener('submit', async function(e) {
      e.preventDefault();
      const abstimmungWas = this.abstimmungWas.value.trim();
      const abstimmungZusatz = this.abstimmungZusatz.value.trim();
      const errorEl = document.getElementById('abstimmungError');
      const successEl = document.getElementById('abstimmungSuccess');
      errorEl.textContent = "";
      successEl.textContent = "";

      if (!abstimmungWas) {
        errorEl.textContent = "Bitte gib ein Thema für die Abstimmung an.";
        return;
      }

      let message = `🗳️ **Neue Abstimmung gestartet**\n\n📋 **Thema:** ${abstimmungWas}\n\n✅ Ja\n❌ Nein`;
      if (abstimmungZusatz) {
        message += `\n\nℹ️ Zusatz: ${abstimmungZusatz}`;
      }

      try {
        const res = await fetch(abstimmungWebhookUrl, {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ content: message }),
        });

        if (res.ok) {
          successEl.textContent = "Abstimmung wurde erfolgreich gesendet!";
          this.reset();
        } else {
          errorEl.textContent = "Fehler beim Senden an Discord.";
        }
      } catch (err) {
        errorEl.textContent = "Netzwerkfehler beim Senden.";
      }
    });

    // Kummerkasten
    const kummerForm = document.getElementById('kummerForm');
    const kummerListe = document.getElementById('kummerListe');
    const kummerError = document.getElementById('kummerError');
    let nachrichten = JSON.parse(localStorage.getItem('kummerNachrichten') || "[]");

    function renderKummerkasten() {
      kummerListe.innerHTML = '';
      nachrichten.forEach((msg, index) => {
        const wrapper = document.createElement('div');
        wrapper.classList.add('info-box');
        wrapper.innerHTML = `
          <p><strong>📝 Nachricht ${index + 1}:</strong><br>${msg.text}</p>
          <div id="antworten-${index}">
            ${msg.antwort ? `<p><strong>Antwort:</strong> ${msg.antwort}</p>` : ''}
          </div>
          ${!msg.antwort ? `
          <details>
            <summary>Antwort schreiben (nur mit Passwort)</summary>
            <form onsubmit="antwortSpeichern(event, ${index})">
              <label for="antwort-${index}">Antwort:</label>
              <textarea id="antwort-${index}" required></textarea>
              <label for="pw-${index}">Passwort:</label>
              <input type="password" id="pw-${index}" required />
              <button type="submit">Antwort absenden</button>
              <p id="fehler-${index}" class="error"></p>
            </form>
          </details>
          ` : ''}
        `;
        kummerListe.appendChild(wrapper);
      });
    }

    kummerForm.addEventListener('submit', function(e) {
      e.preventDefault();
      const text = document.getElementById('kummerNachricht').value.trim();
      if (text.length < 5) {
        kummerError.textContent = "Bitte gib eine etwas längere Nachricht ein.";
        return;
      }
      nachrichten.push({ text, antwort: null });
      localStorage.setItem('kummerNachrichten', JSON.stringify(nachrichten));
      this.reset();
      kummerError.textContent = "";
      renderKummerkasten();
    });

    window.antwortSpeichern = function(e, index) {
      e.preventDefault();
      const antwortText = document.getElementById(`antwort-${index}`).value.trim();
      const pw = document.getElementById(`pw-${index}`).value.trim();
      const fehler = document.getElementById(`fehler-${index}`);

      if (pw !== "FlexCity") {
        fehler.textContent = "Falsches Passwort.";
        return;
      }

      nachrichten[index].antwort = antwortText;
      localStorage.setItem('kummerNachrichten', JSON.stringify(nachrichten));
      renderKummerkasten();
    };

    renderKummerkasten();
  </script>

</body>
</html>
