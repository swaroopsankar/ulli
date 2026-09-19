<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Ulli & Co. — A Rose Gold Chaos Story 🌹</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,400;0,500;0,600;1,500&family=Great+Vibes&display=swap" rel="stylesheet">
<style>
:root {
  --rose-1: #ffe4ec;
  --rose-2: #ffb6c9;
  --rose-3: #ff8fab;
  --rose-4: #e8739e;
  --rose-deep: #7a0c3e;
  --rose-darker: #4a0625;
  --gold: #ffd9a0;
  --gold-deep: #e0a94f;
  --blush-glow: rgba(255,182,201,.6);
  --cream: #fff8f2;
}
* { margin:0; padding:0; box-sizing:border-box; }
html { scroll-behavior: smooth; scroll-snap-type: y proximity; }
body {
  font-family:'Cormorant Garamond', serif;
  overflow-x:hidden;
  cursor:none;
  background: linear-gradient(180deg, var(--rose-darker), #1a0210);
}
::selection { background: var(--rose-3); color:#fff; }
* { transition-timing-function: cubic-bezier(.22,1,.36,1); }

.bokeh-overlay {
  position: fixed; inset:0; pointer-events:none; z-index:1;
  background:
    radial-gradient(circle at 15% 20%, rgba(255,255,255,.15), transparent 25%),
    radial-gradient(circle at 85% 15%, rgba(255,217,160,.15), transparent 30%),
    radial-gradient(circle at 50% 85%, rgba(255,182,201,.2), transparent 35%);
}

#cursorDot {
  position:fixed; width:14px; height:14px; border-radius:50%;
  background:radial-gradient(circle,#fff,var(--rose-3));
  box-shadow:0 0 15px 5px var(--blush-glow);
  pointer-events:none; z-index:99999; transform:translate(-50%,-50%);
  transition: width .15s, height .15s;
}
#cursorRing {
  position:fixed; width:34px; height:34px; border-radius:50%;
  border:2px solid rgba(255,255,255,.6);
  pointer-events:none; z-index:99998; transform:translate(-50%,-50%);
  transition: transform .12s ease-out, opacity .3s;
}
canvas#trailCanvas, canvas#rainCanvas, canvas#starsCanvas {
  position:fixed; top:0; left:0; width:100%; height:100%;
  pointer-events:none;
}
canvas#trailCanvas { z-index:99997; }
canvas#rainCanvas { z-index:8000; }
canvas#starsCanvas { z-index:2; }

.pagenav {
  position:fixed; right:16px; top:50%; transform:translateY(-50%);
  display:flex; flex-direction:column; gap:6px; z-index:9000;
}
.pagenav a {
  width:9px; height:9px; border-radius:50%;
  background:rgba(255,255,255,.5); border:2px solid #fff; display:block;
  transition: transform .2s, background .2s;
}
.pagenav a:hover { transform:scale(1.6); background:var(--rose-3); }
#progressBar {
  position:fixed; top:0; left:0; height:4px; width:0%;
  background:linear-gradient(90deg, var(--gold), var(--rose-3), var(--rose-4));
  z-index:9999; transition:width .1s;
}

#rainToggle {
  position:fixed; top:20px; left:20px; z-index:9500;
  background:rgba(255,255,255,.2); border:1px solid rgba(255,255,255,.5);
  color:#fff; padding:9px 16px; border-radius:999px; font-size:.85em;
  cursor:pointer; backdrop-filter:blur(6px); transition:all .3s;
  font-family:'Cormorant Garamond', serif; font-weight:600;
}
#rainToggle:hover { background:rgba(255,255,255,.35); transform:scale(1.05); }

#musicPlayer {
  position:fixed; bottom:20px; right:20px; z-index:9600;
  background:rgba(74,6,37,.75); backdrop-filter:blur(10px);
  border:1px solid rgba(255,217,160,.4); border-radius:16px;
  padding:10px 16px; display:flex; align-items:center; gap:10px;
  color:var(--cream); font-size:.9em; box-shadow:0 10px 30px rgba(0,0,0,.4);
}
#musicToggle { cursor:pointer; font-size:1.4em; }

section {
  min-height:100vh; display:flex; flex-direction:column; align-items:center; justify-content:center;
  text-align:center; padding:60px 20px; position:relative; overflow:hidden;
  scroll-snap-align: start; scroll-snap-stop: normal;
  opacity:0; transform:translateY(40px);
  transition: opacity 1.1s cubic-bezier(.22,1,.36,1), transform 1.1s cubic-bezier(.22,1,.36,1);
}
section.in-view { opacity:1; transform:translateY(0); }

.s1 {
  background: radial-gradient(circle at 50% 25%, var(--rose-4), var(--rose-deep) 75%);
  color:#fff5f8;
}
.orbit-stage { position:relative; width:420px; height:420px; display:flex; align-items:center; justify-content:center; margin-bottom:20px; }
.orbit-core {
  font-family:'Great Vibes', cursive; font-size:3em; font-weight:400;
  text-shadow:0 0 25px var(--rose-2), 0 0 60px var(--gold);
  z-index:5; animation: corePulse 2.2s ease-in-out infinite;
}
@keyframes corePulse { 0%,100%{transform:scale(1);} 50%{transform:scale(1.08);} }
.orbit-ring { position:absolute; top:50%; left:50%; width:100%; height:100%; animation: spinRing linear infinite; transform-style:preserve-3d; }
.orbit-ring.r1 { animation-duration:14s; }
.orbit-ring.r2 { animation-duration:20s; animation-direction:reverse; }
.orbit-ring.r3 { animation-duration:26s; }
@keyframes spinRing { from{transform:translate(-50%,-50%) rotate(0deg);} to{transform:translate(-50%,-50%) rotate(360deg);} }
.orbit-heart {
  position:absolute; font-size:1.8em; cursor:pointer;
  filter:drop-shadow(0 0 10px var(--rose-2));
  transition: transform .2s; animation: heartWobble 1.6s ease-in-out infinite;
}
.orbit-heart:hover { transform:scale(1.5) !important; }
@keyframes heartWobble { 0%,100%{ filter:drop-shadow(0 0 6px var(--rose-2)); } 50%{ filter:drop-shadow(0 0 20px var(--gold)); } }
.hero-title {
  font-family:'Great Vibes', cursive; font-size:2.8em; margin-top:10px;
  background:linear-gradient(90deg, var(--gold), var(--rose-2), var(--rose-3), var(--gold));
  background-size:300% 100%; -webkit-background-clip:text; background-clip:text; color:transparent;
  animation: shimmerText 6s linear infinite;
  text-shadow: 0 0 40px var(--blush-glow);
}
@keyframes shimmerText { 0%{background-position:0% 50%;} 100%{background-position:300% 50%;} }
.scrolldown { margin-top:25px; font-size:1em; opacity:.9; animation:floaty 2.5s infinite; font-style:italic; }
@keyframes floaty { 0%,100%{transform:translateY(0);} 50%{transform:translateY(-14px);} }

.toast {
  position:fixed; bottom:90px; left:50%; transform:translateX(-50%);
  background:rgba(74,6,37,.85); color:var(--cream); padding:14px 28px; border-radius:20px;
  font-size:1.1em; opacity:0; transition:opacity .4s, transform .4s; z-index:9500;
  pointer-events:none; box-shadow:0 0 30px var(--blush-glow); max-width:85vw; line-height:1.5;
  border:1px solid rgba(255,217,160,.4); font-style:italic;
}
.toast.show { opacity:1; transform:translateX(-50%) translateY(-6px); }
.floating-heart { position:fixed; pointer-events:none; animation:rise 3.2s ease-out forwards; z-index:9400; }
@keyframes rise { 0%{opacity:1; transform:translateY(0) scale(1);} 100%{opacity:0; transform:translateY(-260px) translateX(60px) scale(.4) rotate(360deg);} }

