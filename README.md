<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Mohammad Jishan — Full-Stack Developer</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;600;700;800&family=Inter:wght@400;500;600;700&display=swap" rel="stylesheet">
<style>
  :root{
    --bg:#0d1117;
    --bg-elev:#11161d;
    --bg-card:#141a22;
    --border:#212833;
    --border-soft:#1a212b;
    --text:#e6e8ee;
    --muted:#7d8590;
    --comment:#525a6b;
    --purple:#c792ea;
    --green:#82e6c2;
    --blue:#82aaff;
    --orange:#f5a97f;
    --pink:#f297c7;
    --maxw:1100px;
  }

  *{margin:0;padding:0;box-sizing:border-box;}
  html{scroll-behavior:smooth;}
  body{
    background:var(--bg);
    color:var(--text);
    font-family:'Inter',sans-serif;
    overflow-x:hidden;
    position:relative;
  }
  ::selection{background:var(--purple);color:#0d1117;}
  ::-webkit-scrollbar{width:10px;}
  ::-webkit-scrollbar-track{background:var(--bg);}
  ::-webkit-scrollbar-thumb{background:var(--border);border-radius:10px;}
  ::-webkit-scrollbar-thumb:hover{background:var(--comment);}

  a{color:inherit;text-decoration:none;}
  :focus-visible{outline:2px solid var(--blue);outline-offset:3px;border-radius:4px;}

  .mono{font-family:'JetBrains Mono',monospace;}

  /* ---------- Ambient floating background ---------- */
  .floaters{
    position:fixed;inset:0;z-index:0;pointer-events:none;overflow:hidden;
  }
  .floaters span{
    position:absolute;
    font-family:'JetBrains Mono',monospace;
    color:var(--purple);
    opacity:.06;
    font-weight:700;
    animation:drift 22s ease-in-out infinite;
    user-select:none;
  }
  @keyframes drift{
    0%,100%{transform:translateY(0) rotate(0deg);}
    50%{transform:translateY(-40px) rotate(8deg);}
  }

  /* ---------- Top tab bar ---------- */
  .tabbar{
    position:fixed;top:0;left:0;right:0;z-index:50;
    background:rgba(13,17,23,.85);
    backdrop-filter:blur(10px);
    border-bottom:1px solid var(--border);
    display:flex;align-items:center;
    height:52px;
    padding:0 20px;
  }
  .tabbar .dots{display:flex;gap:7px;margin-right:18px;flex-shrink:0;}
  .tabbar .dots span{width:11px;height:11px;border-radius:50%;display:block;}
  .dots span:nth-child(1){background:#f5716c;}
  .dots span:nth-child(2){background:#f5b85b;}
  .dots span:nth-child(3){background:#6fd17a;}

  .tabs{display:flex;gap:2px;overflow-x:auto;flex:1;scrollbar-width:none;}
  .tabs::-webkit-scrollbar{display:none;}
  .tab{
    font-family:'JetBrains Mono',monospace;
    font-size:.78rem;
    color:var(--muted);
    padding:8px 16px;
    border-radius:6px 6px 0 0;
    white-space:nowrap;
    position:relative;
    transition:color .2s;
    cursor:pointer;
  }
  .tab:hover{color:var(--text);}
  .tab.active{color:var(--text);}
  .tab-indicator{
    position:absolute;bottom:-1px;height:2px;
    background:linear-gradient(90deg,var(--purple),var(--blue));
    border-radius:2px;
    transition:left .35s cubic-bezier(.65,0,.35,1), width .35s cubic-bezier(.65,0,.35,1);
  }

  section, header{
    position:relative;z-index:1;
    max-width:var(--maxw);
    margin:0 auto;
    padding:140px 28px 100px;
  }

  .eyebrow{
    font-family:'JetBrains Mono',monospace;
    font-size:.78rem;
    color:var(--comment);
    display:flex;align-items:center;gap:10px;
    margin-bottom:28px;
  }
  .eyebrow::before{content:'›';color:var(--green);font-weight:700;}
  .eyebrow .ext{color:var(--orange);}

  /* ---------- Hero ---------- */
  .hero{
    min-height:100vh;
    display:flex;flex-direction:column;justify-content:center;
    padding-top:90px;
  }
  .editor-window{
    border:1px solid var(--border);
    border-radius:12px;
    background:var(--bg-elev);
    box-shadow:0 30px 80px -30px rgba(130,170,255,.15), inset 0 0 0 1px rgba(255,255,255,.02);
    overflow:hidden;
  }
  .editor-titlebar{
    display:flex;align-items:center;gap:8px;
    padding:12px 16px;
    border-bottom:1px solid var(--border);
    background:var(--bg-card);
  }
  .editor-titlebar .dots span{width:10px;height:10px;border-radius:50%;display:inline-block;margin-right:6px;}
  .editor-titlebar .filename{
    margin-left:8px;font-family:'JetBrains Mono',monospace;font-size:.78rem;color:var(--muted);
  }
  .code-body{padding:28px 30px 34px;font-family:'JetBrains Mono',monospace;font-size:clamp(.95rem,2.6vw,1.25rem);line-height:1.95;}
  .code-line{
    display:block;white-space:nowrap;overflow:hidden;
    width:0;
    animation:typeline steps(40,end) forwards;
    animation-fill-mode:forwards;
  }
  @keyframes typeline{to{width:var(--w);}}
  .ln{display:inline-block;width:26px;color:var(--comment);user-select:none;}
  .kw{color:var(--purple);} .str{color:var(--green);} .fn{color:var(--blue);}
  .num{color:var(--orange);} .pn{color:var(--muted);} .prop{color:var(--pink);}
  .cursor{
    display:inline-block;width:9px;height:1.2em;background:var(--green);
    vertical-align:middle;margin-left:4px;
    animation:blink 1s step-end infinite;
  }
  @keyframes blink{50%{opacity:0;}}

  .hero-cta{display:flex;gap:14px;margin-top:36px;flex-wrap:wrap;opacity:0;animation:fadeUp .8s ease forwards;animation-delay:3.2s;}
  @keyframes fadeUp{from{opacity:0;transform:translateY(16px);}to{opacity:1;transform:translateY(0);}}
  .btn{
    font-family:'JetBrains Mono',monospace;font-size:.85rem;
    padding:13px 22px;border-radius:8px;
    border:1px solid var(--border);
    transition:transform .25s, border-color .25s, background .25s;
    display:inline-flex;align-items:center;gap:8px;
  }
  .btn-primary{background:linear-gradient(135deg,var(--purple),var(--blue));color:#0d1117;font-weight:700;border:none;}
  .btn-primary:hover{transform:translateY(-3px);box-shadow:0 12px 28px -8px rgba(130,170,255,.45);}
  .btn-ghost{color:var(--text);}
  .btn-ghost:hover{border-color:var(--comment);transform:translateY(-3px);background:var(--bg-card);}

  /* ---------- Reveal on scroll ---------- */
  .reveal{opacity:0;transform:translateY(28px);transition:opacity .7s ease, transform .7s ease;}
  .reveal.in{opacity:1;transform:translateY(0);}

  /* ---------- About ---------- */
  .about-grid{display:grid;grid-template-columns:1.1fr .9fr;gap:50px;align-items:start;}
  .about-grid p{color:var(--muted);font-size:1.05rem;line-height:1.85;margin-bottom:18px;}
  .about-grid strong{color:var(--text);font-weight:600;}
  .stat-block{
    border:1px solid var(--border);border-radius:10px;background:var(--bg-elev);
    padding:18px 20px;margin-bottom:12px;
  }
  .stat-block .n{font-family:'JetBrains Mono',monospace;font-size:1.5rem;color:var(--green);font-weight:700;}
  .stat-block .l{color:var(--muted);font-size:.85rem;margin-top:4px;}

  /* ---------- Skills (stack.json) ---------- */
  .json-block{
    font-family:'JetBrains Mono',monospace;font-size:.92rem;line-height:2;
    border:1px solid var(--border);border-radius:12px;background:var(--bg-elev);
    padding:30px 34px;overflow-x:auto;
  }
  .json-line{display:block;}
  .json-key{color:var(--pink);}
  .json-str{color:var(--green);}
  .json-punc{color:var(--muted);}
  .stagger{opacity:0;transform:translateX(-10px);transition:opacity .5s ease, transform .5s ease;}
  .stagger.in{opacity:1;transform:translateX(0);}

  /* ---------- Projects ---------- */
  .repo-grid{display:grid;grid-template-columns:repeat(2,1fr);gap:20px;}
  .repo-card{
    border:1px solid var(--border);border-radius:12px;background:var(--bg-elev);
    padding:24px 24px 22px;
    transition:transform .35s cubic-bezier(.2,.8,.2,1), border-color .35s, box-shadow .35s;
    position:relative;overflow:hidden;
  }
  .repo-card::before{
    content:'';position:absolute;inset:0;border-radius:12px;
    background:radial-gradient(400px circle at var(--mx,50%) var(--my,50%), rgba(130,170,255,.08), transparent 60%);
    opacity:0;transition:opacity .3s;pointer-events:none;
  }
  .repo-card:hover{transform:translateY(-6px);border-color:#2a3342;box-shadow:0 20px 45px -20px rgba(0,0,0,.6);}
  .repo-card:hover::before{opacity:1;}
  .repo-head{display:flex;align-items:center;gap:10px;margin-bottom:12px;}
  .repo-dot{width:8px;height:8px;border-radius:50%;background:var(--green);box-shadow:0 0 0 0 rgba(130,230,194,.5);animation:pulse 2.4s infinite;}
  @keyframes pulse{0%{box-shadow:0 0 0 0 rgba(130,230,194,.45);}70%{box-shadow:0 0 0 6px rgba(130,230,194,0);}100%{box-shadow:0 0 0 0 rgba(130,230,194,0);}}
  .repo-name{font-family:'JetBrains Mono',monospace;font-size:.95rem;font-weight:600;color:var(--text);}
  .repo-name .ext{color:var(--orange);font-weight:500;}
  .repo-desc{color:var(--muted);font-size:.9rem;line-height:1.6;margin-bottom:16px;}
  .repo-tags{display:flex;gap:7px;flex-wrap:wrap;}
  .repo-tags span{
    font-family:'JetBrains Mono',monospace;font-size:.72rem;color:var(--blue);
    background:rgba(130,170,255,.08);border:1px solid rgba(130,170,255,.18);
    padding:4px 9px;border-radius:6px;
  }

  /* ---------- Stats ---------- */
  .terminal-frame{
    border:1px solid var(--border);border-radius:12px;background:var(--bg-elev);overflow:hidden;
  }
  .terminal-frame .editor-titlebar .filename{color:var(--green);}
  .terminal-body{padding:26px;}
  .terminal-body .prompt{font-family:'JetBrains Mono',monospace;color:var(--comment);font-size:.85rem;margin-bottom:18px;}
  .terminal-body .prompt span{color:var(--green);}
  .stats-imgs{display:flex;flex-wrap:wrap;gap:18px;justify-content:center;}
  .stats-imgs img{max-width:100%;border-radius:8px;}
  .stats-imgs img.wide{width:100%;}

  /* ---------- Connect ---------- */
  .connect-grid{display:grid;grid-template-columns:1fr 1fr;gap:40px;align-items:start;}
  .term-line{font-family:'JetBrains Mono',monospace;font-size:.92rem;line-height:2.1;}
  .term-line .p1{color:var(--green);}
  .term-line .p2{color:var(--blue);}
  .term-line .out{color:var(--muted);}
  .flag-list a{
    display:flex;justify-content:space-between;align-items:center;
    font-family:'JetBrains Mono',monospace;font-size:.88rem;
    padding:11px 14px;border:1px solid var(--border);border-radius:8px;
    margin-bottom:8px;color:var(--muted);
    transition:border-color .25s, color .25s, transform .25s, background .25s;
  }
  .flag-list a:hover{border-color:var(--purple);color:var(--text);transform:translateX(6px);background:var(--bg-card);}
  .flag-list a .flag{color:var(--pink);}
  .flag-list a .arrow{opacity:0;transition:opacity .25s;color:var(--green);}
  .flag-list a:hover .arrow{opacity:1;}

  footer{
    border-top:1px solid var(--border);
    text-align:center;padding:40px 28px 50px;
    color:var(--comment);font-family:'JetBrains Mono',monospace;font-size:.82rem;
    position:relative;z-index:1;
  }
  footer .heart{color:var(--pink);}

  @media (max-width:860px){
    .about-grid, .connect-grid{grid-template-columns:1fr;}
    .repo-grid{grid-template-columns:1fr;}
    section, header{padding:120px 20px 70px;}
  }

  @media (prefers-reduced-motion: reduce){
    *{animation:none !important;transition:none !important;}
    .code-line{width:var(--w) !important;}
  }
</style>
</head>
<body>

<div class="floaters" aria-hidden="true">
  <span style="left:6%;top:18%;font-size:2.4rem;">{ }</span>
  <span style="left:88%;top:12%;font-size:1.6rem;animation-delay:-4s;">=&gt;</span>
  <span style="left:14%;top:62%;font-size:1.8rem;animation-delay:-8s;">&lt;/&gt;</span>
  <span style="left:80%;top:70%;font-size:2.1rem;animation-delay:-2s;">[ ]</span>
  <span style="left:48%;top:8%;font-size:1.4rem;animation-delay:-12s;">const</span>
  <span style="left:92%;top:45%;font-size:1.5rem;animation-delay:-6s;">01</span>
  <span style="left:3%;top:85%;font-size:1.5rem;animation-delay:-10s;">fn()</span>
  <span style="left:60%;top:90%;font-size:1.7rem;animation-delay:-15s;">&amp;&amp;</span>
</div>

<nav class="tabbar">
  <div class="dots"><span></span><span></span><span></span></div>
  <div class="tabs" id="tabs">
    <div class="tab active" data-target="home" data-tab>home.tsx</div>
    <div class="tab" data-target="about" data-tab>about.md</div>
    <div class="tab" data-target="skills" data-tab>stack.json</div>
    <div class="tab" data-target="projects" data-tab>work/</div>
    <div class="tab" data-target="stats" data-tab>stats.log</div>
    <div class="tab" data-target="connect" data-tab>connect.sh</div>
    <div class="tab-indicator" id="indicator"></div>
  </div>
</nav>

<!-- HERO -->
<header id="home" class="hero">
  <div class="editor-window">
    <div class="editor-titlebar">
      <div class="dots">
        <span style="background:#f5716c;"></span>
        <span style="background:#f5b85b;"></span>
        <span style="background:#6fd17a;"></span>
      </div>
      <span class="filename">home.tsx</span>
    </div>
    <div class="code-body">
      <span class="code-line" style="--w:11ch;animation-duration:.5s;animation-delay:.1s;"><span class="kw">const</span> <span class="prop">developer</span> <span class="pn">=</span> <span class="pn">{</span></span>
      <span class="code-line" style="--w:30ch;animation-duration:.7s;animation-delay:.6s;"><span class="ln"></span>&nbsp;&nbsp;<span class="prop">name</span><span class="pn">:</span> <span class="str">'Mohammad Jishan'</span><span class="pn">,</span></span>
      <span class="code-line" style="--w:34ch;animation-duration:.8s;animation-delay:1.3s;"><span class="ln"></span>&nbsp;&nbsp;<span class="prop">role</span><span class="pn">:</span> <span class="str">'Full-Stack Developer'</span><span class="pn">,</span></span>
      <span class="code-line" style="--w:48ch;animation-duration:1s;animation-delay:2.1s;"><span class="ln"></span>&nbsp;&nbsp;<span class="prop">stack</span><span class="pn">:</span> <span class="pn">[</span><span class="str">'Next.js'</span><span class="pn">,</span> <span class="str">'Node'</span><span class="pn">,</span> <span class="str">'AWS'</span><span class="pn">,</span> <span class="str">'AI'</span><span class="pn">]</span><span class="pn">,</span></span>
      <span class="code-line" style="--w:36ch;animation-duration:.8s;animation-delay:3.1s;"><span class="ln"></span>&nbsp;&nbsp;<span class="prop">shipped</span><span class="pn">:</span> <span class="num">100</span><span class="str">+ live projects</span><span class="pn">,</span></span>
      <span class="code-line" style="--w:30ch;animation-duration:.7s;animation-delay:3.9s;"><span class="ln"></span>&nbsp;&nbsp;<span class="prop">status</span><span class="pn">:</span> <span class="str">'open_to_work'</span></span>
      <span class="code-line" style="--w:3ch;animation-duration:.2s;animation-delay:4.6s;"><span class="pn">}</span><span class="cursor"></span></span>
    </div>
  </div>
  <div class="hero-cta">
    <a class="btn btn-primary" href="#projects">view work →</a>
    <a class="btn btn-ghost" href="#connect">say hi</a>
    <a class="btn btn-ghost" href="mailto:rzeesu@gmail.com">download cv</a>
  </div>
</header>

<!-- ABOUT -->
<section id="about">
  <div class="eyebrow">about<span class="ext">.md</span></div>
  <div class="about-grid">
    <div class="reveal">
      <p>I'm a <strong>Full-Stack Developer</strong> who builds modern web applications, AI-powered products, and scalable cloud solutions — currently shipping at <strong>Hodor Infosec</strong>.</p>
      <p>My day-to-day lives across <strong>Next.js, React and Node.js</strong>, with detours into AI integrations, AWS infrastructure, and the occasional Docker container that refuses to behave.</p>
      <p>I care a lot about clean code, performance, and building things people actually enjoy using — and I'm always tinkering with something new in a side project.</p>
    </div>
    <div class="reveal">
      <div class="stat-block"><div class="n">100+</div><div class="l">live websites shipped</div></div>
      <div class="stat-block"><div class="n">7</div><div class="l">featured products built solo</div></div>
      <div class="stat-block"><div class="n">∞</div><div class="l">tabs open in VS Code right now</div></div>
    </div>
  </div>
</section>

<!-- SKILLS -->
<section id="skills">
  <div class="eyebrow">stack<span class="ext">.json</span></div>
  <div class="json-block reveal">
<span class="json-line stagger">{</span>
<span class="json-line stagger">&nbsp;&nbsp;<span class="json-key">"languages"</span><span class="json-punc">:</span> [<span class="json-str">"JavaScript"</span>, <span class="json-str">"TypeScript"</span>, <span class="json-str">"Python"</span>, <span class="json-str">"C++"</span>, <span class="json-str">"C"</span>, <span class="json-str">"R"</span>],</span>
<span class="json-line stagger">&nbsp;&nbsp;<span class="json-key">"frontend"</span><span class="json-punc">:</span> [<span class="json-str">"Next.js"</span>, <span class="json-str">"React"</span>, <span class="json-str">"Tailwind"</span>, <span class="json-str">"GSAP"</span>, <span class="json-str">"shadcn/ui"</span>, <span class="json-str">"MUI"</span>],</span>
<span class="json-line stagger">&nbsp;&nbsp;<span class="json-key">"backend"</span><span class="json-punc">:</span> [<span class="json-str">"Node.js"</span>, <span class="json-str">"Express"</span>, <span class="json-str">"Socket.io"</span>, <span class="json-str">"RabbitMQ"</span>],</span>
<span class="json-line stagger">&nbsp;&nbsp;<span class="json-key">"database"</span><span class="json-punc">:</span> [<span class="json-str">"MongoDB"</span>, <span class="json-str">"PostgreSQL"</span>, <span class="json-str">"MySQL"</span>, <span class="json-str">"Supabase"</span>, <span class="json-str">"Redis"</span>, <span class="json-str">"Prisma"</span>],</span>
<span class="json-line stagger">&nbsp;&nbsp;<span class="json-key">"cloud"</span><span class="json-punc">:</span> [<span class="json-str">"AWS"</span>, <span class="json-str">"Docker"</span>, <span class="json-str">"Firebase"</span>, <span class="json-str">"Vercel"</span>],</span>
<span class="json-line stagger">&nbsp;&nbsp;<span class="json-key">"tools"</span><span class="json-punc">:</span> [<span class="json-str">"Git"</span>, <span class="json-str">"Figma"</span>, <span class="json-str">"Postman"</span>, <span class="json-str">"Jira"</span>]</span>
<span class="json-line stagger">}</span>
  </div>
</section>

<!-- PROJECTS -->
<section id="projects">
  <div class="eyebrow">work<span class="ext">/</span></div>
  <div class="repo-grid">

    <article class="repo-card reveal">
      <div class="repo-head"><span class="repo-dot"></span><span class="repo-name">zeesu-max<span class="ext">.stream</span></span></div>
      <p class="repo-desc">Online video streaming platform with movie info, ratings, and a responsive watch experience.</p>
      <div class="repo-tags"><span>Next.js</span><span>Node</span><span>Streaming</span></div>
    </article>

    <article class="repo-card reveal">
      <div class="repo-head"><span class="repo-dot"></span><span class="repo-name">zeesu-lib<span class="ext">.book</span></span></div>
      <p class="repo-desc">Online book store with PDF downloads and a built-in dictionary integration.</p>
      <div class="repo-tags"><span>React</span><span>PDF</span><span>E-commerce</span></div>
    </article>

    <article class="repo-card reveal">
      <div class="repo-head"><span class="repo-dot"></span><span class="repo-name">retouch<span class="ext">.photo</span></span></div>
      <p class="repo-desc">Real-time online photo editing application with filters and color grading.</p>
      <div class="repo-tags"><span>Canvas</span><span>Filters</span><span>Real-time</span></div>
    </article>

    <article class="repo-card reveal">
      <div class="repo-head"><span class="repo-dot"></span><span class="repo-name">zeesu-verse<span class="ext">.shop</span></span></div>
      <p class="repo-desc">Modern e-commerce platform with filtering, search, and cart management.</p>
      <div class="repo-tags"><span>Next.js</span><span>Stripe</span><span>Cart</span></div>
    </article>

    <article class="repo-card reveal">
      <div class="repo-head"><span class="repo-dot"></span><span class="repo-name">word-test<span class="ext">.type</span></span></div>
      <p class="repo-desc">Typing speed and accuracy testing platform with detailed analytics.</p>
      <div class="repo-tags"><span>JavaScript</span><span>Analytics</span></div>
    </article>

    <article class="repo-card reveal">
      <div class="repo-head"><span class="repo-dot"></span><span class="repo-name">ai-agent<span class="ext">.chat</span></span></div>
      <p class="repo-desc">Gemini-powered conversational AI agent with real-time responses.</p>
      <div class="repo-tags"><span>Gemini API</span><span>AI</span><span>Realtime</span></div>
    </article>

    <article class="repo-card reveal">
      <div class="repo-head"><span class="repo-dot"></span><span class="repo-name">ai-image<span class="ext">.gen</span></span></div>
      <p class="repo-desc">Generates AI images in multiple aspect ratios straight from text prompts.</p>
      <div class="repo-tags"><span>AI</span><span>Image Gen</span></div>
    </article>

  </div>
</section>

<!-- STATS -->
<section id="stats">
  <div class="eyebrow">stats<span class="ext">.log</span></div>
  <div class="terminal-frame reveal">
    <div class="editor-titlebar">
      <div class="dots">
        <span style="background:#f5716c;"></span>
        <span style="background:#f5b85b;"></span>
        <span style="background:#6fd17a;"></span>
      </div>
      <span class="filename">~/zeesu-royalist</span>
    </div>
    <div class="terminal-body">
      <div class="prompt"><span>$</span> git stats --user zeesu-royalist --verbose</div>
      <div class="stats-imgs">
        <img src="https://github-readme-stats.shion.dev/api?username=zeesu-royalist&show_icons=true&theme=tokyonight&hide_border=true&count_private=false" alt="GitHub stats" style="flex:1 1 320px;">
        <img src="https://github-readme-stats.shion.dev/api/top-langs/?username=zeesu-royalist&layout=compact&theme=tokyonight&hide_border=true" alt="Top languages" style="flex:1 1 280px;">
        <img class="wide" src="https://streak-stats.demolab.com?user=zeesu-royalist&theme=tokyonight&hide_border=true" alt="Streak stats">
        <img class="wide" src="https://github-profile-trophy.vercel.app/?username=zeesu-royalist&theme=tokyonight&no-frame=true&row=2&column=4" alt="Trophies">
        <img class="wide" src="https://github-readme-activity-graph.vercel.app/graph?username=zeesu-royalist&theme=tokyo-night&hide_border=true" alt="Activity graph">
      </div>
    </div>
  </div>
</section>

<!-- CONNECT -->
<section id="connect">
  <div class="eyebrow">connect<span class="ext">.sh</span></div>
  <div class="connect-grid">
    <div class="reveal">
      <div class="term-line"><span class="p1">$</span> whoami</div>
      <div class="term-line out">&gt; Mohammad Jishan — Full-Stack Developer</div>
      <div class="term-line" style="margin-top:14px;"><span class="p1">$</span> ./say-hello.sh</div>
      <div class="term-line out">&gt; Always up for a good build, a hard problem, or just a chat about code.</div>
      <a class="btn btn-primary" href="mailto:rzeesu@gmail.com" style="margin-top:24px;display:inline-flex;">rzeesu@gmail.com →</a>
    </div>
    <div class="reveal flag-list">
      <a href="mailto:rzeesu@gmail.com"><span><span class="flag">--email</span> rzeesu@gmail.com</span><span class="arrow">↗</span></a>
      <a href="https://linkedin.com/in/Mohammad-Jishan" target="_blank" rel="noopener"><span><span class="flag">--linkedin</span> /in/mohammad-jishan</span><span class="arrow">↗</span></a>
      <a href="https://x.com/zeesu_royalist" target="_blank" rel="noopener"><span><span class="flag">--x</span> @zeesu_royalist</span><span class="arrow">↗</span></a>
      <a href="https://discord.gg/zeesu_royalist" target="_blank" rel="noopener"><span><span class="flag">--discord</span> zeesu_royalist</span><span class="arrow">↗</span></a>
      <a href="https://instagram.com/zeesu_royalist" target="_blank" rel="noopener"><span><span class="flag">--instagram</span> @zeesu_royalist</span><span class="arrow">↗</span></a>
      <a href="https://facebook.com/zeesu_royalist" target="_blank" rel="noopener"><span><span class="flag">--facebook</span> zeesu_royalist</span><span class="arrow">↗</span></a>
      <a href="https://youtube.com/@zeesu_royalist" target="_blank" rel="noopener"><span><span class="flag">--youtube</span> @zeesu_royalist</span><span class="arrow">↗</span></a>
      <a href="https://reddit.com/user/zeesu_royalist" target="_blank" rel="noopener"><span><span class="flag">--reddit</span> u/zeesu_royalist</span><span class="arrow">↗</span></a>
      <a href="https://pinterest.com/zeesu_royalist" target="_blank" rel="noopener"><span><span class="flag">--pinterest</span> zeesu_royalist</span><span class="arrow">↗</span></a>
      <a href="https://stackoverflow.com/users/zeesu_royalist" target="_blank" rel="noopener"><span><span class="flag">--stackoverflow</span> zeesu_royalist</span><span class="arrow">↗</span></a>
      <a href="#" target="_blank" rel="noopener"><span><span class="flag">--portfolio</span> your-portfolio-link.com</span><span class="arrow">↗</span></a>
    </div>
  </div>
</section>

<footer>
  built with <span class="heart">♥</span> and way too much coffee — © 2026 Mohammad Jishan
</footer>

<script>
  // Scroll reveal
  const revealEls = document.querySelectorAll('.reveal');
  const staggerEls = document.querySelectorAll('.stagger');

  const io = new IntersectionObserver((entries)=>{
    entries.forEach(e=>{
      if(e.isIntersecting){ e.target.classList.add('in'); }
    });
  },{threshold:.15});
  revealEls.forEach(el=>io.observe(el));

  const ioStagger = new IntersectionObserver((entries)=>{
    entries.forEach(e=>{
      if(e.isIntersecting){
        const items = e.target.parentElement.querySelectorAll('.stagger');
        items.forEach((item,i)=> setTimeout(()=> item.classList.add('in'), i*90));
        ioStagger.unobserve(e.target);
      }
    });
  },{threshold:.2});
  if(staggerEls.length){ ioStagger.observe(staggerEls[0]); }

  // Active tab + sliding indicator
  const tabs = document.querySelectorAll('[data-tab]');
  const indicator = document.getElementById('indicator');
  const sections = [...tabs].map(t=>document.getElementById(t.dataset.target));

  function moveIndicator(tab){
    indicator.style.left = tab.offsetLeft + 'px';
    indicator.style.width = tab.offsetWidth + 'px';
  }
  moveIndicator(document.querySelector('.tab.active'));

  tabs.forEach(tab=>{
    tab.addEventListener('click', ()=>{
      document.getElementById(tab.dataset.target).scrollIntoView({behavior:'smooth'});
    });
  });

  const sectionObserver = new IntersectionObserver((entries)=>{
    entries.forEach(entry=>{
      if(entry.isIntersecting){
        const id = entry.target.id;
        tabs.forEach(t=>t.classList.remove('active'));
        const activeTab = document.querySelector('[data-target="'+id+'"]');
        if(activeTab){ activeTab.classList.add('active'); moveIndicator(activeTab); }
      }
    });
  },{threshold:.4, rootMargin:'-80px 0px -40% 0px'});
  sections.forEach(s=> s && sectionObserver.observe(s));

  window.addEventListener('resize', ()=> moveIndicator(document.querySelector('.tab.active')));

  // Cursor glow on repo cards
  document.querySelectorAll('.repo-card').forEach(card=>{
    card.addEventListener('mousemove', e=>{
      const rect = card.getBoundingClientRect();
      card.style.setProperty('--mx', (e.clientX-rect.left)+'px');
      card.style.setProperty('--my', (e.clientY-rect.top)+'px');
    });
  });
</script>

</body>
</html>
