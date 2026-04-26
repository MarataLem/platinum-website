<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SwiftLend — Fast, Transparent Loans</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700;900&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --gold: #C9A84C;
    --gold-light: #F0D98A;
    --gold-dark: #9A7332;
    --ink: #1A1814;
    --ink-soft: #3D3A30;
    --parchment: #FAF8F3;
    --cream: #F2EFE6;
    --muted: #8C8878;
    --border: rgba(201,168,76,0.25);
    --white: #fff;
    --success: #2D7A4F;
    --font-display: 'Playfair Display', Georgia, serif;
    --font-body: 'DM Sans', sans-serif;
  }

  html { scroll-behavior: smooth; }

  body {
    font-family: var(--font-body);
    background: var(--parchment);
    color: var(--ink);
    line-height: 1.7;
    font-size: 16px;
  }

  /* NAV */
  nav {
    position: sticky; top: 0; z-index: 100;
    background: rgba(250,248,243,0.95);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid var(--border);
    padding: 0 5%;
    display: flex; align-items: center; justify-content: space-between;
    height: 68px;
  }
  .nav-brand {
    font-family: var(--font-display);
    font-size: 1.6rem; font-weight: 700;
    color: var(--ink);
    text-decoration: none;
    display: flex; align-items: center; gap: 10px;
  }
  .nav-brand span { color: var(--gold); }
  .nav-logo-mark {
    width: 34px; height: 34px;
    background: var(--gold);
    border-radius: 8px;
    display: grid; place-items: center;
    font-family: var(--font-display);
    font-size: 1.1rem; font-weight: 900;
    color: var(--white);
  }
  .nav-links {
    display: flex; align-items: center; gap: 2rem;
    list-style: none;
  }
  .nav-links a {
    text-decoration: none;
    color: var(--ink-soft);
    font-size: 0.9rem; font-weight: 500;
    letter-spacing: 0.02em;
    transition: color 0.2s;
  }
  .nav-links a:hover { color: var(--gold-dark); }
  .btn-nav {
    background: var(--ink);
    color: var(--white) !important;
    padding: 8px 22px;
    border-radius: 6px;
    font-size: 0.85rem !important;
    transition: background 0.2s !important;
  }
  .btn-nav:hover { background: var(--gold-dark) !important; color: var(--white) !important; }

  /* HERO */
  .hero {
    min-height: 92vh;
    display: grid; grid-template-columns: 1fr 1fr;
    align-items: center;
    padding: 5rem 5% 3rem;
    gap: 4rem;
    position: relative;
    overflow: hidden;
  }
  .hero::before {
    content: '';
    position: absolute; inset: 0;
    background: radial-gradient(ellipse 70% 60% at 60% 50%, rgba(201,168,76,0.08) 0%, transparent 70%);
    pointer-events: none;
  }
  .hero-text { position: relative; z-index: 1; }
  .hero-eyebrow {
    display: inline-flex; align-items: center; gap: 8px;
    font-size: 0.78rem; font-weight: 600; letter-spacing: 0.12em;
    text-transform: uppercase; color: var(--gold-dark);
    background: rgba(201,168,76,0.12);
    border: 1px solid var(--border);
    padding: 6px 14px; border-radius: 100px;
    margin-bottom: 1.5rem;
  }
  .hero-eyebrow::before { content: '●'; font-size: 0.5rem; }
  h1 {
    font-family: var(--font-display);
    font-size: clamp(2.8rem, 5vw, 4.2rem);
    font-weight: 900;
    line-height: 1.1;
    color: var(--ink);
    margin-bottom: 1.5rem;
  }
  h1 em {
    font-style: normal;
    color: var(--gold);
    position: relative;
  }
  h1 em::after {
    content: '';
    position: absolute; bottom: 4px; left: 0; right: 0;
    height: 3px;
    background: var(--gold-light);
    border-radius: 2px;
  }
  .hero-sub {
    font-size: 1.15rem; color: var(--muted);
    max-width: 440px; margin-bottom: 2.5rem;
    font-weight: 300;
  }
  .hero-cta {
    display: flex; gap: 1rem; flex-wrap: wrap; align-items: center;
  }
  .btn-primary {
    display: inline-block;
    background: var(--gold);
    color: var(--ink);
    padding: 14px 34px;
    border-radius: 8px;
    font-family: var(--font-body);
    font-weight: 600; font-size: 0.95rem;
    text-decoration: none;
    border: none; cursor: pointer;
    transition: all 0.2s;
    letter-spacing: 0.01em;
  }
  .btn-primary:hover { background: var(--gold-dark); color: var(--white); transform: translateY(-1px); }
  .btn-ghost {
    display: inline-flex; align-items: center; gap: 8px;
    color: var(--ink-soft);
    font-weight: 500; font-size: 0.95rem;
    text-decoration: none;
    background: none; border: none; cursor: pointer;
    transition: color 0.2s;
  }
  .btn-ghost:hover { color: var(--gold-dark); }
  .btn-ghost svg { transition: transform 0.2s; }
  .btn-ghost:hover svg { transform: translateX(3px); }
  .hero-stats {
    display: flex; gap: 2.5rem; margin-top: 3rem;
    padding-top: 2rem;
    border-top: 1px solid var(--border);
  }
  .stat-item { text-align: left; }
  .stat-value {
    font-family: var(--font-display);
    font-size: 1.8rem; font-weight: 700;
    color: var(--ink);
    display: block;
  }
  .stat-label {
    font-size: 0.8rem; color: var(--muted);
    font-weight: 400; letter-spacing: 0.04em;
  }

  /* CALCULATOR */
  .hero-calc {
    background: var(--white);
    border: 1px solid var(--border);
    border-radius: 20px;
    padding: 2.5rem;
    box-shadow: 0 24px 80px rgba(26,24,20,0.08);
    position: relative; z-index: 1;
  }
  .calc-title {
    font-family: var(--font-display);
    font-size: 1.3rem; font-weight: 700;
    margin-bottom: 0.3rem;
  }
  .calc-sub { font-size: 0.85rem; color: var(--muted); margin-bottom: 2rem; }
  .calc-field { margin-bottom: 1.5rem; }
  .calc-field label {
    display: flex; justify-content: space-between;
    font-size: 0.82rem; font-weight: 600;
    color: var(--ink-soft); margin-bottom: 8px;
    text-transform: uppercase; letter-spacing: 0.05em;
  }
  .calc-field label span {
    font-family: var(--font-display);
    font-size: 1rem; font-weight: 700;
    color: var(--ink); text-transform: none; letter-spacing: 0;
  }
  input[type="range"] {
    width: 100%; -webkit-appearance: none;
    height: 4px;
    background: linear-gradient(to right, var(--gold) 0%, var(--gold) var(--pct, 50%), #E2DDD0 var(--pct, 50%), #E2DDD0 100%);
    border-radius: 2px; outline: none; cursor: pointer;
  }
  input[type="range"]::-webkit-slider-thumb {
    -webkit-appearance: none;
    width: 20px; height: 20px;
    border-radius: 50%;
    background: var(--white);
    border: 2px solid var(--gold);
    box-shadow: 0 2px 8px rgba(201,168,76,0.3);
    cursor: pointer;
  }
  .calc-result {
    background: var(--parchment);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 1.25rem;
    margin-top: 1.5rem;
    display: grid; grid-template-columns: 1fr 1fr 1fr;
    gap: 1rem;
    text-align: center;
  }
  .result-item .r-val {
    font-family: var(--font-display);
    font-size: 1.4rem; font-weight: 700;
    color: var(--ink); display: block;
  }
  .result-item .r-lbl {
    font-size: 0.72rem; color: var(--muted);
    font-weight: 500; letter-spacing: 0.04em; text-transform: uppercase;
  }
  .calc-apply {
    display: block; width: 100%;
    margin-top: 1.5rem;
    background: var(--ink); color: var(--white);
    padding: 14px;
    border: none; border-radius: 10px;
    font-family: var(--font-body);
    font-size: 1rem; font-weight: 600;
    cursor: pointer; transition: background 0.2s;
    text-align: center; text-decoration: none;
  }
  .calc-apply:hover { background: var(--gold-dark); }

  /* SECTION SHARED */
  section { padding: 5rem 5%; }
  .section-label {
    font-size: 0.75rem; font-weight: 600; letter-spacing: 0.14em;
    text-transform: uppercase; color: var(--gold-dark);
    margin-bottom: 1rem;
  }
  h2 {
    font-family: var(--font-display);
    font-size: clamp(1.8rem, 3vw, 2.6rem);
    font-weight: 700; line-height: 1.2;
    color: var(--ink);
  }
  .section-head { max-width: 560px; }
  .section-sub {
    font-size: 1.05rem; color: var(--muted);
    margin-top: 0.75rem; font-weight: 300;
  }

  /* LOAN TYPES */
  .loans-section { background: var(--cream); }
  .loans-grid {
    display: grid; grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 1.25rem; margin-top: 3rem;
  }
  .loan-card {
    background: var(--white);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 2rem;
    transition: all 0.25s;
    cursor: pointer;
    position: relative; overflow: hidden;
  }
  .loan-card::after {
    content: '';
    position: absolute; bottom: 0; left: 0; right: 0;
    height: 3px;
    background: var(--gold);
    transform: scaleX(0); transform-origin: left;
    transition: transform 0.3s;
  }
  .loan-card:hover { box-shadow: 0 16px 48px rgba(26,24,20,0.1); transform: translateY(-3px); }
  .loan-card:hover::after { transform: scaleX(1); }
  .loan-icon {
    width: 52px; height: 52px;
    background: rgba(201,168,76,0.1);
    border-radius: 12px;
    display: grid; place-items: center;
    font-size: 1.5rem; margin-bottom: 1.25rem;
  }
  .loan-card h3 {
    font-family: var(--font-display);
    font-size: 1.2rem; font-weight: 700;
    margin-bottom: 0.5rem;
  }
  .loan-card p { font-size: 0.88rem; color: var(--muted); line-height: 1.6; }
  .loan-rate {
    display: inline-block;
    margin-top: 1rem;
    font-size: 0.8rem; font-weight: 600;
    color: var(--gold-dark);
    background: rgba(201,168,76,0.1);
    padding: 4px 12px; border-radius: 100px;
  }

  /* HOW IT WORKS */
  .how-grid {
    display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 2rem; margin-top: 3.5rem;
    position: relative;
  }
  .how-grid::before {
    content: '';
    position: absolute; top: 28px; left: 5%; right: 5%;
    height: 1px;
    background: repeating-linear-gradient(to right, var(--border) 0, var(--border) 6px, transparent 6px, transparent 14px);
  }
  .step {
    text-align: center;
    position: relative; z-index: 1;
  }
  .step-num {
    width: 56px; height: 56px; border-radius: 50%;
    background: var(--white);
    border: 2px solid var(--gold);
    display: inline-flex; align-items: center; justify-content: center;
    font-family: var(--font-display);
    font-size: 1.3rem; font-weight: 700; color: var(--gold-dark);
    margin: 0 auto 1.25rem;
    box-shadow: 0 4px 16px rgba(201,168,76,0.2);
  }
  .step h3 {
    font-family: var(--font-display);
    font-size: 1.1rem; font-weight: 700;
    margin-bottom: 0.5rem;
  }
  .step p { font-size: 0.88rem; color: var(--muted); max-width: 200px; margin: 0 auto; }

  /* FEATURES */
  .features-section {
    background: var(--ink);
    color: var(--white);
  }
  .features-section .section-label { color: var(--gold-light); }
  .features-section h2 { color: var(--white); }
  .features-section .section-sub { color: rgba(255,255,255,0.5); }
  .features-grid {
    display: grid; grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
    gap: 1.5rem; margin-top: 3rem;
  }
  .feature-card {
    background: rgba(255,255,255,0.05);
    border: 1px solid rgba(255,255,255,0.1);
    border-radius: 16px; padding: 2rem;
    transition: background 0.2s;
  }
  .feature-card:hover { background: rgba(201,168,76,0.1); border-color: rgba(201,168,76,0.3); }
  .feature-icon {
    font-size: 1.75rem; margin-bottom: 1rem;
  }
  .feature-card h3 {
    font-family: var(--font-display);
    font-size: 1.1rem; font-weight: 700;
    color: var(--white); margin-bottom: 0.5rem;
  }
  .feature-card p { font-size: 0.88rem; color: rgba(255,255,255,0.5); line-height: 1.6; }

  /* TESTIMONIALS */
  .testimonials-section { background: var(--parchment); }
  .testi-grid {
    display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1.5rem; margin-top: 3rem;
  }
  .testi-card {
    background: var(--white);
    border: 1px solid var(--border);
    border-radius: 16px; padding: 2rem;
  }
  .stars { color: var(--gold); font-size: 0.85rem; margin-bottom: 1rem; letter-spacing: 3px; }
  .testi-card blockquote {
    font-size: 0.95rem; color: var(--ink-soft);
    font-style: italic; line-height: 1.7;
    margin-bottom: 1.5rem;
  }
  .testi-author { display: flex; align-items: center; gap: 12px; }
  .testi-avatar {
    width: 40px; height: 40px; border-radius: 50%;
    display: grid; place-items: center;
    font-weight: 700; font-size: 0.85rem; color: var(--white);
  }
  .testi-name { font-weight: 600; font-size: 0.9rem; }
  .testi-meta { font-size: 0.78rem; color: var(--muted); }

  /* APPLY CTA */
  .cta-section {
    background: linear-gradient(135deg, var(--gold-dark) 0%, var(--gold) 50%, var(--gold-light) 100%);
    text-align: center; padding: 6rem 5%;
  }
  .cta-section h2 { color: var(--ink); font-size: clamp(2rem, 4vw, 3rem); }
  .cta-section p { color: var(--ink-soft); font-size: 1.1rem; margin: 1rem auto 2.5rem; max-width: 500px; }
  .btn-dark {
    display: inline-block;
    background: var(--ink); color: var(--white);
    padding: 15px 40px; border-radius: 8px;
    font-weight: 600; font-size: 1rem;
    text-decoration: none; transition: all 0.2s;
  }
  .btn-dark:hover { background: #000; transform: translateY(-2px); }

  /* FAQ */
  .faq-section { background: var(--cream); }
  .faq-wrap { max-width: 720px; margin: 3rem auto 0; }
  .faq-item {
    border-bottom: 1px solid var(--border);
    padding: 1.25rem 0;
  }
  .faq-q {
    display: flex; justify-content: space-between; align-items: center;
    font-weight: 600; cursor: pointer;
    gap: 1rem;
    font-size: 0.95rem;
  }
  .faq-arrow {
    width: 24px; height: 24px; min-width: 24px;
    border-radius: 50%;
    border: 1px solid var(--border);
    display: grid; place-items: center;
    transition: transform 0.3s, background 0.2s;
    font-size: 0.9rem;
    color: var(--muted);
  }
  .faq-item.open .faq-arrow {
    transform: rotate(45deg);
    background: var(--gold); color: var(--ink);
    border-color: var(--gold);
  }
  .faq-a {
    max-height: 0; overflow: hidden;
    transition: max-height 0.4s ease;
    font-size: 0.9rem; color: var(--muted);
  }
  .faq-item.open .faq-a { max-height: 200px; padding-top: 0.75rem; }

  /* FOOTER */
  footer {
    background: var(--ink); color: rgba(255,255,255,0.6);
    padding: 4rem 5% 2rem;
  }
  .footer-top {
    display: grid; grid-template-columns: 2fr 1fr 1fr 1fr;
    gap: 3rem; margin-bottom: 3rem;
  }
  .footer-brand {
    font-family: var(--font-display);
    font-size: 1.5rem; font-weight: 700;
    color: var(--white); margin-bottom: 1rem;
  }
  .footer-brand span { color: var(--gold); }
  .footer-desc { font-size: 0.85rem; line-height: 1.7; max-width: 260px; }
  .footer-col h4 {
    font-size: 0.8rem; font-weight: 600;
    letter-spacing: 0.1em; text-transform: uppercase;
    color: var(--white); margin-bottom: 1rem;
  }
  .footer-col ul { list-style: none; }
  .footer-col li { margin-bottom: 0.6rem; }
  .footer-col a { color: rgba(255,255,255,0.5); text-decoration: none; font-size: 0.88rem; transition: color 0.2s; }
  .footer-col a:hover { color: var(--gold-light); }
  .footer-bottom {
    border-top: 1px solid rgba(255,255,255,0.1);
    padding-top: 1.5rem;
    display: flex; justify-content: space-between; align-items: center;
    flex-wrap: wrap; gap: 1rem;
    font-size: 0.8rem;
  }

  /* APPLICATION MODAL */
  .modal-overlay {
    display: none; position: fixed; inset: 0;
    background: rgba(26,24,20,0.7);
    z-index: 200; align-items: center; justify-content: center;
    backdrop-filter: blur(6px);
  }
  .modal-overlay.show { display: flex; }
  .modal {
    background: var(--white);
    border-radius: 20px; padding: 2.5rem;
    width: min(600px, 90vw);
    max-height: 90vh; overflow-y: auto;
    position: relative;
    animation: modalIn 0.3s ease;
  }
  @keyframes modalIn {
    from { opacity: 0; transform: translateY(30px) scale(0.97); }
    to { opacity: 1; transform: translateY(0) scale(1); }
  }
  .modal-close {
    position: absolute; top: 1.25rem; right: 1.25rem;
    width: 32px; height: 32px; border-radius: 50%;
    border: 1px solid var(--border);
    background: none; cursor: pointer;
    font-size: 1rem; color: var(--muted);
    display: grid; place-items: center;
    transition: all 0.2s;
  }
  .modal-close:hover { background: var(--cream); color: var(--ink); }
  .modal h3 { font-family: var(--font-display); font-size: 1.6rem; font-weight: 700; margin-bottom: 0.25rem; }
  .modal-sub { font-size: 0.88rem; color: var(--muted); margin-bottom: 2rem; }
  .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 1rem; margin-bottom: 1rem; }
  .form-field { display: flex; flex-direction: column; gap: 6px; }
  .form-field.full { grid-column: 1 / -1; }
  .form-field label { font-size: 0.8rem; font-weight: 600; color: var(--ink-soft); text-transform: uppercase; letter-spacing: 0.05em; }
  .form-field input, .form-field select {
    border: 1px solid #DDD9CE;
    border-radius: 8px; padding: 10px 14px;
    font-family: var(--font-body); font-size: 0.95rem;
    color: var(--ink); background: var(--parchment);
    transition: border-color 0.2s;
    -webkit-appearance: none; appearance: none;
  }
  .form-field input:focus, .form-field select:focus {
    outline: none;
    border-color: var(--gold);
    box-shadow: 0 0 0 3px rgba(201,168,76,0.15);
  }
  .form-submit {
    display: block; width: 100%;
    background: var(--gold); color: var(--ink);
    padding: 14px; border: none; border-radius: 10px;
    font-family: var(--font-body); font-size: 1rem; font-weight: 600;
    cursor: pointer; margin-top: 1.5rem; transition: all 0.2s;
  }
  .form-submit:hover { background: var(--gold-dark); color: var(--white); }
  .form-note { font-size: 0.78rem; color: var(--muted); text-align: center; margin-top: 0.75rem; }

  /* SUCCESS STATE */
  .success-state { text-align: center; padding: 2rem 0; display: none; }
  .success-icon { font-size: 3rem; margin-bottom: 1rem; }
  .success-state h3 { font-family: var(--font-display); font-size: 1.8rem; }
  .success-state p { color: var(--muted); margin-top: 0.5rem; }

  @media (max-width: 768px) {
    .hero { grid-template-columns: 1fr; padding: 3rem 5%; }
    .hero-calc { order: -1; }
    .hero-stats { gap: 1.5rem; }
    .how-grid::before { display: none; }
    .footer-top { grid-template-columns: 1fr 1fr; }
    .form-row { grid-template-columns: 1fr; }
    nav .nav-links { display: none; }
  }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <a class="nav-brand" href="#">
    <div class="nav-logo-mark">S</div>
    Swift<span>Lend</span>
  </a>
  <ul class="nav-links">
    <li><a href="#loans">Loan Types</a></li>
    <li><a href="#how">How It Works</a></li>
    <li><a href="#faq">FAQ</a></li>
    <li><a href="#apply" class="btn-nav" onclick="openModal(event)">Apply Now</a></li>
  </ul>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="hero-text">
    <div class="hero-eyebrow">Trusted since 2014</div>
    <h1>Fast loans,<br>built around <em>your</em> life.</h1>
    <p class="hero-sub">Get the funds you need — quickly, fairly, and with complete transparency. No hidden fees, no surprises.</p>
    <div class="hero-cta">
      <button class="btn-primary" onclick="openModal(event)">Apply in Minutes</button>
      <a href="#how" class="btn-ghost">
        See how it works
        <svg width="16" height="16" viewBox="0 0 16 16" fill="none">
          <path d="M3 8h10M9 4l4 4-4 4" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
      </a>
    </div>
    <div class="hero-stats">
      <div class="stat-item">
        <span class="stat-value">$2.4B+</span>
        <span class="stat-label">Total funded</span>
      </div>
      <div class="stat-item">
        <span class="stat-value">95K+</span>
        <span class="stat-label">Happy borrowers</span>
      </div>
      <div class="stat-item">
        <span class="stat-value">4.9★</span>
        <span class="stat-label">Customer rating</span>
      </div>
    </div>
  </div>

  <div class="hero-calc">
    <p class="calc-title">Loan Calculator</p>
    <p class="calc-sub">Estimate your monthly payment instantly</p>

    <div class="calc-field">
      <label>Loan Amount <span id="amt-display">$15,000</span></label>
      <input type="range" id="loan-amt" min="1000" max="100000" step="500" value="15000" oninput="calcUpdate()">
    </div>
    <div class="calc-field">
      <label>Loan Term <span id="term-display">36 months</span></label>
      <input type="range" id="loan-term" min="6" max="84" step="6" value="36" oninput="calcUpdate()">
    </div>
    <div class="calc-field">
      <label>Interest Rate <span id="rate-display">8.5%</span></label>
      <input type="range" id="loan-rate" min="3" max="25" step="0.5" value="8.5" oninput="calcUpdate()">
    </div>

    <div class="calc-result">
      <div class="result-item">
        <span class="r-val" id="r-monthly">$473</span>
        <span class="r-lbl">/ month</span>
      </div>
      <div class="result-item">
        <span class="r-val" id="r-total">$17,028</span>
        <span class="r-lbl">Total repaid</span>
      </div>
      <div class="result-item">
        <span class="r-val" id="r-interest">$2,028</span>
        <span class="r-lbl">Interest</span>
      </div>
    </div>

    <button class="calc-apply" onclick="openModal(event)">Apply for This Loan →</button>
  </div>
</section>

<!-- LOAN TYPES -->
<section class="loans-section" id="loans">
  <p class="section-label">Our Products</p>
  <div class="section-head">
    <h2>A loan for every need</h2>
    <p class="section-sub">Flexible options designed to fit your unique financial situation.</p>
  </div>
  <div class="loans-grid">
    <div class="loan-card">
      <div class="loan-icon">🏠</div>
      <h3>Home Loans</h3>
      <p>Purchase your dream home or refinance your existing mortgage with our competitive rates and flexible terms.</p>
      <span class="loan-rate">From 3.9% APR</span>
    </div>
    <div class="loan-card">
      <div class="loan-icon">🚗</div>
      <h3>Auto Loans</h3>
      <p>Finance a new or used vehicle with fast approval and same-day funding available for qualifying applicants.</p>
      <span class="loan-rate">From 4.5% APR</span>
    </div>
    <div class="loan-card">
      <div class="loan-icon">💼</div>
      <h3>Personal Loans</h3>
      <p>Debt consolidation, medical bills, home improvement — get up to $100,000 with no collateral required.</p>
      <span class="loan-rate">From 6.9% APR</span>
    </div>
    <div class="loan-card">
      <div class="loan-icon">🏢</div>
      <h3>Business Loans</h3>
      <p>Fund your growth, equipment, or working capital needs with loan solutions tailored for small businesses.</p>
      <span class="loan-rate">From 7.2% APR</span>
    </div>
    <div class="loan-card">
      <div class="loan-icon">🎓</div>
      <h3>Student Loans</h3>
      <p>Invest in your future with education financing that offers flexible repayment once you graduate.</p>
      <span class="loan-rate">From 5.5% APR</span>
    </div>
    <div class="loan-card">
      <div class="loan-icon">🔄</div>
      <h3>Debt Consolidation</h3>
      <p>Simplify multiple high-interest debts into one affordable monthly payment and potentially save thousands.</p>
      <span class="loan-rate">From 6.2% APR</span>
    </div>
  </div>
</section>

<!-- HOW IT WORKS -->
<section id="how">
  <div style="text-align: center;">
    <p class="section-label">Simple Process</p>
    <h2>From application to funding in 3 steps</h2>
    <p class="section-sub" style="margin: 0 auto; max-width: 500px;">We've eliminated the paperwork. Most applicants receive a decision within minutes.</p>
  </div>
  <div class="how-grid">
    <div class="step">
      <div class="step-num">1</div>
      <h3>Apply Online</h3>
      <p>Fill out our 5-minute application. No hard credit check required to see your rates.</p>
    </div>
    <div class="step">
      <div class="step-num">2</div>
      <h3>Get Approved</h3>
      <p>Receive an instant decision. Our team reviews your application and confirms the offer.</p>
    </div>
    <div class="step">
      <div class="step-num">3</div>
      <h3>Receive Funds</h3>
      <p>Accept your offer and receive funds directly to your bank account, often within 24 hours.</p>
    </div>
    <div class="step">
      <div class="step-num">4</div>
      <h3>Repay Easily</h3>
      <p>Set up autopay for automatic monthly deductions. Manage everything from your dashboard.</p>
    </div>
  </div>
</section>

<!-- FEATURES -->
<section class="features-section">
  <p class="section-label">Why SwiftLend</p>
  <div class="section-head">
    <h2 style="color: var(--white);">Banking-grade security.<br>Human-grade care.</h2>
    <p class="section-sub">We combine technology with genuine support so you always feel confident.</p>
  </div>
  <div class="features-grid">
    <div class="feature-card">
      <div class="feature-icon">🔒</div>
      <h3>256-bit Encryption</h3>
      <p>Your personal and financial data is protected with the same encryption used by top banks worldwide.</p>
    </div>
    <div class="feature-card">
      <div class="feature-icon">⚡</div>
      <h3>Instant Decisions</h3>
      <p>Our AI-powered underwriting system delivers loan decisions in seconds — not days or weeks.</p>
    </div>
    <div class="feature-card">
      <div class="feature-icon">💳</div>
      <h3>No Hidden Fees</h3>
      <p>The APR you see is the APR you pay. We believe in full transparency with no surprise charges.</p>
    </div>
    <div class="feature-card">
      <div class="feature-icon">📱</div>
      <h3>Mobile Dashboard</h3>
      <p>Track payments, view statements, and manage your loan entirely from your smartphone.</p>
    </div>
    <div class="feature-card">
      <div class="feature-icon">🤝</div>
      <h3>Dedicated Support</h3>
      <p>Real loan specialists available 7 days a week via phone, chat, or email — no bots.</p>
    </div>
    <div class="feature-card">
      <div class="feature-icon">🌱</div>
      <h3>Credit Building</h3>
      <p>On-time payments are reported to all three major credit bureaus to help improve your score.</p>
    </div>
  </div>
</section>

<!-- TESTIMONIALS -->
<section class="testimonials-section">
  <p class="section-label">Real Stories</p>
  <h2>People who chose SwiftLend</h2>
  <div class="testi-grid">
    <div class="testi-card">
      <div class="stars">★★★★★</div>
      <blockquote>"I was shocked how fast everything moved. Applied in the morning, had the money in my account by the next day. No complicated forms, just a clean simple process."</blockquote>
      <div class="testi-author">
        <div class="testi-avatar" style="background: #2D5FAA;">JM</div>
        <div>
          <p class="testi-name">James M.</p>
          <p class="testi-meta">Personal Loan, $25,000</p>
        </div>
      </div>
    </div>
    <div class="testi-card">
      <div class="stars">★★★★★</div>
      <blockquote>"Used SwiftLend to consolidate three credit cards. My monthly payment dropped by $340 and I'm actually paying down the principal now. Wish I'd done this sooner."</blockquote>
      <div class="testi-author">
        <div class="testi-avatar" style="background: var(--success);">SA</div>
        <div>
          <p class="testi-name">Sarah A.</p>
          <p class="testi-meta">Debt Consolidation, $42,000</p>
        </div>
      </div>
    </div>
    <div class="testi-card">
      <div class="stars">★★★★★</div>
      <blockquote>"The business loan process was surprisingly smooth. The team was responsive and actually understood what a growing business needs. Highly recommend to other entrepreneurs."</blockquote>
      <div class="testi-author">
        <div class="testi-avatar" style="background: #9A7332;">TC</div>
        <div>
          <p class="testi-name">Tariq C.</p>
          <p class="testi-meta">Business Loan, $80,000</p>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- CTA BANNER -->
<section class="cta-section">
  <h2>Ready to get started?</h2>
  <p>Check your rate in minutes with no impact to your credit score.</p>
  <a href="#apply" class="btn-dark" onclick="openModal(event)">Apply Now — It's Free</a>
</section>

<!-- FAQ -->
<section class="faq-section" id="faq">
  <p class="section-label">Common Questions</p>
  <h2 style="text-align: center;">Frequently asked</h2>
  <div class="faq-wrap">
    <div class="faq-item">
      <div class="faq-q" onclick="toggleFaq(this)">
        Will checking my rate affect my credit score?
        <span class="faq-arrow">+</span>
      </div>
      <div class="faq-a">No. Checking your rate uses a soft credit inquiry, which has no impact on your credit score. Only if you proceed and accept a loan offer will a hard inquiry be placed, which may have a small, temporary effect.</div>
    </div>
    <div class="faq-item">
      <div class="faq-q" onclick="toggleFaq(this)">
        How quickly will I receive my funds?
        <span class="faq-arrow">+</span>
      </div>
      <div class="faq-a">Once your loan is approved and you've accepted the offer, funds are typically deposited within 1–3 business days. Many customers see funds within 24 hours depending on their bank's processing times.</div>
    </div>
    <div class="faq-item">
      <div class="faq-q" onclick="toggleFaq(this)">
        What credit score do I need to qualify?
        <span class="faq-arrow">+</span>
      </div>
      <div class="faq-a">We consider applicants with credit scores of 580 and above. However, a higher score will qualify you for better rates. We also consider income, employment history, and other financial factors in our decision.</div>
    </div>
    <div class="faq-item">
      <div class="faq-q" onclick="toggleFaq(this)">
        Are there any prepayment penalties?
        <span class="faq-arrow">+</span>
      </div>
      <div class="faq-a">Absolutely not. We encourage you to pay off your loan early if you're able to. There are no prepayment fees or penalties of any kind. You'll simply save on the remaining interest.</div>
    </div>
    <div class="faq-item">
      <div class="faq-q" onclick="toggleFaq(this)">
        What documents will I need to apply?
        <span class="faq-arrow">+</span>
      </div>
      <div class="faq-a">Most applicants only need a government-issued ID, proof of income (recent pay stubs or tax returns), and your bank account details for disbursement. Our system handles verification automatically in most cases.</div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-top">
    <div>
      <p class="footer-brand">Swift<span>Lend</span></p>
      <p class="footer-desc">Making loans fast, fair, and transparent since 2014. FDIC-insured deposits. Licensed lender in all 50 states.</p>
    </div>
    <div class="footer-col">
      <h4>Products</h4>
      <ul>
        <li><a href="#">Personal Loans</a></li>
        <li><a href="#">Home Loans</a></li>
        <li><a href="#">Auto Loans</a></li>
        <li><a href="#">Business Loans</a></li>
        <li><a href="#">Student Loans</a></li>
      </ul>
    </div>
    <div class="footer-col">
      <h4>Company</h4>
      <ul>
        <li><a href="#">About Us</a></li>
        <li><a href="#">Careers</a></li>
        <li><a href="#">Press</a></li>
        <li><a href="#">Blog</a></li>
        <li><a href="#">Contact</a></li>
      </ul>
    </div>
    <div class="footer-col">
      <h4>Legal</h4>
      <ul>
        <li><a href="#">Privacy Policy</a></li>
        <li><a href="#">Terms of Service</a></li>
        <li><a href="#">Disclosures</a></li>
        <li><a href="#">Licenses</a></li>
        <li><a href="#">Accessibility</a></li>
      </ul>
    </div>
  </div>
  <div class="footer-bottom">
    <p>© 2026 SwiftLend Financial, Inc. All rights reserved. Loans are subject to credit approval. APR ranges vary based on creditworthiness.</p>
    <p>NMLS #1234567</p>
  </div>
</footer>

<!-- APPLICATION MODAL -->
<div class="modal-overlay" id="modal" onclick="closeModalOutside(event)">
  <div class="modal">
    <button class="modal-close" onclick="closeModal()">✕</button>
    <div id="form-state">
      <h3>Start Your Application</h3>
      <p class="modal-sub">Takes about 5 minutes. No hard credit check at this stage.</p>
      <div class="form-row">
        <div class="form-field">
          <label>First Name</label>
          <input type="text" placeholder="Jane">
        </div>
        <div class="form-field">
          <label>Last Name</label>
          <input type="text" placeholder="Smith">
        </div>
        <div class="form-field">
          <label>Email Address</label>
          <input type="email" placeholder="jane@email.com">
        </div>
        <div class="form-field">
          <label>Phone Number</label>
          <input type="tel" placeholder="(555) 000-0000">
        </div>
        <div class="form-field">
          <label>Loan Type</label>
          <select>
            <option>Personal Loan</option>
            <option>Home Loan</option>
            <option>Auto Loan</option>
            <option>Business Loan</option>
            <option>Student Loan</option>
            <option>Debt Consolidation</option>
          </select>
        </div>
        <div class="form-field">
          <label>Loan Amount</label>
          <input type="text" placeholder="$15,000">
        </div>
        <div class="form-field">
          <label>Employment Status</label>
          <select>
            <option>Employed Full-Time</option>
            <option>Employed Part-Time</option>
            <option>Self-Employed</option>
            <option>Retired</option>
            <option>Other</option>
          </select>
        </div>
        <div class="form-field">
          <label>Annual Income</label>
          <input type="text" placeholder="$60,000">
        </div>
        <div class="form-field full">
          <label>Purpose of Loan</label>
          <input type="text" placeholder="e.g., Home renovation, debt consolidation...">
        </div>
      </div>
      <button class="form-submit" onclick="submitForm()">Check My Rate →</button>
      <p class="form-note">🔒 256-bit SSL encrypted. We never sell your information.</p>
    </div>
    <div class="success-state" id="success-state">
      <div class="success-icon">🎉</div>
      <h3>Application Received!</h3>
      <p>We'll review your details and send your personalized rate options to your email within minutes.</p>
      <button class="calc-apply" style="margin-top: 2rem; width: auto; padding: 12px 32px; display: inline-block;" onclick="closeModal()">Close</button>
    </div>
  </div>
</div>

<script>
  function calcUpdate() {
    const amt = +document.getElementById('loan-amt').value;
    const months = +document.getElementById('loan-term').value;
    const rate = +document.getElementById('loan-rate').value;

    document.getElementById('amt-display').textContent = '$' + amt.toLocaleString();
    document.getElementById('term-display').textContent = months + ' months';
    document.getElementById('rate-display').textContent = rate.toFixed(1) + '%';

    const r = rate / 100 / 12;
    const monthly = r === 0 ? amt / months : (amt * r * Math.pow(1+r, months)) / (Math.pow(1+r, months) - 1);
    const total = monthly * months;
    const interest = total - amt;

    document.getElementById('r-monthly').textContent = '$' + Math.round(monthly).toLocaleString();
    document.getElementById('r-total').textContent = '$' + Math.round(total).toLocaleString();
    document.getElementById('r-interest').textContent = '$' + Math.round(interest).toLocaleString();

    document.querySelectorAll('input[type="range"]').forEach(input => {
      const pct = ((input.value - input.min) / (input.max - input.min)) * 100;
      input.style.setProperty('--pct', pct + '%');
    });
  }

  function toggleFaq(el) {
    const item = el.closest('.faq-item');
    item.classList.toggle('open');
  }

  function openModal(e) {
    e.preventDefault();
    document.getElementById('modal').classList.add('show');
    document.body.style.overflow = 'hidden';
  }

  function closeModal() {
    document.getElementById('modal').classList.remove('show');
    document.body.style.overflow = '';
  }

  function closeModalOutside(e) {
    if (e.target === document.getElementById('modal')) closeModal();
  }

  function submitForm() {
    document.getElementById('form-state').style.display = 'none';
    document.getElementById('success-state').style.display = 'block';
  }

  calcUpdate();
</script>
</body>
</html>
