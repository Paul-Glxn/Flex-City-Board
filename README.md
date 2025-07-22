<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Dashboard Team Flex-City</title>
<style>
  /* Edler, moderner Stil */
  @import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap');

  body {
    font-family: 'Montserrat', sans-serif;
    background: linear-gradient(135deg, #e2e8f0, #cbd5e1);
    color: #2d3748;
    margin: 0;
    padding: 2rem;
    max-width: 700px;
    margin-left: auto;
    margin-right: auto;
    user-select: none;
  }

  h1, h2 {
    font-weight: 700;
    color: #1a202c;
    margin-bottom: 0.5rem;
    border-bottom: 2px solid #4a5568;
    padding-bottom: 0.3rem;
  }

  p {
    font-size: 0.9rem;
    margin-top: 0;
    margin-bottom: 1.5rem;
    color: #4a5568;
  }

  label {
    display: block;
    margin-top: 1rem;
    font-weight: 600;
    color: #2d3748;
    font-size: 0.9rem;
  }

  input, textarea {
    font-family: 'Montserrat', sans-serif;
    font-size: 0.9rem;
    background: #f7fafc;
    border: 1.8px solid #a0aec0;
    border-radius: 6px;
    color: #2d3748;
    padding: 0.8rem 1rem;
    margin-top: 0.3rem;
    width: 100%;
    box-sizing: border-box;
    transition: border-color 0.3s ease;
  }

  input:focus, textarea:focus {
    border-color: #3182ce;
    outline: none;
    background: #ebf8ff;
  }

  textarea {
    resize: vertical;
    min-height: 100px;
  }

  button {
    margin-top: 1.5rem;
    padding: 0.85rem 2rem;
    background: #2b6cb0;
    border: none;
    border-radius: 8px;
    color: white;
    font-weight: 700;
    font-size: 1rem;
    cursor: pointer;
    box-shadow: 0 4px 8px rgba(43,108,176,0.4);
    transition: background-color 0.3s ease;
  }

  button:hover {
    background: #2c5282;
  }

  .info-box {
    background: #edf2f7;
    padding: 1.5rem;
    border-radius: 10px;
    margin-top: 1.5rem;
    color: #1a202c;
    box-shadow: 0 0 8px rgba(160,160,160,0.15);
    font-size: 0.95rem;
    line-height: 1.5;
    white-space: pre-wrap;
  }

  .error {
    color: #e53e3e;
    margin-top: 0.4rem;
    font-size: 0.85rem;
    font-weight: 600;
  }

  .success {
    color: #38a169;
    margin-top: 0.4rem;
    font-size: 0.9rem;
    font-weight: 600;
  }

  small {
    font-size: 0.8rem;
    color: #718096;
  }

  hr {
    border: none;
    border-top: 1px solid #cbd5e1;
    margin: 2.5rem 0;
  }

  /* Form group styling for floating labels */
  .form-group {
    position: relative;
    margin-top: 1.5rem;
  }

  .form-group input,
  .form-group textarea {
    font-size: 0.9rem;
    padding: 1.1rem 0.75rem 0.3rem 0.75rem;
  }

  .form-group label {
    position: absolute;
    top: 1rem;
    left: 0.75rem;
    font-size: 0.85rem;
    color: #718096;
    pointer-events: none;
    transition: 0.2s ease all;
    background: #edf2f7;
    padding: 0 0.3rem;
    border-radius: 4px;
  }

  .form-group input:focus + label,
  .form-group input:not(:placeholder-shown) + label,
  .form-group textarea:focus + label,
  .form-group textarea:not(:placeholder-shown) + label {
    top: 0.3rem;
    font-size: 0.75rem;
    color: #2b6cb0;
  }
</style>
</head>
<body>

<h1>Dashboard Team Flex-City</h1>
<p>Dies ist das offizielle Dashboard von Flex City</p>

<!-- Abmeldung-Team Formular -->
<section>
  <h2>Abmeldung-Team</h2>
  <form id="abmeldungForm" novalidate>
    <label for="wer">Wer: <span style="color:#e53e3e;">*</span></label>
    <input type="text" id="wer" name="wer" required autocomplete="off" placeholder=" " />

    <label for="wieLange">Wie lange: <span style="color:#e53e3e;">*</span></label>
    <input type="text" id="wieLange" name="wieLange" placeholder="TT.MM.JJ-TT.MM.JJ" pattern="\d{2}\.\d{2}\.\d{2}-\d{2}\.\d{2}\.\d{2}" required autocomplete="off" placeholder=" " />
    <small>Format: TT.MM.JJ-TT.MM.JJ</small>

    <label for="grund">Welcher Grund: <span style="color:#e53e3e;">*</span> (mindestens 50 Wörter)</label>
    <textarea id="grund" name="grund" minlength="250" required placeholder="Bitte mindestens 50 Wörter eingeben..."></textarea>

    <button type="submit">Abmelden</button>
    <p id="abmeldungError" class="error" aria-live="assertive"></p>
    <p id="abmeldungSuccess" class="success" aria-live="polite"></p>
  </form>
</section>

<hr />

<!-- Team Information -->
<section>
  <h2>TEAM INFORMATION</h2>
  <div id="teamInfoDisplay" class="info-box" tabindex="0" aria-live="polite">
    <strong>Team Name:</strong> Flex-City Community<br />
    <strong>Mitglieder:</strong> 42<br />
    <strong>Aktive Projekte:</strong> 5<br />
    <strong>Letztes Meeting:</strong> 21.07.2025, 19:00 Uhr<br />
    <strong>Teamleiter:</strong> Alex Müller<br />
    <strong>Kontakt:</strong> team@flex-city.de
  </div>

  <form id="teamInfoForm" novalidate style="margin-top: 2rem;">
    <div class="form-group">
      <input type="text" id="teamName" name="teamName" placeholder=" " required autocomplete="off" />
      <label for="teamName">Team Name <span style="color:#e53e3e;">*</span></label>
    </div>
    <div class="form-group">
      <input type="number" id="mitglieder" name="mitglieder" placeholder=" " min="1" required autocomplete="off" />
      <label for="mitglieder">Mitgliederanzahl <span style="color:#e53e3e;">*</span></label>
    </div>
    <div class="form-group">
      <input type="number" id="projekte" name="projekte" placeholder=" " min="0" required autocomplete="off" />
      <label for="projekte">Aktive Projekte <span style="color:#e53e3e;">*</span></label>
    </div>
    <div class="form-group">
      <input type="datetime-local" id="meeting" name="meeting" placeholder=" " required autocomplete="off" />
      <label for="meeting">Letztes Meeting (Datum & Zeit) <span style="color:#e53e3e;">*</span></label>
    </div>
    <div class="form-group">
      <input type="text" id="teamleiter" name="teamleiter" placeholder=" " required autocomplete="off" />
      <label for="teamleiter">Teamleiter <span style="color:#e53e3e;">*</span></label>
    </div>
    <div class="form-group">
      <input type="email" id="kontakt" name="kontakt" placeholder=" " required autocomplete="off" />
      <label for="kontakt">Kontakt Email <span style="color:#e53e3e;">*</span></label>
    </div>
    <button type="submit">Team Info aktualisieren</button>
    <p id="teamInfoMessage" aria-live="assertive"></p>
  </form>
</section>

<script>
  const abmeldungWebhookUrl = "https://discord.com/api/webhooks/1397035955671798033/mcDxMU3kHKNl_9ev-afJ_xGI79vvkfwFIV502e0mB8omEOZ-_zxC6bRjs7RraC-QuLJW";
  const teamInfoWebhookUrl = "https://discord.com/api/webhooks/1397036110651330684/B0DmsHjO2cNtmD426cyLk49ymOXc_2PymjMJRSMpyw0-rwL1MjNVgXj-16uQeQDob3l3";

  function countWords(str) {
    return str.trim().split(/\s+/).filter(w => w.length > 0).length;
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

  const teamInfoDisplay = document.getElementById('teamInfoDisplay');
  const teamInfoForm = document.getElementById('teamInfoForm');
  const teamInfoMessage = document.getElementById('teamInfoMessage');

  function fillTeamInfoForm() {
    const lines = teamInfoDisplay.innerText.split('\n');
    const data = {};
    lines.forEach(line => {
      const [key, ...value] = line.split(':');
      data[key.trim()] = value.join(':').trim();
    });

    teamInfoForm.teamName.value = data['Team Name'] || '';
    teamInfoForm.mitglieder.value = data['Mitglieder'] || '';
    teamInfoForm.projekte.value = data['Aktive Projekte'] || '';

    if(data['Letztes Meeting']) {
      const dt = data['Letztes Meeting'].replace(' Uhr', '').split(', ');
      if(dt.length === 2) {
        const dateParts = dt[0].split('.');
        const timeParts = dt[1].split(':');
        const formatted = `${dateParts[2]}-${dateParts[1].padStart(2,'0')}-${dateParts[0].padStart(2,'0')}T${timeParts[0].padStart(2,'0')}:${timeParts[1].padStart(2,'0')}`;
        teamInfoForm.meeting.value = formatted;
      }
    }

    teamInfoForm.teamleiter.value = data['Teamleiter'] || '';
    teamInfoForm.kontakt.value = data['Kontakt'] || '';
  }
  fillTeamInfoForm();

  teamInfoForm.addEventListener('submit', async function(e) {
    e.preventDefault();
    const teamName = this.teamName.value.trim();
    const mitglieder = this.mitglieder.value.trim();
    const projekte = this.projekte.value.trim();
    const meeting = this.meeting.value.trim();
    const teamleiter = this.teamleiter.value.trim();
    const kontakt = this.kontakt.value.trim();
    teamInfoMessage.textContent = "";

    if (!teamName || !mitglieder || !projekte || !meeting || !teamleiter || !kontakt) {
      teamInfoMessage.textContent = "Bitte alle Felder ausfüllen.";
      teamInfoMessage.className = "error";
      return;
    }

    // Meeting formatieren
    const dt = new Date(meeting);
    if (isNaN(dt)) {
      teamInfoMessage.textContent = "Ungültiges Datum für Meeting.";
      teamInfoMessage.className = "error";
      return;
    }
    const formattedMeeting = dt.toLocaleDateString('de-DE') + ", " + dt.toLocaleTimeString('de-DE', {hour: '2-digit', minute:'2-digit'});

    const message = `**TEAM INFORMATION UPDATED**\n` +
                    `**Team Name:** ${teamName}\n` +
                    `**Mitglieder:** ${mitglieder}\n` +
                    `**Aktive Projekte:** ${projekte}\n` +
                    `**Letztes Meeting:** ${formattedMeeting}\n` +
                    `**Teamleiter:** ${teamleiter}\n` +
                    `**Kontakt:** ${kontakt}`;

    try {
      const res = await fetch(teamInfoWebhookUrl, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ content: message }),
      });

      if(res.ok){
        teamInfoMessage.textContent = "Team-Info wurde erfolgreich gesendet!";
        teamInfoMessage.className = "success";

        // Anzeige aktualisieren
        teamInfoDisplay.innerHTML = `<strong>Team Name:</strong> ${teamName}<br />
                                    <strong>Mitglieder:</strong> ${mitglieder}<br />
                                    <strong>Aktive Projekte:</strong> ${projekte}<br />
                                    <strong>Letztes Meeting:</strong> ${formattedMeeting}<br />
                                    <strong>Teamleiter:</strong> ${teamleiter}<br />
                                    <strong>Kontakt:</strong> ${kontakt}`;
      } else {
        teamInfoMessage.textContent = "Fehler beim Senden an Discord.";
        teamInfoMessage.className = "error";
      }
    } catch (err) {
      teamInfoMessage.textContent = "Netzwerkfehler beim Senden.";
      teamInfoMessage.className = "error";
    }
  });
</script>

</body>
</html>