.pop-message {
  position:fixed; pointer-events:none; z-index:9700;
  background:rgba(255,255,255,.95); color:var(--rose-deep);
  padding:10px 16px; border-radius:14px; font-size:.95em; font-style:italic;
  box-shadow:0 8px 25px rgba(122,12,62,.3), 0 0 20px var(--blush-glow);
  transform:translate(-50%,-100%) scale(.5); opacity:0;
  animation: popUp 2s ease-out forwards; white-space:nowrap; max-width:220px;
}
@keyframes popUp {
  0% { opacity:0; transform:translate(-50%,-100%) scale(.5); }
  15% { opacity:1; transform:translate(-50%,-130%) scale(1.05); }
  25% { transform:translate(-50%,-125%) scale(1); }
  80% { opacity:1; }
  100% { opacity:0; transform:translate(-50%,-170%) scale(.9); }
}

.rose1 { background:linear-gradient(160deg, var(--rose-1), var(--gold)); }
.rose2 { background:linear-gradient(160deg, var(--gold), var(--rose-2)); }
.rose3 { background:linear-gradient(160deg, var(--rose-2), var(--rose-3)); }
.rose4 { background:linear-gradient(160deg, var(--rose-1), var(--rose-2)); }
.rose5 { background:linear-gradient(160deg, var(--gold), var(--rose-3)); }
.rose6 { background:linear-gradient(160deg, var(--rose-1), var(--gold-deep)); }
section[class*="rose"] { color: var(--rose-deep); }
section[class*="rose"]::before {
  content:''; position:absolute; inset:0; pointer-events:none;
  background: radial-gradient(circle at 20% 20%, rgba(255,255,255,.5), transparent 40%),
              radial-gradient(circle at 80% 80%, rgba(255,255,255,.35), transparent 40%);
}
.title2 {
  font-family:'Great Vibes', cursive; font-size:2.6em; margin-bottom:20px;
  text-shadow:0 2px 8px rgba(122,12,62,.3); position:relative; z-index:2;
}
.sub2 { max-width:600px; font-size:1.15em; margin-bottom:22px; line-height:1.7; position:relative; z-index:2; font-style:italic; }

.roast-list { list-style:none; max-width:600px; text-align:left; margin-bottom:25px; position:relative; z-index:2; }
.roast-list li {
  background:rgba(255,255,255,.55); border-left:6px solid var(--gold-deep); margin:12px 0;
  padding:16px 20px; border-radius:14px; font-size:1.1em;
  box-shadow: 0 8px 25px rgba(122,12,62,.12);
  transition:transform .3s, background .3s, box-shadow .3s, border-color .3s;
}
.roast-list li:hover {
  transform:translateX(14px) scale(1.02);
  background:rgba(255,255,255,.9);
  box-shadow:0 15px 35px rgba(122,12,62,.2);
  border-color: var(--rose-3);
}

.reveal-box {
  background: linear-gradient(160deg, var(--cream), var(--rose-1));
  border:1px solid rgba(255,255,255,.4);
  border-radius:22px; padding:26px; max-width:550px; font-size:1.15em; line-height:1.7;
  cursor:pointer; position:relative; z-index:2; transition: transform .3s, box-shadow .3s;
  box-shadow: 0 0 50px var(--blush-glow), 0 20px 60px rgba(0,0,0,.15);
}
.reveal-box:hover { transform:scale(1.03); box-shadow: 0 0 70px var(--blush-glow), 0 25px 70px rgba(0,0,0,.2); }
.reveal-box .secret { display:none; margin-top:18px; font-style:italic; color:var(--rose-deep); }
.reveal-box.open { background: linear-gradient(160deg, var(--rose-2), var(--gold)); }
.reveal-box.open .secret { display:block; animation:fadeIn .5s ease; }
@keyframes fadeIn { from{opacity:0; transform:translateY(8px);} to{opacity:1; transform:none;} }
.sunflower { font-size:3.8em; margin-bottom:14px; animation:spin 7s linear infinite; position:relative; z-index:2; filter: hue-rotate(300deg); }
@keyframes spin { from{transform:rotate(0);} to{transform:rotate(360deg);} }

.nickname-badges { display:flex; flex-wrap:wrap; gap:14px; justify-content:center; max-width:600px; margin-bottom:20px; position:relative; z-index:2; }
.badge {
  background: linear-gradient(135deg, var(--cream), var(--rose-1));
  border:1px solid var(--gold-deep); border-radius:999px;
  padding:10px 20px; font-weight:600; font-size:1.05em; cursor:pointer;
  color: var(--rose-deep);
  box-shadow: 0 6px 18px rgba(122,12,62,.15);
  transition:transform .3s, background .3s, box-shadow .3s;
}
.badge:hover {
  transform:scale(1.18) rotate(-3deg);
  background: linear-gradient(135deg, var(--gold), var(--rose-3));
  color:#fff;
  box-shadow:0 10px 30px rgba(122,12,62,.3), 0 0 30px var(--blush-glow);
}

.kitab-page { background:linear-gradient(160deg, var(--cream), var(--gold)); }
.kitab-card, .ehsaas-card {
  background: rgba(255,255,255,.65); border:1px solid rgba(255,255,255,.5); border-radius:24px;
  padding:36px; max-width:640px; font-size:1.18em; line-height:2;
  box-shadow: 0 0 50px var(--blush-glow), 0 20px 60px rgba(0,0,0,.2);
  position:relative; z-index:2; transition:transform .3s;
  color: var(--rose-deep);
}
.kitab-card:hover, .ehsaas-card:hover { transform:translateY(-8px); }
.kitab-card::before { content:"📖"; font-size:2.4em; display:block; margin-bottom:14px; }
.ehsaas-page { background:linear-gradient(160deg, var(--rose-1), var(--gold-deep)); }
.ehsaas-card::before { content:"🌹"; font-size:2.4em; display:block; margin-bottom:14px; }
#ehsaasText, #kitabText { white-space:pre-line; font-style:italic; }
.poem-counter { font-size:.8em; opacity:.65; margin-top:16px; letter-spacing:3px; text-transform:uppercase; }

