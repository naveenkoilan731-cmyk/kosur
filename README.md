<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Alex Rivera — Portfolio</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Sans:ital,wght@0,300;0,400;0,500;1,300&display=swap" rel="stylesheet"/>
<style>
  /* ── RESET & VARIABLES ── */
  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  :root {
    --bg-grad: linear-gradient(135deg, #0d0821 0%, #1a0a3c 25%, #0a1a4a 55%, #0d1f5c 80%, #1a0d3c 100%);
    --mesh1: radial-gradient(ellipse at 20% 20%, rgba(120,60,220,0.45) 0%, transparent 55%);
    --mesh2: radial-gradient(ellipse at 80% 10%, rgba(40,100,255,0.35) 0%, transparent 50%);
    --mesh3: radial-gradient(ellipse at 60% 80%, rgba(80,40,200,0.3) 0%, transparent 45%);
    --mesh4: radial-gradient(ellipse at 10% 75%, rgba(20,80,220,0.25) 0%, transparent 40%);
    --glass-bg: rgba(255,255,255,0.06);
    --glass-border: rgba(255,255,255,0.15);
    --glass-shine: rgba(255,255,255,0.08);
    --blur: blur(18px);
    --text: #e8e4ff;
    --text-muted: rgba(200,190,255,0.65);
    --accent: #a78bfa;
    --accent2: #60a5fa;
    --white: #fff;
    --radius: 20px;
    --nav-h: 70px;
  }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'DM Sans', sans-serif;
    color: var(--text);
    min-height: 100vh;
    background: var(--bg-grad);
    overflow-x: hidden;
    position: relative;
  }

  /* ── ANIMATED MESH BACKGROUND ── */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background: var(--mesh1), var(--mesh2), var(--mesh3), var(--mesh4);
    pointer-events: none;
    z-index: 0;
    animation: meshFloat 12s ease-in-out infinite alternate;
  }

  @keyframes meshFloat {
    0%   { opacity: 0.8; transform: scale(1) translateY(0); }
    100% { opacity: 1;   transform: scale(1.05) translateY(-15px); }
  }

  /* Grain overlay */
  body::after {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 0;
    opacity: 0.4;
  }

  /* ── GLASS MIXIN (utility) ── */
  .glass {
    background: var(--glass-bg);
    backdrop-filter: var(--blur);
    -webkit-backdrop-filter: var(--blur);
    border: 1px solid var(--glass-border);
    border-radius: var(--radius);
    position: relative;
    overflow: hidden;
  }
  .glass::before {
    content: '';
    position: absolute;
    inset: 0;
    background: linear-gradient(135deg, var(--glass-shine) 0%, transparent 60%);
    pointer-events: none;
    border-radius: inherit;
  }

  /* ── NAVIGATION ── */
  nav {
    position: fixed;
    top: 0; left: 0; right: 0;
    height: var(--nav-h);
    z-index: 100;
    background: rgba(10,6,30,0.4);
    backdrop-filter: blur(24px);
    -webkit-backdrop-filter: blur(24px);
    border-bottom: 1px solid rgba(255,255,255,0.1);
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 clamp(1.5rem, 5vw, 4rem);
    animation: slideDown 0.6s ease both;
  }

  @keyframes slideDown {
    from { opacity:0; transform: translateY(-20px); }
    to   { opacity:1; transform: translateY(0); }
  }

  .nav-logo {
    font-family: 'Syne', sans-serif;
    font-weight: 800;
    font-size: 1.3rem;
    letter-spacing: -0.03em;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .nav-links {
    display: flex;
    gap: 2.5rem;
    list-style: none;
  }

  .nav-links a {
    color: var(--text-muted);
    text-decoration: none;
    font-size: 0.9rem;
    font-weight: 500;
    letter-spacing: 0.02em;
    transition: color 0.25s;
    position: relative;
  }
  .nav-links a::after {
    content: '';
    position: absolute;
    bottom: -4px; left: 0;
    width: 0; height: 1.5px;
    background: var(--accent);
    transition: width 0.3s ease;
  }
  .nav-links a:hover { color: var(--white); }
  .nav-links a:hover::after { width: 100%; }

  .nav-cta {
    background: linear-gradient(135deg, rgba(167,139,250,0.25), rgba(96,165,250,0.2));
    border: 1px solid rgba(167,139,250,0.4);
    color: var(--accent) !important;
    padding: 0.45rem 1.1rem;
    border-radius: 50px;
    transition: all 0.25s !important;
  }
  .nav-cta:hover {
    background: linear-gradient(135deg, rgba(167,139,250,0.4), rgba(96,165,250,0.35)) !important;
    color: #fff !important;
  }
  .nav-cta::after { display: none !important; }

  /* Hamburger */
  .nav-toggle {
    display: none;
    flex-direction: column;
    gap: 5px;
    cursor: pointer;
    padding: 4px;
  }
  .nav-toggle span {
    display: block;
    width: 22px; height: 2px;
    background: var(--text);
    border-radius: 2px;
    transition: all 0.3s;
  }

  /* ── MAIN WRAPPER ── */
  main {
    position: relative;
    z-index: 1;
    padding-top: var(--nav-h);
  }

  section {
    padding: clamp(3rem, 8vw, 7rem) clamp(1.5rem, 5vw, 4rem);
    max-width: 1200px;
    margin: 0 auto;
  }

  /* ── HERO ── */
  #hero {
    min-height: calc(100vh - var(--nav-h));
    display: flex;
    align-items: center;
    justify-content: center;
    text-align: center;
    flex-direction: column;
    gap: 2rem;
    padding-top: 3rem;
  }

  .hero-eyebrow {
    font-size: 0.8rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--accent2);
    font-weight: 500;
    animation: fadeUp 0.7s 0.2s ease both;
  }

  .hero-bio-card {
    max-width: 640px;
    padding: clamp(2rem, 5vw, 3.5rem);
    animation: fadeUp 0.7s 0.35s ease both;
  }

  .hero-avatar {
    width: 80px; height: 80px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    margin: 0 auto 1.5rem;
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'Syne', sans-serif;
    font-size: 1.8rem;
    font-weight: 800;
    color: #fff;
    box-shadow: 0 0 30px rgba(167,139,250,0.4);
  }

  .hero-name {
    font-family: 'Syne', sans-serif;
    font-size: clamp(2.2rem, 5vw, 3.4rem);
    font-weight: 800;
    letter-spacing: -0.04em;
    line-height: 1.1;
    margin-bottom: 0.6rem;
    background: linear-gradient(135deg, #fff 30%, var(--accent) 70%, var(--accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .hero-role {
    font-size: 1rem;
    color: var(--accent);
    font-weight: 500;
    margin-bottom: 1.2rem;
    letter-spacing: 0.03em;
  }

  .hero-desc {
    color: var(--text-muted);
    font-size: 1rem;
    line-height: 1.75;
    font-weight: 300;
    margin-bottom: 1.8rem;
  }

  .hero-tags {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
    justify-content: center;
    margin-bottom: 1.8rem;
  }

  .tag {
    font-size: 0.75rem;
    padding: 0.3rem 0.85rem;
    border-radius: 50px;
    background: rgba(167,139,250,0.12);
    border: 1px solid rgba(167,139,250,0.25);
    color: var(--accent);
    font-weight: 500;
    letter-spacing: 0.02em;
  }

  .hero-btns {
    display: flex;
    gap: 1rem;
    justify-content: center;
    flex-wrap: wrap;
  }

  .btn {
    padding: 0.7rem 1.8rem;
    border-radius: 50px;
    font-size: 0.9rem;
    font-weight: 500;
    cursor: pointer;
    text-decoration: none;
    transition: all 0.25s;
    font-family: 'DM Sans', sans-serif;
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    border: none;
  }

  .btn-primary {
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    color: #fff;
    box-shadow: 0 4px 20px rgba(167,139,250,0.35);
  }
  .btn-primary:hover {
    transform: translateY(-2px);
    box-shadow: 0 8px 30px rgba(167,139,250,0.5);
  }

  .btn-ghost {
    background: var(--glass-bg);
    backdrop-filter: var(--blur);
    border: 1px solid var(--glass-border);
    color: var(--text);
  }
  .btn-ghost:hover {
    background: rgba(255,255,255,0.1);
    transform: translateY(-2px);
  }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  /* ── SECTION HEADINGS ── */
  .section-label {
    font-size: 0.75rem;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--accent2);
    font-weight: 500;
    margin-bottom: 0.5rem;
  }
  .section-title {
    font-family: 'Syne', sans-serif;
    font-size: clamp(1.8rem, 4vw, 2.6rem);
    font-weight: 700;
    letter-spacing: -0.03em;
    margin-bottom: 0.6rem;
  }
  .section-sub {
    color: var(--text-muted);
    font-size: 1rem;
    font-weight: 300;
    max-width: 520px;
    line-height: 1.7;
    margin-bottom: 3rem;
  }

  /* ── PROJECTS GRID ── */
  #projects { max-width: 1200px; }

  .projects-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1.5rem;
  }

  .project-card {
    padding: 1.8rem;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
    cursor: default;
  }
  .project-card:hover {
    transform: translateY(-6px);
    box-shadow: 0 20px 50px rgba(0,0,0,0.4), 0 0 30px rgba(167,139,250,0.1);
    border-color: rgba(167,139,250,0.3);
  }

  .project-icon {
    width: 48px; height: 48px;
    border-radius: 12px;
    display: flex; align-items: center; justify-content: center;
    font-size: 1.3rem;
    margin-bottom: 1.2rem;
  }

  .project-title {
    font-family: 'Syne', sans-serif;
    font-size: 1.1rem;
    font-weight: 700;
    margin-bottom: 0.5rem;
    letter-spacing: -0.02em;
  }

  .project-desc {
    color: var(--text-muted);
    font-size: 0.88rem;
    line-height: 1.65;
    font-weight: 300;
    margin-bottom: 1.2rem;
  }

  .project-stack {
    display: flex;
    flex-wrap: wrap;
    gap: 0.4rem;
    margin-bottom: 1.2rem;
  }

  .stack-tag {
    font-size: 0.7rem;
    padding: 0.2rem 0.65rem;
    border-radius: 50px;
    background: rgba(96,165,250,0.1);
    border: 1px solid rgba(96,165,250,0.2);
    color: var(--accent2);
    font-weight: 500;
  }

  .project-link {
    font-size: 0.8rem;
    color: var(--accent);
    text-decoration: none;
    display: inline-flex;
    align-items: center;
    gap: 0.3rem;
    font-weight: 500;
    transition: gap 0.2s;
  }
  .project-link:hover { gap: 0.6rem; }

  /* ── SKILLS ── */
  #skills {
    max-width: 1200px;
  }

  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 1rem;
  }

  .skill-item {
    padding: 1.4rem 1.6rem;
  }

  .skill-name {
    font-size: 0.9rem;
    font-weight: 500;
    margin-bottom: 0.6rem;
    display: flex;
    justify-content: space-between;
  }

  .skill-name span:last-child {
    color: var(--accent);
    font-size: 0.8rem;
  }

  .skill-bar-track {
    height: 4px;
    background: rgba(255,255,255,0.08);
    border-radius: 2px;
    overflow: hidden;
  }

  .skill-bar-fill {
    height: 100%;
    border-radius: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    transform: scaleX(0);
    transform-origin: left;
    transition: transform 1s cubic-bezier(0.4,0,0.2,1);
  }

  /* ── CONTACT ── */
  #contact { max-width: 1200px; }

  .contact-card {
    padding: clamp(2.5rem, 5vw, 4rem);
    text-align: center;
    max-width: 580px;
    margin: 0 auto;
  }

  .contact-card h2 {
    font-family: 'Syne', sans-serif;
    font-size: clamp(1.8rem, 4vw, 2.4rem);
    font-weight: 700;
    margin-bottom: 1rem;
    letter-spacing: -0.03em;
    background: linear-gradient(135deg, #fff 40%, var(--accent));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .contact-card p {
    color: var(--text-muted);
    font-size: 1rem;
    font-weight: 300;
    line-height: 1.7;
    margin-bottom: 2rem;
  }

  .social-links {
    display: flex;
    gap: 1rem;
    justify-content: center;
    flex-wrap: wrap;
  }

  .social-link {
    padding: 0.5rem 1.2rem;
    border-radius: 50px;
    background: rgba(255,255,255,0.05);
    border: 1px solid rgba(255,255,255,0.12);
    color: var(--text-muted);
    text-decoration: none;
    font-size: 0.85rem;
    font-weight: 500;
    transition: all 0.25s;
    display: flex;
    align-items: center;
    gap: 0.4rem;
  }
  .social-link:hover {
    background: rgba(167,139,250,0.15);
    border-color: rgba(167,139,250,0.35);
    color: var(--accent);
    transform: translateY(-2px);
  }

  /* ── FOOTER ── */
  footer {
    position: relative;
    z-index: 1;
    text-align: center;
    padding: 2rem;
    color: var(--text-muted);
    font-size: 0.8rem;
    font-weight: 300;
    border-top: 1px solid rgba(255,255,255,0.06);
  }

  /* ── MOBILE MENU ── */
  .mobile-menu {
    display: none;
    position: fixed;
    top: var(--nav-h);
    left: 0; right: 0;
    background: rgba(10,6,30,0.92);
    backdrop-filter: blur(24px);
    z-index: 99;
    padding: 1.5rem;
    border-bottom: 1px solid rgba(255,255,255,0.08);
    flex-direction: column;
    gap: 1rem;
  }
  .mobile-menu.open { display: flex; }
  .mobile-menu a {
    color: var(--text-muted);
    text-decoration: none;
    font-size: 1rem;
    font-weight: 500;
    padding: 0.5rem 0;
    border-bottom: 1px solid rgba(255,255,255,0.05);
    transition: color 0.2s;
  }
  .mobile-menu a:hover { color: var(--white); }

  /* ── RESPONSIVE ── */
  @media (max-width: 900px) {
    .projects-grid {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media (max-width: 600px) {
    .nav-links { display: none; }
    .nav-toggle { display: flex; }

    .projects-grid {
      grid-template-columns: 1fr;
    }

    #hero {
      min-height: auto;
      padding-top: 4rem;
      padding-bottom: 3rem;
    }

    .hero-bio-card {
      padding: 1.8rem 1.5rem;
    }

    .btn { padding: 0.65rem 1.4rem; font-size: 0.85rem; }
  }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <div class="nav-logo">AR.</div>
  <ul class="nav-links">
    <li><a href="#hero">Home</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#skills">Skills</a></li>
    <li><a href="#contact" class="nav-cta">Contact ↗</a></li>
  </ul>
  <div class="nav-toggle" id="navToggle" onclick="toggleMenu()">
    <span></span><span></span><span></span>
  </div>
</nav>

<!-- MOBILE MENU -->
<div class="mobile-menu" id="mobileMenu">
  <a href="#hero" onclick="closeMenu()">Home</a>
  <a href="#projects" onclick="closeMenu()">Projects</a>
  <a href="#skills" onclick="closeMenu()">Skills</a>
  <a href="#contact" onclick="closeMenu()">Contact</a>
</div>

<main>
  <!-- HERO -->
  <section id="hero">
    <p class="hero-eyebrow">✦ Available for opportunities</p>

    <div class="glass hero-bio-card">
      <div class="hero-avatar">AR</div>
      <h1 class="hero-name">Alex Rivera</h1>
      <p class="hero-role">Full-Stack Developer & UI Designer</p>
      <p class="hero-desc">
        I craft beautiful, performant digital experiences — from pixel-perfect interfaces to scalable backend systems. Passionate about turning complex problems into elegant solutions.
      </p>
      <div class="hero-tags">
        <span class="tag">React</span>
        <span class="tag">Node.js</span>
        <span class="tag">TypeScript</span>
        <span class="tag">Figma</span>
        <span class="tag">AWS</span>
        <span class="tag">Python</span>
      </div>
      <div class="hero-btns">
        <a href="#projects" class="btn btn-primary">View Projects ↓</a>
        <a href="#contact" class="btn btn-ghost">Get in Touch</a>
      </div>
    </div>
  </section>

  <!-- PROJECTS -->
  <section id="projects">
    <p class="section-label">✦ Recent Work</p>
    <h2 class="section-title">Featured Projects</h2>
    <p class="section-sub">A selection of things I've built — from side projects to production apps.</p>

    <div class="projects-grid">
      <!-- Card 1 -->
      <div class="glass project-card">
        <div class="project-icon" style="background:rgba(167,139,250,0.15);">🛰️</div>
        <h3 class="project-title">Orbit Dashboard</h3>
        <p class="project-desc">Real-time satellite tracking dashboard with live telemetry visualization and alert management for orbital objects.</p>
        <div class="project-stack">
          <span class="stack-tag">React</span>
          <span class="stack-tag">D3.js</span>
          <span class="stack-tag">WebSocket</span>
        </div>
        <a href="#" class="project-link">View Project →</a>
      </div>

      <!-- Card 2 -->
      <div class="glass project-card">
        <div class="project-icon" style="background:rgba(96,165,250,0.15);">🧠</div>
        <h3 class="project-title">NeuralNote AI</h3>
        <p class="project-desc">AI-powered note-taking app that auto-summarizes, links related concepts, and surfaces forgotten ideas intelligently.</p>
        <div class="project-stack">
          <span class="stack-tag">Next.js</span>
          <span class="stack-tag">OpenAI API</span>
          <span class="stack-tag">PostgreSQL</span>
        </div>
        <a href="#" class="project-link">View Project →</a>
      </div>

      <!-- Card 3 -->
      <div class="glass project-card">
        <div class="project-icon" style="background:rgba(52,211,153,0.15);">🌿</div>
        <h3 class="project-title">EcoTrace</h3>
        <p class="project-desc">Carbon footprint tracker that connects to financial APIs and visualizes your spending's environmental impact over time.</p>
        <div class="project-stack">
          <span class="stack-tag">Vue 3</span>
          <span class="stack-tag">FastAPI</span>
          <span class="stack-tag">Plaid API</span>
        </div>
        <a href="#" class="project-link">View Project →</a>
      </div>

      <!-- Card 4 -->
      <div class="glass project-card">
        <div class="project-icon" style="background:rgba(251,191,36,0.12);">📡</div>
        <h3 class="project-title">Beacon CMS</h3>
        <p class="project-desc">Headless content management system with live collaboration, version history, and AI-assisted content generation.</p>
        <div class="project-stack">
          <span class="stack-tag">TypeScript</span>
          <span class="stack-tag">GraphQL</span>
          <span class="stack-tag">Redis</span>
        </div>
        <a href="#" class="project-link">View Project →</a>
      </div>

      <!-- Card 5 -->
      <div class="glass project-card">
        <div class="project-icon" style="background:rgba(244,114,182,0.12);">🎨</div>
        <h3 class="project-title">Palette Studio</h3>
        <p class="project-desc">Generative color palette tool using ML to extract harmonious palettes from any image or keyword input.</p>
        <div class="project-stack">
          <span class="stack-tag">Python</span>
          <span class="stack-tag">TensorFlow</span>
          <span class="stack-tag">Flask</span>
        </div>
        <a href="#" class="project-link">View Project →</a>
      </div>

      <!-- Card 6 -->
      <div class="glass project-card">
        <div class="project-icon" style="background:rgba(167,139,250,0.15);">⚡</div>
        <h3 class="project-title">Flowstate CLI</h3>
        <p class="project-desc">Developer productivity tool that monitors your coding sessions and provides focus insights and burnout prevention nudges.</p>
        <div class="project-stack">
          <span class="stack-tag">Rust</span>
          <span class="stack-tag">SQLite</span>
          <span class="stack-tag">Shell</span>
        </div>
        <a href="#" class="project-link">View Project →</a>
      </div>
    </div>
  </section>

  <!-- SKILLS -->
  <section id="skills">
    <p class="section-label">✦ Expertise</p>
    <h2 class="section-title">Skills & Tools</h2>
    <p class="section-sub">Technologies I work with daily, ranging from design to deployment.</p>

    <div class="skills-grid">
      <div class="glass skill-item">
        <div class="skill-name"><span>HTML & CSS</span><span>95%</span></div>
        <div class="skill-bar-track"><div class="skill-bar-fill" data-width="0.95"></div></div>
      </div>
      <div class="glass skill-item">
        <div class="skill-name"><span>JavaScript</span><span>90%</span></div>
        <div class="skill-bar-track"><div class="skill-bar-fill" data-width="0.90"></div></div>
      </div>
      <div class="glass skill-item">
        <div class="skill-name"><span>React / Next.js</span><span>88%</span></div>
        <div class="skill-bar-track"><div class="skill-bar-fill" data-width="0.88"></div></div>
      </div>
      <div class="glass skill-item">
        <div class="skill-name"><span>Node.js</span><span>82%</span></div>
        <div class="skill-bar-track"><div class="skill-bar-fill" data-width="0.82"></div></div>
      </div>
      <div class="glass skill-item">
        <div class="skill-name"><span>Python</span><span>80%</span></div>
        <div class="skill-bar-track"><div class="skill-bar-fill" data-width="0.80"></div></div>
      </div>
      <div class="glass skill-item">
        <div class="skill-name"><span>UI/UX Design</span><span>85%</span></div>
        <div class="skill-bar-track"><div class="skill-bar-fill" data-width="0.85"></div></div>
      </div>
    </div>
  </section>

  <!-- CONTACT -->
  <section id="contact" style="display:flex;justify-content:center;">
    <div class="glass contact-card">
      <h2>Let's Build Something</h2>
      <p>Open to freelance, full-time roles, and interesting collaborations. Don't hesitate to reach out — I'd love to chat.</p>
      <a href="mailto:alex@example.com" class="btn btn-primary" style="margin-bottom:1.5rem;display:inline-flex;">✉ Send a Message</a>
      <div class="social-links">
        <a href="#" class="social-link">⬛ GitHub</a>
        <a href="#" class="social-link">💼 LinkedIn</a>
        <a href="#" class="social-link">🐦 Twitter</a>
        <a href="#" class="social-link">🎨 Dribbble</a>
      </div>
    </div>
  </section>
</main>

<footer>
  <p>Designed & built by Alex Rivera · 2025 · Made with ❤️ and too much coffee</p>
</footer>

<script>
  // Mobile menu
  function toggleMenu() {
    document.getElementById('mobileMenu').classList.toggle('open');
  }
  function closeMenu() {
    document.getElementById('mobileMenu').classList.remove('open');
  }

  // Animate skill bars on scroll
  const bars = document.querySelectorAll('.skill-bar-fill');
  const observer = new IntersectionObserver(entries => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        const w = e.target.dataset.width;
        e.target.style.transform = `scaleX(${w})`;
      }
    });
  }, { threshold: 0.3 });
  bars.forEach(b => observer.observe(b));

  // Smooth active nav highlighting on scroll
  const sections = document.querySelectorAll('section[id]');
  const navLinks = document.querySelectorAll('.nav-links a');
  window.addEventListener('scroll', () => {
    let current = '';
    sections.forEach(s => {
      if (window.scrollY >= s.offsetTop - 120) current = s.id;
    });
    navLinks.forEach(a => {
      a.style.color = a.getAttribute('href') === '#' + current
        ? 'var(--white)' : '';
    });
  });
</script>
</body>
</html>
