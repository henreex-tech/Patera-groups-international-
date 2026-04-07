<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Patera Group International</title>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:wght@300;400;600;700&family=Montserrat:wght@300;400;500;600&display=swap" rel="stylesheet"/>
<style>
  :root {
    --gold: #C9A84C;
    --gold-light: #E8C96A;
    --gold-dark: #8B6914;
    --black: #0A0A0A;
    --black-2: #111111;
    --black-3: #1A1A1A;
    --white: #F5F0E8;
    --gray: #888;
  }

  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--black);
    color: var(--white);
    font-family: 'Montserrat', sans-serif;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    width: 12px; height: 12px;
    background: var(--gold);
    border-radius: 50%;
    position: fixed;
    pointer-events: none;
    z-index: 9999;
    transition: transform 0.15s ease;
    transform: translate(-50%, -50%);
  }
  .cursor-ring {
    width: 36px; height: 36px;
    border: 1px solid var(--gold);
    border-radius: 50%;
    position: fixed;
    pointer-events: none;
    z-index: 9998;
    transition: transform 0.3s ease, width 0.3s, height 0.3s;
    transform: translate(-50%, -50%);
    opacity: 0.5;
  }

  /* NAV */
  nav {
    position: fixed; top: 0; left: 0; right: 0;
    z-index: 100;
    padding: 24px 48px;
    display: flex; justify-content: space-between; align-items: center;
    background: linear-gradient(to bottom, rgba(10,10,10,0.95), transparent);
  }
  .nav-logo {
    font-family: 'Cormorant Garamond', serif;
    font-size: 20px;
    font-weight: 600;
    letter-spacing: 4px;
    color: var(--gold);
    text-transform: uppercase;
  }
  .nav-links {
    display: flex; gap: 40px; list-style: none;
  }
  .nav-links a {
    color: var(--white);
    text-decoration: none;
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    opacity: 0.7;
    transition: opacity 0.3s, color 0.3s;
  }
  .nav-links a:hover { opacity: 1; color: var(--gold); }

  /* HERO */
  .hero {
    min-height: 100vh;
    display: flex; align-items: center; justify-content: center;
    position: relative;
    overflow: hidden;
    padding: 120px 48px 80px;
  }

  .hero-bg {
    position: absolute; inset: 0;
    background:
      radial-gradient(ellipse 60% 60% at 70% 50%, rgba(201,168,76,0.08) 0%, transparent 70%),
      radial-gradient(ellipse 40% 40% at 20% 80%, rgba(201,168,76,0.05) 0%, transparent 60%),
      var(--black);
  }

  /* Gold grain texture overlay */
  .hero-bg::after {
    content: '';
    position: absolute; inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.03'/%3E%3C/svg%3E");
    opacity: 0.4;
    pointer-events: none;
  }

  .hero-line {
    position: absolute;
    left: 0; right: 0;
    height: 1px;
    background: linear-gradient(to right, transparent, var(--gold), transparent);
    opacity: 0.2;
  }
  .hero-line.top { top: 120px; }
  .hero-line.bottom { bottom: 80px; }

  .hero-content {
    position: relative; z-index: 2;
    text-align: center;
    max-width: 900px;
  }

  .hero-tag {
    font-size: 10px;
    letter-spacing: 5px;
    color: var(--gold);
    text-transform: uppercase;
    margin-bottom: 32px;
    opacity: 0;
    animation: fadeUp 1s 0.3s forwards;
  }

  .hero-title {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(56px, 10vw, 120px);
    font-weight: 300;
    line-height: 0.9;
    letter-spacing: -2px;
    margin-bottom: 24px;
    opacity: 0;
    animation: fadeUp 1s 0.5s forwards;
  }

  .hero-title span {
    color: var(--gold);
    font-style: italic;
  }

  .hero-sub {
    font-size: 11px;
    letter-spacing: 6px;
    text-transform: uppercase;
    color: var(--gray);
    margin-bottom: 48px;
    opacity: 0;
    animation: fadeUp 1s 0.7s forwards;
  }

  .hero-divider {
    width: 60px; height: 1px;
    background: var(--gold);
    margin: 0 auto 48px;
    opacity: 0;
    animation: fadeUp 1s 0.9s forwards;
  }

  .hero-desc {
    font-size: 13px;
    line-height: 2;
    color: rgba(245,240,232,0.6);
    max-width: 560px;
    margin: 0 auto 56px;
    font-weight: 300;
    opacity: 0;
    animation: fadeUp 1s 1.1s forwards;
  }

  .hero-cta {
    display: inline-flex; gap: 16px;
    opacity: 0;
    animation: fadeUp 1s 1.3s forwards;
  }

  .btn-primary {
    padding: 16px 40px;
    background: var(--gold);
    color: var(--black);
    text-decoration: none;
    font-size: 10px;
    letter-spacing: 3px;
    text-transform: uppercase;
    font-weight: 600;
    transition: background 0.3s, transform 0.3s;
  }
  .btn-primary:hover { background: var(--gold-light); transform: translateY(-2px); }

  .btn-outline {
    padding: 16px 40px;
    border: 1px solid var(--gold);
    color: var(--gold);
    text-decoration: none;
    font-size: 10px;
    letter-spacing: 3px;
    text-transform: uppercase;
    font-weight: 500;
    transition: background 0.3s, color 0.3s, transform 0.3s;
  }
  .btn-outline:hover { background: var(--gold); color: var(--black); transform: translateY(-2px); }

  /* SECTORS */
  .sectors {
    padding: 120px 48px;
    position: relative;
  }

  .section-header {
    text-align: center;
    margin-bottom: 80px;
  }

  .section-tag {
    font-size: 10px;
    letter-spacing: 5px;
    color: var(--gold);
    text-transform: uppercase;
    margin-bottom: 20px;
    display: block;
  }

  .section-title {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(36px, 5vw, 64px);
    font-weight: 300;
    line-height: 1.1;
  }

  .section-title em { color: var(--gold); font-style: italic; }

  .sectors-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 2px;
    max-width: 1200px;
    margin: 0 auto;
  }

  .sector-card {
    background: var(--black-2);
    padding: 56px 40px;
    position: relative;
    overflow: hidden;
    transition: background 0.4s;
    cursor: none;
  }

  .sector-card::before {
    content: '';
    position: absolute;
    bottom: 0; left: 0; right: 0;
    height: 2px;
    background: var(--gold);
    transform: scaleX(0);
    transition: transform 0.4s;
    transform-origin: left;
  }

  .sector-card:hover { background: var(--black-3); }
  .sector-card:hover::before { transform: scaleX(1); }

  .sector-number {
    font-family: 'Cormorant Garamond', serif;
    font-size: 72px;
    font-weight: 300;
    color: rgba(201,168,76,0.08);
    position: absolute;
    top: 16px; right: 24px;
    line-height: 1;
    transition: color 0.4s;
  }
  .sector-card:hover .sector-number { color: rgba(201,168,76,0.15); }

  .sector-icon {
    font-size: 28px;
    margin-bottom: 24px;
    display: block;
  }

  .sector-name {
    font-family: 'Cormorant Garamond', serif;
    font-size: 28px;
    font-weight: 600;
    color: var(--gold);
    margin-bottom: 16px;
  }

  .sector-desc {
    font-size: 12px;
    line-height: 1.9;
    color: rgba(245,240,232,0.5);
    font-weight: 300;
  }

  /* VISION */
  .vision {
    padding: 120px 48px;
    background: var(--black-2);
    position: relative;
    overflow: hidden;
  }

  .vision::before {
    content: 'PATERA';
    position: absolute;
    font-family: 'Cormorant Garamond', serif;
    font-size: 200px;
    font-weight: 700;
    color: rgba(201,168,76,0.03);
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    letter-spacing: 20px;
    white-space: nowrap;
    pointer-events: none;
  }

  .vision-inner {
    max-width: 800px;
    margin: 0 auto;
    text-align: center;
    position: relative; z-index: 2;
  }

  .vision-quote {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(28px, 4vw, 52px);
    font-weight: 300;
    line-height: 1.4;
    margin-bottom: 40px;
  }

  .vision-quote em { color: var(--gold); font-style: italic; }

  .vision-attr {
    font-size: 10px;
    letter-spacing: 4px;
    color: var(--gold);
    text-transform: uppercase;
  }

  /* STATS */
  .stats {
    padding: 100px 48px;
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 2px;
    max-width: 1200px;
    margin: 0 auto;
  }

  .stat-item {
    text-align: center;
    padding: 60px 32px;
    background: var(--black-2);
    position: relative;
  }

  .stat-item::after {
    content: '';
    position: absolute;
    top: 24px; bottom: 24px;
    right: 0;
    width: 1px;
    background: rgba(201,168,76,0.1);
  }
  .stat-item:last-child::after { display: none; }

  .stat-number {
    font-family: 'Cormorant Garamond', serif;
    font-size: 64px;
    font-weight: 300;
    color: var(--gold);
    line-height: 1;
    margin-bottom: 12px;
  }

  .stat-label {
    font-size: 10px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--gray);
  }

  /* CHALLENGE */
  .challenge {
    padding: 120px 48px;
    background: var(--black-3);
    position: relative;
  }

  .challenge-inner {
    max-width: 1100px;
    margin: 0 auto;
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 80px;
    align-items: center;
  }

  .challenge-left h2 {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(36px, 4vw, 56px);
    font-weight: 300;
    margin-bottom: 24px;
    line-height: 1.1;
  }
  .challenge-left h2 em { color: var(--gold); font-style: italic; }

  .challenge-left p {
    font-size: 13px;
    line-height: 2;
    color: rgba(245,240,232,0.6);
    margin-bottom: 32px;
    font-weight: 300;
  }

  .progress-wrap {
    margin-bottom: 32px;
  }

  .progress-header {
    display: flex; justify-content: space-between;
    margin-bottom: 12px;
    font-size: 11px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--gray);
  }

  .progress-bar {
    height: 2px;
    background: rgba(201,168,76,0.15);
    position: relative;
  }

  .progress-fill {
    height: 100%;
    background: linear-gradient(to right, var(--gold-dark), var(--gold-light));
    width: 3%;
    transition: width 2s ease;
    position: relative;
  }

  .progress-fill::after {
    content: '';
    position: absolute;
    right: 0; top: 50%;
    transform: translate(50%, -50%);
    width: 8px; height: 8px;
    background: var(--gold);
    border-radius: 50%;
  }

  .challenge-right {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 2px;
  }

  .challenge-stat {
    background: var(--black-2);
    padding: 40px 28px;
    text-align: center;
  }

  .challenge-stat-num {
    font-family: 'Cormorant Garamond', serif;
    font-size: 40px;
    color: var(--gold);
    font-weight: 300;
    margin-bottom: 8px;
  }

  .challenge-stat-label {
    font-size: 10px;
    letter-spacing: 2px;
    text-transform: uppercase;
    color: var(--gray);
  }

  /* FOOTER */
  footer {
    padding: 80px 48px 40px;
    border-top: 1px solid rgba(201,168,76,0.1);
    text-align: center;
  }

  .footer-logo {
    font-family: 'Cormorant Garamond', serif;
    font-size: 32px;
    font-weight: 600;
    color: var(--gold);
    letter-spacing: 6px;
    text-transform: uppercase;
    margin-bottom: 8px;
  }

  .footer-tag {
    font-size: 10px;
    letter-spacing: 4px;
    color: var(--gray);
    text-transform: uppercase;
    margin-bottom: 40px;
  }

  .footer-links {
    display: flex; justify-content: center; gap: 40px;
    list-style: none;
    margin-bottom: 40px;
  }

  .footer-links a {
    color: var(--gray);
    text-decoration: none;
    font-size: 10px;
    letter-spacing: 2px;
    text-transform: uppercase;
    transition: color 0.3s;
  }
  .footer-links a:hover { color: var(--gold); }

  .footer-copy {
    font-size: 11px;
    color: rgba(136,136,136,0.4);
    letter-spacing: 1px;
  }

  /* Scroll reveal */
  .reveal {
    opacity: 0;
    transform: translateY(40px);
    transition: opacity 0.8s ease, transform 0.8s ease;
  }
  .reveal.visible {
    opacity: 1;
    transform: translateY(0);
  }

  @keyframes fadeUp {
    to { opacity: 1; transform: translateY(0); }
    from { opacity: 0; transform: translateY(30px); }
  }

  /* Scrollbar */
  ::-webkit-scrollbar { width: 4px; }
  ::-webkit-scrollbar-track { background: var(--black); }
  ::-webkit-scrollbar-thumb { background: var(--gold-dark); }

  @media (max-width: 768px) {
    nav { padding: 20px 24px; }
    .nav-links { display: none; }
    .hero { padding: 100px 24px 60px; }
    .sectors { padding: 80px 24px; }
    .vision { padding: 80px 24px; }
    .stats { padding: 60px 24px; }
    .challenge { padding: 80px 24px; }
    .challenge-inner { grid-template-columns: 1fr; gap: 48px; }
    .challenge-right { grid-template-columns: 1fr 1fr; }
    footer { padding: 60px 24px 32px; }
    .hero-cta { flex-direction: column; align-items: center; }
    body { cursor: auto; }
    .cursor, .cursor-ring { display: none; }
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<nav>
  <div class="nav-logo">Patera</div>
  <ul class="nav-links">
    <li><a href="#sectors">Sectors</a></li>
    <li><a href="#vision">Vision</a></li>
    <li><a href="#challenge">Initiative</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="hero-bg"></div>
  <div class="hero-line top"></div>
  <div class="hero-line bottom"></div>
  <div class="hero-content">
    <p class="hero-tag">Est. Akwa Ibom · Nigeria · Global</p>
    <h1 class="hero-title">Patera<br/><span>Group</span><br/>International</h1>
    <p class="hero-sub">Real Estate &nbsp;·&nbsp; Agro Business &nbsp;·&nbsp; Technology &nbsp;·&nbsp; Sports</p>
    <div class="hero-divider"></div>
    <p class="hero-desc">
      A vertically integrated conglomerate building the infrastructure of tomorrow — from the soil of Akwa Ibom to the skylines of the world.
    </p>
    <div class="hero-cta">
      <a href="#sectors" class="btn-primary">Our Sectors</a>
      <a href="#challenge" class="btn-outline">Our Initiative</a>
    </div>
  </div>
</section>

<!-- SECTORS -->
<section class="sectors" id="sectors">
  <div class="section-header reveal">
    <span class="section-tag">What We Build</span>
    <h2 class="section-title">Four Pillars of<br/><em>One Empire</em></h2>
  </div>
  <div class="sectors-grid">
    <div class="sector-card reveal">
      <span class="sector-number">01</span>
      <span class="sector-icon">🏗️</span>
      <h3 class="sector-name">Real Estate</h3>
      <p class="sector-desc">Developing premium residential and commercial properties across Nigeria's fastest-growing corridors. Building not just structures — but communities.</p>
    </div>
    <div class="sector-card reveal">
      <span class="sector-number">02</span>
      <span class="sector-icon">🌱</span>
      <h3 class="sector-name">Agro Business</h3>
      <p class="sector-desc">From Lyco Gold Tomato Base to large-scale farm-to-table operations. We feed the nation while creating sustainable rural economies.</p>
    </div>
    <div class="sector-card reveal">
      <span class="sector-number">03</span>
      <span class="sector-icon">⚡</span>
      <h3 class="sector-name">Technology</h3>
      <p class="sector-desc">Engineering Patera OS — a unified super app ecosystem connecting health, logistics, commerce, and payments into one seamless platform.</p>
    </div>
    <div class="sector-card reveal">
      <span class="sector-number">04</span>
      <span class="sector-icon">⚽</span>
      <h3 class="sector-name">Sports</h3>
      <p class="sector-desc">Identifying and developing elite African talent through our scouting academy. Bridging Nigerian football to the global stage.</p>
    </div>
  </div>
</section>

<!-- VISION -->
<section class="vision" id="vision">
  <div class="vision-inner reveal">
    <div class="vision-quote">
      "We do not build businesses.<br/>We build <em>ecosystems</em> —<br/>where every pillar feeds the next."
    </div>
    <p class="vision-attr">— Henry Umoren, Founder · Patera Group International</p>
  </div>
</section>

<!-- STATS -->
<div class="stats">
  <div class="stat-item reveal">
    <div class="stat-number">4</div>
    <div class="stat-label">Core Sectors</div>
  </div>
  <div class="stat-item reveal">
    <div class="stat-number">1</div>
    <div class="stat-label">Unified Platform</div>
  </div>
  <div class="stat-item reveal">
    <div class="stat-number">∞</div>
    <div class="stat-label">Vision</div>
  </div>
  <div class="stat-item reveal">
    <div class="stat-number">NG</div>
    <div class="stat-label">Built in Nigeria</div>
  </div>
</div>

<!-- CHALLENGE -->
<section class="challenge" id="challenge">
  <div class="challenge-inner">
    <div class="challenge-left reveal">
      <h2>The 100-Day <em>Mission</em></h2>
      <p>
        Before we build an empire, we give back. For 100 days, every comment and every share on our social media generates a kobo-by-kobo contribution to children at an orphanage in Port Harcourt.
      </p>
      <p style="font-size:12px; color: var(--gold); letter-spacing:1px;">
        Every comment = ₦10 &nbsp;·&nbsp; Every share = ₦20
      </p>
      <div class="progress-wrap">
        <div class="progress-header">
          <span>Day 3 of 100</span>
          <span id="pct">3%</span>
        </div>
        <div class="progress-bar">
          <div class="progress-fill" id="progressFill"></div>
        </div>
      </div>
      <a href="https://tiktok.com" class="btn-primary" target="_blank">Follow the Journey</a>
    </div>
    <div class="challenge-right reveal">
      <div class="challenge-stat">
        <div class="challenge-stat-num">3</div>
        <div class="challenge-stat-label">Days Done</div>
      </div>
      <div class="challenge-stat">
        <div class="challenge-stat-num">97</div>
        <div class="challenge-stat-label">Days Left</div>
      </div>
      <div class="challenge-stat">
        <div class="challenge-stat-num">₦10</div>
        <div class="challenge-stat-label">Per Comment</div>
      </div>
      <div class="challenge-stat">
        <div class="challenge-stat-num">₦20</div>
        <div class="challenge-stat-label">Per Share</div>
      </div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer id="contact">
  <div class="footer-logo">Patera</div>
  <p class="footer-tag">Group International &nbsp;·&nbsp; Nigeria &amp; Beyond</p>
  <ul class="footer-links">
    <li><a href="#">TikTok</a></li>
    <li><a href="#">Instagram</a></li>
    <li><a href="#">Facebook</a></li>
    <li><a href="#">X (Twitter)</a></li>
  </ul>
  <p class="footer-copy">© 2025 Patera Group International. All rights reserved. Built in Nigeria.</p>
</footer>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;

  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    cursor.style.left = mx + 'px';
    cursor.style.top = my + 'px';
  });

  function animRing() {
    rx += (mx - rx) * 0.12;
    ry += (my - ry) * 0.12;
    ring.style.left = rx + 'px';
    ring.style.top = ry + 'px';
    requestAnimationFrame(animRing);
  }
  animRing();

  document.querySelectorAll('a, button').forEach(el => {
    el.addEventListener('mouseenter', () => {
      cursor.style.transform = 'translate(-50%,-50%) scale(2)';
      ring.style.width = '56px'; ring.style.height = '56px';
    });
    el.addEventListener('mouseleave', () => {
      cursor.style.transform = 'translate(-50%,-50%) scale(1)';
      ring.style.width = '36px'; ring.style.height = '36px';
    });
  });

  // Scroll reveal
