<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Cartoon Aircraft Game</title>
<style>
body { margin:0; overflow:hidden; background:#87CEEB; font-family:Arial; }
canvas { display:block; }
#ui {
  position:absolute; top:10px; left:10px; color:white;
  font-size:18px; z-index:10;
  text-shadow:1px 1px 3px black;
}
#shopBtn {
  position:absolute; top:10px; right:10px;
  padding:10px; background:#222; color:white; border:none;
}
#shop {
  position:absolute; top:50px; right:10px;
  background:#111; color:white; padding:10px;
  display:none;
}
button { margin:5px 0; display:block; }
</style>
</head>
<body>

<canvas id="game"></canvas>

<div id="ui">
Score: <span id="score">0</span><br>
Coins: <span id="coins">0</span><br>
Aircraft: <span id="aircraft">Free</span>
</div>

<button id="shopBtn">SHOP</button>

<div id="shop">
<h3>Aircraft Shop</h3>
<button onclick="buy(1)">Free Jet</button>
<button onclick="buy(2)">Speed Jet - 1000</button>
<button onclick="buy(3)">Dodge Jet - 5000</button>
<button onclick="buy(4)">Clone Jet - 10000</button>
</div>

<script>
const canvas = document.getElementById("game");
const ctx = canvas.getContext("2d");

canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

let score=0, coins=0;
let speed=2, gameSpeed=2;
let aircraftType=1;

let player={x:120,y:300,w:40,h:30,vy:0};

let obstacles=[];
let coinDrops=[];

// 🎨 Cartoon draw aircraft
function drawPlane(x,y){
  // body
  ctx.fillStyle="#ffcc00";
  ctx.beginPath();
  ctx.ellipse(x,y,30,12,0,0,Math.PI*2);
  ctx.fill();

  // wing
  ctx.fillStyle="#ff9900";
  ctx.beginPath();
  ctx.moveTo(x,y);
  ctx.lineTo(x-20,y+20);
  ctx.lineTo(x+10,y+10);
  ctx.fill();

  // cockpit (cartoon glass)
  ctx.fillStyle="rgba(255,255,255,0.6)";
  ctx.beginPath();
  ctx.arc(x+10,y-3,6,0,Math.PI*2);
  ctx.fill();
}

// ☁️ Cartoon cloud
function drawCloud(o){
  ctx.fillStyle="#fff";
  ctx.beginPath();
  ctx.arc(o.x,o.y,20,0,Math.PI*2);
  ctx.arc(o.x+20,o.y+10,25,0,Math.PI*2);
  ctx.arc(o.x-20,o.y+10,25,0,Math.PI*2);
  ctx.fill();
}

// 🐦 Cartoon bird (crow style but cute)
function drawBird(o){
  ctx.fillStyle="black";
  ctx.beginPath();
  ctx.arc(o.x,o.y,10,0,Math.PI*2);
  ctx.fill();

  ctx.strokeStyle="black";
  ctx.beginPath();
  ctx.moveTo(o.x-10,o.y);
  ctx.lineTo(o.x-25,o.y-5);
  ctx.lineTo(o.x-10,o.y+5);
  ctx.stroke();
}

// ✨ coin
function drawCoin(c){
  ctx.fillStyle="gold";
  ctx.beginPath();
  ctx.arc(c.x,c.y,8,0,Math.PI*2);
  ctx.fill();

  ctx.strokeStyle="orange";
  ctx.stroke();
}

// controls
window.addEventListener("click",()=>{
  player.vy=-6;
});

// shop
document.getElementById("shopBtn").onclick=()=>{
  let s=document.getElementById("shop");
  s.style.display=s.style.display==="none"?"block":"none";
};

function buy(t){
  if(t===1){aircraftType=1; speed=2;}
  if(t===2 && coins>=1000){coins-=1000; aircraftType=2; speed=2.06;}
  if(t===3 && coins>=5000){coins-=5000; aircraftType=3; speed=2.1;}
  if(t===4 && coins>=10000){coins-=10000; aircraftType=4;}
}

// spawn enemies
function spawn(){
  let r=Math.random();
  if(r<0.5){
    obstacles.push({x:canvas.width,y:Math.random()*canvas.height,type:"bird"});
  } else {
    obstacles.push({x:canvas.width,y:Math.random()*canvas.height,type:"cloud"});
  }
}

// coins
function spawnCoin(){
  coinDrops.push({x:canvas.width,y:Math.random()*canvas.height});
}

// update
function update(){
  score++;
  gameSpeed+=0.002;

  player.vy+=0.3;
  player.y+=player.vy;

  if(player.y<0)player.y=0;
  if(player.y>canvas.height)player.y=canvas.height;

  obstacles.forEach(o=>o.x-=gameSpeed*speed);
  coinDrops.forEach(c=>c.x-=gameSpeed*speed);

  // collision
  obstacles.forEach(o=>{
    if(Math.abs(player.x-o.x)<30 && Math.abs(player.y-o.y)<30){
      alert("Game Over! Score: "+score);
      location.reload();
    }
  });

  // collect coins
  coinDrops.forEach((c,i)=>{
    if(Math.abs(player.x-c.x)<20 && Math.abs(player.y-c.y)<20){
      coins+=10;
      coinDrops.splice(i,1);
    }
  });

  draw();
  requestAnimationFrame(update);
}

function draw(){
  ctx.fillStyle="#87CEEB";
  ctx.fillRect(0,0,canvas.width,canvas.height);

  // player
  drawPlane(player.x,player.y);

  // obstacles
  obstacles.forEach(o=>{
    if(o.type==="bird") drawBird(o);
    else drawCloud(o);
  });

  // coins
  coinDrops.forEach(drawCoin);

  document.getElementById("score").innerText=score;
  document.getElementById("coins").innerText=coins;
  document.getElementById("aircraft").innerText=aircraftType;
}

setInterval(spawn,1200);
setInterval(spawnCoin,1800);

update();
</script>

</body>
</html>
