<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Riswan Muhammed M S — Python Dev</title>
<link href="https://fonts.googleapis.com/css2?family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Bebas+Neue&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #050508;
    --surface: #0d0d14;
    --accent: #00ff9d;
    --accent2: #7b5fff;
    --accent3: #ff3d6e;
    --text: #e8e8f0;
    --muted: #5a5a7a;
    --border: rgba(255,255,255,0.07);
  }

  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'DM Sans', sans-serif;
    overflow-x: hidden;
    cursor: none;
  }

  /* CUSTOM CURSOR */
  .cursor {
    position: fixed; width: 12px; height: 12px;
    background: var(--accent); border-radius: 50%;
    pointer-events: none; z-index: 9999;
    transform: translate(-50%, -50%);
    transition: transform 0.1s, width 0.2s, height 0.2s, background 0.2s;
    mix-blend-mode: difference;
  }
  .cursor-ring {
    position: fixed; width: 40px; height: 40px;
    border: 1px solid var(--accent);
    border-radius: 50%; pointer-events: none; z-index: 9998;
    transform: translate(-50%, -50%);
    transition: transform 0.15s ease-out, width 0.3s, height 0.3s, opacity 0.3s;
    opacity: 0.5;
  }

  /* NOISE OVERLAY */
  body::before {
    content: '';
    position: fixed; inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.03'/%3E%3C/svg%3E");
    pointer-events: none; z-index: 1; opacity: 0.4;
  }

  /* HERO */
  .hero {
    min-height: 100vh;
    display: grid;
    grid-template-columns: 1fr 1fr;
    position: relative;
    overflow: hidden;
  }

  .hero-left {
    display: flex; flex-direction: column; justify-content: center;
    padding: 80px 60px;
    position: relative; z-index: 2;
  }

  .tag {
    display: inline-flex; align-items: center; gap: 8px;
    background: rgba(0,255,157,0.08);
    border: 1px solid rgba(0,255,157,0.2);
    color: var(--accent);
    font-family: 'Space Mono', monospace;
    font-size: 11px; letter-spacing: 2px;
    padding: 6px 14px; border-radius: 2px;
    margin-bottom: 32px;
    width: fit-content;
  }
  .tag::before { content: '●'; font-size: 8px; animation: blink 1.5s infinite; }
  @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

  .hero-name {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(64px, 8vw, 120px);
    line-height: 0.9;
    letter-spacing: 2px;
    margin-bottom: 24px;
  }
  .hero-name span {
    display: block;
    background: linear-gradient(135deg, #fff 0%, var(--accent) 60%, var(--accent2) 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
  }
  .hero-name .name-last {
    background: linear-gradient(135deg, var(--accent2) 0%, var(--accent3) 100%);
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .hero-bio {
    font-size: 16px; color: var(--muted); line-height: 1.7;
    max-width: 420px; margin-bottom: 48px;
  }
  .hero-bio strong { color: var(--accent); font-weight: 500; }

  .hero-links {
    display: flex; gap: 16px; flex-wrap: wrap;
  }

  .btn {
    font-family: 'Space Mono', monospace;
    font-size: 12px; letter-spacing: 1.5px; text-transform: uppercase;
    padding: 14px 28px; text-decoration: none;
    border-radius: 2px; transition: all 0.25s; cursor: none;
    display: inline-flex; align-items: center; gap: 8px;
  }
  .btn-primary {
    background: var(--accent); color: #000; font-weight: 700;
  }
  .btn-primary:hover { background: #fff; transform: translateY(-2px); box-shadow: 0 8px 30px rgba(0,255,157,0.3); }

  .btn-ghost {
    border: 1px solid var(--border); color: var(--text);
  }
  .btn-ghost:hover { border-color: var(--accent2); color: var(--accent2); transform: translateY(-2px); }

  /* HERO RIGHT — TERMINAL */
  .hero-right {
    display: flex; align-items: center; justify-content: center;
    padding: 80px 60px 80px 20px;
    position: relative; z-index: 2;
  }

  .terminal {
    width: 100%; max-width: 480px;
    background: #0a0a12; border: 1px solid var(--border);
    border-radius: 8px; overflow: hidden;
    box-shadow: 0 40px 80px rgba(0,0,0,0.6), 0 0 0 1px rgba(255,255,255,0.03);
    animation: float 6s ease-in-out infinite;
  }
  @keyframes float {
    0%,100% { transform: translateY(0) rotate(-0.5deg); }
    50% { transform: translateY(-12px) rotate(0.5deg); }
  }
  .terminal-bar {
    background: #141420; padding: 14px 18px;
    display: flex; align-items: center; gap: 8px;
    border-bottom: 1px solid var(--border);
  }
  .dot { width: 12px; height: 12px; border-radius: 50%; }
  .dot-r { background: #ff5f56; }
  .dot-y { background: #ffbd2e; }
  .dot-g { background: #27c93f; }
  .terminal-title {
    flex: 1; text-align: center;
    font-family: 'Space Mono', monospace; font-size: 11px; color: var(--muted);
  }
  .terminal-body {
    padding: 24px; font-family: 'Space Mono', monospace; font-size: 13px; line-height: 1.9;
  }
  .t-prompt { color: var(--accent2); }
  .t-cmd { color: var(--text); }
  .t-out { color: var(--muted); }
  .t-key { color: var(--accent); }
  .t-val { color: #ff9d6c; }
  .t-string { color: #c3e88d; }
  .t-cursor { display: inline-block; width: 8px; height: 14px; background: var(--accent); animation: blink 1s infinite; vertical-align: middle; }
  .t-comment { color: #3d4466; }

  /* GRID BG */
  .hero::after {
    content: '';
    position: absolute; inset: 0;
    background-image:
      linear-gradient(rgba(0,255,157,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,255,157,0.03) 1px, transparent 1px);
    background-size: 60px 60px;
    pointer-events: none;
  }

  /* GLOW ORBS */
  .orb {
    position: absolute; border-radius: 50%;
    filter: blur(80px); pointer-events: none;
  }
  .orb1 { width: 500px; height: 500px; background: rgba(123,95,255,0.12); top: -100px; right: 10%; }
  .orb2 { width: 300px; height: 300px; background: rgba(0,255,157,0.08); bottom: 10%; left: 5%; }
  .orb3 { width: 200px; height: 200px; background: rgba(255,61,110,0.08); top: 30%; left: 40%; }

  /* MARQUEE */
  .marquee-wrap {
    border-top: 1px solid var(--border); border-bottom: 1px solid var(--border);
    overflow: hidden; padding: 16px 0; background: var(--surface);
    position: relative; z-index: 2;
  }
  .marquee-track {
    display: flex; gap: 60px; white-space: nowrap;
    animation: marquee 30s linear infinite;
  }
  .marquee-item {
    font-family: 'Space Mono', monospace; font-size: 12px;
    letter-spacing: 3px; color: var(--muted); text-transform: uppercase;
    display: flex; align-items: center; gap: 16px;
  }
  .marquee-item::before { content: '◆'; color: var(--accent); font-size: 8px; }
  @keyframes marquee { from { transform: translateX(0); } to { transform: translateX(-50%); } }

  /* SECTIONS */
  section { position: relative; z-index: 2; }

  .section-label {
    font-family: 'Space Mono', monospace;
    font-size: 10px; letter-spacing: 4px; text-transform: uppercase;
    color: var(--accent); margin-bottom: 16px;
    display: flex; align-items: center; gap: 12px;
  }
  .section-label::before { content: '//'; color: var(--muted); }

  .section-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(40px, 5vw, 72px);
    line-height: 1; margin-bottom: 60px; color: var(--text);
    letter-spacing: 1px;
  }

  /* ABOUT */
  .about {
    padding: 120px 80px;
    display: grid; grid-template-columns: 1fr 1fr; gap: 80px;
    align-items: center;
    border-bottom: 1px solid var(--border);
  }

  .about-stats {
    display: grid; grid-template-columns: 1fr 1fr; gap: 2px;
  }
  .stat-card {
    background: var(--surface); padding: 32px;
    border: 1px solid var(--border);
    position: relative; overflow: hidden;
    transition: border-color 0.3s;
  }
  .stat-card:hover { border-color: var(--accent); }
  .stat-card::before {
    content: ''; position: absolute; top: 0; left: 0; right: 0; height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    transform: scaleX(0); transform-origin: left;
    transition: transform 0.4s;
  }
  .stat-card:hover::before { transform: scaleX(1); }
  .stat-num {
    font-family: 'Bebas Neue', sans-serif; font-size: 56px;
    color: var(--accent); line-height: 1;
  }
  .stat-label {
    font-family: 'Space Mono', monospace; font-size: 11px;
    color: var(--muted); letter-spacing: 2px; text-transform: uppercase;
    margin-top: 8px;
  }

  .about-text p {
    color: var(--muted); line-height: 1.8; margin-bottom: 20px; font-size: 15px;
  }
  .about-text p strong { color: var(--text); font-weight: 500; }

  .focus-list {
    margin-top: 32px; display: flex; flex-direction: column; gap: 12px;
  }
  .focus-item {
    display: flex; align-items: center; gap: 16px;
    font-family: 'Space Mono', monospace; font-size: 12px;
    padding: 12px 16px; border: 1px solid var(--border);
    border-radius: 2px; transition: all 0.3s; cursor: none;
  }
  .focus-item:hover { border-color: var(--accent2); background: rgba(123,95,255,0.05); }
  .focus-icon { font-size: 16px; }
  .focus-text { color: var(--text); }
  .focus-sub { color: var(--muted); font-size: 10px; margin-top: 2px; }

  /* SKILLS */
  .skills-section {
    padding: 120px 80px;
    border-bottom: 1px solid var(--border);
  }

  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(90px, 1fr));
    gap: 12px;
  }

  .skill-pill {
    display: flex; flex-direction: column; align-items: center; gap: 10px;
    padding: 20px 12px;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 4px;
    transition: all 0.3s;
    cursor: none;
    position: relative;
    overflow: hidden;
  }
  .skill-pill::after {
    content: ''; position: absolute; inset: 0;
    background: radial-gradient(circle at center, rgba(0,255,157,0.08), transparent 70%);
    opacity: 0; transition: opacity 0.3s;
  }
  .skill-pill:hover { border-color: var(--accent); transform: translateY(-4px); box-shadow: 0 12px 40px rgba(0,0,0,0.4); }
  .skill-pill:hover::after { opacity: 1; }
  .skill-pill img { width: 36px; height: 36px; filter: grayscale(30%); transition: filter 0.3s; }
  .skill-pill:hover img { filter: grayscale(0) drop-shadow(0 0 8px rgba(0,255,157,0.4)); }
  .skill-name { font-family: 'Space Mono', monospace; font-size: 9px; color: var(--muted); text-align: center; letter-spacing: 1px; }

  /* PROJECTS */
  .projects-section {
    padding: 120px 80px;
    border-bottom: 1px solid var(--border);
  }

  .projects-grid {
    display: grid; grid-template-columns: 1fr 1fr; gap: 2px;
  }

  .project-card {
    background: var(--surface); padding: 48px;
    border: 1px solid var(--border);
    position: relative; overflow: hidden;
    transition: all 0.3s; cursor: none;
    group: true;
  }
  .project-card:hover { border-color: rgba(123,95,255,0.4); }
  .project-card::before {
    content: ''; position: absolute; inset: 0;
    background: linear-gradient(135deg, rgba(123,95,255,0.05), transparent);
    opacity: 0; transition: opacity 0.4s;
  }
  .project-card:hover::before { opacity: 1; }

  .project-num {
    font-family: 'Bebas Neue', sans-serif; font-size: 80px;
    color: rgba(255,255,255,0.04); position: absolute;
    top: 20px; right: 30px; line-height: 1; pointer-events: none;
    transition: color 0.3s;
  }
  .project-card:hover .project-num { color: rgba(123,95,255,0.12); }

  .project-tag {
    font-family: 'Space Mono', monospace; font-size: 10px;
    color: var(--accent2); letter-spacing: 2px; text-transform: uppercase;
    margin-bottom: 16px;
  }

  .project-title {
    font-family: 'Bebas Neue', sans-serif; font-size: 36px;
    margin-bottom: 16px; color: var(--text); letter-spacing: 1px;
  }

  .project-desc {
    color: var(--muted); font-size: 14px; line-height: 1.7; margin-bottom: 28px;
  }

  .project-stack {
    display: flex; gap: 8px; flex-wrap: wrap; margin-bottom: 32px;
  }
  .stack-tag {
    font-family: 'Space Mono', monospace; font-size: 10px;
    padding: 4px 10px; border: 1px solid var(--border);
    color: var(--muted); letter-spacing: 1px;
    border-radius: 2px;
  }

  .project-link {
    font-family: 'Space Mono', monospace; font-size: 11px;
    color: var(--accent); text-decoration: none; letter-spacing: 2px;
    text-transform: uppercase; display: inline-flex; align-items: center; gap: 8px;
    transition: gap 0.3s;
  }
  .project-link:hover { gap: 14px; }

  /* CONTACT */
  .contact-section {
    padding: 120px 80px;
    display: grid; grid-template-columns: 1fr 1fr; gap: 80px;
    align-items: center;
  }

  .contact-email {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(28px, 3vw, 42px);
    color: var(--text); margin-bottom: 32px;
    letter-spacing: 1px;
  }
  .contact-email a {
    color: var(--accent); text-decoration: none;
    transition: color 0.3s;
    display: block;
  }
  .contact-email a:hover { color: var(--accent2); }

  .social-links { display: flex; gap: 16px; }
  .social-link {
    display: flex; align-items: center; gap: 12px;
    padding: 14px 24px;
    border: 1px solid var(--border);
    text-decoration: none; color: var(--text);
    font-family: 'Space Mono', monospace; font-size: 12px;
    letter-spacing: 1.5px; text-transform: uppercase;
    transition: all 0.3s; border-radius: 2px;
    cursor: none;
  }
  .social-link:hover { border-color: var(--accent); color: var(--accent); transform: translateY(-2px); }

  .contact-graphic {
    display: flex; align-items: center; justify-content: center;
  }

  /* ANIMATED RING */
  .ring-wrap { position: relative; width: 300px; height: 300px; }
  .ring {
    position: absolute; border-radius: 50%; border: 1px solid;
    animation: spin linear infinite;
  }
  .ring1 { inset: 0; border-color: rgba(0,255,157,0.2); animation-duration: 20s; }
  .ring2 { inset: 20px; border-color: rgba(123,95,255,0.3); animation-duration: 15s; animation-direction: reverse; }
  .ring3 { inset: 50px; border-color: rgba(255,61,110,0.2); animation-duration: 10s; }
  .ring-center {
    position: absolute; inset: 0; display: flex;
    align-items: center; justify-content: center;
    flex-direction: column; text-align: center;
  }
  .ring-text {
    font-family: 'Bebas Neue', sans-serif; font-size: 48px;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text; -webkit-text-fill-color: transparent;
    background-clip: text;
  }
  .ring-sub {
    font-family: 'Space Mono', monospace; font-size: 10px;
    color: var(--muted); letter-spacing: 3px; text-transform: uppercase;
  }
  @keyframes spin { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }

  .ring1::after, .ring2::after {
    content: '◆'; position: absolute; top: -6px; left: calc(50% - 5px);
    font-size: 10px; color: var(--accent); background: var(--bg); padding: 0 2px;
  }
  .ring2::after { color: var(--accent2); top: auto; bottom: -6px; }

  /* FOOTER */
  footer {
    padding: 40px 80px;
    border-top: 1px solid var(--border);
    display: flex; justify-content: space-between; align-items: center;
    position: relative; z-index: 2;
  }
  .footer-name {
    font-family: 'Bebas Neue', sans-serif; font-size: 20px;
    color: var(--muted); letter-spacing: 2px;
  }
  .footer-copy {
    font-family: 'Space Mono', monospace; font-size: 11px;
    color: var(--muted);
  }

  /* SCROLL ANIMATIONS */
  .fade-up {
    opacity: 0; transform: translateY(40px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .fade-up.visible { opacity: 1; transform: translateY(0); }

  /* RESPONSIVE */
  @media (max-width: 900px) {
    .hero { grid-template-columns: 1fr; }
    .hero-right { display: none; }
    .about, .contact-section { grid-template-columns: 1fr; }
    .projects-grid { grid-template-columns: 1fr; }
    .about { padding: 80px 24px; }
    .skills-section, .projects-section, .contact-section { padding: 80px 24px; }
    .hero-left { padding: 60px 24px; }
    footer { padding: 30px 24px; flex-direction: column; gap: 16px; text-align: center; }
  }
</style>
</head>
<body>

<!-- CURSORS -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- HERO -->
<section class="hero">
  <div class="orb orb1"></div>
  <div class="orb orb2"></div>
  <div class="orb orb3"></div>

  <div class="hero-left">
    <div class="tag">Available for collaboration</div>
    <h1 class="hero-name">
      <span>Riswan</span>
      <span>Muhammed</span>
      <span class="name-last">M S</span>
    </h1>
    <p class="hero-bio">
      <strong>Python Developer</strong> obsessed with building
      <strong>Agentic Systems</strong> and <strong>Generative AI</strong> at the frontier.
      Currently crafting <strong>OSAGENT</strong> — an autonomous intelligence layer for the OS.
    </p>
    <div class="hero-links">
      <a href="mailto:riswanmuhammedxa@gmail.com" class="btn btn-primary">↗ Get in touch</a>
      <a href="https://github.com/rixprog" target="_blank" class="btn btn-ghost">⌥ GitHub</a>
      <a href="https://linkedin.com/in/riswanmuhammedms" target="_blank" class="btn btn-ghost">in LinkedIn</a>
    </div>
  </div>

  <div class="hero-right">
    <div class="terminal">
      <div class="terminal-bar">
        <div class="dot dot-r"></div>
        <div class="dot dot-y"></div>
        <div class="dot dot-g"></div>
        <div class="terminal-title">riswan@osagent ~ zsh</div>
      </div>
      <div class="terminal-body">
        <div><span class="t-prompt">➜ ~</span> <span class="t-cmd">cat developer.json</span></div>
        <div class="t-comment"># Fetching profile...</div>
        <br>
        <div><span class="t-out">{</span></div>
        <div>&nbsp;&nbsp;<span class="t-key">"name"</span><span class="t-out">:</span> <span class="t-string">"Riswan Muhammed M S"</span><span class="t-out">,</span></div>
        <div>&nbsp;&nbsp;<span class="t-key">"role"</span><span class="t-out">:</span> <span class="t-string">"Python Developer"</span><span class="t-out">,</span></div>
        <div>&nbsp;&nbsp;<span class="t-key">"focus"</span><span class="t-out">:</span> <span class="t-string">"Agentic Systems"</span><span class="t-out">,</span></div>
        <div>&nbsp;&nbsp;<span class="t-key">"current"</span><span class="t-out">:</span> <span class="t-string">"OSAGENT"</span><span class="t-out">,</span></div>
        <div>&nbsp;&nbsp;<span class="t-key">"learning"</span><span class="t-out">: [</span></div>
        <div>&nbsp;&nbsp;&nbsp;&nbsp;<span class="t-val">"LLM Orchestration"</span><span class="t-out">,</span></div>
        <div>&nbsp;&nbsp;&nbsp;&nbsp;<span class="t-val">"Multi-Agent Frameworks"</span><span class="t-out">,</span></div>
        <div>&nbsp;&nbsp;&nbsp;&nbsp;<span class="t-val">"RAG Pipelines"</span></div>
        <div>&nbsp;&nbsp;<span class="t-out">],</span></div>
        <div>&nbsp;&nbsp;<span class="t-key">"open_to"</span><span class="t-out">:</span> <span class="t-string">"GenAI Collabs"</span></div>
        <div><span class="t-out">}</span></div>
        <br>
        <div><span class="t-prompt">➜ ~</span> <span class="t-cursor"></span></div>
      </div>
    </div>
  </div>
</section>

<!-- MARQUEE -->
<div class="marquee-wrap">
  <div class="marquee-track" id="marqueeTrack">
    <span class="marquee-item">Python</span>
    <span class="marquee-item">Agentic AI</span>
    <span class="marquee-item">LLM Systems</span>
    <span class="marquee-item">Django</span>
    <span class="marquee-item">AWS</span>
    <span class="marquee-item">React</span>
    <span class="marquee-item">Multi-Agent</span>
    <span class="marquee-item">Flask</span>
    <span class="marquee-item">TypeScript</span>
    <span class="marquee-item">RAG</span>
    <span class="marquee-item">Node.js</span>
    <span class="marquee-item">Linux</span>
    <span class="marquee-item">Python</span>
    <span class="marquee-item">Agentic AI</span>
    <span class="marquee-item">LLM Systems</span>
    <span class="marquee-item">Django</span>
    <span class="marquee-item">AWS</span>
    <span class="marquee-item">React</span>
    <span class="marquee-item">Multi-Agent</span>
    <span class="marquee-item">Flask</span>
    <span class="marquee-item">TypeScript</span>
    <span class="marquee-item">RAG</span>
    <span class="marquee-item">Node.js</span>
    <span class="marquee-item">Linux</span>
  </div>
</div>

<!-- ABOUT -->
<section class="about">
  <div class="about-text fade-up">
    <div class="section-label">About</div>
    <div class="section-title">Hacker.<br>Builder.<br>Dreamer.</div>
    <p>I'm a Python developer from Kerala, India, currently obsessed with the frontier of <strong>agentic AI</strong>. I believe the next generation of software will think, plan, and act — and I'm building toward that future.</p>
    <p>When I'm not shipping code, I'm researching multi-agent architectures, autonomous task execution, and the emerging design patterns of agentic systems. My current project <strong>OSAGENT</strong> is my love letter to the idea of truly intelligent computing.</p>

    <div class="focus-list">
      <div class="focus-item">
        <span class="focus-icon">🤖</span>
        <div>
          <div class="focus-text">Agentic Systems</div>
          <div class="focus-sub">Currently learning · OSAGENT project</div>
        </div>
      </div>
      <div class="focus-item">
        <span class="focus-icon">🧬</span>
        <div>
          <div class="focus-text">Generative AI</div>
          <div class="focus-sub">Open to collaborate · LLM pipelines</div>
        </div>
      </div>
      <div class="focus-item">
        <span class="focus-icon">🌐</span>
        <div>
          <div class="focus-text">Full-Stack Python</div>
          <div class="focus-sub">Django · Flask · REST APIs</div>
        </div>
      </div>
    </div>
  </div>

  <div class="about-stats fade-up">
    <div class="stat-card">
      <div class="stat-num">∞</div>
      <div class="stat-label">Ideas shipped</div>
    </div>
    <div class="stat-card">
      <div class="stat-num">20+</div>
      <div class="stat-label">Tools mastered</div>
    </div>
    <div class="stat-card">
      <div class="stat-num">3</div>
      <div class="stat-label">Cloud platforms</div>
    </div>
    <div class="stat-card">
      <div class="stat-num">01</div>
      <div class="stat-label">Mission: AGI</div>
    </div>
  </div>
</section>

<!-- SKILLS -->
<section class="skills-section">
  <div class="section-label">Skills</div>
  <div class="section-title">The Toolkit</div>
  <div class="skills-grid" id="skillsGrid">
    <!-- Populated by JS -->
  </div>
</section>

<!-- PROJECTS -->
<section class="projects-section">
  <div class="section-label">Projects</div>
  <div class="section-title">What I'm Building</div>
  <div class="projects-grid">

    <div class="project-card fade-up">
      <div class="project-num">01</div>
      <div class="project-tag">Active · 2024–2025</div>
      <div class="project-title">OSAGENT</div>
      <p class="project-desc">An autonomous intelligence layer that lets AI agents control and operate an entire operating system. Built with multi-agent orchestration, tool use, and real-time OS interaction.</p>
      <div class="project-stack">
        <span class="stack-tag">Python</span>
        <span class="stack-tag">LLM</span>
        <span class="stack-tag">Multi-Agent</span>
        <span class="stack-tag">Linux</span>
        <span class="stack-tag">Bash</span>
      </div>
      <a href="https://github.com/rixprog" target="_blank" class="project-link">View on GitHub →</a>
    </div>

    <div class="project-card fade-up">
      <div class="project-num">02</div>
      <div class="project-tag">Generative AI · Collab Open</div>
      <div class="project-title">GenAI Pipelines</div>
      <p class="project-desc">RAG architectures, LLM orchestration, and agentic workflow systems. Building modular, production-ready pipelines for intelligent automation at scale.</p>
      <div class="project-stack">
        <span class="stack-tag">Python</span>
        <span class="stack-tag">RAG</span>
        <span class="stack-tag">LangChain</span>
        <span class="stack-tag">AWS</span>
        <span class="stack-tag">GCP</span>
      </div>
      <a href="mailto:riswanmuhammedxa@gmail.com" class="project-link">Collaborate →</a>
    </div>

    <div class="project-card fade-up">
      <div class="project-num">03</div>
      <div class="project-tag">Full Stack · Web</div>
      <div class="project-title">Web Systems</div>
      <p class="project-desc">Full-stack applications with Django and Flask backends, React frontends, and robust database architectures. From MVPs to production-grade deployments.</p>
      <div class="project-stack">
        <span class="stack-tag">Django</span>
        <span class="stack-tag">React</span>
        <span class="stack-tag">MySQL</span>
        <span class="stack-tag">TypeScript</span>
        <span class="stack-tag">Express</span>
      </div>
      <a href="https://github.com/rixprog" target="_blank" class="project-link">View GitHub →</a>
    </div>

    <div class="project-card fade-up">
      <div class="project-num">04</div>
      <div class="project-tag">IoT · Embedded</div>
      <div class="project-title">Hardware + Code</div>
      <p class="project-desc">Arduino-powered hardware projects blending embedded systems with cloud connectivity. Bridging the gap between the physical world and intelligent software.</p>
      <div class="project-stack">
        <span class="stack-tag">Arduino</span>
        <span class="stack-tag">Python</span>
        <span class="stack-tag">AWS IoT</span>
        <span class="stack-tag">Selenium</span>
      </div>
      <a href="https://github.com/rixprog" target="_blank" class="project-link">Explore →</a>
    </div>

  </div>
</section>

<!-- CONTACT -->
<section class="contact-section">
  <div class="fade-up">
    <div class="section-label">Contact</div>
    <div class="section-title">Let's Build<br>Something<br>Wild.</div>
    <div class="contact-email">
      <a href="mailto:riswanmuhammedxa@gmail.com">riswanmuhammedxa<br>@gmail.com</a>
    </div>
    <div class="social-links">
      <a href="https://github.com/rixprog" target="_blank" class="social-link">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0 0 24 12c0-6.63-5.37-12-12-12z"/></svg>
        GitHub
      </a>
      <a href="https://linkedin.com/in/riswanmuhammedms" target="_blank" class="social-link">
        <svg width="16" height="16" viewBox="0 0 24 24" fill="currentColor"><path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433a2.062 2.062 0 0 1-2.063-2.065 2.064 2.064 0 1 1 2.063 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/></svg>
        LinkedIn
      </a>
    </div>
  </div>

  <div class="contact-graphic fade-up">
    <div class="ring-wrap">
      <div class="ring ring1"></div>
      <div class="ring ring2"></div>
      <div class="ring ring3"></div>
      <div class="ring-center">
        <div class="ring-text">Open<br>to Work</div>
        <div class="ring-sub">Kerala, India</div>
      </div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-name">Riswan Muhammed M S</div>
  <div class="footer-copy">© 2025 · Built with intent · riswanmuhammedxa@gmail.com</div>
</footer>

<script>
  // CURSOR
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;

  document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; });

  function animCursor() {
    cursor.style.left = mx + 'px'; cursor.style.top = my + 'px';
    rx += (mx - rx) * 0.12; ry += (my - ry) * 0.12;
    ring.style.left = rx + 'px'; ring.style.top = ry + 'px';
    requestAnimationFrame(animCursor);
  }
  animCursor();

  document.querySelectorAll('a, button, .skill-pill, .project-card, .stat-card, .focus-item').forEach(el => {
    el.addEventListener('mouseenter', () => {
      cursor.style.width = '20px'; cursor.style.height = '20px';
      ring.style.width = '60px'; ring.style.height = '60px';
    });
    el.addEventListener('mouseleave', () => {
      cursor.style.width = '12px'; cursor.style.height = '12px';
      ring.style.width = '40px'; ring.style.height = '40px';
    });
  });

  // SKILLS
  const skills = [
    { name: 'Python', img: 'https://skillicons.dev/icons?i=py' },
    { name: 'Django', img: 'https://skillicons.dev/icons?i=django' },
    { name: 'Flask', img: 'https://skillicons.dev/icons?i=flask' },
    { name: 'React', img: 'https://skillicons.dev/icons?i=react' },
    { name: 'TypeScript', img: 'https://skillicons.dev/icons?i=ts' },
    { name: 'JavaScript', img: 'https://skillicons.dev/icons?i=js' },
    { name: 'Node.js', img: 'https://skillicons.dev/icons?i=nodejs' },
    { name: 'Express', img: 'https://skillicons.dev/icons?i=express' },
    { name: 'AWS', img: 'https://skillicons.dev/icons?i=aws' },
    { name: 'GCP', img: 'https://skillicons.dev/icons?i=gcp' },
    { name: 'Azure', img: 'https://skillicons.dev/icons?i=azure' },
    { name: 'Linux', img: 'https://skillicons.dev/icons?i=linux' },
    { name: 'Bash', img: 'https://skillicons.dev/icons?i=bash' },
    { name: 'Git', img: 'https://skillicons.dev/icons?i=git' },
    { name: 'MySQL', img: 'https://skillicons.dev/icons?i=mysql' },
    { name: 'HTML', img: 'https://skillicons.dev/icons?i=html' },
    { name: 'CSS', img: 'https://skillicons.dev/icons?i=css' },
    { name: 'Selenium', img: 'https://skillicons.dev/icons?i=selenium' },
    { name: 'Arduino', img: 'https://skillicons.dev/icons?i=arduino' },
    { name: 'Zapier', img: 'https://cdn.simpleicons.org/zapier/FF4A00' },
  ];

  const grid = document.getElementById('skillsGrid');
  skills.forEach((s, i) => {
    const el = document.createElement('div');
    el.className = 'skill-pill fade-up';
    el.style.transitionDelay = (i * 40) + 'ms';
    el.innerHTML = `<img src="${s.img}" alt="${s.name}" /><span class="skill-name">${s.name}</span>`;
    grid.appendChild(el);
  });

  // SCROLL ANIMATIONS
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); });
  }, { threshold: 0.1 });

  document.querySelectorAll('.fade-up').forEach(el => observer.observe(el));
</script>
</body>
</html>
