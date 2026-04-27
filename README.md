<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Painel Quiz Automotivo</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Rajdhani:wght@300;400;600&display=swap');

*{margin:0;padding:0;box-sizing:border-box}

body{
  background:#080808;
  font-family:'Rajdhani',sans-serif;
  color:#ccc;
  min-height:100vh;
  display:flex;
  flex-direction:column;
  align-items:center;
  padding:16px;
  background-image:radial-gradient(ellipse at 50% 0%,#1a1205 0%,#080808 55%);
}

/* ===== HEADER ===== */
.header{
  font-family:'Orbitron',monospace;
  font-size:clamp(10px,2vw,15px);
  letter-spacing:5px;
  color:#c8860a;
  text-align:center;
  margin-bottom:12px;
  text-shadow:0 0 12px #c8860a88;
  text-transform:uppercase;
}

/* ===== DASHBOARD SHELL ===== */
.dash-shell{
  width:100%;
  max-width:900px;
  background:radial-gradient(ellipse at 50% 40%,#111108 0%,#050505 100%);
  border:2px solid #2a2000;
  border-radius:28px 28px 40px 40px;
  padding:18px 24px 22px;
  box-shadow:
    0 0 0 1px #3a2a00,
    0 0 40px #00000099,
    inset 0 2px 0 #ffffff08,
    inset 0 -4px 20px #00000066;
  position:relative;
  margin-bottom:18px;
}

.dash-shell::before{
  content:'';
  position:absolute;
  top:0;left:30px;right:30px;height:1px;
  background:linear-gradient(90deg,transparent,#c8860a44,transparent);
}

/* ===== SPEEDO PAIR ===== */
.dash-interior{
  display:flex;
  align-items:center;
  gap:12px;
}

.speedo{
  width:clamp(100px,20vw,155px);
  height:clamp(100px,20vw,155px);
  flex-shrink:0;
  position:relative;
}

.speedo svg{width:100%;height:100%;}

/* ===== LIGHTS PANEL CENTER ===== */
.lights-panel{
  flex:1;
  display:flex;
  flex-direction:column;
  gap:7px;
}

.lights-row{
  display:flex;
  flex-wrap:wrap;
  gap:5px;
  justify-content:center;
}

/* ===== INDIVIDUAL LIGHT ===== */
.light-btn{
  width:clamp(36px,6vw,50px);
  height:clamp(36px,6vw,50px);
  display:flex;
  align-items:center;
  justify-content:center;
  border-radius:6px;
  border:1px solid #1a1a1a;
  background:#0a0a0a;
  cursor:pointer;
  transition:all 0.25s;
  position:relative;
  flex-shrink:0;
}

.light-btn svg{
  width:60%;height:60%;
  opacity:0.18;
  transition:opacity 0.3s, filter 0.3s;
  filter:grayscale(1);
}

/* ACTIVE */
.light-btn.active svg{ opacity:1; filter:none; }
.light-btn.active.c-red   { border-color:#ff3030; box-shadow:0 0 10px #ff303066,inset 0 0 8px #ff303022; background:#150000; }
.light-btn.active.c-amber { border-color:#ffb300; box-shadow:0 0 10px #ffb30066,inset 0 0 8px #ffb30022; background:#120d00; }
.light-btn.active.c-green { border-color:#00e676; box-shadow:0 0 10px #00e67666,inset 0 0 8px #00e67622; background:#001208; }
.light-btn.active.c-blue  { border-color:#00bfff; box-shadow:0 0 10px #00bfff66,inset 0 0 8px #00bfff22; background:#000d14; }

/* SVG colors per class */
.c-red svg   { fill:#ff3030; }
.c-amber svg { fill:#ffb300; }
.c-green svg { fill:#00e676; }
.c-blue svg  { fill:#00bfff; }

/* done = faded */
.light-btn.done svg{ opacity:0.07; filter:grayscale(1); }
.light-btn.done{ border-color:#111; cursor:default; }

/* blink anim for active */
@keyframes lightblink{0%,100%{opacity:1}50%{opacity:0.5}}
.light-btn.active svg{ animation:lightblink 1.4s ease-in-out infinite; }

/* ===== PROGRESS BAR ===== */
.prog-wrap{
  width:100%;
  max-width:900px;
  height:3px;
  background:#111;
  border-radius:2px;
  margin-bottom:14px;
  overflow:hidden;
}
.prog-fill{
  height:100%;
  background:linear-gradient(90deg,#c8860a,#ff6d00);
  border-radius:2px;
  transition:width .5s ease;
  box-shadow:0 0 8px #ffb30088;
}

/* ===== QUIZ CARD ===== */
.quiz-card{
  width:100%;
  max-width:900px;
  background:#0c0c10;
  border:1px solid #222230;
  border-radius:16px;
  padding:24px 28px;
  min-height:190px;
  display:flex;
  flex-direction:column;
  align-items:center;
  justify-content:center;
  text-align:center;
  box-shadow:0 4px 40px #00000080;
  position:relative;
}

.q-phase{
  font-family:'Orbitron',monospace;
  font-size:9px;
  letter-spacing:3px;
  margin-bottom:12px;
  text-transform:uppercase;
}

.q-big-icon{
  font-size:0;
  margin-bottom:12px;
}
.q-big-icon svg{
  width:64px;height:64px;
}

.q-name{
  font-family:'Orbitron',monospace;
  font-size:clamp(16px,4vw,28px);
  font-weight:900;
  letter-spacing:2px;
  margin-bottom:8px;
  line-height:1.1;
}

.q-desc{
  font-size:clamp(13px,2.5vw,16px);
  color:#99a;
  max-width:580px;
  line-height:1.6;
  margin-top:4px;
}

.q-detail-box{
  background:#060c14;
  border:1px solid #003355;
  border-radius:10px;
  padding:16px 22px;
  margin-top:14px;
  max-width:640px;
  text-align:left;
}
.q-detail-title{
  font-family:'Orbitron',monospace;
  font-size:8px;
  letter-spacing:3px;
  color:#00bfff;
  margin-bottom:8px;
}
.q-detail-text{
  font-size:14px;
  color:#a0b8cc;
  line-height:1.7;
}

.idle-txt{ color:#333; font-size:15px; letter-spacing:1px; }

.score{
  position:absolute;
  top:14px; right:18px;
  font-family:'Orbitron',monospace;
  font-size:10px;
  color:#555;
  letter-spacing:2px;
}

/* ===== BUTTONS ===== */
.btn-row{
  display:flex;
  gap:10px;
  margin-top:16px;
  flex-wrap:wrap;
  justify-content:center;
}

.btn{
  font-family:'Orbitron',monospace;
  font-size:9px;
  letter-spacing:2px;
  padding:12px 22px;
  border:none;
  border-radius:7px;
  cursor:pointer;
  text-transform:uppercase;
  font-weight:700;
  transition:all 0.2s;
}
.btn:hover{ transform:translateY(-1px); }

.btn-listen{ background:#0d200d; color:#00e676; border:1px solid #1a4d1a; box-shadow:0 0 8px #00e67611; }
.btn-listen:hover{ box-shadow:0 0 18px #00e67633; }
.btn-reveal{ background:#1e1600; color:#ffb300; border:1px solid #4a3300; box-shadow:0 0 8px #ffb30011; }
.btn-reveal:hover{ box-shadow:0 0 18px #ffb30033; }
.btn-explain{ background:#001520; color:#00bfff; border:1px solid #00335a; box-shadow:0 0 8px #00bfff11; }
.btn-explain:hover{ box-shadow:0 0 18px #00bfff33; }
.btn-next{ background:#160010; color:#cc66ff; border:1px solid #440066; box-shadow:0 0 8px #cc66ff11; }
.btn-next:hover{ box-shadow:0 0 18px #cc66ff33; }
.btn-restart{ background:#1a0010; color:#ff6688; border:1px solid #660022; }

/* color helpers */
.tc-red{color:#ff3030} .tc-amber{color:#ffb300} .tc-green{color:#00e676} .tc-blue{color:#00bfff}

@keyframes slidein{from{opacity:0;transform:translateY(8px)}to{opacity:1;transform:translateY(0)}}
.slidein{ animation:slidein 0.35s ease; }
</style>
</head>
<body>

<div class="header">⬡ Painel Automotivo — Quiz de Luzes ⬡</div>

<div class="dash-shell">
  <div class="dash-interior">
    <!-- Velocímetro esquerdo -->
    <div class="speedo">
      <svg viewBox="0 0 160 160" xmlns="http://www.w3.org/2000/svg">
        <circle cx="80" cy="80" r="76" fill="#090909" stroke="#222" stroke-width="2"/>
        <circle cx="80" cy="80" r="68" fill="none" stroke="#1a1a1a" stroke-width="1"/>
        <!-- tick marks -->
        <g stroke="#333" stroke-width="1.5">
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(-130 80 80)"/>
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(-104 80 80)"/>
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(-78 80 80)"/>
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(-52 80 80)"/>
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(-26 80 80)"/>
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(0 80 80)"/>
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(26 80 80)"/>
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(52 80 80)"/>
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(78 80 80)"/>
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(104 80 80)"/>
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(130 80 80)"/>
        </g>
        <!-- arc -->
        <path d="M 22 115 A 68 68 0 1 1 138 115" fill="none" stroke="#1e1e1e" stroke-width="8" stroke-linecap="round"/>
        <!-- numbers -->
        <text x="80" y="54" fill="#444" font-size="9" text-anchor="middle" font-family="monospace">60</text>
        <text x="110" y="62" fill="#444" font-size="9" text-anchor="middle" font-family="monospace">80</text>
        <text x="126" y="88" fill="#444" font-size="9" text-anchor="middle" font-family="monospace">100</text>
        <text x="52" y="62" fill="#444" font-size="9" text-anchor="middle" font-family="monospace">40</text>
        <text x="36" y="88" fill="#444" font-size="9" text-anchor="middle" font-family="monospace">20</text>
        <!-- red zone -->
        <path d="M 115 35 A 68 68 0 0 1 138 115" fill="none" stroke="#3a0000" stroke-width="6" stroke-linecap="round"/>
        <!-- needle -->
        <line x1="80" y1="80" x2="80" y2="24" stroke="#c8860a" stroke-width="2" stroke-linecap="round" transform="rotate(-60 80 80)"/>
        <circle cx="80" cy="80" r="6" fill="#1a1a1a" stroke="#333" stroke-width="1.5"/>
        <circle cx="80" cy="80" r="2.5" fill="#c8860a"/>
        <!-- RPM label -->
        <text x="80" y="108" fill="#333" font-size="8" text-anchor="middle" font-family="monospace">RPM×1000</text>
        <!-- small icons area -->
        <rect x="55" y="115" width="50" height="16" rx="3" fill="#0d0d0d" stroke="#1a1a1a"/>
        <text x="80" y="126" fill="#c8860a" font-size="7" text-anchor="middle" font-family="Orbitron,monospace">QUIZ</text>
      </svg>
    </div>

    <!-- LIGHTS CENTER -->
    <div class="lights-panel" id="lightsPanel"></div>

    <!-- Velocímetro direito -->
    <div class="speedo">
      <svg viewBox="0 0 160 160" xmlns="http://www.w3.org/2000/svg">
        <circle cx="80" cy="80" r="76" fill="#090909" stroke="#222" stroke-width="2"/>
        <circle cx="80" cy="80" r="68" fill="none" stroke="#1a1a1a" stroke-width="1"/>
        <g stroke="#333" stroke-width="1.5">
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(-130 80 80)"/>
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(-104 80 80)"/>
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(-78 80 80)"/>
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(-52 80 80)"/>
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(-26 80 80)"/>
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(0 80 80)"/>
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(26 80 80)"/>
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(52 80 80)"/>
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(78 80 80)"/>
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(104 80 80)"/>
          <line x1="80" y1="14" x2="80" y2="22" transform="rotate(130 80 80)"/>
        </g>
        <path d="M 22 115 A 68 68 0 1 1 138 115" fill="none" stroke="#1e1e1e" stroke-width="8" stroke-linecap="round"/>
        <text x="80" y="50" fill="#444" font-size="9" text-anchor="middle" font-family="monospace">100</text>
        <text x="112" y="60" fill="#444" font-size="9" text-anchor="middle" font-family="monospace">120</text>
        <text x="128" y="88" fill="#444" font-size="9" text-anchor="middle" font-family="monospace">140</text>
        <text x="50" y="60" fill="#444" font-size="9" text-anchor="middle" font-family="monospace">80</text>
        <text x="34" y="88" fill="#444" font-size="9" text-anchor="middle" font-family="monospace">60</text>
        <!-- red zone -->
        <path d="M 115 35 A 68 68 0 0 1 138 115" fill="none" stroke="#3a0000" stroke-width="6" stroke-linecap="round"/>
        <!-- needle -->
        <line x1="80" y1="80" x2="80" y2="24" stroke="#c8860a" stroke-width="2" stroke-linecap="round" transform="rotate(-100 80 80)"/>
        <circle cx="80" cy="80" r="6" fill="#1a1a1a" stroke="#333" stroke-width="1.5"/>
        <circle cx="80" cy="80" r="2.5" fill="#c8860a"/>
        <text x="80" y="108" fill="#333" font-size="8" text-anchor="middle" font-family="monospace">KM/H</text>
        <rect x="50" y="115" width="60" height="16" rx="3" fill="#0d0d0d" stroke="#1a1a1a"/>
        <text x="80" y="126" fill="#555" font-size="6.5" text-anchor="middle" font-family="monospace">000000 KM</text>
      </svg>
    </div>
  </div>
</div>

<!-- PROGRESS -->
<div class="prog-wrap"><div class="prog-fill" id="progFill" style="width:0%"></div></div>

<!-- QUIZ -->
<div class="quiz-card" id="quizCard">
  <div class="score" id="scoreTxt">0 / 0</div>
  <div class="idle-txt">⬆ Acenda uma luz no painel para começar</div>
</div>
<div class="btn-row" id="btnRow"></div>

<script>
// ===== SVG ICONS (paths only, fill inherited) =====
const ICONS = {
  motor:`<svg viewBox="0 0 24 24"><path d="M7 4v2H5v2H3v8h2v2h2v2h2v-2h4v2h2v-2h2v-2h2V8h-2V6h-2V4h-2v2h-4V4zm0 4h10v6H7z"/></svg>`,
  oleo:`<svg viewBox="0 0 24 24"><path d="M12 2C9.5 2 7 4.5 7 9c0 2.5 1 4.5 2.5 6L12 22l2.5-7C16 13.5 17 11.5 17 9c0-4.5-2.5-7-5-7zm0 2c1.5 0 3 1.8 3 5 0 1.8-.8 3.5-1.7 5H12l-1.3-5C9.8 7.5 9 5.8 9 4c0-3.2 1.5-5 3-5z"/><rect x="3" y="6" width="3" height="6" rx="1"/><line x1="6" y1="9" x2="7" y2="9" stroke-width="2"/></svg>`,
  temp:`<svg viewBox="0 0 24 24"><path d="M13 3H11V13.27A4 4 0 0 0 8 17a4 4 0 0 0 8 0 4 4 0 0 0-3-3.87zM12 19a2 2 0 1 1 0-4 2 2 0 0 1 0 4zM4 8h2M4 12h2M4 16h2" stroke="currentColor" stroke-width="1.5" fill="none"/><path d="M12 17a1 1 0 1 0 0-2 1 1 0 0 0 0 2z"/></svg>`,
  bateria:`<svg viewBox="0 0 24 24"><rect x="2" y="7" width="18" height="11" rx="2" fill="none" stroke="currentColor" stroke-width="2"/><path d="M20 11h2v3h-2zM7 4v3M11 4v3" stroke="currentColor" stroke-width="2"/><line x1="6" y1="12" x2="14" y2="12" stroke="currentColor" stroke-width="2"/><line x1="10" y1="8" x2="10" y2="16" stroke="currentColor" stroke-width="2"/></svg>`,
  freio:`<svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="9" fill="none" stroke="currentColor" stroke-width="2"/><circle cx="12" cy="12" r="4" fill="none" stroke="currentColor" stroke-width="2"/><text x="12" y="16" text-anchor="middle" font-size="8" fill="currentColor" font-weight="bold">!</text></svg>`,
  abs:`<svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="9" fill="none" stroke="currentColor" stroke-width="2"/><text x="12" y="15.5" text-anchor="middle" font-size="7" fill="currentColor" font-weight="bold" font-family="monospace">ABS</text></svg>`,
  airbag:`<svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="7" fill="none" stroke="currentColor" stroke-width="2"/><line x1="12" y1="21" x2="12" y2="17" stroke="currentColor" stroke-width="2"/><line x1="12" y1="7" x2="12" y2="3" stroke="currentColor" stroke-width="1.5"/><line x1="7" y1="12" x2="3" y2="12" stroke="currentColor" stroke-width="1.5"/><line x1="21" y1="12" x2="17" y2="12" stroke="currentColor" stroke-width="1.5"/><path d="M9 9 L6 6M15 9 L18 6M9 15 L6 18M15 15 L18 18" stroke="currentColor" stroke-width="1.2"/><circle cx="12" cy="12" r="2" fill="currentColor"/></svg>`,
  combustivel:`<svg viewBox="0 0 24 24"><path d="M6 2h9l3 4v14a1 1 0 0 1-1 1H4a1 1 0 0 1-1-1V3a1 1 0 0 1 1-1zm8 5l-2-3H6v14h12V8z" fill="none" stroke="currentColor" stroke-width="1.5"/><rect x="7" y="12" width="6" height="3" rx="1"/><line x1="18" y1="8" x2="21" y2="8" stroke="currentColor" stroke-width="1.5"/><line x1="21" y1="8" x2="21" y2="14" stroke="currentColor" stroke-width="1.5"/></svg>`,
  direcao:`<svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="9" fill="none" stroke="currentColor" stroke-width="2"/><line x1="3" y1="12" x2="21" y2="12" stroke="currentColor" stroke-width="1.5"/><circle cx="12" cy="12" r="2" fill="currentColor"/><path d="M12 12 L12 4" stroke="currentColor" stroke-width="2"/></svg>`,
  tpms:`<svg viewBox="0 0 24 24"><ellipse cx="12" cy="14" rx="7" ry="6" fill="none" stroke="currentColor" stroke-width="2"/><path d="M8 8 C8 4 16 4 16 8" fill="none" stroke="currentColor" stroke-width="2"/><line x1="12" y1="8" x2="12" y2="5" stroke="currentColor" stroke-width="2"/><text x="12" y="16" text-anchor="middle" font-size="6" fill="currentColor" font-weight="bold">!</text></svg>`,
  esp:`<svg viewBox="0 0 24 24"><path d="M5 20 C5 14 9 10 12 8 C15 6 19 4 19 4 L17 10 C15 11 13 13 12 16 C11 19 11 22 11 22z" fill="none" stroke="currentColor" stroke-width="1.8"/><circle cx="7" cy="20" r="2" fill="currentColor"/><circle cx="17" cy="20" r="2" fill="currentColor"/><path d="M5 20 h14" stroke="currentColor" stroke-width="1.5"/></svg>`,
  catalisador:`<svg viewBox="0 0 24 24"><path d="M4 12 C4 8 6 6 8 8 C10 10 10 6 12 6 C14 6 14 10 16 8 C18 6 20 8 20 12" fill="none" stroke="currentColor" stroke-width="2"/><path d="M6 12 L18 12 L16 20 L8 20 Z" fill="none" stroke="currentColor" stroke-width="1.8"/><text x="12" y="18.5" text-anchor="middle" font-size="5.5" fill="currentColor">CAT</text></svg>`,
  w4d:`<svg viewBox="0 0 24 24"><circle cx="5" cy="7" r="2.5" fill="none" stroke="currentColor" stroke-width="1.8"/><circle cx="19" cy="7" r="2.5" fill="none" stroke="currentColor" stroke-width="1.8"/><circle cx="5" cy="17" r="2.5" fill="none" stroke="currentColor" stroke-width="1.8"/><circle cx="19" cy="17" r="2.5" fill="none" stroke="currentColor" stroke-width="1.8"/><rect x="7.5" y="9" width="9" height="6" rx="1" fill="none" stroke="currentColor" stroke-width="1.5"/><line x1="5" y1="9.5" x2="7.5" y2="11" stroke="currentColor" stroke-width="1.2"/><line x1="19" y1="9.5" x2="16.5" y2="11" stroke="currentColor" stroke-width="1.2"/><line x1="5" y1="14.5" x2="7.5" y2="13" stroke="currentColor" stroke-width="1.2"/><line x1="19" y1="14.5" x2="16.5" y2="13" stroke="currentColor" stroke-width="1.2"/></svg>`,
  seta_esq:`<svg viewBox="0 0 24 24"><path d="M12 5 L4 12 L12 19 L12 15 C17 15 20 17 20 21 C20 13 17 9 12 9 Z" fill="currentColor"/></svg>`,
  luz_alta:`<svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="4" fill="currentColor"/><line x1="12" y1="2" x2="12" y2="5" stroke="currentColor" stroke-width="2"/><line x1="12" y1="19" x2="12" y2="22" stroke="currentColor" stroke-width="2"/><line x1="2" y1="12" x2="5" y2="12" stroke="currentColor" stroke-width="2"/><line x1="4.2" y1="4.2" x2="6.3" y2="6.3" stroke="currentColor" stroke-width="2"/><line x1="17.7" y1="4.2" x2="15.6" y2="6.3" stroke="currentColor" stroke-width="2"/><line x1="19" y1="12" x2="22" y2="12" stroke="currentColor" stroke-width="2"/></svg>`,
  dpf:`<svg viewBox="0 0 24 24"><rect x="5" y="8" width="14" height="10" rx="2" fill="none" stroke="currentColor" stroke-width="2"/><path d="M8 4 C8 2 10 2 10 4 C10 6 8 6 8 8M12 2 C12 0 14 0 14 2 C14 4 12 4 12 6 C12 7 12 8 12 8M16 4 C16 2 18 2 18 4 C18 6 16 6 16 8" fill="none" stroke="currentColor" stroke-width="1.5"/><line x1="8" y1="13" x2="16" y2="13" stroke="currentColor" stroke-width="1.5"/><line x1="8" y1="16" x2="16" y2="16" stroke="currentColor" stroke-width="1.5"/></svg>`,
  agua_comb:`<svg viewBox="0 0 24 24"><path d="M12 3 C10 7 6 10 6 14 A6 6 0 0 0 18 14 C18 10 14 7 12 3z" fill="none" stroke="currentColor" stroke-width="2"/><line x1="8" y1="20" x2="16" y2="20" stroke="currentColor" stroke-width="2"/><line x1="6" y1="22" x2="18" y2="22" stroke="currentColor" stroke-width="1.5"/><line x1="9" y1="13" x2="15" y2="13" stroke="currentColor" stroke-width="1.5"/></svg>`,
  servico:`<svg viewBox="0 0 24 24"><path d="M12 2 A10 10 0 1 0 12 22 A10 10 0 0 0 12 2" fill="none" stroke="currentColor" stroke-width="2"/><path d="M14.5 8 C13 6.5 10 7 9 9 C8 11 9 13 11 13.5 L11 18 L13 18 L13 13.5 C15 13 16 11 15 9 Z" fill="none" stroke="currentColor" stroke-width="1.5"/></svg>`,
  cinto:`<svg viewBox="0 0 24 24"><ellipse cx="12" cy="7" rx="4" ry="5" fill="none" stroke="currentColor" stroke-width="2"/><path d="M8 12 L5 22 L12 18 L19 22 L16 12" fill="none" stroke="currentColor" stroke-width="2"/><line x1="8" y1="16" x2="16" y2="16" stroke="currentColor" stroke-width="1.5"/></svg>`,
  porta:`<svg viewBox="0 0 24 24"><rect x="4" y="3" width="12" height="18" rx="1" fill="none" stroke="currentColor" stroke-width="2"/><circle cx="14" cy="12" r="1.2" fill="currentColor"/><line x1="16" y1="3" x2="20" y2="6" stroke="currentColor" stroke-width="1.5"/><line x1="20" y1="6" x2="20" y2="18" stroke="currentColor" stroke-width="1.5"/><line x1="16" y1="21" x2="20" y2="18" stroke="currentColor" stroke-width="1.5"/></svg>`,
  cambio:`<svg viewBox="0 0 24 24"><rect x="3" y="3" width="18" height="18" rx="3" fill="none" stroke="currentColor" stroke-width="2"/><text x="12" y="15" text-anchor="middle" font-size="8" fill="currentColor" font-weight="bold">AT</text><path d="M7 8 L17 8" stroke="currentColor" stroke-width="1.5"/></svg>`,
  injecao:`<svg viewBox="0 0 24 24"><path d="M9 3 L9 10 L4 14 L4 20 L20 20 L20 14 L15 10 L15 3 Z" fill="none" stroke="currentColor" stroke-width="1.8"/><line x1="9" y1="3" x2="15" y2="3" stroke="currentColor" stroke-width="2"/><line x1="9" y1="7" x2="15" y2="7" stroke="currentColor" stroke-width="1.2"/><circle cx="8" cy="17" r="1.5" fill="currentColor"/><circle cx="12" cy="17" r="1.5" fill="currentColor"/><circle cx="16" cy="17" r="1.5" fill="currentColor"/></svg>`,
  suspensao:`<svg viewBox="0 0 24 24"><circle cx="7" cy="18" r="3" fill="none" stroke="currentColor" stroke-width="2"/><circle cx="17" cy="18" r="3" fill="none" stroke="currentColor" stroke-width="2"/><path d="M7 15 L7 10 L10 8 L14 8 L17 10 L17 15" fill="none" stroke="currentColor" stroke-width="1.8"/><line x1="10" y1="8" x2="10" y2="4" stroke="currentColor" stroke-width="1.5"/><line x1="14" y1="8" x2="14" y2="4" stroke="currentColor" stroke-width="1.5"/><line x1="8" y1="4" x2="16" y2="4" stroke="currentColor" stroke-width="2"/></svg>`,
  check:`<svg viewBox="0 0 24 24"><path d="M12 2 C10 2 8 3 7 5 L3 19 L5 21 L12 19 L19 21 L21 19 L17 5 C16 3 14 2 12 2z" fill="none" stroke="currentColor" stroke-width="2"/><text x="12" y="15" text-anchor="middle" font-size="9" fill="currentColor" font-weight="bold">!</text></svg>`,
};

const LIGHTS = [
  {id:'motor',   icon:'motor',    color:'c-amber', nome:'CHECK ENGINE',        desc:'Falha detectada no motor ou sistema de emissões pelo ECM.',     det:'Indica que o módulo ECM detectou código de falha. Pode ser tampão frouxo, sensor O2, bobina de ignição ou catalisador. Nunca ignore — leve para leitura OBD-II.'},
  {id:'oleo',    icon:'oleo',     color:'c-red',   nome:'PRESSÃO DE ÓLEO',     desc:'Pressão de lubrificação insuficiente — risco grave ao motor.',   det:'EMERGÊNCIA total. Motor sem lubrificação adequada pode fundir pistões e virabrequim em minutos. Pare imediatamente, desligue e verifique o nível. Se normal, bomba de óleo com defeito.'},
  {id:'temp',    icon:'temp',     color:'c-red',   nome:'SUPERAQUECIMENTO',    desc:'Temperatura do motor acima do limite seguro.',                   det:'Motor superaquecendo. Causas: falta de fluido, termostato travado, ventoinha ou radiador. Pare, desligue o AC, ligue o aquecedor no máximo. NUNCA abra o radiador quente.'},
  {id:'bateria', icon:'bateria',  color:'c-red',   nome:'FALHA NO ALTERNADOR', desc:'Alternador não carrega a bateria — carro pode parar em minutos.', det:'A bateria está se esgotando em movimento. Desligue AC, rádio, faróis se possível. Pode ser correia, escovas ou regulador. Vá direto a uma oficina.'},
  {id:'freio',   icon:'freio',    color:'c-red',   nome:'SISTEMA DE FREIOS',   desc:'Freio de mão acionado ou fluido de freio com nível baixo.',      det:'Fluido baixo = PERIGO: vazamento ou pastilhas desgastadas. Freios podem falhar. Verifique o reservatório. Se baixo, não dirija sem inspeção.'},
  {id:'abs',     icon:'abs',      color:'c-amber', nome:'FALHA NO ABS',        desc:'Antitravamento desativado — maior risco em frenagem brusca.',    det:'O ABS impede travamento em emergências, mantendo controle direcional. Sem ele, em piso escorregadio a roda trava e você perde a direção. Verifique sensores das rodas.'},
  {id:'airbag',  icon:'airbag',   color:'c-red',   nome:'FALHA NO AIRBAG',     desc:'Sistema SRS com defeito — airbag pode não inflar em colisão.',   det:'Em impacto, o airbag pode não abrir — ou abrir sem razão. Ambos perigosos. Pode ser sensor de impacto, conector ou inflator. Exige diagnóstico especializado.'},
  {id:'combustivel',icon:'combustivel',color:'c-amber',nome:'COMBUSTÍVEL BAIXO',desc:'Reserva ativada — aproximadamente 5 a 10 litros restantes.',   det:'Dirigir com tanque muito vazio prejudica a bomba (que usa gasolina como lubrificante) e aspira sedimentos do fundo, entupindo o filtro de combustível.'},
  {id:'direcao', icon:'direcao',  color:'c-amber', nome:'DIREÇÃO ELÉTRICA',    desc:'Falha na direção assistida — volante ficará pesado.',             det:'EPS com defeito. O carro dirige, mas o volante exige muita força. Perigoso em alta velocidade. Pode ser sensor de torque, motor da coluna ou módulo eletrônico.'},
  {id:'tpms',    icon:'tpms',     color:'c-amber', nome:'PNEU MURCHO (TPMS)',  desc:'Um ou mais pneus com pressão abaixo do ideal.',                  det:'Pneus sub-inflados aumentam consumo, pioram frenagem, causam desgaste irregular e risco de estouro. Pressão correta está na coluna da porta do motorista.'},
  {id:'esp',     icon:'esp',      color:'c-amber', nome:'CONTROLE DE ESTAB.',  desc:'ESP ativado ou desligado — sistema de estabilidade.',            det:'Piscando: sistema trabalhando (normal). Fixo: ESP desligado ou com falha. Ele freia rodas individualmente para manter trajetória. Sem ele, risco de capotamento.'},
  {id:'catalisador',icon:'catalisador',color:'c-amber',nome:'CATALISADOR QUENTE',desc:'Temperatura do catalisador perigosamente alta.',              det:'Superaquecimento por mistura rica ou velas/bobinas falhando, jogando combustível não queimado no escapamento. O catalisador pode fundir internamente — caro substituir.'},
  {id:'w4d',     icon:'w4d',      color:'c-amber', nome:'TRAÇÃO 4×4',          desc:'Modo 4WD ativo ou falha no sistema de tração integral.',         det:'Em 4WD no asfalto seco: desgaste e dificuldade em curvas. Se acendeu sozinho: falha eletrônica no sistema. Use 4×4 apenas off-road ou em superfícies escorregadias.'},
  {id:'seta',    icon:'seta_esq', color:'c-green', nome:'INDICADOR DE DIREÇÃO',desc:'Pisca-pisca de direção ativado — sinal de manobra.',             det:'Piscando rápido = lâmpada queimada no circuito. Luz fixa = relay com defeito. Sempre sinalize ANTES da manobra, nunca durante. Multa e risco de acidente.'},
  {id:'luzalta', icon:'luz_alta', color:'c-blue',  nome:'FAROL ALTO',          desc:'Farol pleno ligado — atenção ao uso correto.',                   det:'Use somente em estradas sem iluminação e sem veículos à frente. Deslumbra outros motoristas. Carros modernos têm high beam assist que desliga automaticamente.'},
  {id:'dpf',     icon:'dpf',      color:'c-amber', nome:'FILTRO DE FULIGEM (DPF)',desc:'Filtro de partículas do diesel entupido — perda de potência.', det:'Exclusivo de diesel. A regeneração automática exige 20+ minutos acima de 60 km/h constantes. Uso urbano entope frequentemente. Ignore e danificará o turbo.'},
  {id:'agua',    icon:'agua_comb',color:'c-amber', nome:'ÁGUA NO COMBUSTÍVEL', desc:'Contaminação por água no sistema diesel detectada.',             det:'Exclusivo diesel. Água corrói bicos injetores e danifica a bomba de alta pressão — componentes caríssimos. Drene o separador imediatamente. Não dirija assim.'},
  {id:'servico', icon:'servico',  color:'c-amber', nome:'REVISÃO PROGRAMADA',  desc:'Manutenção periódica próxima ou vencida.',                       det:'Hodômetro ou temporizador atingiu o intervalo (geralmente 10.000 km ou 12 meses). Inclui troca de óleo e filtros. Ignorar pode invalidar garantia. Mecânico reseta após revisão.'},
  {id:'cinto',   icon:'cinto',    color:'c-red',   nome:'CINTO DE SEGURANÇA',  desc:'Ocupante detectado sem cinto afivelhado.',                       det:'O cinto reduz até 45% o risco de morte. Sem cinto, o corpo continua em movimento e colide com painel, volante ou para-brisa na mesma velocidade do impacto. Multa grave.'},
  {id:'porta',   icon:'porta',    color:'c-red',   nome:'PORTA ABERTA',        desc:'Uma ou mais portas não estão completamente fechadas.',           det:'Porta mal fechada pode abrir em curvas, especialmente com passageiros. Verifique todas as portas e o porta-malas. Em alguns carros inclui a tampa do tanque de combustível.'},
  {id:'cambio',  icon:'cambio',   color:'c-amber', nome:'FALHA NA TRANSMISSÃO',desc:'Problema no câmbio automático — "modo de emergência" ativo.',    det:'Pode ser temperatura alta do fluido, solenoides ou módulo. Em emergência o câmbio trava em uma marcha para você chegar a uma oficina. Câmbios automáticos são caríssimos para reparar.'},
  {id:'injecao', icon:'injecao',  color:'c-amber', nome:'SISTEMA DE INJEÇÃO',  desc:'Falha no gerenciamento eletrônico de combustível.',              det:'Bicos entupidos, sensor MAP, TPS, sonda lambda ou bomba fraca. Carro engasga, perde potência ou tem consumo alto. Diagnóstico eletrônico necessário.'},
  {id:'suspensao',icon:'suspensao',color:'c-amber',nome:'SUSPENSÃO / NÍVEL',   desc:'Falha na suspensão eletrônica ou pneumática.',                   det:'Em carros com suspensão a ar: compressor, válvulas ou sensores de altura. Em amortecedores ativos: módulo eletrônico. Suspensão com defeito prejudica manuseio e frenagem.'},
  {id:'check2',  icon:'check',    color:'c-amber', nome:'AVISO GERAL',         desc:'Alerta genérico do sistema — verifique o display de informações.',det:'Usado por vários sistemas para indicar condição anormal. Sempre consulte o display do painel ou o computador de bordo para identificar qual sistema está avisando.'},
];

let currentIdx = -1;
let doneSet = new Set();
let phase = 'idle';
let shuffled = shuffle([...Array(LIGHTS.length).keys()]);
let shPos = 0;

function shuffle(a){ for(let i=a.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[a[i],a[j]]=[a[j],a[i]]}return a;}

// Build grid
const panel = document.getElementById('lightsPanel');
const rows = [8,8,8]; // distribute into rows
let li = 0;
rows.forEach(cnt=>{
  const row = document.createElement('div');
  row.className = 'lights-row';
  for(let i=0;i<cnt && li<LIGHTS.length;i++,li++){
    const l = LIGHTS[li];
    const btn = document.createElement('div');
    btn.className = `light-btn ${l.color}`;
    btn.id = `lb-${li}`;
    btn.innerHTML = ICONS[l.icon] || `<svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="8" fill="none" stroke="currentColor" stroke-width="2"/></svg>`;
    btn.title = l.nome;
    btn.addEventListener('click',()=>activate(li));
    row.appendChild(btn);
  }
  panel.appendChild(row);
});
// remaining
if(li < LIGHTS.length){
  const row = document.createElement('div'); row.className='lights-row';
  while(li<LIGHTS.length){
    const l=LIGHTS[li];
    const btn=document.createElement('div');
    btn.className=`light-btn ${l.color}`;
    btn.id=`lb-${li}`;
    btn.innerHTML=ICONS[l.icon]||`<svg viewBox="0 0 24 24"><circle cx="12" cy="12" r="8" fill="none" stroke="currentColor" stroke-width="2"/></svg>`;
    btn.addEventListener('click',()=>activate(li));
    row.appendChild(btn); li++;
  }
  panel.appendChild(row);
}

function activate(idx){
  document.querySelectorAll('.light-btn.active').forEach(b=>b.classList.remove('active'));
  const btn = document.getElementById(`lb-${idx}`);
  if(!btn) return;
  btn.classList.add('active');
  currentIdx = idx;
  phase = 'question';
  render();
}

function nextAuto(){
  if(doneSet.size >= LIGHTS.length){ showComplete(); return; }
  if(shPos >= shuffled.length){ shPos=0; shuffled=shuffle([...Array(LIGHTS.length).keys()]); }
  let next = shuffled[shPos++];
  let tries=0;
  while(doneSet.has(next) && tries<LIGHTS.length){
    if(shPos>=shuffled.length){shPos=0;shuffled=shuffle([...Array(LIGHTS.length).keys()]);}
    next=shuffled[shPos++]; tries++;
  }
  activate(next);
}

function render(){
  const card = document.getElementById('quizCard');
  const btnRow = document.getElementById('btnRow');
  const progFill = document.getElementById('progFill');
  const scoreTxt = document.getElementById('scoreTxt');

  const pct = (doneSet.size/LIGHTS.length)*100;
  progFill.style.width = pct+'%';

  const l = LIGHTS[currentIdx];
  const colorClass = l.color.replace('c-','tc-');

  // rebuild card
  if(phase==='question'){
    card.innerHTML=`
      <div class="score" id="scoreTxt">${doneSet.size} / ${LIGHTS.length}</div>
      <div class="q-phase" style="color:#ffb300;animation:lightblink 1s infinite">⚡ NOVA LUZ ACENDEU NO PAINEL!</div>
      <div class="q-big-icon">${ICONS[l.icon]||''}</div>
      <div class="q-desc" style="color:#666;margin-top:0">Você sabe o que é esse símbolo?</div>
    `;
    // apply fill color to big icon svg
    const bigSvg = card.querySelector('.q-big-icon svg');
    if(bigSvg){ bigSvg.style.fill = colorOf(l.color); bigSvg.style.stroke = colorOf(l.color); bigSvg.style.width='64px'; bigSvg.style.height='64px'; }
    btnRow.innerHTML=`
      <button class="btn btn-listen" onclick="doListen()">🎙️ OUVIR RESPOSTA</button>
      <button class="btn btn-reveal" onclick="doReveal()">💡 REVELAR</button>
    `;
  }

  if(phase==='listen'){
    card.innerHTML=`
      <div class="score" id="scoreTxt">${doneSet.size} / ${LIGHTS.length}</div>
      <div class="q-phase" style="color:#00e676;animation:lightblink 0.8s infinite">🎙️ AGUARDANDO RESPOSTA...</div>
      <div class="q-big-icon">${ICONS[l.icon]||''}</div>
      <div class="q-desc" style="color:#333">Ouça a pessoa responder, depois revele</div>
    `;
    const bigSvg = card.querySelector('.q-big-icon svg');
    if(bigSvg){ bigSvg.style.fill = colorOf(l.color); bigSvg.style.stroke = colorOf(l.color); bigSvg.style.opacity='0.4'; bigSvg.style.width='64px'; bigSvg.style.height='64px'; }
    btnRow.innerHTML=`<button class="btn btn-reveal" onclick="doReveal()">💡 REVELAR RESPOSTA</button>`;
  }

  if(phase==='revealed'){
    card.innerHTML=`
      <div class="score" id="scoreTxt">${doneSet.size} / ${LIGHTS.length}</div>
      <div class="q-phase" style="color:#c8860a">✅ RESPOSTA</div>
      <div class="q-big-icon">${ICONS[l.icon]||''}</div>
      <div class="q-name ${colorClass} slidein">${l.nome}</div>
      <div class="q-desc slidein">${l.desc}</div>
    `;
    const bigSvg = card.querySelector('.q-big-icon svg');
    if(bigSvg){ bigSvg.style.fill=colorOf(l.color); bigSvg.style.stroke=colorOf(l.color); bigSvg.style.width='56px'; bigSvg.style.height='56px'; }
    btnRow.innerHTML=`
      <button class="btn btn-explain" onclick="doExplain()">🎓 EU EXPLICO DETALHADO</button>
      <button class="btn btn-next" onclick="doNext()">⏭ PRÓXIMA LUZ</button>
    `;
  }

  if(phase==='explained'){
    doneSet.add(currentIdx);
    document.getElementById(`lb-${currentIdx}`)?.classList.add('done');
    progFill.style.width = (doneSet.size/LIGHTS.length*100)+'%';
    card.innerHTML=`
      <div class="score" id="scoreTxt">${doneSet.size} / ${LIGHTS.length}</div>
      <div class="q-phase" style="color:#00bfff">🎓 EXPLICAÇÃO TÉCNICA</div>
      <div class="q-name ${colorClass}">${l.nome}</div>
      <div class="q-detail-box slidein">
        <div class="q-detail-title">📋 DETALHES PARA O APRESENTADOR</div>
        <div class="q-detail-text">${l.det}</div>
      </div>
    `;
    const btns = doneSet.size>=LIGHTS.length
      ? `<button class="btn btn-next" onclick="doNext()">⏭ PRÓXIMA LUZ</button><button class="btn btn-restart" onclick="doRestart()">🔄 REINICIAR</button>`
      : `<button class="btn btn-next" onclick="doNext()">⏭ PRÓXIMA LUZ</button>`;
    btnRow.innerHTML = btns;
  }
}

function colorOf(c){
  const m={
    'c-red':'#ff3030','c-amber':'#ffb300','c-green':'#00e676','c-blue':'#00bfff'
  };
  return m[c]||'#fff';
}

function doListen(){ phase='listen'; render(); }
function doReveal(){ phase='revealed'; render(); }
function doExplain(){ phase='explained'; render(); }
function doNext(){
  document.querySelectorAll('.light-btn.active').forEach(b=>b.classList.remove('active'));
  nextAuto();
}

function showComplete(){
  document.querySelectorAll('.light-btn.active').forEach(b=>b.classList.remove('active'));
  document.getElementById('quizCard').innerHTML=`
    <div class="q-phase" style="color:#ffb300;font-size:14px;letter-spacing:3px">🏆 PARABÉNS!</div>
    <div style="font-size:56px;margin:12px 0">🏆</div>
    <div class="q-name" style="color:#ffb300">QUIZ COMPLETO!</div>
    <div class="q-desc" style="margin-top:8px">Todas as ${LIGHTS.length} luzes foram explicadas com sucesso!</div>
  `;
  document.getElementById('btnRow').innerHTML=`<button class="btn btn-restart" onclick="doRestart()">🔄 REINICIAR QUIZ</button>`;
}

function doRestart(){
  doneSet.clear(); shPos=0; shuffled=shuffle([...Array(LIGHTS.length).keys()]);
  document.querySelectorAll('.light-btn').forEach(b=>b.classList.remove('active','done'));
  document.getElementById('progFill').style.width='0%';
  document.getElementById('btnRow').innerHTML='';
  document.getElementById('quizCard').innerHTML=`<div class="score" id="scoreTxt">0 / ${LIGHTS.length}</div><div class="idle-txt">⬆ Acenda uma luz no painel para começar</div>`;
}

setTimeout(()=>nextAuto(), 700);
</script>
</body>
</html>
