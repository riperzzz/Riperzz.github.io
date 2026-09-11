<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <title>SASP Nord — Gang & Narcotics Division</title>
  <link rel="stylesheet" href="style.css">
</head>

<body>

  <header>
    <h1>SASP Nord — Gang & Narcotics Division</h1>
    <p>Tableau de gestion des enquêtes — Accréditation GND requise</p>
  </header>

  <section class="stats">
    <div class="card">Enquêtes en cours : 4</div>
    <div class="card">Classées : 12</div>
    <div class="card">Cold Cases : 3</div>
    <div class="card">Total dossiers : 19</div>
  </section>

  <section class="filters">
    <select id="filterType">
      <option value="all">Type : Tous</option>
      <option value="fusillade">Fusillade</option>
      <option value="stup">Stupéfiants</option>
      <option value="menace">Menaces de mort</option>
      <option value="gang">Gang / Organisation</option>
    </select>

    <select id="filterStatus">
      <option value="all">Statut : Tous</option>
      <option value="encours">En cours</option>
      <option value="classe">Classé</option>
      <option value="cold">Cold Case</option>
    </select>
  </section>

  <section class="cases" id="casesList">
    <!-- Les dossiers seront injectés ici via JS -->
  </section>

  <script src="script.js"></script>

</body>
</html>


body {
  margin: 0;
  font-family: Arial, sans-serif;
  background: #050b16;
  color: #e5e9f0;
}

header {
  padding: 25px;
  background: #0b1c3d;
  border-bottom: 1px solid #1f2a3c;
  text-align: center;
}

.stats {
  display: flex;
  gap: 15px;
  padding: 20px;
  flex-wrap: wrap;
}

.card {
  background: #111827;
  padding: 15px 20px;
  border-radius: 6px;
  border: 1px solid #1f2937;
  flex: 1;
  min-width: 200px;
}

.filters {
  padding: 20px;
  display: flex;
  gap: 15px;
}

select {
  background: #0f172a;
  color: #e5e9f0;
  padding: 10px;
  border: 1px solid #1f2937;
  border-radius: 4px;
}

.cases {
  padding: 20px;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 20px;
}

.case {
  background: #111827;
  border: 1px solid #1f2937;
  padding: 15px;
  border-radius: 6px;
}

.case h3 {
  margin-top: 0;
  color: #4ea1ff;
}

.status {
  font-weight: bold;
  margin-bottom: 10px;
}

const cases = [
  {
    id: "GND-2026-001",
    type: "fusillade",
    titre: "Fusillade — Quartier Nord",
    statut: "encours",
    resume: "Affrontement armé entre deux groupes rivaux. 3 blessés."
  },
  {
    id: "GND-2026-002",
    type: "stup",
    titre: "Trafic de stupéfiants — Hangar 12",
    statut: "classe",
    resume: "Saisie de 12kg de cocaïne. 2 suspects arrêtés."
  },
  {
    id: "GND-2026-003",
    type: "menace",
    titre: "Menaces de mort — Officier SASP",
    statut: "encours",
    resume: "Menaces reçues par message crypté. Source inconnue."
  },
  {
    id: "GND-2026-004",
    type: "gang",
    titre: "Organisation criminelle — 'Black Serpents'",
    statut: "cold",
    resume: "Réseau structuré actif depuis 2024. Aucune avancée récente."
  }
];

function displayCases(filterType = "all", filterStatus = "all") {
  const list = document.getElementById("casesList");
  list.innerHTML = "";

  cases
    .filter(c =>
      (filterType === "all" || c.type === filterType) &&
      (filterStatus === "all" || c.statut === filterStatus)
    )
    .forEach(c => {
      const div = document.createElement("div");
      div.className = "case";
      div.innerHTML = `
        <h3>${c.id}</h3>
        <div class="status">Statut : ${c.statut}</div>
        <strong>${c.titre}</strong>
        <p>${c.resume}</p>
      `;
      list.appendChild(div);
    });
}

document.getElementById("filterType").addEventListener("change", e => {
  displayCases(e.target.value, document.getElementById("filterStatus").value);
});

document.getElementById("filterStatus").addEventListener("change", e => {
  displayCases(document.getElementById("filterType").value, e.target.value);
});

displayCases();
