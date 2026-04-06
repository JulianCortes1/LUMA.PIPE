<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no">
<meta name="theme-color" content="#F4EEE4">
<meta name="apple-mobile-web-app-capable" content="yes">
<title>LUMA English</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,400;9..144,600;9..144,700&family=Nunito:wght@400;500;600;700;800&display=swap" rel="stylesheet">
<style>
:root{
  --bg:#F4EEE4;--surface:#FDFAF5;--alt:#EDE7D9;
  --purple:#9B72CF;--pl:#D4BBEF;--pp:#F0E8FA;
  --green:#6DB88E;--gl:#B2E0C4;--gp:#E8F7EF;
  --amber:#D4A054;--ap:#FDF1DE;
  --red:#E07070;--rp:#FFEAEA;
  --text:#2C1F14;--mid:#6B5744;--light:#9B8B7A;--border:#DDD4C4;
  --sh:rgba(44,31,20,.09);--nav:68px;--head:60px;
}
*{margin:0;padding:0;box-sizing:border-box;-webkit-tap-highlight-color:transparent}
html,body{height:100%;font-family:'Nunito',sans-serif;background:var(--bg);color:var(--text);overflow:hidden}
#app{height:100vh;height:100dvh;display:flex;flex-direction:column;max-width:430px;margin:0 auto;overflow:hidden}
.app-header{height:var(--head);background:var(--surface);border-bottom:1px solid var(--border);display:flex;align-items:center;justify-content:space-between;padding:0 18px;flex-shrink:0;box-shadow:0 2px 10px var(--sh)}
.logo{font-family:'Fraunces',serif;font-size:22px;font-weight:700;color:var(--purple)}
.logo span{color:var(--green)}
.streak-badge{display:flex;align-items:center;gap:5px;background:var(--pp);border-radius:20px;padding:5px 12px;font-size:13px;font-weight:800;color:var(--purple)}
.content{flex:1;overflow-y:auto;overflow-x:hidden;padding-bottom:calc(var(--nav)+10px);-webkit-overflow-scrolling:touch}
.tab{display:none;padding:18px 15px;animation:fadeUp .3s ease}
.tab.active{display:block}
@keyframes fadeUp{from{opacity:0;transform:translateY(10px)}to{opacity:1;transform:translateY(0)}}
.nav{height:var(--nav);background:var(--surface);border-top:1px solid var(--border);display:flex;padding:0 4px;flex-shrink:0;box-shadow:0 -3px 14px var(--sh)}
.nav-btn{flex:1;display:flex;flex-direction:column;align-items:center;justify-content:center;gap:3px;border:none;background:none;cursor:pointer;color:var(--light);padding:8px 2px;border-radius:10px;transition:color .2s}
.nav-btn.active{color:var(--purple)}
.nav-icon{font-size:21px;line-height:1;transition:transform .2s}
.nav-btn.active .nav-icon{transform:translateY(-2px)}
.nav-dot{width:4px;height:4px;border-radius:50%;background:var(--purple);opacity:0;transition:opacity .2s;margin-top:-2px}
.nav-btn.active .nav-dot{opacity:1}
.nav-lbl{font-size:9.5px;font-weight:800;letter-spacing:.5px;text-transform:uppercase}
.card{background:var(--surface);border-radius:18px;padding:16px;border:1px solid var(--border);box-shadow:0 2px 8px var(--sh);margin-bottom:13px}
.card-p{background:var(--pp);border-color:var(--pl)}
.card-g{background:var(--gp);border-color:var(--gl)}
.card-a{background:var(--ap);border-color:#E8C87A}
.page-title{font-family:'Fraunces',serif;font-size:24px;font-weight:700;line-height:1.2;margin-bottom:3px}
.section-title{font-family:'Fraunces',serif;font-size:16px;font-weight:700;margin-bottom:12px}
.body-text{font-size:14px;line-height:1.6;color:var(--mid)}
.label{font-size:10px;font-weight:800;letter-spacing:1px;text-transform:uppercase;color:var(--light)}
.badge{display:inline-block;padding:3px 9px;border-radius:20px;font-size:10.5px;font-weight:800;text-transform:uppercase;letter-spacing:.5px}
.bp{background:var(--pp);color:var(--purple)}.bg{background:var(--gp);color:#3A9A68}.ba{background:var(--ap);color:#B07830}.bk{background:var(--alt);color:var(--light)}
.prog{height:8px;background:var(--alt);border-radius:10px;overflow:hidden;margin:7px 0}
.prog-fill{height:100%;border-radius:10px;background:linear-gradient(90deg,var(--purple),var(--green));transition:width 1s cubic-bezier(.4,0,.2,1)}
.stats{display:grid;grid-template-columns:1fr 1fr 1fr;gap:9px;margin-bottom:14px}
.stat{background:var(--surface);border:1px solid var(--border);border-radius:13px;padding:13px 8px;text-align:center}
.stat-val{font-family:'Fraunces',serif;font-size:21px;font-weight:700;color:var(--purple)}
.stat-lbl{font-size:9.5px;font-weight:800;color:var(--light);text-transform:uppercase;letter-spacing:.5px;margin-top:2px}
.daily{background:linear-gradient(135deg,var(--purple),#7352B8);border-radius:20px;padding:20px;color:white;position:relative;overflow:hidden;margin-bottom:14px;cursor:pointer}
.daily::before{content:'';position:absolute;top:-15px;right:-15px;width:100px;height:100px;border-radius:50%;background:rgba(255,255,255,.08)}
.daily-tag{font-size:10px;font-weight:800;letter-spacing:1.5px;text-transform:uppercase;opacity:.7;margin-bottom:7px}
.daily-title{font-family:'Fraunces',serif;font-size:19px;font-weight:700;margin-bottom:7px;line-height:1.3}
.daily-meta{font-size:12px;opacity:.75;margin-bottom:14px}
.btn-white{display:inline-flex;align-items:center;background:white;color:var(--purple);border:none;border-radius:25px;padding:8px 16px;font-family:'Nunito',sans-serif;font-size:13px;font-weight:800;cursor:pointer}
.btn{display:inline-flex;align-items:center;justify-content:center;gap:6px;padding:10px 18px;border-radius:25px;font-family:'Nunito',sans-serif;font-size:14px;font-weight:700;cursor:pointer;border:none;transition:all .2s}
.btn-p{background:var(--purple);color:white;box-shadow:0 4px 12px rgba(155,114,207,.35)}
.btn-g{background:var(--green);color:white}
.btn-full{width:100%}
.btn-out{background:transparent;color:var(--purple);border:2px solid var(--pl)}
.btn-sm{padding:7px 14px;font-size:13px}
.btn:disabled{opacity:.5;pointer-events:none}
.quote{background:var(--alt);border-radius:13px;padding:14px;text-align:center;margin-bottom:13px}
.quote-text{font-family:'Fraunces',serif;font-style:italic;font-size:14px;color:var(--mid);line-height:1.5}
.quote-author{font-size:11px;color:var(--light);margin-top:5px;font-weight:700}
.tip-card{background:var(--surface);border:1px solid var(--border);border-radius:15px;padding:15px;margin-bottom:11px;display:flex;gap:12px;align-items:flex-start}
.tip-ico{font-size:24px;flex-shrink:0;margin-top:2px}
.tip-title{font-size:14px;font-weight:800;color:var(--text);margin-bottom:4px}
.tip-body{font-size:13px;color:var(--mid);line-height:1.5}
.block{background:var(--surface);border:1px solid var(--border);border-radius:16px;overflow:hidden;margin-bottom:13px;box-shadow:0 2px 8px var(--sh)}
.block-hdr{display:flex;align-items:center;justify-content:space-between;padding:15px;cursor:pointer;user-select:none}
.b1 .block-hdr{background:var(--pp)}.b2 .block-hdr{background:var(--gp)}.b3 .block-hdr{background:var(--ap)}
.block-title{font-family:'Fraunces',serif;font-size:15px;font-weight:700;color:var(--text)}
.block-sub{font-size:11px;color:var(--mid);margin-top:2px}
.block-right{display:flex;align-items:center;gap:8px}
.chevron{font-size:16px;color:var(--light);transition:transform .3s}
.block.open .chevron{transform:rotate(180deg)}
.lessons-list{display:none;padding:8px}
.block.open .lessons-list{display:block}
.lesson-item{display:flex;align-items:center;gap:11px;padding:11px;border-radius:11px;cursor:pointer;transition:background .2s;margin-bottom:3px}
.lesson-item:hover{background:var(--bg)}
.lesson-ico{width:36px;height:36px;border-radius:9px;display:flex;align-items:center;justify-content:center;font-size:17px;flex-shrink:0}
.ico-v{background:var(--pp)}.ico-l{background:var(--gp)}.ico-g{background:var(--ap)}.ico-e{background:#E8EEFF}.ico-m{background:#FFF0F5}
.lesson-body{flex:1;min-width:0}
.lesson-title{font-size:13.5px;font-weight:700;color:var(--text);white-space:nowrap;overflow:hidden;text-overflow:ellipsis}
.lesson-meta{font-size:11px;color:var(--light);margin-top:2px;display:flex;align-items:center;gap:5px}
.l-status{width:21px;height:21px;border-radius:50%;border:2px solid var(--border);display:flex;align-items:center;justify-content:center;font-size:11px;flex-shrink:0}
.l-status.done{background:var(--green);border-color:var(--green);color:white}
.exam-row{background:var(--ap);border:1px solid #E8C87A;border-radius:11px;padding:13px;margin:6px 0;display:flex;align-items:center;gap:11px;cursor:pointer}
.exam-row.done{background:var(--gp);border-color:var(--gl)}
.exam-title{font-family:'Fraunces',serif;font-size:14px;font-weight:700;color:var(--text)}
.exam-sub{font-size:11px;color:var(--mid)}
.overlay{position:fixed;inset:0;background:rgba(44,31,20,.45);z-index:100;display:none;align-items:flex-end;backdrop-filter:blur(3px)}
.overlay.on{display:flex}
.modal{background:var(--bg);border-radius:24px 24px 0 0;width:100%;max-height:93vh;overflow-y:auto;padding:0 0 28px;animation:slideUp .35s cubic-bezier(.34,1.56,.64,1)}
@keyframes slideUp{from{transform:translateY(100%)}to{transform:translateY(0)}}
.modal-handle{width:38px;height:4px;border-radius:2px;background:var(--border);margin:12px auto 0}
.modal-inner{padding:18px 18px 0}
.act-hdr{background:var(--alt);border-radius:11px;padding:11px 14px;margin-bottom:12px}
.act-hdr-title{font-weight:800;font-size:14px;color:var(--text);margin-bottom:3px}
.act-hdr-sub{font-size:12px;color:var(--mid)}
.q-card{background:var(--surface);border:1px solid var(--border);border-radius:13px;padding:14px;margin-bottom:11px}
.q-text{font-size:14px;font-weight:600;color:var(--text);margin-bottom:11px;line-height:1.5}
.opt{display:flex;align-items:center;gap:9px;width:100%;padding:9px 13px;border:1.5px solid var(--border);border-radius:9px;background:var(--bg);cursor:pointer;font-family:'Nunito',sans-serif;font-size:13.5px;color:var(--text);text-align:left;margin-bottom:7px;transition:all .2s}
.opt:hover:not(:disabled){border-color:var(--pl);background:var(--pp)}
.opt.sel{border-color:var(--purple);background:var(--pp);color:var(--purple)}
.opt.correct{border-color:var(--green);background:var(--gp);color:#2D7D52}
.opt.wrong{border-color:var(--red);background:var(--rp);color:#B04040}
.opt-ltr{width:22px;height:22px;border-radius:50%;background:var(--border);font-size:11px;font-weight:800;display:flex;align-items:center;justify-content:center;flex-shrink:0;color:var(--mid)}
.sel .opt-ltr{background:var(--purple);color:white}
.correct .opt-ltr{background:var(--green);color:white}
.wrong .opt-ltr{background:var(--red);color:white}
.passage{background:var(--alt);border-left:3px solid var(--purple);border-radius:0 10px 10px 0;padding:13px;margin-bottom:13px;font-size:13.5px;line-height:1.7;color:var(--mid);font-style:italic}
.tf-row{display:flex;align-items:flex-start;gap:9px;padding:10px;border:1.5px solid var(--border);border-radius:10px;margin-bottom:8px;background:var(--bg)}
.tf-row.tf-correct{border-color:var(--green);background:var(--gp)}
.tf-row.tf-wrong{border-color:var(--red);background:var(--rp)}
.tf-s{font-size:13.5px;color:var(--text);flex:1;line-height:1.5}
.tf-btns{display:flex;gap:5px;flex-shrink:0;margin-top:1px}
.tf-btn{padding:4px 10px;border-radius:7px;font-size:12px;font-weight:800;cursor:pointer;border:1.5px solid var(--border);background:var(--surface);color:var(--text);font-family:'Nunito',sans-serif}
.tf-btn.active-t{border-color:var(--green);background:var(--gp);color:#2D7D52}
.tf-btn.active-f{border-color:var(--red);background:var(--rp);color:#B04040}
.fill-row{margin-bottom:11px}
.fill-sentence{font-size:14px;color:var(--text);line-height:1.6;margin-bottom:6px}
.fill-blank{display:inline-block;min-width:80px;border-bottom:2px solid var(--purple);color:var(--purple);font-weight:700;text-align:center;padding:2px 8px}
.fill-inp{width:100%;padding:8px 12px;border:1.5px solid var(--border);border-radius:8px;font-family:'Nunito',sans-serif;font-size:14px;background:var(--bg);color:var(--text);outline:none}
.fill-inp:focus{border-color:var(--purple)}
.fill-inp.fill-ok{border-color:var(--green);background:var(--gp);color:#2D7D52}
.fill-inp.fill-err{border-color:var(--red);background:var(--rp);color:#B04040}
.crit-row{display:flex;align-items:center;gap:10px;padding:10px 12px;border:1.5px solid var(--border);border-radius:10px;background:var(--bg);cursor:pointer;margin-bottom:8px}
.crit-row.checked{border-color:var(--green);background:var(--gp)}
.crit-check{width:20px;height:20px;border-radius:5px;border:2px solid var(--border);display:flex;align-items:center;justify-content:center;font-size:12px;flex-shrink:0}
.crit-row.checked .crit-check{background:var(--green);border-color:var(--green);color:white}
.crit-text{font-size:13.5px;color:var(--text);line-height:1.4}
.ext-link{display:flex;align-items:center;gap:10px;background:var(--surface);border:1.5px solid var(--border);border-radius:12px;padding:12px 14px;margin-bottom:10px;text-decoration:none;color:var(--text)}
.ext-link-name{font-size:13.5px;font-weight:700;color:var(--purple)}
.ext-link-sub{font-size:11px;color:var(--light)}
.refl-q{font-size:13.5px;font-weight:600;color:var(--text);margin-bottom:6px}
.refl-inp{width:100%;padding:9px 12px;border:1.5px solid var(--border);border-radius:9px;font-family:'Nunito',sans-serif;font-size:13.5px;background:var(--bg);color:var(--text);outline:none;resize:vertical;min-height:55px;margin-bottom:12px}
.refl-inp:focus{border-color:var(--purple)}
.score-box{text-align:center;padding:22px 16px}
.score-circle{width:78px;height:78px;border-radius:50%;background:var(--pp);border:3px solid var(--pl);display:flex;align-items:center;justify-content:center;margin:0 auto 11px;font-family:'Fraunces',serif;font-size:24px;font-weight:700;color:var(--purple)}
.score-circle.great{background:var(--gp);border-color:var(--gl);color:#2D8050}
.score-msg{font-family:'Fraunces',serif;font-size:17px;font-weight:700;color:var(--text);margin-bottom:5px}
.score-sub{font-size:13px;color:var(--mid)}
.level-display{text-align:center;padding:22px 14px;background:linear-gradient(135deg,var(--pp),var(--gp));border-radius:18px;margin-bottom:14px}
.level-badge{display:inline-block;background:white;border:2px solid var(--pl);border-radius:40px;padding:7px 22px;font-family:'Fraunces',serif;font-size:26px;font-weight:700;color:var(--purple);margin-bottom:7px}
.track{display:flex;align-items:center;gap:8px;margin:6px 0 12px}
.track-lbl{font-size:10px;font-weight:800;color:var(--light);width:28px;text-align:center}
.track-bar{flex:1;height:9px;background:var(--alt);border-radius:10px;overflow:hidden}
.track-fill{height:100%;border-radius:10px}
.tf-p{background:linear-gradient(90deg,var(--pl),var(--purple))}
.tf-g{background:linear-gradient(90deg,var(--gl),var(--green))}
.tf-a{background:linear-gradient(90deg,#E8C87A,var(--amber))}
.result-row{display:flex;align-items:center;justify-content:space-between;padding:11px 0;border-bottom:1px solid var(--border)}
.result-row:last-child{border-bottom:none}
.result-name{font-size:14px;font-weight:700;color:var(--text)}
.result-date{font-size:11px;color:var(--light);margin-top:2px}
.result-score{font-family:'Fraunces',serif;font-size:19px;font-weight:700}
.s-hi{color:var(--green)}.s-mid{color:var(--amber)}.s-lo{color:var(--red)}
.cert{background:var(--surface);border:2px dashed var(--border);border-radius:20px;padding:22px;text-align:center;margin-bottom:14px}
.cert.open{border-style:solid;border-color:var(--gl);background:var(--gp)}
.cert-ico{font-size:44px;margin-bottom:11px;display:block;filter:grayscale(1)}
.cert.open .cert-ico{filter:none}
.cert-title{font-family:'Fraunces',serif;font-size:17px;font-weight:700;color:var(--text);margin-bottom:5px}
.cert-desc{font-size:13px;color:var(--mid);margin-bottom:12px;line-height:1.5}
.cert-date{font-size:12px;font-weight:800;color:var(--green)}
.cert-locked{font-size:12.5px;color:var(--light)}
.conf{position:fixed;pointer-events:none;z-index:200}
.cp{position:absolute;width:9px;height:9px;border-radius:2px;animation:fall linear forwards}
@keyframes fall{0%{transform:translateY(-10px) rotate(0);opacity:1}100%{transform:translateY(100vh) rotate(720deg);opacity:0}}
hr{height:1px;background:var(--border);border:none;margin:12px 0}
.flex{display:flex;align-items:center}.between{justify-content:space-between}.mt12{margin-top:12px}.mb12{margin-bottom:12px}.center{text-align:center}
::-webkit-scrollbar{width:0}
</style>
</head>
<body>
<div id="app">
  <header class="app-header">
    <div class="logo">LU<span>MA</span> <span style="font-size:13px;font-weight:600;color:var(--light);font-family:'Nunito',sans-serif">English</span></div>
    <div class="streak-badge" id="streakEl">🔥 0 días</div>
  </header>
  <div class="content">
    <div id="tab-inicio" class="tab active"></div>
    <div id="tab-curso" class="tab"></div>
    <div id="tab-tips" class="tab"></div>
    <div id="tab-progreso" class="tab"></div>
    <div id="tab-logros" class="tab"></div>
  </div>
  <nav class="nav">
    <button class="nav-btn active" onclick="switchTab('inicio')" id="nb-inicio"><div class="nav-icon">🏠</div><div class="nav-dot"></div><div class="nav-lbl">Inicio</div></button>
    <button class="nav-btn" onclick="switchTab('curso')" id="nb-curso"><div class="nav-icon">📚</div><div class="nav-dot"></div><div class="nav-lbl">Curso</div></button>
    <button class="nav-btn" onclick="switchTab('tips')" id="nb-tips"><div class="nav-icon">💡</div><div class="nav-dot"></div><div class="nav-lbl">Tips</div></button>
    <button class="nav-btn" onclick="switchTab('progreso')" id="nb-progreso"><div class="nav-icon">📊</div><div class="nav-dot"></div><div class="nav-lbl">Progreso</div></button>
    <button class="nav-btn" onclick="switchTab('logros')" id="nb-logros"><div class="nav-icon">🏅</div><div class="nav-dot"></div><div class="nav-lbl">Logros</div></button>
  </nav>
</div>
<div class="overlay" id="overlay" onclick="handleOverlayClick(event)">
  <div class="modal" id="modal"><div class="modal-handle"></div><div class="modal-inner" id="modalInner"></div></div>
</div>
<div class="conf" id="conf"></div>

<script>
// ─── COURSE DATA ─────────────────────────────────────────
var COURSE = [
  {id:1,title:"The Kitchen Speaks",months:"Meses 1-2",cls:"b1",
   lessons:[
    {id:1,title:"Kitchen Vocabulary Basics",type:"vocabulary",icon:"📖",icoCls:"ico-v",
     obj:"Identify and use 30+ kitchen tools and cooking terms in professional contexts.",
     topics:["Kitchen equipment","Food categories","Culinary verbs"],
     acts:[
      {type:"quiz",title:"Kitchen Tools Quiz",qs:[
        {q:"Which tool is used to strain pasta?",opts:["Spatula","Colander","Whisk","Ladle"],c:1},
        {q:"What is a 'cleaver' primarily used for?",opts:["Stirring sauces","Slicing bread","Chopping large cuts of meat","Peeling vegetables"],c:2},
        {q:"Which technique means 'cook slowly in liquid'?",opts:["Sear","Broil","Braise","Saute"],c:2},
        {q:"A 'mandoline' is used to...",opts:["Measure liquids","Slice very thin","Blend soups","Whip cream"],c:1},
        {q:"'Deglaze' means to...",opts:["Drain pasta","Add liquid to lift browned bits","Season the food","Remove the skin"],c:1}
      ]},
      {type:"match",title:"Culinary Terms Match",pairs:[
        {term:"Mise en place",def:"Everything in its place - prep before service"},
        {term:"Al dente",def:"Pasta cooked firm to the bite"},
        {term:"Julienne",def:"Cut into thin matchstick strips"},
        {term:"Baste",def:"Pour cooking juices over food while it cooks"},
        {term:"Blanch",def:"Briefly boil then immediately cool in ice water"}
      ]}
     ]},
    {id:2,title:"A Day at the Restaurant",type:"listening",icon:"🎧",icoCls:"ico-l",
     obj:"Understand and respond to common kitchen and restaurant dialogues between staff.",
     topics:["Restaurant communication","Service vocabulary","Listening for detail"],
     acts:[
      {type:"tf",title:"Kitchen Dialogue Comprehension",
       passage:"HEAD CHEF: Carlos, table 7 ordered the salmon. Plate it with lemon beurre blanc and asparagus. The VIP at table 3 has a nut allergy — double-check every dish. Maria, how long on the risotto? SOUS CHEF: About f