.gallery-page { background:linear-gradient(160deg, var(--rose-deep), var(--rose-3), var(--gold)); color:#fff5f8; }
.gallery-grid { display:flex; flex-wrap:wrap; justify-content:center; gap:28px; max-width:900px; margin:24px 0; perspective:1200px; position:relative; z-index:2; }
.photo-card { width:220px; position:relative; transform-style:preserve-3d; transition:transform .5s cubic-bezier(.34,1.56,.64,1); cursor:pointer; }
.photo-card img {
  width:100%; height:220px; object-fit:cover; border-radius:20px;
  border:3px solid rgba(255,255,255,.7); box-shadow:0 0 40px var(--blush-glow), 0 15px 40px rgba(0,0,0,.4);
  transition:all .4s;
}
.photo-card:hover { transform:rotateY(10deg) rotateX(4deg) scale(1.08); }
.photo-card:hover img { filter:brightness(1.15) saturate(1.3); box-shadow:0 0 60px var(--blush-glow), 0 25px 65px rgba(0,0,0,.55); }
.photo-label { margin-top:12px; font-size:1.1em; font-family:'Great Vibes', cursive; text-shadow:0 2px 6px rgba(0,0,0,.5); }
.photo-caption { display:none; margin-top:6px; font-size:.9em; font-style:italic; background:rgba(0,0,0,.4); border-radius:10px; padding:8px 12px; }
.photo-card.flipped .photo-caption { display:block; animation:fadeIn .4s ease; }

.quiz-page { background:linear-gradient(160deg, var(--rose-1), var(--gold-deep)); }
.quiz-box {
  background: rgba(255,255,255,.6); border-radius:24px; padding:32px; max-width:550px;
  position:relative; z-index:2; box-shadow: 0 0 50px var(--blush-glow), 0 20px 50px rgba(0,0,0,.18);
  color: var(--rose-deep);
}
.quiz-opt {
  display:block; width:100%; margin:10px 0; padding:14px; border-radius:14px;
  border:1px solid var(--gold-deep); background:rgba(255,255,255,.7); font-size:1.05em; cursor:pointer;
  transition:all .3s; color: var(--rose-deep); font-weight:600;
}
.quiz-opt:hover { background:linear-gradient(135deg,var(--gold),var(--rose-3)); color:#fff; transform:scale(1.04); box-shadow:0 10px 25px rgba(122,12,62,.25); }

.meter-page { background:linear-gradient(160deg, var(--rose-1), var(--gold)); }
.meter-wrap { max-width:500px; width:100%; position:relative; z-index:2; }
.meter-track { width:100%; height:24px; border-radius:999px; background:rgba(255,255,255,.6); border:1px solid var(--gold-deep); overflow:hidden; margin:22px 0; box-shadow: inset 0 2px 8px rgba(0,0,0,.1); }
.meter-fill { height:100%; width:0%; background:linear-gradient(90deg, var(--gold), var(--rose-3), var(--rose-4)); transition:width 1.8s ease; }
.meter-btn {
  padding:14px 32px; border-radius:16px; border:none;
  background:linear-gradient(135deg, var(--gold-deep), var(--rose-4)); color:#fff;
  font-size:1.1em; font-weight:600; cursor:pointer; transition:transform .3s;
  box-shadow: 0 10px 30px rgba(122,12,62,.25);
}
.meter-btn:hover { transform:scale(1.08); box-shadow: 0 15px 40px rgba(122,12,62,.35); }

.shower-page {
  background: radial-gradient(circle at 50% 20%, var(--rose-3), var(--rose-deep) 85%);
  color:#fff5f8;
}
.shower-btn {
  padding:18px 44px; border-radius:999px; border:none;
  background: linear-gradient(135deg, var(--gold), var(--rose-3));
  color:#fff; font-family:'Great Vibes', cursive; font-size:1.8em; letter-spacing:1px; cursor:pointer;
  box-shadow: 0 0 60px var(--blush-glow), 0 10px 40px rgba(0,0,0,.3);
  transition:transform .3s, box-shadow .3s; position:relative; z-index:2;
}
.shower-btn:hover { transform:scale(1.1); box-shadow: 0 0 90px var(--blush-glow); }

.song-page { background: radial-gradient(circle at 50% 40%, var(--rose-4), var(--rose-darker) 75%); color:#fff5f8; }
.song-card {
  max-width:620px; background:rgba(255,255,255,.1); border:1px solid rgba(255,217,160,.4);
  border-radius:28px; padding:38px; backdrop-filter:blur(12px); position:relative; z-index:2;
  box-shadow: 0 0 60px var(--blush-glow), 0 20px 60px rgba(0,0,0,.5);
}
.song-title { font-family:'Great Vibes', cursive; font-size:2.2em; margin-bottom:12px; }
.song-note { font-size:1.05em; opacity:.85; margin-top:18px; line-height:1.8; font-style:italic; }
.vinyl {
  width:130px; height:130px; border-radius:50%; margin:0 auto 22px;
  background: repeating-radial-gradient(circle, #2a0416 0, #2a0416 2px, #4a0625 3px, #4a0625 5px);
  border:6px solid var(--rose-3); box-shadow: 0 0 40px var(--blush-glow);
  animation: spinVinyl 4s linear infinite;
  display:flex; align-items:center; justify-content:center;
}
.vinyl::after { content:'🌹'; font-size:1.5em; }
@keyframes spinVinyl { from{transform:rotate(0);} to{transform:rotate(360deg);} }

.final-page { background: radial-gradient(circle at 50% 40%, var(--rose-4), var(--rose-darker) 75%); color:#fff5f8; }
.final-msg {
  max-width:640px; font-size:1.3em; line-height:2; background:rgba(255,255,255,.1);
  border:1px solid rgba(255,217,160,.4); border-radius:28px; padding:38px;
  backdrop-filter:blur(12px); position:relative; z-index:2;
  box-shadow: 0 0 60px var(--blush-glow), 0 20px 60px rgba(0,0,0,.5);
}
.final-badges { display:flex; flex-wrap:wrap; gap:12px; justify-content:center; margin-top:22px; }
.final-badges span {
  background:rgba(255,255,255,.18); border:1px solid rgba(255,217,160,.5); border-radius:999px;
  padding:8px 18px; font-size:.9em;
}

@media (max-width:600px) {
  .orbit-stage { width:300px; height:300px; }
  .hero-title { font-size:2em; }
  .photo-card { width:160px; }
  .photo-card img { height:160px; }
}
</style>
</head>
<body>

<div class="bokeh-overlay"></div>
<canvas id="trailCanvas"></canvas>
<canvas id="rainCanvas"></canvas>
<canvas id="starsCanvas"></canvas>
<div id="cursorDot"></div>
<div id="cursorRing"></div>
<div id="progressBar"></div>
<button id="rainToggle">🌹 Toggle Love Shower</button>

<div id="musicPlayer">
  <span id="musicToggle">▶️</span>
  <span>Video Games</span>
</div>
<div id="ytPlayer" style="position:fixed; top:-9999px; left:-9999px;"></div>

<div class="pagenav">
  <a href="#p1"></a><a href="#p2"></a><a href="#p3"></a><a href="#p4"></a><a href="#p5"></a>
  <a href="#p6"></a><a href="#p7"></a><a href="#p8"></a><a href="#p9"></a><a href="#p10"></a>
  <a href="#p11"></a><a href="#p12"></a><a href="#p13"></a><a href="#p14"></a><a href="#p15"></a>
  <a href="#p16"></a><a href="#p17"></a>
</div>

<section class="s1" id="p1">
  <div class="orbit-stage">
    <div class="orbit-core">Tap Any Heart</div>
    <div class="orbit-ring r1" id="ring1"></div>
    <div class="orbit-ring r2" id="ring2"></div>
    <div class="orbit-ring r3" id="ring3"></div>
  </div>
  <div class="hero-title">Sunita's Rose Gold Chaos Story</div>
  <div class="scrolldown">↓ sixteen more pages of poetry and petals await ↓</div>
</section>

<section class="rose1" id="p2">
  <div class="sunflower">🌻</div>
  <div class="title2">A Gorgeous Nickname Collection</div>
  <div class="nickname-badges" id="badges"></div>
  <div class="sub2">Click any nickname. Each one comes with a reason you earned it.</div>
</section>

<section class="rose2" id="p3">
  <div class="title2">Hall of Fame: Dumbness Edition</div>
  <ul class="roast-list">
    <li>🌹 Gadhi mode: activated at least twice a day.</li>
    <li>😂 Buddhi ho ya bawli — still can't find your own phone while holding it.</li>
    <li>🌟 Hawli by nature, iconic by accident.</li>
    <li>🎯 Certified rascal with zero remorse.</li>
    <li>💛 Somehow the dumbest person I know is also the funniest.</li>
  </ul>
</section>

<section class="ehsaas-page" id="p4">
  <div class="title2">Ehsaas</div>
  <div class="ehsaas-card">
    <p id="ehsaasText"></p>
    <button class="meter-btn" id="ehsaasNext" style="margin-top:20px;">Next Feeling →</button>
    <div class="poem-counter" id="ehsaasCounter"></div>
  </div>
</section>

<section class="gallery-page" id="p5">
  <div class="hero-title" style="font-size:2.4em;">Evidence Files</div>
  <div class="sub2" style="color:#fff5f8;">Exhibit A through D. All chaos. All exquisite.</div>
  <div class="gallery-grid" id="galleryGrid"></div>
</section>

<section class="s1" id="p6" style="background:radial-gradient(circle at 50% 30%, var(--rose-deep), var(--rose-darker) 75%);">
  <div class="orbit-stage">
    <div class="orbit-core">Round Two</div>
    <div class="orbit-ring r1" id="ring4"></div>
    <div class="orbit-ring r2" id="ring5"></div>
  </div>
  <div class="hero-title">More Hearts, Gadhi</div>
</section>

<section class="kitab-page" id="p7">
  <div class="title2">Kitab</div>
  <div class="kitab-card">
    <p id="kitabText"></p>
    <button class="meter-btn" id="kitabNext" style="margin-top:20px;">Turn the Page →</button>
    <div class="poem-counter" id="kitabCounter"></div>
  </div>
</section>

<section class="rose3" id="p8">
  <div class="title2">Idiot Compilation Vol. 2</div>
  <ul class="roast-list">
    <li>😅 Rascal energy: unmatched.</li>
    <li>🙃 Stupid decisions, delivered with full confidence.</li>
    <li>🧠 Common sense: rare sighting.</li>
    <li>💫 Somehow still my favorite disaster.</li>
  </ul>
</section>

<section class="quiz-page" id="p9">
  <div class="title2">Quick Quiz, Buddhi</div>
  <div class="quiz-box">
    <p style="margin-bottom:16px; font-size:1.15em;">What's the real reason this website exists?</p>
    <div class="quiz-opt" data-r="Wrong. But nice try.">To roast you for fun</div>
    <div class="quiz-opt" data-r="Getting warmer, gadhi.">Because you're funny</div>
    <div class="quiz-opt" data-r="...okay maybe this one.">Because I might actually like you</div>
    <div class="quiz-opt" data-r="Sure. Let's go with that.">All of the above, obviously</div>
  </div>
</section>

<section class="rose4" id="p10">
  <div class="title2">Tap If You Dare</div>
  <div class="reveal-box" id="revealBox1">
    Click here, dumbass 👀
    <div class="secret">Fine. Maybe I like you more than I let on. Don't let it go to your head, buddhi.</div>
  </div>
</section>

<section class="meter-page" id="p11">
  <div class="title2">The Chaos-to-Crush Meter</div>
  <div class="meter-wrap">
    <div class="meter-track"><div class="meter-fill" id="meterFill"></div></div>
    <button class="meter-btn" id="meterBtn">Calculate</button>
    <p class="sub2" id="meterResult" style="margin-top:18px;"></p>
  </div>
</section>

<section class="s1" id="p12" style="background:radial-gradient(circle at 50% 30%, var(--rose-3), var(--rose-darker) 75%);">
  <div class="orbit-stage">
    <div class="orbit-core">Round Three</div>
    <div class="orbit-ring r1" id="ring6"></div>
    <div class="orbit-ring r3" id="ring7"></div>
  </div>
  <div class="hero-title">Hawli Deserves More Hearts</div>
</section>

<section class="rose5" id="p13">
  <div class="title2">One More Secret</div>
  <div class="reveal-box" id="revealBox2">
    Tap again, gadhi 🙈
    <div class="secret">This "just friends" thing has been getting harder to say with a straight face lately.</div>
  </div>
</section>

<section class="rose6" id="p14">
  <div class="title2">Final Roast Round</div>
  <ul class="roast-list">
    <li>🐒 Ulli-level logic, world-class comedy.</li>
    <li>🌪️ Bawli chaos, zero apologies.</li>
    <li>🎭 Dumb on the surface, secretly brilliant at making me smile.</li>
    <li>💛 Officially the best kind of disaster.</li>
  </ul>
</section>

<section class="shower-page" id="p15">
  <div class="hero-title" style="font-size:2.4em;">Love Shower</div>
  <div class="sub2" style="color:#fff5f8;">Press the button. Let roses and hearts fall, one poetic line at a time.</div>
  <button class="shower-btn" id="showerBtn">Release the Shower</button>
</section>

<section class="final-page" id="p16">
  <div class="title2">To Sunita, Officially</div>
  <div class="final-msg">
    Ulli. Bawli. Hawli. Gadhi. Buddhi. Dumb. Idiot. Rascal. Stupid. Take your pick —
    all of them somehow mean the same thing on this page: someone I really, really like
    having around.
    <div class="final-badges">
      <span>Ulli</span><span>Bawli</span><span>Hawli</span><span>Gadhi</span>
      <span>Buddhi</span><span>Dumb</span><span>Idiot</span><span>Rascal</span><span>Stupid</span>
    </div>
    <br>This website means nothing. Probably. 🌹
    <div class="music">
      <iframe style="border-radius:15px;" src="https://open.spotify.com/embed/track/0lCOXkpHLxwUDgV0xkZlIf?utm_source=generator" width="350" height="90" frameBorder="0" allowfullscreen="" allow="autoplay; clipboard-write; encrypted-media; fullscreen; picture-in-picture" loading="lazy"></iframe>
    </div>
  </div>
</section>

<section class="song-page" id="p17">
  <div class="song-card">
    <div class="vinyl"></div>
    <div class="song-title">Our Unofficial Theme Song</div>
    <p class="sub2" style="color:#fff5f8;">Video Games — tap play in the corner to let it follow you through the whole page.</p>
    <div class="song-note">Scroll back to the top with the music playing. Some stories are worth replaying. 💛</div>
  </div>
</section>

<div class="toast" id="toast"></div>

<script>
const messages = [
  "Ulli, you're one of a kind. 💛",
  "Bawli but I still like you.",
  "Hawli energy, iconic results.",
  "Gadhi mode: fully charged.",
  "Not everything true needs to be said out loud.",
  "Buddhi at heart, chaos in action.",
  "Dumb decisions, cute execution.",
  "Idiot? Yes. My favorite one.",
  "Rascal certified, forgiven anyway.",
  "Stupid moves, smart heart.",
  "Maybe I like you more than friendship allows.",
  "This is not a confession. Definitely not.",
  "You're the funniest disaster I know.",
  "Okay fine, I might be falling for you.",
  "Don't overthink this. Or do. I don't know.",
  "Exhibit A of chaos, forever cherished.",
  "You're the plot twist I didn't see coming.",
  "Certified icon of nonsense.",
  "You make dumb look adorable.",
  "Officially my favorite headache.",
  "Even your bad ideas are somehow charming.",
  "You're proof chaos can be gorgeous.",
  "Ten out of ten, would tease again.",
  "Gadhi, you owe me for how much you make me laugh.",
  "Ulli, my favorite waste of good sense.",
  "Bawli, but the fun kind.",
  "Hawli, you glow even when you're clueless.",
  "Buddhi, wisdom optional, charm mandatory.",
  "Idiot, but the irreplaceable kind.",
  "Rascal, guilty as charged, unbothered as ever.",
  "Stupid smart, or smart stupid — still you.",
  "Every heart on this page has a piece of you in it.",
  "You're the reason 'dumb' became a compliment.",
  "This page has more roses than sense, like you."
];

const poeticLines = [
  "Teri hasi mein ek shor hai,\njo dil ke sannate ko tod deta hai.",
  "You arrived like an unplanned monsoon —\nloud, messy, impossible to ignore.",
  "Kabhi gadhi, kabhi rani,\npar dil ne toh bas ek hi kahani mani.",
  "In the book of ordinary days,\nyou wrote the only interesting page.",
  "Bawli si baaton mein bhi,\nkuch sachai chhupi lagti hai.",
  "You are the punchline and the poem,\nboth in the same breath.",
  "Har mazaak ke peeche,\nthoda sa dil bhi likha hota hai.",
  "Not every chaos is a mistake —\nsome of it is just you, arriving.",
  "Ulli kehte kehte,\npata nahi kab pyara lagne laga.",
  "You are proof that the heart\ndoesn't ask for permission to feel.",
  "Buddhi ho ya bawli,\ndil toh phir bhi tumhe hi chunta hai.",
  "Somewhere between the teasing and the truth,\nI stopped pretending this was just a joke.",
  "Gulaab ki khushboo mein bhi,\nab teri hasi ghuli si lagti hai.",
  "Every rose in this shower,\ncarries a little bit of your laugh.",
  "Tumhe dekh kar lagta hai,\nchaos bhi khoobsurat ho sakta hai."
];

function shuffle(arr){
  const a = [...arr];
  for(let i=a.length-1;i>0;i--){
    const j = Math.floor(Math.random()*(i+1));
    [a[i],a[j]] = [a[j],a[i]];
  }
  return a;
}

let messagePool = shuffle(messages);
let poeticPool = shuffle(poeticLines);
function nextMessage(){
  if(messagePool.length === 0) messagePool = shuffle(messages);
  return messagePool.pop();
}
function nextPoeticLine(){
  if(poeticPool.length === 0) poeticPool = shuffle(poeticLines);
  return poeticPool.pop();
}
let tapToggle = false;
function nextTapContent(){
  tapToggle = !tapToggle;
  return tapToggle ? nextPoeticLine() : nextMessage();
}

function showToast(text){
  const t = document.getElementById('toast');
  t.textContent = text;
  t.classList.add('show');
  clearTimeout(t._timer);
  t._timer = setTimeout(()=> t.classList.remove('show'), 3200);
}

function spawnHeart(x,y){
  const h = document.createElement('div');
  h.className='floating-heart';
  h.style.left = x+'px'; h.style.top = y+'px';
  h.style.fontSize = (1.5+Math.random()*1.8)+'em';
  h.textContent = ['💕','✨','💛','🌹','💫','💖'][Math.floor(Math.random()*6)];
  document.body.appendChild(h);
  setTimeout(()=>h.remove(),3200);
}

function spawnPopMessage(x, y, text){
  const m = document.createElement('div');
  m.className = 'pop-message';
  m.style.left = x+'px'; m.style.top = y+'px';
  m.textContent = text;
  document.body.appendChild(m);
  setTimeout(()=> m.remove(), 2000);
}

function buildOrbitRing(ringId, count, radius){
  const ring = document.getElementById(ringId);
  if(!ring) return;
  for(let i=0;i<count;i++){
    const angle = (360/count)*i;
    const h = document.createElement('span');
    h.className = 'orbit-heart';
    h.textContent = ['💖','💕','🌹','✨','💛'][i % 5];
    h.style.transform = `rotate(${angle}deg) translate(${radius}px) rotate(-${angle}deg)`;
    h.style.left = '50%'; h.style.top = '50%';
    h.style.marginLeft = '-14px'; h.style.marginTop = '-14px';
    h.addEventListener('click', e=>{
      e.stopPropagation();
      spawnHeart(e.clientX, e.clientY);
      const msg = nextTapContent();
      showToast(msg);
      spawnPopMessage(e.clientX, e.clientY, msg);
    });
    ring.appendChild(h);
  }
}
buildOrbitRing('ring1', 6, 150);
buildOrbitRing('ring2', 8, 190);
buildOrbitRing('ring3', 5, 120);
buildOrbitRing('ring4', 6, 140);
buildOrbitRing('ring5', 7, 180);
buildOrbitRing('ring6', 6, 150);
buildOrbitRing('ring7', 5, 190);

const nicknames = ["Ulli","Bawli","Hawli","Gadhi","Buddhi","Dumb","Idiot","Rascal","Stupid"];
const badgeBox = document.getElementById('badges');
nicknames.forEach(name=>{
  const b = document.createElement('div');
  b.className='badge';
  b.textContent = name;
  b.addEventListener('click', (e)=>{
    const msg = nextTapContent();
    showToast(msg);
    spawnPopMessage(e.clientX, e.clientY, msg);
  });
  badgeBox.appendChild(b);
});

['revealBox1','revealBox2'].forEach(id=>{
  document.getElementById(id).addEventListener('click', function(){
    this.classList.toggle('open');
  });
});

const images = [
  { src: "S1.jpg", label: "Exhibit A", caption: "The chaos begins here." },
  { src: "S2.jpg", label: "Exhibit B", caption: "Peak dumbassery, captured." },
  { src: "S3.jpg", label: "Exhibit C", caption: "Somehow still adorable." },
  { src: "S4.jpg", label: "Exhibit D", caption: "The final piece of evidence." }
];
const galleryGrid = document.getElementById('galleryGrid');
images.forEach(item=>{
  const card = document.createElement('div');
  card.className = 'photo-card';
  card.innerHTML = `
    <img src="${item.src}" alt="${item.label}" loading="lazy" decoding="async" fetchpriority="low">
    <div class="photo-label">${item.label}</div>
    <div class="photo-caption">${item.caption}</div>
  `;
  card.addEventListener('click', (e)=>{
    card.classList.toggle('flipped');
    const msg = nextTapContent();
    showToast(msg);
    spawnPopMessage(e.clientX, e.clientY, msg);
  });
  galleryGrid.appendChild(card);
});

document.querySelectorAll('.quiz-opt').forEach(opt=>{
  opt.addEventListener('click', function(e){
    showToast(this.dataset.r);
    spawnPopMessage(e.clientX, e.clientY, this.dataset.r);
  });
});

document.getElementById('meterBtn').addEventListener('click', ()=>{
  const fill = document.getElementById('meterFill');
  const result = document.getElementById('meterResult');
  const pct = 70 + Math.floor(Math.random()*30);
  fill.style.width = pct + '%';
  setTimeout(()=>{
    result.textContent = `Result: ${pct}% certified crush material, ${pct > 90 ? 'dangerously high, gadhi.' : 'concerning but cute.'}`;
    showToast("The meter never lies, buddhi.");
  }, 1800);
});

const ehsaasPoems = [
  "Ehsaas hai ye, kaha nahi jaata,\nbas dil ke kisi kone mein reh jaata.\nTeri hasi ka shor, teri baaton ka jaal,\ngadhi kahoon ya rani, dono lagti kamaal.",
  "Feeling I didn't plan to name,\nsomewhere between the jokes and the same old game.\nBawli, you snuck in without a sound,\nnow half my thoughts have you around.",
  "Ehsaas kehte hain jo bina kahe samajh aaye,\ntum bologe kuch, main muskura jaaun.\nUlli tum ho, ya koi aur naam,\ndil ne toh bas tumhe hi chuna hai kaam.",
  "It's not love, I keep telling myself that,\nbut ehsaas doesn't ask permission where it sat.\nGadhi, idiot, whatever I call you loud,\nquietly, you're the calm inside this crowd.",
  "Har mazaak ke peeche thoda sach chhupa,\nteri buddhi wali baaton mein bhi kuch pata chala.\nEhsaas itna simple hai, itna saaf,\ntu meri sabse pyari si kharaabi hai, maaf.",
  "Kabhi kabhi ehsaas itna chup hota hai,\nki khud ko bhi samajhne mein waqt lagta hai.\nTum hawli ho, ya kuch aur naam do,\ndil ne toh bas ek hi jawab chun liya hai.",
  "A feeling doesn't knock before it enters,\nit just settles, quietly, at the center.\nRascal, stupid, dumb, whatever you're called,\nyou walked in without asking, and stayed installed.",
  "Ehsaas ka koi rang nahi hota,\nbas dil ke andar chup chaap sota hai.\nTeri gadhi wali baatein bhi kabhi kabhi,\nsabse zyada sach lagti hain mujhe.",
  "I never meant to notice this much,\nthe way your laugh has its own kind of touch.\nBuddhi, ulli, call it what you will,\nthis feeling isn't loud, but it's real, and still.",
  "Ehsaas woh hai jo bina bole samajh aata hai,\ntumhara hona hi kaafi lagta hai.\nBawli ho ya hawli, jo bhi tum ho,\ndil ne toh apna faisla kar liya hai, sacchi.",
  "Gulaab ki pankhudi jaisi narm si baat,\ntumhari chup bhi kabhi keh jaati hai saari raat.\nHawli ho ya gadhi, farak nahi padta,\nehsaas toh bas tumhare naam se hi ban jaata.",
  "Some feelings arrive dressed as jokes,\nwearing laughter like a soft disguise.\nBuddhi, idiot, dumb, whatever the coat,\nunderneath it, something quietly stays alive.",
  "Kuch raaz aise hote hain jo khud bhi anjaan rehte hain,\nteri paheeli aankhon mein wahi sawaal milte hain.\nUlli ho ya rahasya, naam kya rakhoon tumhe,\nehsaas hi shayad sabse saccha jawab de.",
  "There's a language only silence speaks,\nand you fluent in it without trying.\nGadhi, mystic, whatever the cloak,\nsomething unnamed keeps quietly flying.",
  "Tum jitna samjhaogi utna hi uljhta jaata hoon,\nphir bhi is uljhan mein sukoon dhoondh leta hoon.\nBuddhi kaho ya paheeli, farak nahi ab,\nehsaas ki bhasha samajhna seekh gaya hoon shayad.",
  "A riddle wrapped in laughter, a question in disguise,\nyou are the answer I stopped trying to memorize.\nHawli, enigma, whatever fits the frame,\nsome feelings don't need logic, just a name.",
  "Kabhi kabhi tum ek paheeli lagti ho, suljhi hui bhi nahi,\nphir bhi dil kehta hai suljhaana zaroori nahi.\nBawli ho ya rahasya, jo bhi tum ho aaj,\nehsaas ne mujhe sikha diya chup rehna hi ek raaz.",
  "Not everything true needs an explanation,\nsome truths just exist without translation.\nDumb, mystery, whatever suits you here,\nthis feeling stays, quiet, close, and clear.",
  "Tumhari khamoshi ek kitaab hai jo main padh nahi paata,\nphir bhi har safha mujhe kuch naya sikhaata.\nIdiot kahoon ya paheeli, koi baat nahi,\nehsaas ka raaz tumse hi suljhta sahi.",
  "Some feelings are meant to stay half-written,\nlike a secret only the heart has permission.\nRascal, enigma, whatever the guise,\nyou live somewhere between truth and disguise.",
  "Jitna jaanne ki koshish karta hoon utna hi door lagti ho,\nphir bhi paas se dekhoon toh sabse apni lagti ho.\nStupid ho ya rahasya, is baat ka koi hal nahi,\nehsaas bas itna kehta hai — tum sahi ho, sahi ho.",
  "A mystery doesn't need solving to be loved,\nsometimes it just needs to be felt, unproved.\nBuddhi, paheeli, call it what you may,\nthis feeling isn't leaving, it's here to stay."
];

const kitabPoems = [
  "Dil ki kitab mein ek naya panna khula,\nnaam likha tha uspar — Sunita, thoda ullu, thoda bhola.\nHar chapter mein hasi, har line mein shor,\ntu meri kahani ka sabse pyara mod.",
  "Kitab kehti hai kahaniyon ki baat,\nteri chapters mein bas masti aur ghamaand.\nBawli heroine, gadhi si nayi kahani,\nphir bhi lagti ho tum sabse mehmani.",
  "This book has margins full of you,\nscribbled jokes, and feelings too.\nRascal, idiot, stupid, dumb —\nevery label somehow makes you the favorite one.",
  "Kitab ke panno mein tera zikar hai,\nhar mazaak ke peeche thoda pyar hai.\nUlli kahoon ya kuch aur naam doon,\ntujhe apni kahani ka hero bana loon.",
  "Every book needs a character like you,\nchaotic, loud, impossible to see through.\nBuddhi with the wisdom of a confused sparrow,\nstill somehow the brightest part of tomorrow.",
  "Kitab ka pehla panna tha thoda kora,\nphir tumne aakar har khaali jagah bhar dia.\nHawli ho ya buddhi, jo bhi kaho use,\ntum meri sabse pasandida bhool ho, jise main dhoondhta rahoon.",
  "If this life were a story someone wrote,\nyou'd be the twist nobody saw, the plot they quote.\nGadhi, dumb, whatever the name,\nyou made an ordinary tale feel like fame.",
  "Kitab band karne se pehle sochta hoon,\nkya agla chapter bhi tumhare bina likh paunga?\nUlli, bawli, jo bhi ho tum,\nsach yeh hai ki kahani adhoori lagti hai bina tum.",
  "Some characters are written to fade,\nbut you're the one permanent line I made.\nStupid, rascal, idiot too —\nevery version of this story still points to you.",
  "Kitab ke aakhri panne pe bas itna likha hai,\nki tumhare bina yeh kahani thodi si adhuri thi.\nBuddhi ho ya gadhi, koi farak nahi padta,\ntum ho toh yeh kitab poori lagti hai, sacchi.",
  "Gulaabi jild wali ek purani kitab,\njiske har panne pe tumhara zikar hai.\nHawli, gadhi, ya jo bhi naam do,\ntum is kahani ka sabse resplendent asar ho.",
  "A story doesn't need a perfect hero,\njust one who makes the ordinary golden.\nDumb, idiot, rascal, stupid — zero,\nyou turned my plain chapters into something spoken.",
  "Kitab ke kisi kone mein ek anlikha panna hai,\njiski kahani sirf tumhe hi pata hai.\nUlli ho ya rahasya, jo bhi naam do use,\ntum hi ho vo raaz jo main kabhi na chhodoon.",
  "Every story has a page that stays sealed,\nsome mysteries are better left unrevealed.\nHawli, enigma, whatever you're called,\nyou're the chapter that keeps me enthralled.",
  "Kitab padhte padhte kabhi lagta hai tum khud ek paheeli ho,\nsuljhaana chahoon toh bhi na suljhe, aisi haseen bhoolha ho.\nGadhi kaho ya rahasya, farak nahi padta mujhe,\nkahani adhoori achi lagti hai jab tum ismein ho.",
  "A book without a locked drawer feels incomplete,\nyou're the mystery I never want to defeat.\nBuddhi, riddle, whatever the name,\nyou turned my simple story into something untamed.",
  "Kitab ke panno ke beech ek chhupa hua khat mila,\nusme sirf itna likha tha — tum khud ek paheeli ho, sila.\nBawli ho ya rahasya, jo bhi tum ho aaj,\ntumhe samajhna hi shayad meri sabse pyari asafalta hai, raaz.",
  "Not every character needs to be fully known,\nsome are loved best for the mystery they've shown.\nIdiot, enigma, whatever you choose,\nyou're the plot twist I never want to lose.",
  "Kitab ke aakhri panne pe likha hai bas itna,\nki tumhe poora samajhna shayad zaroori nahi tha.\nStupid ho ya rahasya, koi baat nahi,\nkahani tumhare bina bhi adhoori lagti hai sahi.",
  "Some stories are written to be understood,\nyours was written to be felt, not fully could.\nDumb, mystic, whatever the guise,\nyou're the chapter hidden behind kind eyes.",
  "Kitab band kar deta hoon phir bhi khayal aata hai,\ntumhara raaz suljhana mushkil hi sahi lagta hai.\nRascal ho ya paheeli, is baat ka koi ilaaj nahi,\ntum jaisi ho waisi hi kaafi ho, sacchi sahi.",
  "The best books leave something for you to wonder,\nyou're the mystery I never want to plunder.\nBuddhi, riddle, enigma, call it as you please,\nyou're the story I'll keep rereading with ease."
];

let ehsaasPool = shuffle(ehsaasPoems);
let kitabPool = shuffle(kitabPoems);
let ehsaasSeen = 0, kitabSeen = 0;

function nextEhsaas(){
  if(ehsaasPool.length === 0){ ehsaasPool = shuffle(ehsaasPoems); ehsaasSeen = 0; }
  document.getElementById('ehsaasText').innerText = ehsaasPool.pop();
  ehsaasSeen++;
  document.getElementById('ehsaasCounter').textContent = `poem ${ehsaasSeen} of ${ehsaasPoems.length}`;
}
function nextKitab(){
  if(kitabPool.length === 0){ kitabPool = shuffle(kitabPoems); kitabSeen = 0; }
  document.getElementById('kitabText').innerText = kitabPool.pop();
  kitabSeen++;
  document.getElementById('kitabCounter').textContent = `chapter ${kitabSeen} of ${kitabPoems.length}`;
}
nextEhsaas();
nextKitab();
document.getElementById('ehsaasNext').addEventListener('click', nextEhsaas);
document.getElementById('kitabNext').addEventListener('click', nextKitab);

const cursorDot = document.getElementById('cursorDot');
const cursorRing = document.getElementById('cursorRing');
window.addEventListener('mousemove', e=>{
  cursorDot.style.left = e.clientX+'px';
  cursorDot.style.top = e.clientY+'px';
  cursorRing.style.left = e.clientX+'px';
  cursorRing.style.top = e.clientY+'px';
});
document.addEventListener('mousedown', ()=>{ cursorDot.style.width='8px'; cursorDot.style.height='8px'; });
document.addEventListener('mouseup', ()=>{ cursorDot.style.width='14px'; cursorDot.style.height='14px'; });

const canvas = document.getElementById('trailCanvas');
const ctx = canvas.getContext('2d');
function resizeCanvas(){ canvas.width = window.innerWidth; canvas.height = window.innerHeight; }
resizeCanvas();
window.addEventListener('resize', resizeCanvas);

let particles = [];
const colors = ['#ffb6c9','#ffd9a0','#ff8fab','#e8739e','#fff5f8'];

window.addEventListener('mousemove', e=>{
  for(let i=0;i<2;i++){
    particles.push({
      x: e.clientX, y: e.clientY,
      vx: (Math.random()-0.5)*1.4,
      vy: (Math.random()-0.5)*1.4,
      life: 1,
      size: 2 + Math.random()*3,
      color: colors[Math.floor(Math.random()*colors.length)]
    });
  }
  if(particles.length > 220) particles.splice(0, particles.length-220);
});

function animateTrail(){
  ctx.clearRect(0,0,canvas.width,canvas.height);
  for(let i=particles.length-1;i>=0;i--){
    const p = particles[i];
    p.x += p.vx; p.y += p.vy; p.life -= 0.02;
    if(p.life <= 0){ particles.splice(i,1); continue; }
    ctx.globalAlpha = p.life;
    ctx.beginPath();
    ctx.arc(p.x, p.y, p.size, 0, Math.PI*2);
    ctx.fillStyle = p.color;
    ctx.shadowColor = p.color;
    ctx.shadowBlur = 10;
    ctx.fill();
  }
  ctx.globalAlpha = 1;
  requestAnimationFrame(animateTrail);
}
animateTrail();

const rainCanvas = document.getElementById('rainCanvas');
const rctx = rainCanvas.getContext('2d');
function resizeRainCanvas(){ rainCanvas.width = window.innerWidth; rainCanvas.height = window.innerHeight; }
resizeRainCanvas();
window.addEventListener('resize', resizeRainCanvas);

let rainActive = false;
let rainDrops = [];
const rainEmojis = ['🌹','💗','🌸','✨','💛','🕊️','💫'];

function spawnRainDrop(){
  const depth = Math.random();
  rainDrops.push({
    x: Math.random()*rainCanvas.width,
    y: -30,
    baseSpeed: 0.7 + depth*2.2,
    speed: 0.3,
    size: 14 + depth*28,
    sway: 0.5 + Math.random()*2,
    swayOffset: Math.random()*Math.PI*2,
    swaySpeed: 0.008 + Math.random()*0.015,
    emoji: rainEmojis[Math.floor(Math.random()*rainEmojis.length)],
    rot: Math.random()*360,
    rotSpeed: (Math.random()-0.5)*1.8,
    glow: Math.random() > 0.4,
    opacity: 0,
    depth
  });
}

function animateRain(){
  rctx.clearRect(0,0,rainCanvas.width,rainCanvas.height);
  if(rainActive && Math.random() > 0.2){
    for(let i=0;i<3;i++) spawnRainDrop();
  }
  for(let i=rainDrops.length-1;i>=0;i--){
    const d = rainDrops[i];
    d.speed += (d.baseSpeed - d.speed) * 0.02;
    d.y += d.speed;
    d.x += Math.sin(d.y*d.swaySpeed + d.swayOffset) * d.sway * 0.5;
    d.rot += d.rotSpeed;
    d.opacity = Math.min(1, d.opacity + 0.025);
    if(d.y > rainCanvas.height+40){ rainDrops.splice(i,1); continue; }
    rctx.save();
    rctx.globalAlpha = d.opacity * (d.depth*0.6 + 0.4);
    rctx.translate(d.x, d.y);
    rctx.rotate(d.rot*Math.PI/180);
    if(d.glow){
      rctx.shadowColor = '#ffb6c9';
      rctx.shadowBlur = 15 + d.depth*15;
    }
    rctx.font = d.size+'px serif';
    rctx.textAlign = 'center';
    rctx.fillText(d.emoji, 0, 0);
    rctx.restore();
  }
  requestAnimationFrame(animateRain);
}
animateRain();

document.getElementById('rainToggle').addEventListener('click', ()=>{
  rainActive = !rainActive;
  showToast(rainActive ? "Love shower activated. Let it pour, ulli. 🌹" : "Shower paused. For now.");
});

document.getElementById('showerBtn').addEventListener('click', ()=>{
  rainActive = true;
  let count = 0;
  const showerInterval = setInterval(()=>{
    spawnRainDrop();
    count++;
    if(count > 70){ clearInterval(showerInterval); }
  }, 40);
  showToast(nextPoeticLine());
  document.body.style.transition = 'filter 2.4s ease';
  document.body.style.filter = 'brightness(1.12) saturate(1.15)';
  setTimeout(()=>{
    rainActive = false;
    document.body.style.filter = 'none';
  }, 7000);
});

const starsCanvas = document.getElementById('starsCanvas');
const sctx = starsCanvas.getContext('2d');
function resizeStarsCanvas(){ starsCanvas.width = window.innerWidth; starsCanvas.height = window.innerHeight; }
resizeStarsCanvas();
window.addEventListener('resize', resizeStarsCanvas);

let stars = [];
function initStars(){
  stars = [];
  const count = Math.floor((window.innerWidth * window.innerHeight) / 9000);
  for(let i=0;i<count;i++){
    stars.push({
      x: Math.random()*starsCanvas.width,
      y: Math.random()*starsCanvas.height,
      size: 0.6 + Math.random()*1.8,
      baseAlpha: 0.3 + Math.random()*0.5,
      twinkleSpeed: 0.01 + Math.random()*0.025,
      twinklePhase: Math.random()*Math.PI*2,
      driftX: (Math.random()-0.5)*0.06,
      driftY: 0.04 + Math.random()*0.08
    });
  }
}
initStars();
window.addEventListener('resize', initStars);

function animateStars(){
  sctx.clearRect(0,0,starsCanvas.width,starsCanvas.height);
  stars.forEach(s=>{
    s.twinklePhase += s.twinkleSpeed;
    const alpha = s.baseAlpha * (0.5 + 0.5*Math.sin(s.twinklePhase));
    s.x += s.driftX;
    s.y += s.driftY;
    if(s.y > starsCanvas.height+5) s.y = -5;
    if(s.x > starsCanvas.width+5) s.x = -5;
    if(s.x < -5) s.x = starsCanvas.width+5;
    sctx.beginPath();
    sctx.arc(s.x, s.y, s.size, 0, Math.PI*2);
    sctx.fillStyle = `rgba(255,245,248,${alpha})`;
    sctx.shadowColor = 'rgba(255,217,160,0.8)';
    sctx.shadowBlur = s.size*3;
    sctx.fill();
  });
  requestAnimationFrame(animateStars);
}
animateStars();

/* ============================================================
   SMOOTH EASED SCROLLING — 4000% SENSITIVITY MODE
============================================================ */
let currentScroll = window.scrollY;
let targetScroll = window.scrollY;
let scrollVelocity = 0;
let isScrolling = false;

const SENSITIVITY = 40.0; // 4000% multiplier

window.addEventListener('wheel', e => {
  e.preventDefault();
  const delta = e.deltaMode === 1 ? e.deltaY * 18 : e.deltaY;
  scrollVelocity += delta * 0.28 * SENSITIVITY;
  scrollVelocity = Math.max(-1800, Math.min(1800, scrollVelocity));
  targetScroll += scrollVelocity;
  targetScroll = Math.max(0, Math.min(targetScroll, document.body.scrollHeight - window.innerHeight));
  if(!isScrolling){ isScrolling = true; smoothScrollLoop(); }
}, { passive:false });

function smoothScrollLoop(){
  const diff = targetScroll - currentScroll;
  currentScroll += diff * 0.06;
  scrollVelocity *= 0.78;
  window.scrollTo(0, currentScroll);
  if(Math.abs(diff) > 0.15 || Math.abs(scrollVelocity) > 0.15){
    requestAnimationFrame(smoothScrollLoop);
  } else {
    isScrolling = false;
  }
}

window.addEventListener('scroll', ()=>{
  const scrolled = (window.scrollY / (document.body.scrollHeight - window.innerHeight)) * 100;
  document.getElementById('progressBar').style.width = scrolled + '%';
});

const observer = new IntersectionObserver((entries)=>{
  entries.forEach(entry=>{
    if(entry.isIntersecting) entry.target.classList.add('in-view');
  });
}, { threshold:0.2 });
document.querySelectorAll('section').forEach(sec => observer.observe(sec));

setInterval(()=>{
  if(Math.random() > 0.6){
    spawnHeart(Math.random()*window.innerWidth, window.innerHeight + 20);
  }
}, 700);

window.addEventListener('keydown', e=>{
  if(e.code === 'Space'){
    e.preventDefault();
    for(let i=0;i<20;i++){
      setTimeout(()=>{
        spawnHeart(window.innerWidth/2 + (Math.random()-0.5)*300, window.innerHeight/2 + (Math.random()-0.5)*300);
      }, i*40);
    }
    showToast(nextTapContent());
  }
  if(e.code === 'KeyR'){
    rainActive = !rainActive;
    showToast(rainActive ? "Love shower on. 🌹" : "Love shower off.");
  }
});

let ytPlayer, ytReady = false, musicPlaying = false, autoplayAttempted = false;

window.addEventListener('load', ()=>{
  const ytScript = document.createElement('script');
  ytScript.src = "https://www.youtube.com/iframe_api";
  ytScript.async = true;
  document.body.appendChild(ytScript);
});

window.onYouTubeIframeAPIReady = function(){
  ytPlayer = new YT.Player('ytPlayer', {
    height: '1', width: '1',
    videoId: 'ROmaqF_SKUc',
    playerVars: { autoplay:1, mute:1, controls:0, loop:1, playlist:'ROmaqF_SKUc' },
    events: {
      onReady: (e)=>{
        ytReady = true;
        e.target.mute();
        e.target.playVideo();
      },
      onStateChange: (e)=>{
        if(e.data === YT.PlayerState.PLAYING){
          musicPlaying = true;
          document.getElementById('musicToggle').textContent = '⏸️';
        }
        if(e.data === YT.PlayerState.PAUSED || e.data === YT.PlayerState.ENDED){
          musicPlaying = false;
          document.getElementById('musicToggle').textContent = '▶️';
        }
      }
    }
  });
};

function tryAutoplayOnce(){
  if(autoplayAttempted || !ytReady) return;
  autoplayAttempted = true;
  const forcePlay = ()=>{
    ytPlayer.unMute();
    ytPlayer.setVolume(100);
    ytPlayer.playVideo();
    document.getElementById('musicToggle').textContent = '⏸️';
  };
  forcePlay();
  setTimeout(()=>{
    if(ytPlayer.getPlayerState() !== 1) forcePlay();
  }, 600);
}

['click','scroll','wheel','touchstart','keydown'].forEach(evt=>{
  window.addEventListener(evt, tryAutoplayOnce, { once:true, passive:true });
});

document.getElementById('musicToggle').addEventListener('click', (e)=>{
  e.stopPropagation();
  if(!ytReady) return;
  if(musicPlaying){ ytPlayer.pauseVideo(); } else { ytPlayer.playVideo(); }
});
</script>

</body>
</html>
