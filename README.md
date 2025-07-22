<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Flex-City Team Dashboard – Premium Edition</title>

<!-- Google Fonts -->
<link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;600&family=Roboto+Mono&display=swap" rel="stylesheet" />

<style>
  /* Reset */
  *, *::before, *::after {
    box-sizing: border-box;
  }
  body {
    margin: 0; padding: 0;
    font-family: 'Montserrat', sans-serif;
    background: linear-gradient(135deg, #1b1b1b 0%, #2f2f2f 100%);
    color: #eee;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 2rem 1rem;
    transition: background 0.5s ease;
  }

  /* Container */
  .container {
    background: #222;
    border-radius: 16px;
    box-shadow:
      0 8px 24px rgba(0,0,0,0.8),
      inset 0 0 40px #3ab795cc;
    max-width: 900px;
    width: 100%;
    padding: 2.5rem 3rem;
    color: #b2f7ef;
  }

  h1 {
    font-weight: 700;
    font-size: 2.75rem;
    margin-bottom: 0.3rem;
    text-align: center;
    color: #54f0c2;
    text-shadow: 0 0 10px #2ec6a3;
  }
  p.subtitle {
    font-weight: 400;
    font-size: 1.1rem;
    color: #88d6ce;
    text-align: center;
    margin-bottom: 3rem;
    letter-spacing: 0.04em;
  }

  /* Tabs */
  .tabs {
    display: flex;
    gap: 2rem;
    justify-content: center;
    margin-bottom: 2.5rem;
  }
  .tab {
    cursor: pointer;
    padding: 0.75rem 2rem;
    border-radius: 40px;
    font-weight: 600;
    color: #3ec3af;
    background: #122e2a;
    box-shadow:
      0 0 15px #3ec3af66;
    transition: background-color 0.3s ease, color 0.3s ease;
    user-select: none;
  }
  .tab.active {
    background: #54f0c2;
    color: #0d201b;
    box-shadow:
      0 0 20px #54f0c2ff,
      inset 0 0 30px #54f0c2cc;
  }

  /* Forms */
  form {
    max-width: 650px;
    margin: 0 auto;
  }

  /* Form groups with floating labels */
  .form-group {
    position: relative;
    margin-bottom: 2.5rem;
  }
  .form-group input,
  .form-group textarea {
    width: 100%;
    background: #1a3a36;
    border: 2px solid #2ea99d;
    border-radius: 12px;
    padding: 1rem 1.2rem 1rem 1.2rem;
    font-size: 1rem;
    color: #b2f7ef;
    outline: none;
    resize: vertical;
    transition: border-color 0.3s ease;
    font-family: 'Roboto Mono', monospace;
  }
  .form-group textarea {
    min-height: 120px;
  }
  .form-group input:focus,
  .form-group textarea:focus {
    border-color: #54f0c2;
    box-shadow: 0 0 12px #54f0c2aa;
  }

  /* Floating labels */
  label {
    position: absolute;
    top: 50%;
    left: 1.3rem;
    transform: translateY(-50%);
    background: #222;
    padding: 0 0.4rem;
    color: #69bfb1cc;
    font-weight: 600;
    font-size: 0.9rem;
    pointer-events: none;
    transition: all 0.3s ease;
    user-select: none;
  }
  input:focus + label,
  input:not(:placeholder-shown) + label,
  textarea:focus + label,
  textarea:not(:placeholder-shown) + label {
    top: -0.6rem;
    left: 1rem;
    color: #54f0c2;
    font-size: 0.75rem;
  }

  /* Buttons */
  button {
    background: #54f0c2;
    border: none;
    padding: 1rem 2.8rem;
    font-weight: 700;
    color: #0d201b;
    border-radius: 50px;
    font-size: 1.1rem;
    cursor: pointer;
    box-shadow:
      0 4px 15px #54f0c2aa,
      inset 0 0 10px #2ea99dcc;
    transition: background-color 0.25s ease, box-shadow 0.25s ease;
    display: block;
    margin: 2rem auto 0 auto;
  }
  button:hover {
    background: #3ec3af;
    box-shadow:
      0 6px 20px #3ec3afdd,
      inset 0 0 15px #27a494cc;
  }

  /* Error and success messages */
  .message {
    max-width: 650px;
    margin: 0.7rem auto 0 auto;
    text-align: center;
    font-weight: 600;
    user-select: none;
  }
  .error {
    color: #ff6b6b;
  }
  .success {
    color: #9fff5c;
  }

  /* Info box */
  .info-box {
    background: #11332e;
    border-radius: 14px;
    padding: 1.8rem 2rem;
    box-shadow: inset 0 0 15px #2ea99dcc;
    color: #89f5d6;
    font-family: 'Roboto Mono', monospace;
    font-size: 1rem;
    margin-bottom: 3rem;
    white-space: pre-wrap;
  }

  /* Stats section */
  .stats {
    display: flex;
    justify-content: space-around;
    margin-bottom: 2.5rem;
  }
  .stat {
    background: #1f5d50;
    padding: 1rem 1.5rem;
    border-radius: 12px;
    text-align: center;
    box-shadow: 0 0 10px #54f0c2aa;
    flex: 1;
    margin: 0 0.75rem;
  }
  .stat h3 {
    margin: 0 0 0.3rem 0;
    font-size: 1.5rem;
    color: #a4f7d8;
  }
  .stat p {
    margin: 0;
    font-weight: 600;
  }

  /* Responsive */
  @media (max-width: 720px) {
    .stats {
      flex-direction: column;
      gap: 1.2rem;
    }
    .stat {
      margin: 0;
    }
  }

  /* Dark Mode Toggle */
  .dark-toggle {
    position: fixed;
    top: 1rem;
    right: 1rem;
    background: #222;
    border: 2px solid #54f0c2;
    color: #54f0c2;
    padding: 0.5rem 1rem;
    border-radius: 24px;
    font-weight: 700;
    cursor: pointer;
    user-select: none;
    box-shadow: 0 0 10px #54f0c2aa;
    transition: all 0.3s ease;
  }
  .dark-toggle:hover {
    background: #54f0c2;
    color: #222;
    box-shadow: 0 0 20px #54f0c2ff;
  }

  /* Dark Mode Styles */
  body.dark {
    background: linear-gradient(135deg, #0a0a0a 0%, #141414 100%);
    color: #ddd;
  }
  body.dark .container {
    background: #111;
    box-shadow:
      0 8px 24px rgba(0,0,0,0.9),
      inset 0 0 40px #0cf8caaa;
    color: #a6fff1;
  }
  body.dark .tab {
    background: #0c3834;
    color: #0cf8ca;
    box-shadow: 0 0 15px #0cf8ca66;
  }
  body.dark .tab.active {
    background: #0cf8ca;
    color: #01120f;
    box-shadow: 0 0 20px #0cf8caff, inset 0 0 30px #0cf8caaa;
  }
  body.dark input, body.dark textarea {
    background: #0e3b36;
    border-color: #0cf8ca;
    color: #a6fff1;
    text-shadow: 0 0 6px #0cf8caaa;
  }
  body.dark input:focus, body.dark textarea:focus {
    border-color: #0ff8d3;
    box-shadow: 0 0 16px #0ff8d3cc;
  }
  body.dark label {
    color: #0cf8caaa;
  }
  body.dark label:focus, body.dark input:focus + label, body.dark textarea:focus + label {
    color: #0ff8d3;
  }
  body.dark button {
    background: #0cf8ca;
    color: #01120f;
    box-shadow: 0 4px 15px #0cf8caff, inset 0 0 12px #0cf8caaa;
  }
  body.dark button:hover {
    background: #0aafa1;
    box-shadow: 0 6px 20px #0aafa1dd, inset 0 0 15px #0aafa1cc;
  }
  body.dark .info-box {
    background: #06332e;
    box-shadow: inset 0 0 20px #0cf8caaa;
    color: #8fffea;
  }
  body.dark .stats .stat {
    background: #054a44;
    box-shadow: 0 0 12px #0cf8caaa;
    color: #9ff7e6;
  }
</style>
</head>
<body>

<div class="dark-toggle" id="darkToggle">Dark Mode</div>

<div class="container">
  <h1>Flex-City Team Dashboard</h1>
  <p class="subtitle">Das exklusive Management-Dashboard für Flex-City Teammitglieder</p>

  <nav class="tabs" aria-label="Navigation">
    <div class="tab active" data-tab="abmeldung" tabindex="0" role="button" aria-selected="true" aria-controls="abmeldungTab" id="tab-abmeldung">Abmeldung-Team</div>
    <div class="tab" data-tab="teaminfo" tabindex="0" role="button" aria-selected="false" aria-controls="teaminfoTab" id="tab-teaminfo">Team Informationen</div>
    <div class="tab" data-tab="stats" tabindex="0" role="button" aria-selected="false" aria-controls="statsTab" id="tab-stats">Team Statistik</div>
  </nav>

  <!-- Abmeldung -->
  <section id="abmeldungTab" role="tabpanel" aria-labelledby="tab-abmeldung">
    <form id="abmeldungForm" novalidate>
      <div class="form-group">
        <input type="text" id="wer" name="wer" placeholder=" " required autocomplete="off" />
        <label for="wer">Wer meldet sich ab?</label>
      </div>
      <div class="form-group">
        <input type="text" id="warum" name="warum" placeholder=" " required autocomplete="off" />
        <label for="warum">Warum?</label>
      </div>
      <div class="form-group">
        <textarea id="zusatzinfo" name="zusatzinfo" placeholder=" "></textarea>
        <label for="zusatzinfo">Zusätzliche Infos (optional)</label>
      </div>
      <button type="submit">Abmelden</button>
      <div id="formMessage" class="message" role="alert" aria-live="polite"></div>
    </form>
  </section>

  <!-- Teaminfo -->
  <section id="teaminfoTab" role="tabpanel" aria-labelledby="tab-teaminfo" hidden>
    <div class="info-box" tabindex="0">
      <strong>Team Name:</strong> Flex-City Community<br />
      <strong>Mitglieder:</strong> 42<br />
      <strong>Aktive Projekte:</strong> 5<br />
      <strong>Letztes Meeting:</strong> 21.07.2025, 19:00 Uhr<br />
      <strong>Teamleiter:</strong> Alex Müller<br />
      <strong>Kontakt:</strong> team@flex-city.de
    </div>
  </section>

  <!-- Stats -->
  <section id="statsTab" role="tabpanel" aria-labelledby="tab-stats" hidden>
    <div class="stats" tabindex="0" aria-label="Team Statistik">
      <div class="stat">
        <h3>42</h3>
        <p>Mitglieder</p>
      </div>
      <div class="stat">
        <h3>5</h3>
        <p>Projekte</p>
      </div>
      <div class="stat">
        <h3>89%</h3>
        <p>Aktive Teilnahme</p>
      </div>
    </div>
  </section>
</div>

<script>
  // Tab navigation
  const tabs = document.querySelectorAll('.tab');
  const sections = {
    abmeldung: document.getElementById('abmeldungTab'),
    teaminfo: document.getElementById('teaminfoTab'),
    stats: document.getElementById('statsTab')
  };

  tabs.forEach(tab => {
    tab.addEventListener('click', () => switchTab(tab));
    tab.addEventListener('keydown', e => {
      if (e.key === 'Enter' || e.key === ' ') {
        e.preventDefault();
        switchTab(tab);
      }
    });
  });

  function switchTab(activeTab) {
    tabs.forEach(t => {
      t.classList.remove('active');
      t.setAttribute('aria-selected', 'false');
      sections[t.dataset.tab].hidden = true;
    });
    activeTab.classList.add('active');
    activeTab.setAttribute('aria-selected', 'true');
    sections[activeTab.dataset.tab].hidden = false;
  }

  // Form validation and confirmation
  const form = document.getElementById('abmeldungForm');
  const formMessage = document.getElementById('formMessage');

  form.addEventListener('submit', e => {
    e.preventDefault();
    formMessage.textContent = '';
    formMessage.className = 'message';

    const wer = form.wer.value.trim();
    const warum = form.warum.value.trim();

    if (!wer || !warum) {
      formMessage.textContent = 'Bitte füllen Sie alle Pflichtfelder aus.';
      formMessage.classList.add('error');
      return;
    }

    if (wer.length < 3) {
      formMessage.textContent = 'Bitte geben Sie einen gültigen Namen ein (mindestens 3 Zeichen).';
      formMessage.classList.add('error');
      return;
    }
    if (warum.length < 5) {
      formMessage.textContent = 'Bitte geben Sie einen ausführlichen Grund an (mindestens 5 Zeichen).';
      formMessage.classList.add('error');
      return;
    }

    // Confirmation
    const confirmMsg = `Sind Sie sicher, dass Sie sich abmelden möchten?\n\nWer: ${wer}\nWarum: ${warum}\nZusätzliche Infos: ${form.zusatzinfo.value.trim() || '(keine)'}`;
    if (!confirm(confirmMsg)) {
      return;
    }

    // Simulate submission
    formMessage.textContent = 'Ihre Abmeldung wurde erfolgreich übermittelt.';
    formMessage.classList.add('success');
    form.reset();
  });

  // Dark mode toggle
  const darkToggle = document.getElementById('darkToggle');
  darkToggle.addEventListener('click', () => {
    document.body.classList.toggle('dark');
    if (document.body.classList.contains('dark')) {
      darkToggle.textContent = 'Light Mode';
    } else {
      darkToggle.textContent = 'Dark Mode';
    }
  });
</script>

</body>
</html>
