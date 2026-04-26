<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>SwiftLend — Fast, Fair Loans</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --gold: #C9963A;
    --gold-light: #F5E6C8;
    --gold-dark: #8A6220;
    --navy: #0D1B2A;
    --navy-mid: #162840;
    --navy-light: #1E3A55;
    --cream: #FAF7F2;
    --text: #0D1B2A;
    --text-muted: #5A6A7A;
    --white: #FFFFFF;
    --radius: 12px;
  }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--cream);
    color: var(--text);
    line-height: 1.6;
  }

  /* NAV */
  nav {
    position: fixed; top: 0; left: 0; right: 0; z-index: 100;
    background: rgba(13, 27, 42, 0.97);
    backdrop-filter: blur(12px);
    padding: 0 5%;
    display: flex; align-items: center; justify-content: space-between;
    height: 68px;
    border-bottom: 1px solid rgba(201,150,58,0.2);
  }

  .logo {
    font-family: 'Playfair Display', serif;
    font-size: 1.6rem;
    color: var(--gold);
    letter-spacing: 0.02em;
    text-decoration: none;
  }

  .logo span { color: #fff; }

  nav ul {
    list-style: none;
    display: flex; gap: 2.5rem;
  }

  nav ul a {
    color: rgba(255,255,255,0.75);
    text-decoration: none;
    font-size: 0.88rem;
    font-weight: 500;
    letter-spacing: 0.04em;
    text-transform: uppercase;
    transition: color 0.2s;
  }

  nav ul a:hover { color: var(--gold); }

  .nav-cta {
    background: var(--gold);
    color: var(--navy) !important;
    padding: 0.5rem 1.2rem;
    border-radius: 6px;
    font-weight: 600 !important;
    transition: background 0.2s !important;
  }

  .nav-cta:hover { background: #daa94a !important; color: var(--navy) !important; }

  /* HERO */
  .hero {
    min-height: 100vh;
    background: var(--navy);
    display: flex; align-items: center;
    padding: 100px 5% 60px;
    position: relative;
    overflow: hidden;
  }

  .hero::before {
    content: '';
    position: absolute;
    top: -200px; right: -200px;
    width: 700px; height: 700px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(201,150,58,0.12) 0%, transparent 70%);
    pointer-events: none;
  }

  .hero::after {
    content: '';
    position: absolute;
    bottom: -150px; left: -100px;
    width: 500px; height: 500px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(201,150,58,0.07) 0%, transparent 70%);
    pointer-events: none;
  }

  .hero-inner {
    max-width: 1200px; margin: 0 auto; width: 100%;
    display: grid; grid-template-columns: 1fr 1fr; gap: 4rem; align-items: center;
  }

  .hero-tag {
    display: inline-block;
    background: rgba(201,150,58,0.15);
    color: var(--gold);
    font-size: 0.78rem;
    font-weight: 600;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 6px 14px;
    border-radius: 100px;
    border: 1px solid rgba(201,150,58,0.3);
    margin-bottom: 1.5rem;
  }

  .hero h1 {
    font-family: 'Playfair Display', serif;
    font-size: clamp(2.4rem, 4vw, 3.8rem);
    color: #fff;
    line-height: 1.18;
    margin-bottom: 1.2rem;
  }

  .hero h1 em {
    color: var(--gold);
    font-style: italic;
  }

  .hero-sub {
    color: rgba(255,255,255,0.6);
    font-size: 1.08rem;
    max-width: 480px;
    margin-bottom: 2.5rem;
    font-weight: 300;
    line-height: 1.8;
  }

  .hero-btns {
    display: flex; gap: 1rem; flex-wrap: wrap;
  }

  .btn-primary {
    background: var(--gold);
    color: var(--navy);
    padding: 0.85rem 2rem;
    border-radius: var(--radius);
    font-weight: 600;
    font-size: 0.95rem;
    text-decoration: none;
    display: inline-block;
    transition: background 0.2s, transform 0.15s;
    border: none; cursor: pointer;
  }

  .btn-primary:hover { background: #daa94a; transform: translateY(-1px); }

  .btn-outline {
    background: transparent;
    color: #fff;
    padding: 0.85rem 2rem;
    border-radius: var(--radius);
    font-weight: 500;
    font-size: 0.95rem;
    text-decoration: none;
    display: inline-block;
    border: 1px solid rgba(255,255,255,0.25);
    transition: border-color 0.2s, background 0.2s;
    cursor: pointer;
  }

  .btn-outline:hover { border-color: var(--gold); background: rgba(201,150,58,0.08); }

  .hero-stats {
    display: flex; gap: 2rem; margin-top: 3rem;
    padding-top: 2rem;
    border-top: 1px solid rgba(255,255,255,0.08);
  }

  .stat-item { }
  .stat-num {
    font-family: 'Playfair Display', serif;
    font-size: 1.9rem;
    color: var(--gold);
    display: block;
    font-weight: 700;
  }

  .stat-label {
    font-size: 0.78rem;
    color: rgba(255,255,255,0.45);
    text-transform: uppercase;
    letter-spacing: 0.06em;
    font-weight: 500;
  }

  /* LOAN CALCULATOR CARD */
  .calc-card {
    background: #fff;
    border-radius: 20px;
    padding: 2.2rem 2rem;
    box-shadow: 0 30px 80px rgba(0,0,0,0.35);
    position: relative;
    z-index: 2;
  }

  .calc-card h3 {
    font-family: 'Playfair Display', serif;
    font-size: 1.3rem;
    margin-bottom: 1.5rem;
    color: var(--navy);
  }

  .form-group {
    margin-bottom: 1.2rem;
  }

  .form-group label {
    display: block;
    font-size: 0.78rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.06em;
    color: var(--text-muted);
    margin-bottom: 0.4rem;
  }

  .form-group input,
  .form-group select {
    width: 100%;
    padding: 0.7rem 1rem;
    border: 1.5px solid #E5E9EE;
    border-radius: 8px;
    font-family: 'DM Sans', sans-serif;
    font-size: 0.95rem;
    color: var(--text);
    background: #FAFBFC;
    outline: none;
    transition: border-color 0.2s;
  }

  .form-group input:focus,
  .form-group select:focus {
    border-color: var(--gold);
    background: #fff;
  }

  .amount-display {
    background: var(--gold-light);
    border-radius: 8px;
    padding: 1rem 1.2rem;
    display: flex; justify-content: space-between; align-items: center;
    margin-bottom: 1.2rem;
  }

  .amount-display .label {
    font-size: 0.78rem;
    color: var(--gold-dark);
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.05em;
  }

  .amount-display .value {
    font-family: 'Playfair Display', serif;
    font-size: 1.5rem;
    color: var(--gold-dark);
    font-weight: 700;
  }

  .calc-card .btn-primary {
    width: 100%;
    text-align: center;
    margin-top: 0.5rem;
    padding: 0.95rem;
    font-size: 1rem;
  }

  .trust-row {
    display: flex; align-items: center; gap: 0.5rem;
    margin-top: 1rem;
    justify-content: center;
    font-size: 0.78rem;
    color: var(--text-muted);
  }

  .trust-row .dot {
    width: 6px; height: 6px; border-radius: 50%; background: #22C55E;
  }

  /* RANGE SLIDER */
  input[type=range] {
    width: 100%;
    -webkit-appearance: none;
    height: 5px;
    background: #E5E9EE;
    border-radius: 3px;
    outline: none;
    cursor: pointer;
  }

  input[type=range]::-webkit-slider-thumb {
    -webkit-appearance: none;
    width: 20px; height: 20px;
    border-radius: 50%;
    background: var(--gold);
    border: 3px solid #fff;
    box-shadow: 0 0 0 2px var(--gold);
    cursor: pointer;
  }

  /* SECTION SHARED */
  section { padding: 5rem 5%; }

  .section-inner { max-width: 1200px; margin: 0 auto; }

  .section-tag {
    font-size: 0.75rem;
    font-weight: 600;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--gold);
    margin-bottom: 0.6rem;
  }

  .section-title {
    font-family: 'Playfair Display', serif;
    font-size: clamp(1.8rem, 3vw, 2.6rem);
    color: var(--navy);
    line-height: 1.25;
    margin-bottom: 1rem;
  }

  .section-sub {
    color: var(--text-muted);
    font-size: 1rem;
    max-width: 520px;
    line-height: 1.8;
  }

  /* LOAN TYPES */
  .loans-section { background: var(--cream); }

  .loans-header {
    text-align: center; margin-bottom: 3.5rem;
  }

  .loans-header .section-sub { margin: 0 auto; }

  .loans-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
    gap: 1.5rem;
  }

  .loan-card {
    background: #fff;
    border-radius: 16px;
    padding: 2rem 1.8rem;
    border: 1.5px solid #E5E9EE;
    transition: border-color 0.2s, box-shadow 0.2s, transform 0.2s;
    cursor: pointer;
    text-decoration: none;
    color: inherit;
    display: block;
  }

  .loan-card:hover {
    border-color: var(--gold);
    box-shadow: 0 8px 30px rgba(201,150,58,0.15);
    transform: translateY(-3px);
  }

  .loan-icon {
    width: 52px; height: 52px;
    border-radius: 12px;
    background: var(--gold-light);
    display: flex; align-items: center; justify-content: center;
    font-size: 1.4rem;
    margin-bottom: 1.2rem;
  }

  .loan-card h4 {
    font-family: 'Playfair Display', serif;
    font-size: 1.15rem;
    color: var(--navy);
    margin-bottom: 0.5rem;
  }

  .loan-card p {
    font-size: 0.88rem;
    color: var(--text-muted);
    line-height: 1.7;
    margin-bottom: 1.2rem;
  }

  .loan-rate {
    display: flex; align-items: baseline; gap: 0.3rem;
  }

  .rate-num {
    font-family: 'Playfair Display', serif;
    font-size: 1.4rem;
    font-weight: 700;
    color: var(--gold);
  }

  .rate-label {
    font-size: 0.78rem;
    color: var(--text-muted);
    font-weight: 500;
  }

  /* HOW IT WORKS */
  .how-section {
    background: var(--navy);
    position: relative;
    overflow: hidden;
  }

  .how-section::before {
    content: '';
    position: absolute;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    width: 800px; height: 800px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(201,150,58,0.05) 0%, transparent 65%);
    pointer-events: none;
  }

  .how-inner {
    max-width: 1200px; margin: 0 auto;
    display: grid; grid-template-columns: 1fr 1.6fr; gap: 5rem; align-items: center;
  }

  .how-left .section-title { color: #fff; }
  .how-left .section-sub { color: rgba(255,255,255,0.5); }

  .how-steps { display: flex; flex-direction: column; gap: 0; }

  .step {
    display: flex; gap: 1.5rem;
    padding: 1.5rem 0;
    border-bottom: 1px solid rgba(255,255,255,0.06);
    align-items: flex-start;
  }

  .step:last-child { border-bottom: none; }

  .step-num {
    width: 42px; height: 42px;
    border-radius: 50%;
    background: rgba(201,150,58,0.15);
    border: 1.5px solid rgba(201,150,58,0.4);
    display: flex; align-items: center; justify-content: center;
    font-family: 'Playfair Display', serif;
    font-size: 1rem;
    font-weight: 700;
    color: var(--gold);
    flex-shrink: 0;
  }

  .step-content h4 {
    font-weight: 600;
    color: #fff;
    margin-bottom: 0.3rem;
    font-size: 1rem;
  }

  .step-content p {
    font-size: 0.88rem;
    color: rgba(255,255,255,0.45);
    line-height: 1.7;
  }

  /* TRUST BAR */
  .trust-section {
    background: var(--gold);
    padding: 2.5rem 5%;
  }

  .trust-inner {
    max-width: 1200px; margin: 0 auto;
    display: flex; justify-content: space-around; align-items: center;
    flex-wrap: wrap; gap: 1.5rem;
  }

  .trust-item {
    display: flex; align-items: center; gap: 0.8rem;
  }

  .trust-icon { font-size: 1.4rem; }

  .trust-text strong {
    display: block;
    font-weight: 600;
    font-size: 0.9rem;
    color: var(--navy);
  }

  .trust-text span {
    font-size: 0.8rem;
    color: rgba(13,27,42,0.6);
  }

  /* TESTIMONIALS */
  .testimonials-section { background: #fff; }

  .testimonials-header { text-align: center; margin-bottom: 3.5rem; }
  .testimonials-header .section-sub { margin: 0 auto; }

  .testimonials-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 1.5rem;
  }

  .testimonial {
    background: var(--cream);
    border-radius: 16px;
    padding: 1.8rem;
    border: 1.5px solid #EEE;
    position: relative;
  }

  .stars {
    color: var(--gold);
    font-size: 0.9rem;
    letter-spacing: 2px;
    margin-bottom: 1rem;
  }

  .testimonial blockquote {
    font-size: 0.95rem;
    color: var(--text);
    line-height: 1.8;
    margin-bottom: 1.4rem;
    font-weight: 300;
  }

  .testimonial-author {
    display: flex; align-items: center; gap: 0.75rem;
  }

  .avatar {
    width: 40px; height: 40px;
    border-radius: 50%;
    background: var(--gold-light);
    display: flex; align-items: center; justify-content: center;
    font-weight: 700;
    font-size: 0.8rem;
    color: var(--gold-dark);
  }

  .author-info strong {
    display: block;
    font-size: 0.88rem;
    font-weight: 600;
    color: var(--navy);
  }

  .author-info span {
    font-size: 0.78rem;
    color: var(--text-muted);
  }

  /* CTA */
  .cta-section {
    background: var(--navy);
    text-align: center;
    position: relative;
    overflow: hidden;
  }

  .cta-section::before {
    content: '';
    position: absolute;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    width: 600px; height: 300px;
    background: radial-gradient(ellipse, rgba(201,150,58,0.15) 0%, transparent 70%);
    pointer-events: none;
  }

  .cta-inner {
    max-width: 640px; margin: 0 auto; position: relative; z-index: 1;
  }

  .cta-section .section-title { color: #fff; }
  .cta-section .section-sub {
    color: rgba(255,255,255,0.55);
    margin: 0 auto 2.5rem;
  }

  .cta-btns { display: flex; gap: 1rem; justify-content: center; flex-wrap: wrap; }

  /* FOOTER */
  footer {
    background: #080F17;
    padding: 3rem 5% 2rem;
    color: rgba(255,255,255,0.4);
    font-size: 0.82rem;
  }

  .footer-inner {
    max-width: 1200px; margin: 0 auto;
    display: grid; grid-template-columns: 2fr 1fr 1fr 1fr; gap: 2.5rem;
    margin-bottom: 2.5rem;
  }

  footer .logo { font-size: 1.4rem; display: block; margin-bottom: 0.8rem; }

  .footer-about {
    font-size: 0.84rem;
    line-height: 1.8;
    color: rgba(255,255,255,0.35);
    max-width: 280px;
  }

  .footer-col h5 {
    font-size: 0.78rem;
    font-weight: 600;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: rgba(255,255,255,0.6);
    margin-bottom: 1rem;
  }

  .footer-col ul { list-style: none; display: flex; flex-direction: column; gap: 0.6rem; }

  .footer-col ul a {
    color: rgba(255,255,255,0.4);
    text-decoration: none;
    font-size: 0.85rem;
    transition: color 0.2s;
  }

  .footer-col ul a:hover { color: var(--gold); }

  .footer-bottom {
    max-width: 1200px; margin: 0 auto;
    border-top: 1px solid rgba(255,255,255,0.06);
    padding-top: 1.5rem;
    display: flex; justify-content: space-between; align-items: center;
    flex-wrap: wrap; gap: 0.8rem;
  }

  .footer-legal { font-size: 0.78rem; color: rgba(255,255,255,0.25); }

  /* RESPONSIVE */
  @media (max-width: 900px) {
    .hero-inner { grid-template-columns: 1fr; }
    .calc-card { max-width: 480px; }
    .how-inner { grid-template-columns: 1fr; }
    .footer-inner { grid-template-columns: 1fr 1fr; }
  }

  @media (max-width: 600px) {
    nav ul { display: none; }
    .hero-stats { flex-wrap: wrap; gap: 1.5rem; }
    .footer-inner { grid-template-columns: 1fr; }
  }

  /* ANIMATION */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .hero-left > * {
    animation: fadeUp 0.7s ease both;
  }

  .hero-tag { animation-delay: 0.1s; }
  .hero h1 { animation-delay: 0.2s; }
  .hero-sub { animation-delay: 0.3s; }
  .hero-btns { animation-delay: 0.4s; }
  .hero-stats { animation-delay: 0.5s; }

  .calc-card {
    animation: fadeUp 0.8s 0.4s ease both;
  }
</style>
</head>
<body>

<!-- NAV -->
<nav>
  <a class="logo" href="#"><span>Swift</span>Lend</a>
  <ul>
    <li><a href="#loans">Loan Types</a></li>
    <li><a href="#how">How It Works</a></li>
    <li><a href="#testimonials">Reviews</a></li>
    <li><a href="#apply" class="nav-cta">Apply Now</a></li>
  </ul>
</nav>

<!-- HERO -->
<section class="hero">
  <div class="hero-inner">
    <div class="hero-left">
      <div class="hero-tag">&#10003; Trusted by 50,000+ Kenyans</div>
      <h1>Smart Loans for<br><em>Every Journey</em><br>in Life</h1>
      <p class="hero-sub">
        Fast approvals, transparent rates, and flexible repayment plans.
        Get the funds you need — from personal emergencies to business growth.
      </p>
      <div class="hero-btns">
        <a href="#apply" class="btn-primary">Check My Rate</a>
        <a href="#how" class="btn-outline">How It Works</a>
      </div>
      <div class="hero-stats">
        <div class="stat-item">
          <span class="stat-num">24hr</span>
          <span class="stat-label">Approval Time</span>
        </div>
        <div class="stat-item">
          <span class="stat-num">9.5%</span>
          <span class="stat-label">Starting Rate</span>
        </div>
        <div class="stat-item">
          <span class="stat-num">KSh 5M</span>
          <span class="stat-label">Max Loan Amount</span>
        </div>
      </div>
    </div>

    <!-- CALCULATOR -->
    <div>
      <div class="calc-card">
        <h3>Estimate Your Repayment</h3>

        <div class="form-group">
          <label>Loan Amount (KSh)</label>
          <input type="range" id="loanAmount" min="10000" max="5000000" step="10000" value="200000">
          <div style="display:flex;justify-content:space-between;margin-top:6px;">
            <span style="font-size:0.75rem;color:#999;">KSh 10,000</span>
            <span style="font-size:0.85rem;font-weight:600;color:var(--navy)" id="amountLabel">KSh 200,000</span>
            <span style="font-size:0.75rem;color:#999;">KSh 5M</span>
          </div>
        </div>

        <div class="form-group">
          <label>Loan Term</label>
          <select id="loanTerm">
            <option value="6">6 Months</option>
            <option value="12" selected>12 Months</option>
            <option value="24">24 Months</option>
            <option value="36">36 Months</option>
            <option value="60">60 Months</option>
          </select>
        </div>

        <div class="form-group">
          <label>Loan Type</label>
          <select id="loanType">
            <option value="9.5">Personal Loan (9.5% p.a.)</option>
            <option value="12">Business Loan (12% p.a.)</option>
            <option value="8">Home Equity (8% p.a.)</option>
            <option value="14">Emergency Loan (14% p.a.)</option>
          </select>
        </div>

        <div class="amount-display">
          <span class="label">Monthly Payment</span>
          <span class="value" id="monthlyPayment">KSh 17,579</span>
        </div>

        <div style="display:grid;grid-template-columns:1fr 1fr;gap:0.8rem;margin-bottom:1rem;">
          <div style="background:#F5F7FA;border-radius:8px;padding:0.8rem 1rem;">
            <div style="font-size:0.72rem;color:#999;text-transform:uppercase;letter-spacing:0.05em;font-weight:600;margin-bottom:3px;">Total Repayable</div>
            <div style="font-size:1.05rem;font-weight:600;color:var(--navy)" id="totalRepay">KSh 210,948</div>
          </div>
          <div style="background:#F5F7FA;border-radius:8px;padding:0.8rem 1rem;">
            <div style="font-size:0.72rem;color:#999;text-transform:uppercase;letter-spacing:0.05em;font-weight:600;margin-bottom:3px;">Total Interest</div>
            <div style="font-size:1.05rem;font-weight:600;color:var(--gold)" id="totalInterest">KSh 10,948</div>
          </div>
        </div>

        <a href="#apply" class="btn-primary" id="applyBtn">Apply for KSh 200,000</a>

        <div class="trust-row">
          <div class="dot"></div>
          No impact on your credit score to check rates
        </div>
      </div>
    </div>
  </div>
</section>

<!-- TRUST BAR -->
<div class="trust-section">
  <div class="trust-inner">
    <div class="trust-item">
      <span class="trust-icon">🏦</span>
      <div class="trust-text">
        <strong>CBK Regulated</strong>
        <span>Licensed & Compliant</span>
      </div>
    </div>
    <div class="trust-item">
      <span class="trust-icon">🔒</span>
      <div class="trust-text">
        <strong>256-bit SSL</strong>
        <span>Bank-Grade Security</span>
      </div>
    </div>
    <div class="trust-item">
      <span class="trust-icon">⚡</span>
      <div class="trust-text">
        <strong>24hr Disbursement</strong>
        <span>Fast, reliable transfers</span>
      </div>
    </div>
    <div class="trust-item">
      <span class="trust-icon">📞</span>
      <div class="trust-text">
        <strong>24/7 Support</strong>
        <span>Always here for you</span>
      </div>
    </div>
    <div class="trust-item">
      <span class="trust-icon">⭐</span>
      <div class="trust-text">
        <strong>4.8 / 5 Rating</strong>
        <span>From 12,000+ reviews</span>
      </div>
    </div>
  </div>
</div>

<!-- LOAN TYPES -->
<section class="loans-section" id="loans">
  <div class="section-inner">
    <div class="loans-header">
      <div class="section-tag">Our Products</div>
      <h2 class="section-title">A Loan for Every Need</h2>
      <p class="section-sub">Flexible solutions tailored to your goals, backed by fair and transparent terms.</p>
    </div>
    <div class="loans-grid">
      <a class="loan-card" href="#apply">
        <div class="loan-icon">🏠</div>
        <h4>Home Loan</h4>
        <p>Buy, build, or renovate your dream home with competitive rates and terms up to 20 years.</p>
        <div class="loan-rate">
          <span class="rate-num">8%</span>
          <span class="rate-label">p.a. from</span>
        </div>
      </a>
      <a class="loan-card" href="#apply">
        <div class="loan-icon">👤</div>
        <h4>Personal Loan</h4>
        <p>Handle emergencies, school fees, medical bills, or personal goals quickly and easily.</p>
        <div class="loan-rate">
          <span class="rate-num">9.5%</span>
          <span class="rate-label">p.a. from</span>
        </div>
      </a>
      <a class="loan-card" href="#apply">
        <div class="loan-icon">💼</div>
        <h4>Business Loan</h4>
        <p>Grow your business with working capital, equipment financing, or expansion funds.</p>
        <div class="loan-rate">
          <span class="rate-num">12%</span>
          <span class="rate-label">p.a. from</span>
        </div>
      </a>
      <a class="loan-card" href="#apply">
        <div class="loan-icon">🎓</div>
        <h4>Education Loan</h4>
        <p>Invest in your future or your child's education with deferred repayment options.</p>
        <div class="loan-rate">
          <span class="rate-num">10%</span>
          <span class="rate-label">p.a. from</span>
        </div>
      </a>
      <a class="loan-card" href="#apply">
        <div class="loan-icon">🚗</div>
        <h4>Car Loan</h4>
        <p>Finance your next vehicle — new or used — with flexible terms and low monthly payments.</p>
        <div class="loan-rate">
          <span class="rate-num">11%</span>
          <span class="rate-label">p.a. from</span>
        </div>
      </a>
      <a class="loan-card" href="#apply">
        <div class="loan-icon">⚡</div>
        <h4>Emergency Loan</h4>
        <p>Urgent financial need? Get up to KSh 200,000 disbursed within hours, no collateral needed.</p>
        <div class="loan-rate">
          <span class="rate-num">14%</span>
          <span class="rate-label">p.a. from</span>
        </div>
      </a>
    </div>
  </div>
</section>

<!-- HOW IT WORKS -->
<section class="how-section" id="how">
  <div class="section-inner">
    <div class="how-inner">
      <div class="how-left">
        <div class="section-tag" style="color:var(--gold);">Simple Process</div>
        <h2 class="section-title">Get Funded in<br>4 Easy Steps</h2>
        <p class="section-sub">We've removed the paperwork and long waits. Our digital process gets you money fast.</p>
        <a href="#apply" class="btn-primary" style="margin-top:2rem;display:inline-block;">Start Your Application</a>
      </div>
      <div class="how-steps">
        <div class="step">
          <div class="step-num">1</div>
          <div class="step-content">
            <h4>Apply Online in Minutes</h4>
            <p>Fill out our simple form — no branch visits, no paperwork. Just your ID and basic financial details.</p>
          </div>
        </div>
        <div class="step">
          <div class="step-num">2</div>
          <div class="step-content">
            <h4>Get an Instant Decision</h4>
            <p>Our smart system reviews your application in real time. Most applicants receive a decision within hours.</p>
          </div>
        </div>
        <div class="step">
          <div class="step-num">3</div>
          <div class="step-content">
            <h4>Review & Accept Your Offer</h4>
            <p>We'll send you a transparent loan offer — clear rate, exact repayment schedule, no hidden fees.</p>
          </div>
        </div>
        <div class="step">
          <div class="step-num">4</div>
          <div class="step-content">
            <h4>Funds in Your Account</h4>
            <p>Once accepted, funds are disbursed to your M-Pesa or bank account within 24 hours.</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- TESTIMONIALS -->
<section class="testimonials-section" id="testimonials">
  <div class="section-inner">
    <div class="testimonials-header">
      <div class="section-tag">Customer Stories</div>
      <h2 class="section-title">Real People, Real Results</h2>
      <p class="section-sub">Thousands of Kenyans trust SwiftLend to support their financial goals.</p>
    </div>
    <div class="testimonials-grid">
      <div class="testimonial">
        <div class="stars">★★★★★</div>
        <blockquote>"I applied for a business loan on Monday morning and had the funds by Tuesday. The process was completely online and the rates were far better than my bank."</blockquote>
        <div class="testimonial-author">
          <div class="avatar">JM</div>
          <div class="author-info">
            <strong>James Mwangi</strong>
            <span>Business Owner, Nairobi</span>
          </div>
        </div>
      </div>
      <div class="testimonial">
        <div class="stars">★★★★★</div>
        <blockquote>"Used the education loan for my son's university fees. The deferred repayment was a lifesaver — I didn't have to stress while he settled into school."</blockquote>
        <div class="testimonial-author">
          <div class="avatar">GW</div>
          <div class="author-info">
            <strong>Grace Wanjiku</strong>
            <span>Teacher, Nakuru</span>
          </div>
        </div>
      </div>
      <div class="testimonial">
        <div class="stars">★★★★★</div>
        <blockquote>"The calculator on the website was so helpful — I knew exactly what I'd pay before I even applied. Transparent, fast, and the customer support team is excellent."</blockquote>
        <div class="testimonial-author">
          <div class="avatar">BO</div>
          <div class="author-info">
            <strong>Brian Ochieng</strong>
            <span>Freelance Developer, Kisumu</span>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- APPLY CTA -->
<section class="cta-section" id="apply">
  <div class="section-inner">
    <div class="cta-inner">
      <div class="section-tag" style="color:var(--gold);">Ready to Start?</div>
      <h2 class="section-title">Apply Today — It Takes 5 Minutes</h2>
      <p class="section-sub">No hidden fees. No surprises. Just straightforward lending designed for you.</p>
      <div class="cta-btns">
        <button class="btn-primary" onclick="alert('Application form coming soon!')">Apply Now — Free</button>
        <button class="btn-outline" onclick="alert('Our team is available at 0800 123 456')">Talk to an Advisor</button>
      </div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-inner">
    <div>
      <a class="logo" href="#">Swift<span style="color:rgba(255,255,255,0.5)">Lend</span></a>
      <p class="footer-about">
        SwiftLend is a licensed financial services provider regulated by the Central Bank of Kenya. We're committed to fair, transparent, and accessible lending for every Kenyan.
      </p>
    </div>
    <div class="footer-col">
      <h5>Products</h5>
      <ul>
        <li><a href="#">Personal Loans</a></li>
        <li><a href="#">Business Loans</a></li>
        <li><a href="#">Home Loans</a></li>
        <li><a href="#">Car Loans</a></li>
        <li><a href="#">Education Loans</a></li>
      </ul>
    </div>
    <div class="footer-col">
      <h5>Company</h5>
      <ul>
        <li><a href="#">About Us</a></li>
        <li><a href="#">Careers</a></li>
        <li><a href="#">Press</a></li>
        <li><a href="#">Blog</a></li>
      </ul>
    </div>
    <div class="footer-col">
      <h5>Support</h5>
      <ul>
        <li><a href="#">Help Centre</a></li>
        <li><a href="#">Contact Us</a></li>
        <li><a href="#">Privacy Policy</a></li>
        <li><a href="#">Terms of Service</a></li>
      </ul>
    </div>
  </div>
  <div class="footer-bottom">
    <span class="footer-legal">© 2025 SwiftLend Ltd. All rights reserved. Regulated by the Central Bank of Kenya.</span>
    <span class="footer-legal">CBK License No. NBFI/2019/0042</span>
  </div>
</footer>

<script>
  const amountSlider = document.getElementById('loanAmount');
  const amountLabel = document.getElementById('amountLabel');
  const termSelect = document.getElementById('loanTerm');
  const typeSelect = document.getElementById('loanType');
  const monthlyEl = document.getElementById('monthlyPayment');
  const totalEl = document.getElementById('totalRepay');
  const interestEl = document.getElementById('totalInterest');
  const applyBtn = document.getElementById('applyBtn');

  function fmt(n) {
    return 'KSh ' + Math.round(n).toLocaleString('en-KE');
  }

  function calcLoan() {
    const P = parseFloat(amountSlider.value);
    const months = parseInt(termSelect.value);
    const annualRate = parseFloat(typeSelect.value) / 100;
    const r = annualRate / 12;

    let monthly;
    if (r === 0) {
      monthly = P / months;
    } else {
      monthly = P * r * Math.pow(1 + r, months) / (Math.pow(1 + r, months) - 1);
    }

    const total = monthly * months;
    const interest = total - P;

    amountLabel.textContent = fmt(P);
    monthlyEl.textContent = fmt(monthly);
    totalEl.textContent = fmt(total);
    interestEl.textContent = fmt(interest);

    const amtStr = P >= 1000000
      ? 'KSh ' + (P/1000000).toFixed(1) + 'M'
      : 'KSh ' + Math.round(P/1000) + 'K';
    applyBtn.textContent = 'Apply for ' + amtStr;
  }

  amountSlider.addEventListener('input', calcLoan);
  termSelect.addEventListener('change', calcLoan);
  typeSelect.addEventListener('change', calcLoan);
  calcLoan();
</script>

</body>
</html>
