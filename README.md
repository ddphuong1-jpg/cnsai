<!DOCTYPE html>
<html lang="vi">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Portfolio | Đào Dương Nam Phương</title>
<link rel="preconnect" href="https://fonts.googleapis.com"/>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;700;900&family=Rajdhani:wght@300;400;500;600;700&family=Share+Tech+Mono&display=swap" rel="stylesheet"/>
<style>
/* ============================================================
   CSS VARIABLES & RESET
============================================================ */
:root {
  --bg-primary: #040d14;
  --bg-secondary: #071624;
  --bg-card: #0a1e30;
  --bg-card2: #081828;
  --cyan: #00d4ff;
  --cyan-dim: rgba(0,212,255,0.15);
  --cyan-glow: rgba(0,212,255,0.4);
  --green: #00ff88;
  --green-dim: rgba(0,255,136,0.12);
  --orange: #ff6b35;
  --orange-dim: rgba(255,107,53,0.15);
  --text-primary: #e0f4ff;
  --text-secondary: #7fb3cc;
  --text-muted: #3d6b7a;
  --border: rgba(0,212,255,0.18);
  --border-bright: rgba(0,212,255,0.45);
  --font-display: 'Orbitron', monospace;
  --font-body: 'Rajdhani', sans-serif;
  --font-mono: 'Share Tech Mono', monospace;
  --transition: 0.35s cubic-bezier(0.4,0,0.2,1);
}

*, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
html { scroll-behavior: smooth; font-size: 16px; }
body {
  font-family: var(--font-body);
  background: var(--bg-primary);
  color: var(--text-primary);
  overflow-x: hidden;
  min-height: 100vh;
}

/* SCROLLBAR */
::-webkit-scrollbar { width: 5px; }
::-webkit-scrollbar-track { background: var(--bg-primary); }
::-webkit-scrollbar-thumb { background: var(--cyan); border-radius: 2px; }

/* SELECTION */
::selection { background: var(--cyan-dim); color: var(--cyan); }

/* ============================================================
   ANIMATED BACKGROUND
============================================================ */
.grid-bg {
  position: fixed; inset: 0; z-index: 0;
  background-image:
    linear-gradient(rgba(0,212,255,0.03) 1px, transparent 1px),
    linear-gradient(90deg, rgba(0,212,255,0.03) 1px, transparent 1px);
  background-size: 50px 50px;
  pointer-events: none;
}
.grid-bg::after {
  content: '';
  position: absolute; inset: 0;
  background: radial-gradient(ellipse at 20% 50%, rgba(0,212,255,0.04) 0%, transparent 60%),
              radial-gradient(ellipse at 80% 20%, rgba(0,255,136,0.03) 0%, transparent 50%);
}

/* Animated scan line */
.scan-line {
  position: fixed; left: 0; right: 0; height: 2px;
  background: linear-gradient(90deg, transparent, var(--cyan), transparent);
  opacity: 0.3; z-index: 1; pointer-events: none;
  animation: scanLine 6s linear infinite;
}
@keyframes scanLine {
  0% { top: -2px; }
  100% { top: 100vh; }
}

/* ============================================================
   NAVIGATION
============================================================ */
nav {
  position: fixed; top: 0; left: 0; right: 0; z-index: 500;
  height: 64px;
  display: flex; align-items: center; justify-content: space-between;
  padding: 0 clamp(1rem, 5vw, 3.5rem);
  background: rgba(4,13,20,0.92);
  backdrop-filter: blur(20px);
  border-bottom: 1px solid var(--border);
}
nav::after {
  content: '';
  position: absolute; bottom: 0; left: 0; right: 0; height: 1px;
  background: linear-gradient(90deg, transparent, var(--cyan), transparent);
  opacity: 0.5;
}

.nav-logo {
  display: flex; align-items: center; gap: 10px;
  font-family: var(--font-display);
  font-size: 0.85rem; font-weight: 700;
  color: var(--cyan); letter-spacing: 0.1em;
  text-decoration: none;
}
.nav-logo .logo-bracket {
  color: var(--green); font-size: 1.2rem;
}
.logo-dot {
  width: 6px; height: 6px; border-radius: 50%;
  background: var(--green);
  animation: pulse 2s infinite;
}
@keyframes pulse {
  0%,100% { opacity:1; transform:scale(1); }
  50% { opacity:0.4; transform:scale(1.5); }
}

.nav-links {
  display: flex; gap: 0; list-style: none;
}
.nav-links a {
  display: flex; align-items: center; gap: 6px;
  padding: 0 1.2rem; height: 64px;
  font-family: var(--font-display); font-size: 0.62rem;
  font-weight: 600; letter-spacing: 0.12em;
  text-transform: uppercase; text-decoration: none;
  color: var(--text-secondary);
  border-right: 1px solid var(--border);
  transition: all var(--transition);
  position: relative;
  overflow: hidden;
}
.nav-links a:first-child { border-left: 1px solid var(--border); }
.nav-links a::before {
  content: '';
  position: absolute; bottom: 0; left: 0; right: 0; height: 2px;
  background: var(--cyan);
  transform: scaleX(0); transform-origin: center;
  transition: transform var(--transition);
}
.nav-links a:hover, .nav-links a.active {
  color: var(--cyan);
  background: var(--cyan-dim);
}
.nav-links a:hover::before, .nav-links a.active::before { transform: scaleX(1); }
.nav-num {
  font-family: var(--font-mono); font-size: 0.55rem;
  color: var(--cyan); opacity: 0.6;
}

.hamburger {
  display: none; flex-direction: column; gap: 5px;
  background: none; border: 1px solid var(--border);
  padding: 8px; cursor: pointer;
}
.hamburger span {
  display: block; width: 20px; height: 1.5px;
  background: var(--cyan); transition: all 0.3s;
}

/* ============================================================
   PAGE SYSTEM
============================================================ */
.page {
  display: none; opacity: 0;
  min-height: 100vh;
  padding-top: 64px;
  position: relative; z-index: 10;
  transition: opacity 0.5s ease;
}
.page.active {
  display: block; opacity: 1;
  animation: pageEnter 0.6s ease forwards;
}
@keyframes pageEnter {
  from { opacity: 0; transform: translateY(16px); }
  to { opacity: 1; transform: translateY(0); }
}

/* ============================================================
   SHARED COMPONENTS
============================================================ */
.section-wrapper {
  max-width: 1200px; margin: 0 auto;
  padding: clamp(3rem,8vh,6rem) clamp(1.2rem,5vw,3.5rem);
}

.badge {
  display: inline-flex; align-items: center; gap: 6px;
  font-family: var(--font-mono); font-size: 0.7rem;
  color: var(--cyan); letter-spacing: 0.15em;
  text-transform: uppercase;
  padding: 0.35rem 1rem;
  border: 1px solid var(--border-bright);
  background: var(--cyan-dim);
  margin-bottom: 1.5rem;
}
.badge::before { content: '//'; color: var(--green); margin-right: 4px; }

.section-title {
  font-family: var(--font-display);
  font-size: clamp(1.8rem, 4vw, 3rem);
  font-weight: 900;
  line-height: 1.1;
  margin-bottom: 1rem;
  letter-spacing: -0.02em;
}
.section-title .accent { color: var(--cyan); }
.section-title .accent2 { color: var(--green); }

