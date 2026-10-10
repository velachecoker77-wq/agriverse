<!DOCTYPE html>
<html><head><meta charset="utf-8"><meta name="viewport" content="width=device-width,initial-scale=1">
<title>Agriverse - Green Gold Pro</title>
<style>
:root{--g:#0b7a0b;--gold:#ffd700;--bg:#f6f8f4}
body{font-family:system-ui,sans-serif;background:var(--bg);margin:0}
.h{background:linear-gradient(135deg,#0b7a0b,#16c95d);color:#fff;padding:18px 16px;position:sticky;top:0;z-index:9}
.live{background:#ff1a1a;color:#fff;padding:4px 14px;border-radius:20px;font-weight:900;animation:blink 1s infinite}
@keyframes blink{50%{opacity:.6}}
.c{background:#fff;margin:12px;padding:16px;border-radius:20px;box-shadow:0 4px 18px rgba(0,0,0,.06)}
input,select{width:100%;padding:14px;margin:6px 0;border-radius:12px;border:1px solid #d5ddd0;font-size:15px;box-sizing:border-box}
.b{width:100%;padding:16px;border:none;border-radius:14px;background:var(--g);color:#fff;font-weight:900;font-size:16px}
.bag{display:flex;gap:12px;padding:14px;border:1px solid #e5eadd;border-radius:18px;margin:10px 0;background:#fff}
.bag img{width:86px;height:86px;border-radius:14px;object-fit:cover}
.badge{background:#e8f5e9;color:#0b7a0b;padding:3px 10px;border-radius:10px;font-size:12px;font-weight:800}
.confetti{position:fixed;top:-10px;font-size:22px;animation:fall 1.2s linear}
@keyframes fall{to{transform:translateY(100vh) rotate(720deg)}}
</style></head><body>
<div class="h"><div style="display:flex;justify-content:space-between;align-items:center">
<b>🌿 Agriverse<br><span style="font-size:12px;opacity:.9">Green Gold Pro</span></b>
<span class="live">● LIVE</span>
</div><div style="font-size:11px;margin-top:8px">Season: Dry • 18 Farms Online • Kaiyamba + Bagruwa</div></div>

<div class="c">
<h3 id="a" style="margin:0 0 10px">Add Yu Bag</h3>
<button onclick="V()" style="width:100%;padding:12px;border:2px solid var(--g);border-radius:14px;background:#fff;font-weight:800">🎙️ <span id="m">Tok na Krio</span></button>

<select id="cr"><option value="">Choose Crop</option>
<option value="Cassava">🍠 Cassava</option>
<option value="Corn">🌽 Corn</option>
<option value="Rice">🍚 Rice</option>
<option value="Cacao">🍫 Cacao</option>
<option value="Pepper">🌶️ Pepper</option>
</select>

<input id="qt" type="number" placeholder="Kg / Product Quantity">
<input id="pr" type="number" placeholder="Price - Leones">
<input id="vi" placeholder="Place / Village - e.g. Kaiyamba">
<input id="ct" placeholder="Contact / WhatsApp - 076...">

<button class="b" onclick="S()">💾 Save Bag — Green Gold</button>
<p id="msg" style="text-align:center;font-weight:700"></p>
</div>

<div class="c">
<div style="display:flex;justify-content:space-between"><b>Saved Bags (<span id="n">0</span>)</b>
<div><button onclick="exportCSV()" style="padding:6px 10px;border-radius:8px;border:1px solid #ccc;background:#fff">⬇️ CSV</button>
<button onclick="shareWA()" style="padding:6px 10px;border-radius:8px;border:none;background:#25D366;color:#fff">WhatsApp</button></div>
</div>
<div id="bags"></div>
</div>

<div class="c" style="text-align:center;font-size:12px">
<b>Market</b> • Freetown: Rice Le 280k • Moyamba Le 210k • <span style="color:var(--g)">Hold 2 days = +Le70k</span>
</div>

<script>
let crops={Cassava:"https://images.unsplash.com/photo-1608198093002-ad4e005484ec?w=300",Corn:"https://images.unsplash.com/photo-1551754655-cd27e38d2076?w=300",Rice:"https://images.unsplash.com/photo-1536304929831-ee1ca9d44906?w=300",Cacao:"https://images.unsplash.com/photo-1610611424854-860c614dd765?w=300",Pepper:"https://images.unsplash.com/photo-1563565375-f3fdfdbefa83?w=300"}
let d=JSON.parse(localStorage.getItem('ag')||'[]');
function R(){
 document.getElementById('n').innerText=d.length;
 document.getElementById('bags').innerHTML=d.map(x=>`
 <div class="bag">
 <img src="${crops[x.cr]||crops.Rice}">
 <div style="flex:1">
 <div style="display:flex;justify-content:space-between"><span class="badge">${x.cr}</span><span style="font-size:11px;color:#888">${x.id}</span></div>
 <div style="font-weight:800;margin:4px 0">Price: ${Number(x.pr).toLocaleString()} Leones</div>
 <div style="font-size:13px;color:#555">📍 Village: ${x.vi} • 📞 ${x.ct||'N/A'}<br>Qty: ${x.qt}kg • Product: ${x.cr} bag</div>
 </div></div>`).join('')}
}
R();
function S(){
 if(!cr.value||!qt.value||!pr.value){msg.innerText='Fill crop, kg, price';return}
 let id='BG-'+Date.now().toString().slice(-4);
 d.unshift({cr:cr.value,qt:qt.value,pr:pr.value,vi:vi.value||'Kaiyamba',ct:ct.value,id:id,loc:navigator.geolocation?'Moyamba':'Moyamba'});
 localStorage.setItem('ag',JSON.stringify(d));R();msg.innerText='✅ Saved! Bag '+id+' saved to inventory';
 for(let i=0;i<20;i++){let e=document.createElement('div');e.className='confetti';e.innerText=['🎉','✨','🌿'][Math.floor(Math.random()*3)];e.style.left=Math.random()*
