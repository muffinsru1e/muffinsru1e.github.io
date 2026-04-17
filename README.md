<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ScienceACE — AQA GCSE Science Revision</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Serif+Display:ital@0;1&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,400&display=swap" rel="stylesheet">
<style>
:root {
  --bg: #0b0d12;
  --surface: #12151e;
  --surface2: #181c27;
  --surface3: #1e2333;
  --border: rgba(255,255,255,0.06);
  --border2: rgba(255,255,255,0.12);
  --text: #e8eaf2;
  --text2: #a8b0c4;
  --muted: #5a6278;
  --phys: #e5484d;
  --phys-dim: rgba(229,72,77,0.12);
  --bio: #22c55e;
  --bio-dim: rgba(34,197,94,0.12);
  --chem: #3b82f6;
  --chem-dim: rgba(59,130,246,0.12);
  --correct: #22c55e;
  --correct-dim: rgba(34,197,94,0.1);
  --wrong: #ef4444;
  --wrong-dim: rgba(239,68,68,0.1);
  --gold: #f59e0b;
  --r: 14px;
  --r-sm: 9px;
}
*{margin:0;padding:0;box-sizing:border-box}
html{scroll-behavior:smooth}
body{background:var(--bg);color:var(--text);font-family:'DM Sans',sans-serif;min-height:100vh;overflow-x:hidden;line-height:1.6}
body::after{content:'';position:fixed;inset:0;background:radial-gradient(ellipse 80% 50% at 50% -20%,rgba(229,72,77,0.04),transparent);pointer-events:none;z-index:0}

/* NAV */
nav{display:flex;align-items:center;justify-content:space-between;padding:18px 40px;border-bottom:1px solid var(--border);backdrop-filter:blur(24px);position:sticky;top:0;z-index:200;background:rgba(11,13,18,0.88)}
.logo{font-family:'Syne',sans-serif;font-weight:800;font-size:1.35rem;letter-spacing:-0.5px;cursor:pointer}
.logo span{color:var(--phys)}
.nav-right{display:flex;align-items:center;gap:12px}
.score-pill{display:flex;align-items:center;gap:10px;font-size:0.82rem;color:var(--text2);background:var(--surface);padding:7px 16px;border-radius:999px;border:1px solid var(--border2)}
.score-pill strong{color:var(--text);font-weight:600}
.streak-badge{background:linear-gradient(135deg,#f59e0b,#ef4444);color:#fff;font-weight:700;font-size:0.78rem;padding:4px 10px;border-radius:999px}

/* MAIN WRAPPER */
#app{position:relative;z-index:1}
.screen{display:none;max-width:1060px;margin:0 auto;padding:48px 40px}
.screen.active{display:block}
#screen-home{display:block;animation:fadeUp .5s ease}

@media(max-width:700px){
  nav{padding:14px 18px}
  .screen{padding:28px 18px}
}

/* HOME */
.hero-eyebrow{font-size:.72rem;font-weight:600;letter-spacing:2.5px;text-transform:uppercase;color:var(--phys);margin-bottom:18px;opacity:0;animation:fadeUp .5s ease forwards .05s}
.hero-title{font-family:'DM Serif Display',serif;font-size:clamp(2.6rem,6vw,4.8rem);line-height:1.05;letter-spacing:-1.5px;margin-bottom:20px;opacity:0;animation:fadeUp .55s ease forwards .12s}
.hero-title em{font-style:italic;color:var(--phys)}
.hero-sub{font-size:1.05rem;color:var(--text2);max-width:520px;margin-bottom:52px;opacity:0;animation:fadeUp .55s ease forwards .2s}
.subject-grid{display:grid;grid-template-columns:repeat(3,1fr);gap:18px;opacity:0;animation:fadeUp .55s ease forwards .3s}
@media(max-width:720px){.subject-grid{grid-template-columns:1fr}}

.subject-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);padding:30px;cursor:pointer;transition:all .22s ease;position:relative;overflow:hidden}
.subject-card::before{content:'';position:absolute;inset:0;opacity:0;transition:opacity .22s;background:var(--glow)}
.subject-card:hover::before{opacity:1}
.subject-card:hover{transform:translateY(-5px);border-color:var(--accent)}
.subject-card[data-s="physics"]{--accent:var(--phys);--glow:var(--phys-dim)}
.subject-card[data-s="biology"]{--accent:var(--bio);--glow:var(--bio-dim)}
.subject-card[data-s="chemistry"]{--accent:var(--chem);--glow:var(--chem-dim)}
.subject-card:hover{box-shadow:0 0 40px var(--glow),0 16px 40px rgba(0,0,0,.35)}
.s-icon{font-size:2.2rem;margin-bottom:14px;display:block;position:relative}
.s-name{font-family:'Syne',sans-serif;font-size:1.25rem;font-weight:700;color:var(--accent);margin-bottom:7px;position:relative}
.s-desc{font-size:.85rem;color:var(--muted);line-height:1.6;margin-bottom:18px;position:relative}
.s-meta{font-size:.75rem;font-weight:600;color:var(--accent);background:var(--glow);padding:4px 12px;border-radius:999px;border:1px solid var(--accent);display:inline-flex;align-items:center;gap:6px;position:relative;opacity:.9}

/* TOPIC SCREEN */
.back-btn{display:inline-flex;align-items:center;gap:7px;font-size:.85rem;color:var(--muted);cursor:pointer;margin-bottom:28px;background:none;border:none;font-family:inherit;transition:color .18s}
.back-btn:hover{color:var(--text)}
.screen-header{margin-bottom:28px}
.screen-eyebrow{display:flex;align-items:center;gap:10px;margin-bottom:10px}
.subj-badge{font-family:'Syne',sans-serif;font-size:.7rem;font-weight:700;letter-spacing:1.5px;text-transform:uppercase;padding:5px 13px;border-radius:999px;border:1px solid}
.screen-title{font-family:'DM Serif Display',serif;font-size:2rem;line-height:1.15}

.mode-tabs{display:flex;gap:6px;margin-bottom:28px;background:var(--surface);padding:5px;border-radius:var(--r-sm);border:1px solid var(--border);width:fit-content}
.mode-tab{padding:8px 18px;border-radius:7px;font-size:.85rem;font-weight:500;cursor:pointer;transition:all .18s;background:none;border:none;color:var(--muted);font-family:inherit}
.mode-tab.active{background:var(--surface2);color:var(--text);box-shadow:0 2px 10px rgba(0,0,0,.4)}

.topic-section{margin-bottom:28px}
.ts-label{font-size:.68rem;font-weight:700;letter-spacing:2px;text-transform:uppercase;color:var(--muted);margin-bottom:10px;padding-bottom:6px;border-bottom:1px solid var(--border)}
.topic-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(190px,1fr));gap:9px}
.topic-btn{background:var(--surface);border:1px solid var(--border);border-radius:var(--r-sm);padding:14px 16px;cursor:pointer;text-align:left;transition:all .18s;font-family:inherit;color:var(--text);position:relative;overflow:hidden}
.topic-btn:hover{border-color:var(--c-accent,var(--phys));background:var(--surface2);transform:translateY(-2px)}
.topic-btn-name{font-size:.88rem;font-weight:500;margin-bottom:3px;line-height:1.35}
.topic-btn-meta{font-size:.72rem;color:var(--muted)}
.topic-btn .q-count{position:absolute;top:10px;right:12px;font-size:.68rem;color:var(--c-accent,var(--phys));opacity:.7;font-weight:600}

/* QUIZ */
.quiz-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:18px;font-size:.84rem;color:var(--text2)}
.q-info{display:flex;align-items:center;gap:12px}
.progress-bar{height:3px;background:var(--surface2);border-radius:999px;margin-bottom:32px;overflow:hidden}
.progress-fill{height:100%;background:linear-gradient(90deg,var(--c-accent,var(--phys)),color-mix(in srgb,var(--c-accent,var(--phys)) 60%,white));border-radius:999px;transition:width .45s cubic-bezier(.4,0,.2,1)}

.question-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);padding:32px;margin-bottom:16px;animation:fadeUp .35s ease}
.q-tag{font-size:.68rem;font-weight:700;letter-spacing:1.8px;text-transform:uppercase;color:var(--c-accent,var(--phys));margin-bottom:12px;display:flex;align-items:center;gap:8px}
.q-tag::after{content:'';flex:1;height:1px;background:var(--border)}
.q-text{font-size:1.12rem;line-height:1.7;color:var(--text)}
.q-hint{font-size:.82rem;color:var(--text2);margin-top:8px;font-style:italic;background:var(--surface2);padding:8px 14px;border-radius:var(--r-sm);border-left:2px solid var(--c-accent,var(--phys))}

