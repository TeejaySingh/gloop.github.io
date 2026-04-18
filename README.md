<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>GlobalLoop — Connect the Universe</title>
<link href="https://fonts.googleapis.com/css2?family=Orbitron:wght@400;600;800;900&family=Exo+2:wght@300;400;500;600&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
<style>
  :root {
    --void: #020408;
    --deep: #050d1a;
    --nebula-blue: #0a1628;
    --nebula-purple: #1a0a2e;
    --star-white: #e8f0ff;
    --cosmic-cyan: #00d4ff;
    --cosmic-purple: #8b5cf6;
    --nova-pink: #f472b6;
    --solar-gold: #fbbf24;
    --mars-red: #ef4444;
    --like-green: #22c55e;
    --dislike-orange: #f97316;
    --glass: rgba(255,255,255,0.04);
    --glass-border: rgba(0,212,255,0.15);
    --text-primary: #e8f0ff;
    --text-muted: #6b8aa8;
  }

- { margin: 0; padding: 0; box-sizing: border-box; }

body {
background: var(–void);
color: var(–text-primary);
font-family: ‘Exo 2’, sans-serif;
min-height: 100vh;
overflow-x: hidden;
}

/* ─── STARFIELD BACKGROUND ─── */
#starfield {
position: fixed;
top: 0; left: 0;
width: 100%; height: 100%;
z-index: 0;
pointer-events: none;
}

