<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Dashboard Team Flex-City</title>
<style>
  /* Original Design wie von dir gewünscht */
  body {
    font-family: Arial, sans-serif;
    background-color: #222;
    color: #eee;
    max-width: 600px;
    margin: 2rem auto;
    padding: 1rem;
  }
  h1 {
    color: #90ee90;
    text-align: center;
  }
  form {
    margin-top: 1rem;
    background: #333;
    padding: 1rem;
    border-radius: 5px;
  }
  label {
    display: block;
    margin: 0.5rem 0 0.2rem;
  }
  input, textarea {
    width: 100%;
    padding: 0.5rem;
    border: none;
    border-radius: 3px;
    font-size: 1rem;
  }
  textarea {
    resize: vertical;
  }
  button {
    margin-top: 1rem;
    background-color: #90ee90;
    border: none;
    padding: 0.7rem 1.5rem;
    cursor: pointer;
    font-weight: bold;
    border-radius: 3px;
  }
  button:disabled {
    background-color: #555;
    cursor: not-allowed;
  }
  .info-box {
    margin-top: 1rem;
    background: #444;
    padding: 1rem;
    border-radius: 5px;
  }
</style>
</head>
<body>

<h1>Dashboard Team Flex-City</h1>

<section>
  <h2>TEAM INFORMATION</h2>

  <div id="teamInfoBox" class="info-box">Keine Verfügbar</div>

  <form id="teamInfoForm" novalidate>
    <label for="ueberschrift">Überschrift:</label>
    <input type="text" id="ueberschrift" name="ueberschrift" autocomplete="off" />

    <label for="haupttext">Haupttext:</label>
    <textarea id="haupttext" name="haupttext" rows="5"></textarea>

    <button type="submit">Information absenden</button>
  </form>
</section>

<script>
  // Nur minimale JS-Änderung für Team Info
  const form = document.getElementById('teamInfoForm');
  const teamInfoBox = document.getElementById('teamInfoBox');

  function renderTeamInfos(infos) {
    if (!infos.length) {
      teamInfoBox.textContent = "Keine Verfügbar";
      return;
    }
    teamInfoBox.innerHTML = '';
    infos.slice(0, 3).forEach(info => {
      const div = document.createElement('div');
      div.style.marginBottom = '1rem';

      const title = document.createElement('strong');
      title.textContent = info.ueberschrift;

      const text = document.createElement('p');
      text.textContent = info.haupttext;

      div.appendChild(title);
      div.appendChild(text);
      teamInfoBox.appendChild(div);
    });
  }

  function loadTeamInfos() {
    const stored = localStorage.getItem('teamInfos');
    if (!stored) return [];
    try {
      return JSON.parse(stored);
    } catch {
      return [];
    }
  }

  function saveTeamInfo(ueberschrift, haupttext) {
    const infos = loadTeamInfos();
    infos.unshift({ueberschrift, haupttext});
    if(infos.length > 10) infos.pop();
    localStorage.setItem('teamInfos', JSON.stringify(infos));
    renderTeamInfos(infos);
  }

  // Initial render
  renderTeamInfos(loadTeamInfos());

  form.addEventListener('submit', e => {
    e.preventDefault();
    const ueberschrift = form.ueberschrift.value.trim();
    const haupttext = form.haupttext.value.trim();

    if(!ueberschrift || !haupttext) {
      alert('Bitte Überschrift und Haupttext ausfüllen.');
      return;
    }

    saveTeamInfo(ueberschrift, haupttext);
    form.reset();
  });
</script>

</body>
</html>
