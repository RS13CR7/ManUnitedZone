# ManUnitedZone

⚠️ **Disclaimer:** This website is for personal use and entertainment.  
It is **not intended to be used during class or during work hours**. Please respect your school’s rules and only use it responsibly.

---

## About This Website

This is a personal project website designed to host and organize browser games in one convenient dashboard.  
The goal is to make it easy to quickly access games, explore new ones, and save favorites, all from a single page.

---

## Features

- ✅ **Search Bar** – Quickly find games by name  
- ✅ **Featured Section** – Highlight favorite or recommended games  
- ✅ **All Games Grid** – Browse every available game with a clean layout  
- ✅ **Favorites** – Save your favorite games for quick access  
- ✅ **Responsive Design** – Works on desktop and mobile  
- ✅ **Clean UI** – Simple and easy-to-navigate layout  

---

## How to Use

1. Click on “All Games” to see the full collection  
2. Use the search bar to filter games  
3. Click a game to launch it in the embedded player  
4. Add games to favorites for easy access later  

---

## Notes

This site is a **personal project**, and the links included are for personal entertainment only. Always follow your school or workplace guidelines when using any website.




<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Dashboard</title>

<style>
body {
  margin: 0;
  font-family: Arial, sans-serif;
  display: flex;
}

/* Sidebar */
.sidebar {
  width: 220px;
  background: #1e1e2f;
  color: white;
  height: 100vh;
  padding: 20px;
}

.sidebar h2 {
  font-size: 18px;
}

.sidebar a {
  display: block;
  color: white;
  text-decoration: none;
  margin: 10px 0;
  padding: 8px;
  border-radius: 6px;
}

.sidebar a:hover {
  background: #33334d;
}

/* Main */
.main {
  flex: 1;
  padding: 20px;
}

/* Top bar */
.topbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}

.search {
  width: 300px;
  padding: 8px;
  border-radius: 6px;
  border: 1px solid #ccc;
}

/* Game grid */
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
  gap: 15px;
}

.card {
  background: #f4f4f4;
  padding: 15px;
  border-radius: 10px;
  cursor: pointer;
  text-align: center;
}

.card:hover {
  background: #e0e0e0;
}

iframe {
  width: 100%;
  height: 500px;
  border: none;
}

.hidden {
  display: none;
}

button {
  margin-top: 10px;
  padding: 8px 12px;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}

</style>
</head>

<body>

<div class="sidebar">
  <h2>Menu</h2>
  <a onclick="showPage('home')">Home</a>
  <a onclick="showPage('all')">All Games</a>
  <a onclick="showPage('favorites')">Favorites</a>
</div>

<div class="main">
  <div class="topbar">
    <h1>Dashboard</h1>
    <input class="search" placeholder="Search..." oninput="searchGames(this.value)">
  </div>

  <!-- HOME -->
  <div id="home">
    <h2>Featured</h2>
    <div class="grid" id="featured"></div>
  </div>

  <!-- ALL GAMES -->
  <div id="all" class="hidden">
    <h2>All Games</h2>
    <div class="grid" id="games"></div>
  </div>

  <!-- FAVORITES -->
  <div id="favorites" class="hidden">
    <h2>Favorites</h2>
    <div class="grid" id="favList"></div>
  </div>

  <!-- GAME VIEW -->
  <div id="gameView" class="hidden">
    <button onclick="goBack()">⬅ Back</button>
    <h2 id="gameTitle"></h2>
    <iframe id="gameFrame"></iframe>
    <button onclick="addFavorite()">⭐ Add to Favorites</button>
  </div>

</div>

<script>
const games = [
  { name: "Game 1", url: "https://example.com" },
  { name: "Game 2", url: "https://example.com" },
  { name: "Game 3", url: "https://example.com" }
];

let currentGame = null;
let favorites = [];

function loadGames() {
  const gameContainer = document.getElementById("games");
  const featured = document.getElementById("featured");

  gameContainer.innerHTML = "";
  featured.innerHTML = "";

  games.forEach((game, index) => {
    const card = createCard(game);
    gameContainer.appendChild(card);

    if (index < 2) {
      featured.appendChild(createCard(game));
    }
  });
}

function createCard(game) {
  const div = document.createElement("div");
  div.className = "card";
  div.innerText = game.name;
  div.onclick = () => openGame(game);
  return div;
}

function openGame(game) {
  currentGame = game;
  document.getElementById("gameTitle").innerText = game.name;
  document.getElementById("gameFrame").src = game.url;

  hideAll();
  document.getElementById("gameView").classList.remove("hidden");
}

function goBack() {
  document.getElementById("gameFrame").src = "";
  showPage('home');
}

function showPage(page) {
  hideAll();
  document.getElementById(page).classList.remove("hidden");
}

function hideAll() {
  document.querySelectorAll('.main > div').forEach(div => {
    div.classList.add("hidden");
  });
}

function addFavorite() {
  if (!favorites.includes(currentGame)) {
    favorites.push(currentGame);
    renderFavorites();
  }
}

function renderFavorites() {
  const favList = document.getElementById("favList");
  favList.innerHTML = "";

  favorites.forEach(game => {
    favList.appendChild(createCard(game));
  });
}

function searchGames(query) {
  const filtered = games.filter(g =>
    g.name.toLowerCase().includes(query.toLowerCase())
  );

  const container = document.getElementById("games");
  container.innerHTML = "";

  filtered.forEach(game => {
    container.appendChild(createCard(game));
  });
}

loadGames();
</script>

</body>
</html>
