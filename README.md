<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>EduManage LMS — Teacher Portal</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@600;700&family=DM+Sans:wght@400;500;600&display=swap" rel="stylesheet">
<style>
*{box-sizing:border-box;margin:0;padding:0}
:root{
  --maroon:#6B1A2A;--maroon-dark:#4A0F1C;--maroon-light:#8B2A3F;--maroon-pale:#F5E8EB;
  --gold:#C9A227;--gold-light:#E8C04A;--gold-pale:#FDF6E3;--gold-dark:#A07A10;
  --white:#fff;--gray-50:#F8F7F5;--gray-100:#EDEDEA;--gray-200:#D4D3CE;--gray-400:#9A9890;--gray-600:#5C5A54;--gray-800:#2C2C2A;
  --sidebar-w:220px;--font-display:'Playfair Display',serif;--font-body:'DM Sans',sans-serif;
}
body{font-family:var(--font-body);background:var(--gray-50);color:var(--gray-800);overflow-x:hidden}
.app{display:flex;min-height:100vh}
.sidebar{width:var(--sidebar-w);background:var(--maroon-dark);color:var(--white);display:flex;flex-direction:column;position:fixed;top:0;left:0;height:100vh;z-index:100;overflow-y:auto}
.sidebar-logo{padding:24px 20px 16px;border-bottom:1px solid rgba(201,162,39,0.3)}
.sidebar-logo h1{font-family:var(--font-display);font-size:16px;color:var(--gold-light);line-height:1.3}
.sidebar-logo p{font-size:11px;color:rgba(255,255,255,0.5);margin-top:4px}
.sidebar-nav{flex:1;padding:12px 0}
.nav-item{display:flex;align-items:center;gap:10px;padding:11px 20px;cursor:pointer;font-size:13.5px;font-weight:500;color:rgba(255,255,255,0.75);transition:all 0.18s;border-left:3px solid transparent}
.nav-item:hover{background:rgba(201,162,39,0.12);color:var(--white)}
.nav-item.active{background:rgba(201,162,39,0.18);color:var(--gold-light);border-left-color:var(--gold)}
.nav-item svg{width:16px;height:16px;opacity:0.8;flex-shrink:0}
.nav-badge{margin-left:auto;background:var(--gold);color:var(--maroon-dark);font-size:10px;font-weight:700;padding:2px 7px;border-radius:10px}
.sidebar-bottom{padding:12px 0;border-top:1px solid rgba(255,255,255,0.1)}
.main{margin-left:var(--sidebar-w);flex:1;display:flex;flex-direction:column;min-height:100vh}
.topbar{background:var(--white);border-bottom:1px solid var(--gray-100);padding:0 28px;height:58px;display:flex;align-items:center;justify-content:space-between;position:sticky;top:0;z-index:50}
.topbar-title{font-family:var(--font-display);font-size:20px;font-weight:700;color:var(--maroon)}
.topbar-right{display:flex;align-items:center;gap:12px}
.avatar{width:34px;height:34px;border-radius:50%;background:var(--maroon);color:var(--gold-light);font-size:13px;font-weight:700;display:flex;align-items:center;justify-content:center;cursor:pointer;font-family:var(--font-display)}
.content{padding:28px;flex:1}
.screen{display:none}.screen.active{display:block}
.card{background:var(--white);border-radius:12px;border:1px solid var(--gray-100);padding:20px 24px;margin-bottom:16px}
.card-title{font-family:var(--font-display);font-size:15px;font-weight:700;color:var(--maroon);margin-bottom:14px;display:flex;align-items:center;gap:8px}
.grid-2{display:grid;grid-template-columns:1fr 1fr;gap:14px}
.grid-3{display:grid;grid-template-columns:1fr 1fr 1fr;gap:14px}
.grid-4{display:grid;grid-template-columns:repeat(4,1fr);gap:12px}
.stat-card{background:var(--white);border:1px solid var(--gray-100);border-radius:10px;padding:14px 16px}
.stat-label{font-size:11px;color:var(--gray-400);text-transform:uppercase;letter-spacing:0.8px;margin-bottom:4px;font-weight:600}
.stat-val{font-size:26px;font-weight:700;font-family:var(--font-display);color:var(--maroon)}
.stat-sub{font-size:12px;color:var(--gray-400);margin-top:2px}
.subject-card{background:linear-gradient(135deg,var(--maroon) 0%,var(--maroon-light) 100%);color:var(--white);border-radius:12px;padding:18px 20px;cursor:pointer;transition:transform 0.18s,box-shadow 0.18s;position:relative;overflow:hidden}
.subject-card:hover{transform:translateY(-2px);box-shadow:0 8px 24px rgba(107,26,42,0.25)}
.subject-card::after{content:'';position:absolute;top:-20px;right:-20px;width:80px;height:80px;background:rgba(201,162,39,0.2);border-radius:50%}
.subject-card h3{font-family:var(--font-display);font-size:14px;font-weight:700;margin-bottom:4px;position:relative;z-index:1}
.subject-card p{font-size:12px;opacity:0.75;position:relative;z-index:1}
.sc-code{font-size:11px;background:rgba(201,162,39,0.3);color:var(--gold-light);padding:2px 8px;border-radius:6px;display:inline-block;margin-bottom:8px;font-weight:600;position:relative;z-index:1}
.btn{display:inline-flex;align-items:center;gap:6px;padding:8px 16px;border-radius:8px;font-size:13px;font-weight:600;cursor:pointer;border:none;transition:all 0.16s;font-family:var(--font-body)}
.btn-primary{background:var(--maroon);color:var(--white)}.btn-primary:hover{background:var(--maroon-light)}
.btn-gold{background:var(--gold);color:var(--maroon-dark)}.btn-gold:hover{background:var(--gold-light)}
.btn-outline{background:transparent;color:var(--maroon);border:1.5px solid var(--maroon)}.btn-outline:hover{background:var(--maroon-pale)}
.btn-sm{padding:5px 12px;font-size:12px}
.btn-danger{background:#f5e8e8;color:#8B2020;border:none}.btn-danger:hover{background:#f0d0d0}
input[type=text],input[type=email],input[type=password],input[type=number],select,textarea{width:100%;padding:9px 12px;border:1.5px solid var(--gray-200);border-radius:8px;font-family:var(--font-body);font-size:13.5px;color:var(--gray-800);background:var(--white);transition:border 0.16s}
input:focus,select:focus,textarea:focus{outline:none;border-color:var(--maroon)}
label{font-size:12.5px;font-weight:600;color:var(--gray-600);display:block;margin-bottom:5px}
.form-group{margin-bottom:14px}
table{width:100%;border-collapse:collapse;font-size:13px}
th{background:var(--maroon-pale);color:var(--maroon);font-weight:700;padding:10px 12px;text-align:left;font-size:12px;text-transform:uppercase;letter-spacing:0.6px}
td{padding:9px 12px;border-bottom:1px solid var(--gray-100);vertical-align:middle}
tr:hover td{background:var(--gray-50)}
.badge{display:inline-flex;align-items:center;padding:3px 9px;border-radius:20px;font-size:11px;font-weight:700}
.badge-present{background:#E8F5E2;color:#2E7D32}
.badge-absent{background:#FFEBEE;color:#C62828}
.badge-grade{background:var(--gold-pale);color:var(--gold-dark)}
.tab-bar{display:flex;gap:4px;background:var(--gray-100);border-radius:10px;padding:4px;margin-bottom:20px}
.tab{padding:7px 16px;border-radius:7px;font-size:13px;font-weight:600;cursor:pointer;color:var(--gray-600);transition:all 0.16s}
.tab.active{background:var(--white);color:var(--maroon);box-shadow:0 1px 4px rgba(0,0,0,0.1)}
.grade-table input[type=number]{width:60px;text-align:center;padding:4px;font-size:12px}
.grade-cell-computed{background:#FFF8E1;color:var(--gold-dark);font-weight:700;text-align:center;font-size:13px}
.grade-cell-fixed{background:var(--maroon-pale);color:var(--maroon);font-weight:700;font-size:12px;text-align:center}
.search-box{position:relative;flex:1}
.search-box input{padding-left:34px}
.search-box svg{position:absolute;left:10px;top:50%;transform:translateY(-50%);width:15px;height:15px;color:var(--gray-400)}
.student-grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(150px,1fr));gap:12px}
.student-card-grid{background:var(--white);border:1px solid var(--gray-100);border-radius:10px;padding:16px;text-align:center;cursor:pointer;transition:all 0.16s}
.student-card-grid:hover{border-color:var(--maroon);box-shadow:0 4px 12px rgba(107,26,42,0.12)}
.student-avatar{width:52px;height:52px;border-radius:50%;background:var(--maroon);color:var(--gold-light);font-family:var(--font-display);font-size:18px;font-weight:700;display:flex;align-items:center;justify-content:center;margin:0 auto 8px}
.breadcrumb{display:flex;align-items:center;gap:6px;font-size:13px;color:var(--gray-400);margin-bottom:18px}
.breadcrumb span{cursor:pointer;color:var(--maroon);font-weight:500}.breadcrumb span:hover{text-decoration:underline}
.section-header{display:flex;align-items:center;justify-content:space-between;margin-bottom:14px}
.section-title{font-family:var(--font-display);font-size:17px;font-weight:700;color:var(--maroon)}
.final-grade-banner{background:linear-gradient(135deg,var(--maroon) 0%,var(--maroon-light) 100%);color:var(--white);border-radius:12px;padding:18px 24px;display:flex;align-items:center;justify-content:space-between}
.grade-num{font-size:42px;font-weight:800;font-family:var(--font-display);color:var(--gold-light)}
.modal-overlay{position:fixed;inset:0;background:rgba(0,0,0,0.45);z-index:200;display:none;align-items:center;justify-content:center}
.modal-overlay.open{display:flex}
.modal{background:var(--white);border-radius:14px;padding:28px;width:420px;max-width:90vw;max-height:80vh;overflow-y:auto}
.modal-title{font-family:var(--font-display);font-size:18px;font-weight:700;color:var(--maroon);margin-bottom:18px}
.modal-actions{display:flex;gap:10px;justify-content:flex-end;margin-top:18px}
.schedule-row{display:flex;align-items:center;gap:12px;padding:10px 0;border-bottom:1px solid var(--gray-100)}
.schedule-day{width:70px;font-size:12px;font-weight:700;color:var(--gray-400);text-transform:uppercase;letter-spacing:0.5px}
.profile-pic-circle{width:90px;height:90px;border-radius:50%;background:var(--maroon);color:var(--gold-light);font-family:var(--font-display);font-size:30px;font-weight:700;display:flex;align-items:center;justify-content:center;border:3px solid var(--gold);cursor:pointer}
.tag{display:inline-flex;align-items:center;padding:3px 10px;background:var(--maroon-pale);color:var(--maroon);border-radius:20px;font-size:12px;font-weight:600}
.curriculum-item{display:flex;align-items:center;gap:10px;padding:10px 0;border-bottom:1px solid var(--gray-100)}
.ci-num{width:28px;height:28px;border-radius:50%;background:var(--maroon-pale);color:var(--maroon);font-size:12px;font-weight:700;display:flex;align-items:center;justify-content:center;flex-shrink:0}
.ci-title{flex:1;font-size:13.5px;font-weight:500}
.login-screen{min-height:100vh;background:linear-gradient(135deg,var(--maroon-dark) 0%,var(--maroon) 60%,var(--maroon-light) 100%);display:flex;align-items:center;justify-content:center;padding:24px;position:fixed;inset:0;z-index:300}
.login-card{background:var(--white);border-radius:16px;padding:36px;width:380px;max-width:95vw}
.login-logo{text-align:center;margin-bottom:24px}
.login-logo h1{font-family:var(--font-display);font-size:22px;color:var(--maroon);font-weight:700}
.login-logo p{font-size:13px;color:var(--gray-400);margin-top:4px}
.login-tabs{display:flex;gap:4px;background:var(--gray-100);border-radius:10px;padding:4px;margin-bottom:20px}
.login-tab{flex:1;padding:8px;border-radius:7px;font-size:13px;font-weight:600;cursor:pointer;color:var(--gray-600);text-align:center;transition:all 0.16s}
.login-tab.active{background:var(--white);color:var(--maroon)}
.gold-divider{height:3px;background:linear-gradient(90deg,var(--gold),var(--gold-light),var(--gold));border-radius:2px;margin:0 0 20px}
.notice-box{background:var(--gray-50);border:1px dashed var(--gray-200);border-radius:8px;padding:10px 14px;font-size:12px;color:var(--gray-600);text-align:center;margin-top:10px}
.toggle-view{display:flex;gap:4px}
.view-btn{width:32px;height:32px;display:flex;align-items:center;justify-content:center;border-radius:7px;cursor:pointer;border:1.5px solid var(--gray-200);color:var(--gray-400);background:var(--white);transition:all 0.15s}
.view-btn.active{border-color:var(--maroon);color:var(--maroon);background:var(--maroon-pale)}
.settings-row{display:flex;align-items:center;justify-content:space-between;padding:12px 0;border-bottom:1px solid var(--gray-100)}
.toggle-switch{width:42px;height:24px;border-radius:12px;background:var(--gray-200);cursor:pointer;position:relative;transition:background 0.2s;flex-shrink:0}
.toggle-switch.on{background:var(--maroon)}
.toggle-switch::after{content:'';position:absolute;width:18px;height:18px;border-radius:50%;background:white;top:3px;left:3px;transition:left 0.2s}
.toggle-switch.on::after{left:21px}
</style>
</head>
<body>

<!-- LOGIN -->
<div class="login-screen" id="loginScreen">
  <div class="login-card">
    <div class="login-logo">
      <div style="font-size:36px;margin-bottom:8px">🎓</div>
      <h1>EduManage LMS</h1>
      <p>Teacher's Learning Management System</p>
    </div>
    <div class="gold-divider"></div>
    <div class="login-tabs">
      <div class="login-tab active" onclick="switchLoginTab('login')">Sign In</div>
      <div class="login-tab" onclick="switchLoginTab('register')">Register</div>
    </div>
    <div id="loginForm">
      <div class="form-group"><label>Email / Username</label><input type="email" placeholder="teacher@school.edu"/></div>
      <div class="form-group"><label>Password</label><input type="password" placeholder="••••••••"/></div>
      <button class="btn btn-primary" style="width:100%;justify-content:center;padding:11px" onclick="doLogin()">Sign In</button>
      <div class="notice-box">Demo mode — click Sign In with any credentials</div>
    </div>
    <div id="registerForm" style="display:none">
      <div class="form-group"><label>Full Name</label><input type="text" placeholder="Maria Santos"/></div>
      <div class="form-group"><label>Teacher ID</label><input type="text" placeholder="TCH-2024-001"/></div>
      <div class="form-group"><label>Email</label><input type="email" placeholder="m.santos@school.edu"/></div>
      <div class="form-group"><label>Password</label><input type="password" placeholder="Create password"/></div>
      <button class="btn btn-primary" style="width:100%;justify-content:center;padding:11px" onclick="doLogin()">Create Account</button>
    </div>
  </div>
</div>

<!-- APP -->
<div class="app" id="mainApp" style="display:none">
  <aside class="sidebar">
    <div class="sidebar-logo">
      <h1>EduManage LMS</h1>
      <p>Teacher Portal</p>
    </div>
    <nav class="sidebar-nav">
      <div class="nav-item active" data-screen="dashboard" onclick="navTo('dashboard',this)">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/><rect x="14" y="14" width="7" height="7"/><rect x="3" y="14" width="7" height="7"/></svg>
        Dashboard
      </div>
      <div class="nav-item" data-screen="profile" onclick="navTo('profile',this)">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="8" r="4"/><path d="M6 20v-2a4 4 0 014-4h4a4 4 0 014 4v2"/></svg>
        Teacher Profile
      </div>
      <div class="nav-item" data-screen="classes" onclick="navTo('classes',this)">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M17 21v-2a4 4 0 00-4-4H5a4 4 0 00-4 4v2"/><circle cx="9" cy="7" r="4"/><path d="M23 21v-2a4 4 0 00-3-3.87"/><path d="M16 3.13a4 4 0 010 7.75"/></svg>
        Class Information
        <span class="nav-badge">4</span>
      </div>
      <div class="nav-item" data-screen="curriculum" onclick="navTo('curriculum',this)">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M4 19.5A2.5 2.5 0 016.5 17H20"/><path d="M6.5 2H20v20H6.5A2.5 2.5 0 014 19.5v-15A2.5 2.5 0 016.5 2z"/></svg>
        Course Curriculum
      </div>
      <div class="nav-item" data-screen="settings" onclick="navTo('settings',this)">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="12" cy="12" r="3"/><path d="M19.4 15a1.65 1.65 0 00.33 1.82l.06.06a2 2 0 010 2.83 2 2 0 01-2.83 0l-.06-.06a1.65 1.65 0 00-1.82-.33 1.65 1.65 0 00-1 1.51V21a2 2 0 01-4 0v-.09A1.65 1.65 0 009 19.4a1.65 1.65 0 00-1.82.33l-.06.06a2 2 0 01-2.83-2.83l.06-.06A1.65 1.65 0 004.68 15a1.65 1.65 0 00-1.51-1H3a2 2 0 010-4h.09A1.65 1.65 0 004.6 9a1.65 1.65 0 00-.33-1.82l-.06-.06a2 2 0 012.83-2.83l.06.06A1.65 1.65 0 009 4.68a1.65 1.65 0 001-1.51V3a2 2 0 014 0v.09a1.65 1.65 0 001 1.51 1.65 1.65 0 001.82-.33l.06-.06a2 2 0 012.83 2.83l-.06.06A1.65 1.65 0 0019.4 9a1.65 1.65 0 001.51 1H21a2 2 0 010 4h-.09a1.65 1.65 0 00-1.51 1z"/></svg>
        Settings
      </div>
    </nav>
    <div class="sidebar-bottom">
      <div class="nav-item" onclick="doLogout()">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path d="M9 21H5a2 2 0 01-2-2V5a2 2 0 012-2h4"/><polyline points="16,17 21,12 16,7"/><line x1="21" y1="12" x2="9" y2="12"/></svg>
        Log Out
      </div>
    </div>
  </aside>

  <main class="main">
    <div class="topbar">
      <div class="topbar-title" id="topbarTitle">Dashboard</div>
      <div class="topbar-right">
        <div style="font-size:13px;color:var(--gray-600)">S.Y. 2024–2025 · 2nd Semester</div>
        <div class="avatar">MS</div>
      </div>
    </div>

    <div class="content">

      <!-- DASHBOARD -->
      <div class="screen active" id="screen-dashboard">
        <div class="grid-4" style="margin-bottom:20px">
          <div class="stat-card"><div class="stat-label">Subjects Handled</div><div class="stat-val">4</div><div class="stat-sub">This semester</div></div>
          <div class="stat-card"><div class="stat-label">Total Students</div><div class="stat-val">128</div><div class="stat-sub">Enrolled</div></div>
          <div class="stat-card"><div class="stat-label">Classes Today</div><div class="stat-val">3</div><div class="stat-sub">Wednesday</div></div>
          <div class="stat-card"><div class="stat-label">Pending Grades</div><div class="stat-val">12</div><div class="stat-sub">Needs input</div></div>
        </div>
        <div class="card">
          <div class="card-title">Subjects Handled</div>
          <div class="grid-2">
            <div class="subject-card" onclick="navTo('classes',document.querySelector('[data-screen=classes]'))">
              <div class="sc-code">MATH 10</div>
              <h3>Mathematics — Grade 10</h3>
              <p>32 students · Section Sampaguita</p>
            </div>
            <div class="subject-card" onclick="navTo('classes',document.querySelector('[data-screen=classes]'))">
              <div class="sc-code">SCI 10</div>
              <h3>Science — Grade 10</h3>
              <p>30 students · Section Sampaguita</p>
            </div>
            <div class="subject-card" onclick="navTo('classes',document.querySelector('[data-screen=classes]'))">
              <div class="sc-code">MATH 11</div>
              <h3>Pre-Calculus — Grade 11</h3>
              <p>35 students · STEM A</p>
            </div>
            <div class="subject-card" onclick="navTo('classes',document.querySelector('[data-screen=classes]'))">
              <div class="sc-code">STAT 12</div>
              <h3>Statistics — Grade 12</h3>
              <p>31 students · STEM B</p>
            </div>
          </div>
        </div>
        <div class="card">
          <div class="card-title">This Week's Schedule</div>
          <div class="schedule-row"><div class="schedule-day">Mon</div><div style="flex:1;font-size:13.5px;font-weight:600">Mathematics — Grade 10 (Sec. Sampaguita)</div><div style="font-size:12px;color:var(--gray-400)">7:30–9:00 AM · Room 201</div></div>
          <div class="schedule-row"><div class="schedule-day">Tue</div><div style="flex:1;font-size:13.5px;font-weight:600">Science — Grade 10 (Sec. Sampaguita)</div><div style="font-size:12px;color:var(--gray-400)">10:00–11:30 AM · Lab 1</div></div>
          <div class="schedule-row"><div class="schedule-day">Wed</div><div style="flex:1;font-size:13.5px;font-weight:600">Pre-Calculus — Grade 11 (STEM A)</div><div style="font-size:12px;color:var(--gray-400)">8:00–9:30 AM · Room 305</div></div>
          <div class="schedule-row"><div class="schedule-day">Wed</div><div style="flex:1;font-size:13.5px;font-weight:600">Statistics — Grade 12 (STEM B)</div><div style="font-size:12px;color:var(--gray-400)">1:00–2:30 PM · Room 306</div></div>
          <div class="schedule-row" style="border:none"><div class="schedule-day">Fri</div><div style="flex:1;font-size:13.5px;font-weight:600">Pre-Calculus — Grade 11 (STEM A)</div><div style="font-size:12px;color:var(--gray-400)">8:00–9:30 AM · Room 305</div></div>
        </div>
      </div>

      <!-- TEACHER PROFILE -->
      <div class="screen" id="screen-profile">
        <div class="card">
          <div class="section-header">
            <div class="section-title">Teacher Profile</div>
            <button class="btn btn-gold btn-sm" id="profileEditBtn" onclick="toggleProfileEdit()">Edit Profile</button>
          </div>
          <div style="display:flex;align-items:flex-start;gap:28px;margin-bottom:20px">
            <div>
              <div class="profile-pic-circle" onclick="alert('Click to upload photo')">MS</div>
              <div style="text-align:center;font-size:11px;color:var(--gray-400);margin-top:6px">Change photo</div>
            </div>
            <div style="flex:1">
              <div class="grid-2" id="profileView">
                <div><div style="font-size:12px;color:var(--gray-400);margin-bottom:3px">Full Name</div><div style="font-size:15px;font-weight:600" id="vName">Maria Santos</div></div>
                <div><div style="font-size:12px;color:var(--gray-400);margin-bottom:3px">Teacher ID</div><div style="font-size:15px;font-weight:600">TCH-2024-001</div></div>
                <div><div style="font-size:12px;color:var(--gray-400);margin-bottom:3px">Email</div><div style="font-size:15px;font-weight:600" id="vEmail">m.santos@school.edu</div></div>
                <div><div style="font-size:12px;color:var(--gray-400);margin-bottom:3px">Department</div><div style="font-size:15px;font-weight:600" id="vDept">Science & Mathematics</div></div>
              </div>
              <div class="grid-2" id="profileEditForm" style="display:none">
                <div class="form-group"><label>Full Name</label><input type="text" id="eName" value="Maria Santos"/></div>
                <div class="form-group"><label>Teacher ID</label><input type="text" value="TCH-2024-001" disabled style="background:var(--gray-50)"/></div>
                <div class="form-group"><label>Email</label><input type="email" id="eEmail" value="m.santos@school.edu"/></div>
                <div class="form-group"><label>Department</label><input type="text" id="eDept" value="Science & Mathematics"/></div>
              </div>
              <div id="profileSaveRow" style="display:none;margin-top:10px">
                <button class="btn btn-primary btn-sm" onclick="saveProfile()">Save Changes</button>
                <button class="btn btn-outline btn-sm" style="margin-left:8px" onclick="cancelProfileEdit()">Cancel</button>
              </div>
            </div>
          </div>
          <div style="border-top:1px solid var(--gray-100);padding-top:16px">
            <div style="font-size:12.5px;font-weight:700;color:var(--gray-600);margin-bottom:10px;text-transform:uppercase;letter-spacing:0.6px">Subjects Handled</div>
            <div style="display:flex;flex-wrap:wrap;gap:8px">
              <span class="tag">Mathematics — Grade 10</span>
              <span class="tag">Science — Grade 10</span>
              <span class="tag">Pre-Calculus — Grade 11</span>
              <span class="tag">Statistics — Grade 12</span>
            </div>
          </div>
        </div>
      </div>

      <!-- CLASS INFORMATION -->
      <div class="screen" id="screen-classes">
        <div id="classesView">
          <div class="section-header">
            <div class="section-title">Class Information</div>
            <button class="btn btn-primary btn-sm" onclick="openModal('addClassModal')">+ Add Class</button>
          </div>
          <div class="grid-2">
            <div class="card" style="cursor:pointer" onmouseenter="this.style.boxShadow='0 4px 16px rgba(107,26,42,0.12)'" onmouseleave="this.style.boxShadow=''" onclick="openClassDetail('MATH10','Mathematics — Grade 10')">
              <div style="display:flex;align-items:flex-start;justify-content:space-between">
                <div><div style="background:var(--maroon-pale);color:var(--maroon);padding:3px 10px;border-radius:6px;font-size:11px;font-weight:700;display:inline-block;margin-bottom:8px">MATH 10</div><div style="font-size:15px;font-weight:700">Mathematics — Grade 10</div><div style="font-size:12px;color:var(--gray-400);margin-top:3px">Section Sampaguita · 32 students</div></div>
                <div style="font-size:11px;background:var(--gold-pale);color:var(--gold-dark);padding:3px 8px;border-radius:6px;font-weight:700">Q2</div>
              </div>
              <div style="display:flex;gap:8px;margin-top:14px">
                <div style="flex:1;text-align:center;background:var(--gray-50);border-radius:8px;padding:8px"><div style="font-size:18px;font-weight:700;color:var(--maroon)">32</div><div style="font-size:11px;color:var(--gray-400)">Students</div></div>
                <div style="flex:1;text-align:center;background:var(--gray-50);border-radius:8px;padding:8px"><div style="font-size:18px;font-weight:700;color:var(--maroon)">4</div><div style="font-size:11px;color:var(--gray-400)">Quizzes</div></div>
                <div style="flex:1;text-align:center;background:var(--gray-50);border-radius:8px;padding:8px"><div style="font-size:18px;font-weight:700;color:var(--maroon)">3</div><div style="font-size:11px;color:var(--gray-400)">Activities</div></div>
              </div>
            </div>
            <div class="card" style="cursor:pointer" onmouseenter="this.style.boxShadow='0 4px 16px rgba(107,26,42,0.12)'" onmouseleave="this.style.boxShadow=''" onclick="openClassDetail('SCI10','Science — Grade 10')">
              <div style="display:flex;align-items:flex-start;justify-content:space-between">
                <div><div style="background:var(--maroon-pale);color:var(--maroon);padding:3px 10px;border-radius:6px;font-size:11px;font-weight:700;display:inline-block;margin-bottom:8px">SCI 10</div><div style="font-size:15px;font-weight:700">Science — Grade 10</div><div style="font-size:12px;color:var(--gray-400);margin-top:3px">Section Sampaguita · 30 students</div></div>
                <div style="font-size:11px;background:var(--gold-pale);color:var(--gold-dark);padding:3px 8px;border-radius:6px;font-weight:700">Q2</div>
              </div>
              <div style="display:flex;gap:8px;margin-top:14px">
                <div style="flex:1;text-align:center;background:var(--gray-50);border-radius:8px;padding:8px"><div style="font-size:18px;font-weight:700;color:var(--maroon)">30</div><div style="font-size:11px;color:var(--gray-400)">Students</div></div>
                <div style="flex:1;text-align:center;background:var(--gray-50);border-radius:8px;padding:8px"><div style="font-size:18px;font-weight:700;color:var(--maroon)">3</div><div style="font-size:11px;color:var(--gray-400)">Quizzes</div></div>
                <div style="flex:1;text-align:center;background:var(--gray-50);border-radius:8px;padding:8px"><div style="font-size:18px;font-weight:700;color:var(--maroon)">4</div><div style="font-size:11px;color:var(--gray-400)">Activities</div></div>
              </div>
            </div>
          </div>
        </div>

        <!-- CLASS DETAIL -->
        <div id="classDetailView" style="display:none">
          <div class="breadcrumb">
            <span onclick="backToClasses()">Class Information</span>
            <span style="color:var(--gray-200)">›</span>
            <span id="classDetailName" style="cursor:default;color:var(--gray-600)">—</span>
          </div>
          <div class="tab-bar" id="classDetailTabs">
            <div class="tab active" onclick="switchClassTab('students',this)">Students</div>
            <div class="tab" onclick="switchClassTab('grades',this)">Grade Book</div>
            <div class="tab" onclick="switchClassTab('attendance',this)">Attendance</div>
          </div>

          <div id="ctab-students">
            <div style="display:flex;align-items:center;gap:10px;margin-bottom:16px">
              <div class="search-box">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><circle cx="11" cy="11" r="8"/><line x1="21" y1="21" x2="16.65" y2="16.65"/></svg>
                <input type="text" placeholder="Search students…" oninput="renderStudents(this.value)"/>
              </div>
              <div class="toggle-view">
                <div class="view-btn active" id="gridViewBtn" onclick="setView('grid')"><svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><rect x="3" y="3" width="7" height="7"/><rect x="14" y="3" width="7" height="7"/><rect x="3" y="14" width="7" height="7"/><rect x="14" y="14" width="7" height="7"/></svg></div>
                <div class="view-btn" id="listViewBtn" onclick="setView('list')"><svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5"><line x1="8" y1="6" x2="21" y2="6"/><line x1="8" y1="12" x2="21" y2="12"/><line x1="8" y1="18" x2="21" y2="18"/></svg></div>
              </div>
              <button class="btn btn-primary btn-sm" onclick="openModal('addStudentModal')">+ Add Student</button>
            </div>
            <div class="student-grid" id="studentGridView"></div>
            <table id="studentListView" style="display:none">
              <thead><tr><th>Name</th><th>Student ID</th><th>Final Grade</th><th>Actions</th></tr></thead>
              <tbody id="studentListBody"></tbody>
            </table>
          </div>

          <div id="ctab-grades" style="display:none">
            <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:14px">
              <div style="font-size:13px;color:var(--gray-600)">
                Input fields: <span style="background:#FFF0F0;color:#C62828;padding:1px 8px;border-radius:4px;font-size:12px;font-weight:700;border:1px solid #FFCCCC">red</span> &nbsp;
                Computed: <span style="background:#FFF8E1;color:var(--gold-dark);padding:1px 8px;border-radius:4px;font-size:12px;font-weight:700">yellow</span>
              </div>
              <div style="display:flex;gap:8px">
                <button class="btn btn-outline btn-sm" onclick="addQuizColumn()">+ Quiz</button>
                <button class="btn btn-outline btn-sm" onclick="addActivityColumn()">+ Activity</button>
                <button class="btn btn-gold btn-sm" onclick="computeAllGrades()">Recompute All</button>
              </div>
            </div>
            <div style="overflow-x:auto">
              <table class="grade-table" id="gradeTable">
                <thead id="gradeHead"></thead>
                <tbody id="gradeTableBody"></tbody>
              </table>
            </div>
          </div>

          <div id="ctab-attendance" style="display:none">
            <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:14px">
              <div style="font-size:13px;color:var(--gray-600)">Click a cell to toggle Present / Absent</div>
              <button class="btn btn-primary btn-sm" onclick="addAttendanceDate()">+ Add Date</button>
            </div>
            <div style="overflow-x:auto">
              <table id="attendanceTable">
                <thead id="attendanceHead"></thead>
                <tbody id="attendanceBody"></tbody>
              </table>
            </div>
          </div>
        </div>
      </div>

      <!-- STUDENT PROFILE -->
      <div class="screen" id="screen-student">
        <div class="breadcrumb">
          <span onclick="navTo('classes',document.querySelector('[data-screen=classes]'))">Class Information</span>
          <span style="color:var(--gray-200)">›</span>
          <span onclick="backToClassDetail()">Class Detail</span>
          <span style="color:var(--gray-200)">›</span>
          <span id="spBreadcrumb" style="color:var(--gray-600);cursor:default">Student</span>
        </div>
        <div style="display:flex;gap:24px;align-items:flex-start">
          <div style="flex-shrink:0;text-align:center">
            <div class="student-avatar" style="width:80px;height:80px;font-size:26px;margin:0 auto 10px" id="spAvatar">JD</div>
            <div style="font-size:15px;font-weight:700;margin-bottom:3px" id="spName">—</div>
            <div style="font-size:12px;color:var(--gray-400)" id="spId">—</div>
          </div>
          <div style="flex:1">
            <div class="final-grade-banner" style="margin-bottom:16px">
              <div>
                <div style="font-size:11px;opacity:0.7;text-transform:uppercase;letter-spacing:0.8px;margin-bottom:4px">Final Grade</div>
                <div class="grade-num" id="spFinalGrade">—</div>
                <div style="font-size:12px;opacity:0.6;margin-top:4px">Class Performance × 70% + Exam × 30%</div>
              </div>
              <div style="text-align:right">
                <div style="font-size:11px;opacity:0.7">Class Performance (70%)</div>
                <div style="font-size:24px;font-weight:700;color:var(--gold-light);margin:2px 0" id="spClassPerf">—</div>
                <div style="font-size:11px;opacity:0.7;margin-top:8px">Major Exam (30%)</div>
                <div style="font-size:24px;font-weight:700;color:var(--gold-light);margin-top:2px" id="spExamScore">—</div>
              </div>
            </div>
            <div class="card">
              <div class="card-title">Score Breakdown</div>
              <table id="spTable">
                <thead><tr><th>Component</th><th>Raw</th><th>Weight</th><th>Weighted</th></tr></thead>
                <tbody id="spTableBody"></tbody>
              </table>
            </div>
          </div>
        </div>
      </div>

      <!-- CURRICULUM -->
      <div class="screen" id="screen-curriculum">
        <div style="display:flex;align-items:center;justify-content:space-between;margin-bottom:16px">
          <div class="section-title">Course Curriculum</div>
          <div style="display:flex;gap:8px;align-items:center">
            <select id="currLevel" style="width:auto" onchange="renderCurriculum()">
              <option value="basic">Basic Education</option>
              <option value="undergrad">Undergraduate</option>
            </select>
            <select id="currPeriod" style="width:auto" onchange="renderCurriculum()">
              <option value="q1">Quarter 1</option>
              <option value="q2">Quarter 2</option>
              <option value="q3">Quarter 3</option>
              <option value="q4">Quarter 4</option>
            </select>
            <button class="btn btn-primary btn-sm" onclick="openModal('addTopicModal')">+ Add Topic</button>
          </div>
        </div>
        <div class="grid-2" id="curriculumGrid"></div>
      </div>

      <!-- SETTINGS -->
      <div class="screen" id="screen-settings">
        <div class="card">
          <div class="card-title">Account Settings</div>
          <div class="settings-row">
            <div><div style="font-size:13.5px;font-weight:500">Email Notifications</div><div style="font-size:12px;color:var(--gray-400);margin-top:2px">Receive updates about grades and submissions</div></div>
            <div class="toggle-switch on" onclick="this.classList.toggle('on')"></div>
          </div>
          <div class="settings-row">
            <div><div style="font-size:13.5px;font-weight:500">Two-Factor Authentication</div><div style="font-size:12px;color:var(--gray-400);margin-top:2px">Extra security for your account</div></div>
            <div class="toggle-switch" onclick="this.classList.toggle('on')"></div>
          </div>
          <div class="settings-row" style="border:none">
            <div><div style="font-size:13.5px;font-weight:500">Auto-save Grade Book</div><div style="font-size:12px;color:var(--gray-400);margin-top:2px">Save changes automatically every 30 seconds</div></div>
            <div class="toggle-switch on" onclick="this.classList.toggle('on')"></div>
          </div>
        </div>
        <div class="card">
          <div class="card-title">Profile Settings</div>
          <div class="grid-2">
            <div class="form-group"><label>Display Name</label><input type="text" value="Ms. Maria Santos"/></div>
            <div class="form-group"><label>Time Zone</label><select><option>Asia/Manila (UTC+8)</option><option>UTC</option></select></div>
            <div class="form-group"><label>Academic Year</label><select><option>2024–2025</option><option>2023–2024</option></select></div>
            <div class="form-group"><label>Grading Scale</label><select><option>Philippine DepEd (60–100)</option><option>Standard (0–100)</option></select></div>
          </div>
          <button class="btn btn-primary btn-sm">Save Settings</button>
        </div>
        <div class="card">
          <div class="card-title" style="color:#8B2020">Danger Zone</div>
          <div class="settings-row">
            <div><div style="font-size:13.5px;font-weight:500">Reset Grade Book</div><div style="font-size:12px;color:var(--gray-400);margin-top:2px">Clear all grade entries for the current period</div></div>
            <button class="btn btn-danger btn-sm">Reset</button>
          </div>
          <div class="settings-row" style="border:none">
            <div><div style="font-size:13.5px;font-weight:500">Log Out</div><div style="font-size:12px;color:var(--gray-400);margin-top:2px">Sign out of all devices</div></div>
            <button class="btn btn-danger btn-sm" onclick="doLogout()">Log Out</button>
          </div>
        </div>
      </div>

    </div>
  </main>
</div>

<!-- MODALS -->
<div class="modal-overlay" id="addStudentModal">
  <div class="modal">
    <div class="modal-title">Add Student</div>
    <div class="form-group"><label>Full Name</label><input type="text" id="newStudentName" placeholder="e.g. Ana Reyes"/></div>
    <div class="form-group"><label>Student ID</label><input type="text" id="newStudentId" placeholder="STU-2024-XXX"/></div>
    <div class="modal-actions">
      <button class="btn btn-outline btn-sm" onclick="closeModal('addStudentModal')">Cancel</button>
      <button class="btn btn-primary btn-sm" onclick="addStudent()">Add Student</button>
    </div>
  </div>
</div>
<div class="modal-overlay" id="editStudentModal">
  <div class="modal">
    <div class="modal-title">Edit Student</div>
    <div class="form-group"><label>Full Name</label><input type="text" id="editStudentName"/></div>
    <div class="form-group"><label>Student ID</label><input type="text" id="editStudentId" disabled style="background:var(--gray-50)"/></div>
    <div class="modal-actions">
      <button class="btn btn-danger btn-sm" onclick="removeStudent()">Remove</button>
      <div style="flex:1"></div>
      <button class="btn btn-outline btn-sm" onclick="closeModal('editStudentModal')">Cancel</button>
      <button class="btn btn-primary btn-sm" onclick="saveEditStudent()">Save</button>
    </div>
  </div>
</div>
<div class="modal-overlay" id="addClassModal">
  <div class="modal">
    <div class="modal-title">Add Class</div>
    <div class="form-group"><label>Subject Code</label><input type="text" placeholder="e.g. MATH 10"/></div>
    <div class="form-group"><label>Subject Name</label><input type="text" placeholder="e.g. Mathematics — Grade 10"/></div>
    <div class="form-group"><label>Section</label><input type="text" placeholder="e.g. Section Sampaguita"/></div>
    <div class="modal-actions">
      <button class="btn btn-outline btn-sm" onclick="closeModal('addClassModal')">Cancel</button>
      <button class="btn btn-primary btn-sm" onclick="closeModal('addClassModal')">Add Class</button>
    </div>
  </div>
</div>
<div class="modal-overlay" id="addTopicModal">
  <div class="modal">
    <div class="modal-title">Add Topic / Lesson</div>
    <div class="form-group"><label>Topic Title</label><input type="text" id="newTopicTitle" placeholder="e.g. Quadratic Equations"/></div>
    <div class="form-group"><label>Subject</label><select><option>Mathematics — Grade 10</option><option>Science — Grade 10</option><option>Pre-Calculus — Grade 11</option></select></div>
    <div class="form-group"><label>Week / Duration</label><input type="text" placeholder="e.g. Week 3–4"/></div>
    <div class="form-group"><label>Learning Objectives</label><textarea rows="3" placeholder="Students will be able to…"></textarea></div>
    <div class="modal-actions">
      <button class="btn btn-outline btn-sm" onclick="closeModal('addTopicModal')">Cancel</button>
      <button class="btn btn-primary btn-sm" onclick="addTopic()">Add Topic</button>
    </div>
  </div>
</div>

<script>
const COLORS=['#6B1A2A','#8B2A3F','#5C4A1A','#1A4A5C','#2A5C1A','#4A1A5C','#1A3A5C','#5C2A1A'];
let currentStudentIdx=-1;
let students=[
  {name:'Juan dela Cruz',id:'STU-2024-001'},
  {name:'Ana Reyes',id:'STU-2024-002'},
  {name:'Carlo Santos',id:'STU-2024-003'},
  {name:'Maria Garcia',id:'STU-2024-004'},
  {name:'Pedro Lim',id:'STU-2024-005'},
  {name:'Rosa Aquino',id:'STU-2024-006'},
  {name:'Jose Mendoza',id:'STU-2024-007'},
  {name:'Liza Cruz',id:'STU-2024-008'},
];
let gradeData={};
let attDates=['Jan 8','Jan 10','Jan 13','Jan 15','Jan 17'];
let attData={};
let quizCols=['QE1','QE2','QE3','QE4'];
let actCols=['RA1','RA2','RA3'];
let projCols=['P1','P2'];
let currTopics=[
  {title:'Patterns and Sequences',week:'Week 1–2'},
  {title:'Polynomials & Polynomial Equations',week:'Week 3–4'},
  {title:'Polynomial Functions',week:'Week 5–6'},
  {title:'Circles & Tangent Lines',week:'Week 7–8'},
  {title:'Plane Coordinate Geometry',week:'Week 9–10'},
];

function initials(name){return name.split(' ').map(w=>w[0]).join('').toUpperCase().slice(0,2);}
function color(idx){return COLORS[idx%COLORS.length];}
function avg(arr){return arr.length?arr.reduce((a,b)=>a+b,0)/arr.length:0;}
function rand(lo,hi){return Math.floor(Math.random()*(hi-lo+1))+lo;}

function initGradeData(){
  students.forEach(s=>{
    if(!gradeData[s.id]){
      gradeData[s.id]={
        att:rand(17,20),part:rand(78,98),
        qe:quizCols.map(()=>rand(72,98)),
        ra:actCols.map(()=>rand(74,98)),
        p:projCols.map(()=>rand(78,98)),
        exam:rand(72,98)
      };
    }
    if(!attData[s.id]){attData[s.id]={};attDates.forEach(d=>{attData[s.id][d]=Math.random()>0.12?'P':'A';});}
  });
}
function computeFinal(d){
  const qA=avg(d.qe||[]),raA=avg(d.ra||[]),pA=avg(d.p||[]);
  const cp=(d.part||0)*0.1+qA*0.25+raA*0.25+pA*0.4;
  const final=cp*0.7+(d.exam||0)*0.3;
  return{cp:+cp.toFixed(1),exam:d.exam||0,final:+final.toFixed(1)};
}

function navTo(screen,el){
  document.querySelectorAll('.screen').forEach(s=>s.classList.remove('active'));
  document.getElementById('screen-'+screen).classList.add('active');
  document.querySelectorAll('.nav-item').forEach(n=>n.classList.remove('active'));
  if(el)el.classList.add('active');
  const titles={dashboard:'Dashboard',profile:'Teacher Profile',classes:'Class Information',curriculum:'Course Curriculum',settings:'Settings',student:'Student Profile'};
  document.getElementById('topbarTitle').textContent=titles[screen]||'';
  if(screen==='curriculum')renderCurriculum();
}
function backToClasses(){document.getElementById('classesView').style.display='';document.getElementById('classDetailView').style.display='none';}
function backToClassDetail(){navTo('classes',document.querySelector('[data-screen=classes]'));setTimeout(()=>{document.getElementById('classesView').style.display='none';document.getElementById('classDetailView').style.display='block';},50);}

function openClassDetail(code,name){
  document.getElementById('classesView').style.display='none';
  document.getElementById('classDetailView').style.display='block';
  document.getElementById('classDetailName').textContent=name||code;
  initGradeData();
  renderStudents();
  renderGradeTable();
  renderAttendance();
  switchClassTab('students',document.querySelector('#classDetailTabs .tab'));
}
function switchClassTab(tab,el){
  ['students','grades','attendance'].forEach(t=>{document.getElementById('ctab-'+t).style.display='none';});
  document.getElementById('ctab-'+tab).style.display='block';
  document.querySelectorAll('#classDetailTabs .tab').forEach(t=>t.classList.remove('active'));
  if(el)el.classList.add('active');
}
function setView(v){
  if(v==='grid'){document.getElementById('studentGridView').style.display='grid';document.getElementById('studentListView').style.display='none';document.getElementById('gridViewBtn').classList.add('active');document.getElementById('listViewBtn').classList.remove('active');}
  else{document.getElementById('studentGridView').style.display='none';document.getElementById('studentListView').style.display='table';document.getElementById('gridViewBtn').classList.remove('active');document.getElementById('listViewBtn').classList.add('active');renderStudentList();}
}
function renderStudents(filter=''){
  const f=filter.toLowerCase();
  const list=students.filter(s=>!f||s.name.toLowerCase().includes(f)||s.id.toLowerCase().includes(f));
  document.getElementById('studentGridView').innerHTML=list.map((s,i)=>{
    const gi=students.indexOf(s);
    const ini=initials(s.name);const col=color(gi);
    return`<div class="student-card-grid" onclick="openStudentProfile(${gi})">
      <div class="student-avatar" style="background:${col}">${ini}</div>
      <div style="font-size:13px;font-weight:600;margin-bottom:2px">${s.name}</div>
      <div style="font-size:11px;color:var(--gray-400);margin-bottom:10px">${s.id}</div>
      <div style="display:flex;gap:4px;justify-content:center">
        <button class="btn btn-outline btn-sm" style="font-size:11px;padding:3px 8px" onclick="event.stopPropagation();openEditStudent(${gi})">Edit</button>
        <button class="btn btn-primary btn-sm" style="font-size:11px;padding:3px 8px" onclick="event.stopPropagation();openStudentProfile(${gi})">View</button>
      </div>
    </div>`;
  }).join('');
}
function renderStudentList(){
  document.getElementById('studentListBody').innerHTML=students.map((s,i)=>{
    const d=gradeData[s.id];const f=d?computeFinal(d):null;const col=color(i);const ini=initials(s.name);
    return`<tr>
      <td><div style="display:flex;align-items:center;gap:8px"><div style="width:28px;height:28px;border-radius:50%;background:${col};color:#E8C04A;font-size:10px;font-weight:700;display:flex;align-items:center;justify-content:center">${ini}</div>${s.name}</div></td>
      <td style="color:var(--gray-400)">${s.id}</td>
      <td><span class="badge badge-grade">${f?f.final:'—'}</span></td>
      <td><div style="display:flex;gap:6px"><button class="btn btn-outline btn-sm" onclick="openStudentProfile(${i})">View</button><button class="btn btn-outline btn-sm" onclick="openEditStudent(${i})">Edit</button></div></td>
    </tr>`;
  }).join('');
}
function openStudentProfile(idx){
  const s=students[idx];currentStudentIdx=idx;
  const d=gradeData[s.id];const f=d?computeFinal(d):{cp:'—',exam:'—',final:'—'};
  document.getElementById('spBreadcrumb').textContent=s.name;
  document.getElementById('spAvatar').textContent=initials(s.name);
  document.getElementById('spAvatar').style.background=color(idx);
  document.getElementById('spName').textContent=s.name;
  document.getElementById('spId').textContent=s.id;
  document.getElementById('spFinalGrade').textContent=f.final;
  document.getElementById('spClassPerf').textContent=f.cp;
  document.getElementById('spExamScore').textContent=f.exam;
  if(d){
    const qA=avg(d.qe||[]).toFixed(1),raA=avg(d.ra||[]).toFixed(1),pA=avg(d.p||[]).toFixed(1);
    const cp=f.cp;
    document.getElementById('spTableBody').innerHTML=`
      <tr><td>Attendance</td><td>${d.att}/20</td><td>—</td><td>—</td></tr>
      <tr><td>Class Participation</td><td>${d.part}</td><td>10%</td><td>${(d.part*0.1).toFixed(1)}</td></tr>
      <tr><td>Quizzes / Exercises</td><td>${qA} avg</td><td>25%</td><td>${(qA*0.25).toFixed(1)}</td></tr>
      <tr><td>Recitation / Activities</td><td>${raA} avg</td><td>25%</td><td>${(raA*0.25).toFixed(1)}</td></tr>
      <tr><td>Projects</td><td>${pA} avg</td><td>40%</td><td>${(pA*0.4).toFixed(1)}</td></tr>
      <tr style="background:var(--gold-pale)"><td><strong>Class Performance</strong></td><td colspan="2"><strong>× 70%</strong></td><td><strong>${cp}</strong></td></tr>
      <tr><td>Major Examination</td><td>${d.exam}</td><td>30%</td><td>${(d.exam*0.3).toFixed(1)}</td></tr>
      <tr style="background:var(--maroon-pale)"><td><strong style="color:var(--maroon)">FINAL GRADE</strong></td><td colspan="2"><strong style="color:var(--maroon)">Total</strong></td><td><strong style="color:var(--maroon)">${f.final}</strong></td></tr>`;
  }
  navTo('student',null);
}
function openEditStudent(idx){
  currentStudentIdx=idx;const s=students[idx];
  document.getElementById('editStudentName').value=s.name;
  document.getElementById('editStudentId').value=s.id;
  openModal('editStudentModal');
}
function saveEditStudent(){
  if(currentStudentIdx>=0){students[currentStudentIdx].name=document.getElementById('editStudentName').value;renderStudents();}
  closeModal('editStudentModal');
}
function removeStudent(){if(currentStudentIdx>=0){students.splice(currentStudentIdx,1);initGradeData();renderStudents();renderGradeTable();}closeModal('editStudentModal');}
function addStudent(){
  const name=document.getElementById('newStudentName').value.trim();
  const id=document.getElementById('newStudentId').value.trim()||`STU-2024-0${students.length+10}`;
  if(!name)return;
  students.push({name,id});initGradeData();renderStudents();renderGradeTable();
  document.getElementById('newStudentName').value='';document.getElementById('newStudentId').value='';
  closeModal('addStudentModal');
}

function addQuizColumn(){const n=prompt('Quiz name (e.g. QE5):');if(n&&!quizCols.includes(n)){quizCols.push(n);students.forEach(s=>{if(gradeData[s.id])gradeData[s.id].qe.push(rand(72,98));});renderGradeTable();}}
function addActivityColumn(){const n=prompt('Activity name (e.g. RA4):');if(n&&!actCols.includes(n)){actCols.push(n);students.forEach(s=>{if(gradeData[s.id])gradeData[s.id].ra.push(rand(74,98));});renderGradeTable();}}

function renderGradeTable(){
  const head=document.getElementById('gradeHead');
  const body=document.getElementById('gradeTableBody');
  head.innerHTML=`<tr>
    <th style="min-width:130px">Student</th>
    <th class="grade-cell-fixed">Att.</th>
    <th class="grade-cell-fixed">Part (10%)</th>
    ${quizCols.map(q=>`<th class="grade-cell-fixed" style="min-width:65px">${q}</th>`).join('')}
    ${actCols.map(r=>`<th class="grade-cell-fixed" style="min-width:65px">${r}</th>`).join('')}
    ${projCols.map(p=>`<th class="grade-cell-fixed" style="min-width:65px">${p}</th>`).join('')}
    <th class="grade-cell-computed" style="min-width:80px">Class Perf (70%)</th>
    <th class="grade-cell-fixed" style="min-width:75px">Major Exam</th>
    <th class="grade-cell-computed" style="min-width:80px">Exam (30%)</th>
    <th style="background:var(--maroon);color:var(--white);font-size:12px;text-align:center;min-width:90px">Final Grade</th>
  </tr>`;
  body.innerHTML=students.map((s,si)=>{
    const d=gradeData[s.id];if(!d)return'';
    const f=computeFinal(d);const col=color(si);const ini=initials(s.name);
    return`<tr>
      <td><div style="display:flex;align-items:center;gap:6px"><div style="width:22px;height:22px;border-radius:50%;background:${col};color:#E8C04A;font-size:9px;font-weight:700;display:flex;align-items:center;justify-content:center">${ini}</div>${s.name.split(' ')[0]}</div></td>
      <td style="text-align:center">${d.att}/20</td>
      <td><input type="number" min="0" max="100" value="${d.part}" style="width:60px;text-align:center;padding:4px;border:1.5px solid #FFCCCC;border-radius:6px;background:#FFF0F0;font-size:12px" onchange="gradeData['${s.id}'].part=+this.value;recompute('${s.id}')"/></td>
      ${d.qe.map((q,i)=>`<td><input type="number" min="0" max="100" value="${q}" style="width:58px;text-align:center;padding:4px;border:1.5px solid #FFCCCC;border-radius:6px;background:#FFF0F0;font-size:12px" onchange="gradeData['${s.id}'].qe[${i}]=+this.value;recompute('${s.id}')"/></td>`).join('')}
      ${d.ra.map((r,i)=>`<td><input type="number" min="0" max="100" value="${r}" style="width:58px;text-align:center;padding:4px;border:1.5px solid #FFCCCC;border-radius:6px;background:#FFF0F0;font-size:12px" onchange="gradeData['${s.id}'].ra[${i}]=+this.value;recompute('${s.id}')"/></td>`).join('')}
      ${d.p.map((p,i)=>`<td><input type="number" min="0" max="100" value="${p}" style="width:58px;text-align:center;padding:4px;border:1.5px solid #FFCCCC;border-radius:6px;background:#FFF0F0;font-size:12px" onchange="gradeData['${s.id}'].p[${i}]=+this.value;recompute('${s.id}')"/></td>`).join('')}
      <td class="grade-cell-computed" id="cp-${s.id}">${f.cp}</td>
      <td><input type="number" min="0" max="100" value="${d.exam}" style="width:62px;text-align:center;padding:4px;border:1.5px solid #FFCCCC;border-radius:6px;background:#FFF0F0;font-size:12px" onchange="gradeData['${s.id}'].exam=+this.value;recompute('${s.id}')"/></td>
      <td class="grade-cell-computed" id="eg-${s.id}">${(d.exam*0.3).toFixed(1)}</td>
      <td style="text-align:center"><span style="background:var(--maroon);color:var(--white);font-weight:800;font-size:13px;padding:4px 10px;border-radius:6px;display:inline-block" id="fg-${s.id}">${f.final}</span></td>
    </tr>`;
  }).join('');
}
function recompute(sid){
  const d=gradeData[sid];if(!d)return;
  const f=computeFinal(d);
  const cp=document.getElementById('cp-'+sid);const eg=document.getElementById('eg-'+sid);const fg=document.getElementById('fg-'+sid);
  if(cp)cp.textContent=f.cp;if(eg)eg.textContent=(d.exam*0.3).toFixed(1);if(fg)fg.textContent=f.final;
}
function computeAllGrades(){students.forEach(s=>recompute(s.id));}

function renderAttendance(){
  document.getElementById('attendanceHead').innerHTML=`<tr><th>Student</th>${attDates.map(d=>`<th style="text-align:center;min-width:70px">${d}</th>`).join('')}<th style="text-align:center">Total</th></tr>`;
  document.getElementById('attendanceBody').innerHTML=students.map((s,si)=>{
    const col=color(si);const ini=initials(s.name);
    const pres=attData[s.id]?Object.values(attData[s.id]).filter(v=>v==='P').length:0;
    return`<tr><td><div style="display:flex;align-items:center;gap:6px"><div style="width:22px;height:22px;border-radius:50%;background:${col};color:#E8C04A;font-size:9px;font-weight:700;display:flex;align-items:center;justify-content:center">${ini}</div>${s.name.split(' ')[0]}</div></td>
    ${attDates.map(d=>{const v=attData[s.id]?attData[s.id][d]:'—';return`<td style="text-align:center;cursor:pointer" onclick="toggleAtt('${s.id}','${d}',this)"><span class="badge ${v==='P'?'badge-present':'badge-absent'}">${v}</span></td>`}).join('')}
    <td style="text-align:center;font-weight:700">${pres}/${attDates.length}</td></tr>`;
  }).join('');
}
function toggleAtt(sid,date,td){
  if(!attData[sid])attData[sid]={};
  attData[sid][date]=attData[sid][date]==='P'?'A':'P';
  const v=attData[sid][date];
  td.innerHTML=`<span class="badge ${v==='P'?'badge-present':'badge-absent'}">${v}</span>`;
  renderAttendance();
}
function addAttendanceDate(){
  const d=prompt('Enter date label (e.g. Jan 20):');
  if(d&&!attDates.includes(d)){
    attDates.push(d);
    students.forEach(s=>{if(!attData[s.id])attData[s.id]={};attData[s.id][d]='P';});
    renderAttendance();
  }
}

function toggleProfileEdit(){
  const editing=document.getElementById('profileEditForm').style.display!=='none';
  if(editing){cancelProfileEdit();}else{
    document.getElementById('profileView').style.display='none';
    document.getElementById('profileEditForm').style.display='grid';
    document.getElementById('profileSaveRow').style.display='block';
    document.getElementById('profileEditBtn').textContent='Cancel';
  }
}
function saveProfile(){
  document.getElementById('vName').textContent=document.getElementById('eName').value;
  document.getElementById('vEmail').textContent=document.getElementById('eEmail').value;
  document.getElementById('vDept').textContent=document.getElementById('eDept').value;
  cancelProfileEdit();
}
function cancelProfileEdit(){
  document.getElementById('profileView').style.display='grid';
  document.getElementById('profileEditForm').style.display='none';
  document.getElementById('profileSaveRow').style.display='none';
  document.getElementById('profileEditBtn').textContent='Edit Profile';
}

function renderCurriculum(){
  const subjects=['Mathematics — Grade 10','Science — Grade 10'];
  document.getElementById('curriculumGrid').innerHTML=subjects.map(subj=>`
    <div class="card">
      <div class="card-title">${subj}</div>
      ${currTopics.map((t,i)=>`
        <div class="curriculum-item">
          <div class="ci-num">${i+1}</div>
          <div style="flex:1"><div style="font-size:13.5px;font-weight:500">${t.title}</div><div style="font-size:11px;color:var(--gray-400)">${t.week}</div></div>
          <div style="display:flex;gap:6px">
            <button class="btn btn-outline btn-sm" style="font-size:11px;padding:3px 8px" onclick="editTopic(${i})">Edit</button>
            <button class="btn btn-danger btn-sm" style="font-size:11px;padding:3px 8px" onclick="removeTopic(${i})">✕</button>
          </div>
        </div>`).join('')}
    </div>`).join('');
}
function addTopic(){const t=document.getElementById('newTopicTitle').value.trim();if(!t)return;currTopics.push({title:t,week:'Upcoming'});renderCurriculum();closeModal('addTopicModal');document.getElementById('newTopicTitle').value='';}
function editTopic(i){const t=prompt('Edit topic:',currTopics[i].title);if(t){currTopics[i].title=t;renderCurriculum();}}
function removeTopic(i){if(confirm('Remove this topic?')){currTopics.splice(i,1);renderCurriculum();}}

function openModal(id){document.getElementById(id).style.display='flex';}
function closeModal(id){document.getElementById(id).style.display='none';}
document.querySelectorAll('.modal-overlay').forEach(m=>m.addEventListener('click',function(e){if(e.target===this)this.style.display='none';}));

function switchLoginTab(tab){
  document.querySelectorAll('.login-tab').forEach((t,i)=>{t.classList.toggle('active',i===(tab==='login'?0:1));});
  document.getElementById('loginForm').style.display=tab==='login'?'block':'none';
  document.getElementById('registerForm').style.display=tab==='register'?'block':'none';
}
function doLogin(){
  document.getElementById('loginScreen').style.display='none';
  document.getElementById('mainApp').style.display='flex';
  initGradeData();renderStudents();
}
function doLogout(){
  document.getElementById('mainApp').style.display='none';
  document.getElementById('loginScreen').style.display='flex';
}

initGradeData();
renderCurriculum();
</script>
</body>
</html>
