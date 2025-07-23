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
  .hidden {
    display: none;
  }
  .pass-section {
    background: #222;
    padding: 1rem;
    border-radius: 6px;
    margin-bottom: 1rem;
  }
  .small-note {
    font-size: 0.85rem;
    color: #bbb;
  }
</style>
</head>
<body>

  <h1>Dashboard Team Flex-City</h1>
  <p>Offizielles Team Dashboard von Flex City</p>

  <!-- Geplante Meetings Anzeige -->
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

  <hr />

  <!-- Passwort geschützter Bereich zum Ansehen der Teammitglieder & Banns -->
  <section>
    <h2>🔒 Geschützter Bereich: Team & Banns ansehen</h2>
    <div class="pass-section">
      <label for="viewPass">Passwort eingeben (Anzeige):</label>
      <input type="password" id="viewPass" autocomplete="off" />
      <button id="viewPassBtn">Freischalten</button>
      <p id="viewPassError" class="error"></p>
    </div>

    <div id="secureView" class="hidden">
      <h3>Team Mitglieder</h3>
      <ul id="teamMembersList">
        <li><strong>Owner:</strong> [Flex City] KitBary_YT</li>
        <li><strong>Community Manager:</strong> Flex City Paul</li>
        <li><strong>Head Admin:</strong> Keine Mitglieder</li>
        <li><strong>Normaler Admin:</strong> Keine Mitglieder</li>
        <li><strong>Supportleitung:</strong> Keine Mitglieder</li>
        <li><strong>Supporter:</strong> Keine Mitglieder</li>
        <li><strong>Builder:</strong> Keine Mitglieder</li>
        <li><strong>Tester:</strong> Keine Mitglieder</li>
      </ul>

      <h3>Banns</h3>
      <ul id="banList">
        <li>Keine Banns vorhanden.</li>
      </ul>
    </div>
  </section>

  <hr />

  <!-- Passwort geschützter Bereich zum Ändern der Team Mitglieder & Banns -->
  <section>
    <h2>🔐 Geschützter Bereich: Team & Banns bearbeiten</h2>
    <div class="pass-section">
      <label for="editPass">Passwort eingeben (Bearbeiten):</label>
      <input type="password" id="editPass" autocomplete="off" />
      <button id="editPassBtn">Freischalten</button>
      <p id="editPassError" class="error"></p>
    </div>

    <div id="secureEdit" class="hidden">
      <h3>Team Mitglieder hinzufügen</h3>
      <form id="teamAddForm">
        <label for="roleName">Rolle:</label>
        <input type="text" id="roleName" placeholder="z.B. Supporter" autocomplete="off" required />
        <label for="memberName">Name:</label>
        <input type="text" id="memberName" placeholder="z.B. MaxMustermann" autocomplete="off" required />
        <button type="submit">Hinzufügen</button>
      </form>

      <h3>Banns hinzufügen</h3>
      <form id="banAddForm">
        <label for="banName">Name des Gebannten:</label>
        <input type="text" id="banName" placeholder="z.B. Troll123" autocomplete="off" required />
        <label for="banGrund">Grund:</label>
        <textarea id="banGrund" placeholder="Grund des Banns" required></textarea>
        <button type="submit">Bann hinzufügen</button>
      </form>
    </div>
  </section>

  <hr />

  <!-- Abmelden Button -->
  <section>
    <button id="logoutBtn" style="background:#ff6b6b; color:#fff;">Abmelden</button>
  </section>

