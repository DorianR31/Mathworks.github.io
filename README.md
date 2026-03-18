<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MathWorks</title>
<style>
body { margin:0; font-family:Arial,sans-serif; background:linear-gradient(135deg,#0f2027,#203a43,#2c5364); color:white; overflow-x:hidden; }
header { text-align:center; padding:15px; font-size:28px; background:rgba(0,0,0,0.3); position:relative; z-index:2; }
.search-box { display:flex; justify-content:center; margin:20px; }
.search-box input { width:50%; padding:12px; border-radius:20px 0 0 20px; border:none; }
.search-box button { padding:12px; border:none; border-radius:0 20px 20px 0; background:#00c6ff; color:white; cursor:pointer; }
iframe { width:100%; height:45vh; border:none; }
section { padding:20px; text-align:center; }
section h2 { margin-bottom:15px; }
button { cursor:pointer; }
.category-buttons { margin-bottom:20px; }
.category-buttons button { margin:0 5px; padding:10px 15px; border:none; border-radius:10px; background:#00c6ff; color:white; transition:0.3s; }
.category-buttons button:hover { background:#0072ff; transform:scale(1.05); }
.game-grid { display:grid; grid-template-columns: repeat(auto-fit,minmax(120px,1fr)); gap:15px; }
.game-card { background: rgba(0,0,0,0.4); padding:15px; border-radius:15px; cursor:pointer; transition:0.3s; box-shadow:0 0 10px rgba(0,198,255,0.3); }
.game-card:hover { transform: scale(1.15) rotate(2deg); background:#00c6ff; box-shadow:0 0 20px #00c6ff; }
.favorite { border:2px solid gold; }
#passwordScreen { position:fixed; top:0; left:0; width:100%; height:100%; background:linear-gradient(135deg,#1f1c2c,#928dab); display:flex; justify-content:center; align-items:center; flex-direction:column; z-index:999; color:white; animation: fadeIn 1s ease-in; }
#passwordScreen input { padding:15px; font-size:18px; border-radius:10px; border:none; margin-top:10px; }
#passwordScreen button { padding:10px 20px; margin-top:10px; border:none; border-radius:10px; background:#00c6ff; color:white; font-size:16px; transition:0.3s; }
#passwordScreen button:hover { transform:scale(1.1); background:#0072ff; }
#chatWindow { width:60%; height:200px; margin:auto; background:rgba(0,0,0,0.4); padding:10px; overflow-y:auto; border-radius:10px; text-align:left; }
#calcInput, #chatInput { width:60%; padding:10px; margin-top:10px; }
footer { text-align:center; padding:10px; }
@keyframes fadeIn { from {opacity:0;} to {opacity:1;} }
</style>
</head>
<body>

<!-- PASSWORD SCREEN -->
<div id="passwordScreen">
  <h1>Enter Password</h1>
  <input type="password" id="pwInput" placeholder="Password">
  <button onclick="checkPassword()">Enter</button>
</div>

<header>🚀 MathWorks Browser</header>

<!-- SEARCH BOX -->
<div class="search-box">
  <input type="text" id="searchInput" placeholder="Search...">
  <button onclick="searchWeb()">Go</button>
</div>

<!-- BROWSER -->
<iframe id="browserFrame" src="https://www.bing.com"></iframe>

<!-- CALCULATOR -->
<section class="calculator">
  <h2>🧮 Scientific Calculator</h2>
  <input type="text" id="calcInput" placeholder="Enter expression (e.g., 2+3*5)">
  <button onclick="calculate()">=</button>
  <div id="calcResult" style="margin-top:10px; font-size:20px; color:#00ffea;"></div>
</section>

<!-- AI CHAT -->
<section class="ai-chat">
  <h2>🤖 MathWorks AI</h2>
  <div id="chatWindow"></div>
  <input type="text" id="chatInput" placeholder="Ask me anything...">
  <button onclick="sendMessage()">Send</button>
</section>

<!-- GAME LIBRARY -->
<section class="games">
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
</section>

<footer>MathWorks ⚡ Browser + AI + Huge Game Library</footer>

<script>
// PASSWORD LOGIC
function checkPassword(){
  let pw = document.getElementById('pwInput').value;
  if(pw==='1029'){ document.getElementById('passwordScreen').style.display='none'; }
  else{ alert('Incorrect password!'); }
}

// SEARCH BROWSER
function searchWeb(){ 
  let q=document.getElementById('searchInput').value; 
  if(q) document.getElementById('browserFrame').src='https://www.bing.com/search?q='+encodeURIComponent(q); 
}
function loadGame(url){ document.getElementById('browserFrame').src=url; }

// CALCULATOR
function calculate(){
  try {
    let expr = document.getElementById('calcInput').value;
    let result = eval(expr);
    document.getElementById('calcResult').innerText = result;
  } catch(e) { document.getElementById('calcResult').innerText = 'Error'; }
}

// AI CHAT
function sendMessage(){
  const input = document.getElementById('chatInput').value;
  if(!input) return;
  const chatWindow = document.getElementById('chatWindow');
  const userMsg = document.createElement('div');
  userMsg.innerHTML = `<b>You:</b> ${input}`;
  chatWindow.appendChild(userMsg);
  // Dummy AI response (replace with real API later)
  const aiMsg = document.createElement('div');
  aiMsg.innerHTML = `<b>AI:</b> I hear you! You asked: "${input}".`;
  chatWindow.appendChild(aiMsg);
  chatWindow.scrollTop = chatWindow.scrollHeight;
  document.getElementById('chatInput').value = '';
}

// GAME LIBRARY
const games = [
  {name:'Slope',url:'https://sites.google.com/view/unblocked-games100/slope',category:'Action'},
  {name:'Run 3',url:'https://www.hoodamath.com/games/top100gamesof2025.html#run3',category:'Action'},
  {name:'Moto X3M',url:'https://sites.google.com/view/unblocked-games100/motox3m',category:'Action'},
  {name:'Tunnel Rush 2',url:'https://sites.google.com/view/unblocked-games100/tunnelrush2',category:'Action'},
  {name:'Basketball Random',url:'https://sites.google.com/view/unblocked-games100/basketballrandom',category:'Sports'},
  {name:'Soccer Random',url:'https://sites.google.com/view/unblocked-games100/soccerrandom',category:'Sports'},
  {name:'Basketball Stars',url:'https://sites.google.com/view/unblocked-games100/basketballstars',category:'Multiplayer'},
  {name:'Flappy Bird',url:'https://www.hoodamath.com/games/top100gamesof2025.html#flappybird',category:'Arcade'}
  // Add more games here
];

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
    div.innerHTML=`${g.name}<br><button onclick='loadGame("${g.url}")'>Play</button><br><button onclick='toggleFavorite(${i})'>⭐</button>`;
    grid.appendChild(div);
  });
}
renderGames();

// KEYBOARD NAVIGATION
let selectedIndex = 0;
function highlightCard(idx){
  const cards = document.querySelectorAll('.game-card');
  cards.forEach((c,i)=>c.style.outline = i===idx?'3px solid yellow':'none');
  if(cards[idx]) cards[idx].scrollIntoView({behavior:'smooth', block:'center'});
}
document.addEventListener('keydown', function(e){
  const cards = document.querySelectorAll('.game-card');
  if(cards.length===0) return;
  switch(e.key){
    case 'ArrowRight': selectedIndex=(selectedIndex+1)%cards.length; highlightCard(selectedIndex); break;
    case 'ArrowLeft': selectedIndex=(selectedIndex-1+cards.length)%cards.length; highlightCard(selectedIndex); break;
    case 'ArrowDown': selectedIndex=Math.min(selectedIndex+3,cards.length-1); highlightCard(selectedIndex); break;
    case 'ArrowUp': selectedIndex=Math.max(selectedIndex-3,0); highlightCard(selectedIndex); break;
    case 'Enter': if(cards[selectedIndex]) cards[selectedIndex].querySelector('button').click(); break;
    case 'f': case 'F': if(cards[selectedIndex]) cards[selectedIndex].querySelectorAll('button')[1].click(); break;
    case '1': filterCategory('Action'); break;
    case '2': filterCategory('Puzzle'); break;
    case '3': filterCategory('Sports'); break;
    case '4': filterCategory('Multiplayer'); break;
    case '5': filterCategory('Arcade'); break;
  }
});
highlightCard(selectedIndex);
</script>

</body>
</html>
