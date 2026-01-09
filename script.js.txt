/* ===============================
   VARIABLA GLOBALE
================================ */

let currentLevel = 0;
let unlockedLevels = [true, false, false, false, false];
let currentWord = null;
let userAnswer = "";

/* ===============================
   ELEMENTE DOM
================================ */

const map = document.getElementById("map");
const levelBox = document.getElementById("levelBox");
const levelTitle = document.getElementById("levelTitle");
const levelContent = document.getElementById("levelContent");

/* ===============================
   FUNKSIONE BAZË
================================ */

// Merr një fjalë random nga databaza
function merrFjaleRandom() {
  const index = Math.floor(Math.random() * FJALOR.length);
  return FJALOR[index];
}

// Vizaton hartën e niveleve
function drawMap() {
  map.innerHTML = "";

  unlockedLevels.forEach((unlocked, index) => {
    const node = document.createElement("div");
    node.classList.add("node");

    if (unlocked) {
      node.classList.add("unlocked");
      node.onclick = () => openLevel(index);
    } else {
      node.classList.add("locked");
    }

    if (index === currentLevel && unlocked) {
      node.classList.add("active");
    }

    node.innerText = index + 1;
    map.appendChild(node);
  });
}

// Hap një nivel
function openLevel(levelIndex) {
  currentLevel = levelIndex;
  currentWord = merrFjaleRandom();
  userAnswer = "";

  levelBox.classList.remove("hidden");
  loadLevel();
}

/* ===============================
   NGARKIMI I NIVELEVE
================================ */

function loadLevel() {
  const titles = [
    "🧩 Rrokëzimi i fjalës",
    "📖 Kuptimi në kontekst",
    "🔁 Sinonim / Antonim",
    "✍️ Drejtshkrimi",
    "🌍 Origjina & Regjistri"
  ];

  levelTitle.innerText = titles[currentLevel];
  levelContent.innerHTML = "";

  switch (currentLevel) {
    case 0:
      levelRrokezim();
      break;
    case 1:
      levelKontekst();
      break;
    case 2:
      levelSinonim();
      break;
    case 3:
      levelDrejtshkrim();
      break;
    case 4:
      levelOrigjine();
      break;
  }
}

/* ===============================
   NIVELI 1 – RROKËZIMI
================================ */

function levelRrokezim() {
  const shuffled = [...currentWord.rrokje].sort(() => Math.random() - 0.5);

  const display = document.createElement("p");
  display.id = "assembledWord";
  display.style.fontSize = "20px";
  display.style.marginBottom = "15px";
  levelContent.appendChild(display);

  shuffled.forEach(rrokje => {
    const btn = document.createElement("button");
    btn.className = "option";
    btn.innerText = rrokje;
    btn.onclick = () => {
      userAnswer += rrokje;
      display.innerText = userAnswer;
    };
    levelContent.appendChild(btn);
  });
}

/* ===============================
   NIVELI 2 – KONTEKST
================================ */

function levelKontekst() {
  const options = [
    currentWord.shembull,
    "Kjo fjali nuk ka kuptim gjuhësor."
  ].sort(() => Math.random() - 0.5);

  options.forEach(opt => {
    const btn = document.createElement("button");
    btn.className = "option";
    btn.innerText = opt;
    btn.onclick = () => userAnswer = opt;
    levelContent.appendChild(btn);
  });
}

/* ===============================
   NIVELI 3 – SINONIM / ANTONIM
================================ */

function levelSinonim() {
  const options = [
    currentWord.sinonime[0],
    currentWord.antonime[0]
  ].sort(() => Math.random() - 0.5);

  options.forEach(opt => {
    const btn = document.createElement("button");
    btn.className = "option";
    btn.innerText = opt;
    btn.onclick = () => userAnswer = opt;
    levelContent.appendChild(btn);
  });
}

/* ===============================
   NIVELI 4 – DREJTSHKRIMI
================================ */

function levelDrejtshkrim() {
  const wrong =
    currentWord.drejtshkrim.replace("ë", "e") ||
    currentWord.drejtshkrim + "e";

  const options = [
    currentWord.drejtshkrim,
    wrong
  ].sort(() => Math.random() - 0.5);

  options.forEach(opt => {
    const btn = document.createElement("button");
    btn.className = "option";
    btn.innerText = opt;
    btn.onclick = () => userAnswer = opt;
    levelContent.appendChild(btn);
  });
}

/* ===============================
   NIVELI 5 – ORIGJINA & REGJISTRI
================================ */

function levelOrigjine() {
  const options = [
    currentWord.origjine,
    currentWord.origjine === "autoktone" ? "huazim" : "autoktone"
  ].sort(() => Math.random() - 0.5);

  options.forEach(opt => {
    const btn = document.createElement("button");
    btn.className = "option";
    btn.innerText = opt;
    btn.onclick = () => userAnswer = opt;
    levelContent.appendChild(btn);
  });
}

/* ===============================
   KONTROLLI I PËRGJIGJES
================================ */

function submitLevel() {
  let correct = false;

  switch (currentLevel) {
    case 0:
      correct = userAnswer === currentWord.fjala;
      break;
    case 1:
      correct = userAnswer === currentWord.shembull;
      break;
    case 2:
      correct = currentWord.sinonime.includes(userAnswer);
      break;
    case 3:
      correct = userAnswer === currentWord.drejtshkrim;
      break;
    case 4:
      correct = userAnswer === currentWord.origjine;
      break;
  }

  if (correct) {
    alert("✔ Saktë! Niveli u përfundua.");
    if (currentLevel < unlockedLevels.length - 1) {
      unlockedLevels[currentLevel + 1] = true;
    }
    levelBox.classList.add("hidden");
    drawMap();
  } else {
    alert("✖ Gabim. Provo përsëri.");
    userAnswer = "";
    loadLevel();
  }
}

/* ===============================
   START
================================ */

drawMap();
