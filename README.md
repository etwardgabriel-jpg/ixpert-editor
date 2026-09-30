# ixpert-editor
iXpert Editor Pro adalah website editor foto dan video sederhana dengan berbagai fitur editing.
<!DOCTYPE html>
<html lang="id">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<title>iXpert Editor Pro - Acode Fix</title>
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:Inter,system-ui,Arial}
body{min-height:100vh;background:#0a0f0a;color:#fff;display:flex;justify-content:center;padding:16px;
background-image:linear-gradient(rgba(0,0,0,.6),rgba(0,0,0,.6)),url('https://images.unsplash.com/photo-1500534623283-312aade485b7?auto=format&fit=crop&w=1080&q=80');
background-size:cover;background-position:center;background-attachment:fixed}
.glass{background:rgba(15,25,18,.65);backdrop-filter:blur(18px);border:1px solid rgba(255,255,255,.15);border-radius:24px;box-shadow:0 20px 60px rgba(0,0,0,.5);width:100%;max-width:480px;padding:20px}
.top{display:flex;justify-content:space-between;align-items:center;margin-bottom:18px}
.logo{width:44px;height:44px;border-radius:50%;background:linear-gradient(135deg,#3b82f6,#8b5cf6);display:flex;align-items:center;justify-content:center;font-size:20px}
.upgrade{background:linear-gradient(90deg,#facc15,#f59e0b);color:#000;border:none;padding:10px 14px;border-radius:20px;font-weight:800;font-size:12px}
.modeWrap{display:flex;justify-content:center;margin-bottom:16px}
.mode{width:220px;background:rgba(255,255,255,.08);border:1px solid rgba(255,255,255,.15);border-radius:30px;display:flex;padding:4px;position:relative}
.mode span{flex:1;text-align:center;padding:8px;font-size:13px;font-weight:600;z-index:2;cursor:pointer;opacity:.5}
.mode span.active{opacity:1}
.slider{position:absolute;left:4px;top:4px;bottom:4px;width:calc(50% - 4px);background:rgba(255,255,255,.2);border-radius:30px;transition:.3s}
.upload{border:2px dashed rgba(255,255,255,.3);border-radius:18px;padding:28px;text-align:center;cursor:pointer}
.upload:hover{background:rgba(255,255,255,.05)}
.preview{position:relative;width:100%;max-height:52vh;background:#000;border-radius:12px;overflow:hidden;display:flex;justify-content:center;align-items:center;margin-bottom:12px}
.preview img,.preview video{max-width:100%;max-height:52vh;object-fit:contain;transition:.4s}
.filters{display:flex;gap:10px;overflow-x:auto;padding-bottom:8px}
.fbtn{min-width:84px;height:84px;background:rgba(255,255,255,.06);border:2px solid transparent;border-radius:16px;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:4px;cursor:pointer;flex-shrink:0}
.fbtn.active{border-color:#3b82f6;background:rgba(59,130,246,.2)}
.fbtn.prem{background:linear-gradient(135deg,rgba(250,204,21,.15),rgba(249,115,22,.15))}
.download{width:100%;padding:14px;border-radius:12px;border:1px solid rgba(59,130,246,.4);background:rgba(59,130,246,.5);color:#fff;font-weight:800;margin-top:14px}
.progress{display:none;margin-top:12px}
.bar{height:8px;background:#333;border-radius:10px;overflow:hidden}
.bar div{height:100%;width:0%;background:#10b981;transition:.2s}
.modal{position:fixed;inset:0;background:rgba(0,0,0,.8);backdrop-filter:blur(10px);display:none;align-items:center;justify-content:center;padding:16px;z-index:99}
.modal.show{display:flex}
.box{background:rgba(20,30,22,.9);border:1px solid rgba(255,255,255,.15);border-radius:20px;padding:20px;max-width:360px;width:100%}
</style>
</head>

<body>

<div class="glass">

<div class="top">
<div style="display:flex;gap:10px;align-items:center">
<div class="logo"></div>
<div>
<b>iXpert 15 Pro Max</b><br>
<span style="font-size:11px;opacity:.6">Studio Editor</span>
</div>
</div>
<button class="upgrade" onclick="openUp()">👑 UPGRADE</button>
</div>

<div class="modeWrap">
<div class="mode" id="modeBox">
<div class="slider" id="slider"></div>
<span id="mVideo" class="active" onclick="setMode('video')">Video</span>
<span id="mPhoto" onclick="setMode('photo')">Foto</span>
</div>
</div>

<div class="upload" id="uploadArea" onclick="document.getElementById('fileIn').click()">
<div style="font-size:36px">📁</div>
<h3 id="upTitle">Pilih Video</h3>
<p id="upDesc" style="font-size:12px;opacity:.6">Durasi bebas. Tap untuk buka folder</p>
<input type="file" id="fileIn" accept="video/*" hidden>
</div>

<div id="prevWrap" style="display:none">
<div class="preview" id="mediaBox"></div>
<button onclick="resetM()" style="background:none;border:none;color:#f87171;font-size:12px;margin:4px auto;display:block">
🗑 Ganti Media
</button>
</div>

<div id="featSec" style="opacity:.4;pointer-events:none;margin-top:16px">

<div style="font-size:11px;letter-spacing:1px;opacity:.7;margin-bottom:6px">
✨ FITUR EDITOR
</div>

<div class="filters" id="fContainer">

<div class="fbtn active" onclick="apply('normal',this)">
<div>🚫</div>
<span style="font-size:10px">Original</span>
</div>

<div class="fbtn" onclick="apply('hd',this)">
<div>🎥</div>
<span style="font-size:10px">HD iP 15</span>
</div>

<div class="fbtn" onclick="apply('stabil',this)">
<div>📹</div>
<span style="font-size:10px">Stabil</span>
</div>

<div class="fbtn" onclick="apply('cinema',this)">
<div>🎬</div>
<span style="font-size:10px">Cinematic</span>
</div>

<div class="fbtn" id="slow" onclick="apply('slow',this)">
<div>🏃</div>
<span style="font-size:10px">Slowmo</span>
</div>

<div class="fbtn prem" id="p1" style="display:none" onclick="apply('real',this)">
<div>👁️</div>
<span style="font-size:10px">Realistis 18</span>
</div>

<div class="fbtn prem" id="p2" style="display:none" onclick="apply('sunset',this)">
<div>🌅</div>
<span style="font-size:10px">Sunset</span>
</div>

</div>
</div>

<button class="download" id="dlBtn" onclick="startDl()" style="opacity:.5;pointer-events:none">
⬇ Download MP4 / Foto
</button>

<div class="progress" id="prog">
<div style="display:flex;justify-content:space-between;font-size:11px;margin-bottom:4px">
<span>Render...</span>
<span id="perc">0%</span>
</div>
<div class="bar">
<div id="barIn"></div>
</div>
</div>

<div style="text-align:center;font-size:11px;opacity:.6;margin-top:14px">
BY ETWARD GABRIEL AGUSTINUS SILABAN
</div>

</div>

<div class="modal" id="upModal">
<div class="box">

<div style="display:flex;justify-content:space-between">
<h3 style="color:#facc15">iPhone 18 Pro Max</h3>
<button onclick="closeUp()" style="background:rgba(255,255,255,.1);border:none;color:#fff;width:28px;height:28px;border-radius:50%">
✕
</button>
</div>

<p style="font-size:12px;opacity:.7;margin:10px 0">
Unlock filter premium
</p>

<a href="https://wa.me/6282318067970?text=AKSES%20PREMIUM%2015K"
style="display:block;text-align:center;background:#22c55e;color:#fff;padding:12px;border-radius:12px;text-decoration:none;font-weight:800;margin:10px 0">
BUY 15K
</a>

<div style="display:flex;gap:6px">
<input id="codeIn" placeholder="Kode rahasia"
style="flex:1;padding:10px;border-radius:8px;border:1px solid #444;background:#000;color:#fff">

<button onclick="checkCode()"
style="padding:10px 14px;border-radius:8px;border:none;background:#10b981;color:#fff">
Klaim
</button>
</div>

<p id="codeErr" style="font-size:11px;color:#f87171;display:none">
Kode salah!
</p>

</div>
</div>

<script>

let mode='video', isPrem=false, fileURL=null, curFilter='normal';

const fileIn=document.getElementById('fileIn'),
upTitle=document.getElementById('upTitle'),
upDesc=document.getElementById('upDesc');

const prevWrap=document.getElementById('prevWrap'),
mediaBox=document.getElementById('mediaBox'),
uploadArea=document.getElementById('uploadArea');

const featSec=document.getElementById('featSec'),
dlBtn=document.getElementById('dlBtn'),
slider=document.getElementById('slider');

function setMode(m){

mode=m;

if(m==='video'){

slider.style.transform='translateX(0)';
document.getElementById('mVideo').classList.add('active');
document.getElementById('mPhoto').classList.remove('active');

fileIn.accept='video/*';
upTitle.textContent='Pilih Video';
upDesc.textContent='Durasi bebas. Tap buka folder';

document.getElementById('slow').style.display='flex';
dlBtn.textContent='⬇ Download MP4';

}else{

slider.style.transform='translateX(100%)';
document.getElementById('mPhoto').classList.add('active');
document.getElementById('mVideo').classList.remove('active');

fileIn.accept='image/*';
upTitle.textContent='Pilih Foto';
upDesc.textContent='Pilih foto terbaikmu';

document.getElementById('slow').style.display='none';
dlBtn.textContent='⬇ Download Foto';

}

}

fileIn.addEventListener('change',e=>{

const f=e.target.files[0];

if(!f)return;

fileURL=URL.createObjectURL(f);

uploadArea.style.display='none';
prevWrap.style.display='block';

mediaBox.innerHTML='';

let el;

if(mode==='video'){

el=document.createElement('video');
el.src=fileURL;
el.controls=true;
el.loop=true;

}else{

el=document.createElement('img');
el.src=fileURL;

}

el.id='mainMedia';

mediaBox.appendChild(el);

featSec.style.opacity='1';
featSec.style.pointerEvents='auto';

dlBtn.style.opacity='1';
dlBtn.style.pointerEvents='auto';

});

function resetM(){

prevWrap.style.display='none';
uploadArea.style.display='block';
mediaBox.innerHTML='';
fileURL=null;

featSec.style.opacity='.4';
featSec.style.pointerEvents='none';

}

function apply(type,btn){

document.querySelectorAll('.fbtn').forEach(b=>b.classList.remove('active'));

btn.classList.add('active');

curFilter=type;

const m=document.getElementById('mainMedia');

if(!m)return;

m.style.filter='';
m.style.transform='';

if(type==='hd')
m.style.filter='contrast(1.2) saturate(1.4) brightness(1.05)';

if(type==='stabil')
m.style.filter='contrast(1.1)';

if(type==='cinema'){

m.style.filter='contrast(1.3) saturate(1.2) sepia(.2)';

mediaBox.style.boxShadow='inset 0 40px 40px #000,inset 0 -40px 40px #000';

}

if(type==='slow')
m.style.filter='blur(.3px)';

if(type==='real')
m.style.filter='contrast(1.4) saturate(1.6) sharp(1)';

if(type==='sunset')
m.style.filter='sepia(.5) saturate(1.8) hue-rotate(-10deg) contrast(1.2)';

if(type==='normal')
mediaBox.style.boxShadow='none';

}

function startDl(){

if(!fileURL)return;

const prog=document.getElementById('prog'),
bar=document.getElementById('barIn'),
perc=document.getElementById('perc');

prog.style.display='block';

let p=0;

const it=setInterval(()=>{

p+=isPrem?35:7;

if(p>=100){

p=100;

clearInterval(it);

const a=document.createElement('a');

a.href=fileURL;

a.download=
(mode==='video'?'ixpert_video_':'ixpert_foto_')
+Date.now()
+(mode==='video'?'.mp4':'.jpg');

a.click();

perc.textContent='Selesai!';

setTimeout(()=>{
prog.style.display='none';
},1500);

}

bar.style.width=p+'%';
perc.textContent=p+'%';

},isPrem?80:200);

}

function openUp(){
document.getElementById('upModal').classList.add('show');
}

function closeUp(){
document.getElementById('upModal').classList.remove('show');
}

function checkCode(){

const c=document.getElementById('codeIn').value.trim();

if(c==='2013'){

isPrem=true;

document.getElementById('p1').style.display='flex';
document.getElementById('p2').style.display='flex';

document.getElementById('codeErr').style.display='none';

closeUp();

alert('✅ Premium aktif Medz! Filter iP 18 kebuka');

}else{

document.getElementById('codeErr').style.display='block';

}

}

setMode('video');

</script>

</body>
</html>
