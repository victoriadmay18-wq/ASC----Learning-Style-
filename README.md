<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Academic Success Center – Learning Style Survey</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700;900&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --ink: #1a1a2e; --cream: #f5f0e8; --gold: #c9a84c; --gold-light: #e8d5a3;
    --rust: #c0392b; --sage: #4a7c59; --sky: #2e6da4;
    --card: #ffffff; --border: #e0d8cc; --muted: #7a7060;
  }
  * { box-sizing: border-box; margin: 0; padding: 0; }
  body { font-family: 'DM Sans', sans-serif; background: var(--cream); color: var(--ink); min-height: 100vh; }

  header { background: var(--ink); color: var(--cream); padding: 32px 24px 28px; text-align: center; position: relative; overflow: hidden; }
  header::before { content: ''; position: absolute; inset: 0; background: repeating-linear-gradient(45deg,transparent,transparent 40px,rgba(201,168,76,0.06) 40px,rgba(201,168,76,0.06) 41px); }
  .header-eyebrow { font-size: 11px; letter-spacing: 4px; text-transform: uppercase; color: var(--gold); margin-bottom: 10px; font-weight: 500; position: relative; }
  header h1 { font-family: 'Playfair Display', serif; font-size: clamp(24px,5vw,42px); font-weight: 900; line-height: 1.1; position: relative; }
  header h1 span { color: var(--gold); }
  .header-desc { margin-top: 12px; font-size: 14px; color: rgba(245,240,232,0.65); max-width: 500px; margin: 12px auto 0; font-weight: 300; position: relative; }
  .admin-link { position: absolute; top: 16px; right: 20px; font-size: 11px; letter-spacing: 2px; text-transform: uppercase; color: rgba(201,168,76,0.6); cursor: pointer; background: none; border: 1px solid rgba(201,168,76,0.3); padding: 6px 14px; border-radius: 4px; transition: all 0.2s; z-index: 10; }
  .admin-link:hover { color: var(--gold); border-color: var(--gold); }

  .progress-bar-wrap { background: var(--border); height: 4px; position: sticky; top: 0; z-index: 100; }
  .progress-bar-fill { height: 100%; background: var(--gold); transition: width 0.4s ease; width: 0%; }

  main { max-width: 720px; margin: 0 auto; padding: 40px 20px 80px; }
  .step-label { font-size: 11px; letter-spacing: 3px; text-transform: uppercase; color: var(--muted); margin-bottom: 6px; font-weight: 500; }

  .section-header { display: flex; align-items: center; gap: 14px; margin: 40px 0 20px; }
  .section-icon { width: 40px; height: 40px; border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 18px; flex-shrink: 0; }
  .section-icon.visual { background: #dbeafe; } .section-icon.auditory { background: #fce7f3; } .section-icon.kinesthetic { background: #d1fae5; }
  .section-title { font-family: 'Playfair Display', serif; font-size: 20px; font-weight: 700; }
  .section-subtitle { font-size: 13px; color: var(--muted); margin-top: 2px; }

  .card { background: var(--card); border: 1px solid var(--border); border-radius: 12px; padding: 24px 28px; margin-bottom: 12px; transition: border-color 0.2s, box-shadow 0.2s; }
  .card:hover { border-color: var(--gold-light); box-shadow: 0 4px 20px rgba(0,0,0,0.06); }

  .field-group { display: grid; gap: 16px; }
  .field-label { font-size: 12px; letter-spacing: 1.5px; text-transform: uppercase; color: var(--muted); margin-bottom: 6px; font-weight: 500; }
  .field-required { color: var(--rust); margin-left: 2px; }
  input[type="text"], input[type="email"], input[type="password"] { width: 100%; padding: 12px 16px; border: 1.5px solid var(--border); border-radius: 8px; font-family: 'DM Sans', sans-serif; font-size: 15px; color: var(--ink); background: var(--cream); transition: border-color 0.2s; outline: none; }
  input:focus { border-color: var(--gold); background: #fff; }
  input.error { border-color: var(--rust); }
  .field-error { font-size: 12px; color: var(--rust); margin-top: 4px; display: none; }
  .field-error.show { display: block; }

  .question-text { font-size: 15px; font-weight: 400; line-height: 1.5; margin-bottom: 12px; color: var(--ink); }
  .question-num { font-family: 'Playfair Display', serif; font-size: 13px; color: var(--gold); font-weight: 700; margin-right: 6px; }
  .choices { display: flex; gap: 10px; flex-wrap: wrap; }
  .choice-btn { flex: 1; min-width: 90px; padding: 10px 6px; border: 1.5px solid var(--border); border-radius: 8px; background: var(--cream); font-family: 'DM Sans', sans-serif; font-size: 13px; font-weight: 500; color: var(--muted); cursor: pointer; transition: all 0.18s; text-align: center; }
  .choice-btn:hover { border-color: var(--gold); color: var(--ink); }
  .choice-btn.selected { border-color: var(--ink); background: var(--ink); color: var(--cream); }
  .choice-btn.selected.never { background: #4a7c59; border-color: #4a7c59; }
  .choice-btn.selected.sometimes { background: #c9a84c; border-color: #c9a84c; color: var(--ink); }
  .choice-btn.selected.often { background: var(--ink); border-color: var(--ink); }
  .question-item.unanswered .choices .choice-btn { border-color: #e8b4b0; }

  .submit-area { margin-top: 48px; text-align: center; }
  .btn-submit { display: inline-flex; align-items: center; gap: 10px; padding: 16px 48px; background: var(--ink); color: var(--cream); font-family: 'DM Sans', sans-serif; font-size: 15px; font-weight: 500; letter-spacing: 1px; text-transform: uppercase; border: none; border-radius: 4px; cursor: pointer; transition: background 0.2s, transform 0.15s; }
  .btn-submit:hover { background: #2e2e4a; transform: translateY(-1px); }
  .submit-note { margin-top: 14px; font-size: 13px; color: var(--muted); }

  #results-view { display: none; }
  .results-hero { background: var(--ink); color: var(--cream); border-radius: 16px; padding: 48px 40px; text-align: center; position: relative; overflow: hidden; margin-bottom: 32px; }
  .results-hero::before { content: ''; position: absolute; inset: 0; background: radial-gradient(ellipse at 70% 20%,rgba(201,168,76,0.15) 0%,transparent 60%); }
  .results-eyebrow { font-size: 11px; letter-spacing: 4px; text-transform: uppercase; color: var(--gold); margin-bottom: 16px; font-weight: 500; position: relative; }
  .results-name { font-size: 15px; color: rgba(245,240,232,0.6); margin-bottom: 8px; font-weight: 300; position: relative; }
  .results-type { font-family: 'Playfair Display', serif; font-size: clamp(32px,8vw,56px); font-weight: 900; line-height: 1.1; position: relative; }
  .results-type .accent { color: var(--gold); }
  .results-emoji { font-size: 48px; margin-bottom: 16px; display: block; position: relative; }

  .score-grid { display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 16px; margin-bottom: 32px; }
  .score-card { background: var(--card); border: 1px solid var(--border); border-radius: 12px; padding: 20px 16px; text-align: center; }
  .score-card.winner { border-color: var(--gold); box-shadow: 0 4px 20px rgba(201,168,76,0.2); }
  .score-card-label { font-size: 11px; letter-spacing: 2px; text-transform: uppercase; color: var(--muted); margin-bottom: 8px; font-weight: 500; }
  .score-card-num { font-family: 'Playfair Display', serif; font-size: 36px; font-weight: 700; color: var(--ink); }
  .score-card.winner .score-card-num { color: var(--gold); }
  .score-card-max { font-size: 12px; color: var(--muted); margin-top: 2px; }
  .score-bar-track { height: 6px; background: var(--border); border-radius: 3px; margin-top: 10px; overflow: hidden; }
  .score-bar-fill { height: 100%; border-radius: 3px; transition: width 1s ease 0.3s; width: 0; }
  .visual-fill { background: var(--sky); } .auditory-fill { background: #c0392b; } .kinesthetic-fill { background: var(--sage); }

  .strategies-card { background: var(--card); border: 1px solid var(--border); border-radius: 12px; padding: 32px; margin-bottom: 32px; }
  .strategies-title { font-family: 'Playfair Display', serif; font-size: 22px; font-weight: 700; margin-bottom: 20px; display: flex; align-items: center; gap: 10px; }
  .strategy-item { display: flex; align-items: flex-start; gap: 12px; padding: 14px 0; border-bottom: 1px solid var(--border); }
  .strategy-item:last-child { border-bottom: none; }
  .strategy-dot { width: 8px; height: 8px; border-radius: 50%; background: var(--gold); margin-top: 6px; flex-shrink: 0; }
  .strategy-text { font-size: 15px; line-height: 1.5; }

  .cta-card { background: var(--ink); color: var(--cream); border-radius: 12px; padding: 32px; text-align: center; }
  .cta-card p { font-size: 15px; line-height: 1.6; color: rgba(245,240,232,0.75); margin-bottom: 20px; font-weight: 300; }
  .btn-cta { display: inline-block; padding: 14px 36px; background: var(--gold); color: var(--ink); font-family: 'DM Sans', sans-serif; font-size: 14px; font-weight: 500; letter-spacing: 1px; text-transform: uppercase; border: none; border-radius: 4px; cursor: pointer; }
  .btn-cta:hover { opacity: 0.88; }
  .btn-restart { margin-top: 14px; background: none; border: 1px solid rgba(245,240,232,0.3); color: rgba(245,240,232,0.6); font-family: 'DM Sans', sans-serif; font-size: 13px; padding: 10px 24px; border-radius: 4px; cursor: pointer; transition: all 0.2s; display: block; margin-left: auto; margin-right: auto; }
  .btn-restart:hover { color: var(--cream); border-color: rgba(245,240,232,0.5); }

  .validation-banner { display: none; background: #fef2f2; border: 1px solid #fca5a5; color: var(--rust); padding: 14px 20px; border-radius: 8px; font-size: 14px; margin-bottom: 24px; }
  .validation-banner.show { display: block; }

  .modal-overlay { display: none; position: fixed; inset: 0; background: rgba(10,10,20,0.75); z-index: 999; align-items: center; justify-content: center; backdrop-filter: blur(4px); }
  .modal-overlay.open { display: flex; }
  .modal { background: var(--cream); border-radius: 16px; padding: 40px 36px; width: 100%; max-width: 400px; position: relative; box-shadow: 0 24px 80px rgba(0,0,0,0.3); }
  .modal-close { position: absolute; top: 16px; right: 16px; background: none; border: none; font-size: 20px; cursor: pointer; color: var(--muted); }
  .modal h2 { font-family: 'Playfair Display', serif; font-size: 24px; margin-bottom: 6px; }
  .modal p { font-size: 13px; color: var(--muted); margin-bottom: 24px; }
  .btn-login { width: 100%; margin-top: 20px; padding: 14px; background: var(--ink); color: var(--cream); font-family: 'DM Sans', sans-serif; font-size: 14px; font-weight: 500; letter-spacing: 1px; text-transform: uppercase; border: none; border-radius: 6px; cursor: pointer; transition: background 0.2s; }
  .btn-login:hover { background: #2e2e4a; }
  .login-error { font-size: 13px; color: var(--rust); margin-top: 10px; display: none; text-align: center; }
  .login-error.show { display: block; }

  #admin-view { display: none; }
  .admin-header { background: var(--ink); color: var(--cream); padding: 24px 32px; display: flex; align-items: center; justify-content: space-between; flex-wrap: wrap; gap: 14px; }
  .admin-header h2 { font-family: 'Playfair Display', serif; font-size: 26px; font-weight: 700; }
  .admin-header .sub { font-size: 13px; color: rgba(245,240,232,0.5); margin-top: 2px; }
  .admin-actions { display: flex; gap: 10px; }
  .btn-export { padding: 10px 20px; background: var(--gold); color: var(--ink); font-family: 'DM Sans', sans-serif; font-size: 13px; font-weight: 500; border: none; border-radius: 4px; cursor: pointer; transition: opacity 0.2s; }
  .btn-export:hover { opacity: 0.85; }
  .btn-logout { padding: 10px 20px; background: transparent; color: rgba(245,240,232,0.6); font-family: 'DM Sans', sans-serif; font-size: 13px; border: 1px solid rgba(245,240,232,0.25); border-radius: 4px; cursor: pointer; transition: all 0.2s; }
  .btn-logout:hover { color: var(--cream); border-color: rgba(245,240,232,0.5); }

  .admin-body { max-width: 1100px; margin: 0 auto; padding: 32px 24px 80px; }

  .stat-row { display: grid; grid-template-columns: repeat(auto-fit, minmax(160px,1fr)); gap: 16px; margin-bottom: 32px; }
  .stat-card { background: var(--card); border: 1px solid var(--border); border-radius: 12px; padding: 20px 22px; }
  .stat-card.highlight { border-color: var(--gold); }
  .stat-card-label { font-size: 11px; letter-spacing: 2px; text-transform: uppercase; color: var(--muted); margin-bottom: 8px; }
  .stat-card-value { font-family: 'Playfair Display', serif; font-size: 38px; font-weight: 700; color: var(--ink); }
  .stat-card.highlight .stat-card-value { color: var(--gold); font-size: 22px; margin-top: 6px; }
  .stat-card-sub { font-size: 12px; color: var(--muted); margin-top: 4px; }

  .chart-row { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 32px; }
  .chart-card { background: var(--card); border: 1px solid var(--border); border-radius: 12px; padding: 24px; }
  .chart-title { font-family: 'Playfair Display', serif; font-size: 17px; font-weight: 700; margin-bottom: 20px; }
  .donut-wrap { display: flex; align-items: center; gap: 24px; }
  .donut-legend { flex: 1; }
  .legend-item { display: flex; align-items: center; gap: 10px; margin-bottom: 12px; }
  .legend-dot { width: 12px; height: 12px; border-radius: 50%; flex-shrink: 0; }
  .legend-label { font-size: 13px; color: var(--ink); }
  .legend-pct { font-size: 13px; font-weight: 500; color: var(--muted); margin-left: auto; }
  .bar-chart { display: flex; flex-direction: column; gap: 18px; }
  .bar-row-label { font-size: 12px; color: var(--muted); margin-bottom: 5px; display: flex; justify-content: space-between; }
  .bar-row-track { height: 10px; background: var(--border); border-radius: 5px; overflow: hidden; }
  .bar-row-fill { height: 100%; border-radius: 5px; transition: width 0.8s ease; }

  .table-card { background: var(--card); border: 1px solid var(--border); border-radius: 12px; overflow: hidden; }
  .table-toolbar { padding: 18px 24px; border-bottom: 1px solid var(--border); display: flex; align-items: center; justify-content: space-between; gap: 12px; flex-wrap: wrap; }
  .table-title { font-family: 'Playfair Display', serif; font-size: 18px; font-weight: 700; }
  .table-search { padding: 8px 14px; border: 1.5px solid var(--border); border-radius: 6px; font-family: 'DM Sans', sans-serif; font-size: 13px; outline: none; min-width: 200px; background: var(--cream); color: var(--ink); }
  .table-search:focus { border-color: var(--gold); }
  .table-wrap { overflow-x: auto; }
  table { width: 100%; border-collapse: collapse; font-size: 13px; }
  thead { background: #f9f6f0; }
  th { padding: 12px 18px; text-align: left; font-size: 11px; letter-spacing: 1.5px; text-transform: uppercase; color: var(--muted); font-weight: 500; white-space: nowrap; }
  td { padding: 14px 18px; border-top: 1px solid var(--border); vertical-align: middle; }
  tr:hover td { background: #faf8f4; }
  .badge { display: inline-block; padding: 3px 10px; border-radius: 20px; font-size: 11px; font-weight: 500; letter-spacing: 0.5px; }
  .badge.visual { background: #dbeafe; color: #1e40af; }
  .badge.auditory { background: #fce7f3; color: #9d174d; }
  .badge.kinesthetic { background: #d1fae5; color: #065f46; }
  .no-data { text-align: center; padding: 48px 24px; color: var(--muted); font-size: 15px; }
  .btn-delete-row { background: none; border: none; cursor: pointer; color: #e8a0a0; font-size: 14px; padding: 4px; border-radius: 4px; transition: color 0.2s; }
  .btn-delete-row:hover { color: var(--rust); }

  .pagination { display: flex; align-items: center; justify-content: space-between; padding: 14px 24px; border-top: 1px solid var(--border); font-size: 13px; color: var(--muted); flex-wrap: wrap; gap: 10px; }
  .page-btns { display: flex; gap: 6px; }
  .page-btn { padding: 6px 12px; border: 1px solid var(--border); border-radius: 4px; background: var(--cream); cursor: pointer; font-family: 'DM Sans', sans-serif; font-size: 12px; color: var(--ink); transition: all 0.2s; }
  .page-btn:hover, .page-btn.active { background: var(--ink); color: var(--cream); border-color: var(--ink); }
  .page-btn:disabled { opacity: 0.4; cursor: default; background: var(--cream); color: var(--muted); }

  @media(max-width:600px){ .score-grid,.chart-row{grid-template-columns:1fr} .results-hero{padding:32px 20px} .admin-header{flex-direction:column;align-items:flex-start} }
</style>
</head>
<body>

<header>
  <button class="admin-link" onclick="openAdminModal()">Admin</button>
  <div class="header-eyebrow">Academic Success Center</div>
  <h1>Learning <span>Style</span> Survey</h1>
  <p class="header-desc">Discover how you learn best. Answer honestly — there are no right or wrong answers.</p>
</header>
<div class="progress-bar-wrap"><div class="progress-bar-fill" id="progressBar"></div></div>

<main id="survey-main">
  <div id="survey-view">
    <div class="card">
      <div class="step-label">Your Information</div>
      <div class="field-group" style="margin-top:16px;">
        <div>
          <div class="field-label">Full Name <span class="field-required">*</span></div>
          <input type="text" id="fullName" placeholder="Jane Smith">
          <div class="field-error" id="nameError">Please enter your full name.</div>
        </div>
        <div>
          <div class="field-label">SAM ID <span class="field-required">*</span></div>
          <input type="text" id="samId" placeholder="12345678">
          <div class="field-error" id="samIdError">Please enter your SAM ID.</div>
        </div>
        <div>
          <div class="field-label">SAM Email <span class="field-required">*</span></div>
          <input type="email" id="samEmail" placeholder="jsmith@shsu.edu">
          <div class="field-error" id="emailError">Please enter a valid email address.</div>
        </div>
      </div>
    </div>

    <div class="section-header">
      <div class="section-icon visual">👁️</div>
      <div><div class="section-title">Visual Learning</div><div class="section-subtitle">Questions 1–5</div></div>
    </div>
    <div id="visual-questions"></div>

    <div class="section-header">
      <div class="section-icon auditory">🎧</div>
      <div><div class="section-title">Auditory Learning</div><div class="section-subtitle">Questions 6–10</div></div>
    </div>
    <div id="auditory-questions"></div>

    <div class="section-header">
      <div class="section-icon kinesthetic">🤝</div>
      <div><div class="section-title">Kinesthetic Learning</div><div class="section-subtitle">Questions 11–15</div></div>
    </div>
    <div id="kinesthetic-questions"></div>

    <div class="validation-banner" id="validationBanner">⚠️ Please answer all questions before submitting.</div>

    <div class="submit-area">
      <button class="btn-submit" onclick="submitSurvey()">
        <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M5 12h14M12 5l7 7-7 7"/></svg>
        View My Results
      </button>
      <div class="submit-note">Your results will appear instantly on this page.</div>
    </div>
  </div>

  <div id="results-view">
    <div class="results-hero">
      <div class="results-eyebrow">Your Learning Profile</div>
      <div class="results-name" id="results-name"></div>
      <span class="results-emoji" id="results-emoji"></span>
      <div class="results-type" id="results-type"></div>
    </div>
    <div class="score-grid">
      <div class="score-card" id="vs-card"><div class="score-card-label">Visual</div><div class="score-card-num" id="vs-num">0</div><div class="score-card-max">out of 15</div><div class="score-bar-track"><div class="score-bar-fill visual-fill" id="vs-bar"></div></div></div>
      <div class="score-card" id="as-card"><div class="score-card-label">Auditory</div><div class="score-card-num" id="as-num">0</div><div class="score-card-max">out of 15</div><div class="score-bar-track"><div class="score-bar-fill auditory-fill" id="as-bar"></div></div></div>
      <div class="score-card" id="ks-card"><div class="score-card-label">Kinesthetic</div><div class="score-card-num" id="ks-num">0</div><div class="score-card-max">out of 15</div><div class="score-bar-track"><div class="score-bar-fill kinesthetic-fill" id="ks-bar"></div></div></div>
    </div>
    <div class="strategies-card">
      <div class="strategies-title">📋 Recommended Study Strategies</div>
      <div id="strategies-list"></div>
    </div>
    <div class="cta-card">
      <p>Ready to build a personalized study plan? Schedule an appointment with the Academic Success Center and we'll help you put these strategies into action.</p>
      <button class="btn-cta">Schedule an Appointment</button>
      <button class="btn-restart" onclick="restartSurvey()">↩ Retake Survey</button>
    </div>
  </div>
</main>

<div id="admin-view">
  <div class="admin-header">
    <div><h2>Admin Dashboard</h2><div class="sub">Academic Success Center — Learning Style Survey</div></div>
    <div class="admin-actions">
      <button class="btn-export" onclick="exportCSV()">⬇ Export CSV</button>
      <button class="btn-logout" onclick="logoutAdmin()">Log Out</button>
    </div>
  </div>
  <div class="admin-body">
    <div class="stat-row">
      <div class="stat-card"><div class="stat-card-label">Total Submissions</div><div class="stat-card-value" id="stat-total">0</div><div class="stat-card-sub">All time</div></div>
      <div class="stat-card highlight"><div class="stat-card-label">Top Learning Style</div><div class="stat-card-value" id="stat-top">—</div><div class="stat-card-sub">Most common result</div></div>
      <div class="stat-card"><div class="stat-card-label">Visual Learners</div><div class="stat-card-value" id="stat-v">0</div><div class="stat-card-sub" id="stat-v-pct"></div></div>
      <div class="stat-card"><div class="stat-card-label">Auditory Learners</div><div class="stat-card-value" id="stat-a">0</div><div class="stat-card-sub" id="stat-a-pct"></div></div>
      <div class="stat-card"><div class="stat-card-label">Kinesthetic Learners</div><div class="stat-card-value" id="stat-k">0</div><div class="stat-card-sub" id="stat-k-pct"></div></div>
    </div>
    <div class="chart-row">
      <div class="chart-card">
        <div class="chart-title">Learning Style Distribution</div>
        <div class="donut-wrap">
          <svg id="donut-svg" width="110" height="110" viewBox="0 0 110 110"></svg>
          <div class="donut-legend" id="donut-legend"></div>
        </div>
      </div>
      <div class="chart-card">
        <div class="chart-title">Avg. Scores by Category</div>
        <div class="bar-chart" id="avg-bars"></div>
      </div>
    </div>
    <div class="table-card">
      <div class="table-toolbar">
        <div class="table-title">All Responses</div>
        <input type="text" class="table-search" id="tableSearch" placeholder="Search name, SAM ID, or email…" oninput="currentPage=1;renderTable()">
      </div>
      <div class="table-wrap">
        <table>
          <thead><tr><th>#</th><th>Date</th><th>Name</th><th>SAM ID</th><th>Email</th><th>Visual</th><th>Auditory</th><th>Kinesthetic</th><th>Result</th><th></th></tr></thead>
          <tbody id="tbl-body"></tbody>
        </table>
        <div id="no-data" class="no-data" style="display:none;">No submissions yet. Share the survey to start collecting data.</div>
      </div>
      <div class="pagination">
        <div id="page-info"></div>
        <div class="page-btns" id="page-btns"></div>
      </div>
    </div>
  </div>
</div>

<div class="modal-overlay" id="adminModal">
  <div class="modal">
    <button class="modal-close" onclick="closeAdminModal()">✕</button>
    <h2>Admin Access</h2>
    <p>Enter your password to view survey data.</p>
    <div class="field-label">Password</div>
    <input type="password" id="adminPw" placeholder="••••••••" onkeydown="if(event.key==='Enter')loginAdmin()">
    <button class="btn-login" onclick="loginAdmin()">Sign In</button>
    <div class="login-error" id="loginError">Incorrect password. Please try again.</div>
    <div style="margin-top:16px;font-size:11px;color:var(--muted);text-align:center;">Default password: <strong>admin123</strong><br>Change it in the script to secure your data.</div>
  </div>
</div>

<script>
const ADMIN_PASSWORD = 'admin123';
const STORAGE_KEY = 'asc_survey_v1';
const PAGE_SIZE = 10;
let currentPage = 1;

const QUESTIONS = [
  "I remember information better when I write it down.",
  "I can picture textbook pages or notes during a test.",
  "Flashcards help me retain material.",
  "I prefer working in a quiet environment.",
  "Looking at a speaker helps me focus.",
  "I remember information better when I hear it.",
  "I prefer lectures over reading textbooks.",
  "I understand directions better when explained verbally.",
  "Background noise makes it hard for me to focus.",
  "Writing feels tiring for me.",
  "I learn best by practicing or trying something myself.",
  "I prefer hands-on activities over reading directions.",
  "I like moving around while studying.",
  "I learn best when shown how to do something first.",
  "I take frequent study breaks."
];
const answers = new Array(15).fill(null);

function renderQuestions() {
  [['visual-questions',0,5],['auditory-questions',5,10],['kinesthetic-questions',10,15]].forEach(([id,s,e])=>{
    const el = document.getElementById(id);
    el.innerHTML = '';
    for(let i=s;i<e;i++){
      el.innerHTML += `<div class="card question-item" id="qc-${i}">
        <div class="question-text"><span class="question-num">${i+1}.</span>${QUESTIONS[i]}</div>
        <div class="choices">
          <button class="choice-btn never" onclick="pick(${i},1,this)">Never</button>
          <button class="choice-btn sometimes" onclick="pick(${i},2,this)">Sometimes</button>
          <button class="choice-btn often" onclick="pick(${i},3,this)">Often</button>
        </div></div>`;
    }
  });
  updateBar();
}

function pick(i,v,btn){
  answers[i]=v;
  document.getElementById(`qc-${i}`).querySelectorAll('.choice-btn').forEach(b=>b.classList.remove('selected'));
  btn.classList.add('selected');
  document.getElementById(`qc-${i}`).classList.remove('unanswered');
  updateBar();
}

function updateBar(){
  const n = answers.filter(a=>a!==null).length;
  document.getElementById('progressBar').style.width = Math.round(n/15*90)+'%';
}

function validate(){
  let ok=true;
  const name=document.getElementById('fullName').value.trim();
  const sid=document.getElementById('samId').value.trim();
  const em=document.getElementById('samEmail').value.trim();
  ['nameError','samIdError','emailError'].forEach(id=>document.getElementById(id).classList.remove('show'));
  ['fullName','samId','samEmail'].forEach(id=>document.getElementById(id).classList.remove('error'));
  if(!name){document.getElementById('fullName').classList.add('error');document.getElementById('nameError').classList.add('show');ok=false;}
  if(!sid){document.getElementById('samId').classList.add('error');document.getElementById('samIdError').classList.add('show');ok=false;}
  if(!em||!em.includes('@')){document.getElementById('samEmail').classList.add('error');document.getElementById('emailError').classList.add('show');ok=false;}
  if(answers.includes(null)){
    answers.forEach((a,i)=>{if(a===null)document.getElementById(`qc-${i}`).classList.add('unanswered');});
    document.getElementById('validationBanner').classList.add('show');ok=false;
  }
  return ok;
}

function submitSurvey(){
  if(!validate()){document.getElementById('validationBanner').scrollIntoView({behavior:'smooth',block:'center'});return;}
  const name=document.getElementById('fullName').value.trim();
  const samId=document.getElementById('samId').value.trim();
  const email=document.getElementById('samEmail').value.trim();
  let v=0,a=0,k=0;
  for(let i=0;i<5;i++)v+=answers[i];
  for(let i=5;i<10;i++)a+=answers[i];
  for(let i=10;i<15;i++)k+=answers[i];

  let type,emoji,strats;
  if(v>=a&&v>=k){type='Visual Learner';emoji='👁️';strats=['Use color-coded notes','Create diagrams and concept maps','Rewrite notes after class','Use flashcards'];document.getElementById('vs-card').classList.add('winner');}
  else if(a>=v&&a>=k){type='Auditory Learner';emoji='🎧';strats=['Record lectures (if permitted)','Study aloud','Join study groups','Teach material to others'];document.getElementById('as-card').classList.add('winner');}
  else{type='Kinesthetic Learner';emoji='🤝';strats=['Use practice problems','Study in short active intervals','Write on whiteboards','Apply concepts to real-world examples'];document.getElementById('ks-card').classList.add('winner');}

  const recs=getRecords();
  recs.push({id:Date.now(),date:new Date().toLocaleDateString('en-US',{month:'short',day:'numeric',year:'numeric'}),name,samId,email,visual:v,auditory:a,kinesthetic:k,type});
  localStorage.setItem(STORAGE_KEY,JSON.stringify(recs));

  document.getElementById('results-name').textContent=`Hello, ${name}!`;
  document.getElementById('results-emoji').textContent=emoji;
  const pts=type.split(' ');
  document.getElementById('results-type').innerHTML=`${pts[0]} <span class="accent">${pts.slice(1).join(' ')}</span>`;
  document.getElementById('vs-num').textContent=v;
  document.getElementById('as-num').textContent=a;
  document.getElementById('ks-num').textContent=k;
  document.getElementById('strategies-list').innerHTML=strats.map(s=>`<div class="strategy-item"><div class="strategy-dot"></div><div class="strategy-text">${s}</div></div>`).join('');
  document.getElementById('survey-view').style.display='none';
  document.getElementById('results-view').style.display='block';
  document.getElementById('progressBar').style.width='100%';
  window.scrollTo({top:0,behavior:'smooth'});
  setTimeout(()=>{
    document.getElementById('vs-bar').style.width=(v/15*100)+'%';
    document.getElementById('as-bar').style.width=(a/15*100)+'%';
    document.getElementById('ks-bar').style.width=(k/15*100)+'%';
  },200);
}

function restartSurvey(){
  answers.fill(null);
  ['vs-card','as-card','ks-card'].forEach(id=>document.getElementById(id).classList.remove('winner'));
  ['vs-bar','as-bar','ks-bar'].forEach(id=>document.getElementById(id).style.width='0');
  document.getElementById('survey-view').style.display='block';
  document.getElementById('results-view').style.display='none';
  document.getElementById('progressBar').style.width='0';
  document.getElementById('validationBanner').classList.remove('show');
  document.getElementById('fullName').value='';
  document.getElementById('samId').value='';
  document.getElementById('samEmail').value='';
  renderQuestions();
  window.scrollTo({top:0,behavior:'smooth'});
}

function getRecords(){try{return JSON.parse(localStorage.getItem(STORAGE_KEY))||[];}catch{return[];}}

function openAdminModal(){
  document.getElementById('adminModal').classList.add('open');
  document.getElementById('adminPw').value='';
  document.getElementById('loginError').classList.remove('show');
  setTimeout(()=>document.getElementById('adminPw').focus(),100);
}
function closeAdminModal(){document.getElementById('adminModal').classList.remove('open');}
function loginAdmin(){
  if(document.getElementById('adminPw').value===ADMIN_PASSWORD){closeAdminModal();showAdmin();}
  else{document.getElementById('loginError').classList.add('show');document.getElementById('adminPw').value='';}
}
function logoutAdmin(){
  document.getElementById('admin-view').style.display='none';
  document.getElementById('survey-main').style.display='block';
  window.scrollTo({top:0,behavior:'smooth'});
}

function showAdmin(){
  document.getElementById('survey-main').style.display='none';
  document.getElementById('admin-view').style.display='block';
  document.getElementById('progressBar').style.width='0';
  document.getElementById('tableSearch').value='';
  currentPage=1;
  refreshAdmin();
  window.scrollTo({top:0,behavior:'smooth'});
}

function refreshAdmin(){
  const recs=getRecords();
  const total=recs.length;
  const vc=recs.filter(r=>r.type==='Visual Learner').length;
  const ac=recs.filter(r=>r.type==='Auditory Learner').length;
  const kc=recs.filter(r=>r.type==='Kinesthetic Learner').length;
  document.getElementById('stat-total').textContent=total;
  document.getElementById('stat-v').textContent=vc;
  document.getElementById('stat-a').textContent=ac;
  document.getElementById('stat-k').textContent=kc;
  const pct=n=>total?Math.round(n/total*100)+'% of total':'—';
  document.getElementById('stat-v-pct').textContent=pct(vc);
  document.getElementById('stat-a-pct').textContent=pct(ac);
  document.getElementById('stat-k-pct').textContent=pct(kc);
  if(total===0){document.getElementById('stat-top').textContent='—';}
  else{const mx=Math.max(vc,ac,kc);document.getElementById('stat-top').textContent=vc===mx?'Visual':ac===mx?'Auditory':'Kinesthetic';}
  drawDonut(vc,ac,kc,total);
  drawAvgBars(recs);
  renderTable();
}

function drawDonut(v,a,k,total){
  const svg=document.getElementById('donut-svg');
  const legend=document.getElementById('donut-legend');
  const cx=55,cy=55,r=38,sw=18,circ=2*Math.PI*r;
  const data=[{l:'Visual',n:v,c:'#2e6da4'},{l:'Auditory',n:a,c:'#c0392b'},{l:'Kinesthetic',n:k,c:'#4a7c59'}];
  if(total===0){
    svg.innerHTML=`<circle cx="${cx}" cy="${cy}" r="${r}" fill="none" stroke="#e0d8cc" stroke-width="${sw}"/>`;
    legend.innerHTML=data.map(d=>`<div class="legend-item"><div class="legend-dot" style="background:${d.c}"></div><div class="legend-label">${d.l}</div><div class="legend-pct">—</div></div>`).join('');
    return;
  }
  let offset=0,paths='';
  data.forEach(d=>{
    const dash=d.n/total*circ;
    paths+=`<circle cx="${cx}" cy="${cy}" r="${r}" fill="none" stroke="${d.c}" stroke-width="${sw}" stroke-dasharray="${dash} ${circ-dash}" stroke-dashoffset="${-offset}" transform="rotate(-90 ${cx} ${cy})" opacity="0.88"/>`;
    offset+=dash;
  });
  svg.innerHTML=paths+`<text x="${cx}" y="${cy+6}" text-anchor="middle" font-family="Playfair Display,serif" font-size="18" font-weight="700" fill="#1a1a2e">${total}</text>`;
  legend.innerHTML=data.map(d=>`<div class="legend-item"><div class="legend-dot" style="background:${d.c}"></div><div class="legend-label">${d.l}</div><div class="legend-pct">${Math.round(d.n/total*100)}%</div></div>`).join('');
}

function drawAvgBars(recs){
  const el=document.getElementById('avg-bars');
  if(!recs.length){el.innerHTML='<div style="color:var(--muted);font-size:14px;padding:10px 0">No data yet.</div>';return;}
  el.innerHTML='';
  const av=recs.reduce((s,r)=>s+r.visual,0)/recs.length;
  const aa=recs.reduce((s,r)=>s+r.auditory,0)/recs.length;
  const ak=recs.reduce((s,r)=>s+r.kinesthetic,0)/recs.length;
  [[av,'Visual','#2e6da4'],[aa,'Auditory','#c0392b'],[ak,'Kinesthetic','#4a7c59']].forEach(([avg,lbl,col])=>{
    el.innerHTML+=`<div><div class="bar-row-label"><span>${lbl}</span><span style="color:var(--ink);font-weight:500">${avg.toFixed(1)}/15</span></div><div class="bar-row-track"><div class="bar-row-fill" style="background:${col};width:${avg/15*100}%"></div></div></div>`;
  });
}

function renderTable(){
  const recs=getRecords();
  const q=document.getElementById('tableSearch').value.toLowerCase();
  const filtered=q?recs.filter(r=>r.name.toLowerCase().includes(q)||r.samId.toLowerCase().includes(q)||r.email.toLowerCase().includes(q)):recs;
  const total=filtered.length;
  const pages=Math.max(1,Math.ceil(total/PAGE_SIZE));
  if(currentPage>pages)currentPage=pages;
  const start=(currentPage-1)*PAGE_SIZE;
  const slice=[...filtered].reverse().slice(start,start+PAGE_SIZE);
  const tbody=document.getElementById('tbl-body');
  const noData=document.getElementById('no-data');
  if(!total){tbody.innerHTML='';noData.style.display='block';}
  else{
    noData.style.display='none';
    tbody.innerHTML=slice.map((r,i)=>{
      const n=total-start-i;
      const bc=r.type==='Visual Learner'?'visual':r.type==='Auditory Learner'?'auditory':'kinesthetic';
      return `<tr>
        <td style="color:var(--muted)">${n}</td>
        <td style="color:var(--muted);white-space:nowrap">${r.date}</td>
        <td style="font-weight:500">${esc(r.name)}</td>
        <td>${esc(r.samId)}</td>
        <td style="color:var(--muted)">${esc(r.email)}</td>
        <td>${r.visual}</td><td>${r.auditory}</td><td>${r.kinesthetic}</td>
        <td><span class="badge ${bc}">${r.type.replace(' Learner','')}</span></td>
        <td><button class="btn-delete-row" onclick="delRec(${r.id})" title="Delete">✕</button></td>
      </tr>`;
    }).join('');
  }
  document.getElementById('page-info').textContent=total?`Showing ${start+1}–${Math.min(start+PAGE_SIZE,total)} of ${total}`:'';
  const pb=document.getElementById('page-btns');pb.innerHTML='';
  if(pages>1){
    const prev=document.createElement('button');prev.className='page-btn';prev.textContent='←';prev.disabled=currentPage===1;prev.onclick=()=>{currentPage--;renderTable();};pb.appendChild(prev);
    for(let p=1;p<=Math.min(pages,7);p++){const btn=document.createElement('button');btn.className='page-btn'+(p===currentPage?' active':'');btn.textContent=p;const pp=p;btn.onclick=()=>{currentPage=pp;renderTable();};pb.appendChild(btn);}
    const next=document.createElement('button');next.className='page-btn';next.textContent='→';next.disabled=currentPage===pages;next.onclick=()=>{currentPage++;renderTable();};pb.appendChild(next);
  }
}

function delRec(id){
  if(!confirm('Delete this response? This cannot be undone.'))return;
  localStorage.setItem(STORAGE_KEY,JSON.stringify(getRecords().filter(r=>r.id!==id)));
  refreshAdmin();
}

function esc(s){return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;');}

function exportCSV(){
  const recs=getRecords();
  if(!recs.length){alert('No data to export yet.');return;}
  const rows=[['#','Date','Full Name','SAM ID','Email','Visual Score','Auditory Score','Kinesthetic Score','Learning Style']];
  recs.forEach((r,i)=>rows.push([i+1,r.date,`"${r.name.replace(/"/g,'""')}"`,r.samId,r.email,r.visual,r.auditory,r.kinesthetic,r.type]));
  const csv=rows.map(r=>r.join(',')).join('\n');
  const a=document.createElement('a');
  a.href=URL.createObjectURL(new Blob([csv],{type:'text/csv'}));
  a.download=`asc-survey-${new Date().toISOString().slice(0,10)}.csv`;
  a.click();
}

renderQuestions();
</script>
</body>
</html>