.card {
  background: var(--bg-card);
  border: 1px solid var(--border);
  padding: 2rem;
  position: relative;
  transition: all var(--transition);
  overflow: hidden;
}
.card::before {
  content: '';
  position: absolute; top: 0; left: 0;
  width: 2px; height: 0;
  background: linear-gradient(180deg, var(--cyan), var(--green));
  transition: height 0.4s ease;
}
.card:hover { border-color: var(--border-bright); background: #0d2035; }
.card:hover::before { height: 100%; }

.card-corner {
  position: absolute; width: 12px; height: 12px;
  border-color: var(--cyan); border-style: solid;
  opacity: 0.4;
}
.card-corner.tl { top: 0; left: 0; border-width: 1px 0 0 1px; }
.card-corner.tr { top: 0; right: 0; border-width: 1px 1px 0 0; }
.card-corner.bl { bottom: 0; left: 0; border-width: 0 0 1px 1px; }
.card-corner.br { bottom: 0; right: 0; border-width: 0 1px 1px 0; }

.tag {
  display: inline-block;
  font-family: var(--font-mono); font-size: 0.65rem;
  color: var(--green); letter-spacing: 0.1em;
  padding: 0.2rem 0.6rem;
  border: 1px solid var(--green-dim);
  background: var(--green-dim);
  margin: 0.2rem;
}

.mono-text {
  font-family: var(--font-mono);
  color: var(--cyan); font-size: 0.8rem;
}

.glitch-line {
  height: 1px;
  background: linear-gradient(90deg, transparent, var(--cyan), var(--green), transparent);
  margin: 2.5rem 0; opacity: 0.3;
}

/* ============================================================
   PAGE 1 — HOME / ABOUT
============================================================ */

/* HERO */
.hero {
  min-height: calc(100vh - 64px);
  display: grid; grid-template-columns: 1.1fr 0.9fr;
  align-items: center; gap: 4rem;
  max-width: 1200px; margin: 0 auto;
  padding: clamp(2rem,6vh,4rem) clamp(1.2rem,5vw,3.5rem);
}

.hero-status {
  display: flex; align-items: center; gap: 8px;
  font-family: var(--font-mono); font-size: 0.72rem;
  color: var(--green); margin-bottom: 1.5rem;
  letter-spacing: 0.12em;
}
.status-dot {
  width: 8px; height: 8px; border-radius: 50%;
  background: var(--green);
  box-shadow: 0 0 8px var(--green);
  animation: pulse 2s infinite;
}

.hero-name {
  font-family: var(--font-display);
  font-size: clamp(2.2rem, 5vw, 4.2rem);
  font-weight: 900; line-height: 1.05;
  letter-spacing: -0.01em;
  margin-bottom: 0.3rem;
}
.hero-name .line1 { color: var(--text-primary); }
.hero-name .line2 { color: var(--cyan); text-shadow: 0 0 30px var(--cyan-glow); }
.hero-name .line3 {
  color: var(--green);
  text-shadow: 0 0 20px rgba(0,255,136,0.4);
  font-size: 0.75em;
}

.hero-sub {
  font-family: var(--font-mono); font-size: 0.82rem;
  color: var(--text-secondary); letter-spacing: 0.08em;
  margin: 1.2rem 0;
  padding: 0.6rem 1rem;
  border-left: 2px solid var(--cyan);
  background: var(--cyan-dim);
}

.hero-desc {
  color: var(--text-secondary);
  font-size: 1.05rem; line-height: 1.75;
  margin-bottom: 2rem;
}
.hero-desc strong { color: var(--text-primary); font-weight: 600; }

.hero-btns {
  display: flex; gap: 1rem; flex-wrap: wrap;
  margin-bottom: 2.5rem;
}
.btn {
  display: inline-flex; align-items: center; gap: 8px;
  padding: 0.75rem 1.8rem;
  font-family: var(--font-display); font-size: 0.65rem;
  font-weight: 600; letter-spacing: 0.15em;
  text-transform: uppercase; text-decoration: none;
  border: none; cursor: pointer;
  transition: all var(--transition);
}
.btn-primary {
  background: var(--cyan); color: var(--bg-primary);
  clip-path: polygon(8px 0%, 100% 0%, calc(100% - 8px) 100%, 0% 100%);
}
.btn-primary:hover {
  background: var(--green);
  box-shadow: 0 0 24px rgba(0,255,136,0.4);
  transform: translateY(-2px);
}
.btn-ghost {
  background: transparent; color: var(--cyan);
  border: 1px solid var(--border-bright);
}
.btn-ghost:hover {
  background: var(--cyan-dim);
  box-shadow: 0 0 16px var(--cyan-glow);
  transform: translateY(-2px);
}

.hero-metrics {
  display: grid; grid-template-columns: repeat(4, 1fr);
  gap: 1px; border: 1px solid var(--border);
  background: var(--border);
}
.metric-box {
  background: var(--bg-card);
  padding: 1rem 0.8rem; text-align: center;
  transition: background var(--transition);
}
.metric-box:hover { background: var(--bg-secondary); }
.metric-val {
  font-family: var(--font-display); font-size: 1.5rem;
  font-weight: 700; color: var(--cyan);
  text-shadow: 0 0 12px var(--cyan-glow);
  display: block;
}
.metric-lab {
  font-family: var(--font-mono); font-size: 0.58rem;
  color: var(--text-muted); letter-spacing: 0.1em;
  text-transform: uppercase; display: block;
  margin-top: 0.25rem;
}

/* HERO VISUAL */
.hero-visual { position: relative; }

.terminal-window {
  background: var(--bg-secondary);
  border: 1px solid var(--border);
  position: relative;
  box-shadow: 0 0 40px rgba(0,212,255,0.08);
}
.terminal-bar {
  display: flex; align-items: center; gap: 6px;
  padding: 0.6rem 1rem;
  background: rgba(0,212,255,0.06);
  border-bottom: 1px solid var(--border);
}
.t-dot {
  width: 10px; height: 10px; border-radius: 50%;
}
.t-dot.r { background: #ff5f57; }
.t-dot.y { background: #febc2e; }
.t-dot.g { background: #28c840; }
.t-title {
  font-family: var(--font-mono); font-size: 0.68rem;
  color: var(--text-muted); margin-left: 8px;
}
.terminal-body { padding: 1.5rem; }
.t-line {
  font-family: var(--font-mono); font-size: 0.78rem;
  line-height: 1.9; white-space: nowrap;
}
.t-prompt { color: var(--green); }
.t-cmd { color: var(--text-primary); }
.t-out { color: var(--cyan); }
.t-out2 { color: var(--text-secondary); }
.t-warn { color: var(--orange); }
.t-cursor {
  display: inline-block; width: 8px; height: 14px;
  background: var(--cyan); vertical-align: middle;
  animation: blink 1s step-end infinite;
}
@keyframes blink { 0%,100% {opacity:1;} 50% {opacity:0;} }

.profile-ring {
  width: 90px; height: 90px; border-radius: 50%;
  border: 2px solid var(--cyan);
  display: flex; align-items: center; justify-content: center;
  font-family: var(--font-display); font-size: 1.8rem; font-weight: 700;
  color: var(--cyan);
  background: var(--cyan-dim);
  box-shadow: 0 0 20px var(--cyan-glow), inset 0 0 20px rgba(0,212,255,0.1);
  margin: 1.5rem auto 0;
  position: relative;
}
.profile-ring::before {
  content: '';
  position: absolute; inset: -6px; border-radius: 50%;
  border: 1px dashed rgba(0,212,255,0.3);
  animation: spin 12s linear infinite;
}
@keyframes spin { to { transform: rotate(360deg); } }

/* ABOUT DETAILS */
.about-grid {
  display: grid; grid-template-columns: 3fr 2fr;
  gap: 2.5rem; margin-top: 3rem;
}

.info-item {
  display: flex; align-items: flex-start; gap: 1rem;
  padding: 1rem 1.2rem;
  border: 1px solid var(--border);
  background: var(--bg-card2);
  margin-bottom: 0.8rem;
  transition: all var(--transition);
}
.info-item:hover { border-color: var(--cyan); background: var(--bg-card); }
.info-icon {
  width: 36px; height: 36px; flex-shrink: 0;
  display: flex; align-items: center; justify-content: center;
  font-size: 1.1rem;
  border: 1px solid var(--border);
  background: var(--cyan-dim);
  color: var(--cyan);
}
.info-label {
  font-family: var(--font-mono); font-size: 0.65rem;
  color: var(--text-muted); letter-spacing: 0.1em;
  text-transform: uppercase; display: block; margin-bottom: 0.2rem;
}
.info-value {
  font-size: 0.92rem; color: var(--text-primary); font-weight: 500;
}

.skill-bar-item { margin-bottom: 1.2rem; }
.skill-bar-head {
  display: flex; justify-content: space-between; align-items: center;
  margin-bottom: 0.4rem;
}
.skill-name {
  font-family: var(--font-mono); font-size: 0.72rem;
  color: var(--text-secondary); letter-spacing: 0.08em;
}
.skill-pct {
  font-family: var(--font-mono); font-size: 0.7rem;
  color: var(--cyan);
}
.skill-track {
  height: 3px; background: var(--border);
  position: relative; overflow: hidden;
}
.skill-fill {
  height: 100%;
  background: linear-gradient(90deg, var(--cyan), var(--green));
  box-shadow: 0 0 6px var(--cyan-glow);
  width: 0; transition: width 1.2s cubic-bezier(0.4,0,0.2,1);
}

/* GOALS */
.goal-item {
  display: flex; gap: 1.2rem; align-items: flex-start;
  padding: 1.2rem;
  border: 1px solid var(--border);
  background: var(--bg-card2);
  margin-bottom: 0.8rem;
  transition: all var(--transition);
}
.goal-item:hover { border-color: var(--cyan); }
.goal-num {
  font-family: var(--font-display); font-size: 1.8rem;
  font-weight: 900; color: var(--cyan); opacity: 0.2;
  line-height: 1; flex-shrink: 0;
  min-width: 40px;
}
.goal-title {
  font-family: var(--font-display); font-size: 0.7rem;
  font-weight: 700; color: var(--cyan); letter-spacing: 0.1em;
  margin-bottom: 0.4rem;
}
.goal-text { font-size: 0.9rem; color: var(--text-secondary); line-height: 1.7; }
.goal-text strong { color: var(--text-primary); }

/* PORTFOLIO PURPOSE */
.purpose-grid {
  display: grid; grid-template-columns: repeat(3, 1fr);
  gap: 1px; background: var(--border);
  margin-top: 2rem;
}
.purpose-item {
  background: var(--bg-card2);
  padding: 1.8rem 1.5rem;
  text-align: center;
  transition: background var(--transition);
  position: relative;
}
.purpose-item:hover { background: var(--bg-card); }
.purpose-num {
  font-family: var(--font-display); font-size: 2.5rem;
  font-weight: 900; color: var(--cyan); opacity: 0.15;
  line-height: 1; margin-bottom: 1rem;
}
.purpose-icon { font-size: 1.8rem; margin-bottom: 0.8rem; display: block; }
.purpose-title {
  font-family: var(--font-display); font-size: 0.68rem;
  font-weight: 700; color: var(--cyan); letter-spacing: 0.1em;
  margin-bottom: 0.6rem;
}
.purpose-text { font-size: 0.82rem; color: var(--text-secondary); line-height: 1.7; }

/* ============================================================
   PAGE 2 — PROJECTS
============================================================ */
.ex-hero {
  padding: clamp(3rem,6vh,5rem) clamp(1.2rem,5vw,3.5rem) 0;
  max-width: 1200px; margin: 0 auto;
}

.ex-grid {
  display: grid; grid-template-columns: repeat(auto-fill, minmax(min(100%, 540px), 1fr));
  gap: 1px; background: var(--border);
  margin: 2rem 0;
  max-width: 1200px; margin-left: auto; margin-right: auto;
}

.ex-card {
  background: var(--bg-card2);
  padding: 0;
  cursor: pointer;
  transition: all var(--transition);
  position: relative;
  overflow: hidden;
}
.ex-card:hover { background: var(--bg-card); }
.ex-card::before {
  content: '';
  position: absolute; top: 0; left: 0; bottom: 0; width: 0;
  background: linear-gradient(180deg, var(--cyan-dim), transparent);
  transition: width 0.4s ease;
}
.ex-card:hover::before { width: 3px; }

.ex-card-header {
  display: flex; align-items: flex-start; justify-content: space-between;
  padding: 1.8rem 2rem 1.2rem;
  border-bottom: 1px solid var(--border);
}
.ex-num {
  font-family: var(--font-display); font-size: 2.8rem;
  font-weight: 900; color: var(--cyan); opacity: 0.12;
  line-height: 1;
}
.ex-badge-wrap { text-align: right; }
.ex-module {
  font-family: var(--font-mono); font-size: 0.6rem;
  color: var(--orange); letter-spacing: 0.12em; text-transform: uppercase;
  display: block; margin-bottom: 0.3rem;
}
.ex-status {
  display: inline-flex; align-items: center; gap: 5px;
  font-family: var(--font-mono); font-size: 0.6rem;
  color: var(--green); letter-spacing: 0.1em;
}
.ex-status::before {
  content: ''; width: 5px; height: 5px; border-radius: 50%;
  background: var(--green);
  box-shadow: 0 0 6px var(--green);
}

.ex-card-body { padding: 1.2rem 2rem 2rem; }
.ex-title {
  font-family: var(--font-display); font-size: 0.9rem;
  font-weight: 700; color: var(--text-primary);
  line-height: 1.35; margin-bottom: 0.8rem;
  letter-spacing: 0.02em;
}
.ex-desc { font-size: 0.88rem; color: var(--text-secondary); line-height: 1.75; margin-bottom: 1rem; }

/* Expandable panel */
.ex-expand-btn {
  display: flex; align-items: center; gap: 8px;
  font-family: var(--font-mono); font-size: 0.65rem;
  color: var(--cyan); letter-spacing: 0.1em;
  background: none; border: 1px solid var(--border);
  padding: 0.5rem 1rem; cursor: pointer;
  transition: all var(--transition);
  width: 100%; margin-top: 1rem;
}
.ex-expand-btn:hover { border-color: var(--cyan); background: var(--cyan-dim); }
.ex-expand-btn .arrow { transition: transform 0.3s; }
.ex-expand-btn.open .arrow { transform: rotate(90deg); }

.ex-panel {
  max-height: 0; overflow: hidden;
  transition: max-height 0.5s ease, padding 0.3s ease;
  border-top: 1px solid transparent;
  background: rgba(0,212,255,0.02);
}
.ex-panel.open {
  max-height: 1500px;
  border-top-color: var(--border);
  padding: 1.5rem 2rem;
}

.process-list { list-style: none; margin-bottom: 1.2rem; }
.process-list li {
  display: flex; gap: 0.8rem; align-items: flex-start;
  font-size: 0.85rem; color: var(--text-secondary);
  padding: 0.55rem 0; border-bottom: 1px solid rgba(0,212,255,0.05);
  line-height: 1.65;
}
.process-list li:last-child { border-bottom: none; }
.ps-num {
  font-family: var(--font-mono); font-size: 0.65rem;
  color: var(--cyan); flex-shrink: 0; margin-top: 2px;
  min-width: 28px;
}

.result-box {
  padding: 1rem 1.2rem;
  border-left: 2px solid var(--green);
  background: var(--green-dim);
  font-size: 0.84rem; color: var(--text-secondary);
  line-height: 1.7;
}
.result-box strong { color: var(--green); }

.compare-table {
  width: 100%; border-collapse: collapse;
  font-size: 0.78rem; margin: 0.8rem 0;
}
.compare-table th {
  background: rgba(0,212,255,0.12);
  color: var(--cyan); font-family: var(--font-mono);
  font-size: 0.65rem; letter-spacing: 0.1em; padding: 0.6rem 0.8rem;
  text-align: left;
}
.compare-table td {
  padding: 0.55rem 0.8rem;
  border-bottom: 1px solid var(--border);
  color: var(--text-secondary); vertical-align: top;
}
.compare-table tr:nth-child(even) td { background: rgba(0,212,255,0.02); }
.compare-table td.good { color: var(--green); font-weight: 600; }
.compare-table td.warn { color: var(--orange); font-weight: 600; }
.compare-table td.bad { color: #ff4444; font-weight: 600; }

.ethics-grid {
  display: grid; grid-template-columns: 1fr 1fr;
  gap: 0.6rem;
}
.ethics-item {
  padding: 0.8rem;
  border: 1px solid var(--border);
  background: var(--bg-card);
  font-size: 0.8rem;
}
.ethics-item-title {
  font-family: var(--font-mono); font-size: 0.62rem;
  color: var(--cyan); letter-spacing: 0.1em;
  margin-bottom: 0.35rem;
}
.ethics-item p { color: var(--text-secondary); line-height: 1.65; }

/* ============================================================
   PAGE 3 — REFLECTION
============================================================ */
.refl-header {
  padding: clamp(3rem,6vh,5rem) clamp(1.2rem,5vw,3.5rem) 0;
  max-width: 1200px; margin: 0 auto;
}

.exp-block {
  padding: 2.5rem 2rem;
  border: 1px solid var(--border);
  background: var(--bg-card2);
  margin-bottom: 1.5rem;
  position: relative;
  overflow: hidden;
  transition: all var(--transition);
}
.exp-block:hover { border-color: var(--border-bright); background: var(--bg-card); }
.exp-block::after {
  content: attr(data-num);
  position: absolute; right: 1.5rem; top: 1.5rem;
  font-family: var(--font-display); font-size: 4rem;
  font-weight: 900; color: var(--cyan); opacity: 0.05;
  line-height: 1; pointer-events: none;
}

.exp-label {
  font-family: var(--font-display); font-size: 0.65rem;
  font-weight: 700; color: var(--cyan); letter-spacing: 0.15em;
  text-transform: uppercase; margin-bottom: 0.8rem;
  display: flex; align-items: center; gap: 8px;
}
.exp-label::before {
  content: ''; width: 20px; height: 1px;
  background: var(--cyan); flex-shrink: 0;
}
.exp-title {
  font-family: var(--font-display); font-size: 1.1rem;
  font-weight: 700; color: var(--text-primary);
  margin-bottom: 1rem; line-height: 1.3;
}
.exp-text { font-size: 0.95rem; color: var(--text-secondary); line-height: 1.8; }
.exp-text strong { color: var(--text-primary); font-weight: 600; }

.lesson-grid {
  display: grid; grid-template-columns: repeat(2, 1fr);
  gap: 1px; background: var(--border);
}
.lesson-item {
  background: var(--bg-card2);
  padding: 1.8rem;
  transition: background var(--transition);
  position: relative; overflow: hidden;
}
.lesson-item:hover { background: var(--bg-card); }
.lesson-num {
  font-family: var(--font-display); font-size: 3rem;
  font-weight: 900; color: var(--cyan); opacity: 0.12;
  line-height: 1; margin-bottom: 0.5rem;
}
.lesson-title {
  font-family: var(--font-display); font-size: 0.75rem;
  font-weight: 700; color: var(--cyan); letter-spacing: 0.08em;
  margin-bottom: 0.6rem;
}
.lesson-text { font-size: 0.88rem; color: var(--text-secondary); line-height: 1.7; }
.lesson-text strong { color: var(--text-primary); }

.challenge-item {
  display: flex; gap: 1.5rem;
  padding: 1.2rem;
  border: 1px solid var(--border);
  background: var(--bg-card2);
  margin-bottom: 0.8rem;
  transition: all var(--transition);
}
.challenge-item:hover { border-color: var(--orange); background: var(--bg-card); }
.challenge-label {
  flex: 0 0 200px;
  font-family: var(--font-mono); font-size: 0.72rem;
  color: var(--orange); letter-spacing: 0.06em;
  display: flex; align-items: center;
}
.challenge-sol { font-size: 0.88rem; color: var(--text-secondary); line-height: 1.7; }
.challenge-sol strong { color: var(--text-primary); }

.quote-block {
  text-align: center;
  padding: 4rem 2rem;
  border: 1px solid var(--border);
  background: var(--bg-card2);
  position: relative;
  overflow: hidden;
  margin-top: 3rem;
}
.quote-block::before {
  content: '"';
  position: absolute; left: -20px; top: -40px;
  font-family: var(--font-display); font-size: 20rem;
  color: var(--cyan); opacity: 0.025;
  line-height: 1;
}
.quote-text {
  font-family: var(--font-display); font-size: clamp(1rem,2vw,1.3rem);
  font-weight: 400; color: var(--text-primary);
  line-height: 1.65; max-width: 70ch; margin: 0 auto;
  letter-spacing: 0.02em;
}
.quote-text em { color: var(--cyan); font-style: normal; }
.quote-author {
  font-family: var(--font-mono); font-size: 0.72rem;
  color: var(--green); margin-top: 1.5rem;
  letter-spacing: 0.15em;
}

/* FOOTER */
footer {
  position: relative; z-index: 10;
  background: rgba(4,13,20,0.95);
  border-top: 1px solid var(--border);
  padding: 1.5rem clamp(1.2rem,5vw,3.5rem);
  display: flex; align-items: center; justify-content: space-between;
  flex-wrap: wrap; gap: 1rem;
}
.footer-brand {
  font-family: var(--font-display); font-size: 0.7rem;
  color: var(--cyan); letter-spacing: 0.1em;
}
.footer-meta {
  font-family: var(--font-mono); font-size: 0.65rem;
  color: var(--text-muted); letter-spacing: 0.08em;
}
.footer-integrity {
  font-family: var(--font-mono); font-size: 0.62rem;
  color: var(--green); letter-spacing: 0.08em;
  display: flex; align-items: center; gap: 6px;
}
.footer-integrity::before { content: '✓'; color: var(--green); }

/* UTILITY */
.reveal {
  opacity: 0; transform: translateY(18px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}
.reveal.visible { opacity: 1; transform: none; }

/* ============================================================
   MOBILE
============================================================ */
@media (max-width: 960px) {
  .hero { grid-template-columns: 1fr; }
  .hero-visual { display: none; }
  .about-grid { grid-template-columns: 1fr; }
  .purpose-grid { grid-template-columns: 1fr; }
  .lesson-grid { grid-template-columns: 1fr; }
  .challenge-item { flex-direction: column; }
  .challenge-label { flex: none; }
}
@media (max-width: 700px) {
  .nav-links { display: none; }
  .nav-links.open {
    display: flex; flex-direction: column; gap: 0;
    position: fixed; top: 64px; left: 0; right: 0;
    background: rgba(4,13,20,0.98);
    border-bottom: 1px solid var(--border);
    z-index: 400;
  }
  .nav-links.open a { height: 52px; border-right: none; border-top: 1px solid var(--border); }
  .hamburger { display: flex; }
  .hero-metrics { grid-template-columns: repeat(2,1fr); }
  .ethics-grid { grid-template-columns: 1fr; }
  footer { flex-direction: column; align-items: flex-start; gap: 0.5rem; }
}
</style>
</head>
<body>

<!-- BACKGROUND -->
<div class="grid-bg"></div>
<div class="scan-line"></div>

<!-- NAV -->
<nav id="nav">
  <a href="#" class="nav-logo" onclick="showPage('home');return false;">
    <span class="logo-bracket">[</span>
    <span>DNPH</span>
    <span class="logo-bracket">]</span>
    <span class="logo-dot"></span>
  </a>
  <ul class="nav-links" id="navLinks">
    <li><a href="#" onclick="showPage('home');return false;" id="nav-home" class="active">
      <span class="nav-num">01</span> Giới Thiệu
    </a></li>
    <li><a href="#" onclick="showPage('projects');return false;" id="nav-projects">
      <span class="nav-num">02</span> Dự Án
    </a></li>
    <li><a href="#" onclick="showPage('reflection');return false;" id="nav-reflection">
      <span class="nav-num">03</span> Tổng Kết
    </a></li>
  </ul>
  <button class="hamburger" id="hamburger" aria-label="Menu">
    <span></span><span></span><span></span>
  </button>
</nav>

<!-- ================================================================
     PAGE 1 — HOME
================================================================ -->
<div class="page active" id="page-home">

  <!-- HERO -->
  <div class="hero">
    <div class="hero-content">
      <div class="hero-status">
        <span class="status-dot"></span>
        PORTFOLIO.ACTIVE — K70P-ME1 — ĐH CÔNG NGHỆ
      </div>
      <h1 class="hero-name">
        <span class="line1">ĐÀO DƯƠNG</span><br/>
        <span class="line2">NAM PHƯƠNG</span><br/>
        <span class="line3">// SINH VIÊN KỸ THUẬT</span>
      </h1>
      <div class="hero-sub">
        &gt; MSV: 25024023 &nbsp;|&nbsp; Lớp: K70P-ME1 &nbsp;|&nbsp; Đại học Công nghệ, ĐHQGHN
      </div>
      <p class="hero-desc">
        Sinh viên ngành <strong>Kỹ thuật Cơ điện tử</strong> với niềm đam mê khám phá giao thoa giữa
        <strong>trí tuệ nhân tạo</strong>, <strong>vật liệu tiên tiến</strong> và <strong>tự động hóa thông minh</strong>.
        Portfolio này là hành trình học tập — không chỉ lưu trữ sản phẩm, mà còn phản ánh
        tư duy phản biện và tinh thần liêm chính học thuật.
      </p>
      <div class="hero-btns">
        <button class="btn btn-primary" onclick="showPage('projects')">
          ⚡ Xem Dự Án
        </button>
        <button class="btn btn-ghost" onclick="showPage('reflection')">
          ◈ Tổng Kết
        </button>
      </div>
      <div class="hero-metrics">
        <div class="metric-box">
          <span class="metric-val">07</span>
          <span class="metric-lab">Bài tập</span>
        </div>
        <div class="metric-box">
          <span class="metric-val">100%</span>
          <span class="metric-lab">Liêm chính</span>
        </div>
        <div class="metric-box">
          <span class="metric-val">4+</span>
          <span class="metric-lab">Công cụ AI</span>
        </div>
        <div class="metric-box">
          <span class="metric-val">Mức 4</span>
          <span class="metric-lab">Mục tiêu</span>
        </div>
      </div>
    </div>

    <div class="hero-visual">
      <div class="terminal-window">
        <div class="terminal-bar">
          <span class="t-dot r"></span>
          <span class="t-dot y"></span>
          <span class="t-dot g"></span>
          <span class="t-title">portfolio_v1.0 — bash</span>
        </div>
        <div class="terminal-body">
          <div class="t-line"><span class="t-prompt">❯ </span><span class="t-cmd">whoami</span></div>
          <div class="t-line"><span class="t-out">→ Đào Dương Nam Phương</span></div>
          <div class="t-line">&nbsp;</div>
          <div class="t-line"><span class="t-prompt">❯ </span><span class="t-cmd">cat info.json</span></div>
          <div class="t-line"><span class="t-out2">{</span></div>
          <div class="t-line"><span class="t-out2">&nbsp;&nbsp;"msv": </span><span class="t-out">"25024023"</span><span class="t-out2">,</span></div>
          <div class="t-line"><span class="t-out2">&nbsp;&nbsp;"lop": </span><span class="t-out">"K70P-ME1"</span><span class="t-out2">,</span></div>
          <div class="t-line"><span class="t-out2">&nbsp;&nbsp;"truong": </span><span class="t-out">"UET-VNU"</span><span class="t-out2">,</span></div>
          <div class="t-line"><span class="t-out2">&nbsp;&nbsp;"so_thich": </span><span class="t-out">"[Robotics, AI, Nhiếp ảnh]"</span></div>
          <div class="t-line"><span class="t-out2">}</span></div>
          <div class="t-line">&nbsp;</div>
          <div class="t-line"><span class="t-prompt">❯ </span><span class="t-cmd">ls ./projects/</span></div>
          <div class="t-line"><span class="t-out">bai1/ bai2/ bai3/ bai4/ bai5/ bai6/ bai7/</span></div>
          <div class="t-line">&nbsp;</div>
          <div class="t-line"><span class="t-prompt">❯ </span><span class="t-cmd">status --check</span></div>
          <div class="t-line"><span class="t-out">[✓] 7/7 tasks COMPLETED</span></div>
          <div class="t-line"><span class="t-out">[✓] academic_integrity: OK</span></div>
          <div class="t-line"><span class="t-prompt">❯ </span><span class="t-cursor"></span></div>
        </div>
      </div>
      <div class="profile-ring">ĐNP</div>
    </div>
  </div>

  <!-- ABOUT DETAILS -->
  <div class="section-wrapper">
    <div class="badge">01 — Giới thiệu bản thân</div>
    <div class="about-grid reveal">
      <div>
        <h2 class="section-title">Về <span class="accent">Tôi</span></h2>
        <p style="color:var(--text-secondary);font-size:0.96rem;line-height:1.8;margin-bottom:1.5rem;">
          Tôi là <strong style="color:var(--text-primary)">Đào Dương Nam Phương</strong> — sinh viên năm nhất Đại học Công nghệ, ĐHQGHN.
          Xuất phát từ đam mê với cơ học và điện tử, tôi đang khám phá cách kết hợp
          <strong style="color:var(--cyan)">trí tuệ nhân tạo</strong> vào giải quyết các bài toán kỹ thuật thực tiễn —
          từ dự đoán vật liệu tiên tiến đến tối ưu hóa hệ thống tự động.
        </p>

        <div class="info-item">
          <div class="info-icon">🎓</div>
          <div>
            <span class="info-label">Ngành học</span>
            <span class="info-value">Kỹ thuật Cơ điện tử — Đại học Công nghệ, ĐHQGHN</span>
          </div>
        </div>
        <div class="info-item">
          <div class="info-icon">🏷</div>
          <div>
            <span class="info-label">Mã số sinh viên & Lớp</span>
            <span class="info-value">25024023 — K70P-ME1</span>
          </div>
        </div>
        <div class="info-item">
          <div class="info-icon">⚙️</div>
          <div>
            <span class="info-label">Sở thích</span>
            <span class="info-value">Lập trình Robot · Nghiên cứu AI/Vật liệu · Nhiếp ảnh kỹ thuật số · Mô hình hóa 3D</span>
          </div>
        </div>
        <div class="info-item">
          <div class="info-icon">🌐</div>
          <div>
            <span class="info-label">Môn học Portfolio</span>
            <span class="info-value">Nhập môn Công nghệ số & Ứng dụng Trí tuệ nhân tạo</span>
          </div>
        </div>

        <div class="glitch-line"></div>
        <h3 style="font-family:var(--font-display);font-size:1rem;color:var(--cyan);letter-spacing:0.08em;margin-bottom:1.2rem;">KỸ NĂNG SỐ</h3>

        <div class="skill-bar-item">
          <div class="skill-bar-head">
            <span class="skill-name">Quản lý Tệp & Thư mục</span>
            <span class="skill-pct">90%</span>
          </div>
          <div class="skill-track"><div class="skill-fill" data-pct="90"></div></div>
        </div>
        <div class="skill-bar-item">
          <div class="skill-bar-head">
            <span class="skill-name">Tìm kiếm Học thuật Nâng cao</span>
            <span class="skill-pct">88%</span>
          </div>
          <div class="skill-track"><div class="skill-fill" data-pct="88"></div></div>
        </div>
        <div class="skill-bar-item">
          <div class="skill-bar-head">
            <span class="skill-name">Prompt Engineering</span>
            <span class="skill-pct">87%</span>
          </div>
          <div class="skill-track"><div class="skill-fill" data-pct="87"></div></div>
        </div>
        <div class="skill-bar-item">
          <div class="skill-bar-head">
            <span class="skill-name">Cộng tác Trực tuyến (Trello/Drive)</span>
            <span class="skill-pct">92%</span>
          </div>
          <div class="skill-track"><div class="skill-fill" data-pct="92"></div></div>
        </div>
        <div class="skill-bar-item">
          <div class="skill-bar-head">
            <span class="skill-name">AI Tạo sinh & Sáng tạo Nội dung</span>
            <span class="skill-pct">83%</span>
          </div>
          <div class="skill-track"><div class="skill-fill" data-pct="83"></div></div>
        </div>
        <div class="skill-bar-item">
          <div class="skill-bar-head">
            <span class="skill-name">Đạo đức AI & Liêm chính Học thuật</span>
            <span class="skill-pct">96%</span>
          </div>
          <div class="skill-track"><div class="skill-fill" data-pct="96"></div></div>
        </div>
      </div>

      <div>
        <h3 style="font-family:var(--font-display);font-size:0.85rem;color:var(--cyan);letter-spacing:0.1em;margin-bottom:1.2rem;">MỤC TIÊU HỌC TẬP</h3>
        <div class="goal-item">
          <div class="goal-num">01</div>
          <div>
            <div class="goal-title">NGẮN HẠN — 2024/2025</div>
            <div class="goal-text">Thành thạo <strong>kỹ năng số cốt lõi</strong> — quản lý thông tin, khai thác AI có đạo đức, cộng tác trực tuyến. Đạt GPA ≥ 3.4/4.0 học kỳ đầu tiên.</div>
          </div>
        </div>
        <div class="goal-item">
          <div class="goal-num">02</div>
          <div>
            <div class="goal-title">TRUNG HẠN — 2025/2027</div>
            <div class="goal-text">Nghiên cứu ứng dụng <strong>Machine Learning</strong> trong khoa học vật liệu và cơ điện tử. Tham gia nhóm nghiên cứu, đăng bài hội nghị sinh viên.</div>
          </div>
        </div>
        <div class="goal-item">
          <div class="goal-num">03</div>
          <div>
            <div class="goal-title">DÀI HẠN — SAU TỐT NGHIỆP</div>
            <div class="goal-text">Trở thành <strong>kỹ sư nghiên cứu</strong> tại tổ chức công nghệ hàng đầu hoặc theo đuổi học bổng Tiến sĩ về <strong>AI & Vật liệu thông minh</strong> tại Nhật/EU.</div>
          </div>
        </div>

        <div class="glitch-line"></div>
        <h3 style="font-family:var(--font-display);font-size:0.85rem;color:var(--green);letter-spacing:0.1em;margin-bottom:0.5rem;">CÔNG CỤ SỬ DỤNG</h3>
        <div style="margin-bottom:1.5rem;">
          <span class="tag">ChatGPT</span><span class="tag">Gemini</span><span class="tag">Claude</span>
          <span class="tag">Canva AI</span><span class="tag">Trello</span><span class="tag">Google Drive</span>
          <span class="tag">Google Docs</span><span class="tag">Discord</span><span class="tag">Google Scholar</span>
          <span class="tag">Consensus</span><span class="tag">Elicit</span><span class="tag">ScienceDirect</span>
        </div>
        <div style="padding:1rem 1.2rem;border:1px solid rgba(0,255,136,0.3);background:var(--green-dim);">
          <div style="font-family:var(--font-mono);font-size:0.62rem;color:var(--green);letter-spacing:0.1em;margin-bottom:0.4rem;">// CAM KẾT LIÊM CHÍNH</div>
          <p style="font-size:0.82rem;color:var(--text-secondary);line-height:1.7;">
            Mọi nội dung được <strong style="color:var(--text-primary)">tự thực hiện</strong>. Việc dùng AI được <strong style="color:var(--text-primary)">khai báo rõ ràng</strong>. AI chỉ là công cụ hỗ trợ — không thay thế tư duy.
          </p>
          <div style="font-family:var(--font-mono);font-size:0.62rem;color:var(--green);margin-top:0.6rem;">✓ VERIFIED — Academic Integrity Standard</div>
        </div>
      </div>
    </div>

    <!-- PORTFOLIO PURPOSE -->
    <div class="glitch-line"></div>
    <div class="badge">Mục tiêu Portfolio</div>
    <h2 class="section-title reveal">Ba <span class="accent">Mục Đích</span> Cốt Lõi</h2>
    <div class="purpose-grid reveal">
      <div class="purpose-item">
        <div class="purpose-num">01</div>
        <span class="purpose-icon">💾</span>
        <div class="purpose-title">LƯU TRỮ SẢN PHẨM</div>
        <div class="purpose-text">Hệ thống hóa toàn bộ bài tập, dự án và sản phẩm số từ học phần thành hồ sơ năng lực có thể truy xuất và đối chiếu trong tương lai.</div>
      </div>
      <div class="purpose-item">
        <div class="purpose-num">02</div>
        <span class="purpose-icon">⚡</span>
        <div class="purpose-title">THỂ HIỆN KỸ NĂNG SỐ</div>
        <div class="purpose-text">Minh chứng cụ thể và có hệ thống cho năng lực sử dụng công nghệ số — từ quản lý tệp, khai thác thông tin đến ứng dụng AI tạo sinh sáng tạo.</div>
      </div>
      <div class="purpose-item">
        <div class="purpose-num">03</div>
        <span class="purpose-icon">⚖️</span>
        <div class="purpose-title">LIÊM CHÍNH HỌC THUẬT</div>
        <div class="purpose-text">Cam kết minh bạch về nguồn gốc nội dung, sử dụng AI có trách nhiệm và tuân thủ quy chuẩn đạo đức trong mọi sản phẩm được trình bày.</div>
      </div>
    </div>
  </div>
</div><!-- END PAGE HOME -->


<!-- ================================================================
     PAGE 2 — PROJECTS
================================================================ -->
<div class="page" id="page-projects">
  <div class="ex-hero">
    <div class="badge">02 — Bài tập thành phần</div>
    <h1 class="section-title">07 Dự Án <span class="accent">Thực Hành</span></h1>
    <p style="color:var(--text-secondary);font-size:0.92rem;max-width:65ch;line-height:1.7;margin-top:0.5rem;">
      Mỗi bài trình bày theo cấu trúc: <span class="mono-text">MỤC TIÊU → QUÁ TRÌNH → SẢN PHẨM</span>.
      Nhấn vào nút <span class="mono-text">[EXPAND]</span> để xem chi tiết từng bài.
    </p>
  </div>

  <div class="ex-grid" style="padding:0 clamp(1.2rem,5vw,3.5rem);max-width:none;">

    <!-- BÀI 1 -->
    <div class="ex-card reveal">
      <div class="ex-card-header">
        <div class="ex-num">01</div>
        <div class="ex-badge-wrap">
          <span class="ex-module">Mục 1.4</span>
          <span class="ex-status">COMPLETED</span>
        </div>
      </div>
      <div class="ex-card-body">
        <div class="ex-title">THAO TÁC TỆP VÀ THƯ MỤC<br/>— Máy tính & Thiết bị ngoại vi</div>
        <div class="ex-desc">
          Thực hành toàn diện với File Explorer: tạo, đổi tên, sao chép, di chuyển, xóa tệp và thư mục.
          Nắm vững thao tác Recycle Bin và khôi phục dữ liệu.
        </div>
        <div>
          <span class="tag">File Explorer</span><span class="tag">Windows OS</span>
          <span class="tag">Ctrl+C/V/X</span><span class="tag">Recycle Bin</span>
        </div>
        <button class="ex-expand-btn" onclick="togglePanel(this)">
          <span>▶</span><span class="arrow">›</span> CHI TIẾT BÀI TẬP
        </button>
        <div class="ex-panel">
          <div style="font-family:var(--font-mono);font-size:0.65rem;color:var(--cyan);letter-spacing:0.1em;margin-bottom:0.6rem;">// QUANG TRÌNH THỰC HIỆN</div>
          <ul class="process-list">
            <li><span class="ps-num">S.01</span>Mở File Explorer (Windows+E), truy cập ổ D: hoặc Documents.</li>
            <li><span class="ps-num">S.02</span>Tạo thư mục <code style="color:var(--cyan)">ThucHanh_DaoDuongNamPhuong</code> bằng New → Folder.</li>
            <li><span class="ps-num">S.03</span>Tạo tệp GhiChu.txt → đổi tên thành <code style="color:var(--cyan)">GhiChuQuanTrong.txt</code>.</li>
            <li><span class="ps-num">S.04</span>Tạo thư mục con TaiLieu; sao chép tệp vào bằng Ctrl+C/V.</li>
            <li><span class="ps-num">S.05</span>Tạo DiChuyen.txt → Cut & Paste vào TaiLieu (Ctrl+X/V).</li>
            <li><span class="ps-num">S.06</span>Xóa tệp → Recycle Bin → Restore; xóa vĩnh viễn bằng Shift+Delete.</li>
          </ul>
          <div class="result-box">
            <strong>Sản phẩm cuối:</strong> Cấu trúc thư mục hoàn chỉnh minh chứng 6 thao tác cơ bản. Nắm vững sự khác biệt giữa Copy/Move/Delete và cơ chế Recycle Bin. Xây dựng thói quen đặt tên tệp có cấu trúc: <code style="color:var(--green)">[MÔN]_[LOẠI]_[NỘI DUNG]_v[VER].ext</code>
          </div>
          <div style="margin-top:1rem;">
            <div style="font-family:var(--font-mono);font-size:0.62rem;color:var(--cyan);margin-bottom:0.4rem;">// KIẾN THỨC QUAN TRỌNG</div>
            <p style="font-size:0.84rem;color:var(--text-secondary);line-height:1.7;">
              Hiểu được cấu trúc hệ thống tệp phân cấp, sự khác biệt giữa copy và move ở cấp độ bit, và tầm quan trọng của quy chuẩn đặt tên file trong quản lý thông tin dài hạn.
            </p>
          </div>
        </div>
      </div>
    </div>

    <!-- BÀI 2 -->
    <div class="ex-card reveal">
      <div class="ex-card-header">
        <div class="ex-num">02</div>
        <div class="ex-badge-wrap">
          <span class="ex-module">Mục 2.4</span>
          <span class="ex-status">COMPLETED</span>
        </div>
      </div>
      <div class="ex-card-body">
        <div class="ex-title">PHÁT TRIỂN KỸ NĂNG TÌM KIẾM<br/>VÀ ĐÁNH GIÁ THÔNG TIN HỌC THUẬT</div>
        <div class="ex-desc">
          Chủ đề: <em>Tác động của AI đến hành vi mua sắm trực tuyến</em>. Sử dụng toán tử nâng cao, tìm kiếm 10 nguồn đa dạng, đánh giá theo tiêu chí học thuật.
        </div>
        <div>
          <span class="tag">Google Scholar</span><span class="tag">ScienceDirect</span>
          <span class="tag">Harvard Style</span><span class="tag">McKinsey/Gartner</span>
        </div>
        <button class="ex-expand-btn" onclick="togglePanel(this)">
          <span>▶</span><span class="arrow">›</span> CHI TIẾT BÀI TẬP
        </button>
        <div class="ex-panel">
          <div style="font-family:var(--font-mono);font-size:0.65rem;color:var(--cyan);letter-spacing:0.1em;margin-bottom:0.6rem;">// CHIẾN LƯỢC TÌM KIẾM</div>
          <p style="font-size:0.84rem;color:var(--text-secondary);line-height:1.7;margin-bottom:1rem;">
            Từ khóa: <code style="color:var(--cyan)">"Artificial Intelligence"</code>, <code style="color:var(--cyan)">"Consumer Behavior"</code>, <code style="color:var(--cyan)">"E-commerce"</code>, <code style="color:var(--cyan)">"Personalization"</code>, <code style="color:var(--cyan)">"AI Ethics"</code>
          </p>
          <table class="compare-table">
            <thead><tr><th>Nguồn tài liệu</th><th>Tác giả / Năm</th><th>Loại</th><th>Đánh giá</th></tr></thead>
            <tbody>
              <tr><td>International Journal of Information Management</td><td>Dwivedi et al. (2021)</td><td>Q1 Journal</td><td class="good">✓ Rất cao</td></tr>
              <tr><td>Journal of the Academy of Marketing Science</td><td>Huang & Rust (2021)</td><td>Q1 Journal</td><td class="good">✓ Rất cao</td></tr>
              <tr><td>Journal of the Academy of Marketing Science</td><td>Davenport et al. (2020)</td><td>Q1 Journal</td><td class="good">✓ Cao</td></tr>
              <tr><td>Tạp chí Công thương Việt Nam</td><td>Nguyen M.H. (2022)</td><td>Nội địa</td><td class="good">✓ Trung bình</td></tr>
              <tr><td>McKinsey & Company Report</td><td>McKinsey (2023)</td><td>Báo cáo</td><td class="warn">△ Tham khảo</td></tr>
              <tr><td>Gartner Top Trends 2024</td><td>Gartner (2024)</td><td>Báo cáo</td><td class="warn">△ Tham khảo</td></tr>
              <tr><td>Blog cá nhân không rõ nguồn</td><td>Không rõ</td><td>Blog</td><td class="bad">✗ Loại bỏ</td></tr>
            </tbody>
          </table>
          <div class="result-box" style="margin-top:0.8rem;">
            <strong>Sản phẩm cuối:</strong> Danh mục 10 tài liệu trích dẫn theo Harvard Style, kèm bảng đánh giá theo mô hình CRAAP (Currency, Relevance, Authority, Accuracy, Purpose). Tổng hợp chiến lược tìm kiếm hiệu quả cho nghiên cứu học thuật.
          </div>
        </div>
      </div>
    </div>

    <!-- BÀI 3 -->
    <div class="ex-card reveal">
      <div class="ex-card-header">
        <div class="ex-num">03</div>
        <div class="ex-badge-wrap">
          <span class="ex-module">Mục 3.4</span>
          <span class="ex-status">COMPLETED</span>
        </div>
      </div>
      <div class="ex-card-body">
        <div class="ex-title">TỐI ƯU HÓA QUY TRÌNH HỌC TẬP<br/>QUA KỸ THUẬT PROMPT ENGINEERING</div>
        <div class="ex-desc">
          Tiếp cận AI như "đối tác tư duy". Thử nghiệm 3 phiên bản Prompt (Basic → Structured → Expert) trên các tác vụ học thuật thực tế, phân tích hiệu quả qua bảng so sánh.
        </div>
        <div>
          <span class="tag">Chain-of-Thought</span><span class="tag">Role-play</span>
          <span class="tag">Few-shot</span><span class="tag">Context Priming</span>
        </div>
        <button class="ex-expand-btn" onclick="togglePanel(this)">
          <span>▶</span><span class="arrow">›</span> CHI TIẾT BÀI TẬP
        </button>
        <div class="ex-panel">
          <div style="font-family:var(--font-mono);font-size:0.65rem;color:var(--cyan);letter-spacing:0.1em;margin-bottom:0.8rem;">// SO SÁNH PROMPT TRƯỚC & SAU</div>
          <table class="compare-table">
            <thead><tr><th>Tiêu chí</th><th>❌ Prompt Cơ bản</th><th>✅ Prompt Nâng cao</th></tr></thead>
            <tbody>
              <tr><td>Nội dung</td><td>"Tóm tắt bài báo Sol-gel này giúp tôi."</td><td>Role-play biên tập viên Nature + CoT 3 bước + yêu cầu thuật ngữ chuyên ngành</td></tr>
              <tr><td>Vai trò AI</td><td>Không xác định</td><td>Chỉ định rõ (Biên tập viên Nature / GS Vật lý)</td></tr>
              <tr><td>Định dạng</td><td>Đoạn văn dài</td><td>Bảng + danh sách + câu hỏi phản biện</td></tr>
              <tr><td>Chất lượng</td><td class="bad">Chung chung, 120 từ</td><td class="good">Chuyên sâu, 650+ từ có cấu trúc</td></tr>
            </tbody>
          </table>
          <div style="margin-top:1rem;">
            <div style="font-family:var(--font-mono);font-size:0.62rem;color:var(--cyan);margin-bottom:0.4rem;">// 3 NGUYÊN TẮC VÀNG ĐÃ RÚT RA</div>
            <ul class="process-list">
              <li><span class="ps-num">R.01</span><strong style="color:var(--text-primary)">Context Priming:</strong> Thiết lập vai trò rõ ràng giúp AI giới hạn không gian từ vựng chuyên môn, loại bỏ nhiễu thông tin.</li>
              <li><span class="ps-num">R.02</span><strong style="color:var(--text-primary)">Decomposition (CoT):</strong> Phân rã bài toán thành các bước trung gian ngăn AI đưa ra kết luận vội vàng (hallucination).</li>
              <li><span class="ps-num">R.03</span><strong style="color:var(--text-primary)">Delimitation:</strong> Ràng buộc cụ thể ("không quá 200 chữ", "dùng bảng") buộc AI chắt lọc thông tin chất lượng cao nhất.</li>
            </ul>
          </div>
          <div class="result-box">
            <strong>Sản phẩm cuối:</strong> Báo cáo phân tích kỹ thuật Prompt Engineering với bảng so sánh 5 tiêu chí. Bộ quy tắc thiết kế prompt cá nhân hóa cho môi trường học thuật kỹ thuật.
          </div>
        </div>
      </div>
    </div>

    <!-- BÀI 4 -->
    <div class="ex-card reveal">
      <div class="ex-card-header">
        <div class="ex-num">04</div>
        <div class="ex-badge-wrap">
          <span class="ex-module">Mục 4.4</span>
          <span class="ex-status">COMPLETED</span>
        </div>
      </div>
      <div class="ex-card-body">
        <div class="ex-title">KỸ NĂNG LÀM VIỆC NHÓM<br/>& CÔNG CỤ HỢP TÁC TRỰC TUYẾN</div>
        <div class="ex-desc">
          Dự án nhóm: <em>Nghiên cứu kỹ thuật Prompt Engineering</em>. Vai trò: Phụ trách phân tích kỹ thuật & quản lý tài liệu. Sử dụng hệ sinh thái Trello + Drive + Docs + Discord.
        </div>
        <div>
          <span class="tag">Trello Kanban</span><span class="tag">Google Drive</span>
          <span class="tag">Google Docs</span><span class="tag">Discord</span>
        </div>
        <button class="ex-expand-btn" onclick="togglePanel(this)">
          <span>▶</span><span class="arrow">›</span> CHI TIẾT BÀI TẬP
        </button>
        <div class="ex-panel">
          <div style="font-family:var(--font-mono);font-size:0.65rem;color:var(--cyan);letter-spacing:0.1em;margin-bottom:0.8rem;">// HỆ THỐNG CỘNG TÁC ĐÃ TRIỂN KHAI</div>
          <ul class="process-list">
            <li><span class="ps-num">T.01</span><strong style="color:var(--cyan)">Trello Kanban:</strong> 4 cột (Backlog→To-do→Doing→Review→Done), hệ thống Label màu (Đỏ:Gấp, Vàng:Bình thường, Xanh:Kỹ thuật), cập nhật tiến độ 4 lần/tuần.</li>
            <li><span class="ps-num">T.02</span><strong style="color:var(--cyan)">Google Drive:</strong> Cấu trúc 3 cấp: <code>[Nhóm]_Dự_án > 1.Tài_liệu_tham_khảo / 2.Dữ_liệu_thô / 3.Bản_nháp</code>. Quy chuẩn đặt tên: <code>YYMMDD_Mảng_Nội-dung_v1.x</code>.</li>
            <li><span class="ps-num">T.03</span><strong style="color:var(--cyan)">Google Docs:</strong> Sử dụng Suggesting Mode thay vì chỉnh sửa trực tiếp, Add Comment cho thuật ngữ chuyên sâu. Khôi phục nội dung bị xóa nhầm qua Version History.</li>
            <li><span class="ps-num">T.04</span><strong style="color:var(--cyan)">Discord:</strong> Pin Message cho link Drive quan trọng, quy định đồng bộ file lên Drive ngay khi gửi. 12+ lượt tương tác chủ động/tuần.</li>
          </ul>
          <div class="result-box">
            <strong>Sản phẩm cuối:</strong> Báo cáo cá nhân phân tích 3 thách thức chính (phân tán thông tin, xung đột phiên bản, định lượng tiến độ) kèm giải pháp hệ thống. Minh chứng ảnh chụp Trello board và Google Drive structure.
          </div>
        </div>
      </div>
    </div>

    <!-- BÀI 5 -->
    <div class="ex-card reveal">
      <div class="ex-card-header">
        <div class="ex-num">05</div>
        <div class="ex-badge-wrap">
          <span class="ex-module">Mục 5.4</span>
          <span class="ex-status">COMPLETED</span>
        </div>
      </div>
      <div class="ex-card-body">
        <div class="ex-title">SÁNG TẠO NỘI DUNG SỐ<br/>BẰNG AI — INFOGRAPHIC VẬT LIỆU</div>
        <div class="ex-desc">
          Dự án: Infographic <em>"Ứng dụng AI trong khám phá vật liệu mới"</em>. Sử dụng ChatGPT + Gemini + Canva AI theo quy trình 4 bước, kết hợp sáng tạo cá nhân.
        </div>
        <div>
          <span class="tag">ChatGPT</span><span class="tag">Gemini</span>
          <span class="tag">Canva AI</span><span class="tag">Infographic</span>
        </div>
        <button class="ex-expand-btn" onclick="togglePanel(this)">
          <span>▶</span><span class="arrow">›</span> CHI TIẾT BÀI TẬP
        </button>
        <div class="ex-panel">
          <div style="font-family:var(--font-mono);font-size:0.65rem;color:var(--cyan);letter-spacing:0.1em;margin-bottom:0.8rem;">// QUY TRÌNH 4 BƯỚC</div>
          <ul class="process-list">
            <li><span class="ps-num">B.01</span><strong style="color:var(--cyan)">ChatGPT — Xây dựng nội dung:</strong> Prompt yêu cầu nội dung ngắn gọn dành cho sinh viên, gồm: khái niệm, quy trình, lợi ích, ứng dụng thực tế của AI trong khoa học vật liệu.</li>
            <li><span class="ps-num">B.02</span><strong style="color:var(--cyan)">Gemini — Mở rộng ví dụ:</strong> Bổ sung ví dụ cụ thể: DeepMind dự đoán vật liệu, AI phát triển pin lithium, thiết kế vật liệu sinh học.</li>
            <li><span class="ps-num">B.03</span><strong style="color:var(--cyan)">Chỉnh sửa cá nhân:</strong> Loại bỏ phần quá học thuật, viết lại ngôn ngữ dễ hiểu, thiết kế sơ đồ quy trình riêng, thêm phần "tương lai của AI".</li>
            <li><span class="ps-num">B.04</span><strong style="color:var(--cyan)">Canva AI — Thiết kế:</strong> Prompt tiếng Anh với chủ đề scientific blue/purple, icons AI + batteries + solar panels + lab. Chỉnh sửa bố cục, thêm biểu tượng cá nhân.</li>
          </ul>
          <div style="background:var(--bg-card);border:1px solid var(--border);padding:1rem;margin:0.8rem 0;">
            <div style="font-family:var(--font-mono);font-size:0.62rem;color:var(--green);margin-bottom:0.5rem;">// INFOGRAPHIC — QUY TRÌNH AI</div>
            <div style="font-family:var(--font-mono);font-size:0.72rem;color:var(--cyan);text-align:center;padding:0.5rem;">
              Dữ liệu nghiên cứu → Huấn luyện AI → Dự đoán vật liệu → Kiểm tra lab → Vật liệu mới
            </div>
            <div style="display:grid;grid-template-columns:repeat(4,1fr);gap:0.5rem;margin-top:0.8rem;text-align:center;font-size:0.72rem;color:var(--text-secondary);">
              <div>⚡ Pin lithium thế hệ mới</div>
              <div>☀️ Pin mặt trời cao hiệu suất</div>
              <div>🔬 Vật liệu y sinh</div>
              <div>🚗 Công nghệ xe điện</div>
            </div>
          </div>
          <div class="result-box">
            <strong>Sản phẩm cuối:</strong> Infographic hoàn chỉnh + Báo cáo so sánh 3 công cụ AI (ChatGPT vs Gemini vs Canva AI). Khai báo đầy đủ vai trò AI — tác giả chịu trách nhiệm toàn bộ nội dung cuối cùng.
          </div>
        </div>
      </div>
    </div>

    <!-- BÀI 6 -->
    <div class="ex-card reveal">
      <div class="ex-card-header">
        <div class="ex-num">06</div>
        <div class="ex-badge-wrap">
          <span class="ex-module">Mục 6.4</span>
          <span class="ex-status">COMPLETED</span>
        </div>
      </div>
      <div class="ex-card-body">
        <div class="ex-title">SỬ DỤNG AI CÓ TRÁCH NHIỆM<br/>& ĐẠO ĐỨC TRONG HỌC TẬP</div>
        <div class="ex-desc">
          Nghiên cứu chính sách AI của VNU-ĐHQGHN; thực hiện nhiệm vụ viết luận với hỗ trợ AI; phân tích đạo đức; xây dựng bộ nguyên tắc cá nhân có cơ sở lý thuyết.
        </div>
        <div>
          <span class="tag">AI Ethics</span><span class="tag">VNU Policy</span>
          <span class="tag">Sol-gel Research</span><span class="tag">Academic Integrity</span>
        </div>
        <button class="ex-expand-btn" onclick="togglePanel(this)">
          <span>▶</span><span class="arrow">›</span> CHI TIẾT BÀI TẬP
        </button>
        <div class="ex-panel">
          <div style="font-family:var(--font-mono);font-size:0.65rem;color:var(--cyan);letter-spacing:0.1em;margin-bottom:0.8rem;">// BỘ NGUYÊN TẮC CÁ NHÂN — AI CÓ TRÁCH NHIỆM</div>
          <div class="ethics-grid">
            <div class="ethics-item">
              <div class="ethics-item-title">01 — MINH BẠCH (Transparency)</div>
              <p>Luôn khai báo khi AI có đóng góp đáng kể. Ghi rõ công cụ và vai trò AI so với đóng góp cá nhân trong từng sản phẩm.</p>
            </div>
            <div class="ethics-item">
              <div class="ethics-item-title">02 — TRÁCH NHIỆM (Accountability)</div>
              <p>Dù AI hỗ trợ ở mức nào, tác giả chịu hoàn toàn trách nhiệm về độ chính xác, chất lượng và hệ quả của nội dung.</p>
            </div>
            <div class="ethics-item">
              <div class="ethics-item-title">03 — KHÔNG ĐẠO VĂN AI</div>
              <p>Không sao chép nguyên văn đầu ra AI. Mọi nội dung phải được tư duy lại, chỉnh sửa, và là sản phẩm của quá trình nhận thức cá nhân.</p>
            </div>
            <div class="ethics-item">
              <div class="ethics-item-title">04 — TƯ DUY PHÊ PHÁN</div>
              <p>AI có thể "hallucinate". Luôn kiểm chứng thông tin từ nguồn học thuật uy tín. Tin tưởng có phê phán, không tin tuyệt đối.</p>
            </div>
            <div class="ethics-item">
              <div class="ethics-item-title">05 — TÔN TRỌNG BẢN QUYỀN</div>
              <p>Chỉ sử dụng AI tạo sinh cho nội dung không vi phạm quyền sở hữu trí tuệ. Không dùng AI để sao chép tác phẩm người khác.</p>
            </div>
            <div class="ethics-item">
              <div class="ethics-item-title">06 — PHÁT TRIỂN BẢN THÂN</div>
              <p>AI là công cụ học hỏi, không phải máy "làm bài thay". Mục tiêu cuối cùng là phát triển năng lực tư duy thực sự của bản thân.</p>
            </div>
          </div>
          <div class="result-box" style="margin-top:0.8rem;">
            <strong>Sản phẩm cuối:</strong> Báo cáo nghiên cứu chính sách AI của VNU + minh chứng thực hiện bài luận Sol-gel theo từng bước có AI hỗ trợ + bộ 6 nguyên tắc đạo đức cá nhân tham chiếu UNESCO (2022) & EU AI Act (2024).
          </div>
        </div>
      </div>
    </div>

    <!-- BÀI 7 -->
    <div class="ex-card reveal" style="grid-column: 1 / -1;">
      <div class="ex-card-header">
        <div class="ex-num">07</div>
        <div class="ex-badge-wrap">
          <span class="ex-module">Nghiên cứu Khoa học</span>
          <span class="ex-status">COMPLETED</span>
        </div>
      </div>
      <div class="ex-card-body">
        <div class="ex-title">ỨNG DỤNG AI TRONG KHÁM PHÁ VẬT LIỆU PIN THỂ RẮN<br/>— NGHIÊN CỨU TỔNG QUAN HỆ THỐNG</div>
        <div class="ex-desc">
          Câu hỏi nghiên cứu: <em>AI hỗ trợ sàng lọc, dự đoán và thiết kế vật liệu chất điện phân rắn như thế nào?</em>
          Tổng quan 5 bài báo ISI/Scopus tiêu biểu (2017–2023), phân tích xu hướng từ ML truyền thống đến GNN quy mô lớn.
        </div>
        <div>
          <span class="tag">Machine Learning</span><span class="tag">Graph Neural Networks</span>
          <span class="tag">Solid-State Battery</span><span class="tag">DeepMind GNoME</span>
          <span class="tag">Consensus AI</span><span class="tag">Elicit</span>
        </div>
        <button class="ex-expand-btn" onclick="togglePanel(this)">
          <span>▶</span><span class="arrow">›</span> CHI TIẾT NGHIÊN CỨU
        </button>
        <div class="ex-panel">
          <div style="display:grid;grid-template-columns:1fr 1fr;gap:1.5rem;margin-bottom:1.2rem;">
            <div>
              <div style="font-family:var(--font-mono);font-size:0.62rem;color:var(--cyan);margin-bottom:0.6rem;">// 5 BÀI BÁO TIÊU BIỂU</div>
              <ul class="process-list">
                <li><span class="ps-num">2017</span>Sendek et al. — Logistic Regression/SVM sàng lọc 12.111 vật liệu chứa Li → phát hiện Li5B7S13 tiềm năng.</li>
                <li><span class="ps-num">2018</span>Ahmad et al. — SVR + Random Forest dự đoán cửa sổ ổn định điện hóa, MAE &lt; 0.15V.</li>
                <li><span class="ps-num">2020</span>Allam et al. — XGBoost + High-throughput DFT đề xuất 5 hệ vật liệu mới &gt;10⁻³ S/cm.</li>
                <li><span class="ps-num">2021</span>Hatakeyama-Sato et al. — Graph-based ML thiết kế màng polyme lai gốm, kiểm chứng thực nghiệm.</li>
                <li><span class="ps-num">2023</span>Google DeepMind — GNoME: 381.000 vật liệu mới, <strong style="color:var(--green)">528 fast-ion conductors</strong> cho pin thể rắn.</li>
              </ul>
            </div>
            <div>
              <div style="font-family:var(--font-mono);font-size:0.62rem;color:var(--cyan);margin-bottom:0.6rem;">// XU HƯỚNG CHUYỂN DỊCH MÔ HÌNH</div>
              <ul class="process-list">
                <li><span class="ps-num">Giai đoạn 1</span>ML truyền thống (SVM, RF): Phụ thuộc Feature Engineering thủ công.</li>
                <li><span class="ps-num">Giai đoạn 2</span>Gradient Boosting (XGBoost): Kết hợp High-throughput DFT, độ chính xác cao hơn.</li>
                <li><span class="ps-num">Giai đoạn 3</span>Graph Neural Networks: Biểu diễn tinh thể dạng đồ thị, tự học đặc trưng từ cấu trúc nguyên tử.</li>
                <li><span class="ps-num">Tương lai</span>Closed-loop Autonomous Labs: AI + Robot + thực nghiệm tự động khép kín.</li>
              </ul>
            </div>
          </div>
          <div style="padding:1rem;border:1px solid var(--border);background:var(--bg-card);margin-bottom:0.8rem;">
            <div style="font-family:var(--font-mono);font-size:0.62rem;color:var(--orange);margin-bottom:0.4rem;">// 3 KHOẢNG TRỐNG NGHIÊN CỨU (Research Gaps)</div>
            <div style="display:grid;grid-template-columns:repeat(3,1fr);gap:0.8rem;font-size:0.8rem;color:var(--text-secondary);">
              <div><strong style="color:var(--orange)">① Data Scarcity:</strong> Dữ liệu huấn luyện thiên lệch về các vật liệu thành công, thiếu dữ liệu thất bại → AI bị bias.</div>
              <div><strong style="color:var(--orange)">② Synthesis Gap:</strong> Vật liệu dự đoán tốt trên máy tính nhưng không thể tổng hợp thực tế do kinetics phức tạp.</div>
              <div><strong style="color:var(--orange)">③ Black-Box:</strong> Học sâu thiếu tính diễn giải vật lý (Explainable AI), giảm tin tưởng của kỹ sư thực nghiệm.</div>
            </div>
          </div>
          <div class="result-box">
            <strong>Sản phẩm cuối:</strong> Báo cáo nghiên cứu khoa học 3.000+ từ với bảng tổng hợp 5 bài báo (8 cột phân tích), phân tích xu hướng thuật toán, đánh giá khoảng trống nghiên cứu và triển vọng "Phòng thí nghiệm tự chủ đóng kín". Tra cứu qua Consensus AI và Elicit.
          </div>
        </div>
      </div>
    </div>

  </div><!-- end ex-grid -->
</div><!-- END PAGE PROJECTS -->


<!-- ================================================================
     PAGE 3 — REFLECTION
================================================================ -->
<div class="page" id="page-reflection">
  <div class="refl-header">
    <div class="badge">03 — Tổng kết & Suy ngẫm</div>
    <h1 class="section-title">Nhìn Lại <span class="accent">Hành Trình</span><br/>Để Tiến <span class="accent2">Về Phía Trước</span></h1>
    <p style="color:var(--text-secondary);font-size:0.92rem;max-width:65ch;line-height:1.7;margin-top:0.5rem;">
      Sau một học kỳ với 7 bài tập thành phần — đây là những gì tôi thực sự học được,
      cảm nhận được, và mang theo.
    </p>
  </div>

  <div class="section-wrapper">
    <!-- TRẢI NGHIỆM -->
    <div class="badge">Trải nghiệm thực tế</div>
    <div class="exp-block reveal" data-num="01">
      <div class="exp-label">Cảm nhận cá nhân</div>
      <div class="exp-title">Từ "biết dùng máy tính" đến "tư duy số"</div>
      <div class="exp-text">
        Trước học kỳ này, tôi nghĩ mình đã "thành thạo công nghệ" vì biết dùng máy tính, tìm kiếm Google, và đã từng dùng ChatGPT.
        Nhưng qua 7 bài tập, tôi nhận ra có một khoảng cách rất lớn giữa <strong>"biết dùng"</strong> và <strong>"dùng có hệ thống, có chiến lược và có đạo đức"</strong>.
        <br/><br/>
        Bài học đầu tiên về quản lý tệp tưởng như đơn giản — nhưng chính việc xây dựng một hệ thống đặt tên nhất quán đã giúp tôi tiết kiệm hàng giờ mỗi tuần.
        Bài nghiên cứu về pin thể rắn (Bài 7) là lần đầu tiên tôi cảm nhận được sức mạnh thực sự của AI nghiên cứu — khi <strong>Consensus AI và Elicit</strong>
        giúp tôi sàng lọc 120+ bài báo xuống còn 5 bài tiêu biểu nhất chỉ trong 30 phút.
      </div>
    </div>

    <div class="exp-block reveal" data-num="02">
      <div class="exp-label">Khoảnh khắc thay đổi quan điểm</div>
      <div class="exp-title">AI không phải "máy trả lời" — mà là "đối tác tư duy"</div>
      <div class="exp-text">
        Bước ngoặt lớn nhất trong học kỳ là khi tôi thay đổi cách nhìn về AI. Lúc đầu, tôi thường prompt kiểu
        <em style="color:var(--cyan)">"Giải thích X cho tôi"</em> và nhận về những câu trả lời chung chung.
        Sau khi học Prompt Engineering (Bài 3), tôi bắt đầu thiết kế prompt như một <strong>bài toán kỹ thuật</strong> —
        xác định vai trò, ngữ cảnh, ràng buộc, định dạng đầu ra.
        <br/><br/>
        Lần đầu tiên tôi dùng kỹ thuật <strong>Chain-of-Thought + Role-play</strong> để phân tích bài báo Sol-gel,
        kết quả đầu ra của AI đột nhiên trở nên sâu sắc và có cấu trúc đến mức tôi phải đọc lại để hiểu.
        Đó là khoảnh khắc tôi hiểu: <em>chất lượng của câu trả lời phản ánh chất lượng của câu hỏi</em>.
      </div>
    </div>

    <div class="exp-block reveal" data-num="03">
      <div class="exp-label">Trải nghiệm nhóm</div>
      <div class="exp-title">Cộng tác số không tự nhiên — nó cần thiết kế</div>
      <div class="exp-text">
        Dự án nhóm (Bài 4) là thử thách thực tế nhất. Tuần đầu, nhóm 4 người thất bại hoàn toàn về cộng tác:
        file gửi qua Zalo, thông tin quan trọng bị "trôi", hai người cùng chỉnh sửa một đoạn văn và xóa mất công việc của nhau.
        <br/><br/>
        Giải pháp không phải là "cố gắng hơn" — mà là <strong>thiết kế lại quy trình làm việc</strong>:
        Pin Message, Suggesting Mode trên Google Docs, phân quyền Drive, và rule "mọi file phải có trên Drive trước khi gửi vào chat".
        Sau khi áp dụng, nhóm tôi hoàn thành công việc nhanh hơn gấp đôi với chất lượng tốt hơn nhiều.
        Bài học: <strong>hệ thống tốt quan trọng hơn nỗ lực cá nhân</strong>.
      </div>
    </div>

    <div class="glitch-line"></div>

    <!-- KIẾN THỨC -->
    <div class="badge">Kiến thức & Kỹ năng</div>
    <h2 class="section-title reveal">Những Bài Học <span class="accent">Quan Trọng Nhất</span></h2>
    <div class="lesson-grid reveal">
      <div class="lesson-item">
        <div class="lesson-num">01</div>
        <div class="lesson-title">HỆ THỐNG HÓA TIẾT KIỆM HƠN TỐC ĐỘ</div>
        <div class="lesson-text">Đầu tư 2 giờ thiết kế cấu trúc thư mục và quy tắc đặt tên (Bài 1) đã tiết kiệm hàng chục giờ tìm kiếm file về sau. <strong>Tư duy dài hạn trong quản lý thông tin là kỹ năng nền tảng</strong> của mọi kỹ sư.</div>
      </div>
      <div class="lesson-item">
        <div class="lesson-num">02</div>
        <div class="lesson-title">CHẤT LƯỢNG CÂU HỎI = CHẤT LƯỢNG CÂU TRẢ LỜI</div>
        <div class="lesson-text">Prompt Engineering (Bài 3) dạy tôi rằng <strong>thiết kế câu hỏi là một kỹ năng kỹ thuật</strong>. Một prompt được cấu trúc tốt không chỉ cho kết quả AI tốt hơn — nó còn buộc chính mình phải suy nghĩ rõ ràng hơn về vấn đề.</div>
      </div>
      <div class="lesson-item">
        <div class="lesson-num">03</div>
        <div class="lesson-title">ĐÁNH GIÁ NGUỒN TIN LÀ KỸ NĂNG SỐNG CÒN</div>
        <div class="lesson-text">Bài 2 cho thấy 40%+ kết quả trang đầu Google không đủ tiêu chuẩn học thuật. <strong>Mô hình CRAAP và kỹ năng đọc bài báo ISI</strong> là công cụ không thể thiếu trong thời đại thông tin nhiễu.</div>
      </div>
      <div class="lesson-item">
        <div class="lesson-num">04</div>
        <div class="lesson-title">AI THAY ĐỔI TỐC ĐỘ NGHIÊN CỨU KHOA HỌC</div>
        <div class="lesson-text">Bài 7 về pin thể rắn cho thấy AI (GNoME của DeepMind) <strong>rút ngắn chu kỳ phát triển vật liệu từ 18 năm xuống 12 tháng</strong>. Tôi — một kỹ sư tương lai — phải hiểu và biết khai thác sức mạnh này.</div>
      </div>
    </div>

    <div class="glitch-line"></div>

    <!-- THÁCH THỨC -->
    <div class="badge">Thách thức & Giải pháp</div>
    <h2 class="section-title reveal">Những <span class="accent">Thách Thức</span> Đã Vượt Qua</h2>

    <div class="challenge-item reveal">
      <div class="challenge-label">⚠ QUẢN LÝ THỜI GIAN</div>
      <div class="challenge-sol">
        Bị quá tải khi song song 7 bài tập với môn chuyên ngành. <strong>Giải pháp:</strong> Áp dụng Time-blocking (Pomodoro 50/10) và ưu tiên theo ma trận Eisenhower. Hoàn thành tất cả đúng hạn và không hy sinh chất lượng.
      </div>
    </div>
    <div class="challenge-item reveal">
      <div class="challenge-label">⚠ CÁM DỖ LẠM DỤNG AI</div>
      <div class="challenge-sol">
        Cám dỗ dùng AI làm toàn bộ bài tập rất lớn — đặc biệt với Bài 7 (nghiên cứu khoa học phức tạp). <strong>Giải pháp:</strong> Tự đặt quy tắc: AI chỉ hỗ trợ sàng lọc tài liệu và kiểm tra lập luận; phân tích và kết luận phải là của mình. Kết quả: sản phẩm có chiều sâu thực sự.
      </div>
    </div>
    <div class="challenge-item reveal">
      <div class="challenge-label">⚠ KHOẢNG CÁCH NGÔN NGỮ CHUYÊN NGÀNH</div>
      <div class="challenge-sol">
        Bài 7 đòi hỏi hiểu thuật ngữ về GNN, DFT, solid electrolyte — vượt xa kiến thức năm 1. <strong>Giải pháp:</strong> Dùng chính kỹ thuật Prompt Engineering (Bài 3) để yêu cầu AI giải thích theo cấp độ từng bước. Biến thách thức thành ứng dụng thực tế của bài học.
      </div>
    </div>
    <div class="challenge-item reveal">
      <div class="challenge-label">⚠ ĐÁNH GIÁ CHÍNH XÁC NGUỒN TIN</div>
      <div class="challenge-sol">
        Lúc đầu không phân biệt được peer-reviewed và non-peer-reviewed, bị nhầm lẫn giữa báo cáo công ty (McKinsey) và bài báo ISI. <strong>Giải pháp:</strong> Thực hành đánh giá 15+ nguồn theo mô hình CRAAP. Nay có thể xác định chất lượng nguồn trong vòng 2 phút.
      </div>
    </div>

    <div class="glitch-line"></div>

    <!-- TÂM ĐẮC -->
    <div class="badge">Điều tâm đắc nhất</div>
    <div class="quote-block reveal">
      <div class="quote-text">
        "Điều tôi tâm đắc nhất không phải là 7 sản phẩm đã hoàn thành, mà là <em>thói quen tư duy</em> đã hình thành.
        Tôi học cách <em>đặt câu hỏi trước khi tìm câu trả lời</em>, kiểm chứng trước khi tin tưởng, và khai báo trước khi nộp.
        Đây là nền tảng của một kỹ sư nghiên cứu — không chỉ giỏi kỹ thuật,
        mà còn trung thực với khoa học và có trách nhiệm với xã hội."
      </div>
      <div class="quote-author">— Đào Dương Nam Phương · MSV 25024023 · ĐH Công nghệ, ĐHQGHN · 2025</div>
    </div>

  </div>
</div><!-- END PAGE REFLECTION -->


<!-- FOOTER -->
<footer>
  <div class="footer-brand">[ PORTFOLIO_v1.0 ] — ĐÀO DƯƠNG NAM PHƯƠNG</div>
  <div class="footer-meta">MSV: 25024023 · K70P-ME1 · UET-VNU · HK I/2024-2025</div>
  <div class="footer-integrity">Liêm chính học thuật được cam kết trong toàn bộ nội dung</div>
</footer>

<script>
/* ============================================================
   PAGE NAVIGATION
============================================================ */
function showPage(id) {
  document.querySelectorAll('.page').forEach(p => {
    p.classList.remove('active');
  });
  document.querySelectorAll('.nav-links a').forEach(a => {
    a.classList.remove('active');
  });

  const page = document.getElementById('page-' + id);
  const navEl = document.getElementById('nav-' + id);
  if (page) {
    page.classList.add('active');
    window.scrollTo({ top: 0, behavior: 'smooth' });
  }
  if (navEl) navEl.classList.add('active');

  // Close mobile menu
  document.getElementById('navLinks').classList.remove('open');

  // Trigger skill bars if home
  if (id === 'home') {
    setTimeout(animateSkillBars, 400);
  }
  // Trigger reveals
  setTimeout(checkReveal, 200);
}

/* ============================================================
   HAMBURGER
============================================================ */
document.getElementById('hamburger').addEventListener('click', function() {
  document.getElementById('navLinks').classList.toggle('open');
});
document.addEventListener('click', function(e) {
  const nav = document.getElementById('nav');
  if (!nav.contains(e.target)) {
    document.getElementById('navLinks').classList.remove('open');
  }
});

/* ============================================================
   EXPAND PANELS
============================================================ */
function togglePanel(btn) {
  const panel = btn.nextElementSibling;
  const isOpen = panel.classList.contains('open');
  panel.classList.toggle('open', !isOpen);
  btn.classList.toggle('open', !isOpen);
  btn.querySelector('span').textContent = isOpen ? '▶' : '▼';
}

/* ============================================================
   SCROLL REVEAL
============================================================ */
function checkReveal() {
  document.querySelectorAll('.page.active .reveal').forEach(el => {
    const rect = el.getBoundingClientRect();
    if (rect.top < window.innerHeight * 0.9) {
      el.classList.add('visible');
    }
  });
}
window.addEventListener('scroll', checkReveal);

/* ============================================================
   SKILL BARS
============================================================ */
function animateSkillBars() {
  document.querySelectorAll('.skill-fill').forEach(bar => {
    const pct = bar.getAttribute('data-pct');
    bar.style.width = pct + '%';
  });
}

/* ============================================================
   INIT
============================================================ */
window.addEventListener('DOMContentLoaded', () => {
  checkReveal();
  setTimeout(animateSkillBars, 600);

  // Typewriter for terminal (subtle effect)
  const tLines = document.querySelectorAll('.terminal-body .t-line');
  tLines.forEach((line, i) => {
    line.style.opacity = '0';
    line.style.transition = 'opacity 0.3s';
    setTimeout(() => { line.style.opacity = '1'; }, i * 120);
  });
});
</script>
</body>
</html>