.options-grid{display:grid;gap:9px;margin-bottom:12px}
.opt-btn{background:var(--surface);border:1.5px solid var(--border);border-radius:var(--r-sm);padding:14px 18px;cursor:pointer;text-align:left;font-family:inherit;font-size:.95rem;color:var(--text);transition:all .18s;display:flex;align-items:center;gap:14px;line-height:1.5}
.opt-btn:hover:not(:disabled){border-color:var(--c-accent,var(--phys));background:var(--surface2);transform:translateX(4px)}
.opt-letter{width:28px;height:28px;border-radius:50%;background:var(--surface2);border:1px solid var(--border2);display:flex;align-items:center;justify-content:center;font-size:.72rem;font-weight:700;flex-shrink:0;transition:all .2s;font-family:'Syne',sans-serif}
.opt-btn.correct{border-color:var(--correct);background:var(--correct-dim)}
.opt-btn.correct .opt-letter{background:var(--correct);border-color:var(--correct);color:#000}
.opt-btn.wrong{border-color:var(--wrong);background:var(--wrong-dim)}
.opt-btn.wrong .opt-letter{background:var(--wrong);border-color:var(--wrong);color:#fff}
.opt-btn:disabled{cursor:default;opacity:.8}

.explanation{background:var(--surface2);border-left:3px solid var(--c-accent,var(--phys));border-radius:0 var(--r-sm) var(--r-sm) 0;padding:18px 22px;font-size:.9rem;line-height:1.75;color:var(--text2);margin-top:14px;display:none}
.explanation.show{display:block;animation:fadeUp .3s ease}
.explanation strong{color:var(--text)}
.explanation .e-title{font-family:'Syne',sans-serif;font-size:.7rem;font-weight:700;letter-spacing:1.5px;text-transform:uppercase;color:var(--c-accent,var(--phys));margin-bottom:8px;display:block}

.action-row{display:flex;gap:10px;margin-top:14px}
.next-btn{flex:1;padding:15px;background:var(--c-accent,var(--phys));color:#fff;border:none;border-radius:var(--r-sm);font-family:'Syne',sans-serif;font-size:.95rem;font-weight:700;cursor:pointer;letter-spacing:.4px;transition:all .18s;display:none}
.next-btn.show{display:block}
.next-btn:hover{opacity:.88;transform:translateY(-1px)}
.skip-btn{padding:15px 20px;background:none;border:1.5px solid var(--border2);border-radius:var(--r-sm);font-family:inherit;font-size:.88rem;color:var(--muted);cursor:pointer;transition:all .18s;display:none}
.skip-btn.show{display:block}
.skip-btn:hover{color:var(--text);border-color:var(--border2)}

/* LOADING */
.loading{text-align:center;padding:72px 20px}
.spinner{width:38px;height:38px;border:2.5px solid var(--surface2);border-top-color:var(--c-accent,var(--phys));border-radius:50%;animation:spin .75s linear infinite;margin:0 auto 18px}
.loading p{color:var(--muted);font-size:.9rem}

/* RESULT */
.result-card{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);padding:52px 40px;text-align:center;animation:fadeUp .4s ease}
.result-emoji{font-size:3.5rem;margin-bottom:14px}
.result-score{font-family:'DM Serif Display',serif;font-size:5.5rem;line-height:1;color:var(--c-accent,var(--phys));margin-bottom:4px}
.result-pct{font-size:.82rem;color:var(--muted);text-transform:uppercase;letter-spacing:2px;font-weight:600;margin-bottom:10px}
.result-msg{font-size:1rem;color:var(--text2);max-width:380px;margin:0 auto 32px;line-height:1.7}
.result-breakdown{display:flex;justify-content:center;gap:20px;margin-bottom:32px;flex-wrap:wrap}
.rb-item{background:var(--surface2);border:1px solid var(--border);border-radius:var(--r-sm);padding:14px 22px;text-align:center}
.rb-val{font-family:'Syne',sans-serif;font-size:1.5rem;font-weight:800;display:block}
.rb-label{font-size:.72rem;color:var(--muted);text-transform:uppercase;letter-spacing:1px}
.result-btns{display:flex;gap:10px;justify-content:center;flex-wrap:wrap}
.btn-p,.btn-s{padding:13px 26px;border-radius:var(--r-sm);font-family:'Syne',sans-serif;font-weight:700;font-size:.88rem;cursor:pointer;border:none;transition:all .18s;letter-spacing:.3px}
.btn-p{background:var(--c-accent,var(--phys));color:#fff}
.btn-p:hover{opacity:.88;transform:translateY(-2px)}
.btn-s{background:var(--surface2);color:var(--text);border:1.5px solid var(--border2)}
.btn-s:hover{border-color:var(--c-accent,var(--phys));transform:translateY(-2px)}

/* NOTES */
.notes-body{background:var(--surface);border:1px solid var(--border);border-radius:var(--r);overflow:hidden}
.notes-toc{background:var(--surface2);border-bottom:1px solid var(--border);padding:20px 30px}
.notes-toc-title{font-size:.7rem;font-weight:700;letter-spacing:2px;text-transform:uppercase;color:var(--muted);margin-bottom:12px}
.notes-toc-links{display:flex;flex-wrap:wrap;gap:8px}
.toc-link{font-size:.8rem;color:var(--text2);background:var(--surface);padding:5px 12px;border-radius:6px;border:1px solid var(--border);cursor:pointer;transition:all .18s;text-decoration:none;display:inline-block}
.toc-link:hover{color:var(--text);border-color:var(--c-accent,var(--phys))}
.notes-content{padding:36px}
.notes-content h2{font-family:'DM Serif Display',serif;font-size:1.7rem;color:var(--c-accent,var(--phys));margin-bottom:6px;line-height:1.2}
.notes-content .intro-text{font-size:.95rem;color:var(--text2);margin-bottom:28px;padding-bottom:20px;border-bottom:1px solid var(--border)}
.notes-section{margin-bottom:32px;padding-bottom:32px;border-bottom:1px solid var(--border)}
.notes-section:last-child{border-bottom:none;margin-bottom:0;padding-bottom:0}
.notes-section h3{font-family:'Syne',sans-serif;font-size:.95rem;font-weight:700;margin-bottom:14px;color:var(--text);display:flex;align-items:center;gap:10px}
.notes-section h3::before{content:'';width:3px;height:18px;background:var(--c-accent,var(--phys));border-radius:2px;flex-shrink:0}
.notes-section p,.notes-section li{font-size:.9rem;color:var(--text2);line-height:1.8}
.notes-section ul{list-style:none;display:flex;flex-direction:column;gap:6px}
.notes-section li{padding-left:18px;position:relative}
.notes-section li::before{content:'→';position:absolute;left:0;color:var(--c-accent,var(--phys));font-weight:700}
.formula-box{background:var(--surface2);border:1px solid var(--border2);border-radius:var(--r-sm);padding:14px 20px;margin:10px 0;font-family:'Courier New',monospace;font-size:.92rem;color:var(--c-accent,var(--phys));text-align:center;letter-spacing:.5px;font-weight:600}
.key-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(180px,1fr));gap:10px;margin:12px 0}
.key-card{background:var(--surface2);border:1px solid var(--border);border-radius:var(--r-sm);padding:13px 16px}
.kc-label{font-size:.68rem;font-weight:700;letter-spacing:1px;text-transform:uppercase;color:var(--muted);margin-bottom:5px}
.kc-val{font-size:.88rem;color:var(--text);line-height:1.4}
.exam-tip{background:rgba(245,158,11,.07);border:1px solid rgba(245,158,11,.25);border-radius:var(--r-sm);padding:14px 18px;margin:14px 0;font-size:.88rem;color:#e8c97a;line-height:1.7}
.exam-tip::before{content:'★ EXAM TIP: ';font-weight:700;font-family:'Syne',sans-serif;font-size:.72rem;letter-spacing:1.5px;text-transform:uppercase}
.required-practical{background:rgba(59,130,246,.06);border:1px solid rgba(59,130,246,.2);border-radius:var(--r-sm);padding:14px 18px;margin:14px 0;font-size:.88rem;color:var(--text2);line-height:1.7}
.required-practical::before{content:'🔬 REQUIRED PRACTICAL: ';font-weight:700;font-family:'Syne',sans-serif;font-size:.72rem;letter-spacing:1.5px;text-transform:uppercase;color:var(--phys)}
.notes-table{width:100%;border-collapse:collapse;font-size:.85rem;margin:12px 0}
.notes-table th{background:var(--surface2);color:var(--text);font-family:'Syne',sans-serif;font-size:.72rem;font-weight:700;letter-spacing:1px;text-transform:uppercase;padding:10px 14px;text-align:left;border:1px solid var(--border)}
.notes-table td{padding:9px 14px;border:1px solid var(--border);color:var(--text2);vertical-align:top}
.notes-table tr:nth-child(even) td{background:rgba(255,255,255,.02)}

/* ANIMATIONS */
@keyframes fadeUp{from{opacity:0;transform:translateY(14px)}to{opacity:1;transform:translateY(0)}}
@keyframes spin{to{transform:rotate(360deg)}}

/* TOAST */
.toast{position:fixed;bottom:28px;right:28px;background:var(--surface2);border:1px solid var(--border2);border-radius:var(--r-sm);padding:12px 18px;font-size:.85rem;z-index:999;animation:fadeUp .3s ease;max-width:280px;color:var(--text2)}
</style>
</head>
<body>
<nav>
  <div class="logo" onclick="goHome()">Science<span>ACE</span></div>
  <div class="nav-right">
    <div class="score-pill">⭐ <strong id="nav-score">0</strong> pts &nbsp;
      <span class="streak-badge" id="nav-streak" style="display:none">0🔥</span>
    </div>
  </div>
</nav>

<div id="app">

<!-- HOME -->
<div id="screen-home" class="screen active">
  <p class="hero-eyebrow">AQA GCSE Triple Science</p>
  <h1 class="hero-title">Ace your<br><em>science exams</em></h1>
  <p class="hero-sub">Hundreds of randomised practice questions, detailed revision notes and instant feedback — no login needed.</p>
  <div class="subject-grid">
    <div class="subject-card" data-s="physics" onclick="openSubject('physics')">
      <span class="s-icon">⚛️</span>
      <div class="s-name">Physics</div>
      <div class="s-desc">Forces, energy, waves, electricity, magnetism, particle model, radioactivity &amp; space.</div>
      <span class="s-meta">8 topics · 200+ questions</span>
    </div>
    <div class="subject-card" data-s="biology" onclick="openSubject('biology')">
      <span class="s-icon">🧬</span>
      <div class="s-name">Biology</div>
      <div class="s-desc">Cell biology, organisation, infection, bioenergetics, homeostasis, genetics &amp; ecology.</div>
      <span class="s-meta">8 topics · 200+ questions</span>
    </div>
    <div class="subject-card" data-s="chemistry" onclick="openSubject('chemistry')">
      <span class="s-icon">🧪</span>
      <div class="s-name">Chemistry</div>
      <div class="s-desc">Atomic structure, bonding, quantitative, reactions, rates, organic &amp; analysis.</div>
      <span class="s-meta">8 topics · 200+ questions</span>
    </div>
  </div>
</div>

<!-- TOPICS -->
<div id="screen-topics" class="screen">
  <button class="back-btn" onclick="goHome()">← All Subjects</button>
  <div class="screen-header">
    <div class="screen-eyebrow">
      <span class="subj-badge" id="topic-badge"></span>
      <span style="font-size:.82rem;color:var(--muted)">AQA GCSE</span>
    </div>
    <h2 class="screen-title" id="topic-title">Choose a Topic</h2>
  </div>
  <div class="mode-tabs">
    <button class="mode-tab active" id="tab-quiz" onclick="switchMode('quiz')">📝 Practice Quiz</button>
    <button class="mode-tab" id="tab-notes" onclick="switchMode('notes')">📖 Revision Notes</button>
  </div>
  <div id="topic-list"></div>
</div>

<!-- QUIZ -->
<div id="screen-quiz" class="screen">
  <button class="back-btn" onclick="backToTopics()">← Topics</button>
  <div class="quiz-header">
    <div class="q-info">
      <span id="q-counter">Q1 / 10</span>
      <span style="color:var(--muted);font-size:.8rem" id="q-topic-name"></span>
    </div>
    <span id="q-score-live" style="font-weight:600"></span>
  </div>
  <div class="progress-bar"><div class="progress-fill" id="progress-fill" style="width:0%"></div></div>
  <div id="quiz-content"></div>
</div>

<!-- NOTES -->
<div id="screen-notes" class="screen">
  <button class="back-btn" onclick="backToTopics()">← Topics</button>
  <div class="screen-header">
    <div class="screen-eyebrow">
      <span class="subj-badge" id="notes-badge"></span>
    </div>
    <h2 class="screen-title" id="notes-title"></h2>
  </div>
  <div class="notes-body">
    <div class="notes-toc" id="notes-toc"></div>
    <div class="notes-content" id="notes-content"></div>
  </div>
</div>

</div><!-- end #app -->

<script>
// ═══════════════════════════════════════════════════════════════
// STATE
// ═══════════════════════════════════════════════════════════════
const S = {
  subject: null, topic: null, mode: 'quiz',
  questions: [], qi: 0, sessionCorrect: 0, sessionTotal: 0,
  totalScore: 0, streak: 0,
};

// ═══════════════════════════════════════════════════════════════
// SUBJECT CONFIG
// ═══════════════════════════════════════════════════════════════
const SUBJECTS = {
  physics: {
    color: '#e5484d', dim: 'rgba(229,72,77,0.12)',
    topics: [
      { id:'forces',     name:'Forces & Motion',                paper:'Paper 1' },
      { id:'energy',     name:'Energy Stores & Transfers',      paper:'Paper 1' },
      { id:'waves',      name:'Waves',                          paper:'Paper 1' },
      { id:'em_spec',    name:'Electromagnetic Spectrum',       paper:'Paper 1' },
      { id:'electricity',name:'Electricity & Circuits',         paper:'Paper 2' },
      { id:'magnetism',  name:'Magnetism & Electromagnetism',   paper:'Paper 2' },
      { id:'particles',  name:'Particle Model of Matter',       paper:'Paper 1' },
      { id:'atomic',     name:'Atomic Structure & Radioactivity',paper:'Paper 1'},
      { id:'space',      name:'Space Physics',                  paper:'Paper 2' },
    ]
  },
  biology: {
    color: '#22c55e', dim: 'rgba(34,197,94,0.12)',
    topics: [
      { id:'cells',         name:'Cell Biology',                   paper:'Paper 1' },
      { id:'organisation',  name:'Organisation',                   paper:'Paper 1' },
      { id:'infection',     name:'Infection & Response',           paper:'Paper 1' },
      { id:'bioenergetics', name:'Bioenergetics',                  paper:'Paper 1' },
      { id:'homeostasis',   name:'Homeostasis & Response',         paper:'Paper 2' },
      { id:'inheritance',   name:'Inheritance & Variation',        paper:'Paper 2' },
      { id:'evolution',     name:'Evolution & Classification',     paper:'Paper 2' },
      { id:'ecology',       name:'Ecology & Biodiversity',         paper:'Paper 2' },
    ]
  },
  chemistry: {
    color: '#3b82f6', dim: 'rgba(59,130,246,0.12)',
    topics: [
      { id:'atomic_chem',  name:'Atomic Structure & Periodic Table', paper:'Paper 1' },
      { id:'bonding',      name:'Bonding, Structure & Properties',   paper:'Paper 1' },
      { id:'quantitative', name:'Quantitative Chemistry',            paper:'Paper 1' },
      { id:'chem_changes', name:'Chemical Changes',                  paper:'Paper 1' },
      { id:'electrolysis', name:'Electrolysis',                      paper:'Paper 1' },
      { id:'energy_chem',  name:'Energy Changes',                    paper:'Paper 2' },
      { id:'rates',        name:'Rates of Reaction & Equilibrium',   paper:'Paper 2' },
      { id:'organic',      name:'Organic Chemistry',                 paper:'Paper 2' },
      { id:'analysis',     name:'Chemical Analysis',                 paper:'Paper 2' },
    ]
  }
};

// ═══════════════════════════════════════════════════════════════
// QUESTION BANK  (templates with randomised values)
// ═══════════════════════════════════════════════════════════════
// Each entry: { gen: fn() => {q, opts:[4], ans:0-3, exp, hint?} }
// Multiple generators per topic for variety.

function rnd(min,max){return Math.floor(Math.random()*(max-min+1))+min}
function rndF(min,max,dp=1){return parseFloat((Math.random()*(max-min)+min).toFixed(dp))}
function shuffle(arr){let a=[...arr];for(let i=a.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[a[i],a[j]]=[a[j],a[i]]}return a}

// Makes wrong answers around a correct value
function wrongsAround(correct, spread, count=3, round=0){
  const set=new Set();
  while(set.size<count){
    let w=correct+(Math.random()<.5?1:-1)*rnd(1,spread);
    if(w!==correct&&w>0) set.add(round?Math.round(w/round)*round:w);
  }
  return [...set];
}

function makeQ(q,correct,wrongs,exp,hint){
  const allOpts=[correct,...wrongs];
  // shuffle but remember where correct ended up
  const shuffled=shuffle(allOpts);
  return {q,opts:shuffled,ans:shuffled.indexOf(correct),exp,hint};
}

const QB = {

// ── PHYSICS ──────────────────────────────────────────────────────
physics_forces: [
  ()=>{const m=rnd(500,3000),a=rndF(0.5,8);const F=parseFloat((m*a).toFixed(1));return makeQ(
    `A vehicle of mass ${m} kg accelerates at ${a} m/s². What is the resultant force acting on it?`,
    `${F} N`, wrongsAround(F,F*0.4,3,1).map(v=>v+' N'), `F = ma = ${m} × ${a} = ${F} N (Newton's 2nd law).`
  )},
  ()=>{const W=rnd(200,1500);const m=parseFloat((W/10).toFixed(1));return makeQ(
    `An object weighs ${W} N on Earth (g = 10 N/kg). What is its mass?`,
    `${m} kg`, wrongsAround(m,m*0.5,3,0.5).map(v=>v+' kg'), `W = mg  →  m = W ÷ g = ${W} ÷ 10 = ${m} kg.`
  )},
  ()=>{const u=rnd(0,20),a=rnd(1,6),t=rnd(2,8);const v=u+a*t;return makeQ(
    `An object starts at ${u} m/s and accelerates at ${a} m/s² for ${t} s. What is its final velocity?`,
    `${v} m/s`, wrongsAround(v,v*0.4,3,1).map(w=>w+' m/s'), `v = u + at = ${u} + (${a} × ${t}) = ${v} m/s.`
  )},
  ()=>makeQ('Which of the following is a VECTOR quantity?','Velocity',['Speed','Mass','Temperature'],
    'Vectors have both magnitude and direction. Velocity is speed in a given direction.','Think: does it have a direction?'),
  ()=>makeQ('What does Newton\'s First Law state?',
    'An object remains at rest or moves at constant velocity unless acted on by a resultant force.',
    ['The resultant force equals mass times acceleration.','Every action has an equal and opposite reaction.','Objects always accelerate due to gravity.'],
    'Newton\'s 1st Law = Law of Inertia. A non-zero resultant force is needed to change motion.'),
  ()=>{const m=rnd(10,80),v=rnd(2,15);const p=m*v;return makeQ(
    `Calculate the momentum of a ${m} kg object moving at ${v} m/s.`,
    `${p} kg m/s`, wrongsAround(p,p*0.4,3,5).map(w=>w+' kg m/s'), `p = mv = ${m} × ${v} = ${p} kg m/s.`
  )},
  ()=>makeQ('Stopping distance equals:','Thinking distance + braking distance',
    ['Speed × time','Reaction time × speed','Braking distance only'],
    'Stopping distance = thinking distance (reaction time × speed) + braking distance (depends on forces).'),
  ()=>makeQ('A resultant force of zero means:','The object is in equilibrium (stationary or constant velocity)',
    ['The object is accelerating','All individual forces are zero','The object is decelerating'],
    'Equilibrium = zero resultant force. Forces can exist but cancel out. The object does NOT change velocity.'),
  ()=>{const F=rnd(100,2000),m=rnd(10,200);const a=parseFloat((F/m).toFixed(2));return makeQ(
    `A resultant force of ${F} N acts on a ${m} kg mass. What is the acceleration?`,
    `${a} m/s²`, wrongsAround(a,a*0.5,3,0.1).map(w=>Math.abs(w).toFixed(2)+' m/s²'), `a = F/m = ${F}/${m} = ${a} m/s².`
  )},
  ()=>makeQ('Which factor does NOT affect thinking distance?','Road surface condition',
    ['Speed of vehicle','Driver reaction time','Alcohol consumption'],
    'Thinking distance = reaction time × speed. Road condition affects braking distance, not thinking distance.'),
  ()=>{const d=rnd(20,200),t=rnd(5,30);const s=parseFloat((d/t).toFixed(2));return makeQ(
    `An object travels ${d} m in ${t} s at constant speed. What is its speed?`,
    `${s} m/s`, wrongsAround(s,s*0.5,3,0.1).map(w=>Math.abs(parseFloat(w.toFixed(2)))+' m/s'), `Speed = distance ÷ time = ${d} ÷ ${t} = ${s} m/s.`
  )},
  ()=>makeQ("Newton's 3rd Law states:",'For every action there is an equal and opposite reaction force on a different object.',
    ['F = ma','Resultant force causes acceleration','Objects fall with constant velocity'],
    "The paired forces act on DIFFERENT objects, are equal in size and opposite in direction."),
],

physics_energy: [
  ()=>{const m=rnd(1,20),h=rnd(1,20);const gpe=m*10*h;return makeQ(
    `A ${m} kg object is lifted ${h} m. Calculate its gain in gravitational potential energy. (g = 10 N/kg)`,
    `${gpe} J`, wrongsAround(gpe,gpe*0.4,3,5).map(w=>w+' J'), `GPE = mgh = ${m} × 10 × ${h} = ${gpe} J.`
  )},
  ()=>{const m=rnd(1,20),v=rnd(1,15);const ke=parseFloat((0.5*m*v*v).toFixed(1));return makeQ(
    `Calculate the kinetic energy of a ${m} kg object moving at ${v} m/s.`,
    `${ke} J`, wrongsAround(ke,ke*0.4,3,5).map(w=>w+' J'), `KE = ½mv² = ½ × ${m} × ${v}² = ${ke} J.`
  )},
  ()=>{const P=rnd(500,3000),t=rnd(30,600);const E=P*t;return makeQ(
    `A ${P} W device runs for ${t} s. How much energy does it transfer?`,
    `${E} J`, wrongsAround(E,E*0.4,3,100).map(w=>w+' J'), `E = Pt = ${P} × ${t} = ${E} J.`
  )},
  ()=>{const E=rnd(100,3000),t=rnd(10,120);const P=parseFloat((E/t).toFixed(1));return makeQ(
    `A device transfers ${E} J of energy in ${t} s. What is its power?`,
    `${P} W`, wrongsAround(P,P*0.5,3,5).map(w=>w+' W'), `Power = Energy ÷ time = ${E} ÷ ${t} = ${P} W.`
  )},
  ()=>{const eff=rnd(30,90);const inp=rnd(200,2000);const use=Math.round(inp*eff/100);return makeQ(
    `A motor is ${eff}% efficient. It receives ${inp} J of energy input. How much is usefully transferred?`,
    `${use} J`, wrongsAround(use,use*0.4,3,10).map(w=>w+' J'), `Useful output = efficiency × input = ${eff/100} × ${inp} = ${use} J.`
  )},
  ()=>makeQ('Which energy store is associated with a compressed spring?','Elastic potential',
    ['Kinetic','Gravitational potential','Chemical'],
    'Springs (compressed or stretched) store elastic potential energy.'),
  ()=>makeQ('The principle of conservation of energy states:','Energy cannot be created or destroyed, only transferred or transformed.',
    ['Energy is always lost as heat','Energy can be created by burning fuel','Kinetic energy is always conserved'],
    'Total energy in a closed system is constant. "Dissipated" energy goes to thermal stores — it is not lost.'),
  ()=>makeQ('What is meant by a "dissipated" energy transfer?','Energy transferred to the surroundings in a less useful form (usually thermal).',
    ['Energy stored in a chemical form','Useful energy output','Energy input to a machine'],
    'Dissipated energy is wasted — typically heating the surroundings via friction or air resistance.'),
  ()=>makeQ('Which method of reducing energy loss in a building involves filling gaps in external walls?','Cavity wall insulation',
    ['Double glazing','Loft insulation','Draught-proofing'],
    'Cavity wall insulation fills the air gap in double-brick walls, reducing convection losses.'),
  ()=>{const u=rnd(5,20);const ke=parseFloat((0.5*u*u).toFixed(1));return makeQ(
    `A 1 kg ball moving at ${u} m/s comes to rest. How much kinetic energy is dissipated?`,
    `${ke} J`, wrongsAround(ke,ke*0.5,3,1).map(w=>w+' J'), `KE = ½mv² = ½ × 1 × ${u}² = ${ke} J. All converted to thermal/sound.`
  )},
],

physics_waves: [
  ()=>{const f=rnd(1,500),lam=rndF(0.1,10);const v=parseFloat((f*lam).toFixed(2));return makeQ(
    `A wave has frequency ${f} Hz and wavelength ${lam} m. What is its wave speed?`,
    `${v} m/s`, wrongsAround(v,v*0.5,3,1).map(w=>w+' m/s'), `v = fλ = ${f} × ${lam} = ${v} m/s.`
  )},
  ()=>{const v=rnd(200,400),f=rnd(100,1000);const lam=parseFloat((v/f).toFixed(3));return makeQ(
    `Sound travels at ${v} m/s. If its frequency is ${f} Hz, what is its wavelength?`,
    `${lam} m`, wrongsAround(lam,lam*0.5,3,0.01).map(w=>parseFloat(Math.abs(w).toFixed(3))+' m'), `λ = v/f = ${v}/${f} = ${lam} m.`
  )},
  ()=>makeQ('What is the difference between a transverse and a longitudinal wave?',
    'In transverse waves, oscillations are perpendicular to energy transfer. In longitudinal waves, oscillations are parallel.',
    ['Longitudinal waves travel faster','Transverse waves need a medium, longitudinal do not','Longitudinal waves have higher frequency'],
    'Light is transverse; sound is longitudinal. Longitudinal waves have compressions and rarefactions.'),
  ()=>makeQ('What does the amplitude of a wave represent?','The maximum displacement from the equilibrium position.',
    ['The distance between two crests','The number of waves per second','The speed of the wave'],
    'Amplitude = maximum displacement. A higher amplitude means more energy carried.'),
  ()=>makeQ('Which of the following correctly defines wave frequency?','The number of complete waves passing a point per second.',
    ['The distance between two successive crests','The maximum displacement of the wave','The speed at which energy travels'],
    'Frequency is measured in Hertz (Hz). f = 1/T where T is the period.'),
  ()=>{const T=rndF(0.01,2,2);const f=parseFloat((1/T).toFixed(2));return makeQ(
    `A wave has a period of ${T} s. What is its frequency?`,
    `${f} Hz`, wrongsAround(f,f*0.5,3,0.1).map(w=>parseFloat(Math.abs(w).toFixed(2))+' Hz'), `f = 1/T = 1/${T} = ${f} Hz.`
  )},
  ()=>makeQ('Which statement about the reflection of waves is correct?',
    'The angle of incidence equals the angle of reflection (measured from the normal).',
    ['The angle of incidence equals the angle of refraction','Waves speed up on reflection','The frequency changes on reflection'],
    'Law of reflection: angle of incidence = angle of reflection. Both measured from the normal.'),
  ()=>makeQ('Refraction of waves occurs because:','Waves change speed when moving between different media.',
    ['Waves reflect off a surface','The frequency of the wave changes','The wave loses energy'],
    'Refraction happens at the boundary between media of different density. Speed changes, frequency stays the same, wavelength changes.'),
],

physics_em_spec: [
  ()=>makeQ('Arrange the following EM waves in order of INCREASING frequency: radio, visible, gamma.',
    'Radio → Visible → Gamma',
    ['Gamma → Visible → Radio','Visible → Radio → Gamma','Radio → Gamma → Visible'],
    'The electromagnetic spectrum from low to high frequency: radio, microwave, infrared, visible, UV, X-ray, gamma.'),
  ()=>makeQ('What speed do all electromagnetic waves travel at in a vacuum?','3 × 10⁸ m/s',
    ['3 × 10⁶ m/s','3 × 10¹⁰ m/s','300 m/s'],
    'All EM waves travel at the speed of light (c = 3 × 10⁸ m/s) in a vacuum.'),
  ()=>makeQ('Which type of EM radiation is used in medical imaging to detect bone fractures?','X-rays',
    ['Gamma rays','Infrared','Microwaves'],
    'X-rays are absorbed by dense materials like bone. Gamma rays are also used medically but for cancer treatment and imaging internal organs.'),
  ()=>makeQ('Which EM wave has the LONGEST wavelength?','Radio waves',
    ['Microwaves','Infrared','X-rays'],
    'Radio waves have the longest wavelength (metres to km) and lowest frequency in the EM spectrum.'),
  ()=>makeQ('Ultraviolet radiation is dangerous because:','It can cause skin cancer and damage eyesight by ionising cells.',
    ['It heats objects too quickly','It travels faster than visible light','It reflects off all surfaces'],
    'UV is ionising at high doses — it can damage DNA in skin cells, leading to mutations.'),
  ()=>makeQ('Infrared radiation is used for:','Thermal imaging, remote controls and optical fibre communication.',
    ['Killing cancer cells','Detecting bone fractures','Sterilising medical equipment'],
    'IR is emitted by warm objects (thermal imaging), used in TV remotes, and transmitted through optical fibres.'),
  ()=>makeQ('Gamma rays and X-rays are both:','Ionising electromagnetic radiation.',
    ['Mechanical waves','Longitudinal waves','Slower than visible light'],
    'Both are ionising — they carry enough energy to remove electrons from atoms. This makes them dangerous to living tissue.'),
],

physics_electricity: [
  ()=>{const V=rnd(3,24),R=rnd(1,20);const I=parseFloat((V/R).toFixed(2));return makeQ(
    `A component has resistance ${R} Ω and a p.d. of ${V} V across it. What current flows?`,
    `${I} A`, wrongsAround(I,I*0.5,3,0.1).map(w=>parseFloat(Math.abs(w).toFixed(2))+' A'), `I = V/R = ${V}/${R} = ${I} A. (Ohm's Law)`
  )},
  ()=>{const I=rndF(0.2,5,1),R=rnd(2,40);const V=parseFloat((I*R).toFixed(1));return makeQ(
    `A current of ${I} A flows through a ${R} Ω resistor. What is the potential difference?`,
    `${V} V`, wrongsAround(V,V*0.5,3,1).map(w=>w+' V'), `V = IR = ${I} × ${R} = ${V} V.`
  )},
  ()=>makeQ('In a SERIES circuit, which quantity is the SAME through all components?','Current',
    ['Potential difference','Resistance','Power'],
    'In series: current is the same everywhere. Voltage divides between components.'),
  ()=>makeQ('In a PARALLEL circuit, which quantity is the SAME across all branches?','Potential difference (voltage)',
    ['Current','Resistance','Power'],
    'In parallel: voltage across each branch equals the supply voltage. Current splits between branches.'),
  ()=>{const V=rnd(3,12),I=rndF(0.1,3,1);const P=parseFloat((V*I).toFixed(2));return makeQ(
    `A component operates at ${V} V and draws ${I} A. What is its power?`,
    `${P} W`, wrongsAround(P,P*0.5,3,0.5).map(w=>w+' W'), `P = VI = ${V} × ${I} = ${P} W.`
  )},
  ()=>{const P=rnd(100,3000),t=rnd(60,3600);const E=parseFloat((P*t).toFixed(0));return makeQ(
    `A ${P} W device runs for ${t} s. Calculate the energy transferred.`,
    `${E} J`, wrongsAround(E,E*0.3,3,1000).map(w=>w+' J'), `E = Pt = ${P} × ${t} = ${E} J.`
  )},
  ()=>makeQ('What does an oscilloscope display?','Voltage against time',
    ['Current against resistance','Power against time','Frequency against voltage'],
    'An oscilloscope shows how voltage varies with time. The trace shape indicates AC or DC and frequency.'),
  ()=>makeQ('The live wire in a UK plug is coloured:','Brown',
    ['Blue','Green and yellow','Red'],
    'UK wiring: Live = Brown, Neutral = Blue, Earth = Green/Yellow.'),
  ()=>{const R1=rnd(2,10),R2=rnd(2,10);const Rs=R1+R2;return makeQ(
    `Two resistors, ${R1} Ω and ${R2} Ω, are connected in series. What is the total resistance?`,
    `${Rs} Ω`, wrongsAround(Rs,Rs*0.4,3,1).map(w=>w+' Ω'), `Series: R_total = R1 + R2 = ${R1} + ${R2} = ${Rs} Ω.`
  )},
  ()=>makeQ('Which component has a resistance that decreases as temperature increases?','Thermistor (NTC)',
    ['Fixed resistor','LDR','Diode'],
    'An NTC (Negative Temperature Coefficient) thermistor decreases resistance as temperature rises — useful in thermostats.'),
  ()=>makeQ('What is the function of a fuse in a circuit?','It melts and breaks the circuit if the current exceeds a safe level.',
    ['It stores charge','It reduces voltage','It measures current'],
    'A fuse contains a thin wire that melts if excess current flows, protecting the appliance and preventing fires.'),
],

physics_magnetism: [
  ()=>makeQ('What happens to the force on a current-carrying conductor in a magnetic field if the current is doubled?','The force doubles.',
    ['The force halves','The force stays the same','The force quadruples'],
    'F = BIL. Force is directly proportional to current, so doubling I doubles F.'),
  ()=>makeQ('What is electromagnetic induction?','A potential difference (and current) is induced when a conductor moves relative to a magnetic field.',
    ['A magnet is created by passing current through iron','A current is destroyed by a magnetic field','Magnets attract all metals'],
    'EMF is induced when there is a change in magnetic flux linkage — by moving the conductor or changing the field.'),
  ()=>makeQ('How can the size of the induced EMF in a generator be increased?',
    'Increasing the number of turns on the coil, using a stronger magnet, or rotating faster.',
    ['Using a weaker magnet','Decreasing the number of turns','Slowing the rotation'],
    'Induced EMF ∝ rate of change of flux linkage = more turns, stronger field, faster rotation.'),
  ()=>makeQ('A step-up transformer:','Increases voltage and decreases current.',
    ['Increases both voltage and current','Decreases voltage and increases current','Has fewer turns on the secondary coil'],
    'Step-up: N_s > N_p, so V_s > V_p. Since power is conserved (ideal transformer), I_s < I_p.'),
  ()=>{const Vp=rnd(100,400),Np=rnd(100,1000),Ns=rnd(100,1000);const Vs=Math.round(Vp*Ns/Np);return makeQ(
    `A transformer has ${Np} primary turns and ${Ns} secondary turns. If the primary voltage is ${Vp} V, what is the secondary voltage?`,
    `${Vs} V`, wrongsAround(Vs,Vs*0.4,3,10).map(w=>w+' V'), `Vs/Vp = Ns/Np → Vs = ${Vp} × ${Ns}/${Np} = ${Vs} V.`
  )},
  ()=>makeQ('Why is electricity transmitted at high voltage across the National Grid?','High voltage means low current, which reduces power lost as heat in the cables (P = I²R).',
    ['High voltage is safer for workers','High voltage makes cables lighter','High voltage increases the power output'],
    'P_loss = I²R. Using high V means low I, dramatically reducing resistive heating losses in transmission cables.'),
  ()=>makeQ('Which rule is used to find the direction of force on a current-carrying conductor in a magnetic field?','Fleming\'s Left-Hand Rule',
    ['Fleming\'s Right-Hand Rule','The Right-hand grip rule','Lenz\'s Law'],
    "Fleming's Left = motors (force/motion). Fleming's Right = generators (induced current)."),
],

physics_particles: [
  ()=>{const m=rnd(1,5),T1=rnd(10,40),T2=rnd(41,100);const c=4200;const Q=m*c*(T2-T1);return makeQ(
    `Calculate the energy needed to heat ${m} kg of water from ${T1}°C to ${T2}°C. (specific heat capacity of water = 4200 J/kg°C)`,
    `${Q} J`, wrongsAround(Q,Q*0.3,3,10000).map(w=>w+' J'), `Q = mcΔT = ${m} × 4200 × (${T2}-${T1}) = ${m} × 4200 × ${T2-T1} = ${Q} J.`
  )},
  ()=>makeQ('Which state of matter has particles that are close together but able to flow past each other?','Liquid',
    ['Solid','Gas','Plasma'],
    'Liquids have close-packed but mobile particles — they have a fixed volume but no fixed shape.'),
  ()=>makeQ('What happens to the pressure of a fixed mass of gas if the volume is halved at constant temperature?','The pressure doubles.',
    ['The pressure halves','The pressure stays the same','The pressure quadruples'],
    'Boyle\'s Law: P₁V₁ = P₂V₂. Halving volume doubles pressure (assuming constant temperature).'),
  ()=>makeQ('What is the definition of specific latent heat?','The energy required to change the state of 1 kg of a substance at constant temperature.',
    ['The energy to heat 1 kg by 1°C','The energy to melt all of a substance','The temperature at which a substance boils'],
    'SLH has units J/kg. No temperature change occurs during state changes — energy goes into breaking intermolecular bonds.'),
  ()=>{const m=rnd(1,5),L=rnd(200000,400000);const Q=m*L;return makeQ(
    `How much energy is needed to vaporise ${m} kg of a liquid with specific latent heat of vaporisation ${L} J/kg?`,
    `${Q} J`, wrongsAround(Q,Q*0.3,3,50000).map(w=>w+' J'), `Q = mL = ${m} × ${L} = ${Q} J.`
  )},
  ()=>makeQ('Brownian motion provides evidence for:','The random motion of particles in fluids.',
    ['The wave nature of light','The fixed positions of particles in solids','Gravity acting on particles'],
    'Brownian motion (random jiggling of pollen grains in water) showed that water molecules move randomly and collide with visible particles.'),
],

physics_atomic: [
  ()=>makeQ('An alpha particle consists of:','2 protons and 2 neutrons (a helium nucleus).',
    ['1 proton and 1 neutron','2 protons and 0 neutrons','0 protons and 2 neutrons'],
    'Alpha (α) = ²₄He nucleus = 2p + 2n. Charge: +2. Stopped by a sheet of paper.'),
  ()=>makeQ('Which type of nuclear radiation has the GREATEST penetrating power?','Gamma (γ)',
    ['Alpha (α)','Beta (β)','Neutron'],
    'Gamma is the most penetrating — requires several cm of lead or metres of concrete to reduce intensity significantly.'),
  ()=>makeQ('What is meant by the half-life of a radioactive isotope?','The time taken for half the radioactive nuclei in a sample to decay.',
    ['The time for all atoms to decay','The time for the activity to become zero','The average lifetime of one atom'],
    'Half-life is constant for a given isotope and does not depend on external conditions.'),
  ()=>{const init=rnd(800,3200),n=rnd(2,5);const rem=Math.round(init/Math.pow(2,n));return makeQ(
    `A sample initially has ${init} radioactive nuclei. After ${n} half-lives, how many remain?`,
    `${rem}`, wrongsAround(rem,rem*0.5,3,10).map(w=>String(Math.max(1,Math.round(w)))), `After ${n} half-lives: ${init} ÷ 2^${n} = ${init} ÷ ${Math.pow(2,n)} = ${rem}.`
  )},
  ()=>makeQ('What happens to the atomic number when a nucleus emits a beta-minus particle?','It increases by 1.',
    ['It decreases by 1','It stays the same','It decreases by 2'],
    'Beta-minus: a neutron → proton + electron. Proton number +1, mass number unchanged.'),
  ()=>makeQ('Which application uses the ionising properties of alpha radiation?','Smoke detectors.',
    ['Medical tracers','Cancer radiotherapy','PET scanning'],
    'Alpha emitters in smoke detectors ionise air, allowing current to flow. Smoke particles absorb alpha radiation, reducing current and triggering an alarm.'),
  ()=>makeQ('Nuclear fission involves:','A large nucleus splitting into two smaller nuclei, releasing energy and neutrons.',
    ['Two small nuclei joining to form a larger one','An electron being emitted from the nucleus','A proton changing into a neutron'],
    'Fission: heavy nucleus (e.g. U-235) + neutron → 2 daughter nuclei + 2-3 neutrons + energy. Used in nuclear power stations.'),
  ()=>makeQ('Nuclear fusion involves:','Two light nuclei joining to form a heavier nucleus, releasing energy.',
    ['A heavy nucleus splitting apart','Beta particle emission','Gamma ray absorption'],
    'Fusion (e.g. in the Sun): H + H → He + energy. Requires extremely high temperatures to overcome electrostatic repulsion.'),
],

physics_space: [
  ()=>makeQ('What keeps planets in orbit around the Sun?','Gravity (gravitational attraction between the planet and the Sun).',
    ['Magnetic force','The planet\'s kinetic energy alone','Electrostatic force'],
    'Gravity provides the centripetal force needed to keep planets in their elliptical orbits.'),
  ()=>makeQ('The life cycle of a star similar in mass to the Sun ends as:','A white dwarf.',
    ['A neutron star','A black hole','A red giant permanently'],
    'Sun-like stars: main sequence → red giant → planetary nebula → white dwarf. Massive stars end as neutron stars or black holes.'),
  ()=>makeQ('What is the evidence that the universe is expanding?','The red-shift of distant galaxies — their light is stretched to longer wavelengths.',
    ['The brightness of stars increases over time','The number of galaxies is decreasing','Cosmic microwave background radiation cools galaxies'],
    'Red-shift: light from distant galaxies is shifted to longer (redder) wavelengths, indicating they move away from us. More distant = greater red-shift.'),
  ()=>makeQ('The Big Bang theory suggests:','The universe began as an extremely hot, dense point and has been expanding ever since.',
    ['The universe has always existed in its current state','The universe is contracting','Stars are exploding outward from a central point'],
    'Evidence for Big Bang: cosmic microwave background radiation and the red-shift of galaxies.'),
  ()=>makeQ('A light-year is:','The distance light travels in one year (about 9.46 × 10¹⁵ m).',
    ['The time for light to travel 1 m','A unit of time equal to one year','The speed of light per second'],
    'Light-year is a unit of DISTANCE, not time. It\'s used because distances in space are so vast.'),
],

// ── BIOLOGY ──────────────────────────────────────────────────────
biology_cells: [
  ()=>makeQ('Which organelle controls the cell\'s activities and contains DNA?','Nucleus',
    ['Ribosome','Mitochondrion','Vacuole'],
    'The nucleus contains chromosomes (DNA) and controls gene expression — it directs what the cell does.'),
  ()=>makeQ('What is the function of mitochondria?','Site of aerobic respiration — produces ATP (energy for the cell).',
    ['Produce proteins','Control what enters the cell','Store water and minerals'],
    'Mitochondria are the powerhouses of the cell: glucose + oxygen → CO₂ + water + ATP.'),
  ()=>makeQ('Which of these features is found in plant cells but NOT animal cells?','Cell wall, chloroplasts and large permanent vacuole.',
    ['Nucleus','Cell membrane','Mitochondria'],
    'Plant cells have: cellulose cell wall (rigid support), chloroplasts (photosynthesis), and a large central vacuole (turgor pressure).'),
  ()=>makeQ('Osmosis is defined as:','The movement of water molecules from a high water potential to a low water potential through a partially permeable membrane.',
    ['Movement of any molecule from high to low concentration','Active movement of water requiring ATP','Random movement of all particles'],
    'Osmosis is a special case of diffusion involving ONLY water, through a partially permeable membrane, down a water potential gradient.'),
  ()=>makeQ('What does mitosis produce?','Two genetically identical diploid daughter cells.',
    ['Four genetically unique haploid cells','Two genetically unique diploid cells','One cell with double the DNA'],
    'Mitosis: used for growth, repair and asexual reproduction. Produces 2 identical cells with the same number of chromosomes as the parent.'),
  ()=>makeQ('Which type of cell division produces gametes (sex cells)?','Meiosis.',
    ['Mitosis','Binary fission','Budding'],
    'Meiosis produces 4 genetically unique haploid cells (gametes). It introduces genetic variation via crossing over.'),
  ()=>makeQ('Active transport differs from diffusion because:','It moves substances against the concentration gradient and requires energy (ATP).',
    ['It moves substances down the concentration gradient','It only involves water molecules','No membrane is needed'],
    'Active transport requires carrier proteins and ATP — used to absorb glucose and mineral ions against the gradient.'),
  ()=>{const mag=rnd(100,1000),actual=rndF(0.01,0.5,2);const image=parseFloat((mag*actual).toFixed(2));return makeQ(
    `A cell has an actual length of ${actual} mm and is magnified ×${mag}. What is the image size?`,
    `${image} mm`, wrongsAround(image,image*0.5,3,1).map(w=>Math.abs(w).toFixed(2)+' mm'), `Image = magnification × actual size = ${mag} × ${actual} = ${image} mm.`
  )},
  ()=>makeQ('What is a prokaryotic cell?','A cell with no membrane-bound nucleus — its DNA floats freely in the cytoplasm.',
    ['A cell with a nucleus','A cell with chloroplasts','A multicellular organism\'s cell'],
    'Prokaryotes (bacteria) have no nucleus or membrane-bound organelles. They are smaller and simpler than eukaryotic cells.'),
  ()=>makeQ('Which process allows cells to take up large particles by engulfing them?','Phagocytosis.',
    ['Osmosis','Active transport','Diffusion'],
    'Phagocytosis = "cell eating". White blood cells engulf pathogens this way.'),
],

biology_organisation: [
  ()=>makeQ('In the heart, which chambers pump blood to the LUNGS?','The right ventricle.',
    ['The left ventricle','The right atrium','The left atrium'],
    'Right side of heart → lungs (pulmonary circulation). Left side → body (systemic circulation). Ventricles pump; atria receive.'),
  ()=>makeQ('What is the role of valves in the heart?','To prevent the backflow of blood.',
    ['To increase blood pressure','To produce blood cells','To pump blood into arteries'],
    'Valves (atrioventricular and semilunar) ensure one-way blood flow through the heart.'),
  ()=>makeQ('Which blood vessel carries oxygenated blood away from the heart?','Aorta (and pulmonary vein from lungs to heart)',
    ['Vena cava','Pulmonary artery','Capillary'],
    'Arteries carry blood AWAY from the heart. The aorta carries oxygenated blood to the body. (Pulmonary artery is the exception — it carries deoxygenated blood to lungs.)'),
  ()=>makeQ('What is the function of villi in the small intestine?','To increase the surface area for absorption of digested nutrients.',
    ['To produce digestive enzymes','To neutralise stomach acid','To store bile'],
    'Villi (and microvilli) massively increase surface area. They have a rich blood supply and are only one cell thick — ideal for absorption.'),
  ()=>makeQ('What is the role of lipase in digestion?','It breaks down fats (lipids) into fatty acids and glycerol.',
    ['It breaks down proteins into amino acids','It breaks down starch into sugars','It breaks down nucleic acids'],
    'Lipase is produced in the pancreas and small intestine. Products: fatty acids + glycerol.'),
  ()=>makeQ('Where is bile produced and where is it stored?','Produced in the liver; stored in the gall bladder.',
    ['Produced in the pancreas; stored in the stomach','Produced in the small intestine; stored in the liver','Produced in the stomach; stored in the spleen'],
    'Bile emulsifies fats (increases surface area for lipase). It also neutralises stomach acid in the small intestine.'),
  ()=>makeQ('What are the main structures in the leaf adapted for photosynthesis?',
    'Chloroplasts in palisade cells, stomata for gas exchange, and spongy mesophyll for internal surface area.',
    ['Root hair cells and xylem','Villi and capillaries','Guard cells and phloem'],
    'The leaf is adapted with: palisade mesophyll (packed with chloroplasts), air spaces (gas diffusion), stomata (CO₂ in / O₂ out), waxy cuticle (waterproof).'),
  ()=>makeQ('What is the function of xylem tissue in plants?','Transport water and mineral ions from roots to leaves (transpiration stream).',
    ['Transport sugars from leaves to rest of plant','Carry out photosynthesis','Exchange gases with atmosphere'],
    'Xylem: dead, hollow tubes with lignified walls. Water moves up by transpiration pull (cohesion-tension).'),
],

biology_infection: [
  ()=>makeQ('Which type of pathogen is responsible for the disease malaria?','A protist (Plasmodium).',
    ['A bacterium','A virus','A fungus'],
    'Malaria is caused by Plasmodium — a eukaryotic protist. It is spread by the Anopheles mosquito vector.'),
  ()=>makeQ('How do viruses cause disease?','They invade host cells and take over their machinery to replicate, causing cell damage and death.',
    ['They produce toxins that are released into the blood','They are too large to enter cells','They only affect the immune system'],
    'Viruses are not cells — they inject genetic material into host cells, replicate, then burst out, destroying the host cell.'),
  ()=>makeQ('What is the role of antibodies in the immune response?','They bind to antigens on pathogens, marking them for destruction.',
    ['They engulf pathogens directly','They produce toxins to kill bacteria','They lower body temperature'],
    'B-lymphocytes produce specific antibodies that bind to antigens. Antibodies can neutralise pathogens, clump them (agglutination) or label them for phagocytosis.'),
  ()=>makeQ('How do vaccines provide protection against disease?','They introduce dead or weakened antigens, stimulating the immune system to produce memory cells without causing disease.',
    ['They kill all bacteria in the body','They provide ready-made antibodies permanently','They prevent all mutations in viruses'],
    'Vaccines = active immunity. Memory cells remain — on re-exposure, faster/stronger antibody response prevents illness.'),
  ()=>makeQ('Why do antibiotics NOT work against viral infections?','Viruses have no cell wall or ribosomes of their own — antibiotics target bacterial structures.',
    ['Viruses are too large for antibiotics','Viruses are made of the same material as body cells','Antibiotics are anti-inflammatory drugs'],
    'Antibiotics target bacterial cell walls or protein synthesis machinery. Viruses use host cell machinery, so antibiotics cannot selectively target them.'),
  ()=>makeQ('What is meant by antibiotic resistance?','Some bacteria survive treatment due to a mutation and pass on the resistant gene, making antibiotics less effective.',
    ['Antibiotics become too strong over time','The human body rejects antibiotics','Viruses become immune to antibiotics'],
    'MRSA is a key example. Overuse and misuse of antibiotics accelerates resistance — bacteria evolve via natural selection.'),
],

biology_bioenergetics: [
  ()=>makeQ('What is the word equation for aerobic respiration?','Glucose + Oxygen → Carbon dioxide + Water (+ energy released)',
    ['Glucose → Lactic acid + energy','Glucose + Water → Oxygen + Glucose','Carbon dioxide + Water → Glucose + Oxygen'],
    'Aerobic respiration releases about 38 ATP per glucose molecule. Occurs in the mitochondria.'),
  ()=>makeQ('What is the word equation for anaerobic respiration in ANIMALS?','Glucose → Lactic acid (+ small amount of energy)',
    ['Glucose → Ethanol + Carbon dioxide','Glucose + Oxygen → Carbon dioxide + Water','Lactic acid → Glucose + Energy'],
    'Animal anaerobic respiration produces lactic acid (causes muscle fatigue). Yeast produces ethanol + CO₂.'),
  ()=>makeQ('What is the word equation for photosynthesis?','Carbon dioxide + Water → Glucose + Oxygen',
    ['Glucose + Oxygen → Carbon dioxide + Water','Glucose → Carbon dioxide + Water + Energy','Carbon dioxide + Glucose → Oxygen + Water'],
    'Photosynthesis converts light energy into chemical energy stored in glucose. Occurs in chloroplasts.'),
  ()=>makeQ('Which factor is a limiting factor for photosynthesis on a dim winter day?','Light intensity.',
    ['Carbon dioxide concentration','Water availability','Temperature'],
    'Limiting factors: light intensity, CO₂ concentration, temperature and water. On a dim winter day, light is most likely limiting.'),
  ()=>makeQ('What is oxygen debt (EPOC)?','The extra oxygen needed after exercise to break down lactic acid that built up during anaerobic respiration.',
    ['The oxygen stored in muscles for later use','The oxygen lost during breathing','A measure of aerobic fitness'],
    'During recovery, the liver converts lactic acid to glucose (using oxygen). This oxygen used is the "debt" repaid during panting after exercise.'),
  ()=>{const rate=rnd(5,40),hrs=rnd(2,12);const total=rate*hrs*60;return makeQ(
    `A plant photosynthesises at a rate of ${rate} cm³ O₂ per minute. How much O₂ is produced in ${hrs} hours?`,
    `${total} cm³`, wrongsAround(total,total*0.4,3,50).map(w=>w+' cm³'), `Total = ${rate} × (${hrs} × 60) = ${rate} × ${hrs*60} = ${total} cm³.`
  )},
],

biology_homeostasis: [
  ()=>makeQ('What is homeostasis?','The maintenance of a constant internal environment within the body despite external changes.',
    ['The digestion of food in the intestines','The production of hormones in glands','The transport of oxygen in blood'],
    'Homeostasis maintains temperature, blood glucose, water levels etc. at optimal set points using negative feedback.'),
  ()=>makeQ('Which organ detects blood glucose levels and secretes insulin?','The pancreas.',
    ['The liver','The kidney','The thyroid gland'],
    'The islets of Langerhans in the pancreas: beta cells secrete insulin (when glucose HIGH), alpha cells secrete glucagon (when glucose LOW).'),
  ()=>makeQ('How does insulin lower blood glucose levels?','It stimulates cells to take up glucose and the liver to convert glucose to glycogen (glycogenesis).',
    ['It stimulates the breakdown of glycogen to glucose','It causes the kidneys to excrete glucose','It speeds up respiration in all cells'],
    'Insulin → cells absorb glucose + liver converts glucose → glycogen. Blood glucose falls back to set point.'),
  ()=>makeQ('What is Type 1 diabetes?','An autoimmune condition where the pancreas cannot produce insulin.',
    ['A condition where cells cannot respond to insulin','A dietary disease from excess sugar','A condition only affecting children'],
    'Type 1: immune system destroys beta cells. No insulin produced. Managed with insulin injections.'),
  ()=>makeQ('Which part of the brain acts as the thermoregulatory centre?','The hypothalamus.',
    ['The cerebral cortex','The cerebellum','The medulla oblongata'],
    'The hypothalamus monitors blood temperature and triggers responses (shivering, vasodilation etc.) to correct deviations.'),
  ()=>makeQ('Which response helps the body cool down when it is too hot?','Sweating and vasodilation of skin blood vessels.',
    ['Shivering and vasoconstriction','Increased metabolic rate','Contraction of erector muscles'],
    'Hot: sweat evaporates (latent heat), blood vessels dilate (more heat lost by radiation). Cold: shiver (generate heat), vasoconstrict (reduce heat loss).'),
  ()=>makeQ('What is the function of ADH (anti-diuretic hormone)?','It causes the kidneys to reabsorb more water, producing more concentrated (less) urine.',
    ['It increases urine production','It raises blood pressure by constricting arteries','It stimulates glucose uptake by cells'],
    'When blood is too concentrated: hypothalamus → pituitary releases ADH → kidney collecting duct more permeable to water → more reabsorption.'),
],

biology_inheritance: [
  ()=>makeQ('What is a genotype?','The alleles an organism has for a particular gene.',
    ['The observable characteristics of an organism','The number of chromosomes in a cell','The sex of an organism'],
    'Genotype = genetic make-up (e.g. Bb). Phenotype = observable characteristic (e.g. brown eyes).'),
  ()=>makeQ('In genetics, what does "heterozygous" mean?','The organism has two different alleles for a gene (e.g. Bb).',
    ['The organism has two identical alleles','The organism has no alleles for the gene','The organism expresses the recessive allele'],
    'Heterozygous = Bb (one dominant, one recessive). Homozygous = BB or bb (both the same).'),
  ()=>makeQ('A dominant allele:','Is expressed in the phenotype whenever it is present (even as one copy).',
    ['Is only expressed when two copies are present','Is always harmful','Is on the X chromosome only'],
    'Dominant alleles are expressed in both homozygous (AA) and heterozygous (Aa) organisms.'),
  ()=>makeQ('Which sex chromosomes does a human female have?','XX.',
    ['XY','YY','X only'],
    'Females: XX. Males: XY. The Y chromosome contains the SRY gene that triggers male development.'),
  ()=>{const Pp_cross = ()=>{
    const r = ['PP','Pp','Pp','pp'];
    const purple = 3, white = 1;
    return makeQ(
      'In a cross between two heterozygous parents (Pp × Pp), what is the expected ratio of dominant to recessive phenotypes?',
      '3 : 1', ['1 : 1','1 : 2 : 1','2 : 1'],
      'Punnet square: PP, Pp, Pp, pp → 3 dominant (PP or Pp) : 1 recessive (pp).'
    );
  }; return Pp_cross()},
  ()=>makeQ('What is the name of the condition caused by having an extra chromosome 21?','Down syndrome (trisomy 21).',
    ['Cystic fibrosis','Turner syndrome','Klinefelter syndrome'],
    'Down syndrome: non-disjunction during meiosis → gamete with 2 copies of chromosome 21 → offspring has 47 chromosomes.'),
  ()=>makeQ('Cystic fibrosis is caused by:','A recessive allele that causes thick, sticky mucus to build up in the lungs and digestive system.',
    ['A dominant allele on the Y chromosome','A mutation in chromosome 21','An X-linked recessive allele'],
    'CF = autosomal recessive. Both parents must carry at least one recessive allele (f). Ff carriers are unaffected.'),
],

biology_evolution: [
  ()=>makeQ('Natural selection works because:','Individuals with better-adapted characteristics survive, reproduce more, and pass on their advantageous alleles.',
    ['Organisms choose to develop useful traits','Mutations are always beneficial','All organisms of a species have identical DNA'],
    'Natural selection: variation → differential survival → reproduction → allele frequency change over generations.'),
  ()=>makeQ('What provides the evidence for evolution?','Fossils, DNA similarities between species, and observed changes in populations (e.g. antibiotic resistance).',
    ['The complexity of organisms proves a designer','Fossils show all organisms appeared at once','Species never change'],
    'Multiple lines of evidence: fossil record, comparative anatomy, molecular biology (shared DNA), direct observation of natural selection.'),
  ()=>makeQ('Which scientist is credited with developing the theory of evolution by natural selection?','Charles Darwin.',
    ['Gregor Mendel','Alfred Russel Wallace alone','Louis Pasteur'],
    'Darwin published "On the Origin of Species" (1859). Wallace independently developed a similar theory. Mendel worked on genetics.'),
  ()=>makeQ('What is meant by speciation?','The formation of a new species when populations become reproductively isolated and diverge through natural selection.',
    ['The extinction of a species','A mutation in one individual','The interbreeding of two species'],
    'Speciation: populations isolated → different selection pressures → accumulate different mutations → eventually cannot interbreed = new species.'),
  ()=>makeQ('The binomial naming system for organisms was developed by:','Carl Linnaeus.',
    ['Charles Darwin','Aristotle','Gregor Mendel'],
    'Linnaeus: each organism gets a two-part Latin name (genus + species), e.g. Homo sapiens.'),
],

biology_ecology: [
  ()=>makeQ('What is a food chain? Give the correct order.','Producer → Primary consumer → Secondary consumer → Tertiary consumer',
    ['Consumer → Producer → Decomposer','Predator → Prey → Producer','Sun → Consumer → Decomposer'],
    'Food chains start with a producer (plant) and transfer energy through trophic levels. Each arrow shows energy flow.'),
  ()=>makeQ('Approximately what percentage of energy is transferred between trophic levels?','10%.',
    ['90%','50%','25%'],
    'About 10% of energy is passed on — the rest is lost as heat from respiration, movement and waste. This limits food chain length.'),
  ()=>makeQ('What is biodiversity?','The variety of living organisms in an ecosystem — both the number of species and the abundance of each.',
    ['The number of individuals of one species','The total mass of organisms in an area','The rate of energy flow through an ecosystem'],
    'High biodiversity = healthy, stable ecosystem. Monocultures have very low biodiversity and are vulnerable to disease.'),
  ()=>makeQ('What is the role of decomposers in an ecosystem?','They break down dead organisms and waste, returning minerals and nutrients to the soil.',
    ['They are the primary producers in a food chain','They eat living animals','They photosynthesize to produce energy'],
    'Decomposers (bacteria and fungi) recycle nutrients — essential for the carbon and nitrogen cycles.'),
  ()=>makeQ('Which human activity has caused the greatest loss of biodiversity globally?','Habitat destruction (deforestation, urbanisation, agriculture).',
    ['Captive breeding programmes','Recycling','Organic farming'],
    'Habitat loss eliminates species that depend on that habitat — the leading cause of modern mass extinction.'),
  ()=>{const pop1=rnd(200,1000),pop2=rnd(200,1000),area=rnd(10,100);const d=parseFloat(((pop1+pop2)/(2*area)).toFixed(1));return makeQ(
    `A field of ${area} m² is sampled twice. Counts: ${pop1} and ${pop2}. Estimate population density (per m²).`,
    `${d} per m²`, wrongsAround(d,d*0.5,3,0.5).map(w=>parseFloat(Math.abs(w).toFixed(1))+' per m²'), `Mean = (${pop1}+${pop2})/2 = ${Math.round((pop1+pop2)/2)}. Density = ${Math.round((pop1+pop2)/2)}/${area} = ${d} per m².`
  )},
],

// ── CHEMISTRY ────────────────────────────────────────────────────
chemistry_atomic_chem: [
  ()=>{const p=rnd(1,20),n=rnd(0,25);const A=p+n;return makeQ(
    `An atom has ${p} protons and ${n} neutrons. What is its mass number?`,
    `${A}`, wrongsAround(A,A*0.4,3,1).map(w=>String(Math.max(1,Math.round(Math.abs(w))))), `Mass number = protons + neutrons = ${p} + ${n} = ${A}.`
  )},
  ()=>makeQ('What are isotopes?','Atoms of the same element with the same number of protons but different numbers of neutrons.',
    ['Atoms of different elements','Atoms with the same mass number','Ions of the same element'],
    'Isotopes have the same atomic number (element) but different mass numbers due to different neutron counts.'),
  ()=>makeQ('Which subatomic particle determines what element an atom is?','The number of protons (atomic number).',
    ['The number of neutrons','The number of electrons','The mass number'],
    'Atomic number = number of protons = the identity of the element. Change protons → different element.'),
  ()=>{const p=rnd(3,20);let period;if(p<=2)period=1;else if(p<=10)period=2;else if(p<=18)period=3;else period=4;return makeQ(
    `An element has atomic number ${p}. In which period of the periodic table does it appear?`,
    `Period ${period}`, [`Period ${period+1}`,`Period ${period>1?period-1:period+2}`,`Period ${Math.min(period+2,7)}`].filter(x=>x!==`Period ${period}`).slice(0,3), `Period number = number of occupied electron shells. Z=${p} → ${period} shells → Period ${period}.`
  )},
  ()=>makeQ('Mendeleev arranged elements in his periodic table primarily by:','Relative atomic mass, with exceptions made to group elements with similar properties.',
    ['Atomic number','Alphabetical order','Density'],
    'Mendeleev used atomic mass but swapped some elements (e.g. Te/I) to keep similar properties in columns. Modern table uses atomic number.'),
  ()=>makeQ('Elements in the same GROUP of the periodic table have similar chemical properties because:','They have the same number of electrons in their outer shell.',
    ['They have the same mass number','They are all metals','They have the same number of neutrons'],
    'Chemical properties depend on outer electron configuration. Same group = same number of outer electrons = similar reactivity.'),
  ()=>makeQ('What happens to atomic radius as you go DOWN a group in the periodic table?','It increases — more electron shells are added.',
    ['It decreases','It stays the same','It first increases then decreases'],
    'More shells → larger atom. The increased shielding also reduces nuclear pull on outer electrons.'),
  ()=>makeQ('The relative charge of a neutron is:','0 (neutral).',
    ['+1','-1','+2'],
    'Proton: +1. Neutron: 0. Electron: −1. Atoms are neutral because protons = electrons.'),
],

chemistry_bonding: [
  ()=>makeQ('Which type of bonding involves the transfer of electrons from a metal to a non-metal?','Ionic bonding.',
    ['Covalent bonding','Metallic bonding','Hydrogen bonding'],
    'Ionic: metal loses electrons → positive ion; non-metal gains electrons → negative ion. Electrostatic attraction holds them together.'),
  ()=>makeQ('What is covalent bonding?','Sharing of electron pairs between non-metal atoms.',
    ['Transfer of electrons between atoms','Attraction between oppositely charged ions','Free electrons flowing through a structure'],
    'Covalent bonds form between non-metals. Shared electrons give each atom a full outer shell.'),
  ()=>makeQ('Why do ionic compounds have high melting points?','Strong electrostatic attractions between oppositely charged ions in a lattice require a lot of energy to break.',
    ['They have covalent bonds','They contain free electrons','They are made of small molecules'],
    'Ionic lattices have strong 3D electrostatic forces in all directions — lots of energy needed to separate ions.'),
  ()=>makeQ('Which structure allows metals to conduct electricity?','Metallic bonding — delocalised electrons that can move freely through the lattice.',
    ['Fixed ions that carry charge','Covalent bonds between metal atoms','Ionic lattice with mobile ions'],
    'In metals: positive ions in a sea of delocalised electrons. Electrons carry charge → electrical conductivity.'),
  ()=>makeQ('Diamond has a very high melting point because:','Each carbon atom forms 4 strong covalent bonds in a giant covalent lattice, requiring huge energy to break.',
    ['It has metallic bonds','It contains ionic bonds','It is made of small C₂ molecules'],
    'Diamond: each C bonded to 4 others covalently in a rigid 3D structure. Very hard, very high mp, does not conduct electricity.'),
  ()=>makeQ('Graphite conducts electricity because:','Each carbon atom forms 3 covalent bonds, leaving one delocalised electron per atom that can carry charge.',
    ['It has ionic bonds','It contains mobile ions','It is a metal'],
    'Graphite: layers of hexagonal rings with 1 delocalised electron per C. Layers held by weak van der Waals forces → slippery lubricant.'),
  ()=>makeQ('What is the shape of a water molecule?','Bent/V-shaped (bond angle ~104.5°).',
    ['Linear','Trigonal planar','Tetrahedral'],
    'Water: 2 bonding pairs + 2 lone pairs on oxygen. Lone pairs repel more → bond angle 104.5°.'),
  ()=>makeQ('Fullerenes (e.g. buckminsterfullerene C₆₀) can be used:','As drug-delivery molecules, lubricants and in electronics.',
    ['As structural materials replacing steel','As fuel in combustion engines','As ionic conductors'],
    'Fullerenes have a cage-like structure. C₆₀ (bucky-ball) can carry drug molecules inside. Carbon nanotubes are used in electronics.'),
],

chemistry_quantitative: [
  ()=>{const moles=rndF(0.5,5,1),Mr=rnd(18,100);const mass=parseFloat((moles*Mr).toFixed(1));return makeQ(
    `Calculate the mass of ${moles} moles of a substance with Mr = ${Mr}.`,
    `${mass} g`, wrongsAround(mass,mass*0.4,3,5).map(w=>w+' g'), `mass = moles × Mr = ${moles} × ${Mr} = ${mass} g.`
  )},
  ()=>{const mass=rnd(10,200),Mr=rnd(18,100);const moles=parseFloat((mass/Mr).toFixed(3));return makeQ(
    `How many moles are in ${mass} g of a substance with Mr = ${Mr}?`,
    `${moles} mol`, wrongsAround(moles,moles*0.5,3,0.05).map(w=>parseFloat(Math.abs(w).toFixed(3))+' mol'), `moles = mass ÷ Mr = ${mass} ÷ ${Mr} = ${moles} mol.`
  )},
  ()=>makeQ('What is the Avogadro constant?','6.02 × 10²³ — the number of particles in one mole.',
    ['6.02 × 10⁻²³','3.0 × 10⁸','1.67 × 10⁻²⁷'],
    'One mole of any substance contains 6.02 × 10²³ particles (atoms, molecules or ions).'),
  ()=>{const actual=rndF(5,25,1),theoretical=rndF(actual,35,1);const pct=parseFloat((actual/theoretical*100).toFixed(1));return makeQ(
    `The theoretical yield of a reaction is ${theoretical} g. The actual yield obtained is ${actual} g. What is the percentage yield?`,
    `${pct}%`, wrongsAround(pct,pct*0.4,3,5).map(w=>parseFloat(Math.abs(w).toFixed(1))+'%'), `% yield = (actual/theoretical) × 100 = (${actual}/${theoretical}) × 100 = ${pct}%.`
  )},
  ()=>makeQ('What does atom economy measure?','The proportion of reactant atoms that end up in the desired product (by mass).',
    ['The percentage yield of a reaction','The rate of a chemical reaction','The purity of a product'],
    'Atom economy = (Mr of desired product ÷ sum of Mr of all reactants) × 100. High atom economy = less waste.'),
  ()=>{const conc=rndF(0.1,3,2),vol=rndF(0.1,1,2);const moles=parseFloat((conc*vol).toFixed(3));return makeQ(
    `A solution has concentration ${conc} mol/dm³ and volume ${vol} dm³. How many moles of solute are present?`,
    `${moles} mol`, wrongsAround(moles,moles*0.5,3,0.05).map(w=>parseFloat(Math.abs(w).toFixed(3))+' mol'), `moles = concentration × volume = ${conc} × ${vol} = ${moles} mol.`
  )},
],

chemistry_chem_changes: [
  ()=>makeQ('In which order does the reactivity series list metals?','Potassium > Sodium > Lithium > Calcium > Magnesium > Aluminium > Zinc > Iron > Copper',
    ['Copper > Iron > Zinc > Aluminium > Magnesium > Calcium > Lithium > Sodium > Potassium','Iron > Copper > Zinc > Sodium > Potassium','Calcium > Copper > Sodium > Potassium > Iron'],
    'Mnemonic: Please Stop Letting Children Make A Zinc Iron Copper mess! (K, Na, Li, Ca, Mg, Al, Zn, Fe, Cu)'),
  ()=>makeQ('What is oxidation in terms of electrons?','Loss of electrons.',
    ['Gain of electrons','Gain of oxygen and electrons','Loss of hydrogen only'],
    'OIL RIG: Oxidation Is Loss, Reduction Is Gain (of electrons). In terms of oxygen: oxidation = gain of oxygen.'),
  ()=>makeQ('What type of reaction occurs when an acid reacts with a metal carbonate?','Neutralisation — producing a salt, water and carbon dioxide.',
    ['Combustion','Decomposition only','Displacement'],
    'Acid + metal carbonate → salt + water + CO₂. E.g. HCl + CaCO₃ → CaCl₂ + H₂O + CO₂.'),
  ()=>makeQ('What is the pH of a neutral solution?','7.',
    ['0','14','1'],
    'pH scale: 0–6 = acidic, 7 = neutral, 8–14 = alkaline. pH = −log[H⁺].'),
  ()=>makeQ('Which indicator turns red in acid and blue in alkali?','Litmus.',
    ['Phenolphthalein','Methyl orange','Universal indicator'],
    'Litmus: red in acid, blue in alkali. Universal indicator gives a range of colours for more precise pH.'),
  ()=>makeQ('What is a displacement reaction?','A more reactive metal displaces a less reactive metal from its compound.',
    ['A metal reacting with water','An acid reacting with an alkali','A metal losing electrons to oxygen'],
    'E.g. Fe + CuSO₄ → FeSO₄ + Cu. Iron is more reactive than copper, so it displaces copper from its salt.'),
],

chemistry_electrolysis: [
  ()=>makeQ('What is electrolysis?','The breakdown of an ionic compound (when molten or dissolved) using electricity.',
    ['The spontaneous decomposition of a compound','The reaction of metals with acid','The formation of ionic bonds'],
    'Electrolysis: ionic compound → electrodes → ions discharged. Needs free-moving ions (molten or in solution).'),
  ()=>makeQ('At which electrode does reduction take place during electrolysis?','Cathode (negative electrode).',
    ['Anode (positive electrode)','Both electrodes equally','Neither — it happens in solution'],
    'CATS: Cathode = negative, Anode = positive. Cations (+) attracted to cathode → gain electrons → reduced.'),
  ()=>makeQ('What is produced at the cathode during the electrolysis of copper sulfate solution using copper electrodes?','Copper metal is deposited.',
    ['Oxygen gas','Hydrogen gas','Sulfate ions'],
    'Cu²⁺ ions gain 2 electrons at cathode → Cu. The copper anode dissolves to replenish Cu²⁺ ions. Used for copper purification.'),
  ()=>makeQ('What is produced at the ANODE during electrolysis of dilute sulfuric acid?','Oxygen gas.',
    ['Hydrogen gas','Chlorine gas','Sulfur dioxide'],
    'At the anode (positive), OH⁻ ions are discharged: 4OH⁻ → 2H₂O + O₂ + 4e⁻. Hydrogen forms at cathode.'),
  ()=>makeQ('The electrolysis of brine produces:','Chlorine (at anode), hydrogen (at cathode), and sodium hydroxide solution.',
    ['Sodium metal, chlorine, and water','Oxygen, hydrogen, and sodium','Only chlorine and hydrogen'],
    'Brine = NaCl(aq). Products: Cl₂ (anode), H₂ (cathode), NaOH (remains in solution). All are industrially important.'),
],

chemistry_energy_chem: [
  ()=>makeQ('What is an exothermic reaction?','A reaction that releases energy to the surroundings, causing the temperature to rise.',
    ['A reaction that absorbs energy from the surroundings','A reaction producing only gases','A reaction requiring a catalyst'],
    'Exothermic: products have LESS energy than reactants. ΔH is negative. Examples: combustion, neutralisation, oxidation.'),
  ()=>makeQ('What is an endothermic reaction?','A reaction that absorbs energy from the surroundings, causing the temperature to fall.',
    ['A reaction that releases heat','A reaction that only occurs at high temperature','A reaction with no energy change'],
    'Endothermic: products have MORE energy than reactants. ΔH is positive. Examples: thermal decomposition, photosynthesis.'),
  ()=>{const BE_r=rnd(300,800),BE_p=rnd(100,BE_r-10);const dH=BE_r-BE_p;return makeQ(
    `In a reaction, the energy needed to break bonds in reactants is ${BE_r} kJ/mol and the energy released when bonds form in products is ${BE_p} kJ/mol. What is the overall energy change?`,
    `${dH} kJ/mol released (exothermic)`, [`${BE_p-BE_r} kJ/mol absorbed (endothermic)`,`${BE_r+BE_p} kJ/mol released`,`${BE_r} kJ/mol absorbed`], `ΔH = energy in − energy out = ${BE_r} − ${BE_p} = +${dH} kJ/mol. Energy IN > energy OUT → exothermic.`
  )},
  ()=>makeQ('Which type of cell converts chemical energy directly into electrical energy?','A fuel cell (e.g. hydrogen fuel cell).',
    ['A solar cell','A nuclear reactor','An electrolytic cell'],
    'Hydrogen fuel cell: H₂ + O₂ → H₂O + electricity. Only by-product is water — very clean.'),
  ()=>makeQ('In a reaction profile diagram, activation energy is:','The energy needed to start the reaction — the difference between reactants and the peak (transition state).',
    ['The overall energy change of the reaction','The energy released by the products','The energy of the reactants alone'],
    'Activation energy = minimum energy needed for particles to react. A catalyst lowers activation energy.'),
],

chemistry_rates: [
  ()=>makeQ('Which factor does NOT increase the rate of reaction?','Decreasing the concentration of reactants.',
    ['Increasing temperature','Adding a catalyst','Increasing surface area (smaller particles)'],
    'Factors that increase rate: temperature ↑ (more kinetic energy), concentration ↑ (more collisions), surface area ↑, catalyst (alternative pathway).'),
  ()=>makeQ('How does a catalyst increase the rate of reaction?','It provides an alternative reaction pathway with lower activation energy.',
    ['It increases the temperature of the reaction','It is permanently used up in the reaction','It increases the concentration of reactants'],
    'Catalysts are not consumed — they are unchanged at the end. They lower activation energy → more particles have enough energy to react.'),
  ()=>makeQ('What does collision theory state?','Reactions occur when particles collide with sufficient energy (≥ activation energy) and correct orientation.',
    ['All collisions result in a reaction','Particles must be stationary to react','Reactions require heat to start'],
    'Collision theory: particles must meet, have enough energy (activation energy), and the right orientation. More frequent/energetic collisions = faster rate.'),
  ()=>makeQ('In a reversible reaction at dynamic equilibrium:','The rate of the forward reaction equals the rate of the reverse reaction, and concentrations remain constant.',
    ['The reaction has stopped completely','Only products are present','The concentrations of all species are equal'],
    'Dynamic equilibrium: both forward and reverse reactions continue at equal rates → no net change in concentrations.'),
  ()=>makeQ('Le Chatelier\'s Principle states:','If conditions of an equilibrium are changed, the equilibrium shifts to oppose that change.',
    ['Increasing temperature always shifts equilibrium right','All equilibria favour reactants','Adding a catalyst shifts equilibrium to the right'],
    'Le Chatelier\'s: pressure ↑ → shift to fewer gas molecules. Temperature ↑ → shift endothermic direction. Catalyst: no shift, just faster equilibrium.'),
  ()=>makeQ('What effect does increasing pressure have on the equilibrium: N₂(g) + 3H₂(g) ⇌ 2NH₃(g)?','Shifts right (toward fewer moles of gas) — increases yield of NH₃.',
    ['Shifts left','No effect on equilibrium position','Increases rate only, not equilibrium position'],
    'Left side: 1+3 = 4 moles of gas. Right: 2 moles. Increasing pressure favours the side with fewer gas molecules → shifts right.'),
],

chemistry_organic: [
  ()=>makeQ('What is the general formula of alkanes?','CₙH₂ₙ₊₂.',
    ['CₙH₂ₙ','CₙHₙ','CₙH₂ₙ₋₂'],
    'Alkanes are saturated hydrocarbons with only C–C single bonds. Methane CH₄, Ethane C₂H₆, Propane C₃H₈.'),
  ()=>makeQ('What is the general formula of alkenes?','CₙH₂ₙ.',
    ['CₙH₂ₙ₊₂','CₙH₂ₙ₋₂','CₙHₙ'],
    'Alkenes are unsaturated hydrocarbons with at least one C=C double bond. Ethene C₂H₄, Propene C₃H₆.'),
  ()=>makeQ('How can you distinguish between an alkane and an alkene?','Add bromine water — an alkene decolourises it (orange to colourless); an alkane does not.',
    ['Burn them — alkenes produce a smokier flame','Add universal indicator','Test with litmus paper'],
    'Alkenes react with bromine water by addition across the C=C double bond, removing the orange bromine colour.'),
  ()=>makeQ('What is cracking in the context of crude oil?','Breaking large hydrocarbon molecules into smaller, more useful ones using heat and a catalyst.',
    ['Dissolving oil in water','Separating crude oil by boiling point','Burning hydrocarbons completely'],
    'Cracking converts long-chain alkanes into alkenes + shorter alkanes. Produces fuels and monomers for plastics.'),
  ()=>makeQ('What type of reaction is polymerisation?','Addition polymerisation — many small alkene monomers join to form one long polymer chain.',
    ['Combustion','Substitution','Decomposition'],
    'Addition polymerisation: n(CH₂=CH₂) → (-CH₂-CH₂-)ₙ (poly(ethene)). The C=C double bond opens to link monomers.'),
  ()=>makeQ('Ethanol can be produced by:','Fermentation of glucose using yeast (in anaerobic conditions) OR hydration of ethene.',
    ['Burning alkanes in oxygen','Electrolysis of ethane solution','Thermal decomposition of methane'],
    'Fermentation: C₆H₁₂O₆ → 2C₂H₅OH + 2CO₂. Hydration: C₂H₄ + H₂O → C₂H₅OH (catalyst: phosphoric acid, high T).'),
],

chemistry_analysis: [
  ()=>makeQ('A substance gives an orange/red flame in a flame test. Which ion is present?','Calcium (Ca²⁺).',
    ['Sodium (Na⁺)','Potassium (K⁺)','Lithium (Li⁺)'],
    'Flame test colours: Li = red, Na = yellow/orange, K = lilac/purple, Ca = orange-red, Ba = green.'),
  ()=>makeQ('How do you test for CO₂ gas?','Bubble through limewater (calcium hydroxide solution) — it turns milky/cloudy if CO₂ is present.',
    ['Use damp red litmus paper','Apply a lit splint — it pops','Use anhydrous copper sulfate'],
    'CO₂ + Ca(OH)₂ → CaCO₃ (white precipitate) + H₂O. The cloudiness is caused by the calcium carbonate precipitate.'),
  ()=>makeQ('What reagent is used to test for chloride ions?','Silver nitrate solution (acidified with nitric acid) — gives a white precipitate.',
    ['Acidified potassium dichromate','Barium chloride solution','Universal indicator'],
    'Cl⁻ + Ag⁺ → AgCl (white ppt). Br⁻ → AgBr (cream). I⁻ → AgI (yellow). Remember the colours!'),
  ()=>makeQ('What is the purpose of chromatography?','To separate and identify mixtures of substances based on how far they travel through a medium.',
    ['To measure the pH of a substance','To test for metal ions','To measure the mass of a substance'],
    'Rf = distance moved by substance ÷ distance moved by solvent. Same Rf = same substance.'),
  ()=>makeQ('A student tests an unknown solution with sodium hydroxide solution and gets a blue precipitate. Which ion is present?','Cu²⁺ (copper ions).',
    ['Fe²⁺ (iron(II) ions)','Fe³⁺ (iron(III) ions)','NH₄⁺ (ammonium ions)'],
    'NaOH + Cu²⁺ → Cu(OH)₂ (blue ppt). Fe²⁺ → green ppt. Fe³⁺ → brown ppt. Mg²⁺/Al³⁺ → white ppt.'),
],

};

// ═══════════════════════════════════════════════════════════════
// NOTES DATA  (comprehensive, AQA spec-aligned)
// ═══════════════════════════════════════════════════════════════
const NOTES = {

physics_forces: {
  title:'Forces & Motion',
  intro:'Forces cause objects to start moving, stop, speed up, slow down or change direction. This topic covers the AQA required content for motion, Newton\'s laws, momentum and stopping distance.',
  sections:[
    { h:'Key Equations', content:`
      <div class="formula-box">F = ma &nbsp; (resultant force = mass × acceleration)</div>
      <div class="formula-box">W = mg &nbsp; (weight = mass × gravitational field strength)</div>
      <div class="formula-box">p = mv &nbsp; (momentum = mass × velocity)</div>
      <div class="formula-box">v = u + at &nbsp; | &nbsp; v² = u² + 2as &nbsp; | &nbsp; s = ut + ½at²</div>
      <div class="formula-box">speed = distance ÷ time</div>
    `},
    { h:"Newton's Three Laws", content:`
      <ul>
        <li><strong>1st Law:</strong> An object remains stationary or moves at constant velocity unless a resultant force acts on it (inertia).</li>
        <li><strong>2nd Law:</strong> The acceleration of an object is directly proportional to the resultant force and inversely proportional to its mass: F = ma.</li>
        <li><strong>3rd Law:</strong> For every action force there is an equal and opposite reaction force on a DIFFERENT object.</li>
      </ul>
      <div class="exam-tip">Newton's 3rd law pairs always act on different objects, are the same type of force, equal in size and opposite in direction.</div>
    `},
    { h:'Scalars and Vectors', content:`
      <div class="key-grid">
        <div class="key-card"><div class="kc-label">Scalar (magnitude only)</div><div class="kc-val">Speed, distance, mass, time, energy, temperature</div></div>
        <div class="key-card"><div class="kc-label">Vector (magnitude + direction)</div><div class="kc-val">Velocity, displacement, force, acceleration, momentum, weight</div></div>
      </div>
    `},
    { h:'Stopping Distance', content:`
      <p>Stopping distance = <strong>thinking distance</strong> + <strong>braking distance</strong></p>
      <ul>
        <li><strong>Thinking distance</strong> depends on: reaction time, speed. Reaction time affected by: alcohol, drugs, tiredness, distractions.</li>
        <li><strong>Braking distance</strong> depends on: speed, road condition (ice, wet), tyre condition, brake condition, vehicle mass.</li>
      </ul>
      <div class="exam-tip">Braking distance is proportional to v² — doubling speed quadruples braking distance!</div>
    `},
    { h:'Weight vs Mass', content:`
      <ul>
        <li><strong>Mass</strong>: the amount of matter in an object — measured in kg — constant everywhere.</li>
        <li><strong>Weight</strong>: the gravitational force on an object — measured in Newtons — varies with location.</li>
        <li>On Earth g = 10 N/kg. On the Moon g ≈ 1.6 N/kg.</li>
      </ul>
    `},
    { h:'Required Practical', content:`<div class="required-practical">Investigate the effect of force on acceleration using a trolley, ticker tape and pulley system. Plot F vs a to verify F=ma.</div>`},
  ]
},

physics_energy: {
  title:'Energy Stores & Transfers',
  intro:'Energy cannot be created or destroyed — only transferred between stores. AQA requires you to identify energy stores, describe pathways and calculate efficiency.',
  sections:[
    { h:'Energy Stores', content:`
      <div class="key-grid">
        <div class="key-card"><div class="kc-label">Kinetic</div><div class="kc-val">Moving objects. KE = ½mv²</div></div>
        <div class="key-card"><div class="kc-label">Gravitational Potential</div><div class="kc-val">Raised objects. GPE = mgh</div></div>
        <div class="key-card"><div class="kc-label">Elastic Potential</div><div class="kc-val">Compressed/stretched springs. E = ½ke²</div></div>
        <div class="key-card"><div class="kc-label">Chemical</div><div class="kc-val">Fuel, food, batteries</div></div>
        <div class="key-card"><div class="kc-label">Thermal</div><div class="kc-val">Hot objects</div></div>
        <div class="key-card"><div class="kc-label">Nuclear</div><div class="kc-val">Radioactive nuclei</div></div>
        <div class="key-card"><div class="kc-label">Magnetic</div><div class="kc-val">Magnets attracting each other</div></div>
        <div class="key-card"><div class="kc-label">Electrostatic</div><div class="kc-val">Charged particles</div></div>
      </div>
    `},
    { h:'Key Equations', content:`
      <div class="formula-box">KE = ½mv²</div>
      <div class="formula-box">GPE = mgh</div>
      <div class="formula-box">Power = Energy ÷ Time (P = E/t) &nbsp; [Watts, W]</div>
      <div class="formula-box">Efficiency = useful output ÷ total input (× 100%)</div>
      <div class="formula-box">Q = mcΔT &nbsp; (thermal energy = mass × specific heat capacity × ΔT)</div>
    `},
    { h:'Energy Transfer Pathways', content:`
      <ul>
        <li><strong>Mechanical work:</strong> a force moves an object</li>
        <li><strong>Electrical work:</strong> charge moves through a potential difference</li>
        <li><strong>Heating:</strong> by conduction, convection or radiation</li>
        <li><strong>Radiation:</strong> EM waves (e.g. light, infrared)</li>
      </ul>
      <p>Wasted energy is usually dissipated to thermal stores in the surroundings. It's not "lost" — just harder to use.</p>
    `},
    { h:'Reducing Energy Loss in Buildings', content:`
      <ul>
        <li><strong>Loft insulation:</strong> fibres trap air, reducing convection</li>
        <li><strong>Cavity wall insulation:</strong> foam fills wall gap, reducing convection</li>
        <li><strong>Double glazing:</strong> air gap reduces conduction</li>
        <li><strong>Draught-proofing:</strong> seals gaps reducing convective loss</li>
        <li><strong>Reflective foil:</strong> behind radiators reflects heat back into room</li>
      </ul>
      <div class="exam-tip">Payback time = cost of measure ÷ annual saving. A cheaper measure with short payback time may be better even if it saves less energy.</div>
    `},
  ]
},

biology_cells: {
  title:'Cell Biology',
  intro:'All living organisms are made of cells. This topic covers cell structure, microscopy, cell division and transport processes.',
  sections:[
    { h:'Animal vs Plant vs Bacterial Cells', content:`
      <table class="notes-table">
        <tr><th>Feature</th><th>Animal</th><th>Plant</th><th>Bacterial</th></tr>
        <tr><td>Nucleus</td><td>✓</td><td>✓</td><td>✗ (no membrane)</td></tr>
        <tr><td>Cell membrane</td><td>✓</td><td>✓</td><td>✓</td></tr>
        <tr><td>Cytoplasm</td><td>✓</td><td>✓</td><td>✓</td></tr>
        <tr><td>Mitochondria</td><td>✓</td><td>✓</td><td>✗</td></tr>
        <tr><td>Ribosomes</td><td>✓</td><td>✓</td><td>✓ (smaller)</td></tr>
        <tr><td>Cell wall (cellulose)</td><td>✗</td><td>✓</td><td>✓ (different material)</td></tr>
        <tr><td>Chloroplasts</td><td>✗</td><td>✓</td><td>✗</td></tr>
        <tr><td>Permanent vacuole</td><td>✗</td><td>✓</td><td>✗</td></tr>
      </table>
    `},
    { h:'Microscopy & Magnification', content:`
      <div class="formula-box">Image size = Magnification × Actual size</div>
      <div class="formula-box">Magnification = Image size ÷ Actual size</div>
      <ul>
        <li><strong>Light microscopes:</strong> max magnification ~×1500, resolution ~200 nm. Can view living cells.</li>
        <li><strong>Electron microscopes:</strong> magnification ×1,000,000+, resolution ~0.2 nm. Shows organelles in detail. Must be dead.</li>
      </ul>
    `},
    { h:'Transport Processes', content:`
      <table class="notes-table">
        <tr><th>Process</th><th>Direction</th><th>Energy?</th><th>What moves?</th></tr>
        <tr><td>Diffusion</td><td>High → low concentration</td><td>No (passive)</td><td>Any small molecule</td></tr>
        <tr><td>Osmosis</td><td>High → low water potential</td><td>No (passive)</td><td>Water only</td></tr>
        <tr><td>Active transport</td><td>Low → high (against gradient)</td><td>Yes (ATP)</td><td>Glucose, mineral ions</td></tr>
      </table>
      <div class="exam-tip">Factors increasing rate of diffusion: larger surface area, steeper concentration gradient, higher temperature, shorter distance.</div>
    `},
    { h:'Cell Division', content:`
      <ul>
        <li><strong>Mitosis:</strong> produces 2 genetically IDENTICAL daughter cells (diploid). Used for: growth, repair, asexual reproduction.</li>
        <li><strong>Meiosis:</strong> produces 4 genetically UNIQUE daughter cells (haploid). Used for: production of gametes.</li>
        <li><strong>Meiosis introduces variation</strong> by independent assortment and crossing over during prophase I.</li>
      </ul>
    `},
    { h:'Required Practical', content:`<div class="required-practical">Use a light microscope to observe and draw cells. Prepare slides using iodine (plant cells) or methylene blue (animal cells).</div>`},
  ]
},

biology_infection: {
  title:'Infection & Response',
  intro:'Pathogens are organisms that cause infectious disease. The body has multiple lines of defence. Understanding vaccines, antibiotics and the immune system is essential.',
  sections:[
    { h:'Types of Pathogen', content:`
      <div class="key-grid">
        <div class="key-card"><div class="kc-label">Bacteria</div><div class="kc-val">Salmonella, tuberculosis, gonorrhoea. Treated with antibiotics.</div></div>
        <div class="key-card"><div class="kc-label">Viruses</div><div class="kc-val">Influenza, HIV, measles. No antibiotic cure — vaccines or antivirals.</div></div>
        <div class="key-card"><div class="kc-label">Fungi</div><div class="kc-val">Rose black spot, athlete's foot. Treated with antifungals.</div></div>
        <div class="key-card"><div class="kc-label">Protists</div><div class="kc-val">Malaria (Plasmodium via mosquito). Treated with antimalarials.</div></div>
      </div>
    `},
    { h:'The Immune Response', content:`
      <ul>
        <li><strong>Non-specific defences:</strong> skin (physical barrier), mucus + cilia (trap pathogens), stomach acid (kills microbes).</li>
        <li><strong>Phagocytosis:</strong> white blood cells (phagocytes) engulf and destroy pathogens.</li>
        <li><strong>Antibodies:</strong> produced by B-lymphocytes. Specific to each antigen. Mark pathogens for destruction.</li>
        <li><strong>Memory cells:</strong> remain after infection — cause faster, larger response on re-exposure (immunity).</li>
      </ul>
    `},
    { h:'Vaccines', content:`
      <ul>
        <li>Introduce dead/weakened/fragment of pathogen → no disease, but immune response triggered.</li>
        <li>Memory cells formed → long-lasting protection.</li>
        <li><strong>Herd immunity:</strong> when enough of the population is vaccinated, infection cannot spread easily to unvaccinated individuals.</li>
      </ul>
      <div class="exam-tip">Vaccines give ACTIVE immunity (body makes its own antibodies). Antibody injections give PASSIVE immunity (no memory cells formed — temporary).</div>
    `},
    { h:'Antibiotics & Resistance', content:`
      <ul>
        <li>Antibiotics kill bacteria (or stop reproduction) — NOT viruses.</li>
        <li><strong>Antibiotic resistance:</strong> bacteria with random mutations that resist antibiotics survive, reproduce and pass on resistant genes.</li>
        <li>MRSA (Methicillin-resistant Staphylococcus aureus) is a major concern in hospitals.</li>
        <li>To reduce resistance: complete antibiotic courses, don't use for viral infections, reduce agricultural use.</li>
      </ul>
    `},
  ]
},

biology_bioenergetics: {
  title:'Bioenergetics',
  intro:'Bioenergetics covers how organisms obtain and use energy — through photosynthesis and respiration.',
  sections:[
    { h:'Photosynthesis', content:`
      <div class="formula-box">6CO₂ + 6H₂O → C₆H₁₂O₆ + 6O₂ &nbsp; (requires light energy)</div>
      <ul>
        <li>Occurs in <strong>chloroplasts</strong> (contain chlorophyll which absorbs light).</li>
        <li><strong>Limiting factors:</strong> light intensity, CO₂ concentration, temperature, water availability.</li>
        <li>At the <strong>compensation point</strong>, rate of photosynthesis = rate of respiration — net gas exchange is zero.</li>
      </ul>
      <div class="exam-tip">On a rate vs light intensity graph, the plateau is where CO₂ or temperature has become limiting — not light.</div>
    `},
    { h:'Aerobic vs Anaerobic Respiration', content:`
      <table class="notes-table">
        <tr><th></th><th>Aerobic</th><th>Anaerobic (animals)</th><th>Anaerobic (yeast)</th></tr>
        <tr><td>Reactants</td><td>Glucose + O₂</td><td>Glucose</td><td>Glucose</td></tr>
        <tr><td>Products</td><td>CO₂ + H₂O + ATP</td><td>Lactic acid + ATP</td><td>Ethanol + CO₂ + ATP</td></tr>
        <tr><td>Location</td><td>Mitochondria</td><td>Cytoplasm</td><td>Cytoplasm</td></tr>
        <tr><td>ATP yield</td><td>~38 ATP</td><td>2 ATP</td><td>2 ATP</td></tr>
      </table>
    `},
    { h:'Exercise & Oxygen Debt', content:`
      <ul>
        <li>During vigorous exercise, insufficient O₂ → anaerobic respiration → lactic acid build-up.</li>
        <li>Lactic acid causes muscle fatigue and pain.</li>
        <li><strong>Oxygen debt:</strong> extra O₂ needed after exercise to convert lactic acid → glucose in the liver.</li>
        <li>Heart rate, breathing rate and tidal volume all increase during exercise to deliver more O₂.</li>
      </ul>
    `},
  ]
},

biology_homeostasis: {
  title:'Homeostasis & Response',
  intro:'Homeostasis maintains a stable internal environment. The nervous and endocrine systems coordinate responses.',
  sections:[
    { h:'The Nervous System', content:`
      <ul>
        <li><strong>CNS:</strong> brain + spinal cord. Processes information and coordinates response.</li>
        <li><strong>Sensory neurones:</strong> carry impulses from receptors to CNS.</li>
        <li><strong>Motor neurones:</strong> carry impulses from CNS to effectors (muscles/glands).</li>
        <li><strong>Reflex arc:</strong> stimulus → receptor → sensory neurone → relay neurone (in spinal cord) → motor neurone → effector. Fast, automatic, bypasses brain.</li>
      </ul>
    `},
    { h:'Hormonal Control', content:`
      <div class="key-grid">
        <div class="key-card"><div class="kc-label">Insulin (pancreas β cells)</div><div class="kc-val">↑ glucose → insulin released → cells absorb glucose + liver converts glucose to glycogen</div></div>
        <div class="key-card"><div class="kc-label">Glucagon (pancreas α cells)</div><div class="kc-val">↓ glucose → glucagon released → liver converts glycogen → glucose (glycogenolysis)</div></div>
        <div class="key-card"><div class="kc-label">ADH (pituitary gland)</div><div class="kc-val">Dehydrated → ADH released → kidney collects more water → concentrated urine</div></div>
        <div class="key-card"><div class="kc-label">Oestrogen / Progesterone</div><div class="kc-val">Control the menstrual cycle; used in contraceptive pill and fertility treatment (FSH, LH)</div></div>
      </div>
    `},
    { h:'Thermoregulation', content:`
      <table class="notes-table">
        <tr><th>Too hot</th><th>Too cold</th></tr>
        <tr><td>Vasodilation (skin vessels widen — more heat loss by radiation)</td><td>Vasoconstriction (vessels narrow — less heat lost)</td></tr>
        <tr><td>Sweating (evaporation cools skin)</td><td>Shivering (muscle contractions generate heat)</td></tr>
        <tr><td>Erector muscles relax (hair lies flat — less insulation)</td><td>Erector muscles contract (hair stands up — traps air)</td></tr>
      </table>
    `},
    { h:'Diabetes', content:`
      <ul>
        <li><strong>Type 1:</strong> autoimmune — pancreas can't produce insulin. Managed with insulin injections and blood glucose monitoring.</li>
        <li><strong>Type 2:</strong> cells don't respond to insulin (insulin resistance). Linked to obesity. Managed with diet, exercise, medication.</li>
      </ul>
    `},
  ]
},

biology_inheritance: {
  title:'Inheritance & Variation',
  intro:'Genes are sections of DNA that code for proteins. Understanding inheritance requires knowledge of alleles, Punnett squares and genetic diseases.',
  sections:[
    { h:'Key Definitions', content:`
      <div class="key-grid">
        <div class="key-card"><div class="kc-label">Gene</div><div class="kc-val">A section of DNA coding for a specific protein</div></div>
        <div class="key-card"><div class="kc-label">Allele</div><div class="kc-val">A different version of a gene</div></div>
        <div class="key-card"><div class="kc-label">Genotype</div><div class="kc-val">The alleles an organism has (e.g. Bb)</div></div>
        <div class="key-card"><div class="kc-label">Phenotype</div><div class="kc-val">The observable characteristics</div></div>
        <div class="key-card"><div class="kc-label">Dominant</div><div class="kc-val">Expressed whenever present (e.g. B in Bb)</div></div>
        <div class="key-card"><div class="kc-label">Recessive</div><div class="kc-val">Only expressed when homozygous (bb)</div></div>
        <div class="key-card"><div class="kc-label">Homozygous</div><div class="kc-val">Both alleles the same (BB or bb)</div></div>
        <div class="key-card"><div class="kc-label">Heterozygous</div><div class="kc-val">Two different alleles (Bb)</div></div>
      </div>
    `},
    { h:'Genetic Diseases', content:`
      <ul>
        <li><strong>Cystic fibrosis:</strong> autosomal recessive (ff). Thick mucus in lungs and digestive system.</li>
        <li><strong>Polydactyly:</strong> autosomal dominant (D). Extra fingers/toes.</li>
        <li><strong>Sickle cell anaemia:</strong> autosomal recessive. Red blood cells are sickle-shaped — can't carry O₂ efficiently.</li>
      </ul>
      <div class="exam-tip">Carrier: a person with one dominant and one recessive allele (Ff) who does not show the recessive disease but can pass it to offspring.</div>
    `},
    { h:'Sex Determination', content:`
      <p>Humans have 23 pairs of chromosomes. The 23rd pair are sex chromosomes: XX (female) or XY (male).</p>
      <p>The father determines the sex of the child — he passes either X or Y. Mother always passes X.</p>
      <div class="exam-tip">In a Punnett square crossing XX × XY: offspring are 50% XX (female) and 50% XY (male).</div>
    `},
    { h:'DNA & Protein Synthesis', content:`
      <ul>
        <li>DNA is a double helix made of nucleotides (sugar + phosphate + base).</li>
        <li>Base pairs: A-T and C-G.</li>
        <li><strong>Transcription:</strong> DNA → mRNA in the nucleus.</li>
        <li><strong>Translation:</strong> mRNA → protein at ribosomes.</li>
        <li>Every 3 bases (codon) codes for one amino acid.</li>
      </ul>
    `},
  ]
},

biology_ecology: {
  title:'Ecology & Biodiversity',
  intro:'Ecology studies how organisms interact with each other and their environment. Understanding ecosystems, biodiversity and human impact is essential.',
  sections:[
    { h:'Key Terms', content:`
      <div class="key-grid">
        <div class="key-card"><div class="kc-label">Ecosystem</div><div class="kc-val">All organisms in an area + their non-living environment</div></div>
        <div class="key-card"><div class="kc-label">Community</div><div class="kc-val">All organisms of different species living in an area</div></div>
        <div class="key-card"><div class="kc-label">Population</div><div class="kc-val">All organisms of the same species in an area</div></div>
        <div class="key-card"><div class="kc-label">Habitat</div><div class="kc-val">The place where an organism lives</div></div>
        <div class="key-card"><div class="kc-label">Biodiversity</div><div class="kc-val">Variety of species AND abundance of individuals</div></div>
      </div>
    `},
    { h:'Energy Flow in Food Chains', content:`
      <ul>
        <li>Food chains: Producer → Primary consumer → Secondary consumer → Tertiary consumer.</li>
        <li>Only ~10% of energy is transferred between trophic levels.</li>
        <li>90% is lost as: heat from respiration, movement, waste products (faeces, urine).</li>
        <li>This limits the length of food chains (usually 4–5 levels max).</li>
      </ul>
      <div class="formula-box">Biomass transferred = 10% of previous trophic level</div>
    `},
    { h:'The Carbon Cycle', content:`
      <ul>
        <li><strong>CO₂ removed from atmosphere:</strong> photosynthesis (plants), dissolved in oceans.</li>
        <li><strong>CO₂ returned to atmosphere:</strong> respiration (all organisms), combustion (burning fossil fuels), decomposition.</li>
        <li>Decomposers (bacteria & fungi) break down dead material, returning carbon as CO₂.</li>
      </ul>
    `},
    { h:'Required Practical — Sampling', content:`
      <div class="required-practical">Use quadrats (random sampling) to estimate population size. Use transects to study how species change across a habitat. Apply the capture-recapture method for mobile organisms: Population = (M1 × M2) ÷ R.</div>
    `},
    { h:'Biodiversity & Conservation', content:`
      <ul>
        <li>Threats to biodiversity: habitat destruction, pollution, invasive species, climate change, overexploitation.</li>
        <li>Conservation methods: protected areas, captive breeding, seed banks, legal protection, international agreements.</li>
        <li>High biodiversity = more stable ecosystems (more food web connections = more resilience to change).</li>
      </ul>
    `},
  ]
},

chemistry_atomic_chem: {
  title:'Atomic Structure & the Periodic Table',
  intro:'Understanding atomic structure is the foundation of all chemistry. The periodic table organises elements by atomic number and reveals patterns in properties.',
  sections:[
    { h:'Subatomic Particles', content:`
      <table class="notes-table">
        <tr><th>Particle</th><th>Relative mass</th><th>Relative charge</th><th>Location</th></tr>
        <tr><td>Proton</td><td>1</td><td>+1</td><td>Nucleus</td></tr>
        <tr><td>Neutron</td><td>1</td><td>0</td><td>Nucleus</td></tr>
        <tr><td>Electron</td><td>~1/1836</td><td>−1</td><td>Shells (orbitals)</td></tr>
      </table>
      <div class="formula-box">Mass number (A) = protons + neutrons &nbsp;|&nbsp; Atomic number (Z) = protons</div>
    `},
    { h:'Isotopes & Relative Atomic Mass', content:`
      <ul>
        <li><strong>Isotopes:</strong> same element (same Z), different mass number (different number of neutrons).</li>
        <li>Example: Carbon-12 (6p, 6n) and Carbon-14 (6p, 8n).</li>
        <li><strong>Relative atomic mass (Ar):</strong> weighted average of all isotopes. E.g. Chlorine has Ar ≈ 35.5 due to Cl-35 and Cl-37.</li>
      </ul>
    `},
    { h:'Electronic Configuration', content:`
      <ul>
        <li>Shell 1: max 2 electrons. Shell 2: max 8. Shell 3: max 8.</li>
        <li>Example: Na (11 electrons) → 2, 8, 1</li>
        <li>Outer electrons determine chemical properties and group number.</li>
        <li>Period number = number of electron shells.</li>
      </ul>
      <div class="exam-tip">Elements in the same GROUP have the same number of outer shell electrons → similar chemical properties.</div>
    `},
    { h:'Development of the Atomic Model', content:`
      <ul>
        <li><strong>Dalton:</strong> solid indivisible spheres.</li>
        <li><strong>Thomson (1897):</strong> plum pudding — electrons embedded in positive "dough".</li>
        <li><strong>Rutherford (1909):</strong> gold foil experiment — most mass in tiny positive nucleus.</li>
        <li><strong>Bohr (1913):</strong> electrons in defined shells/orbits.</li>
        <li><strong>Chadwick (1932):</strong> discovered the neutron.</li>
      </ul>
    `},
    { h:'The Periodic Table', content:`
      <ul>
        <li>Elements arranged in order of <strong>increasing atomic number</strong>.</li>
        <li><strong>Periods:</strong> horizontal rows — number of shells = period number.</li>
        <li><strong>Groups:</strong> vertical columns — outer electrons = group number (for groups 1–7).</li>
        <li>Group 1 (alkali metals): very reactive, one outer electron, react vigorously with water.</li>
        <li>Group 7 (halogens): reactive non-metals, gain 1 electron to complete outer shell.</li>
        <li>Group 0 (noble gases): full outer shell → very unreactive.</li>
        <li>Transition metals: high melting points, often coloured compounds, multiple oxidation states, good catalysts.</li>
      </ul>
    `},
  ]
},

chemistry_bonding: {
  title:'Bonding, Structure & Properties',
  intro:'The type of bonding and structure of a substance determines its physical and chemical properties.',
  sections:[
    { h:'Types of Bonding', content:`
      <table class="notes-table">
        <tr><th>Type</th><th>Between</th><th>What happens</th></tr>
        <tr><td>Ionic</td><td>Metal + non-metal</td><td>Electrons transferred → oppositely charged ions attracted</td></tr>
        <tr><td>Covalent</td><td>Non-metals</td><td>Electrons shared between atoms</td></tr>
        <tr><td>Metallic</td><td>Metal atoms</td><td>Sea of delocalised electrons + positive ions</td></tr>
      </table>
    `},
    { h:'Giant Ionic Lattice', content:`
      <ul>
        <li>Regular 3D lattice of oppositely charged ions.</li>
        <li>High melting/boiling points (strong electrostatic forces).</li>
        <li>Conduct electricity when molten or dissolved (mobile ions), NOT when solid.</li>
        <li>Often soluble in water.</li>
      </ul>
    `},
    { h:'Covalent Substances', content:`
      <ul>
        <li><strong>Simple molecular:</strong> small molecules (H₂O, CO₂, CH₄). Low mp/bp (weak intermolecular forces). Do not conduct electricity.</li>
        <li><strong>Giant covalent:</strong> Diamond (4 bonds/C — very hard, no conductivity), Graphite (3 bonds/C — delocalised electrons conduct, layers slide — lubricant), Silicon dioxide.</li>
        <li><strong>Polymers:</strong> very long chains — higher mp than simple molecules but lower than giant structures.</li>
        <li><strong>Fullerenes:</strong> cage-like structures (C₆₀, nanotubes) — used in drug delivery, electronics, lubricants.</li>
      </ul>
    `},
    { h:'Nanoparticles', content:`
      <ul>
        <li>Size: 1–100 nm. Huge surface area to volume ratio.</li>
        <li>Used in: sunscreens, antibacterials, drug delivery, electronics.</li>
        <li>Potential risks to health and environment are still being studied.</li>
      </ul>
    `},
  ]
},

chemistry_quantitative: {
  title:'Quantitative Chemistry',
  intro:'Quantitative chemistry allows us to calculate the amounts of substances in reactions using the mole concept.',
  sections:[
    { h:'The Mole', content:`
      <div class="formula-box">moles = mass ÷ Mr (relative formula mass)</div>
      <div class="formula-box">mass = moles × Mr</div>
      <div class="formula-box">moles = concentration (mol/dm³) × volume (dm³)</div>
      <div class="formula-box">moles of gas at RTP = volume (dm³) ÷ 24</div>
      <p>Avogadro's constant: 1 mole = 6.02 × 10²³ particles.</p>
    `},
    { h:'Balancing Equations & Ratios', content:`
      <ul>
        <li>A balanced equation gives the molar ratio of reactants to products.</li>
        <li>Example: 2H₂ + O₂ → 2H₂O means 2 moles H₂ reacts with 1 mole O₂ to give 2 moles H₂O.</li>
        <li>Identify the limiting reactant — this is the one that runs out first and determines how much product forms.</li>
      </ul>
    `},
    { h:'Yield & Atom Economy', content:`
      <div class="formula-box">% yield = (actual yield ÷ theoretical yield) × 100</div>
      <div class="formula-box">Atom economy = (Mr desired product ÷ ΣMr all reactants) × 100</div>
      <ul>
        <li>Yield < 100% due to: reversible reactions, purification losses, side reactions.</li>
        <li>High atom economy = greener chemistry (less waste).</li>
      </ul>
    `},
    { h:'Titration Calculations', content:`
      <ul>
        <li>Titration finds the concentration of an unknown solution.</li>
        <li>Steps: find moles of known solution → use ratio from equation → find moles of unknown → calculate concentration.</li>
      </ul>
      <div class="exam-tip">Always use mean titre, excluding anomalous results. Titre = volume of solution added from burette.</div>
    `},
  ]
},

chemistry_rates: {
  title:'Rates of Reaction & Equilibrium',
  intro:'The rate of a reaction measures how quickly reactants are converted to products. Understanding equilibrium is essential for industrial chemistry.',
  sections:[
    { h:'Factors Affecting Rate', content:`
      <ul>
        <li><strong>Temperature:</strong> more energy → more frequent + energetic collisions → more exceed activation energy.</li>
        <li><strong>Concentration:</strong> more particles per unit volume → more frequent collisions.</li>
        <li><strong>Surface area:</strong> smaller particles → greater surface area exposed → more collisions.</li>
        <li><strong>Catalyst:</strong> provides alternative pathway with lower activation energy.</li>
        <li><strong>Pressure (gases):</strong> higher pressure → higher concentration → more collisions.</li>
      </ul>
    `},
    { h:'Measuring Rate', content:`
      <ul>
        <li>Rate = change in quantity ÷ time.</li>
        <li>Can measure: loss of mass (CO₂ given off), volume of gas produced, colour change, change in turbidity.</li>
        <li>On a graph: steeper gradient = faster rate. Reaction stops when line becomes horizontal.</li>
      </ul>
      <div class="required-practical">Investigate how concentration of HCl affects rate with marble chips (CaCO₃). Measure CO₂ gas volume or mass loss over time.</div>
    `},
    { h:'Equilibrium & Le Chatelier', content:`
      <ul>
        <li>In a closed system, a reversible reaction reaches <strong>dynamic equilibrium</strong> — forward rate = reverse rate, concentrations constant.</li>
        <li><strong>Le Chatelier's Principle:</strong> if conditions change, equilibrium shifts to oppose the change.</li>
        <li>↑Temperature → shifts in the endothermic direction.</li>
        <li>↑Pressure → shifts to the side with fewer moles of gas.</li>
        <li>↑Concentration of reactant → shifts right (more product).</li>
        <li>Catalyst: does NOT shift equilibrium — just reaches it faster.</li>
      </ul>
    `},
    { h:'Haber Process', content:`
      <div class="formula-box">N₂(g) + 3H₂(g) ⇌ 2NH₃(g) &nbsp; ΔH = −92 kJ/mol</div>
      <ul>
        <li>Conditions: 450°C, 200 atm, iron catalyst.</li>
        <li>Compromise: lower temperature gives higher yield but too slow. 450°C is the optimum compromise.</li>
        <li>Higher pressure favours NH₃ (fewer gas moles on right) but is expensive and dangerous above 200 atm.</li>
        <li>Unreacted N₂ and H₂ are recycled.</li>
      </ul>
    `},
  ]
},

chemistry_analysis: {
  title:'Chemical Analysis',
  intro:'Chemical analysis is used to identify substances and determine purity. AQA requires knowledge of flame tests, ion tests and chromatography.',
  sections:[
    { h:'Flame Tests', content:`
      <table class="notes-table">
        <tr><th>Ion</th><th>Flame colour</th></tr>
        <tr><td>Lithium (Li⁺)</td><td>Crimson/red</td></tr>
        <tr><td>Sodium (Na⁺)</td><td>Yellow/orange</td></tr>
        <tr><td>Potassium (K⁺)</td><td>Lilac/purple</td></tr>
        <tr><td>Calcium (Ca²⁺)</td><td>Orange-red</td></tr>
        <tr><td>Barium (Ba²⁺)</td><td>Green</td></tr>
        <tr><td>Copper (Cu²⁺)</td><td>Blue-green</td></tr>
      </table>
    `},
    { h:'Testing for Ions (NaOH)', content:`
      <table class="notes-table">
        <tr><th>Ion</th><th>Observation with NaOH</th></tr>
        <tr><td>Cu²⁺</td><td>Blue precipitate</td></tr>
        <tr><td>Fe²⁺</td><td>Green precipitate</td></tr>
        <tr><td>Fe³⁺</td><td>Brown/orange precipitate</td></tr>
        <tr><td>Al³⁺, Mg²⁺, Ca²⁺</td><td>White precipitate</td></tr>
        <tr><td>NH₄⁺</td><td>Ammonia gas (pungent smell, turns damp red litmus blue)</td></tr>
      </table>
    `},
    { h:'Testing for Anions', content:`
      <table class="notes-table">
        <tr><th>Ion</th><th>Test</th><th>Result</th></tr>
        <tr><td>Cl⁻</td><td>AgNO₃ (acidified)</td><td>White precipitate (AgCl)</td></tr>
        <tr><td>Br⁻</td><td>AgNO₃ (acidified)</td><td>Cream precipitate (AgBr)</td></tr>
        <tr><td>I⁻</td><td>AgNO₃ (acidified)</td><td>Yellow precipitate (AgI)</td></tr>
        <tr><td>SO₄²⁻</td><td>BaCl₂ (acidified)</td><td>White precipitate (BaSO₄)</td></tr>
        <tr><td>CO₃²⁻</td><td>HCl → bubble through limewater</td><td>Limewater turns milky</td></tr>
      </table>
    `},
    { h:'Testing for Gases', content:`
      <table class="notes-table">
        <tr><th>Gas</th><th>Test</th><th>Result</th></tr>
        <tr><td>H₂</td><td>Burning splint</td><td>"Squeaky pop"</td></tr>
        <tr><td>O₂</td><td>Glowing splint</td><td>Splint relights</td></tr>
        <tr><td>CO₂</td><td>Limewater</td><td>Turns milky/cloudy</td></tr>
        <tr><td>Cl₂</td><td>Damp litmus paper</td><td>Bleached white</td></tr>
        <tr><td>NH₃</td><td>Damp red litmus paper</td><td>Turns blue</td></tr>
      </table>
    `},
    { h:'Chromatography', content:`
      <div class="formula-box">Rf = distance moved by substance ÷ distance moved by solvent</div>
      <ul>
        <li>Same Rf value = same substance.</li>
        <li>If a spot doesn't move → not soluble in that solvent.</li>
        <li>Used to test purity: pure substance → one spot. Mixture → multiple spots.</li>
      </ul>
    `},
  ]
},

// ── PHYSICS MISSING NOTES ─────────────────────────────────────

physics_waves: {
  title:'Waves',
  intro:'Waves transfer energy from one place to another without transferring matter. AQA requires you to understand wave properties, types, reflection, refraction, and sound.',
  sections:[
    { h:'Wave Properties', content:`
      <div class="key-grid">
        <div class="key-card"><div class="kc-label">Amplitude</div><div class="kc-val">Maximum displacement from equilibrium position. Larger amplitude = more energy.</div></div>
        <div class="key-card"><div class="kc-label">Wavelength (λ)</div><div class="kc-val">Distance from one crest (or trough) to the next. Measured in metres.</div></div>
        <div class="key-card"><div class="kc-label">Frequency (f)</div><div class="kc-val">Number of complete waves passing a point per second. Measured in Hertz (Hz).</div></div>
        <div class="key-card"><div class="kc-label">Period (T)</div><div class="kc-val">Time for one complete wave. T = 1/f. Measured in seconds.</div></div>
        <div class="key-card"><div class="kc-label">Wave speed (v)</div><div class="kc-val">Speed at which energy is transferred. v = fλ. Measured in m/s.</div></div>
      </div>
      <div class="formula-box">v = fλ &nbsp;|&nbsp; T = 1/f &nbsp;|&nbsp; f = 1/T</div>
    `},
    { h:'Transverse vs Longitudinal Waves', content:`
      <table class="notes-table">
        <tr><th></th><th>Transverse</th><th>Longitudinal</th></tr>
        <tr><td>Oscillation direction</td><td>Perpendicular to wave travel</td><td>Parallel to wave travel</td></tr>
        <tr><td>Features</td><td>Crests and troughs</td><td>Compressions and rarefactions</td></tr>
        <tr><td>Examples</td><td>All EM waves, water waves, S-waves</td><td>Sound, ultrasound, P-waves</td></tr>
        <tr><td>Can travel in vacuum?</td><td>Yes (EM waves)</td><td>No (needs a medium)</td></tr>
      </table>
      <div class="exam-tip">Sound CANNOT travel through a vacuum — this was proved by the bell-jar experiment (ringing bell goes silent as air is pumped out).</div>
    `},
    { h:'Reflection & Refraction', content:`
      <ul>
        <li><strong>Reflection:</strong> angle of incidence = angle of reflection (both measured from the normal). The normal is a line perpendicular to the surface at the point of incidence.</li>
        <li><strong>Refraction:</strong> waves change speed (and direction) when moving between media of different density. Frequency stays the same; wavelength and speed change.</li>
        <li>Moving from less dense → more dense medium: waves slow down and bend <em>toward</em> the normal.</li>
        <li>Moving from more dense → less dense medium: waves speed up and bend <em>away</em> from the normal.</li>
      </ul>
    `},
    { h:'Sound Waves', content:`
      <ul>
        <li>Sound travels as longitudinal waves — particles vibrate parallel to wave direction.</li>
        <li>Speed of sound in air ≈ 340 m/s. Travels faster through solids and liquids (particles closer together).</li>
        <li>Human hearing range: 20 Hz – 20,000 Hz. Ultrasound is above 20,000 Hz.</li>
        <li><strong>Ultrasound uses:</strong> medical imaging (no ionising radiation), sonar, quality control (detecting cracks).</li>
        <li>Pitch is determined by frequency. Loudness is determined by amplitude.</li>
      </ul>
      <div class="exam-tip">In an echo calculation: distance = (speed × time) ÷ 2. Divide by 2 because sound travels to the surface AND back.</div>
    `},
    { h:'Required Practical', content:`
      <div class="required-practical">Investigate the relationship between frequency and wavelength for waves on a string (or ripple tank). Measure wave speed using v = fλ and verify it remains constant when frequency changes.</div>
    `},
  ]
},

physics_em_spec: {
  title:'Electromagnetic Spectrum',
  intro:'Electromagnetic (EM) waves are transverse waves that all travel at 3 × 10⁸ m/s in a vacuum. They transfer energy without needing a medium.',
  sections:[
    { h:'The EM Spectrum (low f → high f)', content:`
      <table class="notes-table">
        <tr><th>Type</th><th>Wavelength</th><th>Uses</th><th>Hazards</th></tr>
        <tr><td><strong>Radio</strong></td><td>Metres → km</td><td>Broadcasting, communications</td><td>None significant</td></tr>
        <tr><td><strong>Microwave</strong></td><td>mm → cm</td><td>Cooking, mobile phones, satellites</td><td>Internal heating of tissue</td></tr>
        <tr><td><strong>Infrared (IR)</strong></td><td>~700 nm</td><td>Thermal imaging, remote controls, optical fibres, grills</td><td>Skin burns</td></tr>
        <tr><td><strong>Visible light</strong></td><td>400–700 nm</td><td>Vision, photography, optical fibres</td><td>None at normal intensity</td></tr>
        <tr><td><strong>Ultraviolet (UV)</strong></td><td>~400 nm</td><td>Sun beds, sterilisation, security marking</td><td>Skin cancer, eye damage</td></tr>
        <tr><td><strong>X-rays</strong></td><td>~0.1 nm</td><td>Medical imaging (bones), airport security</td><td>Cell/DNA damage, cancer</td></tr>
        <tr><td><strong>Gamma (γ)</strong></td><td>&lt;0.01 nm</td><td>Killing cancer cells, sterilising equipment, medical tracers</td><td>Cell/DNA damage, cancer</td></tr>
      </table>
      <div class="exam-tip">All EM waves travel at c = 3 × 10⁸ m/s in a vacuum. Higher frequency = shorter wavelength = more energy per photon.</div>
    `},
    { h:'Properties of EM Waves', content:`
      <ul>
        <li>All EM waves are <strong>transverse</strong>.</li>
        <li>All travel at <strong>3 × 10⁸ m/s</strong> in a vacuum (the speed of light, c).</li>
        <li>They can all be reflected, refracted, diffracted, and undergo interference.</li>
        <li>They transfer energy as <strong>photons</strong>. Higher frequency = higher energy photon.</li>
        <li>Radio waves through IR are <strong>non-ionising</strong>. UV through gamma are <strong>ionising</strong> (can remove electrons from atoms, damaging DNA).</li>
      </ul>
    `},
    { h:'Radio Waves & Communication', content:`
      <ul>
        <li>Long-wave radio diffracts around the Earth's curvature — good for long-distance broadcasting.</li>
        <li>Short-wave radio reflects off the ionosphere — used for global communication.</li>
        <li>Microwaves pass through the atmosphere — used for satellite communication and mobile phones.</li>
        <li>Optical fibres use total internal reflection to carry visible light/IR signals with very low signal loss.</li>
      </ul>
    `},
    { h:'Infrared & Temperature', content:`
      <ul>
        <li>All objects above absolute zero emit infrared radiation.</li>
        <li>Hotter objects emit more IR and at higher frequencies.</li>
        <li>Dark, matt surfaces are better emitters and absorbers of IR than shiny, light surfaces.</li>
        <li>This is why solar panels and radiators are often painted black/dark.</li>
      </ul>
    `},
  ]
},

physics_electricity: {
  title:'Electricity & Circuits',
  intro:'Electricity involves the flow of charge (electrons) through conductors. AQA covers circuit components, calculations using Ohm\'s Law, and domestic electricity.',
  sections:[
    { h:'Key Equations', content:`
      <div class="formula-box">V = IR &nbsp; (potential difference = current × resistance)</div>
      <div class="formula-box">P = VI = I²R = V²/R &nbsp; (power)</div>
      <div class="formula-box">E = Pt = VIt &nbsp; (energy transferred)</div>
      <div class="formula-box">Q = It &nbsp; (charge = current × time)</div>
      <div class="formula-box">E = QV &nbsp; (energy = charge × p.d.)</div>
    `},
    { h:'Circuit Components', content:`
      <table class="notes-table">
        <tr><th>Component</th><th>Symbol</th><th>Function</th></tr>
        <tr><td>Resistor</td><td>Rectangle</td><td>Resists current flow</td></tr>
        <tr><td>Variable resistor</td><td>Rectangle with arrow</td><td>Adjustable resistance</td></tr>
        <tr><td>Thermistor (NTC)</td><td>Rectangle with T</td><td>Resistance decreases as temperature increases</td></tr>
        <tr><td>LDR</td><td>Rectangle with arrows</td><td>Resistance decreases as light intensity increases</td></tr>
        <tr><td>Diode</td><td>Triangle + line</td><td>Allows current in one direction only</td></tr>
        <tr><td>LED</td><td>Diode with arrows out</td><td>Emits light when current flows</td></tr>
        <tr><td>Capacitor</td><td>Two parallel lines</td><td>Stores charge temporarily</td></tr>
      </table>
    `},
    { h:'Series vs Parallel Circuits', content:`
      <table class="notes-table">
        <tr><th></th><th>Series</th><th>Parallel</th></tr>
        <tr><td>Current</td><td>Same through all components</td><td>Splits at each junction</td></tr>
        <tr><td>Voltage</td><td>Divides across components (adds up to supply)</td><td>Same across each branch</td></tr>
        <tr><td>Resistance</td><td>R_total = R₁ + R₂ + R₃</td><td>1/R_total = 1/R₁ + 1/R₂</td></tr>
        <tr><td>Fault</td><td>One break stops all</td><td>Other branches still work</td></tr>
      </table>
      <div class="exam-tip">Adding resistors in parallel always reduces total resistance — even adding a very large resistor in parallel makes total resistance slightly smaller.</div>
    `},
    { h:'I–V Characteristics', content:`
      <ul>
        <li><strong>Ohmic resistor (fixed):</strong> straight line through origin — current proportional to voltage (Ohm's Law holds).</li>
        <li><strong>Filament bulb:</strong> curve — resistance increases as temperature increases (atoms vibrate more, impede electron flow).</li>
        <li><strong>Diode:</strong> only conducts when forward biased above ~0.7 V; very high resistance in reverse.</li>
      </ul>
      <div class="required-practical">Plot I–V characteristics of a resistor, filament bulb and diode. Use an ammeter in series and voltmeter in parallel. Vary voltage using a variable resistor.</div>
    `},
    { h:'Domestic Electricity & Safety', content:`
      <ul>
        <li><strong>Mains supply:</strong> 230 V AC at 50 Hz in the UK. AC reverses direction 50 times per second.</li>
        <li><strong>UK plug wiring:</strong> Live (brown) = 230 V, Neutral (blue) = 0 V, Earth (green/yellow) = safety.</li>
        <li><strong>Fuse:</strong> thin wire that melts if current exceeds safe level. Must be in the live wire.</li>
        <li><strong>Earth wire:</strong> connects metal casing to ground. If live wire touches the casing, current flows to earth → fuse blows → circuit breaks safely.</li>
        <li><strong>RCD (Residual Current Device):</strong> detects tiny differences in current between live and neutral; trips much faster than a fuse.</li>
      </ul>
      <div class="formula-box">Energy (kWh) = Power (kW) × Time (h) &nbsp;|&nbsp; Cost = Energy × price per kWh</div>
    `},
  ]
},

physics_magnetism: {
  title:'Magnetism & Electromagnetism',
  intro:'Magnetism arises from moving charges. The interaction of magnetic fields and current-carrying conductors underpins motors, generators and transformers.',
  sections:[
    { h:'Magnetic Fields', content:`
      <ul>
        <li>Field lines go from <strong>north to south</strong> outside the magnet. Closer lines = stronger field.</li>
        <li>Like poles repel; unlike poles attract.</li>
        <li>A current-carrying wire creates a <strong>circular magnetic field</strong> around it (right-hand grip rule: thumb = current direction, fingers = field direction).</li>
        <li>A solenoid creates a field like a bar magnet. Adding a soft-iron core makes an <strong>electromagnet</strong>.</li>
      </ul>
      <div class="exam-tip">The Earth's magnetic field is caused by convection currents of molten iron in the outer core, not by a permanent magnet.</div>
    `},
    { h:'The Motor Effect', content:`
      <div class="formula-box">F = BIL &nbsp; (Force = magnetic flux density × current × length)</div>
      <ul>
        <li>A current-carrying conductor in a magnetic field experiences a force (the <strong>motor effect</strong>).</li>
        <li><strong>Fleming's Left-Hand Rule</strong> gives the direction of force: First finger = Field, seCond finger = Current, thuMb = Motion (force).</li>
        <li>Force is maximum when current is perpendicular to the field; zero when parallel.</li>
        <li>The <strong>DC motor</strong> uses a split-ring commutator to reverse current direction every half turn, keeping rotation continuous.</li>
      </ul>
    `},
    { h:'Electromagnetic Induction', content:`
      <ul>
        <li>A potential difference is <strong>induced</strong> whenever a conductor moves relative to a magnetic field (or the field changes).</li>
        <li>If the circuit is complete, an induced current flows.</li>
        <li><strong>Increase the induced EMF</strong> by: moving faster, using a stronger magnet, adding more turns to the coil.</li>
        <li><strong>Lenz's Law:</strong> the induced current always opposes the change causing it (conservation of energy).</li>
        <li><strong>Fleming's Right-Hand Rule</strong> gives the direction of induced current in generators.</li>
      </ul>
      <div class="exam-tip">LEFT hand = motor (force from current). RIGHT hand = generator (current from force). Remember: Left = motor starts with L like "eLectrical → motion".</div>
    `},
    { h:'Transformers', content:`
      <div class="formula-box">Vₚ/Vₛ = Nₚ/Nₛ &nbsp;|&nbsp; VₚIₚ = VₛIₛ (ideal transformer)</div>
      <ul>
        <li><strong>Step-up transformer:</strong> more turns on secondary → higher voltage, lower current.</li>
        <li><strong>Step-down transformer:</strong> fewer turns on secondary → lower voltage, higher current.</li>
        <li>Transformers only work with <strong>AC</strong> — the changing field induces an EMF in the secondary coil.</li>
        <li><strong>National Grid:</strong> power stations generate at ~25,000 V → step UP to 400,000 V for transmission → step DOWN for homes (230 V). High voltage = low current = less power lost as heat (P = I²R).</li>
      </ul>
    `},
  ]
},

physics_particles: {
  title:'Particle Model of Matter',
  intro:'The particle model explains the properties of solids, liquids and gases, and allows us to calculate energy changes during heating and state changes.',
  sections:[
    { h:'States of Matter', content:`
      <table class="notes-table">
        <tr><th></th><th>Solid</th><th>Liquid</th><th>Gas</th></tr>
        <tr><td>Particle arrangement</td><td>Regular lattice, close-packed</td><td>Random, close-packed</td><td>Random, far apart</td></tr>
        <tr><td>Particle movement</td><td>Vibrate about fixed positions</td><td>Flow past each other</td><td>Move freely and rapidly</td></tr>
        <tr><td>Shape</td><td>Fixed</td><td>Takes container shape</td><td>Fills container</td></tr>
        <tr><td>Volume</td><td>Fixed</td><td>Fixed</td><td>Fills container</td></tr>
        <tr><td>Density</td><td>High</td><td>High</td><td>Very low</td></tr>
      </table>
    `},
    { h:'Key Equations', content:`
      <div class="formula-box">Q = mcΔT &nbsp; (thermal energy = mass × specific heat capacity × temperature change)</div>
      <div class="formula-box">Q = mL &nbsp; (energy for state change = mass × specific latent heat)</div>
      <div class="formula-box">ρ = m/V &nbsp; (density = mass ÷ volume)</div>
      <div class="formula-box">pV = constant &nbsp; (Boyle's Law — constant temperature)</div>
      <div class="formula-box">p/T = constant &nbsp; (Gay-Lussac's Law — constant volume)</div>
    `},
    { h:'Specific Heat Capacity', content:`
      <ul>
        <li>The <strong>specific heat capacity (c)</strong> is the energy needed to raise 1 kg of a substance by 1°C.</li>
        <li>Water: c = 4200 J/kg°C. Aluminium: c = 900 J/kg°C. Iron: c = 450 J/kg°C.</li>
        <li>On a temperature-time graph, a steeper gradient means lower specific heat capacity.</li>
      </ul>
      <div class="required-practical">Measure specific heat capacity by heating a known mass of material with a known power for a measured time. Use Q = Pt = mcΔT to calculate c.</div>
    `},
    { h:'Specific Latent Heat & State Changes', content:`
      <ul>
        <li>During a <strong>state change</strong>, temperature stays constant — energy is used to break/form intermolecular bonds, not increase kinetic energy.</li>
        <li><strong>Specific latent heat of fusion (L_f):</strong> energy to melt/freeze 1 kg. Water: 334,000 J/kg.</li>
        <li><strong>Specific latent heat of vaporisation (L_v):</strong> energy to boil/condense 1 kg. Water: 2,260,000 J/kg.</li>
        <li>L_v is always much greater than L_f — more bonds must be broken to vaporise.</li>
      </ul>
    `},
    { h:'Gas Pressure & the Particle Model', content:`
      <ul>
        <li>Gas pressure is caused by particles colliding with the walls of a container.</li>
        <li><strong>Boyle's Law:</strong> at constant temperature, pressure × volume = constant (P₁V₁ = P₂V₂). Halving volume doubles pressure.</li>
        <li><strong>Temperature and pressure:</strong> increasing temperature increases particle speed → more frequent, harder collisions → greater pressure.</li>
        <li><strong>Absolute zero (0 K = −273°C):</strong> the temperature at which particles have minimum kinetic energy. Gas pressure would be zero.</li>
        <li>Convert: T(K) = T(°C) + 273</li>
      </ul>
    `},
  ]
},

physics_atomic: {
  title:'Atomic Structure & Radioactivity',
  intro:'This topic covers the structure of the atom, nuclear radiation, radioactive decay, half-life and nuclear reactions — all essential AQA content.',
  sections:[
    { h:'The Nuclear Atom', content:`
      <table class="notes-table">
        <tr><th>Particle</th><th>Location</th><th>Relative mass</th><th>Relative charge</th></tr>
        <tr><td>Proton</td><td>Nucleus</td><td>1</td><td>+1</td></tr>
        <tr><td>Neutron</td><td>Nucleus</td><td>1</td><td>0</td></tr>
        <tr><td>Electron</td><td>Shells (orbits)</td><td>~1/1836</td><td>−1</td></tr>
      </table>
      <ul>
        <li>The nucleus is tiny compared to the atom — if the atom were a football stadium, the nucleus would be a pea in the centre.</li>
        <li><strong>Atomic (proton) number Z:</strong> number of protons = number of electrons in a neutral atom.</li>
        <li><strong>Mass (nucleon) number A:</strong> protons + neutrons. Neutrons = A − Z.</li>
        <li><strong>Isotopes:</strong> atoms of the same element with different numbers of neutrons.</li>
      </ul>
    `},
    { h:'Types of Nuclear Radiation', content:`
      <table class="notes-table">
        <tr><th></th><th>Alpha (α)</th><th>Beta-minus (β⁻)</th><th>Gamma (γ)</th></tr>
        <tr><td>What is it?</td><td>2 protons + 2 neutrons (He nucleus)</td><td>Fast electron from nucleus (neutron → proton + electron)</td><td>EM wave from nucleus</td></tr>
        <tr><td>Charge</td><td>+2</td><td>−1</td><td>0</td></tr>
        <tr><td>Relative mass</td><td>4</td><td>~0</td><td>0</td></tr>
        <tr><td>Penetrating power</td><td>Low (stopped by paper/skin)</td><td>Medium (stopped by ~5mm aluminium)</td><td>High (reduced by thick lead/concrete)</td></tr>
        <tr><td>Ionising power</td><td>Very high</td><td>Medium</td><td>Low</td></tr>
        <tr><td>Speed</td><td>~5% speed of light</td><td>~80% speed of light</td><td>Speed of light</td></tr>
      </table>
    `},
    { h:'Nuclear Decay Equations', content:`
      <ul>
        <li><strong>Alpha decay:</strong> mass number −4, atomic number −2. e.g. ²³⁸₉₂U → ²³⁴₉₀Th + ⁴₂He</li>
        <li><strong>Beta-minus decay:</strong> mass number unchanged, atomic number +1. A neutron becomes a proton + electron. e.g. ¹⁴₆C → ¹⁴₇N + ⁰₋₁e</li>
        <li><strong>Gamma emission:</strong> no change in mass number or atomic number — just releases energy.</li>
      </ul>
      <div class="exam-tip">In nuclear equations, the top numbers (mass) must balance on both sides AND the bottom numbers (atomic) must balance.</div>
    `},
    { h:'Half-life & Activity', content:`
      <ul>
        <li><strong>Activity:</strong> the number of nuclear decays per second. Measured in Becquerels (Bq).</li>
        <li><strong>Half-life:</strong> time for activity (or number of undecayed nuclei) to halve. It is constant and cannot be changed by temperature, pressure or chemical state.</li>
        <li>After n half-lives: remaining nuclei = initial × (½)ⁿ.</li>
      </ul>
      <div class="formula-box">After n half-lives: N = N₀ × (½)ⁿ</div>
      <div class="exam-tip">Short half-life isotopes are used for medical tracers (decay quickly, limiting patient exposure). Long half-life isotopes are useful for radiometric dating.</div>
    `},
    { h:'Uses of Radiation', content:`
      <div class="key-grid">
        <div class="key-card"><div class="kc-label">Smoke detectors</div><div class="kc-val">Alpha emitter ionises air → current flows. Smoke absorbs alpha → current drops → alarm triggers.</div></div>
        <div class="key-card"><div class="kc-label">Medical tracers</div><div class="kc-val">Gamma-emitting isotopes injected → detected externally. Short half-life essential.</div></div>
        <div class="key-card"><div class="kc-label">Cancer treatment</div><div class="kc-val">Gamma rays focused on tumour from multiple angles to kill cancer cells.</div></div>
        <div class="key-card"><div class="kc-label">Thickness gauges</div><div class="kc-val">Beta source + detector. More material absorbed = less detected = product too thick.</div></div>
        <div class="key-card"><div class="kc-label">Carbon-14 dating</div><div class="kc-val">Half-life 5,730 years. Ratio of C-14 to C-12 in dead material gives age.</div></div>
        <div class="key-card"><div class="kc-label">Nuclear power</div><div class="kc-val">Fission of U-235. Chain reaction controlled by control rods. Heat → steam → turbines.</div></div>
      </div>
    `},
    { h:'Nuclear Fission & Fusion', content:`
      <ul>
        <li><strong>Fission:</strong> a large unstable nucleus (e.g. U-235) absorbs a neutron and splits into two smaller nuclei + 2–3 neutrons + energy. The released neutrons cause further fissions — a <strong>chain reaction</strong>.</li>
        <li><strong>Fusion:</strong> two light nuclei (e.g. H isotopes) join to form a heavier nucleus, releasing large amounts of energy. Powers the Sun and stars.</li>
        <li>Fusion requires extremely high temperatures (~10⁷ K) to overcome electrostatic repulsion between nuclei — this makes it very difficult to achieve on Earth.</li>
      </ul>
    `},
  ]
},

physics_space: {
  title:'Space Physics',
  intro:'Space physics covers our Solar System, stellar evolution, the expanding universe and the evidence for the Big Bang — all required by AQA Triple Physics.',
  sections:[
    { h:'Our Solar System', content:`
      <ul>
        <li>The Sun is a star at the centre of our Solar System. 8 planets orbit it in elliptical paths.</li>
        <li>Planets (in order): Mercury, Venus, Earth, Mars, Jupiter, Saturn, Uranus, Neptune.</li>
        <li><strong>Gravity</strong> provides the centripetal force that keeps planets, moons and satellites in orbit.</li>
        <li>Planets closer to the Sun have shorter orbital periods and greater orbital speeds.</li>
        <li>The Milky Way is our galaxy — a spiral galaxy containing ~200 billion stars. The Solar System is in one of its outer arms.</li>
      </ul>
    `},
    { h:'Life Cycle of Stars', content:`
      <table class="notes-table">
        <tr><th>Stage</th><th>Sun-like star</th><th>Massive star (&gt;8× Sun)</th></tr>
        <tr><td>Birth</td><td colspan="2">Nebula → protostar (gravity causes collapse + heating)</td></tr>
        <tr><td>Main sequence</td><td colspan="2">Nuclear fusion: H → He. Radiation pressure balances gravity. Stable for millions/billions of years.</td></tr>
        <tr><td>Giant phase</td><td>Red giant (expands as H runs out)</td><td>Red supergiant</td></tr>
        <tr><td>Death</td><td>Planetary nebula → White dwarf → (eventually black dwarf)</td><td>Supernova → Neutron star OR Black hole</td></tr>
      </table>
      <div class="exam-tip">All elements heavier than iron are formed in supernovae. Elements up to iron are formed by nuclear fusion in main-sequence stars.</div>
    `},
    { h:'The Expanding Universe & Red-shift', content:`
      <ul>
        <li>Distant galaxies show <strong>red-shift</strong> — their light is stretched to longer (redder) wavelengths, indicating they are moving away from us.</li>
        <li>The further a galaxy, the greater its red-shift and the faster it recedes (<strong>Hubble's Law</strong>).</li>
        <li>This evidence shows the universe is <strong>expanding</strong> — all galaxies moving apart.</li>
        <li>Looking back in time: if everything is moving apart now, everything must have been at a single point — the <strong>Big Bang</strong>.</li>
      </ul>
    `},
    { h:'The Big Bang & Cosmic Microwave Background', content:`
      <ul>
        <li>The Big Bang (~13.8 billion years ago): the universe began as an extremely hot, dense point and has been expanding ever since.</li>
        <li><strong>Cosmic Microwave Background (CMB) radiation:</strong> uniform microwave radiation from all directions in space — a "thermal afterglow" of the Big Bang. This is strong evidence for the Big Bang theory.</li>
        <li>As the universe expanded, it cooled — energy became matter, atoms formed, stars and galaxies condensed under gravity.</li>
      </ul>
    `},
    { h:'Satellites & Orbits', content:`
      <ul>
        <li><strong>Low Earth Orbit (LEO) ~200–2000 km:</strong> fast orbit (90 min), short communication delay. Used for: spy satellites, ISS, some communication satellites.</li>
        <li><strong>Geostationary orbit ~36,000 km:</strong> 24-hour period — stays above the same point on Earth. Used for: TV, weather, communications.</li>
        <li>All orbits: gravity provides centripetal acceleration. No fuel needed once in orbit (vacuum, no friction).</li>
      </ul>
    `},
  ]
},

// ── BIOLOGY MISSING NOTES ────────────────────────────────────

biology_organisation: {
  title:'Organisation',
  intro:'Organisation covers how cells, tissues and organs work together in living systems, including digestion, circulation and plant transport.',
  sections:[
    { h:'Levels of Organisation', content:`
      <div class="key-grid">
        <div class="key-card"><div class="kc-label">Cell</div><div class="kc-val">Basic unit of life. e.g. red blood cell, muscle cell</div></div>
        <div class="key-card"><div class="kc-label">Tissue</div><div class="kc-val">Group of similar cells with the same function. e.g. muscle tissue, epithelium</div></div>
        <div class="key-card"><div class="kc-label">Organ</div><div class="kc-val">Group of different tissues working together. e.g. stomach, heart, leaf</div></div>
        <div class="key-card"><div class="kc-label">Organ system</div><div class="kc-val">Group of organs working together. e.g. digestive system, circulatory system</div></div>
      </div>
    `},
    { h:'The Digestive System', content:`
      <ul>
        <li><strong>Mouth:</strong> mechanical digestion (chewing) + amylase (starch → sugars).</li>
        <li><strong>Stomach:</strong> protease (proteins → amino acids); HCl kills bacteria and creates optimum pH for protease.</li>
        <li><strong>Small intestine:</strong> lipase (fats → fatty acids + glycerol), protease, amylase from pancreas; bile from liver emulsifies fats; absorption via villi.</li>
        <li><strong>Large intestine:</strong> water reabsorbed; faeces formed.</li>
      </ul>
      <table class="notes-table">
        <tr><th>Enzyme</th><th>Produced in</th><th>Substrate → Product</th></tr>
        <tr><td>Amylase</td><td>Salivary glands, pancreas</td><td>Starch → maltose/glucose</td></tr>
        <tr><td>Protease</td><td>Stomach, pancreas</td><td>Proteins → amino acids</td></tr>
        <tr><td>Lipase</td><td>Pancreas, small intestine</td><td>Lipids → fatty acids + glycerol</td></tr>
      </table>
      <div class="exam-tip">Bile is NOT an enzyme — it emulsifies fats (breaks large fat droplets into tiny ones) to increase surface area for lipase to work on.</div>
    `},
    { h:'The Heart & Circulatory System', content:`
      <ul>
        <li>Humans have a <strong>double circulatory system</strong>: pulmonary circulation (heart → lungs → heart) and systemic circulation (heart → body → heart).</li>
        <li><strong>Right side of heart:</strong> receives deoxygenated blood from body (vena cava) → pumps to lungs (pulmonary artery).</li>
        <li><strong>Left side of heart:</strong> receives oxygenated blood from lungs (pulmonary vein) → pumps to body (aorta).</li>
        <li>Heart muscle is supplied by coronary arteries. Blockage → heart attack.</li>
      </ul>
      <table class="notes-table">
        <tr><th>Blood vessel</th><th>Carries</th><th>Structure</th></tr>
        <tr><td>Artery</td><td>Blood away from heart (high pressure)</td><td>Thick muscular walls, narrow lumen, elastic</td></tr>
        <tr><td>Vein</td><td>Blood to heart (low pressure)</td><td>Thin walls, wide lumen, valves prevent backflow</td></tr>
        <tr><td>Capillary</td><td>Exchange between blood and tissues</td><td>One cell thick, permeable walls, huge network</td></tr>
      </table>
    `},
    { h:'Blood Components', content:`
      <div class="key-grid">
        <div class="key-card"><div class="kc-label">Red blood cells</div><div class="kc-val">Biconcave disc. No nucleus. Contain haemoglobin. Carry O₂.</div></div>
        <div class="key-card"><div class="kc-label">White blood cells</div><div class="kc-val">Immune defence. Phagocytes (engulf) and lymphocytes (antibodies).</div></div>
        <div class="key-card"><div class="kc-label">Platelets</div><div class="kc-val">Cell fragments. Trigger blood clotting at wounds.</div></div>
        <div class="key-card"><div class="kc-label">Plasma</div><div class="kc-val">Liquid. Carries dissolved nutrients, CO₂, urea, hormones, heat.</div></div>
      </div>
    `},
    { h:'Plant Organisation & Transport', content:`
      <ul>
        <li><strong>Xylem:</strong> carries water and mineral ions from roots → stems → leaves. Dead cells with lignified walls. Movement is by transpiration pull (passive).</li>
        <li><strong>Phloem:</strong> carries dissolved sugars (sucrose) from leaves to rest of plant. Living cells. Movement is called translocation (requires energy).</li>
        <li><strong>Transpiration:</strong> evaporation of water from leaves through stomata, pulling water up from roots. Rate increased by: higher temperature, lower humidity, more wind, more light.</li>
        <li><strong>Guard cells:</strong> control opening and closing of stomata. Swollen (turgid) = open; flaccid = closed.</li>
      </ul>
      <div class="required-practical">Use a potometer to measure transpiration rate under different conditions (light, wind, temperature, humidity).</div>
    `},
  ]
},

biology_evolution: {
  title:'Evolution & Classification',
  intro:'Evolution explains how all life on Earth descended from common ancestors through natural selection. Classification organises the diversity of life into a logical system.',
  sections:[
    { h:'Natural Selection', content:`
      <ul>
        <li>Within a species, individuals vary due to genetic mutations and sexual reproduction.</li>
        <li>Some variations are <strong>better adapted</strong> to the environment — these individuals survive, reproduce more, and pass on advantageous alleles.</li>
        <li>Over many generations, the frequency of advantageous alleles increases in the population.</li>
        <li>This is <strong>evolution by natural selection</strong> — the mechanism proposed by Darwin (1859).</li>
      </ul>
      <div class="exam-tip">Key phrase: "survival of the fittest" means survival of the best-adapted, not the strongest. "Fittest" = best fit to the environment.</div>
    `},
    { h:'Evidence for Evolution', content:`
      <ul>
        <li><strong>Fossil record:</strong> shows changes in organisms over time; transitional fossils link ancient and modern species. Gaps exist because soft tissue rarely fossilises.</li>
        <li><strong>Antibiotic resistance (observed evolution):</strong> bacteria with resistant mutations survive treatment, reproduce → resistant population. Direct, real-time evidence for natural selection.</li>
        <li><strong>Comparative anatomy:</strong> homologous structures (e.g. pentadactyl limb in mammals) suggest common ancestry.</li>
        <li><strong>DNA/protein comparisons:</strong> more similar DNA = more closely related. Chimpanzees share ~98% of human DNA.</li>
        <li><strong>Embryology:</strong> many vertebrate embryos look similar at early stages, suggesting shared ancestry.</li>
      </ul>
    `},
    { h:'Darwin vs Lamarck', content:`
      <table class="notes-table">
        <tr><th></th><th>Darwin (accepted)</th><th>Lamarck (rejected)</th></tr>
        <tr><td>Mechanism</td><td>Natural selection — random variation + differential survival</td><td>Inheritance of acquired characteristics</td></tr>
        <tr><td>Example</td><td>Giraffe: random mutations gave longer necks → better survival → more offspring</td><td>Giraffe stretched its neck → longer neck passed to offspring</td></tr>
        <tr><td>Why wrong/right?</td><td>Supported by genetics, fossil record, observed examples</td><td>Characteristics acquired in a lifetime cannot be inherited (DNA doesn't change this way)</td></tr>
      </table>
    `},
    { h:'Speciation', content:`
      <ul>
        <li>Speciation occurs when populations of the same species become <strong>reproductively isolated</strong> (e.g. by a geographical barrier).</li>
        <li>Different selection pressures act on each population → different mutations accumulate → populations diverge.</li>
        <li>Eventually, they can no longer interbreed to produce <strong>fertile offspring</strong> → they are now different species.</li>
        <li>Example: Darwin's finches on the Galapagos Islands — different islands, different food sources → different beak shapes evolved.</li>
      </ul>
    `},
    { h:'Classification', content:`
      <ul>
        <li><strong>Linnaeus</strong> developed the binomial naming system: each species has a two-part Latin name (Genus species), e.g. <em>Homo sapiens</em>.</li>
        <li>Classification hierarchy (largest → smallest): <strong>Domain → Kingdom → Phylum → Class → Order → Family → Genus → Species</strong>.</li>
        <li>Mnemonic: <em>Dear King Philip Came Over For Great Spaghetti.</em></li>
        <li>The <strong>three-domain system</strong> (Woese): Bacteria, Archaea, Eukarya. Based on molecular evidence (ribosomal RNA).</li>
        <li>The five kingdoms: Animals, Plants, Fungi, Protists, Prokaryotes.</li>
      </ul>
    `},
  ]
},

// ── CHEMISTRY MISSING NOTES ──────────────────────────────────

chemistry_chem_changes: {
  title:'Chemical Changes',
  intro:'This topic covers the reactivity series, acid reactions, salt formation, and oxidation-reduction — all core AQA content for Paper 1.',
  sections:[
    { h:'The Reactivity Series', content:`
      <div class="formula-box">K > Na > Li > Ca > Mg > Al > (C) > Zn > Fe > (H) > Cu > Ag > Au</div>
      <ul>
        <li>More reactive metals: react more vigorously with water and acids; harder to extract from ores; better reducing agents.</li>
        <li>Metals above hydrogen in the series react with dilute acids to produce a salt + hydrogen gas.</li>
        <li>Metals above carbon must be extracted by electrolysis (too reactive for carbon reduction).</li>
        <li>Metals below carbon are extracted by reduction with carbon (cheaper and easier).</li>
      </ul>
    `},
    { h:'Reactions of Acids', content:`
      <table class="notes-table">
        <tr><th>Reaction type</th><th>Equation pattern</th><th>Example</th></tr>
        <tr><td>Acid + metal</td><td>→ salt + hydrogen</td><td>Zn + H₂SO₄ → ZnSO₄ + H₂</td></tr>
        <tr><td>Acid + metal oxide</td><td>→ salt + water</td><td>CuO + 2HCl → CuCl₂ + H₂O</td></tr>
        <tr><td>Acid + metal hydroxide</td><td>→ salt + water</td><td>NaOH + HCl → NaCl + H₂O</td></tr>
        <tr><td>Acid + metal carbonate</td><td>→ salt + water + CO₂</td><td>CaCO₃ + 2HCl → CaCl₂ + H₂O + CO₂</td></tr>
        <tr><td>Acid + ammonia</td><td>→ ammonium salt</td><td>NH₃ + HNO₃ → NH₄NO₃</td></tr>
      </table>
      <div class="exam-tip">Salt name = metal name + acid ion. HCl → chloride; H₂SO₄ → sulfate; HNO₃ → nitrate; H₃PO₄ → phosphate.</div>
    `},
    { h:'pH and Neutralisation', content:`
      <ul>
        <li>pH measures hydrogen ion concentration. pH = −log[H⁺].</li>
        <li>pH &lt; 7 = acidic (excess H⁺); pH 7 = neutral; pH &gt; 7 = alkaline (excess OH⁻).</li>
        <li>Strong acids/bases fully dissociate (e.g. HCl → H⁺ + Cl⁻). Weak acids partially dissociate (e.g. CH₃COOH ⇌ H⁺ + CH₃COO⁻).</li>
        <li>Neutralisation: H⁺ + OH⁻ → H₂O</li>
        <li>Universal indicator gives a range of colours; a pH meter gives a precise numerical value.</li>
      </ul>
    `},
    { h:'Oxidation, Reduction & OIL RIG', content:`
      <ul>
        <li><strong>OIL RIG:</strong> Oxidation Is Loss (of electrons), Reduction Is Gain (of electrons).</li>
        <li>In terms of oxygen: oxidation = gain of oxygen; reduction = loss of oxygen.</li>
        <li><strong>Redox reactions</strong> involve both oxidation and reduction simultaneously.</li>
        <li><strong>Displacement reactions</strong> are redox reactions: the more reactive metal (reducing agent) loses electrons; the less reactive metal ion (oxidising agent) gains electrons.</li>
        <li>Example: Fe + CuSO₄ → FeSO₄ + Cu. Iron oxidised (loses 2e⁻), copper ions reduced (gain 2e⁻).</li>
      </ul>
      <div class="required-practical">Investigate reactions of metals with dilute acids to establish a reactivity series. Observe rate of bubbling and temperature change as indicators of reactivity.</div>
    `},
  ]
},

chemistry_electrolysis: {
  title:'Electrolysis',
  intro:'Electrolysis uses electrical energy to decompose ionic compounds. It is used industrially to extract reactive metals, purify copper, and make important chemicals from brine.',
  sections:[
    { h:'Principles of Electrolysis', content:`
      <ul>
        <li>Electrolysis requires a <strong>molten or dissolved ionic compound</strong> (electrolyte) with free-moving ions.</li>
        <li><strong>Cathode (−):</strong> cations (positive ions) are attracted → gain electrons → reduced. Metals or hydrogen are deposited.</li>
        <li><strong>Anode (+):</strong> anions (negative ions) are attracted → lose electrons → oxidised. Non-metals (or oxygen) are released.</li>
        <li><strong>CATS:</strong> Cathode = Anode = Positive. Cathode = negative. Remember: <em>reduction at cathode, oxidation at anode</em>.</li>
      </ul>
      <div class="formula-box">Cathode: cation + e⁻ → reduced product &nbsp;|&nbsp; Anode: anion − e⁻ → oxidised product</div>
    `},
    { h:'Electrolysis of Molten Ionic Compounds', content:`
      <ul>
        <li>Molten compounds (e.g. lead bromide, PbBr₂) have free ions that can migrate to electrodes.</li>
        <li>Cathode: Pb²⁺ + 2e⁻ → Pb (lead metal deposited).</li>
        <li>Anode: 2Br⁻ → Br₂ + 2e⁻ (bromine gas produced).</li>
        <li>This method is used to extract highly reactive metals (Na, Al, Ca) that cannot be reduced by carbon.</li>
      </ul>
    `},
    { h:'Electrolysis of Solutions — Discharge Order', content:`
      <ul>
        <li>When electrolysing aqueous solutions, water also provides H⁺ and OH⁻ ions, so there is competition at each electrode.</li>
        <li><strong>At cathode:</strong> if metal ion is BELOW hydrogen in reactivity series → metal deposited. If ABOVE hydrogen → hydrogen gas produced instead.</li>
        <li><strong>At anode:</strong> if halide ions (Cl⁻, Br⁻, I⁻) present → halogen gas produced. Otherwise → oxygen produced from OH⁻ ions.</li>
      </ul>
      <table class="notes-table">
        <tr><th>Electrolyte</th><th>Cathode product</th><th>Anode product</th></tr>
        <tr><td>Dilute H₂SO₄</td><td>Hydrogen (H₂)</td><td>Oxygen (O₂)</td></tr>
        <tr><td>CuSO₄(aq)</td><td>Copper (Cu)</td><td>Oxygen (O₂)</td></tr>
        <tr><td>Brine (NaCl aq)</td><td>Hydrogen (H₂)</td><td>Chlorine (Cl₂)</td></tr>
        <tr><td>CuSO₄ with Cu electrodes</td><td>Copper deposited</td><td>Copper dissolves</td></tr>
      </table>
    `},
    { h:'Industrial Electrolysis — Brine', content:`
      <ul>
        <li>Brine (saturated NaCl solution) → chlorine (Cl₂) at anode, hydrogen (H₂) at cathode, sodium hydroxide (NaOH) in solution.</li>
        <li><strong>Chlorine:</strong> making PVC, bleach, disinfectants, solvents.</li>
        <li><strong>Hydrogen:</strong> making margarine, ammonia (Haber process), fuel cells.</li>
        <li><strong>Sodium hydroxide:</strong> making soap, paper, ceramics, oven cleaners.</li>
      </ul>
    `},
    { h:'Copper Purification', content:`
      <ul>
        <li>Impure copper is used as the anode; pure copper is the cathode; copper sulfate solution is the electrolyte.</li>
        <li>Anode: Cu → Cu²⁺ + 2e⁻ (copper dissolves).</li>
        <li>Cathode: Cu²⁺ + 2e⁻ → Cu (pure copper deposits).</li>
        <li>Impurities fall off the anode as "anode sludge". The pure copper cathode grows.</li>
      </ul>
      <div class="required-practical">Electroplate a piece of metal with copper using copper sulfate solution. Measure mass of cathode before and after to calculate mass deposited.</div>
    `},
  ]
},

chemistry_energy_chem: {
  title:'Energy Changes in Reactions',
  intro:'All chemical reactions involve energy changes. Understanding exothermic and endothermic reactions, bond energies and reaction profiles is essential AQA content.',
  sections:[
    { h:'Exothermic vs Endothermic', content:`
      <table class="notes-table">
        <tr><th></th><th>Exothermic</th><th>Endothermic</th></tr>
        <tr><td>Energy change</td><td>Released to surroundings</td><td>Absorbed from surroundings</td></tr>
        <tr><td>Temperature change</td><td>Surroundings get hotter</td><td>Surroundings get colder</td></tr>
        <tr><td>ΔH value</td><td>Negative (−)</td><td>Positive (+)</td></tr>
        <tr><td>Products vs reactants</td><td>Products have LESS energy</td><td>Products have MORE energy</td></tr>
        <tr><td>Examples</td><td>Combustion, neutralisation, oxidation, respiration</td><td>Thermal decomposition, photosynthesis, dissolving ammonium nitrate</td></tr>
      </table>
    `},
    { h:'Reaction Profile Diagrams', content:`
      <ul>
        <li>Y-axis = energy. X-axis = reaction progress.</li>
        <li><strong>Activation energy:</strong> the minimum energy particles need to react — the "hump" above reactants on the diagram.</li>
        <li>A catalyst provides an alternative pathway with a <strong>lower activation energy</strong> — shown as a smaller hump on the diagram.</li>
        <li>Overall energy change (ΔH) = energy of products − energy of reactants.</li>
      </ul>
      <div class="exam-tip">On a reaction profile: if products are LOWER than reactants → exothermic (ΔH negative). If products are HIGHER → endothermic (ΔH positive).</div>
    `},
    { h:'Bond Energies', content:`
      <div class="formula-box">ΔH = Energy to break bonds − Energy released forming bonds</div>
      <ul>
        <li>Breaking bonds requires energy input (endothermic).</li>
        <li>Forming bonds releases energy (exothermic).</li>
        <li>If more energy is released (forming) than needed (breaking) → overall exothermic reaction.</li>
        <li>If more energy is needed (breaking) than released (forming) → overall endothermic reaction.</li>
      </ul>
      <div class="exam-tip">You will be given bond energy values in the exam. Add up all bonds broken (reactants) and all bonds formed (products), then subtract to find ΔH.</div>
    `},
    { h:'Fuel Cells', content:`
      <ul>
        <li>A fuel cell uses a continuous supply of fuel (usually hydrogen) and oxygen to produce electricity directly.</li>
        <li><strong>Hydrogen fuel cell:</strong> H₂ + ½O₂ → H₂O + electrical energy. Only by-product is water — very clean.</li>
        <li>More efficient than burning fuel in an engine (fewer energy conversion steps).</li>
        <li>Limitations: hydrogen storage, production cost, infrastructure, fuel cell durability.</li>
      </ul>
    `},
  ]
},

chemistry_organic: {
  title:'Organic Chemistry',
  intro:'Organic chemistry is the chemistry of carbon compounds. AQA covers hydrocarbons (alkanes, alkenes), reactions of carbon compounds, and polymers.',
  sections:[
    { h:'Crude Oil & Fractional Distillation', content:`
      <ul>
        <li>Crude oil is a <strong>mixture of hydrocarbons</strong> (mostly alkanes) formed from ancient marine organisms over millions of years.</li>
        <li><strong>Fractional distillation</strong> separates crude oil by boiling point. The fractionating column is hot at the bottom and cool at the top.</li>
        <li>Shorter carbon chains: lower boiling point, less viscous, more flammable, more volatile — collected near the top.</li>
        <li>Longer carbon chains: higher boiling point, more viscous, less flammable — collected near the bottom.</li>
      </ul>
      <table class="notes-table">
        <tr><th>Fraction</th><th>Carbon chain length</th><th>Uses</th></tr>
        <tr><td>Gases (LPG)</td><td>1–4 C</td><td>Heating, cooking</td></tr>
        <tr><td>Petrol</td><td>5–10 C</td><td>Car fuel</td></tr>
        <tr><td>Kerosene</td><td>10–16 C</td><td>Aviation fuel</td></tr>
        <tr><td>Diesel</td><td>15–25 C</td><td>Lorries, buses</td></tr>
        <tr><td>Fuel oil / bitumen</td><td>25–70+ C</td><td>Ships, road surfacing</td></tr>
      </table>
    `},
    { h:'Alkanes', content:`
      <div class="formula-box">General formula: CₙH₂ₙ₊₂ &nbsp;|&nbsp; All C–C single bonds (saturated)</div>
      <ul>
        <li>Methane (CH₄), Ethane (C₂H₆), Propane (C₃H₈), Butane (C₄H₁₀).</li>
        <li>Alkanes undergo <strong>combustion</strong>: complete → CO₂ + H₂O; incomplete (limited O₂) → CO + C (soot).</li>
        <li>Alkanes undergo <strong>substitution reactions</strong> with halogens in UV light: e.g. CH₄ + Cl₂ → CH₃Cl + HCl.</li>
      </ul>
    `},
    { h:'Alkenes', content:`
      <div class="formula-box">General formula: CₙH₂ₙ &nbsp;|&nbsp; C=C double bond (unsaturated)</div>
      <ul>
        <li>Ethene (C₂H₄), Propene (C₃H₆).</li>
        <li>Alkenes undergo <strong>addition reactions</strong> — the double bond opens to react with other molecules.</li>
        <li>Addition of H₂ (hydrogenation): alkene → alkane. Used to harden vegetable oils (making margarine).</li>
        <li>Addition of Br₂: decolourises orange bromine water → confirms C=C present. This is the test to distinguish alkenes from alkanes.</li>
        <li>Addition of H₂O (hydration): alkene + steam → alcohol. Conditions: 300°C, phosphoric acid catalyst.</li>
      </ul>
    `},
    { h:'Cracking', content:`
      <ul>
        <li>Cracking breaks large alkane molecules into smaller, more useful ones.</li>
        <li><strong>Thermal cracking:</strong> high temperature (450–750°C) and pressure.</li>
        <li><strong>Catalytic cracking:</strong> zeolite catalyst, lower temperature (~450°C).</li>
        <li>Products: shorter alkanes (fuels) + alkenes (used as monomers for plastics and in synthesis).</li>
        <li>Meets demand — there is more need for petrol and alkenes than for heavy fractions.</li>
      </ul>
    `},
    { h:'Alcohols & Carboxylic Acids', content:`
      <ul>
        <li><strong>Alcohols:</strong> contain –OH group. Methanol, ethanol, propanol. Used as fuels, solvents, in drinks.</li>
        <li>Ethanol production: fermentation (glucose + yeast → ethanol + CO₂, at ~30°C) OR hydration of ethene.</li>
        <li>Alcohols react with carboxylic acids to form <strong>esters</strong> (sweet smells, used in flavourings and perfumes).</li>
        <li><strong>Carboxylic acids:</strong> contain –COOH group. Ethanoic acid (vinegar). Weak acids. React with Na, Na₂CO₃, alcohols.</li>
      </ul>
    `},
    { h:'Polymers', content:`
      <ul>
        <li><strong>Addition polymerisation:</strong> alkene monomers join via their C=C bonds. e.g. n(CH₂=CH₂) → (–CH₂–CH₂–)ₙ (polyethene/polythene).</li>
        <li>Other addition polymers: polypropene (from propene), PVC (from chloroethene), PTFE (from tetrafluoroethene).</li>
        <li><strong>Condensation polymerisation:</strong> monomers join with loss of a small molecule (usually water or HCl). e.g. nylon (polyamide), polyester.</li>
        <li><strong>Disposing of polymers:</strong> landfill (non-biodegradable), incineration (produces CO₂/toxic gases), recycling (preferred), biodegradable polymers (new development).</li>
      </ul>
    `},
  ]
},

};

// ═══════════════════════════════════════════════════════════════
// NAVIGATION
// ═══════════════════════════════════════════════════════════════
function showScreen(id){
  document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
}

function goHome(){S.subject=null;showScreen('screen-home')}

function openSubject(subj){
  S.subject=subj;
  S.mode='quiz';
  const col=SUBJECTS[subj].color;
  const badge=document.getElementById('topic-badge');
  badge.textContent=subj.charAt(0).toUpperCase()+subj.slice(1);
  badge.style.color=col;badge.style.borderColor=col;badge.style.background=SUBJECTS[subj].dim;
  document.getElementById('topic-title').textContent='Choose a Topic';
  document.querySelectorAll('.mode-tab').forEach(t=>t.classList.remove('active'));
  document.getElementById('tab-quiz').classList.add('active');
  renderTopicList(subj);
  showScreen('screen-topics');
}

function switchMode(m){
  S.mode=m;
  document.querySelectorAll('.mode-tab').forEach(t=>t.classList.remove('active'));
  document.getElementById('tab-'+m).classList.add('active');
}

function backToTopics(){
  S.questions=[];S.qi=0;
  showScreen('screen-topics');
}

// ═══════════════════════════════════════════════════════════════
// TOPIC LIST
// ═══════════════════════════════════════════════════════════════
function renderTopicList(subj){
  const topics=SUBJECTS[subj].topics;
  const col=SUBJECTS[subj].color;
  const p1=topics.filter(t=>t.paper==='Paper 1');
  const p2=topics.filter(t=>t.paper==='Paper 2');
  let html='';
  [[p1,'Paper 1'],[p2,'Paper 2']].forEach(([ts,label])=>{
    if(!ts.length)return;
    html+=`<div class="topic-section"><div class="ts-label">${label}</div><div class="topic-grid">`;
    ts.forEach(t=>{
      const key=subj+'_'+t.id;
      const qcount=QB[key]?QB[key].length*4+'+ questions':'';
      html+=`<button class="topic-btn" style="--c-accent:${col}" onclick="pickTopic('${t.id}','${t.name}')">
        <div class="topic-btn-name">${t.name}</div>
        <div class="topic-btn-meta">${t.paper} · AQA</div>
        ${qcount?`<span class="q-count">${qcount}</span>`:''}
      </button>`;
    });
    html+='</div></div>';
  });
  document.getElementById('topic-list').innerHTML=html;
}

// ═══════════════════════════════════════════════════════════════
// START TOPIC
// ═══════════════════════════════════════════════════════════════
function pickTopic(id,name){
  S.topic={id,name};
  if(S.mode==='notes') showNotes();
  else startQuiz();
}

// ═══════════════════════════════════════════════════════════════
// QUIZ ENGINE
// ═══════════════════════════════════════════════════════════════
function buildQuestionSet(key,count=10){
  const pool=QB[key];
  if(!pool) return [];
  // Generate up to count questions by cycling generators with random values
  const qs=[];
  const rounds=Math.ceil(count/pool.length);
  for(let r=0;r<rounds;r++) pool.forEach(gen=>{if(qs.length<count) qs.push(gen())});
  return shuffle(qs).slice(0,count);
}

function startQuiz(){
  const key=S.subject+'_'+S.topic.id;
  const qs=buildQuestionSet(key,10);
  if(!qs.length){toast('No questions available for this topic yet.');return;}
  S.questions=qs;S.qi=0;S.sessionCorrect=0;S.sessionTotal=0;S.answered=false;
  const col=SUBJECTS[S.subject].color;
  document.getElementById('quiz-content').style.setProperty('--c-accent',col);
  document.getElementById('progress-fill').style.setProperty('background',col);
  document.getElementById('q-topic-name').textContent=S.topic.name;
  applyColor(col);
  showScreen('screen-quiz');
  renderQ();
}

function applyColor(col){
  document.querySelectorAll('.progress-fill').forEach(el=>el.style.background=col);
  document.getElementById('quiz-content').style.setProperty('--c-accent',col);
}

function renderQ(){
  const total=S.questions.length;
  const i=S.qi;
  const q=S.questions[i];
  const col=SUBJECTS[S.subject].color;
  document.getElementById('q-counter').textContent=`Q${i+1} / ${total}`;
  document.getElementById('progress-fill').style.width=((i/total)*100)+'%';
  document.getElementById('q-score-live').textContent=`✓ ${S.sessionCorrect}`;
  const letters=['A','B','C','D'];
  const opts=q.opts.map((o,idx)=>`
    <button class="opt-btn" onclick="pick(${idx})" id="o${idx}">
      <span class="opt-letter">${letters[idx]}</span><span>${o}</span>
    </button>`).join('');
  document.getElementById('quiz-content').innerHTML=`
    <div class="question-card">
      <div class="q-tag">${S.topic.name} · Q${i+1}</div>
      <div class="q-text">${q.q}</div>
      ${q.hint?`<div class="q-hint">💡 ${q.hint}</div>`:''}
    </div>
    <div class="options-grid">${opts}</div>
    <div class="explanation" id="exp">
      <span class="e-title">Explanation</span>${q.exp}
    </div>
    <div class="action-row">
      <button class="skip-btn show" id="skip-btn" onclick="skipQ()">Skip</button>
      <button class="next-btn" id="next-btn" onclick="nextQ()">${i===total-1?'See Results →':'Next →'}</button>
    </div>`;
  S.answered=false;
}

function pick(idx){
  if(S.answered)return;
  S.answered=true;
  const q=S.questions[S.qi];
  const correct=q.ans;
  const ok=idx===correct;
  document.querySelectorAll('.opt-btn').forEach(b=>b.disabled=true);
  document.getElementById('o'+idx).classList.add(ok?'correct':'wrong');
  if(!ok) document.getElementById('o'+correct).classList.add('correct');
  document.getElementById('exp').classList.add('show');
  document.getElementById('next-btn').classList.add('show');
  document.getElementById('skip-btn').classList.remove('show');
  S.sessionTotal++;
  if(ok){S.sessionCorrect++;S.totalScore+=10;S.streak++;}
  else{S.streak=0;}
  updateScore();
}

function skipQ(){nextQ();}

function nextQ(){
  S.qi++;
  if(S.qi>=S.questions.length) showResult();
  else renderQ();
}

function showResult(){
  const total=S.questions.length;
  const sc=S.sessionCorrect;
  const pct=Math.round((sc/total)*100);
  const col=SUBJECTS[S.subject].color;
  document.getElementById('progress-fill').style.width='100%';
  const emoji=sc===total?'🏆':pct>=70?'⭐':pct>=50?'📚':'💪';
  const msg=sc===total?'Flawless! You\'ve mastered this topic.':pct>=70?'Great work! Solid understanding.':pct>=50?'Good start — read the notes and retry.':'Keep going — every attempt builds knowledge.';
  document.getElementById('quiz-content').innerHTML=`
    <div class="result-card">
      <div class="result-emoji">${emoji}</div>
      <div class="result-score" style="color:${col}">${sc}/${total}</div>
      <div class="result-pct">${pct}% correct</div>
      <div class="result-msg">${msg}</div>
      <div class="result-breakdown">
        <div class="rb-item"><span class="rb-val" style="color:${col}">${S.totalScore}</span><div class="rb-label">Total Score</div></div>
        <div class="rb-item"><span class="rb-val" style="color:#f59e0b">${S.streak}🔥</span><div class="rb-label">Streak</div></div>
      </div>
      <div class="result-btns">
        <button class="btn-p" style="background:${col}" onclick="startQuiz()">Try Again</button>
        <button class="btn-s" onclick="S.topic.id&&showNotes()">Read Notes</button>
        <button class="btn-s" onclick="backToTopics()">Pick Topic</button>
      </div>
    </div>`;
}

// ═══════════════════════════════════════════════════════════════
// NOTES
// ═══════════════════════════════════════════════════════════════
function showNotes(){
  const key=S.subject+'_'+S.topic.id;
  const data=NOTES[key];
  const col=SUBJECTS[S.subject].color;
  const badge=document.getElementById('notes-badge');
  badge.textContent=S.topic.name;badge.style.color=col;badge.style.borderColor=col;badge.style.background=SUBJECTS[S.subject].dim;
  document.getElementById('notes-title').textContent=S.topic.name;
  if(!data){
    document.getElementById('notes-toc').innerHTML='';
    document.getElementById('notes-content').innerHTML=`<p style="color:var(--muted);padding:20px">Detailed notes for this topic are coming soon! Try the quiz in the meantime.</p>`;
    showScreen('screen-notes');return;
  }
  // TOC
  const tocLinks=data.sections.map((s,i)=>`<a class="toc-link" href="#ns${i}" style="--c-accent:${col}">${s.h}</a>`).join('');
  document.getElementById('notes-toc').innerHTML=`<div class="notes-toc-title">Contents</div><div class="notes-toc-links">${tocLinks}</div>`;
  // Content
  let html=`<h2>${data.title}</h2>${data.intro?`<div class="intro-text">${data.intro}</div>`:''}`;
  data.sections.forEach((s,i)=>{
    html+=`<div class="notes-section" id="ns${i}"><h3 style="--c-accent:${col}">${s.h}</h3>${s.content}</div>`;
  });
  document.getElementById('notes-content').innerHTML=html;
  // Style section headers with color
  document.querySelectorAll('.notes-section h3::before').forEach(el=>el.style.background=col);
  showScreen('screen-notes');
}

// ═══════════════════════════════════════════════════════════════
// SCORE
// ═══════════════════════════════════════════════════════════════
function updateScore(){
  document.getElementById('nav-score').textContent=S.totalScore;
  const sb=document.getElementById('nav-streak');
  if(S.streak>=2){sb.style.display='inline-flex';sb.textContent=S.streak+'🔥';}
  else sb.style.display='none';
}

function toast(msg){
  const t=document.createElement('div');
  t.className='toast';t.textContent=msg;
  document.body.appendChild(t);
  setTimeout(()=>t.remove(),3500);
}
</script>
</body>
</html>
