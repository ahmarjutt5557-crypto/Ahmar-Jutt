<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ahmar Jutt - AI 3D Studio ULTRA</title>
<style>
*{margin:0;padding:0;box-sizing:border-box;font-family:system-ui}
body{background:#08080f;color:#fff}
.header{background:linear-gradient(90deg,#6a00ff,#ff006a);padding:12px;text-align:center;position:sticky;top:0;z-index:99}
.header h1{font-size:17px}
.wrap{max-width:1150px;margin:auto;padding:10px;display:grid;grid-template-columns:1fr 1fr;gap:10px}
@media(max-width:800px){.wrap{grid-template-columns:1fr}}
.card{background:#13131f;border:1px solid #2a2a44;border-radius:14px;padding:12px;margin-bottom:10px}
.card h3{color:#ffcc00;font-size:14px;margin-bottom:8px}
label{font-size:11px;color:#999;display:block;margin:6px 0 3px}
input,select,textarea{width:100%;background:#0c0c16;border:1px solid #333;color:#fff;border-radius:8px;padding:9px;font-size:13px}
textarea{height:95px}
.row{display:grid;grid-template-columns:1fr 1fr;gap:6px}
.btn{width:100%;padding:11px;border:none;border-radius:10px;font-weight:bold;cursor:pointer;margin-top:8px}
.btn-gen{background:linear-gradient(90deg,#ffcc00,#ff4400);color:#000;font-size:16px}
#canvas{width:100%;aspect-ratio:9/16;background:#000;border-radius:12px}
.voice-list{max-height:150px;overflow:auto;background:#0c0c16;border-radius:8px}
.voice-item{padding:7px;border-radius:6px;cursor:pointer;font-size:11px;display:flex;justify-content:space-between}
.voice-item.active{background:#6a00ff}
.progress{height:6px;background:#222;border-radius:10px;overflow:hidden}
.progress div{height:100%;background:#00ff88;width:0%}
.thumb{width:100%;border-radius:10px;margin-top:6px}
.small{font-size:11px;color:#aaa;margin-top:4px;white-space:pre-wrap}
</style>
</head>
<body>
<div class="header"><h1>🔥 AHMAR JUTT ULTRA 3D - 200 VOICES - YT READY 🔥</h1></div>
<div class="wrap">
<div>
<div class="card"><h3>📝 Script + Language (3 Options)</h3>
<textarea id="script">If you put on a shirt with a giant T across the front and then spend the day wearing it you might get a little more attention than usual because the wide bar makes your upper chest look broader while the long line makes your torso seem tapered and together they create the illusion of a stronger V-shaped body.</textarea>
<div class="row"><select id="lang"><option value="en-US">English</option><option value="ur-PK">Urdu</option><option value="hi-IN">Hindi</option></select><select id="dur"><option value="10">10 Sec</option><option value="30" selected>30 Sec</option><option value="60">60 Sec</option><option value="90">90 Sec</option><option value="120">2 Min</option></select></div></div>

<div class="card"><h3>🎙️ Voice Studio - 200+ Voices</h3>
<div class="row"><select id="gender"><option value="all">All 200 Voices</option><option value="male">Mard - Male</option><option value="female">Aurat - Female</option></select><select id="pitchType"><option>Bari Awaz</option><option>Break Wali</option><option>Normal</option></select></div>
<div id="vList" class="voice-list">Loading 200 voices...</div>
<div class="row"><div><label>Pitch <span id="pV">1</span></label><input type="range" id="pitch" min="0.5" max="2" step="0.1" value="1" oninput="pV.innerText=this.value"></div><div><label>Speed <span id="rV">1</span></label><input type="range" id="rate" min="0.5" max="1.8" step="0.1" value="1" oninput="rV.innerText=this.value"></div></div>
<label>Break / Pause</label><select id="brk"><option value="0">No Break</option><option value="0.8" selected>0.8s Break</option><option value="1.5">1.5s Break</option></select></div>

<div class="card"><h3>🧍 3D Character - Aapki Video Jaisa</h3>
<div class="row"><select id="tType"><option value="T">Bara T - Viral (Aapki Video)</option><option value="L">Ulta T</option><option value="V">V Shape</option></select><select id="bg"><option value="street">Street - Gali</option><option value="city">City</option><option value="park">Park</option></select></div>
<div class="row"><input type="color" id="shirtCol" value="#ffffff"><input type="color" id="designCol" value="#000000"></div>
<div class="row"><select id="extra"><option value="people" selected>Log - People</option><option value="all">People+Animals+Birds</option><option value="none">Single</option></select><select id="act"><option value="walk">Walk - Chalta Hua</option><option value="flex">Flex Body</option></select></div></div>

<button class="btn btn-gen" onclick="gen()">🚀 CREATE VIDEO - HD QUALITY</button>
<div class="progress" style="margin-top:8px"><div id="bar"></div></div>
<p id="stat" style="font-size:11px;color:#ffcc00;margin-top:4px">Ready</p>

<div class="card"><h3>📦 YouTube Pack - Auto</h3>
<p class="small" id="ytTitle">Title: T-Shirt Ka Jadoo! V-Shape Body Trick</p>
<p class="small" id="ytDesc">Description auto...</p>
<p class="small" id="ytTags">Tags: #Tshirt #Fashion #BodyLanguage</p>
<canvas id="thumbCanvas" width="1280" height="720" class="thumb"></canvas>
<div class="row"><button class="btn" style="background:#222;color:#fff" onclick="downThumb()">⬇️ Thumbnail Download</button><button class="btn" style="background:#222;color:#fff" onclick="downCaption()">⬇️ Captions (SRT)</button></div>
</div>
</div>

<div>
<div class="card"><h3>👀 LIVE Preview - Aapki Video Jaisi Quality</h3>
<canvas id="canvas" width="1080" height="1920"></canvas>
<video id="final" controls style="width:100%;display:none;margin-top:8px;border-radius:12px;aspect-ratio:9/16;background:#000"></video>
<div class="row"><button class="btn" style="background:#00ff88;color:#000" onclick="preview()">▶️ Preview + Voice</button><button class="btn" style="background:#00aaff;color:#fff" onclick="downVideo()">⬇️ FULL VIDEO DOWNLOAD</button></div>
<p style="font-size:10px;color:#888;margin-top:4px">HD 1080x1920 - Gallery me puri chalegi - YouTube Shorts Ready</p>
</div>
</div>
</div>

<script>
let voices=[], selVoice=null, chunks=[], frame=0, anim;
const cvs=document.getElementById('canvas'), ctx=cvs.getContext('2d');
const tCvs=document.getElementById('thumbCanvas'), tCtx=tCvs.getContext('2d');
function loadV(){voices=speechSynthesis.getVoices();let l=document.getElementById('vList');l.innerHTML='';voices.slice(0,200).forEach((v,i)=>{let d=document.createElement('div');d.className='voice-item'+(i==0?' active':'');d.innerHTML='<span>'+v.name.slice(0,18)+'</span><span>'+v.lang+'</span>';d.onclick=()=>{document.querySelectorAll('.voice-item').forEach(e=>e.classList.remove('active'));d.classList.add('active');selVoice=v;};l.appendChild(d);});if(voices[0])selVoice=voices[0];}
speechSynthesis.onvoiceschanged=loadV;setTimeout(loadV,800);
function draw(){frame++;ctx.clearRect(0,0,1080,1920);let bg=document.getElementById('bg').value;if(bg=='street'){ctx.fillStyle='#87CEEB';ctx.fillRect(0,0,1080,1200);ctx.fillStyle='#555';ctx.fillRect(0,1200,1080,720);}else{ctx.fillStyle='#7ec8ff';ctx.fillRect(0,0,1080,1920);}let x=540+Math.sin(frame*0.08)*12;let y=650+Math.sin(frame*0.12)*10;let shirt=document.getElementById('shirtCol').value;let dcol=document.getElementById('designCol').value;ctx.fillStyle='#ffdbac';ctx.beginPath();ctx.arc(x,y-180,80,0,Math.PI*2);ctx.fill();ctx.fillStyle='#ccc';ctx.fillRect(x-50,y-130,100,26);ctx.fillStyle=shirt;ctx.fillRect(x-165,y-90,330,390);ctx.fillStyle=dcol;if(document.getElementById('tType').value=='T'){ctx.fillRect(x-120,y-70,240,45);ctx.fillRect(x-22,y-70,44,270);}else{ctx.fillRect(x-18,y-70,36,270);ctx.fillRect(x-18,y+200,120,30);}ctx.fillStyle='#1e3a8a';ctx.fillRect(x-135,y+300,120,600);ctx.fillRect(x+15,y+300,120,600);let sw=Math.sin(frame*0.12)*35;ctx.fillStyle='#ffdbac';ctx.fillRect(x-210+sw,y-60,60,210);ctx.fillRect(x+150-sw,y-60,60,210);ctx.fillStyle='#fff';ctx.fillRect(x-150,y+900,120,38);ctx.fillRect(x+30,y+900,120,38);if(document.getElementById('extra').value!='none'){ctx.fillStyle='#ff8c00';ctx.fillRect(750,900,90,210);ctx.fillStyle='#ffdbac';ctx.beginPath();ctx.arc(795,860,33,0,Math.PI*2);ctx.fill();}let txt=document.getElementById('script').value;let w=txt.split(' ');let idx=Math.floor(frame/20)%w.length;let chunk=w.slice(idx,idx+7).join(' ');ctx.fillStyle='rgba(0,0,0,0.75)';ctx.fillRect(0,1650,1080,120);ctx.fillStyle='#fff';ctx.font='bold 38px Arial';ctx.textAlign='center';ctx.fillText(chunk.slice(0,40),540,1730);}
function loop(){draw();anim=requestAnimationFrame(loop);}loop();
function preview(){speechSynthesis.cancel();let t=document.getElementById('script').value;let u=new SpeechSynthesisUtterance(t);if(selVoice)u.voice=selVoice;u.pitch=parseFloat(document.getElementById('pitch').value);u.rate=parseFloat(document.getElementById('rate').value);u.lang=document.getElementById('lang').value;speechSynthesis.speak(u);}
function gen(){document.getElementById('stat').innerText='HD Video + Voice + Thumbnail Generate...';chunks=[];let stream=cvs.captureStream(30);let rec=new MediaRecorder(stream,{mimeType:'video/webm;codecs=vp9'});rec.ondataavailable=e=>{if(e.data.size>0)chunks.push(e.data)};rec.onstop=()=>{let blob=new Blob(chunks,{type:'video/webm'});let url=URL.createObjectURL(blob);let v=document.getElementById('final');v.src=url;v.style.display='block';makeThumb();makeYT();document.getElementById('stat').innerText='✅ READY - Full Video + Thumbnail + Title Ready';document.getElementById('bar').style.width='100%';};rec.start();preview();let dur=parseInt(document.getElementById('dur').value)*1000;let s=Date.now();let it=setInterval(()=>{let pct=20+((Date.now()-s)/dur)*80;document.getElementById('bar').style.width=Math.min(pct,95)+'%';if(Date.now()-s>dur){clearInterval(it);rec.stop();speechSynthesis.cancel();}},100);}
function makeThumb(){tCtx.fillStyle=document.getElementById('shirtCol').value;tCtx.fillRect(0,0,1280,720);tCtx.fillStyle=document.getElementById('designCol').value;tCtx.font='bold 220px Arial';tCtx.textAlign='center';tCtx.fillText('T',640,500);tCtx.fillStyle='#000';tCtx.font='bold 52px Arial';tCtx.fillText('T-SHIRT KA JAADU!',640,650);}
function makeYT(){let txt=document.getElementById('script').value.slice(0,60);document.getElementById('ytTitle').innerText='Title: '+txt+' | V-Shape Body Trick #Shorts';document.getElementById('ytDesc').innerText='Description:\n'+document.getElementById('script').value+'\n\n#Fashion #TshirtTrick #BodyLanguage #Viral #Shorts\nLanguage: '+document.getElementById('lang').value+'\nDuration: '+document.getElementById('dur').value+'s';document.getElementById('ytTags').innerText='Tags: T-shirt trick, V shape body, fashion hack, body language, viral shorts';}
function downVideo(){if(!chunks.length){alert('Pehle Create Video dabao');return;}let b=new Blob(chunks,{type:'video/webm'});let u=URL.createObjectURL(b);let a=document.createElement('a');a.href=u;a.download='ahmar-3D-HD-'+Date.now()+'.webm';a.click();}
function downThumb(){let a=document.createElement('a');a.href=tCvs.toDataURL();a.download='thumbnail-'+Date.now()+'.png';a.click();}
function downCaption(){let txt=document.getElementById('script').value;let srt='1\n00:00:00,000 --> 00:00:'+document.getElementById('dur').value+',000\n'+txt;let b=new Blob([srt],{type:'text/plain'});let u=URL.createObjectURL(b);let a=document.createElement('a');a.href=u;a.download='captions.srt';a.click();}
</script>
</body>
</html>
