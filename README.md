<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MathWorks</title>
<style>
body { margin:0; font-family:Arial,sans-serif; background:linear-gradient(135deg,#0f2027,#203a43,#2c5364); color:white; overflow:hidden; }
header { text-align:center; padding:15px; font-size:28px; background:rgba(0,0,0,0.3); position:relative; z-index:2; }
.search-box { display:flex; justify-content:center; margin:20px; }
.search-box input { width:50%; padding:12px; border-radius:20px 0 0 20px; border:none; }
.search-box button { padding:12px; border:none; border-radius:0 20px 20px 0; background:#00c6ff; color:white; cursor:pointer; }
iframe { width:100%; height:45vh; border:none; }
.games { padding:20px; text-align:center; z-index:1; position:relative; }
.games h2 { margin-bottom:15px; }
.category-buttons { margin-bottom:20px; }
.category-buttons button { margin:0 5px; padding:10px 15px; border:none; border-radius:10px; background:#00c6ff; color:white; cursor:pointer; transition:0.3s; }
.category-buttons button:hover { background:#0072ff; transform:scale(1.05); }
.game-grid { display:grid; grid-template-columns: repeat(auto-fit,minmax(120px,1fr)); gap:15px; }
.game-card { background: rgba(0,0,0,0.4); padding:15px; border-radius:15px; cursor:pointer; transition:0.3s; box-shadow:0 0 10px rgba(0,198,255,0.3); }
.game-card:hover { transform: scale(1.15) rotate(2deg); background:#00c6ff; box-shadow:0 0 20px #00c6ff; }
.favorite { border:2px solid gold; }
footer { text-align:center; padding:10px; }
#passwordScreen { position:fixed; top:0; left:0; width:100%; height:100%; background:linear-gradient(135deg,#1f1c2c,#928dab); display:flex; justify-content:center; align-items:center; flex-direction:column; z-index:999; color:white; animation: fadeIn 1s ease-in; }
#passwordScreen input { padding:15px; font-size:18px; border-radius:10px; border:none; margin-top:10px; }
#passwordScreen button { padding:10px 20px; margin-top:10px; border:none; border-radius:10px; background:#00c6ff; color:white; cursor:pointer; font-size:16px; transition:0.3s; }
#passwordScreen button:hover { transform:scale(1.1); background:#0072ff; }
@keyframes fadeIn { from {opacity:0;} to {opacity:1;} }
</style>
</head>
<body>
<div id="passwordScreen">
  <h1>Enter Password</h1>
  <input type="password" id="pwInput" placeholder="Password">
  <button onclick="checkPassword()">Enter</button>
</div>

<header>🚀 MathWorks Browser</header>

<div class="search-box">
  <input type="text" id="searchInput" placeholder="Search...">
  <button onclick="searchWeb()">Go</button>
</div>

<iframe id="browserFrame" src="https://www.bing.com"></iframe>

<div class="games">
  <h2>🎮 Game Library</h2>
  <div class="category-buttons">
    <button onclick="filterCategory('Action')">Action / Adventure</button>
    <button onclick="filterCategory('Puzzle')">Puzzle / Brain</button>
    <button onclick="filterCategory('Sports')">Sports / Racing</button>
    <button onclick="filterCategory('Multiplayer')">Multiplayer / 2-Player</button>
    <button onclick="filterCategory('Arcade')">IO & Arcade / Classic</button>
    <button onclick="showFavorites()">⭐ Favorites</button>
  </div>
  <div class="game-grid" id="gameGrid"></div>
</div>

<footer>MathWorks ⚡ Browser + AI + Huge Game Library</footer>

<script>
// PASSWORD LOGIC
function checkPassword(){
  let pw = document.getElementById('pwInput').value;
  if(pw==='1029'){ document.getElementById('passwordScreen').style.display='none'; }
  else{ alert('Incorrect password!'); }
}

const games = [
  // -- ACTION / ADVENTURE (40+)
  {name:'Slope',url:'https://sites.google.com/view/unblocked-games100/slope',category:'Action'},
  {name:'Run 3',url:'https://www.hoodamath.com/games/top100gamesof2025.html#run3',category:'Action'},
  {name:'Moto X3M',url:'https://sites.google.com/view/unblocked-games100/motox3m',category:'Action'},
  {name:'Tunnel Rush 2',url:'https://sites.google.com/view/unblocked-games100/tunnelrush2',category:'Action'},
  {name:'Snow Rider 3D',url:'https://www.hoodamath.com/games/top100gamesof2025.html#snowrider3d',category:'Action'},
  {name:'Rolly Vortex',url:'https://www.hoodamath.com/games/top100gamesof2025.html#rollyvortex',category:'Action'},
  {name:'Getting Over It',url:'https://www.hoodamath.com/games/top100gamesof2025.html#gettingoverit',category:'Action'},
  {name:'Helix Jump',url:'https://www.hoodamath.com/games/top100gamesof2025.html#helixjump',category:'Action'},
  {name:'Drift Boss',url:'https://www.hoodamath.com/games/top100gamesof2025.html#driftboss',category:'Action'},
  {name:'Mountain Bike Runner',url:'https://www.hoodamath.com/games/top100gamesof2025.html#mountainbikerunner',category:'Action'},
  {name:'Slope Run',url:'https://www.hoodamath.com/games/top100gamesof2025.html#sloperun',category:'Action'},
  {name:'Stickman Hook',url:'https://www.hoodamath.com/games/top100gamesof2025.html#stickmanhook',category:'Action'},
  {name:'Twin Shot',url:'https://www.hoodamath.com/games/top100gamesof2025.html#twinshot',category:'Action'},
  {name:'Mad Truck Challenge',url:'https://www.hoodamath.com/games/top100gamesof2025.html#madtruckchallenge',category:'Action'},
  {name:'Jumping Penalty',url:'https://www.hoodamath.com/games/top100gamesof2025.html#jumpingpenalty',category:'Action'},
  {name:'Water Slide 3D',url:'https://www.hoodamath.com/games/top100gamesof2025.html#waterslide3d',category:'Action'},
  {name:'Police Chase',url:'https://www.hoodamath.com/games/top100gamesof2025.html#policechase',category:'Action'},
  // (Add more action up to 50 if you want)
  
  // -- PUZZLE / BRAIN (40+)
  {name:'2048',url:'https://sites.google.com/view/unblocked-games100/2048',category:'Puzzle'},
  {name:'Chess',url:'https://sites.google.com/view/unblocked-games100/chess',category:'Puzzle'},
  {name:'Connect 4',url:'https://sites.google.com/view/unblocked-games100/connect4',category:'Puzzle'},
  {name:'Sudoku',url:'https://sites.google.com/view/unblocked-games100/sudoku',category:'Puzzle'},
  {name:'Block Blast',url:'https://www.hoodamath.com/games/top100gamesof2025.html#blockblast',category:'Puzzle'},
  {name:'Cubeform',url:'https://www.hoodamath.com/games/top100gamesof2025.html#cubeform',category:'Puzzle'},
  {name:'Candy Clicker 2',url:'https://www.hoodamath.com/games/top100gamesof2025.html#candyclicker2',category:'Puzzle'},
  {name:'Four Colors',url:'https://www.hoodamath.com/games/top100gamesof2025.html#fourcolors',category:'Puzzle'},
  {name:'Math Duck',url:'https://www.hoodamath.com/games/top100gamesof2025.html#mathduck',category:'Puzzle'},
  // (Add more puzzle to reach 40+)
  
  // -- SPORTS / RACING (50+)
  {name:'Basketball Random',url:'https://sites.google.com/view/unblocked-games100/basketballrandom',category:'Sports'},
  {name:'Soccer Random',url:'https://sites.google.com/view/unblocked-games100/soccerrandom',category:'Sports'},
  {name:'Volleyball Legends',url:'https://sites.google.com/view/unblocked-games100/volleyball',category:'Sports'},
  {name:'Eggy Car',url:'https://www.hoodamath.com/games/top100gamesof2025.html#eggycar',category:'Sports'},
  {name:'Wheelie Bike',url:'https://www.hoodamath.com/games/top100gamesof2025.html#wheeliebike',category:'Sports'},
  {name:'8 Ball Pool',url:'https://www.hoodamath.com/games/top100gamesof2025.html#8ballpool',category:'Sports'},
  {name:'Court Clash Basketball',url:'https://www.hoodamath.com/games/top100gamesof2025.html#courtclashbasketball',category:'Sports'},
  {name:'Bike Hero',url:'https://www.hoodamath.com/games/top100gamesof2025.html#bikehero',category:'Sports'},
  // (Add more sports titles to exceed 50)
  
  // -- MULTIPLAYER / 2-PLAYER (30+)
  {name:'Head Soccer',url:'https://sites.google.com/view/unblocked-games100/headsoccer',category:'Multiplayer'},
  {name:'Basketball Stars',url:'https://sites.google.com/view/unblocked-games100/basketballstars',category:'Multiplayer'},
  {name:'Boxing Random',url:'https://sites.google.com/view/unblocked-games100/boxingrandom',category:'Multiplayer'},
  {name:'Volley Random',url:'https://sites.google.com/view/unblocked-games100/volleyrandom',category:'Multiplayer'},
  {name:'1 on 1 Basketball',url:'https://www.hoodamath.com/games/top100gamesof2025.html#1on1basketball',category:'Multiplayer'},
  // (Add more 2-player games to reach 30)
  
  // -- IO & ARCADE / CLASSIC (50+)
  {name:'Flappy Bird',url:'https://www.hoodamath.com/games/top100gamesof2025.html#flappybird',category:'Arcade'},
  {name:'Dino Game',url:'https://www.hoodamath.com/games/top100gamesof2025.html#dinogame',category:'Arcade'},
  {name:'Neon Blaster',url:'https://sites.google.com/view/unblocked-games100/neonblaster',category:'Arcade'},
  {name:'Pac-Man Clone',url:'https://www.hoodamath.com/games/top100gamesof2025.html#pacman',category:'Arcade'},
  {name:'Stick Merge',url:'https://www.hoodamath.com/games/top100gamesof2025.html#stickmerge',category:'Arcade'},
  // (Add more classic arcade games to exceed 50)
];

// SEARCH & BROWSING
function searchWeb(){ let q=document.getElementById('searchInput').value; if(q) document.getElementById('browserFrame').src='https://www.bing.com/search?q='+encodeURIComponent(q); }
function loadGame(url){ document.getElementById('browserFrame').src=url; }

// FAVORITES
function toggleFavorite(idx){
  let favs=JSON.parse(localStorage.getItem('favorites')||'[]');
  if(favs.includes(idx)) favs=favs.filter(i=>i!==idx); else favs.push(idx);
  localStorage.setItem('favorites',JSON.stringify(favs));
  renderGames(currentCategory);
}

let currentCategory='All';
function filterCategory(cat){ currentCategory=cat; renderGames(cat); }
function showFavorites(){ currentCategory='Favorites'; renderGames(); }

function renderGames(filter='All'){
  let grid=document.getElementById('gameGrid');
  grid.innerHTML='';
  let favs=JSON.parse(localStorage.getItem('favorites')||'[]');
  games.forEach((g,i)=>{
    if(filter==='Favorites' && !favs.includes(i)) return;
    if(filter!=='All' && filter!=='Favorites' && g.category!==filter) return;
    let div=document.createElement('div');
    div.className='game-card'+(favs.includes(i)?' favorite':'');
    div.innerHTML=`${g.name}<br><button onclick='loadGame(\"${g.url}\")'>Play</button><br><button onclick='toggleFavorite(${i})'>⭐</button>`;
    grid.appendChild(div);
  });
}
renderGames();
</script>
</body>
</html>
