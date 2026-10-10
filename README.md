<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1">
<title>AGRIVERSE SL - Bhashini Edition</title>
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:sans-serif}
body{background:#fdf8ee}
.header{background:linear-gradient(135deg,#00205B,#0b7a0b);color:#fff;padding:14px 16px}
.top{display:flex;justify-content:space-between;align-items:center}
.lang{padding:6px 10px;border-radius:8px;background:#ffd700;font-weight:800}
.card{background:#fff;margin:12px;padding:16px;border-radius:16px;box-shadow:0 4px 12px rgba(0,0,0,.1)}
.input{width:100%;padding:12px;margin:6px 0;border-radius:10px;border:1px solid #ccc}
.btn{width:100%;padding:14px;border:none;border-radius:12px;font-weight:800;cursor:pointer}
.btn-save{background:#00205B;color:#fff}
.btn-mic{background:#fff;border:1px solid green;color:green;margin-bottom:8px}
</style>
</head>
<body>
<div class="header">
<div class="top"><b>🌿 AGRIVERSE SL</b>
<select id="langSel" class="lang" onchange="changeLang()">
<option value="en">English</option>
<option value="kri" selected>Krio</option>
<option value="men">Mende</option>
<option value="tem">Temne</option>
<option value="lim">Limba</option>
</select>
</div>
<div style="font-size:11px;margin-top:6px">🇸🇱 Bhashini Salone • If AI speaks your language, access gets easier</div>
</div>

<div class="card">
<h3 id="addTitle">➕ Add Yu Bag</h3>
<button class="btn btn-mic" onclick="startVoice()">🎙️ <span id="micText">Tok - Tok na Krio</span></button>
<input id="crop" class="input" placeholder="Wet crop? e.g. Cassava">
<input id="qty" class="input" type="number" placeholder="Omus kg?">
<input id="price" class="input" type="number" placeholder="Price Le">
<input id="village" class="input" placeholder="District - Usai yu de?">
<button class="btn btn-save" onclick="saveBag()">💾 Save Bag - Put Am</button>
<p id="msg" style="color:green;text-align:center;font-weight:800"></p>
</div>

<div class="card">📦 Bags (<span id="count">0</span>)<div id="bags"></div></div>

<script>
function changeLang(){
 let m={en:["Add New Bag","Speak to Add"],kri:["Add Yu Bag","Tok - Tok na Krio"],men:["Add Bag","Tok Mende"],tem:["Add Bag","Tok Temne"],lim:["Add Bag","Talk Limba"]};
 let l=document.getElementById('langSel').value;
 document.getElementById('addTitle').innerText=m[l][0];
 document.getElementById('micText').innerText=m[l][1];
}
let bagsData=JSON.parse(localStorage.getItem('ag')||'[]');
function render(){document.getElementById('count').innerText=bagsData.length;document.getElementById('bags').innerHTML=bagsData.map(b=>`<div style="padding:8px;border-bottom:1px solid #eee">🇸🇱 ${b.id} - ${b.crop} ${b.qty}kg</div>`).reverse().join('');}
render();
function saveBag(){let id='SL-'+Date.now().toString().slice(-6);bagsData.push({id,crop:document.getElementById('crop').value,qty:document.getElementById('qty').value,price:document.getElementById('price').value});localStorage.setItem('ag',JSON.stringify(bagsData));render();document.getElementById('msg').innerText='✅ Bag '+id+' Don don!';}
function startVoice(){
 let Rec=window.SpeechRecognition||window.webkitSpeechRecognition;
 let rec=new Rec(); rec.lang='en-SL';
 document.getElementById('msg').innerText='🎙️ Listening... Tok now';
 rec.onresult=function(e){
  let t=e.results[0][0].transcript.toLowerCase();
  document.getElementById('msg').innerText='Yu tok: '+t;
  if(t.includes('cassava')) document.getElementById('crop').value='Cassava';
  if(t.includes('rice')) document.getElementById('crop').value='Rice';
  let nums=t.match(/\d+/);
  if(nums) document.getElementById('qty').value=nums[0];
 }
 rec.start();
}
changeLang();
</script>
</body>
</html>
