<!DOCTYPE html>
<html lang="fr">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Médecine Pratique — Site de révision (340 pathologies)</title>
<style>
:root{
  --bg:#f2f5f9; --card:#ffffff; --card2:#f8fafc; --text:#1b2534; --muted:#5b6b7f;
  --border:#dde5ee; --primary:#0e6ba8; --primary-soft:#e3f0fa; --danger:#d64545;
  --ok:#188a5b; --ok-soft:#e2f5ec; --warn:#c2760a; --warn-soft:#fdf1dd;
  --shadow:0 1px 3px rgba(15,35,60,.08),0 6px 18px rgba(15,35,60,.06);
  --radius:14px; --nav-h:58px; --max:1120px;
}
html[data-theme="dark"]{
  --bg:#0e1626; --card:#182338; --card2:#1d2a42; --text:#e5ecf5; --muted:#9db0c6;
  --border:#2c3c58; --primary:#4db1e8; --primary-soft:#12314a; --danger:#ff7b7b;
  --ok:#4cc98e; --ok-soft:#123428; --warn:#f0b455; --warn-soft:#3a2c12;
  --shadow:0 1px 3px rgba(0,0,0,.5),0 8px 22px rgba(0,0,0,.35);
}
*{box-sizing:border-box;margin:0;padding:0}
html{scroll-behavior:smooth}
body{
  font-family:-apple-system,BlinkMacSystemFont,"Segoe UI",Roboto,"Helvetica Neue",Arial,"Noto Sans",sans-serif;
  background:var(--bg); color:var(--text); line-height:1.6; font-size:16px;
  -webkit-text-size-adjust:100%;
}
a{color:var(--primary);text-decoration:none}
a:hover{text-decoration:underline}
button{font-family:inherit;font-size:1rem;cursor:pointer;border:none;background:none;color:inherit}
img,svg{max-width:100%}
::selection{background:var(--primary-soft)}

/* ===== Header ===== */
header.top{
  position:sticky;top:0;z-index:50;background:color-mix(in srgb,var(--card) 88%,transparent);
  backdrop-filter:blur(10px);-webkit-backdrop-filter:blur(10px);border-bottom:1px solid var(--border);
}
.hrow{display:flex;align-items:center;gap:12px;max-width:var(--max);margin:0 auto;padding:10px 16px}
.brand{display:flex;align-items:center;gap:10px;font-weight:800;font-size:1.02rem;white-space:nowrap;color:var(--text)}
.brand:hover{text-decoration:none}
.logo{width:34px;height:34px;flex:none;border-radius:9px;background:linear-gradient(135deg,#0e6ba8,#12a488);
  display:flex;align-items:center;justify-content:center;color:#fff;font-size:1.05rem}
.brand small{display:block;font-weight:500;font-size:.68rem;color:var(--muted);letter-spacing:.02em}
.searchwrap{flex:1;max-width:520px;position:relative;margin-left:auto}
#search{
  width:100%;padding:9px 14px 9px 38px;border-radius:999px;border:1px solid var(--border);
  background:var(--card2);color:var(--text);font-size:.95rem;outline:none;transition:border .15s;
}
#search:focus{border-color:var(--primary)}
.searchwrap .sicon{position:absolute;left:12px;top:50%;transform:translateY(-50%);color:var(--muted);pointer-events:none;font-size:.95rem}
.theme-btn{width:38px;height:38px;flex:none;border-radius:50%;border:1px solid var(--border);background:var(--card2);font-size:1.05rem;display:flex;align-items:center;justify-content:center;transition:transform .15s}
.theme-btn:hover{transform:scale(1.08)}
nav.topnav{display:flex;gap:4px;margin-left:6px}
nav.topnav a{
  padding:8px 14px;border-radius:999px;font-weight:600;font-size:.92rem;color:var(--muted);white-space:nowrap;
}
nav.topnav a:hover{background:var(--primary-soft);color:var(--primary);text-decoration:none}
nav.topnav a.active{background:var(--primary);color:#fff}

/* ===== Search overlay ===== */
#searchpanel{
  position:fixed;inset:0;z-index:90;display:none;background:rgba(8,15,28,.45);padding-top:70px;
}
#searchpanel.open{display:block}
.sp-inner{max-width:680px;margin:0 auto;background:var(--card);border:1px solid var(--border);
  border-radius:16px;box-shadow:var(--shadow);overflow:hidden;max-height:calc(100vh - 100px);display:flex;flex-direction:column}
.sp-head{display:flex;gap:10px;align-items:center;padding:12px 16px;border-bottom:1px solid var(--border)}
.sp-head input{flex:1;padding:10px 14px;border-radius:10px;border:1px solid var(--border);background:var(--card2);color:var(--text);font-size:1rem;outline:none}
#sp-results{overflow-y:auto;padding:8px}
.sp-item{display:block;width:100%;text-align:left;padding:10px 12px;border-radius:10px}
.sp-item:hover,.sp-item.sel{background:var(--primary-soft);text-decoration:none}
.sp-item .t{font-weight:700;color:var(--text)}
.sp-item .b{font-size:.78rem;color:var(--muted)}
.sp-item .sn{font-size:.83rem;color:var(--muted);display:-webkit-box;-webkit-line-clamp:1;-webkit-box-orient:vertical;overflow:hidden}
.sp-item mark{background:transparent;color:var(--primary);font-weight:800}
.sp-empty{padding:22px;text-align:center;color:var(--muted);font-size:.92rem}

/* ===== Bottom nav (mobile) ===== */
nav.bottom{
  display:none;position:fixed;bottom:0;left:0;right:0;z-index:60;background:var(--card);
  border-top:1px solid var(--border);padding:4px 6px calc(4px + env(safe-area-inset-bottom));
}
nav.bottom a{
  flex:1;display:flex;flex-direction:column;align-items:center;gap:1px;padding:6px 2px;border-radius:10px;
  color:var(--muted);font-size:.64rem;font-weight:600;text-decoration:none !important;
}
nav.bottom a .ic{font-size:1.15rem}
nav.bottom a.active{color:var(--primary)}

/* ===== Layout ===== */
main{max-width:var(--max);margin:0 auto;padding:26px 16px calc(90px + env(safe-area-inset-bottom));min-height:70vh}
.crumbs{display:flex;flex-wrap:wrap;gap:6px;align-items:center;font-size:.83rem;color:var(--muted);margin-bottom:14px}
.crumbs a{color:var(--muted);font-weight:600}
.crumbs a:hover{color:var(--primary)}
.crumbs .sep{opacity:.5}
h1.pageh{font-size:clamp(1.35rem,3.2vw,1.9rem);line-height:1.25;margin-bottom:6px;font-weight:800}
.lead{color:var(--muted);max-width:75ch;margin-bottom:18px}
.section{margin:26px 0}
.section>h2{font-size:1.15rem;margin-bottom:12px;font-weight:800}

/* ===== Cards & grids ===== */
.grid{display:grid;gap:14px}
.grid.depts{grid-template-columns:repeat(auto-fill,minmax(235px,1fr))}
.card{background:var(--card);border:1px solid var(--border);border-radius:var(--radius);box-shadow:var(--shadow)}
.dept-card{display:flex;flex-direction:column;gap:8px;padding:18px;position:relative;overflow:hidden;transition:transform .15s,box-shadow .15s;border-top:4px solid var(--dc,#0e6ba8)}
.dept-card:hover{transform:translateY(-3px);text-decoration:none}
.dept-card .ic{font-size:1.7rem}
.dept-card .nm{font-weight:800;color:var(--text);font-size:1.02rem;line-height:1.3}
.dept-card .mt{font-size:.8rem;color:var(--muted)}
.dept-card .go{color:var(--primary);font-weight:700;font-size:.85rem;margin-top:auto}
.minibar{height:6px;border-radius:99px;background:var(--border);overflow:hidden}
.minibar>span{display:block;height:100%;border-radius:99px;background:var(--ok);transition:width .3s}

/* ===== Badges & pills ===== */
.badge{display:inline-flex;align-items:center;gap:5px;padding:3px 10px;border-radius:999px;font-size:.72rem;font-weight:700;letter-spacing:.01em}
.badge.urg{background:var(--danger);color:#fff}
.badge.dept{background:color-mix(in srgb,var(--dc,#0e6ba8) 14%,transparent);color:var(--dc,#0e6ba8)}
html[data-theme="dark"] .badge.dept{color:color-mix(in srgb,var(--dc,#0e6ba8) 55%,#fff)}
.badge.spec{background:var(--primary-soft);color:var(--primary)}
.badge.ok{background:var(--ok-soft);color:var(--ok)}
.badge.warn{background:var(--warn-soft);color:var(--warn)}
.badge.off{background:var(--card2);color:var(--muted);border:1px solid var(--border)}

/* ===== Home hero ===== */
.hero{
  background:linear-gradient(140deg,var(--primary) 0%,#0b846e 100%);
  border-radius:20px;color:#fff;padding:clamp(22px,5vw,40px);position:relative;overflow:hidden;
}
.hero h1{font-size:clamp(1.5rem,4.5vw,2.5rem);font-weight:800;line-height:1.15;margin-bottom:10px}
.hero p{opacity:.92;max-width:62ch;font-size:clamp(.92rem,2vw,1.05rem)}
.hero .stats{display:flex;flex-wrap:wrap;gap:10px;margin-top:18px}
.hero .stat{background:rgba(255,255,255,.16);border:1px solid rgba(255,255,255,.25);padding:8px 15px;border-radius:12px;font-size:.85rem;font-weight:700}
.hero .stat b{font-size:1.15rem;display:block}
.quick{display:flex;flex-wrap:wrap;gap:10px;margin-top:18px}
.btn{
  display:inline-flex;align-items:center;justify-content:center;gap:8px;padding:10px 18px;border-radius:12px;
  font-weight:700;font-size:.92rem;border:1px solid transparent;transition:filter .15s,transform .15s;text-decoration:none !important;
}
.btn:hover{filter:brightness(1.06);transform:translateY(-1px)}
.btn.primary{background:var(--primary);color:#fff}
.btn.ghost{background:var(--card);border-color:var(--border);color:var(--text)}
.btn.white{background:rgba(255,255,255,.18);border-color:rgba(255,255,255,.4);color:#fff}
.btn.ok{background:var(--ok);color:#fff}
.btn.warn{background:var(--warn);color:#fff}
.btn.danger{background:var(--danger);color:#fff}
.btn.sm{padding:7px 13px;font-size:.82rem;border-radius:10px}

/* ===== Progress panel ===== */
.progress-card{padding:18px;display:flex;flex-wrap:wrap;gap:18px;align-items:center}
.progress-card .bigbar{flex:1;min-width:220px}
.p-label{display:flex;justify-content:space-between;font-size:.85rem;color:var(--muted);margin-bottom:6px;font-weight:600}
.pcounts{display:flex;gap:8px;flex-wrap:wrap}

/* ===== Dept view : accordions ===== */
.dept-head{display:flex;flex-wrap:wrap;gap:14px;align-items:center;padding:20px;border-left:5px solid var(--dc,#0e6ba8);margin-bottom:18px}
.dept-head .ic{font-size:2.2rem}
.dept-head h1{font-size:clamp(1.25rem,3vw,1.7rem)}
.dept-head .desc{flex-basis:100%;color:var(--muted);font-size:.92rem;max-width:85ch}
.dept-tools{display:flex;gap:8px;flex-wrap:wrap;margin-left:auto}
.acc{margin-bottom:14px;overflow:hidden}
.acc-head{
  width:100%;display:flex;align-items:center;gap:12px;padding:15px 18px;text-align:left;font-weight:800;font-size:1rem;
}
.acc-head:hover{background:var(--card2)}
.acc-head .num{flex:none;width:30px;height:30px;border-radius:9px;display:flex;align-items:center;justify-content:center;
  background:var(--primary-soft);color:var(--primary);font-size:.82rem;font-weight:800}
.acc-head .ttl{flex:1;min-width:0}
.acc-head .ttl .cnt{display:block;font-size:.74rem;color:var(--muted);font-weight:600}
.acc-head .chev{transition:transform .2s;color:var(--muted);flex:none}
.acc.open .acc-head .chev{transform:rotate(90deg)}
.acc-body{display:none;border-top:1px solid var(--border)}
.acc.open .acc-body{display:block}
.grp{padding:12px 18px 6px}
.grp+.grp{border-top:1px dashed var(--border)}
.grp h4{font-size:.8rem;text-transform:uppercase;letter-spacing:.05em;color:var(--muted);margin:6px 0 8px;font-weight:800}
.plist{list-style:none}
.plist li a{
  display:flex;align-items:center;gap:10px;padding:9px 12px;border-radius:10px;color:var(--text);font-size:.93rem;font-weight:600;
}
.plist li a:hover{background:var(--primary-soft);text-decoration:none}
.plist .st{margin-left:auto;flex:none;font-size:.7rem;font-weight:800}
.plist .nm i{font-style:normal;color:var(--muted);font-weight:500}

/* ===== Pathology page ===== */
.path-head{padding:22px;border-left:5px solid var(--dc,#0e6ba8)}
.path-head h1{font-size:clamp(1.25rem,3.2vw,1.75rem);line-height:1.3;margin:8px 0 10px}
.path-badges{display:flex;flex-wrap:wrap;gap:7px;margin-bottom:14px}
.status-tools{display:flex;flex-wrap:wrap;gap:8px}
.sec-block{padding:16px 22px;border-top:1px solid var(--border)}
.sec-block:first-child{border-top:none}
.sec-block.key{background:color-mix(in srgb,var(--dc,#0e6ba8) 6%,transparent)}
.sec-block.key p{font-weight:600}
.sec-block h3{display:flex;align-items:center;gap:8px;font-size:.95rem;margin-bottom:7px;color:var(--dc,#0e6ba8)}
html[data-theme="dark"] .sec-block h3{color:color-mix(in srgb,var(--dc,#0e6ba8) 55%,#fff)}
.sec-block p{font-size:.95rem;overflow-wrap:anywhere}
.pathnav{display:flex;gap:8px;margin-top:16px;flex-wrap:wrap}
.src-note{padding:13px 22px;font-size:.8rem;color:var(--muted);border-top:1px solid var(--border);display:flex;flex-wrap:wrap;gap:8px;align-items:center}

/* ===== Flashcards ===== */
.fc-setup,.qcm-setup{padding:20px;display:flex;flex-direction:column;gap:14px}
.fc-setup .row,.qcm-setup .row{display:flex;flex-wrap:wrap;gap:10px;align-items:center}
.field{display:flex;flex-direction:column;gap:4px;min-width:170px;flex:1}
.field label{font-size:.78rem;font-weight:800;color:var(--muted);text-transform:uppercase;letter-spacing:.04em}
select,input[type="number"]{
  padding:9px 12px;border-radius:10px;border:1px solid var(--border);background:var(--card2);color:var(--text);font-size:.95rem;
}
.checkline{display:flex;gap:8px;align-items:center;font-size:.92rem;font-weight:600;color:var(--muted)}
.fc-deck{max-width:760px;margin:0 auto}
.fc-card{
  background:var(--card);border:1px solid var(--border);border-radius:18px;box-shadow:var(--shadow);
  min-height:320px;display:flex;flex-direction:column;cursor:pointer;position:relative;
  transition:transform .15s;padding:26px;word-break:break-word;
}
.fc-card:hover{transform:translateY(-2px)}
.fc-front{margin:auto;text-align:center;padding:20px 6px}
.fc-front .n{font-size:clamp(1.2rem,3.4vw,1.7rem);font-weight:800;line-height:1.3}
.fc-front .hint{margin-top:18px;font-size:.8rem;color:var(--muted)}
.fc-back{display:flex;flex-direction:column;gap:13px}
.fc-back h4{font-size:.72rem;text-transform:uppercase;letter-spacing:.05em;color:var(--primary);margin-bottom:3px}
.fc-back p{font-size:.9rem}
.fc-actions{display:flex;gap:10px;margin-top:16px;flex-wrap:wrap}
.fc-actions .btn{flex:1;min-width:130px}
.fc-count{display:flex;justify-content:space-between;font-size:.83rem;color:var(--muted);font-weight:700;margin:0 4px 8px}
.deckbar{height:8px;border-radius:99px;background:var(--border);overflow:hidden;margin-bottom:18px}
.deckbar>span{display:block;height:100%;background:var(--primary);transition:width .3s}

/* ===== QCM ===== */
.qz-card{max-width:760px;margin:0 auto;padding:24px}
.qz-meta{display:flex;justify-content:space-between;font-size:.82rem;color:var(--muted);font-weight:700;margin-bottom:6px;flex-wrap:wrap;gap:6px}
.qz-q{font-size:1.02rem;font-weight:700;margin:8px 0 18px;line-height:1.5}
.qz-q .type{display:block;font-size:.72rem;color:var(--primary);text-transform:uppercase;letter-spacing:.05em;margin-bottom:6px}
.opt{
  display:block;width:100%;text-align:left;padding:13px 16px;border-radius:12px;border:2px solid var(--border);
  background:var(--card2);font-weight:600;font-size:.93rem;margin-bottom:9px;transition:border .12s,transform .08s;
}
.opt:hover:not(:disabled){border-color:var(--primary);transform:translateX(3px)}
.opt.good{border-color:var(--ok);background:var(--ok-soft);color:var(--ok)}
.opt.bad{border-color:var(--danger);background:color-mix(in srgb,var(--danger) 10%,transparent);color:var(--danger)}
.qz-feedback{padding:12px 14px;border-radius:12px;font-size:.88rem;margin:6px 0 14px;font-weight:600}
.qz-feedback.good{background:var(--ok-soft);color:var(--ok)}
.qz-feedback.bad{background:color-mix(in srgb,var(--danger) 9%,transparent);color:var(--danger)}
.qz-end{text-align:center;padding:16px}
.qz-end .score{font-size:2.6rem;font-weight:800;color:var(--primary)}
.qz-wrong{margin-top:16px;text-align:left}
.qz-wrong li{padding:9px 4px;border-bottom:1px dashed var(--border);font-size:.9rem;list-style:none}

/* ===== Sources ===== */
.src-card{display:flex;gap:14px;padding:18px;align-items:flex-start}
.src-card .ic{font-size:1.6rem;flex:none}
.src-card h3{font-size:1rem;margin-bottom:4px}
.src-card p{font-size:.88rem;color:var(--muted);margin-bottom:8px}
.note-box{padding:16px 18px;border-radius:12px;background:var(--warn-soft);color:var(--warn);font-size:.88rem;font-weight:600;margin:16px 0}
.note-box.blue{background:var(--primary-soft);color:var(--primary)}

/* ===== Utilities ===== */
.center{text-align:center}
.muted{color:var(--muted)}
.flex{display:flex;flex-wrap:wrap;gap:10px;align-items:center}
.spacer{flex:1}
kbd{background:var(--card2);border:1px solid var(--border);border-bottom-width:2px;border-radius:6px;padding:1px 7px;font-size:.78rem;font-family:inherit;font-weight:700}
.hidden{display:none !important}

/* ===== Responsive ===== */
@media (max-width:900px){
  nav.topnav{display:none}
}
@media (max-width:768px){
  nav.bottom{display:flex}
  main{padding:18px 12px calc(100px + env(safe-area-inset-bottom))}
  .hrow{flex-wrap:wrap;gap:8px;padding:10px 12px}
  .searchwrap{order:3;flex-basis:100%;max-width:none}
  .dept-head{padding:16px}
  .dept-tools{margin-left:0}
  .sec-block{padding:14px 16px}
  .fc-card{min-height:300px;padding:20px}
  .field{min-width:100%}
}
@media (max-width:420px){
  .brand small{display:none}
  .hero .stat{padding:6px 11px;font-size:.78rem}
}
@media print{
  header.top,nav.bottom,.theme-btn,#searchpanel{display:none !important}
  main{padding:0}
  body{background:#fff}
}
</style>
</head>
<body>
<header class="top">
  <div class="hrow">
    <a class="brand" href="#/">
      <span class="logo">⚕</span>
      <span>Médecine Pratique<small>Révision · 5 départements</small></span>
    </a>
    <div class="searchwrap">
      <span class="sicon">🔍</span>
      <input id="search" type="search" placeholder="Rechercher une pathologie…" autocomplete="off" aria-label="Rechercher une pathologie">
    </div>
    <nav class="topnav" id="topnav">
      <a href="#/" data-route="home">Accueil</a>
      <a href="#/revision" data-route="revision">Fiches</a>
      <a href="#/qcm" data-route="qcm">QCM</a>
      <a href="#/sources" data-route="sources">Sources</a>
    </nav>
    <button class="theme-btn" id="themeBtn" aria-label="Basculer le thème">🌙</button>
  </div>
</header>

<div id="searchpanel" role="dialog" aria-label="Résultats de recherche">
  <div class="sp-inner">
    <div class="sp-head">
      <span>🔍</span>
      <input id="sp-input" type="text" placeholder="Nom de la pathologie, signe, traitement…" autocomplete="off">
      <button class="btn sm ghost" id="sp-close">Fermer</button>
    </div>
    <div id="sp-results"></div>
  </div>
</div>

<main id="app" aria-live="polite"></main>

<footer style="max-width:var(--max);margin:0 auto;padding:20px 16px 30px;color:var(--muted);font-size:.78rem;text-align:center">
  Médecine Pratique — site de révision statique & hors ligne · Contenus enrichis d'après les sources officielles (MSD Manuels, OMS, HAS…) · Outil pédagogique, ne remplace pas les références officielles ni l'avis médical.
</footer>

<nav class="bottom" id="bottomnav">
  <a href="#/" data-route="home"><span class="ic">🏠</span>Accueil</a>
  <a href="#/revision" data-route="revision"><span class="ic">🃏</span>Fiches</a>
  <a href="#/qcm" data-route="qcm"><span class="ic">❓</span>QCM</a>
  <a href="#/sources" data-route="sources"><span class="ic">📚</span>Sources</a>
  <a href="#" id="nav-search"><span class="ic">🔍</span>Recherche</a>
</nav>

<script>
var DEPTS=[];
/* ============================================================
   DÉPARTEMENT 1 — MÉDECINE INTERNE (9 spécialités)
   ============================================================ */
DEPTS.push({
id:"med",name:"Médecine Interne",icon:"🩺",color:"#0d9488",
desc:"Médecine interne de l'adulte : les neuf grandes spécialités médicales, des urgences cardiologiques aux maladies systémiques, avec les pathologies essentielles à connaître sur le bout des doigts.",
specs:[

{id:"cardio",num:1,name:"Cardiologie & Pathologies Vasculaires",groups:[
{name:"Ischémie & Coronaropathies",paths:[
{n:"Syndrome Coronarien Aigu avec sus-décalage de ST (SCA ST+) — Infarctus du myocarde",q:"infarctus du myocarde",ur:true,
d:"Nécrose du myocarde secondaire à l'occlusion thrombotique complète d'une artère coronaire, le plus souvent sur plaque d'athérome rompue ; correspond à l'infarctus transmural (avec onde Q). Urgence absolue dont le pronostic dépend de la rapidité de reperfusion.",
s:"Douleur thoracique constrictive rétrosternale prolongée (> 20 min), en barre, irradiant vers le bras gauche, l'épaule et la mâchoire, résistante à la trinitrine ; sueurs, nausées, angoisse de mort ; formes atypiques chez le diabétique, la femme et le sujet âgé (dyspnée, malaise, tableau digestif).",
dx:"ECG en moins de 10 minutes : sus-décalage de ST dans au moins 2 dérivations contiguës, ou bloc de branche gauche de novo ; troponine élevée (sans attendre le résultat pour reperfuser) ; échocardiographie : hypokinésie segmentaire ; radiographie et bilan biologique associés.",
t:"Reperfusion en urgence : angioplastie primaire dans les 120 min (idéal < 90 min) ou thrombolyse si angioplastie inaccessible dans les délais ; quadrithérapie antithrombotique d'attaque (aspirine + inhibiteur P2Y12 + anticoagulant) ; bêtabloquant, statine forte dose, IEC ; prévention secondaire à vie et réadaptation cardiovasculaire.",
k:"Toute douleur thoracique impose un ECG en moins de 10 minutes : chaque minute perdue = myocyte perdu."}
,
{n:"Syndrome Coronarien Aigu sans sus-décalage de ST (SCA ST-) — Angor instable",q:"syndrome coronarien aigu",ur:true,
d:"Ischémie myocardique aiguë par thrombose coronaire incomplète ou obstruction transitoire : angor instable si la troponine reste normale, infarctus sans sus-décalage (NSTEMI) si la troponine s'élève.",
s:"Douleur angineuse de novo à l'effort, croissante ou survenant au repos, prolongée, calmée partiellement par la trinitrine ; équivalents : dyspnée, épigastralgies, sueurs ; le plus souvent chez l'adulte à risque cardiovasculaire.",
dx:"ECG répété : sous-décalage de ST, ondes T négatives ou normal ; troponine répétée à la 3e heure (stratification) ; score de risque GRACE ; coronarographie selon la stratification (haut risque si élévation de troponine, dynamique de ST, GRACE élevé).",
t:"Aspirine + inhibiteur P2Y12 + anticoagulation (HBPM ou fondaparinux) ; angiographie précoce (moins de 24-72 h) chez les patients à haut risque avec revascularisation ; bêtabloquant, statine, IEC ; jamais de thrombolyse dans le SCA ST-.",
k:"SCA ST- = pas de thrombolyse : la stratégie repose sur l'antithrombotique et l'angioplastie différée si le risque est élevé."}
,
{n:"Angor stable (chronique)",q:"angor stable",
d:"Ischémie myocardique d'effort par sténose coronaire athéromateuse fixe, sans nécrose ; traduction clinique de la maladie coronaire chronique, premier motif de coronarographie.",
s:"Douleur constrictive rétrosternale déclenchée par l'effort, le froid, le repas ou l'émotion, calmée en quelques minutes par l'arrêt ou la trinitrine sublinguale ; dyspnée d'effort ; examen physique souvent normal entre les crises.",
dx:"Épreuve d'effort ou échographie/IRM de stress (recherche d'ischémie), scanner coronaire (score calcique et sténoses), coronarographie si revascularisation envisagée ; bilan des facteurs de risque (HTA, diabète, lipides, tabac).",
t:"Traitement médical de fond : aspirine, statine, bêtabloquant, trinitrine à la demande ; contrôle strict des facteurs de risque, arrêt du tabac, activité physique ; revascularisation (angioplastie ou pontage) si angor invalidant ou ischémie étendue prouvée.",
k:"Angor typique = douleur d'effort rétrosternale calmée par le repos ou la trinitrine en moins de 10 minutes."}
]},
{name:"Insuffisance Cardiaque & Myocardiopathies",paths:[
{n:"Insuffisance Cardiaque Aiguë — Œdème aigu du poumon (OAP) cardiogénique",q:"œdème aigu du poumon",ur:true,
d:"Décompensation brutale de la fonction cardiaque avec congestion pulmonaire aiguë par élévation rapide des pressions capillaires pulmonaires ; l'OAP est la forme typique, urgence vitale.",
s:"Dyspnée aiguë brutale avec orthopnée, crépitants en marée montante aux deux bases, expectoration mousseuse rosée, sueurs, tachycardie, turgescence jugulaire, angoisse ; terrain : cardiopathie connue, trouble du rythme, infarctus récent, écart de sel ou de traitement.",
dx:"Clinique + radiographie thoracique (syndrome interstitiel puis alvéolaire, cardiomégalie) ; ECG, BNP/NT-proBNP élevé, échocardiographie (fraction d'éjection) ; recherche systématique du facteur déclenchant (arythmie, ischémie, écart thérapeutique, anémie, infection).",
t:"Position assise jambes pendues, oxygène, diurétique de l'anse IV (furosémide), dérivés nitrés si la tension le permet, ventilation non invasive si détresse ; inotropes (dobutamine) si choc ; traitement du facteur déclenchant ; relais par le traitement de fond de l'insuffisance cardiaque.",
k:"OAP = asseoir le patient, oxygène + diurétique IV + vasodilatateur : toujours chercher la cause de la décompensation."}
,
{n:"Insuffisance Cardiaque Chronique (HFrEF et HFpEF)",q:"insuffisance cardiaque",
d:"Incapacité chronique du cœur à assurer un débit adapté, avec dyspnée et rétention hydrosodée : à fraction d'éjection altérée (HFrEF ≤ 40 %) ou préservée (HFpEF ≥ 50 %, terrain hypertendu, âgé, obèse) ; classification NYHA I à IV.",
s:"Dyspnée d'effort, orthopnée, œdèmes des membres inférieurs déclives, prise de poids rapide, asthénie ; turgescence jugulaire, reflux hépato-jugulaire, tachycardie, galop B3, crépitants des bases.",
dx:"Échocardiographie (fraction d'éjection, morphologie, valves) ; BNP/NT-proBNP ; ECG, radiographie thoracique ; bilan étiologique : ischémique, hypertendu, valvulaire, rythmique, toxique (alcool), carenciel (sélénium, thiamine).",
t:"HFrEF : quadrithérapie de fond améliorant la survie — sacubitril-valsartan (ou IEC/ARA2) + bêtabloquant + antialdostérone + gliflozine — plus diurétique si congestion ; règles hygiéno-diététiques (sel, poids quotidien, activité adaptée), éducation, vaccinations grippale et pneumococcique ; dispositifs (défibrillateur, resynchronisation) selon indications ; suivi régulier.",
k:"La quadrithérapie (ARNI/IEC, bêtabloquant, antialdostérone, gliflozine) est le socle vital du traitement de l'HFrEF ; la prise de poids de 2 kg en 3 jours annonce une décompensation."}
,
{n:"Myocardiopathies (dilatée, hypertrophique, restrictive, du per-partum)",q:"myocardiopathie",
d:"Maladies primitives du myocardium : dilatée (dilatation du VG avec FE altérée ; génétique, toxique, post-myocarditique), hypertrophique (hypertrophie asymétrique septale souvent obstructive, maladie génétique à transmission dominante), restrictive (infiltration : amylose, hémochromatose), et du per-partum (dysfonction VG du dernier mois de grossesse ou des mois post-partum).",
s:"Signes d'insuffisance cardiaque, palpitations, troubles du rythme (fibrillation auriculaire, tachycardie ventriculaire) ; syncope d'effort et risque de mort subite dans la forme hypertrophique ; la myocardiopathie du per-partum survient chez une femme sans cardiopathie connue.",
dx:"Échocardiographie (dilatation, hypertrophie, fonction, obstruction sous-aortique) ; IRM cardiaque (cartographie, fibrose) ; ECG et Holter ; coronaires normales ; bilan génétique et familiaux (enquête de première ligne familiale dans la forme hypertrophique).",
t:"Traitement de l'insuffisance cardiaque ; forme hypertrophique obstructive : bêtabloquants, éviter les vasodilatateurs et la déplétion volémique, défibrillateur si risque de mort subite, myectomie/alcoolisation en cas d'obstruction invalidante ; dilatée : traitement de fond et exploration d'une greffe au stade avancé ; per-partum : traitement de l'insuffisance cardiaque et conseil sur les grossesses ultérieures selon la récupération de la FE.",
k:"Myocardiopathie hypertrophique : diurétiques et vasodilatateurs aggrave l'obstruction, et le risque de mort subite impose une stratification familiale."}
,
{n:"Péricardite aiguë et Tamponnade cardiaque",q:"péricardite",ur:true,
d:"Inflammation du péricarde, le plus souvent virale ou idiopathique ; l'épanchement péricardique abondant ou rapide peut se compliquer de tamponnade : compression des cavités cardiaques, urgence vitale extrême.",
s:"Douleur thoracique augmentée en décubitus, à l'inspiration et calmée penché en avant, fièvre, frottement péricardique ; tamponnade : dyspnée, hypotension, turgescence jugulaire, pouls paradoxal, assourdissement des bruits du cœur, choc.",
dx:"ECG : sus-décalage concave diffus, sous-décalage du PQ, microvoltage, alternance électrique si épanchement abondant ; échocardiographie (épanchement, collapse des cavités droites, tamponnade) ; biologie inflammatoire, troponine (myopéricardite), NFS.",
t:"Péricardite : AINS forte dose + colchicine 3 mois (prévention des récidives) + repos sportif ; corticoïdes seulement si contre-indication aux AINS ou forme récurrente réfractaire ; tamponnade : péricardocentèse échoguidée en urgence avec remplissage prudent en attendant.",
k:"Douleur soulagée penché en avant + frottement = péricardite ; tamponnade (hypotension + turgescence + pouls paradoxal) = drainage péricardique immédiat."}
,
{n:"Myocardite aiguë",q:"myocardite",ur:true,
d:"Inflammation du myocarde, le plus souvent virale (entérovirus, parvovirus B19) ou post-infectieuse et immune ; première cause d'insuffisance cardiaque aiguë à coronaires saines chez l'adulte jeune ; formes fulminantes avec choc cardiogénique.",
s:"Douleur thoracique pseudoinfarctus chez un adulte jeune, syndrome viral récent (myalgies, fièvre), dyspnée, palpitations, asthénie ; troubles du rythme, insuffisance cardiaque aiguë ; myocardite fulminante : choc, défaillance multiviscérale.",
dx:"Troponine élevée, ECG (troubles du rythme, anomalies diffuses), échocardiographie (dysfonction VG parfois segmentaire) ; IRM cardiaque = examen clé (œdème, rehaussement tardif) ; coronaires normales ; biopsie myocardique si forme fulminante ou doute.",
t:"Hospitalisation avec monitorage rythmique ; traitement symptomatique de l'insuffisance cardiaque, arrêt du sport 3 à 6 mois ; immunothérapie (immunoglobulines, immunosuppresseurs) selon la forme ; assistance circulatoire ou greffe dans les formes fulminantes.",
k:"Adulte jeune + douleur thoracique + troponine élevée + coronaires saines = myocardite ; l'IRM cardiaque confirme le diagnostic."}
]},
{name:"Troubles du Rythme & de la Conduction",paths:[
{n:"Fibrillation et Flutter auriculaires",q:"fibrillation auriculaire",
d:"Troubles du rythme supraventriculaire : la fibrillation auriculaire (activation atriale anarchique 350-600/min, rythme ventriculaire irrégulier) est le trouble du rythme soutenu le plus fréquent ; le flutter (macro-réentrée atriale à environ 300/min) est souvent régulier à 150/min.",
s:"Palpitations irrégulières (FA) ou rapides et régulières (flutter), dyspnée, asthénie, douleur thoracique ; complications : embolie systémique (accident vasculaire cérébral), décompensation cardiaque ; fréquemment asymptomatique et découvert fortuitement.",
dx:"ECG 12 dérivations : ondes f irrégulières sans onde P individuelle (FA) ou ondes F en dents de scie (flutter) ; recherche des facteurs favorisants : HTA, valvulopathie, hyperthyroïdie, alcool, apnées du sommeil, obésité ; échocardiographie (taille des oreillettes, valve, fonction VG).",
t:"Anticoagulation au long cours selon le score CHA2DS2-VASc (AOD ou AVK) pour prévenir l'AVC ; contrôle de la fréquence (bêtabloquant, digoxine) ou du rythme (cardioversion, antiarythmique, ablation) ; le flutter a une cure par ablation isthmique ; traiter les facteurs favorisants (perte de poids, sevrage alcoolique, traitement des apnées).",
k:"La FA est la première cause d'AVC cardia-embolique : évaluer le CHA2DS2-VASc et anticoaguler dès que le risque le justifie."}
,
{n:"Tachycardies Paroxystiques SupraVentriculaires (TPSV)",q:"tachycardie supraventriculaire",
d:"Tachycardies régulières à QRS fins de début et de fin brusques, souvent en rapport avec une réentrée intr nodale ou sur voie accessoire (Wolff-Parkinson-White) ; terrain : sujet jeune sans cardiopathie.",
s:"Palpitations en coup de tonnerre, oppression, polyurie en fin de crise, malaise, angoisse ; durée de quelques minutes à quelques heures ; crises récidivantes avec intervalle libre.",
dx:"ECG per-critique : tachycardie 150-250/min à QRS fins, ondes P rétrogrades (négatives en II) ou cachées dans le QRS ; ECG intercritique (onde delta du WPW) ; Holter, exploration électrophysiologique avant ablation.",
t:"Crise : manœuvres vagales (Valsalva, massage carotidien) puis adénosine IV en flash (ou vérapamil si QRS fins) ; cardioversion électrique si mauvaise tolérance ; traitement de fond : l'ablation par radiofréquence est curatrice dans la grande majorité des cas.",
k:"L'adénosine IV en flash interrompt la plupart des TPSV à QRS fins ; l'ablation par cathéter guérit définitivement."}
,
{n:"Tachycardie Ventriculaire (TV) et Fibrillation Ventriculaire (FV)",q:"tachycardie ventriculaire",ur:true,
d:"Tachycardie à QRS larges d'origine ventriculaire (> 100/min, plus de 3 battements) ; la fibrillation ventriculaire est un rythme d'arrêt circulatoire : activité électrique ventriculaire désorganisée, inefficace, mort subite si non traitée en quelques minutes.",
s:"Palpitations, malaise, syncope, détresse hémodynamique ou arrêt cardiaque (FV) ; TV monomorphe sur cardiopathie ancienne (séquelles d'infarctus) ; TV polymorphe : ischémie aiguë, hypokaliémie, allongement du QT (torsades de pointes).",
dx:"ECG per-critique : tachycardie régulière à QRS larges, dissociation auriculo-ventriculaire ; en arrêt : rythme de fibrillation ventriculaire sur le monitorage ; bilan : ionogramme (K, Mg), troponine, QT mesuré, échocardiographie, IRM, Holter.",
t:"TV mal tolérée ou FV : choc électrique externe immédiat + réanimation cardiopulmonaire (adrénaline 1 mg toutes les 3-5 min, amiodarone) ; TV bien tolérée : amiodarone IV, correction des troubles ioniques et de l'ischémie ; prévention : bêtabloquant, défibrillateur implantable si FE altérée ou mort subite récupérée, traitement de la cardiopathie.",
k:"Tachycardie régulière à QRS larges = TV jusqu'à preuve du contraire ; FV = choc électrique immédiat, chaque minute compte."}
,
{n:"Blocs Auriculo-Ventriculaires (BAV de grades 1, 2 et 3)",q:"bloc auriculo-ventriculaire",ur:true,
d:"Troubles de conduction entre oreillettes et ventricules : BAV du 1er degré (PR allongé > 200 ms), du 2e degré type I de Wenckebach (allongement progressif du PR puis QRS non conduit, bénin) ou type II (QRS non conduit brutal, risque de bloc complet), du 3e degré (dissociation auriculo-ventriculaire complète).",
s:"BAV 1 et 2 souvent asymptomatiques (palpitations, sensations de pauses) ; BAV 3 : bradycardie profonde 30-40/min, syncopes d'Adams-Stokes, insuffisance cardiaque, asthénie ; causes : dégénérative (maladie de Lenègre), infarctus, iatrogène (bêtabloquant, digoxine, amiodarone), infectieuse (maladie de Lyme).",
dx:"ECG 12 dérivations (PR allongé, ondes P non suivies de QRS, dissociation complète) ; Holter ; bilan étiologique (enzymes cardiaques, sérologie Lyme, médication) ; échocardiographie.",
t:"BAV 3 ou BAV 2 de type II symptomatique : stimulation cardiaque définitive (pacemaker) ; arrêt ou adaptation des bradycardisants ; traiter les causes réversibles (Lyme, infarctus) ; atropine ou isoprénaline en attente du pacemaker.",
k:"Syncopes d'Adams-Stokes par bradycardie extrême = BAV complet : pacemaker ; un BAV 2 de type II impose une stimulation sans attendre le bloc complet."}
,
{n:"Blocs de branche (gauche, droit) et dysfonction sinusale",q:"dysfonction sinusale",
d:"Retard de conduction intraventriculaire : bloc de branche gauche (souvent cardiopathie sous-jacente) ou droit (souvent bénin, isolé) sur l'ECG ; la dysfonction sinusale (maladie de l'oreillette) associe bradycardie sinusale inappropriée, pauses et alternance bradycardie-tachycardie.",
s:"Souvent asymptomatiques ; dysfonction sinusale : syncopes, lipothymies, asthénie, intolérance à l'effort, palpitations ; un bloc de branche gauche nouveau doit toujours faire rechercher une cardiopathie.",
dx:"ECG : QRS > 120 ms avec aspect caractéristique en V1/V6 ; Holter des pauses et de la fréquence minimale nocturne ; épreuve d'effort si chronotropisme douteux ; bilan de la cardiopathie sous-jacente.",
t:"Dysfonction sinusale symptomatique : pacemaker (stimulation atriale si conduction auriculo-ventriculaire intacte), adaptation des bradycardisants ; bloc de branche isolé sans cardiopathie : simple surveillance ; bloc de branche gauche avec altération de la FE ou syncopes : explorations spécialisées.",
k:"Pause sinusale > 3 secondes ou bradycardie symptomatique = pacemaker ; tout bloc de branche gauche nouveau = bilan cardiopathie."}
]},
{name:"Valvulopathies & Infections",paths:[
{n:"Sténose et Insuffisance Mitrale",q:"sténose mitrale",
d:"Sténose mitrale : rétrécissement de l'orifice (surface normale 4-6 cm² ; serrée < 1,5 cm²), quasi toujours d'origine rhumatismale ; insuffisance mitrale : reflux systolique par prolapsus dégénératif, ischémique, rhumatismale ou dilatation de l'anneau.",
s:"Sténose : dyspnée d'effort, hémoptysies, fibrillation auriculaire, œdèmes, roulement diastolique apexien avec renforcement présystolique (le souffle le mieux entendu en décubitus latéral gauche) ; insuffisance : souffle systolique apexien irradiant à l'aisselle, dyspnée, palpitations, éclat de B1.",
dx:"Auscultation + échocardiographie doppler (surface, gradient, taille de l'oreillette gauche, pression artérielle pulmonaire, fonction du VG) ; ECG (fibrillation auriculaire, hypertrophie auriculaire gauche) ; radiographie (oreillette gauche agrandie, surcharge) ; échocardiographie transœsophagienne avant chirurgie.",
t:"Prévention du rhumatisme articulaire aigu (pénicilline), anticoagulation en cas de FA ; sténose serrée symptomatique : commissurotomie percutanée par ballon (si valve souple) ou remplacement valvulaire ; insuffisance sévère symptomatique : réparation mitrale (chirurgie plastie) de préférence, ou remplacement ; prophylaxie de l'endocardite selon les situations à risque.",
k:"La sténose mitrale de l'adulte jeune est rhumatismale : penser à la prévention secondaire par pénicilline et à l'anticoagulation de la FA associée."}
,
{n:"Sténose et Insuffisance Aortiques",q:"sténose aortique",
d:"Sténose aortique : rétrécissement valvulaire calcifié dégénératif (sujet âgé) ou sur bicuspide congénitale (sujet jeune) ; serrée si surface < 1 cm² ou gradient moyen > 40 mmHg ; insuffisance aortique : reflux diastolique par atteinte valvulaire (rhumatismale, endocardite, anévrysme de l'aorte ascendante).",
s:"Sténose : triade majeure — angor, syncope d'effort, insuffisance cardiaque — qui annonce un pronostic sombre sans remplacement ; souffle éjectionnel râpeux au 2e espace intercostal droit irradiant aux carotides, B2 assourdi, pouls parvus et tardif ; insuffisance : souffle diastolique aspiratif au bord gauche du sternum, élargissement de la différentielle, pouls bondissant.",
dx:"Échocardiographie doppler (surface, gradient, vitesse maximale, FE, morphologie) ; ECG (hypertrophie du VG) ; scanner ou IRM avant chirurgie ; épreuve d'effort contre-indiquée si sténose serrée symptomatique.",
t:"Sténose aortique serrée symptomatique : remplacement valvulaire aortique chirurgical ou transcathéter (TAVI chez le sujet âgé ou fragile) — seul traitement curatif ; surveillance échographique si asymptomatique ; insuffisance sévère symptomatique : chirurgie valvulaire ; suivi médical : prévention de l'endocardite, contrôle des facteurs de risque.",
k:"L'apparition des symptômes (angor, syncope, insuffisance cardiaque) d'une sténose aortique serrée = indication opératoire, le risque de mort subite devient majeur."}
,
{n:"Valvulopathies tricuspidiennes",q:"insuffisance tricuspide",
d:"Atteinte de la valve tricuspide : l'insuffisance tricuspide est la plus fréquente, le plus souvent fonctionnelle par hypertension pulmonaire ou dilatation du ventricule droit ; la sténose est rare (rhumatismale, associée à l'atteinte mitrale).",
s:"Insuffisance cardiaque droite : œdèmes déclives, turgescence jugulaire avec onde V, hépatomégalie douloureuse, ascite ; souffle systolique xiphoïdien ou para-sternal gauche augmentant à l'inspiration (signe de Rivero-Carvallo).",
dx:"Échocardiographie (importance du reflux, pression artérielle pulmonaire, fonction du ventricule droit, valve) ; ECG ; bilan de l'hypertension pulmonaire et de la cardiopathie gauche.",
t:"Diurétiques et traitement de la cause (hypertension pulmonaire, cardiopathie gauche) ; réparation ou remplacement tricuspide si fuite organique sévère, ou prophylaxie tricuspide lors d'une chirurgie mitrale associée.",
k:"Souffle droit qui augmente à l'inspiration (Rivero-Carvallo) : l'insuffisance tricuspide est le plus souvent fonctionnelle, secondaire à une hypertension pulmonaire."}
,
{n:"Endocardite Infectieuse (valve native ou prothétique)",q:"endocardite infectieuse",ur:true,
d:"Greffe bactérienne sur l'endocarde valvulaire : streptocoques oraux et staphylocoque doré (devenu le premier germe sur valve native), entérocoques, groupe HACEK ; terrain : valvulopathie, prothèse valvulaire, toxicomanie intraveineuse, mauvaise hygiène dentaire, cathéter, hémodialyse.",
s:"Fièvre prolongée + souffle cardiaque + altération de l'état général ; signes périphériques : splénomégalie, hémorragies conjonctivales, taches cutanées de Janeway (indolores, paumes/plantes), faux panaris d'Osler (douloureux, pulpe des doigts), taches de Roth rétiniennes ; complications emboliques (AVC, splénique, rénale) et cardiaques (abcès, insuffisance cardiaque).",
dx:"Trois paires d'hémocultures avant toute antibiothérapie ; échocardiographie transthoracique puis transœsophagienne (végétations, abcès, désinsertion prothétique) ; critères de Duke ; syndrome inflammatoire, NFS, hématurie microscopique.",
t:"Antibiothérapie IV bactéricide adaptée au germe, prolongée 4 à 6 semaines (relais parfois oral selon protocoles) ; chirurgie valvulaire chez 30-40 % des patients : insuffisance cardiaque, embolies récidivantes, abcès, infection non contrôlée ; recherche et traitement de la porte d'entrée (dentaire, cutanée).",
k:"Fièvre + souffle cardiaque = hémocultures répétées puis échocardiographie : ne jamais débuter les antibiotiques avant les prélèvements."}
]},
{name:"Vasculaire & Hypertension",paths:[
{n:"Hypertension Artérielle Essentielle et HTA résistante",q:"hypertension artérielle",
d:"Élévation chronique de la pression artérielle (PA ≥ 140/90 mmHg au cabinet, ≥ 135/85 en automesure) sans cause identifiée dans 90-95 % des cas ; HTA résistante : non contrôlée malgré trois antihypertenseurs dont un diurétique à doses optimales avec une bonne observance.",
s:"Le plus souvent asymptomatique : céphalées occipitales matinales, acouphènes, phosphènes, épistaxis ; gravité par ses complications : AVC, infarctus, insuffisance cardiaque, néphropathie, artériopathie, rétinopathie hypertensive.",
dx:"Confirmation par automesure ou MAPA ; bilan initial : ionogramme, créatinine, glycémie, lipides, ECG (hypertrophie du VG), bandelette urinaire, fond d'œil ; dans l'HTA résistante : vérifier l'observance, la prise de AINS/corticoïdes, doser l'aldostérone et la rénine, éliminer une cause secondaire et une apnée du sommeil.",
t:"Mesures hygiéno-diététiques (sel < 5-6 g/j, perte de poids, activité physique, limitation de l'alcool, arrêt du tabac) ; monothérapie ou combinaison d'emblée (IEC ou ARA2 avec thiazidique et/ou inhibiteur calcique) avec titration rapide ; objectif PA < 130/80 mmHg chez la plupart des patients ; HTA résistante : ajouter la spironolactone en quatrième ligne.",
k:"L'HTA est le premier facteur de risque cardiovasculaire modifiable : traiter au seuil et à l'objectif, selon le risque global et non la PA seule."}
,
{n:"HTA secondaires (rénovasculaire, endocrinienne)",q:"hypertension artérielle secondaire",
d:"Hypertension de cause identifiée (5-10 % des HTA) : rénovasculaire (sténose de l'artère rénale par athérome ou dysplasie des femmes jeunes), endocrinienne (hyperaldostéronisme primaire — la plus fréquente —, phéochromocytome, syndrome de Cushing, hyper- ou hypothyroïdie, hyperparathyroïdie), parenchymateuse rénale, iatrogène (AINS, corticoïdes, contraceptifs), apnées du sommeil.",
s:"Signes d'appel : HTA du sujet jeune (< 40 ans), HTA résistante ou brutalement sévère, hypokaliémie, souffle abdominal, triade paroxystique du phéochromocytome (céphalées-sueurs-palpitations), prises pondérales, ronflements avec somnolence diurne, cycle anormal des PA.",
dx:"Orienté par la clinique : dosage rénine-aldostérone (rapport aldostérone/rénine élevé), métanéphrines plasmatiques ou urinaires, cortisol (freinage), TSH, échographie-doppler des artères rénales puis angio-IRM ou angio-TDM, polysomnographie.",
t:"Traitement de la cause : adrénalectomie (adénome de Conn, phéochromocytome après blocage adrénergique), revascularisation rénale si indiquée, traitement de l'apnée du sommeil, arrêt du médicament responsable ; antihypertenseurs en attendant et parfois à vie.",
k:"HTA du sujet jeune, résistante ou avec hypokaliémie : doser rénine et aldostérone — l'hyperaldostéronisme primaire est la première HTA secondaire."}
,
{n:"Urgences et poussées hypertensives (encéphalopathie, dissection)",q:"urgence hypertensive",ur:true,
d:"Urgence hypertensive : PA > 180/110 mmHg avec atteinte viscérale aiguë menaçante (encéphalopathie hypertensive, dissection aortique, œdème aigu du poumon, éclampsie, AVC, insuffisance rénale aiguë) ; poussée hypertensive : PA élevée sans retentissement viscéral immédiat.",
s:"Encéphalopathie : céphalées intenses, confusion, convulsions, troubles visuels, œdème papillaire ; dissection : douleur thoracique ou dorsale transfixiante, asymétrie des pouls, insuffisance aortique ; œdème aigu du poumon : dyspnée aiguë, crépitants ; poussée simple : souvent peu symptomatique.",
dx:"PA aux deux bras, fond d'œil, ECG, troponine, créatinine, ionogramme, protéinurie ; imagerie d'urgence selon le tableau (angio-TDM aortique, TDM cérébrale, radiographie du thorax) ; éliminer une cause (cocaïne, arrêt du traitement, rétention hydrosodée, grossesse).",
t:"Urgence hypertensive : hospitalisation en soins intensifs, baisse contrôlée et encadrée de la PA par voie IV (nicardipine, labétalol, urapidil) — environ 10-15 % la première heure, sans chute brutale (risque d'ischémie cérébrale ou myocardique) ; dissection : bêtabloquant IV + antihypertenseur, avis chirurgical urgent ; poussée simple : réajustement oral rapide et consultation précoce.",
k:"Dans l'urgence hypertensive, la PA doit baisser de façon contrôlée : une chute brutale expose à l'ischémie cérébrale et cardiaque."}
,
{n:"Artériopathie Oblitérante des Membres Inférieurs (AOMI) & Ischémie critique",q:"artériopathie des membres inférieurs",ur:true,
d:"Athérosclérose des artères des membres inférieurs : claudication intermittente (stade II de Leriche et Fontaine), douleur de décubissement (stade III), troubles trophiques et ulcères (stade IV = ischémie critique, menace de perte du membre).",
s:"Douleur à la marche disparaissant à l'arrêt (claudication du mollet, de la fesse, de la cuisse selon le niveau lésionnel), froideur des pieds, abolition des pouls, souffle fémoral ; ischémie critique : douleur de repos soulagée par la jampe pendante, ulcères noirs, douleurs nocturnes.",
dx:"Index de pression systolique (IPS < 0,90 ; souvent < 0,40 dans l'ischémie critique) ; écho-doppler artériel des membres inférieurs ; angio-TDM ou angio-IRM avant revascularisation ; bilan cardiovasculaire complet (coronaires, carotides : même terrain athéromateux).",
t:"Arrêt impératif du tabac ; marche quotidienne ; traitement médical optimal : antiagrégant plaquettaire, statine, IEC ou ARA2, contrôle du diabète ; revascularisation (endovasculaire ou pontage) si ischémie critique ou claudication invalidante ; soins de pieds et amputation mineure ou majeure dans les formes avancées.",
k:"L'AOMI est un marqueur de haut risque cardiovasculaire : la survie dépend du traitement médical (tabac, statine, antiagrégant), pas seulement du sauvetage du membre."}
,
{n:"Maladie Thrombo-Embolique Veineuse (MTEV) : TVP & Embolie Pulmonaire",q:"embolie pulmonaire",ur:true,
d:"Thrombose veineuse profonde (TVP) des membres inférieurs le plus souvent, compliquée ou non d'embolie pulmonaire (EP) ; facteurs de risque : immobilisation, chirurgie, cancer actif, grossesse et post-partum, contraception œstroprogestative, thrombophilie, voyage prolongé, âge.",
s:"TVP : douleur et œdème unilatéraux du mollet, chaleur, douleur à la dorsiflexion du pied ; EP : dyspnée brutale, douleur thoracique, tachycardie, polypnée, syncope ou malaise, parfois signes de choc dans les formes graves.",
dx:"Probabilité clinique (scores de Genève ou de Wells) + D-dimères pour exclure si probabilité faible ou intermédiaire ; écho-doppler veineux des membres inférieurs (TVP) ; angio-TDM des artères pulmonaires (EP) ; ECG, gaz du sang, échocardiographie si gravité ; recherche d'un cancer ou d'une thrombophilie selon le contexte.",
t:"Anticoagulation curative immédiate (HBPM, fondaparinux ou AOD) 3 mois minimum, prolongée si facteur de risque persistant ou idiopathique ; EP grave avec instabilité : thrombolyse systémique ; filtre cave temporaire si contre-indication à l'anticoagulation ; bas de compression et prophylaxie lors des situations à risque.",
k:"Probabilité clinique faible + D-dimères négatifs = EP exclue sans imagerie ; toute TVP proximale impose une anticoagulation curative immédiate."}
,
{n:"Phénomène de Raynaud et acrosyndromes",q:"phénomène de Raynaud",
d:"Spasme paroxystique des artères distales déclenché par le froid ou le stress, réalisant la triade pâleur-cyanose-rougeur des doigts : phénomène de Raynaud primaire (maladie de Raynaud, femme jeune, symétrique, bénin) ou secondaire (sclérodermie systémique, connectivites, outils vibrants, médicaments vasoconstricteurs).",
s:"Accès paroxystiques bilatéraux et symétriques (primaire) : doigts blancs puis bleutés puis rouges avec paresthésies ; signes de secondarité : asymétrie, apparition tardive, douleurs, ulcérations pulpaires ou cicatrices étoilées, télangiectasies, sclérodactylie.",
dx:"Capillaroscopie péri-unguéale (mégacapillaires et raréfaction = sclérodermie) ; anticorps (anticentromère, anti-Scl-70, antinucléaires) ; NFS, CRP ; distinction primaire/secondaire sur les critères cliniques et la capillaroscopie.",
t:"Protection contre le froid (gants chauffants), arrêt du tabac et des vasoconstricteurs (bêtabloquants, décongestionnants, caféine excessive) ; inhibiteurs calciques (nifédipine, amlodipine) au long cours ; iloprost IV ou sildénafil si ulcères sclérodermiques ; traitement de la maladie causale.",
k:"Raynaud symétrique d'une femme jeune = primitif ; Raynaud asymétrique, tardif ou compliqué d'ulcères = sclérodermie : capillaroscopie et anticorps."}
]}
]},

{id:"pneumo",num:2,name:"Pneumologie",groups:[
{name:"Pathologies Obstructives & Réactives",paths:[
{n:"Asthme de l'adulte (chronique et état de mal asthmatique)",q:"asthme",ur:true,
d:"Maladie inflammatoire chronique des bronches avec hyperréactivité bronchique et obstruction variable des voies aériennes, réversible sous traitement ; souvent atopique ; l'état de mal asthmatique est la crise résistante aux bronchodilatateurs, urgence vitale.",
s:"Dyspnée paroxystique sifflante, wheezing, toux nocturne, oppression thoracique, déclenchées par l'effort, les allergènes, les infections, le froid ou les AINS ; état de mal : tirage, sueurs, épuisement, puis silence auscultatoire et hypercapnie signant le danger.",
dx:"EFR avec test de réversibilité (VEMS augmentant d'au moins 12 % et 200 mL après bronchodilatateur) ; variabilité du débit expiratoire de pointe ; bilan allergologique ; radiographie pour éliminer un diagnostic différentiel ; suivi par questionnaire de contrôle (ACT).",
t:"Traitement de fond par paliers (GINA) : association CSI-formotérol en fond et à la demande (stratégie MART) ; éducation (technique inhalatoire, plan d'action écrit, éviction des allergènes) ; exacerbation : bronchodilatateur nébulisé, corticoïdes oraux 5-7 jours, oxygène ; état de mal : salbutamol continu, corticoïdes IV, sulfate de magnésium IV, appel réanimatoire.",
k:"Une consommation croissante de bronchodilatateur de secours (plus d'une bombe par mois) signe un asthme non contrôlé : revoir l'observance du fond et les facteurs déclenchants."}
,
{n:"Broncho-Pneumopathie Chronique Obstructive (BPCO) et exacerbations",q:"BPCO",
d:"Obstruction bronchique permanente et progressive liée au tabac (ou expositions professionnelles), associant bronchite chronique et emphysème ; classification GOLD 1-4 sur le VEMS et groupes ABE sur le risque d'exacerbations.",
s:"Toux chronique productive, dyspnée d'effort lentement croissante, sibilants ; exacerbations : majoration de la dyspnée et des crachats devenant purulents ; évolue vers l'insuffisance respiratoire chronique (cyanose, polyglobulie, œdèmes du cœur pulmonaire chronique).",
dx:"EFR post-bronchodilatateur : VEMS/CVF < 0,70 confirme l'obstruction non réversible ; gaz du sang ; radiographie (distension, emphysème) ; ECG et échographie si cœur pulmonaire ; dosage de l'alpha-1-antitrypsine si sujet jeune ou non fumeur.",
t:"Sevrage tabagique (seule mesure qui ralentit l'évolution) ; bronchodilatateurs de longue durée (LAMA + LABA), CSI si exacerbations répétées ; réhabilitation respiratoire, vaccinations grippale et pneumococcique ; exacerbation : bronchodilatateurs nébulisés, corticoïdes courts, antibiotique si purulence, oxygénothérapie ciblant une SpO2 88-92 % ; oxygénothérapie de longue durée et VNI au stade d'insuffisance respiratoire chronique.",
k:"Dans l'exacerbation de BPCO, l'oxygène vise une SpO2 de 88-92 % : l'hyperoxie aggrave l'hypercapnie et peut entraîner le coma."}
,
{n:"Dilatation des Bronches (DDB) / Bronchectasies",q:"bronchectasies",
d:"Dilatation permanente et irréversible des bronches avec inflammation chronique et surinfections récidivantes ; causes : post-infectieuses (tuberculose, coqueluche), mucoviscidose, déficit immunitaire, obstacle endobronchique, corps étranger, nombreuses formes idiopathiques.",
s:"Toux chronique avec expectorations abondantes, purulentes, en « moule bronchique », hémoptysies, infections respiratoires à répétition ; crépitants localisés, hippocratisme digital, douleurs thoraciques.",
dx:"Scanner thoracique haute résolution = examen clé (bronches dilatées ne s'amincissant pas, signe de l'anneau de sceau, impactions mucoïdes) ; EFR ; fibroscopie bronchique si obstacle suspecté ; bilan étiologique : test de sudation et mucoviscidose, immunité (IgG), bilan digestif.",
t:"Drainage quotidien des sécrétions (kinésithérapie respiratoire) ; antibiothérapie des poussées adaptée aux germes colonisants (H. influenzae, P. aeruginosa), antibiothérapie au long cours (macrolides) si poussées fréquentes ; vaccinations ; embolisation artérielle si hémoptysie ; résection chirurgicale rare, pour les formes localisées.",
k:"Expectorations chroniques abondantes et purulentes = scanner thoracique : les DDB sont une cause traitable d'infections respiratoires récidivantes."}
]},
{name:"Infections Pulmonaires",paths:[
{n:"Pneumonie Aiguë Communautaire (PAC) simple et grave",q:"pneumonie communautaire",ur:true,
d:"Infection aiguë du parenchyme pulmonaire acquise hors hôpital : pneumocoque (premier germe), germes atypiques (Legionella, Mycoplasma, Chlamydophila), virus ; gravité évaluée par le score CRB-65.",
s:"Début brutal : fièvre à 39-40 °C avec frissons, douleur thoracique latérale, toux et expectorations rouillées, herpès labial ; crépitants en foyer, souffle tubaire ; signes de gravité : confusion, polypnée ≥ 30/min, PA systolique < 90 mmHg, cyanose, hypoxémie.",
dx:"Radiographie thoracique (condensation alvéolaire systématisée) ; NFS, CRP ; SpO2 ; hémocultures et antigénuries si formes graves ; score CRB-65 (Confusion, Respiration, Blood pressure, 65 ans) pour la décision d'hospitalisation.",
t:"Amoxicilline orale en première intention (ajouter un macrolide ou une fluoroquinolone si suspicion de germe atypique ou forme hospitalisée) ; oxygène, hydratation, antipyrétiques ; hospitalisation si CRB-65 ≥ 1 ou comorbidités ; prévention par vaccination antipneumococcique et antigrippale des sujets à risque.",
k:"CRB-65 : chaque élément (confusion, FR ≥ 30/min, PA < 90/60, âge ≥ 65 ans) justifie l'hospitalisation d'une pneumonie communautaire."}
,
{n:"Pneumonies nosocomiales et acquises à l'hôpital",q:"pneumonie nosocomiale",
d:"Pneumonie survenant au moins 48 heures après l'admission, le plus souvent sous ventilation mécanique : bacilles Gram négatif (Pseudomonas aeruginosa, entérobactéries), staphylocoque doré, germes multirésistants selon les antibiothérapies préalables et l'écologie du service.",
s:"Fièvre ou hypothermie nouvelle, expectorations purulentes, hypoxémie, infiltration radiologique récente chez un patient hospitalisé ou ventilé ; dégradation hémodynamique ou neurologique.",
dx:"Radiographie ou scanner (infiltrat nouveau) ; prélèvements respiratoires protégés ou lavage broncho-alvéolaire avec cultures semi-quantitatives ; hémocultures ; procalcitonine ; distinguer colonisation et infection.",
t:"Antibiothérapie probabiliste à large spectre tenant compte de l'écologie locale et des facteurs de risque de résistance, réévaluée à 48-72 h sur les cultures ; durée courte (7-8 jours) si évolution favorable ; prévention : hygiène des mains, position demi-assise, sevrage ventilatoire rapide.",
k:"Chez un patient ventilé, toute fièvre avec infiltrat nouveau doit couvrir Pseudomonas et les germes multirésistants : l'antibiothérapie probabiliste se calibre sur l'écologie de l'unité."}
,
{n:"Tuberculose pulmonaire et pleurale",q:"tuberculose",
d:"Infection à Mycobacterium tuberculosis, transmission aérienne : infection latente puis tuberculose maladie chez environ 10 % des infectés (davantage si immunodépression, VIH, diabète, dénutrition) ; formes pulmonaires, pleurales, miliaires et extrapulmonaires.",
s:"Fièvre vespérale, sueurs nocturnes, amaigrissement, toux chronique de plus de 3 semaines, hémoptysies ; pleurésie : douleur et épanchement ; miliaire : dyspnée fébrile aiguë avec altération profonde de l'état général.",
dx:"Radiographie (infiltrats apicaux, caverne, adénopathies) ; recherche de BAAR sur 3 crachats (ou tubages, fibroscopie) avec microscopie, PCR et cultures ; sérologie VIH systématique ; IDR ou tests IGRA pour l'infection latente.",
t:"Quadrithérapie 2 mois (isoniazide, rifampicine, pyrazinamide, éthambutol) puis bithérapie 4 mois ; observance contrôlée, isolement respiratoire initial ; déclaration obligatoire et enquête autour du cas (dépistage des contacts) ; surveillance hépatique et ophtalmologique.",
k:"Toux chronique de plus de 3 semaines avec sueurs nocturnes et amaigrissement = 3 crachats à la recherche de BAAR + radiographie ; traiter 6 mois et dépister l'entourage."}
,
{n:"Abcès du poumon et empyème pleural",q:"abcès du poumon",
d:"Abcès pulmonaire : collection purulente intraparenchymateuse (fausse route, pneumonie nécrosante ; anaérobies, staphylocoque, entérobactéries) ; empyème : collection purulente de la cavité pleurale, complication des pleurésies infectées.",
s:"Fièvre prolongée et en plateau, douleur thoracique, expectorations purulentes parfois fétides, hémoptysies, amaigrissement ; empyème : douleur fébrile avec matité, dyspnée, syndrome inflammatoire majeur.",
dx:"Radiographie puis scanner (cavité à niveau hydro-aérique pour l'abcès, collection pleurale) ; ponction pleurale : pus, pH < 7,20, germes à la culture ; hémocultures ; recherche de la cause (fausse route, foyer dentaire, immunodépression, obstacle).",
t:"Antibiothérapie prolongée 4 à 6 semaines couvrant les anaérobies et les germes identifiés ; drainage thoracique de l'empyème (ou drainage radiologique de l'abcès) ; kinésithérapie de drainage ; chirurgie (décortication, résection) si échec ; traitement de la cause.",
k:"Expectoration fétide ou cavité à niveau hydro-aérique = abcès à anaérobies ; tout empyème impose un drainage."}
,
{n:"Bronchite aiguë et coqueluche de l'adulte",q:"coqueluche",
d:"Inflammation bronchique aiguë d'origine virale (90 % des cas) chez le sujet sain, sans atteinte parenchymateuse ; la coqueluche (Bordetella pertussis), souvent atténuée chez l'adulte, provoque une toux persistante très contagieuse pour le nourrisson.",
s:"Toux sèche puis grasse de 1 à 3 semaines, sans fièvre élevée ni signes de gravité, sibilants possibles ; coqueluche : quintes de toux persistantes (plus de 2-3 semaines) avec reprise inspiratoire, vomissements, sueurs, parfois syncopes de toux.",
dx:"Clinique ; radiographie normale en cas de doute ; coqueluche : PCR naso-pharyngée (3 premières semaines), sérologie ensuite, hyperlymphocytose évocatrice ; pas d'examen utile pour la bronchite virale.",
t:"Bronchite : traitement symptomatique, pas d'antibiotique systématique (sauf terrain à risque) ; coqueluche : macrolide (azithromycine 3-5 jours) pour limiter la contagiosité, antibioprophylaxie des sujets contacts, vaccination de rappel de l'adulte et stratégie du cocooning autour des nouveau-nés.",
k:"Toux persistant plus de 3 semaines chez l'adulte = PCR coqueluche : macrolide et protection des nourrissons de l'entourage."}
]},
{name:"Vasculaires, Interstitielles & Pleurales",paths:[
{n:"Embolie pulmonaire (vue sous l'angle pneumologique)",q:"embolie pulmonaire",ur:true,
d:"Obstruction aiguë du lit artériel pulmonaire par un thrombus veineux, responsable de cœur pulmonaire aigu ; deuxième grande cause de dyspnée aiguë aux urgences, parfois révélatrice d'une thrombose veineuse profonde silencieuse ; les récidives exposent à l'hypertension pulmonaire thrombo-embolique chronique.",
s:"Dyspnée aiguë inexpliquée, tachycardie, douleur, syncope, hypoxémie avec hypocapnie initiale ; signes droits : turgescence jugulaire, galop droit, hypotension ; dyspnée chronique et intolérance à l'effort dans l'HTP post-embolique.",
dx:"Angio-TDM des artères pulmonaires (ou scintigraphie de ventilation-perfusion si contre-indication) ; D-dimères pour exclure si probabilité clinique faible ; ECG (tachycardie, aspect S1Q3T3), échocardiographie (dilatation et dysfonction du VD), gaz du sang.",
t:"Anticoagulation curative immédiate ; thrombolyse si EP grave avec instabilité ; soins de support (oxygène, remplissage prudent) ; au long cours : anticoagulation, recherche de cause (cancer, thrombophilie) ; HTP thrombo-embolique chronique : endartériectomie pulmonaire ou traitement médical spécialisé.",
k:"Toute dyspnée aiguë inexpliquée avec tachycardie et désaturation doit faire évoquer l'embolie pulmonaire, même sans signe de thrombose veineuse."}
,
{n:"Pathologies Pulmonaires Interstitielles Diffuses (PID) / Fibrose Pulmonaire Idiopathique (FPI)",q:"fibrose pulmonaire idiopathique",
d:"Groupe hétérogène de pneumopathies interstitielles : FPI (la plus fréquente et la plus grave, homme de plus de 60 ans), PID des connectivites, pneumopathies d'hypersensibilité, sarcoïdose, pneumoconioses, PID médicamenteuses ; évolution vers la fibrose et l'insuffisance respiratoire.",
s:"Dyspnée d'effort progressive, toux sèche chronique, crépitants secs bilatéraux des bases en « velcro », hippocratisme digital dans la FPI ; exacerbations aiguës de la FPI (dégradation rapide) ; retentissement : insuffisance respiratoire, hypertension pulmonaire.",
dx:"Scanner thoracique haute résolution (fibrose des bases, aspect en rayon de miel, réticulations) ; EFR : trouble ventilatoire restrictif avec baisse de la DLCO ; LBA et biopsies si nécessaire ; bilan auto-immun et antigénique ; diagnostic en réunion multidisciplinaire.",
t:"FPI : antifibrotiques (pirfénidone, nintédanib) qui ralentissent le déclin de la fonction ; oxygénothérapie, réhabilitation, vaccinations ; corticoïdes/immunosuppresseurs selon l'étiologie (sarcoïdose, connectivite, pneumopathie d'hypersensibilité) ; arrêt des expositions ; greffe pulmonaire dans les formes avancées.",
k:"Crépitants en velcro des bases + toux sèche chronique = scanner et EFR : la FPI se diagnostique en réunion multidisciplinaire et ses exacerbations mettent en jeu le pronostic vital."}
,
{n:"Sarcoïdose pulmonaire et systémique",q:"sarcoïdose",
d:"Granulomatose systémique non caséeuse de cause inconnue ; atteinte thoracique dans 90 % des cas (adénopathies hilaires et médiastinales, atteinte parenchymateuse) ; autres cibles : peau, œil, nerfs, cœur, reins (hypercalcémie), rate.",
s:"Souvent latente ou découverte sur une radiographie ; toux sèche, dyspnée, douleurs thoraciques, altération de l'état général ; syndrome de Löfgren (aigu, de bon pronostic) : fièvre, arthralgies, érythème noueux, adénopathies hilaires bilatérales ; uvéite antérieure, atteinte cardiaque rythmique.",
dx:"Scanner thoracique (adénopathies hilaires bilatérales, micronodules, fibrose) ; EFR (restrictif) ; enzyme de conversion élevée, hypercalcémie et hypercalciurie ; LBA lymphocytaire (rapport CD4/CD8 élevé) et biopsies (granulomes) ; bilan d'extension : ophtalmologique, cardiaque (IRM, Holter), rénal.",
t:"Abstention avec surveillance si peu symptomatique (régression spontanée dans près de la moitié des cas) ; corticothérapie prolongée si atteinte viscérale menaçante (cardiaque, neurologique, oculaire, pulmonaire sévère, hypercalcémie) ; méthotrexate en épargne cortisonique ; surveillance EFR, ophtalmologique et calcémie.",
k:"La triade de Löfgren (fièvre, arthralgies, érythème noueux + adénopathies hilaires bilatérales) est un mode d'entrée de bon pronostic de la sarcoïdose."}
,
{n:"Épanchement pleural exsudatif et transsudatif (Pleurésie)",q:"épanchement pleural",
d:"Accumulation de liquide dans la cavité pleurale : transsudat (protéines < 30 g/L, absence d'inflammation : insuffisance cardiaque, cirrhose, syndrome néphrotique) ou exsudat (protéines > 30 g/L ou critères de Light : rapport protéines pleurales/sériques > 0,5 et LDH > 0,6) d'origine inflammatoire, infectieuse ou tumorale.",
s:"Douleur thoracique majorée à l'inspiration profonde, dyspnée, matité à la percussion, abolition du murmure vésiculaire et des vibrations vocales ; fièvre si infection ; épanchements abondants : détresse et déviation médiastinale controlatérale.",
dx:"Radiographie (opacité déclive avec ligne concave) ; ponction pleurale exploratrice : critères de Light (protéines, LDH), cellularité, glucose, pH, cytologie, bactériologie et recherche de BK ; scanner ; biopsies pleurales si suspicion tumorale ou tuberculeuse.",
t:"Ponction évacuatrice si épanchement abondant ou dyspnéisant ; transsudat : traitement de la cause (insuffisance cardiaque, cirrhose) ; exsudat : traitement étiologique (tuberculose, pneumonie, cancer, embolie) ; empyème : drainage ; pleurodèse ou drainages itératifs des récidives néoplasiques symptomatiques.",
k:"Toute pleurésie exsudative inexpliquée impose la recherche d'une tuberculose et d'un cancer (cytologie, imagerie, biopsies)."}
,
{n:"Pneumothorax spontané et secondaire",q:"pneumothorax",ur:true,
d:"Épanchement gazeux de la cavité pleurale : spontané primitif (sujet jeune longiligne fumeur, rupture de bulles sous-pleurales) ou secondaire (BPCO, asthme, PID, tuberculose) ; le décollement comprime le poumon ; risque vital si pneumothorax compressif.",
s:"Douleur thoracique latérale brutale avec dyspnée ; tympanisme, abolition du murmure vésiculaire et des vibrations vocales ; formes complètes : détresse ; compressif : choc, cyanose, distension veineuse — urgence absolue.",
dx:"Radiographie thoracique de face (hyperclarté avec décollement pleural, absence de trame en dehors de la ligne) ; scanner si doute, forme bilatérale ou secondaire ; jamais d'attente d'imagerie si suspicion de pneumothorax compressif.",
t:"De petite taille et bien toléré : surveillance ou exsufflation à l'aiguille ; abondant ou mal toléré : drainage thoracique ; compressif : exsufflation immédiate à l'aiguille (2e espace intercostal) puis drainage ; récidives : symphyse pleurale chirurgicale (pleurodèse, VATS) ; arrêt du tabac, contre-indication temporaire à la plongée et à l'avion.",
k:"Pneumothorax compressif = exsufflation immédiate à l'aiguille sans attendre l'imagerie : c'est une urgence vitale."}
,
{n:"Insuffisance Respiratoire Chronique (IRC) et Syndrome d'Apnées du Sommeil (SAOS)",q:"syndrome d'apnées du sommeil",
d:"IRC : incapacité chronique à maintenir l'hématose (hypoxémie ± hypercapnie) sur poumon chronique (BPCO, PID, obésité, cyphoscoliose, maladies neuromusculaires) ; SAOS : collapsus répété des voies aériennes supérieures pendant le sommeil chez le ronfleur en surpoids, source de fragmentation du sommeil et de risque cardiovasculaire.",
s:"IRC : dyspnée chronique, cyanose, polyglobulie, œdèmes du cœur pulmonaire chronique, céphalées matinales de l'hypercapnie ; SAOS : ronflements sonores, apnées observées par l'entourage, somnolence diurne excessive (score d'Epworth), réveils en sursaut, nycturie, HTA, obésité abdominale.",
dx:"Gaz du sang (hypoxémie ± hypercapnie) ; EFR ; polysomnographie ou polygraphie ventilatoire : index apnées-hypopnées ≥ 5/heure avec symptômes ; ECG/échographie (cœur pulmonaire chronique) ; NFS (polyglobulie).",
t:"IRC : oxygénothérapie de longue durée (au moins 15 h/j) si hypoxémie sévère, ventilation non invasive si hypercapnie symptomatique, réhabilitation, vaccinations ; SAOS : perte de poids, pression positive continue (PPC) nocturne — traitement de référence — ou orthèse d'avancée mandibulaire ; dépistage et traitement des comorbidités cardiovasculaires.",
k:"Somnolence diurne + ronflements + HTA = polygraphie : le SAOS est fréquent, sous-diagnostiqué, et la PPC transforme le pronostic."}
]}
]},

{id:"gastro",num:3,name:"Gastro-Entérologie & Hépatologie",groups:[
{name:"Appareil Digestif Haut & Bas",paths:[
{n:"Ulcère Gastro-Duodénal (UGD) et complications (hémorragie, perforation)",q:"ulcère gastroduodénal",ur:true,
d:"Perte de substance de la muqueuse gastrique ou duodénale liée au déséquilibre agression-défense : Helicobacter pylori (plus de 80 %) et AINS/aspirine sont les deux grandes causes ; complications : hémorragie digestive, perforation, sténose pylorique.",
s:"Douleur épigastrique rythmée par les repas (ulcère duodénal : calmée par l'alimentation, réveillant le malade la nuit) ; complications : méléna ou hématémèse (hémorragie), péritonite épigastrique en bois (perforation), vomissements postprandiaux (sténose).",
dx:"FOGD avec biopsies antrales et fundiques (histologie, recherche de H. pylori : test rapide à l'uréase) ; test respiratoire à l'urée ou antigène fécal à distance des IPP ; NFS (anémie) ; scanner en urgence si suspicion de perforation (pneumopéritoine).",
t:"IPP double dose 4 à 8 semaines ; éradication systématique de H. pylori (trithérapie ou quadrithérapie selon les résistances) ; arrêt des AINS, coprescription d'IPP si indispensables ; hémorragie : hémostase endoscopique + IPP IV, transfusion restrictive ; perforation : chirurgie en urgence.",
k:"Tout ulcère gastrique doit être biopsié et contrôlé endoscopiquement pour éliminer un adénocarcinome ; l'éradication de H. pylori prévient les récidives."}
,
{n:"Gastrites aiguës et chroniques à Helicobacter pylori",q:"gastrite Helicobacter pylori",
d:"Inflammation de la muqueuse gastrique : aiguë (caustiques, AINS, alcool, stress) ou chronique, dominée par l'infection à Helicobacter pylori (présente chez la moitié de l'humanité), facteur d'ulcère, d'atrophie et d'adénocarcinome gastrique ; la gastrite fundique auto-immune (maladie de Biermer) donne une carence en B12.",
s:"Souvent muette : épigastralgies, nausées, ballonnements, pyrosis ; gastrite atrophique ou Biermer : anémie macrocytaire, signes neurologiques de la carence en B12 ; à long terme : ulcère, cancer gastrique, lymphome MALT.",
dx:"FOGD avec biopsies antrales et fundiques (histologie, H. pylori) ; test respiratoire à l'urée, antigène fécal (la sérologie ne permet pas de vérifier l'éradication) ; NFS, vitaminémie B12, ferritinémie si atrophie.",
t:"IPP puis éradication de H. pylori, avec contrôle de l'éradication par test respiratoire à 4-6 semaines si ulcère ou haut risque ; sevrage (alcool, tabac, AINS) ; supplémentation en B12 dans la maladie de Biermer ; surveillance endoscopique si gastrite atrophique ou métaplasie intestinale.",
k:"H. pylori est classé cancérogène : son éradication prévient l'ulcère et le cancer gastrique ; vérifier la guérison par test respiratoire."}
,
{n:"RGO (Reflux Gastro-Œsophagien) et œsophagite de Barrett",q:"reflux gastro-œsophagien",
d:"Passage anormal du contenu gastrique dans l'œsophage (incompétence du cardia, hernie hiatale) : pyrosis et régurgitations ; l'inflammation chronique peut mener à la métaplasie intestinale (œsophage de Barrett), précurseur de l'adénocarcinome œsophagien.",
s:"Pyrosis (brûlure rétrosternale ascendante) majoré en décubitus, penché en avant et après repas gras ou alcoolisés, régurgitations acides, toux nocturne, dysphonie matinale ; signes d'alarme imposant la FOGD : dysphagie, amaigrissement, anémie, hémorragie, âge supérieur à 50 ans.",
dx:"Chez le sujet jeune typique : diagnostic clinique avec traitement d'épreuve ; FOGD si signes d'alarme ou résistance aux IPP : œsophagite peptique (classification de Los Angeles), Barrett (biopsies étagées) ; pH-métrie et manométrie si doute ou avant chirurgie.",
t:"Hygiène : repas fractionnés, surélévation de la tête du lit, perte de poids, arrêt du tabac et de l'alcool ; IPP 4 à 8 semaines puis à la demande ou en continu si nécessaire ; œsophage de Barrett : IPP à vie et surveillance endoscopique programmée, résection ou ablation endoscopique en cas de dysplasie.",
k:"Dysphagie + amaigrissement chez un refluxeur ancien = FOGD en urgence : éliminer une complication (sténose, Barrett, cancer)."}
,
{n:"Maladies Inflammatoires Chroniques de l'Intestin (MICI) : Crohn & RCH",q:"maladie de Crohn",
d:"Maladie de Crohn : inflammation segmentaire et transmurale de tout le tube digestif (prédilection iléocæcale), évoluant par poussées ; rectocolite hémorragique : inflammation continue et superficielle du côlon, rectum toujours atteint, limitée au cadre colique.",
s:"Diarrhée chronique (glairo-sanglante dans la RCH), douleurs abdominales surtout de la fosse iliaque droite, amaigrissement, fièvre, aphtose buccale ; signes extra-digestifs : arthralgies, érythème noueux, uvéite, cholangite sclérosante (RCH) ; complications : sténoses, fistules et abcès (Crohn), colite aiguë grave avec risque de mégacôlon toxique.",
dx:"Iléocoloscopie avec biopsies étagées (granulomes dans le Crohn, atteinte continue dans la RCH) ; entéro-IRM ou vidéo-capsule ; calprotectine fécale (suivi de l'inflammation) ; bilan nutritionnel et inflammatoire ; coloscopie de dépistage du cancer après 8-10 ans d'évolution.",
t:"Poussées : corticoïdes ; entretien : immunosuppresseurs (azathioprine, méthotrexate) et biothérapies (anti-TNF, anti-intégrine, anti-IL-12/23) selon la sévérité ; corticorésistance ou complications : chirurgie (coloproctectomie curative dans la RCH, résections limitées dans le Crohn) ; sevrage tabagique (aggrave le Crohn), supplémentation (fer, B12, vitamine D).",
k:"RCH = rectorragies et diarrhée glairo-sanglante ; Crohn = douleur de la fosse iliaque droite avec fistules et sténoses ; la colite aiguë grave fait redouter le mégacôlon toxique."}
,
{n:"Appendicite aiguë de l'adulte",q:"appendicite",ur:true,
d:"Inflammation aiguë de l'appendice iléo-cæcal par obstruction de sa lumière (stercolithe, hyperplasie lymphoïde) : première cause d'abdomen aigu chirurgical, maximum d'incidence entre 10 et 30 ans ; risque de perforation et de péritonite en cas de retard.",
s:"Douleur péri-ombilicale migrant après quelques heures vers la fosse iliaque droite, défense au point de McBurney, anorexie, nausées, fièvre modérée ; signes de Rovsing et du psoas ; sujet âgé, femme enceinte et immunodéprimé : formes trompeuses au risque de retard.",
dx:"Clinique + hyperleucocytose à PNN et CRP ; échographie (femme jeune) ou scanner abdomino-pelvien (adulte) : appendice supérieur à 6 mm, infiltration de la graisse ; β-hCG systématique chez toute femme en âge de procréer.",
t:"Appendicectomie cœlioscopique avec antibioprophylaxie ; formes compliquées (abcès, plastron) : antibiothérapie et drainage, appendicectomie différée ; à jeun, antalgiques, prévention thrombo-embolique.",
k:"Douleur de la fosse iliaque droite avec fièvre et défense = appendicite jusqu'à preuve du contraire ; β-hCG chez toute femme en âge de procréer."}
,
{n:"Occlusion intestinale aiguë (strangulation, obstruction, bride)",q:"occlusion intestinale",ur:true,
d:"Arrêt du transit intestinal : occlusion par strangulation (étranglement herniaire, volvulus, torsion mésentérique — souffrance digestive immédiate) ou par obstruction (brides post-opératoires, tumeur sténosante, fécalome, intussusception) ; grêle et côlon sont concernés.",
s:"Douleurs abdominales paroxystiques, vomissements (précoces dans l'occlusion du grêle), arrêt des matières et des gaz, météorisme ; strangulation : fièvre, défense, tachycardie, choc ; hernie étranglée : masse inguinale douloureuse, tendue, non réductible.",
dx:"Radiographie puis scanner abdomino-pelvien (dilatation d'amont, niveaux hydro-aériques, pneumatose ou ischémie des anses si strangulation) ; ionogramme (déshydratation), NFS ; examen systématique des orifices herniaires.",
t:"Hospitalisation : à jeun, aspiration naso-gastrique, réhydratation et correction ionique, antibiothérapie si strangulation ; chirurgie urgente devant toute suspicion de souffrance digestive (résection) ; occlusion sur bride incomplète : traitement médical d'abord ; occlusion colique gauche : endoprothèse ou chirurgie.",
k:"Vomissements + arrêt des matières et des gaz + météorisme = occlusion ; toute hernie douloureuse non réductible = étranglement = chirurgie en urgence."}
,
{n:"Diverticulite colique et sigmoïdite",q:"diverticulite",
d:"Inflammation d'un ou plusieurs diverticules coliques (sigmoïde surtout) par obstruction et microperforation : complication de la diverticulose, fréquente après 50 ans dans les pays occidentaux ; poussées simples et compliquées (abcès, péritonite, fistule, sténose).",
s:"Douleur de la fosse iliaque gauche avec fièvre et troubles du transit (constipation ou diarrhée), défense locale ; formes compliquées : masse abdominale (abcès), péritonite, pneumaturie et fécalurie (fistule colovésicale) ; hémorragie digestive abondante possible par rupture d'une artère diverticulaire.",
dx:"Scanner abdomino-pelvien avec injection = examen clé (densification péri-diverticulaire, abcès, diffusion péritonéale) ; NFS, CRP ; examen cytobactériologique des urines ; coloscopie après refroidissement pour éliminer un cancer.",
t:"Poussée simple : repos digestif, antalgiques, antibiothérapie (amoxicilline-acide clavulanique ou quinolone avec métronidazole) ; compliquée : drainage d'abcès, chirurgie si péritonite ou échec ; prévention des récidives : régime riche en fibres ; résection sigmoïdienne programmée si récidives.",
k:"Fosse iliaque gauche fébrile de l'adulte = diverticulite sigmoïdienne : scanner ; coloscopie après refroidissement pour éliminer un cancer."}
,
{n:"Troubles fonctionnels intestinaux (Syndrome de l'intestin irritable - SII)",q:"syndrome de l'intestin irritable",
d:"Trouble fonctionnel intestinal (hypersensibilité viscérale et perturbation de l'axe entéro-cérébral) : douleurs abdominales chroniques récurrentes et troubles du transit sans lésion organique (critères de Rome IV) ; première cause de consultation gastro-entérologique.",
s:"Douleurs abdominales améliorées par l'évacuation, ballonnements, alternance constipation-diarrhée, symptômes évoluant depuis plus de 6 mois, sans signe d'alarme (pas d'amaigrissement, de rectorragies, de réveils nocturnes, pas d'anémie).",
dx:"Diagnostic positif clinique (critères de Rome IV) ; examens normaux : NFS, CRP, sérologie cœliaque, calprotectine fécale négative (écarte une MICI) ; coloscopie seulement si signes d'alarme ou âge supérieur à 50 ans.",
t:"Information et rassurance ; régime pauvre en FODMAP, fibres solubles (ispaghule) ; antispasmodiques, probiotiques ; antidépresseurs à faible dose si douleur rebelle ; thérapie cognitivo-comportementale ; pas de chirurgie.",
k:"Le SII est un diagnostic positif (Rome IV) posé après avoir écarté les signes d'alarme : sang, amaigrissement, fièvre, anémie, symptômes nocturnes."}
]},
{name:"Hépatologie",paths:[
{n:"Hépatites virales aiguës (A, B, C, D, E)",q:"hépatite virale aiguë",ur:true,
d:"Inflammation hépatique aiguë d'origine virale : A et E (transmission fécale-orale, guérison sans séquelle, hépatite fulminante possible — surtout E chez la femme enceinte) ; B (parentérale et sexuelle, surinfection D possible), C (guérison spontanée dans 20-30 % des cas).",
s:"Asthénie intense, nausées, anorexie, ictère (urines foncées, selles décolorées), hépatomégalie sensible, prurit ; formes anictériques très fréquentes ; hépatite fulminante : encéphalopathie hépatique et troubles de la coagulation.",
dx:"Transaminases (ALAT 10 à 50 fois la normale), cholestase, TP (marqueur de gravité — hépatite fulminante si inférieur à 50 %) ; sérologies : IgM anti-VHA, AgHBs et IgM anti-HBc, ARN du VHC, IgM anti-VHE ; NFS-plaquettes ; échographie hépatique.",
t:"Traitement symptomatique (repos relatif, arrêt des hépatotoxiques dont alcool) ; hépatite fulminante : soins intensifs, transplantation en urgence ; prévention : hygiène (A, E), vaccination (A, B), précautions sexuelles et du sang (B, C) ; séro-vaccination du nouveau-né de mère porteuse du VHB.",
k:"Ictère fébrile avec transaminases très élevées = hépatite virale aiguë ; le TP est le marqueur de gravité qui fait craindre l'hépatite fulminante."}
,
{n:"Hépatites chroniques B et C",q:"hépatite chronique",
d:"Infections chroniques (VHB : 5 % des adultes immunocompétents ; VHC : 70-80 % des contaminations) évoluant silencieusement vers la cirrhose et le carcinome hépatocellulaire ; contamination parentérale, sexuelle (B), toxicomanie intraveineuse, transfusions anciennes (C), soins à risque.",
s:"Longtemps asymptomatiques (découverte fortuite) : asthénie, douleur de l'hypochondre droit ; signes d'hépatopathie chronique tardifs : angiomes stellaires, érythrose palmaire, splénomégalie ; complications après 20-30 ans : cirrhose, carcinome hépatocellulaire.",
dx:"Sérologies et charges virales (AgHBs, AgHBe, ADN du VHB ; ARN du VHC), transaminases, TP, plaquettes ; FibroScan (fibrose) et échographie ; dépistage VIH et hépatite D si VHB ; surveillance échographique semestrielle du carcinome si cirrhose.",
t:"VHB : analogues nucléosidiques suppressifs prolongés (ténofovir, entécavir) ; VHC : antiviraux à action directe, guérison dans plus de 95 % des cas en 8-12 semaines ; sevrage alcoolique, vaccination contre l'hépatite A ; dépistage des contacts ; surveillance du carcinome hépatocellulaire.",
k:"Le VHC se guérit aujourd'hui en 8-12 semaines d'antiviraux oraux (plus de 95 %) ; le VHB se contrôle à vie par analogues nucléosidiques."}
,
{n:"Cirrhose hépatique (alcoolique, virale, NASH/métabolique) et ses complications",q:"cirrhose",ur:true,
d:"Fibrose hépatique diffuse avec nodules de régénération, responsable d'insuffisance hépatocellulaire et d'hypertension portale ; causes : alcool (la première), VHB/VHC, stéatopathie métabolique, hémochromatose, maladies auto-immunes, cholestases chroniques.",
s:"Stigmates : angiomes stellaires, érythrose palmaire, circulation veineuse collatérale, splénomégalie, ictère ; hypertension portale : ascite, varices œsophagiennes, encéphalopathie ; les quatre grandes décompensations : hémorragie digestive, ascite, encéphalopathie, ictère.",
dx:"Biologie (TP, albumine, plaquettes, bilirubine — scores Child-Pugh et MELD) ; échographie-doppler (foie dysmorphique, hypertension portale, détection du carcinome) ; FibroScan ; endoscopie (varices) ; ponction d'ascite ; enquête étiologique complète.",
t:"Sevrage définitif d'alcool et traitement de la cause ; prévention des complications : bêtabloquant pour les varices, régime hyposodé et diurétiques pour l'ascite, vaccinations ; surveillance échographique semestrielle du carcinome hépatocellulaire ; transplantation hépatique en cas de décompensation ou de carcinome sur critères.",
k:"La cirrhose compensée reste silencieuse pendant des années : la première décompensation (ascite, hémorragie, ictère, encéphalopathie) divise l'espérance de vie."}
,
{n:"Ascite (simple et infectée / péritonite bactérienne spontanée)",q:"ascite",ur:true,
d:"Accumulation de liquide dans le péritoine, le plus souvent par hypertension portale de la cirrhose ; la péritonite bactérienne spontanée (PBS) est son infection sans perforation digestive — souvent pauci-symptomatique, dépistée par la ponction d'ascite.",
s:"Augmentation du périmètre abdominal, matité déclive, signe du flot, œdèmes, dyspnée ; PBS : fièvre ou hypothermie, douleurs abdominales, encéphalopathie aiguë ou décompensation inexpliquée, diarrhée ; chez le cirrhotique, toute dégradation doit faire évoquer une PBS.",
dx:"Ponction d'ascite exploratrice systématique à l'entrée et devant toute décompensation : cellularité (PNN supérieur ou égal à 250/mm³ = PBS), culture en flacon, protides, glucose, LDH ; hémocultures ; échographie.",
t:"Ascite simple : régime hyposodé, diurétiques (spironolactone puis furosémide), ponctions évacuatrices avec albumine si abondantes ; PBS : antibiothérapie IV immédiate (céphalosporine de 3e génération) 5-7 jours + albumine (prévention du syndrome hépato-rénal) ; prophylaxie secondaire par norfloxacine ou ciprofloxacine.",
k:"Chez un cirrhotique avec ascite, toute fièvre ou décompensation = ponction d'ascite : PNN ≥ 250/mm³ impose une antibiothérapie immédiate sans attendre les cultures."}
,
{n:"Hémorragie digestive par rupture de varices œsophagiennes",q:"varices œsophagiennes",ur:true,
d:"Hémorragie digestive haute par rupture de varices œsophagiennes (hypertension portale de la cirrhose) : urgence vitale, première cause de mortalité chez le cirrhotique décompensé ; récidive précoce fréquente dans les premiers jours.",
s:"Hématémèse et/ou méléna, collapsus, pâleur, tachycardie, marbrures ; terrain cirrhotique connu (ascite, ictère, angiomes) ; souvent déclenchée par une infection (PBS) ou un écart ; l'ulcère reste un diagnostic différentiel possible.",
dx:"NFS, plaquettes, TP, groupe sanguin, rai, urée ; FOGD dès la stabilisation hémodynamique (varices, saignement actif, ligature) ; bilan de la cirrhose ; pas de sonde naso-gastrique traumatique.",
t:"Réanimation : remplissage restrictif (objectif Hb 7-8 g/dL), correction de la coagulopathie selon besoins ; antibioprophylaxie systématique (céphalosporine 3e génération — réduit la mortalité) ; vasoconstricteur (terlipressine, somatostatine) ; ligature endoscopique ; échec : sonde de tamponnement puis TIPS ou chirurgie ; prévention secondaire : bêtabloquant + ligatures.",
k:"Hématémèse chez un cirrhotique = urgence absolue : antibiothérapie + terlipressine + FOGD pour ligature, sans sur-remplir."}
,
{n:"Encéphalopathie hépatique",q:"encéphalopathie hépatique",
d:"Syndrome neuropsychiatrique potentiellement réversible de l'insuffisance hépatique et des shunts porto-systémiques (accumulation d'ammoniaque et de toxines neuro-actives) ; déclenchée par infection, hémorragie digestive, constipation, diurétiques excessifs, sédatifs, azotémie.",
s:"Troubles fluctuants du sommeil (inversion nycthémérale), de l'humeur et de la vigilance : désorientation, confusion, ralentissement jusqu'au coma ; asterixis (flapping tremor) des mains tendues ; hypertonie, réflexes vifs.",
dx:"Clinique sur terrain hépatique (grades I à IV) ; ammoniémie souvent élevée mais peu spécifique ; éliminer les autres causes de confusion (hypoglycémie, hyponatrémie, infection, accident vasculaire cérébral, sevrage alcoolique, hématome sous-dural) ; recherche systématique du facteur déclenchant.",
t:"Traiter le facteur déclenchant (PBS en premier lieu, constipation, hémorragie) ; lactulose per os ou lavements (acidification colique et transit) ± rifaximine ; éviter les benzodiazépines et les diurétiques excessifs ; alimentation protéinée maintenue sans excès ; évaluation pour une transplantation hépatique.",
k:"Flapping tremor + confusion chez un cirrhotique = encéphalopathie hépatique : chercher et traiter le facteur déclenchant (péritonite bactérienne spontanée en tête)."}
,
{n:"Syndrome hépato-rénal",q:"syndrome hépato-rénal",ur:true,
d:"Insuffisance rénale fonctionnelle du cirrhotique décompensé (avec ascite), par vasoconstriction rénale majeure, sans cause rénale propre ; type 1 : rapidement progressif, de mauvais pronostic à court terme ; type 2 : installation lente avec ascite réfractaire.",
s:"Oligurie et élévation de la créatinine malgré l'arrêt des diurétiques et un remplissage, chez un cirrhotique ascitique (souvent après une PBS ou une hémorragie) ; pas de protéinurie significative ni d'hématurie, sodium urinaire bas.",
dx:"Diagnostic d'élimination : absence de choc, d'infection non traitée, de néphrotoxiques, pas d'amélioration après remplissage par albumine pendant 48 h ; urée, créatinine, ionogramme urinaire ; ponction d'ascite (éliminer une PBS).",
t:"Terlipressine + albumine (traitement de référence du type 1) ; arrêt des diurétiques et des néphrotoxiques, ponctions évacuatrices avec albumine ; TIPS dans certains cas ; transplantation hépatique = seul traitement définitif ; prévention de la PBS (antibioprophylaxie).",
k:"Toute insuffisance rénale chez un cirrhotique ascitique impose d'éliminer d'abord une PBS et les néphrotoxiques, puis d'évoquer le syndrome hépato-rénal : terlipressine + albumine."}
,
{n:"Stéatose hépatique non alcoolique (NAFLD / NASH)",q:"stéatose hépatique",
d:"Stéatopathie métabolique associée à l'obésité, au diabète de type 2 et à la dyslipidémie : maladie hépatique chronique la plus fréquente au monde ; la stéatohépatite (NASH) peut évoluer vers la fibrose, la cirrhose et le carcinome hépatocellulaire.",
s:"Longtemps asymptomatique : asthénie, douleur sourde de l'hypochondre droit, découverte d'une cytolyse ou d'une hépatomégalie lors d'un bilan métabolique ; contexte d'obésité abdominale, HTA, diabète, dyslipidémie.",
dx:"Diagnostic d'exclusion (consommation d'alcool négligeable, sérologies virales négatives, pas de médicament stéatosant) ; score FIB-4, FibroScan (stéatose et fibrose) ; bilan métabolique complet ; biopsie seulement si doute sur la sévérité.",
t:"Perte de poids de 7 à 10 % (régime, activité physique, chirurgie bariatrique si obésité morbide) : seule mesure réellement efficace ; contrôle du diabète et des lipides (les statines sont sûres et indiquées sur le risque cardiovasculaire) ; sevrage alcoolique ; surveillance de la fibrose et du risque cardiovasculaire (première cause de mortalité).",
k:"Cytolyse « inexpliquée » chez un patient obèse ou diabétique = stéatopathie métabolique : évaluer la fibrose (FibroScan) — la mortalité est d'abord cardiovasculaire."}
,
{n:"Thrombose de la veine porte",q:"thrombose de la veine porte",ur:true,
d:"Obstruction de la veine porte par thrombus (aiguë ou chronique) : causes locales (cirrhose, carcinome hépatique, chirurgie splénectomique, infection abdominale) ou générales (syndrome myéloprolifératif, thrombophilie, contraception) ; risque d'ischémie mésentérique et d'hypertension portale.",
s:"Douleurs abdominales, fièvre, ascite, hémorragie digestive (gastropathie hypertensive) ; forme aiguë : tableau abdominal aigu, parfois infarctus mésentérique ; forme chronique : cavernome porte, hypersplénisme, varices.",
dx:"Écho-doppler des vaisseaux hépatiques (première intention) ; angio-TDM ou angio-IRM ; bilan de thrombophilie et de myéloprolifération (mutation JAK2) ; recherche de cirrhose et de carcinome ; endoscopie (varices).",
t:"Anticoagulation curative 6 mois minimum (à vie si thrombophilie ou syndrome myéloprolifératif) ; antibiothérapie si thrombose septique (pyléphlébite) ; traitement de la cause ; prévention du saignement des varices avant l'anticoagulation ; TIPS ou chirurgie dans certains cas.",
k:"Thrombose porte sur cirrhose = éliminer un carcinome hépatocellulaire ; thrombose porte du sujet jeune = chercher un syndrome myéloprolifératif (mutation JAK2)."}
]},
{name:"Pancréatologie & Voies Biliaires",paths:[
{n:"Pancréatite aiguë (biliaire, alcoolique, métabolique)",q:"pancréatite aiguë",ur:true,
d:"Auto-digestion enzymatique du pancréas : biliaire (migration lithiasique, 40 %) ou alcoolique (30 %) surtout ; forme œdémateuse (80 %, bon pronostic) ou nécrosante-hémorragique (20 %, mortalité 15-20 %) ; autres causes : hypertriglycéridémie, hypercalcémie, CPRE, médicaments, virus.",
s:"Douleur épigastrique transfixiante en barre, intense, irradiant en ceinture et vers le dos, nausées, vomissements, iléus réflexe ; signes de gravité : collapsus, cyanose des flancs (Grey-Turner) et de l'ombilic (Cullen), défaillance d'organe.",
dx:"Lipasémie supérieure à 3 fois la normale (diagnostic) ; échographie biliaire en urgence (cause) ; scanner à 72-96 h pour la nécrose (pas avant) ; CRP à 48 h (supérieure à 150 mg/L = gravité), score de Balthazar ; ionogramme, calcémie, triglycérides, bilan étiologique complet.",
t:"Hospitalisation : jeûne, réhydratation massive, antalgiques (paracétamol puis morphine), oxygène ; nutrition entérale précoce si forme grave ; antibiothérapie seulement si infection de nécrose (ponction guidée) ; pancréatite biliaire : CPRE en urgence si angiocholite, cholécystectomie avant la sortie ; drainage ou débridement des collections infectées.",
k:"Épigastralgie transfixiante + lipasémie > 3 N = pancréatite aiguë : échographie à la recherche d'une cause biliaire et réévaluation à 48 h (CRP) pour dépister la nécrose."}
,
{n:"Pancréatite chronique",q:"pancréatite chronique",
d:"Inflammation chronique destructrice du pancréas : alcool et tabac (70-80 %), formes héréditaires, tropicales ou obstructives ; aboutit à l'insuffisance exocrine (malabsorption) et endocrine (diabète de type 3c).",
s:"Douleurs épigastriques chroniques transfixiantes évoluant par poussées, amaigrissement, stéatorrhée (selles grasses, abondantes, flottantes), diabète ; complications : pseudokystes, sténose du cholédoque, thrombose splénique, dépendance aux antalgiques, risque de cancer.",
dx:"Scanner ou IRM (calcifications pancréatiques, dilatation canalaire, atrophie) ; cholangio-IRM ; élastase fécale abaissée (insuffisance exocrine) ; glycémie et HbA1c ; bilan nutritionnel.",
t:"Sevrage alcool-tabac (seule mesure modifiant l'histoire naturelle) ; extraits pancréatiques enzymatiques au cours des repas, régime hypolipidique et supplémentation vitaminique ; antalgiques progressifs jusqu'au bloc cœliaque ; insuline pour le diabète ; drainage des pseudokystes symptomatiques ; traitement endoscopique ou chirurgical des douleurs rebelles et des sténoses.",
k:"Douleurs épigastriques récidivantes + stéatorrhée + calcifications pancréatiques = pancréatite chronique ; le sevrage est la clé du pronostic."}
,
{n:"Lithiase biliaire (cholélithiase) et complications (angiocholite, cholécystite aiguë)",q:"lithiase biliaire",ur:true,
d:"Calculs de la vésicule biliaire : asymptomatiques dans 80 % des cas ; complications : colique hépatique, cholécystite aiguë (calcul enclavé dans le col vésiculaire), angiocholite (obstruction du cholédoque avec infection biliaire), pancréatite biliaire, fistule ou iléus biliaire.",
s:"Colique hépatique : douleur brutale de l'hypochondre droit, en coup de poignard, irradiant à l'épaule droite, avec nausées, apyrétique ; cholécystite : fièvre + douleur + signe de Murphy ; angiocholite : douleur + fièvre avec frissons + ictère (urgence).",
dx:"Échographie abdominale (calculs, paroi vésiculaire épaissie, dilation des voies biliaires) ; biologie (NFS, CRP, bilirubine, PAL, GGT, lipase) ; angiocholite : cholangio-IRM ou écho-endoscopie, hémocultures ; scanner si doute ou complication.",
t:"Colique hépatique : antalgiques et cholécystectomie programmée ; cholécystite : antibiothérapie et cholécystectomie précoce (moins de 72 h) ; angiocholite : antibiothérapie IV + drainage biliaire endoscopique urgent (CPRE avec sphinctérotomie) dans les 24 h ; pancréatite biliaire : cholécystectomie avant la sortie.",
k:"Douleur + fièvre + ictère = angiocholite = urgence : antibiothérapie et drainage biliaire sans délai."}
]}
]},

{id:"nephro",num:4,name:"Néphrologie & Troubles Hydro-Électrolytiques",groups:[
{name:"Insuffisance Rénale",paths:[
{n:"Insuffisance Rénale Aiguë (IRA) : fonctionnelle, organique, obstructive",q:"insuffisance rénale aiguë",ur:true,
d:"Baisse rapide de la fonction rénale (créatinine multipliée par 1,5-2 ou diurèse < 0,5 mL/kg/h pendant 6-12 h) : fonctionnelle (hypoperfusion des reins sains : déshydratation, hémorragie, choc), organique (atteinte intrinsèque : nécrose tubulaire aiguë ischémique ou toxique, glomérulonéphrite, néphrite interstitielle), obstructive (obstacle sur les voies urinaires : prostate, calcul, tumeur).",
s:"Oligurie ou anurie, œdèmes, nausées, vomissements, confusion, HTA ; signes d'urémie : prurit, urémie cutanée, péricardite, haleine uréférale ; orientation : soif et pli cutané (fonctionnelle), globe vésical ou colique (obstructive), contexte toxique ou inflammatoire (organique).",
dx:"Échographie rénale systématique (taille des reins, dilatation pyélocalicielle = obstacle) ; ionogramme, urée, créatinine ; bandelette urinaire et ECBU ; sodium urinaire et fraction d'excrétion du sodium (FENa < 1 % = fonctionnelle) ; protéinurie, échographie des voies urinaires ; étiologie guidée par le contexte.",
t:"Cause fonctionnelle : remplissage ; arrêt de tous les néphrotoxiques (AINS, IEC/ARA2, aminosides, produits de contraste) et adaptation des posologies ; obstructive : dérivation urinaire (sondage, néphrostomie) ; hyperkaliémie menaçante : antagonisation et épuration ; dialyse si oligoanurie prolongée, urémie, surcharge, acidose réfractaire ; nutrition et prévention du saignement.",
k:"Devant toute IRA : échographie (obstacle ?) + ECBU, arrêter les néphrotoxiques ; l'IRA fonctionnelle se corrige par le seul remplissage."}
,
{n:"Insuffisance Rénale Chronique (IRC) et néphroprotection",q:"insuffisance rénale chronique",
d:"Baisse permanente et progressive du débit de filtration (DFG < 60 mL/min/1,73 m² depuis plus de 3 mois), stades 1 à 5 ; causes principales : diabète et HTA (néphropathies vasculaires), glomérulonéphrites chroniques, polykystose, néphropathies obstructives et toxiques.",
s:"Longtemps silencieuse : asthénie, pâleur (anémie), prurit, œdèmes, HTA, nycturie ; complications : anémie, ostéodystrophie rénale, acidose métabolique, hyperkaliémie, maladie cardiovasculaire accélérée ; au stade terminal : urémie, urémie péricardique, dénutrition.",
dx:"DFG estimé (CKD-EPI) sur la créatinine ; protéinurie (rapport protéines/créatinine urinaire) ; ionogramme, calcium, phosphore, PTH, ferritine, bicarbonates ; échographie (taille des reins, dilatation) ; fond d'œil et bilan cardiovasculaire.",
t:"Néphroprotection : IEC ou ARA2 (surtout si protéinurie), PA < 130/80, équilibre glycémique, arrêt du tabac, éviter les néphrotoxiques et ajuster toutes les posologies au DFG ; traiter l'anémie (fer, agents stimulant l'érythropoïèse), les troubles phospho-calciques (chélateurs, vitamine D), l'acidose (bicarbonates) ; au stade 5 : information et préparation à l'épuration extrarénale (hémodialyse, dialyse péritonéale) ou greffe ; vaccinations.",
k:"La néphroprotection (IEC/ARA2 + PA < 130/80 + équilibre glycémique + arrêt du tabac) retarde la dialyse de plusieurs années ; ajuster les doses au DFG."}
]},
{name:"Glomérulopathies & Urologie Médicale",paths:[
{n:"Syndrome néphrotique (pur et impur)",q:"syndrome néphrotique",
d:"Fuite urinaire massive de protéines : protéinurie ≥ 3 g/j + hypoalbuminémie < 30 g/L + œdèmes ± hyperlipidémie ; pur si isolé (chez l'adulte : maladie des lésions glomérulaires minimales, hyalinose segmentaire et focale, néphropathie extramembraneuse, amylose, diabète) ; impur si hématurie, HTA ou insuffisance rénale associées (glomérulonéphrite).",
s:"Œdèmes blancs, mous et déclives, prise de poids, œdèmes palpébraux matinaux, anasarque, épanchements ; complications : thromboses veineuses et artérielles (perte d'antithrombine), infections à germes encapsulés (perte d'IgG), hyperlipidémie, hypovolémie.",
dx:"Protéinurie des 24 h ou rapport protéines/créatinine ≥ 3 g/g ; créatinine, électrophorèse des protides sériques ; complément sérique, immunofixation, anticorps (antinucléaires), sérologies (VHB, VHC, VIH) ; biopsie rénale chez l'adulte (histologie décisive) ; éliminer diabète, lupus, néoplasie, médicaments (AINS, lithium).",
t:"Régime hyposodé, diurétiques de l'anse pour les œdèmes ; IEC ou ARA2 (réduisent la protéinurie) ; anticoagulation prophylactique si albumine < 20 g/L ; statines ; corticoïdes et immunosuppresseurs selon l'histologie ; traitement de la cause ; vaccination antipneumococcique.",
k:"Œdèmes + protéinurie ≥ 3 g/j = syndrome néphrotique : biopsie rénale chez l'adulte ; albumine < 20 g/L = risque thrombotique élevé."}
,
{n:"Syndrome néphritique aigu",q:"syndrome néphritique",
d:"Inflammation glomérulaire aiguë d'origine immunitaire : hématurie macroscopique, protéinurie modérée, HTA, œdèmes et insuffisance rénale d'installation rapide ; post-infectieuse ou associée à une maladie systémique (lupus, vascularite, purpura rhumatoïde).",
s:"Urines « bouillon sale » ou coca-cola (hématurie), œdèmes périphériques, HTA parfois sévère avec céphalées, oligurie, asthénie ; contexte : angine ou infection cutanée récente, purpura, arthralgies, infection virale.",
dx:"Bandelette urinaire (sang + protéines) et sédiment (hématies dysmorphiques, cylindres hématiques) ; créatinine, ionogramme ; complément C3-C4 (abaissé dans les glomérulonéphrites post-infectieuses et lupiques), ASLO ; protéinurie quantifiée ; biopsie rénale si doute sur une glomérulonéphrite rapidement progressive.",
t:"Repos, restriction hydrosodée, diurétiques de l'anse (œdèmes, HTA), antihypertenseurs (inhibiteurs calciques) ; glomérulonéphrite post-streptococcique : guérison spontanée avec surveillance (protéinurie, fonction rénale) ; formes prolifératives ou vascularites : corticoïdes ± cyclophosphamide, échanges plasmatiques selon le type.",
k:"Hématurie macroscopique + HTA + œdèmes = syndrome néphritique aigu : penser à l'angine récente et doser le complément."}
,
{n:"Glomérulonéphrites aiguës post-streptococciques et chroniques",q:"glomérulonéphrite post-streptococcique",
d:"Glomérulonéphrite aiguë post-infectieuse : dépôts immuns 10 à 21 jours après une angine ou un impétigo à streptocoque bêta-hémolytique du groupe A ; les glomérulonéphrites chroniques (maladie de Berger à dépôts d'IgA, prolifératives) évoluent lentement vers l'insuffisance rénale terminale.",
s:"Syndrome néphritique 10 à 21 jours après l'épisode infectieux : œdèmes, urines foncées, HTA ; maladie de Berger : hématuries macroscopiques récidivantes contemporaines ou postérieures immédiates des infections ORL ; GN chroniques : HTA, protéinurie, dégradation lente et silencieuse du DFG.",
dx:"C3 abaissé avec normalisation en 6-8 semaines (post-streptococcique), ASLO et anti-DNase B élevés ; hématurie dysmorphique, protéinurie ; biopsie rénale si atypie ou évolution non résolutive ; surveillance prolongée (DFG, protéinurie, TA).",
t:"GNA post-streptococcique : traitement symptomatique (diurétiques, antihypertenseurs), guérison habituelle surtout chez l'enfant ; éradication du foyer streptococcique (entourage) ; GN chroniques : néphroprotection (IEC/ARA2, contrôle tensionnel), corticoïdes et immunosuppresseurs selon l'histologie et la sévérité.",
k:"Dans la maladie de Berger, l'hématurie suit l'infection ORL de 1 à 2 jours (contre 10-21 jours dans la GNA post-streptococcique) — le complément est normal dans la maladie de Berger."}
,
{n:"Infections urinaires basses (Cystite) et hautes (Pyélonéphrite aiguë)",q:"pyélonéphrite",ur:true,
d:"Infection urinaire basse (cystite : Escherichia coli dans 80 % des cas) : inflammation vésicale sans fièvre ; haute (pyélonéphrite aiguë) : atteinte du parenchyme rénal avec fièvre et douleur lombaire ; l'infection est compliquée si terrain particulier (grossesse, homme, obstacle, sonde, diabète, immunodépression).",
s:"Cystite : pollakiurie, brûlures mictionnelles, urines troubles, sans fièvre ; pyélonéphrite : fièvre à 38,5-40 °C avec frissons, douleur de la fosse lombaire exquise à la percussion, nausées, parfois tableau septique grave (pyonéphrose).",
dx:"Bandelette urinaire (leucocytes et nitrites positifs) ; ECBU avec antibiogramme avant l'antibiothérapie (systématique si fièvre, homme, grossesse, récidive) ; hémocultures si fièvre élevée ; échographie ou scanner si suspicion d'obstacle, de pyonéphrose ou complication.",
t:"Cystite simple de la femme : fosfomycine-trométamol en dose unique ou traitement court adapté aux recommandations ; pyélonéphrite simple : fluoroquinolone ou céphalosporine de 3e génération, relais oral selon l'antibiogramme, 7 à 10 jours ; hospitalisation si signes de gravité, grossesse, homme, vomissements ; drainage d'un obstacle infecté en urgence ; hydratation abondante.",
k:"Fièvre + douleur lombaire = pyélonéphrite : ECBU et hémocultures avant l'antibiothérapie ; toute infection urinaire de l'homme ou de la femme enceinte est compliquée."}
,
{n:"Lithiase urinaire (Colique néphrétique)",q:"colique néphrétique",ur:true,
d:"Calcul du haut appareil urinaire (oxalate de calcium dans 75 % des cas, acide urique, struvite) obstruant brutalement la voie excrétrice : colique néphrétique par mise en tension des voies urinaires ; facteurs : apports hydriques faibles, hypercalciurie, hyperuricosurie, terrain.",
s:"Douleur lombaire brutale, intense, en coup de poignard, irradiant vers l'aine et les organes génitaux externes, sans position antalgique (agitation) ; hématurie microscopique, nausées, pollakiurie si calcul bas situé ; fièvre = complication (pyélonéphrite obstructive).",
dx:"Scanner abdomino-pelvien sans injection (examen de référence : taille, siège, densité du calcul) ; échographie et radiographie d'alternative ; bandelette urinaire (hématurie) ; créatinine ; bilan métabolique à distance (calciurie, uricurie, parathyroïde si récidives).",
t:"Antalgiques : AINS en première intention (IV ou suppositoire), morphine si échec ; élimination spontanée attendue si calcul < 5-6 mm ; fièvre ou anurie = drainage urgent en urgence (sonde double J, néphrostomie) ; traitements des calculs : urétéroscopie, lithotripsie extracorporelle, néphrolithotomie percutanée selon taille et siège ; prévention : boissons abondantes et correction des anomalies métaboliques.",
k:"Colique néphrétique + fièvre = pyélonéphrite obstructive = drainage urgent, pas d'expectative ; l'AINS est l'antalgique de référence."}
,
{n:"Polykystose rénale autosomique dominante",q:"polykystose rénale",
d:"Maladie héréditaire autosomique dominante (gènes PKD1, PKD2) : kystes rénaux bilatéraux progressifs menant à l'insuffisance rénale terminale entre 50 et 70 ans ; atteintes associées : kystes hépatiques, anévrismes intracrâniens, HTA, valvulopathies, diverticulose.",
s:"Douleurs lombaires ou abdominales, hématurie (hémorragie intrakystique), HTA souvent révélatrice, infections de kystes, augmentation progressive du périmètre abdominal ; complications : insuffisance rénale chronique, kystes hépatiques, rupture d'anévrisme (HSA), lithiases.",
dx:"Échographie ou IRM (reins augmentés de taille, multiples kystes bilatéraux) ; critères de Pei selon l'âge et les antécédents familiaux ; dépistage familial (et génétique si forme atypique) ; IRM cérébrale si antécédents familiaux d'anévrisme ou d'hémorragie ; TA, DFG, échographie cardiaque.",
t:"Contrôle tensionnel strict (IEC/ARA2 en première ligne) ; hydratation abondante (2-3 L/j) ; tolvaptan chez l'adulte à fonction rénale en déclin rapide (ralentit la progression) ; éviter les néphrotoxiques ; traitement des infections et douleurs ; dialyse ou greffe au stade terminal (greffe de bon pronostic) ; dépistage des anévrismes si antécédents familiaux.",
k:"HTA du sujet jeune + gros reins kystiques + antécédents familiaux = polykystose ; dépister les anévrismes intracrâniens si famille avec hémorragie."}
]},
{name:"Troubles Hydro-Électrolytiques & Acido-Basiques",paths:[
{n:"Hyponatrémie et Hypernatrémie",q:"hyponatrémie",ur:true,
d:"Hyponatrémie (Na < 135 mmol/L) : hypovolémique (pertes digestives, diurétiques), euvolémique (SIADH : cancers, médicaments, affections neurologiques ou pulmonaires ; hypothyroïdie), hypervolémique (insuffisance cardiaque, cirrhose, syndrome néphrotique) ; hypernatrémie (Na > 145 mmol/L) : perte d'eau pure (soif altérée du sujet âgé, diabète insipide) ou surcharge sodée.",
s:"Hyponatrémie : asthénie, anorexie, nausées, crampes, confusion, convulsions et coma si Na < 120 mmol/L ou baisse rapide ; hypernatrémie : soif intense, fièvre, sécheresse des muqueuses, confusion, hypertonie, convulsions.",
dx:"Ionogramme sanguin et urinaire (Na, osmolalité) ; osmolalité plasmatique ; évaluation clinique du volume extracellulaire ; bilan étiologique du SIADH (scanner, médicaments, TSH, cortisol) ; glycémie (fausse hyponatrémie de l'hyperglycémie).",
t:"Hyponatrémie aiguë symptomatique : sérum salé hypertonique (3 %) avec correction limitée à 4-6 mmol/L les premières heures ; chronique : restriction hydrique (SIADH), arrêt des médicaments en cause, correction lente (8-10 mmol/L maximum par 24 h) ; hypernatrémie : compenser le déficit hydrique (eau orale ou solutés hypotoniques) à vitesse contrôlée (≤ 10 mmol/L/24 h).",
k:"Corriger la natrémie lentement (8-10 mmol/L par 24 h) : une correction trop rapide provoque le syndrome de démyélinisation osmotique."}
,
{n:"Hypokaliémie et Hyperkaliémie menaçante",q:"hypokaliémie",ur:true,
d:"Hypokaliémie (K < 3,5 mmol/L) : pertes digestives (vomissements, laxatifs), pertes rénales (diurétiques, hyperaldostéronisme, alcalose), transfert intracellulaire (insuline, bêta-2-mimétiques) ; hyperkaliémie (K > 5,5 mmol/L, menaçante > 6,5 ou avec signes ECG) : insuffisance rénale, IEC/ARA2/spironolactone, AINS, acidoses, catabolisme, hémolyse.",
s:"Hypokaliémie : faiblesse musculaire (quadricipitale en particulier), crampes, constipation, iléus, palpitations ; ECG : T aplati, onde U, sous-décalage du ST, allongement du QT, torsades de pointes ; hyperkaliémie : paresthésies, faiblesse ascendante, paralysie ; ECG : T amples et pointues en pic de tente, élargissement du QRS, puis asystole.",
dx:"Ionogramme (éliminer une fausse hyperkaliémie : hémolyse du prélèvement, garrot prolongé, thrombocytose) ; ECG systématique ; kaliurèse (basse = pertes extra-rénales) ; magnésémie (une hypomagnésémie entretient l'hypokaliémie) ; gaz du sang ; TA (HTA + hypokaliémie = hyperaldostéronisme).",
t:"Hypokaliémie : potassium oral (chlorure de potassium) ; IV si K < 3 mmol/L ou trouble du rythme (dilué, surveillance ECG) ; corriger la cause et l'hypomagnésémie associée ; hyperkaliémie avec signes ECG : calcium IV immédiat (stabilisation membranaire), insuline + glucose IV, bêta-2-mimétiques nébulisés, puis épuration (diurétique, résine, dialyse) ; arrêt des hyperkaliémiants.",
k:"Hyperkaliémie avec ECG modifié = calcium IV immédiat puis insuline-glucose ; hypokaliémie rebelle = doser le magnésium."}
,
{n:"Hypocalcémie et Hypercalcémie maligne",q:"hypocalcémie",ur:true,
d:"Hypocalcémie (calcium corrigé < 2,20 mmol/L) : hypoparathyroïdie (post-chirurgicale surtout, auto-immune), carence en vitamine D, pseudohypoparathyroïdie ; hypercalcémie (calcium corrigé > 2,60 mmol/L, grave > 3,50) : hyperparathyroïdie primitive (sujet ambulatoire) et cancers (métastases lytiques, myélome, sécrétion de PTHrp — sujet hospitalisé).",
s:"Hypocalcémie : paresthésies péribuccales et des extrémités, crampes, tétanie (Chvostek, Trousseau), laryngospasme, convulsions, QT long ; hypercalcémie : polyuro-polydipsie, nausées, vomissements, constipation, confusion, coma — « pierres, os, douleurs abdominales, confusions ».",
dx:"Calcémie corrigée à l'albuminémie, phosphorémie (élevée = hypoparathyroïdie, basse = carence en vitamine D), PTH, 25-OH-vitamine D, magnésémie ; ECG (QT long dans l'hypo-, QT court dans l'hypercalcémie) ; électrophorèse des protides, imagerie selon contexte.",
t:"Hypocalcémie symptomatique : gluconate de calcium IV lent sous monitorage ; entretien : calcium oral et calcitriol si hypoparathyroïdie, vitamine D native et calcium si carence ; corriger l'hypomagnésémie ; hypercalcémie : réhydratation saline IV massive d'abord, puis biphosphonates IV (acide zolédronique), dénosumab si réfractaire, corticoïdes (myélome, granulomatoses), dialyse si forme sévère.",
k:"Hypercalcémie = réhydrater d'abord, biphosphonates ensuite (le cercle vicieux déshydratation-hypercalcémie est mortel) ; tétanie + QT long = hypocalcémie."}
,
{n:"Acidose métabolique (trou anionique élevé ou normal) et alcalose métabolique",q:"acidose métabolique",
d:"Acidose métabolique (pH < 7,38, bicarbonates < 22 mmol/L) : à trou anionique élevé (acidocétose diabétique, acidose lactique, insuffisance rénale, intoxications à l'éthylène glycol ou au méthanol) ou à trou anionique normal (pertes de bicarbonates : diarrhées, acidose tubulaire rénale) ; alcalose métabolique (pH > 7,42, bicarbonates > 26) : pertes acides (vomissements, aspiration gastrique, diurétiques) ou apports excessifs de bicarbonates.",
s:"Acidose : dyspnée ample de Kussmaul (hyperventilation compensatrice), nausées, asthénie, confusion, coma ; alcalose : paresthésies, tétanie (baisse du calcium ionisé), troubles du rythme (hypokaliémie associée), hypoventilation compensatrice.",
dx:"Gaz du sang (pH, bicarbonates) et ionogramme avec calcul du trou anionique (Na − [Cl + HCO3], normal < 16 mmol/L) ; cétonémie, lactates, glycémie, urée-créatinine, osmolalité (trou osmolaire = intoxication) ; chlorurie urinaire pour l'alcalose (basse = pertes gastriques ou diurétiques, élevée = hyperaldostéronisme).",
t:"Acidose : traitement de la cause (insuline dans l'acidocétose, remplissage et antidotes des toxiques, épuration) ; bicarbonates seulement si pH < 7,1-7,2 ; surveillance du potassium (l'acidose masque un déficit potassique total) ; alcalose : remplissage salé + chlorure de potassium (chloro-sensible), traitement de la cause (spironolactone si hyperaldostéronisme), arrêt des diurétiques et des vomissements.",
k:"Devant tout trouble acido-basique : calculer le trou anionique ; l'acidose masque un déficit potassique global qui se révèle à la correction."}
]}
]},

{id:"endo",num:5,name:"Endocrinologie & Métabolisme",groups:[
{name:"Diabétologie",paths:[
{n:"Diabète Sucré de Type 1 et de Type 2",q:"diabète sucré",
d:"Hyperglycémie chronique : diabète de type 1 par destruction auto-immune des cellules bêta pancréatiques (déficit insulinique absolu, sujet jeune, cétose) ; de type 2 par insulinorésistance et déficit sécrétoire progressif (90 % des cas, terrain familial, obésité, sédentarité).",
s:"Polyurie, polydipsie, amaigrissement, asthénie ; type 1 : installation rapide en quelques jours ou semaines avec cétose chez un sujet jeune ; type 2 : longtemps asymptomatique, découvert fortuitement ou à l'occasion d'une complication (infection, bilan) ; autres types : gestationnel, secondaire (corticoïdes, pancréatopathie).",
dx:"Glycémie à jeun ≥ 1,26 g/L (à deux reprises), HbA1c ≥ 6,5 %, ou hyperglycémie ≥ 2 g/L avec symptômes ; anticorps anti-GAD et anti-îlots (type 1) ; bilan initial : fond d'œil, microalbuminurie, lipides, ECG, examen des pieds, recherche des critères du syndrome métabolique.",
t:"Type 1 : insulinothérapie intensive d'emblée (basal-bolus ou pompe) avec éducation (autosurveillance, comptage des glucides, adaptation des doses) ; type 2 : mesures hygiéno-diététiques + metformine, puis associations selon les comorbidités cardiorénales (inhibiteurs SGLT2, agonistes GLP-1, gliptines), insuline à un stade avancé ; éducation thérapeutique, vaccinations, suivi trimestriel de l'HbA1c.",
k:"Polyuro-polydipsie + amaigrissement + cétose chez un sujet jeune = type 1 = insuline d'emblée, jamais d'antidiabétique oral seul."}
,
{n:"Complications aiguës du diabète : Acidocétose, Coma hyperosmolaire, Hypoglycémie",q:"acidocétose diabétique",ur:true,
d:"Acidocétose diabétique (surtout type 1) : insulinopénie absolue aboutissant à hyperglycémie + cétose + acidose métabolique ; coma hyperosmolaire (type 2, sujet âgé) : hyperglycémie majeure (souvent > 6 g/L) avec déshydratation profonde sans cétose ; hypoglycémie iatrogène (insuline, sulfamés) : glycémie < 0,60 g/L.",
s:"Acidocétose : polyurie, dyspnée de Kussmaul, haleine acétonique, vomissements, douleurs abdominales pseudochirurgicales, déshydratation, confusion puis coma ; hyperosmolaire : altération profonde de la conscience, déshydratation majeure, convulsions ; hypoglycémie : sueurs, tremblements, faim, palpitations, confusion, convulsions, coma.",
dx:"Glycémie capillaire et cétonémie (ou cétonurie) immédiates ; gaz du sang (acidose métabolique à trou anionique élevé), ionogramme (potassium!), NFS ; hyperosmolaire : osmolalité plasmatique calculée élevée, fonction rénale ; toujours chercher le facteur déclenchant (infection, oubli d'insuline, infarctus).",
t:"Acidocétose : réhydratation IV saline, insuline IVSE à faible dose, apport de potassium dès la kaliémie vérifiée, prévention de l'œdème cérébral (enfant) ; hyperosmolaire : réhydratation très progressive, insuline à faible dose ; hypoglycémie : resucrage oral ou glucose IV (G30 %) si inconscient, glucagon IM ; éducation à la prévention ; traiter le facteur déclenchant.",
k:"Diabétique inconscient = glycémie capillaire immédiate : l'hypoglycémie se traite en quelques minutes ; acidocétose = remplissage + insuline IV + potassium."}
,
{n:"Complications chroniques : Rétinopathie, Néphropathie, Neuropathie, Pied diabétique",q:"complications du diabète",
d:"Complications microangiopathiques (rétinopathie diabétique — première cause de cécité de l'adulte jeune ; néphropathie — première cause d'insuffisance rénale terminale ; neuropathie sensitive distale) et macroangiopathiques (coronaropathie, artériopathie des membres inférieurs, AVC) ; le pied diabique associe neuropathie et artériopathie (ulcères, infections, ostéite).",
s:"Rétinopathie : souvent silencieuse jusqu'à la baisse d'acuité visuelle ; néphropathie : protéinurie puis insuffisance rénale ; neuropathie : paresthésies, brûlures, anesthésie « en chaussette », ulcérations indolores, neuropathie végétative (gastroparésie, diarrhée, hypotension orthostatique, troubles érectiles) ; pied : mal perforant plantaire, déformations, infection.",
dx:"Dépistage annuel : fond d'œil (ou photographie rétinienne), rapport protéines/créatinine urinaire et DFG, examen des pieds (monofilament, diapason, pouls), ECG ; évaluation cardiovasculaire globale (TA, lipides, tabac).",
t:"Équilibre glycémique (HbA1c individualisée vers 7 %), contrôle tensionnel strict (IEC/ARA2 si néphropathie), statine, arrêt du tabac = prévention de toutes les complications ; rétinopathie : photocoagulation laser, anti-VEGF intravitréens ; pied : éducation, soins podologiques, décharge de l'ulcère, revascularisation si ischémie, antibiothérapie des infections ; suivi multidisciplinaire.",
k:"Le dépistage annuel (fond d'œil, protéinurie, monofilament) précède les lésions irréversibles ; tout ulcère du pied diabique = radiographie (ostéite) et évaluation artérielle."}
]},
{name:"Pathologies Thyroïdiennes & Parathyroïdiennes",paths:[
{n:"Hypothyroïdie (Thyroïdite de Hashimoto, myxœdème)",q:"hypothyroïdie",
d:"Insuffisance de sécrétion des hormones thyroïdiennes : thyroïdite chronique auto-immune de Hashimoto (première cause, goitre ferme), causes iatrogènes (thyroïdectomie, iode 131, amiodarone, lithium), carence iodée ; le coma mixedémateux est la forme extrême, urgence vitale.",
s:"Asthénie, frilosité, prise de poids, constipation, bradycardie, peau sèche et infiltrée, syndrome dépressif, ralentissement psychomoteur, raucité de la voix, oligoménorrhée, alopécie, crampes ; coma mixedémateux : hypothermie, bradycardie majeure, hyponatrémie, confusion puis coma.",
dx:"TSH élevée avec T4L basse (hypothyroïdie franche) ; anticorps anti-TPO (Hashimoto) ; bilan lipidique (hypercholestérolémie), NFS (anémie), créatinine, CPK ; échographie si goitre ou nodule.",
t:"Lévothyroxine à vie, dose progressive chez le sujet âgé ou coronarien (risque d'angor ou d'arythmie), contrôle de la TSH à 6-8 semaines puis annuel ; coma mixedémateux : hospitalisation en soins intensifs, lévothyroxine IV, réchauffement progressif, hydrocortisone (insuffisance surrénale associée possible).",
k:"TSH élevée = hypothyroïdie ; débuter la lévothyroxine prudemment chez le coronarien ; coma avec hypothermie et bradycardie chez une hypothyroïdienne = coma mixedémateux."}
,
{n:"Hyperthyroïdie (Maladie de Basedow, adénome toxique)",q:"hyperthyroïdie",
d:"Thyrotoxicose : maladie de Basedow (anticorps stimulant le récepteur de la TSH : goitre diffus, orbitopathie, première cause), adénome toxique et goitre multinodulaire toxique ; l'orage thyrotoxique est l'urgence vitale (thyrotoxicose décompensée, souvent déclenchée par infection, chirurgie ou iode).",
s:"Intolérance à la chaleur, sueurs, amaigrissement avec appétit conservé, tachycardie ou fibrillation auriculaire, tremblement fin des mains, diarrhée, nervosité, aménorrhée ; Basedow : goitre vasculaire, exophtalmie, myxœdème prétibial ; orage : fièvre, agitation et délire, tachyarythmie, défaillance cardiaque.",
dx:"TSH basse ou indosable avec T4L (et T3L) élevées ; anticorps anti-récepteurs de la TSH (Basedow) ; échographie-doppler et scintigraphie (fixation diffuse = Basedow, nodule chaud = adénome toxique) ; ECG (fibrillation auriculaire).",
t:"Antithyroïdiens de synthèse (carbimazole) 12-18 mois avec surveillance de la NFS (agranulocytose) ; bêtabloquant symptomatique ; iode radioactif ou thyroïdectomie selon le contexte (récidive, goitre, désir de grossesse) ; orage thyrotoxique : soins intensifs, antithyroïdiens à forte dose, bêtabloquant, corticoïdes, refroidissement.",
k:"TSH basse + T4L élevée = hyperthyroïdie ; l'exophtalmie signe la maladie de Basedow ; l'orage thyrotoxique est une urgence vitale."}
,
{n:"Thyroïdites aiguës et subaiguës (de De Quervain)",q:"thyroïdite subaiguë",
d:"Inflammation thyroïdienne : subaiguë de De Quervain (post-virale, douloureuse, la plus fréquente des thyroïdites douloureuses), aiguë suppurée (bactérienne, rare), silencieuse ou du post-partum (auto-immunes, indolores) ; évolution en trois phases : thyrotoxicose brève, intervalle libre, hypothyroïdie transitoire.",
s:"De Quervain : douleur cervicale antérieure irradiant vers la mâchoire et l'oreille, fièvre, asthénie, goitre dur et douloureux à la palpation ; thyroïdites indolores : thyrotoxicose modérée puis asthénie et prise de poids ; la thyroïdite du post-partum survient dans l'année suivant l'accouchement.",
dx:"TSH basse et T4L élevée en phase initiale, puis hypothyroïdie ; VS très élevée et CRP (De Quervain) ; scintigraphie : fixation thyroïdienne quasi nulle (contre l'hyperfixation du Basedow) ; anticorps anti-TPO (formes auto-immunes).",
t:"De Quervain : AINS puis corticoïdes en dégression progressive ; bêtabloquant en phase de thyrotoxicose (pas d'antithyroïdiens de synthèse) ; formes auto-immunes : surveillance, lévothyroxine si hypothyroïdie ; thyroïdite suppurée : antibiothérapie et drainage ; guérison habituelle, environ 10 % d'hypothyroïdie définitive.",
k:"Douleur thyroïdienne + fièvre + thyrotoxicose = De Quervain : scintigraphie blanche et VS élevée ; corticoïdes, pas d'antithyroïdiens."}
,
{n:"Nodules thyroïdiens et cancers de la thyroïde",q:"nodule thyroïdien",
d:"Nodule thyroïdien (palpable chez environ 5 % des femmes, fréquent à l'échographie) : le plus souvent bénin (nodule colloïde, adénome) ; carcinome différencié (papillaire surtout, de bon pronostic) rare, favorisé par irradiation cervicale et antécédents familiaux ; carcinome médullaire (cellules C, calcitonine) parfois familial (NEM2).",
s:"Le plus souvent asymptomatique, découvert à la palpation ou à l'échographie ; signes de malignité : nodule dur et fixé, croissance rapide, adénopathie cervicale, dysphonie (nerf récurrent), dysphagie ; nodule toxique : signes d'hyperthyroïdie.",
dx:"Échographie thyroïdienne avec classification EU-TIRADS (échogénicité, microcalcifications, forme plus haute que large) ; TSH ; cytoponction à l'aiguille fine des nodules suspects (classification de Bethesda) ; scanner ou IRM si extension ; calcitonine si suspicion de carcinome médullaire.",
t:"Nodule bénin : surveillance échographique ; carcinome différencié : thyroïdectomie totale ± curage ganglionnaire, puis irathérapie et hormonothérapie suppressive selon le risque, suivi par thyroglobuline ; carcinome médullaire : chirurgie élargie et enquête génétique (RET) ; formes avancées : thérapies ciblées.",
k:"Devant tout nodule : TSH + échographie (EU-TIRADS), cytoponction si nœud suspect — la grande majorité des nodules sont bénins."}
,
{n:"Hyperparathyroïdie et hypoparathyroïdie",q:"hyperparathyroïdie",
d:"Hyperparathyroïdie primitive : hypercalcémie par adénome parathyroïdien unique (85 %), hyperplasie des quatre glandes ou carcinome ; secondaire : carence en vitamine D et insuffisance rénale chronique ; hypoparathyroïdie : post-chirurgicale (première cause), auto-immune ou congénitale (syndrome de DiGeorge).",
s:"Hyperparathyroïdie : « pierres, os, douleurs abdominales, confusions » — lithiases rénales récidivantes, ostéoporose précoce, ulcères, asthénie, troubles psychiatriques ; hypoparathyroïdie : tétanie, paresthésies péribuccales, crampes, cataracte, dystrophie dentaire, QT long.",
dx:"Hyperparathyroïdie : calcémie élevée avec PTH inadaptée (normale ou élevée malgré l'hypercalcémie), phosphorémie basse, calciurie ; localisation préopératoire (échographie, scintigraphie MIBI) ; ostéodensitométrie ; hypoparathyroïdie : calcémie basse + PTH indosable + phosphorémie élevée, magnésémie.",
t:"Hyperparathyroïdie symptomatique ou répondant aux critères : parathyroïdectomie (curative dans plus de 95 %) ; forme modérée : surveillance ou chirurgie selon les recommandations ; insuffisance rénale : chélateurs sans calcium, vitamine D active ; hypoparathyroïdie : calcium oral et calcitriol à vie (la PTH absente ne permet pas d'activer la vitamine D).",
k:"Hypercalcémie + PTH non freinée = hyperparathyroïdie primitive : l'adénome se guérit par la chirurgie."}
]},
{name:"Surrénales & Hypophyse",paths:[
{n:"Insuffisance surrénalienne chronique (Maladie d'Addison) et aiguë (crise addisonienne)",q:"maladie d'Addison",ur:true,
d:"Insuffisance surrénale : primaire ou maladie d'Addison (destruction des surrénales : auto-immune dans les pays occidentaux, tuberculose ailleurs) avec déficit en cortisol et en aldostérone ; secondaire (hypopituitarisme, corticothérapie prolongée arrêtée brutalement) isolée en cortisol ; la crise addisonienne est l'urgence aiguë.",
s:"Asthénie intense, amaigrissement, hypotension orthostatique, mélanodermie (teint cuivré, plis) dans la forme primaire, vomissements, douleurs abdominales, hypoglycémies, hyponatrémie avec hyperkaliémie (primaire), perte du goût du sel ; crise : collapsus, fièvre, confusion, hypoglycémie, déshydratation.",
dx:"Cortisol à 8 h bas (ou insuffisant) avec ACTH élevée (primaire) ou basse (secondaire) ; test de stimulation au Synacthène (pas d'élévation du cortisol) ; ionogramme (hyponatrémie, hyperkaliémie), glycémie ; anticorps anti-21-hydroxylase, scanner surrénalien, recherche des autres auto-immunités ; en urgence : traiter sans attendre les résultats.",
t:"Crise addisonienne : hydrocortisone IV immédiate + remplissage salé + glucose, traitement du facteur déclenchant ; entretien : hydrocortisone orale en 2-3 prises et fludrocortisone (forme primaire), éducation à l'adaptation des doses (doublement en cas de stress, fièvre, chirurgie), carte d'insuffisant surrénalien, alimentation salée ; jamais d'arrêt brutal d'une corticothérapie prolongée.",
k:"Hypotension + mélanodermie + hyponatrémie avec hyperkaliémie = Addison ; en urgence : hydrocortisone IV sans attendre le dosage."}
,
{n:"Syndrome de Cushing (hypercorticisme)",q:"syndrome de Cushing",
d:"Hypercortisolisme chronique : maladie de Cushing (adénome hypophysaire corticotrope, 70 % des formes endogènes), adénome ou carcinome surrénalien, sécrétion ectopique d'ACTH (cancers bronchiques) ; l'hypercortisolisme iatrogène par corticoïdes est de loin la cause la plus fréquente.",
s:"Obésité facio-tronculaire, faciès lunaire, bosse de bison, vergetures pourpres larges, fragilité cutanée avec hématomes, amyotrophie proximale, HTA, diabète, ostéoporose, troubles psychiatriques, aménorrhée et hirsutisme dans les formes surrénaliennes ; hyperpigmentation si sécrétion élevée d'ACTH.",
dx:"Trois tests de dépistage : cortisol libre urinaire des 24 h, cortisol salivaire nocturne, freinage minute à la dexaméthasone ; ACTH plasmatique (élevée = origine hypophysaire ou ectopique, basse = surrénale) ; localisation : IRM hypophysaire, scanner surrénalien, cathétérisme des sinus pétreux si discordance ; bilan des autres axes hypophysaires.",
t:"Chirurgie de la lésion responsable (adénome hypophysaire par voie transsphénoïdale, surrénalome) ; anticortisoliques (kétoconazole, métyrapone) en attente du traitement, en cas d'échec ou de sécrétion ectopique ; substituer le cortisol en post-opératoire jusqu'à la récupération de l'axe ; radiothérapie hypophysaire dans certains cas ; suivi endocrinien à vie.",
k:"HTA + obésité facio-tronculaire + vergetures pourpres + fragilité cutanée = Cushing ; penser d'abord à une cause iatrogène (corticoïdes)."}
,
{n:"Phéochromocytome",q:"phéochromocytome",
d:"Tumeur chromaffine de la médullosurrénale (ou paragangliome extra-surrénalien) sécrétant des catécholamines : cause rare d'HTA (moins de 1 %), parfois familiale (NEM 2, von Hippel-Lindau, NF1, paragangliomes héréditaires — près de 40 % des cas).",
s:"HTA permanente résistante ou paroxystique avec triade céphalées-sueurs-palpitations ; paroxysmes : pâleur, angoisse de mort, tremblement, douleurs abdominales, déclenchés par le stress, la chirurgie, certains médicaments et aliments (tyramine) ; complications : cardiomyopathie, troubles du rythme, AVC.",
dx:"Dérivés méthoxylés plasmatiques (métanéphrines) ou urinaires = examen de référence, prélevés au repos ; scanner ou IRM surrénalienne ; scintigraphie au MIBI ou TEP si paragangliome ou forme métastatique ; bilan génétique systématique ; explorer les autres glandes si syndrome de NEM 2 (calcitonine, calcium).",
t:"Préparation médicale de 10-15 jours avant tout geste : alphabloquant (phénoxybenzamine) avec expansion volémique, puis bêtabloquant (jamais seul : crise hypertensive) ; adrénalectomie cœlioscopique ; suivi à vie (récidive et malignité possibles) ; dépistage génétique familial.",
k:"HTA paroxystique + céphalées-sueurs-palpitations = dérivés méthoxylés ; jamais de bêtabloquant seul avant alphabloquant."}
,
{n:"Adénomes hypophysaires (prolactinome, acromégalie, maladie de Cushing)",q:"adénome hypophysaire",
d:"Tumeurs hypophysaires : prolactinome (le plus fréquent), adénome somatotrope (acromégalie), corticotrope (maladie de Cushing), adénomes non sécrétants (révélés par des signes compressifs) ; retentissement possible : atteinte du chiasma optique et insuffisance antéhypophysaire.",
s:"Prolactinome : galactorrhée, aménorrhée, infertilité, impuissance, baisse de la libido ; macro-adénome : céphalées, hémianopsie bitemporale, panhypopituitarisme ; acromégalie : augmentation de la pointure, épaississement des traits, prognathisme, macroglossie, sueurs, HTA, diabète, apnées du sommeil, syndrome du canal carpien.",
dx:"Hormonologie : prolactine, IGF-1 (acromégalie), axe corticotrope ; IRM hypophysaire ; champ visuel ; test de freinage au glucose oral pour l'acromégalie ; bilan complet des axes antéhypophysaires (thyroïde, surrénale, gonadique).",
t:"Prolactinome : agonistes dopaminergiques (cabergoline) en première intention, chirurgie si échec ; acromégalie : chirurgie transsphénoïdale puis analogues de la somatostatine ou antagonistes du récepteur de la GH ; maladie de Cushing : chirurgie hypophysaire ; adénome non sécrétant : surveillance ou chirurgie selon le retentissement ; substituer les déficits hypophysaires.",
k:"Aménorrhée-galactorrhée = prolactine + IRM ; hémianopsie bitemporale = compression du chiasma optique par un macro-adénome hypophysaire."}
,
{n:"Diabète insipide (central et néphrogénique)",q:"diabète insipide",
d:"Polyurie hypotonique (plus de 3 L/j d'urines diluées) : central par déficit en hormone antidiurétique (tumeur ou chirurgie hypothalamo-hypophysaire, traumatisme, histiocytose, idiopathique) ou néphrogénique par résistance rénale à l'ADH (lithium, hypercalcémie, hypokaliémie, génétique).",
s:"Polyurie abondante d'urines claires avec polydipsie intense et besoin impérieux de boire, nycturie ; déshydratation et hypernatrémie si l'accès à l'eau est limité (sujet âgé dépendant, enfant, troubles de la conscience) ; glycémie normale, contrairement au diabète sucré.",
dx:"Osmolalité urinaire basse malgré une osmolalité plasmatique élevée ; épreuve de restriction hydrique avec test à la desmopressine (réponse = central, absence de réponse = néphrogénique) ; IRM hypophysaire (central) ; bilan étiologique (lithium, calcémie, kaliémie).",
t:"Central : desmopressine à vie (orale ou nasale), éducation pour éviter l'hyponatrémie par surdosage ; néphrogénique : arrêt du médicament causal, corriger la calcémie et la kaliémie, régime pauvre en sel et protéines, diurétique thiazidique (effet antidiurétique paradoxal) ; accès libre à l'eau dans tous les cas.",
k:"Polyuro-polydipsie avec urines claires et glycémie normale = diabète insipide ; l'accès libre à l'eau prévient l'hypernatrémie."}
]},
{name:"Métabolisme & Lipides",paths:[
{n:"Dyslipidémies (hypercholestérolémie, hypertriglycéridémie, mixtes)",q:"dyslipidémie",
d:"Anomalies du bilan lipidique : hypercholestérolémie pure (LDL-cholestérol élevé, dont l'hypercholestérolémie familiale — LDL très élevé, xanthomes tendineux, infarctus familiaux précoces), hypertriglycéridémie (alcool, diabète, obésité, médicaments ; risque de pancréatite aiguë au-delà de 10 g/L), formes mixtes.",
s:"Le plus souvent asymptomatiques (découverte au bilan) ; xanthomes tendineux et arc cornéen avant 45 ans (hypercholestérolémie familiale), xanthomes éruptifs (hypertriglycéridémie majeure) ; l'expression clinique est l'athérosclérose : angor, infarctus, artériopathie, AVC.",
dx:"Bilan lipidique à jeun de 12 h (cholestérol total, LDL, HDL, triglycérides) ; éliminer les causes secondaires (hypothyroïdie, diabète, syndrome néphrotique, cholestase, alcool) ; évaluation du risque cardiovasculaire global (SCORE2) ; lipoprotéine(a) dosée une fois dans la vie ; dépistage familial en cascade si hypercholestérolémie familiale.",
t:"Mesures hygiéno-diététiques (alimentation de type méditerranéen, activité physique, arrêt du tabac et de l'alcool) ; statine adaptée au risque cardiovasculaire avec objectifs de LDL-c selon le risque ; hypertriglycéridémie : contrôle du diabète et de l'alcool, oméga-3, fibrates si risque de pancréatite ; hypercholestérolémie familiale : ézétimibe, acide bempédoïque, anticorps anti-PCSK9.",
k:"Le LDL-c guide l'intensité de la statine selon le risque cardiovasculaire ; xanthomes + infarctus familiaux avant 50 ans = hypercholestérolémie familiale (dépistage familial en cascade)."}
,
{n:"Goutte et hyperuricémie asymptomatique",q:"goutte",
d:"Arthropathie microcristalline due au dépôt d'urate monosodique sur hyperuricémie chronique (diminution de l'élimination rénale dans 90 % des cas, surproduction dans le reste) ; facteurs : alcool, viandes et abats, fructose, diurétiques, insuffisance rénale, hémopathies ; l'hyperuricémie asymptomatique ne se traite pas.",
s:"Crise aiguë : monoarthrite brutale de la première métatarsophalangienne (podagre) : gros orteil rouge, chaud, luisant, douloureux au moindre contact (même le drap), réveil nocturne typique ; tophus (oreilles, articulations) et arthropathie chronique destructrice ; complications : lithiase urique, néphropathie uratique.",
dx:"Clinique typique (podagre) suffisante pour traiter ; ponction articulaire : microcristaux d'urate en fuseau, à extrémités effilées, en lumière polarisée négative ; uricémie (souvent normale pendant la crise !) ; uricurie, fonction rénale, bilan métabolique associé.",
t:"Crise : colchicine à faible dose ou AINS (si fonction rénale correcte et absence de contre-indication), corticoïdes ou inhibiteur d'IL-1 si contre-indication ; ne jamais débuter ni arrêter l'hypo-uricémiant en pleine crise ; traitement de fond (après plusieurs crises) : allopurinol à dose progressive (ou fébuxostat), objectif d'uricémie < 60 mg/L, couverture par colchicine 6 mois ; régime et arrêt de l'alcool.",
k:"L'uricémie peut être normale pendant la crise de goutte ; l'allopurinol se débute à distance de la crise, à faible dose croissante, avec colchicine de couverture."}
,
{n:"Obésité et syndrome métabolique",q:"obésité",
d:"Obésité : excès de masse grasse (IMC ≥ 30 kg/m², morbide ≥ 40), maladie chronique multifactorielle (génétique, environnementale, iatrogène, endocrinienne rare) ; syndrome métabolique : périmètre abdominal élevé associé à au moins deux critères (triglycérides élevés, HDL bas, HTA, hyperglycémie).",
s:"Asthénie, dyspnée d'effort, ronflements et apnées, lombalgies, gonarthrose, reflux, retentissement psychosocial ; complications : diabète de type 2, HTA, dyslipidémie, stéatohépatite, syndrome d'apnées du sommeil, pathologies thrombo-emboliques, cancers, infertilité (SOPK).",
dx:"IMC et périmètre abdominal ; bilan : glycémie et HbA1c, bilan lipidique, transaminases, TA ; dépistage des complications (polygraphie du sommeil, FibroScan) ; éliminer les causes rares (hypothyroïdie, hypercortisolisme, syndromes génétiques).",
t:"Prise en charge chronique : rééducation diététique et activité physique adaptée, thérapie comportementale ; traitements médicamenteux (agonistes GLP-1, orlistat) selon indications ; chirurgie bariatrique si IMC ≥ 40 (ou ≥ 35 avec comorbidités) après évaluation pluridisciplinaire et engagement de suivi à vie ; traitement systématique des comorbidités.",
k:"L'obésité est une maladie chronique : la perte de poids même modérée (5-10 %) améliore le diabète, l'HTA et la stéatose."}
]}
]},

{id:"hemato",num:6,name:"Hématologie Clinique",groups:[
{name:"Anémies de l'Adulte",paths:[
{n:"Anémie ferriprive (carence en fer)",q:"anémie ferriprive",
d:"Anémie microcytaire hypochrome par carence martiale : saignements chroniques (gynécologiques, digestifs — première cause à rechercher chez l'homme et la femme ménopausée), carence d'apport, malabsorption, grossesse, helminthiases dans les zones d'endémie.",
s:"Pâleur, asthénie, dyspnée d'effort, palpitations, chute des cheveux, ongles cassants (koïlonychie), perlèche, glossite ; syndrome des jambes sans repos ; chez l'enfant, troubles de l'attention et des apprentissages.",
dx:"NFS : hémoglobine basse, VGM < 80 fL ; ferritinémie abaissée (moins de 15-30 µg/L) avec coefficient de saturation de la transferrine bas (contrairement aux inflammatoires) ; recherche de la source de saignement : interrogatoire et examen, endoscopies digestives (FOGD et coloscopie) si carence inexpliquée, surtout après 50 ans.",
t:"Fer oral pendant 3 mois au-delà de la normalisation de l'hémoglobine (recharge des réserves) ; traiter la cause du saignement ; vitamine C pour l'absorption ; transfusion réservée aux anémies mal tolérées.",
k:"Toute carence martiale de l'adulte ou de la femme ménopausée = chercher un saignement digestif (FOGD-coloscopie) : le fer seul ne suffit pas."}
,
{n:"Anémies mégaloblastiques (vitamine B12 et folates)",q:"anémie mégaloblastique",
d:"Anémie macrocytaire arégénérative par carence en vitamine B12 (maladie de Biermer : gastrite auto-immune à l'origine d'un déficit en facteur intrinsèque ; gastrectomie, malabsorption iléale, végétalisme) ou en acide folique (alcoolisme, grossesse, carence d'apport, médicaments antifoliques).",
s:"Asthénie, pâleur avec subictère, glossite de Hunter (langue rouge, lisse, douloureuse), anorexie, diarrhée ; carence en B12 : paresthésies des extrémités, ataxie, déficits sensitivo-moteurs (sclérose combinée de la moelle), troubles cognitifs et thymiques.",
dx:"NFS : macrocytose (VGM > 100 fL) avec réticulocytes bas ; vitaminémies B12 et folates ; anticorps anti-facteur intrinsèque et anti-cellules pariétales gastriques (Biermer) ; FOGD avec biopsies fundiques (gastrite atrophique) ; LDH élevées (érythropoïèse inefficace).",
t:"Vitamine B12 : recharge par voie IM puis entretien à vie dans le Biermer ; acide folique oral ; jamais de folates seuls en cas de carence mixte (ils corrigent l'anémie mais aggravent les signes neurologiques de la carence en B12) ; surveillance neurologique.",
k:"Anémie macrocytaire + glossite + paresthésies = carence en B12 ; folates seuls interdits si carence mixte : risque d'aggravation neurologique."}
,
{n:"Anémies inflammatoires et chroniques",q:"anémie des maladies chroniques",
d:"Anémie des maladies chroniques (infections prolongées, cancers, maladies inflammatoires) : séquestration du fer dans le macrophages par l'hepcidine (ferritine normale ou haute), hémolyse discrète et production insuffisante d'EPO ; normocytaire ou légèrement microcytaire.",
s:"Signes de l'anémie (asthénie, pâleur, dyspnée) sur un terrain de maladie chronique connue ; fièvre, amaigrissement, syndrome inflammatoire biologique ; l'hémoglobine descend rarement au-dessous de 9 g/dL.",
dx:"NFS ; ferritinémie normale ou élevée avec saturation de la transferrine basse (discrimination avec la carence martiale : ferritine basse) ; CRP élevée ; recherche de la cause (néoplasie, infection, inflammation) ; éliminer une insuffisance rénale associée.",
t:"Traitement de la maladie causale ; le fer oral est inefficace (carence de séquestration) ; agents stimulant l'érythropoïèse dans l'insuffisance rénale chronique ou sous chimiothérapie (objectif Hb autour de 10-12 g/dL) ; transfusion si mauvaise tolérance.",
k:"Anémie avec ferritine normale ou élevée et CRP haute = anémie inflammatoire : chercher la cause, pas une carence."}
,
{n:"Anémies hémolytiques (auto-immunes - AHAI, corpusculaires)",q:"anémie hémolytique",
d:"Destruction prématurée des globules rouges (durée de vie < 120 jours) : corpusculaires (sphérocytose héréditaire de Minkowski-Chauffard, drépanocytose, thalassémies, déficit en G6PD) ou extracorpusculaires (auto-immunes — AHAI à anticorps chauds ou froids —, mécaniques : valves cardiaques, microangiopathie, médicaments, infectieuses : paludisme).",
s:"Pâleur ictérique, urines foncées, splénomégalie, asthénie, dyspnée ; crises aiguës : fièvre, douleurs abdominales ou lombaires, chute de l'hémoglobine ; AHAI à anticorps froids : acrosyndrome déclenché par le froid ; déficit en G6PD : hémolyse brutale après médicaments (sulfamidés, antipaludéens) ou ingestion de fèves.",
dx:"Anémie régénérative (réticulocytes élevés) + LDH élevées + haptoglobine effondrée + bilirubine libre augmentée ; test de Coombs direct (positif = AHAI) ; frottis : schizocytes (mécanique), sphérocytes (Minkowski) ; dosage de G6PD à distance de la crise, électrophorèse de l'hémoglobine.",
t:"Traitement de la cause ; AHAI à anticorps chauds : corticoïdes en première intention, puis rituximab, immunosuppresseurs ou splénectomie en cas de rechute ; anticorps froids : éviter le froid, traiter la cause sous-jacente (mycoplasme, EBV, hémopathie) ; supplémentation en folates ; transfusion avec prudence en urgence.",
k:"Anémie + réticulocytes élevés + haptoglobine basse = hémolyse ; Coombs positif = auto-immune, négatif = corpusculaire ou mécanique (voir le frottis)."}
,
{n:"Drépanocytose (syndromes falciformes de l'adulte, crises vaso-occlusives)",q:"drépanocytose",ur:true,
d:"Hémoglobinopathie héréditaire (hémoglobine S homozygote SS ou double hétérozygote SC/S-bêta-thalassémie) : falciformation des globules rouges à la désaturation, responsible d'une hémolyse chronique et d'occlusions microvasculaires (crises vaso-occlusives) ; très fréquente en Afrique subsaharienne.",
s:"Anémie hémolytique chronique régénérative avec ictère ; crises vaso-occlusives : douleurs osseuses brutales du dos et des membres, fièvre ; complications : syndrome thoracique aigu (dyspnée, douleur, hypoxémie), AVC ischémique, rétinopathie, ostéonécrose de la tête fémorale, ulcères de jambe, priapisme, lithiase biliaire, infections à pneumocoque (asplénie fonctionnelle).",
dx:"NFS (Hb habituellement 6-9 g/dL, réticulocytes élevés), frottis avec drépanocytes ; électrophorèse de l'hémoglobine (diagnostic et génotype) ; en crise : radio/scanner thoracique, gaz du sang, hémocultures ; suivi : échographie transcrânienne (enfant), fond d'œil, statut vaccinal.",
t:"Crise vaso-occlusive : hydratation, antalgiques par paliers (morphine si besoin), oxygène, réchauffement ; chercher un facteur déclenchant (infection, déshydratation) ; fond : hydroxyurée (réduit les crises), transfusions programmées ou échanges transfusionnels (prévention secondaire de l'AVC), vaccination antipneumococcique et pénicilline prophylactique ; greffe de moelle ou thérapies géniques (formes sévères) ; éducation et carte de drépanocytaire.",
k:"Douleur osseuse fébrile chez un drépanocytaire = crise vaso-occlusive à soulager rapidement (antalgiques IV) tout en dépistant le syndrome thoracique aigu."}
]},
{name:"Hémopathies Malignes & Syndromes Myélo/Lymphoprolifératifs",paths:[
{n:"Leucémie Myéloïde Chronique (LMC) et Leucémies Aiguës (LAL / LAM)",q:"leucémie aiguë",ur:true,
d:"LMC : néoplasie myéloproliférative avec translocation BCR-ABL (chromosome Philadelphie), leucocytose élevée et splénomégalie ; leucémies aiguës : prolifération de blastes médullaires — lymphoblastique (LAL) ou myéloblastique (LAM) — évinçant les lignées normales.",
s:"LMC : découverte fortuite d'une hyperleucocytose, asthénie, splénomégalie, parfois signes d'hypermétabolisme ; leucémies aiguës : syndrome anémique, infections récidivantes (neutropénie) et hémorragique (thrombopénie) d'installation rapide : asthénie, purpura, fièvre, gingivorragies ; LAM : hypertrophie gingivale, chlorome ; LAM3 : coagulation intravasculaire disséminée.",
dx:"NFS avec frottis (blastes) ; myélogramme : blastes ≥ 20 % (leucémie aiguë), avec immunophénotypage et cytogénétique (Philadelphie dans la LMC, t(15;17) dans la LAM3) ; LDH, urée, ionogramme, uricémie (syndrome de lyse) ; bilan d'hémostase.",
t:"LMC : inhibiteurs de la tyrosine kinase (imatinib et générations suivantes) à vie — survie proche de la population générale ; LAL : chimiothérapie selon protocoles, éventuellement allogreffe ; LAM3 : acide tout-trans-rétinoïque (ATRA) + chimiothérapie, en urgence (CIVD) ; autres LAM : chimiothérapie intensive ± allogreffe ; soins de support et prévention du syndrome de lyse.",
k:"Blastes au frottis ou au myélogramme ≥ 20 % = leucémie aiguë : transfert immédiat en hématologie ; la LAM3 (promyélocytaire) se complique de CIVD dès l'annonce."}
,
{n:"Leucémie Lymphoïde Chronique (LLC)",q:"leucémie lymphoïde chronique",
d:"Prolifération de lymphocytes B matures, la plus fréquente des leucémies de l'adulte occidental (âge médian 70 ans) ; évolution lente sur des années, classification de Binet (A, B, C) selon l'extension et l'insuffisance médullaire.",
s:"Découverte fortuite d'une hyperlymphocytose (stade A) ; adénopathies superficielles bilatérales, splénomégalie ; stades avancés : asthénie, sueurs nocturnes, amaigrissement, infections récidivantes (hypogammaglobulinémie), anémie et infections ; manifestations auto-immunes (anémie hémolytique, PTI).",
dx:"NFS : hyperlymphocytose persistante (> 5 G/L) ; frottis : lymphocytes matures et ombres de Gümprecht ; immunophénotypage sanguin (diagnostic) ; électrophorèse des protides ; TDM si évolution ; pas de myélogramme systématique.",
t:"Binet A : abstention-surveillance (le traitement ne modifie pas le pronostic) ; stades actifs (anémie, thrombopénie, symptômes) : immunochimiothérapie ou inhibiteurs (ibrutinib, vénétoclax) ; prophylaxie des infections (vaccinations, immunoglobulines si infections récidivantes) ; suivi hématologique.",
k:"Hyperlymphocytose du sujet âgé avec ombres de Gümprecht = LLC : le stade A de Binet se surveille, il ne se traite pas."}
,
{n:"Myélome Multiple (Maladie de Kahler)",q:"myélome multiple",
d:"Prolifération plasmocytaire clonale médullaire sécrétant une immunoglobuline monoclonale ; les manifestations cardinales (CRAB) : hyperCalcémie, atteinte Rénale, Anémie, lésions osseuses (Bone disease) ; maladie du sujet âgé (médiane 70 ans).",
s:"Douleurs osseuses (rachis, côtes) avec fractures et tassements spontanés, asthénie (anémie), soif, polyurie et confusion (hypercalcémie), infections récidivantes (immunoparalysie), insuffisance rénale ; rarement hyperviscosité (IgA).",
dx:"Électrophorèse et immunofixation des protides sériques et urinaires (pic monoclonal) ; plasmocytose médullaire ; bilan CRAB : NFS, créatinine, calcémie, radiographies du squelette ou IRM/TEP ; chaînes légères libres ; β2-microglobuline et albuminémie (score ISS).",
t:"Traitement systémique (protéasome-inhibiteur + immunomodulateur + anti-CD38) suivi d'autogreffe de cellules souches chez les patients fit ; bisphosphonates pour prévenir les événements osseux (avec soins dentaires préalables) ; hypercalcémie : hydratation + biphosphonates ; antibiothérapie et prévention des infections ; radiothérapie antalgique sur lésion menaçante.",
k:"Douleurs osseuses + anémie + insuffisance rénale + hypercalcémie chez un sujet âgé = myélome : électrophorèse avec immunofixation."}
,
{n:"Lymphomes Malins Non Hodgkiniens (LMNH) et Maladie de Hodgkin",q:"lymphome",
d:"Proliférations lymphoïdes malignes : maladie de Hodgkin (cellules de Sternberg, bimodale — jeune adulte et sujet âgé —, adénopathies souvent sus-diaphragmatiques, forte curabilité) ; lymphomes non hodgkiniens : agressifs (diffus à grandes cellules B, Burkitt) ou indolents (folliculaire, MALT, zone marginale).",
s:"Adénopathies superficielles fermes, indolores, persistantes (cervicales, sus-claviculaires) ; symptômes B : fièvre, sueurs nocturnes, amaigrissement supérieur à 10 % ; asthénie, prurit (Hodgkin) ; compressions : syndrome cave, dyspnée médiastinale, compression médullaire ; splénomégalie.",
dx:"Biopsie ganglionnaire (adénectomie) avec histologie — indispensable ; TEP-TDM et scanner thoraco-abdomino-pelvien ; biopsie ostéomédullaire ; NFS, LDH (facteur pronostique), sérologies VIH et VHC ; classification d'Ann Arbor pour le staging.",
t:"Hodgkin : chimiothérapie (ABVD) ± radiothérapie, guérison dans plus de 80 % des cas ; LMNH agressifs : immunochimiothérapie (R-CHOP) ± radiothérapie, autogreffe en rechute ; LMNH indolents : surveillance ou rituximab ± chimiothérapie ; prévention du syndrome de lyse (Burkitt) ; suivi à long terme (secondes tumeurs, cardiaque).",
k:"Adénopathie ferme indolore depuis plus de 3 semaines = adénectomie ; jamais de corticoïdes avant la biopsie : ils font fondre le lymphome."}
,
{n:"Polyglobulie de Vaquez et Thrombocythémie essentielle",q:"polyglobulie de Vaquez",
d:"Néoplasies myéloprolifératives Philadelphie-négatives : polyglobulie de Vaquez (prolifération érythrocytaire, mutation JAK2 V617F quasi constante) et thrombocythémie essentielle (prolifération plaquettaire, JAK2, CALR ou MPL) ; risque thrombotique et hémorragique, évolution possible vers myélofibrose ou leucémie.",
s:"Vaquez : céphalées, vertiges, visage rouge violacé, prurit à l'eau chaude, acroparesthésies, érythermalgie (brûlures des pieds), HTA, thromboses ; thrombocythémie : thromboses artérielles et veineuses, érythermalgie, hémorragies ; splénomégalie dans les deux.",
dx:"Vaquez : hémoglobine et hématocrite élevés, érythropoïétine basse, JAK2+ (après avoir éliminé une polyglobulie secondaire : hypoxie, tabagisme, EPO) ; thrombocythémie : plaquettes > 450 G/L persistantes, plaquettes géantes au frottis, mutation JAK2/CALR/MPL, fer normal.",
t:"Vaquez : saignées (hématocrite < 45 %) ± hydroxyurée ou interféron selon le risque thrombotique ; thrombocythémie : aspirine à faible dose en cas de symptômes vasculaires, cytoreduction (hydroxyurée, anagrélide) si risque élevé ; contrôle des facteurs de risque cardiovasculaire ; surveillance de la transformation.",
k:"Érythermalgie (pieds rouges et brûlants) + thromboses = néoplasie myéloproliférative : JAK2."}
]},
{name:"Hémostase & Troubles de la Coagulation",paths:[
{n:"Purpura Thrombopénique Immuno-allergique / Idiopathique (PTI)",q:"purpura thrombopénique immunologique",
d:"Thrombopénie périphérique par auto-anticorps anti-plaquettes, sans autre cause (diagnostic d'élimination) ; aigu et spontanément résolutif chez l'enfant, chronique et volontiers récidivant chez l'adulte.",
s:"Purpura pétéchial et ecchymotique disséminé (membres et muqueuses), épistaxis, gingivorragies, ménorragies ; pas de saignement profond (pas d'hémarthrose, contrairement à l'hémophilie) ; pas de splénomégalie ni d'adénopathie, état général conservé.",
dx:"NFS : thrombopénie isolée (parfois < 10 G/L), frottis normal (pas de schizocytes), hémoglobine et leucocytes normaux ; myélogramme réservé aux formes atypiques ; éliminer : VIH, VHC, H. pylori, lupus, médicaments, grossesse, microangiopathie ; score hémorragique pour la décision.",
t:"Enfant aigu : surveillance seule dans la majorité des cas (récupération en semaines) ; adulte avec saignement ou plaquettes < 20-30 G/L : corticoïdes, immunoglobulines IV en urgence hémorragique ; formes chroniques : agonistes du récepteur de la TPO, rituximab, splénectomie ; éviter les antiagrégants et les injections intramusculaires.",
k:"Thrombopénie isolée avec purpura, frottis normal et NFS par ailleurs normale = PTI (diagnostic d'élimination) ; plaquettes < 20 G/L ou saignement actif = traitement urgent."}
,
{n:"Coagulation Intra-Vasculaire Disséminée (CIVD)",q:"coagulation intravasculaire disséminée",ur:true,
d:"Activation diffuse de la coagulation (libération de facteur tissulaire) : consommation paradoxale des plaquettes et des facteurs de coagulation aboutissant à la fois à des thromboses microvasculaires et à un syndrome hémorragique ; causes : sepsis (méningocoque, bacilles Gram négatif), cancers (prostatique, leucémie promyélocytaire), complications obstétricales (HRP, embolie amniotique), traumatismes, brûlures.",
s:"Hémorragies diffuses : saignement des points de ponction et des muqueuses, ecchymoses étendues, épistaxis, hématurie ; parallèlement thromboses et défaillances d'organe (rein, cerveau, extrémités), choc ; contexte aigu grave chez un patient hospitalisé.",
dx:"Thrombopénie + TP abaissé + TCA allongé + fibrinogène abaissé + D-dimères élevés (marqueurs de consommation) ; schizocytes possibles ; biologie répétée (cinétique) ; purpura fulminans de l'enfant (méningocoque).",
t:"Traitement de la cause (antibiothérapie du sepsis, vidange utérine, chimiothérapie de la LAM3) — la clé du pronostic ; compensation : plasma frais congelé, concentrés plaquettaires, fibrinogène ; soins de support en réanimation ; héparine réservée aux formes thrombotiques prédominantes.",
k:"Thrombopénie + TP bas + fibrinogène bas + D-dimères élevés = CIVD : traiter la cause et compenser."}
,
{n:"Hémophilie A et B / Maladie de Willebrand",q:"hémophilie",
d:"Hémophilies : déficits héréditaires liés à l'X en facteur VIII (A, 80 %) ou IX (B), responsables d'hémorragies profondes ; maladie de Willebrand : déficit quantitatif ou qualitatif du facteur de Willebrand, autosomique dominant, la plus fréquente des maladies hémorragiques héréditaires, avec hémorragies superficielles.",
s:"Hémophilie : hémarthroses spontanées ou post-traumatiques (genou, coude, cheville) aboutissant à l'arthropathie, hématomes profonds (psoas), hématuries, saignements prolongés post-chirurgicaux ; Willebrand : ménorragies depuis la puberté, épistaxis, ecchymoses, saignements post-opératoires ou post-extraction dentaire.",
dx:"TCA allongé avec TP et taux de prothrombine normaux, temps de céphaline activée corrigé par le plasma témoin ; dosages : facteurs VIII et IX, antigène et activité du facteur de Willebrand ; hémogramme normal ; antécédents familiaux ( transmission liée à l'X).",
t:"Hémophilie : substituer le facteur manquant (prophylaxie régulière dans les formes sévères), émicizumab (hémophilie A), acide tranexamique ; arthropathies : kinésithérapie, prise en charge orthopédique ; Willebrand : desmopressine dans les formes légères, concentrés de facteur de Willebrand ; éviter AINS et injections intramusculaires ; carte de maladie hémorragique.",
k:"Hémarthrose récidivante chez un garçon = hémophilie (TCA allongé isolé) ; ménorragies et épistaxis familiaux = Willebrand."}
,
{n:"Syndromes hémorragiques et thrombophilies constitutionnelles ou acquises",q:"thrombophilie",
d:"Syndromes hémorragiques : par anomalie plaquettaire qualitative (aspirine, urémie), déficit rares en facteurs, anomalies de la paroi vasculaire ; thrombophilies : constitutionnelles (facteur V Leiden, mutation G20210A de la prothrombine, déficits en protéine C, S, antithrombine) ou acquises (syndrome des antiphospholipides, cancers, grossesse, œstroprogestatifs), prédisposant aux thromboses veineuses.",
s:"Hémorragique : purpura, ecchymoses spontanées, saignements muqueux, prolongation des saignements post-opératoires ; thrombophilie : thrombose veineuse profonde ou embolie pulmonaire inaugurante chez le sujet jeune, récidivante, familiale, ou de siège insolite (cérébral, mésentérique), fausses couches à répétition (antiphospholipides).",
dx:"Hémorragique : NFS-plaquettes, TCA, TP, temps de saignement ou PFA-100, dosages spécifiques ; thrombophilie : bilan à distance de l'épisode et des anticoagulants (au moins 3 mois) : recherche de facteur V Leiden et de la mutation de la prothrombine, protéines C, S, antithrombine, anticoagulant lupique et anticorps anticardiolipine (critères de Sydney pour le SAPL).",
t:"Hémorragique : arrêt des médicaments en cause, traitements locaux, acide tranexamique, substitution ; thrombophilie : anticoagulation curative de l'épisode (durée selon la cause), contre-indication des œstroprogestatifs, prophylaxie des situations à risque (chirurgie, immobilisation, grossesse) ; SAPL : anticoagulation au long cours après un événement thrombotique.",
k:"Thrombose veineuse du sujet jeune, récidivante, familiale ou insolite = bilan de thrombophilie à distance des anticoagulants."}
]}
]},

{id:"infectio",num:7,name:"Infectiologie & Médecine Tropicale",groups:[
{name:"Infections Systémiques & Tropicales",paths:[
{n:"Paludisme simple et Paludisme grave (accès pernicieux)",q:"paludisme",ur:true,
d:"Infection par des hématozoaires du genre Plasmodium (falciparum responsable des formes mortelles ; vivax, ovale, malariae, knowlesi), transmis par la piqûre de l'anophèle femelle ; incubation 7 à 30 jours ; urgence diagnostique devant toute fièvre au retour d'une zone d'endémie.",
s:"Accès simple : fièvre, céphalées, courbatures, frissons, nausées — tableau pseudo-grippal, parfois accès fébriles périodiques ; accès grave (falciparum) : troubles de la conscience ou convulsions (neuropaludisme), anémie profonde, ictère, oligo-anurie, détresse respiratoire, hypoglycémie, collapsus.",
dx:"Test de diagnostic rapide (TDR) et goutte épaisse avec frottis mince (espèce et parasitémie) — à répéter si négatifs devant une forte suspicion ; NFS et plaquettes (thrombopénie), créatinine, glycémie, ionogramme ; éliminer les autres causes de fièvre du voyageur.",
t:"Accès simple à falciparum : dérivé de l'artémisinine en association (artéméther-luméfantrine) en cure courte ; accès grave : artésunate IV en urgence, soins de support en réanimation, surveillance neurologique et glycémique ; paludisme à vivax/ovale : traitement de la forme hépatique (primaquine ou tafénoquine après dépistage G6PD) ; chimioprophylaxie du voyageur adaptée à la zone.",
k:"Toute fièvre dans les 3 mois suivant un retour d'endémie palustre = paludisme jusqu'à preuve du contraire : TDR et goutte épaisse en urgence, la même journée."}
,
{n:"Infection à VIH / SIDA et infections opportunistes",q:"VIH",
d:"Infection par le virus de l'immunodéficience humaine (VIH-1, VIH-2), transmise par voie sexuelle, sanguine et de la mère à l'enfant ; destruction progressive des lymphocytes T-CD4 aboutissant au SIDA (CD4 < 200/mm³) avec infections opportunistes et cancers.",
s:"Primo-infection : syndrome pseudo-grippal avec fièvre, éruption maculeuse, angine, polyadénopathies ; phase chronique asymptomatique (années) ; SIDA : pneumocystose (dyspnée fébrile sèche, desaturation), toxoplasmose cérébrale (abcès), cryptococcose neuroméningée, rétinite à CMV, candidose œsophagienne, tuberculose, sarcome de Kaposi, cachexie.",
dx:"Dépistage : test ELISA combiné antigène-anticorps, confirmation par immunoblot ou quatrième génération ; suivi : charge virale ARN-VIH et lymphocytes CD4 ; bilan initial : génotype de résistance, sérologies associées (hépatites, syphilis, toxoplasmose), NFS, transaminases ; dépistage des partenaires et déclaration.",
t:"Trithérapie antirétrovirale à vie (deux INTI + un troisième agent) avec l'objectif d'une charge virale indétectable (alors plus de transmission sexuelle, I = I) ; prophylaxie de la pneumocystose si CD4 < 200 (cotrimoxazole) ; prévention : préservatif, PrEP, traitement post-exposition dans les 48 h, dépistage régulier ; PTME : traitement de la femme enceinte.",
k:"Toute exposition à risque (rapport non protégé, partage de matériel, accident d'exposition au sang) = TPE à débuter idéalement dans les 4 premières heures ; I = I : indétectable = non transmetteur."}
,
{n:"Fièvre Typhoïde et paratyphoïde",q:"fièvre typhoïde",
d:"Septicémie à Salmonella Typhi ou Paratyphi (fièvres entériques), transmission fécale-orale par l'eau et les aliments contaminés ; incubation 7-14 jours ; endémique dans les régions de faible hygiène sanitaire (Asie du Sud, Afrique subsaharienne).",
s:"Fièvre croissante puis en plateau avec bradycardie relative, céphalées, obnubilation (tuphos), douleurs abdominales, constipation puis diarrhée, splénomégalie, taches rosées lenticulaires du tronc ; complications de la 3e semaine : perforation iléale (péritonite), hémorragie digestive, choc.",
dx:"Hémocultures (positives dès la première semaine) puis coprocultures ; sérodiagnostic de Widal et Felix (interprétation délicate, sérologie de confirmation) ; NFS (leuconeutropénie), CRP modérée, transaminases ; imagerie si suspicion de perforation.",
t:"Céfotaxime ou ceftriaxone IV 7-14 jours (ou fluoroquinolone selon les résistances locales) ; traitement des complications (chirurgie si perforation) ; réhydratation, antipyrétiques ; éviction des manipulateurs d'aliments jusqu'à guérison bactériologique ; hygiène, prophylaxie du voyageur (vaccin).",
k:"Fièvre progressive avec tuphos et douleurs abdominales au retour d'un voyage = fièvre typhoïde : hémocultures avant tout antibiotique."}
,
{n:"Fièvres d'Origine Indéterminée (FOI)",q:"fièvre d'origine inconnue",
d:"Fièvre supérieure à 38,3 °C évoluant depuis plus de 3 semaines sans diagnostic après une évaluation de première intention adaptée ; trois grands groupes : infections (tuberculose, endocardite, abcès profonds), néoplasies (lymphomes, cancers rénaux et coliques), maladies inflammatoires (maladie de Horton, maladie de Still, lupus) ; jusqu'à 20 % restent inexpliquées.",
s:"Fièvre prolongée avec altération de l'état général, sueurs, amaigrissement ; signes d'orientation à rechercher à l'interrogatoire et à l'examen répété : voyages, animaux, contage tuberculeux, immunodépression, valves cardiaques, traitement médicamenteux récent.",
dx:"Démarche rigoureuse et hiérarchisée : NFS, CRP, hémocultures répétées, LDH, électrophorèse des protides, sérologies ciblées, scanner thoraco-abdomino-pelvien, échocardiographie (recherche d'endocardite), TEP-TDM ; biopsies des lésions accessibles ; arrêt des médicaments suspects.",
t:"Traitement de la cause identifiée ; éviter antibiotiques et corticoïdes probabilistes qui masquent le diagnostic ; réévaluations cliniques répétées ; le pronostic des FOI authentiquement inexpliquées est bon.",
k:"Fièvre prolongée inexpliquée : refaire interrogatoire et examen clinique, répéter hémocultures ; pas d'antibiothérapie probabiliste sans foyer."}
,
{n:"Tétanos et Rage humaine",q:"tétanos",ur:true,
d:"Tétanos : toxi-infection à Clostridium tetani (spores telluriques pénétrant par une plaie souillée), dont la toxine tetanospasmine provoque contractures et spasmes ; rage : encéphalite mortelle à Lyssavirus, transmise par morsure, griffure ou léchage de mammifère (chien, chat, chauve-souris).",
s:"Tétanos : trismus et risus sardonicus, contractures paroxystiques déclenchées par stimuli (bruit, lumière), opisthotonos, spasmes laryngés (asphyxie) ; courte incubation = gravité ; rage : prodromes (douleur et prurit de la plaie), puis hydrophobie et aérophobie, agitation, hypersialorrhée, paralysie, coma et décès une fois les signes apparus.",
dx:"Tétanos : diagnostic purement clinique (plaie souillée, statut vaccinal) ; rage : le diagnostic biologique ne doit jamais retarder la prophylaxie — la conduite dépend de la catégorie d'exposition (I léchage cutané sain, II morsure sans saignement, III morsure avec saignement ou léchage de muqueuse/plaie).",
t:"Tétanos : soins intensifs, immunoglobulines antitétaniques, nettoyage et débridement de la plaie, sédation ± curarisation, ventilation ; vaccination à la sortie ; rage post-exposition : lavage immédiat de la plaie au savon pendant 15 minutes, vaccination ± immunoglobulines selon la catégorie et le statut de l'animal ; pas de traitement curatif une fois déclarée.",
k:"Trismus après plaie souillée = tétanos ; toute morsure de mammifère = lavage immédiat au savon et avis médical pour prophylaxie antirabique, sans attendre."}
,
{n:"Trypanosomiase Humaine Africaine (THA) / Maladie du sommeil",q:"trypanosomiase africaine",
d:"Maladie du sommeil : Trypanosoma brucei gambiense (Afrique de l'Ouest et centrale, réservoir humain) ou rhodesiense (Afrique de l'Est, réservoir animal), transmis par la mouche tsé-tsé (Glossina) ; phase hémolymphatique puis méningo-encéphalitique.",
s:"Phase I : chancre d'inoculation, fièvres récurrentes, adénopathies cervicales postérieures (signe de Winterbottom), splénomégalie, prurit, œdèmes faciaux ; phase II : troubles du sommeil (somnolence diurne, inversion du rythme), troubles psychiatriques et neurologiques, tremblements, cachexie, coma puis décès.",
dx:"Parasitologie directe (goutte épaisse, ponction ganglionnaire) ; sérologie CATT (dépistage gambiense) ; ponction lombaire obligatoire avant traitement : phase II si cellules du LCR > 5/mm³ ; NFS, plaquettes, fonction rénale et hépatique.",
t:"Phase I : pentamidine (gambiense) ou suramine (rhodesiense) ; phase II : fexinidazole ou association nifurtimox-eflornithine (gambiense), melarsoprol pour le rhodesiense ; hospitalisation spécialisée, surveillance du LCR après traitement ; lutte antivectorielle et dépistage des porteurs.",
k:"Adénopathies cervicales postérieures + troubles du sommeil au retour d'Afrique = trypanosomiase : le stade (LCR) conditionne le traitement, jamais la clinique seule."}
,
{n:"Choléra et fièvres éruptives graves (Rougeole compliquée)",q:"choléra",ur:true,
d:"Choléra : diarrhée aqueuse profuse « eau de riz » due à Vibrio cholerae (toxine cholérique), transmission hydrique et alimentaire, épidémies explosives ; rougeole : infection virale éruptive ultra-contagieuse (paramyxovirus), potentiellement grave chez l'enfant dénutri, la femme enceinte et l'immunodéprimé.",
s:"Choléra : diarrhée indolore brutale et massive avec vomissements, déshydratation fulgurante (yeux cernés, pli cutané, voix éteinte, collapsus), crampes, acidose ; rougeole : fièvre élevée, catarrhe oculo-respiratoire, signe de Koplik, éruption maculo-papuleuse descendante ; complications : pneumonie, laryngite, diarrhée, kératite et cécité, encéphalite.",
dx:"Choléra : test rapide sur selles, coproculture (milieu TCBS) ; ionogramme, créatinine (insuffisance rénale fonctionnelle) ; rougeole : clinique (Koplik), sérologie ou PCR sur salive ; recherche des complications (radiographie thoracique, saturation).",
t:"Choléra : réhydratation immédiate et massive par soluté de réhydratation orale (SRO), IV (Ringer lactate) si choc ; zinc 10-14 jours ; antibiothérapie (doxycycline) qui raccourcit la durée d'excrétion ; rougeole : vitamine A (réduit la mortalité), traitement des complications, oxygène ; isolement respiratoire ; vaccination (rougeole) ; eau potable et hygiène (choléra).",
k:"Choléra = réhydratation massive immédiate (SRO) : la mort survient par déshydratation en quelques heures ; rougeole = vitamine A et dépistage des complications."}
]},
{name:"Neuroméningées & Ostéo-articulaires",paths:[
{n:"Méningites bactériennes aiguës, virales et tuberculeuses",q:"méningite bactérienne",ur:true,
d:"Inflammation des méninges : bactérienne purulente (pneumocoque, méningocoque — purpura fulminans —, listeria chez l'immunodéprimé et le sujet âgé) = urgence absolue ; virale (entérovirus, ourlien) le plus souvent bénigne, sauf l'encéphalite herpétique ; tuberculeuse : évoluant sur des semaines, risque d'hydrocéphalie et de séquelles neurologiques.",
s:"Fièvre, céphalées intenses, vomissements en jet, raideur de nuque, photophobie, confusion, coma, crises convulsives ; purpura nécrotique extensif (méningocoque) = choc septique ; méningite tuberculeuse : installation subaiguë, fièvre vespérale, atteinte des nerfs crâniens, hydrocéphalie.",
dx:"Ponction lombaire (sauf contre-indications : signes de focalisation, coma, purpura fulminans = antibiothérapie immédiate sans PL) : liquide trouble à prédominance de PNN et hypoglycorachie (bactérienne), clair lymphocytaire (virale), lymphocytaire avec hypoglycorachie et chlorures bas (tuberculeuse) ; TDM avant PL si signes neurologiques focaux ; hémocultures, PCR (herpès, entérovirus).",
t:"Bactérienne : céphalosporine de 3e génération IV (céfotaxime ou ceftriaxone) immédiatement dès la suspicion, avant la PL si nécessaire, ± amoxicilline (listeria) et dexaméthasone ; herpétique : aciclovir IV ; tuberculeuse : antituberculeux + corticoïdes ; prophylaxie des contacts du méningocoque (rifampicine ou ciprofloxacine) ; déclaration obligatoire.",
k:"Suspicion de méningite purulente = C3G IV immédiatement, sans attendre PL ni scanner ; purpura fulminans = choc septique, antibiothérapie dans l'heure."}
,
{n:"Encéphalites infectieuses (herpétique)",q:"encéphalite herpétique",ur:true,
d:"Encéphalite : inflammation du parenchyme cérébral, le plus souvent virale ; HSV-1 en est la première cause sporadique et la plus grave (sans traitement, mortalité élevée) ; autres : VZV, entérovirus, arbovirus (West Nile, Zika), VIH ; éliminer une encéphalite auto-immune (anti-NMDA-R) et une listériose.",
s:"Fièvre + céphalées + syndrome confusionnel d'installation rapide, crises d'épilepsie, troubles du comportement et de la mémoire, troubles focaux (aphasie, hémiplégie), signes méningés modérés ; formes graves : coma, crises subintrantes, œdème cérébral.",
dx:"Ponction lombaire : méningite lymphocytaire, PCR herpétique dans le LCR (faussement négative dans les premiers jours) ; IRM cérébrale (atteinte temporale interne évocatrice) ; EEG (décharges périodiques temporales) ; sans attendre : aciclovir probabiliste devant tout tableau compatible.",
t:"Aciclovir IV en urgence devant toute suspicion, avant la confirmation (chaque heure compte pour le pronostic) ; traitement des crises (benzodiazépine puis antiépileptique) ; soins de support en réanimation ; encéphalite auto-immune : immunothérapie (corticoïdes, immunoglobulines, rituximab).",
k:"Fièvre + confusion + crises épileptiques = encéphalite herpétique jusqu'à preuve du contraire : aciclovir IV immédiatement, IRM et PCR en cours de traitement."}
,
{n:"Spondylodiscite infectieuse et arthrite septique",q:"arthrite septique",ur:true,
d:"Spondylodiscite : infection du disque intervertébral et des corps vertébraux (staphylocoque doré en tête, brucellose, tuberculose — mal de Pott) par dissémination hématogène ou contiguïté ; arthrite septique : infection de l'articulation (staphylocoque, gonocoque), destruction cartilagineuse en quelques jours.",
s:"Spondylodiscite : rachialgies inflammatoires fébriles, majorées la nuit, raideur segmentaire, parfois déficit neurologique (abcès épidural) ; arthrite : monoarthrite aiguë extrêmement douloureuse, chaude, rouge, tuméfiée (genou le plus souvent) avec fièvre et frissons ; évolution destructrice rapide.",
dx:"NFS, CRP, hémocultures ; ponction articulaire ou disco-vertébrale (bactériologie avec ensemencement sur flacons, PCR universelle) avant l'antibiothérapie ; IRM rachidienne (spondylodiscite, abcès) ; recherche de la porte d'entrée (cutanée, urinaire, dentaire) et d'une endocardite.",
t:"Antibiothérapie IV adaptée au germe, prolongée : 6 semaines (spondylodiscite) ou 3-4 semaines (arthrite) ; arthrite : drainage (ponctions-lavages itératives ou arthrotomie/lavage chirurgical) ; immobilisation, antalgiques ; abcès ou déficit neurologique : chirurgie en urgence.",
k:"Monoarthrite aiguë fébrile = arthrite septique jusqu'à preuve du contraire : ponction articulaire en urgence avant l'antibiothérapie ; rachialgie fébrile = IRM."}
,
{n:"Abcès cérébral",q:"abcès cérébral",ur:true,
d:"Collection purulente intraparenchymateuse cérébrale, par contiguïté (otite, mastoïdite, sinusite, infection dentaire), dissémination hématogène (endocardite, sepsis, cardiopathie congénitale cyanogène) ou post-traumatique/post-chirurgicale ; germes : streptocoques et anaérobies, staphylocoques, entérobactéries, souvent plurimicrobiens.",
s:"Céphalées progressives, fièvre inconstante, crises d'épilepsies, déficit focal (hémiparésie, aphasie), troubles de conscience, œdème papillaire ; évolution subaiguë sur des jours à semaines ; abcès multiples en cas de dissémination hématogène.",
dx:"IRM cérébrale avec injection (ou TDM) : lésion arrondie à rehaussement périphérique (ring), effet de masse, œdème ; hémocultures ; recherche de la porte d'entrée (ORL, dentaire, échocardiographie) ; ponction-lombaise contre-indiquée (risque d'engagement).",
t:"Antibiothérapie IV prolongée 6-8 semaines (céphalosporine de 3e génération + métronidazole, adaptée ensuite aux prélèvements) ; ponction-aspiration stéréotaxique ou chirurgie (bactériologie, décompression) ; anticonvulsivants ; corticoïdes si œdème menaçant ; traitement de la porte d'entrée.",
k:"Céphalées + crises + déficit focal = IRM avec injection ; jamais de PL devant un abcès cérébral (risque d'engagement)."}
]}
]},

{id:"rheumato",num:8,name:"Rhumatologie & Maladies Systémiques (Auto-immunes)",groups:[
{name:"Connectivites & Maladies Systémiques",paths:[
{n:"Lupus Érythémateux Disséminé (LED)",q:"lupus érythémateux disséminé",
d:"Maladie auto-immune systémique touchant préférentiellement la femme jeune (90 % des cas) : production d'auto-anticorps et dépôts immuns responsables d'atteintes cutanées, articulaires, rénales, hématologiques et neurologiques ; évolution par poussées.",
s:"Asthénie, arthralgies inflammatoires symétriques des mains non destructrices, éruption malaire en aile de papillon avec photosensibilité, alopécie diffuse, aphtose, phénomène de Raynaud, sérites (pleurésie, péricardite), néphropathie glomérulaire (protéinurie, hématurie), cytopénies, atteinte neurologique (crises convulsives, psychose).",
dx:"Anticorps antinucléaires (présents dans plus de 95 % des cas), anti-ADN natif et anti-Sm (spécifiques), consommation du complément (C3-C4 abaissés lors des poussées) ; bilan d'atteinte : protéinurie et sédiment urinaire, créatinine, NFS, ECG-échocardiographie ; antiphospholipides associés.",
t:"Hydroxychloroquine systématique au long cours (fond) avec photoprotection ; poussées : corticoïdes adaptés à la sévérité ± immunosuppresseurs (mycophénolate, azathioprine, rituximab) ; néphropathie lupique : ponction-biopsie rénale pour classifier et traiter ; prévention de l'ostéoporose cortisonique et des infections (vaccinations avant immunosuppression).",
k:"Femme jeune + arthralgies + éruption photosensible + protéinurie = lupus : anti-ADN natif avec complément bas signent la poussée."}
,
{n:"Sclérodermie systémique",q:"sclérodermie systémique",
d:"Connectivite caractérisée par une fibrose cutanée et viscérale et des anomalies microvasculaires ; forme cutanée limitée (CREST : calcinose, Raynaud, atteinte œsophagienne, sclérodactylie, télangiectasies) et diffuse (risque d'atteinte viscérale précoce).",
s:"Phénomène de Raynaud sévère et inaugural avec ulcères digitaux, sclérodactylie remontant vers les avant-bras, visage figé (masque sclérodermique, microstomie), télangiectasies, calcinoses ; atteintes viscérales : œsophagienne (reflux, dysphagie), pulmonaire (pneumopathie interstitielle, hypertension pulmonaire — pronostic), rénale (crise sclérodermique avec HTA maligne).",
dx:"Capillaroscopie péri-unguéale (mégacapillaires et raréfaction) ; anticorps : anticentromère (limitée), anti-Scl-70 et anti-ARN polymérase III (diffuse) ; bilan viscéral annuel : EFR avec DLCO, échocardiographie (HTAP), scanner thoracique, FOGD, tension artérielle et créatinine.",
t:"Traitement symptomatique : IPP à forte dose pour le reflux, vasodilatateurs (inhibiteurs calciques, sildénafil, bosentan) pour le Raynaud, l'HTAP et les ulcères ; immunosuppresseurs (cyclophosphamide, mycophénolate) pour la pneumopathie interstitielle ; crise rénale sclérodermique : inhibiteur de l'enzyme de conversion en urgence ; soins des ulcères digitaux ; suivi multidisciplinaire.",
k:"Raynaud sévère + sclérodactylie = sclérodermie : le pronostic se joue sur l'atteinte pulmonaire (PID, HTAP) ; crise rénale = IEC immédiat."}
,
{n:"Syndrome de Gougerot-Sjögren",q:"syndrome de Sjögren",
d:"Connectivite caractérisée par l'atteinte autoimmune des glandes exocrines : syndrome sec oculaire et buccal ; forme primitive ou secondaire (associée au lupus, à la polyarthrite rhumatoïde) ; risque de lymphome à long terme.",
s:"Sécheresse oculaire (kératoconjonctivite sicca : sensation de sable, sensation de brûlure), sécheresse buccale (xérostomie, dysphagie, caries rapides, candidose), fatigue chronique invalidante, arthralgies ; atteintes systémiques : toux sèche (trachéite), tubulopathie rénale, vascularite, neuropathies ; parotidomégalie persistante (suspecte de lymphome).",
dx:"Test de Schirmer et break-up time (hypolacrymie) ; anticorps anti-SSA/Ro et anti-SSB/La ; biopsie des glandes salivaires accessoires (sialadénite lymphocytaire focale) ; échographie des glandes salivaires ; bilan d'extension et surveillance biologiques (électrophorèse, immunoglobulines).",
t:"Traitements symptomatiques : substituts lacrymaux et salivaires, pilocarpine ou céviméline, hygiène bucco-dentaire rigoureuse ; atteinte systémique : corticoïdes ± immunosuppresseurs ; surveillance rapprochée de la parotidomégalie et des anomalies biologiques (risque de lymphome).",
k:"Syndrome sec + anti-SSA = Gougerot-Sjögren : toute parotidomégalie persistante ou gammapathie impose d'écarter un lymphome."}
,
{n:"Polymyosite et Dermatomyosite",q:"dermatomyosite",
d:"Myopathies inflammatoires acquises : faiblesse musculaire proximale (polymyosite) avec, dans la dermatomyosite, éruption caractéristique (érythème heliotrope des paupières, papules de Gottron) ; après 40-50 ans, la dermatomyosite peut révéler un cancer (syndrome paranéoplasique).",
s:"Déficit moteur proximal symétrique progressif (peigner ses cheveux, se lever d'une chaise, monter les escaliers), myalgies, élévation des CPK ; dermatomyosite : érythème heliotrope, papules de Gottron sur les faces d'extension des doigts, signe du décolleté et du châle ; arthralgies, dysphagie, pneumopathie interstitielle.",
dx:"CPK et aldolases élevées, EMG myogène ; IRM musculaire et biopsie musculaire (inflammation, nécrose) ; anticorps (anti-Jo-1 avec pneumopathie, anti-Mi-2, anti-TIF1-gamma) ; scanner thoraco-abdomino-pelvien à la recherche d'un cancer ; EFR.",
t:"Corticoïdes à forte dose avec décroissance lente ± méthotrexate ou azathioprine en épargne ; immunoglobulines IV (dermatomyosite) ; dépistage et traitement du cancer associé ; rééducation douce ; prévention de l'ostéoporose et des infections.",
k:"Déficit moteur proximal + CPK élevées = myopathie inflammatoire ; dermatomyosite de l'adulte après 50 ans = scanner à la recherche d'un cancer."}
,
{n:"Maladie de Horton (Artérite à cellules géantes) et Pseudopolyarthrite rhizomélique (PPR)",q:"artérite à cellules géantes",ur:true,
d:"Vasculartie des grosses artères (temporal, carotides externes, aorte) de la personne de plus de 50 ans ; la pseudopolyarthrite rhizomélique en est la forme associée ou révélatrice (douleurs inflammatoires des ceintures scapulaire et pelvienne).",
s:"Céphalées temporales unilatérales et inédites, hypersensibilité du cuir chevelu, claudication de la mâchoire, artère temporale indurée et non battante ; troubles visuels transitoires ou cécite brutale (neuropathie optique ischémique antérieure aiguë) = urgence absolue ; fièvre, amaigrissement, syndrome inflammatoire majeur ; PPR : douleurs et raideur des épaules et des racines, enraidissement matinal prolongé.",
dx:"VS et CRP très élevées après 50 ans ; écho-doppler des artères temporelles (halo hypoéchogène) ; biopsie de l'artère temporale (granulome à cellules géantes, lésions segmentaires) ; TEP-TDM pour l'atteinte aortique ; anémie inflammatoire.",
t:"Corticothérapie immédiate dès la suspicion, sans attendre la biopsie : la cécité installée est définitive ; bolus IV si signes visuels ou ischémiques ; décroissance très lente sur 1-2 ans avec suivi de la CRP ; PPR : corticoïdes à dose plus faible ; prévention de l'ostéoporose ; surveillance échographique de l'aorte (anévrisme).",
k:"Céphalée temporale inédite après 50 ans + VS élevée = Horton : corticoïdes immédiatement — la biopsie ne doit jamais retarder le traitement (menace de cécité)."}
,
{n:"Périartérite noueuse (PAN) et Granulomatose avec polyangéite (Wegener)",q:"granulomatose avec polyangéite",ur:true,
d:"Vascularites nécrosantes : périartérite noueuse (artères de moyen calibre, souvent liée à l'hépatite B) touchant reins, peau, nerfs et tube digestif ; granulomatose avec polyangéite (ex-Wegener, ANCA anti-PR3) : atteinte ORL et pulmonaire avec glomérulonéphrite extracapillaire.",
s:"PAN : fièvre prolongée, amaigrissement, neuropathie périphérique multinevritique douloureuse, nodules cutanés et livedo, hypertension, douleurs abdominales (infarctus mésentérique) ; GPA : obstruction nasale croûteuse et épistaxis récidivantes, otite séreuse, sclérite, hémoptysies (nodules pulmonaires), atteinte rénale rapidement progressive.",
dx:"ANCA (anti-PR3 pour la GPA) ; biopsie de l'organe atteint (granulomes, nécrose fibrinoïde des vaisseaux) ; NFS, créatinine et sédiment urinaire (syndrome néphritique) ; scanner thoracique et sinusien ; sérologie hépatite B ; laryngoscopie.",
t:"Formes graves : corticoïdes fortes doses + cyclophosphamide ou rituximab, puis traitement d'entretien (azathioprine, rituximab) ; PAN liée à l'hépatite B : antiviral ± échanges plasmatiques ; cotrimoxazole en prophylaxie de la pneumocystose ; surveillance de la fonction rénale et ORL.",
k:"Sinusite chronique croûteuse + hémoptysie + hématurie = granulomatose avec polyangéite (anti-PR3) ; mononévrite + nodules + douleurs abdominales = PAN."}
,
{n:"Maladie de Behçet",q:"maladie de Behçet",
d:"Maladie inflammatoire chronique des pays de la soie et du bassin méditerranéen : vascularite des vaisseaux de tout calibre associant aphtose bipolaire récidivante et atteintes cutanées, oculaires, articulaires, vasculaires et neurologiques ; aucun test spécifique (critères cliniques).",
s:"Aphtose buccale récidivante (plus de 3/an) et aphtose génitale laissant des cicatrices, uvéite antérieure avec hypopyon ou rétinite (menace visuelle), érythème noueux, pseudofolliculite, pathergie (pustule après piqûre), arthrites des grosses articulations ; thromboses veineuses et anévrismes artériels, atteinte neurologique (méningo-encéphalite).",
dx:"Critères internationaux (aphtose + signes associés) ; angiographie ou angio-TDM (anévrismes, thromboses), IRM cérébrale, examen ophtalmologique complet (avec angiographie rétinienne) ; HLA-B51 associé ; éliminer les autres causes d'aphtose (cœliaque, VIH, spondyloarthrite).",
t:"Colchicine (aphtose, érythème noueux) ; corticoïdes et immunosuppresseurs (azathioprine, cyclosporine, anti-TNF, anticorps anti-IL-17) pour l'uvéite et l'atteinte neurologique ; anticoagulation discutée au cas par cas dans les thromboses ; arrêt du tabac ; suivi ophtalmologique rapproché.",
k:"Aphtose bipolaire + uvéite + thromboses = Behçet ; la pathergie (pustule de piqûre) est un signe d'orientation."}
]},
{name:"Rhumatismes Inflammatoires Chroniques",paths:[
{n:"Polyarthrite rhumatoïde (PR)",q:"polyarthrite rhumatoïde",
d:"Polyarthrite inflammatoire chronique bilatérale et symétrique, destructrice (érosions osseuses), touchant préférentiellement les petites articulations des mains et des pieds ; facteurs rhumatoïdes et anti-CCP ; atteintes extra-articulaires et surmortalité cardiovasculaire.",
s:"Douleurs articulaires inflammatoires (réveil nocturne, dérouillage matinal supérieur à 30 minutes) des mains (métacarpophalangiennes, interphalangiennes proximales), poignets et pieds ; synovites palpables ; déformations tardives (main en coup de vent cubital, boutonnière) ; syndrome sec, nodules rhumatoïdes, atteinte pleuro-pulmonaire.",
dx:"Facteurs rhumatoïdes et anti-CCP (spécifiques) ; VS et CRP ; radiographies des mains et pieds (pincements, érosions, géodes) ; échographie articulaire (synovites) ; évaluation de l'activité (DAS28) et du retentissement fonctionnel.",
t:"Méthotrexate précoce (fenêtre d'opportunité des 3-6 premiers mois) ± corticoïdes à dose faible transitoire ; biothérapies (anti-TNF, anti-IL-6, anti-CD20, inhibiteurs de JAK) si échec du méthotrexate ; kinésithérapie, orthèses, réadaptation ; prévention du risque cardiovasculaire et de l'ostéoporose ; vaccinations avant immunosuppression.",
k:"La PR doit être traitée dans les 6 premiers mois par méthotrexate : cette fenêtre d'opportunité prévient les destructions irréversibles."}
,
{n:"Spondylarthrite ankylosante et spondyloarthrites",q:"spondylarthrite ankylosante",
d:"Rhumatisme inflammatoire du squelette axial et des enthèses du sujet jeune, associé à HLA-B27 ; appartient au groupe des spondyloarthrites (avec rhumatisme psoriasique, arthrites réactionnelles, spondyloarthrites des entéropathies) ; évolue vers l'ankylose.",
s:"Lombalgie inflammatoire du sujet jeune : réveil nocturne (seconde moitié de nuit), raideur matinale prolongée, améliorée par le mouvement et l'activité, pas par le repos ; fessalgie à bascule ; enthésites (talalgies), arthrites périphériques asymétriques des membres inférieurs, uvéite antérieure aiguë ; attitude d'ankylose tardive.",
dx:"Radiographies des sacro-iliques (sacro-iliite) ± IRM (détection précoce : œdème osseux) ; HLA-B27 ; CRP ; critères ASAS ; mesure de la mobilité rachidienne (test de Schober, occiput-mur) ; examen ophtalmologique si œil rouge douloureux.",
t:"AINS en continu + kinésithérapie quotidienne posturale (pierre angulaire) ; biothérapies (anti-TNF, anti-IL-17) si activité persistante malgré les AINS ; arrêt du tabac (aggrave fortement le pronostic) ; uvéite : collyre corticoïde et avis ophtalmologique urgent.",
k:"Lombalgie du sujet jeune, réveillant en seconde partie de nuit et calmée par l'exercice = spondyloarthrite : IRM des sacro-iliques si radiographie normale."}
,
{n:"Rhumatisme psoriasique",q:"rhumatisme psoriasique",
d:"Spondyloarthrite associée au psoriasis (présent dans 80 % des cas, parfois secondaire) : atteintes axiale et périphérique, dactylites et enthésites ; risque de destruction articulaire et de handicap fonctionnel.",
s:"Arthralgies asymétriques des membres inférieurs, dactylite (doigt ou orteil « en saucisse »), enthésites (talalgies), atteinte axiale ; psoriasis (plaques érythémato-squameuses des coudes, genoux, cuir chevelu), atteinte unguéale (onychose, décollements) ; uvéite possible.",
dx:"Radiographies (érosions avec prolifération osseuse, sacro-iliite) ; pas de marqueur biologique spécifique (CRP normale ou élevée, facteurs rhumatoïdes négatifs) ; évaluation dermatologique (PASI) ; IRM en cas de normalité des radiographies.",
t:"AINS et kinésithérapie ; méthotrexate si atteinte cutanée et périphérique ; biothérapies adaptées : anti-IL-17 ou anti-IL-12/23 (prédominance cutanée), anti-TNF (atteinte axiale) ; soins cutanés, arrêt du tabac et de l'alcool ; suivi dermatologique et rhumatologique conjoint.",
k:"Psoriasis + talalgie ou dactylite = rhumatisme psoriasique (un tiers des psoriasis environ) ; l'atteinte unguéale oriente vers l'atteinte articulaire."}
]},
{name:"Rhumatismes Dégénératifs & Métaboliques",paths:[
{n:"Arthrose (gonarthrose, coxarthrose, omarthrose)",q:"arthrose",
d:"Maladie articulaire dégénative du cartilage avec remodelage osseux sous-chondral : première cause de handicap chez l'adulte après 50 ans ; facteurs : âge, surcharge pondérale, dysplasie, traumatismes, méniscectomie.",
s:"Douleur mécanique (déclenchée par le mouvement et la station debout, calmée par le repos) avec raideur brève (moins de 30 minutes), crépitations, limitation progressive ; poussées congestives ; gonarthrose : épanchements récidivants ; arthrose digitale : nodosités d'Heberden et de Bouchard.",
dx:"Clinique ; radiographie (pincement de l'interligne, ostéophytes, condensation sous-chondrale) — corrélation radioclinique médiocre ; pas de syndrome inflammatoire biologique ; évaluation fonctionnelle (Douleur, Autonomie).",
t:"Perte de poids et activité adaptée, kinésithérapie (renforcement du quadriceps), paracétamol puis AINS courts ou applications locales ; infiltrations de corticoïdes lors des poussées ; arthroplastie totale de hanche ou de genou dans les formes invalidantes.",
k:"Douleur mécanique + raideur brève + crépitations = arthrose ; le renforcement musculaire et la perte de poids valent tous les antalgiques."}
,
{n:"Chondrocalcinose articulaire (pseudogoutte)",q:"chondrocalcinose",
d:"Dépôts de cristaux de pyrophosphate de calcium dans les cartilages et fibrocartilages : chondrocalcinose radiologique (fréquente après 60 ans, souvent asymptomatique) ; la crise de pseudogoutte est une arthrite aiguë à cristaux mimant la goutte ou une arthrite septique ; causes métaboliques associées à chercher avant 60 ans.",
s:"Crise aiguë : monoarthrite ou oligoarthrite brutale, très douloureuse, chaude et rouge (genou, poignet), souvent fébrile ; forme chronique : arthropathie dégénérative atypique avec poussées ; localisations radiologiques : ménisques du genou, ligament triangulaire du carpe, symphyse pubienne.",
dx:"Radiographie (calcifications des fibrocartilages) ; ponction articulaire : cristaux de pyrophosphate de calcium (rhombiques, biréfringence positive) ; bilan métabolique si sujet jeune : ferritinémie (hémochromatose), calcémie et PTH (hyperparathyroïdie), TSH, magnésémie.",
t:"Crise : AINS ou colchicine, corticoïdes oraux ou infiltration si contre-indication, glace et repos articulaire ; pas de traitement curatif des dépôts ; traiter la maladie associée (saignées dans l'hémochromatose) ; formes chroniques : antalgiques, kinésithérapie.",
k:"Monoarthrite aiguë fébrile du sujet âgé avec chondrocalcinose = pseudogoutte ; chez le sujet jeune = chercher une hémochromatose ou une hyperparathyroïdie."}
,
{n:"Ostéoporose et ostéomalacie",q:"ostéoporose",
d:"Ostéoporose : réduction de la densité minérale osseuse (T-score ≤ -2,5) et de la qualité architecturale, fragilisant l'os (fractures du poignet, tassements vertébraux, col du fémur) ; ostéomalacie : défaut de minéralisation de la trame ostéoïde (carence profonde en vitamine D, hypophosphatémie).",
s:"Ostéoporose : silencieuse jusqu'à la fracture de faible énergie ; tassements vertébraux : douleur dorsale brutale, perte de taille, cyphose ; ostéomalacie : douleurs osseuses diffuses (bassin, rachis, côtes), faiblesse musculaire proximale avec marche de canard, déformations.",
dx:"Ostéodensitométrie (T-score) ; radiographies du rachis (tassements) ; bilan des causes secondaires : calcium, phosphore, PTH, 25-OH-vitamine D, électrophorèse, TSH, cortisol ; ostéomalacie : 25-OH-D effondrée, PAL élevées, hypophosphorémie.",
t:"Ostéoporose : calcium et vitamine D + antirésorbeurs (bisphosphonates, dénosumab) ou tériparatide selon le risque de fracture ; arrêt du tabac et de l'alcool, prévention des chutes, activité en charge ; ostéomalacie : recharge en vitamine D (forte dose puis entretien) et calcium, correction de la cause.",
k:"Toute fracture de faible énergie (poignet, tassement, col du fémur) = ostéodensitométrie et bilan, puis traitement antifracturaire : l'objectif est d'éviter la fracture suivante."}
,
{n:"Lombalgies communes et radiculalgies (sciatique, névralgie cervico-brachiale)",q:"lombalgie",
d:"Lombalgie commune (95 % des cas, d'origine discale, articulaire ou musculaire, sans lésion grave) et radiculalgies par conflit disco-radiculaire : sciatique du adulte (L5 ou S1), névralgie cervico-brachiale ; les drapeaux rouges font craindre une lombalgie secondaire (fracture, infection, cancer, déficit).",
s:"Lombalgie mécanique aggravée par l'effort, le port de charges et l'antéflexion ; sciatique : douleur lancinante descendant dans un membre inférieur — L5 (face externe de la jambe, dos du pied, gros orteil) ou S1 (face postérieure, plante, talon) — avec parfois paresthésies et déficit ; drapeaux rouges : fièvre, amaigrissement, cancer, traumatisme, immunodépression, déficit moteur, troubles sphinctériens.",
dx:"Examen clinique : Lasègue, déficit moteur segmentaire, réflexes (rotulien L4, achilléen S1) ; imagerie (TDM ou IRM) seulement si drapeau rouge, déficit neurologique ou échec du traitement après 4 à 6 semaines ; pas d'imagerie systématique dans la lombalgie commune.",
t:"Lombalgie et sciatique communes : maintien de l'activité (le repos au lit est délétère), antalgiques par paliers, kinésithérapie, éducation posturale ; infiltration ou chirurgie si déficit moteur, syndrome de la queue de cheval (urgence chirurgicale) ou échec d'un traitement bien conduit de 6 à 8 semaines.",
k:"Rester actif malgré la douleur dans la lombalgie commune ; troubles sphinctériens ou anesthésie en selle avec sciatique = queue de cheval = chirurgie en urgence."}
]}
]},

{id:"geria",num:9,name:"Gériatrie & Pathologies Transversales de l'Interniste",groups:[
{name:"Grands Syndromes Gériatriques",paths:[
{n:"Iatrogénie médicamenteuse et polymédication chez le sujet âgé",q:"iatrogénie médicamenteuse",
d:"Effets indésirables et interactions des médicaments liés à la polymédication (au moins 5 molécules) : première cause d'hospitalisation évitable après 75 ans ; les modifications pharmacocinétiques (baisse de la clairance rénale et hépatique, hypoalbuminémie) et pharmacodynamiques (sensibilité accrue) augmentent la toxicité.",
s:"Chutes, confusion mentale, hypotension orthostatique, incontinence et rétention urinaire, constipation, syndrome extrapyramidal, hémorragies digestives, déshydratation, hypoglycémies ; déclin fonctionnel inexpliqué ; médicaments à risque : benzodiazépines, anticholinergiques, psychotropes, AINS, diurétiques, anticoagulants.",
dx:"Revue systématique de l'ordonnance avec le patient (pilulier réel, automédication, phytothérapie) ; listes de référence (critères de prescription potentiellement inappropriée STOPP-START, Beers) ; estimation du débit de filtration glomérulaire pour adapter les doses ; recherche de syndrome cognitif dépressif.",
t:"Déprescription raisonnée : arrêter les molécules sans indication actuelle, aux bénéfices inférieurs aux risques (benzodiazépines au long cours, AINS, anticholinergiques, doublons) ; adapter les posologies au DFG ; réévaluer l'ordonnance à chaque transition de soins ; intégrer l'espérance de vie et les objectifs de soins.",
k:"Toute décompensation gériatrique = revoir l'ordonnance : la polymédication est la première cause d'hospitalisation évitable du sujet âgé."}
,
{n:"Troubles de la marche et chutes à répétition (syndrome post-chute)",q:"chutes de la personne âgée",ur:true,
d:"Chutes de la personne âgée : cause multifactorielle (troubles visuels et de l'équilibre, sarcopénie, pathologies neurologiques et articulaires, iatrogénie, environnement) ; la chute à répétition est un marqueur de fragilité et annonce la perte d'autonomie ; le syndrome post-chute (peur de retomber) pérennise le déconditionnement.",
s:"Instabilité, marche ralentie à petits pas, difficulté au demi-tour, chutes répétées ; conséquences : fractures (col du fémur — l'urgence orthogératrique), hématomes sous anticoagulants, plaies, immobilisation en chaîne (escarres, infections, thromboses) ; syndrome post-chute : réduction des activités, désocialisation, dépression.",
dx:"Évaluation plurifactorielle : tests de marche (Get-up and Go, Tinetti), vision et audition, tension orthostatique, examen neurologique et articulaire, revue médicamenteuse ; recherche d'une cause spécifique (trouble du rythme, hydrocéphalie à pression normale, Parkinson iatrogène) ; évaluation osseuse (ostéodensitométrie, vitamine D).",
t:"Prévention : réadaptation de la marche et renforcement musculaire (kinésithérapie, tai-chi), correction sensorielle, adaptation du logement (éclairage, barres d'appui, tapis), adaptation médicamenteuse ; prévention de l'ostéoporose (vitamine D, antirésorbeurs) ; après fracture du col : prise en charge orthogératrique précoce (chirurgie rapide, lever précoce).",
k:"Une chute n'est jamais banale après 65 ans : évaluation multifactorielle, réadaptation et adaptation de l'ordonnance — jamais de contentement ni d'alitement."}
,
{n:"Syndrome de glissement et dépression du sujet âgé",q:"dépression de la personne âgée",
d:"Syndrome de glissement : décrochage psychocomportemental de la personne âgée après un événement de vie (deuil, hospitalisation, chute, institutionalisation) : refus alimentaire, mutisme, alitement, déclin fonctionnel rapide ; la dépression du sujet âgé est fréquente, sous-diagnostiquée, souvent atypique (complaintes somatiques, ralentissement) et de haut risque suicidaire.",
s:"Asthénie, anorexie et perte de poids, perte d'intérêt et de plaisir, repli, insomnie, plaintes somatiques multiples (douleurs, constipation), ralentissement cognitif pouvant mimer une démence (pseudodémence dépressive) ; idées délirantes de ruine ou d'indignité, passage à l'acte suicidaire parfois silencieux (refus de s'alimenter, de se soigner).",
dx:"Échelles de dépistage (mini-GDS, GDS) ; diagnostic différentiel avec la démence débutante (troubles mnésiques d'apparition rapide, évaluation après traitement antidépresseur) ; éliminer les causes organiques : hypothyroïdie, carences (B12, folates), iatrogénie, douleur, rétention, épilepsie ; évaluation du risque suicidaire.",
t:"Prise en charge globale : réhabilitation nutritionnelle et motrice précoce, stimulations, soutien social et familial ; antidépresseur (IRS en première intention, posologie initiale réduite, réévaluation à 4-6 semaines) ; psychothérapies adaptées ; prévention : maintien des repères, du lever et des activités lors de toute hospitalisation.",
k:"Personne âgée alitée, anorexique et mutique = dépister la dépression (souvent masquée) : elle peut mimer une démence — réversible sous traitement."}
,
{n:"Troubles cognitifs majeurs (Démences : Alzheimer, vasculaire, corps de Lewy)",q:"démence",
d:"Déclin cognitif acquis assez sévère pour interférer avec l'autonomie : maladie d'Alzheimer (60-70 %, atteinte progressive de la mémoire épisodique), démence vasculaire (facteurs de risque vasculaires, installation en escalier), démence à corps de Lewy (fluctuations, hallucinations visuelles, parkinsonisme, hypersensibilité aux neuroleptiques), dégénérescence lobaire fronto-temporale (troubles du comportement et du langage).",
s:"Troubles de la mémoire récente avec désorientation temporo-spatiale, difficultés instrumentales (gestes, finances, médicaments), troubles du comportement (errance, apathie, agitation, hallucinations) ; corps de Lewy : fluctuations cognitives majeures, hallucinations visuelles détaillées, chutes, parkinsonisme ; vasculaire : épisodes focaux, marche à petits pas, troubles sphinctériens.",
dx:"Tests cognitifs (MMSE, MoCA) et évaluation fonctionnelle (IADL) ; bilan causal : NFS, TSH, B12, ionogramme, calcémie, scanner ou IRM cérébrale (atrophie, lésions vasculaires) ; bilan neuropsychologique ; consultation mémoire ; éliminer les causes curables (hydrocéphalie à pression normale, dépression, iatrogénie).",
t:"Mesures non pharmacologiques prioritaires (environnement stable et sécurisé, rééducation cognitive, formation et répit des aidants) ; inhibiteurs de la cholinestérase (Alzheimer, Lewy) puis mémantine ; démence à corps de Lewy : neuroleptiques formellement contre-indiqués ; contrôle des facteurs vasculaires ; protection juridique et directives anticipées précoces.",
k:"Hallucinations visuelles + fluctuations + parkinsonisme = démence à corps de Lewy : jamais de neuroleptique (réactions catastrophiques) ; toujours chercher une cause curable de trouble cognitif."}
,
{n:"Dénutrition protéino-énergétique de la personne âgée",q:"dénutrition de la personne âgée",
d:"Déséquilibre entre apports et besoins : dénutrition si perte de poids d'au moins 5 % en 1 mois ou 10 % en 6 mois ; causes : anorexie (dépression, solitude, pathologie), hypercatabolisme (infection, chirurgie, escarres), troubles masticatoires et de déglutition, dépendance, pauvreté.",
s:"Perte de poids involontaire, asthénie, fonte musculaire (sarcopénie), affaiblissement immunitaire (infections récidivantes), mauvaise cicatrisation, escarres, œdèmes de carence ; aggravation du déclin cognitif et fonctionnel ; asthénie et chutes.",
dx:"Poids répétés (courbe pondérale), IMC ; circonférence du mollet (< 31 cm : sarcopénie) ; albumine et préalbumine (en interprétant l'inflammation) ; Mini Nutritional Assessment (MNA) ; recherche des causes : examen bucco-dentaire, dépression, douleur, déglutition, autonomie, ressources financières.",
t:"Enrichissement calorique et protéique des repas (collations, compléments nutritionnels oraux 2/j), aide au repas et cadre convivial ; traitement des causes (prothèse dentaire, douleur, humeur) ; surveillance pondérale à 1 mois ; prévention systématique lors de tout épisode aigu ou d'hospitalisation.",
k:"Perte de poids de 5 % en 1 mois = dénutrition : chercher les causes (bouche, humeur, moyens financiers) et enrichir les apports, pas seulement « surveiller »."}
]},
{name:"Urgences Médicales Transversales",paths:[
{n:"États de choc (Septique, Cardiogénique, Anaphylactique, Hypovolémique)",q:"choc septique",ur:true,
d:"Insuffisance circulatoire aiguë avec inadéquation entre l'apport d'oxygène et les besoins cellulaires : choc septique (vasodilatation et dysfonction microcirculatoire sur infection), cardiogénique (défaillance de pompe), hypovolémique (hémorragie ou déshydratation), anaphylactique (hypersensibilité IgE-dépendante), obstructif (embolie pulmonaire, tamponnade, pneumothorax compressif).",
s:"Hypotension (PAS < 90 mmHg), marbrures, tachycardie, oligurie (< 0,5 mL/kg/h), troubles de conscience, lactates élevés ; orientation : fièvre et point d'appel infectieux (septique), œdème aigu du poumon et turgescence jugulaire (cardiogénique), saignement extériorisé ou interne (hypovolémique), urticaire géante, œdème de Quincke et bronchospasme (anaphylactique).",
dx:"Échographie au lit du patient (fonction cardiaque, VCI, épanchement péricardique), lactates, ionogramme, NFS, gaz du sang ; hémocultures et prélèvements du site infectieux ; échographie FAST (hémopéritoine) ; ECG ; radiographie thoracique ; étiologie guidée par le contexte.",
t:"Remplissage vasculaire par cristalloïdes (prudent si insuffisance cardiaque) ; noradrénaline si choc réfractaire au remplissage ; choc septique : antibiothérapie probabiliste dans l'heure et contrôle de la source ; anaphylaxie : adrénaline IM 0,3 à 0,5 mg immédiate (à répéter), oxygène, remplissage, puis antihistaminiques et corticoïdes ; hémorragique : contrôle du saignement et stratégie transfusionnelle ; monitorage (diurèse, ScvO2).",
k:"Anaphylaxie = adrénaline IM immédiate à répéter, avant tout le reste ; choc septique = antibiothérapie dans l'heure, remplissage et noradrénaline."}
,
{n:"Arrêt Cardiorespiratoire (ACR) et protocoles de réanimation",q:"arrêt cardiaque",ur:true,
d:"Abolition des signes de vie (inconscience, absence de ventilation normale, absence de pouls) ; causes cardiaques (coronarienne en premier) ou secondaires : les causes réversibles à systématiquement rechercher — hypoxie, hypovolémie, hypo- et hyperkaliémie, hypothermie, pneumothorax compressif, tamponnade, toxiques, thrombose coronarienne ou pulmonaire.",
s:"Inconscience, apnée ou respiration agonale (gasps), absence de pouls central ; sur monitorage : fibrillation ventriculaire, tachycardie ventriculaire sans pouls, activité électrique sans pouls ou asystolie ; chaque minute sans réanimation réduit la survie d'environ 10 %.",
dx:"Reconnaissance immédiate (signes de vie), rythme sur le défibrillateur ; pendant la réanimation : gaz du sang et kaliémie, glycémie, échographie clinique ; bilan étiologique après récupération d'une circulation spontanée (ECG, coronarographie, scanner).",
t:"Chaîne de survie : alerter, réanimation cardiopulmonaire précoce (100 à 120 compressions/min, 5-6 cm, interruptions < 10 s), défibrillation précoce si FV/TV ; adrénaline 1 mg IV toutes les 3-5 min, amiodarone ; gestion des voies aériennes ; traitement des causes réversibles ; soins post-arrêt : oxygénation contrôlée (SpO2 94-98 %), hémodynamique, température (cible 36 °C), angioplastie si infarctus.",
k:"Massage précoce + défibrillation précoce = survie ; ne pas interrompre les compressions plus de 10 secondes ; après le retour à une circulation spontanée, éviter l'hyperoxie et l'hypotension."}
,
{n:"Comas non traumatiques (explorations étiologiques)",q:"coma",ur:true,
d:"Abolition durable de la conscience sans traumatisme : causes métaboliques et toxiques réversibles (hypoglycémie, acidocétose, hyponatrémie, encéphalopathie hépatique, éthylisme, intoxications médicamenteuses) ou structurelles (accident vasculaire cérébral, hémorragie méningée, tumeur, abcès, état de mal épileptique).",
s:"Inconscience (score de Glasgow), respiration anormale (Cheyne-Stokes, Kussmaul), tonus pupillaire : myosis (opiacés), mydriase aréactive (anoxie), asymétrie pupillaire (engagement) ; signes de localisation, raideur de nuque, sueurs et tremblements (hypoglycémie), points de ponction ; fièvre, purpura (méningite).",
dx:"Glasgow, glycémie capillaire immédiate ; gaz du sang, ionogramme, calcémie, ammoniémie, recherche de toxiques, NFS, TP ; TDM cérébrale en urgence ; ponction lombaire après imagerie si hémorragie méningée non vue ; EEG (état de mal non convulsif).",
t:"Gestes immédiats avant l'étiologie : liberté des voies aériennes (intubation si Glasgow ≤ 8), position latérale de sécurité, oxygène, perfusion ; glucose IV si hypoglycémie, naloxone si opiacés suspectés, thiamine avant le glucose chez l'alcoolique ; traitement de la cause (antidotes, osmothérapie, drainage) ; prévention des complications (escarres, aspiration, thrombose).",
k:"Coma = glycémie capillaire immédiate (hypoglycémie curable en une minute) ; Glasgow ≤ 8 = intubation ; pupilles asymétriques = urgence neurochirurgicale potentielle."}
,
{n:"Toxidermies médicamenteuses graves (Stevens-Johnson et Lyell)",q:"nécrolyse épidermique toxique",ur:true,
d:"Réactions cutanées médicamenteuses sévères avec nécrose épidermique : syndrome de Stevens-Johnson (décollement inférieur à 10 % de la surface corporelle) et nécrolyse épidermique toxique de Lyell (supérieure à 30 %) ; médicaments responsables habituels : antiépileptiques (carbamazépine, lamotrigine), sulfamides, allopurinol, AINS, antirétroviraux ; réaction retardée 7 à 21 jours après l'introduction.",
s:"Prodrome pseudo-grippal (fièvre, brûlures oculaires) puis éruption maculeuse douloureuse, atteinte des muqueuses (conjonctivite, chéilite hémorragique, stomatite, atteinte génitale), décollement épidermique déclenché au doigt (signe de Nikolsky), purpura ; complications : sepsis sur perte de barrière, déshydratation, atteinte bronchique, insuffisance rénale.",
dx:"Clinique (score SCORTEN pour le pronostic) ; biopsie cutanée (nécrose kératinocytaire) ; arrêt du médicament causal et enquête de pharmacovigilance ; hémocultures, ionogramme, NFS ; avis ophtalmologique urgent (séquelles cornéennes).",
t:"Arrêt immédiat de tous les médicaments suspects et non indispensables ; transfert en réanimation ou en centre de brûlés : réanimation hydro-électrolytique et calorique, soins locaux antiseptiques, analgésie, prévention de l'infection (pas d'antibiothérapie probabiliste systématique) ; immunoglobulines IV ou corticoïdes discutés selon les protocoles ; déclaration en pharmacovigilance et inscription de l'allergie au dossier.",
k:"Éruption médicamenteuse fébrile + atteinte des muqueuses + signe de Nikolsky = Stevens-Johnson/Lyell : arrêt du médicament et transfert en réanimation."}
]}
]}
]});


/* ============================================================
   DÉPARTEMENT 2 — PÉDIATRIE (8 spécialités)
   ============================================================ */
DEPTS.push({
id:"ped",name:"Pédiatrie",icon:"👶",color:"#f59e0b",
desc:"Pathologies du nouveau-né, du nourrisson et de l'enfant : de la néonatologie aux urgences tropicales pédiatriques, en passant par les maladies chroniques de l'enfant et les troubles du développement.",
specs:[

{id:"ped-neo",num:1,name:"Néonatologie & Pathologies du Nouveau-Né",groups:[
{name:"Détresses Respiratoires Néonatales",paths:[
{n:"Maladie des membranes hyalines (MMH) / Syndrome de détresse respiratoire du prématuré",q:"détresse respiratoire du nouveau-né",ur:true,
d:"Détresse respiratoire du grand prématuré par déficit en surfactant alvéolaire (immaturité pulmonaire) : atélectasies diffuses, pneumopathie adhésive ; risque majeur avant 32 semaines d'aménorrhée.",
s:"Détresse respiratoire d'apparition dans les premières heures : polypnée, geignements expiratoires, tirage (intercostal, xiphoïdien, ensellure nasale), cyanose, apnées ; dégradation progressive sans traitement ; parfois ballonnement thoracique en cas de pneumothorax."
,
dx:"Radiographie thoracique : poumons blancs, bronchogramme aérien ; gaz du sang (hypoxie, hypercapnie) ; score de Silverman ; score d'Apgar et contexte de prématurité.",
t:"Oxygénothérapie et pression positive continue (CPAP) d'emblée ; surfactant exogène par intubation ; corticothérapie anténatale (bétaméthasone) pour la prévention ; soins du prématuré (incubateur, nutrition, prévention de l'hypothermie) ; complications : dysplasie broncho-pulmonaire, hémorragie pulmonaire.",
k:"Prématuré + détresse respiratoire dans les premières heures = maladie des membranes hyalines : surfactant et CPAP ; la corticothérapie anténatale la prévient."}
,
{n:"Inhalation méconiale",q:"inhalation méconiale",ur:true,
d:"Syndrome d'inhalation méconiale du nouveau-né à terme ou post-maturé : souffrance fœtale aiguë provoquant l'émission de méconium dans le liquide amniotique et son inhalation, responsable d'obstruction bronchique et d'un tableau de détresse avec hypertension pulmonaire persistante.",
s:"Liquide amniotique teinté (vert) + détresse respiratoire dès la naissance, polypnée, tirage, cyanose, thorax distendu (hyperinflation) ; aggravation possible avec hypertension pulmonaire (cyanose réfractaire).",
dx:"Anamnèse (liquide teinté, souffrance fœtale, Apgar bas) ; radiographie thoracique (infiltrats, hyperinflation, atélectasies) ; gaz du sang ; échocardiographie si suspicion d'hypertension pulmonaire persistante.",
t:"Aspiration prudente de l'oropharynx à la naissance si liquide teinté (pas d'intubation systématique) ; oxygène, ventilation au besoin, drainage thoracique si pneumothorax ; hypertension pulmonaire : monoxyde d'azote inhalé, oscillations ; antibiothérapie si surinfection.",
k:"Liquide amniotique teinté + détresse respiratoire du nouveau-né à terme = inhalation méconiale : aspiration prudente et surveillance de l'hypertension pulmonaire persistante."}
,
{n:"Tachypnée transitoire du nouveau-né (poumon humide)",q:"tachypnée transitoire du nouveau-né",
d:"Détresse respiratoire bénigne et transitoire (48-72 h) par résorption retardée du liquide pulmonaire fœtal, surtout après césarienne sans travail ; le diagnostic le plus fréquent de détresse respiratoire néonatale non grave à terme.",
s:"Polypnée et tirage modérés dès la première heure, sans geignement majeur, cyanose rare ; nouveau-né à terme ou post-maturé en général bon état général ; résolution spontanée en 48 à 72 heures.",
dx:"Radiographie : hyperinflation, épanchement des scissures, lignes de Kerley, épanchement pleural discret ( « poumon humide ») ; gaz du sang peu perturbés ; évolution rapidement favorable.",
t:"Oxygène modéré et surveillance ; alimentation fractionnée, perfusion si besoin ; pas de surfactant ni d'antibiotiques en l'absence de contexte infectieux ; réassurance parentale (guérison sans séquelle).",
k:"Détresse respiratoire modérée du nouveau-né à terme après césarienne, guérissant en 48-72 h = poumon humide : diagnostic d'évolution, favorable."}
,
{n:"Apnées du prématuré",q:"apnée du prématuré",ur:true,
d:"Pauses respiratoires supérieures à 20 secondes (ou plus courtes avec bradycardie/désaturation) par immaturité des centres respiratoires ; pathologie quasi constante du grand prématuré, diagnostic d'élimination des autres causes (infection, hypoglycémie, anémie, reflux).",
s:"Pauses respiratoires avec cyanose et bradycardie sur monitorage, parfois pâleur et hypotonie ; rythme nycthéméral, survenant surtout pendant le sommeil ; régression vers l'âge corrigé du terme.",
dx:"Enregistrement cardiorespiratoire (monitorage) ; éliminer les causes : NFS-CRP et hémoculture (infection), glycémie, ionogramme, bilan anémique, examen neurologique, contexte de reflux ; éventuel EEG selon le tableau.",
t:"Stimulation tactile lors des épisodes ; caféine citrate (traitement de référence) ; CPAP si épisodes persistants ; prévention : position, soins de développement, traitement des causes associées (anémie, reflux, infection) ; surveillance en unité kangourou.",
k:"Apnée du prématuré = diagnostic d'élimination : toujours éliminer une infection néonatale ou une hypoglycémie avant d'incriminer l'immaturité."}
]},
{name:"Infections Néonatales",paths:[
{n:"Infection néonatale précoce et tardive (sepsis à Streptocoque B, E. coli)",q:"infection néonatale",ur:true,
d:"Infection bactérienne du nouveau-né : précoce (moins de 72 h, transmission materno-fœtale : streptocoque B, E. coli, listeria) ou tardive (après 72 h, flore hospitalière et communautaire) ; le tableau peut se limiter à une thermo-instabilité ou une hypotonie.",
s:"Signes trompeurs et peu spécifiques : fièvre ou hypothermie, refus alimentaire, hypotonie, geignements, pâleur ou grisaille, détresse respiratoire, apnées, bradycardie, ictère d'apparition précoce ; forme grave : choc septique, méningite associée.",
dx:"Hémocultures, ponction lombaire (PL systématique si sepsis), ECBU, NFS-CRP-procalcitonine ; anamnèse maternelle : portage de streptocoque B, fièvre, RPM prolongée, chorioamniotite ; prélèvements gastriques et auriculaires discutés.",
t:"Antibiothérapie probabiliste IV d'emblée : amoxicilline + gentamicine (ou céfotaxime) après les prélèvements, adaptée ensuite ; réanimation (remplissage, catécholamines) si choc ; prévention : dépistage du portage maternel de streptocoque B à 37 SA et antibioprophylaxie per-partum.",
k:"Un nouveau-né « qui va mal » (grisaille, hypotonie, refus alimentaire) = infection jusqu'à preuve du contraire : PL et antibiothérapie après hémocultures."}
,
{n:"Méningite purulente du nouveau-né",q:"méningite néonatale",ur:true,
d:"Méningite bactérienne du nouveau-né (streptocoque B, E. coli, listeria, entérobactéries) : la présentation est souvent fruste, sans raideur de nuque — toute infection néonatale peut se compliquer d'une méningite associée.",
s:"Signes d'infection néonatale (thermo-instabilité, refus alimentaire, hypotonie) + irritabilité, pleurs aigus, bombé de la fontanelle, convulsions, apnées ; absence de raideur de nuque constante à cet âge.",
dx:"Ponction lombaire systématique devant tout sepsis néonatal : liquide trouble, hypercytose à PNN, hypoglycorachie, germe à l'examen direct ; hémocultures ; TDM cérébrale si signes neurologiques focaux ou convulsions (complications : ventriculite, abcès, hydrocéphalie).",
t:"Antibiothérapie IV adaptée et prolongée (céfotaxime + amoxicilline initialement, 3 semaines minimum) ; traitement des convulsions ; surveillance de l'hydrocéphalie (échographies transfontanelaires) ; séquelles possibles (surdité, retard mental) : suivi neurosensoriel.",
k:"Chez le nouveau-né, la méningite n'a pas de raideur : bombé de fontanelle, convulsions ou simple « sepsis » = PL systématique."}
,
{n:"Conjonctivite néonatale (ophtalmie néonatale)",q:"conjonctivite néonatale",
d:"Conjonctivite du nouveau-né dans les premiers jours ou semaines de vie : cause chimique (instillations à la naissance), bactérienne (Chlamydia trachomatis — la plus fréquente, gonocoque — la plus grave) ou virale (herpès) ; la gonococcique menace la cornée.",
s:"Œil rouge avec sécrétions : sérosité puis pus abondant (gonocoque), paupières œdématiées et bicollement ; chlamydiose : sécrétions mucopurulentes parfois tardives (2e semaine), souvent unilatérale ; herpétique : vésicules périoculaires, kératite.",
dx:"Prélèvements conjonctivaux (bactériologie, PCR chlamydia et gonocoque) ; examiner la cornée à la fluorescéine ; examen des parents (IST) ; la gonococcique est à déclaration obligatoire.",
t:"Lavages au sérum physiologique ; chlamydia : érythromycine orale (traiter aussi la mère) ; gonocoque : C3G IV ou IM + lavages (urgence : risque de perforation cornéenne) ; herpès : aciclovir IV ; traiter systématiquement les parents (IST) et dépister les co-infections.",
k:"Pus abondant des premiers jours de vie = ophtalmie gonococcique : C3G immédiat, risque de cécité ; toujours dépister et traiter les parents."}
]},
{name:"Ictères & Troubles Métaboliques",paths:[
{n:"Ictère néonatal physiologique et pathologique (ictère nucléaire, incompatibilité rhésus ou ABO)",q:"ictère néonatal",ur:true,
d:"Ictère néonatal par hyperbilirubinémie libre : physiologique (immaturité de la glucuronyltransférase, jours 2-5, sans danger) ou pathologique (précoce : hémolyse par incompatibilité rhésus/ABO ; retardé : allaitement, infection, hypothyroïdie, déficit en G6PD) ; le risque majeur est l'ictère nucléaire (kernictère) par dépôt de bilirubine dans les noyaux gris centraux.",
s:"Ictère cutanéo-muqueux d'extension céphalo-caudale ; ictère pathologique : précoce (premières 24 h), intense, avec pâleur ou hépatosplénomégalie (hémolyse) ; signes d'ictère nucléaire : hypertonie opisthotonos, pleurs aigus, sommeil inversé, convulsions, surdité — urgence absolue.",
dx:"Bilirubine totale et libre sur sang capillaire (courbes selon âge et terme) ; groupe sanguin et RAI mère/enfant, test de Coombs (incompatibilité) ; NFS-réticulocytes (hémolyse), G6PD, TSH ; examen clinique (recherche d'infection, hématome).",
t:"Photothérapie selon les courbes (âge, terme, facteurs de risque) ; exsanguino-transfusion si valeurs menaçantes ; hémolyse rhésus : prévention par immunoglobulines anti-D chez la mère ; ictère nucléaire : échange transfusionnel en urgence ; traiter les causes (infection, hypothyroïdie).",
k:"Ictère dès les premières 24 heures, ou avec pâleur, ou fébrile = pathologique : Coombs et bilirubinémie — l'ictère nucléaire est une urgence de l'exsanguinotransfusion."}
,
{n:"Hypoglycémie du nouveau-né de mère diabétique et hypothermie néonatale",q:"hypoglycémie néonatale",ur:true,
d:"Hypoglycémie néonatale (inférieure à 0,30 g/L la première semaine) : le nouveau-né de mère diabétique (hyperinsulinisme compensatoire) est le terrain classique ; l'hypothermie (inférieure à 36 °C) l'accompagne souvent chez le prématuré et le nourrisson en détresse.",
s:"Signes non spécifiques : tremblements, hypertonie, hypotonie, pleurs, refus alimentaire, cyanose, apnées, convulsions ; nouveau-né macrosome (mère diabétique), ou au contraire hypotrophe ; hypothermie : extrémités froides, grisaille.",
dx:"Glycémie capillaire de dépistage systématique chez tout nouveau-né à risque (mère diabétique, prématuré, macrosome, hypotrophe, détresse) confirmée au laboratoire ; température ; bilan si hypoglycémie persistante (insulinémie, cortisol, GH).",
t:"Alimentation précoce (tétée ou gavage) si glycémie modérément abaissée ; glucose IV (G10 %) si sévère ou asymptomatique résistant ; corriger l'hypothermie : peau à peau, incubateur ; surveillance glycémique répétée ; équilibre du diabète maternel pendant la grossesse = prévention.",
k:"Nouveau-né de mère diabétique = macrosome + hypoglycémie + détresse respiratoire : surveiller glycémie et température dès la première heure."}
,
{n:"Asphyxie périnatale et encéphalopathie ischémique hypoxique (EIH)",q:"encéphalopathie anoxique",ur:true,
d:"Souffrance périnatale aiguë (anoxie ou ischémie) : encéphalopathie ischémique hypoxique du nouveau-né à terme, classée en stades de Sarnat I à III ; cause majeure de mortalité néonatale et de paralysie cérébrale dans le monde.",
s:"Score d'Apgar bas (moins de 7 à 5 minutes), liquide amniotique teinté, pH cordon acide ; nouveau-né hypotonique, sans cry, éventuellement convulsions dans les 24 premières heures ; stade II : hypotonie, convulsions, troubles de succion ; stade III : coma, hypertonie ou hypotonie majeure.",
dx:"pH et lactates au cordon, score d'Apgar, examen neurologique séquentiel ; EEG et imagerie (IRM cérébrale) pour le pronostic ; surveillance glycémique et hémodynamique ; bilan de coagulation, fonctions rénales et hépatiques (atteinte multiviscérale).",
t:"Réanimation néonatale immédiate ; hypothermie thérapeutique contrôlée (33-34 °C pendant 72 h) dans les 6 heures si encéphalopathie modérée à sévère — réduit la mortalité et le handicap ; soins de support : équilibre glycémique, hémodynamique, anticonvulsivants ; suivi neurodéveloppemental prolongé.",
k:"Apgar bas + acidose + convulsions néonatales = encéphalopathie hypoxique-ischémique : hypothermie thérapeutique dans les 6 heures, dans un centre de néonatologie."}
]}
]},

{id:"ped-infect",num:2,name:"Infectiologie & Médecine Tropicale Pédiatrique",groups:[
{name:"Urgences & Formes Graves",paths:[
{n:"Paludisme grave de l'enfant (neuropaludisme, anémie palustre aiguë)",q:"paludisme de l'enfant",ur:true,
d:"Paludisme à Plasmodium falciparum de l'enfant de zone d'endémie (ou au retour de voyage) ; la mortalité pédiatrique palustre se concentre avant 5 ans ; critères de gravité OMS : troubles de la conscience (neuropaludisme), anémie sévère, détresse respiratoire, hypoglycémie, convulsions répétées.",
s:"Fièvre (parfois irrégulière), prostration, refus alimentaire, vomissements ; neuropaludisme : obnubilation, convulsions, coma ; anémie palustre aiguë : pâleur profonde, polypnée, tachycardie ; détresse respiratoire (acidose), urines foncées.",
dx:"Test de diagnostic rapide et goutte épaisse (espèce, parasitémie) en urgence ; glycémie, NFS (anémie, thrombopénie), créatinine, ionogramme, lactates ; examen neurologique ; éliminer une méningite (PL si doute chez l'enfant inconscient).",
t:"Artésunate IV en urgence (traitement de référence du paludisme grave, supérieur à la quinine) suivi d'une cure complète par ACT ; soins de support : transfusion si anémie sévère, correction de l'hypoglycémie, oxygène ; soins intensifs si coma ; prévention : moustiquaires imprégnées, chimioprophylaxie de la femme enceinte (TPI).",
k:"Enfant fébrile comateux en zone d'endémie = neuropaludisme : artésunate IV immédiatement, goutte épaisse et glycémie (hypoglycémie fréquente)."}
,
{n:"Sepsis sévère et choc septique pédiatrique",q:"choc septique de l'enfant",ur:true,
d:"Réponse inflammatoire systémique à une infection avec défaillance d'organe (sepsis sévère) ou hypotension réfractaire au remplissage (choc septique) ; chez l'enfant, la présentation est une fièvre avec tachycardie et polypnée, l'hypotension étant tardive (signe préagonique).",
s:"Fièvre (ou hypothermie chez le nourrisson), tachycardie, polypnée, allongement du temps de recoloration cutanée (plus de 3 s), marbrures, pâleur, oligurie, agitation puis abattement, confusion ; points d'appel : pneumonie, méningite, gastro-entérite, infection urinaire, rougeole.",
dx:"Hémocultures et prélèvements selon le point d'appel (PL, ECBU, radiographie) ; NFS-CRP-procalcitonine, lactates, gaz du sang, ionogramme, glycémie ; monitorage : diurèse horaire, TA (les valeurs normales dépendent de l'âge).",
t:"Antibiothérapie IV probabiliste large dans l'heure après hémocultures ; remplissage prudent par cristalloïdes (10-20 mL/kg, réévalué, prudence si détresse respiratoire) ; vasopresseurs (adrénaline ou noradrénaline) précoces ; correction des troubles métaboliques (hypoglycémie, hypocalcémie) ; source control (drainage) ; soins intensifs.",
k:"Chez l'enfant, l'hypotension est un signe tardif : le temps de recoloration cutanée allongé et la tachycardie fébrile annoncent le choc — remplissage et antibiotiques sans attendre la chute tensionnelle."}
,
{n:"Purpura fulminans (infection à méningocoque)",q:"purpura fulminans",ur:true,
d:"Septicémie à Neisseria meningitidis avec coagulation intravasculaire disséminée : purpura nécrotique extensif et choc septique fulminant ; urgence absolue de pronostic mortel (heures) ; pics chez le nourrisson et l'adolescent.",
s:"Fièvre élevée brutale avec purpura pétéchial puis ecchymotique et nécrotique extensif (membres, visage), choc (marbrures, cyanose, extrémités froides), trouble de conscience ; évolution parfois foudroyante (décès en quelques heures) ; méningite associée possible (raideur) mais souvent absente.",
dx:"Clinique = urgence : aucun examen ne doit retarder l'antibiothérapie ; hémocultures et ponction lombaire seulement si hémodynamique stable ; TDM inutile ; NFS, coagulation (CIVD), lactates.",
t:"Antibiothérapie IMMÉDIATE avant tout : céfotaxime ou ceftriaxone IV en urgence (y compris en pré-hospitalier) ; réanimation : remplissage, catécholamines, correction de la CIVD (fibrinogène, plasma), sédation-analgésie ; transfert en réanimation ; prophylaxie des contacts (rifampicine ou ciprofloxacine) ; vaccination anti-méningococcique en prévention.",
k:"Fièvre + purpura nécrotique = purpura fulminans : C3G IV immédiate, sans attendre hémocultures ni PL — chaque minute compte."}
,
{n:"Méningites bactériennes aiguës et encéphalites infectieuses de l'enfant",q:"méningite de l'enfant",ur:true,
d:"Méningites bactériennes de l'enfant : pneumocoque et méningocoque après la vaccination anti-Haemophilus ; nouveau-né (streptocoque B, E. coli) ; encéphalites virales (herpétique, rougeole, arboviroses) atteignant le parenchyme cérébral.",
s:"Chez le nourrisson : fièvre, irritabilité ou abattement, refus alimentaire, vomissements, bombé de fontanelle, convulsions (pas de raideur de nuque fiable) ; enfant plus grand : céphalées, raideur de nuque, vomissements, photophobie ; encéphalite : troubles de conscience, crises, troubles du comportement.",
dx:"Ponction lombaire (sauf CI) : hypercytose à PNN et hypoglycorachie (bactérienne), PCR herpétique ; hémocultures, NFS-CRP ; TDM si signes de focalisation ou hypertension intracrânienne ; chez le nourrisson : bilan complet de l'infection (urines, radiographie).",
t:"C3G IV à forte dose immédiate (céfotaxime ou ceftriaxone) ± dexaméthasone ; encéphalite herpétique : aciclovir IV ; traitement des convulsions ; soins de support ; suivi des séquelles (surdité : audition systématique après guérison) ; prophylaxie des contacts si méningocoque.",
k:"Fièvre + irritabilité ou fontanelle bombée chez un nourrisson = PL en urgence ; l'antibiothérapie ne doit jamais être retardée par l'imagerie."}
,
{n:"Tétanos néonatal et de l'enfant",q:"tétanos néonatal",ur:true,
d:"Tétanos du nouveau-né par contamination du cordon à la naissance (pratiques d'hygiène non stériles, mère non vaccinée) : une des causes évitables de mortalité néonatale dans les pays à faibles ressources ; l'enfant non vacciné est exposé par les plaies souillées.",
s:"Nouveau-né de 3 à 28 jours (le plus souvent entre 5 et 15 jours) qui refuse de s'alimenter, puis trismus, rigidité, spasmes déclenchés par les stimuli, opisthotonos, spasmes laryngés ; mère non vaccinée contre le tétanos.",
dx:"Diagnostic clinique (rien ne doit retarder la prise en charge) ; anamnèse maternelle : absence de vaccination, accouchement à domicile avec coupe du cordon sur instrument non stérile.",
t:"Soins intensifs : calme absolu (pièce sombre et silencieuse), aspiration des sécrétions, sédation et curarisation si spasmes, ventilation ; immunoglobulines antitétaniques et sérum antitétanique ; antibiothérapie (métronidazole) ; nettoyage de la plaie/cordon ; vaccination de l'enfant et de l'entourage ; prévention : vaccination des femmes enceintes.",
k:"Nouveau-né qui ne tète plus et devient raide = tétanos ombilical : mère non vaccinée — la vaccination des femmes enceintes (VAT) l'éradique."}
]},
{name:"Infections Courantes & Tropicales",paths:[
{n:"Fièvre typhoïde compliquée de l'enfant",q:"fièvre typhoïde de l'enfant",
d:"Salmonellose systémique (Salmonella Typhi) de l'enfant dans les zones de faible hygiène : fièvre prolongée avec douleurs abdominales ; complications digestives hémorragiques et perforatives.",
s:"Fièvre croissante en plateau avec abattement, céphalées, anorexie, douleurs abdominales, diarrhée ou constipation, splénomégalie, langue saburrale ; complications : hémorragie digestive (méléna), perforation intestinale (péritonite), choc septique, troubles neurologiques.",
dx:"Hémocultures (les plus rentables la première semaine), coproculture, sérodiagnostic de Widal ; NFS (leuconeutropénie), CRP ; échographie ou radiographie si suspicion de perforation (pneumopéritoine).",
t:"Céfotaxime ou ceftriaxone IV (ou azithromycine selon sensibilité) 7-10 jours ; prise en charge chirurgicale de la perforation ; réhydratation et nutrition ; éviction scolaire et mesures d'hygiène ; vaccination des voyageurs ; assainissement de l'eau.",
k:"Fièvre prolongée chez un enfant en zone d'endémie avec tuphos et douleurs abdominales = fièvre typhoïde : hémocultures ; surveiller perforation et hémorragie."}
,
{n:"Rougeole et complications (pneumonie, kératite, dénutrition post-rougeoleuse)",q:"rougeole",ur:true,
d:"Infection virale éruptive ultra-contagieuse (paramyxovirus, Morbillivirus) : fièvre, catarrhe, éruption ; chez l'enfant dénutri, immunodéprimé ou carencé en vitamine A, la rougeole est grave (pneumonie, kératite cécitante, encéphalite) ; immunodépression transitoire et dénutrition post-rougeole.",
s:"Fièvre élevée, conjonctivite, coryza, toux (catarrhe oculo-respiratoire), signe de Koplik (taches blanches sur muqueuse jugale) puis éruption maculo-papuleuse descendante (visage puis tronc et membres) ; complications : pneumonie (première cause de mort), laryngite, diarrhée, kératite et cécité, encéphalite, poussée de dénutrition.",
dx:"Clinique (Koplik = pathognomonique) ; confirmation : IgM ou PCR sur salive/urine ; sérologie VIH si forme atypique ; recherche des complications : radiographie, examen ophtalmologique à la fluorescéine.",
t:"Vitamine A forte dose (2 journées consécutives — réduit la mortalité) ; traitement des complications : oxygène, antibiothérapie des surinfections bactériennes, soins oculaires (pommade + vitamine A) ; nutrition (alimentation enrichie) ; isolement respiratoire ; déclaration obligatoire ; vaccination en prévention (ROR) et vaccination d'urgence des contacts.",
k:"Fièvre + catarrhe + Koplik puis éruption descendante = rougeole : vitamine A systématique et surveillance nutritionnelle ; la vaccination prévient tout."}
,
{n:"Coqueluche (quintes de toux cyanosantes du nourrisson)",q:"coqueluche",ur:true,
d:"Infection à Bordetella pertussis : toux persistante paroxystique de plus de 2 semaines, très grave chez le nourrisson de moins de 3 mois (apnées, quintes cyanosantes) ; la source est souvent un adulte ou un adolescent peu symptomatique.",
s:"Phase catarrhale (rhinite, toux banale 1-2 semaines) puis quintes : toux en éperonnement suivi d'une reprise inspiratoire (chant du coq), vomissements, cyanose, apnées chez le nourrisson ; complications : surinfection bactérienne, convulsions (hypoxie), détresses, décès avant 3 mois.",
dx:"PCR naso-pharyngée (3 premières semaines) ou sérologie ; NFS : hyperleucocytose à lymphocytes ; radiographie si suspicion de surinfection ; enquête autour du cas (l'entourage est la source).",
t:"Nourrisson : hospitalisation, surveillance monitorée (apnées), oxygène, alimentation fractionnée ; azithromycine 5 jours (le nourrisson et l'entourage) ; antibioprophylaxie des contacts proches ; prévention : vaccination du nourrisson (2, 3, 4 puis rappels) et cocooning (vaccination des parents et fratrie).",
k:"Toux en quintes avec reprise inspiratoire et vomissements = coqueluche ; chez le nourrisson, les apnées et les quintes cyanosantes imposent l'hospitalisation."}
,
{n:"Oreillons, Varicelle et exanthèmes viraux de l'enfant",q:"varicelle de l'enfant",
d:"Infections éruptives virales banales de l'enfance : oreillons (paramyxovirus, parotidite), varicelle (VZV : vésicules en « gouttes de rosée »), roséole, mégalérythème érythémateux ; la varicelle reste grave chez l'immunodéprimé, le nouveau-né et l'adulte.",
s:"Oreillons : tuméfaction parotidienne douloureuse bilatérale, fièvre, risque d'orchite (adolescent) et de méningite ; varicelle : fièvre modérée, éruption vésiculaire prurigineuse d'âges différents (polymorphisme) tronc puis visage ; roséole : fièvre 3 jours puis éruption à la défervescence.",
dx:"Clinique le plus souvent ; PCR ou sérologies dans les formes graves ou atypiques ; NFS-CRP si surinfection (varicelle : impétigo, surinfection streptococcique).",
t:"Symptomatique : antipyrétiques (paracétamol jamais d'AINS dans la varicelle), soins des lésions (antisepsie douce, ongles courts), hydratation ; aciclovir si immunodépression, varicelle néonatale, pneumopathie ; oreillons : soutien, orchite (suspensoire, antalgiques) ; isolation scolaire ; éviter l'aspirine (risque de syndrome de Reye).",
k:"Varicelle = éruption vésiculaire polymorphe (éléments d'âges différents) ; jamais d'aspirine ni d'AINS chez l'enfant (syndrome de Reye, surinfections à streptocoque A)."}
,
{n:"Parasitoses intestinales massives (ascaridiose, ankylostomose, giardiase)",q:"parasitoses intestinales de l'enfant",
d:"Helminthiases et protozooses intestinales de l'enfant en zone tropicale : ascaridiose (Ascaris lumbricoides), ankylostomose (Ancylostoma duodenale — anémie ferriprive), giardiase (Giardia duodenalis) ; responsables de troubles digestifs, de malnutrition et d'anémie.",
s:"Douleurs abdominales, diarrhée chronique ou intermittente, ballonnement, anorexie, retard de croissance, pâleur (ankylostomose : saignement chronique) ; ascaridiose : vomissements de vers, obstruction intestinale, toux (phase de migration) ; giardiase : diarrhée graisseuse, asthénie.",
dx:"Examen parasitologique des selles (œufs, kystes, larves, à plusieurs reprises) ; NFS (éosinophilie, anémie), ferritine ; courbe de croissance ; protides et albumine.",
t:"Antiparasitaires : albendazole ou mébendazole (ascaridiase, ankylostomose), métronidazole ou nitazoxanide (giardiase) ; supplémentation en fer (ankylostomose) et renutrition ; hygiène : eau potable, lavage des mains, port de chaussures (ankylostome), assainissement ; déparasitage de masse dans les zones d'endémie (OMS).",
k:"Anémie ferriprive + retard de croissance en zone tropicale = parasitose intestinale (ankylostomose en premier) : coprologie et fer."}
]}
]},

{id:"ped-pneumo",num:3,name:"Pneumologie Pédiatrique",groups:[
{name:"Infections Respiratoires Aiguës (IRA)",paths:[
{n:"Bronchiolite aiguë du nourrisson (VRS)",q:"bronchiolite",ur:true,
d:"Infection virale épidémique (hivernale) des bronchioles du nourrisson de moins de 2 ans, le plus souvent au virus respiratoire syncytial (VRS) : obstruction bronchiolaire avec sibilants et gêne expiratoire ; première cause d'hospitalisation du nourrisson.",
s:"Rhinite suivie de toux, polypnée, sibilants expiratoires, tirage et battements des ailes du nez, difficultés alimentaires (baisse des prises), fièvre modérée ; signes de gravité : apnées, refus alimentaire, désaturation, épuisement, déshydratation.",
dx:"Clinique (aucun examen systématique) ; radiographie seulement si doute (surinfection, pneumopathie) ; saturation en oxygène ; réévaluation de la tolérance alimentaire et respiratoire.",
t:"Désobstruction rhinopharyngée et fractionnement des repas (mesures essentielles) ; oxygène si SpO2 < 90-92 % ; hydratation, kinésithérapie de désobstruction discutée ; pas de bronchodilatateurs systématiques ni d'antibiotiques ni de corticoïdes ; hospitalisation si âge < 6 semaines, apnées, mauvaise tolérance, terrain (prématurité, cardiopathie) ; prévention : anticorps monoclonaux anti-VRS pour les nourrissons à très haut risque.",
k:"Bronchiolite = nourrisson sifflant en épidémie hivernale : désobstruction et fractionnement des repas — ni antibiotiques ni corticoïdes ; surveiller l'alimentation avant tout."}
,
{n:"Pneumonie aiguë communautaire (PAC) et bronchopneumonies de l'enfant",q:"pneumonie de l'enfant",ur:true,
d:"Infection du parenchyme pulmonaire de l'enfant : pneumocoque le plus souvent, mais aussi Mycoplasma (âge scolaire), virus, staphylocoque (formes graves) ; les bronchopneumonies du nourrisson sont souvent virales ou mixtes.",
s:"Fièvre élevée, toux, polypnée (signe cardinal, plus fiable que la fièvre chez le nourrisson), tirage, geignement ; signes de gravité : refus alimentaire, déshydratation, cyanose, apnées, abattement ; auscultation : crépitants focalisés ou diffus.",
dx:"Polypnée et signes de lutte ; radiographie thoracique (foyer de condensation) si signes de gravité ou doute, pas systématique dans les formes légères ; NFS-CRP, hémocultures si hospitalisée ; saturation ; éliminer une inhalation (fausse route), une tuberculose, un corps étranger si évolution traînante.",
t:"Ambulatoire : amoxicilline orale (première intention) 5-7 jours ; formes graves ou nourrisson : céphalosporine de 3e génération IV ± macrolide (germe atypique du grand enfant) ; oxygène, hydratation, antipyrétiques ; prévention : vaccination antipneumococcique et antigrippale.",
k:"Chez l'enfant, la polypnée fébrile définit la pneumonie : âge et gravité orientent l'antibiothérapie (amoxicilline ; atypiques du grand enfant)."}
,
{n:"Laryngite aiguë sous-glottique (croup) et épiglottite",q:"croup",ur:true,
d:"Laryngite aiguë sous-glottique (croup) : œdème sous-glottique viral (para-influenza) du nourrisson et du jeune enfant ; l'épiglottite (à Haemophilus influenzae b, devenue rare grâce à la vaccination) reste l'urgence absolue du carrefour aéro-digestif.",
s:"Croup : toux aboyante, dysphonie, tirage inspiratoire, symptômes majorés la nuit, fièvre modérée ; épiglottite : enfant toxique, hypersialorrhée, position assise en trépied, dysphagie majeure, absence de toux, détresse rapide — urgence absolue (risque d'obstruction complète).",
dx:"Croup : clinique (score de Westley), pas d'examen agressif ; épiglottite : AUCUN examen de l'oropharynx (risque de déclenchement du laryngospasme) — l'intubation en conditions contrôlées au bloc confirme le diagnostic.",
t:"Croup : corticoïdes systématiques (dexaméthasone ou prednisolone orale, une dose) ± adrénaline nébulisée si forme sévère, apaisement, oxygène ; épiglottite : appeler l'ORL et l'anesthésiste-réanimateur, intubation au bloc opératoire, céphalosporine de 3e génération IV — ne jamais allonger ni examiner la gorge.",
k:"Toux aboyante nocturne du nourrisson = laryngite : une dose de corticoïdes ; enfant assis bavant sans toux = épiglottite : intubation au bloc, jamais d'examen de la gorge ni de décubitus."}
,
{n:"Bronchite aiguë et angines aiguës (virales et streptococciques) de l'enfant",q:"angine",
d:"Bronchite aiguë : toux virale banale de l'enfant (pas d'antibiotique) ; angine : pharyngite aiguë — virale dans 70-90 % des cas, streptococcique (streptocoque du groupe A) chez l'enfant de plus de 3 ans, à traiter pour prévenir le rhumatisme articulaire aigu.",
s:"Bronchite : toux sèche puis grasse pendant 8-10 jours, fièvre modérée, bon état général ; angine : douleur pharyngée, dysphagie, fièvre, exsudat et punctuations du voile (angine érythémato-pultacée), adénopathies cervicales ; âge 3-15 ans et absence de toux = streptococcique probable.",
dx:"Test de diagnostic rapide du streptocoque A (TDR) chez l'enfant de plus de 3 ans (obligatoire avant toute antibiothérapie) ; pas d'examen pour la bronchite virale ni pour l'angine du petit enfant (moins de 3 ans : presque toujours virale).",
t:"Angine streptococcique (TDR positif) : amoxicilline orale 6 jours ; angine virale et bronchite : traitement symptomatique (paracétamol, hydratation) sans antibiotique ; éducation des familles ; la vaccination n'existe pas contre ces virus.",
k:"Angine de l'enfant de plus de 3 ans = TDR avant tout antibiotique ; TDR positif : amoxicilline 6 jours pour prévenir le rhumatisme articulaire aigu."}
]},
{name:"Pathologies Chroniques & Obstructions",paths:[
{n:"Asthme du nourrisson, de l'enfant et de l'adolescent",q:"asthme de l'enfant",ur:true,
d:"Maladie inflammatoire chronique des bronches la plus fréquente de l'enfant : sifflements récidivants déclenchés par les infections virales (nourrisson), l'effort, les allergènes ; le diagnostic est clinique, sur la répétition des épisodes et leur réversibilité.",
s:"Épisodes récidivants de sibilants, toux nocturne, dyspnée d'effort, oppression ; exacerbations : polypnée, sibilants, tirage, désaturation ; terrain atopique (eczéma, rhinite allergique) et familial.",
dx:"Clinique (fréquence et sévérité des crises, intervalles libres) ; EFR avec test de réversibilité dès que l'âge le permet (5-6 ans) ; bilan allergologique ; carnet de crises et questionnaire de contrôle (ACT-enfant).",
t:"Éducation (technique d'inhalation, plan d'action écrit) ; traitement de fond par corticoïdes inhalés si asthme persistant, bêta-2 de courte durée à la demande ; exacerbation : bêta-2 nébulisé répété, corticoïdes oraux 3-5 jours, oxygène ; hospitalisation si signes de gravité ; contrôle de l'environnement (tabagisme passif ++).",
k:"Sifflements récidivants chez l'enfant = asthme : corticoïdes inhalés en fond et éducation réduisent les crises ; l'exacerbation = bêta-2 + corticoïdes oraux."}
,
{n:"Corps étranger des voies aériennes (inhalation et fausse route)",q:"corps étranger des voies aériennes",ur:true,
d:"Inhalation d'un corps étranger (arachide, petit objet) chez l'enfant de 1 à 3 ans : accident de la vie courante, urgence diagnostique et thérapeutique ; toute toux ou détresse brutale dans un contexte de jeu ou de repas doit l'évoquer.",
s:"Toux brutale, suffocation, détresse respiratoire aiguë au décours d'un jeu ou d'un repas ; asymétrie auscultatoire (abolition unilatérale du murmure vésiculaire, sifflement localisé) ; formes traînantes : pneumopathie récidivante du même territoire, toux chronique.",
dx:"Anamnèse + examen (asymétrie) ; radiographie thoracique en inspiration et expiration (piège à air, corps étranger radio-opaque) ; endoscopie bronchique diagnostique et thérapeutique.",
t:"Enfant qui tousse et respire : ne pas s'affoler, oxygène, endoscopie sous anesthésie générale rapide en centre spécialisé ; obstruction complète : tapes dorsales et manœuvre de Heimlich adaptée à l'âge, appel immédiat des secours ; jamais de tentative de récupération à l'aveugle ; prévention : pas d'arachides ni de petits objets avant 4-5 ans.",
k:"Accès de suffocation chez un jeune enfant = corps étranger inhalé : asymétrie auscultatoire et endoscopie ; obstruction complète = Heimlich adapté à l'âge et appel des secours."}
,
{n:"Dysplasie broncho-pulmonaire (chez l'ancien prématuré)",q:"dysplasie bronchopulmonaire",
d:"Complication chronique de la grande prématurité (ancien nouveau-né traité pour maladie des membranes hyalines) : anomalie du développement pulmonaire nécessitant oxygène ou assistance respiratoire au-delà de 36 semaines d'âge corrigé.",
s:"Ancien prématuré : polypnée persistante, tirage modéré, épisodes de désaturation, bronchiolites et infections respiratoires récidivantes, tolérance à l'effort limitée, difficultés alimentaires.",
dx:"Contexte (terme, durée de l'oxygénothérapie et de la ventilation) ; radiographie ou scanner thoracique (distension, anomalies interstitielles) ; saturation en air ambiant, gaz du sang ; suivi pneumologique et de la croissance.",
t:"Oxygénothérapie à domicile si hypoxémie ; vaccinations complètes (grippe, pneumocoque, immunoprophylaxie du VRS si indiqué) ; traitement des exacerbations ; nutrition enrichie, kinésithérapie respiratoire ; protection contre le tabagisme passif.",
k:"Ancien prématuré qui siffle et se désature = dysplasie broncho-pulmonaire : vaccinations, oxygène si besoin, et surtout zéro tabac."}
,
{n:"Apnées obstructives du sommeil de l'enfant (hypertrophie amygdalienne/végétations)",q:"apnées obstructives du sommeil de l'enfant",
d:"Syndrome d'apnées obstructives de l'enfant, avant tout par hypertrophie amygdalienne et adénoïdienne : obstruction répétée des voies aériennes supérieures pendant le sommeil, retentissant sur la croissance, le comportement et les apprentissages.",
s:"Ronflements sonores et réguliers, pauses respiratoires observées par les parents, sommeil agité, position nocturne anormale (cou en extension), sueurs, énurésie ; retentissement diurne : somnolence ou au contraire hyperactivité, troubles de l'attention, retard de croissance.",
dx:"Examen ORL (amygdales, végétations, cavum), courbe de croissance ; polygraphie ventilatoire nocturne ; avis orthodontique ; évaluation des apprentissages.",
t:"Adénoïdectomie ± amygdalectomie (traitement curatif dans la grande majorité des cas) ; réévaluation post-opératoire ; mesures associées : perte de poids si surpoids, traitement de la rhinite allergique ; pression positive continue si persistance.",
k:"Enfant qui ronfle toutes les nuits avec des pauses = apnées obstructives : polygraphie et avis ORL — l'adénoïdectomie guérit la plupart."}
]}
]},

{id:"ped-gastro",num:4,name:"Gastro-Entérologie & Nutrition Pédiatrique",groups:[
{name:"Troubles Aigus & Déshydratation",paths:[
{n:"Gastro-entérite aiguë (virale à rotavirus, bactérienne) et déshydratation aiguë",q:"gastro-entérite aiguë de l'enfant",ur:true,
d:"Diarrhée aiguë infectieuse du nourrisson et de l'enfant (virale : rotavirus, norovirus dans la majorité ; bactérienne : salmonelle, shigelle, E. coli selon le contexte) ; le risque vital est la déshydratation aiguë (légère, modérée ou sévère avec collapsus).",
s:"Diarrhée liquide abondante ± vomissements, fièvre modérée, douleurs abdominales ; déshydratation : soif, muqueuses sèches, cernes, fontanelle déprimée, pli cutané persistant, oligurie, perte de poids ; sévère : choc, marbrures, troubles de conscience.",
dx:"Perte de poids sur la courbe, signes cliniques de déshydratation ; ionogramme, urée, glycémie si déshydratation sévère ; coproculture et recherche de toxines seulement si contexte (sang, fièvre élevée, épidémie, retour de voyage).",
t:"Réhydratation orale systématique d'abord : soluté de réhydratation orale (SRO) par petites quantités fréquentes ; réalimentation précoce (poursuite de l'allaitement maternel) ; zinc 10-14 jours ; réhydratation IV si choc ou échec oral ; pas d'antidiarrhéiques ni d'antibiotiques systématiques ; prévention : hygiène, vaccination anti-rotavirus.",
k:"Gastro-entérite de l'enfant = SRO précoces et réalimentation rapide : la déshydratation tue encore ; jamais d'antidiarrhéique."}
,
{n:"Invagination intestinale aiguë (IIA) du nourrisson",q:"invagination intestinale",ur:true,
d:"Engainement d'un segment intestinal dans le segment d'aval (iléo-cæcal le plus souvent) chez le nourrisson de 3 mois à 2 ans (pic entre 6 et 9 mois) : obstacle avec risque de nécrose intestinale ; parfois secondaire à une lésion en tête (diverticule de Meckel, purpura rhumatoïde).",
s:"Paroxystisme : crises douloureuses avec pleurs inconsolables, repli des jambes sur l'abdomen, pâleur, vomissements, entre des intervalles libres ; selles glairo-sanglantes « groseille » tardives ; masse abdominale en boudin ; enfant abattu, choc si nécrose.",
dx:"Échographie abdominale (signe de la cible, boudin) = examen de référence ; radiographie si suspicion de perforation ; la clinique des crises paroxystiques du nourrisson suffit à déclencher l'urgence.",
t:"Réduction par lavement pneumatique ou hydrostatique sous contrôle radiologique (première intention si enfant stable) ; chirurgie si échec, perforation ou instabilité (résection si nécrose) ; à jeun, réhydratation, antibioprophylaxie ; surveillance (récidive dans 10 % des cas).",
k:"Nourrisson avec crises douloureuses paroxystiques + vomissements + pâleur = invagination intestinale aiguë : échographie en urgence, lavement réducteur."}
,
{n:"Sténose du pylore du nourrisson (vomissements en jet)",q:"sténose du pylore",ur:true,
d:"Hypertrophie du pylore entre la 2e et la 8e semaine de vie (garçon en premier) : obstruction gastrique progressive avec vomissements en jet, déshydratation et alcalose métabolique hypochlorémique hypokaliémique.",
s:"Vomissements en jet, non bilieux, juste après les biberons, chez un nourrisson affamé qui réclame immédiatement après avoir vomi ; perte de poids, constipation, déshydratation ; parfois péristaltisme gastrique visible et olive pylorique palpable.",
dx:"Échographie abdominale (pylore épaissi, canal allongé) ; ionogramme : alcalose métabolique avec hypochlorémie et hypokaliémie (perte d'acide gastrique) ; gaz du sang.",
t:"Correction hydro-électrolytique d'abord (chlore, potassium) — elle conditionne l'opérabilité ; pylorotomie extramuqueuse (Ramstedt, cœlioscopie) curative ; sonde gastrique, réalimentation précoce post-opératoire.",
k:"Nourrisson de 2 à 8 semaines vomissant en jet non bilieux = sténose du pylore : échographie + ionogramme (alcalose hypochlorémique hypokaliémique) ; réhydrater avant d'opérer."}
,
{n:"Appendicite aiguë de l'enfant",q:"appendicite de l'enfant",ur:true,
d:"Inflammation de l'appendice de l'enfant : tableau souvent plus trompeur que chez l'adulte (diarrhée, localisation atypique), avec un risque de perforation plus élevé chez le petit enfant (un tiers des cas avant 5 ans).",
s:"Douleur péri-ombilicale migrant vers la fosse iliaque droite, fièvre modérée, vomissements, anorexie, arrêt du transit ; enfant immobile, boitant, qui tousse en se protégeant l'abdomen ; chez le petit : tableau d'occlusion ou de péritonite généralisée plus fréquent.",
dx:"Clinique (défense, signe du psoas) + NFS-CRP ; échographie (première intention en pédiatrie), scanner si doute ; β-hCG chez l'adolescente ; scores pédiatriques d'aide à la décision.",
t:"Appendicectomie cœlioscopique avec antibioprophylaxie ; formes compliquées (abcès, plastron) : antibiothérapie IV, drainage, appendicectomie différée ; à jeun, antalgiques, réhydratation.",
k:"Enfant qui marche penché ou refuse de sauter, avec fièvre et douleur abdominale = appendicite : imagerie et avis chirurgical — le risque de perforation est majeur avant 5 ans."}
]},
{name:"Malnutrition & Troubles Digestifs Chroniques",paths:[
{n:"Malnutrition Aiguë Sévère (MAS) : Kwashiorkor, Marasme et formes mixtes",q:"malnutrition de l'enfant",ur:true,
d:"Malnutrition aiguë sévère (poids/taille < -3 z-scores OMS et/ou œdèmes) : marasme (déficit calorique global, fonte musculaire), kwashiorkor (déficit protéique avec œdèmes), formes mixtes ; première cause de mortalité de l'enfant de moins de 5 ans dans les pays à faibles ressources.",
s:"Amaigrissement majeur (marasme) ou œdèmes des pieds et du visage, cheveux décolorés et ternes, lésions cutanées érythémato-squameuses en « flocons de peinture », apathie, anorexie, hépatomégalie (kwashiorkor) ; complications : hypoglycémie, hypothermie, infections graves, anémie, diarrhée, déshydratation.",
dx:"Anthropométrie : rapport poids/taille, périmètre brachial < 115 mm, présence d'œdèmes ; recherche des complications : glycémie, température, NFS, ionogramme, infection ; test de l'appétit (lait thérapeutique) pour orienter le niveau de prise en charge.",
t:"Protocole OMS de stabilisation (10 étapes) : prévenir et traiter l'hypoglycémie et l'hypothermie, antibiothérapie systématique, lait thérapeutique F-75, réalimentation prudente (éviter le syndrome de renutrition) ; phase de transition puis réhabilitation (F-100 ou aliments thérapeutiques prêts à l'emploi) ; dépistage et prise en charge communautaire si appétit conservé.",
k:"Œdèmes + apathie + cheveux décolorés = kwashiorkor ; réalimenter prudemment (F-75) : le syndrome de renutrition (hypokaliémie, hypophosphorémie) tue plus vite que la faim."}
,
{n:"Reflux gastro-œsophagien (RGO) physiologique et compliqué du nourrisson",q:"reflux gastro-œsophagien du nourrisson",
d:"RGO du nourrisson : régurgitations du nourrisson bien portant (physiologique, par immaturité du cardia), s'améliorant avec la diversification ; il devient pathologique en cas de retentissement (cassure pondérale, œsophagite, toux chronique, infections respiratoires récidivantes).",
s:"Régurgitations post-prandiales chez un nourrisson en bon état général (RGO simple) ; signes de complication : cassure de la courbe de poids, pleurs et refus alimentaires (œsophagite), anémie, toux nocturne, fausses routes, apnées.",
dx:"Clinique (dans l'immense majorité) ; pH-métrie ou endoscopie seulement dans les formes compliquées ou douteuses ; courbe de croissance ; éliminer une malformation sous-jacente si tableau atypique.",
t:"RGO simple : rassurer, épaissir les biberons ou ajuster les postures, fractionner les repas ; coucher sur le dos (jamais ventral : mort inattendue du nourrisson) ; formes compliquées : inhibiteur de la pompe à protons et avis spécialisé ; traiter une allergie aux protéines de lait de vache associée.",
k:"Les régurgitations d'un nourrisson qui grossit bien = RGO physiologique : rassurer, aucun examen ; une cassure pondérale ou des signes respiratoires font tout changer."}
,
{n:"Constipation chronique fonctionnelle et Mégacôlon congénital (maladie de Hirschsprung)",q:"maladie de Hirschsprung",ur:true,
d:"Constipation chronique de l'enfant : fonctionnelle dans l'immense majorité (rétention, alimentation, post-évictionnelle) ; la maladie de Hirschsprung (aganglionose congénitale du côlon terminal) se révèle dès la naissance par un retard d'émission du méconium et un mégacôlon obstructif.",
s:"Constipation fonctionnelle : selles dures et rares, épisodes d'encoprésie (débordement), douleurs abdominales, fissures anales ; Hirschsprung : absence d'émission de méconium dans les 48 premières heures de vie, distension abdominale, vomissements bilieux, et entérocolite aiguë (diarrhée fécale, choc — urgence).",
dx:"Constipation fonctionnelle : examen clinique (toucher rectal : réservoir plein), sans imagerie ; suspicion de Hirschsprung : radiographie (distension colique avec rectum vide), manométrie anorectale, biopsie rectale (absence de ganglions) ; lavement aux hydrosolubles (zone de transition).",
t:"Fonctionnelle : éducation à la toilette, laxatifs osmotiques (macrogol) au long cours, fibres et hydratation ; Hirschsprung : chirurgie (résection du segment aganglionnaire, parfois stomie temporaire) ; entérocolite aiguë : lavages coliques, antibiothérapie, réanimation.",
k:"Nouveau-né sans méconium à 48 heures + distension = Hirschsprung (biopsie rectale) ; l'entérocolite en est l'urgence vitale ; chez le grand enfant, la constipation est fonctionnelle : macrogol et éducation."}
,
{n:"Intolérance au gluten (Maladie cœliaque) et allergies aux protéines de lait de vache (APLV)",q:"maladie cœliaque de l'enfant",
d:"Maladie cœliaque : entéropathie auto-immune par intolérance permanente au gluten (blé, orge, seigle) chez l'enfant prédisposé (HLA-DQ2/DQ8) ; allergie aux protéines de lait de vache (APLV) : allergie alimentaire IgE-dépendante ou non, la plus fréquente du nourrisson.",
s:"Cœliaque : diarrhée chronique, distension abdominale, cassure de la courbe pondérale, asthénie, carence martiale résistante, irritabilité ; formes frustes de l'enfant plus grand (retard de taille, anémie, puberté retardée) ; APLV : vomissements, diarrhée ou constipation, coliques, eczéma, glairo-sang dans les selles du nourrisson.",
dx:"Cœliaque : anticorps anti-transglutaminase IgA (avec dosage des IgA totales) sous régime contenant du gluten, confirmation par biopsies duodénales ; APLV : test de provocation orale contrôlé, IgE spécifiques et tests cutanés selon la forme.",
t:"Cœliaque : régime sans gluten strict à vie, substitution et suivi des carences (fer, vitamine D, calcium), suivi diététique ; APLV : hydrolysats extensifs de protéines (ou régime d'exclusion chez la mère qui allaite), réintroduction différée après l'âge d'un an le plus souvent ; éducation à la lecture des étiquettes.",
k:"Diarrhée chronique + cassure pondérale + carence en fer résistante = maladie cœliaque : anti-transglutaminase sous régime normal ; l'APLV guérit le plus souvent avant 2 ans."}
]}
]},

{id:"ped-hemato",num:5,name:"Hématologie & Immunologie Pédiatrique",groups:[
{name:"Anémies & Hémoglobinopathies",paths:[
{n:"Drépanocytose pédiatrique (syndromes SS, SC : crises, séquestration splénique, syndrome thoracique aigu)",q:"drépanocytose de l'enfant",ur:true,
d:"Hémoglobinopathie homozygote SS ou hétérozygote composite SC révélée dès la première année (protection par l'hémoglobine F décroissante) : hémolyse chronique, crises vaso-occlusives et infections à germes encapsulés (asplénie fonctionnelle) ; dépistage néonatal en France.",
s:"Anémie et ictère chroniques, crises douloureuses osseuses ou abdominales dès 6 mois ; séquestration splénique du nourrisson (splénomégalie brutale + chute de l'hémoglobine = urgence) ; syndrome thoracique aigu (fièvre, douleur, hypoxémie) ; syndrome mains-pieds (dactylite) révélateur, AVC ischémique, infections à pneumocoque.",
dx:"Dépistage néonatal (électrophorèse) ; NFS réticulocytes, électrophorèse de l'hémoglobine ; en crise : hémocultures, radio/scanner thoracique, échodoppler transcrânien annuel (risque d'AVC) ; statut vaccinal et pénicilloprophylaxie.",
t:"Crise vaso-occlusive : hydratation, antalgiques par paliers, oxygène ; séquestration splénique : transfusion en urgence ; syndrome thoracique : oxygène, antibiotiques, transfusion ; fond : hydroxyurée dès 9-12 mois (réduit les crises), vaccinations complètes + pénicilline V prophylactique jusqu'à 5 ans, transfusions programmées (prévention de l'AVC) ; éducation des parents (fièvre = consultation immédiate).",
k:"Drépanocytaire fébrile = urgence : antibiothérapie parentérale après hémocultures (septicémie à pneumocoque) ; splénomégalie brutale + pâleur = séquestration, transfuser."}
,
{n:"Anémie ferriprive du nourrisson (carence martiale)",q:"anémie ferriprive de l'enfant",
d:"Carence en fer du nourrisson (6 mois à 2 ans) : prématurité, allaitement exclusif prolongé sans supplémentation, lait de vache trop tôt et en excès, alimentation pauvre en fer ; la plus fréquente des carences nutritionnelles de l'enfant.",
s:"Pâleur, asthénie, irritabilité, anorexie, stagnation pondérale, troubles de l'attention ; forme sévère : souffle systolique anémique, hypotrophie ; la pica (géophagie) est possible chez le grand enfant.",
dx:"NFS : anémie microcytaire hypochrome (VGM bas), réticulocytes normaux ou bas ; ferritine basse, coefficient de saturation de la transferrine abaissé ; pas d'endoscopies systématiques chez le nourrisson (enquête diététique d'abord).",
t:"Sel ferreux oral 3 mois (jusqu'à reconstitution des réserves), à distance des produits laitiers (qui freinent l'absorption) ; correction diététique : lait enrichi en fer, diversification avec aliments riches en fer (viandes, légumes verts) ; supplémentation systématique des prématurés et nourrissons allaités au-delà de 4-6 mois.",
k:"Anémie microcytaire du nourrisson entre 6 mois et 2 ans = carence martiale : fer oral et correction du régime ; l'excès de lait de vache en est la grande cause."}
,
{n:"Anémies hémolytiques auto-immunes et constitutionnelles de l'enfant",q:"anémie hémolytique de l'enfant",
d:"Hémolyses de l'enfant : constitutionnelles (sphérocytose héréditaire de Minkowski-Chauffard, déficit en G6PD, thalassémies) ou auto-immunes (anémie hémolytique auto-immune, souvent post-infectieuse : mycoplasme, EBV) ; l'hémolyse aiguë de l'enfant est une urgence.",
s:"Pâleur brutale, ictère, urines foncées, asthénie, fièvre, splénomégalie ; sphérocytose : ictère néonatal et antécédents familiaux ; G6PD : crise après médicament, fève ou infection ; AHAI : phase d'anémie profonde rapide.",
dx:"NFS avec réticulocytes élevés, LDH élevées, haptoglobine basse, bilirubine libre élevée ; test de Coombs direct (positif = AHAI) ; frottis (sphérocytes), dosage de G6PD à distance, électrophorèse de l'hémoglobine ; surveiller la tolérance (défaillance cardiaque si Hb très basse).",
t:"Transfusion si anémie mal tolérée (avec précautions immunologiques dans l'AHAI) ; AHAI : corticoïdes, immunoglobulines IV si résistance ; sphérocytose : acide folique, splénectomie différée après 6 ans si besoin ; G6PD : éviter les médicaments oxydants (liste écrite) ; supplémentation en folates.",
k:"Pâleur brutale + ictère + urines foncées = hémolyse aiguë : Coombs direct en urgence, transfuser si mauvaise tolérance ; dans le déficit en G6PD, la crise survient après un médicament oxydant."}
]},
{name:"Hémostase & Hémopathies",paths:[
{n:"Purpura Thrombopénique Immuno-allergique / Idiopathique (PTI) aigu de l'enfant",q:"purpura thrombopénique de l'enfant",ur:true,
d:"Thrombopénie autoimmune de l'enfant, souvent 1-2 semaines après une virose, sans autre anomalie de l'hémogramme ; forme aiguë bénigne de l'enfant (récupération spontanée dans 80 % des cas en moins de 6 mois), à distinguer des formes chroniques et des PTI secondaires.",
s:"Purpura pétéchial et ecchymotique d'apparition brutale chez un enfant par ailleurs en bon état général, sans fièvre ni hépato-splénomégalie (éléments de gravité à rechercher) ; épistaxis, gingivorragies possibles ; pas de saignement profond.",
dx:"NFS : thrombopénie isolée (parfois inférieure à 10 G/L), frottis normal, hémoglobine et leucocytes normaux ; myélogramme inutile dans la forme typique de l'enfant ; éliminer une leucémie (blastes), un syndrome hémolytique et urémique (schizocytes), une infection.",
t:"Enfant sans saignement muqueux majeur : abstention et surveillance (l'évolution spontanée est favorable) ; saignements abondants ou plaquettes très basses : corticoïdes ou immunoglobulines IV ; formes hémorragiques sévères : hospitalisation, transfusion plaquettaire réservée aux hémorragies menaçantes ; éviter les activités à risque de traumatisme ; contrôle à 6 mois (chronicisation).",
k:"Purpura brutale de l'enfant bien portant, sans fièvre ni splénomégalie = PTI aigu post-viral : NFS seule suffit ; l'évolution est spontanément favorable dans 80 % des cas."}
,
{n:"Hémophilie et maladies hémorragiques constitutionnelles de l'enfant",q:"hémophilie de l'enfant",
d:"Déficits héréditaires liés à l'X en facteur VIII (hémophilie A) ou IX (hémophilie B), exprimés chez le garçon (les filles conductrices) : hémorragies profondes spontanées ou post-traumatiques ; sévérité selon le taux de facteur.",
s:"Hémarthroses récidivantes (genou, coude, cheville) dès la marche, hématomes profonds, saignements prolongés après circoncision ou extraction, épistaxis ; hémorragies intracrâniennes rares mais graves ; l'arthropathie hémophilique détruit les articulations.",
dx:"TCA allongé avec TP normal ; dosage des facteurs VIII et IX ; antécédents familiaux (un tiers de néomutations) ; échographie articulaire des hémarthroses ; dépistage familial et conseil génétique.",
t:"Substitution en facteur (prophylaxie régulière dans les formes sévères : 2-3 injections par semaine ou émicizumab pour l'hémophilie A avec inhibiteur), traitement à la demande des épisodes ; acide tranexamique (muqueuses, extractions) ; contre-indication des intramusculaires et des AINS ; éducation : sport adapté, carte de maladie hémorragique ; suivi en centre de référence.",
k:"Hémarthrose spontanée du garçon = hémophilie : TCA allongé, facteur VIII ou IX bas ; éviter les intramusculaires, substituer précocement toute hémorragie."}
,
{n:"Leucémies aiguës (LAL, LAM) et lymphomes de l'enfant",q:"leucémie de l'enfant",ur:true,
d:"Premiers cancers de l'enfant : leucémie aiguë lymphoblastique (80 % des leucémies, pic entre 2 et 5 ans, forte curabilité — plus de 90 % de survie) et leucémies aiguës myéloblastiques ; lymphomes (Hodgkin, non hodgkinien de Burkitt) ; envahissement médullaire par des blastes.",
s:"Asthénie, pâleur (anémie), fièvre et infections (neutropénie), purpura et saignements (thrombopénie) ; douleurs osseuses (fémurs, rachis) révélatrices fréquentes, boiterie ; adénopathies, splénomégalie, syndrome tumoral (médiastinal : toux, dyspnée ; masse abdominale de Burkitt) ; chez le nourrisson : irritabilité, refus alimentaire.",
dx:"NFS et frottis (blastes) ; myélogramme avec immunophénotypage et cytogénétique ; bilan d'extension (PL, imagerie) ; LDH (masse tumorale) ; urée, ionogramme, uricémie (prévention du syndrome de lyse).",
t:"Prise en charge en hématologie pédiatrique : chimiothérapie par protocoles standardisés (LAL : corticoïdes, poly-chimiothérapie d'induction, consolidation, entretien sur 2-3 ans) ; prévention du syndrome de lyse (hyperhydratation, allopurinol) ; soins de support (transfusions, antibiothérapies, nutrition) ; greffe de moelle dans les rechutes ; recherche d'essais cliniques.",
k:"Enfant pâle, fébrile et purpurique avec douleurs osseuses = leucémie aiguë : NFS-frottis en urgence ; la LAL de l'enfant se guérit dans plus de 90 % des cas."}
]}
]},

{id:"ped-nephro",num:6,name:"Néphrologie, Urologie & Endocrinologie Pédiatrique",groups:[
{name:"Néphrologie & Urologie",paths:[
{n:"Infection urinaire de l'enfant et recherche de reflux vésico-urétéral",q:"infection urinaire de l'enfant",ur:true,
d:"Infection urinaire de l'enfant : fièvre isolée du nourrisson (pyélonéphrite aiguë) ou signes urinaires du grand enfant ; germe : E. coli ; toute PNA de l'enfant fait rechercher une uropathie sous-jacente (dysplasie, reflux vésico-urétéral).",
s:"Nourrisson : fièvre isolée, vomissements, stagnation pondérale, ictère, urines malodorantes ; grand enfant : brûlures mictionnelles, pollakiurie, douleur lombaire, fièvre, énurésie secondaire ; infections récidivantes",
dx:"Bandelette et ECBU avec antibiogramme (ponction vésicale ou collecte propre chez le nourrisson) ; échographie des voies urinaires à la recherche d'une dilatation (à faire pour toute première PNA) ; cystographie rétrograde si dilatation ou infections récidivantes (reflux vésico-urétéral).",
t:"Antibiothérapie adaptée (C3G IV ou orale selon l'âge et la tolérance, puis relais) ; traitement des uropathies (chirurgie du reflux sévère) ; prophylaxie antibactérienne au long cours dans les reflux importants ; hygiène mictionnelle, traitement de la constipation ; suivi tensionnel et rénal à long terme.",
k:"Fièvre isolée du nourrisson = ECBU systématique : la PNA de l'enfant impose une échographie ; fièvre + mauvaise prise pondérale + urines troubles = infection urinaire."}
,
{n:"Syndrome néphrotique pur de l'enfant (néphrose lipoïdique)",q:"syndrome néphrotique de l'enfant",ur:true,
d:"Syndrome néphrotique de l'enfant (90 % entre 1 et 10 ans) : le plus souvent une néphrose lipoïdique (lésions glomérulaires minimales) ; œdèmes et protéinurie massive ; bonne réponse aux corticoïdes dans la majorité des cas.",
s:"Œdèmes blancs et mous débutant au visage (paupières) le matin, ascite, prise de poids, parfois épanchements et douleurs abdominales ; protéinurie abondante ; complications : infections (pneumocoque), thromboses, hypovolémie ; le pur est sans hématurie ni HTA ni insuffisance rénale (sinon = impur).",
dx:"Protéinurie ≥ 50 mg/kg/j ou rapport protéines/créatinine élevé, hypoalbuminémie, hyperlipidémie ; BU (protéinurie 3+ ou 4+) ; NFS, ionogramme, créatinine, complément (normal dans la néphrose) ; biopsie réservée aux formes atypiques (hématurie, HTA, insuffisance rénale, âge < 1 an ou > 11 ans).",
t:"Régime hyposodé ; corticothérapie orale (prednisone 60 mg/m²) : réponse en 4 semaines dans 90 % des cas ; rechutes fréquentes (relais ou agents d'épargne : lévamisole, ciclosporine, mycophénolate) ; vaccinations (pneumocoque, varicelle) ; prophylaxie par pénicilline si œdèmes majeurs ; éviter les intramusculaires.",
k:"Œdèmes palpébraux du matin + protéinurie massive chez un enfant entre 1 et 10 ans = néphrose lipoïdique : corticoïdes, guérison habituelle ; le syndrome impur (hématurie, HTA, IRA) impose la biopsie."}
,
{n:"Glomérulonéphrite aiguë post-streptococcique (GNAPS)",q:"glomérulonéphrite post-streptococcique",
d:"Glomérulonéphrite aiguë immunitaire 10-21 jours après une angine ou un impétigo streptococcique de l'enfant (6-12 ans) : syndrome néphritique aigu, généralement résolutif en quelques semaines.",
s:"Hématurie macroscopique « bouillon sale » ou coca-cola, œdèmes du visage, HTA, oligurie, asthénie ; résolution spontanée dans la grande majorité (diurèse reprend, la tension se normalise, l'hématurie disparaît en semaines).",
dx:"Hématurie dysmorphique avec cylindres, protéinurie modérée ; créatinine, ionogramme, TA ; C3 abaissé (normalisation en 6-8 semaines) et ASLO élevés ; streptococcie de la gorge ou cutanée ; PAS de biopsie dans le tableau typique (réservée aux formes atypiques ou qui ne guérissent pas).",
t:"Repos, restriction hydrosodée, diurétiques si surcharge, antihypertenseurs (inhibiteurs calciques) ; éradication du foyer streptococcique (pénicilline) et dépistage des contacts ; surveillance de la diurèse, de la TA et de la créatinine jusqu'à normalisation ; pronostic excellent chez l'enfant.",
k:"Hématurie brune + œdèmes + HTA deux semaines après une angine = GNAPS : C3 bas et ASLO élevés ; guérison habituelle, pas de biopsie dans la forme typique."}
,
{n:"Malformations urogénitales congénitales (hydronéphrose, valves de l'urètre postérieur)",q:"hydronéphrose",
d:"Anomalies congénitales des voies urinaires découvertes en anténatal (échographie) ou après une infection urinaire : hydronéphrose par syndrome de la jonction pyélo-urétérale, reflux vésico-urétéral, valves de l'urètre postérieur (obstruction sous-vésicale du garçon — la plus grave).",
s:"Dilatation pyélocalicielle découverte en anténatal (échographie du 2e trimestre) ou postnatal ; valves de l'urètre postérieur : obstacle du nouveau-né garçon avec mauvais jet urinaire, distension vésicale, insuffisance rénale, détresse ; formes plus frustes : infections urinaires à répétition, retard de croissance, incontinence.",
dx:"Échographie anténatale et postnatale des reins et des voies urinaires ; échographie vésicale, urétrocystographie rétrograde (valves, reflux) ; scintigraphie rénale (fonction relative) ; créatinine et ionogramme (fonction néphronique).",
t:"Valves de l'urètre postérieur : drainage vésical (sondage) et résection endoscopique des valves en urgence néonatale ; hydronéphrose : surveillance échographique, chirurgie de la jonction si dégradation de la fonction ou dilatation majeure ; reflux : prophylaxie antibiotique puis traitement chirurgical des grades élevés ; suivi néphrologique à long terme (insuffisance rénale possible).",
k:"Hydronéphrose fœtale = suivi échographique anténatal et postnatal ; mauvais jet urinaire + vessie distendue du nouveau-né garçon = valves de l'urètre postérieur, drainage en urgence."}
]},
{name:"Endocrinologie & Croissance",paths:[
{n:"Diabète sucré de Type 1 de l'enfant (acidocétose inaugurale)",q:"diabète de type 1 de l'enfant",ur:true,
d:"Diabète de type 1 de l'enfant et de l'adolescent : destruction auto-immune des cellules bêta, insulinopénie absolue ; la révélation se fait souvent par une acidocétose (un quart des découvertes) ou un syndrome cardinal d'installation rapide.",
s:"Polyurie (revenir aux couches, lever nocturne), polydipsie, amaigrissement, asthénie, douleurs abdominales ; acidocétose : vomissements, dyspnée de Kussmaul, haleine acétonique, déshydratation, confusion, coma ; chez le nourrisson, l'installation est foudroyante et trompeuse.",
dx:"Glycémie ≥ 1,26 g/L (à jeun) ou ≥ 2 g/L avec symptômes ; cétonémie, gaz du sang, ionogramme (potassium) ; anticorps anti-GAD et anti-îlots ; en acidocétose : surveiller l'enfant (œdème cérébral, complication spécifique pédiatrique).",
t:"Acidocétose : réhydratation prudente (éviter l'œdème cérébral), insuline IVSE, apport de potassium, surveillance neurologique rapprochée ; ensuite insulinothérapie intensive à vie : basal-bolus ou pompe (± boucle fermée), éducation de l'enfant et des parents (autosurveillance, glucides, hypoglycémies) ; suivi pédiatrique multidisciplinaire ; école du diabète.",
k:"Polyuro-polydipsie + amaigrissement chez un enfant = glycémie immédiate ; dans l'acidocétose de l'enfant, la réhydratation prudente prévient l'œdème cérébral, complication propre à cet âge."}
,
{n:"Retard de croissance staturo-pondérale et nanismes endocriniens",q:"retard de croissance",
d:"Retard de croissance : cassure ou ralentissement de la courbe de taille ; causes : nutritionnelles et maladies chroniques (les plus fréquentes), endocriniennes (déficit en hormone de croissance, hypothyroïdie, hypercortisolisme, puberté retardée), génétiques (Turner, dyschondrostéose), constitutionnels (retard pubertaire familial, le plus banal).",
s:"Taille inférieure à -2 déviations standard ou croisant vers le bas plusieurs couloirs de la courbe ; poids et contexte orientent : maigreur (dénutrition, maladie chronique), surpoids (hypercortisolisme, hypothyroïdie) ; âge osseux, vitesse de croissance, antécédents familiaux.",
dx:"Courbes de croissance et vitesse de taille ; âge osseux (radiographie main-poignet) ; bilan de première intention : NFS, CRP, anticorps cœliaques, TSH, ionogramme, urée, créatinine, bilan martial, gaz du sang ; si orienté : IGF-1, tests de stimulation de la GH, caryotype (fille), IRM hypophysaire.",
t:"Traitement de la cause : renutrition, maladie chronique contrôlée, lévothyroxine, hormone de croissance biosynthétique dans les déficits confirmés (et Turner, insuffisance rénale) ; prise en charge psychologique de la taille et de la puberté ; le retard pubertaire constitutionnel rattrape sa croissance avec la puberté.",
k:"Toute cassure de la courbe de croissance = bilan : la courbe qui traverse plusieurs couloirs est plus alarmante qu'une taille stable, petite (retard constitutionnel familial)."}
,
{n:"Hypothyroïdie congénitale",q:"hypothyroïdie congénitale",
d:"Insuffisance thyroïdienne présente dès la naissance (ectopie thyroïdienne, agénésie, trouble de l'hormonosynthèse, carence iodée maternelle) : cause évitable de retard mental ; dépistage néonatal systématique (test de Guthrie à 3 jours).",
s:"Nouveau-né souvent asymptomatique les premiers jours (d'où l'importance du dépistage) : ictère prolongé, hypotonie, macroglossie, hernie ombilicale, constipation, hypothermie, cri rauque, somnolence, fontanelles larges ; non traité : retard mental et de croissance irréversibles (crétinisme).",
dx:"Dépistage néonatal systématique (TSH sur papier buvard) confirmé par TSH élevée et T4L basse ; scintigraphie et échographie (ectopie, agénésie) ; caryotype si contexte (trisomie 21 associée) ; enquête familiale.",
t:"Lévothyroxine dès les premiers jours de vie (le cerveau dépend de la thyroïde les 2-3 premières années) ; dose initiale élevée ; surveillance de la TSH et de la T4L rapprochée (objectif de T4L haute-normale) ; suivi neurodéveloppemental ; éducation : traitement à jeun, à vie.",
k:"Le dépistage néonatal de l'hypothyroïdie (Guthrie) permet un développement intellectuel normal si la lévothyroxine débute dans les 15 premiers jours."}
,
{n:"Puberté précoce et puberté retardée",q:"puberté précoce",
d:"Puberté précoce (fille avant 8 ans, garçon avant 9 ans) : centrale (activation prématuré de l'axe hypothalamo-hypophysaire, souvent idiopathique chez la fille, suspecter une lésion chez le garçon) ou périphérique (tumeur hormonale) ; puberté retardée (absence de développement après 13 ans chez la fille, 14 ans chez le garçon) : le plus souvent constitutionnelle/familiale.",
s:"Précoce : développement mammaire (fille) ou pilosité et testicules augmentés (garçon), accélération de la vitesse de croissance, avance d'âge osseux (risque de taille finale diminuée) ; retardée : absence de caractères sexuels, petite taille avec retard de l'âge osseux, retentissement psychologique.",
dx:"Évaluation clinique (stades de Tanner, courbe de croissance, âge osseux) ; hormonaux : LH, FSH, estradiol ou testostérone, test de stimulation GnRH ; échographie pelvienne (fille) ou testiculaire ; IRM hypophysaire (puberté centrale du garçon, ou fille avant 6 ans) ; bilan étiologique (hypothyroïdie, tumeurs, syndrome de McCune-Albright).",
t:"Puberté précoce centrale : agonistes de la GnRH (blocage pubertaire) pour préserver la taille finale, traitement de la cause (lésion) ; périphérique : traiter la tumeur ou l'hyperfonctionnement ; puberté retardée constitutionnelle : surveillance et réassurance, parfois induction brève par testostérone ou œstrogènes ; prise en charge psychologique.",
k:"Puberté précoce du garçon = IRM hypothalamo-hypophysaire à la recherche d'une lésion ; chez la fille, elle est le plus souvent idiopathique ; puberté retardée = le plus souvent constitutionnelle, surveiller la courbe."}
]}
]},

{id:"ped-neuro",num:7,name:"Neurologie Pédiatrique & Développement",groups:[
{name:"Urgences Neurologiques",paths:[
{n:"Convulsions hyperpyréctiques (fébriles) simples et complexes",q:"convulsions fébriles",
d:"Convulsions fébriles de l'enfant de 6 mois à 5 ans, sans infection du système nerveux central ni épilepsie sous-jacente : simples (généralisées, tonico-cloniques, moins de 15 minutes, sans récidive dans 24 h) ou complexes (focales, prolongées, récidivantes).",
s:"Convulsion généralisée tonico-clonique lors d'une fièvre, souvent au début de l'épisode fébrile, chez un enfant par ailleurs normal entre les crises ; l'examen neurologique post-critique redevient normal ; complexes : durée supérieure à 15 minutes, caractère focal, déficit transitoire post-critique.",
dx:"Diagnostic de l'épisode fébrile (otite, angine, virose) : la PL n'est indiquée que si l'enfant a moins de 12-18 mois avec examen douteux, ou si une méningite est suspectée ; glycémie ; pas d'EEG ni d'imagerie dans les formes simples.",
t:"Crise en cours : position latérale de sécurité, durée de la crise (si plus de 5 min : diazépam rectal ou midazolam buccal) ; antipyrétiques (paracétamol, découverture) ; réassurance parentale : les formes simples sont bénignes, le risque d'épilepsie n'est que légèrement augmenté ; récidives possibles (un tiers des cas).",
k:"Convulsion fébrile de l'enfant de 6 mois à 5 ans = bénigne dans sa forme simple : chercher la cause de la fièvre, pas d'EEG systématique ; l'examen neurologique doit être normal entre les crises."}
,
{n:"État de mal épileptique de l'enfant",q:"état de mal épileptique",ur:true,
d:"Crise épileptique de plus de 5 minutes (définition opérationnelle) ou crises répétées sans reprise de conscience ; urgence vitale : hypoxie cérébrale, défaillance ; causes de l'enfant : fièvre et infection (surtout avant 2 ans), épilepsie connue mal traitée, anomalie métabolique, intoxication.",
s:"Convulsion tonico-clonique prolongée ou répétitive sans reprise de conscience entre les crises ; l'état de mal non convulsif (confusion prolongée) est plus insidieux ; surveillance : voie aérienne, saturation, glycémie, hémodynamique.",
dx:"Glycémie capillaire immédiate ; ionogramme, calcémie, NFS, CRP, hémocultures, PL si fièvre ; traitement de la cause (infection, hyponatrémie, hypoglycémie) ; EEG en cas de coma inexpliqué ; imagerie si traumatisme ou déficit focal.",
t:"Protocole : benzodiazépine IV ou intra-muqueuse (midazolam, clonazépam, diazépam) à répéter une fois, puis deuxième ligne (phénobarbital ou phénytoïne/fosphénytoïne IV) si échec à 10 minutes, puis anesthésie générale au-delà de 30 minutes ; soins de support : libertés des voies aériennes, oxygène, prévention de l'hypoglycémie et de l'hyperthermie ; réanimation pédiatrique.",
k:"Convulsion de l'enfant de plus de 5 minutes = état de mal : benzodiazépine sans tarder, glycémie, et escalade thérapeutique programmée (2e ligne à 10 min, réanimation à 30 min)."}
,
{n:"Épilepsies de l'enfant (syndrome de West, absences, épilepsies généralisées)",q:"épilepsie de l'enfant",
d:"Épilepsies de l'enfant : syndromes âge-dépendants — spasmes infantiles de West (4-8 mois, hypsarythmie), épilepsie-absence de l'enfant (pic 6-7 ans), épilepsie myoclonique juvénile, épilepsies focales bénignes (rolandique), syndromes épileptiques graves (Lennox-Gastaut, Dravet).",
s:"West : spasmes en flexion en salves (réveil), régression psychomotrice, hypsarythmie à l'EEG ; absences : ruptures de contact brèves et fréquentes (plusieurs dizaines par jour), arrêt de l'activité, pas de chute, déclenchées par l'hyperventilation ; myoclonies du réveil (juvénile).",
dx:"EEG intercritique et critique (hypsarythmie dans le West, pointes-ondes bilatérales symétriques dans l'absence) ; vidéo-EEG ; IRM cérébrale dans les formes focales ou avec retard ; bilan métabolique et génétique des épilepsies graves.",
t:"Traitement antiépileptique adapté au syndrome : absences — éthosuximide ou acide valproïque (les carbamazépine et phénytoïne les aggravent) ; myocloniques — valproate, lévétiracétam ; West — corticoïdes et vigabatrine (surtout si sclérose tubéreuse) ; éducation de la famille (observance, conduite à tenir en crise, autorisations) ; les absences guérissent souvent à l'adolescence.",
k:"Ruptures de contact brèves et répétées chez l'écolier = absences : hyperventilation provoquante, EEG, éthosuximide ou valproate — jamais de carbamazépine."}
]},
{name:"Développement & Pathologies Neurologiques",paths:[
{n:"Retard psychomoteur et troubles du neurodéveloppement (troubles du spectre de l'autisme - TSA)",q:"troubles du spectre de l'autisme",
d:"Retard psychomoteur : atteinte de l'acquisition des étapes motrices ou cognitives (se tenir assis, marcher, parler) ; troubles du spectre de l'autisme : trouble du neurodéveloppement caractérisé par des difficultés de communication et d'interaction sociale et des comportements restreints et stéréotypés ; causes : génétiques (trisomie 21, X fragile), métaboliques, infectieuses (CMV), hypoxiques, idiopathiques.",
s:"Retard des acquisitions constaté sur les étapes (ne tient pas sa tête à 4 mois, ne marche pas à 18 mois, pas de mots à 2 ans) ; TSA : absence de pointage et de regard conjoint, indifférence aux autres, intérêts restreints, stéréotypies, intolérance aux changements, troubles sensoriels ; régression des acquisitions = signal d'alarme.",
dx:"Évaluation du développement (échelles) ; bilan étiologique : caryotype et génétique, métabolisme (phénylcétonurie dépistée), IRM cérébrale, audiogramme et examen ophtalmologique systématiques ; diagnostic TSA sur critères (DSM-5, ADOS) ; recherche des comorbidités (épilepsie, troubles digestifs).",
t:"Prise en charge précoce et intensive : orthophonie, psychomotricité, éducation structurée (ABA, TEACCH), intégration scolaire adaptée (accompagnement) ; information et soutien des parents ; traitement des comorbidités (épilepsie, troubles du sommeil) ; pas de traitement curatif de l'autisme lui-même, méfiance envers les approches non validées.",
k:"Un enfant qui ne dit pas de mots à 2 ans ou perd ses acquisitions = évaluation développementale : audition d'abord, puis bilan neurodéveloppemental ; l'intervention précoce conditionne le pronostic."}
,
{n:"Infirmité Moteur Cérébrale (IMC) / Paralysie cérébrale",q:"paralysie cérébrale de l'enfant",
d:"Trouble moteur permanent (non progressif) secondaire à une lésion cérébrale précoce (prématurité, asphyxie périnatale, infection, ictère nucléaire) : atteintes pyramidales et extrapyramidales, uni- ou bilatérales ; les fonctions cognitives peuvent être préservées (IMC).",
s:"Retard des acquisitions motrices, hypertonie spastique (hémiplégie, diplégie — prématuré —, quadriplégie), marches anormales (sur la pointe des pieds), dystonies, dyskinésies ; complications orthopédiques (luxation de hanche, scoliose, pieds bots), épilepsie associée, troubles de la déglutition et du langage, douleurs.",
dx:"Examen neurologique et suivi du développement ; IRM cérébrale (lésions de la prématurité, séquelles anoxiques) ; évaluation multidimensionnelle : motrice (GMFCS), déglutition, langage, cognition, vision, audition ; recherche de la cause.",
t:"Rééducation précoce et continue (kinésithérapie, orthophonie, ergothérapie) ; spasticité : toxine botulique, plâtres, mobilisation, parfois chirurgie orthopédique (transferts tendineux, ostéotomies) et rhizotomie dorsale ; appareillages et aides techniques (marche, déplacement) ; prise en charge multidisciplinaire et soutien familial ; scolarité adaptée.",
k:"Toute hypertonie ou asymétrie motrice du nourrisson = paralysie cérébrale à explorer (IRM) : la lésion est fixe mais la prise en charge précoce change la trajectoire fonctionnelle."}
,
{n:"Hydrocéphalie congénitale et acquise (hypertension intracrânienne)",q:"hydrocéphalie de l'enfant",ur:true,
d:"Dilatation ventriculaire par trouble de la circulation ou de la résorption du liquide cephalorachidien : congénitale (sténose de l'aqueduc, spina bifida, toxoplasmose) ou acquise (hémorragie, méningite, tumeur) ; l'hypertension intracrânienne de l'enfant menace la vue et la conscience.",
s:"Chez le nourrisson : augmentation rapide du périmètre crânien (courbe qui déborde), fontanelles bombées et tendues, veines du scalp dilatées, regard en coucher de soleil, vomissements, irritabilité ou somnolence ; grand enfant : céphalées matinales, vomissements en jet, troubles visuels, œdème papillaire, troubles de la marche.",
dx:"Périmètre crânien répété (courbe) ; échographie transfontanellaire (nourrisson), TDM ou IRM cérébrale ; fond d'œil (œdème papillaire) ; recherche de la cause (tumeur du cervelet et tronc dans les formes acquises de l'enfant).",
t:"Dérivation du LCR (chirurgie) : valve ventriculo-péritonéale ou ventriculo-cisternostomie (3e ventriculocisternostomie) ; traitement de la cause (tumeur) ; mesures d'urgence de l'hypertension intracrânienne ; surveillance à vie des valves (dysfonctionnement, infections) ; suivi du développement.",
k:"Courbe du périmètre crânien qui déborde + fontanelle bombée = hydrocéphalie : imagerie en urgence ; céphalée matinale avec vomissements en jet chez l'enfant = hypertension intracrânienne, chercher la tumeur."}
,
{n:"Troubles des apprentissages (dyslexie, dyspraxie, TDAH)",q:"troubles des apprentissages",
d:"Troubles spécifiques des apprentissages : dyslexie (lecture), dysorthographie (orthographe), dyscalculie, dyspraxie (coordination et gestes), dysphasie (langage oral) ; TDAH : trouble du déficit de l'attention avec ou sans hyperactivité, d'origine neurodéveloppementale.",
s:"Dyslexie : lenteur et erreurs de lecture malgré une intelligence normale, refus du travail écrit, installation d'un échec scolaire avec retentissement émotionnel ; dyspraxie : maladresse, écriture illisible, difficultés en géométrie et sport ; TDAH : inattention, impulsivité, hyperactivité, fonctionnement en « pile ou face », épuisement scolaire.",
dx:"Bilan pluriprofessionnel : psychométrie (WISC), bilan orthophonique (dyslexie-dysphasie), psychomoteur (dyspraxie), ophtalmologique et auditif (à éliminer) ; critères DSM-5 pour le TDAH (questionnaires parents-enseignants) ; aucun examen biologique systématique.",
t:"Rééducations ciblées (orthophonie, psychomotricité), aménagements scolaires (PAI, PAP, tiers temps, ordinateur) ; TDAH : approches psychothérapiques et parentales d'abord, méthylphénidate (forme à action prolongée) dans les formes invalidantes avec surveillance de la croissance et de l'appétit ; valorisation des points forts.",
k:"Échec scolaire chez un enfant vif et curieux = dyslexie ou TDAH jusqu'à preuve du contraire : bilan pluriprofessionnel, jamais de jugement paresseux hâtif."}
]}
]},

{id:"ped-cardio",num:8,name:"Cardiologie Pédiatrique & Rhumatologie",groups:[
{name:"Cardiopathies",paths:[
{n:"Cardiopathies congénitales cyanogènes (tétralogie de Fallot, transposition des gros vaisseaux)",q:"tétralogie de Fallot",ur:true,
d:"Cardiopathies congénitales avec shunt droite-gauche et cyanose : tétralogie de Fallot (sténose pulmonaire + CIV + déviation de l'aorte + hypertrophie droite, la plus fréquente des cyanogènes), transposition des gros vaisseaux (aorte et artère pulmonaire inversées), atrésie pulmonaire.",
s:"Cyanose centrale (lèvres, extrémités, conjonctives) permanente ou aux pleurs ou à la tétée, hypoxémies sévères (« malaises anoxiques » du Fallot : accroupissement soulage), dyspnée d'effort, polycythémie secondaire, hippocratisme digital, souffle éjectionnel (Fallot) ; retard de croissance.",
dx:"Saturation en oxygène basse ; radiographie (cœur « en sabot » du Fallot, médiastin étroit de la transposition), ECG, échocardiographie (diagnostic) ; angio-IRM ; diagnostic prénatal en échographie.",
t:"Nouveau-né cyanogène : prostaglandine E1 IV pour maintenir le canal artériel ouvert (transposition, atrésies) en attendant la chirurgie ; transposition : switch artériel dans les premiers jours ; Fallot : chirurgie réparatrice complète dans les premiers mois (ou anastomose palliative) ; malaise anoxique : position genoux-poitrine, bêtabloquant, oxygène ; prévention de l'endocardite.",
k:"Nouveau-né cyanosé = échocardiographie urgente et prostaglandine E1 pour maintenir le canal artériel ouvert ; le malaise anoxique du Fallot est soulagé par l'accroupissement (position genoux-poitrine)."}
,
{n:"Cardiopathies congénitales non cyanogènes (CIV, CIA, canal artériel persistant)",q:"communication interventriculaire",
d:"Cardiopathies congénitales avec shunt gauche-droite (hyperdébit pulmonaire sans cyanose) : communication interventriculaire (CIV, la plus fréquente), communication interauriculaire (CIA), canal artériel persistant (prématuré, rubéole) ; les larges shunts entraînent une insuffisance cardiaque et une hypertension pulmonaire.",
s:"Souffle holosystolique gauche (CIV), souffle continu (canal artériel), souffle systolique pulmonaire (CIA) ; petites CIV : souffle intense paradoxalement (très limité), enfant asymptomatique ; larges shunts : dyspnée, sueurs des biberons, cassure pondérale, infections respiratoires ; hypertension pulmonaire d'Eisenmenger si tardive (shunt inversé, cyanose).",
dx:"Échocardiographie (siège, taille, retentissement) ; ECG, radiographie ; cathétérisme si pression artérielle pulmonaire à évaluer ; surveillance de la croissance et de la tolérance.",
t:"Petits shunts : surveillance spontanée (fermeture de la CIV dans une grande partie des cas) ; shunts larges : traitement médical de l'insuffisance cardiaque (diurétiques, IEC) et chirurgie (fermeture de la CIV ou de la CIA, ligature ou prothèse du canal) avant l'installation de l'hypertension pulmonaire ; CIA et canal : fermeture percutanée possible ; prévention de l'endocardite.",
k:"Shunt gauche-droit large = opérer avant l'hypertension pulmonaire fixée (syndrome d'Eisenmenger : contre-indication à la fermeture) ; petit shunt = surveillance, fermeture souvent spontanée."}
,
{n:"Rhumatisme Articulaire Aigu (RAA) et cardite rhumatismale",q:"rhumatisme articulaire aigu",ur:true,
d:"Complication post-streptococcique (streptocoque du groupe A) autoimmune de l'enfant de 5 à 15 ans, 2-3 semaines après une angine non traitée : arthrite migratrice, cardite (la gravité : valvulopathies), chorée, nodule et érythème marginé ; principale cause de valvulopathie dans les pays à faibles ressources.",
s:"Critères de Jones : arthralgies inflammatoires des grosses articulations migratrices, fièvre ; cardite : souffle (insuffisance mitrale ou aortique), tachycardie, insuffisance cardiaque ; chorée de Sydenham (mouvements anormaux), nodules sous-cutanés, érythème marginé ; récidives cardiaques (vulnérabilité).",
dx:"Preuves d'une infection streptococcique (ASLO, anti-DNase B, prélèvement de gorge) ; syndrome inflammatoire (VS, CRP) ; ECG (allongement du PR), échocardiographie (valvulopathie) ; critères de Jones révisés.",
t:"Repos au lit ; pénicilline (éradication) puis benzathine-pénicilline G IM toutes les 3-4 semaines jusqu'à l'âge adulte (prophylaxie des récidives) ; anti-inflammatoires (aspirine forte dose, corticoïdes si cardite sévère) ; traitement de l'insuffisance cardiaque ; suivi cardiologique à vie (valvulopathies) ; traitement des angines streptococciques = prévention.",
k:"Arthrite migratrice + souffle cardiaque chez l'enfant après une angine = RAA (Jones) : prophylaxie par benzathine-pénicilline des années durant — l'angine streptococcique de l'enfant doit être traitée (TDR puis amoxicilline)."}
,
{n:"Myocardites et péricardites aiguës de l'enfant",q:"myocardite de l'enfant",ur:true,
d:"Inflammation du myocarde (virale le plus souvent : entérovirus, parvovirus, adénovirus) ou du péricarde de l'enfant : l'insuffisance cardiaque aiguë sur cœur sain et la myocardite fulminante sont des urgences ; le péricardite s'accompagne d'un épanchement parfois abondant.",
s:"Myocardite : infection virale récente puis dyspnée, tachycardie, vomissements, douleur abdominale, fatigue, choc cardiogénique ; péricardite : douleur thoracique soulagée penché en avant, frottement, dyspnée, fièvre ; tamponnade : turgescence jugulaire, hépatomégalie, pouls paradoxal.",
dx:"Troponine élevée, ECG (troubles diffus, microvoltage), échocardiographie (dysfonction, épanchement) ; NFS-CRP, PCR virales ; IRM cardiaque ; explorations du liquide péricardique si tamponnade ; diagnostics différentiels : cardiomyopathie, Kawasaki.",
t:"Hospitalisation avec monitorage ; insuffisance cardiaque : diurétiques, inotropes, soins intensifs (forme fulminante : assistance, ECMO) ; péricardite : AINS + colchicine ; tamponnade : péricardocentèse ; arrêt du sport 3-6 mois ; suivi de la récupération de la fonction cardiaque.",
k:"Enfant avec infection virale puis défaillance cardiaque = myocardite : échocardiographie et troponine, soins intensifs — l'évolution peut être fulminante."}
]},
{name:"Rhumatologie & Orthopédie Pédiatrique",paths:[
{n:"Arthrite Idiopathique Juvénile (AIJ)",q:"arthrite juvénile idiopathique",
d:"Arthrite inflammatoire chronique de début avant 16 ans, évoluant plus de 6 semaines, de cause inconnue ; formes : oligoarticulaire (la plus fréquente, petite fille, risque d'uvéite), polyarticulaire, systémique (maladie de Still : fièvre évanescente, éruption, polyarthrite), enthésite-related (adolescent HLA-B27), psoriasique.",
s:"Arthrite (gonflement, douleur, raideur matinale) de plus de 6 semaines ; boiterie, refus de marcher, raideur au réveil ; forme systémique : fièvre hectique biphasique avec éruption salmonée aux pics, hépatosplénomégalie, polyadénopathie, anémie ; l'uvéite antérieure est silencieuse (dépistage obligatoire).",
dx:"Clinique (nombre d'articulations, extra-articulaire) ; NFS, CRP, VS, facteurs rhumatoïdes et ACPA, ANA (uvéite des oligoarthrites) ; ponction articulaire si articulation unique (éliminer une infection) ; imagerie ; dépistage de l'uvéite par examen ophtalmologique répété (lampe à fente).",
t:"Anti-inflammatoires (AINS) et corticoïdes intra-articulaires ou systémiques (forme systémique) ; méthotrexate en première intention de fond ; biothérapies (anti-IL-1 ou anti-IL-6 dans la forme systémique, anti-TNF) ; kinésithérapie précoce ; dépistage de l'uvéite (examens ophtalmologiques répétés) ; prévention de des déformations.",
k:"Arthrite de plus de 6 semaines avant 16 ans = AIJ ; l'uvéite antérieure est silencieuse et destructive : dépistage ophtalmologique systématique et répété."}
,
{n:"Ostéomyélite aiguë et arthrite septique de l'enfant",q:"ostéomyélite de l'enfant",ur:true,
d:"Infection osseuse (ostéomyélite aiguë, staphylocoque doré en tête) ou articulaire (arthrite septique) de l'enfant : hématogène, touchant les métaphyses des os longs (fémur, tibia, humérus) ; risque de séquelles (épiphysiodèse, destruction articulaire) si le diagnostic tarde.",
s:"Douleur osseuse fébrile avec boiterie ou refus de marcher ou de mobiliser le membre, douleur exquise à la palpation métaphysaire, sans rougeur au début (profonde) ; arthrite septique : articulation chaude, gonflée, extrêmement douloureuse (hanche : position en flexion, attitude vicieuse) ; nourrisson : fièvre isolée, irritabilité, pseudo-paralysie.",
dx:"NFS-CRP-procalcitonine, hémocultures ; ponction articulaire en urgence avant les antibiotiques (arthrite septique) ; imagerie : radiographie normale au début, échographie (épanchement, abcès sous-périosté), IRM (examen de référence) ; scintigraphie parfois.",
t:"Antibiothérapie IV probabiliste après prélèvements (anti-staphylococcique : oxacilline ou C1G, ± amoxicilline chez le petit) puis relais oral prolongé (3-6 semaines ostéomyélite, 2-3 semaines arthrite) ; arthrite septique : drainage chirurgical ou ponctions-lavages en urgence (hanche = chirurgie) ; immobilisation, antalgiques.",
k:"Enfant fébrile qui refuse de marcher ou boite = ostéomyélite ou arthrite septique : CRP, IRM et prélèvements avant l'antibiothérapie ; la hanche septique se draine chirurgicalement en urgence."}
,
{n:"Dysplasie Développementale de la Hanche (DDH) et Pieds Bots Varus Équins (PBVE)",q:"dysplasie de la hanche",
d:"Dysplasie développementale de la hanche : instabilité ou luxation de la hanche du nouveau-né et nourrisson (terrain : fille, siège, oligoamnios, antécédents familiaux) ; pied bot varus équin (PBVE) : déformation congénitale du pied (varus équin adductus), décelable dès la naissance.",
s:"DDH : limitation de l'abduction, pli fessier asymétrique, signe du ressaut (Barlow, Ortolani) chez le nouveau-né, boiterie ou marche en équilibre tardive ; PBVE : pied déformé non réductible (varus, équin, creux), le pied talus est au contraire réductible et bénin.",
dx:"DDH : examen systématique à la naissance et aux consultations du 1er mois ; échographie de hanche (avant 4 mois) puis radiographie ; dépistage ciblé des nouveau-nés à risque ; PBVE : examen clinique à la naissance, radiographie au besoin.",
t:"DDH : harnais de Pavlik (avant 3-6 mois) si instabilité, puis réduction et plâtre sous traction ou chirurgie si échec ; PBVE : méthode fonctionnelle (kinésithérapie) et surtout manipulations-plâtres successifs (méthode de Ponseti), ténotomie du tendon d'Achille souvent nécessaire, chaussures d'entretien ; prise en charge orthopédique spécialisée dès la maternité.",
k:"Examen des hanches à chaque consultation du nourrisson (abduction limitée, pli asymétrique) : le harnais de Pavlik dans les premiers mois évite la chirurgie ; le pied bot se traite par la méthode de Ponseti dès la naissance."}
]}
]}
]});


/* ============================================================
   DÉPARTEMENT 3 — GYNÉCOLOGIE-OBSTÉTRIQUE (5 spécialités)
   ============================================================ */
DEPTS.push({
id:"gyn",name:"Gynécologie-Obstétrique",icon:"🤰",color:"#ec4899",
desc:"Urgences maternelles vitales, suivi des grossesses à haut risque, gynécologie médicale et endocrinienne, pathologies tumorales et planification familiale : la prise en charge de la femme de la puberté à la ménopause.",
specs:[

{id:"gyn-urg",num:1,name:"Urgences Obstétricales & Maternelles Vitales",groups:[
{name:"Hémorragies de la Grossesse & du Post-Partum",paths:[
{n:"Hémorragie de la Délivrance (HPD) et atonie utérine",q:"hémorragie du post-partum",ur:true,
d:"Saignement génital de plus de 500 mL après l'accouchement (voie basse) ou 1000 mL (césarienne) : première cause de mortalité maternelle évitable ; cause principale : atonie utérine (75 %), puis plaies du tractus génital, rétention placentaire et troubles de la coagulation.",
s:"Saignement abondant immédiat ou différé du post-partum, utérus mou et mal rétracté (atone) ou au contraire dur (déchirure), état de choc hémorragique (pâleur, tachycardie, hypotension) ; les 4 causes à passer en revue : tonus (atone), tissu (rétention), traumatisme (plaies), thrombine (coagulation).",
dx:"Clinique : évaluation quantitative des pertes, toucher pelvien et examen sous valves (plaies), révision utérine (rétention), bilan de coagulation (fibrinogène), groupe-RAI ; la mesure est répétable (sacs gradués).",
t:"Prise en charge protocolaire immédiate : massage utérin, ocytocine IV (puis sulprostone/carbétocine si atonie), vidange vésicale, révision utérine et sutures des plaies ; remplissage et transfusion (fibrinogène) précoces ; échec : tamponnement intra-utérin (ballon), ligatures vasculaires, radiologie interventionnelle, hysterectomie d'hémostase en dernier recours.",
k:"Hémorragie du post-partum = protocole d'urgence : ocytocine d'emblée, et ne jamais laisser s'installer le choc (transfuser tôt, fibrinogène) ; l'hystérectomie d'hémostase est le sauvetage ultime."}
,
{n:"Placenta prævia",q:"placenta praevia",ur:true,
d:"Insertion du placenta sur le segment inférieur de l'utérus, recouvrant partiellement ou totalement le col (prævia recouvrant) : cause classique d'hémorragie du 3e trimestre, par segment inférieur mal vascularisé et peu contractile ; terrain : utérus cicatriciel, multiparité.",
s:"Hémorragie génitale indolore, rouge vif, survenant au repos au 3e trimestre, récidivante et de plus en plus abondante ; utérus souple, présent souvent haut ou transverse ; le saignement cède souvent spontanément puis récidide.",
dx:"Échographie obstétricale (localisation placentaire — voie sus-pubienne, endovaginale si doute ; prævia recouvrant, partiel, marginal) ; MAP associée à surveiller ; pas de toucher vaginal intempestif ; IRM si placenta accreta suspecté (antécédent de césarienne + prævia).",
t:"Hospitalisation si hémorragie ou prævia recouvrant ; tocolyse prudente si nécessaire, corticothérapie pour la maturation pulmonaire ; éviter tout toucher vaginal ; césarienne programmée (recouvrant) avant terme ; accouchement voie basse possible pour les praevia marginaux selon les protocoles ; préparer la césarienne hémorragique (placenta accreta : cellule de garde).",
k:"Hémorragie indolore rouge vif au 3e trimestre = placenta prævia : échographie, jamais de toucher vaginal, hospitalisation ; prævia + césarienne antérieure = suspecter placenta accreta."}
,
{n:"Hématome Rétro-Placentaire (HRP) / Décollement prématuré du placenta normalement inséré",q:"décollement placentaire",ur:true,
d:"Décollement aigu du placenta normalement inséré avant la naissance, formant un hématome rétro-placentaire : urgence materno-fœtale (souffrance fœtale aiguë, mort fœtale in utero, coagulation intravasculaire disséminée) ; terrain : HTA et pré-éclampsie, tabac, traumatisme.",
s:"Douleur utérine brutale en « coup de poignard », utérus dur et douloureux en « bois », contractions en spasme continu, hémorragie extériorisée de sang noir non coagulable ou inapparente (forme cachée) ; souffrance fœtale aiguë ou mort fœtale ; choc maternel parfois disproportionné aux pertes ; CIVD dans les formes graves.",
dx:"Clinique + monitoring fœtal (bradycardie, anomalies du rythme) ; échographie (hématome rétro-placentaire, mais souvent normale) ; bilan de coagulation et fibrinogène (CIVD), NFS ; diagnostic avant tout clinique.",
t:"Extraction fœtale en urgence (césarienne la plus souvent ; voie basse si mort fœtale et accouchement rapide possible) ; réanimation maternelle : remplissage, produits sanguins (fibrinogène, plasma), traitement de la CIVD ; surveillance post-partum (récidive, insuffisance rénale, CIVD) ; aucune tocolyse.",
k:"Utérus dur en bois + douleur brutale + souffrance fœtale = HRP : extraction en urgence, la CIVD guette (fibrinogène effondré)."}
,
{n:"Rupture utérine (sur utérus cicatriciel ou sain)",q:"rupture utérine",ur:true,
d:"Déchirure de la paroi utérine, le plus souvent sur utérus cicatriciel (césarienne antérieure, myomectomie) pendant le travail, rarement spontanée sur utérus sain ; urgence materno-fœtale absolue.",
s:"Pendant le travail : douleur brutale sus-symphysaire, perte des contractions, disparition des bruits du cœur fœtal, régression de la présentation, hémorragie génitale et choc ; signes prémonitoires sur cicatrice : douleur fixée sus-symphysaire, utérus douloureux, saignement ; hématurie si lésion vésicale.",
dx:"Clinique devant tout tableau algique et/ou anomalie du rythme cardiaque fœtal sur utérus cicatriciel pendant le travail ; exploration utérine systématique après accouchement sur cicatrice ; NFS, bilan de coagulation, groupe ; pas d'imagerie : la laparotomie est diagnostique et thérapeutique.",
t:"Laparotomie en urgence : réparation de la rupture ou hystérectomie (déchirure étendue, hémorragie non contrôlée) ; réanimation (remplissage, transfusion) ; extraction fœtale immédiate ; césarienne systématique pour les grossesses ultérieures ; prévention : surveillance rapprochée des essais de voie basse sur cicatrice.",
k:"Toute anomalie du rythme fœtal + douleur brutale pendant un travail sur utérus cicatriciel = rupture utérine : laparotomie immédiate, sans imagerie."}
,
{n:"Hémopéritoine sur Grossesse Extra-Utérine (GEU) rompue",q:"grossesse extra-utérine",ur:true,
d:"Grossesse extra-utérine (GEU) : implantation hors de la cavité utérine (trompe dans 95 % des cas) ; la rupture tubaire avec hémopéritoine est l'urgence chirurgicale classique de la femme en âge de procréer avec douleur pelvienne et retard de règles.",
s:"Retard de règles ou aménorrhée + douleur pelvienne latéralisée brutale + métrorragies noirâtres ; rupture : douleur violente avec irradiation scapulaire, malaise ou syncope, défense, choc hémorragique ; épaule droite douloureuse (irritation phrénique par le sang).",
dx:"β-hCG plasmatiques positifs avec échographie pelvienne (utérus vide, masse latéro-utérine, épanchement du Douglas) ; taux de β-hCG et progestérone ; NFS, groupe-RAI ; culdocentèse historique ; en urgence absolue, la clinique suffit à opérer.",
t:"Rupture = chirurgie urgente (cœlioscopie ou laparotomie) : salpingectomie le plus souvent, réanimation transfusionnelle ; GEU non rompue : méthotrexate si critères (β-hCG bas, absence de battement cardiaque, taille limitée, absence de rupture) ou cœlioscopie conservatrice (salpingotomie) ; surveillance des β-hCG jusqu'à négativation ; prévention : dépistage et traitement des salpingites.",
k:"Toute femme en âge de procréer avec douleur pelvienne et retard de règles = β-hCG immédiat : l'hémopéritoine de GEU rompue peut tuer en quelques heures."}
,
{n:"Embolie amniotique",q:"embolie amniotique",ur:true,
d:"Passage brutal de liquide amniotique dans la circulation maternelle (travail, césarienne, post-partum immédiat) : réaction anaphylactoïde et obstruction vasculaire pulmonaire catastrophique — cause rare mais de mortalité maternelle très élevée ; imprévisible et non prévenable.",
s:"Pendant le travail ou juste après : détresse respiratoire aiguë et cyanose, collapsus, arrêt cardiaque, convulsions puis coma ; saignement massif par coagulation intravasculaire disséminée dans un second temps ; les survivantes aux premières minutes présentent une CIVD majeure.",
dx:"Diagnostic de confrontation en urgence (accouchement récent + collapsus + hypoxie) ; gaz du sang, ECG, échographie (cœur pulmonaire aigu) ; la présence de cellules amniotiques dans le sang (ancien critère) n'est plus indispensable ; rien ne doit retarder la réanimation.",
t:"Réanimation immédiate : oxygénation, remplissage et catécholamines, réanimation cardiopulmonaire si arrêt, accouchement immédiat si survie maternelle au cours du travail ; prise en charge de la CIVD (plasma, plaquettes, fibrinogène, acide tranexamique) ; soins intensifs multidisciplinaires (réanimateur, obstétricien, anesthésiste).",
k:"Collapsus brutal avec hypoxie pendant le travail ou le post-partum immédiat = embolie amniotique : réanimation, extraction fœtale, et anticipation de la CIVD."}
]},
{name:"Pathologies Hypertensives Graves de la Grossesse",paths:[
{n:"Pré-éclampsie sévère et Éclampsie (crises convulsives)",q:"pré-éclampsie",ur:true,
d:"HTA gravidique (après 20 SA) avec protéinurie : dysfonction endothéliale placentaire ; forme sévère (PA ≥ 160/110, protéinurie massive, signes biologiques ou neurologiques) et éclampsie : crise convulsive ou coma, complication grave pour la mère (HELLP, HRP, CIVD, insuffisance rénale) et le fœtus (RCIU, MFIU).",
s:"Œdèmes, céphalées, phosphènes, acouphènes, bar épigastrique ou douleur de l'hypochondre droit (signes de menace) ; HTA et protéinurie ; éclampsie : crise convulsive tonico-clonique, le plus souvent au 3e trimestre ou en post-partum ; signes de gravité : oligurie, hématémèse, confusion.",
dx:"PA répétées, protéinurie (BU puis RPC), NFS-plaquettes (HELLP), ASAT-ALAT, LDH, créatinine, uricémie, bilan de coagulation ; monitoring fœtal, Doppler ombilical et cérébral, croissance ; protéinurie et bilan d'organes répétés.",
t:"Hospitalisation, repos, contrôle tensionnel (nicardipine IV, labétalol, nicardipine per os) ; sulfate de magnesium IV (prévention et traitement de l'éclampsie) ; corticothérapie de maturation si avant 34 SA ; la seule issue : l'extraction fœtale (césarienne ou déclenchement selon terme et gravité) ; surveillance post-partum (48-72 h : régression, puis normalisation) ; aspirine à faible dose en prévention chez les femmes à risque.",
k:"Céphalées + phosphènes + barre épigastrique chez une femme enceinte hypertendue = pré-éclampsie sévère : sulfate de magnésium et extraction fœtale — le seul traitement curatif est la naissance."}
,
{n:"Syndrome HELLP (Hemolysis, Elevated Liver enzymes, Low Platelet count)",q:"syndrome HELLP",ur:true,
d:"Complication de la pré-éclampsie associant hémolyse (H), cytolyse hépatique (EL : Elevated Liver enzymes) et thrombopénie (LP : Low Platelets) ; forme grave, parfois sans HTA manifeste ; risque maternel (hématome sous-capsulaire du foie, CIVD, éclampsie) et fœtal.",
s:"Douleur de l'hypochondre droit ou épigastrique, nausées, vomissements, céphalées, œdèmes, HTA et protéinurie inconstantes ; ictère rare ; les signes de pré-éclampsie peuvent manquer (HELLP « pur »), d'où la biologie systématique.",
dx:"NFS-plaquettes (moins de 100 G/L), LDH et hémolyse (schizocytes, haptoglobine basse), ASAT-ALAT élevées, bilirubine, bilan de coagulation, créatinine, uricémie ; bilan fœtal (RCIU, Dopplers).",
t:"Hospitalisation en urgence, bilan de coagulation répété ; corticoïdes pour la maturation pulmonaire si avant 34 SA (la dexaméthasone a aussi un effet sur le HELLP) ; extraction fœtale sans délai dans les formes symptomatiques ou avant 34 SA ; surveillance post-partum avec correction biologique lente (48-72 h) ; examens complémentaires si évolution anormale (hématome sous-capsulaire : scanner, échographie).",
k:"Barre épigastrique ou hypochondre droit + thrombopénie chez une femme enceinte ou du post-partum = HELLP : extraire le fœtus, surveiller le foie et la coagulation."}
,
{n:"Encéphalopathie hypertensive gravidique et HDP surajoutée",q:"hypertension gravidique",
d:"Encéphalopathie hypertensive de la femme enceinte (HTA maligne avec céphalées, troubles visuels, convulsions) : urgence thérapeutique ; HTA chronique de la grossesse : HTA connue avant la grossesse ou découverte avant 20 SA, avec risque de pré-éclampsie surajoutée ; l'HTA gestationnelle (après 20 SA, sans protéinurie) disparaît en post-partum.",
s:"PA très élevée (supérieure à 160/110) avec céphalées intenses, phosphènes, vision floue, vomissements, obnubilation, voire convulsions ; œdème papillaire au fond d'œil ; l'HTA chronique s'aggrave souvent au 2e-3e trimestre (surajout de protéinurie = pré-éclampsie surajoutée).",
dx:"PA aux deux bras et en MAPA, protéinurie, fond d'œil, bilan de pré-éclampsie complet (NFS, plaquettes, ASAT-ALAT, LDH, créatinine) ; éliminer les causes secondaires chez la nullipare jeune (reins, rénine-aldostérone, toxiques) ; bilan fœtal.",
t:"Encéphalopathie : baisse contrôlée de la PA IV (nicardipine, labétalol), sulfate de magnésium si signes neurologiques ; HTA chronique : poursuivre ou adapter le traitement (labétalol, inhibiteurs calciques, méthildopa ; arrêt des IEC/ARA2 tératogènes) ; aspirine préventive ; surveillance rapprochée du fœtus ; l'extraction s'impose en cas de pré-éclampsie surajoutée.",
k:"Les IEC et ARA2 sont contre-indiqués pendant la grossesse (tératogènes) : labétalol, inhibiteurs calciques ou méthildopa ; toute HTA connue avant 20 SA = HTA chronique, surveiller la survenue d'une pré-éclampsie surajoutée."}
]},
{name:"Infections & Sepsis Sévères",paths:[
{n:"Choc septique post-abortum (avortement compliqué / provoqué)",q:"avortement infecté",ur:true,
d:"Infection génitale haute après un avortement spontané ou provoqué (surtout manœuvres non médicalisées) : endométrite et sepsis pelvien avec risque de choc septique, de péritonite et de CIVD ; grande cause de mortalité maternelle là où l'avortement est dangereux.",
s:"Fièvre élevée avec frissons, douleurs pelvienne et abdominale, métrorragies fétides, utérus gros, mou et douloureux, lochies nauséabondes ; choc septique : marbrures, hypotension, oligurie, confusion ; péritonite et abcès pelviens possibles.",
dx:"NFS-CRP-procalcitonine, hémocultures, prélèvements vaginaux et endométriaux ; échographie pelvienne (rétention, abcès, perforation) ; radiographie ou TDM (corps étranger, perforation, gaz) ; bilan de coagulation.",
t:"Antibiothérapie IV probabiliste large et rapide (C3G + métronidazole ± gentamicine) ; évacuation utérine de toute rétention (aspiration, révision) — le contrôle de la source est vital ; réanimation du choc (remplissage, catécholamines) ; chirurgie si perforation, péritonite ou abcès ; surveillance en soins intensifs.",
k:"Fièvre + lochies fétides + utérus douloureux après un avortement = sepsis post-abortum : antibiotiques et évacuation utérine, l'un sans l'autre est insuffisant."}
,
{n:"Endométrite aiguë du post-partum et choc septique puerpéral",q:"endométrite du post-partum",ur:true,
d:"Infection de l'endomètre dans les suites de couches (2e-10e jour) : fièvre puerpérale, première cause d'infection du post-partum, surtout après césarienne ; complication : abcès pelvien, thrombophlébite pelvienne, sepsis grave.",
s:"Fièvre (supérieure à 38,5 °C) en plateau avec lochies troubles ou fétides, utérus involutif et douloureux, métrorragies ; douleurs pelviennes ; signes de gravité : hypotension, tachycardie, confusion, douleur latéro-utérine (thrombophlébite pelvienne).",
dx:"NFS-CRP, hémocultures, prélèvements vaginaux et endométriaux ; échographie pelvienne (rétention placentaire, abcès) ; éliminer les autres sources de fièvre du post-partum (mastite, infection urinaire, angine, thrombose) ; recherche de thrombophlébite (échodoppler) si douleur latéralisée.",
t:"Antibiothérapie IV probabiliste (amoxicilline-acide clavulanique + gentamicine, ou C3G + métronidazole selon protocoles) 48-72 h puis relais oral ; évacuation d'une rétention utérine ; anticoagulation curative si thrombophlébite pelvienne ; drainage des abcès ; soins de support du sepsis.",
k:"Fièvre après J2 du post-partum avec utérus douloureux et lochies fétides = endométrite : antibiotiques IV, et penser à la thrombophlébite pelvienne si douleur latéralisée fébrile."}
,
{n:"Fasciite nécrosante périnéale (gangrène de Fournier post-partum / post-césarienne)",q:"gangrène de Fournier",ur:true,
d:"Infection nécrosante rapide des fascias et du tissu sous-cutané périnéo-scrotal (ou de la paroi post-césarienne) : synergies microbiennes (aérobies et anaérobies, streptocoque A, E. coli) ; urgence chirurgicale et dermatologique avec mortalité élevée.",
s:"Douleur périnéale ou pariétale intense disproportionnée aux signes cutanés (débuts : érythème, œdème, crépitation gazeuse), puis placard violacé, bulles, nécrose et fasciite extensive, fièvre élevée et choc septique ; porte d'entrée : épisiotomie infectée, plaie opératoire, abcès.",
dx:"Clinique (douleur disproportionnée + signes généraux) ; syndrome inflammatoire majeur, gaz des tissus sur radiographie/scanner ; bactériologies des prélèvements per-opératoires ; score LRINEC d'aide ; pas de retard chirurgical pour imager.",
t:"Chirurgie de sauvetage immédiate : excision large de tous les tissus nécrosés (réinterventions itératives) ; antibiothérapie IV à large spectre (C3G + métronidazole ± pénicilline, adaptée aux prélèvements) ; réanimation du choc ; oxygénothérapie hyperbare discutée ; soins de plaies et reconstruction secondaire (greffes).",
k:"Douleur périnéale ou pariétale post-opératoire disproportionnée, avec fièvre et œdème = fasciite nécrosante : bloc opératoire immédiat, l'excision large est le seul traitement."}
]}
]},

{id:"gyn-gross",num:2,name:"Pathologies de la Grossesse & Suivi Obstétrical (Grossesses à Haut Risque)",groups:[
{name:"Complications de la Dynamique & de la Statique Fœtale",paths:[
{n:"Menace d'Accouchement Prématuré (MAP) et rupture prématurée des membranes (RPM)",q:"menace d'accouchement prématuré",ur:true,
d:"MAP : contractions utérines avant 37 SA avec col modifié ; RPM : perte de liquide amniotique avant le travail (chorioamniotite si infection : le risque principal) ; la prématurité reste la première cause de morbidité néonatale.",
s:"MAP : contractions utérines régulières douloureuses ou non, pesanteur pelvienne, modification du col (examen ou échographie du col) ; RPM : écoulement liquidien vulvaire de liquide clair, parfois limpide continu ; chorioamniotite : fièvre maternelle, liquide ou lochies fétides, tachycardie fœtale et maternelle.",
dx:"Contractions au tocomètre, échographie du col (longueur < 25 mm) ; diagnostic de la RPM : examen au speculum (écoulement du cul-de-sac), test à l'insuline-like growth factor ou à la diamine-oxydase, échographie (oligoamnios) ; éviter tout toucher ; NFS-CRP, prélèvements, monitoring fœtal.",
t:"Hospitalisation, repos, tocolyse (nicardipine ou atosiban — 48 h pour le transfert et la corticothérapie) ; corticothérapie de maturation pulmonaire (bétaméthasone) avant 34 SA ; MgSO4 pour la neuroprotection avant 32 SA ; RPM à terme : déclenchement ; avant terme : surveillance infectieuse et antibiothérapie (prolongation de la grossesse si pas d'infection) ; antibiothérapie de la RPM pour prolonger la grossesse.",
k:"MAP avant 34 SA = corticoïdes + tocolyse 48 h (le temps de maturation et de transfert en maternité adaptée) ; fièvre maternelle sur RPM = chorioamniotite = extraire."}
,
{n:"Souffrance Fœtale Aiguë (SFA) per-partum (anomalies du rythme cardiaque fœtal - RCF)",q:"souffrance fœtale aiguë",ur:true,
d:"Hypoxie fœtale aiguë pendant le travail, détectée sur le rythme cardiaque fœtal (RCF) : anomalies (ralentissements précoces, tardifs, variables sévères, tachycardie, perte de la variabilité) ; l'objectif est d'extraire avant l'acidose et l'encéphalopathie.",
s:"Anomalies du RCF au monitoring : ralentissements tardifs (hypoxie), répétitifs et prolongés, tachycardie basale, perte de la variabilité, rythme sinusoïdal (anémie fœtale) ; liquide amniotique teinté (méconium) ; causes : hypercinésie, hypotension maternelle, HRP, cordons (circulaire serré, procidence), utérus hypercontractile.",
dx:"Analyse du RCF (classification) et de sa réactivité ; pH au scalp en cas de doute ; causes maternelles à corriger (hypotension péri-durale, décubitus, Hypercinésie) ; évaluation globale : RCF + liquide + progression du travail.",
t:"Mesures immédiates : arrêt des ocytociques, changement de position maternelle, oxygène, remplissage, tocolyse de sauvetage si hypercinésie ; si anomalies sévères persistantes : extraction en urgence (césarienne ou instrumental selon la progression) ; réanimation néonatale préparée ; discuter les causes avant le terme suivant.",
k:"Ralentissements tardifs répétés ou perte de variabilité du RCF = SFA : corriger les causes maternelles et extraire sans délai si persistance — l'objectif est d'éviter l'encéphalopathie anoxique."}
,
{n:"Dystocies dynamiques (anomalies de la contraction) et mécaniques (disproportion foeto-pelvienne)",q:"dystocie",ur:true,
d:"Dystocie = difficulté mécanique de l'accouchement : dynamique (contractions insuffisantes ou incoordonnées, le plus souvent) ou mécanique (disproportion foeto-pelvienne : fœtus trop gros, bassin rétréci, présentation défléchie ou postérieure).",
s:"Travail qui ne progresse pas : dilatation stationnaire (arrêt de dilatation), absence de descente de la présentation, contractions anarchiques ou insuffisantes ; présentation haute et mobile, bosse de cuir chevelu importante, circumduction des contractions (utérus en retrait) ; risque de rupture utérine et de SFA.",
dx:"Partogramme (dilatation et descente dans le temps) ; évaluation de la contraction (tocographie interne) ; appréciation du bassin (mesures cliniques, pelvimétrie selon protocoles) ; échographie du poids fœtal estimé ; monitoring fœtal permanent.",
t:"Dynamique : amniotomie, ocytocine adaptée sous monitorage, réanimation maternelle (analgésie, hydratation) ; mécanique : césarienne en cas de disproportion vraie ou présentation non engagée à dilatation complète ; extraction instrumentale si mécanique modérée et descente acquise ; anticipation : césarienne programmée pour macrosomie ou bassin limité.",
k:"Un travail qui n'avance plus = partogramme : rechercher dynamique (ocytocine) ou mécanique (césarienne) ; l'ocytocine ne corrige pas une disproportion."}
,
{n:"Présentations dystociques (siège, transversale, front, face)",q:"présentation du siège",
d:"Présentations non céphaliques ou mal fléchies à terme : siège (décomplété, complet, bas siège), transversale (épaule), front, face (présentation faciale antérieure ou postérieure) ; risque de dystocie mécanique, de procidence du cordon et de traumatisme néonatal.",
s:"Présentation sentie latérale ou haute au toucher, hauteur utérine atypique, fœtus position transversale palpable ; le diagnostic est fait par le toucher vaginal et l'échographie en début de travail ; procidence du cordon : cordon senti au toucher avec anomalie du RCF = urgence absolue.",
dx:"Toucher vaginal (identification des présentations) ; échographie (type de siège, déflexion, estimation pondérale) ; radiopelvimétrie discutée pour l'épreuve de voie basse du siège ; monitoring fœtal.",
t:"Siège à terme : césarienne programmée dans la majorité des cas (protocoles, épreuve de voie basse possible selon critères : siège complet ou décomplété, estimation pondérale normale, bassin favorable) ; transversale et front : césarienne ; face postérieure : césarienne ; version par manœuvre externe proposée avant 37 SA ; procidence du cordon : extraction immédiate.",
k:"Présentation transversale, front ou face postérieure = césarienne ; le siège se discute selon les critères (poids estimé, type de siège, bassin) ; procidence du cordon = urgence d'extraction."}
,
{n:"Retard de Croissance Intra-Utérin (RCIU) et hypotrophie fœtale",q:"retard de croissance intra-utérin",
d:"RCIU : fœtus dont la croissance est inférieure à son potentiel (le plus souvent < 3e ou 10e percentile avec anomalie de la vélocité) par insuffisance placentaire (RCIU « asymétrique » tardif), anomalie chromosomique ou infectieuse (RCIU « symétrique » précoce) ; l'hypotrophie à la naissance expose à l'hypoglycémie et à la détresse.",
s:"Hauteur utérine inférieure à l'âge gestationnel (courbe), diminution des mouvements actifs fœtaux (signe d'alerte) ; risque de souffrance fœtale chronique, de MFIU, d'oligoamnios ; RCIU précoce symétrique : chercher anomalie congénitale ou infection (toxoplasmose, CMV).",
dx:"Échographie obstétricale répétée (croissance, biométrie, estimée pondérale) ; Dopplers ombilicaux (résistances élevées, anomalies), cérébraux ( redistribution — épargne cérébrale) et veineux ; rythme cardiaque fœtal ; bilan étiologique : sérologies, caryotype, recherche de pré-éclampsie, tabac.",
t:"Surveillance pluridisciplinaire : Dopplers et RCF répétés, évaluation de la vitalité ; arrêt du tabac, correction des causes maternelles (HTA, dénutrition) ; déclenchement ou césarienne quand le bénéfice extra-utérin dépasse le risque intra-utérin (Dopplers pathologiques, terme atteint) ; corticothérapie avant 34 SA ; surveillance néonatale de l'hypoglycémie et de l'hypothermie.",
k:"Diminution des mouvements actifs fœtaux ou hauteur utérine trop petite = échographie + Doppler : un RCIU avec Doppler ombilical pathologique est un fœtus à surveiller de près, l'extraction se décide sur la balance des risques."}
,
{n:"Macrosomie fœtale et dystocie des épaules",q:"dystocie des épaules",ur:true,
d:"Macrosomie : poids fœtal estimé supérieur au 90e percentile (plus de 4 kg à terme ; supérieur à 4,5 kg = risque majeur), souvent sur diabète gestationnel ; la dystocie des épaules est sa complication redoutée : dégagement des épaules impossible après la naissance de la tête (épaule postérieure bloquée sur le promontoire).",
s:"Macrosomie : hauteur utérine supérieure à l'âge gestationnel, hydramnios possible, diabète maternel ; dystocie des épaules : après la naissance de la tête, rétraction de la tête (signe de la tortue), absence d'engagement des épaules, temps de dégagement prolongé — urgence néonatale (hypoxie, lésions du plexus brachial).",
dx:"Estimation pondérale échographique (marge d'erreur importante) ; recherche de diabète gestationnel (HGPO) ; la dystocie des épaules est un diagnostic per-partum, clinique.",
t:"Dystocie des épaules : appel à l'aide, manœuvre de MacRoberts (flexion des cuisses sur l'abdomen maternel) + supra-pubienne (pression sur l'épaule antérieure), épisiotomie déjà faite ou à élargir, manœuvre de Woods ou de Jacquemier si échec (rotation des épaules, extraction de l'épaule postérieure) ; casser la clavicule en dernier recours ; réanimation néonatale ; macrosomie confirmée chez la diabétique : césarienne programmée selon seuils ; prévention du diabète gestationnel.",
k:"Tête née + signe de la tortue = dystocie des épaules : MacRoberts + pression sus-pubienne, aider sans tirer sur la tête (plexus brachial) ; macrosomie du diabétique = césarienne discutée au-delà de 4,25-4,5 kg."}
]},
{name:"Infections Gravidiques & Médicales",paths:[
{n:"Pyélonéphrite aiguë de la femme enceinte",q:"pyélonéphrite de la femme enceinte",ur:true,
d:"Infection haute des voies urinaires de la femme enceinte (E. coli le plus souvent), favorisée par la dilatation urinaire gravidique et la stase : risque d'accouchement prématuré et de sepsis ; toute infection urinaire de la femme enceinte est grave.",
s:"Fièvre élevée avec frissons, douleur lombaire unilatérale, vomissements, contractions utérines (menace d'accouchement prématuré) ; formes graves : sepsis, déshydratation ; l'infection urinaire basse asymptomatique (bactériurie) dépistée mensuellement.",
dx:"ECBU avec antibiogramme et hémocultures ; NFS-CRP, ionogramme, créatinine ; monitoring des contractions et du RCF ; échographie urinaire si suspicion d'obstacle (dilatation, lithiase).",
t:"Hospitalisation : antibiothérapie IV (C3G), adaptée à l'antibiogramme puis relais oral 10-14 jours ; hydratation, antipyrétiques (paracétamol) ; tocolyse si contractions avant 37 SA ; surveillance fœtale ; traiter la bactériurie asymptomatique dépistée (risque de pyélonéphrite et de prématurité).",
k:"Fièvre + douleur lombaire chez une femme enceinte = pyélonéphrite : hospitalisation et C3G IV ; dépister et traiter toute bactériurie asymptomatique de la grossesse."}
,
{n:"Paludisme gravidique (accès simple et grave chez la femme enceinte)",q:"paludisme de la femme enceinte",ur:true,
d:"Paludisme chez la femme enceinte en zone d'endémie (P. falciparum) : gravité accrue (anémie, hypoglycémie, œdème pulmonaire) et retentissement fœtal (avortement, prématurité, hypotrophie, mort fœtale) ; le placenta est un site de séquestration parasitaire.",
s:"Fièvre, céphalées, courbatures, parfois anémie profonde et détresse ; chez la femme enceinte, l'accès peut être apyrétique ou trompeur (fièvre et anémie, hypoglycémie) ; accès grave : troubles de conscience, convulsions (à distinguer de l'éclampsie), détresse respiratoire, collapsus.",
dx:"TDR et goutte épaisse (parasitémie) ; NFS (anémie), plaquettes, glycémie, créatinine ; distinguer du paludisme et de l'éclampsie devant des convulsions (les deux peuvent coexister) ; RCF et croissance fœtale.",
t:"Accès simple : artéméther-luméfantrine oral (ou quinine selon terme et protocoles) ; accès grave : artésunate IV, soins de support (transfusion, correction de l'hypoglycémie) ; surveillance fœtale ; prévention : moustiquaires imprégnées et traitement préventif intermittent (TPI) aux visites prénatales en zone d'endémie.",
k:"Fièvre chez une femme enceinte en zone d'endémie = goutte épaisse immédiate : le paludisme gravidique est plus grave pour la mère (anémie, hypoglycémie) et le fœtus (prématurité, hypotrophie)."}
,
{n:"Infections congénitales et du premier trimestre (Toxoplasmose, Rubéole, Cytomégalovirus, Herpès, Syphilis)",q:"infections congénitales",ur:true,
d:"Infections pouvant traverser le placenta et atteindre le fœtus : toxoplasmose (rare en France, risque élevé de transmission au 3e trimestre mais sévérité maximale en début de grossesse), rubéole (éradication par la vaccination), cytomégalovirus (CMV — la plus fréquente des infections congénitales), syphilis, herpès, varicelle, Zika et VIH (PTME).",
s:"Souvent infections maternelles pauci-symptomatiques (syndrome pseudo-grippal, éruption) ; atteinte fœtale : RCIU, anomalies échographiques (dilatation ventriculaire, calcifications intracrâniennes, hépatomégalie, épanchements), éruption pétéchiale à la naissance ; surdité et retard mental (CMV, toxoplasmose).",
dx:"Sérologies maternelles (toxoplasmose et rubéole obligatoires et mensuelles chez les femmes non immunes ; syphilis au premier examen) ; en cas de séroconversion : PCR amniotique (amniocentèse à partir de 18 SA et 4 semaines après la contamination), échographies fœtales spécialisées ; PCR CMV dans les urines ou la salive du nouveau-né.",
t:"Toxoplasmose : spiramycine (prévention de la transmission) puis pyriméthamine-sulfadiazine (traitement fœtus atteint) ; syphilis : benzylpénicilline G (traitement maternel et fœtal) ; herpès : aciclovir et césarienne si lésions en travail ; CMV : pas de traitement validé en anténatal (valaciclovir dans certains protocoles), suivi audiométrique du nouveau-né ; prévention : hygiène (toxoplasmose), vaccination ROR avant la grossesse, consignes CMV (crèches).",
k:"Femme enceinte non immune de la toxoplasmose = sérologie mensuelle et règles hygiéno-diététiques (viande bien cuite, légumes lavés, chats) ; séroconversion = amniocentèse à 18 SA et 4 semaines, puis traitement adapté."}
,
{n:"Diabète gestationnel et HTA chronique de la grossesse",q:"diabète gestationnel",
d:"Diabète gestationnel : intolérance au glucose découverte pendant la grossesse (2e-3e trimestre), favorisée par l'obésité, les antécédents familiaux, l'âge maternel ; risques : macrosomie, dystocie des épaules, hypoglycémie néonatale, pré-éclampsie, diabète de type 2 ultérieur ; HTA chronique : connue avant la grossesse ou découverte avant 20 SA (voir fiche Urgences obstétricales).",
s:"Le plus souvent asymptomatique (dépistage systématique entre 24 et 28 SA chez les femmes à risque) ; signes d'appel rares : polyurie-polydipsie ; macrosomie fœtale, hydramnios ; HTA chronique : chiffres élevés dès le début, fond d'œil et retentissement rénal.",
dx:"Hyperglycémie provoquée par voie orale 75 g (HGPO) : glycémie à jeun supérieure à 0,92 g/L, ou à 1 h supérieure à 1,80 g/L, ou à 2 h supérieure à 1,53 g/L ; auto-surveillance glycémique ; suivi fœtal (croissance, hydramnios).",
t:"Diététique et activité physique d'abord ; insuline si les glycémies restent hors cibles (la metformine est parfois utilisée selon protocoles) ; surveillance fœtale, déclenchement ou césarienne selon poids estimé ; dépistage de l'hypoglycémie néonatale ; suivi post-partum : HGPO à 4-12 semaines (risque de diabète de type 2), allaitement, perte de poids.",
k:"Macrosomie + hydramnios = diabète gestationnel méconnu ; l'objectif glycémique strict (jeûne < 0,95 g/L, post-prandiale < 1,20 g/L) prévient la macrosomie et la dystocie des épaules."}
,
{n:"Hyperémèse gravidique avec retentissement métabolique",q:"hyperémèse gravidique",ur:true,
d:"Vomissements gravidiques incoercibles au-delà du 1er trimestre (le plus souvent 6-10 SA), avec déshydratation, perte de poids supérieure à 5 % et troubles métaboliques (acidose, hypokaliémie) ; parfois isolée ou en rapport avec une grossesse molaire ou multiple.",
s:"Nausées et vomissements permanents, intolérance alimentaire, perte de poids, déshydratation (soif, pli cutané, oligurie), asthénie ; signes de gravité : ictère, confusion, hémorragies (déficit en B1 : encéphalopathie de Gayet-Wernicke si vomissements prolongés).",
dx:"Ionogramme (hypokaliémie, acidose), urée-créatinine, NFS, bilan hépatique (cytolyse modérée), β-hCG élevées (môle ?) ; échographie obstétricale (grossesse molaire, gémellaire) ; cétonurie et cétonémie.",
t:"Réhydratation IV avec potassium, antiémétiques (dompéridone, métoclopramide, ondansétron si besoin, selon protocoles) ; thiamine (vitamine B1) avant toute perfusion glucosée ; reprise alimentaire fractionnée ; formes sévères : hospitalisation, nutrition parentérale ou entérale exceptionnellement ; l'interruption de grossesse reste exceptionnelle.",
k:"Vomissements de la grossesse + perte de poids supérieure à 5 % ou hypokaliémie = hyperémèse : réhydrater, et toujours donner de la vitamine B1 avant le glucose (prévention de l'encéphalopathie de Gayet-Wernicke)."}
]}
]},

{id:"gyn-med",num:3,name:"Gynécologie Médicale & Endocrine",groups:[
{name:"Troubles du Cycle & Pathologies Hormonales",paths:[
{n:"Aménorrhées primaires et secondaires",q:"aménorrhée",
d:"Absence de menstruations : primaire (pas de ménarche à 15 ans ou à 13 ans sans caractères sexuels secondaires) ou secondaire (arrêt des règles de plus de 3 mois chez une femme antérieurement réglée, non enceinte ni ménopausée) ; la première cause de l'aménorrhée secondaire reste la grossesse.",
s:"Primaire : impubérisme ou développement des caractères sexuels sans règles (obstacle utéro-vaginal : imperforation hyménéale, vagin ; syndrome de Rokitansky ; syndrome de Turner) ; secondaire : grossesse, syndrome des ovaires polykystiques, hyperprolactinémie (galactorrhée), insuffisance ovarienne prématurée (bouffées de chaleur), aménorrhée hypothalamique (perte de poids, sport intensif, stress).",
dx:"β-hCG systématique ; bilan hormonal : FSH, LH, estradiol, prolactine, TSH ; échographie pelvienne (utérus, ovaires) ; caryotype si aménorrhée primaire avec FSH élevée (Turner) ; test aux progestatifs ; IRM hypophysaire si prolactine élevée ou céphalées.",
t:"Traitement de la cause : hyperprolactinémie (agonistes dopaminergiques), SOPK (régularisation, insulinosensibilisation, traitement de l'infertilité), insuffisance ovarienne (traitement hormonal substitutif jusqu'à l'âge de la ménopause), obstacles (chirurgie), aménorrhée hypothalamique (reprise pondérale) ; prévention de l'ostéoporose si hypoestrogénie prolongée.",
k:"Toute aménorrhée secondaire = β-hCG d'abord ; puis le couple FSH-estradiol oriente : FSH élevée = origine ovarienne, FSH basse = origine centrale (hypothalamo-hypophysaire)."}
,
{n:"Hémorragies utérines dysfonctionnelles (ménorragies, métrorragies)",q:"ménorragies",ur:true,
d:"Saignements utérins anormaux chez une femme non enceinte, sans cause organique décelable (dysfonctionnels : cycles sans ovulation, terrain péri-ménopausique) ; les ménorragies abondantes exposent à l'anémie ferriprive ; chez la femme après 40 ans, toute métrorragie impose d'éliminer un cancer de l'endomètre.",
s:"Ménorragies : règles abondantes ou prolongées (plus de 7 jours), caillots, anémie ; métrorragies : saignements en dehors des règles, post-coïtaux (orienter vers le col) ou post-ménopausiques (orienter vers l'endomètre) ; cycle irrégulier, dysménorrhées.",
dx:"β-hCG ; NFS et ferritine ; échographie pelvienne (fibrome, polype, épaississement de l'endomètre) ; examen au speculum (col, IST) ; biopsie d'endomètre ou hystéroscopie si femme après 40-45 ans, post-ménopausique ou échographie anormale ; bilan de coagulation chez l'adolescente.",
t:"Aigu : acide tranexamique, progestatifs ou œstrogènes selon l'intensité, correction d'une anémie (fer, transfusion si nécessaire) ; fond : progestatifs en 2e phase ou dispositif intra-utérin au lévonorgestrel (réduction majeure des ménorragies), pilule œstroprogestative ; traitement des causes organiques découvertes (polype, fibrome) ; dilatation-curetage ou ablation endométriale dans les formes rebelles.",
k:"Métrorragie post-ménopausique ou après 45 ans = évaluation de l'endomètre (échographie puis biopsie) : ne jamais traiter sans éliminer un cancer de l'endomètre."}
,
{n:"Syndrome des Ovaires PolyKystiques (SOPK)",q:"syndrome des ovaires polykystiques",
d:"Trouble endocrinien le plus fréquent de la femme en âge de procréer (critères de Rotterdam — 2 sur 3 : oligo-anovulation, hyperandrogénie clinique ou biologique, aspect échographique) ; insulinorésistance et syndrome métabolique associés ; risque de diabète, d'infertilité et d'hyperplasie endométriale.",
s:"Spanioménorrhée ou aménorrhée, hirsutisme (visage, seins, ligne blanche), acné, alopécie androgénique, surpoids ; infertilité par anovulation ; présence éventuelle d'acanthosis nigricans (insulinorésistance) ; troubles thymiques associés.",
dx:"Éliminer les autres causes d'hyperandrogénie (hyperplasie congénitale des surrénales : 17-OH progestérone, hyperprolactinémie, tumeurs : tableau sévère d'installation rapide) ; testostérone et SDHEA ; échographie (ovaires multifolliculaires) ; bilan métabolique : glycémie, HGPO, lipides, tour de taille.",
t:"Mesures hygiéno-diététiques (perte de poids rétablit souvent l'ovulation) ; contraception œstroprogestative antiandrogénique (cyprotérone, drospirénone) si pas de désir de grossesse ; désir de grossesse : induction de l'ovulation (letrozole ou clomifène, puis gonadotrophines, chirurgie ovarienne en échec) ; metformine si insulinorésistance ; prévention de l'hyperplasie endométriale (progestatifs réguliers) ; dépistage des anomalies métaboliques.",
k:"Oligoménorrhée + hirsutisme + échographie typique = SOPK (Rotterdam) : toujours dépister l'insulinorésistance et protéger l'endomètre ; un hyperandrogénisme d'installation rapide et sévère fait chercher une tumeur."}
,
{n:"Endométriose et adénomyose utérine",q:"endométriose",
d:"Présence de tissu endométrial en dehors de la cavité utérine (ovaires, péritoine, ligaments, intestin, vessie), hormono-dépendante et inflammatoire ; l'adénomyose est l'atteinte du myomètre (endométriose interne) ; première cause de douleurs pelviennes chroniques et d'infertilité.",
s:"Dysménorrhées sévères intenses et progressives, douleurs pelviennes chroniques, dyspareunie profonde, troubles digestifs ou urinaires cataméniaux (radiques aux règles) ; infertilité ; l'adénomyose : utérus globuleux, ménorragies et dysménorrhées ; l'examen est souvent normal ou retrouve des nodules du cul-de-sac postérieur.",
dx:"Échographie pelvienne (endométriomes ovariens = kystes échogènes homogènes, adénomyose) et IRM pelvienne (cartographie des lésions) ; examen clinique dédié ; le diagnostic de certitude reste histologique (coelioscopie) mais l'imagerie suffit pour le traitement médical.",
t:"Traitement médical de première intention (contraception continue, progestatifs, agonistes GnRH en cure courte) pour les douleurs ; chirurgie conservatrice (exérèse des lésions) dans les formes résistantes ou avec infertilité ; prise en charge de l'infertilité (FIV selon contexte) ; adénomyose : DIU au lévonorgestrel ou progestatifs, hysterectomie dans les formes majeures ; prise en charge de la douleur chronique (centres spécialisés).",
k:"Dysménorrhées sévères et progressives chez l'adulte jeune = endométriose : ne pas banaliser (« règles douloureuses normales » n'existe pas) ; imagerie dédiée et centre de référence."}
,
{n:"Dysménorrhées primaires et secondaires sévères",q:"dysménorrhée",
d:"Dysménorrhée : douleurs pelviennes survenant avec les règles ; primaire (adolescente, sans pathologie pelvienne, spasmodique, cédant avec l'âge et la parité) ou secondaire (adulte, révélatrice d'une endométriose, d'un fibrome, d'une adénomyose ou d'une infection génitale).",
s:"Primaire : douleurs spasmodiques hypogastriques débutant juste avant ou avec les règles, irradiant vers les lombes et les cuisses, avec signes fonctionnels (nausées, diarrhée), cédant avec le temps ; secondaire : douleurs croissantes avec l'âge, résistantes aux antalgiques, avec dyspareunie ou ménorragies associées.",
dx:"Examen clinique pelvien ; échographie pelvienne à la recherche d'une cause (endométriose, fibrome, malformation si adolescente) ; calendrier des douleurs ; arrêt du diagnostic de primaire si évolution atypique (résistance aux AINS, aggravation).",
t:"Primaire : AINS au moment des règles (ibuprofène, naproxène) ± contraception œstroprogestative (réduit les douleurs dans la majorité des cas) ; chaleur locale, réassurance ; secondaire : traitement de la cause (endométriose, fibrome) ; contraception continue.",
k:"Des règles invalidantes chaque mois ne sont jamais « normales » : si les AINS ne suffisent pas, chercher une cause (endométriose en premier) par l'imagerie."}
,
{n:"Insuffisance Ovarienne Prématurée (IOP) et ménopause",q:"insuffisance ovarienne prématurée",
d:"IOP : arrêt du fonctionnement ovarien avant 40 ans (aménorrhée avec FSH élevée et estradiol bas, confirmée à deux mois d'intervalle) : causes génétiques (Turner, FMR1), auto-immunes, iatrogènes (chimiothérapie, radiothérapie), idiopathiques ; ménopause : cessation définitive des règles après 45-55 ans (12 mois d'aménorrhée), par épuisement du capital folliculaire.",
s:"Spanio-aménorrhée, bouffées de chaleur, sueurs nocturnes, sécheresse vaginale, dyspareunie, troubles du sommeil et de l'humeur, baisse de libido ; à long terme : ostéoporose, risque cardiovasculaire accru ; IOP : l'infertilité est la plainte principale, souvent en trompe l'œil (5 % de grossesses spontanées).",
dx:"FSH élevée et estradiol bas (à deux reprises à un mois d'intervalle pour l'IOP) ; bilan étiologique : caryotype, FMR1, anticorps (Addison, thyroïde), échographie pelvienne ; ostéodensitométrie ; bilan lipidique et cardiovasculaire.",
t:"Traitement hormonal substitutif : recommandé jusqu'à l'âge naturel de la ménopause dans l'IOP (prévention de l'ostéoporose et cardiovasculaire) ; après 50 ans : THS selon la symptomatologie et la fenêtre d'opportunité (doses minimales, réévaluation annuelle) ; mesure de la qualité de vie (bouffées, sexualité : traitement local de l'atrophie vaginale) ; dépistage des complications (mammographie, ostéodensitométrie) ; accompagnement de l'infertilité (don d'ovocytes).",
k:"Aménorrhée avec bouffées de chaleur avant 40 ans = IOP : FSH-estradiol à deux reprises, caryotype et bilan auto-immun ; THS obligatoire jusqu'à 50 ans pour protéger cœur et os."}
]},
{name:"Infections Gynécologiques & IST",paths:[
{n:"Infections Sexuellement Transmissibles (IST) : Chlamydia, Gonococcie, Trichomonase, Herpès génital",q:"infections sexuellement transmissibles",ur:true,
d:"IST bactériennes (Chlamydia trachomatis — la plus fréquente, gonocoque, syphilis, mycoplasme) ou parasitaires (Trichomonas vaginalis) et virales (herpès HSV-2, VPH, VIH) ; co-infections fréquentes ; le dépistage et le traitement des partenaires sont indissociables de celui de la patiente.",
s:"Le plus souvent asymptomatiques (chlamydia) ; leucorrhées anormales (jaunes-vertes, mousseuses : trichomonas ; purulentes : gonocoque), brûlures mictionnelles, métrorragies post-coïtales, douleurs pelviennes (salpingite) ; herpès : vésicules et ulcérations génitales douloureuses récidivantes ; syphilis : chancre induré indolore puis éruption.",
dx:"PCR sur premier jet d'urine ou prélèvements génitaux (chlamydia, gonocoque) ; prélèvement vaginal frais (trichomonas) ; sérologies syphilis et VIH systématiques ; dépistage de toutes les IST en cas de diagnostic positif ; examen sous speculum.",
t:"Chlamydia : doxycycline 7 jours (ou azithromycine dose unique selon protocoles) ; gonocoque : ceftriaxone IM (résistances croissantes) ; trichomonase : métronidazole (traitement du partenaire obligatoire) ; herpès : aciclovir/valaciclovir (épisodes et suppression des récidives) ; abstinence sexuelle pendant le traitement, dépistage et traitement des partenaires ; déclaration obligatoire (syphilis, gonococcie) et prévention (préservatif, vaccination VPH et hépatite B).",
k:"Une IST découverte = dépistage complet des autres (VIH, syphilis, VHB) et traitement des partenaires : sinon réinfestation ; chlamydia asymptomatique = première cause d'infertilité tubaire évitable."}
,
{n:"Pelvi-péritonites et Salpingites aiguës / chroniques (Maladie Inflammatoire Pelvienne - MIP)",q:"salpingite",ur:true,
d:"Infection ascendante de l'endomètre, des trompes et du péritoine pelvien (MIP) : Chlamydia et gonocoque surtout, flore vaginale ; grande cause de stérilité tubaire, de GEU et de douleurs chroniques ; formes aiguës (salpingite, pelvi-péritonite) et chroniques (hydrosalpynx, adhérences).",
s:"Douleurs pelviennes bilatérales spontanées et provoquées (examen : douleur à la mobilisation utérine), leucorrhées et métrorragies, fièvre ; pelvi-péritonite : défense, douleur au toucher, masse latéro-utérine (abcès de Douglas) ; chronique : douleurs cycliques, infertilité, GEU.",
dx:"PCR chlamydia et gonocoque, prélèvements vaginaux, NFS-CRP, β-hCG (éliminer une GEU) ; échographie pelvienne (épaississement des trompes, abcès) ; coelioscopie dans les formes douteuses ou abcédées ; à distance : hystérosalpingographie (perméabilité tubaire).",
t:"Salpingite simple : antibiothérapie probabiliste (ceftriaxone IM + doxycycline + métronidazole 14 jours) en ambulatoire ; formes graves (pelvi-péritonite, abcès, grossesse, VIH) : hospitalisation, antibiothérapie IV, drainage ou chirurgie des abcès ; traitement du ou des partenaires ; suivi de fertilité ; prévention : dépistage IST et préservatif.",
k:"Douleur pelvienne + leucorrhées + douleur à la mobilisation utérine = salpingite : antibiotiques sans délai (chaque jour compte pour la fertilité tubaire) et traitement du partenaire."}
,
{n:"Vaginoses bactériennes et candidoses vulvo-vaginales récidivantes",q:"vaginose bactérienne",
d:"Déséquilibres de la flore vaginale : vaginose bactérienne (prolifération de Gardnerella et anaérobies, sans inflammation, pH élevé) et candidose vulvo-vaginale (Candida albicans, inflammation, pH normal) ; les récidives (plus de 4 épisodes/an) imposent de chercher un terrain (diabète, immunodépression, VIH).",
s:"Vaginose : leucorrhées grisâtres homogènes, odeur de « poisson pourri » (test à la potasse positif), absence de prurit et de brûlure ; candidose : leucorrhées blanches en « lait caillé », prurit vulvaire intense, brûlures, œdème et érythème vulvaire, dyspareunie.",
dx:"Examen au speculum, pH vaginal (élevé dans la vaginose, normal dans la candidose), prélèvement vaginal (examen direct, culture) ; test à la potasse (vaginose) ; glycémie et sérologie VIH si candidoses récidivantes.",
t:"Vaginose : métronidazole (oral ou local) ou clindamycine locale ; candidose : azolés locaux (éconazole, clotrimazole) ou fluconazole oral (dose unique) ; candidoses récidivantes : fluconazole hebdomadaire pendant 6 mois, contrôle du diabète, arrêt des facteurs (antibiotiques, douches vaginales, port de vêtements occlusifs) ; le traitement du partenaire n'est pas systématique (sauf balanites récidivantes).",
k:"Prurit + leucorrhées blanches = candidose (pH normal) ; odeur de poisson sans inflammation = vaginose (pH élevé) ; candidoses récidivantes = contrôler la glycémie et le statut VIH."}
,
{n:"Bartholinite aiguë et abcès de la glande de Bartholin",q:"bartholinite",ur:true,
d:"Infection de la glande de Bartholin (glande vestibulaire majeure) : kyste obstructif puis infection à germes banals ou IST, formant un abcès de la grande lèvre, très douloureux ; atteinte le plus souvent unilatérale de la femme en âge de procréer.",
s:"Tuméfaction douloureuse, chaude et rouge de la partie postérieure de la grande lèvre, gênant la marche et la position assise ; fièvre possible ; kyste indolore entre les épisodes (récidives fréquentes) ; parfois fistulisation spontanée.",
dx:"Clinique (examen vulvaire) ; prélèvements de l'abcès (bactériologie, recherche de gonocoque et chlamydia) ; pas d'imagerie dans la forme typique.",
t:"Antalgiques, bains de siège ; abcès : incision et drainage à la lame (drainage simple) — la marsupialisation (confection d'une poche) réduit les récidives ; antibiothérapie si cellulite ou contexte IST ; kystes récidivants : marsupialisation ou exérèse de la glande à froid.",
k:"Tuméfaction douloureuse de la grande lèvre = bartholinite abcédée : drainage chirurgical (la simple ponction récidive), et dépister les IST."}
]}
]},

{id:"gyn-chir",num:4,name:"Gynécologie Chirurgicale & Pathologies Tumorales",groups:[
{name:"Pathologies Utérines & Annexielles",paths:[
{n:"Myomes utérins / Fibromes utérins (sous-muqueux, intramuraux, sous-séreux)",q:"fibrome utérin",
d:"Tumeurs bénignes du muscle utérin (les plus fréquentes des tumeurs pelviennes, femme de 30-50 ans) : sous-muqueux (hémorragies, infertilité), intramuraux et sous-séreux (compression, masse) ; hormono-dépendants (régression après la ménopause).",
s:"Ménorragies abondantes avec anémie (sous-muqueux), pesanteur pelvienne, masse abdominale (utérus bosselé), pollakiurie et constipation par compression, dysménorrhées ; complications : torsion d'un myome sous-séreux pédiculé, nécrobiose (douleur aiguë chez la femme enceinte), infertilité ou fausses couches.",
dx:"Échographie pelvienne (cartographie : nombre, siège, taille) ± IRM pelvienne (avant chirurgie ou mapping) ; NFS et ferritine (anémie) ; exploration de la cavité (hystéroscopie) si sous-muqueux ou interférence avec la fertilité ; aucune biologie spécifique.",
t:"Asymptomatique : surveillance ; ménorragies : acide tranexamique, progestatifs, DIU lévonorgestrel, embolisation des artères utérines ; chirurgie : myomectomie (conservatrice, désir de grossesse) ou hystérectomie (formes majeures, sans désir de grossesse) ; myome sous-muqueux : résection hystéroscopique ; nécrobiose gravidique : antalgiques (pas de chirurgie en dehors des complications).",
k:"Ménorragies abondantes de la femme de 35-50 ans = fibrome : échographie, corriger le fer, et proposer un traitement conservateur si désir de grossesse."}
,
{n:"Kystes ovariens fonctionnels et organiques (kystes dermoïdes, endométriomes)",q:"kyste ovarien",
d:"Kystes ovariens : fonctionnels (folliculaire, lutéal — régressant spontanément) ou organiques (tératome dermoïde, endométriome, cystadénome) ; complications : torsion d'annexe, rupture, hémorragie intrakystique ; la notion de « kyste » chez une femme ménopausée est suspecte (tumeur).",
s:"Le plus souvent asymptomatiques (découverte échographique) ; douleurs pelviennes sourdes, pesanteur, troubles du cycle (fonctionnels) ; torsion : douleur pelvienne brutale intense avec nausées et vomissements (urgence) ; rupture : douleur avec défense ; ménopause : toute masse annexielle est potentiellement néoplasique.",
dx:"Échographie pelvienne (taille, contenu, cloisons, vascularisation au doppler : score de malignité) ; CA-125 (modérément utile, élevé aussi dans l'endométriose et les affections bénignes) ; β-hCG (grossesse) ; IRM pelvienne en cas de doute ; contrôle échographique à 6-8 semaines pour prouver le caractère fonctionnel (chez la femme en âge de procréer).",
t:"Fonctionnel : surveillance échographique (régression spontanée), contraception œstroprogestative pour prévenir les récidives ; organique symptomatique ou > 5-6 cm : kystectomie cœlioscopique (conservation ovariale) ; endométriome : traitement médical ou chirurgie selon fertilité ; suspicion de malignité ou ménopause : prise en charge en oncologie (annexectomie, bilan d'extension).",
k:"Chez la femme en âge de procréer, un kyste simple régresse : contrôle à 6-8 semaines avant tout traitement ; après la ménopause, toute masse ovarienne est une tumeur jusqu'à preuve du contraire."}
,
{n:"Torsion d'annexe (trompe et/ou ovaire)",q:"torsion ovarienne",ur:true,
d:"Rotation de l'annexe (ovaire ± trompe) autour de son pédicule vasculaire : ischémie puis nécrose de l'ovaire ; terrain : kyste ou tumeur ovarienne (dermoïde surtout), hyperstimulation, femme jeune ; urgence chirurgicale préservant la fertilité.",
s:"Douleur pelvienne brutale, intense, en coup de poignard, avec nausées et vomissements, irradiant vers l'aine ; parfois douleur intermittente (torsion-détorsion) ; fièvre tardive, défense ; masse latéro-utérine douloureuse à l'examen.",
dx:"Échographie pelvienne et doppler : masse annexielle (souvent kystique) avec diminution ou abolition du flux artériel ovarien (signe capital, mais un flux présent n'élimine pas le diagnostic) ; NFS-CRP, β-hCG ; la cœlioscopie est diagnostique et thérapeutique.",
t:"Cœlioscopie en urgence : détorsion et conservation de l'annexe (même si l'ovaire paraît noir — récupération possible) avec cystectomie ou fixation ; annexectomie si nécrose étendue ou tumeur suspecte ; pas d'expectative chez la femme jeune : toute suspicion opère.",
k:"Douleur pelvienne brutale + masse ovarienne = torsion d'annexe : cœlioscopie urgente, un doppler normal n'élimine rien ; détordre et conserver (fertilité)."}
,
{n:"Prolapsus génito-urinaire (cystocèle, hystéroptose, rectocèle) et Incontinence urinaire d'effort (IUE)",q:"prolapsus génital",
d:"Descente des organes pelviens par défaillance des soutiens (accouchements, ménopause, obésité, constipation) : cystocèle (vessie), hystéroptose (utérus), rectocèle, élytrocèle ; l'incontinence urinaire d'effort (fuites à l'effort, toux, éternuements) par insuffisance sphinctérienne est souvent associée (à distinguer de l'incontinence par urgenturie).",
s:"Sensation de boule ou de poids vaginal, majorée en fin de journée, régressant en décubitus ; tuméfaction vulvaire ; troubles mictionnels (fuites à l'effort, dysurie par compression, mictions incomplètes) et digestifs (constipation, dyschésie) ; l'IUE : fuites synchrones de l'effort, sans besoin préalable.",
dx:"Examen clinique pelvien debout et couché (classification POP-Q des étages) ; bilan urodynamique et calendrier mictionnel ; test à la toux ; échographie pelvienne et post-mictionnelle ; évaluation de la qualité de vie.",
t:"Mesures conservatrices : rééducation périnéale (séances), traitement de la constipation et de la toux, anneaux pessaires (femmes non opérables ou en attente) ; chirurgie : cure de prolapsus par voie vaginale (promontofixation cœlioscopique, interventions vaginales avec ou sans prothèse) ; IUE : rééducation d'abord, puis bandelette sous-urétrale (TVT) ; prudence avec les prothèses (complications, encadrement réglementaire).",
k:"Boule vaginale de la femme âgée multipare = prolapsus : rééducation et pessaire ou chirurgie selon l'âge et le souhait ; les fuites à l'effort se traitent par bandelette sous-urétrale après rééducation."}
]},
{name:"Pathologies Trophoblastiques & Oncologie Gynécologique",paths:[
{n:"Maladie trophoblastique gestationnelle (Môle hydatiforme complète et partielle, choriocarcinome)",q:"môle hydatiforme",ur:true,
d:"Tumeurs trophoblastiques gestationnelles : môle hydatiforme complète (duplication androgénétique, risque de choriocarcinome 15-20 %) ou partielle (œuf triploïde) ; le choriocarcinome est la tumeur trophoblastique maligne (métastases pulmonaires, vaginales, cérébrales), très chimiosensible.",
s:"Môle : métrorragies du premier trimestre (aspect « grains de raisin »), utérus plus gros que l'âge gestationnel, β-hCG très élevées, hyperémèse, HTA/pré-éclampsie avant 20 SA (signe d'appel), absence de battements cardiaques fœtaux (môle complète) ; choriocarcinome : métrorragies du post-môle, métastases (dyspnée, hémorragies, troubles neurologiques).",
dx:"β-hCG plasmatiques très élevées ; échographie (utérus rempli de vésicules, « tempête de neige », absence d'embryon) ; histologie (aspiration) ; bilan d'extension du choriocarcinome (radiographie ou TDM thoracique, IRM cérébrale, échographie hépatique).",
t:"Évacuation utérine (aspiration) de la môle, histologie systématique ; surveillance des β-hCG hebdomadaires jusqu'à négativation puis mensuelle pendant 6-12 mois (score FIGO/OMS pronostique) ; contraception pendant la surveillance (pas de grossesse) ; persistance d'un taux ou choriocarcinome : chimiothérapie (méthotrexate en première ligne, polychimiothérapie des formes à risque) ; hystérectomie possible ; guérison dans la grande majorité, fertilité préservée.",
k:"Métrorragies du premier trimestre avec utérus trop gros et β-hCG très élevées = môle hydatiforme : évacuation puis surveillance stricte des β-hCG (la grossesse est interdite jusqu'à leur normalisation prolongée)."}
,
{n:"Lésions précancéreuses et cancers du col de l'utérus (dysplasies CIN 1/2/3, carcinome invasif)",q:"cancer du col de l'utérus",
d:"Cancer du col lié au papillomavirus oncogènes (HPV 16, 18) : progression des dysplasies cervicales intra-épithéliales (CIN 1, 2, 3) vers le carcinome épidermoïde ou adénocarcinome invasif en 10-15 ans ; la vaccination et le frottis (dépistage) ont transformé son épidémiologie.",
s:"Lésions précancéreuses : asymptomatiques (découverte au frottis/HPV) ; cancer invasif : métrorragies post-coïtales ou spontanées, leucorrhées, douleurs pelviennes tardives (paramètres, vessie, rectum) ; saignements et anémie ; lésion du col visible ou non au speculum.",
dx:"Dépistage : frottis cervico-utérin (cytologie) et/ou test HPV (protocoles actuels) ; colposcopie avec biopsies dirigées (CIN) ; conisation (diagnostique et thérapeutique) ; cancer : imagerie IRM pelvienne, examen sous anesthésie (classification FIGO) ; bilan d'extension (TDM, TEP).",
t:"CIN 1 : surveillance ; CIN 2-3 : conisation (exérèse de la zone de transformation) ; cancer précoce : chirurgie (conisation large, hystérectomie élargie avec curage) ou radio-chimiothérapie concomitante selon le stade ; stades avancés : radio-chimiothérapie, chimiothérapie palliative, thérapies ciblées (bevacizumab, immunothérapie) ; prévention : vaccination HPV (filles et garçons) et dépistage organisé.",
k:"Métrorragies post-coïtales = examen du col et frottis : ne jamais traiter une « cervicite » sans avoir éliminé un cancer ; le dépistage HPV/frottis touche les lésions avant l'invasion."}
,
{n:"Cancers de l'endomètre et hyperplasies atypiques",q:"cancer de l'endomètre",
d:"Adénocarcinome de l'endomètre (premier cancer gynécologique dans les pays riches, femme ménopausée, obésité et hyperestrogénie non compensée) ; précédé d'hyperplasies endométriales (simple, complexe, atypique — cette dernière étant un précurseur direct).",
s:"Métrorragies post-ménopausiques (le signe cardinal — tout saignement après la ménopause impose une exploration), leucorrhées, douleurs pelviennes tardives ; terrain : obésité, diabète, nulliparité, tamoxifène, syndrome de Lynch (colon + endomètre), syndrome des ovaires polykystiques.",
dx:"Échographie pelvienne (épaisseur de l'endomètre : plus de 4-5 mm après la ménopause) ; biopsie d'endomètre (pipelle) ou hystéroscopie-biopsie ; histologie ; bilan d'extension : IRM pelvienne, TDM, dosage CA-125 ; recherche de syndrome de Lynch si contexte familial.",
t:"Hyperplasie atypique : progestatifs (DIU lévonorgestrel) ou hystérectomie selon l'âge et le désir ; cancer : chirurgie (hystérectomie avec annexectomie ± curage, cœlioscopique) selon le stade, complétée par radiothérapie (formes à risque), chimiothérapie et hormonothérapie (progestatifs des formes métastatiques bien différenciées) ; suivi ; prévention : traitement des facteurs (obésité, progestatifs en cas d'hyperestrogénie).",
k:"Toute métrorragie post-ménopausique = échographie puis biopsie d'endomètre : le cancer de l'endomètre guérit dans plus de 80 % des cas quand il est découvert à ce stade."}
,
{n:"Cancers de l'ovaire et tumeurs borderline",q:"cancer de l'ovaire",
d:"Cancers ovariens : épithéliaux (les plus fréquents, femme ménopausée — carcinome séreux haut grade) ; tumeurs germinales (jeune femme : dysgerminome) ; tumeurs borderline (prolifération épithéliale sans invasion, pronostic intermédiaire) ; hérédité : mutations BRCA1/2 et syndrome de Lynch.",
s:"Cancer de l'ovaire = maladie insidieuse (tueur silencieux) : troubles digestifs vagues (ballonnements, pesanteur), augmentation du périmètre abdominal, douleurs, pollakiurie ; masse pelvienne, ascite ; formes avancées : occlusion, pleurésie, amaigrissement ; tumeurs borderline : masse asymptomatique le plus souvent.",
dx:"Échographie puis IRM pelvienne (masse complexe, cloisons, végétations, ascite) ; CA-125 (élevé, peu spécifique) ; TDM thoraco-abdomino-pelvien (extension) ; bilan génétique (BRCA) ; la cytologie de l'ascite ou du lavage péritonéal ; le diagnostic histologique est chirurgical.",
t:"Chirurgie de référence : annexectomie avec stadiation complète (ou cytoréduction maximale dans les formes avancées) ± chimiothérapie (carboplatine-paclitaxel) néoadjuvante ou adjuvante ; tumeurs borderline : chirurgie conservatrice possible (jeune femme) ; entretien par thérapies ciblées (anti-angiogéniques, PARP inhibiteurs pour les mutations BRCA) ; surveillance CA-125 et imagerie ; dépistage familial (BRCA) et chirurgie prophylactique discutée.",
k:"Troubles digestifs vagues et augmentation du périmètre abdominal chez une femme de plus de 50 ans = toucher pelvien et échographie : le cancer de l'ovaire est découvert tard, la cytoréduction et le traitement médical en découlent."}
,
{n:"Pathologies bénignes et malignes du sein (fibroadénomes, mastopathies, cancer du sein)",q:"cancer du sein",ur:true,
d:"Pathologie mammaire : bénigne (fibroadénome — nodule mobile de la femme jeune, kystes, mastopathie fibrokystique) et maligne (cancer du sein : carcinome canalaire ou lobulaire, premier cancer de la femme) ; dépistage organisé par mammographie dès 50 ans, et dans les formes héréditaires (BRCA1/2) plus tôt par IRM.",
s:"Nodule mammaire dur, fixé, indolore ; rétraction cutanée ou du mamelon, écoulement sanglant, modification récente du sein ; formes localement avancées : peau d'orange, ulcération, adénopathie axillaire ; fibroadénome : nodule souple, mobile, bien limité, de la femme de 20-30 ans ; mastite du post-partum à distinguer du carcinome inflammatoire.",
dx:"Imagerie : mammographie et échographie (selon l'âge) ; microbiopsie (macrobopsie) de tout nodule suspect (ACR 4-5) ; examen clinique bilatéral et aires ganglionnaires ; IRM si BRCA ou bilan d'extension ; bilan pré-thérapeutique (TDM/TEP selon protocoles, récepteurs hormonaux et HER2 sur la biopsie).",
t:"Cancer : chirurgie conservatrice ou mastectomie avec ganglion sentinelle (± curage) ; radiothérapie (après chirurgie conservatrice) ; traitements systémiques selon le sous-type : hormonothérapie (récepteurs positifs), chimiothérapie, anti-HER2 (trastuzumab), immunothérapie ; formes métastatiques : traitements prolongés ; fibroadénome : surveillance ou exérèse ; kystes : ponction si douloureux ; reconstruction mammaire et accompagnement.",
k:"Tout nodule mammaire dur ou fixé, quelle que soit l'âge = imagerie et biopsie : le cancer du sein chez la femme jeune est plus agressif et la mammographie seule peut le manquer (échographie, IRM)."}
]}
]},

{id:"gyn-pf",num:5,name:"Planification Familiale & Prévention",groups:[
{name:"Contraception & Interventions Préventives",paths:[
{n:"Contraception hormonale (orale, injectable, implants sous-cutanés)",q:"contraception hormonale",
d:"Contraception hormonale : œstroprogestative (pilule combinée, anneau, patch — bloque l'ovulation) ou microprogestative (pilule, implant sous-cutané d'étonogestrel, injectable — épaissit la glaire) ; efficacité supérieure à 99 % à condition d'une observance parfaite ; choix selon le profil de risque (tabac, migraine avec aura, thrombose, allaitement).",
s:"Effets indésirables : céphalées, nausées, tension mammaire, spotting (microprogestatifs), prise de poids ; risques : thrombose veineuse (œstroprogestatifs, surtout de 3e génération), HTA ; contre-indications des œstroprogestatifs : tabac après 35 ans, migraine avec aura, antécédent thrombotique, cancer hormonodépendant, allaitement (préférer les microprogestatifs).",
dx:"Consultation de contraception : interrogatoire (tabac, migraines, antécédents, ATCD familiaux thrombotiques), tension artérielle, poids, examen ; pas d'examen complémentaire systématique.",
t:"Information sur les méthodes et l'observance ; pilule œstroprogestative (la mieux tolérée en 2e génération) ou microprogestative selon les contre-indications ; implant : 3 ans, très efficace, sans observance ; injectable : rappel toutes les 8-13 semaines ; dépistage des IST non couvert par la contraception hormonale (préservatif) ; suivi annuel.",
k:"La contraception œstroprogestative est contre-indiquée après 35 ans chez la fumeuse et en cas de migraine avec aura (risque d'AVC) ; l'implant et le DIU efficaces sans observance."}
,
{n:"Dispositifs intra-utérins (DIU / Stérilet au cuivre ou hormonal)",q:"stérilet",
d:"Contraception intra-utérine de longue durée : au cuivre (effet spermicide local, jusqu'à 10 ans, sans hormone) ou hormonal au lévonorgestrel (atrophie endométriale, règles diminuées, 5 ans) ; parmi les méthodes les plus efficaces (supérieure à 99 %), indépendante de l'observance.",
s:"DIU cuivre : règles plus abondantes et douloureuses possible ; DIU hormonal : spotting initial puis règles diminuées ou absentes (traitement des ménorragies) ; complications rares : douleurs à la pose, expulsion, infection (premier mois), perforation (rare), grossesse extra-utérine en cas de grossesse sur DIU.",
dx:"Consultation préalable : information, dépistage des IST si risque (pas de test systématique chez l'asymptomatique à bas risque), taille utérine ; pose en première partie de cycle idéalement (ou n'importe quand si pas de risque de grossesse) ; vérification des fils à la suite et auto-palpation.",
t:"Pose (ou retrait-échange) par un soignant formé ; antalgiques si douleur ; suivi : contrôle des fils à 4-6 semaines puis annuellement ; DIU hormonal : alternative à la chirurgie dans les ménorragies ; encadrer les règles abondantes du cuivre (AINS, acide tranexamique) ; contraception d'urgence au cuivre possible jusqu'à 5 jours après un rapport.",
k:"Le DIU convient aux nullipares et aux adolescentes : les restrictions d'anciennes recommandations ont disparu ; le DIU cuivre reste une contraception d'urgence efficace jusqu'à 5 jours."}
,
{n:"Contraception définitive (ligature des trompes, vasectomie du partenaire)",q:"stérilisation tubaire",
d:"Contraception définitive : féminine (ligature ou occlusion tubaire par cœlioscopie ou hystéroscopie — essure) ou masculine (vasectomie, plus simple et plus fiable) ; décisions irréversibles nécessitant une information loyale (consentement écrit, délai de réflexion selon la législation) ; à proposer aux couples dont la famille est constituée.",
s:"Aucun effet secondaire hormonal ; vasectomie : intervention locale sous anesthésie locale, azoospermie effective après 3 mois (contrôle du spermogramme obligatoire) ; ligature : cœlioscopie sous anesthésie générale, règles conservées ; regrets possibles (âge jeune, événement de vie) d'où l'importance de la consultation préalable.",
dx:"Consultation d'information (motivation, alternatives réversibles, consentement) ; bilan pré-opératoire standard ; contrôle du spermogramme à 3 mois (vasectomie) avant l'arrêt des autres contraceptions.",
t:"Vasectomie : geste ambulatoire, azoospermie à confirmer par spermogrammes ; ligature/occlusion tubaire : cœlioscopie ou pose hystéroscopique avec vérification de la bonne position ; contraception intermédiaire jusqu'à efficacité confirmée ; information sur l'irréversibilité (les techniques de reperméabilisation sont aléatoires) ; PMA avec don de spermatozoïdes ou FIV si regret.",
k:"La stérilisation est définitive : proposer d'abord les méthodes réversibles de longue durée (DIU, implant) ; la vasectomie est plus simple et plus fiable que la ligature tubaire."}
,
{n:"Contraception d'urgence",q:"contraception d'urgence",ur:true,
d:"Contraception post-coïtale après rapport non ou mal protégé : lévonorgestrel (efficace jusqu'à 72 h — 3 jours, plus précoce = plus efficace), acétate d'ulipristal (jusqu'à 120 h — 5 jours) ou DIU au cuivre (jusqu'à 120 h, la méthode la plus efficace, plus de 99 %) ; n'interrompt pas une grossesse déjà installée (ce n'est pas un avortement).",
s:"Contexte : rapport non protégé, rupture ou oubli de pilule (plus de 12 h selon le type), expulsion du DIU, échec du préservatif ; violences sexuelles : protocole dédié (contraception d'urgence + PPE + dépistage + plainte) ; saignements ou retard de règles à surveiller ensuite.",
dx:"Aucun examen préalable obligatoire (pas de test de grossesse avant la prise, sauf contexte) ; datation précise du rapport ; éliminer une grossesse évolutive si retard de règles important.",
t:"Lévonorgestrel le plus tôt possible (pharmacie sans ordonnance) ; ulipristal si plus de 72 h (ordonnance) ; DIU cuivre posé par un professionnel jusqu'à 120 h ; pas de méthode méthode de contraception régulière : démarrer une contraception durable ; test de grossesse si retard de règles ; PPE (VIH, IST) et dépistages en cas de rapport à risque ; accès gratuit pour les mineures.",
k:"Contraception d'urgence = le plus tôt possible (l'efficacité décroît toutes les heures) ; le DIU cuivre est la méthode la plus efficace jusqu'à 5 jours ; compléter par une contraception régulière."}
,
{n:"Dépistage des lésions cervicales (frottis cervico-utérin, inspection visuelle à l'acide acétique - IVA/IVL)",q:"frottis cervico-utérin",
d:"Dépistage des lésions précancéreuses du col : frottis cervico-utérin (cytologie) et/ou test HPV (organisé de 25 à 65 ans selon les protocoles actuels) ; dans les pays à faibles ressources, l'inspection visuelle à l'acide acétique (IVA) et au lugol (IVL) avec traitement immédiat des lésions (« screen and treat ») sauve des vies.",
s:"Dépistage chez une femme asymptomatique (rappel par le programme organisé tous les 3 ans pour le frottis, 5 ans pour le test HPV) ; IVA : acide acétique appliqué sur le col, lésions acéto-blanches orientant une biopsie ou un traitement immédiat (cryothérapie, LEEP).",
dx:"Frottis (prélèvement de la zone de transformation) ou autoprélèvement vaginal (HPV) ; en cas d'anomalie : colposcopie avec biopsies ; IVA/IVL : lecture immédiate à la colposcope ou à l'œil nu.",
t:"Résultat normal : poursuite du dépistage au rythme prévu ; ASC-US/HPV positif : contrôles ou colposcopie selon protocole ; lésions de haut grade : conisation ; screen and treat : traitement immédiat des lésions visibles (cryothérapie ambulatoire) dans les ressources limitées ; vaccination HPV en complément du dépistage (pas en remplacement).",
k:"Le dépistage du cancer du col (frottis/HPV de 25 à 65 ans) rejoint la vaccination HPV : ensemble, ils peuvent éliminer ce cancer ; IVA + cryothérapie = dépistage et traitement en une seule visite."}
,
{n:"Prise en charge des victimes de violences sexuelles (soins d'urgence, prophylaxie post-exposition VIH/IST)",q:"violences sexuelles",ur:true,
d:"Prise en charge globale de la victime d'agression sexuelle : soins somatiques, contraception d'urgence, prophylaxie post-exposition (PPE) du VIH et des IST, recueil médico-légal (certificat), accompagnement psychologique et dépôt de plainte accompagné ; la victime doit être crue et informée à chaque étape.",
s:"Contexte de l'agression (date, type de rapport, agresseur connu ou non), lésions génitales et extragénitales, douleurs, saignements ; état psychique (sidération, panique) ; la victime peut se présenter tardivement ou sans plainte initiale.",
dx:"Examen clinique complet avec consentement (lésions, prélèvements médico-légaux dans le cadre du protocole) ; prélèvements IST initiaux (VIH, VHB, VHC, syphilis, chlamydia, gonocoque) ; test de grossesse initial ; certification par un médecin formé (certificateur).",
t:"Soins des lésions ; contraception d'urgence (cuivre ou ulipristal selon délai) ; PPE du VIH si rapport à risque dans les 48 h (au mieux dans les 4 h) pendant 28 jours ; prophylaxie IST (antibiothérapie) et hépatite B (vaccination ± immunoglobulines) ; certificat médico-légal (sans dépôt de plainte obligatoire pour les soins) ; accompagnement psychologique et associatif, suivi sérologique à 1, 3 et 6 mois ; inscription au protocole violences (référent, structure dédiée).",
k:"Violences sexuelles = une seule consultation peut tout changer : contraception d'urgence + PPE VIH dans les 48 h + certificat + accompagnement ; le dépôt de plainte n'est jamais une condition des soins."}
]}
]}
]});


/* ============================================================
   DÉPARTEMENT 4 — CHIRURGIE (5 spécialités)
   ============================================================ */
DEPTS.push({
id:"chir",name:"Chirurgie",icon:"🩻",color:"#ef4444",
desc:"Urgences chirurgicales vitales, traumatologie lourde, chirurgie viscérale et orthopédique réglée : les pathologies opératoires essentielles, de la salle de déchocage au bloc programmé.",
specs:[

{id:"chir-urg",num:1,name:"Urgences Chirurgicales Vitales & Traumatologie Lourde",groups:[
{name:"Polytraumatismes & Chocs Traumatiques",paths:[
{n:"Choc hémorragique sur polytraumatisme",q:"choc hémorragique",ur:true,
d:"Choc hypovolémique par hémorragie massive chez un polytraumatisé : premières causes de saignement : intra-abdominal (rate, foie), thoracique, pelvien (fracture du bassin), fémoral ; la coagulopathie traumatique (consommation, hypothermie, acidose — triade létale) aggrave le pronostic.",
s:"Hypotension, tachycardie, pâleur, marbrures, agitation (hypoperfusion cérébrale), polypnée ; détresse associée selon les lésions (détresse respiratoire, coma) ; attention : le polytraumatisé jeune peut maintenir une PA normale jusqu'à 30-40 % de perte sanguine (choc compensé).",
dx:"Gestes sauveurs immédiats avant l'imagerie ; écho-Fast (épanchement intra-abdominal, péricardique, pleural) ; radiographie du bassin et du thorax au déchocage ; TDM corps entier si stabilisé ; bilan biologique (groupe, NFS, coagulation, lactates).",
t:"Protocole de prise en charge du choc hémorragique : garrot (hémorragie des membres), ceinture pelvienne, drainage thoracique si indiqué ; remplissage restreint (hypotension permissive), acide tranexamique précoce, protocole de transfusion massive (plasma : culots ≈ 1:1, fibrinogène, plaquettes), lutte contre l'hypothermie et l'acidose ; laparotomie ou thoracotomie d'hémostase en urgence ; radiologie interventionnelle ou embolisation ; gestion des lésions par priorités.",
k:"Polytraumatisé instable = écho-Fast et bloc opératoire, pas de TDM ; acide tranexamique et protocole transfusionnel massif : traiter la triade létale (hypothermie, acidose, coagulopathie)."}
,
{n:"Rupture traumatique de la rate, du foie ou des viscères creux",q:"traumatisme de la rate",ur:true,
d:"Traumatismes abdominaux fermés ou ouverts : lésions d'organes pleins (rate — le plus fréquent, foie) responsables d'hémopéritoine, et de viscères creux (estomac, intestin, colon, vessie) responsables de péritonite ; les lésions spléniques et hépatiques sont le plus souvent traitées de façon non opératoire si stabilité.",
s:"Traumatisme abdominal (volant, ceinture, choc direct, arme) : douleur abdominale, défense, choc hémorragique (organe plein), contracture et sepsis tardif (viscère creux) ; signe de Battle (traumatisme des reins), ecchymose en ceinture (ceinture de sécurité : lésions du grêle et du mésentère) ; hypotension au décubitus.",
dx:"Écho-Fast (hémopéritoine) ; TDM abdominale avec injection si stables (classification des lésions spléniques et hépatiques, pneumopéritoine) ; lipasémie, ECBU (hématurie), NFS ; cœlioscopie ou laparotomie si instabilité ou péritonite.",
t:"Organes pleins stables (la majorité) : surveillance en soins intensifs avec répétition de l'examen et de l'hémoglobine, embolisation artérielle si active ; instabilité ou lésion grave : chirurgie (splénectomie, hémostase hépatique packing) ; viscères creux : réparation ou résection-anastomose, lavage péritonéal, antibiothérapie ; après splénectomie : vaccinations (pneumocoque, méningocoque, Haemophilus) et antibioprophylaxie à vie du risque d'd'infection à germes encapsulés.",
k:"Traumatisme abdominal + hypotension = hémorragie interne jusqu'à preuve du contraire : écho-Fast au déchocage ; après splénectomie, les vaccinations anti-pneumococcique et anti-méningococcique sont vitales."}
,
{n:"Plaies pénétrantes du thorax (hémothorax, pneumothorax compressif) et de l'abdomen",q:"plaie pénétrante du thorax",ur:true,
d:"Plaies par arme blanche ou par balle : thoraciques (pneumothorax, hémothorax — parfois compressif : urgence absolue, lésions cardiaques et des gros vaisseaux) et abdominales (lésions d'organes, péritonite, éviscération) ; la plaie pénétrante de l'abdomen avec éviscération ou choc est opérée d'emblée.",
s:"Plaie thoracique : détresse respiratoire, emphysème sous-cutané, choc (hémothorax massif ou lésion cardiaque : tamponnade), plaie « soufflante » (plaie aspirante) ; pneumothorax compressif : distension veineuse, hypotension, abolition unilatérale du murmure, tympanisme — exsufflation immédiate ; plaie abdominale : douleur, défense, éviscération, hémorragie extériorisée.",
dx:"Plaies thoraciques : radio au lit si le patient le permet (pneumothorax, hémothorax), écho-Fast (tamponnade) ; jamais d'attente devant un pneumothorax compressif clinique ; plaies abdominales : TDM si stable, laparotomie si instable, éviscération, péritonite ; bilan lésionnel per-opératoire.",
t:"Plaie thoracique : pansement occlusif trois faces si plaie soufflante, drainage thoracique d'emblée (exsufflation à l'aiguille si compressif), thoracotomie d'hémostase si drainage massif (plus de 1500 mL d'emblée ou 200 mL/h) ; tamponnade : péricardocentèse puis chirurgie ; plaie abdominale : exploration (cœlioscopie ou laparotomie), réparation, antibiothérapie, prévention du tétanos.",
k:"Pneumothorax compressif = exsufflation immédiat à l'aiguille sans imagerie ; plaie thoracique drain thoracique d'emblée ; éviscération ou péritonite = laparotomie sans TDM."}
,
{n:"Traumatismes crânio-encéphaliques graves avec engagement cérébral",q:"traumatisme crânien",ur:true,
d:"Traumatisme crânien avec lésions cérébrales (hématome extradural, sous-dural, contusions, œdème) ; l'engagement (herniation cérébrale : passage du cerveau par l'orifice tentoriel ou le foramen magnum) est l'urgence neurochirurgicale absolue : mydriase aréactive, décérébration, arrêt respiratoire.",
s:"Trouble de conscience (Glasgow), confusion, agitation, amnésie, vomissements ; engagement temporal : anisocorie avec mydriase aréactive homolatérale, hémiplégie controlatérale, bradycardie et hypertension (signe de Cushing) puis arrêt ; extradural : intervalle lucide classique ; écoulement de LCR (rhinorrhée, otorrhée) = brèche méningée.",
dx:"TDM cérébrale sans injection en urgence (hématome, œdème, fractures, engagement) ; score de Glasgow répété ; pupilles ; jamais de PL ; surveillance continue de la conscience ; bilan lésionnel associé (polytraumatisé).",
t:"Engagement : mesures de sauvetage immédiates (osmothérapie : mannitol ou sérum salé hypertonique, tête à 30°, sédation, normocapnie) et neurochirurgie urgente (évacuation de l'hématome, trépanation-décompression) ; TC grave : intubation, monitorage de la pression intracrânienne, neuroréanimation ; prévention des complications (convulsions : prophylaxie brève, thrombose) ; rééducation.",
k:"Mydriase aréactive après un traumatisme crânien = engagement = osmothérapie immédiate et bloc neurochirurgical ; un intervalle lucide suivi d'un coma évoque l'hématome extradural."}
]},
{name:"Urgences Abdominales Aiguës (Abdomen Aigu Chirurgical)",paths:[
{n:"Péritonite aiguë généralisée (perforation d'ulcère, perforation colique ou appendiculaire)",q:"péritonite",ur:true,
d:"Inflammation du péritoine par perforation d'un viscère (ulcère gastro-duodénal, appendice, côlon, diverticule, estomac) ou par diffusion d'une infection : abdomen chirurgical aigu, urgence opératoire ; le tableau évolue vers le choc septique.",
s:"Douleur abdominale brutale puis généralisée, contracture abdominale généralisée (ventre de bois), arrêt du transit, vomissements, fièvre, tachycardie, hypotension, déshydratation ; les diarrhées et les rectorragies sont absentes ; le tableau s'atténue chez le sujet âgé, sous corticoïdes ou immunodéprimé.",
dx:"TDM abdomino-pelvien avec injection (pneumopéritoine, abcès, origine de la perforation) ; radiographie debout (pneumopéritoine en croissant sous-costo-phrénique) ; NFS, CRP, ionogramme, bilan de coagulation ; hypokaliémie et déshydratation à corriger avant l'anesthésie.",
t:"Prise en charge chirurgicale en urgence : laparotomie ou cœlioscopie (suture de la perforation ulcéreuse avec épiplooplastie, appendicectomie, résection colique ± colostomie, lavage péritonéal abondant) ; antibiothérapie IV large spectre, réanimation hydro-électrolytique, sonde gastrique, antalgie ; soins intensifs si choc septique.",
k:"Contracture généralisée + arrêt du transit + fièvre = péritonite : TDM puis bloc opératoire sans délai ; le traitement est chirurgical, jamais l'antibiothérapie seule."}
,
{n:"Occlusion intestinale aiguë par strangulation (étranglement herniaire, volvulus)",q:"étranglement herniaire",ur:true,
d:"Occlusion avec souffrance digestive : étranglement herniaire (hernie inguinale, crurale, ombilicale non réductible), volvulus du grêle ou du sigmoïde (tour de spire sur mésentère ou mésosigmoïde) ; la nécrose intestinale impose une résection : urgence chirurgicale absolue.",
s:"Douleurs abdominales paroxystiques intenses et permanentes entre les crises, vomissements précoces, arrêt des matières et des gaz, météorisme ; hernie douloureuse, tendue, non réductible et non expansive à la toux ; volvulus du sigmoïde : distension majeure (météorisme en tonneau) ; fièvre, tachycardie, défense = souffrance en cours.",
dx:"Scanner abdomino-pelvien (niveaux hydro-aériques, anses dilatées, hernie étranglée, volvulus avec signe du tourbillon, pneumatose ou rehaussement pariétal anormal = ischémie) ; ionogramme (déshydratation, acidose), NFS (hyperleucocytose), lactates ; radiographie (volvulus du sigmoïde : cadre colique géant).",
t:"Réanimation : à jeun, aspiration naso-gastrique, correction hydro-électrolytique, antibiothérapie ; chirurgie urgente : réduction de l'étranglement avec résection des anses nécrotiques et réparation de la paroi, ou résection-anastomose ; volvulus du sigmoïde : endoscopie dévolvulatrice en urgence si gangrène absente (puis sigmoïdectomie programmée), chirurgie sinon ; prévention : cure de toutes les hernies diagnostiquées.",
k:"Toute hernie douloureuse non réductible = étranglement = chirurgie en urgence ; attendre, c'est la nécrose intestinale et la résection."}
,
{n:"Occlusion intestinale aiguë par obstruction (bride, tumeur sténosante, fécalome)",q:"occlusion intestinale",
d:"Occlusion sans souffrance digestive initiale : brides post-opératoires (la première cause chez l'adulte opéré), tumeurs coliques sténosantes (côlon gauche surtout), fécalome (sujet âgé), sténoses (radique, ischémique, Crohn) ; le risque évolutif est la strangulation et la perforation (caecale en cas d'obstruction colique fermée).",
s:"Douleurs abdominales paroxystiques, vomissements (tardifs dans l'occlusion colique), arrêt des matières et des gaz, distension progressive ; bride : terrain de chirurgie abdominale antérieure, paroxystisme douloureux, météorisme modéré ; occlusion colique : distension majeure, vomissements tardifs ; fécalome : sujet âgé, constipation, faux besoins.",
dx:"Scanner abdomino-pelvien avec injection (transition mécanique, cause, absence de signes de souffrance) ; radiographie (niveaux hydro-aériques, distension) ; ionogramme, NFS ; colonoscopie en urgence dans certaines obstructions coliques (endoprothèse).",
t:"Occlusion sur bride partielle : traitement médical d'abord (aspiration, réhydratation) avec réévaluation à 48 h ; complète ou non résolutive : chirurgie (adhésiolyse par cœlioscopie) ; tumeur colique : endoprothèse métallique couverte (décompression) ou chirurgie en un temps (résection ± colostomie) selon le contexte ; fécalome : désimpaction manuelle et lavages ; prévention des récidives de brides : pas de mesure validée.",
k:"Occlusion sur bride partielle = médicale 48 h maximum ; occlusion colique complète : décompression urgente (endoprothèse ou chirurgie) pour éviter la perforation caccale."}
,
{n:"Infarctus mésentérique (ischémie aiguë mésentérique)",q:"ischémie mésentérique",ur:true,
d:"Ischémie aiguë de l'intestin grêle par embolie (fibrillation auriculaire, thrombus), thrombose de l'artère mésentérique supérieure (athérome) ou thrombose mésentérique veineuse (thrombophilie, cirrhose) ; urgence absolue : la mortalité dépasse 50 % si le diagnostic tarde.",
s:"Douleur abdominale brutale et intense, disproportionnée à l'examen (examen longtemps normal : « douleur exquise, ventre plat »), nausées, diarrhée parfois sanglante, anorexie ; secondairement : distension, défense, choc septique et acidose (nécrose étendue) ; terrain : FA, athérome, insuffisance cardiaque, thrombophilie.",
dx:"Angio-TDM des vaisseaux mésentériques en urgence (occlusion artérielle ou veineuse, absence de rehaussement pariétal, pneumatose) ; lactates élevés et acidose métabolique (tardifs), NFS, ionogramme, CRP ; ECG (fibrillation auriculaire) ; laparotomie diagnostique si doute.",
t:"Réanimation, anticoagulation immédiate, antibiothérapie ; revascularisation urgente (radiologie interventionnelle : embolectomie, thrombolyse, stenting, ou chirurgie : embolectomie, pontage) ± résection des anses nécrotiques avec anastomose ou stomie ; laparostomie et second look à 24-48 h (réévaluation de la viabilité) ; ischémie veineuse : anticoagulation curative ; traitement de la cause (anticoagulation au long cours de la FA).",
k:"Douleur abdominale brutale disproportionnée à un examen normal, surtout en fibrillation auriculaire = angio-TDM mésentérique immédiat : chaque heure de retard condamne des mètres d'intestin."}
]},
{name:"Urgences Vasculaires & Cutanées Graves",paths:[
{n:"Ischémie aiguë des membres (embolie ou thrombose artérielle)",q:"ischémie aiguë des membres",ur:true,
d:"Arrêt brutal de la perfusion d'un membre par embolie (cœur : FA, infarctus, valvulopathie — le plus souvent) ou thrombose sur plaque (poplitée, fémorale) ; les 6 P : douleur, pâleur, absence de pouls, paresthésies, paralysie, poikilothermie ; fenêtre thérapeutique de 6 h avant nécrose.",
s:"Douleur brutale et intense du membre, pâleur puis marbrures, froideur, abolition des pouls, paresthésies puis anesthésie et paralysie (ischémie menaçante) ; ischémie de stade III : déficit sensitivo-moteur, douleur à la mobilisation passive = urgence absolue.",
dx:"Échodoppler artériel en urgence ; angio-TDM des membres et de l'aorte (cause, terrains) ; ECG (fibrillation auriculaire), bilan de coagulation, ionogramme ; créatine phosphokinase (rhabdomyolyse) et lactates.",
t:"Héparinothérapie immédiate ; ischémie menaçante : revascularisation en urgence (embolectomie par sonde de Fogarty, thrombectomie, pontage) ; thrombolyse in situ dans certaines ischémies non immédiatement menaçantes ; syndrome de reperfusion : fasciotomie des loges, alcalinisation, surveillance de la rhabdomyolyse (insuffisance rénale) ; traitement de la cause (anticoagulation, cardioversion) ; amputation si nécrose étendue.",
k:"Membre blanc, froid et douloureux = héparine puis revascularisation : au-delà de 6 heures, le muscle necrose (rhabdomyolyse, syndrome des loges de reperfusion)."}
,
{n:"Dissection aortique aiguë (prise en charge médico-chirurgicale)",q:"dissection aortique",ur:true,
d:"Déchirure de l'intima aortique créant un faux chenal dans la média : dissection de type A (aorte ascendante — chirurgie en urgence) ou de type B (descendante — traitement médical, sauf complication) ; facteurs : HTA, bicuspidie, Marfan, grossesse, cocaïne.",
s:"Douleur thoracique ou dorsale brutale, en coup de poignard, migratrice (vers l'abdomen ou les jambes), migratrice et déchirante, maximale d'emblée ; asymétrie des pouls et des tensions aux deux bras, souffle diastolique (insuffisance aortique), déficits neurologiques ou ischémie d'un membre, syncopes ; forme hémorragique : choc (rupture).",
dx:"Angio-TDM aortique en urgence (flap intimal, faux chenal, extension) ou échocardiographie transœsophagienne ; ECG (éliminer un infarctus), NFS, D-dimères, troponine, créatinine ; radiographie du thorax (élargissement du médiastin) ; pas d'anticoagulation avant le diagnostic.",
t:"Contrôle tensionnel strict IV (bêtabloquant puis vasodilatateur — viser FC 60 et PAS 100-120, éviter la tachycardie et les à-coups tensionnels) ; antalgiques, calme ; type A : chirurgie urgente (remplacement de l'aorte ascendante) ; type B compliquée (ischémie viscérale, rupture, expansion) : endoprothèse thoracique ou chirurgie ; suivi à vie par imagerie et contrôle tensionnel.",
k:"Douleur thoracique migratrice et déchirante avec asymétrie des pouls = angio-TDM aortique immédiat ; type A = chirurgie en urgence ; jamais d'anticoagulation ni de thrombolyse avant d'avoir éliminé la dissection."}
,
{n:"Brûlures graves et étendues (syndrome du brûlé, sepsis sur brûlure)",q:"brûlures",ur:true,
d:"Brûlures cutanées graves : profondeur (2e degré profond, 3e degré) et étendue (surface corporelle brûlée) ; le syndrome du brûlé associe hypovolémie (exsudation massive), hypermétabolisme et risque infectieux majeur (la peau n'est plus une barrière) ; critères d'admission en centre de brûlés.",
s:"Douleur (2e degré superficiel), phlyctènes, plaques blanches ou carbonisées indolores (3e degré), œdème ; inhalation de fumées : brûlures du visage, voix rauque, suies, dyspnée (œdème laryngé, intoxication au CO et aux cyanures) ; choc hypovolémique des brûlures étendues ; sepsis tardif sur brûlure.",
dx:"Évaluation de la surface (règle des neuf, palme de la main = 1 %) et de la profondeur ; carboxyhémoglobine (intoxication au CO), lactates (cyanures), gaz du sang ; fibroscopie si suspicion d'inhalation ; surveiller la diurèse.",
t:"Sauvetage : dégagement, refroidissement des brûlures récentes (eau tempérée, jamais glacée), voies veineuses, réanimation hydro-électrolytique selon formule (Ringer lactate) ; voie aérienne (intubation si inhalation) ; pansements stériles, antalgie majeure (morphine), tétanos ; excision-greffe précoce des brûlures profondes en centre spécialisé ; nutrition hypercalorique, prévention du tétanos et de l'infection.",
k:"Brûlure du visage ou voix rauque = intubation précoce (l'œdème laryngé se majore) ; surface et profondeur commandent l'orientation vers un centre de brûlés ; refroidir tôt mais jamais avec de la glace."}
,
{n:"Fasciite nécrosante et gangrène gazeuse (urgences infectieuses nécrosantes)",q:"fasciite nécrosante",ur:true,
d:"Infections nécrosantes des tissus mous : fasciite nécrosante (streptocoque A, synergies microbiennes) et gangrène gazeuse (Clostridium perfringens : myonécrose avec gaz) ; terrain : diabète, immunodépression, plaie souillée ; mortalité élevée, sauvetage par le bloc opératoire.",
s:"Douleur disproportionnée aux signes cutanés, œdème tendu, chaleur, puis placard violacé, bulles, crépitation gazeuse, hypoesthésie (nécrose des nerfs), signes toxiques (fièvre, confusion, choc) ; gangrène gazeuse : douleur brutale, œdème, crépitation (le gaz n'est pas toujours visible d'emblée), sepsis fulminant.",
dx:"Clinique (douleur disproportionnée = signe cardinal) ; syndrome inflammatoire majeur, hyperleucocytose ; radiographie ou TDM (gaz dans les tissus) ; prélèvements per-opératoires ; score LRINEC d'aide ; le pronostic dépend de la précocité du geste, pas de l'imagerie.",
t:"Bloc opératoire en urgence : excision large de tous les tissus nécrotiques (fascia compris), réinterventions quotidiennes d'excision ; antibiothérapie IV à forte dose (amoxicilline ou pénicilline G + clindamycine + gentamicine selon protocoles) ; réanimation du choc septique ; oxygénothérapie hyperbare discutée (gangrène gazeuse) ; amputation si membre non sauvable.",
k:"Toute douleur des tissus mous disproportionnée à l'aspect cutané, chez un diabétique, = fasciite nécrosante jusqu'à preuve du contraire : bloc opératoire immédiat, l'excision large est le seul traitement."}
]}
]},

{id:"chir-aigu",num:2,name:"Pathologies Chirurgicales Aiguës & Loco-Régionales",groups:[
{name:"Affections Abdominales Aiguës Courantes",paths:[
{n:"Appendicite aiguë (simple, suppurée, gangréneuse)",q:"appendicite",ur:true,
d:"Inflammation de l'appendice, de la forme catarrhale (simple) à la suppuration et à la gangrène (risque de perforation et de péritonite) ; première cause d'abdomen aigu chirurgical entre 10 et 30 ans.",
s:"Douleur péri-ombilicale migrant en fosse iliaque droite (4-6 h), anorexie, nausées, fièvre modérée ; défense de McBurney, signes de Rovsing, du psoas ; formes : appendicite du sujet âgé (trompeuse, retard), appendicite pelvienne (diarrhée, faux besoins), rétro-cæcale (douleur lombaire) ; perforation : péritonite, masse (plastron appendiculaire).",
dx:"NFS-CRP, β-hCG ; échographie (surtout femme jeune) ou scanner (adulte) ; score d'Alvarado ; forme compliquée : abcès ou plastron au scanner.",
t:"Appendicectomie cœlioscopique avec antibioprophylaxie (le plus tôt est le mieux, avant perforation) ; plastron ou abcès : antibiothérapie ± drainage, appendicectomie différée (intervalle de 6-12 semaines) ; à jeun, antalgiques, prévention thrombo-embolique.",
k:"Anorexie + douleur migratrice de la fosse iliaque droite avec fièvre = appendicite : imagerie et chirurgie sans attendre, la gangrène perforée transforme le pronostic."}
,
{n:"Cholécystite aiguë lithiasique ou alithiasique",q:"cholécystite aiguë",ur:true,
d:"Inflammation de la vésicule biliaire par enclavement d'un calcul dans le col ou le canal cystique (lithiasique, la plus fréquente) ou sur terrain (alithiasique : soins intensifs, parentérale, brûlés) ; risque de perforation, de péritonite biliaire et d'empyème.",
s:"Douleur de l'hypochondre droit fébrile, nausées, vomissements, signe de Murphy positif (blocage inspiratoire à la palpation) ; ictère absent sauf migration (angiocholite associée) ; formes compliquées : empyème (masse fébrile), perforation (péritonite), formes du sujet âgé trompeuses.",
dx:"Échographie abdominale (paroi vésiculaire épaissie supérieure à 4 mm, calcul, épanchement péri-vésiculaire, Murphy échographique) ; NFS-CRP, bilan hépatique, lipase ; TDM si doute ; hémocultures si fièvre élevée.",
t:"Antibiothérapie IV (C3G ou amoxicilline-acide clavulanique selon protocoles), à jeun, antalgiques ; cholécystectomie précoce (dans les 72 premières heures, cœlioscopique) chez le patient stable ; cholécystectomie différée après antibiothérapie si terrain ou complications locales ; empyème ou échec : cholécystostomie percutanée ou chirurgie ; alithiasique : cholécystostomie de sauvetage.",
k:"Hypochondre droit fébrile + Murphy = cholécystite : échographie et cholécystectomie précoce (moins de 72 h) ; l'ictère ou la confusion y ajoutée fait craindre l'angiocholite."}
,
{n:"Angiocholite aiguë (infection des voies biliaires sur obstacle)",q:"angiocholite",ur:true,
d:"Cholangite aiguë : infection biliaire en amont d'un obstacle (calcul de la voie biliaire principale surtout, tumeur, sténose) ; urgence vitale : le pus sous pression dans les voies biliaires diffuse systémiquement (choc septique, CIVD, abcès hépatiques).",
s:"Triade de Charcot : douleur de l'hypochondre droit + fièvre avec frissons + ictère ; forme grave (pentade de Reynolds) : confusion et choc septique ; urines foncées, selles décolorées, prurit ; souvent sur lithiase connue ou après prothèse.",
dx:"Bilan hépatique (cholestase), NFS-CRP, hémocultures ; échographie (dilatation des voies biliaires, calcul) ; cholangio-IRM ou écho-endoscopie ; TDM si complication (abcès) ; le drainage ne doit pas attendre l'imagerie parfaite si choc.",
t:"Antibiothérapie IV à large spectre immédiate + drainage biliaire urgent en moins de 24 h (cholangio-pancréatographie rétrograde endoscopique avec sphinctérotomie et extraction des calculs, ou drainage percutané) ; réanimation du choc septique ; cholécystectomie dans le même séjour (lithiase) ; formes tumorales : prothèse ou dérivation.",
k:"Douleur + fièvre + ictère = angiocholite : antibiotiques ET drainage biliaire sous 24 h, l'un ne va pas sans l'autre."}
,
{n:"Pancréatite aiguë nécrotico-hémorragique (indication chirurgicale de drainage ou débridement)",q:"pancréatite aiguë nécrosante",ur:true,
d:"Forme grave de pancréatite aiguë (20 %) : nécrose pancréatique et péri-pancréatique, collections (pseudokystes, collection fermée encapsulée ou infectée) ; la nécrose infectée (fièvre + imagerie) impose le drainage ou le débridement ; causes : biliaire, alcoolique.",
s:"Épigastralgie transfixiante intense, vomissements, iléus ; défaillance d'organe (choc, insuffisance respiratoire, rénale) ; nécrose infectée : fièvre persistante après 7-10 jours, sepsis ; collections : masse épigastrique, nausées, ictère par compression.",
dx:"Lipasémie ; TDM avec injection à 72-96 h (quantification de la nécrose, collections) ; écho-endoscopie ou TDM de contrôle à 3-4 semaines (collections organisées) ; ponction guidée si suspicion d'infection (preuve bactériologique) ; CRP, NFS, hémocultures.",
t:"Phase aiguë : réanimation, jeûne, nutrition entérale (pas de débridement stérile) ; nécrose infectée : antibiothérapie à visée pancréatique (carbapénème, quinolone + métronidazole) et drainage (radiologique d'abord — dérivation gastrique ou transmurale, puis nécrosectomie différée de préférence après 4 semaines) ; pseudokystes symptomatiques : dérivation interne ; cholécystectomie à distance (origine biliaire).",
k:"Nécrose pancréatique stérile = pas de chirurgie (nutrition entérale et réanimation) ; nécrose infectée = drainage minimal invasif, idéalement différé au-delà de la 4e semaine."}
,
{n:"Hernies de la paroi abdominale étranglées (inguinale, ombilicale, crurale) et éventrations étranglées",q:"hernie étranglée",ur:true,
d:"Hernies de la paroi : inguinale (directe ou indirecte), crurale (femme âgée, risque d'étranglement élevé, contenu iléal souvent), ombilicale ; l'étranglement comprime le contenu (anse grêle, épiploon) : occlusion et souffrance digestive ; l'éventration étranglée est la complication des laparotomies.",
s:"Masse inguinale ou ombilicale douloureuse, tendue, irréductible, non expansive à la toux, avec occlusion (vomissements, arrêt du transit) et signes de souffrance (fièvre, défense, masse sensible) ; hernie crurale : tuméfaction sous-crurale douloureuse chez une femme âgée, occlusion parfois inaugurale.",
dx:"Examen clinique (masse irréductible) ; TDM (contenu herniaire, souffrance de l'anse, évaluation de l'occlusion) si doute ou chez l'obèse ; ionogramme, NFS ; jamais de tentative de réduction forcée en cas de signes de souffrance.",
t:"Chirurgie urgente (abord direct : libération du contenu, résection des anses nécrotiques, réparation par prothèse ou suture selon la contamination) ; antibiothérapie si résection digestive ; correction hydro-électrolytique en pré-opératoire ; hernies non compliquées : cure programmée (cœlioscopie, Lichtenstein) pour prévenir l'étranglement.",
k:"Hernie douloureuse irréductible = étranglement : chirurgie urgente, jamais de réduction forcée si fièvre ou défense ; la hernie crurale étrangle plus souvent et plus vite que l'inguinale."}
]},
{name:"Traumatismes des Membres & Orthopédie d'Urgence",paths:[
{n:"Fractures ouvertes des os longs (classification de Gustilo)",q:"fracture ouverte",ur:true,
d:"Fracture avec communication entre le foyer de fracture et l'extérieur (plaie) : contamination et risque d'infection osseuse (ostéite, ostéomyélite) ; classification de Gustilo : type I (plaie punctiforme, propre), II (plaie de moins de 2 cm sans écrasement), III (plaie extensive, écrasement, lésion vasculaire III C) — le type commande le traitement et le pronostic.",
s:"Plaie en regard d'une fracture, parfois saignement extériorisé, os visible ; déformation, douleur, impotence, crépitement ; lésions associées : vasculaires (ischémie du membre), nerveuses, syndrome des loges ; souillure (terre, vêtements), écrasement (Gustilo III).",
dx:"Radiographies orthogonales du segment ; évaluation vasculaire (pouls, doppler) et nerveuse ; photographie de la plaie (pas d'exploration répétée ni de palpation inutile) ; bilan pré-opératoire ; le type de Gustilo est déterminé au bloc.",
t:"Antibioprophylaxie IV précoce (C1G ou amoxicilline-acide clavulanique, ajout métronidazole et aminoside selon Gustilo et souillure) ; prévention du tétanos ; parage et lavage abondants au bloc en urgence, fixation (fixateur externe pour Gustilo III, enclouage possible dans certains cas I-II), couverture cutanée (suturé, plastie, lambeau) ; réparation vasculaire si Gustilo III C ; suites : consolidation surveillée, infection du matériel possible.",
k:"Toute fracture ouverte = antibiotiques dans l'heure, antitétanique, parage au bloc : chaque heure de retard augmente le risque d'ostéite ; ne jamais refermer d'emblée une plaie souillée."}
,
{n:"Fractures complexes articulaires et luxations irréductibles (hanche, genou, épaule, coude)",q:"fracture articulaire",ur:true,
d:"Fractures articulaires (déplacées, comminutives : tibia plateau, plateaux tibiaux, cotyle, radius distal, calcanéum) : l'objectif est la restitution anatomique de la surface articulaire (arthrose post-traumatique) ; luxations irréductibles ou associées à une fracture : urgence de réduction (ischémie, nerf).",
s:"Douleur, impotence, déformation, hémarthrose (genou) ; luxation de hanche : attitude vicieuse en flexion-rotation, inégalité de longueur, risque de sciatique ; luxation du genou : déformation majeure, ischémie poplitée à dépister absolument (pouls) ; épaule (réduction en urgence avant œdème) ; ouverture cutanée possible (fracture ouverte).",
dx:"Radiographies de face et profil (classifications) ; TDM pour les fractures articulaires complexes (fragment, déplacement) ; évaluation vasculaire et nerveuse (pouls, doppler à toute luxation du genou) ; TDM avant réduction des luxations cervicales.",
t:"Luxations : réduction en urgence sous sédation ou anesthésie (genou : réduction + artériographie si pouls anormaux, ischémie = chirurgie vasculaire) ; fractures articulaires déplacées : ostéosynthèse anatomique (plaque, vis) le plus souvent dans les 24-72 h, fixateur externe en attendant si lésions des tissus mous ; rééducation précoce, prévention de la raideur et de l'arthrose.",
k:"Toute luxation du genou = pouls poplités avant et après réduction (ischémie), toute luxation de hanche postérieure = tester le sciatique ; fracture articulaire déplacée = TDM et chirurgie anatomique."}
,
{n:"Syndrome des loges aigu (syndrome de Volkmann)",q:"syndrome des loges",ur:true,
d:"Hypertension dans une loge aponévrotique musculaire inextensible (traumatisme, fractures, écrasement, brûlures, ischémie reperfusion) : ischémie des muscles et des nerfs, définitive en quelques heures (rétraction ischémique de Volkmann : séquelles graves du membre).",
s:"Douleur disproportionnée, intense et progressive, majorée à l'étirement passif des muscles de la loge, résistante aux antalgiques ; loge dure et tendue à la palpation ; paresthésies puis anesthésie dans le territoire nerveux ; pouls souvent présents longtemps (le syndrome des loges précède l'oblitération artérielle) ; évolue vers la nécrose et la rétraction.",
dx:"Clinique (le diagnostic est clinique, la mesure de pression des loges est une aide) ; seuils : pression intralogue proche de la diastolique (delta inférieur à 30 mmHg) ; surveillance continue ; éliminer une lésion artérielle associée (doppler).",
t:"Aponévrotomie de sauvetage en urgence (incisions de décharge de toutes les loges atteintes, laissées ouvertes, fermeture ou greffe secondaire) ; traiter la cause (réduction de fracture, revascularisation) ; rhabdomyolyse : hydratation, alcalinisation, surveillance de la fonction rénale ; séquelles : chirurgie des rétractions, transferts.",
k:"Douleur disproportionnée et loge dure après un traumatisme = syndrome des loges : aponévrotomie immédiate, la présence des pouls ne rassure jamais."}
,
{n:"Traumatismes vasculaires des membres avec section artérielle",q:"traumatisme vasculaire",ur:true,
d:"Section, plaie ou contusion artérielle des membres (armes blanches, armes à feu, fractures déplacées — genou, coude, supracondylaire de l'enfant — luxations) : l'ischémie menace le membre (6 h) ; les faux anévrismes et fistules artério-veineuses sont les complications retardées.",
s:"Hémorragie externe (plaie hémorragique), hématome expansif et pulsatile, souffle ; signes d'ischémie : pâleur, absence de pouls, paresthésies, paralysie ; chez l'enfant : fracture supracondylienne avec abolition du pouls radial (spasme ou lésion humérale).",
dx:"Clinique (indice de suspicion des lésions osseuses) ; index de pression systolique abaissé ; angio-TDM (si stable) ou artériographie per-opératoire ; doppler ; pas d'imagerie si ischémie patente : bloc opératoire.",
t:"Hémostase provisoire : compression manuelle (pas de clampage aveugle), garrot si hémorragie massive incoercible ; exploration chirurgicale urgente : réparation (suture, patch, greffe veineuse ou prothétique), fasciotomie associée systématique en cas d'ischémie prolongée (reperfusion) ; revascularisation avant l'ostéosynthèse définitive si fracture déplacée ; anticoagulation et surveillance post-opératoire.",
k:"Absence de pouls après une fracture ou une luxation du genou/coude = exploration vasculaire urgente ; toujours fasciotomier après revascularisation prolongée."}
]},
{name:"Urgences Urologiques & Proctologiques",paths:[
{n:"Rétention Aiguë d'Urine (RAU) sur obstacle prostatique ou sténose urétrale",q:"rétention aiguë d'urine",ur:true,
d:"Impossibilité brutale d'uriner avec globe vésical : chez l'homme âgé (adénome prostatique, cancer, tumeur de vessie), sténose urétrale (suites d'instrumentation, IST), causes neurologiques ou médicamenteuses (anticholinergiques) ; la prolongée distend la vessie (atonie).",
s:"Douleur hypogastrique brutale avec envie impérieuse, globe vésical (soufflure sus-pubienne, matité), absence d'émission d'urine ; gêne, agitation ; fièvre si infection urinaire sur stagnation ; chez le sujet âgé, la rétention chronique est indolore (globe déclenché par un obstacle ou une infection).",
dx:"Clinique (matité sus-pubienne) ; échographie (globe, résidu, obstacle prostatique, calcul, tumeur) ; bandelette et ECBU (infection) ; créatinine et ionogramme si rétention prolongée ; toucher rectal (prostate) ; après sondage : débitmétrie et bilan urodynamique à distance.",
t:"Sondage vésical à demeure en urgence (sondage évacuateur progressif si rétention massive et ancienne : risque d'hémorragie et de déséquilibre — diurèse post-obstructive à surveiller) ; ECBU et antibiothérapie si infection ; traitement de la cause : α-bloquant et 5-alpha-réductase (adénome), résection endoscopique, sténose urétrale (dilatations, urétrotomie) ; arrêt des médicaments rétentionnants ; échec du sondage : cystofix ou cathéter sus-pubien.",
k:"Rétention aiguë d'urine = sondage évacuateur (lent si globe ancien) puis recherche de la cause : ne jamais laisser une vessie se distendre, ni sonder en force si urétrite à risque de fausse route."}
,
{n:"Priapisme aigu et traumatismes des organes génitaux externes",q:"priapisme",ur:true,
d:"Priapisme : érection douloureuse prolongée (plus de 4 h) non liée à l'excitation : ischémique (drépanocytose, injections intracaverneuses, médicaments — urgence, risque de dysfonction érectile définitive) ou non ischémique (post-traumatique, fistule artério-veineuse) ; traumatismes génitaux : fracture des corps caverneux, rupture urétrale, torsion testiculaire associée.",
s:"Priapisme ischémique : verge douloureuse et rigide, corpora caverneux durs et sensibles, gland mou ; drépanocytose ou injection récente ; fracture des corps caverneux : craquement audible lors du rapport avec érection, hématome en « aubergine », déviation ; rupture de l'urètre : méat ensanglanté, rétention, hématome périnéal.",
dx:"Priapisme : gaz du sang du sang caverneux (acidose = ischémique) ; échographie-doppler pénienne ; drépanocytose : NFS et réticulocytes ; rupture urétrale : urétrographie rétrograde avant tout sondage ; traumatisme testiculaire : échographie scrotale.",
t:"Priapisme ischémique : ponction-aspiration des corps caverneux avec lavage et injection d'agent alpha-mimétique (étiléfrine), en urgence urologique ; drépanocytose : hydratation, oxygène, échange transfusionnel si réfractaire ; shunt chirurgical au décours ; fracture des corps caverneux : chirurgie immédiate (suture) ; rupture urétrale : jamais de sondage forcé — cystostomie de décharge puis réparation (voie basse ou haute selon le siège).",
k:"Priapisme douloureux depuis plus de 4 h = urgence urologique : aspiration-lavage caverneux, la dysfonction érectile devient définitive au-delà de 24-48 h ; méat sanglant après un traumatisme pelvien = urétrographie, jamais de sonde à l'aveugle."}
,
{n:"Thrombose hémorroïdaire externe aiguë et abcès de la marge anale / phlegmon ischio-rectal",q:"thrombose hémorroïdaire",ur:true,
d:"Pathologies anales aiguës : thrombose hémorroïdaire externe (caillot dans une hémorroïde externe, douloureuse mais bénigne) ; abcès anal (fissure infectée, cryptite : abcès sous-cutané, ischio-rectal, intersphinctérien, pelvi-rectal) qui peut se compliquer de fasciite périnéale et dont le drainage peut révéler une maladie de Crohn ; la fistule anale est la complication chronique de l'abcès.",
s:"Thrombose externe : tuméfaction anodale violacée, dure et très douloureuse, apparition brutale, résolution en quelques jours-semaines ; abcès anal : douleur anale intense et battante, tuméfaction chaude, fièvre, rétention d'urines parfois ; ischio-rectal : douleur profonde fessière avec fièvre et masquage des signes locaux ; pas de rectorragies abondantes.",
dx:"Examen en position genu-pectorale (inspection et toucher rectal — douloureux) ; aucun examen ne doit retarder le drainage ; imagerie (IRM pelvienne, écho-endoscopie) pour les abcès profonds ou récidivants ; après drainage : recherche de maladie de Crohn (endoscopie à distance).",
t:"Thrombose externe récente (moins de 72 h) : excision ou incision-extraction du caillot, sinon antalgiques, topiques et repos ; abcès anal : drainage chirurgical en urgence (anesthésie, incision large, méchage, pas d'antibiothérapie systématique chez l'immunocompétent) ; antibiothérapie si cellulite, diabète, immunodépression ; traitement de la fistule secondaire (autres temps opératoires) ; dépistage Crohn et VIH si récidives.",
k:"Douleur anale brutale avec tuméfaction = thrombose si superficielle, abcès si fébrile : l'abcès anal se draine en urgence (le retard expose à la fasciite et à la fistule)."}
]}
]},

{id:"chir-reglee",num:3,name:"Chirurgie Viscérale, Digestive & Endocrinienne Réglée",groups:[
{name:"Paroi Abdominale & Hernies",paths:[
{n:"Hernies inguinales, ombilicales et spigéliennes non compliquées (plicature ou prothèse)",q:"hernie inguinale",
d:"Hernies de la paroi non compliquées : inguinale (oblique externe à travers l'orifice profond, directe à travers la paroi postérieure), ombilicale (congénitale ou acquise), spigélienne (ligne semi-lunaire, rare) ; le traitement est chirurgical, la cœlioscopie et les prothèses sans tension (Lichtenstein, TAPP, TEP) ont transformé la récupération.",
s:"Tuméfaction inguinale ou ombilicale réductible, augmentant à la toux et à l'effort, indolore ou gênante ; disparition en décubitus ; chez l'homme : descente dans la bourse ; complications possibles (étranglement) ; hernie de l'enfant (péritonéovaginale persistante) et de la femme (crurale).",
dx:"Examen clinique (masse réductible, expansivité à la toux) ; échographie en cas de doute diagnostic différentiel avec lymphadénopathie, lipome, varices) ; TDM des hernies atypiques ou de l'obèse ; pas d'examen systématique chez l'adulte typique.",
t:"Cure chirurgicale ambulatoire : voie cœlioscopique (TEP, TAPP) ou inguinale (Lichtenstein avec prothèse) selon le terrain et les habitudes ; ombilicale : suture ou prothèse ; enfant : fermeture simple du sac ; reprise d'une activité en quelques semaines ; abstention surveillée possible chez le sujet très âgé asymptomatique.",
k:"Toute hernie symptomatique se répare avant qu'elle ne s'étrangle ; la cure moderne est ambulatoire, sans tension, avec prothèse."}
,
{n:"Éventrations post-opératoires chroniques",q:"éventration",
d:"Déhiscence de la paroi abdominale après laparotomie (désunion aiguë ou dilatation progressive de l'orifice) : sac péritonéal couvert par la peau ; facteurs : obésité, diabète, infection du site opératoire, corticoïdes, toux chronique, dénutrition ; complications : étranglement, occlusion.",
s:"Tuméfaction pariétale réductible augmentant à l'effort (collier herniaire), gêne fonctionnelle, douleurs ; signes d'occlusion possible ; la paroi est déhiscente avec perte de la sangle musculaire (conséquences ventilatoires chez l'obèse et l'insuffisant respiratoire).",
dx:"Examen (orifice, contenu, réductibilité) ; TDM abdominale (cartographie des orifices, contenu, prise en charge) ; bilan nutritionnel et des comorbidités avant réparation ; évaluation des contre-indications (infection active, tabac, obésité majeure à corriger d'abord).",
t:"Réparation chirurgicale (laparoscopie ou laparotomie) : prothèse retromusculaire (Rives-Stoppa) ou intrapéritonéale, renfort biologique si contamination ; préparation : arrêt du tabac, perte de poids, kinésithérapie respiratoire préalable ; contentions et ceintures si abstention ; récidives possibles (10-20 %) selon le terrain.",
k:"Éventration = perte de la sangle abdominale : préparer le terrain (tabac, poids, respiration) avant la réparation par prothèse retromusculaire."}
]},
{name:"Hépatobiliaire & Pancréatique",paths:[
{n:"Lithiase biliaire symptomatique et indications de cholécystectomie (cœlioscopie)",q:"cholécystectomie",
d:"Cholélithiase (calculs de la vésicule) symptomatique : coliques hépatiques récidivantes ( indication formelle de cholécystectomie), cholécystite, pancréatite biliaire, angiocholite ; la cholécystectomie cœlioscopique est le traitement de référence (chirurgie la plus fréquente en France).",
s:"Colique hépatique : douleur brutale de l'hypochondre droit, en coup de poignard, irradiant à l'épaule, avec nausées, apyrétique, résolution en quelques heures ; calculs asymptomatiques : pas de traitement (sauf exceptions : porcelaine, calculs > 3 cm, patient greffé ou immunodéprimé).",
dx:"Échographie abdominale (calculs, paroi, dilatation des voies biliaires) ; bilan hépatique et lipase ; la colique hépatique est clinique : la douleur est brève, la cholécystite dure plus de 6 h avec fièvre.",
t:"Coliques hépatiques récidivantes : cholécystectomie cœlioscopique programmée ; après cholécystite : cholécystectomie précoce dans le même séjour ; après pancréatite biliaire : cholécystectomie avant la sortie (risque de récidive) ; dissolution ou lithotripsie : indications très limitées (refus de chirurgie) ; complications de la chirurgie : plaie de la voie biliaire principale (dépistage per-opératoire, cholangiographie).",
k:"Calculs asymptomatiques = abstention ; colique hépatique ou complication = cholécystectomie cœlioscopique, au mieux dans le même séjour après une complication."}
,
{n:"Kystes hydatiques du foie et abcès amibiens compliqués",q:"kyste hydatique du foie",ur:true,
d:"Kyste hydatique du foie : infection parasitaire à Echinococcus granulosus (chien-mouton, zones d'élevage) : kyste à paroi propre, contenu fille, risque de rupture (choc anaphylactique) ou de surinfection ; abcès amibien : Entamoeba histolytica (voyage tropical), volumineux abcès unique « pâte d'anchois ».",
s:"Kyste hydatique : douleurs de l'hypochondre droit, masse lisse, parfois allergie (urticaire) ; complications : rupture dans les voies biliaires (angiocholite, ictère), compression, infection ; abcès amibien : fièvre et douleur hépatique sans leucocytose majeure, évolution lente, amibiase colique associée possible.",
dx:"Échographie et TDM hépatique (kyste à paroi propre, calcifications, membranes, vésicules filles ; classification de Gharbi) ; sérologie hydatique (Elisa, Western blot) ; amibiase : sérologie amibienne et PCR, échographie/TDM (abcès unique, souvent lobe droit).",
t:"Kyste hydatique : chirurgie (résection du dôme saillant, périkystectomie) avec protection péri-opératoire (abords protégés, sérum salé hypertonique) et albendazole péri-opératoire (± PAIR : ponction-aspiration-injection-réaspiration dans les cas sélectionnés) ; abcès amibien : métronidazole (le plus souvent suffisant), drainage percutané des gros abcès ou des formes compliquées ; prévention : hygiène, lutte contre le cycle chien-mouton.",
k:"Kyste hépatique chez un patient d'élevage ou de zone d'endémie = hydatide : ne jamais ponctionner sans protocole (risque anaphylactique et dissémination) ; abcès amibien = métronidazole d'abord, drainage des formes menaçantes."}
,
{n:"Tumeurs bénignes et malignes du foie, des voies biliaires et du pancréas (duodénopancréatectomie céphalique)",q:"cancer du pancréas",
d:"Tumeurs hépatobiliaires et pancréatiques : hépatocarcinome (sur cirrhose), métastases hépatiques (colorectales surtout), cholangiocarcinome, tumeurs biliaires (Klatskin), adénocarcinome canalaire pancréatique (tête — ictère révélateur ; pronostic sévère) ; la duodénopancréatectomie céphalique (DPC, intervention de Whipple) est l'exérèse de référence des tumeurs de la tête.",
s:"Ictère cholestatique progressif et indolore (tête du pancréas, hile), douleurs épigastriques transfixiantes avec amaigrissement (cancer du pancréas), urines foncées, selles décolorées, prurit ; hépatocarcinome : décompensation décompensation de cirrhose, douleur de l'hypochondre droit, α-fœtoprotéine ; cholangiocarcinome : ictère fébrile.",
dx:"Bilan d'extension : TDM thoraco-abdomino-pelvien, IRM hépatique et cholangio-IRM ; marqueurs (ACE, CA 19-9, α-fœtoprotéine) ; biopsies échoguidées ou écho-endoscopie avec ponction ; évaluation de la réscabilité et de l'opérabilité (nutritionnel, âge, comorbidités) ; laparoscopie d'évaluation.",
t:"Chirurgie si réscécable : DPC (tête du pancréas), hépatectomie (tumeurs hépatiques), résection biliaire avec anastomose hépatico-jéjunale ; formes localement avancées : chimiothérapie (FOLFIRINOX, gemcitabine ± nab-paclitaxel), radiothérapie, soins de support ; ictère : drainage biliaire endoscopique (prothèse) ; douleur : neurolyse du plexus cœliaque ; hépatocarcinome : ablation percutanée, embolisation (TACE), immunothérapie selon le stade BCLC et le terrain.",
k:"Ictère progressif, indolore et amaigrissant chez un sujet de plus de 60 ans = cancer de la tête du pancréas jusqu'à preuve du contraire ; l'imagerie et le bilan d'extension décident de la résection (DPC) ou du traitement palliatif."}
]},
{name:"Tube Digestif & Oncologie Digestive",paths:[
{n:"Cancers du côlon et du rectum (colectomies segmentaires, résections rectales)",q:"cancer colorectal",
d:"Adénocarcinomes colorectaux (polypes dégénérés) : côlon droit (anémie), côlon gauche et rectum (troubles du transit, rectorragies) ; le dépistage par test immunologique et la coloscopie sauvent des vies ; la chirurgie segmentaire avec curage est le traitement curatif des formes localisées.",
s:"Anémie ferriprive (côlon droit), alternance diarrhée-constipation, rectorragies, faux besoins, amaigrissement, douleurs abdominales ; occlusion révélatrice (côlon gauche) ; contexte : antécédents familiaux, polypose, MICI, âge supérieur à 50 ans.",
dx:"Coloscopie totale avec biopsies (et repérage tatouage) ; TDM thoraco-abdomino-pelvien (extension, métastases hépatiques) ; ACE (suivi) ; IRM rectale (stade, marge, statut ganglionnaire) ; réunion de concertation pluridisciplinaire.",
t:"Chirurgie : colectomie segmentaire avec curage (hémicolectomie droite ou gauche, résection sigmoïdienne) cœlioscopique dans la majorité des cas ; cancer du rectum : radiochimiothérapie néoadjuvante des formes localement avancées puis exérèse totale du mésorectum (avec conservation sphinctérienne si possible) ; chimiothérapie adjuvante (stades III) ; métastases hépatiques résécables : résections en un ou deux temps ; dépistage (test immunologique tous les 2 ans de 50 à 74 ans) et coloscopie.",
k:"Anémie ferriprive inexpliquée après 50 ans = coloscopie ; le dépistage organisé et la chirurgie des formes localisées guérissent plus de la moitié des cancers colorectaux."}
,
{n:"Diverticulose colique sigmoïdienne (sigmoïdectomie de propreté)",q:"diverticulose",
d:"Diverticulose colique (hernies de la muqueuse au point de pénétration vasculaire, sigmoïde surtout) : asymptomatique dans 80 % ; complications : poussées de diverticulite, hémorragie, abcès, fistule, péritonite, sténose ; la sigmoïdectomie dite « de propreté » est proposée après complications récidivantes.",
s:"Poussées : douleur de la fosse iliaque gauche, fièvre, troubles du transit ; hémorragie diverticulaire : rectorragies rouge vif abondantes et indolores (artère perforée) ; complications : masse (abcès), pneumaturie (fistule colovésicale) ; après une première poussée simple, le risque de récidive augmente.",
dx:"TDM abdomino-pelvien (poussées : classification de Hinchey pour les compliquées) ; coloscopie après refroidissement (éliminer un cancer, jamais en phase aiguë : risque de perforation) ; NFS, CRP ; hémorragie : coloscopie en urgence si besoin.",
t:"Poussée simple : antalgiques, ± antibiotiques, régime ; abcès : drainage (radiologique) et antibiothérapie ; péritonite : chirurgie (sigmoïdectomie avec ou sans rétablissement immédiat, selon la contamination) ; sigmoïdectomie programmée (cœlioscopique) après 2 poussées ou complication (jeune, immunodéprimé) ; hémorragie : transfusion, coloscopie, embolisation (rarement colectomie) ; régime riche en fibres en prévention.",
k:"Rectorragies abondantes rouges chez un sujet de plus de 50 ans porteur d'une diverticulose = hémorragie diverticulaire : réanimation puis coloscopie ; sigmoïdectomie programmée après plusieurs poussées."}
,
{n:"Pathologies de l'œsophage (achalasie, reflux sévère) et cancers gastriques (gastrectomies)",q:"cancer de l'estomac",
d:"Pathologies chirurgicales de l'œsophage et de l'estomac : achalasie (défaut de relaxation du cardia : dysphagie paroxystique, régurgitations, dilatation œsophagienne), reflux gastro-œsophagien sévère avec hernie hiatale volumineuse, adénocarcinome gastrique (surtout antro-pylorique, lymphome MALT), cancer de l'œsophage.",
s:"Achalasie : dysphagie paradoxale (liquides plus difficile que solides au début), régurgitations alimentaires, perte de poids, douleurs rétrosternales ; cancer gastrique : épigastralgies atypiques, anorexie, amaigrissement, anémie, dysphagie (œsophage) ; hémorragie ou perforation inaugurales possibles.",
dx:"FOGD avec biopsies (tumeurs, gastrite, H. pylori) ; transit œso-gastro-duodénal et manométrie (achalasie) ; TDM thoraco-abdomino-pelvien (extension), écho-endoscopie (profondeur, ganglions) ; recherche d'H. pylori.",
t:"Achalasie : dilatation pneumatique endoscopique ou myotomie chirurgicale (Heller) ± fundoplicature ; reflux sévère : fundoplicature (Nissen) ; cancer gastrique : gastrectomie totale ou des deux tiers (D2, avec curage) ± chimiothérapie péri-opératoire ; œsophage : œsophagectomie (thoracique ou transhiatale) après radio-chimiothérapie selon les protocoles ; H. pylori : éradication (prévention du cancer gastrique et du lymphome MALT) ; soins de support et nutrition.",
k:"Épigastralgies atypiques avec anorexie et anémie après 50 ans = FOGD avec biopsies : l'éradication de H. pylori prévient le cancer gastrique."}
]},
{name:"Chirurgie Endocrinienne",paths:[
{n:"Goitres multinodulaires toxiques ou compressifs et cancers de la thyroïde (thyroïdectomie totale)",q:"thyroïdectomie",
d:"Chirurgie thyroïdienne : goitres multinodulaires (compressifs : dysphagie, dyspnée, plongement rétro-sternal, ou toxiques) et cancers thyroïdiens (papillaire le plus fréquent, vésiculaire, médullaire) ; la thyroïdectomie totale est l'intervention de référence, avec repérage des nerfs récurrents et des parathyroïdes.",
s:"Goitre : masse cervicale antérieure, bascule à la déglutition, signes compressifs (dyspnée, dysphagie, gêne au décubitus, signe de Pemberton), hyperthyroïdie (goitre toxique) ; cancer : nodule dur, adénopathie cervicale, dysphonie (nerf récurrent) ; contexte d'irradiation cervicale ou familial (médullaire : NEM2).",
dx:"TSH, calcitonine (médullaire) ; échographie thyroïdienne avec classification EU-TIRADS et cytoponction des nodules suspects (Bethesda) ; scanner du thorax (extension rétro-sternale) ; laryngoscopie pré-opératoire (mobilité des cordes).",
t:"Goitre compressif ou toxique : thyroïdectomie totale (ou subtotale) ; cancer différencié : thyroïdectomie totale ± curage central et latéral, puis irathérapie et hormonothérapie suppressive selon le risque ; médullaire : thyroïdectomie avec curage extensif et génétique (RET) ; complications de la chirurgie : hypoparathyroïdie (calcium, vitamine D), paralysie récurrentielle (dysphonie), hématome compressif (urgence) ; suivi : thyroglobuline, échographie.",
k:"Nodule thyroïdien dur ou adénopathie cervicale = échographie et cytoponction (EU-TIRADS) avant toute chirurgie ; après thyroïdectomie totale : surveiller calcémie (hypoparathyroïdie) et voix (récurrent)."}
,
{n:"Hyperparathyroïdies primaires et secondaires (parathyroïdectomie)",q:"parathyroïdectomie",
d:"Chirurgie parathyroïdienne : hyperparathyroïdie primaire (adénome unique dans 85 %, hyperplasie des quatre glandes) avec hypercalcémie ; secondaire (insuffisance rénale chronique : hyperplasie des quatre glandes sur hypocalcémie chronique) ou tertiaire (autonomie sur parathyroïde de l'insuffisant rénal) ; la parathyroïdectomie est curative dans la forme primaire.",
s:"Primaire : « pierres, os, douleurs abdominales, confusions » — lithiases rénales, ostéoporose, ulcères, troubles psychiques ; formes asymptomatiques découvertes au bilan ; secondaire : calcifications, prurit, ostéodystrophie rénale, hyperparathyroïdie réfractaire du dialysé.",
dx:"Calcémie élevée avec PTH inadaptée (primaire) ; phosphorémie, calciurie, vitamine D ; localisation : échographie cervicale et scintigraphie au MIBI (double localisation avant chirurgie) ; ostéodensitométrie ; secondaire : PTH très élevée du dialysé, bilan phospho-calcique.",
t:"Primaire : parathyroïdectomie ciblée (adénome repéré) ou exploration des quatre glandes selon l'imagerie et le contexte (forme familiale, NEM) ; chirurgie ambulatoire, surveillance de la calcémie post-opératoire (hypocalcémie « de la faim osseuse ») ; formes asymptomatiques répondant à des critères : chirurgie ou surveillance ; secondaire réfractaire : parathyroïdectomie subtotale ou totale avec autogreffe ; traitement médical (calcimimétiques) alternative.",
k:"Hypercalcémie + PTH non freinée = hyperparathyroïdie primaire : localiser l'adénome (échographie + MIBI) avant la parathyroïdectomie ciblée ; surveiller la calcémie post-opératoire (hypocalcémie de la faim osseuse)."}
]}
]},

{id:"chir-ortho",num:4,name:"Chirurgie Orthopédique, Traumatologique & Rachidienne Réglée",groups:[
{name:"Pathologies Dégénératives & Articulaires",paths:[
{n:"Arthrose de la hanche (coxarthrose) et du genou (gonarthrose) — Indications de prothèses totales de hanche (PTH) et de genou (PTG)",q:"arthrose de la hanche",
d:"Arthrose symptomatique invalidante de la hanche (coxarthrose primitive ou secondaire : dysplasie, épiphysiolyse, nécrose de la tête fémorale, séquelle de fracture) et du genou (gonarthrose fémoro-tibiale ou fémoro-patellaire) ; les prothèses totales de hanche et de genou sont les interventions qui transforment le plus la qualité de vie.",
s:"Douleur mécanique de l'aine irradiant à la cuisse et au genou (coxarthrose), douleur du genou à la marche et aux escaliers, décharge en boitant, raideur matinale brève, réveils nocturnes par changement de position ; limitation du périmètre de marche, impotence fonctionnelle, retentissement sur la qualité de vie.",
dx:"Radiographies standard de hanche et genou debout (pincement, ostéophytes, géodes) ; bilan pré-opératoire : radios en charge pour la planification, évaluation du capital osseux et ligamentaire ; éliminer une cause inflammatoire ou septique.",
t:"Traitement conservateur d'abord : perte de poids, kinésithérapie, antalgiques, AINS, infiltrations, viscosupplémentation (genou) ; arthrose invalidante résistante : arthroplastie totale (PTH — par voie antérieure mini-invasive ou postérieure — ou PTG), rééducation immédiate, prévention de la thrombose ; prothèse unicompartimentale du genou dans certains cas ; la durée de vie des prothèses (20-25 ans) fait temporiser chez le sujet jeune.",
k:"Coxarthrose = douleur de l'aine et non de la fesse ; prothèse quand la douleur invalidante résiste au traitement conservateur — le timing dépend de l'âge et de l'activité."}
,
{n:"Pathologies de l'épaule (rupture de la coiffe des rotateurs, instabilité récidivante)",q:"rupture de la coiffe des rotateurs",
d:"Pathologies de l'épaule : rupture de la coiffe des rotateurs (sus-épineux surtout : dégénérative après 50 ans ou traumatique), épaule gelée (capsulite rétractile), instabilité récidivante (luxations antérieures répétées du jeune sportif, lésion de Bankart), arthrose acromio-claviculaire et omarthrose.",
s:"Rupture de coiffe : douleur nocturne (couché sur l'épaule), impossibilité de lever le bras ou de s'habiller, faiblesse à l'abduction et à la rotation externe, signe du coin de table ; instabilité : épisodes de luxation récidivants, appréhension en abduction-rotation externe ; épaule gelée : raideur douloureuse progressive dans toutes les directions.",
dx:"Examen clinique orienté (tests de coiffe, craquements, recherche d'instabilité et d'appréhension) ; radiographies standard ; échographie et IRM de l'épaule (rupture, rétraction, dégénérescence graisseuse) ; arthroscanner dans l'instabilité (lésion osseuse de Bankart, encoche).",
t:"Ruptures partielles ou vieilles du sujet âgé : rééducation kinésithérapie, antalgiques, infiltration (résultats souvent suffisants) ; rupture invalidante du sujet actif : réparation arthroscopique (réinsertion tendineuse), protection de la rééducation ; instabilité récidivante : rééducation d'abord, puis intervention de stabilisation (Bankart arthroscopique ou butée de Latarjet) ; épaule gelée : kinésithérapie douce et patience (guérison en 12-24 mois), arthrolyse dans les formes rétractées.",
k:"Douleur nocturne de l'épaule après 50 ans + impossibilité de lever le bras = rupture de coiffe (échographie-IRM) ; luxation récidivante du jeune sportif = stabilisation chirurgicale."}
,
{n:"Lésions méniscales et ligamentaires du genou (rupture du ligament croisé antérieur - LCA)",q:"rupture du ligament croisé antérieur",
d:"Lésions du genou du sportif et du sujet âgé : rupture du ligament croisé antérieur (pivots, entorses en valgus-rotation), lésions méniscales (cliquetis, blocages ; ménisque interne du sujet âgé dégénératif, lésion en anse de seau du jeune), ruptures du LCP ou des ligaments latéraux, entorses graves.",
s:"Entorse avec œdème rapide (hémarthrose : genou gonflé en quelques heures), impotence, sensation de déchirure ; instabilité en pivot (le genou « lâche » dans les changements de direction) ; blocage vrai (lésion méniscale en anse de seau) ; pseudo-blocages et douleurs en flexion (lésions méniscales).",
dx:"Examen clinique : tests de Lachman (le plus sensible), tiroir antérieur, pivot shift ; palpation des interlignes (ménisques) ; radiographies (arrachements, fractures, pièces détachées) ; IRM du genou (ligaments, ménisques, lésions osseuses) ; ponction d'une hémarthrose en cas de doute.",
t:"Entorse récente : protocole RICE (repos, glace, compression, élévation), immobilisation courte et antalgiques ; LCA rompu du sportif (pivot) : ligamentoplastie (préparation musculaire préalable, greffe : DIDT ou Kenneth-Jones) ; sujet sédentaire plus âgé : rééducation et renforcement musculaires ; méniscectomie partielle arthroscopique limitée (plus le ménisque est préservé, mieux c'est — sutures méniscales du jeune) ; prévention des entorses : proprioception.",
k:"Hémarthrose du genou après un sport de pivot = rupture du LCA jusqu'à preuve du contraire (Lachman) ; préserver le ménisque (sutures du jeune, méniscectomie la plus limitée possible) pour protéger le cartilage."}
]},
{name:"Traumatologie Séquellaire & Rachis",paths:[
{n:"Pseudarthroses et cals vicieux osseux",q:"pseudarthrose",
d:"Pseudarthrose : absence de consolidation d'une fracture après 6 mois (hypertrophique : bonne vascularisation, stabilité insuffisante ; atrophique : perte de substance ou vascularisation compromise) ; cal vicieux : consolidation en mauvaise position (angulation, rotation, raccourcissement) avec retentissement fonctionnel et articulaire.",
s:"Douleurs mécaniques persistantes au foyer de fracture, mobilité anormale, impossibilité d'appui, déformation (cal vicieux), raideur et retentissement sur les articulations voisines (surcharge, arthrose secondaire) ; la pseudarthrose infectée (ostéite) saigne et suppure parfois.",
dx:"Radiographies standard et comparatives (traversée du foyer par les travées osseuses = consolidation) ; TDM (pseudarthrose, cals vicieux complexes) ; scintigraphie ou IRM (infection, vitalité) ; bilan biologique (CRP si suspicion d'infection du matériel).",
t:"Pseudarthrose hypertrophique : stabilisation mécanique (plaque, enclouage, décortication de Judet avec greffe spongieuse) ; atrophique : greffe osseuse (spongieuse, vascularisée) et ostéosynthèse stable ; infection : ablation ou changement du matériel, antibiotiques prolongés (selon protocoles) ; cal vicieux : ostéotomie corrective ; cals vicieux tolérés du sujet âgé : adaptation et rééducation ; prévention : réduction anatomique, stabilité, protection de la vascularisation et de la peau.",
k:"Douleur persistante et mobilité anormale 6 mois après une fracture = pseudarthrose : stabiliser, greffer, et toujours éliminer une infection (matériel, CRP)."}
,
{n:"Hernies discales lombaires et cervicales (discectomies, arthrodèses)",q:"hernie discale",
d:"Protrusion ou exclusion du disque intervertébral (lombaire L4-L5 et L5-S1 surtout ; cervicales C5-C6 et C6-C7) comprimant une racine : sciatique ou névralgie cervico-brachiale ; la chirurgie (discectomie) est réservée aux échecs du traitement médical, aux déficits et aux urgences (queue de cheval).",
s:"Lombalgie aiguë puis douleur radiculaire (sciatique L5 ou S1), majorée par la toux et la défécation, attitude antalgique inclinaison, Lasègue positif ; déficit moteur ou abolition d'un réflexe ; syndrome de la queue de cheval (anesthésie en selle, troubles sphinctériens) = urgence absolue ; cervicale : douleur du membre supérieur selon le territoire.",
dx:"Examen neurologique complet (moteur, sensitif, réflexes, sphincters) ; IRM rachidienne (hernie, compression, sténose) ; radiographies (discopathie, instabilité) ; électromyogramme si ancien doute ; jamais de scanner avant avis si queue de cheval suspectée cliniquement (l'IRM et la chirurgie sont urgentes).",
t:"Traitement médical 6 à 8 semaines (antalgiques, AINS, kinésithérapie, maintien de l'activité) : la plupart des hernies guérissent ; chirurgie : discectomie (microchirurgicale ou endoscopique) si sciatique hyperalgique résistante, déficit moteur, ou récidivante ; queue de cheval : discectomie en urgence ; cervicales : discectomie avec arthrodèse (greffe et plaque) ou remplacement discal ; rééducation post-opératoire.",
k:"Sciatique déficitaire ou hyperalgique résistante 6-8 semaines = discectomie ; anesthésie en selle + troubles sphinctériens = queue de cheval = chirurgie en urgence."}
,
{n:"Canal lombaire étroit (sténose canalaire) symptomatique",q:"canal lombaire étroit",
d:"Rétrécissement du canal lombaire (dégénératif : hypertrophie articulaire et ligamentaire, spondylolisthesis, constitutionnel) comprimant les racines de la queue de cheval : claudication neurologique des membres inférieurs, du sujet de plus de 60 ans ; à distinguer de la claudication artérielle.",
s:"Douleurs et lourdeurs des jambes déclenchées par la marche et la station debout, soulagées par la flexion (position penchée en avant, caddie de supermarché : signe du caddie), claudication à distance variable, paresthésies ; lombalgie associée ; examen au repos souvent normal ; formes graves : déficits, troubles sphinctériens (rares).",
dx:"IRM lombaire (sténose, niveaux, spondylolisthesis) ; examen vasculaire (pouls, IPS : éliminer l'artérite et les associations) ; électromyogramme si doute ; retentissement fonctionnel (périmètre de marche, échelle).",
t:"Traitement médical d'abord : kinésithérapie (assouplissement en flexion), antalgiques, infiltrations épidurales, adaptation (vélo, marche penchée) ; formes invalidantes résistantes : décompression chirurgicale (laminectomie, laminotomie) ± arthrodèse si instabilité ou spondylolisthesis ; rééducation post-opératoire ; régression souvent incomplète des symptômes anciens.",
k:"Claudication des jambes soulagée penché en avant ou assis = canal lombaire étroit (le caddie soulage) ; l'IPS et les pouls vérifient l'absence d'artériopathie associée."}
]}
]},

{id:"chir-plast",num:5,name:"Chirurgie Plastique, Reconstructrice, Vasculaire Périphérique & Petite Chirurgie",groups:[
{name:"Chirurgie Vasculaire Périphérique",paths:[
{n:"Artériopathie Oblitérante des Membres Inférieurs (AOMI) — pontages artériels, endartériectomies",q:"pontage artériel",ur:true,
d:"Revascularisation de l'AOMI au stade de claudication sévère ou d'ischémie critique : pontages (veine saphène inversée ou in situ, prothèse) et techniques endovasculaires (angioplastie-stent, endartériectomie fémorale profonde, athérectomie) ; le choix dépend des lésions et du terrain ; le pronostic global reste dominé par le risque cardiovasculaire.",
s:"Claudication invalidante (< 200-300 m) ou ischémie critique (douleur de repos, ulcères, gangrène, IPS < 0,4) ; absence de pouls, plaies chroniques ; terrain : tabac, diabète, insuffisance rénale, coronaropathie associée fréquente.",
dx:"IPS, échodoppler artériel complet ; angio-TDM ou angio-IRM (cartographie pré-opératoire : lit d'aval, veine saphène) ; artériographie (diagnostique et thérapeutique) ; bilan cardiaque avant chirurgie (coronaropathie silencieuse) ; évaluation du risque anesthésique.",
t:"Optimisation médicale : arrêt du tabac, statine, antiagrégant, IEC, contrôle du diabète, réadaptation à la marche ; revascularisation : endovasculaire d'abord dans la plupart des lésions courtes, pontage (fémoro-poplité ou distal, veine saphène) pour les lésions longues et l'ischémie critique ; endartériectomie (fémorale superficielle, carotide) ; soins des plaies ischémiques (débridement, pansements) ; amputation mineure ou majeure si membre non sauvable ; suivi duplex des pontages.",
k:"Ischémie critique = revascularisation rapide (pontage ou endoluminal) : chaque semaine compte pour le sauvetage de membre ; le traitement médical du risque cardiovasculaire prolonge la survie au-delà du membre."}
,
{n:"Varices des membres inférieurs (safénectomie, traitement endovasculaire)",q:"varices",
d:"Incontinence des veines superficielles (saphène interne ou externe, perforantes) : varices primaires (terrain, hérédité) ou secondaires (syndrome post-thrombotique) ; complications : œdème, hypodermite, eczéma variqueux, ulcère variqueux, hémorragie, thrombophlébite superficielle ; les traitements endovasculaires dominent aujourd'hui.",
s:"Dilatations veineuses visibles, lourdeurs et œdèmes vespéraux, douleurs, démangeaisons ; signes d'insuffisance veineuse chronique (classification CEAP) : hypodermite ocre, dermite ocre, eczéma, atrophie blanche, lipodermatosclérose, ulcère sus-malléolaire interne ; hémorragie sur rupture de varice ; cordons douloureux (thrombophlébite superficielle).",
dx:"Échodoppler veineux complet debout (reflux saphènes, perforantes, perméabilité profonde — indispensable avant tout traitement) ; classification CEAP ; éliminer une obstruction profonde (post-thrombotique) ; circonstances (estrogènes, grossesse).",
t:"Mesures physiques : compression élastique (bas) et phlébotoniques (symptômes) ; traitement radical des reflux : techniques endoveineuses thermiques (laser, radiofréquence) ou chimiques (mousse sclérosante écho-guidée), phlébectomies associées ; safénectomie chirurgicale (stripping) dans certains cas ; thrombophlébite superficielle saphène : anticoagulation (proche d'une profonde) ; ulcère variqueux : compression (traitement majeur), pansements, greffe si besoin.",
k:"Avant tout traitement de varices : échodoppler debout à la recherche du reflux (saphène et perforantes) ; l'ulcère variqueux guérit par la compression, pas par les pansements seuls."}
,
{n:"Fistules artério-veineuses pour hémodialyse chronique",q:"fistule artério-veineuse",
d:"Abord vasculaire pour l'hémodialyse chronique : fistule artério-veineuse native (radio-céphalique de Cimino-Brescia au poignet, huméro-céphalique au bras — la mieux tolérée et la plus durable) ou prothétique (PTFE) si veines épuisées ; la création précède le début de la dialyse (maturation 4-8 semaines).",
s:"Maturation de la fistule : vibration (frémissement) et souffle continus, veine dilatée et artérialisée à partir de 4 semaines ; complications : non-maturation, sténose (diminution du frémissement, mauvais débit), thrombose (urgence), anévrisme, vol ischémique de la main (froid, douleurs, ulcères), infection (surtout prothèses).",
dx:"Examen clinique de la fistule avant chaque dialyse (frémissement, souffle, hémostase) ; surveillance du débit (mesure dilutionnelle) et de la pression veineuse ; échodoppler des fistules à problème ; fistulographie (sténoses) et angioplastie.",
t:"Préserver le capital veineux des insuffisants rénaux dès le diagnostic (pas de perfusions ni de prélèvements au bras non dominant, éviter les cathéters centraux) ; création de la fistule native (chirurgie sous anesthésie locale) 4-8 semaines avant la dialyse attendue ; complications : angioplastie des sténoses, thrombectomie urgente de la thrombose, ligature ou revascularisation du vol ischémique ; prothèse si pas de veine ; éducation du patient (autosurveillance du frémissement).",
k:"Insuffisant rénal : préserver les veines des avant-bras dès le début (bras non dominant) et créer la fistule native AVANT la première dialyse ; disparition du frémissement = thrombose = urgence."}
]},
{name:"Chirurgie Plastique & Dermatologique",paths:[
{n:"Exérèse de tumeurs cutanées bénignes (lipomes, kystes sébacés) et malignes (carcinomes, mélanomes) avec marges et reconstruction",q:"mélanome",ur:true,
d:"Chirurgie cutanée : tumeurs bénignes (lipomes, kystes épidermoïdes ou sébacés, naevus) et malignes — carcinome basocellulaire (le plus fréquent, localement invasif), carcinome spinocellulaire, mélanome (potentiel métastatique, pronostic lié à l'indice de Breslow) ; l'exérèse avec marges saines et la reconstruction (suture, plastie, greffe, lambeau) font partie du même temps opératoire.",
s:"Lésion cutanée qui grandit, change d'aspect, saigne, démange ; mélanome : critères ABCDE (Asymétrie, Bord irrégulier, Couleur non homogène, Diamètre supérieur à 6 mm, Évolution) ; basocellulaire : nodule translucide à bordures perlées avec télangiectasies (visage) ; spinocellulaire : croûte ou ulceration (dos des mains, lèvres) ; lipome et kyste : tuméfaction mobile et indolore.",
dx:"Examen de toute la peau (et des aires ganglionnaires) ; dermoscopie ; biopsie-exérèse (mélanome suspecté : exérèse complète première avec marge de sécurité) ; lésion fixée ou ulcérée : biopsie ; pour le mélanome : Breslow (épaisseur), ulcération, mitoses, recherche du ganglion sentinelle si Breslow > 0,8 mm ; imagerie selon le stade.",
t:"Exérèse avec marges adaptées à l'histologie (mélanome : marges selon Breslow, 0,5 à 2 cm ; basocellulaire : 3-5 mm) ; reconstruction : suture directe, plastie locale, greffe ou lambeau ; ganglion sentinelle du mélanome (> 0,8 mm) ; formes avancées : immunothérapie et thérapies ciblées (BRAF) du mélanome, chirurgie et radiothérapie des carcinomes ; bénignes : exérèse simple ; photoprotection et surveillance dermatologique.",
k:"Toute lésion cutanée qui change (ABCDE) = consultation rapide : le pronostic du mélanome dépend de son épaisseur au moment de l'exérèse — un mélanome fin est guéri par la chirurgie."}
,
{n:"Prise en charge chirurgicale des escarres de décubitus (lambeaux cutanés)",q:"escarre",
d:"Nécrose cutanée ischémique par pression prolongée (sujets immobilisés, spinal, soins intensifs) : sacrum, talons, ischions, occiput ; stades I (érythème) à IV (atteinte osseuse et musculaire) ; la prise en charge est pluridisciplinaire, la chirurgie (excision et lambeau musculo-cutané) ne venant qu'après l'optimisation de tous les facteurs.",
s:"Placard d'appui : érythème ne blanchissant pas (stade I), phlyctène ou abrasion (II), perte de substance jusqu'au fascia (III), nécrose étendue à l'os (IV) ; fièvre et infection des tissus mous, ostéite sous-jacente ; dénutrition, incontinence, immobilité : les facteurs à corriger avant toute chirurgie.",
dx:"Examen complet des zones d'appui ; bilan nutritionnel (albumine, préalbumine) ; imagerie si ostéite (IRM, scintigraphie) et prélèvements ; évaluation des capacités de rééducation et du projet de soins.",
t:"Prévention d'abord (c'est la clé) : changements de position toutes les 2-3 h, supports de décharge (matelas, coussins), soins de peau, nutrition, traitement de l'incontinence ; débridement des nécroses, pansements avancés (hydrocolloïdes, alginates), pression négative ; chirurgie (excision-suture ou lambeau musculo-cutané de couverture) : uniquement après stabilisation nutritionnelle et engagement de la décharge post-opératoire ; ostéite : antibiothérapie prolongée ; rééducation.",
k:"L'escarre est un marqueur de qualité des soins : prévention (décharge et nutrition) avant tout ; le lambeau n'est jamais la première mesure, et sans décharge post-opératoire, il échoue."}
,
{n:"Réparation des pertes de substance cutanée post-traumatiques ou post-infectieuses",q:"greffe de peau",
d:"Couverture des pertes de substance cutanée : post-traumatiques (délabrements, avulsions, brûlures) ou post-infectieuses (fasciites nécrosantes, abcès étendus) ; l'arsenal : cicatrisation dirigée, suture, greffe de peau mince ou totale, substituts dermiques, lambeaux locaux, régionaux ou libres (microchirurgie) ; le choix dépend du lit, des tissus exposés et de la zone.",
s:"Perte de substance avec exposition possible de tendons, os, articulations ou matériel (le tissu noble interdit la greffe simple) ; plaies chroniques infectées (débridement répétés) ; contexte traumatique (mains, membres inférieurs, visage) ou septique ; l'état local (infection, œdème) conditionne le timing.",
dx:"Bilan de la perte de substance (taille, profondeur, tissus exposés, vascularisation — doppler des lambeaux) ; prélèvements bactériologiques ; bilan de l'état général et des comorbidités (tabac, diabète : facteurs d'échec) ; radiographies si corps étranger ou fracture associée.",
t:"Parage et détersion (chirurgicale, hydrosurgique) de tout tissu dévitalisé ; couverture par greffe de peau mince (lit bien vascularisé) ou totale (zones exposées : mains, visage) ; substituts dermiques et matrices dans les plaies complexes ; lambeaux locaux ou régionaux si tendon, os ou matériel exposés ; lambeaux libres micro-anastomosés pour les grandes pertes de substance ; pansement à pression négative en préparation ; rééducation et prévention des rétractions ; arrêt du tabac avant tout geste.",
k:"Tendon, os ou matériel exposé = pas de greffe simple : il faut du tissu vascularisé (lambeau) ; débrider large dans l'infection, couvrir une fois la plaie propre."}
]}
]}
]});


/* ============================================================
   DÉPARTEMENT 5 — NEUROPSYCHIATRIE (Neurologie & Psychiatrie)
   ============================================================ */
DEPTS.push({
id:"neuro",name:"Neuropsychiatrie (Neurologie & Psychiatrie)",icon:"🧠",color:"#6366f1",
desc:"Urgences neurologiques et psychiatriques, maladies neurodégénératives et neuromusculaires, psychiatrie générale et addictologie : le système nerveux et la psychiatrie de l'adulte.",
specs:[

{id:"neuro-urg",num:1,name:"Urgences Neurologiques & Psychiatriques Aiguës",groups:[
{name:"Urgences Vasculaires & Ischémiques Cérébrales",paths:[
{n:"Accident Vasculaire Cérébral (AVC) ischémique en phase aiguë (thrombolyse / thrombectomie)",q:"AVC ischémique",ur:true,
d:"Déficit neurologique brutal par occlusion artérielle cérébrale : ischémie du territoire de l'artère cérébrale moyenne (hémiplégie, aphasie, hémianopsie), cérébrale antérieure ou postérieure ; la fenêtre thérapeutique de la thrombolyse (alvéplase, moins de 4,5 h) et de la thrombectomie mécanique (moins de 6-24 h selon critères) impose une prise en charge « time is brain ».",
s:"Déficit focal brutal : hémiplégie ou hémiparésie controlatérale, asymétrie faciale, aphasie (territoire gauche), hémianopsie, ataxie, vertiges (postérieur) ; conscience le plus souvent conservée (ischémique) ; confusion des signes selon le territoire ; à dater précisément (dernière heure de normalité).",
dx:"TDM cérébrale sans injection en urgence (éliminer une hémorragie) ; imagerie de perfusion ou IRM (pénombre) pour les fenêtres étendues ; glycémie (hypoglycémie fausse AVC), ECG (fibrillation auriculaire), bilan de coagulation ; étiologie à distance : échodoppler des troncs, Holter, échocardiographie.",
t:"Unité neurovasculaire (UNV) ; thrombolyse IV dans les 4,5 h si critères (alvéplase) ; thrombectomie mécanique si occlusion d'un gros tronc dans les 6-24 h (critères d'imagerie) ; aspirine à 24 h ; prévention des complications (escarres, thrombose, déglutition) ; étiologie : anticoagulation de la FA, endartériectomie/stent carotidien, contrôle des facteurs de risque ; rééducation précoce.",
k:"Le pronostic de l'AVC ischémique se joue en minutes : « time is brain » — TDM immédiate, dernière heure de normalité notée, UNV et reperfusion si éligible."}
,
{n:"Accident Vasculaire Cérébral (AVC) hémorragique (hématome intraparenchymateux)",q:"hématome cérébral",ur:true,
d:"Hémorragie cérébrale spontanée (hypertension chronique — noyaux gris centraux, cervelet, protubérance —, amyloïdie corticale du sujet âgé, anticoagulants, malformations) : déficit brutal avec céphalées, vomissements et troubles de conscience souvent plus marqués que dans l'ischémique.",
s:"Déficit focal brutal avec céphalées intenses, vomissements, hypertension, troubles de conscience variables jusqu'au coma ; hématome cérébelleux : vertiges, ataxie, troubles axiaux (engagement : urgence chirurgicale) ; hématome lobar du sujet âgé (amyloïdie) ; terrain anticoagulant (AVK/AOD) à l'interrogatoire.",
dx:"TDM cérébrale sans injection (hyperdensité spontanée) = examen clé ; évaluation du volume et de la ventriculite ; IRM (étiologie, malformation) ; bilan de coagulation et anticoagulants, tension artérielle ; angio-TDM si malformation suspectée (sujet jeune).",
t:"Soins intensifs : contrôle tensionnel strict (PA cible 130-140 selon protocoles), arrêt et antagonisation des anticoagulants (vitamine K, concentré de complexe prothrombique, idarucizumab ou andexanet), correction des troubles de coagulation ; hématome cérébelleux avec hydrocéphalie ou engagement : chirurgie évacuatrice urgente (dérivation ventriculaire) ; prévention des complications (rééducation précoce) ; recherche étiologique (artériographie/IRM si sujet jeune).",
k:"AVC avec céphalées, vomissements ou troubles de conscience = TDM (hémorragie) ; antagoniser sans délai les anticoagulants ; l'hématome cérébelleux menaçant se draine en urgence."}
,
{n:"Hémorragie sous-arachnoïdienne (HSA) par rupture d'anévrisme intracrânien",q:"hémorragie sous-arachnoïdienne",ur:true,
d:"Irruption de sang dans les espaces sous-arachnoïdiens par rupture d'un anévrisme du polygone de Willis (hypertension, tabac, terrain familial, polykystose) : céphalée brutale en coup de tonnerre, irritation méningée ; risque de resaignement précoce (le premier jour) et de vasospasme (4-14 jours).",
s:"Céphalée brutale, catastrophique, en coup de tonnerre, maximale d'emblée, avec raideur de nuque, vomissements, photophobie, perte de connaissance brève, parfois déficit focal (anévrisme moyen : paralysie oculomotrice) ; grade I-V (WFNS) ; resaignement : aggravation brutale secondaire.",
dx:"TDM cérébrale sans injection (hyperdensité des espaces sous-arachnoïdiens) — si normale et forte suspicion : ponction lombaire (liquide xanthochromique) ; angio-TDM (anévrisme) ou artériographie ; surveillance du vasospasme (doppler transcrânien).",
t:"Repos, analgésie, contrôle tensionnel ; exclusion de l'anévrisme en urgence (embolisation endovasculaire ou clip chirurgical) pour prévenir le resaignement ; nimodipine (prévention du vasospasme) ; surveillance en soins intensifs neurologiques : vasospasme (triple H, angioplastie), hydrocéphalie (dérivation), hyponatrémie ; contrôle des facteurs de risque et recherche des autres anévrismes.",
k:"Céphalée en coup de tonnerre, maximale d'emblée = HSA jusqu'à preuve du contraire : TDM, PL si doute, et exclusion de l'anévrisme (le resaignement du premier jour est mortel)."}
,
{n:"Thrombose veineuse cérébrale (phlébite cérébrale)",q:"thrombose veineuse cérébrale",ur:true,
d:"Occlusion thrombotique des sinus veineux duraux (sinus sagittal supérieur, latéral, caverneux) ou des veines cérébrales : céphalées et hypertension intracrânienne, déficits focaux ou crises, hémorragies infarctus veineux hémorragiques ; terrain : femmes jeunes (contraception, post-partum), thrombophilie, infection ORL, Behçet.",
s:"Céphalée progressive ou brutale avec œdème papillaire, crises d'épilepsie, déficits focaux (hémiplégie, aphasie), syndrome d'hypertension intracrânienne (nausées, flou visuel) ; sinus caverneux : œdème orbitaire, chimosis, paralysie oculomotrice, fièvre (infection faciale) ; formes trombosantes lentement évolutives.",
dx:"Angio-IRM ou angio-TDM veineux (défaut d'opacification des sinus, vide) ; séquences T2/IRM ; ponction lombaire (pression élevée, si l'imagerie le permet) ; bilan de thrombophilie, contraception, grossesse, recherche d'une infection ou d'une maladie systémique.",
t:"Anticoagulation curative (héparine puis AVK 6-12 mois) même en cas d'infarctus veineux hémorragique ; traitement de la cause (arrêt des œstroprogestatifs, infection, post-partum) ; crises : antiépileptiques ; hypertension intracrânienne : acétazolamide, dérivation si menace visuelle ; surveillance visuelle ; pronostic globalement favorable sous traitement.",
k:"Céphalées avec œdème papillaire et crises chez une femme jeune sous œstroprogestatifs = thrombose veineuse cérébrale : angio-IRM veineuse ; anticoaguler, même si l'infarctus est hémorragique."}
]},
{name:"Urgences Infectieuses & Inflammatoires Centrales",paths:[
{n:"Méningites bactériennes aiguës et encéphalites herpétiques ou virales",q:"méningite",ur:true,
d:"Méningite bactérienne (pneumocoque, méningocoque) : purulence des méninges, urgence absolue ; encéphalite (HSV le plus fréquent et le plus grave) : atteinte du parenthyme cérébral avec crises et confusion ; les deux tableaux peuvent s'associer (méningo-encéphalite).",
s:"Méningite : fièvre, céphalées intenses, vomissements en jet, raideur de nuque, photophobie, purpura (méningocoque) ; encéphalite : fièvre + confusion + crises d'épilepsie, troubles du comportement, déficits focaux (temporal : HSV) ; coma dans les formes graves.",
dx:"Ponction lombaire (sauf contre-indication) : liquide trouble à PNN (bactérienne) ou lymphocytaire (virale), hypoglycorachie ; PCR herpes dans le LCR ; TDM avant PL si signes de focalisation ; hémocultures ; jamais d'antibiothérapie retardée par l'imagerie.",
t:"Méningite bactérienne : C3G IV immédiate (céfotaxime ou ceftriaxone) ± amoxicilline (listeria) et dexaméthasone ; encéphalite herpétique : aciclovir IV immédiat avant confirmation ; traitement des crises ; soins intensifs si coma ; prophylaxie des contacts du méningocoque ; déclaration obligatoire.",
k:"Fièvre + céphalées + raideur de nuque = PL en urgence (sauf CI) et C3G sans délai ; fièvre + confusion + crises = aciclovir immédiat (encéphalite herpétique)."}
,
{n:"Abcès cérébral et empyème subdural",q:"abcès cérébral",ur:true,
d:"Collection purulente intraparenchymateuse (abcès) ou sous-durale (empyème, souvent d'origine sinusienne ou otitique) : staphylocoques, streptocoques et anaérobies ; portes d'entrée : ORL (sinusite, otite), dentaire, endocardite, traumatisme, chirurgie ; l'empyème est le plus urgent des deux.",
s:"Céphalées progressives, fièvre inconstante, crises d'épilepsies, déficit focal progressif, troubles de conscience, œdème papillaire ; empyème : fièvre et céphalées avec syndrome méningé et évolution rapide, souvent après une sinusite frontale ; abcès multiples : sepsis ou endocardite.",
dx:"IRM cérébrale avec injection (ou TDM) : lésion à rehaussement périphérique (coiffe), effet de masse, collection sous-durale (empyème) ; hémocultures, bilan de la porte d'entrée (ORL, dentaire, échocardiographie) ; contre-indication de la PL (engagement).",
t:"Antibiothérapie IV prolongée 6-8 semaines (C3G + métronidazole ± antistaphylococcique) ; drainage chirurgical ou ponction-aspiration stéréotaxique (diagnostic et décompression) ; empyème : drainage en urgence ; anticonvulsivants ; corticoïdes si œdème menaçant ; traitement de la porte d'entrée ; surveillance rapprochée.",
k:"Céphalées fébriles avec crises ou déficit focal = IRM avec injection ; jamais de PL devant un abcès cérébral ; l'empyème sous-dural frontal draine en urgence."}
,
{n:"Myélite aiguë transverse",q:"myélite transverse",ur:true,
d:"Inflammation aiguë de la moelle épinière (déficit sensitivo-moteur sous-lésionnel avec niveau sensitif et troubles sphinctériens) : première poussée possible de SEP, myélite post-infectieuse, neuromyélite optique (NMO, anti-AQP4), vascularites ; urgence diagnostique et thérapeutique.",
s:"Déficit moteur des membres inférieurs ou des quatre membres (selon le niveau) d'installation en heures-jours, troubles sensitifs avec niveau métamérique, rétention urinaire ou incontinence, constipation, douleurs rachidiennes ; signe de Lhermitte possible ; fièvre ou infection récente.",
dx:"IRM médullaire urgente (hypersignal, gonflement médullaire, prise de contraste ; éliminer une compression !) ; IRM cérébrale (plaques de SEP) ; ponction lombaire (pléiocytose, bandes oligoclonales) ; anticorps anti-AQP4 et anti-MOG ; bilan étiologique (infections, lupus, sarcoidose).",
t:"Éliminer une compression médullaire en urgence (imagerie) ; corticothérapie IV à forte dose (méthylprednisolone) des myélites inflammatoires ; échanges plasmatiques si régression insuffisante ; traitement de la cause (NMO : immunosuppresseurs) ; sondage, prévention des complications (thrombose, escarres) ; rééducation ; suivi (risque de SEP).",
k:"Tout déficit médullaire aigu (niveau sensitif + rétention) = IRM médullaire en urgence : éliminer une compression, corticoïdes IV ; l'antécédent ou l'atteinte oculaire oriente vers NMO ou SEP."}
]},
{name:"Urgences Critiques & Fonctionnelles",paths:[
{n:"État de mal épileptique (partiel ou généralisé)",q:"état de mal épileptique",ur:true,
d:"Crise épileptique de plus de 5 minutes ou crises répétées sans reprise de conscience ; formes convulsives (généralisées ou focales motrices) et non convulsives (confusion prolongée) ; urgence vitale : hypoxie cérébrale, décompensation ; causes : épilepsie connue avec rupture thérapeutique, sevrage alcoolique, AVC, métabolique, toxique.",
s:"Convulsion tonico-clonique prolongée ou répétée sans intervalle de conscience ; état de mal non convulsif : confusion ou coma inexpliqué avec anomalies EEG ; surveillance : voies aériennes, saturation, hémodynamique, glycémie, température.",
dx:"Glycémie capillaire immédiate ; ionogramme, calcémie, NFS, CRP, hémocultures si fièvre ; toxiques (alcoolémie, médicaments) ; EEG (état non convulsif) ; TDM cérébrale à distance de la crise ou IRM ; PL si fièvre ; cause médicamenteuse (théophylline, ISRS, sevrage brutal des antiépileptiques).",
t:"Protocole : benzodiazépine (clonazépam, midazolam ou diazépam IV) à répéter une fois, puis 2e ligne à 10 min (fosphénytoïne, phénobarbital ou lévétiracétam IV), puis anesthésie générale (thiopental, midazolam ou propofol) au-delà de 30-40 min avec EEG continu ; soins de support : voies aériennes, oxygène, correction des troubles ; traitement de la cause.",
k:"Crise épileptique de plus de 5 minutes = traitement protocolaire : benzodiazépine IV d'emblée, sans attendre la fin spontanée ; l'escalade est programmée (2e ligne à 10 min, réanimation au-delà de 30 min)."}
,
{n:"Crise suicidaire aiguë (tentative de suicide imminente ou avérée)",q:"crise suicidaire",ur:true,
d:"Urgence psychiatrique : crise suicidaire (idéation, planification, passage à à l'acte imminent) ou tentative de suicide avérée (intoxication médicamenteuse le plus souvent) ; évaluation systématique du risque de récidive et protection immédiate du patient ; la crise est le plus souvent un état transitoire.",
s:"Idées suicidaires, ruminations, angoisse, insomnie, sentiment d'impasse, préparation (lettres, dons, moyens) ; tentative : intoxication volontaire (paracétamol, psychotropes), phlébotomie, défenestration, pendaison ; après la tentative : déni, minimisation ou souffrance aiguë ; facteurs de risque : dépression, veuvage, isolement, antécédents, alcool.",
dx:"Évaluation du risque suicidaire (idées, plan, moyens, antécédents, impulsivité, consommation) ; bilan somatique de la tentative (paraclinique selon le mode : paracétamolémie, gaz du sang, ECG) ; jamais de banalisation ; évaluation psychiatrique systématique avant toute sortie.",
t:"Sécurisation immédiate (hospitalisation si risque élevé, surveillance rapprochée, objets dangereux retirés) ; traitement somatique de la tentative (antidotes : N-acétylcystéine du paracétamol) ; soin psychiatrique : alliance, crise suicidaire = urgence médicale, hospitalisation en psychiatrie si nécessaire (consentement ou soins sans consentement si danger immédiat) ; suivi rapproché après la crise (période vulnérable), impliquer l'entourage ; prévention : 3114 (numéro national de prévention du suicide).",
k:"Toute crise suicidaire = évaluation immédiate du risque et protection (jamais de sortie sans avis psychiatrique) ; les semaines qui suivent une tentative sont la période la plus vulnérable : suivi rapproché."}
,
{n:"État d'agitation psychomotrice aiguë et Bouffée Délirante Aiguë (BDA)",q:"agitation psychomotrice",ur:true,
d:"Agitation psychomotrice : comportement moteur excessif et non contrôlé, avec potentialité dangereuse ; causes psychiatriques (bouffée délirante aiguë — délire polymorphe brutal, souvent à thème persécutoire —, accès maniaque, dépression, confusion) et organiques (confusion, sevrage, intoxication, hypoglycémie, AVC, épilepsie) : toujours éliminer l'urgence organique.",
s:"Agitation, agressivité, cris, déambulation, refus de soins, angoisse massive ; BDA : délire aigu polymorphe (persécution, mégalomanie, mystique), hallucinations, dépersonnalisation, onirisme, insomnie ; confusion : désorientation, fluctuation, troubles attentionnels.",
dx:"Recherche d'une cause organique d'abord : glycémie, température, saturation, toxiques, gaz du sang, ionogramme, TDM cérébrale si doute ; pas de sédation excessive avant l'examen ; anamnèse (entourage, traitement, terrain) ; l'agitation du sujet âgé = confusion jusqu'à preuve du contraire.",
t:"Isolement, calme, parole apaisante (désescalade verbale d'abord) ; si nécessaire : sédation médicamenteuse (benzodiazépine ± neuroleptique, voie IM si refus) avec surveillance clinique et monitorage ; bilan organique ; BDA : hospitalisation psychiatrique, neuroleptiques (amisulpride, rispéridone), surveillance ; soins sans consentement si danger immédiat (procédure légale).",
k:"Agitation = cause organique à éliminer d'abord (confusion, hypoglycémie, sevrage, toxique) ; désescalade verbale, puis sédation raisonnée avec surveillance ; l'agitation du sujet âgé est une confusion jusqu'à preuve du contraire."}
,
{n:"Syndrome malin des neuroleptiques et catatonie aiguë",q:"syndrome malin des neuroleptiques",ur:true,
d:"Syndrome malin des neuroleptiques (SMN) : réaction idiosyncrasique aux antipsychotiques (et aux antiémétiques neuroleptiques, arrêt brutal d'agonistes dopaminergiques) : rigidité, hyperthermie, troubles végétatifs et de conscience ; la catatonie (immobilité, négativisme, flexibilité cireuse, stupeur) en est le proche syndrome, traitée par benzodiazépines et ECT.",
s:"Hyperthermie supérieure à 38,5 °C, hypertonie musculaire « en tuyau de plomb » avec tremblements, hypersudation, tachycardie, hypertension, instabilité végétative, troubles de conscience (obnubilation au coma) ; syndrome biologique : hyperCPK massives (rhabdomyolyse), hyperleucocytose ; catatonie : mutisme, immobilité, postures, négativisme, écholalie, accidents de déshydratation et de thrombose.",
dx:"Clinique + terrain (neuroleptique introduit ou arrêt d'agoniste dopaminergique) ; CPK, NFS, ionogramme (insuffisance rénale, hyperkaliémie), bilan de rhabdomyolyse ; éliminer une infection, un syndrome sérotoninergique ( prise d'ISRS : myoclonies, hyperréflexie), un coup de chaleur, une hyperthermie maligne ; EEG.",
t:"Arrêt immédiat du neuroleptique (ou réintroduction de l'agoniste dopaminergique arrêté) ; hospitalisation en soins intensifs : refroidissement, réhydratation massive, traitement de la rhabdomyolyse ; dantrolène et agonistes dopaminergiques (bromocriptine) ; catatonie : benzodiazépines à forte dose (lorazépam) et électroconvulsivothérapie (rapide et très efficace) ; prévention de la récidive (réintroduction prudente, alternatives).",
k:"Fièvre + rigidité + troubles végétatiques sous neuroleptique = syndrome malin : arrêt du médicament, soins intensifs, dantrolène ; la catatonie répond spectaculairement aux benzodiazépines puis à l'ECT."}
]}
]},

{id:"neuro-clin",num:2,name:"Neurologie Clinique & Pathologies Subaiguës / Chroniques",groups:[
{name:"Troubles du Mouvement & Pathologies Neurodégénératives",paths:[
{n:"Maladie de Parkinson idiopathique et syndromes parkinsoniens atypiques",q:"maladie de Parkinson",
d:"Maladie de Parkinson idiopathique : dégénérescence dopaminergique nigrostriée (corps de Lewy), asymétrique et progressive (triade : tremblement de repos, akinésie, rigidité) ; syndromes parkinsoniens atypiques (paralysie supranucléaire progressive, atrophie multisystématisée, dégénérescence cortico-basale) : résistance à la lévodopa, signes précoces additionnels, pronostic plus sévère.",
s:"Tremblement de repos asymétrique (4-6 Hz), bradykinésie (maladresse, micrographie, perte du ballancement du bras), rigidité plastique en roue dentée, perte des automatismes ; troubles non moteurs : hyposmie, constipation, troubles du sommeil paradoxal, dépression ; atypiques : chutes précoces, paralysie verticale du regard (PSP), dysautonomie sévère (AMS), apraxie asymétrique (DCB).",
dx:"Clinique (critères diagnostiques, asymétrie initiale, réponse à la dopa) ; test dopa-sensibilité ; IRM cérébrale (éliminer une cause : hydrocéphalie, lésion vasculaire) ; DAT-scan si doute ; examens neuropsychologiques ; causes secondaires (neuroleptiques !).",
t:"Traitement symptomatique adapté à l'âge et au stade : lévodopa (le plus efficace), agonistes dopaminergiques, inhibiteurs de la MAO-B ; suivi de la dyskinésie et des fluctuations ; stimulation cérébrale profonde dans les formes fluctuantes du sujet jeune ; kinésithérapie, orthophonie, activité physique ; troubles non moteurs traités (constipation, sommeil, dépression) ; éducation patient-aidants.",
k:"Parkinson = asymétrique, dopa-sensible, avec signes non moteurs précoces ; chutes précoces ou dysautonomie sévère ou résistance à la lévodopa = parkinsonien atypique ; jamais de neuroleptique classique chez un parkinsonien."}
,
{n:"Troubles neurocognitifs majeurs : Alzheimer, démence à corps de Lewy, vasculaire, fronto-temporale",q:"démence",
d:"Déclin cognitif interférant avec l'autonomie : maladie d'Alzheimer (60-70 % : mémoire épisodique initiale), démence à corps de de Lewy (fluctuations, hallucinations visuelles, parkinsonisme), démence vasculaire (à-coups, facteurs de risque, lésions à l'imagerie), dégénérescence fronto-temporale (troubles du comportement et/ou du langage, sujet plus jeune).",
s:"Troubles de mémoire récents (Alzheimer), désorientation temporo-spatiale, difficultés instrumentales, apathie ; corps de Lewy : hallucinations visuelles détaillées, fluctuations cognitives majeures, parkinsonisme, troubles du sommeil paradoxal, hypersensibilité aux neuroleptiques ; vasculaire : installation en escalier, marche à petits pas ; fronto-temporale : désinhibition, apathie, aphasie primaire.",
dx:"Tests cognitifs (MMSE, MoCA) et bilan neuropsychologique ; bilan causal : NFS, TSH, B12, ionogramme, scanner ou IRM cérébrale ; éliminer une cause curable (hydrocéphalie, dépression, iatrogénie, hypothyroïdie) ; évaluation fonctionnelle et sociale ; parfois ponction lombaire ou TEP (formes atypiques ou jeunes).",
t:"Mesures non pharmacologiques prioritaires (routine, environnement, formation des aidants, rééducation cognitive) ; inhibiteurs de la cholinestérase (Alzheimer, Lewy) puis mémantine ; corps de Lewy : neuroleptiques formellement contre-indiqués ; contrôle des facteurs vasculaires (démence vasculaire) ; directives anticipées, protection juridique, soutien des aidants ; suivi régulier.",
k:"Hallucinations visuelles + fluctuations + parkinsonisme = démence à corps de Lewy : jamais de neuroleptique ; toujours chercher une cause curable de trouble cognitif avant de conclure à Alzheimer."}
,
{n:"Chorée de Huntington et syndromes choréiques",q:"chorée de Huntington",
d:"Maladie neurodégénérative autosomique dominante (expansion CAG du gène HTT) : troubles moteurs (chorée : mouvements involontaires brusques et désordonnés), psychiatriques et cognitifs, d'installation vers 30-50 ans ; pénétrance liée à la taille de la répétition et anticipation (formes juvéniles par transmission paternelle).",
s:"Chorée progressive (mouvements involontaires du visage, tronc, membres), troubles de l'équilibre et de la marche, dystonie ; troubles psychiatriques : irritabilité, apathie, dépression, désinhibition, parfois psychose ; déclin cognitif (ralentissement, troubles exécutifs) ; antécédents familiaux souvent évocateurs (diagnostic parfois caché).",
dx:"Consultation de génétique (test présymptomatique encadré par la loi, avec accompagnement psychologique) ; analyse génétique (expansion CAG ≥ 36 répétitions) ; IRM cérébrale (atrophie caudée) ; bilan neuropsychologique et psychiatrique ; conseil génétique familial.",
t:"Pas de traitement curatif : tetrabénazine ou deutérétrabénazine (chorée), neuroleptiques atypiques si besoin ; antidépresseurs, anxiolytiques, prise en charge comportementale ; kinésithérapie, orthophonie, aide sociale et administrative ; suivi multidisciplinaire ; information de la famille et conseil génétique (diagnostic présymptomatique à la demande du patient majeur).",
k:"Chorée + troubles psychiatriques + antécédents familiaux = Huntington (test génétique avec consentement et accompagnement) ; jamais de test présymptomatique d'un tiers sans sa demande."}
,
{n:"Tremblement essentiel et dystonies focales ou généralisées",q:"tremblement essentiel",
d:"Tremblement essentiel : tremblement d'action bilatéral et symétrique des membres supérieurs (parfois tête et voix), héréditaire, lentement progressif, amélioré par l'alcool ; dystonies : contractions musculaires soutenues provoquant des postures anormales et mouvements de torsion — focales (torticollis spasmodique, blépharospasme, crampe de l'écrivain), généralisées (dystonie DYT1).",
s:"Tremblement essentiel : tremblement des deux mains à l'action (écrire, porter une tasse), majoré par l'émotion, amélioré par l'alcool, sans autre signe neurologique ; dystonie cervicale : torticolis avec douleur, tremblement de tête ; blépharospasme : clonies et fermeture involontaire des yeux ; dystonie de tâche (musiciens, écrivains).",
dx:"Clinique (tremblement d'action vs repos parkinsonien, asymétrie, autres signes) ; examens normaux ; IRM ou bilan si signes atypiques (éliminer un parkinsonisme, une maladie de Wilson chez le jeune : céruléoplasmine) ; l'amélioration par l'alcool est un indice diagnostique.",
t:"Tremblement essentiel : propranolol ou primidone (première ligne), topiramate, gabapentine ; échec : stimulation thalamique (VIM) ou échographie focalisée ; dystonies focales : toxine botulique (traitement de référence, répété tous les 3-4 mois), rééducation ; dystonies généralisées : anticholinergiques, baclofène, stimulation pallidale ; prise en charge de la douleur et du retentissement social.",
k:"Tremblement des mains à l'action, bilatéral, familial et calmé par l'alcool = tremblement essentiel (à distinguer du repos parkinsonien) ; la toxine botulique transforme la vie des dystonies focales."}
]},
{name:"Épilepsies & Céphalées Chroniques",paths:[
{n:"Épilepsies généralisées et focales pharmacorésistantes",q:"épilepsie",
d:"Épilepsies : syndromes généralisés (génétiques : JME, absences) ou focaux (lésionnels : sclérose hippocampique, dysplasie corticale, séquelle, tumeur) ; la pharmacorésistance est définie par l'échec de deux traitements bien conduits : elle ouvre l'évaluation préchirurgicale (focale) et les alternatives (diète cétogène, neurostimulation).",
s:"Crises généralisées tonico-cloniques, absences, myoclonies (JME : matinées) ; crises focales : aura épigastrique, sensitive, olfactive), automatismes, regard vide, post-critique ; retentissement : chutes, blessures, conduite automobile, psychosocial, mort subite (SUDEP) ; pharmacorésistance : crises persistantes malgré deux antiépileptiques adaptés.",
dx:"EEG (intercritique et vidéo-EEG prolongé) ; IRM cérébrale épileptologie spécifique (coupes fines temporales) ; enregistrement vidéo-EEG des crises ; bilan métabolique et génétique si contexte ; évaluation neuropsychologique et psychiatrique.",
t:"Monothérapie adaptée au syndrome (valproate des généralisées — sauf grossesse, lévétiracétam, lamotrigine ; carbamazépine des focales) ; vérifier l'observance (première cause d'échec) ; pharmacorésistance focale : évaluation préchirurgicale (résection du foyer, thermoablation) ; stimulation du nerf vague, diète cétogène ; sécurité (conduite, baignade, hauteur) ; contraception et projet de grossesse adaptés (valproate tératogène : interdit chez la femme en âge de procréer sauf exceptions) ; éducation patient-entourage.",
k:"Échec de deux antiépileptiques bien conduits = pharmacorésistance : évaluation chirurgicale du foyer (la résection peut guérir) ; valproate interdit chez la femme en âge de procréer tératogénicité)."}
,
{n:"Migraines (avec et sans aura) et céphalées de tension chroniques",q:"migraine",
d:"Migraine : céphalée primaire récurrente (5 attaques minimum) : pulsatile, unilatérale, modérée à sévère, aggravée par l'activité, avec nausées, photophobie et phonophobie ; avec aura (visuel le plus souvent, réversible, 5-60 min) ou sans ; céphalée de tension : bilatérale, en étau, légère à modérée, sans signes accompagnateurs.",
s:"Migraine : 4-72 heures, pulsatile, unilatérale (bilateralisation possible), nausées, intolérance lumière et bruit, aggravée par l'effort, préférence pour le repos au calme ; aura visuelle (scotomes scintillants), sensitive ou du langage précédant la céphalée ; menstruelle ; céphalée de tension : bilatérale, en étau, sans nausée, parfois chronique (plus de 15 jours/mois).",
dx:"Diagnostic clinique (critères ICHD-3) ; examen neurologique normal ; imagerie seulement si signes d'alarme (céphalée en coup de tonnerre, déficit, fièvre, œdème papillaire, céphalée inhabituelle ou âge > 50 ans) ; calendrier des crises (fréquence, déclencheurs) ; médicaments de crise excessifs = céphalée par abus médicamenteux.",
t:"Crise : AINS ou triptan (précocement, dans l'heure) ± antiémétique ; formes sévères : triptan par voie non orale ; fond (plus de 3-4 crises/mois) : topiramate, propranolol, amitriptyline, flunarizine, et anticorps anti-CGRP (formes invalidantes) ; éviter l'abus de traitements de crise (plus de 10 jours/mois : céphalée chronique) ; repérer et éviter les déclencheurs (sommeil, jeûne, alcool, stress) ; céphalée de tension : antalgiques ponctuels, gestion du stress, physiothérapie, amitriptyline si chronique.",
k:"Migraine = pulsatile + nausées + photophobie ; imagerie seulement devant des signes d'alarme ; limiter les traitements de crise à 10 jours/mois (risque de céphalée par abus médicamenteux)."}
,
{n:"Algie vasculaire de la face (céphalée histaminique de Horton)",q:"algie vasculaire de la face",ur:true,
d:"Algie vasculaire de la face (cluster headache) : céphalée primaire la plus douloureuse : douleur strictement unilatérale orbitaire ou temporale, très intense, de 15-180 minutes, en salves (1 à 3 par jour) pendant des périodes (« clusters ») de semaines à mois, avec signes végétatiques homolatéraux ; homme fumeur typiquement.",
s:"Douleur extrême, en broche, orbitaire unilatérale stricte, d'installation explosive, avec larmoiement, rougeur oculaire, ptosis, rhinorrhée et agitation (le patient ne tient pas en place, contrairement à la migraine) ; salves quotidiennes à heure fixe (souvent nocturnes) ; périodes de crises séparées de rémissions ; forme chronique sans rémission.",
dx:"Clinique (critères ICHD-3, unilatéralité stricte, signes végétatiques, agitation) ; examen ophtalmologique et imagerie si premier épisode ou atypie (éliminer une lésion sinusienne, une dissection carotidienne, un glomus) ; pas d'examen systématique dans la forme typique.",
t:"Crise : oxygène à haut débit (15 L/min, masque à réserve — traitement de référence) ou sumatriptan sous-cutané ; prophylaxie de la période : vérapamil (référence), court cours de corticoïdes, lithium dans les formes chroniques ; arrêt du tabac ; formes rebelles : stimulation du nerf occipital, anticorps anti-CGRP ; le patient garde ses traitements d'attaque à portée de main.",
k:"Douleur orbitaire explosive, unilatérale stricte, à heure fixe, avec patient agité et l'œil rouge qui pleure = algie vasculaire de la face : oxygène à haut débit et sumatriptan sous-cutané."}
,
{n:"Névralgie du trijumeau et autres névralgies cranio-faciales",q:"névralgie du trijumeau",
d:"Névralgie du trijumeau (tic douloureux) : douleurs fulgurantes unilatérales brèves (secondes) dans un ou plusieurs territoires du V, déclenchées par des stimuli anodins (mastication, froid, toucher du visage) ; classique (compression vasculaire du nerf à sa sortie) ou secondaire (sclérose en plaques, tumeur de l'angle ponto-cérébelleux).",
s:"Décharges électriques brèves (1-2 secondes) dans le territoire du trijumeau (V2-V3 le plus souvent, V1 plus rarement), avec zones gâchette (lavage des dents, mastication, baiser, vent) ; intervalles libres ; patient craignant de manger et de parler (perte de poids) ; bilatéralité ou déficit sensitif = chercher une cause secondaire.",
dx:"Clinique (douleurs brèves électriques, zones gâchette) ; IRM cérébrale avec séquences fines de l'angle ponto-cérébelleux (compression vasculaire, tumeur, plaques de SEP — systématique au diagnostic) ; examen neurologique (hypoesthésie cornéenne) ; bilan dentaire (éliminer une origine dentaire).",
t:"Carbamazépine (ou oxcarbazépine) de première intention ; deuxième ligne : gabapentine, baclofène, lamotrigine ; échec ou intolérance médicamenteuse : chirurgie (décompression vasculaire microchirurgicale — la plus durable, rhizotomie percutanée, radiochirurgie gamma-knife) ; formes paroxystiques de la SEP : alternatives adaptées ; prise en charge de la douleur chronique associée.",
k:"Douleurs électriques brèves du visage déclenchées par la mastication ou le toucher = névralgie du trijumeau : IRM systématique (compression, SEP, tumeur), carbamazépine d'abord, décompression chirurgicale si échec."}
]},
{name:"Pathologies Neuromusculaires & de la Moelle Épinière",paths:[
{n:"Sclérose en plaques (SEP) et maladies démyélinisantes",q:"sclérose en plaques",
d:"Maladie inflammatoire démyélinisante du système nerveux central chez l'adulte jeune (femme surtout) : poussées disséminées dans le temps et l'espace (formes rémittentes) ou progression d'emblée/secondaire ; lésions (plaques) démyélinisantes périventriculaires, du nerf optique, du tronc, de la moelle ; variantes : neuromyélite optique (NMO), MOG-associated disease.",
s:"Névrite optique rétrobulbaire (baisse d'acuité visuelle unilatérale, douleur à la mobilisation, œdème papillaire discret), myélite (déficit sous-lésionnel, niveau sensitif, troubles sphinctériens), troubles sensitifs, atteinte tronculaire (diplopie, vertiges, nystagmus), fatigue ; formes rémittentes (85 %) et progressives.",
dx:"IRM cérébrale et médullaire (plaques en hypersignal T2 disséminées, prise de contraste des lésions récentes) ; ponction lombaire (bandes oligoclonales) ; OCT (épaisseur de la couche des fibres optiques) ; critères de McDonald (dissémination) ; bilan différentiel : NMO (anti-AQP4), MOG, vascularites, carences (B12), sarcoïdose, Lyme.",
t:"Traitement des poussées : corticoïdes IV (méthylprednisolone) ; traitement de fond des formes rémittentes : immunomodulateurs et immunosuppresseurs (injectables, oraux — fingolimod, diméthylfumarate —, et anticorps monoclonaux anti-CD20 : rituximab, ocrélizumab) selon l'agressivité ; formes progressives : ocrélizumab (PP) ; kinésithérapie, rééducation, gestion de la fatigue, suivi multidisciplinaire (vessie, sphincters, sexualité, humeur) ; vaccination avant immunosuppresseurs.",
k:"Chez l'adulte jeune, une névrite optique ou une myélite = SEP jusqu'à preuve du contraire (IRM cérébrale et médullaire, critères de dissémination) ; le traitement de fond prévient le handicap cumulatif."}
,
{n:"Syndrome de Guillain-Barré (polyradiculonévrite aiguë inflammatoire)",q:"syndrome de Guillain-Barré",ur:true,
d:"Polyradiculonévrite aiguë inflammatoire post-infectieuse (Campylobacter jejuni, virus) : démyélinisation auto-immune des nerfs périphériques ; déficit moteur ascendant symétrique en 1-4 semaines (variante : Miller-Fisher — ophtalmoplégie, ataxie, aréflexie) ; la surveillance respiratoire et autonome fait le pronostic.",
s:"Faiblesse musculaire symétrique ascendante (d'abord membres inférieurs : difficulté à monter les escaliers), aréflexie ostéotendineuse, douleurs rachidiennes et musculaires ; atteinte respiratoire (dégradation des débits inspiratoires) et dysautonomie (arythmie, poussées tensionnelles, rétention) = signes de gravité ; pas de fièvre ; troubles sensitifs modérés.",
dx:"PL (dissociation albumino-cytologique : protéines élevées sans cellules, après la 1re semaine) ; électroneuromyogramme (bloc de conduction, ralentissement) ; surveiller la capacité vitale (CVF) et les débits ; anticorps anti-gangliosides (Miller-Fisher : anti-GQ1b) ; éliminer les diagnostics différentiels (hypokaliémie, botulisme, myasthénie, Lyme, porphyrie).",
t:"Hospitalisation systématique avec surveillance de la fonction respiratoire (CVF répétée) et cardiaque ; immunoglobulines IV ou échanges plasmatiques (efficacité équivalente, précoces) ; réanimation si défaillance respiratoire (intubation) ; prévention des complications (anticoagulation, escarres, rééducation) ; la récupération se fait sur des semaines à mois ; arrêt des urgences monitoring cardiaque.",
k:"Déficit moteur ascendant symétrique avec aréflexie = Guillain-Barré : hospitaliser, surveiller la capacité vitale (intubation si dégradation), immunoglobulines IV ; jamais de diurétique (hypotension dysautonomique)."}
,
{n:"Myasthénie auto-immune (crise myasthénique)",q:"myasthénie",ur:true,
d:"Maladie auto-immune de la jonction neuromusculaire (anticorps anti-récepteurs de l'acétylcholine ou anti-MuSK) : faiblesse musculaire fluctuante et fatigable (ptosis, diplopie, troubles de déglutition, déficit des membres) ; la crise myasthénique (défaillance respiratoire et déglutition) est l'urgence ; thymome associé à rechercher.",
s:"Ptosis et diplopie fluctuants (majorés en fin de journée), dysarthrie, difficultés à mastiquer et déglutir (fausses routes), déficit des membres et de la nuque, fatigabilité à l'effort ; crise myasthénique : détresse respiratoire et encombrement ; crise cholinergique (surdose d'anticholinestérasiques) : hypersialorrhée, sueurs, diarrhée, myosis.",
dx:"Tests cliniques (fatigabilité : test de Simpson, ice-pack test du ptosis) ; anticorps anti-RACH et anti-MuSK ; électromyogramme (décrément à la stimulation répétitive) ; scanner thoracique (thymome) ; la crise : débits respiratoires, gaz du sang ; éliminer un syndrome de Lambert-Eaton (déficit amélioré par l'effort, néoplasie).",
t:"Traitement symptomatique : anticholinestérasiques (pyridostigmine) ; traitement de fond : corticoïdes (introduction lente : aggravation transitoire), immunosuppresseurs, rituximab ; thymectomie (formes avec thymome ou généralisées du sujet jeune) ; crise myasthénique : soins intensifs, immunoglobulines IV ou échanges plasmatiques, ventilation non invasive, éviter les médicaments déclencheurs (aminosides, fluoroquinolones, bêtabloquants, magnésium, curares).",
k:"Ptosis et diplopie fluctuants en fin de journée = myasthénie ; en crise : immunoglobulines IV et ventilation — et connaître la liste des médicaments contre-indiqués (aminosides, fluoroquinolones, curares)."}
,
{n:"Neuropathies périphériques (polyneuropathies métaboliques/diabétiques, mononeuropathies)",q:"neuropathie périphérique",
d:"Atteintes des nerfs périphériques : polyneuropathies (longueur-dépendantes : diabète — la première cause —, alcool, carences B1/B12, chimiothérapies, amylose, paranéoplasiques, héréditaires) et mononeuropathies (compression : canal carpien — médian, nerf ulnaire, radial, SPE à la fibula ; névralgie d'Arnold) ; polyneuropathies multiples (vascularite, diabète).",
s:"Polyneuropathie distale : paresthésies en chaussettes (et gants), brûlures, hypoesthésie, abolition des réflexes achilléens, troubles trophiques et ulcères indolores (pied diabétique) ; canal carpien : paresthésies nocturnes des trois premiers doigts, claudication de la main, atrophie thénarienne ; ulnaire : main en griffe.",
dx:"Electroneuromyogramme (axes : axonale, démyélinisante) ; bilan étiologique : glycémie et HbA1c, B12, TSH, électrophorèse, alcool, médicaments ; ponction lombaire si démyélinisante (polyradiculonévrite inflammatoire démyélinisante chronique) ; échographie nerveuse (compressions) ; score de neuropathie diabétique, monofilament.",
t:"Traitement de la cause (équilibre glycémique ++, sevrage, supplémentation) ; douleurs neuropathiques : prégabaline/gabapentine, duloxétine, amitriptyline, patchs (lidocaïne, capsaïcine) ; soins et éducation des pieds diabétiques (chaussures, inspection) ; canal carpien : attelle nocturne, infiltration, chirurgie de décompression ; CIDP : corticoïdes, immunoglobulines IV.",
k:"Paresthésies en chaussettes + réflexes achilléens abolis = polyneuropathie : l'ENMG et le bilan étiologique (diabète, alcool, B12) ; tout ulcère du pied diabétique indolore est neuropathique."}
,
{n:"Sclérose Latérale Amyotrophique (SLA) / Maladie de Charcot",q:"sclérose latérale amyotrophique",
d:"Maladie du motoneurone de l'adulte (50-70 ans) : dégénérescence des motoneurones centraux et périphériques — déficit moteur progressif avec amyotrophies, fasciculations et syndrome pyramidal — sans troubles sensitifs, sphinctériens ni oculomoteurs ; pronostic sévère (survie médiane 3-5 ans).",
s:"Déficit moteur distal d'un membre (main maladroite, pied qui traîne), fasciculations (langue d'abord), crampes, amyotrophies, hyperréflexie et signe de Babinski (mélange central et périphérique) ; troubles de la déglutition et de la phonation (bulbaire) ; l'émotion labile (pseudobulbaire) ; la respiration se dégrade tardivement ; sensibilité et intellect (le plus souvent) préservés.",
dx:"Électroneuromyogramme (dénervation et atteinte du motoneurone périphérique, sensibilité normale) ; IRM (éliminer une compression médullaire, une myélopathie) ; bilan (B12, TSH, protéines, paranéoplasique) ; critères (El Escorial révisés) ; consultation multidisciplinaire SLA ; entretien d'annonce dédié.",
t:"Prise en charge multidisciplinaire : riluzole (modeste ralentissement) ; ventilation non invasive (dyspnée, hypercapnie) et assistance à la toux ; gastrostomie d'alimentation (dysphagie) ; kinésithérapie et appareillage (orthèses, fauteuil) ; prise en charge de la spasticité, de l'hypersalivation, de la pseudobulbaire traitement symptomatique) ; soutien psychologique patient-famille, directives anticipées ; essais cliniques.",
k:"Chez un adulte, déficit moteur progressif avec fasciculations, amyotrophies et réflexes vifs (mélange pyramidal et périphérique), sans trouble sensitif = SLA : ENMG et centre de référence ; l'annonce et l'accompagnement font partie du traitement."}
,
{n:"Myopathies inflammatoires et dystrophies musculaires (Duchenne, etc.)",q:"myopathie inflammatoire",
d:"Myopathies : inflammatoires (polymyosite, dermatomyosite — avec rash pathognomonique et risque de cancer chez le sujet âgé —, myosite à inclusions) et dystrophiques héréditaires (Duchenne/Becker — dystrophine, lié à l'X, myopathie de l'enfant ; Steinert — myotonique) ; le déficit est proximal et la créatine-kinase élevée.",
s:"Déficit moteur proximal (se relever, monter les escaliers, se coiffer), myalgies (inflammatoires), dermatomyosite : érythème heliotrope et papules de Gottron ; Duchenne : démarche de canard, hypertrophie des mollets (pseudo-hypertrophie), signe de Gowers, rétraction, cardiomyopathie et scoliose ; Steinert : myotonie (relâchement lent), cataracte, troubles cardiaques et endocriniens.",
dx:"CPK élevées, aldolases ; EMG myogène ; IRM musculaire ; biopsie musculaire (inflammation, dystrophine, western blot) ; anticorps de myosite (anti-Jo1, anti-Mi2, anti-TIF1-γ) ; bilan du retentissement : cardiaque (ECG, ETT), respiratoire (EFR), génétique (dystrophine, myotonine) ; dermatomyosite du sujet âgé : recherche de cancer.",
t:"Inflammatoires : corticoïdes ± immunosuppresseurs (méthotrexate, azathioprine), rituximab ou immunoglobulines IV selon la forme ; dermatomyosite : dépistage et traitement du cancer associé ; Duchenne : corticoïdes (prolongent la marche), prise en charge orthopédique et respiratoire, suivi cardiaque, thérapies géniques (thérapies géniques), conseil génétique ; Steinert : suivi cardiaque (troubles du rythme), appareillage, éducation ; kinésithérapie, rééducation ; association de patients et soutien.",
k:"Déficit moteur proximal + CPK élevées = myopathie (biopsie et anticorps) ; une dermatomyosite de l'adulte après 50 ans impose la recherche d'un cancer."}
,
{n:"Myélopathies compressives et cervicarthrosiques",q:"myélopathie compressive",ur:true,
d:"Compression médullaire lente (cervicarthrose avec canal étroit et moelle comprimée, hernie discale calcifiée, tumeur, épidurite) ou aiguë (hématome, abcès, fracture) : déficit sous-lésionnel des quatre membres ou des membres inférieurs, troubles sensitifs et sphinctériens ; la compression aiguë est une urgence chirurgicale.",
s:"Marche perturbée (spasticité, déséquilibre), main maladroite (cervicale : troubles fins), paresthésies avec niveau sensitif, troubles sphinctériens, signe de Lhermitte ; cervicarthrose du sujet âgé (canal cervical étroit) ; formes aiguës : paraplégie ou tétraplégie brutales (hématome, abcès, métastase : urgence absolue).",
dx:"IRM médullaire urgente (compression, niveau, cause : hernie, arthrose, tumeur, abcès, hématome) ; scanner du rachis (os, calcifications) ; examen neurologique détaillé (moteur, sensitif, sphinctérien, réflexes) ; bilan pré-opératoire ; étiologie (biologie, TDM corps entier si métastase suspectée).",
t:"Compression aiguë : chirurgie décompressive en urgence (hématome, abcès, tumeur) ; cervicarthrose : décompression chirurgicale (laminectomie, corpectomie, arthrodèse) si déficit progressif ou marche menacée ; rééducation précoce et prolongée ; tumeurs : corticoïdes (œdème), radiothérapie ou chirurgie selon le type ; suivi de la récupération (souvent incomplète si le déficit est ancien).",
k:"Tout déficit des quatre membres avec troubles sphinctériens = IRM médullaire en urgence : une compression (hématome, abcès, métastase) se décompresse dans les heures."}
]}
]},

{id:"neuro-psy",num:3,name:"Psychiatrie Générale & Troubles de l'Humeur",groups:[
{name:"Troubles Psychotiques",paths:[
{n:"Schizophrénie (paranoïde, hébéphrénique, catatonique)",q:"schizophrénie",
d:"Trouble psychotique chronique (installation vers 15-25 ans chez le garçon, plus tard chez la fille) : syndrome positif (délire, hallucinations), négatif (retrait, émoussement affectif, apathie) et désorganisé ; évolution par épisodes avec dégradation fonctionnelle ; formes cliniques : paranoïde (délire structuré), hébéphrénique (désorganisation), catatonique.",
s:"Idées délirantes (persécution, référence, influence, divulgation de la pensée), hallucinations acoustico-verbales (voix commentant ou ordonnant), retrait social, émoussement, anhédonie, désorganisation (discours, comportement), négligence de soi ; anosognosie fréquente ; souffrance dépressive et risque suicidaire associés.",
dx:"Clinique (critères DSM-5 : durée supérieure à 6 mois, retentissement) ; éliminer les psychoses organiques et toxiques (cannabis, amphétamines, stéroïdes ; épilepsie temporale) ; bilan initial (biologique, imagerie selon contexte) ; évaluation du risque (suicide, hétéro-agressivité), cognitif et fonctionnel ; avis psychiatrique.",
t:"Traitement antipsychotique au long cours (seconde génération : rispéridone, aripiprazole, olanzapine ; formes injectables à action prolongée favorisant l'observance) ; prévention des rechutes (arrêt du cannabis ++, observance) ; prise en charge psychosociale : psychoéducation, remédiation cognitive, réhabilitation, entraide ; suivi métabolique des antipsychotiques (poids, glycémie, lipides) ; hospitalisation si risque ou décompensation ; soutien de la famille.",
k:"La schizophrénie se traite au long cours : l'observance et l'arrêt du cannabis pèsent plus que le choix de la molécule ; surveiller le poids et le métabolisme des antipsychotiques de seconde génération."}
,
{n:"Troubles schizo-affectifs et troubles délirants persistants (paranoïa)",q:"trouble délirant persistant",
d:"Trouble schizo-affectif : épisodes psychotiques coexistant avec des épisodes thymiques majeurs (maniaques ou dépressifs) ; trouble délirant persistant (paranoïa) : délire systématisé, bien structuré et non bizarre, souvent à thème persécutoire ou passionnel (jalousie, érotomanie, revendication), sans désorganisation ni déclin, le sujet restant fonctionnel.",
s:"Schizo-affectif : symptômes psychotiques ET épisodes dépressifs majeurs ou maniaques dans le même épisode ; paranoïa : délire cohérent et plausible (le médecin peut y être trompé au premier abord), hypervigilance, revendication, procédures ; pas d'hallucinations majeures ni de déclin cognitif ; risque hétéro-agressif des thèmes de persécution.",
dx:"Clinique et évolution (durée supérieure à 6 mois pour la paranoïa) ; éliminer une psychose organique ou toxique ; évaluation du risque de passage à l'acte (thèmes persécutoires) ; examen psychiatrique répété (la crédulité du délire peut égarer) ; bilan cognitif et fonctionnel.",
t:"Antipsychotiques au long cours (la paranoïa est souvent d'observance difficile : formes injectables, alliance patient-équipe) ; thymorégulateurs du trouble schizo-affectif (valproate, lithium) ; psychothérapie de soutien, jamais de confrontation brutale au délire ; approche familiale et sociale ; évaluation régulière du risque ; hospitalisation si dangerosité.",
k:"Devant un délire plausible et systématisé chez un adulte resté fonctionnel : paranoïa — l'alliance thérapeutique prime, la confrontation au délire est contre-productive."}
]},
{name:"Troubles de l'Humeur & Affectifs",paths:[
{n:"Épisode Dépressif Majeur (dépression unipolaire)",q:"dépression",
d:"Épisode dépressif caractérisé (critères DSM : au moins 2 semaines d'humeur triste ou anhédonie + symptômes associés) : ruminations, culpabilité, ralentissement, troubles du sommeil et de l'appétit, risque suicidaire ; formes : légère, modérée, sévère (avec ou sans caractéristiques psychotiques, mélancoliques).",
s:"Humeur triste, anhédonie (perte du plaisir), asthénie, ralentissement psychomoteur ou agitation, insomnie ou hypersomnie, anorexie, perte de poids, troubles de la concentration, sentiments de culpabilité et d'indignité, idées noires ou suicidaires ; forme mélancolique : douleur morale, réveil précoce, ralentissement majeur, risque suicidaire aigu.",
dx:"Clinique (échelles : MADRS, PHQ-9) ; évaluation systématique du risque suicidaire ; éliminer une cause organique : hypothyroïdie, carences, anémie, syndrome dépressif d'un trouble bipolaire méconnu (interrogatoire sur les épisodes d'excitation) ; retentissement social et fonctionnel.",
t:"Selon la sévérité : psychothérapie (TCC, activation comportementale) des formes légères à modérées ; antidépresseur (ISRS en première ligne, 4-6 semaines d'essai, poursuite 6 mois après la rémission) ; formes sévères ou mélancoliques : association antidépresseur + neuroleptique, électroconvulsivothérapie (efficace et rapide) ; hospitalisation si risque suicidaire ; éducation (observance, délai d'action) ; vigilance à l'installation d'un virage maniaque.",
k:"Toute dépression = évaluation du risque suicidaire et recherche d'antécédents d'excitation (bipolarité : les antidépresseurs seuls y sont dangereux) ; l'ECT des formes mélancoliques est rapide et sauve des vies."}
,
{n:"Trouble Bipolaire (type I et II, épisodes maniaques ou hypomaniaques)",q:"trouble bipolaire",
d:"Trouble de l'humeur avec épisodes maniaques (type I) ou hypomaniaques (type II) alternant avec des épisodes dépressifs : maladie chronique à haut risque suicidaire ; la manie : exaltation de l'humeur, hyperactivité, diminution du besoin de sommeil, désinhibition ; diagnostic souvent retardé (10 ans, pris pour une dépression récurrente).",
s:"Épisode maniaque : euphorie ou irritabilité, idées de grandeur, accélération (logorrhée, fuite des idées), hyperactivité, achats inconsidérés, sexualité désinhibée, besoin de sommeil diminué (le signe cardinal) sans fatigue ; hypomanie : forme atténuée sans retentissement majeur ; épisodes dépressifs plus fréquents et longs ; cycles rapides ; consommation de toxiques associée fréquente.",
dx:"Anamnèse longitudinale (entourage) : épisodes d'excitation passés inaperçus ; échelles (MDRS, ASRM) ; critères DSM-5 ; éliminer les causes organiques et toxiques (thyréotoxicose, corticoïdes, cocaïne, antidépresseurs déclencheurs) ; bilan pré-thymorégulateur (ionogramme, fonction rénale et thyroïdienne, β-hCG avant lithium).",
t:"Thymorégulateurs au long cours : lithium (référence — surveillance de la lithiémie, thyroïde, rein), valproate (interdit chez la femme en âge de procréer sauf cas particuliers), lamotrigine (poussées dépressives) ; épisode maniaque : neuroleptique ou benzodiazépine + thymorégulateur ; dépression bipolaire : jamais d'antidépresseur seul (virage maniaque) ; psychoéducation (rythmes de vie, sommeil, repérage précoce) ; psychothérapie ; hospitalisation des manies aiguës.",
k:"Besoin de sommeil diminué sans fatigue + exaltation + désinhibition = manie ; le trouble bipolaire se traite par thymorégulateur à vie — jamais d'antidépresseur seul (risque de virage maniaque)."}
,
{n:"Dysthymie et cyclothymie",q:"dysthymie",
d:"Troubles de l'humeur chroniques et atténués : dysthymie (trouble dépressif persistant — humeur dépressive la plupart du temps pendant au moins 2 ans, sans jamais atteindre les critères d'épisode dépressif caractérisé complet) ; cyclothymie : oscillations chroniques (au moins 2 ans) entre hypomanie atténuée et dépression légère, sans épisodes complets.",
s:"Dysthymie : tristesse de fond, asthénie, faible estime de soi, culpabilité, pessimisme, troubles du sommeil et de l'appétit modérés, fonctionnement préservé mais pénible (« la déprime » durable) ; cyclothymie : alternances sur des jours-semaines d'une hyperactivité légère et d'un fond dépressif, souvent à l'adolescence ; risque d'évolution vers un trouble bipolaire.",
dx:"Clinique sur la durée (2 ans de symptômes) ; recherche d'épisodes dépressifs caractérisés ou d'hypomanies vraies (qui reclasseraient le trouble) ; éliminer les causes organiques (hypothyroïdie, carences) et l'abus de substances ; évaluation du retentissement et du risque suicidaire.",
t:"Psychothérapie (TCC, thérapies interpersonnelles) au premier plan ; antidépresseurs (ISRS) si retentissement significatif ou résistance à la psychothérapie ; hygiène de vie (rythmes, sommeil, activité physique, alcool) ; cyclothymie : stabilisation des rythmes, psychoéducation, thymorégulateurs si aggravation ; suivi prolongé.",
k:"Une humeur dépressive « de toujours » pendant plus de 2 ans = dysthymie ; chez le cyclothymique, surveiller l'évolution vers un trouble bipolaire complet."}
]},
{name:"Troubles Anxieux & Liés au Stress",paths:[
{n:"Trouble Anxieux Généralisé (TAG) et Trouble panique",q:"trouble panique",ur:true,
d:"Trouble anxieux généralisé : inquiétude excessive et incontrôlable sur divers événements (au moins 6 mois), tension et symptômes physiques ; trouble panique : attaques de panique spontanées et récurrentes (peur intense avec symptômes physiques crescendo en 10 min), avec anxiété anticipatoire et comportements d'évitement.",
s:"TAG : soucis permanents, irritabilité, fatigabilité, troubles de la concentration, tensions musculaires, insomnie ; attaque de panique : palpitations, douleur thoracique, sensation d'étouffement, tremblements, paresthésies, peur de mourir ou de devenir fou, déréalisation ; la première attaque amène souvent aux urgences (« faux infarctus ») ; attaques situationnelles avec agoraphobie secondaire.",
dx:"Clinique (échelles : GAD-7, échelle de panique) ; éliminer les causes organiques de la première attaque : ECG, thyroïde, glycémie, caféine et toxiques, épilepsie temporale, phéochromocytome (rare) ; recherche de la dépression associée ; retentissement et évitements.",
t:"TCC de première intention (relaxation, exposition, restructuration cognitive) ; ISRS (préféré aux benzodiazépines : efficacité à long terme sans dépendance) ; benzodiazépines en cure courte pour l'acutisation, jamais au long cours ; respiration et hygiène de vie (café, alcool) ; information sur la nature bénigne et la mécanique de l'attaque.",
k:"Palpitations + oppression + peur de mourir en crescendo de 10 minutes = attaque de panique : ECG rassurant une fois, puis TCC et ISRS ; les benzodiazépines au long cours créent la dépendance qu'elles prétendent éviter."}
,
{n:"Phobies spécifiques et phobie sociale",q:"phobie sociale",
d:"Phobie spécifique : peur intense et irrationnelle d'un objet ou d'une situation (animaux, sang-injections, hauteurs, transports, situations confinées) avec évitement ; phobie sociale (anxiété sociale) : peur du regard et du jugement d'autrui (exposé, rencontre, restaurant), évitement social avec retentissement scolaire et professionnel.",
s:"Exposition à l'objet ou à la situation : anxiété majeure, voire attaque de panique, avec évitement ou endurance dans la souffrance ; phobie sociale : rougissement, tremblements, diarrhée anticipatoire, évitement des présentations et des interactions ; l'inhibition et la consommation d'alcool « pour tenir » aggravent le trouble ; la phobie des injections s'accompagne de réactions vagales (malaise).",
dx:"Clinique (critères DSM-5, durée supérieure à 6 mois) ; retentissement fonctionnel ; rechercher la dépression et la consommation de toxiques (alcool) ; pas d'examen complémentaire systématique.",
t:"Traitement de choix : thérapie cognitivo-comportementale avec exposition graduée (efficacité durable) ; phobie sociale : TCC (exposition sociale, entraînement aux habiletés), ISRS ou IMAO selon la sévérité ; phobie spécifique : le médicament a peu de place, l'exposition guérit ; traitement des réactions vagales (phobie du sang : tension musculaire).",
k:"La phobie se soigne par l'exposition graduée (TCC), pas par l'évitement ni les anxiolytiques ; dans la phobie sociale, l'alcool « facilitant » installe une double dépendance."}
,
{n:"Trouble Obsessionnel-Compulsif (TOC)",q:"trouble obsessionnel compulsif",
d:"TOC : obsessions (idées, images ou impulsions intrusives, répétitives, vécues comme absurdes et sources d'angoisse) et compulsions (comportements répétitifs destinés à neutraliser : lavage, vérification, comptage, ordre, rituels mentaux) ; chronique et invalidant, souvent méconnu (honte, secret).",
s:"Obsessions de contamination (lavage des mains des dizaines de fois), de doute (vérifications des portes et gaz), de symétrie et d'exactitude, agressives ou sexuelles (effroi du patient), religieuses ou scrupuleuses ; compulsions manifestes ou mentales (récitation, comptage) ; durée journalière importante (supérieure à 1 h), retentissement majeur ; comorbidités : dépression, tics, anxiété.",
dx:"Clinique (Y-BOCS : sévérité) ; critères DSM-5 (obsessions ou compulsions reconnues comme excessives le plus souvent) ; recherche des comorbidités (tics, dépression, troubles alimentaires) ; absence de déficit de conscience du caractère absurde possible ; bilan avant traitement médicamenteux.",
t:"TCC avec exposition et prévention de la réponse (EPR — traitement de référence) ; ISRS à forte dose (ou clomipramine) pendant 8-12 semaines avant conclure à l'échec ; formes sévères résistantes : association, augmentation, rTMS, parfois neurochirurgie fonctionnelle ; prise en charge familiale (les proches ne doivent pas participer aux rituels) ; soutien des associations.",
k:"Lavage et vérification répétitifs, reconnus absurdes mais incontournables = TOC : exposition avec prévention de la réponse + ISRS à forte dose ; la famille ne doit pas « aider » à vérifier."}
,
{n:"Trouble de Stress Post-Traumatique (TSPT / PTSD)",q:"état de stress post-traumatique",
d:"TSPT : apparition après un événement traumatique (menace de mort, violence, agression, accident, catastrophe, combat) d'un syndrome associant reviviscences, évitements, hyperactivité neurovégétative et altérations de la cognition et de l'humeur, pendant plus d'un mois ; les femmes en âge de toutes les populations, professions exposées incluses.",
s:"Reviviscences (cauchemars répétitifs, flashbacks, détresse aux rappels), évitements (lieux, pensées, personnes), hypervigilance (sursaut, insomnie, irritabilité), anesthésie affective, culpabilité du survivant, perte d'intérêt ; symptômes dissociatifs aigus (réaction immédiate) ; comorbidités : dépression, addictions, troubles somatiques.",
dx:"Clinique (critères DSM-5, échelle PCL) ; délai supérieur à 1 mois (en deçà : réaction aiguë au stress) ; évaluation du risque suicidaire et des comorbidités ; le récit du trauma n'est pas systématiquement nécessaire au premier entretien (ne pas forcer).",
t:"Psychothérapies basées sur le trauma : thérapie cognitivo-comportementale focalisée sur le trauma (exposition progressive), EMDR (désensibilisation) ; traitement précoce des réactions aigues (information, soutien, debriefing non systématique) ; ISRS (sévérité ou comorbidité) ; prise en charge des addictions associées ; thérapie de groupe et entraide (vétérans, victimes) ; suivi prolongé.",
k:"Après un événement menaçant : reviviscences + évitement + hypervigilance pendant plus d'un mois = TSPT (les thérapies focalisées sur le trauma et l'EMDR guérissent) ; ne jamais forcer le récit."}
]}
]},

{id:"neuro-addict",num:4,name:"Addictologie, Troubles du Sommeil & Géronto-Psychiatrie",groups:[
{name:"Addictions & Dépendances",paths:[
{n:"Alcoolisme chronique, syndrome de sevrage alcoolique et delirium tremens (Wernicke-Korsakoff)",q:"sevrage alcoolique",ur:true,
d:"Trouble de l'usage de l'alcool (consommation avec dépendance : perte de contrôle, tolérance, craving) ; le sevrage (8-48 h après l'arrêt) va du syndrome mineur (tremblements, sueurs, anxiété) au delirium tremens (confusion, hallucinations, tremblements majeurs, déshydratation, mortalité 5-15 %) ; l'encéphalopathie de Gayet-Wernicke (carence en B1) précède le syndrome de Korsakoff (amnésie irréversible).",
s:"Dépendance : consommation matinale, incapacité à arrêter, grosses conséquences (travail, famille) ; sevrage : tremblements, sueurs, tachycardie, HTA, anxiété, insomnie, crises comitiales (6-48 h), hallucinose ; delirium tremens (48-72 h) : confusion majeure, hallucinations visuelles, tremblements intenses, fièvre, collapsus ; Wernicke : confusion, ataxie, ophtalmoplégie (triade incomplète le plus souvent) ; Korsakoff : amnésie antérograde, fabulations.",
dx:"CAGE, AUDIT (dépistage) ; gamma-GT et VGM élevés, cytolyse, NFS ; sevrage : ionogramme, magnésémie, glycémie, thiamine ; jamais de glucose avant la vitamine B1 ; delirium tremens : hospitalisation (détresse, fièvre, déshydratation) ; IRM si suspicion de Wernicke (atrophie mammillaire).",
t:"Sevrage encadré : benzodiazépines (diazépam ou oxazépam selon le foie) à doses dégressives, réhydratation, vitamine B1 systématique avant toute perfusion glucosée, correction du magnésium et du potassium ; delirium tremens : hospitalisation en soins intensifs, benzodiazépines fortes ; Wernicke : thiamine IV forte dose d'urgence ; l'abstinence : psychothérapies, groupes d'entraide, naltrexone ou acamprosate, disulfiram, suivi addictologique ; complications somatiques (cirrhose, pancréatite, cardiomyopathie, cancers) à dépister.",
k:"Toute consommation d'alcool à risque = vitamine B1 avant le glucose (prévention du Wernicke) ; le delirium tremens est une urgence vitale : benzodiazépines, B1, réhydratation en soins intensifs."}
,
{n:"Dépendance aux opiacés, à la cocaïne, au cannabis et aux stimulants",q:"dépendance aux opiacés",ur:true,
d:"Troubles de l'usage des substances : opiacés (héroïne, oxycodone — dépendance rapide, overdose : myosis, bradypnée, coma), cocaïne et crack (stimulant, complications cardiovasculaires et psychiatriques), cannabis (le plus consommé, psychose chez le vulnérable), stimulants type amphétamines (risque de psychose et de dépression).",
s:"Opiacés : craving, tolérance, syndrome de sevrage à l'arrêt (douleurs, diarrhée, mydriase, chair de poule, éternuations, frissons) à distinguer du manque ; overdose : trouble de conscience avec myosis et bradypnée (urgence : naloxone) ; cocaïne : euphorie puis dysphorie, complications cardiaques (IDM, arythmie), AVC, paranoïa ; cannabis : amotivation, mémoire, psychose ; stimulants : insomnie, amaigrissement, psychose.",
dx:"Interrogatoire non jugeant, évaluation de la dépendance et des voies (injection : VIH, VHC) ; toxicologie urinaire ; bilan somatique : VIH, VHC, NFS, hépatique, cardiaque (cocaïne) ; complications infectieuses (abcès, endocardite) ; évaluation psychiatrique (dépression, psychose, suicide).",
t:"Opiacés : traitements de substitution (buprénorphine — Subutex, méthadone) + suivi addictologique et psychosocial ; overdose : naloxone IM ou IV (à répéter), maintien des fonctions, formation à la naloxone de l'entourage ; sevrage opiacé : substitution progressive, clonidine, antalgiques ; cocaïne et stimulants : pas de substitution — psychothérapies (contingence), traitement des complications ; cannabis : TCC, information (psychose) ; tous : réduction des risques (échange de seringues, tests), prise en charge des comorbidités psychiatriques.",
k:"Coma + myosis + bradypnée = overdose d'opiacés : naloxone immédiate (à répéter, demi-vie courte) ; la buprénorphine et la méthadone stabilisent la dépendance aux opiacés et diminuent la mortalité."}
,
{n:"Addiction aux jeux de hasard et d'argent / troubles comportementaux liés aux écrans",q:"addiction aux jeux",
d:"Addictions comportementales : jeux de hasard et d'argent (addiction la mieux décrite : perte de contrôle, mise croissante, « chasse » aux pertes, mensonges) ; jeux vidéo en ligne (usage problématique : préoccupation, tolérance, retrait, déscolarisation) et usage problématique des écrans et réseaux sociaux (scrolling compulsif, cyberdépendance, cyberharcèlement chez l'adolescent).",
s:"Jeux d'argent : préoccupation croissante, besoin de miser davantage, tentatives d'arrêt infructueuses, dette, mensonges à l'entourage, jeu de « rattrapage » des pertes, mise en jeu la relation familiale et professionnelle ; écrans : temps croissant au détriment du sommeil, de l'école et de la sociabilité, irritabilité au sevrage, échec des tentatives de limitation ; comorbidités : dépression, anxiété, TDAH.",
dx:"Évaluation du comportement (échelles : PGSI pour les jeux d'argent) ; retentissement financier, familial, scolaire ou professionnel ; dépistage des comorbidités psychiatriques et de l'alcool ; dette à objectiver ; pas de critère biologique.",
t:"Psychothérapies (TCC, entretien motivationnel) au premier plan ; groupes d'entraide (Joueurs anonymes) ; mesures de protection : interdiction volontaire de jeux, contrôle des accès financiers, aidants financiers ; traitement des comorbidités ; écrans : hygiène numérique négociée (pas d'interdiction brutale), activités alternatives, rétablissement du sommeil et de la scolarité ; accompagnement familial ; formes sévères : structures addictologiques dédiées.",
k:"Perte de contrôle sur l'argent misé et « chasse » aux pertes = addiction aux jeux : l'interdiction volontaire de jeu et le contrôle des accès financiers soutiennent la psychothérapie."}
]},
{name:"Troubles du Sommeil",paths:[
{n:"Insomnies chroniques primaires et secondaires",q:"insomnie",
d:"Insomnie chronique (plus de 3 nuits par semaine pendant plus de 3 mois, avec retentissement diurne) : primaire (psychophysiologique : hyperactivation, mauvaises habitudes) ou secondaire (dépression, anxiété, douleur, reflux, hyperthyroïdie, médicaments, alcool, sevrage) ; la plainte : difficulté d'endormissement, réveils nocturnes ou trop matinaux.",
s:"Difficultés d'endormissement (ruminations), réveils prolongés, réveil précoce avec fatigabilité diurne, irritabilité, troubles de l'attention ; comportements inadéquats installés : temps passé au lit éveillé, siestes, café, écrans nocturnes, alcool « pour dormir » (fragmentation du sommeil) ; l'anxiété de performance (peur de ne pas dormir) entretient l'insomnie.",
dx:"Agenda du sommeil (2 semaines : heures, réveils, siestes) ; interrogatoire (hygiène, substances, symptômes d'apnées et de jambes sans repos, dépression) ; éliminer les causes secondaires ; polysomnographie seulement si doute (apnées, mouvements périodiques).",
t:"Traitement de première intention : thérapie cognitivo-comportementale de l'insomnie (TCC-I : contrôle des stimulus, restriction du temps de de sommeil, hygiène, restructuration des croyances) ; hygiène du sommeil (horaires réguliers, pas d'écrans ni de café, chambre dédiée) ; hypnotiques (zolpidem, zopiclone) en cure courte seulement (dépendance, chutes du sujet âgé) ; traitement de la cause secondaire ; lumière du jour et activité physique.",
k:"L'insomnie chronique se traite par TCC-I, pas par les hypnotiques au long cours (dépendance, chutes, mémoire) ; l'agenda du sommeil est l'examen clé."}
,
{n:"Syndrome d'Apnées-Hypopnées Obstructives du Sommeil (SAOS) et retentissement neuropsychologique",q:"apnées du sommeil",
d:"SAOS : collapsus répété du pharynx pendant le sommeil (ronflements, apnées observées, désaturations) chez le sujet en surpoids, avec somnolence diurne excessive ; retentissement cardiovasculaire (HTA, risque cardiovasculaire) et neuropsychologique (attention, mémoire, humeur, accidentologie au travail et au volant).",
s:"Ronflements sonores, apnées observées par le conjoint, réveils en sursaut avec sensation d'étouffement, nycturie, céphalées matinales, somnolence diurne (endormissements au volant — danger légal et vital), fatigue, irritabilité, troubles cognitifs (attention, mémoire de travail), dépression ; obésité, tour de cou augmenté, rétrognathie.",
dx:"Polysomnographie ou polygraphie ventilatoire (index apnées-hypopnées ≥ 5/h avec symptômes) ; questionnaire d'Epworth (somnolence) ; bilan cardiovasculaire (TA, HTA résistante), glycémie ; avis ORL (obstacle anatomique) ; évaluation cognitive et thymique si plainte.",
t:"Pression positive continue (PPC) nocturne — traitement de référence, efficacité sur la somnolence, la tension et la cognition ; orthèse d'avancée mandibulaire (formes légères, intolérance) ; perte de poids (souvent curatrice des formes modérées), arrêt de l'alcool et des sédatifs du soir ; chirurgie ORL sélectionnée (amygdales, chirurgie maxillo-mandibulaire) ; information sur la conduite et le travail à risque.",
k:"Ronflements + apnées observées + somnolence au volant = SAOS : polygraphie, PPC ; c'est une maladie cardiovasculaire et cognitive autant qu'un trouble du sommeil."}
,
{n:"Narcolepsie et hypersomnies idiopathiques",q:"narcolepsie",
d:"Narcolepsie de type 1 (avec cataplexie) : hypersomnie centrale par perte des neurones à orexine (hypocrétine), début chez l'adolescent et l'adulte jeune ; cataplexie (chutes du tonus déclenchées par l'émotion), paralysies du sommeil et hallucinations hypnagogiques ; type 2 sans cataplexie ; hypersomnie idiopathique (sommeil long, réveil difficile, pas de cataplexie).",
s:"Somnolence diurne permanente avec endormissements soudains irrésistibles (micro-siestes rafraîchissantes), cataplexie (dérobement des jambes, chute du visage au rire — le signe spécifique), hallucinations hypnagogiques (au à l'endormissement), paralysies du sommeil (réveil avec incapacité à bouger, effrayante), sommeil nocturné fragmenté ; hypersomnie idiopathique : sommeil profond et long, ivresse du sommeil au réveil, siestes non rafraîchissantes.",
dx:"Consultation de sommeil : agenda, échelle d'Epworth ; polysomnographie puis tests itératifs de latence d'endormissement (latence moyenne ≤ 8 min, endormissements en sommeil paradoxal) ; taux d'hypocrétine du LCR abaissé (type 1) ; IRM si atypie ; éliminer les autres hypersomnies (SAOS, dépression, médicaments, privation de sommeil).",
t:"Traitement symptomatique à vie : stimulants de l'éveil (modafinil, méthylphénidate, pitolisant) ; cataplexie : oxybate de sodium (ou antidépresseurs sérotoninergiques) ; organisation des siestes programmées ; information du patient et de l'entourage (conduite, travail) ; associations de patients ; suivi dans les centres du sommeil.",
k:"Somnolence irrésistible + dérobement au rire (cataplexie) = narcolepsie type 1 : tests itératifs de latence et hypocrétine du LCR ; siestes programmées et traitement de l'éveil."}
,
{n:"Parasomnies (terreurs nocturnes, somnambulisme, trouble du comportement en sommeil paradoxal)",q:"parasomnie",
d:"Parasomnies : épisodes indésirables du sommeil — éveils confusionnels et terreurs nocturnes (sommeil lent profond, premier tiers de la nuit, chez l'enfant), somnambulisme (déambulation les yeux ouverts, amnésie) ; trouble du comportement en sommeil paradoxal (TCSP) : perte de l'atonie du sommeil paradoxal, le patient « joue ses rêves » (cris, gestes violents) — chez l'homme de plus de 50 ans, il annonce souvent une maladie neurodégénérative (synucléinopathie : Parkinson, Lewy).",
s:"Terreurs nocturnes : cri brutal, terreur, signes végétatifs, enfant difficile à réveiller puis rendormissement, amnésie totale (à distinguer du cauchemar : réveil complet, souvenir) ; somnambulisme : lever, déambulation, gestes complexes, yeux ouverts, amnésie ; TCSP : rêves violents (bagarres, fuite), blessures du patient ou du conjoint, souvenir onirique riche au réveil.",
dx:"Anamnèse et vidéo (domicile) ; polysomnographie (TCSP : tonus musculaire exagéré en sommeil paradoxal, critère diagnostique ; somnambulisme : éveils confusionnels du sommeil lent) ; IRM et suivi neurologique du TCSP (risque de conversion en parkinsonien à 10 ans) ; sécurité de la chambre.",
t:"Sécurisation de l'environnement (matelas au sol, verrous, objets dangereux retirés) ; hygiène du sommeil et restriction du sommeil (facteurs déclenchants) ; terreurs et somnambulisme de l'enfant : rassurer, réveil programmé préventif, évolution bénigne ; TCSP : clonazépam au coucher (ou mélatonine forte dose) ; traitement des causes (apnées, médicaments déclencheurs : antidépresseurs sérotoninergiques) ; suivi neurologique du TCSP.",
k:"L'adulte d'âge mûr qui « joue ses rêves » avec blessures nocturnes = trouble du comportement en sommeil paradoxal : polysomnographie, clonazépam, et suivi neurologique (précurseur fréquent de Parkinson)."}
]},
{name:"Géronto-Psychiatrie & Troubles du Comportement",paths:[
{n:"Syndrome confusionnel aigu (delirium) de la personne âgée",q:"delirium",ur:true,
d:"Confusion aiguë de la personne âgée : trouble attentionnel fluctuant avec désorientation, troubles de la conscience et du cycle veille-sommeil, souvent nocturne ; jamais normal à cet âge, c'est un signal d'alarme d'une cause sous-jacente (infection, rétention, médicaments, métabolique, douleur, AVC, constipation) ; le sujet âgé se confuse pour peu.",
s:"Apparition brutale (heures-jours) : inattention, désorientation temporelle puis spatiale, propos incohérents, hallucinations visuelles, agitation nocturne et somnolence diurne, fluctuation des symptômes (lucidité par intermittence) ; formes apathiques ou agitées ; terrain : démence préexistante (facteur de risque majeur), hospitalisation, chirurgie.",
dx:"Recherche systématique de la cause : infection (ECBU — la cause la plus fréquente —, pulmonaire), rétention aiguë d'urine (globe), fécalome, bilan métabolique (hyponatrémie, hypercalcémie, hypoglycémie), iatrogénie (nouveaux médicaments : benzodiazépines, anticholinergiques, opioïdes), hypoxie, douleur, AVC (TDM si déficit) ; échelle CAM au lit du malade.",
t:"Traitement de la cause (souvent multiple) ; mesures non pharmacologiques : réorientation (horloge, calendrier, lunettes, prothèses auditives), présence familiale, environnement calme et éclairé le jour, lutte contre la privation de sommeil ; contention physique à éviter absolument ; sédation médicamenteuse seulement si danger vital immédiat (faibles doses de neuroleptique, prudence) ; lever précoce, hydratation, nutrition ; prévention (personnes âgées hospitalisées : programme de prévention du delirium).",
k:"Toute confusion aiguë chez le sujet âgé a une cause (ECBU, globe, fécalome, iatrogénie en tête) : la traiter, ne jamais sédater sans chercher ; la contention aggrave."}
,
{n:"Troubles du comportement associés à la démence (agressivité, déambulation, apathie)",q:"troubles du comportement de la démence",
d:"Symptômes psycho-comportementaux de la démence : agitation, agressivité (verbale ou physique), déambulation, errance, cri, comportements moteurs aberrants, apathie, troubles du sommeil, comportements sexuels désinhibés, idées délirantes (vol, identification erronée) et hallucinations ; surajoutés au déclin cognitif, ils épuisent l'aidant et précipitent l'institutionnalisation.",
s:"Agitation verbale ou physique (coups, cris, refus de soins), déambulation sans but et tentatives de sortie (risque d'errance et de fugue), hoarding (accumulation), désinhibition, apathie (abandon des activités), troubles du rythme veille-sommeil avec inversion nycthémérale, symptômes à prédominance vespérale (sundowning) ; délire du vol et de la maison (identification de l'aidant comme étranger).",
dx:"Évaluation du contexte : douleur (souvent en cause, ECPA : échelle comportementale de la douleur), infection, rétention, constipation, iatrogénie (anticholinergiques) = toujours éliminer un facteur déclenchant ; horizon de la démence (stade, type : Lewy et fronto-temporale les plus comportementales) ; charge de l'aidant ; les comportements analysés comme une communication (besoin non exprimé).",
t:"Mesures non pharmacologiques d'abord (recommandées) : identifier le besoin, activités adaptées, musicothérapie, réminiscence, environnement stable et sécurisé (errance sécurisée), éducation et répit des aidants ; traiter la douleur et les facteurs somatiques ; médicaments en dernier recours : doses minimales de neuroleptique (risperidone approuvée à court terme) avec surveillance (chutes, AVC, mortalité accrue — contre-indiqués dans la démence à corps de Lewy) ; antidépresseurs si humeur ; protection juridique si nécessaire.",
k:"Derrière un trouble du comportement d'un dément : chercher la douleur, l'infection, la rétention ou le médicament (ECPA) ; mesures non médicamenteuses d'abord, neuroleptiques en dernier recours, jamais dans la démence à corps de Lewy."}
,
{n:"Dépression du sujet âgé et syndrome de glissement",q:"dépression de la personne âgée",
d:"Dépression de la personne âgée : fréquente, sous-diagnostiquée et sous-traitée, souvent atypique (complaintes somatiques, douleurs, ralentissement, pseudo-démence dépressive) ; le risque suicidaire est élevé (idées délirantes de ruine et d'indignité) ; le syndrome de glissement (décrochage psychocomportemental après un événement : deuil, chute, hospitalisation) en est l'expression extrême : refus alimentaire, mutisme, alitement.",
s:"Asthénie, anorexie, perte de poids, insomnie, douleurs somatiques multiples, ralentissement, perte d'intérêt, repli, anhédonie, irritabilité ; plaintes cognitives (pseudodémence : « je perds la mémoire » — en fait attentionnelle) ; signes psychotiques : culpabilité, ruine, indignité ; le sujet âgé nie souvent la tristesse (alexithymie, générations) ; suicide : passage à l'acte silencieux, méthodes létales.",
dx:"Échelles gériatriques (GDS, mini-GDS) ; éliminer les causes organiques : hypothyroïdie, carence B12, anémie, iatrogénie (bêtabloquants, corticoïdes), douleur chronique, constipation ; évaluation cognitive (avant et après traitement de l'humeur) ; évaluation du risque suicidaire et du contexte social (isolement, deuil).",
t:"Antidépresseur (ISRS à doses progressives, surveillance hyponatrémie et digestion) : efficacité démontrée à tout âge, réévaluation à 6-8 semaines ; psychothérapies adaptées (rappels de vie, TCC) ; syndrome de glissement : hospitalisation, réhabilitation nutritionnelle et motrice, stimulations, soutien social ; prévention : suivi des deuils et hospitalisations, activations ; électroconvulsivothérapie des formes sévères ou psychotiques (rapide et efficace) ; vigilance suicide durable.",
k:"Chez le sujet âgé, la dépression prend le masque du corps et de la mémoire : traiter l'humeur avant de conclure à la démence (pseudodémence réversible) ; le risque suicidaire est majeur."}
]}
]}
]});



</script>
<script>
"use strict";
/* ================= Helpers ================= */
var $=function(s){return document.querySelector(s)};
function esc(s){return String(s).replace(/[&<>"']/g,function(c){return{"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c]})}
function trunc(s,n){if(s.length<=n)return s;return s.slice(0,n).replace(/\s+\S*$/,"")+"…"}
function norm(s){return String(s).toLowerCase().normalize("NFD").replace(/[\u0300-\u036f]/g,"")}
function shuffleArr(a){a=a.slice();for(var i=a.length-1;i>0;i--){var j=Math.floor(Math.random()*(i+1));var t=a[i];a[i]=a[j];a[j]=t}return a}
function rnd(arr){return arr[Math.floor(Math.random()*arr.length)]}

/* ================= Index ================= */
var IDX={},ALL=[],IDXDEPT={};
DEPTS.forEach(function(d){
  IDXDEPT[d.id]=d;
  d.specs.forEach(function(sp){
    sp.groups.forEach(function(g,gi){
      g.paths.forEach(function(p,pi){
        var id=d.id+"-"+sp.id+"-"+gi+"-"+pi;
        var node={id:id,dept:d,spec:sp,group:g,gi:gi,pi:pi,p:p};
        g._gi=gi;p._pi=pi;p._id=id;
        IDX[id]=node;ALL.push(node);
      });
    });
  });
});
function nodesOfDept(d){return ALL.filter(function(n){return n.dept===d})}
function nodesOfSpec(sp){return ALL.filter(function(n){return n.spec===sp})}
function specById(id){for(var i=0;i<DEPTS.length;i++){for(var j=0;j<DEPTS[i].specs.length;j++){if(DEPTS[i].specs[j].id===id)return DEPTS[i].specs[j]}}return null}

/* ================= Progression (localStorage) ================= */
var LSK="mpr_v1";
var PROG=loadProg();
function loadProg(){try{return JSON.parse(localStorage.getItem(LSK)||"{}")}catch(e){return{}}}
function saveProg(){try{localStorage.setItem(LSK,JSON.stringify(PROG))}catch(e){}}
function stOf(id){var v=PROG[id];return v?v.st:0}
function setSt(id,v){if(v)PROG[id]={st:v,ts:Date.now()};else delete PROG[id];saveProg()}
function statsOf(nodes){var ok=0,rev=0;nodes.forEach(function(n){var s=stOf(n.id);if(s===1)ok++;else if(s===2)rev++});return{ok:ok,rev:rev,total:nodes.length}}
function stPill(id){var s=stOf(id);if(!s)return"";return s===1?'<span class="badge ok st">✓</span>':'<span class="badge warn st">↻</span>'}

/* ================= Lien MSD ================= */
function msdUrl(p){return "https://www.msdmanuals.com/fr/professional/SearchResults?query="+encodeURIComponent(p.q||p.n)}

/* ================= Thème ================= */
function applyTheme(t){document.documentElement.setAttribute("data-theme",t);$("#themeBtn").textContent=t==="dark"?"☀️":"🌙";try{localStorage.setItem("mpr_theme",t)}catch(e){}}
(function(){var t=null;try{t=localStorage.getItem("mpr_theme")}catch(e){}
if(!t)t=(window.matchMedia&&window.matchMedia("(prefers-color-scheme: dark)").matches)?"dark":"light";
applyTheme(t)})();
$("#themeBtn").addEventListener("click",function(){applyTheme(document.documentElement.getAttribute("data-theme")==="dark"?"light":"dark")});

/* ================= Recherche ================= */
function doSearch(term){
  var t=norm(term.trim());
  if(t.length<2)return[];
  var res=[];
  ALL.forEach(function(n){
    var nn=norm(n.p.n);var sc=-1;
    if(nn.indexOf(t)>=0)sc=nn.indexOf(t)===0?0:1;
    else if(norm(n.p.k).indexOf(t)>=0||norm(n.p.t).indexOf(t)>=0||norm(n.p.dx).indexOf(t)>=0)sc=2;
    else if(norm(n.p.s).indexOf(t)>=0||norm(n.p.d).indexOf(t)>=0)sc=3;
    if(sc>=0)res.push({n:n,sc:sc});
  });
  res.sort(function(a,b){return a.sc-b.sc||a.n.p.n.localeCompare(b.n.p.n,"fr")});
  return res.slice(0,25);
}
function hi(text,term){
  var e=esc(text);
  if(!term||term.length<2)return e;
  try{var re=new RegExp("("+term.replace(/[.*+?^${}()|[\]\\]/g,"\\$&")+")","ig");return e.replace(re,"<mark>$1</mark>")}catch(err){return e}
}
function openSearch(){$("#searchpanel").classList.add("open");var i=$("#sp-input");i.focus();i.select()}
function closeSearch(){$("#searchpanel").classList.remove("open");$("#search").value="";$("#sp-input").value="";$("#sp-results").innerHTML=""}
function renderSearch(term){
  var box=$("#sp-results");
  var items=doSearch(term);
  if(!term||term.trim().length<2){box.innerHTML='<div class="sp-empty">Saisissez au moins 2 caractères…</div>';return}
  if(!items.length){box.innerHTML='<div class="sp-empty">Aucun résultat pour « '+esc(term)+' »</div>';return}
  box.innerHTML=items.map(function(r){
    var n=r.n;
    return '<a class="sp-item" href="#/p/'+n.id+'" data-close="1">'+
      '<div class="t">'+hi(n.p.n,term)+'</div>'+
      '<div class="b">'+esc(n.dept.name)+' › '+esc(n.spec.name)+'</div>'+
      '<div class="sn">'+hi(trunc(n.p.d,140),term)+'</div></a>';
  }).join("");
}
$("#search").addEventListener("focus",function(){openSearch();$("#sp-input").value=this.value;renderSearch(this.value)});
$("#search").addEventListener("input",function(){$("#sp-input").value=this.value;renderSearch(this.value)});
$("#sp-input").addEventListener("input",function(){renderSearch(this.value)});
$("#sp-close").addEventListener("click",closeSearch);
$("#searchpanel").addEventListener("click",function(e){if(e.target===this)closeSearch()});
$("#searchpanel").addEventListener("click",function(e){if(e.target.closest("[data-close]"))closeSearch()});$("#nav-search").addEventListener("click",function(e){e.preventDefault();openSearch()});
document.addEventListener("keydown",function(e){
  if(e.key==="Escape")closeSearch();
  var fcView=document.querySelector(".fc-card");
  if(e.key===" "&&fcView&&!e.target.closest("input,select,textarea,button")){e.preventDefault();flipCard()}
});

/* ================= Vues ================= */
function viewHome(){
  var totSpecs=DEPTS.reduce(function(a,d){return a+d.specs.length},0);
  var s=statsOf(ALL);
  var pct=s.total?Math.round(s.ok/s.total*100):0;
  var cards=DEPTS.map(function(d){
    var dn=nodesOfDept(d),st=statsOf(dn),p=st.total?Math.round(st.ok/st.total*100):0;
    return '<a class="card dept-card" href="#/dept/'+d.id+'" style="--dc:'+d.color+'">'+
      '<span class="ic">'+d.icon+'</span>'+
      '<span class="nm">'+esc(d.name)+'</span>'+
      '<span class="mt">'+d.specs.length+' spécialités · '+dn.length+' pathologies</span>'+
      '<span class="minibar" title="'+p+' % maîtrisées"><span style="width:'+p+'%"></span></span>'+
      '<span class="go">Explorer →</span></a>';
  }).join("");
  return ''+
  '<section class="hero">'+
    '<h1>Médecine Pratique<br>Plateforme de révision</h1>'+
    '<p>Toutes les pathologies du programme, organisées par départements et spécialités, avec fiches synthétiques enrichies d\u2019après les sources officielles (MSD Manuels, OMS, HAS…). Conçue pour réviser efficacement : fiches, flashcards et QCM.</p>'+
    '<div class="stats">'+
      '<span class="stat"><b>'+DEPTS.length+'</b>Départements</span>'+
      '<span class="stat"><b>'+totSpecs+'</b>Spécialités</span>'+
      '<span class="stat"><b>'+ALL.length+'</b>Pathologies</span>'+
      '<span class="stat"><b>100 %</b>Hors ligne</span>'+
    '</div>'+
    '<div class="quick">'+
      '<a class="btn white" href="#/revision">🃏 Fiches flashcards</a>'+
      '<a class="btn white" href="#/qcm">❓ QCM d\u2019entraînement</a>'+
      '<a class="btn white" href="#/sources">📚 Sources</a>'+
    '</div>'+
  '</section>'+

  '<div class="section"><div class="card progress-card">'+
    '<div class="bigbar">'+
      '<div class="p-label"><span>Progression globale</span><span>'+s.ok+' / '+s.total+' maîtrisées ('+pct+' %)</span></div>'+
      '<div class="minibar" style="height:10px"><span style="width:'+pct+'%"></span></div>'+
    '</div>'+
    '<div class="pcounts">'+
      '<span class="badge ok">✓ '+s.ok+' maîtrisées</span>'+
      '<span class="badge warn">↻ '+s.rev+' à revoir</span>'+
      '<span class="badge off">• '+Math.max(0,s.total-s.ok-s.rev)+' non vues</span>'+
      '<span class="spacer"></span>'+
      '<button class="btn sm ghost" data-act="reset-prog">Réinitialiser</button>'+
    '</div>'+
  '</div></div>'+

  '<div class="section"><h2>Départements & spécialités</h2><div class="grid depts">'+cards+'</div></div>'+

  '<div class="section"><h2>Comment réviser ?</h2><div class="grid" style="grid-template-columns:repeat(auto-fill,minmax(240px,1fr))">'+
    '<div class="card" style="padding:16px"><h3 style="font-size:.95rem;margin-bottom:6px">1 · Lire les fiches</h3><p class="muted" style="font-size:.88rem">Chaque pathologie comporte une définition, les signes cliniques, les examens clés, le traitement et un point clé à retenir. Marquez chaque fiche « maîtrisée » ou « à revoir ».</p></div>'+
    '<div class="card" style="padding:16px"><h3 style="font-size:.95rem;margin-bottom:6px">2 · Mémoriser</h3><p class="muted" style="font-size:.88rem">Le mode Fiches (flashcards) propose un paquet de cartes par spécialité ou département, à retourner de mémoire, avec évaluation « je savais / à revoir ».</p></div>'+
    '<div class="card" style="padding:16px"><h3 style="font-size:.95rem;margin-bottom:6px">3 · S\u2019évaluer</h3><p class="muted" style="font-size:.88rem">Le mode QCM génère automatiquement des questions (définitions, signes cliniques, rattachement à la spécialité) avec correction immédiate et score final.</p></div>'+
  '</div></div>';
}

function viewDept(d){
  var dn=nodesOfDept(d),st=statsOf(dn),p=st.total?Math.round(st.ok/st.total*100):0;
  var accs=d.specs.map(function(sp,si){
    var open=OPENED.has(sp.id)?true:(CLOSED.has(sp.id)?false:si===0);
    var sn=nodesOfSpec(sp),sst=statsOf(sn);
    var groups=sp.groups.map(function(g){
      return '<div class="grp"><h4>'+esc(g.name)+'</h4><ul class="plist">'+
        g.paths.map(function(pp){
          return '<li><a href="#/p/'+pp._id+'"><span class="nm">'+esc(pp.n)+'</span>'+
            (pp.ur?'<span class="badge urg">Urgence</span>':'')+stPill(pp._id)+
            '<span class="chev" style="color:var(--muted)">›</span></a></li>';
        }).join("")+'</ul></div>';
    }).join("");
    return '<div class="card acc'+(open?" open":"")+'" data-spec="'+sp.id+'">'+
      '<button class="acc-head" data-act="acc"><span class="num">'+sp.num+'</span>'+
      '<span class="ttl">'+esc(sp.name)+'<span class="cnt">'+sn.length+' pathologies · '+sst.ok+' ✓ maîtrisées</span></span>'+
      '<span class="chev">▸</span></button>'+
      '<div class="acc-body">'+groups+'</div></div>';
  }).join("");
  return ''+
  '<div class="crumbs"><a href="#/">Accueil</a><span class="sep">›</span><span>'+esc(d.name)+'</span></div>'+
  '<div class="card dept-head" style="--dc:'+d.color+'">'+
    '<span class="ic">'+d.icon+'</span>'+
    '<div><h1 class="pageh">'+esc(d.name)+'</h1><div class="mt" style="font-size:.85rem;color:var(--muted)">'+d.specs.length+' spécialités · '+dn.length+' pathologies</div></div>'+
    '<div class="dept-tools">'+
      '<a class="btn primary sm" href="#/revision?dept='+d.id+'">🃏 Réviser</a>'+
      '<a class="btn ghost sm" href="#/qcm?dept='+d.id+'">❓ QCM</a>'+
    '</div>'+
    '<p class="desc">'+esc(d.desc)+'</p>'+
    '<div class="desc" style="flex-basis:100%"><div class="p-label"><span>Progression du département</span><span>'+st.ok+' / '+st.total+' ('+p+' %)</span></div>'+
    '<div class="minibar" style="height:8px"><span style="width:'+p+'%"></span></div></div>'+
  '</div>'+
  accs;
}

function viewPath(node){
  var n=node,p=n.p,d=n.dept,sp=n.spec;
  var specList=nodesOfSpec(sp);
  var idx=specList.indexOf(n);
  var prev=idx>0?specList[idx-1]:null;
  var next=idx<specList.length-1?specList[idx+1]:null;
  var s=stOf(n.id);
  return ''+
  '<div class="crumbs"><a href="#/">Accueil</a><span class="sep">›</span><a href="#/dept/'+d.id+'">'+esc(d.name)+'</a><span class="sep">›</span><a href="#/dept/'+d.id+'">'+esc(sp.name)+'</a></div>'+
  '<div class="card" style="--dc:'+d.color+'">'+
    '<div class="path-head">'+
      '<div class="path-badges">'+
        '<span class="badge dept" style="--dc:'+d.color+'">'+d.icon+' '+esc(d.name)+'</span>'+
        '<span class="badge spec">'+esc(sp.name)+'</span>'+
        (p.ur?'<span class="badge urg">🚨 Urgence</span>':'')+
      '</div>'+
      '<h1>'+esc(p.n)+'</h1>'+
      '<div class="status-tools">'+
        '<button class="btn sm '+(s===1?"ok":"ghost")+'" data-act="st" data-v="1">✓ Je maîtrise</button>'+
        '<button class="btn sm '+(s===2?"warn":"ghost")+'" data-act="st" data-v="2">↻ À revoir</button>'+
        (s?'<button class="btn sm ghost" data-act="st" data-v="0">✕ Effacer</button>':'')+
      '</div>'+
    '</div>'+
    '<div class="sec-block"><h3>📖 Définition</h3><p>'+esc(p.d)+'</p></div>'+
    '<div class="sec-block"><h3>🩺 Signes cliniques</h3><p>'+esc(p.s)+'</p></div>'+
    '<div class="sec-block"><h3>🔬 Examens & diagnostic</h3><p>'+esc(p.dx)+'</p></div>'+
    '<div class="sec-block"><h3>💊 Traitement & prise en charge</h3><p>'+esc(p.t)+'</p></div>'+
    '<div class="sec-block key"><h3>⭐ Point clé</h3><p>'+esc(p.k)+'</p></div>'+
    '<div class="src-note">🔗 Source officielle : <a href="'+msdUrl(p)+'" target="_blank" rel="noopener">Consulter « '+esc(p.q||p.n)+' » sur MSD Manuels (édition professionnelle)</a> — lien externe, nécessite une connexion internet.</div>'+
  '</div>'+
  '<div class="pathnav">'+
    (prev?'<a class="btn ghost sm" href="#/p/'+prev.id+'">← '+esc(trunc(prev.p.n,44))+'</a>':'')+
    '<span class="spacer"></span>'+
    (next?'<a class="btn ghost sm" href="#/p/'+next.id+'">'+esc(trunc(next.p.n,44))+' →</a>':'')+
  '</div>';
}

function specOptions(selDept,selSpec){
  var html='<option value="">Toutes les spécialités</option>';
  DEPTS.forEach(function(d){
    if(selDept&&d.id!==selDept)return;
    html+='<optgroup label="'+esc(d.icon+" "+d.name)+'">'+d.specs.map(function(sp){
      return '<option value="'+sp.id+'">'+sp.num+". "+esc(sp.name)+'</option>';
    }).join("")+'</optgroup>';
  });
  return html;
}
function deptOptions(sel){
  return '<option value="">Tous les départements</option>'+DEPTS.map(function(d){
    return '<option value="'+d.id+'">'+esc(d.icon+" "+d.name)+'</option>';
  }).join("");
}
function scopePool(q){
  var sp=q.spec?specById(q.spec):null;
  if(sp)return nodesOfSpec(sp);
  if(q.dept&&IDXDEPT[q.dept])return nodesOfDept(IDXDEPT[q.dept]);
  return ALL;
}

/* ================= Flashcards ================= */
var FC=null;
function startDeck(q){
  var pool=scopePool(q).slice();
  if(q.todo)pool=pool.filter(function(n){return stOf(n.id)!==1});
  if(!pool.length)return false;
  FC={deck:q.shuffle===false?pool:shuffleArr(pool),i:0,flip:false,ok:0,rev:0,skip:0,scope:q};
  return true;
}
function flipCard(){if(!FC||FC.empty||FC.i>=FC.deck.length)return;FC.flip=!FC.flip;route()}
function fcMark(v){
  if(!FC||FC.i>=FC.deck.length)return;
  var n=FC.deck[FC.i];
  if(v)setSt(n.id,v);
  if(v===1)FC.ok++;else if(v===2)FC.rev++;else FC.skip++;
  FC.flip=false;FC.i++;route();
}
function viewRevision(q){
  if(FC&&!FC.empty&&FC.i<FC.deck.length)return viewDeck();
  if(FC&&FC.i>=FC.deck.length)return viewDeckEnd();
  var cnt=scopePool(q).length;
  return ''+
  '<div class="crumbs"><a href="#/">Accueil</a><span class="sep">›</span><span>Fiches flashcards</span></div>'+
  '<h1 class="pageh">🃏 Fiches flashcards</h1>'+
  '<p class="lead">Retournez chaque carte de mémoire, puis évaluez-vous : « je savais » ou « à revoir ». Votre progression est enregistrée sur cet appareil (aucune connexion nécessaire).</p>'+
  '<div class="card fc-setup" style="max-width:760px">'+
    '<div class="row">'+
      '<div class="field"><label for="rv-dept">Département</label><select id="rv-dept">'+deptOptions(q.dept)+'</select></div>'+
      '<div class="field"><label for="rv-spec">Spécialité</label><select id="rv-spec">'+specOptions(q.dept,q.spec)+'</select></div>'+
    '</div>'+
    '<div class="row">'+
      '<label class="checkline"><input type="checkbox" id="rv-shuffle" checked> Mélanger les cartes</label>'+
      '<label class="checkline"><input type="checkbox" id="rv-todo"> Seulement les non maîtrisées</label>'+
    '</div>'+
    '<div class="row">'+
      '<span class="muted" style="font-size:.85rem" id="rv-count">'+cnt+' cartes dans ce périmètre</span>'+
      '<span class="spacer"></span>'+
      '<button class="btn primary" data-act="fc-start">Commencer →</button>'+
    '</div>'+
  '</div>'+
  '<p class="muted" style="font-size:.8rem;margin-top:10px">Astuce : <kbd>Espace</kbd> retourne la carte.</p>';
}
function viewDeck(){
  var n=FC.deck[FC.i],p=n.p;
  var pct=Math.round(FC.i/FC.deck.length*100);
  var back=
    '<div class="fc-back">'+
    '<div><h4>📖 Définition</h4><p>'+esc(p.d)+'</p></div>'+
    '<div><h4>🩺 Signes cliniques</h4><p>'+esc(p.s)+'</p></div>'+
    '<div><h4>🔬 Diagnostic</h4><p>'+esc(p.dx)+'</p></div>'+
    '<div><h4>💊 Traitement</h4><p>'+esc(p.t)+'</p></div>'+
    '<div><h4>⭐ Point clé</h4><p>'+esc(p.k)+'</p></div>'+
    '</div>';
  var front=
    '<div class="fc-front">'+
    '<div class="path-badges" style="justify-content:center">'+
      '<span class="badge dept" style="--dc:'+n.dept.color+'">'+n.dept.icon+' '+esc(n.dept.name)+'</span>'+
      '<span class="badge spec">'+esc(n.spec.name)+'</span>'+
      (p.ur?'<span class="badge urg">🚨 Urgence</span>':'')+
    '</div>'+
    '<div class="n" style="margin-top:14px">'+esc(p.n)+'</div>'+
    '<div class="hint">Quelle est sa définition, ses signes, son diagnostic, son traitement ?<br>Touchez la carte pour voir la réponse.</div>'+
    '</div>';
  return ''+
  '<div class="crumbs"><a href="#/">Accueil</a><span class="sep">›</span><a href="#/revision">Fiches</a></div>'+
  '<div class="fc-deck">'+
    '<div class="fc-count"><span>Carte '+(FC.i+1)+' / '+FC.deck.length+'</span>'+
    '<span><button class="btn sm ghost" data-act="fc-new">⚙ Nouveau paquet</button></span></div>'+
    '<div class="deckbar"><span style="width:'+pct+'%"></span></div>'+
    '<div class="fc-card" data-act="fc-flip">'+(FC.flip?back:front)+'</div>'+
    '<div class="fc-actions">'+
      '<button class="btn warn" data-act="fc-mark" data-v="2">↻ À revoir</button>'+
      '<button class="btn ok" data-act="fc-mark" data-v="1">✓ Je savais</button>'+
      '<button class="btn ghost" data-act="fc-mark" data-v="0">→ Passer</button>'+
    '</div>'+
  '</div>';
}
function viewDeckEnd(){
  return ''+
  '<div class="crumbs"><a href="#/">Accueil</a><span class="sep">›</span><a href="#/revision">Fiches</a></div>'+
  '<div class="qz-card card" style="max-width:640px;margin:0 auto;text-align:center">'+
  '<h1 class="pageh">Paquet terminé ! 🎉</h1>'+
  '<div class="flex" style="justify-content:center;margin:16px 0">'+
    '<span class="badge ok">✓ '+FC.ok+' sues</span>'+
    '<span class="badge warn">↻ '+FC.rev+' à revoir</span>'+
    '<span class="badge off">→ '+FC.skip+' passées</span>'+
  '</div>'+
  '<div class="flex" style="justify-content:center">'+
    '<button class="btn primary" data-act="fc-again">Rejouer le même périmètre</button>'+
    '<button class="btn ghost" data-act="fc-new">Changer de périmètre</button>'+
  '</div></div>';
}

/* ================= QCM ================= */
var QZ=null;
function makeQ(node,pool){
  var types=["def","sig","spec"];
  var type=rnd(types);
  if(type==="spec"){
    var spOpts=[{n:node.spec.name,v:true}];
    var others=DEPTS.reduce(function(a,d){return a.concat(d.specs.map(function(s){return{s:s,dept:d}}))},[]).filter(function(o){return o.s.id!==node.spec.id});
    var same=others.filter(function(o){return o.dept===node.dept});
    var picks=(same.length>=3?same:others);
    shuffleArr(picks).slice(0,3).forEach(function(o){spOpts.push({n:o.s.name,v:false})});
    var opts=shuffleArr(spOpts);
    return{type:"spec",label:"Rattachement",prompt:node.p.n,node:node,opts:opts.map(function(o){return{t:o.n,v:o.v}})};
  }
  var opts=[{t:node.p.n,v:true}];
  var sameSpec=pool.filter(function(x){return x.spec===node.spec&&x!==node});
  var sameDept=pool.filter(function(x){return x.dept===node.dept&&x.spec!==node.spec});
  var rest=pool.filter(function(x){return x.dept!==node.dept});
  var picks=sameSpec.length>=3?sameSpec:(sameSpec.concat(sameDept).length>=3?sameSpec.concat(sameDept):sameSpec.concat(sameDept,rest));
  shuffleArr(picks).slice(0,3).forEach(function(x){opts.push({t:x.p.n,v:false})});
  opts=shuffleArr(opts);
  return{type:type,label:type==="def"?"Définition":"Signes cliniques",
    prompt:trunc(type==="def"?node.p.d:node.p.s,230),node:node,opts:opts};
}
function startQuiz(q){
  var pool=scopePool(q).slice();
  if(pool.length<6)return;
  shuffleArr(pool);
  var nb=Math.min(q.nb||10,pool.length);
  QZ={qs:pool.slice(0,nb).map(function(n){return makeQ(n,pool)}),i:0,score:0,answered:false,picked:-1,scope:q};
}
function viewQcm(q){
  if(QZ&&QZ.i<QZ.qs.length)return viewQuiz();
  if(QZ&&QZ.i>=QZ.qs.length)return viewQuizEnd();
  var cnt=scopePool(q).length;
  return ''+
  '<div class="crumbs"><a href="#/">Accueil</a><span class="sep">›</span><span>QCM</span></div>'+
  '<h1 class="pageh">❓ QCM d\u2019entraînement</h1>'+
  '<p class="lead">Questions générées automatiquement à partir des fiches : identifier la pathologie d\u2019après sa définition ou ses signes cliniques, ou la rattacher à sa spécialité. Correction immédiate après chaque réponse.</p>'+
  '<div class="card qcm-setup" style="max-width:760px">'+
    '<div class="row">'+
      '<div class="field"><label for="qz-dept">Département</label><select id="qz-dept">'+deptOptions(q.dept)+'</select></div>'+
      '<div class="field"><label for="qz-spec">Spécialité</label><select id="qz-spec">'+specOptions(q.dept,q.spec)+'</select></div>'+
      '<div class="field" style="min-width:120px;flex:0 1 130px"><label for="qz-nb">Questions</label><select id="qz-nb">'+
        [5,10,15,20].map(function(v){return '<option value="'+v+'"'+(v===10?" selected":"")+'>'+v+'</option>'}).join("")+'</select></div>'+
    '</div>'+
    '<div class="row"><span class="muted" style="font-size:.85rem">'+cnt+' pathologies dans ce périmètre</span>'+
    '<span class="spacer"></span><button class="btn primary" data-act="qz-start">Commencer →</button></div>'+
  '</div>';
}
function viewQuiz(){
  var q=QZ.qs[QZ.i];
  var letters=["A","B","C","D","E"];
  var opts=q.opts.map(function(o,i){
    var cls="opt";
    if(QZ.answered){if(o.v)cls+=" good";else if(i===QZ.picked)cls+=" bad"}
    return '<button class="'+cls+'" data-act="qz-pick" data-i="'+i+'" '+(QZ.answered?"disabled":"")+'>'+
      '<b>'+letters[i]+'.</b> '+esc(o.t)+'</button>';
  }).join("");
  var fb="";
  if(QZ.answered){
    var good=QZ.qs[QZ.i].opts[QZ.picked].v;
    fb='<div class="qz-feedback '+(good?"good":"bad")+'">'+(good?"✓ Bonne réponse !":"✗ Réponse incorrecte — la bonne réponse est surlignée en vert.")+
    '<div style="margin-top:6px;font-weight:500">'+esc(trunc(q.node.p.k,200))+'</div></div>';
  }
  return ''+
  '<div class="crumbs"><a href="#/">Accueil</a><span class="sep">›</span><a href="#/qcm">QCM</a></div>'+
  '<div class="qz-card card">'+
    '<div class="qz-meta"><span>Question '+(QZ.i+1)+' / '+QZ.qs.length+'</span><span>Score : '+QZ.score+'</span>'+
    '<span class="spacer"></span><button class="btn sm ghost" data-act="qz-new">Quitter</button></div>'+
    '<div class="deckbar" style="margin-bottom:14px"><span style="width:'+Math.round(QZ.i/QZ.qs.length*100)+'%"></span></div>'+
    '<div class="qz-q"><span class="type">'+q.label+' —</span>'+
    (q.type==="spec"?'Quelle spécialité correspond à « <b>'+esc(q.prompt)+'</b> » ?':
     q.type==="def"?'Quelle pathologie correspond à cette définition ?<br><span style="font-weight:500">« '+esc(q.prompt)+' »</span>':
     'Quelle pathologie évoque-t-on devant ces éléments cliniques ?<br><span style="font-weight:500">« '+esc(q.prompt)+' »</span>')+
    '</div>'+
    opts+fb+
    (QZ.answered?'<button class="btn primary" data-act="qz-next">'+(QZ.i+1<QZ.qs.length?"Question suivante →":"Voir les résultats →")+'</button>':'')+
  '</div>';
}
function viewQuizEnd(){
  var wrong=QZ.qs.filter(function(q){return q.pickedWrong});
  return ''+
  '<div class="crumbs"><a href="#/">Accueil</a><span class="sep">›</span><a href="#/qcm">QCM</a></div>'+
  '<div class="qz-card card" style="max-width:680px;margin:0 auto">'+
  '<div class="qz-end">'+
    '<div class="score">'+QZ.score+' / '+QZ.qs.length+'</div>'+
    '<p class="muted">'+(QZ.score===QZ.qs.length?"Sans faute, bravo ! 🏆":QZ.score>=QZ.qs.length*0.7?"Bon score, continuez ! 👍":"Relisez les fiches des pathologies manquées ci-dessous.")+'</p>'+
    (wrong.length?'<ul class="qz-wrong">'+wrong.map(function(q){
      return '<li>✗ '+esc(q.node.p.n)+' <a href="#/p/'+q.node.id+'">→ voir la fiche</a></li>';
    }).join("")+'</ul>':'')+
    '<div class="flex" style="justify-content:center;margin-top:18px">'+
      '<button class="btn primary" data-act="qz-again">Rejouer</button>'+
      '<button class="btn ghost" data-act="qz-new">Changer le périmètre</button>'+
    '</div>'+
  '</div></div>';
}

/* ================= Sources ================= */
function viewSources(){
  var srcs=[
    ["📕","MSD Manuels — Édition professionnelle","La référence principale utilisée pour enrichir chaque fiche : définitions, signes cliniques, démarche diagnostique et principes thérapeutiques, en français.","https://www.msdmanuals.com/fr/professional"],
    ["📗","MSD Manuels — Édition grand public","La version grand public du même manuel, utile pour des formulations simples et des explications destinées aux patients.","https://www.msdmanuals.com/fr/accueil"],
    ["🌐","Organisation Mondiale de la Santé (OMS)","Recommandations internationales : paludisme, VIH, tuberculose, urgences et santé publique.","https://www.who.int/fr"],
    ["🏥","Haute Autorité de Santé (HAS)","Recommandations et guides français : bon usage des médicaments, parcours de soins, recommandations de bonne pratique.","https://www.has-sante.fr"],
    ["🇫🇷","Santé publique France","Données épidémiologiques et recommandations françaises (vaccinations, maladies infectieuses, maladies chroniques).","https://www.santepubliquefrance.fr"],
    ["🔬","Inserm","Dossiers santé et actualités de la recherche biomédicale en français.","https://www.inserm.fr"],
    ["🧬","Orphanet","Le portail de référence des maladies rares : fiches détaillées et encyclopédie.","https://www.orpha.net"]
  ];
  return ''+
  '<div class="crumbs"><a href="#/">Accueil</a><span class="sep">›</span><span>Sources</span></div>'+
  '<h1 class="pageh">📚 Sources & méthodologie</h1>'+
  '<p class="lead">Ce site de révision suit fidèlement l\u2019organisation du document source « Médecine pratique » : 5 départements, leurs spécialités et l\u2019ensemble des pathologies listées. Chaque fiche a été rédigée et enrichie en s\u2019appuyant sur les références médicales officielles ci-dessous, dont les MSD Manuels (édition professionnelle en français).</p>'+
  '<div class="note-box blue">💾 Site 100 % statique et hors ligne : il fonctionne sans connexion internet. Seuls les liens « Consulter sur MSD Manuels » ouvrent une page web externe et nécessitent une connexion.</div>'+
  '<div class="grid" style="grid-template-columns:repeat(auto-fill,minmax(300px,1fr))">'+
    srcs.map(function(s){return '<div class="card src-card"><span class="ic">'+s[0]+'</span><div><h3>'+s[1]+'</h3><p>'+s[2]+'</p><a href="'+s[3]+'" target="_blank" rel="noopener">'+s[3].replace("https://","")+' ↗</a></div></div>'}).join("")+
  '</div>'+
  '<div class="section"><h2>Avertissement</h2><div class="note-box">⚕️ Outil pédagogique de révision destiné aux étudiants et professionnels de santé. Les fiches sont des synthèses : elles ne remplacent ni les références officielles complètes (MSD Manuels, OMS, HAS), ni les protocoles locaux, ni l\u2019avis d\u2019un médecin. En situation réelle, toujours se référer aux recommandations en vigueur et aux urgences médicales.</div></div>';
}

/* ================= Routeur ================= */
var OPENED=new Set(),CLOSED=new Set();
function parseHash(){
  var h=(location.hash||"#/").slice(2);
  var parts=h.split("?");
  var seg=parts[0].split("/").filter(Boolean);
  var q={};
  if(parts[1])new URLSearchParams(parts[1]).forEach(function(v,k){q[k]=v});
  return{seg:seg,q:q};
}
function route(){
  closeSearch();
  var r=parseHash(),app=$("#app"),html="";
  if(r.seg.length===0)html=viewHome();
  else if(r.seg[0]==="dept"&&IDXDEPT[r.seg[1]])html=viewDept(IDXDEPT[r.seg[1]]);
  else if(r.seg[0]==="p"&&IDX[r.seg[1]])html=viewPath(IDX[r.seg[1]]);
  else if(r.seg[0]==="revision")html=viewRevision(r.q);
  else if(r.seg[0]==="qcm")html=viewQcm(r.q);
  else if(r.seg[0]==="sources")html=viewSources();
  else html='<div class="card" style="padding:40px;text-align:center"><h1 class="pageh">Page introuvable</h1><p class="muted">Le lien demandé n\u2019existe pas.</p><a class="btn primary" href="#/" style="margin-top:12px">Retour à l\u2019accueil</a></div>';
  app.innerHTML=html;
  var cur=r.seg.length?r.seg[0]:"home";
  document.querySelectorAll("[data-route]").forEach(function(a){
    var on=a.dataset.route===cur||(a.dataset.route==="home"&&(cur==="dept"||cur==="p"));
    a.classList.toggle("active",!!on);
  });
  window.scrollTo(0,0);
  afterRender(r);
}
function afterRender(r){
  function bindScope(page,route){
    var dS=$("#"+page+"-dept"),sS=$("#"+page+"-spec");
    if(!dS||!sS)return;
    dS.value=r.q.dept||"";
    sS.value=r.q.spec||"";
    dS.addEventListener("change",function(){location.hash="#/"+route+(this.value?"?dept="+this.value:"")});
    sS.addEventListener("change",function(){
      var p=new URLSearchParams(),sp=this.value?specById(this.value):null;
      if(sp){var dd=null;DEPTS.forEach(function(d){if(d.specs.indexOf(sp)>=0)dd=d});
        if(dd)p.set("dept",dd.id);p.set("spec",sp.id);}
      else if(dS.value)p.set("dept",dS.value);
      var qs=p.toString();
      location.hash="#/"+route+(qs?"?"+qs:"");
    });
  }
  if(r.seg[0]==="revision")bindScope("rv","revision");
  if(r.seg[0]==="qcm")bindScope("qz","qcm");
}

/* ================= Actions globales ================= */
document.addEventListener("click",function(e){
  var t=e.target.closest("[data-act]");
  if(!t)return;
  var act=t.dataset.act;
  if(act==="acc"){
    var acc=t.closest(".acc");acc.classList.toggle("open");
    var sid=acc.dataset.spec;
    if(acc.classList.contains("open")){OPENED.add(sid);CLOSED.delete(sid)}
    else{CLOSED.add(sid);OPENED.delete(sid)}
    return;
  }
  if(act==="st"){
    var r=parseHash(),node=IDX[r.seg[1]];
    if(node){setSt(node.id,parseInt(t.dataset.v,10)||0);route()}
    return;
  }
  if(act==="reset-prog"){
    if(confirm("Effacer toute votre progression (fiches maîtrisées / à revoir) ?")){PROG={};saveProg();route()}
    return;
  }
  if(act==="fc-start"){
    var dS=$("#rv-dept"),sS=$("#rv-spec");
    var ok=startDeck({dept:dS?dS.value:"",spec:sS?sS.value:"",shuffle:$("#rv-shuffle").checked,todo:$("#rv-todo").checked});
    if(!ok){alert("Aucune carte dans ce périmètre avec ces filtres.");return}
    route();return;
  }
  if(act==="fc-flip"){flipCard();return}
  if(act==="fc-mark"){fcMark(parseInt(t.dataset.v,10));return}
  if(act==="fc-new"){FC=null;location.hash="#/revision";route();return}
  if(act==="fc-again"){var sc=FC.scope;startDeck(sc);route();return}
  if(act==="qz-start"){
    var dQ=$("#qz-dept"),sQ=$("#qz-spec");
    QZ=null;startQuiz({dept:dQ?dQ.value:"",spec:sQ?sQ.value:"",nb:parseInt($("#qz-nb").value,10)||10});
    if(!QZ){alert("Périmètre trop restreint pour générer un QCM (6 pathologies minimum).");return}
    route();return;
  }
  if(act==="qz-pick"){
    if(!QZ||QZ.answered)return;
    var i=parseInt(t.dataset.i,10);
    QZ.picked=i;QZ.answered=true;
    var q=QZ.qs[QZ.i];q.pickedWrong=!q.opts[i].v;
    if(q.opts[i].v)QZ.score++;
    route();return;
  }
  if(act==="qz-next"){QZ.i++;QZ.answered=false;QZ.picked=-1;route();return}
  if(act==="qz-again"){var qc=QZ.scope;QZ=null;startQuiz(qc);route();return}
  if(act==="qz-new"){QZ=null;location.hash="#/qcm";route();return}
});

/* ================= Boot ================= */
window.addEventListener("hashchange",route);
route();

</script>
</body>
</html>