.nebula-bg {
position: fixed;
top: 0; left: 0;
width: 100%; height: 100%;
z-index: 0;
background:
radial-gradient(ellipse 80% 60% at 20% 30%, rgba(139,92,246,0.12) 0%, transparent 60%),
radial-gradient(ellipse 60% 80% at 80% 70%, rgba(0,212,255,0.10) 0%, transparent 60%),
radial-gradient(ellipse 50% 40% at 50% 10%, rgba(244,114,182,0.07) 0%, transparent 50%),
radial-gradient(ellipse 100% 100% at 50% 50%, #020408 60%, #050d1a 100%);
animation: nebulaPulse 12s ease-in-out infinite alternate;
pointer-events: none;
}

@keyframes nebulaPulse {
0% { opacity: 0.8; }
100% { opacity: 1; }
}

/* ─── NAVBAR ─── */
nav {
position: fixed;
top: 0; left: 0; right: 0;
z-index: 1000;
background: rgba(2,4,8,0.85);
backdrop-filter: blur(20px);
border-bottom: 1px solid var(–glass-border);
padding: 0 24px;
height: 60px;
display: flex;
align-items: center;
justify-content: space-between;
}

.logo {
font-family: ‘Orbitron’, sans-serif;
font-size: 22px;
font-weight: 900;
background: linear-gradient(135deg, var(–cosmic-cyan), var(–cosmic-purple), var(–nova-pink));
-webkit-background-clip: text;
-webkit-text-fill-color: transparent;
background-clip: text;
letter-spacing: 2px;
display: flex;
align-items: center;
gap: 10px;
}

.logo-icon {
width: 36px;
height: 36px;
border-radius: 50%;
background: linear-gradient(135deg, var(–cosmic-cyan), var(–cosmic-purple));
display: flex;
align-items: center;
justify-content: center;
font-size: 18px;
position: relative;
box-shadow: 0 0 20px rgba(0,212,255,0.4);
animation: orbitGlow 3s ease-in-out infinite;
}

@keyframes orbitGlow {
0%, 100% { box-shadow: 0 0 20px rgba(0,212,255,0.4); }
50% { box-shadow: 0 0 40px rgba(139,92,246,0.6); }
}

.nav-search {
flex: 1;
max-width: 360px;
margin: 0 24px;
position: relative;
}

.nav-search input {
width: 100%;
background: var(–glass);
border: 1px solid var(–glass-border);
border-radius: 24px;
padding: 8px 20px 8px 40px;
color: var(–text-primary);
font-family: ‘Exo 2’, sans-serif;
font-size: 14px;
outline: none;
transition: border-color 0.3s;
}

.nav-search input::placeholder { color: var(–text-muted); }
.nav-search input:focus { border-color: var(–cosmic-cyan); }
.nav-search::before {
content: ‘🔍’;
position: absolute;
left: 14px;
top: 50%;
transform: translateY(-50%);
font-size: 14px;
opacity: 0.5;
}

.nav-actions {
display: flex;
align-items: center;
gap: 8px;
}

.nav-btn {
background: var(–glass);
border: 1px solid var(–glass-border);
border-radius: 12px;
padding: 8px 16px;
color: var(–text-primary);
font-family: ‘Exo 2’, sans-serif;
font-size: 13px;
font-weight: 500;
cursor: pointer;
transition: all 0.3s;
white-space: nowrap;
}

.nav-btn:hover { border-color: var(–cosmic-cyan); color: var(–cosmic-cyan); }
.nav-btn.primary {
background: linear-gradient(135deg, var(–cosmic-cyan), var(–cosmic-purple));
border: none;
color: #fff;
font-weight: 600;
}
.nav-btn.primary:hover { opacity: 0.85; transform: translateY(-1px); }

.avatar-nav {
width: 36px;
height: 36px;
border-radius: 50%;
background: linear-gradient(135deg, var(–cosmic-purple), var(–nova-pink));
display: flex;
align-items: center;
justify-content: center;
font-size: 16px;
cursor: pointer;
border: 2px solid var(–glass-border);
transition: border-color 0.3s;
}
.avatar-nav:hover { border-color: var(–cosmic-cyan); }

/* ─── MAIN LAYOUT ─── */
.page-wrapper {
position: relative;
z-index: 1;
display: grid;
grid-template-columns: 260px 1fr 280px;
gap: 0;
min-height: 100vh;
padding-top: 60px;
}

/* ─── LEFT SIDEBAR ─── */
.sidebar-left {
padding: 20px 16px;
position: sticky;
top: 60px;
height: calc(100vh - 60px);
overflow-y: auto;
border-right: 1px solid var(–glass-border);
}

.sidebar-left::-webkit-scrollbar { width: 4px; }
.sidebar-left::-webkit-scrollbar-thumb { background: var(–glass-border); border-radius: 2px; }

.user-profile-card {
background: var(–glass);
border: 1px solid var(–glass-border);
border-radius: 16px;
padding: 20px;
text-align: center;
margin-bottom: 20px;
position: relative;
overflow: hidden;
}

.profile-banner {
position: absolute;
top: 0; left: 0; right: 0;
height: 60px;
background: linear-gradient(135deg, var(–cosmic-purple), var(–cosmic-cyan));
opacity: 0.4;
}

.profile-avatar-lg {
width: 64px;
height: 64px;
border-radius: 50%;
background: linear-gradient(135deg, var(–cosmic-cyan), var(–nova-pink));
display: flex;
align-items: center;
justify-content: center;
font-size: 28px;
margin: 30px auto 10px;
border: 3px solid var(–void);
position: relative;
box-shadow: 0 0 20px rgba(0,212,255,0.3);
}

.online-dot {
position: absolute;
bottom: 2px; right: 2px;
width: 14px; height: 14px;
background: var(–like-green);
border-radius: 50%;
border: 2px solid var(–void);
}

.user-name {
font-family: ‘Orbitron’, sans-serif;
font-size: 14px;
font-weight: 700;
color: var(–text-primary);
margin-bottom: 4px;
}

.user-handle { font-size: 12px; color: var(–cosmic-cyan); font-family: ‘Space Mono’, monospace; }

.user-stats {
display: grid;
grid-template-columns: 1fr 1fr 1fr;
gap: 8px;
margin-top: 16px;
padding-top: 16px;
border-top: 1px solid var(–glass-border);
}

.stat-item { text-align: center; }
.stat-num { font-family: ‘Orbitron’, sans-serif; font-size: 15px; font-weight: 800; color: var(–cosmic-cyan); }
.stat-label { font-size: 10px; color: var(–text-muted); text-transform: uppercase; letter-spacing: 1px; }

.nav-menu { list-style: none; }
.nav-menu li {
margin-bottom: 4px;
}
.nav-menu a {
display: flex;
align-items: center;
gap: 12px;
padding: 10px 14px;
border-radius: 12px;
color: var(–text-primary);
text-decoration: none;
font-size: 14px;
font-weight: 500;
transition: all 0.2s;
cursor: pointer;
}
.nav-menu a:hover, .nav-menu a.active {
background: var(–glass);
color: var(–cosmic-cyan);
border: 1px solid var(–glass-border);
}
.nav-menu a .icon { font-size: 18px; width: 24px; text-align: center; }

.menu-section-label {
font-size: 10px;
font-weight: 700;
color: var(–text-muted);
text-transform: uppercase;
letter-spacing: 2px;
padding: 16px 14px 6px;
}

/* ─── FEED ─── */
.feed {
padding: 20px 24px;
max-width: 680px;
margin: 0 auto;
width: 100%;
}

/* Create Post */
.create-post {
background: var(–glass);
border: 1px solid var(–glass-border);
border-radius: 20px;
padding: 20px;
margin-bottom: 20px;
backdrop-filter: blur(10px);
}

.create-post-top {
display: flex;
gap: 14px;
align-items: flex-start;
margin-bottom: 14px;
}

.create-post-avatar {
width: 42px; height: 42px;
border-radius: 50%;
background: linear-gradient(135deg, var(–cosmic-cyan), var(–nova-pink));
display: flex;
align-items: center;
justify-content: center;
font-size: 20px;
flex-shrink: 0;
box-shadow: 0 0 15px rgba(0,212,255,0.25);
}

.create-post-input {
flex: 1;
background: rgba(255,255,255,0.06);
border: 1px solid var(–glass-border);
border-radius: 12px;
padding: 12px 16px;
color: var(–text-primary);
font-family: ‘Exo 2’, sans-serif;
font-size: 14px;
resize: none;
outline: none;
min-height: 80px;
transition: border-color 0.3s;
}
.create-post-input::placeholder { color: var(–text-muted); }
.create-post-input:focus { border-color: var(–cosmic-cyan); }

.create-post-actions {
display: flex;
gap: 10px;
align-items: center;
justify-content: space-between;
}

.post-action-btn {
display: flex;
align-items: center;
gap: 6px;
background: none;
border: 1px solid var(–glass-border);
border-radius: 8px;
padding: 6px 12px;
color: var(–text-muted);
font-family: ‘Exo 2’, sans-serif;
font-size: 12px;
cursor: pointer;
transition: all 0.2s;
}
.post-action-btn:hover { border-color: var(–cosmic-cyan); color: var(–cosmic-cyan); }

.post-submit-btn {
background: linear-gradient(135deg, var(–cosmic-cyan), var(–cosmic-purple));
border: none;
border-radius: 10px;
padding: 8px 24px;
color: #fff;
font-family: ‘Orbitron’, sans-serif;
font-size: 12px;
font-weight: 700;
letter-spacing: 1px;
cursor: pointer;
transition: all 0.3s;
box-shadow: 0 0 20px rgba(0,212,255,0.2);
}
.post-submit-btn:hover { transform: translateY(-2px); box-shadow: 0 0 30px rgba(0,212,255,0.4); }

/* ─── POST CARD ─── */
.post-card {
background: var(–glass);
border: 1px solid var(–glass-border);
border-radius: 20px;
padding: 20px;
margin-bottom: 16px;
backdrop-filter: blur(10px);
transition: border-color 0.3s, transform 0.2s;
animation: fadeInUp 0.5s ease both;
}

.post-card:hover {
border-color: rgba(0,212,255,0.3);
transform: translateY(-1px);
}

@keyframes fadeInUp {
from { opacity: 0; transform: translateY(20px); }
to { opacity: 1; transform: translateY(0); }
}

.post-card:nth-child(2) { animation-delay: 0.1s; }
.post-card:nth-child(3) { animation-delay: 0.2s; }
.post-card:nth-child(4) { animation-delay: 0.3s; }
.post-card:nth-child(5) { animation-delay: 0.4s; }

.post-header {
display: flex;
align-items: flex-start;
gap: 12px;
margin-bottom: 14px;
}

.post-avatar {
width: 44px; height: 44px;
border-radius: 50%;
display: flex;
align-items: center;
justify-content: center;
font-size: 20px;
flex-shrink: 0;
position: relative;
border: 2px solid transparent;
}

.post-avatar.verified::after {
content: ‘✦’;
position: absolute;
bottom: -2px; right: -2px;
width: 16px; height: 16px;
background: var(–cosmic-cyan);
border-radius: 50%;
font-size: 8px;
display: flex;
align-items: center;
justify-content: center;
color: var(–void);
border: 2px solid var(–void);
line-height: 12px;
text-align: center;
}

.post-meta { flex: 1; }
.post-author {
font-family: ‘Orbitron’, sans-serif;
font-size: 13px;
font-weight: 700;
color: var(–text-primary);
display: flex;
align-items: center;
gap: 6px;
}

.badge {
font-size: 9px;
padding: 2px 6px;
border-radius: 4px;
font-family: ‘Space Mono’, monospace;
font-weight: 700;
text-transform: uppercase;
letter-spacing: 1px;
}
.badge-trader { background: rgba(251,191,36,0.15); color: var(–solar-gold); border: 1px solid rgba(251,191,36,0.3); }
.badge-marketer { background: rgba(244,114,182,0.15); color: var(–nova-pink); border: 1px solid rgba(244,114,182,0.3); }
.badge-verified { background: rgba(0,212,255,0.15); color: var(–cosmic-cyan); border: 1px solid rgba(0,212,255,0.3); }

.post-time { font-size: 11px; color: var(–text-muted); font-family: ‘Space Mono’, monospace; margin-top: 2px; }
.post-location { font-size: 11px; color: var(–cosmic-purple); }

.post-menu-btn {
background: none;
border: none;
color: var(–text-muted);
cursor: pointer;
padding: 4px 8px;
border-radius: 6px;
font-size: 18px;
transition: all 0.2s;
}
.post-menu-btn:hover { background: var(–glass); color: var(–text-primary); }

.post-content {
font-size: 14px;
line-height: 1.7;
color: var(–text-primary);
margin-bottom: 14px;
}

.post-content .hashtag { color: var(–cosmic-cyan); cursor: pointer; }
.post-content .mention { color: var(–nova-pink); cursor: pointer; }

.post-image {
border-radius: 12px;
overflow: hidden;
margin-bottom: 14px;
border: 1px solid var(–glass-border);
}

.post-image-placeholder {
height: 220px;
display: flex;
align-items: center;
justify-content: center;
font-size: 48px;
position: relative;
overflow: hidden;
}

.cosmos-img-1 {
background: linear-gradient(135deg, #0a0020, #1a0050, #000830, #001040);
background-size: 400% 400%;
animation: cosmosShift 8s ease infinite;
}
.cosmos-img-2 {
background: linear-gradient(135deg, #200010, #500020, #200030, #100040);
background-size: 400% 400%;
animation: cosmosShift 10s ease infinite reverse;
}
.cosmos-img-3 {
background: linear-gradient(135deg, #001020, #002030, #001a40, #000d20);
background-size: 400% 400%;
animation: cosmosShift 6s ease infinite;
}

@keyframes cosmosShift {
0%, 100% { background-position: 0% 50%; }
50% { background-position: 100% 50%; }
}

.post-image-placeholder .img-label {
position: absolute;
bottom: 12px; left: 12px;
background: rgba(0,0,0,0.5);
padding: 4px 10px;
border-radius: 6px;
font-size: 11px;
font-family: ‘Space Mono’, monospace;
color: var(–cosmic-cyan);
}

.market-card {
border: 1px solid rgba(251,191,36,0.25);
border-radius: 12px;
padding: 14px;
margin-bottom: 14px;
background: rgba(251,191,36,0.05);
}

.market-card-label {
font-family: ‘Space Mono’, monospace;
font-size: 10px;
color: var(–solar-gold);
text-transform: uppercase;
letter-spacing: 2px;
margin-bottom: 8px;
}

.market-ticker {
display: flex;
align-items: center;
gap: 16px;
}

.ticker-symbol {
font-family: ‘Orbitron’, sans-serif;
font-size: 18px;
font-weight: 800;
color: var(–text-primary);
}

.ticker-price { font-size: 20px; font-weight: 600; color: var(–solar-gold); }
.ticker-change.up { color: var(–like-green); font-size: 13px; font-family: ‘Space Mono’, monospace; }
.ticker-change.down { color: var(–mars-red); font-size: 13px; font-family: ‘Space Mono’, monospace; }

/* Post Actions */
.post-actions {
display: flex;
align-items: center;
gap: 6px;
padding-top: 14px;
border-top: 1px solid var(–glass-border);
}

.action-btn {
display: flex;
align-items: center;
gap: 6px;
background: none;
border: 1px solid transparent;
border-radius: 10px;
padding: 7px 12px;
color: var(–text-muted);
font-family: ‘Exo 2’, sans-serif;
font-size: 13px;
font-weight: 500;
cursor: pointer;
transition: all 0.2s;
}

.action-btn:hover { border-color: var(–glass-border); background: var(–glass); }

.action-btn.like:hover { color: var(–like-green); border-color: rgba(34,197,94,0.3); background: rgba(34,197,94,0.08); }
.action-btn.like.active { color: var(–like-green); border-color: rgba(34,197,94,0.4); background: rgba(34,197,94,0.1); }

.action-btn.dislike:hover { color: var(–dislike-orange); border-color: rgba(249,115,22,0.3); background: rgba(249,115,22,0.08); }
.action-btn.dislike.active { color: var(–dislike-orange); border-color: rgba(249,115,22,0.4); background: rgba(249,115,22,0.1); }

.action-btn.comment:hover { color: var(–cosmic-cyan); border-color: var(–glass-border); background: var(–glass); }
.action-btn.share:hover { color: var(–cosmic-purple); border-color: rgba(139,92,246,0.3); background: rgba(139,92,246,0.08); }
.action-btn.trade:hover { color: var(–solar-gold); border-color: rgba(251,191,36,0.3); background: rgba(251,191,36,0.08); }

.action-spacer { flex: 1; }

/* ─── RIGHT SIDEBAR ─── */
.sidebar-right {
padding: 20px 16px;
position: sticky;
top: 60px;
height: calc(100vh - 60px);
overflow-y: auto;
border-left: 1px solid var(–glass-border);
}

.sidebar-right::-webkit-scrollbar { width: 4px; }
.sidebar-right::-webkit-scrollbar-thumb { background: var(–glass-border); border-radius: 2px; }

.widget {
background: var(–glass);
border: 1px solid var(–glass-border);
border-radius: 16px;
padding: 16px;
margin-bottom: 16px;
backdrop-filter: blur(10px);
}

.widget-title {
font-family: ‘Orbitron’, sans-serif;
font-size: 11px;
font-weight: 700;
color: var(–cosmic-cyan);
text-transform: uppercase;
letter-spacing: 2px;
margin-bottom: 14px;
display: flex;
align-items: center;
gap: 6px;
}

/* Live Chat Widget */
.chat-list { list-style: none; }
.chat-item {
display: flex;
align-items: center;
gap: 10px;
padding: 8px 0;
cursor: pointer;
border-radius: 8px;
padding-left: 4px;
transition: background 0.2s;
}
.chat-item:hover { background: rgba(255,255,255,0.04); }

.chat-avatar {
width: 36px; height: 36px;
border-radius: 50%;
display: flex;
align-items: center;
justify-content: center;
font-size: 16px;
flex-shrink: 0;
position: relative;
}

.chat-online::after {
content: ‘’;
position: absolute;
bottom: 0; right: 0;
width: 10px; height: 10px;
background: var(–like-green);
border-radius: 50%;
border: 2px solid var(–void);
}

.chat-info { flex: 1; min-width: 0; }
.chat-name { font-size: 13px; font-weight: 600; color: var(–text-primary); white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.chat-preview { font-size: 11px; color: var(–text-muted); white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.chat-time { font-size: 10px; color: var(–text-muted); font-family: ‘Space Mono’, monospace; }

/* Trending */
.trend-item {
padding: 8px 0;
border-bottom: 1px solid rgba(255,255,255,0.04);
cursor: pointer;
transition: padding-left 0.2s;
}
.trend-item:hover { padding-left: 4px; }
.trend-item:last-child { border-bottom: none; }
.trend-num { font-size: 10px; color: var(–text-muted); font-family: ‘Space Mono’, monospace; }
.trend-tag { font-size: 13px; font-weight: 600; color: var(–cosmic-cyan); }
.trend-count { font-size: 11px; color: var(–text-muted); }

/* Market Widget */
.market-row {
display: flex;
align-items: center;
justify-content: space-between;
padding: 8px 0;
border-bottom: 1px solid rgba(255,255,255,0.04);
cursor: pointer;
}
.market-row:last-child { border-bottom: none; }
.market-row-sym { font-family: ‘Orbitron’, sans-serif; font-size: 12px; font-weight: 700; color: var(–text-primary); }
.market-row-name { font-size: 11px; color: var(–text-muted); }
.market-row-price { font-size: 13px; font-weight: 600; color: var(–solar-gold); text-align: right; }
.market-row-change { font-size: 11px; font-family: ‘Space Mono’, monospace; }
.green { color: var(–like-green); }
.red { color: var(–mars-red); }

/* People to Connect */
.suggest-item {
display: flex;
align-items: center;
gap: 10px;
padding: 8px 0;
}

.suggest-avatar {
width: 40px; height: 40px;
border-radius: 50%;
display: flex;
align-items: center;
justify-content: center;
font-size: 18px;
flex-shrink: 0;
border: 2px solid transparent;
}

.suggest-info { flex: 1; min-width: 0; }
.suggest-name { font-size: 13px; font-weight: 600; color: var(–text-primary); white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
.suggest-meta { font-size: 11px; color: var(–text-muted); }

.connect-btn {
background: none;
border: 1px solid var(–cosmic-cyan);
border-radius: 8px;
padding: 5px 12px;
color: var(–cosmic-cyan);
font-family: ‘Exo 2’, sans-serif;
font-size: 11px;
font-weight: 600;
cursor: pointer;
transition: all 0.2s;
flex-shrink: 0;
}
.connect-btn:hover { background: rgba(0,212,255,0.1); }
.connect-btn.connected { background: rgba(0,212,255,0.15); border-color: transparent; color: var(–cosmic-cyan); }

/* LIVE chat window */
.chat-window {
position: fixed;
bottom: 20px;
right: 20px;
width: 320px;
background: rgba(5,13,26,0.95);
border: 1px solid var(–glass-border);
border-radius: 16px;
overflow: hidden;
backdrop-filter: blur(20px);
z-index: 999;
box-shadow: 0 20px 60px rgba(0,0,0,0.5);
display: none;
flex-direction: column;
height: 420px;
}

.chat-window.open { display: flex; animation: slideUp 0.3s ease; }

@keyframes slideUp {
from { transform: translateY(30px); opacity: 0; }
to { transform: translateY(0); opacity: 1; }
}

.chat-window-header {
display: flex;
align-items: center;
gap: 10px;
padding: 14px 16px;
background: linear-gradient(135deg, rgba(0,212,255,0.1), rgba(139,92,246,0.1));
border-bottom: 1px solid var(–glass-border);
cursor: pointer;
}

.chat-window-name { font-family: ‘Orbitron’, sans-serif; font-size: 13px; font-weight: 700; flex: 1; }
.chat-close-btn { background: none; border: none; color: var(–text-muted); cursor: pointer; font-size: 18px; line-height: 1; }
.chat-close-btn:hover { color: var(–text-primary); }

.chat-messages {
flex: 1;
overflow-y: auto;
padding: 14px;
display: flex;
flex-direction: column;
gap: 10px;
}
.chat-messages::-webkit-scrollbar { width: 4px; }
.chat-messages::-webkit-scrollbar-thumb { background: var(–glass-border); }

.msg { max-width: 80%; }
.msg.received { align-self: flex-start; }
.msg.sent { align-self: flex-end; }

.msg-bubble {
padding: 8px 12px;
border-radius: 12px;
font-size: 13px;
line-height: 1.5;
}

.msg.received .msg-bubble {
background: var(–glass);
border: 1px solid var(–glass-border);
color: var(–text-primary);
border-radius: 4px 12px 12px 12px;
}

.msg.sent .msg-bubble {
background: linear-gradient(135deg, rgba(0,212,255,0.2), rgba(139,92,246,0.2));
border: 1px solid rgba(0,212,255,0.3);
color: var(–text-primary);
border-radius: 12px 4px 12px 12px;
}

.msg-time { font-size: 10px; color: var(–text-muted); margin-top: 3px; font-family: ‘Space Mono’, monospace; }
.msg.sent .msg-time { text-align: right; }

.chat-input-row {
display: flex;
gap: 8px;
padding: 12px 14px;
border-top: 1px solid var(–glass-border);
}

.chat-input {
flex: 1;
background: var(–glass);
border: 1px solid var(–glass-border);
border-radius: 10px;
padding: 8px 12px;
color: var(–text-primary);
font-family: ‘Exo 2’, sans-serif;
font-size: 13px;
outline: none;
}
.chat-input::placeholder { color: var(–text-muted); }

.chat-send-btn {
background: linear-gradient(135deg, var(–cosmic-cyan), var(–cosmic-purple));
border: none;
border-radius: 10px;
width: 36px;
height: 36px;
cursor: pointer;
display: flex;
align-items: center;
justify-content: center;
font-size: 16px;
transition: all 0.2s;
}
.chat-send-btn:hover { transform: scale(1.05); }

/* Toast */
.toast {
position: fixed;
bottom: 30px;
left: 50%;
transform: translateX(-50%) translateY(60px);
background: rgba(5,13,26,0.95);
border: 1px solid var(–cosmic-cyan);
border-radius: 12px;
padding: 10px 20px;
font-size: 13px;
color: var(–cosmic-cyan);
z-index: 2000;
transition: transform 0.3s ease;
backdrop-filter: blur(10px);
white-space: nowrap;
}
.toast.show { transform: translateX(-50%) translateY(0); }

/* Story/Loop bar */
.loops-bar {
display: flex;
gap: 14px;
overflow-x: auto;
padding-bottom: 8px;
margin-bottom: 20px;
scrollbar-width: none;
}
.loops-bar::-webkit-scrollbar { display: none; }

.loop-item {
display: flex;
flex-direction: column;
align-items: center;
gap: 6px;
cursor: pointer;
flex-shrink: 0;
}

.loop-ring {
width: 56px; height: 56px;
border-radius: 50%;
padding: 2px;
background: linear-gradient(135deg, var(–cosmic-cyan), var(–cosmic-purple), var(–nova-pink));
transition: transform 0.2s;
}
.loop-ring:hover { transform: scale(1.08); }

.loop-inner {
width: 100%; height: 100%;
border-radius: 50%;
border: 2px solid var(–void);
background: var(–nebula-blue);
display: flex;
align-items: center;
justify-content: center;
font-size: 22px;
}

.loop-name { font-size: 11px; color: var(–text-muted); text-align: center; max-width: 60px; overflow: hidden; text-overflow: ellipsis; white-space: nowrap; }

.add-loop-ring {
width: 56px; height: 56px;
border-radius: 50%;
border: 2px dashed var(–glass-border);
display: flex;
align-items: center;
justify-content: center;
font-size: 24px;
color: var(–text-muted);
cursor: pointer;
transition: all 0.2s;
}
.add-loop-ring:hover { border-color: var(–cosmic-cyan); color: var(–cosmic-cyan); }

/* Notification badge */
.notif-badge {
background: var(–mars-red);
color: #fff;
font-size: 10px;
font-weight: 700;
padding: 2px 5px;
border-radius: 10px;
min-width: 18px;
text-align: center;
font-family: ‘Space Mono’, monospace;
}

@media (max-width: 900px) {
.page-wrapper { grid-template-columns: 60px 1fr; }
.sidebar-right { display: none; }
.nav-search { display: none; }
.sidebar-left { padding: 12px 8px; }
.user-profile-card { display: none; }
.nav-menu a span.label { display: none; }
.menu-section-label { display: none; }
}
</style>

</head>
<body>

<div class="nebula-bg"></div>
<canvas id="starfield"></canvas>

<!-- NAV -->

<nav>
  <div class="logo">
    <div class="logo-icon">🌐</div>
    GLOBALLOOP
  </div>

  <div class="nav-search">
    <input type="text" placeholder="Search the universe…" id="searchInput">
  </div>

  <div class="nav-actions">
    <button class="nav-btn" onclick="showToast('🌌 Exploring…')">🌌 Explore</button>
    <button class="nav-btn" onclick="showToast('💹 Markets coming soon!')">💹 Trade</button>
    <button class="nav-btn" onclick="openChat()">💬 Chat <span class="notif-badge">3</span></button>
    <button class="nav-btn">🔔 <span class="notif-badge">7</span></button>
    <div class="avatar-nav" onclick="showToast('👨‍🚀 Your profile')">👨‍🚀</div>
  </div>
</nav>

<!-- LAYOUT -->

<div class="page-wrapper">

  <!-- LEFT SIDEBAR -->

  <aside class="sidebar-left">
    <div class="user-profile-card">
      <div class="profile-banner"></div>
      <div class="profile-avatar-lg">👨‍🚀<div class="online-dot"></div></div>
      <div class="user-name">AstroUser</div>
      <div class="user-handle">@astro_loop</div>
      <div class="user-stats">
        <div class="stat-item">
          <div class="stat-num">1.2K</div>
          <div class="stat-label">Links</div>
        </div>
        <div class="stat-item">
          <div class="stat-num">847</div>
          <div class="stat-label">Loops</div>
        </div>
        <div class="stat-item">
          <div class="stat-num">43</div>
          <div class="stat-label">Trades</div>
        </div>
      </div>
    </div>

```
<ul class="nav-menu">
  <li><a class="active" onclick="showToast('🏠 Home')">
    <span class="icon">🏠</span><span class="label">Home Feed</span>
  </a></li>
  <li><a onclick="showToast('👤 Profile')">
    <span class="icon">👤</span><span class="label">My Profile</span>
  </a></li>
  <li><a onclick="openChat()">
    <span class="icon">💬</span><span class="label">Messages</span>
    <span class="notif-badge" style="margin-left:auto">3</span>
  </a></li>
  <li><a onclick="showToast('🌐 Global Groups')">
    <span class="icon">🌐</span><span class="label">Global Groups</span>
  </a></li>
  <li><a onclick="showToast('🌌 Loops (Stories)')">
    <span class="icon">🌌</span><span class="label">Loops</span>
  </a></li>

  <div class="menu-section-label">Commerce</div>
  <li><a onclick="showToast('💹 Trading Hub')">
    <span class="icon">💹</span><span class="label">Trading Hub</span>
  </a></li>
  <li><a onclick="showToast('📣 Marketing')">
    <span class="icon">📣</span><span class="label">Marketing</span>
  </a></li>
  <li><a onclick="showToast('🛸 Marketplace')">
    <span class="icon">🛸</span><span class="label">Marketplace</span>
  </a></li>

  <div class="menu-section-label">Discover</div>
  <li><a onclick="showToast('🌠 Trending')">
    <span class="icon">🌠</span><span class="label">Trending</span>
  </a></li>
  <li><a onclick="showToast('📡 Live Streams')">
    <span class="icon">📡</span><span class="label">Live Streams</span>
  </a></li>
  <li><a onclick="showToast('⚙️ Settings')">
    <span class="icon">⚙️</span><span class="label">Settings</span>
  </a></li>
</ul>
```

  </aside>

  <!-- FEED -->

  <main class="feed">

```
<!-- Loops bar -->
<div class="loops-bar">
  <div class="loop-item">
    <div class="add-loop-ring" onclick="showToast('➕ Create a Loop!')">+</div>
    <span class="loop-name">Your Loop</span>
  </div>
  <div class="loop-item" onclick="showToast('👩‍🚀 NovaStar loop')">
    <div class="loop-ring"><div class="loop-inner">👩‍🚀</div></div>
    <span class="loop-name">NovaStar</span>
  </div>
  <div class="loop-item" onclick="showToast('🤖 CryptoBot loop')">
    <div class="loop-ring"><div class="loop-inner">🤖</div></div>
    <span class="loop-name">CryptoBot</span>
  </div>
  <div class="loop-item" onclick="showToast('🌍 EarthVibes loop')">
    <div class="loop-ring"><div class="loop-inner">🌍</div></div>
    <span class="loop-name">EarthVibes</span>
  </div>
  <div class="loop-item" onclick="showToast('🔭 StarGazer loop')">
    <div class="loop-ring"><div class="loop-inner">🔭</div></div>
    <span class="loop-name">StarGazer</span>
  </div>
  <div class="loop-item" onclick="showToast('💫 GalaxyCeo loop')">
    <div class="loop-ring"><div class="loop-inner">💫</div></div>
    <span class="loop-name">GalaxyCeo</span>
  </div>
  <div class="loop-item" onclick="showToast('🛸 AliensExist loop')">
    <div class="loop-ring"><div class="loop-inner">🛸</div></div>
    <span class="loop-name">AliensExist</span>
  </div>
</div>

<!-- Create Post -->
<div class="create-post">
  <div class="create-post-top">
    <div class="create-post-avatar">👨‍🚀</div>
    <textarea class="create-post-input" id="newPostText" placeholder="What's looping in the universe today? Share with the world…"></textarea>
  </div>
  <div class="create-post-actions">
    <button class="post-action-btn" onclick="showToast('📸 Photo upload coming soon!')">📸 Photo</button>
    <button class="post-action-btn" onclick="showToast('📡 Live Stream coming soon!')">📡 Live</button>
    <button class="post-action-btn" onclick="showToast('💹 Share Trade!')">💹 Trade</button>
    <button class="post-action-btn" onclick="showToast('📣 Boost Post')">📣 Boost</button>
    <button class="post-submit-btn" onclick="submitPost()">LAUNCH 🚀</button>
  </div>
</div>

<!-- Post Feed -->
<div id="postFeed">

  <!-- Post 1 -->
  <div class="post-card">
    <div class="post-header">
      <div class="post-avatar verified" style="background: linear-gradient(135deg,#0a1628,#1a0a2e); border-color: var(--cosmic-cyan);">🌌</div>
      <div class="post-meta">
        <div class="post-author">NebulaCorp Official <span class="badge badge-verified">✦ Verified</span><span class="badge badge-marketer">Marketing</span></div>
        <div class="post-time">2 minutes ago</div>
        <div class="post-location">🌏 Global Broadcast</div>
      </div>
      <button class="post-menu-btn">⋯</button>
    </div>
    <div class="post-content">
      Excited to announce our new global expansion into 47 new markets! 🚀 The universe is our playground. Join us as we connect every corner of the cosmos. <span class="hashtag">#GlobalLoop</span> <span class="hashtag">#Expansion</span> <span class="mention">@GlobalLoopUsers</span>
    </div>
    <div class="post-image">
      <div class="post-image-placeholder cosmos-img-1">
        🌌
        <div class="img-label">🌌 Nebula Campaign 2025</div>
      </div>
    </div>
    <div class="post-actions">
      <button class="action-btn like" onclick="toggleReaction(this,'like')">👍 Like <span class="count">2.4K</span></button>
      <button class="action-btn dislike" onclick="toggleReaction(this,'dislike')">👎 Dislike <span class="count">89</span></button>
      <button class="action-btn comment" onclick="showToast('💬 Comments open!')">💬 <span class="count">341</span></button>
      <div class="action-spacer"></div>
      <button class="action-btn share" onclick="showToast('🔗 Link copied to clipboard!')">🔗 Share</button>
      <button class="action-btn trade" onclick="showToast('💹 View trade post!')">💹 Trade</button>
    </div>
  </div>

  <!-- Post 2 — Trade post -->
  <div class="post-card">
    <div class="post-header">
      <div class="post-avatar" style="background: linear-gradient(135deg,#1a0a00,#2e1500); border-color: var(--solar-gold);">📈</div>
      <div class="post-meta">
        <div class="post-author">CosmicTrader_X <span class="badge badge-trader">Trader</span></div>
        <div class="post-time">18 minutes ago</div>
        <div class="post-location">💹 Trading Hub</div>
      </div>
      <button class="post-menu-btn">⋯</button>
    </div>
    <div class="post-content">
      Just closed a massive position on $GLBL 🔥 Galaxy sector is heating up. If you missed the entry at 42.50, there's still time — next support is at 39.80. Do your own research! <span class="hashtag">#Crypto</span> <span class="hashtag">#Trading</span> <span class="hashtag">#GlobalLoop</span>
    </div>
    <div class="market-card">
      <div class="market-card-label">📊 Live Position Shared</div>
      <div class="market-ticker">
        <div>
          <div class="ticker-symbol">$GLBL</div>
          <div style="font-size:11px;color:var(--text-muted)">GlobalLoop Token</div>
        </div>
        <div>
          <div class="ticker-price">$47.23</div>
          <div class="ticker-change up">▲ +11.2% (24h)</div>
        </div>
      </div>
    </div>
    <div class="post-actions">
      <button class="action-btn like" onclick="toggleReaction(this,'like')">👍 Like <span class="count">1.1K</span></button>
      <button class="action-btn dislike" onclick="toggleReaction(this,'dislike')">👎 Dislike <span class="count">234</span></button>
      <button class="action-btn comment" onclick="showToast('💬 Comments open!')">💬 <span class="count">88</span></button>
      <div class="action-spacer"></div>
      <button class="action-btn share" onclick="showToast('🔗 Shared!')">🔗 Share</button>
      <button class="action-btn trade" onclick="showToast('💹 Copy Trade opened!')">💹 Copy Trade</button>
    </div>
  </div>

  <!-- Post 3 -->
  <div class="post-card">
    <div class="post-header">
      <div class="post-avatar" style="background: linear-gradient(135deg,#0a0020,#200040); border-color: var(--nova-pink);">👩‍🚀</div>
      <div class="post-meta">
        <div class="post-author">NovaStar_Luna</div>
        <div class="post-time">1 hour ago</div>
        <div class="post-location">🇯🇵 Tokyo, Japan</div>
      </div>
      <button class="post-menu-btn">⋯</button>
    </div>
    <div class="post-content">
      The night sky here in Tokyo reminds me why I joined GlobalLoop — connecting with minds across the cosmos from a rooftop in Shibuya. The universe really is one giant conversation. 🌠✨ <span class="hashtag">#CosmicConnection</span> <span class="hashtag">#GlobalLoop</span>
    </div>
    <div class="post-image">
      <div class="post-image-placeholder cosmos-img-2">
        🌠
        <div class="img-label">📍 Shibuya, Tokyo · Night</div>
      </div>
    </div>
    <div class="post-actions">
      <button class="action-btn like" onclick="toggleReaction(this,'like')">👍 Like <span class="count">6.7K</span></button>
      <button class="action-btn dislike" onclick="toggleReaction(this,'dislike')">👎 Dislike <span class="count">12</span></button>
      <button class="action-btn comment" onclick="showToast('💬 Join the conversation!')">💬 <span class="count">512</span></button>
      <div class="action-spacer"></div>
      <button class="action-btn share" onclick="showToast('🔗 Shared!')">🔗 Share</button>
    </div>
  </div>

  <!-- Post 4 -->
  <div class="post-card">
    <div class="post-header">
      <div class="post-avatar" style="background: linear-gradient(135deg,#001020,#002040); border-color: var(--cosmic-cyan);">🔭</div>
      <div class="post-meta">
        <div class="post-author">StarGazer_Pro <span class="badge badge-verified">✦ Verified</span></div>
        <div class="post-time">3 hours ago</div>
        <div class="post-location">🌍 Earth Orbit Station</div>
      </div>
      <button class="post-menu-btn">⋯</button>
    </div>
    <div class="post-content">
      Breaking: New exoplanet cluster discovered 400 light-years away — atmospheric data suggests water vapor! 🌊 This changes everything we know about habitable zones. Full report drops tomorrow. <span class="hashtag">#Science</span> <span class="hashtag">#Space</span> <span class="hashtag">#Discovery</span>
    </div>
    <div class="post-image">
      <div class="post-image-placeholder cosmos-img-3">
        🪐
        <div class="img-label">🔭 Exoplanet K2-18c · Artist Render</div>
      </div>
    </div>
    <div class="post-actions">
      <button class="action-btn like" onclick="toggleReaction(this,'like')">👍 Like <span class="count">89.2K</span></button>
      <button class="action-btn dislike" onclick="toggleReaction(this,'dislike')">👎 Dislike <span class="count">1.4K</span></button>
      <button class="action-btn comment" onclick="showToast('💬 Mind = blown!')">💬 <span class="count">14.2K</span></button>
      <div class="action-spacer"></div>
      <button class="action-btn share" onclick="showToast('🔗 Shared across the galaxy!')">🔗 Share</button>
    </div>
  </div>

</div><!-- end postFeed -->
```

  </main>

  <!-- RIGHT SIDEBAR -->

  <aside class="sidebar-right">

```
<!-- People to Connect -->
<div class="widget">
  <div class="widget-title">👥 Connect Now</div>
  <div class="suggest-item">
    <div class="suggest-avatar" style="background: linear-gradient(135deg,#002040,#004080);">🌍</div>
    <div class="suggest-info">
      <div class="suggest-name">EarthVibes</div>
      <div class="suggest-meta">🌐 Lagos · 12K loops</div>
    </div>
    <button class="connect-btn" onclick="toggleConnect(this)">+ Link</button>
  </div>
  <div class="suggest-item">
    <div class="suggest-avatar" style="background: linear-gradient(135deg,#200010,#400020);">🤖</div>
    <div class="suggest-info">
      <div class="suggest-name">CryptoBot_9</div>
      <div class="suggest-meta">💹 Trader · 45K loops</div>
    </div>
    <button class="connect-btn" onclick="toggleConnect(this)">+ Link</button>
  </div>
  <div class="suggest-item">
    <div class="suggest-avatar" style="background: linear-gradient(135deg,#001a00,#003000);">💫</div>
    <div class="suggest-info">
      <div class="suggest-name">GalaxyCeo</div>
      <div class="suggest-meta">📣 Marketer · 8.2K loops</div>
    </div>
    <button class="connect-btn" onclick="toggleConnect(this)">+ Link</button>
  </div>
  <div class="suggest-item">
    <div class="suggest-avatar" style="background: linear-gradient(135deg,#1a1a00,#303000);">🛸</div>
    <div class="suggest-info">
      <div class="suggest-name">AliensExist</div>
      <div class="suggest-meta">🌌 Researcher · 3.1K loops</div>
    </div>
    <button class="connect-btn" onclick="toggleConnect(this)">+ Link</button>
  </div>
</div>

<!-- Live Chat -->
<div class="widget">
  <div class="widget-title">💬 Live Connections</div>
  <ul class="chat-list">
    <li class="chat-item" onclick="openChat('NovaStar_Luna')">
      <div class="chat-avatar chat-online" style="background:linear-gradient(135deg,#0a0020,#200040);">👩‍🚀</div>
      <div class="chat-info">
        <div class="chat-name">NovaStar_Luna</div>
        <div class="chat-preview">Just posted about Tokyo 🌠</div>
      </div>
      <div class="chat-time">2m</div>
    </li>
    <li class="chat-item" onclick="openChat('CosmicTrader')">
      <div class="chat-avatar chat-online" style="background:linear-gradient(135deg,#1a0a00,#2e1500);">📈</div>
      <div class="chat-info">
        <div class="chat-name">CosmicTrader_X</div>
        <div class="chat-preview">GLBL still looking bullish 📈</div>
      </div>
      <div class="chat-time">15m</div>
    </li>
    <li class="chat-item" onclick="openChat('StarGazer')">
      <div class="chat-avatar" style="background:linear-gradient(135deg,#001020,#002040);">🔭</div>
      <div class="chat-info">
        <div class="chat-name">StarGazer_Pro</div>
        <div class="chat-preview">Report drops tomorrow!</div>
      </div>
      <div class="chat-time">1h</div>
    </li>
    <li class="chat-item" onclick="openChat('EarthVibes')">
      <div class="chat-avatar chat-online" style="background:linear-gradient(135deg,#002040,#004080);">🌍</div>
      <div class="chat-info">
        <div class="chat-name">EarthVibes</div>
        <div class="chat-preview">You there? 👋</div>
      </div>
      <div class="chat-time">3h</div>
    </li>
  </ul>
</div>

<!-- Trending -->
<div class="widget">
  <div class="widget-title">🌠 Trending Loops</div>
  <div class="trend-item" onclick="showToast('#GlobalLoop is trending!')">
    <div class="trend-num">01</div>
    <div class="trend-tag">#GlobalLoop</div>
    <div class="trend-count">842K loops</div>
  </div>
  <div class="trend-item" onclick="showToast('#CosmicTrade trending!')">
    <div class="trend-num">02</div>
    <div class="trend-tag">#CosmicTrade</div>
    <div class="trend-count">241K loops</div>
  </div>
  <div class="trend-item" onclick="showToast('#SpaceDiscovery trending!')">
    <div class="trend-num">03</div>
    <div class="trend-tag">#SpaceDiscovery</div>
    <div class="trend-count">119K loops</div>
  </div>
  <div class="trend-item" onclick="showToast('#NebulaCorp trending!')">
    <div class="trend-num">04</div>
    <div class="trend-tag">#NebulaCorp</div>
    <div class="trend-count">88K loops</div>
  </div>
  <div class="trend-item" onclick="showToast('#MilkyWayMarket trending!')">
    <div class="trend-num">05</div>
    <div class="trend-tag">#MilkyWayMarket</div>
    <div class="trend-count">55K loops</div>
  </div>
</div>

<!-- Market -->
<div class="widget">
  <div class="widget-title">💹 Live Markets</div>
  <div class="market-row" onclick="showToast('$GLBL — GlobalLoop Token')">
    <div>
      <div class="market-row-sym">$GLBL</div>
      <div class="market-row-name">GlobalLoop</div>
    </div>
    <div>
      <div class="market-row-price">$47.23</div>
      <div class="market-row-change green">▲ +11.2%</div>
    </div>
  </div>
  <div class="market-row" onclick="showToast('$NOVA — NovaCoin')">
    <div>
      <div class="market-row-sym">$NOVA</div>
      <div class="market-row-name">NovaCoin</div>
    </div>
    <div>
      <div class="market-row-price">$12.80</div>
      <div class="market-row-change red">▼ -2.4%</div>
    </div>
  </div>
  <div class="market-row" onclick="showToast('$STAR — StarAsset')">
    <div>
      <div class="market-row-sym">$STAR</div>
      <div class="market-row-name">StarAsset</div>
    </div>
    <div>
      <div class="market-row-price">$3.14</div>
      <div class="market-row-change green">▲ +5.9%</div>
    </div>
  </div>
  <div class="market-row" onclick="showToast('$ORBT — OrbitCoin')">
    <div>
      <div class="market-row-sym">$ORBT</div>
      <div class="market-row-name">OrbitCoin</div>
    </div>
    <div>
      <div class="market-row-price">$0.88</div>
      <div class="market-row-change red">▼ -0.7%</div>
    </div>
  </div>
</div>
```

  </aside>
</div>

<!-- CHAT WINDOW -->

<div class="chat-window" id="chatWindow">
  <div class="chat-window-header" onclick="closeChat()">
    <div class="chat-avatar" style="background:linear-gradient(135deg,#0a0020,#200040);font-size:16px;">👩‍🚀</div>
    <div class="chat-window-name" id="chatWindowName">NovaStar_Luna</div>
    <div style="font-size:10px;color:var(--like-green);font-family:'Space Mono',monospace;">● ONLINE</div>
    <button class="chat-close-btn" onclick="closeChat()">✕</button>
  </div>
  <div class="chat-messages" id="chatMessages">
    <div class="msg received">
      <div class="msg-bubble">Hey! Did you see the Tokyo post? 🌠</div>
      <div class="msg-time">2m ago</div>
    </div>
    <div class="msg sent">
      <div class="msg-bubble">Yes! Amazing shot, love it 🚀</div>
      <div class="msg-time">1m ago</div>
    </div>
    <div class="msg received">
      <div class="msg-bubble">Thanks! GlobalLoop connecting us all 🌌</div>
      <div class="msg-time">Just now</div>
    </div>
  </div>
  <div class="chat-input-row">
    <input class="chat-input" id="chatInput" placeholder="Message across the universe…" onkeypress="handleChatKey(event)">
    <button class="chat-send-btn" onclick="sendMessage()">➤</button>
  </div>
</div>

<!-- TOAST -->

<div class="toast" id="toast"></div>

<script>
// Starfield
const canvas = document.getElementById('starfield');
const ctx = canvas.getContext('2d');
let stars = [];

function resizeCanvas() {
  canvas.width = window.innerWidth;
  canvas.height = window.innerHeight;
}

function createStars() {
  stars = [];
  for (let i = 0; i < 300; i++) {
    stars.push({
      x: Math.random() * canvas.width,
      y: Math.random() * canvas.height,
      r: Math.random() * 1.5 + 0.2,
      alpha: Math.random() * 0.8 + 0.2,
      speed: Math.random() * 0.3 + 0.05,
      twinkle: Math.random() * Math.PI * 2,
      twinkleSpeed: Math.random() * 0.03 + 0.01
    });
  }
}

function drawStars() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  stars.forEach(s => {
    s.twinkle += s.twinkleSpeed;
    const a = s.alpha * (0.6 + 0.4 * Math.sin(s.twinkle));
    ctx.beginPath();
    ctx.arc(s.x, s.y, s.r, 0, Math.PI * 2);
    ctx.fillStyle = `rgba(232,240,255,${a})`;
    ctx.fill();
    s.y += s.speed;
    if (s.y > canvas.height) { s.y = 0; s.x = Math.random() * canvas.width; }
  });
  requestAnimationFrame(drawStars);
}

resizeCanvas(); createStars(); drawStars();
window.addEventListener('resize', () => { resizeCanvas(); createStars(); });

// Toast
let toastTimer;
function showToast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  clearTimeout(toastTimer);
  toastTimer = setTimeout(() => t.classList.remove('show'), 2500);
}

// Reactions
function toggleReaction(btn, type) {
  const countEl = btn.querySelector('.count');
  const raw = countEl.textContent.replace(/[KM]/g,'');
  let num = parseFloat(raw);
  const suffix = countEl.textContent.includes('K') ? 'K' : countEl.textContent.includes('M') ? 'M' : '';

  if (btn.classList.contains('active')) {
    btn.classList.remove('active');
    num -= 1;
    showToast(type === 'like' ? '👍 Like removed' : '👎 Dislike removed');
  } else {
    // deactivate sibling
    const siblings = btn.parentElement.querySelectorAll('.action-btn.' + (type === 'like' ? 'dislike' : 'like'));
    siblings.forEach(s => {
      if (s.classList.contains('active')) {
        s.classList.remove('active');
        const sc = s.querySelector('.count');
        const sn = parseFloat(sc.textContent) - 1;
        sc.textContent = sn + (sc.textContent.includes('K') ? 'K' : '');
      }
    });
    btn.classList.add('active');
    num += 1;
    showToast(type === 'like' ? '👍 Liked!' : '👎 Disliked!');
  }
  countEl.textContent = num.toFixed(num % 1 === 0 ? 0 : 1) + suffix;
}

// Connect
function toggleConnect(btn) {
  if (btn.textContent.trim() === '+ Link') {
    btn.textContent = '✓ Linked';
    btn.classList.add('connected');
    showToast('🌐 Linked across the universe!');
  } else {
    btn.textContent = '+ Link';
    btn.classList.remove('connected');
    showToast('🔗 Unlinked');
  }
}

// Chat
let chatOpen = false;
function openChat(name) {
  const win = document.getElementById('chatWindow');
  const nameEl = document.getElementById('chatWindowName');
  if (name) nameEl.textContent = name;
  win.classList.add('open');
  chatOpen = true;
}
function closeChat() {
  document.getElementById('chatWindow').classList.remove('open');
  chatOpen = false;
}
function sendMessage() {
  const input = document.getElementById('chatInput');
  const text = input.value.trim();
  if (!text) return;
  const msgs = document.getElementById('chatMessages');
  const div = document.createElement('div');
  div.className = 'msg sent';
  div.innerHTML = `<div class="msg-bubble">${text}</div><div class="msg-time">Just now</div>`;
  msgs.appendChild(div);
  input.value = '';
  msgs.scrollTop = msgs.scrollHeight;

  setTimeout(() => {
    const replies = [
      'Signals received across the cosmos! 🌌',
      'Connecting the universe, one loop at a time 🚀',
      'That resonates through the galaxy ✨',
      'GlobalLoop bringing worlds together! 🌍',
      'Transmission confirmed 📡'
    ];
    const reply = document.createElement('div');
    reply.className = 'msg received';
    reply.innerHTML = `<div class="msg-bubble">${replies[Math.floor(Math.random()*replies.length)]}</div><div class="msg-time">Just now</div>`;
    msgs.appendChild(reply);
    msgs.scrollTop = msgs.scrollHeight;
  }, 1200);
}
function handleChatKey(e) { if (e.key === 'Enter') sendMessage(); }

// Submit post
function submitPost() {
  const text = document.getElementById('newPostText').value.trim();
  if (!text) { showToast('✍️ Write something to launch!'); return; }
  const feed = document.getElementById('postFeed');
  const card = document.createElement('div');
  card.className = 'post-card';
  card.style.animationDelay = '0s';
  card.innerHTML = `
    <div class="post-header">
      <div class="post-avatar" style="background:linear-gradient(135deg,var(--cosmic-cyan),var(--nova-pink));">👨‍🚀</div>
      <div class="post-meta">
        <div class="post-author">AstroUser <span class="badge badge-verified">✦ You</span></div>
        <div class="post-time">Just now</div>
        <div class="post-location">🌌 GlobalLoop</div>
      </div>
      <button class="post-menu-btn">⋯</button>
    </div>
    <div class="post-content">${text.replace(/(#\w+)/g,'<span class="hashtag">$1</span>').replace(/(@\w+)/g,'<span class="mention">$1</span>')}</div>
    <div class="post-actions">
      <button class="action-btn like" onclick="toggleReaction(this,'like')">👍 Like <span class="count">0</span></button>
      <button class="action-btn dislike" onclick="toggleReaction(this,'dislike')">👎 Dislike <span class="count">0</span></button>
      <button class="action-btn comment" onclick="showToast('💬 Comments!')">💬 <span class="count">0</span></button>
      <div class="action-spacer"></div>
      <button class="action-btn share" onclick="showToast('🔗 Shared!')">🔗 Share</button>
    </div>
  `;
  feed.insertBefore(card, feed.firstChild);
  document.getElementById('newPostText').value = '';
  showToast('🚀 Post launched into the universe!');
}
</script>

</body>
</html>
