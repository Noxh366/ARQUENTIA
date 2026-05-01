<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>ARQUENTIA — Diseño, Decoración, Arquitectura</title>
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=Archivo:wght@300;400;500;600&family=Bebas+Neue&display=swap" rel="stylesheet">
<style>
  :root {
    --black: #080b0f;
    --dark: #0d1117;
    --panel: #111820;
    --card: #141c26;
    --border: rgba(0,188,212,0.15);
    --cyan: #00bcd4;
    --cyan-dim: rgba(0,188,212,0.6);
    --cyan-glow: rgba(0,188,212,0.12);
    --white: #f0f4f8;
    --muted: #7a8fa8;
    --text: #c8d6e5;
  }

  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--black);
    color: var(--text);
    font-family: 'Archivo', sans-serif;
    font-weight: 300;
    overflow-x: hidden;
    cursor: default;
  }

  /* ── CUSTOM CURSOR ── */
  .cursor {
    width: 10px; height: 10px;
    background: var(--cyan);
    border-radius: 50%;
    position: fixed; pointer-events: none; z-index: 9999;
    transform: translate(-50%,-50%);
    transition: transform 0.1s, width 0.3s, height 0.3s, opacity 0.3s;
    mix-blend-mode: screen;
  }
  .cursor-ring {
    width: 36px; height: 36px;
    border: 1px solid var(--cyan-dim);
    border-radius: 50%;
    position: fixed; pointer-events: none; z-index: 9998;
    transform: translate(-50%,-50%);
    transition: transform 0.18s ease, width 0.3s, height 0.3s, opacity 0.3s;
  }
  body:hover .cursor { opacity: 1; }

  /* ── NOISE OVERLAY ── */
  body::before {
    content: '';
    position: fixed; inset: 0; z-index: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none; opacity: 0.5;
  }

  /* ── NAV ── */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    padding: 20px 60px;
    display: flex; align-items: center; justify-content: space-between;
    background: linear-gradient(to bottom, rgba(8,11,15,0.95) 0%, transparent 100%);
    backdrop-filter: blur(4px);
    transition: padding 0.4s;
  }
  nav.scrolled { padding: 14px 60px; background: rgba(8,11,15,0.97); }
  .nav-logo {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1.6rem;
    letter-spacing: 0.25em;
    color: var(--white);
    text-decoration: none;
  }
  .nav-logo span { color: var(--cyan); }
  .nav-links { display: flex; gap: 36px; list-style: none; }
  .nav-links a {
    color: var(--muted); font-size: 0.72rem; letter-spacing: 0.18em;
    text-transform: uppercase; text-decoration: none;
    position: relative; padding-bottom: 4px;
    transition: color 0.3s;
  }
  .nav-links a::after {
    content: ''; position: absolute; bottom: 0; left: 0;
    width: 0; height: 1px; background: var(--cyan);
    transition: width 0.35s ease;
  }
  .nav-links a:hover { color: var(--white); }
  .nav-links a:hover::after { width: 100%; }
  .nav-cta {
    border: 1px solid var(--border); color: var(--cyan);
    padding: 8px 22px; font-size: 0.7rem; letter-spacing: 0.18em;
    text-transform: uppercase; text-decoration: none;
    transition: background 0.3s, border-color 0.3s, color 0.3s, box-shadow 0.3s;
    position: relative; overflow: hidden;
  }
  .nav-cta::before {
    content: ''; position: absolute; inset: 0;
    background: var(--cyan); transform: scaleX(0); transform-origin: left;
    transition: transform 0.35s ease; z-index: -1;
  }
  .nav-cta:hover { color: var(--black); border-color: var(--cyan); box-shadow: 0 0 20px var(--cyan-glow); }
  .nav-cta:hover::before { transform: scaleX(1); }

  /* ── HERO ── */
  #hero {
    min-height: 100vh;
    display: flex; flex-direction: column;
    align-items: center; justify-content: center;
    position: relative; overflow: hidden;
    padding: 120px 60px 80px;
  }
  .hero-grid-lines {
    position: absolute; inset: 0; z-index: 0;
    background-image:
      linear-gradient(rgba(0,188,212,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(0,188,212,0.03) 1px, transparent 1px);
    background-size: 60px 60px;
    animation: gridPulse 8s ease-in-out infinite;
  }
  @keyframes gridPulse {
    0%,100% { opacity: 0.5; } 50% { opacity: 1; }
  }
  .hero-glow {
    position: absolute; width: 600px; height: 600px;
    background: radial-gradient(circle, rgba(0,188,212,0.08) 0%, transparent 70%);
    border-radius: 50%; top: 50%; left: 50%;
    transform: translate(-50%,-50%);
    animation: glowPulse 4s ease-in-out infinite;
    pointer-events: none;
  }
  @keyframes glowPulse {
    0%,100% { transform: translate(-50%,-50%) scale(1); opacity: 0.6; }
    50% { transform: translate(-50%,-50%) scale(1.1); opacity: 1; }
  }
  .hero-badge {
    font-size: 0.65rem; letter-spacing: 0.3em; text-transform: uppercase;
    color: var(--cyan); border: 1px solid var(--border);
    padding: 6px 18px; margin-bottom: 36px;
    position: relative; z-index: 1;
    animation: fadeUp 0.8s ease forwards; opacity: 0;
    animation-delay: 0.2s;
  }
  .hero-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(5rem, 12vw, 11rem);
    letter-spacing: 0.12em; line-height: 0.9;
    color: var(--white); text-align: center;
    position: relative; z-index: 1;
    animation: fadeUp 0.9s ease forwards; opacity: 0;
    animation-delay: 0.4s;
  }
  .hero-title .accent { color: var(--cyan); }
  .hero-sub {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(1rem, 2vw, 1.4rem);
    font-weight: 300; font-style: italic;
    color: var(--muted); letter-spacing: 0.15em;
    margin-top: 20px; text-align: center;
    position: relative; z-index: 1;
    animation: fadeUp 1s ease forwards; opacity: 0;
    animation-delay: 0.6s;
  }
  .hero-desc {
    max-width: 520px; text-align: center; margin-top: 28px;
    font-size: 0.88rem; line-height: 1.9; color: var(--muted);
    position: relative; z-index: 1;
    animation: fadeUp 1s ease forwards; opacity: 0;
    animation-delay: 0.8s;
  }
  .hero-actions {
    display: flex; gap: 20px; margin-top: 48px;
    position: relative; z-index: 1;
    animation: fadeUp 1s ease forwards; opacity: 0;
    animation-delay: 1s;
  }
  .btn-primary {
    background: var(--cyan); color: var(--black);
    padding: 14px 38px; font-size: 0.72rem; font-weight: 600;
    letter-spacing: 0.2em; text-transform: uppercase; text-decoration: none;
    position: relative; overflow: hidden;
    transition: box-shadow 0.3s, transform 0.3s;
    display: inline-block;
  }
  .btn-primary::before {
    content: ''; position: absolute; top: 0; left: -100%;
    width: 100%; height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255,255,255,0.3), transparent);
    transition: left 0.5s ease;
  }
  .btn-primary:hover { box-shadow: 0 0 40px rgba(0,188,212,0.5); transform: translateY(-2px); }
  .btn-primary:hover::before { left: 100%; }
  .btn-secondary {
    border: 1px solid var(--border); color: var(--text);
    padding: 14px 38px; font-size: 0.72rem; letter-spacing: 0.2em;
    text-transform: uppercase; text-decoration: none;
    position: relative; overflow: hidden;
    transition: border-color 0.3s, color 0.3s, transform 0.3s;
    display: inline-block;
  }
  .btn-secondary:hover { border-color: var(--cyan); color: var(--cyan); transform: translateY(-2px); }
  .hero-scroll {
    position: absolute; bottom: 40px; left: 50%; transform: translateX(-50%);
    z-index: 1; text-align: center;
    animation: fadeIn 1.5s ease forwards; animation-delay: 1.5s; opacity: 0;
  }
  .scroll-line {
    width: 1px; height: 50px; background: linear-gradient(to bottom, var(--cyan), transparent);
    margin: 0 auto 10px;
    animation: scrollAnim 2s ease-in-out infinite;
  }
  @keyframes scrollAnim {
    0%,100% { transform: scaleY(1); opacity: 0.6; }
    50% { transform: scaleY(1.3); opacity: 1; }
  }
  .scroll-text { font-size: 0.6rem; letter-spacing: 0.3em; color: var(--muted); text-transform: uppercase; }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeIn {
    from { opacity: 0; } to { opacity: 1; }
  }

  /* ── SECTION COMMON ── */
  section { position: relative; z-index: 1; }
  .section-header {
    text-align: center; margin-bottom: 80px;
    opacity: 0; transform: translateY(40px);
    transition: opacity 0.8s ease, transform 0.8s ease;
  }
  .section-header.visible { opacity: 1; transform: translateY(0); }
  .section-label {
    font-size: 0.62rem; letter-spacing: 0.4em; text-transform: uppercase;
    color: var(--cyan); margin-bottom: 16px; display: block;
  }
  .section-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: clamp(2.8rem, 6vw, 5rem);
    letter-spacing: 0.08em; color: var(--white); line-height: 1;
  }
  .section-subtitle {
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.1rem; font-style: italic;
    color: var(--muted); margin-top: 14px; letter-spacing: 0.05em;
  }
  .section-rule {
    width: 60px; height: 1px; background: var(--cyan);
    margin: 20px auto 0;
  }

  /* ── STATS ── */
  #stats {
    padding: 80px 60px;
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
  }
  .stats-grid {
    display: grid; grid-template-columns: repeat(4, 1fr);
    gap: 1px; background: var(--border);
    max-width: 1100px; margin: 0 auto;
  }
  .stat-item {
    background: var(--black); padding: 48px 40px;
    text-align: center;
    opacity: 0; transform: translateY(20px);
    transition: opacity 0.6s ease, transform 0.6s ease, background 0.3s;
  }
  .stat-item.visible { opacity: 1; transform: translateY(0); }
  .stat-item:hover { background: var(--panel); }
  .stat-num {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 3.5rem; color: var(--cyan); letter-spacing: 0.05em; line-height: 1;
  }
  .stat-label { font-size: 0.7rem; letter-spacing: 0.2em; color: var(--muted); text-transform: uppercase; margin-top: 10px; }

  /* ── SERVICES ── */
  #servicios { padding: 120px 60px; }
  .services-grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 2px;
    max-width: 1200px; margin: 0 auto;
    background: var(--border);
  }
  .service-card {
    background: var(--dark);
    padding: 52px 44px;
    position: relative; overflow: hidden;
    cursor: pointer;
    opacity: 0; transform: translateY(30px);
    transition: opacity 0.7s ease, transform 0.7s ease, background 0.4s;
  }
  .service-card.visible { opacity: 1; transform: translateY(0); }
  .service-card::before {
    content: ''; position: absolute; inset: 0;
    background: linear-gradient(135deg, var(--cyan-glow), transparent 60%);
    opacity: 0; transition: opacity 0.4s;
  }
  .service-card::after {
    content: ''; position: absolute; bottom: 0; left: 0; right: 0;
    height: 2px; background: var(--cyan);
    transform: scaleX(0); transform-origin: left;
    transition: transform 0.4s ease;
  }
  .service-card:hover { background: var(--panel); }
  .service-card:hover::before { opacity: 1; }
  .service-card:hover::after { transform: scaleX(1); }
  .service-card:hover .service-icon { color: var(--cyan); transform: scale(1.1) rotate(-5deg); }
  .service-card:hover .service-arrow { transform: translateX(6px); opacity: 1; }
  .service-num {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 4rem; color: rgba(0,188,212,0.06);
    position: absolute; top: 20px; right: 28px;
    line-height: 1; letter-spacing: 0.05em;
    transition: color 0.4s;
  }
  .service-card:hover .service-num { color: rgba(0,188,212,0.12); }
  .service-icon {
    font-size: 1.8rem; margin-bottom: 28px; display: block;
    transition: color 0.4s, transform 0.4s;
  }
  .service-name {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1.6rem; letter-spacing: 0.08em;
    color: var(--white); margin-bottom: 14px;
  }
  .service-desc {
    font-size: 0.83rem; line-height: 1.9;
    color: var(--muted); margin-bottom: 28px;
  }
  .service-tags {
    display: flex; flex-wrap: wrap; gap: 8px; margin-bottom: 28px;
  }
  .tag {
    font-size: 0.6rem; letter-spacing: 0.15em; text-transform: uppercase;
    border: 1px solid var(--border); color: var(--muted);
    padding: 4px 10px;
    transition: border-color 0.3s, color 0.3s;
  }
  .service-card:hover .tag { border-color: rgba(0,188,212,0.3); color: var(--cyan-dim); }
  .service-arrow {
    font-size: 0.7rem; letter-spacing: 0.2em; color: var(--cyan);
    text-transform: uppercase; opacity: 0;
    transition: transform 0.3s, opacity 0.3s;
    display: inline-block;
  }

  /* ── PROCESS ── */
  #proceso {
    padding: 120px 60px;
    background: var(--dark);
    border-top: 1px solid var(--border);
  }
  .process-steps {
    display: grid; grid-template-columns: repeat(4, 1fr);
    gap: 0; max-width: 1200px; margin: 0 auto;
    position: relative;
  }
  .process-steps::before {
    content: ''; position: absolute;
    top: 30px; left: 12.5%; right: 12.5%;
    height: 1px; background: linear-gradient(90deg, transparent, var(--border), var(--border), transparent);
  }
  .step {
    padding: 0 30px; text-align: center;
    opacity: 0; transform: translateY(30px);
    transition: opacity 0.7s ease, transform 0.7s ease;
  }
  .step.visible { opacity: 1; transform: translateY(0); }
  .step-dot {
    width: 60px; height: 60px; border-radius: 50%;
    border: 1px solid var(--border); background: var(--dark);
    display: flex; align-items: center; justify-content: center;
    margin: 0 auto 28px;
    font-family: 'Bebas Neue', sans-serif; font-size: 1.1rem;
    color: var(--cyan); letter-spacing: 0.05em;
    position: relative; z-index: 1;
    transition: background 0.3s, border-color 0.3s, box-shadow 0.3s;
  }
  .step:hover .step-dot {
    background: var(--cyan); color: var(--black);
    border-color: var(--cyan); box-shadow: 0 0 30px rgba(0,188,212,0.3);
  }
  .step-title {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1.2rem; letter-spacing: 0.1em;
    color: var(--white); margin-bottom: 12px;
  }
  .step-desc { font-size: 0.8rem; line-height: 1.8; color: var(--muted); }

  /* ── FEATURE STRIP ── */
  #feature {
    padding: 120px 60px;
    display: grid; grid-template-columns: 1fr 1fr;
    gap: 80px; max-width: 1300px; margin: 0 auto;
    align-items: center;
  }
  .feature-visual {
    position: relative; height: 480px;
    opacity: 0; transform: translateX(-40px);
    transition: opacity 0.9s ease, transform 0.9s ease;
  }
  .feature-visual.visible { opacity: 1; transform: translateX(0); }
  .feature-box {
    position: absolute; border: 1px solid var(--border);
    background: var(--panel);
  }
  .feature-box-main {
    width: 80%; height: 80%;
    top: 0; left: 0;
    display: flex; align-items: center; justify-content: center;
    overflow: hidden;
  }
  .feature-box-accent {
    width: 50%; height: 45%;
    bottom: 0; right: 0;
    background: var(--card);
    border-color: var(--cyan);
    display: flex; align-items: center; justify-content: center;
  }
  .arch-graphic {
    width: 100%; height: 100%;
    display: flex; align-items: center; justify-content: center;
    overflow: hidden;
  }
  .arch-graphic svg { width: 100%; height: 100%; }
  .feature-content {
    opacity: 0; transform: translateX(40px);
    transition: opacity 0.9s ease, transform 0.9s ease;
  }
  .feature-content.visible { opacity: 1; transform: translateX(0); }
  .feature-list { margin-top: 32px; }
  .feature-item {
    display: flex; align-items: flex-start; gap: 20px;
    padding: 20px 0; border-bottom: 1px solid var(--border);
    transition: padding-left 0.3s;
    cursor: default;
  }
  .feature-item:hover { padding-left: 8px; }
  .fi-dot {
    width: 6px; height: 6px; border-radius: 50%;
    background: var(--cyan); margin-top: 6px; flex-shrink: 0;
  }
  .fi-text h4 { font-size: 0.8rem; font-weight: 500; color: var(--white); margin-bottom: 4px; letter-spacing: 0.05em; }
  .fi-text p { font-size: 0.78rem; color: var(--muted); line-height: 1.7; }

  /* ── TESTIMONIALS / QUOTE ── */
  #quote {
    padding: 100px 60px;
    text-align: center;
    border-top: 1px solid var(--border);
    border-bottom: 1px solid var(--border);
    background: var(--dark);
    position: relative; overflow: hidden;
  }
  #quote::before {
    content: '"'; position: absolute; top: -40px; left: 50%;
    transform: translateX(-50%);
    font-family: 'Cormorant Garamond', serif;
    font-size: 20rem; color: rgba(0,188,212,0.03);
    line-height: 1; pointer-events: none;
  }
  .quote-text {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(1.4rem, 3vw, 2.2rem);
    font-weight: 300; font-style: italic;
    color: var(--white); max-width: 800px; margin: 0 auto;
    line-height: 1.6; letter-spacing: 0.02em;
    opacity: 0; transform: translateY(30px);
    transition: opacity 0.9s ease, transform 0.9s ease;
  }
  .quote-text.visible { opacity: 1; transform: translateY(0); }
  .quote-author {
    font-size: 0.68rem; letter-spacing: 0.3em; text-transform: uppercase;
    color: var(--cyan); margin-top: 32px;
    opacity: 0; transition: opacity 0.9s ease 0.3s;
  }
  .quote-author.visible { opacity: 1; }

  /* ── CONTACT ── */
  #contacto { padding: 120px 60px; }
  .contact-inner {
    max-width: 1100px; margin: 0 auto;
    display: grid; grid-template-columns: 1fr 1fr;
    gap: 80px; align-items: center;
  }
  .contact-left {
    opacity: 0; transform: translateY(30px);
    transition: opacity 0.8s ease, transform 0.8s ease;
  }
  .contact-left.visible { opacity: 1; transform: translateY(0); }
  .contact-info { margin-top: 48px; }
  .contact-item {
    display: flex; align-items: center; gap: 20px;
    padding: 20px 0; border-bottom: 1px solid var(--border);
    transition: gap 0.3s;
  }
  .contact-item:hover { gap: 26px; }
  .ci-icon { font-size: 1.2rem; color: var(--cyan); }
  .ci-label { font-size: 0.6rem; letter-spacing: 0.25em; text-transform: uppercase; color: var(--muted); }
  .ci-value { font-size: 0.95rem; color: var(--white); margin-top: 3px; }
  .contact-right {
    opacity: 0; transform: translateY(30px);
    transition: opacity 0.8s ease 0.2s, transform 0.8s ease 0.2s;
  }
  .contact-right.visible { opacity: 1; transform: translateY(0); }
  .contact-card {
    background: var(--dark); border: 1px solid var(--border);
    padding: 52px;
  }
  .contact-card h3 {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1.8rem; letter-spacing: 0.1em; color: var(--white); margin-bottom: 8px;
  }
  .contact-card p { font-size: 0.83rem; color: var(--muted); margin-bottom: 36px; line-height: 1.8; }
  .cta-group { display: flex; flex-direction: column; gap: 14px; }
  .cta-wa {
    display: flex; align-items: center; gap: 14px;
    background: #25d366; color: #000;
    padding: 16px 28px; text-decoration: none;
    font-size: 0.78rem; font-weight: 600; letter-spacing: 0.1em;
    transition: box-shadow 0.3s, transform 0.3s;
  }
  .cta-wa:hover { box-shadow: 0 0 30px rgba(37,211,102,0.4); transform: translateY(-2px); }
  .cta-email {
    display: flex; align-items: center; gap: 14px;
    border: 1px solid var(--border); color: var(--text);
    padding: 16px 28px; text-decoration: none;
    font-size: 0.78rem; letter-spacing: 0.1em;
    transition: border-color 0.3s, color 0.3s, transform 0.3s;
  }
  .cta-email:hover { border-color: var(--cyan); color: var(--cyan); transform: translateY(-2px); }

  /* ── FOOTER ── */
  footer {
    padding: 50px 60px;
    border-top: 1px solid var(--border);
    display: flex; align-items: center; justify-content: space-between;
  }
  .footer-logo {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1.4rem; letter-spacing: 0.25em; color: var(--white);
  }
  .footer-logo span { color: var(--cyan); }
  .footer-copy { font-size: 0.68rem; color: var(--muted); letter-spacing: 0.1em; }
  .footer-tagline {
    font-family: 'Cormorant Garamond', serif;
    font-style: italic; font-size: 0.85rem; color: var(--muted);
  }

  /* ── SCROLL ANIMATIONS DELAY ── */
  .stat-item:nth-child(1) { transition-delay: 0s; }
  .stat-item:nth-child(2) { transition-delay: 0.1s; }
  .stat-item:nth-child(3) { transition-delay: 0.2s; }
  .stat-item:nth-child(4) { transition-delay: 0.3s; }
  .service-card:nth-child(1) { transition-delay: 0s; }
  .service-card:nth-child(2) { transition-delay: 0.1s; }
  .service-card:nth-child(3) { transition-delay: 0.2s; }
  .service-card:nth-child(4) { transition-delay: 0.1s; }
  .service-card:nth-child(5) { transition-delay: 0.2s; }
  .service-card:nth-child(6) { transition-delay: 0.3s; }
  .step:nth-child(1) { transition-delay: 0s; }
  .step:nth-child(2) { transition-delay: 0.15s; }
  .step:nth-child(3) { transition-delay: 0.3s; }
  .step:nth-child(4) { transition-delay: 0.45s; }

  /* ── VIDEO SECTION ── */
  #video-demo {
    padding: 120px 60px;
    background: var(--dark);
    border-top: 1px solid var(--border);
  }
  .video-container {
    max-width: 1000px; margin: 0 auto;
    opacity: 0; transform: translateY(40px);
    transition: opacity 0.9s ease, transform 0.9s ease;
  }
  .video-container.visible { opacity: 1; transform: translateY(0); }
  .video-frame {
    position: relative;
    border: 1px solid var(--border);
    background: var(--black);
    overflow: hidden;
    box-shadow:
      0 40px 80px rgba(0,0,0,0.6),
      0 0 0 1px rgba(0,188,212,0.08),
      0 0 80px rgba(0,188,212,0.06);
  }
  .video-frame::before {
    content: '';
    position: absolute; inset: 0; z-index: 1; pointer-events: none;
    background:
      linear-gradient(to bottom, rgba(8,11,15,0.3) 0%, transparent 15%, transparent 85%, rgba(8,11,15,0.3) 100%),
      linear-gradient(to right, rgba(8,11,15,0.2) 0%, transparent 10%, transparent 90%, rgba(8,11,15,0.2) 100%);
  }
  .video-frame::after {
    content: '';
    position: absolute; inset: 0; z-index: 2; pointer-events: none;
    background:
      linear-gradient(var(--cyan), var(--cyan)) top left / 30px 1px no-repeat,
      linear-gradient(var(--cyan), var(--cyan)) top left / 1px 30px no-repeat,
      linear-gradient(var(--cyan), var(--cyan)) top right / 30px 1px no-repeat,
      linear-gradient(var(--cyan), var(--cyan)) top right / 1px 30px no-repeat,
      linear-gradient(var(--cyan), var(--cyan)) bottom left / 30px 1px no-repeat,
      linear-gradient(var(--cyan), var(--cyan)) bottom left / 1px 30px no-repeat,
      linear-gradient(var(--cyan), var(--cyan)) bottom right / 30px 1px no-repeat,
      linear-gradient(var(--cyan), var(--cyan)) bottom right / 1px 30px no-repeat;
    opacity: 0.6;
  }
  .video-frame video {
    width: 100%; display: block;
    object-fit: cover;
  }
  .video-badge {
    display: inline-flex; align-items: center; gap: 8px;
    border: 1px solid var(--border);
    background: rgba(0,188,212,0.06);
    padding: 6px 16px; margin-bottom: 28px;
    font-size: 0.62rem; letter-spacing: 0.25em;
    text-transform: uppercase; color: var(--cyan);
  }
  .video-badge::before {
    content: '';
    width: 6px; height: 6px; border-radius: 50%;
    background: var(--cyan);
    animation: videoPulse 1.5s ease-in-out infinite;
  }
  @keyframes videoPulse {
    0%,100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.4; transform: scale(0.8); }
  }
  .video-meta {
    display: flex; align-items: center; justify-content: space-between;
    margin-top: 24px; padding: 0 4px; flex-wrap: wrap; gap: 16px;
  }
  .video-meta-left h3 {
    font-family: 'Bebas Neue', sans-serif;
    font-size: 1.4rem; letter-spacing: 0.1em; color: var(--white);
  }
  .video-meta-left p { font-size: 0.78rem; color: var(--muted); margin-top: 3px; line-height: 1.7; }
  .video-meta-right {
    font-size: 0.62rem; letter-spacing: 0.2em; text-transform: uppercase;
    color: var(--muted); text-align: right;
  }
  .video-meta-right span { color: var(--cyan); display: block; font-size: 0.72rem; margin-top: 2px; }

  /* ── RESPONSIVE ── */
  @media (max-width: 900px) {
    nav { padding: 18px 28px; }
    .nav-links { display: none; }
    #hero { padding: 120px 28px 80px; }
    #stats, #servicios, #proceso, #feature, #contacto, footer { padding-left: 28px; padding-right: 28px; }
    .stats-grid { grid-template-columns: repeat(2, 1fr); }
    .services-grid { grid-template-columns: 1fr; }
    .process-steps { grid-template-columns: 1fr 1fr; gap: 40px; }
    .process-steps::before { display: none; }
    #feature { grid-template-columns: 1fr; }
    .feature-visual { height: 300px; }
    .contact-inner { grid-template-columns: 1fr; }
    footer { flex-direction: column; gap: 20px; text-align: center; }
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- NAV -->
<nav id="navbar">
  <a href="#hero" class="nav-logo">ARQ<span>U</span>ENTIA</a>
  <ul class="nav-links">
    <li><a href="#servicios">Servicios</a></li>
    <li><a href="#proceso">Proceso</a></li>
    <li><a href="#video-demo">Video</a></li>
    <li><a href="#contacto">Contacto</a></li>
  </ul>
  <a href="#contacto" class="nav-cta">Solicitar Proyecto</a>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="hero-grid-lines"></div>
  <div class="hero-glow"></div>
  <div class="hero-badge">Diseño · Decoración · Arquitectura</div>
  <h1 class="hero-title">ARQ<span class="accent">U</span>ENTIA</h1>
  <p class="hero-sub">diseño. decoración. arquitectura</p>
  <p class="hero-desc">Transformamos espacios en experiencias. Creamos proyectos arquitectónicos de alta calidad que combinan funcionalidad, estética y visión contemporánea para hacer realidad tus ideas.</p>
  <div class="hero-actions">
    <a href="#servicios" class="btn-primary">Ver Servicios</a>
    <a href="#contacto" class="btn-secondary">Iniciar Proyecto</a>
  </div>
  <div class="hero-scroll">
    <div class="scroll-line"></div>
    <span class="scroll-text">Descubrir</span>
  </div>
</section>

<!-- STATS -->
<section id="stats">
  <div class="stats-grid">
    <div class="stat-item">
      <div class="stat-num">+150</div>
      <div class="stat-label">Proyectos Completados</div>
    </div>
    <div class="stat-item">
      <div class="stat-num">+8</div>
      <div class="stat-label">Años de Experiencia</div>
    </div>
    <div class="stat-item">
      <div class="stat-num">100%</div>
      <div class="stat-label">Clientes Satisfechos</div>
    </div>
    <div class="stat-item">
      <div class="stat-num">6</div>
      <div class="stat-label">Áreas de Especialidad</div>
    </div>
  </div>
</section>

<!-- SERVICES -->
<section id="servicios">
  <div class="section-header">
    <span class="section-label">Lo que ofrecemos</span>
    <h2 class="section-title">SERVICIOS</h2>
    <p class="section-subtitle">Soluciones integrales para cada etapa de tu proyecto</p>
    <div class="section-rule"></div>
  </div>
  <div class="services-grid">
    <div class="service-card">
      <span class="service-num">01</span>
      <span class="service-icon">🏛</span>
      <h3 class="service-name">Arquitectura</h3>
      <p class="service-desc">Diseñamos proyectos arquitectónicos con precisión técnica y creatividad visionaria. Desde residencias unifamiliares hasta desarrollos comerciales, cada proyecto refleja la identidad de quien lo habitará.</p>
      <div class="service-tags"><span class="tag">Diseño</span><span class="tag">Planificación</span><span class="tag">Consultoría</span></div>
      <span class="service-arrow">Explorar →</span>
    </div>
    <div class="service-card">
      <span class="service-num">02</span>
      <span class="service-icon">🎨</span>
      <h3 class="service-name">Renders Exteriores</h3>
      <p class="service-desc">Visualizaciones fotorrealistas que dan vida a tu proyecto antes de construirlo. Nuestros renders de día capturan cada detalle de materiales, texturas y entorno para una presentación impactante.</p>
      <div class="service-tags"><span class="tag">Fotorrealismo</span><span class="tag">3D</span><span class="tag">Día</span></div>
      <span class="service-arrow">Explorar →</span>
    </div>
    <div class="service-card">
      <span class="service-num">03</span>
      <span class="service-icon">🌙</span>
      <h3 class="service-name">Ambientación Nocturna</h3>
      <p class="service-desc">Renders nocturnos con iluminación dramática y atmósfera cinematográfica. Mostramos cómo tu proyecto cobra una vida completamente diferente y más sofisticada bajo la luz artificial.</p>
      <div class="service-tags"><span class="tag">Iluminación</span><span class="tag">Noche</span><span class="tag">Atmósfera</span></div>
      <span class="service-arrow">Explorar →</span>
    </div>
    <div class="service-card">
      <span class="service-num">04</span>
      <span class="service-icon">📐</span>
      <h3 class="service-name">Plantas Arquitectónicas 3D</h3>
      <p class="service-desc">Plantas arquitectónicas tridimensionales que comunican el espacio de forma intuitiva y poderosa. Ideales para presentaciones a clientes, desarrolladores y equipos de ventas inmobiliarias.</p>
      <div class="service-tags"><span class="tag">Distribución</span><span class="tag">3D</span><span class="tag">Inmobiliario</span></div>
      <span class="service-arrow">Explorar →</span>
    </div>
    <div class="service-card">
      <span class="service-num">05</span>
      <span class="service-icon">📋</span>
      <h3 class="service-name">Planos Ejecutivos AutoCAD</h3>
      <p class="service-desc">Documentación técnica profesional elaborada en AutoCAD con los estándares de la industria. Planos de construcción precisos, acotados y listos para la ejecución de tu proyecto.</p>
      <div class="service-tags"><span class="tag">AutoCAD</span><span class="tag">Técnico</span><span class="tag">Construcción</span></div>
      <span class="service-arrow">Explorar →</span>
    </div>
    <div class="service-card">
      <span class="service-num">06</span>
      <span class="service-icon">🪴</span>
      <h3 class="service-name">Interiorismo & Jardinería</h3>
      <p class="service-desc">Creamos espacios interiores armoniosos y jardines que complementan tu arquitectura. Diseñamos ambientes que equilibran estética, funcionalidad y bienestar en cada rincón del proyecto.</p>
      <div class="service-tags"><span class="tag">Interior</span><span class="tag">Jardín</span><span class="tag">Bienestar</span></div>
      <span class="service-arrow">Explorar →</span>
    </div>
  </div>
</section>

<!-- PROCESS -->
<section id="proceso">
  <div class="section-header">
    <span class="section-label">Cómo trabajamos</span>
    <h2 class="section-title">NUESTRO PROCESO</h2>
    <p class="section-subtitle">Un camino claro desde la idea hasta la realidad</p>
    <div class="section-rule"></div>
  </div>
  <div class="process-steps">
    <div class="step">
      <div class="step-dot">01</div>
      <h3 class="step-title">Consulta Inicial</h3>
      <p class="step-desc">Entendemos tu visión, necesidades y presupuesto. Escuchamos cada detalle para garantizar que el proyecto refleje exactamente lo que imaginas.</p>
    </div>
    <div class="step">
      <div class="step-dot">02</div>
      <h3 class="step-title">Propuesta de Diseño</h3>
      <p class="step-desc">Desarrollamos conceptos creativos adaptados a tu proyecto. Presentamos bocetos, referencias y estrategias visuales para validar la dirección.</p>
    </div>
    <div class="step">
      <div class="step-dot">03</div>
      <h3 class="step-title">Desarrollo & Renders</h3>
      <p class="step-desc">Producimos renders fotorrealistas, planos técnicos y toda la documentación necesaria con la mayor precisión y calidad del mercado.</p>
    </div>
    <div class="step">
      <div class="step-dot">04</div>
      <h3 class="step-title">Entrega Final</h3>
      <p class="step-desc">Proporcionamos todos los archivos en formatos listos para construcción, presentación o venta. Acompañamiento post-entrega incluido.</p>
    </div>
  </div>
</section>

<!-- FEATURE SECTION -->
<section id="feature" style="padding:120px 60px;">
  <div class="feature-visual" style="max-width:500px; width:100%;">
    <div class="feature-box feature-box-main">
      <div class="arch-graphic">
        <svg viewBox="0 0 400 320" fill="none" xmlns="http://www.w3.org/2000/svg">
          <!-- Blueprint Grid -->
          <defs>
            <pattern id="grid" width="20" height="20" patternUnits="userSpaceOnUse">
              <path d="M 20 0 L 0 0 0 20" fill="none" stroke="rgba(0,188,212,0.08)" stroke-width="0.5"/>
            </pattern>
          </defs>
          <rect width="400" height="320" fill="url(#grid)"/>
          <!-- House outline -->
          <path d="M 80 260 L 80 140 L 200 60 L 320 140 L 320 260 Z" stroke="rgba(0,188,212,0.5)" stroke-width="1.5" fill="none"/>
          <line x1="80" y1="260" x2="320" y2="260" stroke="rgba(0,188,212,0.5)" stroke-width="1.5"/>
          <!-- Roof ridge -->
          <line x1="200" y1="60" x2="200" y2="100" stroke="rgba(0,188,212,0.25)" stroke-width="1" stroke-dasharray="4,4"/>
          <!-- Windows -->
          <rect x="110" y="170" width="50" height="40" stroke="rgba(0,188,212,0.5)" stroke-width="1" fill="rgba(0,188,212,0.05)"/>
          <line x1="135" y1="170" x2="135" y2="210" stroke="rgba(0,188,212,0.3)" stroke-width="0.8"/>
          <rect x="240" y="170" width="50" height="40" stroke="rgba(0,188,212,0.5)" stroke-width="1" fill="rgba(0,188,212,0.05)"/>
          <line x1="265" y1="170" x2="265" y2="210" stroke="rgba(0,188,212,0.3)" stroke-width="0.8"/>
          <!-- Door -->
          <rect x="173" y="210" width="54" height="50" stroke="rgba(0,188,212,0.6)" stroke-width="1.5" fill="rgba(0,188,212,0.05)"/>
          <!-- Dimension lines -->
          <line x1="80" y1="280" x2="320" y2="280" stroke="rgba(0,188,212,0.25)" stroke-width="0.8"/>
          <line x1="80" y1="276" x2="80" y2="284" stroke="rgba(0,188,212,0.25)" stroke-width="0.8"/>
          <line x1="320" y1="276" x2="320" y2="284" stroke="rgba(0,188,212,0.25)" stroke-width="0.8"/>
          <text x="200" y="296" fill="rgba(0,188,212,0.5)" font-size="9" text-anchor="middle" font-family="Archivo, sans-serif">12.00 m</text>
          <!-- Side dim -->
          <line x1="60" y1="140" x2="60" y2="260" stroke="rgba(0,188,212,0.25)" stroke-width="0.8"/>
          <line x1="56" y1="140" x2="64" y2="140" stroke="rgba(0,188,212,0.25)" stroke-width="0.8"/>
          <line x1="56" y1="260" x2="64" y2="260" stroke="rgba(0,188,212,0.25)" stroke-width="0.8"/>
          <text x="40" y="205" fill="rgba(0,188,212,0.5)" font-size="9" text-anchor="middle" font-family="Archivo, sans-serif" transform="rotate(-90,40,205)">6.00 m</text>
          <!-- Corner dots -->
          <circle cx="80" cy="260" r="3" fill="rgba(0,188,212,0.6)"/>
          <circle cx="320" cy="260" r="3" fill="rgba(0,188,212,0.6)"/>
          <circle cx="200" cy="60" r="3" fill="rgba(0,188,212,0.8)"/>
          <circle cx="80" cy="140" r="3" fill="rgba(0,188,212,0.6)"/>
          <circle cx="320" cy="140" r="3" fill="rgba(0,188,212,0.6)"/>
          <!-- ARQUENTIA watermark -->
          <text x="200" y="30" fill="rgba(0,188,212,0.15)" font-size="10" text-anchor="middle" font-family="Bebas Neue, sans-serif" letter-spacing="6">ARQUENTIA</text>
          <text x="200" y="316" fill="rgba(0,188,212,0.15)" font-size="8" text-anchor="middle" font-family="Archivo, sans-serif" letter-spacing="3">ARQ-2025</text>
        </svg>
      </div>
    </div>
    <div class="feature-box feature-box-accent">
      <svg viewBox="0 0 180 140" width="160" fill="none" xmlns="http://www.w3.org/2000/svg">
        <rect width="180" height="140" fill="none"/>
        <!-- 3D box representation -->
        <polygon points="90,15 160,55 160,105 90,65" fill="rgba(0,188,212,0.06)" stroke="rgba(0,188,212,0.4)" stroke-width="1"/>
        <polygon points="20,55 90,15 90,65 20,105" fill="rgba(0,188,212,0.04)" stroke="rgba(0,188,212,0.3)" stroke-width="1"/>
        <polygon points="20,105 90,65 160,105 90,125" fill="rgba(0,188,212,0.08)" stroke="rgba(0,188,212,0.5)" stroke-width="1"/>
        <!-- Top face highlight -->
        <line x1="90" y1="15" x2="90" y2="65" stroke="rgba(0,188,212,0.2)" stroke-width="0.8" stroke-dasharray="3,3"/>
        <text x="90" y="135" fill="rgba(0,188,212,0.5)" font-size="8" text-anchor="middle" font-family="Archivo, sans-serif" letter-spacing="2">3D RENDER</text>
      </svg>
    </div>
  </div>
  <div class="feature-content">
    <span class="section-label">¿Por qué elegirnos?</span>
    <h2 class="section-title">CALIDAD<br>Y COMPROMISO</h2>
    <p style="font-size:0.88rem; color:var(--muted); line-height:1.9; margin-top:20px;">En Arquentia, cada proyecto es tratado como una obra única. Combinamos el dominio técnico con una sensibilidad estética refinada para producir resultados que superan expectativas.</p>
    <div class="feature-list">
      <div class="feature-item">
        <div class="fi-dot"></div>
        <div class="fi-text">
          <h4>Renderizado Fotorrealista de Alta Gama</h4>
          <p>Utilizamos software de última generación para producir imágenes que capturan materiales, luz y ambiente con fidelidad cinematográfica.</p>
        </div>
      </div>
      <div class="feature-item">
        <div class="fi-dot"></div>
        <div class="fi-text">
          <h4>Tiempos de Entrega Comprometidos</h4>
          <p>Respetamos los plazos acordados porque entendemos que tu proyecto tiene un calendario. Puntualidad como parte de nuestra propuesta de valor.</p>
        </div>
      </div>
      <div class="feature-item">
        <div class="fi-dot"></div>
        <div class="fi-text">
          <h4>Revisiones Incluidas en el Proceso</h4>
          <p>Trabajamos contigo en iteraciones hasta que el resultado refleje exactamente tu visión. Tu satisfacción es el objetivo final de cada entrega.</p>
        </div>
      </div>
      <div class="feature-item">
        <div class="fi-dot"></div>
        <div class="fi-text">
          <h4>Documentación Lista para Construcción</h4>
          <p>Los planos ejecutivos que producimos cumplen con normativas técnicas y están listos para ser utilizados directamente en obra.</p>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- VIDEO DEMO -->
<section id="video-demo">
  <div class="video-container">
    <div class="section-header" style="text-align:left; margin-bottom:48px;">
      <span class="section-label">Nuestro trabajo en acción</span>
      <h2 class="section-title">VIDEO DEMO</h2>
      <p class="section-subtitle">Así se ve la calidad Arquentia en movimiento</p>
      <div class="section-rule" style="margin:20px 0 0;"></div>
    </div>
    <div class="video-badge">Reproducción Demo</div>
    <div class="video-frame">
      <video
        controls
        autoplay
        muted
        loop
        playsinline
        src="arquentia_demo.mp4"
      ></video>
    </div>
    <div class="video-meta">
      <div class="video-meta-left">
        <h3>PROYECTO DEMOSTRATIVO</h3>
        <p>Renders exteriores, ambientación nocturna y visualización arquitectónica.<br>Diseño y producción: Arquentia Studio.</p>
      </div>
      <div class="video-meta-right">
        Formato de entrega
        <span>Video · Renders · Planos</span>
      </div>
    </div>
  </div>
</section>

<!-- QUOTE -->
<section id="quote">
  <p class="quote-text">"La arquitectura no es sólo construcción. Es la materialización de un sueño, la traducción de una idea en un espacio que se vive, se siente y perdura."</p>
  <p class="quote-author">— Arquentia Studio, 2025</p>
</section>

<!-- CONTACT -->
<section id="contacto">
  <div class="section-header">
    <span class="section-label">Hablemos</span>
    <h2 class="section-title">CONTACTO</h2>
    <p class="section-subtitle">Estamos listos para hacer realidad tu proyecto</p>
    <div class="section-rule"></div>
  </div>
  <div class="contact-inner">
    <div class="contact-left">
      <span class="section-label">Información de contacto</span>
      <h3 style="font-family:'Bebas Neue',sans-serif;font-size:2.2rem;letter-spacing:0.08em;color:var(--white);line-height:1.1;">INICIEMOS<br>TU PROYECTO</h3>
      <p style="font-size:0.85rem;color:var(--muted);margin-top:16px;line-height:1.9;">Cuéntanos sobre tu proyecto. Nuestro equipo responderá a la brevedad con una propuesta personalizada para tus necesidades.</p>
      <div class="contact-info">
        <div class="contact-item">
          <span class="ci-icon">📱</span>
          <div>
            <div class="ci-label">WhatsApp</div>
            <div class="ci-value">9932778155</div>
          </div>
        </div>
        <div class="contact-item">
          <span class="ci-icon">✉️</span>
          <div>
            <div class="ci-label">Email</div>
            <div class="ci-value">olivia_morales_h@outlook.es</div>
          </div>
        </div>
        <div class="contact-item">
          <span class="ci-icon">🏢</span>
          <div>
            <div class="ci-label">Servicios</div>
            <div class="ci-value">Arquitectura · Renders · Planos · Interiorismo</div>
          </div>
        </div>
      </div>
    </div>
    <div class="contact-right">
      <div class="contact-card">
        <h3>¿LISTO PARA EMPEZAR?</h3>
        <p>Contáctanos directamente por WhatsApp o correo electrónico. Respondemos en menos de 24 horas y ofrecemos una consulta inicial sin costo.</p>
        <div class="cta-group">
          <a href="https://wa.me/529932778155" class="cta-wa" target="_blank">
            <span>💬</span>
            <span>Escribir por WhatsApp</span>
          </a>
          <a href="mailto:olivia_morales_h@outlook.es" class="cta-email">
            <span>📧</span>
            <span>Enviar un correo</span>
          </a>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-logo">ARQ<span>U</span>ENTIA</div>
  <p class="footer-tagline">diseño. decoración. arquitectura</p>
  <p class="footer-copy">© 2025 Arquentia. Todos los derechos reservados.</p>
</footer>

<script>
  // ── CURSOR ──
  const cursor = document.getElementById('cursor');
  const cursorRing = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;
  document.addEventListener('mousemove', e => { mx = e.clientX; my = e.clientY; });
  function animCursor() {
    cursor.style.left = mx + 'px'; cursor.style.top = my + 'px';
    rx += (mx - rx) * 0.12; ry += (my - ry) * 0.12;
    cursorRing.style.left = rx + 'px'; cursorRing.style.top = ry + 'px';
    requestAnimationFrame(animCursor);
  }
  animCursor();
  document.querySelectorAll('a, button, .service-card, .feature-item').forEach(el => {
    el.addEventListener('mouseenter', () => {
      cursor.style.width = '16px'; cursor.style.height = '16px';
      cursorRing.style.width = '56px'; cursorRing.style.height = '56px';
      cursorRing.style.borderColor = 'var(--cyan)';
    });
    el.addEventListener('mouseleave', () => {
      cursor.style.width = '10px'; cursor.style.height = '10px';
      cursorRing.style.width = '36px'; cursorRing.style.height = '36px';
      cursorRing.style.borderColor = 'var(--cyan-dim)';
    });
  });

  // ── NAV SCROLL ──
  const navbar = document.getElementById('navbar');
  window.addEventListener('scroll', () => {
    navbar.classList.toggle('scrolled', window.scrollY > 60);
  });

  // ── INTERSECTION OBSERVER ──
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) entry.target.classList.add('visible');
    });
  }, { threshold: 0.12 });

  document.querySelectorAll('.section-header, .stat-item, .service-card, .step, .feature-visual, .feature-content, .contact-left, .contact-right, .quote-text, .quote-author, .video-container').forEach(el => observer.observe(el));
</script>
</body>
</html>