<script>
  // --- Lokaler Speicher Helfer ---
  const STORAGE_KEYS = {
    abmeldungen: 'flexcity_abmeldungen',
    teamInfo: 'flexcity_teamInfo',
    meetings: 'flexcity_meetings',
    abstimmungen: 'flexcity_abstimmungen',
    kummer: 'flexcity_kummer',
    teamMembers: 'flexcity_teamMembers',
    bans: 'flexcity_bans'
  };

  // Lade Daten aus localStorage oder Default
  function loadData(key, defaultValue) {
    const data = localStorage.getItem(key);
    if (data) return JSON.parse(data);
    return defaultValue;
  }
  // Speichern
  function saveData(key, value) {
    localStorage.setItem(key, JSON.stringify(value));
  }

  // --- Abmeldung-Formular Logik ---
  const abmeldungForm = document.getElementById('abmeldungForm');
  const abmeldungError = document.getElementById('abmeldungError');
  const abmeldungSuccess = document.getElementById('abmeldungSuccess');

  let abmeldungen = loadData(STORAGE_KEYS.abmeldungen, []);

  abmeldungForm.addEventListener('submit', e => {
    e.preventDefault();
    abmeldungError.textContent = '';
    abmeldungSuccess.textContent = '';

    const wer = abmeldungForm.wer.value.trim();
    const von = abmeldungForm.von.value;
    const bis = abmeldungForm.bis.value;
    const grund = abmeldungForm.grund.value.trim();

    if (!wer || !von || !bis || !grund) {
      abmeldungError.textContent = 'Bitte alle Pflichtfelder ausfüllen.';
      return;
    }

    // Mindestens 50 Wörter prüfen
    if (grund.split(/\s+/).length < 50) {
      abmeldungError.textContent = 'Der Grund muss mindestens 50 Wörter enthalten.';
      return;
    }

    abmeldungen.push({ wer, von, bis, grund });
    saveData(STORAGE_KEYS.abmeldungen, abmeldungen);

    abmeldungSuccess.textContent = `Abmeldung von ${wer} erfolgreich eingetragen für den Zeitraum von ${von} bis ${bis}.`;
    abmeldungForm.reset();
  });

  // --- Team Information Logik ---
  const teamInfoForm = document.getElementById('teamInfoForm');
  const teamInfoBox = document.getElementById('teamInfoBox');
  const teamInfoError = document.getElementById('teamInfoError');
  const teamInfoSuccess = document.getElementById('teamInfoSuccess');

  let teamInfo = loadData(STORAGE_KEYS.teamInfo, null);

  function renderTeamInfo() {
    if (!teamInfo) {
      teamInfoBox.innerHTML = 'Keine Verfügbar';
      return;
    }
    teamInfoBox.innerHTML = `<h3>${teamInfo.ueberschrift}</h3><p>${teamInfo.haupttext.replace(/\n/g, '<br>')}</p><p><em>Geschrieben von: ${teamInfo.geschriebenVon}</em></p>`;
  }
  renderTeamInfo();

  teamInfoForm.addEventListener('submit', e => {
    e.preventDefault();
    teamInfoError.textContent = '';
    teamInfoSuccess.textContent = '';

    const ueberschrift = teamInfoForm.ueberschrift.value.trim();
    const haupttext = teamInfoForm.haupttext.value.trim();
    const geschriebenVon = teamInfoForm.geschriebenVon.value.trim();

    if (!ueberschrift || !haupttext || !geschriebenVon) {
      teamInfoError.textContent = 'Bitte alle Pflichtfelder ausfüllen.';
      return;
    }

    teamInfo = { ueberschrift, haupttext, geschriebenVon };
    saveData(STORAGE_KEYS.teamInfo, teamInfo);
    renderTeamInfo();

    teamInfoSuccess.textContent = 'Team Information erfolgreich aktualisiert.';
    teamInfoForm.reset();
  });

  // --- Meetings Logik ---
  const meetingForm = document.getElementById('meetingForm');
  const meetingListContent = document.getElementById('meetingListContent');
  const meetingError = document.getElementById('meetingError');
  const meetingSuccess = document.getElementById('meetingSuccess');

  let meetings = loadData(STORAGE_KEYS.meetings, []);

  meetingForm.addEventListener('submit', e => {
    e.preventDefault();
    meetingError.textContent = '';
    meetingSuccess.textContent = '';

    const datum = meetingForm.meetingDatum.value;
    const grund = meetingForm.meetingGrund.value.trim();
    const leiter = meetingForm.meetingLeiter.value.trim();

    if (!datum || !grund || !leiter) {
      meetingError.textContent = 'Bitte alle Pflichtfelder ausfüllen.';
      return;
    }

    meetings.push({ datum, grund, leiter });
    saveData(STORAGE_KEYS.meetings, meetings);
    updateMeetingList();
    meetingSuccess.textContent = 'Meeting erfolgreich eingetragen.';
    meetingForm.reset();
  });

  function updateMeetingList() {
    if (meetings.length === 0) {
      meetingListContent.textContent = 'Keine Meetings eingetragen.';
      return;
    }
    meetings.sort((a,b) => new Date(a.datum) - new Date(b.datum));
    let html = '';
    for (const m of meetings) {
      const dateStr = new Date(m.datum).toLocaleString('de-DE', { dateStyle:'short', timeStyle:'short' });
      html += `<p>📅 <strong>${dateStr}</strong>: ${m.grund} (Leiter: ${m.leiter})</p>`;
    }
    meetingListContent.innerHTML = html;
  }
  updateMeetingList();

  // --- Abstimmung Logik ---
  const abstimmungForm = document.getElementById('abstimmungForm');
  const abstimmungError = document.getElementById('abstimmungError');
  const abstimmungSuccess = document.getElementById('abstimmungSuccess');

  let abstimmungen = loadData(STORAGE_KEYS.abstimmungen, []);

  abstimmungForm.addEventListener('submit', e => {
    e.preventDefault();
    abstimmungError.textContent = '';
    abstimmungSuccess.textContent = '';

    const was = abstimmungForm.abstimmungWas.value.trim();
    const zusatz = abstimmungForm.abstimmungZusatz.value.trim();

    if (!was) {
      abstimmungError.textContent = 'Bitte das Thema der Abstimmung eingeben.';
      return;
    }

    abstimmungen.push({ was, zusatz, zeit: new Date().toISOString() });
    saveData(STORAGE_KEYS.abstimmungen, abstimmungen);
    abstimmungSuccess.textContent = 'Abstimmung erfolgreich eingetragen.';
    abstimmungForm.reset();
  });

  // --- Kummerkasten Logik ---
  const kummerForm = document.getElementById('kummerForm');
  const kummerNachricht = document.getElementById('kummerNachricht');
  const kummerListe = document.getElementById('kummerListe');
  const kummerError = document.getElementById('kummerError');

  let kummerMessages = loadData(STORAGE_KEYS.kummer, []);

  kummerForm.addEventListener('submit', e => {
    e.preventDefault();
    kummerError.textContent = '';
    const msg = kummerNachricht.value.trim();
    if (!msg) {
      kummerError.textContent = 'Bitte eine Nachricht eingeben.';
      return;
    }
    kummerMessages.push({ text: msg, zeit: new Date().toLocaleString() });
    saveData(STORAGE_KEYS.kummer, kummerMessages);
    renderKummer();
    kummerNachricht.value = '';
  });

  function renderKummer() {
    if (kummerMessages.length === 0) {
      kummerListe.innerHTML = '<p>Keine Nachrichten.</p>';
      return;
    }
    let html = '';
    for (const m of kummerMessages) {
      html += `<div style="border-bottom:1px solid #444; margin-bottom:0.5rem; padding-bottom:0.5rem;">
      <small>${m.zeit}</small><br />${m.text}</div>`;
    }
    kummerListe.innerHTML = html;
  }
  renderKummer();

  // --- Team Mitglieder & Banns Speicher und Darstellung ---
  let teamMembers = loadData(STORAGE_KEYS.teamMembers, {
    "Owner": ["[Flex City] KitBary_YT"],
    "Community Manager": ["Flex City Paul"],
    "Head Admin": [],
    "Normaler Admin": [],
    "Supportleitung": [],
    "Supporter": [],
    "Builder": [],
    "Tester": []
  });

  let bans = loadData(STORAGE_KEYS.bans, []);

  const teamMembersList = document.getElementById('teamMembersList');
  const banList = document.getElementById('banList');

  function renderTeamAndBans() {
    // Team Mitglieder anzeigen
    teamMembersList.innerHTML = '';
    for (const role in teamMembers) {
      const members = teamMembers[role];
      const displayMembers = members.length ? members.join(', ') : 'Keine Mitglieder';
      const li = document.createElement('li');
      li.innerHTML = `<strong>${role}:</strong> ${displayMembers}`;
      teamMembersList.appendChild(li);
    }

    // Banns anzeigen
    banList.innerHTML = '';
    if (bans.length === 0) {
      banList.innerHTML = '<li>Keine Banns vorhanden.</li>';
    } else {
      for (const b of bans) {
        const li = document.createElement('li');
        li.textContent = `${b.name} - Grund: ${b.grund}`;
        banList.appendChild(li);
      }
    }
  }
  renderTeamAndBans();

  // --- Passwort Bereiche ---
  const viewPassInput = document.getElementById('viewPass');
  const viewPassBtn = document.getElementById('viewPassBtn');
  const viewPassError = document.getElementById('viewPassError');
  const secureView = document.getElementById('secureView');

  const editPassInput = document.getElementById('editPass');
  const editPassBtn = document.getElementById('editPassBtn');
  const editPassError = document.getElementById('editPassError');
  const secureEdit = document.getElementById('secureEdit');

  // Passwort Konstanten
  const VIEW_PASS = '2012';
  const EDIT_PASS = 'FlexCity';

  // View Bereich Passwort Check
  viewPassBtn.addEventListener('click', () => {
    const pass = viewPassInput.value.trim();
    if (pass === VIEW_PASS) {
      secureView.classList.remove('hidden');
      viewPassError.textContent = '';
      viewPassInput.value = '';
    } else {
      viewPassError.textContent = 'Falsches Passwort!';
      secureView.classList.add('hidden');
    }
  });

  // Edit Bereich Passwort Check
  editPassBtn.addEventListener('click', () => {
    const pass = editPassInput.value.trim();
    if (pass === EDIT_PASS) {
      secureEdit.classList.remove('hidden');
      editPassError.textContent = '';
      editPassInput.value = '';
    } else {
      editPassError.textContent = 'Falsches Passwort!';
      secureEdit.classList.add('hidden');
    }
  });

  // --- Team Mitglieder hinzufügen ---
  const teamAddForm = document.getElementById('teamAddForm');

  teamAddForm.addEventListener('submit', e => {
    e.preventDefault();

    const role = document.getElementById('roleName').value.trim();
    const name = document.getElementById('memberName').value.trim();

    if (!role || !name) return;

    if (!teamMembers[role]) {
      teamMembers[role] = [];
    }
    teamMembers[role].push(name);
    saveData(STORAGE_KEYS.teamMembers, teamMembers);

    renderTeamAndBans();
    teamAddForm.reset();
  });

  // --- Banns hinzufügen ---
  const banAddForm = document.getElementById('banAddForm');

  banAddForm.addEventListener('submit', e => {
    e.preventDefault();

    const name = document.getElementById('banName').value.trim();
    const grund = document.getElementById('banGrund').value.trim();

    if (!name || !grund) return;

    bans.push({ name, grund });
    saveData(STORAGE_KEYS.bans, bans);

    renderTeamAndBans();
    banAddForm.reset();
  });

  // --- Abmelden Button ---
  const logoutBtn = document.getElementById('logoutBtn');

  logoutBtn.addEventListener('click', () => {
    secureView.classList.add('hidden');
    secureEdit.classList.add('hidden');
    viewPassInput.value = '';
    editPassInput.value = '';
    viewPassError.textContent = '';
    editPassError.textContent = '';
  });

</script>
</body>
</html>
