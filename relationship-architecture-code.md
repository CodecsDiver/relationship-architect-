# Daniel & Veronica's Relationship Architecture
## Prototype 1 — Full Source Code
## Generated: July 4, 2026

---

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Daniel &amp; Veronica's Relationship Architecture</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;0,600;1,300;1,400&family=JetBrains+Mono:wght@300;400;500&display=swap">
<style>
  :root {
    --bg: #060B14; --bg-panel: #08101E; --gold: #C9A451; --rose: #D4847A;
    --text: #E8DECE; --text-dim: rgba(232,222,206,0.4); --border: rgba(201,164,81,0.12);
    --topbar-bg: rgba(6,11,20,0.98);
  }
  * { box-sizing: border-box; }
  html, body { margin: 0; height: 100%; background: var(--bg); color: var(--text); font-family: 'Cormorant Garamond', Georgia, serif; overflow: hidden; }
  #app { display: flex; flex-direction: column; height: 100vh; }

  /* ── Top bar ── */
  #topbar { display: flex; align-items: center; gap: 14px; padding: 0 20px; height: 56px; background: var(--topbar-bg); border-bottom: 1px solid var(--border); flex-shrink: 0; z-index: 20; position: relative; }
  #topbar .logo { display: flex; align-items: center; gap: 10px; cursor: pointer; flex-shrink: 0; }
  #topbar .title { font-family: 'JetBrains Mono', monospace; font-size: 9.5px; color: var(--gold); letter-spacing: 1.5px; }
  #topbar .subtitle { font-size: 8px; letter-spacing: 3px; color: var(--text-dim); text-transform: uppercase; }
  #topbar .spacer { flex: 1; }

  /* Theme picker */
  .theme-picker { display: flex; align-items: center; gap: 7px; }
  .theme-picker-label { font-family: 'JetBrains Mono', monospace; font-size: 7.5px; color: var(--text-dim); letter-spacing: 1.5px; text-transform: uppercase; }
  .theme-swatch { width: 18px; height: 18px; border-radius: 50%; cursor: pointer; border: 2px solid transparent; transition: all 0.18s; flex-shrink: 0; }
  .theme-swatch:hover { transform: scale(1.18); }
  .theme-swatch.active { border-color: var(--text); box-shadow: 0 0 0 1px rgba(255,255,255,0.15); }

  /* Status badge */
  #status-badge { font-family: 'JetBrains Mono', monospace; font-size: 9px; color: var(--text-dim); flex-shrink: 0; }

  /* ── Layout ── */
  #body { display: flex; flex: 1; overflow: hidden; min-height: 0; }

  /* ── Sidebar ── */
  #sidebar { width: 232px; flex-shrink: 0; background: var(--bg-panel); border-right: 1px solid var(--border); display: flex; flex-direction: column; overflow-y: auto; }
  #sidebar .eyebrow { font-family: 'JetBrains Mono', monospace; font-size: 7.5px; color: rgba(201,164,81,0.3); letter-spacing: 3px; text-transform: uppercase; margin: 14px 0 8px; padding-left: 12px; }
  .nav-item { display: flex; align-items: center; gap: 8px; padding: 7px 10px 7px 12px; border-radius: 6px; cursor: pointer; margin: 0 8px 1px; user-select: none; color: rgba(232,222,206,0.58); border-left: 2px solid transparent; font-family: 'JetBrains Mono', monospace; font-size: 11.5px; transition: background 0.15s; }
  .nav-item:hover { background: rgba(201,164,81,0.07); }
  .nav-item.active { background: rgba(201,164,81,0.12); border-left: 2px solid var(--gold); color: var(--gold); }
  .nav-item .icon { width: 18px; text-align: center; font-size: 13px; }
  .nav-item .label { flex: 1; }
  .nav-item .check { font-size: 10px; color: var(--gold); }
  #add-file-item { color: rgba(212,132,122,0.72); border: 1.5px dashed rgba(212,132,122,0.3); margin: 8px; border-radius: 8px; padding: 9px 10px 9px 12px; }
  #add-file-item:hover { background: rgba(212,132,122,0.07); border-color: rgba(212,132,122,0.55); }

  /* ── Content ── */
  #content { flex: 1; overflow-y: auto; padding: 44px 52px; position: relative; }
  #content h1 { font-size: 22px; font-weight: 300; letter-spacing: 4px; color: var(--text); text-transform: uppercase; margin: 0 0 6px; }
  #content .motto { font-size: 12px; font-style: italic; color: var(--text-dim); margin-bottom: 28px; }

  /* ── Toolbar ── */
  #toolbar { display: flex; gap: 10px; margin-bottom: 24px; flex-wrap: wrap; }
  .tb-btn { font-family: 'JetBrains Mono', monospace; font-size: 10px; letter-spacing: 0.5px; padding: 8px 16px; border-radius: 8px; cursor: pointer; border: 1px solid var(--border); background: rgba(255,255,255,0.02); color: var(--text-dim); transition: all 0.15s; }
  .tb-btn:hover { border-color: rgba(201,164,81,0.4); color: var(--text); }
  .tb-btn.save { color: var(--gold); border-color: rgba(201,164,81,0.35); }
  .tb-btn.delete { color: var(--rose); border-color: rgba(212,132,122,0.3); }

  /* ── Home dashboard ── */
  #home-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(252px,1fr)); gap: 12px; }
  .home-card { background: rgba(255,255,255,0.02); border: 1px solid var(--border); border-radius: 12px; padding: 20px; cursor: pointer; transition: all 0.15s; }
  .home-card:hover { background: rgba(201,164,81,0.05); border-color: rgba(201,164,81,0.28); }
  .home-card .hc-top { display: flex; align-items: flex-start; gap: 10px; margin-bottom: 12px; }
  .home-card .hc-icon { width: 36px; height: 36px; border-radius: 8px; background: rgba(201,164,81,0.08); border: 1px solid rgba(201,164,81,0.18); display: flex; align-items: center; justify-content: center; font-size: 17px; flex-shrink: 0; }
  .home-card .hc-label { font-size: 15px; font-weight: 500; color: var(--text); line-height: 1.2; }
  .home-card .hc-motto { font-size: 10.5px; color: var(--text-dim); font-style: italic; margin-top: 2px; }
  .home-card .hc-bar-track { height: 3px; background: rgba(201,164,81,0.08); border-radius: 2px; overflow: hidden; margin-top: 8px; }
  .home-card .hc-bar-fill { height: 100%; background: linear-gradient(90deg, var(--gold), var(--rose)); }
  .home-card .hc-meta { display: flex; justify-content: space-between; align-items: center; }
  .home-card .hc-count { font-family: 'JetBrains Mono', monospace; font-size: 9px; color: rgba(201,164,81,0.45); }
  .home-card .hc-pct { font-family: 'JetBrains Mono', monospace; font-size: 9px; color: var(--gold); }

  /* ── Fields ── */
  .field-block { background: rgba(255,255,255,0.02); border: 1px solid var(--border); border-radius: 10px; overflow: hidden; margin-bottom: 14px; }
  .field-block .field-label { display: flex; align-items: center; gap: 8px; padding: 10px 14px; border-bottom: 1px solid var(--border); font-family: 'JetBrains Mono', monospace; font-size: 10px; color: var(--gold); }
  .field-block textarea { display: block; width: 100%; min-height: 80px; padding: 12px 14px; background: transparent; border: none; outline: none; resize: vertical; box-sizing: border-box; font-size: 14px; line-height: 1.8; color: var(--text); font-family: 'Cormorant Garamond', serif; }

  /* ── Seeded content ── */
  .seeded-banner {
    display: flex; align-items: center; gap: 10px; padding: 10px 16px; margin-bottom: 14px;
    background: rgba(201,164,81,0.06); border: 1.5px dashed rgba(201,164,81,0.3); border-radius: 8px;
    font-family: 'JetBrains Mono', monospace; font-size: 9px; color: rgba(201,164,81,0.75); letter-spacing: 0.3px;
  }
  .seeded-banner .sb-lock { font-size: 13px; flex-shrink: 0; }
  .seeded-table { border: 1px solid var(--border); border-radius: 10px; overflow: hidden; margin-bottom: 14px; }
  .seeded-table .st-header { display: flex; background: rgba(201,164,81,0.07); border-bottom: 1px solid var(--border); }
  .seeded-table .st-hcell { padding: 9px 14px; font-family: 'JetBrains Mono', monospace; font-size: 8px; color: var(--gold); letter-spacing: 0.8px; text-transform: uppercase; flex: 1; }
  .seeded-table .st-hcell.wide { flex: 2; }
  .seeded-table .st-hcell.lock-col { flex: 0 0 36px; text-align: center; }
  .seeded-table .st-row { display: flex; align-items: stretch; border-bottom: 1px solid rgba(201,164,81,0.06); border-left: 3px solid rgba(201,164,81,0.22); background: rgba(201,164,81,0.025); }
  .seeded-table .st-row:last-child { border-bottom: none; }
  .seeded-table .st-cell { padding: 9px 14px; font-size: 12.5px; color: var(--text-dim); font-style: italic; font-family: 'Cormorant Garamond', serif; flex: 1; line-height: 1.5; }
  .seeded-table .st-cell.wide { flex: 2; }
  .seeded-table .st-cell.lock-cell { flex: 0 0 36px; display: flex; align-items: center; justify-content: center; font-size: 11px; opacity: 0.55; }
  .seeded-user-row { background: rgba(255,255,255,0.03); border-left: 3px solid rgba(212,132,122,0.2); }
  .seeded-user-row .st-cell { color: var(--text); font-style: normal; }

  /* ── Principles list ── */
  .principles-locked { border: 1px solid var(--border); border-radius: 10px; overflow: hidden; margin-bottom: 14px; background: rgba(255,255,255,0.015); }
  .principles-locked .pl-header { display: flex; align-items: center; gap: 10px; padding: 10px 14px; border-bottom: 1px solid var(--border); background: rgba(201,164,81,0.06); }
  .principles-locked .pl-header-text { font-family: 'JetBrains Mono', monospace; font-size: 9px; color: var(--gold); flex: 1; }
  .principles-locked .pl-lock { font-size: 12px; opacity: 0.6; }
  .principles-locked .pl-item { display: flex; align-items: center; gap: 12px; padding: 9px 14px; border-bottom: 1px solid rgba(201,164,81,0.05); border-left: 3px solid rgba(201,164,81,0.18); }
  .principles-locked .pl-item:last-child { border-bottom: none; }
  .principles-locked .pl-num { font-family: 'JetBrains Mono', monospace; font-size: 8.5px; color: rgba(201,164,81,0.4); width: 16px; flex-shrink: 0; }
  .principles-locked .pl-text { font-size: 14px; color: var(--text-dim); font-style: italic; }

  /* ── Constellation ── */
  .constellation-wrap { border: 1px solid var(--border); border-radius: 10px; overflow: hidden; margin-bottom: 14px; background: rgba(255,255,255,0.01); }
  .constellation-wrap .cw-header { padding: 10px 16px; border-bottom: 1px solid var(--border); font-family: 'JetBrains Mono', monospace; font-size: 8px; color: var(--gold); letter-spacing: 1.5px; display: flex; align-items: center; gap: 8px; }

  /* ── System Architecture module cards ── */
  .sa-section-label { font-family: 'JetBrains Mono', monospace; font-size: 8px; color: var(--text-dim); letter-spacing: 3px; text-transform: uppercase; margin: 28px 0 12px; }
  .sa-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(220px, 1fr)); gap: 10px; margin-bottom: 14px; }
  .sa-card { border: 1px solid var(--border); border-radius: 10px; overflow: hidden; background: rgba(255,255,255,0.015); transition: border-color 0.25s, box-shadow 0.25s; }
  .sa-card:hover { border-color: rgba(201,164,81,0.25); }
  .sa-card.sa-highlighted { border-color: var(--gold); box-shadow: 0 0 0 2px rgba(201,164,81,0.18), 0 8px 32px rgba(0,0,0,0.35); }
  .sa-card-header { display: flex; align-items: center; gap: 10px; padding: 11px 13px; border-bottom: 1px solid var(--border); }
  .sa-card-dot { width: 8px; height: 8px; border-radius: 50%; flex-shrink: 0; }
  .sa-card-name { font-size: 14px; font-weight: 500; color: var(--text); flex: 1; line-height: 1.2; }
  .sa-card-subs { padding: 9px 13px 2px; display: flex; flex-direction: column; gap: 5px; }
  .sa-sub { display: flex; align-items: center; gap: 7px; font-size: 11.5px; color: var(--text-dim); font-style: italic; }
  .sa-sub-dot { width: 3px; height: 3px; border-radius: 50%; flex-shrink: 0; opacity: 0.6; }
  .sa-card-notes { padding: 6px 10px 10px; }
  .sa-card-notes textarea { width: 100%; background: rgba(255,255,255,0.02); border: 1px solid rgba(201,164,81,0.08); border-radius: 6px; padding: 7px 10px; color: var(--text); font-family: 'Cormorant Garamond', serif; font-size: 12.5px; line-height: 1.6; resize: none; outline: none; min-height: 56px; transition: border-color 0.15s; }
  .sa-card-notes textarea:focus { border-color: rgba(201,164,81,0.3); }
  .sa-card-notes textarea:read-only { opacity: 0.5; cursor: default; }
  .field-block textarea:read-only { opacity: 0.55; cursor: default; }

  /* ── Weekly Governance ── */
  .wg-eyebrow { font-family:'JetBrains Mono',monospace; font-size:7.5px; letter-spacing:3px; text-transform:uppercase; color:var(--gold); opacity:0.55; margin:28px 0 10px; }
  .wg-two-col { display:grid; grid-template-columns:1fr 1fr; gap:12px; margin-bottom:14px; }
  .wg-card { background:rgba(255,255,255,0.02); border:1px solid var(--border); border-radius:10px; overflow:hidden; }
  .wg-card-header { padding:10px 14px; border-bottom:1px solid var(--border); display:flex; align-items:center; justify-content:space-between; }
  .wg-card-name { font-size:15px; font-weight:500; color:var(--text); }
  .wg-card-body { padding:12px 14px; display:flex; flex-direction:column; gap:10px; }
  .wg-field-label { font-family:'JetBrains Mono',monospace; font-size:8px; color:var(--gold); letter-spacing:0.5px; margin-bottom:3px; }
  .wg-rating-row { display:flex; align-items:center; gap:10px; }
  .wg-rating-row input[type=range] { flex:1; accent-color:var(--gold); cursor:pointer; }
  .wg-rating-val { font-family:'JetBrains Mono',monospace; font-size:11px; color:var(--gold); width:16px; text-align:right; }
  .wg-textarea { width:100%; background:rgba(255,255,255,0.03); border:1px solid var(--border); border-radius:6px; padding:8px 10px; color:var(--text); font-family:'Cormorant Garamond',serif; font-size:13px; line-height:1.7; resize:none; outline:none; min-height:56px; box-sizing:border-box; }
  .wg-textarea:focus { border-color:rgba(201,164,81,0.35); }
  .wg-input { width:100%; background:rgba(255,255,255,0.03); border:1px solid var(--border); border-radius:6px; padding:7px 10px; color:var(--text); font-family:'Cormorant Garamond',serif; font-size:13px; outline:none; box-sizing:border-box; }
  .wg-input:focus { border-color:rgba(201,164,81,0.35); }
  .wg-metrics-table { border:1px solid var(--border); border-radius:10px; overflow:hidden; margin-bottom:14px; }
  .wg-metrics-head { display:grid; grid-template-columns:1fr 90px 90px 60px; background:rgba(201,164,81,0.06); border-bottom:1px solid var(--border); }
  .wg-metrics-hcell { padding:9px 14px; font-family:'JetBrains Mono',monospace; font-size:7.5px; color:var(--gold); letter-spacing:0.5px; text-transform:uppercase; text-align:center; }
  .wg-metrics-hcell:first-child { text-align:left; }
  .wg-metric-row { display:grid; grid-template-columns:1fr 90px 90px 60px; align-items:center; border-bottom:1px solid rgba(201,164,81,0.05); }
  .wg-metric-row:last-child { border-bottom:none; }
  .wg-metric-name { padding:9px 14px; font-size:13px; color:var(--text); }
  .wg-metric-cell { padding:6px 10px; display:flex; flex-direction:column; align-items:center; gap:3px; }
  .wg-metric-cell input[type=range] { width:68px; accent-color:var(--gold); cursor:pointer; }
  .wg-metric-val { font-family:'JetBrains Mono',monospace; font-size:10px; color:var(--gold); }
  .wg-avg-bar-wrap { padding:6px 12px; display:flex; align-items:center; gap:6px; }
  .wg-avg-bar { flex:1; height:4px; border-radius:2px; background:rgba(201,164,81,0.1); overflow:hidden; }
  .wg-avg-fill { height:100%; border-radius:2px; background:linear-gradient(90deg,var(--gold),var(--rose)); transition:width 0.3s; }
  .wg-action-table { border:1px solid var(--border); border-radius:10px; overflow:hidden; margin-bottom:14px; }
  .wg-action-head { display:grid; grid-template-columns:2fr 100px 90px 2fr 32px; background:rgba(201,164,81,0.06); border-bottom:1px solid var(--border); }
  .wg-action-hcell { padding:8px 10px; font-family:'JetBrains Mono',monospace; font-size:7.5px; color:var(--gold); letter-spacing:0.5px; text-transform:uppercase; }
  .wg-action-row { display:grid; grid-template-columns:2fr 100px 90px 2fr 32px; align-items:stretch; border-bottom:1px solid rgba(201,164,81,0.05); }
  .wg-action-row:last-child { border-bottom:none; }
  .wg-action-cell input,.wg-action-cell select { width:100%; background:transparent; border:none; outline:none; color:var(--text); font-family:'Cormorant Garamond',serif; font-size:13px; padding:8px 10px; box-sizing:border-box; }
  .wg-action-cell select { cursor:pointer; }
  .wg-action-del { display:flex; align-items:center; justify-content:center; cursor:pointer; color:rgba(212,132,122,0.35); font-size:13px; }
  .wg-action-del:hover { color:var(--rose); }
  .wg-add-row { display:flex; align-items:center; gap:8px; padding:9px 12px; cursor:pointer; color:rgba(212,132,122,0.65); font-family:'JetBrains Mono',monospace; font-size:9px; border-top:1px solid var(--border); }
  .wg-add-row:hover { background:rgba(212,132,122,0.05); }
  .wg-horizon-grid { display:grid; grid-template-columns:repeat(auto-fill,minmax(175px,1fr)); gap:10px; margin-bottom:14px; }
  .wg-horizon-card { background:rgba(255,255,255,0.02); border:1px solid var(--border); border-radius:10px; overflow:hidden; }
  .wg-horizon-head { padding:8px 12px; border-bottom:1px solid var(--border); }
  .wg-horizon-label { font-family:'JetBrains Mono',monospace; font-size:9px; color:var(--gold); }
  .wg-meeting-meta { display:flex; gap:12px; margin-bottom:20px; flex-wrap:wrap; }
  .wg-meta-field { display:flex; flex-direction:column; gap:5px; }
  .wg-meta-field input { background:rgba(255,255,255,0.03); border:1px solid var(--border); border-radius:6px; padding:7px 10px; color:var(--text); font-family:'JetBrains Mono',monospace; font-size:11px; outline:none; }
  .wg-meta-field input:focus { border-color:rgba(201,164,81,0.35); }

  /* ── Add File footer (every section) ── */
  .add-file-footer { margin-top: 36px; padding: 16px 20px; border: 1.5px dashed rgba(212,132,122,0.28); border-radius: 10px; display: flex; align-items: center; justify-content: space-between; cursor: pointer; transition: all 0.18s; }
  .add-file-footer:hover { background: rgba(212,132,122,0.04); border-color: rgba(212,132,122,0.5); }
  .add-file-footer .aff-left { display: flex; align-items: center; gap: 12px; }
  .add-file-footer .aff-icon { width: 30px; height: 30px; border-radius: 8px; background: rgba(212,132,122,0.1); border: 1px solid rgba(212,132,122,0.22); display: flex; align-items: center; justify-content: center; font-size: 16px; color: rgba(212,132,122,0.8); flex-shrink: 0; }
  .add-file-footer .aff-label { font-family: 'JetBrains Mono', monospace; font-size: 11px; color: rgba(212,132,122,0.72); }
  .add-file-footer .aff-sub { font-size: 11px; color: var(--text-dim); font-style: italic; margin-top: 1px; }
  .add-file-footer .aff-arrow { font-size: 18px; color: rgba(212,132,122,0.35); }

  /* ── Add File modal ── */
  #add-file-modal { display: none; position: fixed; inset: 0; background: rgba(0,0,0,0.72); backdrop-filter: blur(6px); z-index: 500; align-items: center; justify-content: center; }
  #add-file-modal.open { display: flex; }
  .afm-panel { width: 460px; background: var(--bg-panel); border: 1px solid var(--border); border-radius: 14px; box-shadow: 0 40px 100px rgba(0,0,0,0.7); overflow: hidden; }
  .afm-titlebar { display: flex; align-items: center; justify-content: space-between; padding: 16px 20px; border-bottom: 1px solid var(--border); }
  .afm-title { display: flex; align-items: center; gap: 10px; font-size: 17px; font-weight: 500; color: var(--text); }
  .afm-close { width: 28px; height: 28px; display: flex; align-items: center; justify-content: center; cursor: pointer; border-radius: 6px; color: var(--text-dim); font-size: 18px; transition: all 0.15s; }
  .afm-close:hover { background: rgba(255,255,255,0.07); color: var(--text); }
  .afm-body { padding: 22px 20px; }
  .afm-field-label { font-family: 'JetBrains Mono', monospace; font-size: 8.5px; color: var(--gold); letter-spacing: 1px; text-transform: uppercase; margin-bottom: 7px; }
  .afm-input { width: 100%; background: rgba(255,255,255,0.03); border: 1px solid var(--border); border-radius: 8px; padding: 10px 13px; color: var(--text); font-family: 'Cormorant Garamond', serif; font-size: 15px; outline: none; margin-bottom: 20px; transition: border-color 0.15s; }
  .afm-input:focus { border-color: rgba(201,164,81,0.4); }
  .afm-layouts { display: flex; gap: 8px; margin-bottom: 22px; }
  .afm-layout { flex: 1; padding: 14px 10px; border-radius: 8px; border: 1.5px solid var(--border); cursor: pointer; text-align: center; transition: all 0.15s; }
  .afm-layout:hover, .afm-layout.selected { border-color: var(--gold); background: rgba(201,164,81,0.07); }
  .afm-layout .al-icon { font-size: 22px; margin-bottom: 5px; }
  .afm-layout .al-label { font-family: 'JetBrains Mono', monospace; font-size: 8.5px; color: var(--text-dim); }
  .afm-create { width: 100%; padding: 12px; background: linear-gradient(135deg, var(--gold), var(--rose)); border: none; border-radius: 8px; color: #060B14; font-family: 'JetBrains Mono', monospace; font-size: 11px; font-weight: 500; letter-spacing: 0.5px; cursor: pointer; }
  .afm-create:hover { opacity: 0.9; }

  /* ── Toast ── */
  #toast { position: fixed; bottom: 20px; right: 20px; background: linear-gradient(135deg, #C9A451, #D4847A); color: #060B14; padding: 11px 18px; border-radius: 10px; font-family: 'JetBrains Mono', monospace; font-size: 11px; font-weight: 500; z-index: 1000; box-shadow: 0 8px 28px rgba(0,0,0,0.5); display: none; }

  /* ── Loading ── */
  #loading-screen { position: fixed; inset: 0; background: var(--bg); display: flex; align-items: center; justify-content: center; flex-direction: column; gap: 12px; z-index: 999; }
  #loading-screen .spinner { width: 28px; height: 28px; border: 2px solid rgba(201,164,81,0.2); border-top-color: var(--gold); border-radius: 50%; animation: spin 0.8s linear infinite; }
  @keyframes spin { to { transform: rotate(360deg); } }
  #loading-screen .msg { font-family: 'JetBrains Mono', monospace; font-size: 10px; color: var(--text-dim); letter-spacing: 1px; }
</style>
</head>
<body>

<!-- background watermark removed -->

<div id="loading-screen">
  <div class="spinner"></div>
  <div class="msg">CONNECTING TO DATABASE...</div>
</div>

<div id="app" style="display:none;">

  <!-- ── Top bar ── -->
  <div id="topbar">
    <div class="logo" onclick="goHome()">
      <svg width="34" height="34" viewBox="0 0 34 34" xmlns="http://www.w3.org/2000/svg">
        <circle cx="17" cy="17" r="16" fill="none" stroke="var(--gold)" stroke-width="1.2"/>
        <text x="17" y="22.5" text-anchor="middle" font-family="Cormorant Garamond, Georgia, serif" font-size="13" font-weight="600" fill="var(--gold)" letter-spacing="-0.5">DV</text>
        <path d="M0,3 C0,1 2,0 3.5,1.5 C5,0 7,1 7,3 C7,5.5 3.5,8 3.5,8 C3.5,8 0,5.5 0,3Z" fill="var(--rose)" transform="translate(21.8,16.4) scale(0.72)"/>
      </svg>
      <div>
        <div class="title">&lt;/&gt; relationship.architecture</div>
        <div class="subtitle">Daniel &amp; Veronica</div>
      </div>
    </div>
    <div class="spacer"></div>

    <!-- Media Player -->
    <div id="media-player" onclick="window.open('https://soundcloud.com/dan-tanner-189193050','_blank')" style="display:flex;align-items:center;gap:10px;background:rgba(255,255,255,0.03);border:1px solid var(--border);border-radius:8px;padding:5px 12px;flex-shrink:0;cursor:pointer;transition:border-color 0.15s;" onmouseover="this.style.borderColor='rgba(201,164,81,0.35)'" onmouseout="this.style.borderColor='var(--border)'">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="var(--gold)" style="flex-shrink:0;opacity:0.8;"><path d="M1.175 12.225c-.046 0-.094.01-.134.026C.484 12.41 0 13.025 0 13.75c0 .725.484 1.34 1.041 1.499.04.016.088.026.134.026h.933v-3.05h-.933zm3.318-2.316c-.26 0-.52.026-.77.078V15.275h7.754V9.01A6.608 6.608 0 0 0 8.17 8.7a6.55 6.55 0 0 0-3.677 1.209zm9.574-1.417c-.26 0-.52.026-.77.078v6.705h1.54V8.57a6.6 6.6 0 0 0-.77-.078zm3.085.39v6.393h1.54V8.882a6.55 6.55 0 0 0-1.54 0zm3.086.52v5.873h1.54V9.402a6.55 6.55 0 0 0-1.54 0zm3.085.39v5.483H24V10.13a6.55 6.55 0 0 0-1.677-.338z"/></svg>
      <div style="font-family:'Cormorant Garamond',serif;font-style:italic;font-size:12px;color:var(--text-dim);">Dan Tanner</div>
      <div style="font-family:'JetBrains Mono',monospace;font-size:9px;color:var(--gold);opacity:0.7;">▶ OPEN PLAYLIST</div>
    </div>

    <!-- Theme picker -->
    <div class="theme-picker">
      <span class="theme-picker-label">Theme</span>
      <select id="theme-select" onchange="applyTheme(this.value)" style="background:rgba(255,255,255,0.04);border:1px solid var(--border);color:var(--text);font-family:'JetBrains Mono',monospace;font-size:9.5px;padding:5px 8px;border-radius:6px;cursor:pointer;outline:none;">
        <option value="midnight">Midnight Gold</option>
        <option value="warm">Warm Ember</option>
        <option value="cool">Cool Slate</option>
        <option value="mono">Monochrome</option>
        <option value="dracula">Dracula</option>
        <option value="neon">Neon</option>
        <option value="pastel">Pastel</option>
        <option value="vanilla">Vanilla Walnut</option>
        <option value="olive">Olive Saffron</option>
      </select>
    </div>

    <div id="status-badge">● connected</div>
  </div>

  <div id="body">
    <!-- ── Sidebar ── -->
    <div id="sidebar">
      <div class="nav-item" id="dashboard-item" onclick="goHome()" style="margin-top:12px;">
        <span class="icon">🏛</span><span class="label">Dashboard</span>
      </div>
      <div class="eyebrow">📁 Our Relationship</div>
      <div id="nav-list"></div>
      <div style="flex:1;min-height:12px;"></div>
      <div class="nav-item" id="add-file-item" onclick="openAddFile()">
        <span class="icon" style="font-size:15px;">＋</span><span class="label">Add File</span>
      </div>
    </div>

    <div id="content"></div>
  </div>
</div>

<!-- ── Delete Confirm Modal ── -->
<div id="delete-confirm-modal" style="display:none;position:fixed;inset:0;background:rgba(0,0,0,0.72);backdrop-filter:blur(6px);z-index:600;align-items:center;justify-content:center;" onclick="if(event.target===this)closeDeleteConfirm()">
  <div style="width:360px;background:var(--bg-panel);border:1px solid var(--border);border-radius:14px;box-shadow:0 40px 100px rgba(0,0,0,0.7);overflow:hidden;" onclick="event.stopPropagation()">
    <div style="padding:20px 22px 0;"><div id="dcm-title" style="font-size:17px;font-weight:500;color:var(--text);margin-bottom:8px;">Clear this section?</div><div style="font-size:13px;color:var(--text-dim);font-style:italic;line-height:1.6;">All content in this section will be erased. This cannot be undone.</div></div>
    <div style="display:flex;gap:10px;padding:20px 22px;">
      <button onclick="closeDeleteConfirm()" style="flex:1;padding:11px;background:rgba(255,255,255,0.03);border:1px solid var(--border);border-radius:8px;color:var(--text-dim);font-family:'JetBrains Mono',monospace;font-size:10px;cursor:pointer;">Cancel</button>
      <button id="dcm-confirm-btn" style="flex:1;padding:11px;background:rgba(212,132,122,0.15);border:1px solid rgba(212,132,122,0.4);border-radius:8px;color:var(--rose);font-family:'JetBrains Mono',monospace;font-size:10px;cursor:pointer;">Clear Content</button>
    </div>
  </div>
</div>

<!-- ── Add File Modal ── -->
<div id="add-file-modal" onclick="handleModalBackdrop(event)">
  <div class="afm-panel" onclick="event.stopPropagation()">
    <div class="afm-titlebar">
      <div class="afm-title"><span>📄</span> New File</div>
      <div class="afm-close" onclick="closeAddFile()">✕</div>
    </div>
    <div class="afm-body">
      <div class="afm-field-label">File Name</div>
      <input class="afm-input" id="afm-name" type="text" placeholder="e.g. Parenting Plan, Home Fund, Travel Goals…" />
      <div class="afm-field-label">Starting Layout</div>
      <div class="afm-layouts">
        <div class="afm-layout selected" id="afm-blank" onclick="selectLayout('blank')">
          <div class="al-icon">📄</div>
          <div class="al-label">BLANK</div>
        </div>
        <div class="afm-layout" id="afm-clone" onclick="selectLayout('clone')">
          <div class="al-icon">📋</div>
          <div class="al-label">CLONE A SECTION</div>
        </div>
      </div>
      <button class="afm-create" onclick="createFile()">CREATE FILE</button>
    </div>
  </div>
</div>

<div id="toast"></div>

<script>

  /* ══════════════════════════════════════════
     THEMES
  ══════════════════════════════════════════ */
  const THEMES = {
    midnight: { '--bg':'#060B14','--bg-panel':'#08101E','--gold':'#C9A451','--rose':'#D4847A','--text':'#E8DECE','--text-dim':'rgba(232,222,206,0.4)','--border':'rgba(201,164,81,0.12)','--topbar-bg':'rgba(6,11,20,0.98)' },
    warm:     { '--bg':'#120A04','--bg-panel':'#1C1008','--gold':'#D4A46A','--rose':'#C47860','--text':'#F0E6D4','--text-dim':'rgba(240,230,212,0.4)','--border':'rgba(212,164,106,0.15)','--topbar-bg':'rgba(18,10,4,0.98)' },
    cool:     { '--bg':'#04080F','--bg-panel':'#070D1C','--gold':'#6EB0D4','--rose':'#8AA4C8','--text':'#D4E4F0','--text-dim':'rgba(212,228,240,0.4)','--border':'rgba(110,176,212,0.15)','--topbar-bg':'rgba(4,8,15,0.98)' },
    mono:     { '--bg':'#080808','--bg-panel':'#101010','--gold':'#C8C8C8','--rose':'#888888','--text':'#F0F0F0','--text-dim':'rgba(240,240,240,0.38)','--border':'rgba(200,200,200,0.1)','--topbar-bg':'rgba(8,8,8,0.98)' },
    dracula:  { '--bg':'#1e1f29','--bg-panel':'#282a36','--gold':'#bd93f9','--rose':'#ff79c6','--text':'#f8f8f2','--text-dim':'rgba(248,248,242,0.42)','--border':'rgba(189,147,249,0.14)','--topbar-bg':'rgba(30,31,41,0.98)' },
    neon:     { '--bg':'#080808','--bg-panel':'#0e0e0e','--gold':'#00ff9f','--rose':'#ff2d78','--text':'#ffffff','--text-dim':'rgba(255,255,255,0.42)','--border':'rgba(0,255,159,0.18)','--topbar-bg':'rgba(8,8,8,0.98)' },
    pastel:   { '--bg':'#1a1228','--bg-panel':'#221830','--gold':'#c8a8e8','--rose':'#f0a0b8','--text':'#f0e8ff','--text-dim':'rgba(240,232,255,0.42)','--border':'rgba(200,168,232,0.18)','--topbar-bg':'rgba(26,18,40,0.98)' },
    vanilla:  { '--bg':'#2E1601','--bg-panel':'#4C2602','--gold':'#F9A620','--rose':'#00DFCC','--text':'#F7E9AB','--text-dim':'rgba(247,233,171,0.42)','--border':'rgba(249,166,32,0.16)','--topbar-bg':'rgba(46,22,1,0.98)' },
    olive:    { '--bg':'#1C1E0C','--bg-panel':'#272B10','--gold':'#FF961F','--rose':'#870005','--text':'#FFF7E9','--text-dim':'rgba(255,247,233,0.42)','--border':'rgba(255,150,31,0.16)','--topbar-bg':'rgba(28,30,12,0.98)' }
  };

  window.applyTheme = function(key) {
    const t = THEMES[key]; if (!t) return;
    Object.entries(t).forEach(([p,v]) => document.documentElement.style.setProperty(p, v));
    const sel = document.getElementById('theme-select');
    if (sel) sel.value = key;
    try { localStorage.setItem('dv_theme', key); } catch(e){}
  };

  /* ══════════════════════════════════════════
     SYSTEM ARCHITECTURE MODULES
  ══════════════════════════════════════════ */
  const SA_MODULES = [
    {key:'foundation',         name:'Foundation',          items:['Shared Vision','Core Agreement','Renewal Ritual'],           color:'#C9A451'},
    {key:'communication',      name:'Communication',        items:['Weekly Meeting','Daily Check-in','Conflict Protocol'],       color:'#D4847A'},
    {key:'emotional_health',   name:'Emotional Health',     items:['Support Agreements','Repair Protocol','Therapy'],            color:'#9E8AC0'},
    {key:'physical_health',    name:'Physical Health',      items:['Fitness Goals','Nutrition','Rest & Recovery'],               color:'#7AAAC8'},
    {key:'finances',           name:'Finances',             items:['Budget System','Savings','Investment Plan'],                 color:'#7AB87A'},
    {key:'home',               name:'Home',                 items:['Chores Split','Environment','Hosting'],                     color:'#C9A451'},
    {key:'family',             name:'Family',               items:['Family Values','Extended Family','Future Children'],         color:'#D4847A'},
    {key:'adventure',          name:'Adventure',            items:['Travel Goals','Date Nights','Shared Hobbies'],              color:'#9E8AC0'},
    {key:'intimacy',           name:'Intimacy',             items:['Physical Connection','Emotional Closeness','Vulnerability'], color:'#7AAAC8'},
    {key:'conflict_resolution',name:'Conflict Resolution',  items:['Fighting Rules','Repair Process','Mediation'],              color:'#C87A7A'},
    {key:'future_planning',    name:'Future Planning',       items:['5-Year Plan','Retirement','Estate Planning'],               color:'#7AB87A'},
    {key:'legacy',             name:'Legacy',               items:['Values to Pass On','Community Impact','Our Story'],         color:'#B89AE0'}
  ];

  /* ══════════════════════════════════════════
     SECTIONS
  ══════════════════════════════════════════ */
  const SECTIONS = [
    { id:"executive_summary", icon:"🏛", label:"Executive Summary", motto:"Why this architecture exists.",
      fields:[
        {key:"purpose",label:"Our Purpose",placeholder:"Why does this architecture exist?"},
        {key:"mission",label:"Mission Statement",placeholder:"What we do, for each other, and why — one powerful sentence."},
        {key:"vision",label:"Vision Statement",placeholder:"What are we building toward? The 10-year horizon in one sentence."},
        {key:"success",label:"Success Definition",placeholder:"What does a thriving, healthy relationship look like specifically for us?"},
        {key:"philosophy",label:"Relationship Philosophy",placeholder:"Our core belief about love, partnership, and what it means to truly commit."}
      ]},
    { id:"guiding_principles", icon:"◆", label:"Guiding Principles", motto:"Our non-negotiable rules.",
      fields:[{key:"additional",label:"Additional Principles",placeholder:"Any other guiding principles we want to add..."}]},
    { id:"core_values", icon:"💎", label:"Core Values", motto:"The foundation everything flows from.",
      fields:[
        {key:"love_def",label:"Love & Respect — Definition",placeholder:""},
        {key:"love_behaviors",label:"Love & Respect — Behaviors",placeholder:""},
        {key:"love_antipatterns",label:"Love & Respect — Anti-Patterns",placeholder:""},
        {key:"love_examples",label:"Love & Respect — Examples",placeholder:""},
        {key:"comm_def",label:"Communication — Definition",placeholder:""},
        {key:"comm_behaviors",label:"Communication — Expected Behaviors",placeholder:""},
        {key:"comm_meeting_rules",label:"Communication — Meeting Rules",placeholder:""},
        {key:"comm_conflict_rules",label:"Communication — Conflict Rules",placeholder:""},
        {key:"trust_built",label:"Trust — How It's Built",placeholder:""},
        {key:"trust_repaired",label:"Trust — How It's Repaired",placeholder:""},
        {key:"trust_violations",label:"Trust — Violations",placeholder:""},
        {key:"growth_learning",label:"Growth — Learning",placeholder:""},
        {key:"growth_health",label:"Growth — Health",placeholder:""},
        {key:"growth_spiritual",label:"Growth — Spiritual",placeholder:""},
        {key:"growth_career",label:"Growth — Career",placeholder:""},
        {key:"growth_financial",label:"Growth — Financial",placeholder:""},
        {key:"growth_relationship",label:"Growth — Relationship",placeholder:""}
      ]},
    { id:"system_architecture", icon:"🗂", label:"System Architecture", motto:"Our relationship as a living system.",
      fields: SA_MODULES.map(m => ({key:'sa_'+m.key, label:m.name+' — Notes & Commitments', placeholder:'Current status, intentions, and commitments for this module…'})) },

    { id:"weekly_governance", icon:"📅", label:"Weekly Governance Meeting", motto:"Sunday review, align, and decide.",
      fields:[
        {key:"checkin_daniel",label:"Check-in — Daniel (Mood, Energy, Stress, Win, Struggle)",placeholder:""},
        {key:"checkin_veronica",label:"Check-in — Veronica (Mood, Energy, Stress, Win, Struggle)",placeholder:""},
        {key:"appreciation_d_to_v",label:"Appreciation — Daniel to Veronica",placeholder:"3 things I'm grateful for / 3 things you did well"},
        {key:"appreciation_v_to_d",label:"Appreciation — Veronica to Daniel",placeholder:"3 things I'm grateful for / 3 things you did well"},
        {key:"open_issues",label:"Open Issues",placeholder:"Anything bothering us, avoided, or unresolved?"},
        {key:"action_items",label:"Action Items (Owner / Status / Notes)",placeholder:""},
        {key:"metrics",label:"Metrics (1–10): Overall, Communication, Intimacy, Stress, Finances, Health, Faith, Fun",placeholder:""},
        {key:"adr_log",label:"Decisions — ADR Log",placeholder:"ADR-002: ..."},
        {key:"new_goals",label:"New Goals (Daily/Weekly/Monthly/Yearly/Lifetime)",placeholder:""}
      ]},
    { id:"goals_architecture", icon:"🎯", label:"Goals Architecture", motto:"Our OKR-style goal system.",
      fields:[{key:"active_goals",label:"Active Goals (Goal / Milestone / Tasks / Owner / Deadline / Status)",placeholder:""}]},
    { id:"long_term_roadmap", icon:"⛰", label:"Long-Term Roadmap", motto:"Our future, by horizon.",
      fields:[
        {key:"one_year",label:"1 Year — Near-Term Horizon",placeholder:"Key goals, where we want to be"},
        {key:"five_year",label:"5 Years — Mid-Term Vision",placeholder:"Key goals, major milestones"},
        {key:"ten_year",label:"10 Years — Long-Term Architecture",placeholder:"Life we're building, major milestones"},
        {key:"retirement",label:"Retirement — Freedom Phase",placeholder:"Our retirement vision, financial target"},
        {key:"legacy",label:"Legacy — What We Leave Behind",placeholder:"How we want to be remembered"}
      ]},
    { id:"risk_register", icon:"⚠", label:"Risk Register", motto:"Known risks, named honestly.", fields:[{key:"custom_risks",label:"Additional Risks",placeholder:"Add your own risks here..."}]},
    { id:"decision_log", icon:"📜", label:"Decision Log", motto:"Every major decision, documented.",
      fields:[{key:"decisions",label:"Decisions (Date / Decision / Reasoning / Outcome)",placeholder:"Buying a home, marriage, career moves..."}]},
    { id:"meeting_notes", icon:"🗒", label:"Meeting Notes", motto:"Record of each weekly session.",
      fields:[{key:"notes_log",label:"Meeting Entries (Date / Week # / Key Topics / Notes / Action Items)",placeholder:""}]},
    { id:"appendix", icon:"📚", label:"Appendix", motto:"Everything else that shapes us.",
      fields:[
        {key:"books_resources",label:"Books & Resources",placeholder:"Books, podcasts, therapists, courses..."},
        {key:"dreams_daniel",label:"Daniel's Dreams",placeholder:""},
        {key:"dreams_veronica",label:"Veronica's Dreams",placeholder:""},
        {key:"bucket_list",label:"Bucket List",placeholder:"Places to go, things to do, experiences to share..."},
        {key:"quotes",label:"Our Quotes",placeholder:"We're not just building a relationship. We're architecting a life we love."},
        {key:"anniversaries",label:"Anniversaries & Important Dates",placeholder:""}
      ]}
  ];

  let currentView = "home";
  let sectionData = {};
  let editMode = {};
  let customSections = [];
  let addFileLayout = 'blank';

  /* ══════════════════════════════════════════
     CONSTELLATION (System Architecture)
  ══════════════════════════════════════════ */
  function buildConstellation() {
    return `<canvas id="constellation-canvas" style="width:100%;height:460px;display:block;border-radius:0 0 10px 10px;"></canvas>`;
  }

  function initConstellationCanvas(canvas) {
    if (canvas._cleanup) canvas._cleanup();
    const ctx = canvas.getContext('2d');
    const dpr = window.devicePixelRatio || 1;
    const W = canvas.offsetWidth || 700;
    const H = 460;
    canvas.width = W * dpr; canvas.height = H * dpr;
    canvas.style.width = W + 'px'; canvas.style.height = H + 'px';
    ctx.scale(dpr, dpr);

    function css(v) { return getComputedStyle(document.documentElement).getPropertyValue(v).trim() || (v === '--gold' ? '#C9A451' : v === '--rose' ? '#D4847A' : '#E8DECE'); }

    const NCX = W / 2, NCY = H / 2, R = Math.min(W, H) * 0.36;

    const nodes = SA_MODULES.map((m, i) => {
      const a = (i / SA_MODULES.length) * 2 * Math.PI - Math.PI / 2;
      return { ...m, bx: NCX + R * Math.cos(a), by: NCY + R * Math.sin(a),
               x: NCX + R * Math.cos(a), y: NCY + R * Math.sin(a),
               vx: 0, vy: 0, a, gp: Math.random() * Math.PI * 2 };
    });

    const bgStars = Array.from({length: 90}, () => ({
      x: Math.random() * W, y: Math.random() * H,
      r: Math.random() * 1.4 + 0.2, ph: Math.random() * Math.PI * 2, sp: 0.4 + Math.random() * 1.2
    }));
    const shoots = []; let lastShoot = 0;
    let mx = -9999, my = -9999, hovKey = null;
    const zoom = { s:1, tx:0, ty:0, ts:1, ttx:0, tty:0, focusKey:null };

    window._constellationZoom = (key) => {
      if (key) {
        const n = nodes.find(n => n.key === key);
        if (!n) return;
        zoom.ts = 2.2; zoom.ttx = W/2 - n.bx * 2.2; zoom.tty = H/2 - n.by * 2.2; zoom.focusKey = key;
      } else { zoom.ts = 1; zoom.ttx = 0; zoom.tty = 0; zoom.focusKey = null; }
    };

    canvas.onmousemove = e => { const r = canvas.getBoundingClientRect(); mx = (e.clientX-r.left)*(W/r.width); my = (e.clientY-r.top)*(H/r.height); };
    canvas.onmouseleave = () => { mx = -9999; my = -9999; };
    canvas.onclick = e => {
      const r = canvas.getBoundingClientRect();
      const px = ((e.clientX-r.left)*(W/r.width) - zoom.tx) / zoom.s;
      const py = ((e.clientY-r.top)*(H/r.height) - zoom.ty) / zoom.s;
      let hit = nodes.find(n => Math.hypot(px-n.x, py-n.y) < 22);
      if (hit) {
        if (zoom.focusKey === hit.key) { window._constellationZoom(null); const p = document.getElementById('constellation-popup'); if(p) p.style.display='none'; }
        else { window._constellationZoom(hit.key); window.highlightModule(hit.key, e); }
      } else { window._constellationZoom(null); const p = document.getElementById('constellation-popup'); if(p) p.style.display='none'; }
    };

    let raf;
    function draw(ts) {
      const t = ts * 0.001;
      const gold = css('--gold'), rose = css('--rose'), textCol = css('--text');
      ctx.clearRect(0, 0, W, H);

      // Lerp zoom
      zoom.s  += (zoom.ts  - zoom.s)  * 0.07;
      zoom.tx += (zoom.ttx - zoom.tx) * 0.07;
      zoom.ty += (zoom.tty - zoom.ty) * 0.07;

      // Twinkling background stars
      for (const s of bgStars) {
        const a = 0.08 + 0.72 * (0.5 + 0.5 * Math.sin(t * s.sp + s.ph));
        ctx.beginPath(); ctx.arc(s.x, s.y, s.r, 0, Math.PI*2);
        ctx.fillStyle = `rgba(255,255,255,${a.toFixed(2)})`; ctx.fill();
      }

      // Shooting stars
      if (ts - lastShoot > 3800 + Math.random()*3000) {
        const ang = 0.2 + Math.random()*0.5, spd = 5 + Math.random()*9;
        shoots.push({ x: Math.random()*W, y: Math.random()*H*0.2-20, vx: Math.cos(ang)*spd, vy: Math.sin(ang)*spd, life: 1, len: 55+Math.random()*110 });
        lastShoot = ts;
      }
      for (let i = shoots.length-1; i >= 0; i--) {
        const s = shoots[i]; s.x+=s.vx; s.y+=s.vy; s.life-=0.013;
        if (s.life<=0||s.x>W+150||s.y>H+50) { shoots.splice(i,1); continue; }
        const mag = Math.hypot(s.vx,s.vy);
        const g = ctx.createLinearGradient(s.x,s.y, s.x-s.vx/mag*s.len, s.y-s.vy/mag*s.len);
        g.addColorStop(0,`rgba(255,255,240,${(s.life*0.9).toFixed(2)})`); g.addColorStop(1,'rgba(255,255,240,0)');
        ctx.beginPath(); ctx.moveTo(s.x,s.y); ctx.lineTo(s.x-s.vx/mag*s.len, s.y-s.vy/mag*s.len);
        ctx.strokeStyle=g; ctx.lineWidth=1.8*s.life; ctx.stroke();
        ctx.beginPath(); ctx.arc(s.x,s.y,1.8*s.life,0,Math.PI*2); ctx.fillStyle=`rgba(255,255,255,${s.life.toFixed(2)})`; ctx.fill();
      }

      ctx.save(); ctx.translate(zoom.tx, zoom.ty); ctx.scale(zoom.s, zoom.s);
      const tmx = (mx - zoom.tx) / zoom.s, tmy = (my - zoom.ty) / zoom.s;

      // Spring physics — mouse repulsion
      hovKey = null;
      for (const n of nodes) {
        const dx = n.x-tmx, dy = n.y-tmy, d = Math.hypot(dx,dy);
        if (d < 70 && d > 1) {
          // Gentle attraction with tangential roll — orbs drift toward mouse and orbit it
          const attract = (1 - d/70) * 2.2;
          const orbit   = (1 - d/70) * 1.4;
          n.vx += -(dx/d)*attract + (-dy/d)*orbit;
          n.vy += -(dy/d)*attract + ( dx/d)*orbit;
          if (d < 22) hovKey = n.key;
        }
        n.vx += (n.bx-n.x)*0.08; n.vy += (n.by-n.y)*0.08;
        n.vx *= 0.78; n.vy *= 0.78; n.x += n.vx; n.y += n.vy;
      }

      // Edges
      nodes.forEach((n,i) => { const nx=nodes[(i+1)%nodes.length]; ctx.beginPath(); ctx.moveTo(n.x,n.y); ctx.lineTo(nx.x,nx.y); ctx.strokeStyle='rgba(201,164,81,0.1)'; ctx.lineWidth=0.6; ctx.stroke(); });
      nodes.forEach(n => { ctx.beginPath(); ctx.moveTo(NCX,NCY); ctx.lineTo(n.x,n.y); ctx.strokeStyle='rgba(201,164,81,0.07)'; ctx.lineWidth=0.4; ctx.stroke(); });
      [[0,6],[1,7],[2,8],[3,9],[4,10],[5,11]].forEach(([a,b]) => { ctx.beginPath(); ctx.moveTo(nodes[a].x,nodes[a].y); ctx.lineTo(nodes[b].x,nodes[b].y); ctx.strokeStyle='rgba(212,132,122,0.06)'; ctx.lineWidth=0.4; ctx.stroke(); });

      // Sub-item dots
      nodes.forEach(n => { n.items.forEach((_,j) => { const sa=n.a+(j-1)*0.55,sd=28,sx=n.x+sd*Math.cos(sa),sy=n.y+sd*Math.sin(sa); ctx.beginPath(); ctx.moveTo(n.x,n.y); ctx.lineTo(sx,sy); ctx.strokeStyle=n.color+'44'; ctx.lineWidth=0.5; ctx.stroke(); ctx.beginPath(); ctx.arc(sx,sy,2.2,0,Math.PI*2); ctx.fillStyle=n.color+'80'; ctx.fill(); }); });

      // Nodes
      nodes.forEach(n => {
        const gp = 0.5+0.5*Math.sin(t*1.5+n.gp);
        const active = n.key===hovKey||n.key===zoom.focusKey;
        const gr = active ? 32+gp*14 : 15+gp*8;
        for (let p=4;p>=1;p--) { const a=active?(0.28+gp*0.18)/p:(0.1+gp*0.05)/p; ctx.beginPath(); ctx.arc(n.x,n.y,gr*p/3.5,0,Math.PI*2); ctx.fillStyle=n.color+Math.round(a*255).toString(16).padStart(2,'0'); ctx.fill(); }
        ctx.beginPath(); ctx.arc(n.x,n.y,active?9:6.5,0,Math.PI*2); ctx.fillStyle=n.color; ctx.shadowColor=n.color; ctx.shadowBlur=active?28:14; ctx.fill(); ctx.shadowBlur=0;
        ctx.beginPath(); ctx.arc(n.x,n.y,(active?9:6.5)+(active?5:2.5)*gp,0,Math.PI*2); ctx.strokeStyle=n.color+Math.round((active?0.7:0.28)*255).toString(16).padStart(2,'0'); ctx.lineWidth=active?1.8:0.8; ctx.stroke();
        // Label
        const isR=n.bx>NCX+25,isL=n.bx<NCX-25,isT=n.by<NCY,pad=17;
        let lx,ly,align;
        if(isR){lx=n.x+pad;align='left';ly=n.y;}else if(isL){lx=n.x-pad;align='right';ly=n.y;}else{lx=n.x;align='center';ly=isT?n.y-pad-2:n.y+pad+4;}
        ctx.font=`${active?9:8}px "JetBrains Mono",monospace`; ctx.fillStyle=active?textCol:textCol+'a0'; ctx.textAlign=align; ctx.textBaseline='middle';
        ctx.shadowColor=n.color; ctx.shadowBlur=active?7:0;
        const pts=n.name.split(' ');
        if(pts.length>1&&!isR&&!isL){ctx.fillText(pts[0],lx,ly-5);ctx.fillText(pts.slice(1).join(' '),lx,ly+5);}else{ctx.fillText(n.name,lx,ly);}
        ctx.shadowBlur=0;
      });

      // Center DV
      const cg=0.5+0.5*Math.sin(t*0.8);
      ctx.beginPath(); ctx.arc(NCX,NCY,38+cg*5,0,Math.PI*2); ctx.fillStyle=`rgba(201,164,81,${(0.05+cg*0.04).toFixed(3)})`; ctx.fill();
      ctx.beginPath(); ctx.arc(NCX,NCY,30,0,Math.PI*2); ctx.strokeStyle=gold; ctx.lineWidth=1.4; ctx.shadowColor=gold; ctx.shadowBlur=10+cg*10; ctx.stroke(); ctx.shadowBlur=0;
      ctx.font='600 18px "Cormorant Garamond",serif'; ctx.fillStyle=gold; ctx.textAlign='center'; ctx.textBaseline='middle'; ctx.shadowColor=gold; ctx.shadowBlur=12+cg*10; ctx.fillText('DV',NCX,NCY-1); ctx.shadowBlur=0;
      ctx.font='11px serif'; ctx.fillStyle=rose; ctx.shadowColor=rose; ctx.shadowBlur=8; ctx.fillText('♥',NCX+9,NCY+5); ctx.shadowBlur=0;
      ctx.font='6px "JetBrains Mono",monospace'; ctx.fillStyle=gold+'80'; ctx.textAlign='center'; ctx.fillText('ARCHITECTURE',NCX,NCY+16);
      ctx.restore();
      canvas.style.cursor = hovKey ? 'pointer' : 'default';
      raf = requestAnimationFrame(draw);
    }
    raf = requestAnimationFrame(draw);
  }

  /* ══════════════════════════════════════════
     SEEDED RISK REGISTER TABLE
  ══════════════════════════════════════════ */
  const SEEDED_RISKS = [
    ['Financial Stress',     'High',   'High',   'Build 6-month emergency fund; monthly budget reviews'],
    ['Poor Communication',   'Medium', 'High',   'Weekly governance meetings; 24-hr rule for hard conversations'],
    ['Burnout',              'Medium', 'High',   'Protect rest days; share workload; quarterly check-ins'],
    ['Family Conflict',      'Low',    'Medium', 'United front; discuss privately first; set clear boundaries'],
    ['Health Issues',        'Low',    'High',   'Annual checkups; health insurance; emergency savings'],
    ['Career Instability',   'Low',    'High',   'Dual-income stability; 6-month savings runway; network actively'],
    ['Emotional Distance',   'Medium', 'High',   'Weekly dates; daily check-ins; therapy if drift persists']
  ];

  function buildSeededRiskTable() {
    let h = `
    <div class="seeded-banner">
      <span class="sb-lock">🔒</span>
      <span><strong>SEEDED EXAMPLES</strong> — These 7 rows are pre-loaded starting points. They are locked and separate from your real data. Add your own risks in the field below.</span>
    </div>
    <div class="seeded-table">
      <div class="st-header">
        <div class="st-hcell">Risk</div>
        <div class="st-hcell">Likelihood</div>
        <div class="st-hcell">Impact</div>
        <div class="st-hcell wide">Mitigation Plan</div>
        <div class="st-hcell lock-col">🔒</div>
      </div>`;
    SEEDED_RISKS.forEach(([risk, like, impact, mit]) => {
      h += `<div class="st-row">
        <div class="st-cell">${risk}</div>
        <div class="st-cell">${like}</div>
        <div class="st-cell">${impact}</div>
        <div class="st-cell wide">${mit}</div>
        <div class="st-cell lock-cell">🔒</div>
      </div>`;
    });
    h += `</div>`;
    return h;
  }

  /* ══════════════════════════════════════════
     SEEDED ADR (for weekly governance)
  ══════════════════════════════════════════ */
  function buildSeededADR() {
    return `<div class="seeded-banner">
      <span class="sb-lock">🔒</span>
      <span><strong>ADR-001 (SEEDED EXAMPLE)</strong> — "We will never go to bed angry without acknowledging the issue." Rationale: Trust is built in moments. Status: Active</span>
    </div>`;
  }

  /* ══════════════════════════════════════════
     WEEKLY GOVERNANCE RENDER
  ══════════════════════════════════════════ */
  const WG_METRICS = ['Overall Relationship','Communication','Intimacy','Stress Level','Financial Health','Physical Health','Spiritual / Faith','Fun & Adventure'];
  const WG_HORIZONS = [{key:'daily',label:'Daily',icon:'☀️'},{key:'weekly',label:'Weekly',icon:'📅'},{key:'monthly',label:'Monthly',icon:'🗓'},{key:'yearly',label:'Yearly',icon:'🎯'},{key:'lifetime',label:'Lifetime',icon:'♾️'}];

  function renderWeeklyGovernance(content, sec, data, isEditing, fieldRefs) {
    const f = data.fields || {};
    const ro = !isEditing;
    const inp = (key, placeholder, type) => {
      const el = document.createElement(type === 'textarea' ? 'textarea' : 'input');
      if (type !== 'textarea') el.type = type || 'text';
      el.className = type === 'textarea' ? 'wg-textarea' : 'wg-input';
      el.placeholder = placeholder || '';
      el.value = f[key] || '';
      el.readOnly = ro;
      fieldRefs[key] = el;
      return el;
    };
    const div = (html, cls) => { const d = document.createElement('div'); if (cls) d.className = cls; if (html) d.innerHTML = html; return d; };
    const eyebrow = t => { const d = div(t,'wg-eyebrow'); return d; };

    // ── Meeting Header ──
    content.appendChild(eyebrow('Meeting Details'));
    const metaRow = div('','wg-meeting-meta');
    const dateField = div('','wg-meta-field');
    dateField.innerHTML = '<div class="wg-field-label">DATE</div>';
    const dateInp = document.createElement('input'); dateInp.type='date'; dateInp.value=f['wg_date']||''; dateInp.readOnly=ro; fieldRefs['wg_date']=dateInp; dateField.appendChild(dateInp);
    const weekField = div('','wg-meta-field');
    weekField.innerHTML = '<div class="wg-field-label">WEEK #</div>';
    const weekInp = document.createElement('input'); weekInp.type='number'; weekInp.placeholder='e.g. 42'; weekInp.style.width='90px'; weekInp.value=f['wg_week']||''; weekInp.readOnly=ro; fieldRefs['wg_week']=weekInp; weekField.appendChild(weekInp);
    metaRow.appendChild(dateField); metaRow.appendChild(weekField);
    content.appendChild(metaRow);

    // ── Check-ins ──
    content.appendChild(eyebrow('Check-In'));
    const checkGrid = div('','wg-two-col');
    [['D','Daniel','wg_d'],['V','Veronica','wg_v']].forEach(([initial,name,prefix]) => {
      const card = div('','wg-card');
      const hdr = div('','wg-card-header');
      hdr.innerHTML = `<span class="wg-card-name">${name}</span><span style="font-family:'JetBrains Mono',monospace;font-size:10px;color:var(--gold)">${initial}</span>`;
      card.appendChild(hdr);
      const body = div('','wg-card-body');
      ['Mood','Energy','Stress'].forEach(metric => {
        const mkey = `${prefix}_${metric.toLowerCase()}`;
        const wrap = div('');
        wrap.innerHTML = `<div class="wg-field-label">${metric.toUpperCase()} <span class="wg-rating-val" id="rv_${mkey}">${f[mkey]||5}</span>/10</div>`;
        const row = div('','wg-rating-row');
        const slider = document.createElement('input'); slider.type='range'; slider.min=1; slider.max=10; slider.value=f[mkey]||5;
        slider.disabled=ro;
        const valSpan = wrap.querySelector(`#rv_${mkey}`);
        slider.oninput = () => { if(valSpan) valSpan.textContent=slider.value; };
        fieldRefs[mkey] = slider;
        row.appendChild(slider);
        wrap.appendChild(row);
        body.appendChild(wrap);
      });
      ['Win of the Week','Struggle of the Week'].forEach(label => {
        const mkey = `${prefix}_${label.toLowerCase().replace(/ /g,'_')}`;
        const wrap = div('');
        wrap.innerHTML = `<div class="wg-field-label">${label.toUpperCase()}</div>`;
        wrap.appendChild(inp(mkey, `What was your ${label.toLowerCase()}?`, 'textarea'));
        body.appendChild(wrap);
      });
      card.appendChild(body);
      checkGrid.appendChild(card);
    });
    content.appendChild(checkGrid);

    // ── Appreciation ──
    content.appendChild(eyebrow('Appreciation Exchange'));
    const apprGrid = div('','wg-two-col');
    [['Daniel → Veronica','wg_appr_d'],['Veronica → Daniel','wg_appr_v']].forEach(([label,prefix]) => {
      const card = div('','wg-card');
      card.innerHTML = `<div class="wg-card-header"><span class="wg-card-name" style="font-size:13px;">${label}</span></div>`;
      const body = div('','wg-card-body');
      [1,2,3].forEach(n => {
        const key = `${prefix}_${n}`;
        const wrap = div('');
        wrap.innerHTML = `<div class="wg-field-label">GRATITUDE ${n}</div>`;
        wrap.appendChild(inp(key,'Something I appreciate…','textarea'));
        body.appendChild(wrap);
      });
      card.appendChild(body);
      apprGrid.appendChild(card);
    });
    content.appendChild(apprGrid);

    // ── Open Issues ──
    content.appendChild(eyebrow('Open Issues'));
    const issWrap = div('','field-block');
    issWrap.innerHTML = '<div class="field-label">Anything bothering us, avoided, or unresolved?</div>';
    issWrap.appendChild(inp('wg_open_issues','List any tensions, unresolved topics, or things needing discussion…','textarea'));
    content.appendChild(issWrap);

    // ── Action Items ──
    content.appendChild(eyebrow('Action Items'));
    const aiTable = div('','wg-action-table');
    aiTable.innerHTML = '<div class="wg-action-head"><div class="wg-action-hcell">Task</div><div class="wg-action-hcell">Owner</div><div class="wg-action-hcell">Status</div><div class="wg-action-hcell">Notes</div><div class="wg-action-hcell"></div></div>';
    const aiBody = div(''); aiTable.appendChild(aiBody);
    let aiRows = []; try { aiRows = JSON.parse(f['wg_action_items']||'[]'); } catch(e){}
    if (!aiRows.length) aiRows = [{task:'',owner:'',status:'Pending',notes:''}];
    const renderAIRows = () => {
      aiBody.innerHTML='';
      aiRows.forEach((row,i) => {
        const tr = div('','wg-action-row');
        ['task','owner'].forEach(col => {
          const td = div('','wg-action-cell'); const inp2=document.createElement('input'); inp2.type='text'; inp2.value=row[col]||''; inp2.placeholder=col==='task'?'Task…':'Owner…'; inp2.readOnly=ro; inp2.oninput=e=>{aiRows[i][col]=e.target.value;}; td.appendChild(inp2); tr.appendChild(td);
        });
        const stCell = div('','wg-action-cell'); const sel=document.createElement('select'); sel.disabled=ro; ['Pending','In Progress','Done'].forEach(s=>{const o=document.createElement('option');o.value=s;o.textContent=s;if(row.status===s)o.selected=true;sel.appendChild(o);}); sel.onchange=e=>{aiRows[i].status=e.target.value;}; stCell.appendChild(sel); tr.appendChild(stCell);
        const notesCell = div('','wg-action-cell'); const ni=document.createElement('input'); ni.type='text'; ni.value=row.notes||''; ni.placeholder='Notes…'; ni.readOnly=ro; ni.oninput=e=>{aiRows[i].notes=e.target.value;}; notesCell.appendChild(ni); tr.appendChild(notesCell);
        const del = div('✕','wg-action-del'); del.onclick=()=>{if(ro)return;aiRows.splice(i,1);renderAIRows();}; tr.appendChild(del);
        aiBody.appendChild(tr);
      });
    };
    renderAIRows();
    const aiAddRow = div('+ Add Item','wg-add-row');
    aiAddRow.onclick=()=>{if(ro)return;aiRows.push({task:'',owner:'',status:'Pending',notes:''});renderAIRows();};
    aiTable.appendChild(aiAddRow);
    fieldRefs['wg_action_items'] = { get value(){ return JSON.stringify(aiRows); } };
    content.appendChild(aiTable);

    // ── Metrics Table ──
    content.appendChild(eyebrow('Weekly Metrics (1–10)'));
    const metricsTable = div('','wg-metrics-table');
    metricsTable.innerHTML = '<div class="wg-metrics-head"><div class="wg-metrics-hcell" style="text-align:left;">Metric</div><div class="wg-metrics-hcell">Daniel</div><div class="wg-metrics-hcell">Veronica</div><div class="wg-metrics-hcell">Avg</div></div>';
    WG_METRICS.forEach((metric, i) => {
      const row = div('','wg-metric-row');
      row.innerHTML = `<div class="wg-metric-name">${metric}</div>`;
      const dKey = `wg_metric_d_${i}`, vKey = `wg_metric_v_${i}`;
      const dVal = parseInt(f[dKey])||5, vVal = parseInt(f[vKey])||5;
      [['D',dKey,dVal],['V',vKey,vVal]].forEach(([who,key,val]) => {
        const cell = div('','wg-metric-cell');
        const sl = document.createElement('input'); sl.type='range'; sl.min=1; sl.max=10; sl.value=val; sl.disabled=ro;
        const vv = div(val,'wg-metric-val');
        sl.oninput = () => { vv.textContent=sl.value; updateAvg(); };
        fieldRefs[key]=sl; cell.appendChild(sl); cell.appendChild(vv); row.appendChild(cell);
      });
      const avgWrap = div('','wg-avg-bar-wrap');
      const bar = div('','wg-avg-bar'); const fill = div('','wg-avg-fill'); bar.appendChild(fill); avgWrap.appendChild(bar);
      row.appendChild(avgWrap);
      metricsTable.appendChild(row);
      const updateAvg = () => {
        const dS = row.querySelectorAll('input[type=range]')[0];
        const vS = row.querySelectorAll('input[type=range]')[1];
        const avg = ((parseInt(dS.value)+parseInt(vS.value))/2);
        fill.style.width = (avg/10*100)+'%';
      };
      updateAvg();
    });
    content.appendChild(metricsTable);

    // ── ADR Log ──
    content.appendChild(eyebrow('Decision Log (ADR)'));
    const adrWrap = div('');
    adrWrap.innerHTML = buildSeededADR();
    content.appendChild(adrWrap);
    const adrTable = div('','wg-action-table');
    adrTable.innerHTML = '<div class="wg-action-head"><div class="wg-action-hcell">Date</div><div class="wg-action-hcell" style="flex:2">Decision</div><div class="wg-action-hcell" style="flex:2">Reasoning</div><div class="wg-action-hcell" style="flex:2">Outcome</div><div class="wg-action-hcell"></div></div>';
    const adrBody = div(''); adrTable.appendChild(adrBody);
    let adrRows = []; try { adrRows = JSON.parse(f['wg_adr_entries']||'[]'); } catch(e){}
    const renderADRRows = () => {
      adrBody.innerHTML='';
      adrRows.forEach((row,i) => {
        const tr = div('','wg-action-row'); tr.style.gridTemplateColumns='90px 1fr 1fr 1fr 32px';
        ['date','decision','reasoning','outcome'].forEach(col => {
          const td = div('','wg-action-cell'); const ni=document.createElement('input'); ni.type='text'; ni.value=row[col]||''; ni.placeholder=col.charAt(0).toUpperCase()+col.slice(1)+'…'; ni.readOnly=ro; ni.oninput=e=>{adrRows[i][col]=e.target.value;}; td.appendChild(ni); tr.appendChild(td);
        });
        const del=div('✕','wg-action-del'); del.onclick=()=>{if(ro)return;adrRows.splice(i,1);renderADRRows();}; tr.appendChild(del);
        adrBody.appendChild(tr);
      });
    };
    renderADRRows();
    const adrAdd=div('+ Add Decision','wg-add-row'); adrAdd.onclick=()=>{if(ro)return;adrRows.push({date:'',decision:'',reasoning:'',outcome:''});renderADRRows();}; adrTable.appendChild(adrAdd);
    fieldRefs['wg_adr_entries']={get value(){return JSON.stringify(adrRows);}};
    content.appendChild(adrTable);

    // ── New Goals ──
    content.appendChild(eyebrow('New Goals This Week'));
    const hGrid = div('','wg-horizon-grid');
    WG_HORIZONS.forEach(h => {
      const card = div('','wg-horizon-card');
      card.innerHTML = `<div class="wg-horizon-head"><span style="font-size:14px;">${h.icon}</span>&nbsp;<span class="wg-horizon-label">${h.label.toUpperCase()}</span></div>`;
      const key = `wg_goal_${h.key}`;
      const ta = inp(key,`${h.label} goals…`,'textarea'); ta.style.borderRadius='0'; ta.style.border='none'; ta.style.minHeight='72px';
      card.appendChild(ta);
      hGrid.appendChild(card);
    });
    content.appendChild(hGrid);
  }

  /* ══════════════════════════════════════════
     ADD FILE FOOTER (every section tab)
  ══════════════════════════════════════════ */
  function buildAddFileFooter(parentId) {
    const el = document.createElement('div');
    el.className = 'add-file-footer';
    el.onclick = () => openAddFile(parentId);
    el.innerHTML = `
      <div class="aff-left">
        <div class="aff-icon">＋</div>
        <div>
          <div class="aff-label">Add File</div>
          <div class="aff-sub">Create a new document in this section</div>
        </div>
      </div>
      <div class="aff-arrow">→</div>`;
    return el;
  }

  /* ══════════════════════════════════════════
     NAV
  ══════════════════════════════════════════ */
  function renderNav() {
    document.getElementById('dashboard-item').className = 'nav-item' + (currentView === 'home' ? ' active' : '');
    const navList = document.getElementById('nav-list');
    navList.innerHTML = '';
    SECTIONS.forEach(sec => {
      const item = document.createElement('div');
      item.className = 'nav-item' + (sec.id === currentView ? ' active' : '');
      item.onclick = () => { currentView = sec.id; renderNav(); renderContent(); };
      const check = (sectionData[sec.id] && sectionData[sec.id].completed) ? '<span class="check">✓</span>' : '';
      item.innerHTML = `<span class="icon">${sec.icon}</span><span class="label">${sec.label}</span>${check}`;
      navList.appendChild(item);
      // Render custom child files indented under this section
      customSections.filter(cs => cs.parentId === sec.id).forEach(cs => {
        const child = document.createElement('div');
        child.className = 'nav-item' + (cs.id === currentView ? ' active' : '');
        child.style.cssText = 'padding-left:28px;font-size:10.5px;';
        child.onclick = () => openDocEditor(cs.id, cs.label, (sectionData[cs.id] && sectionData[cs.id].fields && sectionData[cs.id].fields.body) || '');
        child.innerHTML = `<span class="icon" style="font-size:11px;">📄</span><span class="label">${cs.label}</span>`;
        navList.appendChild(child);
      });
    });
    // Orphan custom sections (no parent) at bottom
    customSections.filter(cs => !cs.parentId).forEach(cs => {
      const item = document.createElement('div');
      item.className = 'nav-item' + (cs.id === currentView ? ' active' : '');
      item.onclick = () => openDocEditor(cs.id, cs.label, (sectionData[cs.id] && sectionData[cs.id].fields && sectionData[cs.id].fields.body) || '');
      item.innerHTML = `<span class="icon">📄</span><span class="label">${cs.label}</span>`;
      navList.appendChild(item);
    });
  }

  /* ══════════════════════════════════════════
     HOME
  ══════════════════════════════════════════ */
  function renderHome() {
    const content = document.getElementById("content");
    content.innerHTML = `
      <h1>Daniel &amp; Veronica's Relationship</h1>
      <div class="motto">Designed to grow. Built on love.</div>
      <div id="home-grid"></div>`;
    const grid = document.getElementById("home-grid");
    SECTIONS.forEach(sec => {
      const pct = pctFor(sec.id);
      const filled = filledCountFor(sec.id);
      const card = document.createElement("div");
      card.className = "home-card";
      card.onclick = () => { currentView = sec.id; renderNav(); renderContent(); };
      card.innerHTML = `
        <div class="hc-top">
          <div class="hc-icon">${sec.icon}</div>
          <div>
            <div class="hc-label">${sec.label}</div>
            <div class="hc-motto">${sec.motto}</div>
          </div>
        </div>
        <div class="hc-meta">
          <span class="hc-count">${filled}/${sec.fields.length} entries</span>
          <span class="hc-pct">${pct}%</span>
        </div>
        <div class="hc-bar-track"><div class="hc-bar-fill" style="width:${pct}%"></div></div>`;
      grid.appendChild(card);
    });
    // Custom sections
    customSections.forEach(sec => {
      const card = document.createElement("div");
      card.className = "home-card";
      card.onclick = () => { currentView = sec.id; renderNav(); renderContent(); };
      card.innerHTML = `
        <div class="hc-top">
          <div class="hc-icon">📄</div>
          <div><div class="hc-label">${sec.label}</div><div class="hc-motto">Custom section</div></div>
        </div>
        <div class="hc-meta"><span class="hc-count">0/0 entries</span><span class="hc-pct">—</span></div>
        <div class="hc-bar-track"><div class="hc-bar-fill" style="width:0%"></div></div>`;
      grid.appendChild(card);
    });
    // Add File footer on home too
    content.appendChild(buildAddFileFooter(null));
  }

  /* ══════════════════════════════════════════
     SECTION CONTENT
  ══════════════════════════════════════════ */
  function renderContent() {
    // Cleanup any running canvas animations
    const oldCanvas = document.getElementById('constellation-canvas');
    if (oldCanvas && oldCanvas._cleanup) oldCanvas._cleanup();
    const content = document.getElementById("content");
    if (currentView === "home") { renderHome(); return; }

    const sec = [...SECTIONS, ...customSections].find(s => s.id === currentView);
    if (!sec) { renderHome(); return; }
    const data = sectionData[sec.id] || { fields: {} };
    const isEditing = editMode[sec.id] === true;

    content.innerHTML = `<h1>${sec.icon || ''} ${sec.label}</h1><div class="motto">${sec.motto || ''}</div>`;

    // Toolbar
    const toolbar = document.createElement("div");
    toolbar.id = "toolbar";
    toolbar.innerHTML = `
      <button class="tb-btn save" id="btn-save">Save</button>
      <button class="tb-btn" id="btn-edit" style="${isEditing ? 'color:var(--gold);border-color:rgba(201,164,81,0.4)' : ''}">${isEditing ? "🔓 Lock" : "✏️ Edit"}</button>
      <button class="tb-btn" id="btn-export">Export</button>
      <button class="tb-btn" id="btn-close">Close</button>
      <button class="tb-btn delete" id="btn-delete">Delete</button>`;
    content.appendChild(toolbar);

    // ── Special: Guiding Principles — seeded list ──
    if (sec.id === "guiding_principles") {
      const PRINCIPLES = [
        'Love Before Ego','Radical Honesty','Team Over Individual','Attack Problems, Not People',
        'Continuous Improvement','Assume Positive Intent','Protect Trust at All Costs','Grace Over Perfection'
      ];
      const wrap = document.createElement("div");
      wrap.innerHTML = `
        <div class="seeded-banner"><span class="sb-lock">🔒</span><span><strong>SEEDED EXAMPLES</strong> — These 8 core principles are pre-loaded. They're locked and always visible. Add your own below.</span></div>
        <div class="principles-locked">
          <div class="pl-header">
            <div class="pl-header-text">CORE PRINCIPLES — Fixed Reference</div>
            <span class="pl-lock">🔒</span>
          </div>
          ${PRINCIPLES.map((p,i) => `<div class="pl-item"><span class="pl-num">${i+1}</span><span class="pl-text">${p}</span></div>`).join('')}
        </div>`;
      content.appendChild(wrap);
    }

    // ── Special: System Architecture ──
    if (sec.id === "system_architecture") {
      // Constellation overview
      const wrap = document.createElement("div");
      wrap.className = "constellation-wrap";
      wrap.innerHTML = `
        <div class="cw-header">⬡ SYSTEM ARCHITECTURE &nbsp;·&nbsp; 12 MODULES &nbsp;·&nbsp; 36 SUB-COMPONENTS</div>
        ${buildConstellation()}`;
      content.appendChild(wrap);
      requestAnimationFrame(() => {
        const cvs = document.getElementById('constellation-canvas');
        if (cvs) initConstellationCanvas(cvs);
      });

      // Module cards grid
      const gridLabel = document.createElement("div");
      gridLabel.className = "sa-section-label";
      gridLabel.textContent = "Module breakdown — notes & commitments";
      content.appendChild(gridLabel);

      const grid = document.createElement("div");
      grid.className = "sa-grid";
      SA_MODULES.forEach(m => {
        const fieldKey = 'sa_' + m.key;
        const card = document.createElement("div");
        card.className = 'sa-card';
        card.id = 'sa-card-' + m.key;
        card.innerHTML = `
          <div class="sa-card-header">
            <div class="sa-card-dot" style="background:${m.color}"></div>
            <div class="sa-card-name">${m.name}</div>
          </div>
          <div class="sa-card-subs">
            ${m.items.map(it => `<div class="sa-sub"><div class="sa-sub-dot" style="background:${m.color}"></div>${it}</div>`).join('')}
          </div>
          <div style="padding:8px 10px 10px;">
            <div onclick="openAddFileFromModule('${m.key}')" style="display:flex;align-items:center;gap:8px;padding:8px 10px;border:1.5px dashed rgba(212,132,122,0.3);border-radius:7px;cursor:pointer;" onmouseover="this.style.background='rgba(212,132,122,0.07)'" onmouseout="this.style.background='transparent'">
              <span style="font-size:14px;color:rgba(212,132,122,0.75);">+</span>
              <span style="font-family:'JetBrains Mono',monospace;font-size:8.5px;color:rgba(212,132,122,0.65);">Add file</span>
            </div>
          </div>`;
        grid.appendChild(card);
      });
      content.appendChild(grid);

      // Skip the default fields loop for this section
      content.appendChild(buildAddFileFooter(sec.id));
      document.getElementById("btn-save").onclick = () => saveSection(sec, fieldRefs);
      document.getElementById("btn-edit").onclick = () => { editMode[sec.id] = !isEditing; renderContent(); };
      document.getElementById("btn-export").onclick = () => exportSection(sec, fieldRefs);
      document.getElementById("btn-close").onclick = () => { currentView = "home"; renderNav(); renderContent(); };
      document.getElementById("btn-delete").onclick = () => deleteSectionContent(sec, fieldRefs);
      return;
    }

    // ── Special: Risk Register — seeded table ──
    if (sec.id === "risk_register") {
      const wrap = document.createElement("div");
      wrap.innerHTML = buildSeededRiskTable();
      content.appendChild(wrap);
    }

    // ── Special: Weekly Governance — seeded ADR ──
    if (sec.id === "weekly_governance") {
      const adr = (sec.fields || []).find(f => f.key === "adr_log");
      if (adr) {
        // Inject seeded ADR above the ADR field — handled below
        content.dataset.showAdr = "1";
      }
    }

    // Fields
    const fieldRefs = {};
    (sec.fields || []).forEach(f => {
      // For weekly_governance, inject seeded ADR example before adr_log field
      if (sec.id === "weekly_governance" && f.key === "adr_log") {
        const adrWrap = document.createElement("div");
        adrWrap.innerHTML = buildSeededADR();
        content.appendChild(adrWrap);
      }

      const block = document.createElement("div");
      block.className = "field-block";
      block.innerHTML = `<div class="field-label">${f.label}</div>`;
      const textarea = document.createElement("textarea");
      textarea.placeholder = f.placeholder;
      textarea.value = (data.fields && data.fields[f.key]) || "";
      textarea.readOnly = !isEditing;
      fieldRefs[f.key] = textarea;
      block.appendChild(textarea);
      content.appendChild(block);
    });

    // Custom section placeholder
    if (sec.isCustom) {
      const ph = document.createElement("div");
      ph.style.cssText = "padding:48px 20px;text-align:center;color:var(--text-dim);font-style:italic;font-size:15px;border:1px solid var(--border);border-radius:10px;";
      ph.textContent = "This file is ready for content. Switch to Edit mode to begin.";
      content.appendChild(ph);
    }

    document.getElementById("btn-save").onclick = () => saveSection(sec, fieldRefs);
    document.getElementById("btn-edit").onclick = () => { editMode[sec.id] = !isEditing; renderContent(); };
    document.getElementById("btn-export").onclick = () => exportSection(sec, fieldRefs);
    document.getElementById("btn-close").onclick = () => { currentView = "home"; renderNav(); renderContent(); };
    document.getElementById("btn-delete").onclick = () => deleteSectionContent(sec, fieldRefs);

    // ── Add File footer ── every section tab
    content.appendChild(buildAddFileFooter(sec.id));
  }

  /* ══════════════════════════════════════════
     HELPERS
  ══════════════════════════════════════════ */
  function pctFor(id) {
    const d = sectionData[id]; if (!d || !d.fields) return 0;
    const vals = Object.values(d.fields);
    const filled = vals.filter(v => v && v.trim()).length;
    return vals.length ? Math.round((filled / vals.length) * 100) : 0;
  }
  function filledCountFor(id) {
    const d = sectionData[id]; if (!d || !d.fields) return 0;
    return Object.values(d.fields).filter(v => v && v.trim()).length;
  }
  function showToast(msg) {
    const t = document.getElementById("toast");
    t.textContent = msg; t.style.display = "block";
    clearTimeout(window._toastTimer);
    window._toastTimer = setTimeout(() => { t.style.display = "none"; }, 2800);
  }

  function saveSection(sec, fieldRefs) {
    const newFields = {};
    (sec.fields || []).forEach(f => { newFields[f.key] = fieldRefs[f.key].value; });
    const merged = { ...sectionData[sec.id], fields: newFields, lastEditedAt: new Date().toISOString() };
    try { localStorage.setItem('dv_sec_' + sec.id, JSON.stringify(merged)); } catch(e) {}
    sectionData[sec.id] = merged;
    showToast('✓ Saved');
  }

  function exportSection(sec, fieldRefs) {
    let text = `${sec.label}\n${"=".repeat(sec.label.length)}\n\n`;
    (sec.fields || []).forEach(f => { text += `${f.label}:\n${fieldRefs[f.key].value || "(empty)"}\n\n`; });
    const blob = new Blob([text], { type: "text/plain" });
    const url = URL.createObjectURL(blob);
    const a = document.createElement("a");
    a.href = url; a.download = `${sec.id}.txt`; a.click();
    URL.revokeObjectURL(url);
    showToast("↓ Exported");
  }

  let _pendingDeleteFn = null;
  function openDeleteConfirm(label, onConfirm) {
    _pendingDeleteFn = onConfirm;
    document.getElementById('dcm-title').textContent = `Clear "${label}"?`;
    const modal = document.getElementById('delete-confirm-modal');
    modal.style.display = 'flex';
    document.getElementById('dcm-confirm-btn').onclick = () => { closeDeleteConfirm(); _pendingDeleteFn && _pendingDeleteFn(); };
  }
  function closeDeleteConfirm() {
    document.getElementById('delete-confirm-modal').style.display = 'none';
  }

  async function deleteSectionContent(sec, fieldRefs) {
    openDeleteConfirm(sec.label, async () => {
      const emptyFields = {};
      (sec.fields || []).forEach(f => emptyFields[f.key] = '');
      try { localStorage.removeItem('dv_sec_' + sec.id); } catch(e) {}
      if (sec.isCustom) {
        customSections = customSections.filter(s => s.id !== sec.id);
        try { localStorage.setItem('dv_custom_sections', JSON.stringify(customSections)); } catch(e) {}
        currentView = 'home'; renderNav(); renderContent();
        showToast('Deleted');
        return;
      }
      sectionData[sec.id] = { ...sectionData[sec.id], fields: emptyFields, completed: false };
      showToast('Cleared');
      renderContent();
    });
  }

  /* ══════════════════════════════════════════
     DOC EDITOR (floating window for custom files)
  ══════════════════════════════════════════ */
  let _docEditorId = null;

  window.openDocEditor = function(id, name, body) {
    _docEditorId = id;
    let overlay = document.getElementById('doc-editor-overlay');
    if (!overlay) {
      overlay = document.createElement('div');
      overlay.id = 'doc-editor-overlay';
      overlay.style.cssText = 'position:fixed;inset:0;background:rgba(0,0,0,0.78);backdrop-filter:blur(8px);z-index:550;display:flex;align-items:center;justify-content:center;';
      overlay.onclick = e => { if (e.target === overlay) saveAndCloseDocEditor(); };
      document.body.appendChild(overlay);
    }
    overlay.innerHTML = `
      <div style="width:min(720px,92vw);height:min(580px,88vh);background:var(--bg-panel);border:1px solid var(--border);border-radius:14px;box-shadow:0 48px 120px rgba(0,0,0,0.75);display:flex;flex-direction:column;overflow:hidden;">
        <div style="display:flex;align-items:center;gap:12px;padding:14px 18px;border-bottom:1px solid var(--border);background:rgba(255,255,255,0.015);flex-shrink:0;">
          <svg width="28" height="28" viewBox="0 0 34 34" xmlns="http://www.w3.org/2000/svg" style="flex-shrink:0;"><circle cx="17" cy="17" r="16" fill="none" stroke="var(--gold)" stroke-width="1.2"/><text x="17" y="22.5" text-anchor="middle" font-family="Cormorant Garamond,serif" font-size="13" font-weight="600" fill="var(--gold)" letter-spacing="-0.5">DV</text><path d="M0,3 C0,1 2,0 3.5,1.5 C5,0 7,1 7,3 C7,5.5 3.5,8 3.5,8 C3.5,8 0,5.5 0,3Z" fill="var(--rose)" transform="translate(21.8,16.4) scale(0.72)"/></svg>
          <div style="flex:1;font-family:'Cormorant Garamond',serif;font-size:16px;font-weight:500;color:var(--text);">${name}</div>
          <div style="display:flex;gap:7px;align-items:center;margin-right:8px;">
            <div onclick="saveAndCloseDocEditor()" style="width:13px;height:13px;border-radius:50%;background:#ff5f57;cursor:pointer;flex-shrink:0;" title="Save &amp; Close"></div>
            <div style="width:13px;height:13px;border-radius:50%;background:rgba(255,255,255,0.1);flex-shrink:0;"></div>
            <div style="width:13px;height:13px;border-radius:50%;background:rgba(255,255,255,0.1);flex-shrink:0;"></div>
          </div>
          <button onclick="saveAndCloseDocEditor()" style="font-family:'JetBrains Mono',monospace;font-size:9.5px;padding:6px 14px;border-radius:6px;border:1px solid rgba(201,164,81,0.3);background:transparent;color:var(--gold);cursor:pointer;">Save &amp; Close</button>
        </div>
        <textarea id="doc-editor-body" style="flex:1;width:100%;padding:28px 32px;background:transparent;border:none;outline:none;resize:none;font-family:'Cormorant Garamond',serif;font-size:16px;line-height:1.9;color:var(--text);" placeholder="Start writing…">${body || ''}</textarea>
        <div style="display:flex;align-items:center;justify-content:space-between;padding:10px 18px;border-top:1px solid var(--border);background:rgba(255,255,255,0.01);">
          <div style="display:flex;gap:8px;">
            <button onclick="exportDocEditor('${name}')" style="font-family:'JetBrains Mono',monospace;font-size:9px;padding:7px 14px;border-radius:6px;border:1px solid var(--border);background:transparent;color:var(--text-dim);cursor:pointer;">↓ Export</button>
            <button onclick="deleteDocEditor('${name}')" style="font-family:'JetBrains Mono',monospace;font-size:9px;padding:7px 14px;border-radius:6px;border:1px solid rgba(212,132,122,0.3);background:transparent;color:var(--rose);cursor:pointer;">Delete</button>
          </div>
          <div style="font-family:'JetBrains Mono',monospace;font-size:8px;color:var(--text-dim);">Auto-saves on close &nbsp;·&nbsp; <span id="doc-editor-status">unsaved</span></div>
        </div>
      </div>`;
    overlay.style.display = 'flex';
  };

  window.exportDocEditor = function(name) {
    const ta = document.getElementById('doc-editor-body');
    const body = ta ? ta.value : '';
    const blob = new Blob([body], { type: 'text/plain' });
    const url = URL.createObjectURL(blob);
    const a = document.createElement('a');
    a.href = url; a.download = (name || 'document') + '.txt'; a.click();
    URL.revokeObjectURL(url);
    showToast('↓ Exported');
  };

  window.deleteDocEditor = function(name) {
    openDeleteConfirm(name, () => {
      if (!_docEditorId) return;
      try { localStorage.removeItem('dv_sec_' + _docEditorId); } catch(e) {}
      customSections = customSections.filter(s => s.id !== _docEditorId);
      try { localStorage.setItem('dv_custom_sections', JSON.stringify(customSections)); } catch(e) {}
      const overlay = document.getElementById('doc-editor-overlay');
      if (overlay) overlay.style.display = 'none';
      _docEditorId = null;
      renderNav();
      showToast('Deleted');
    });
  };

  window.saveAndCloseDocEditor = function() {
    if (!_docEditorId) return;
    const ta = document.getElementById('doc-editor-body');
    const body = ta ? ta.value : '';
    const merged = { ...sectionData[_docEditorId], fields: { body }, lastEditedAt: new Date().toISOString() };
    try { localStorage.setItem('dv_sec_' + _docEditorId, JSON.stringify(merged)); } catch(e) {}
    sectionData[_docEditorId] = merged;
    showToast('✓ Saved');
    const overlay = document.getElementById('doc-editor-overlay');
    if (overlay) overlay.style.display = 'none';
    _docEditorId = null;
  };

  /* ══════════════════════════════════════════
     ADD FILE MODAL
  ══════════════════════════════════════════ */
  let addFileParentId = null;
  window.openAddFile = function(parentId) {
    addFileParentId = parentId || null;
    document.getElementById('add-file-modal').classList.add('open');
    document.getElementById('afm-name').focus();
  };
  window.closeAddFile = function() {
    document.getElementById("add-file-modal").classList.remove("open");
    document.getElementById("afm-name").value = "";
    selectLayout('blank');
  };
  window.handleModalBackdrop = function(e) {
    if (e.target === document.getElementById("add-file-modal")) closeAddFile();
  };
  window.selectLayout = function(layout) {
    addFileLayout = layout;
    document.getElementById("afm-blank").classList.toggle("selected", layout === "blank");
    document.getElementById("afm-clone").classList.toggle("selected", layout === "clone");
  };
  let _modulePresetBody = null;

  window.openAddFileFromModule = function(moduleKey) {
    const m = SA_MODULES.find(x => x.key === moduleKey);
    if (!m) return;
    _modulePresetBody = m.items.map(it => '\u2022 ' + it).join('\n\n');
    addFileParentId = 'system_architecture';
    document.getElementById('afm-name').value = m.name;
    document.getElementById('add-file-modal').classList.add('open');
    const popup = document.getElementById('constellation-popup');
    if (popup) popup.style.display = 'none';
  };

  window.createFile = function() {
    const name = document.getElementById('afm-name').value.trim();
    if (!name) { document.getElementById('afm-name').focus(); return; }
    const id = 'custom_' + Date.now();
    const body = _modulePresetBody || '';
    _modulePresetBody = null;
    const newSection = { id, label: name, icon: '\ud83d\udcc4', motto: 'Custom document', fields: [], isCustom: true, parentId: addFileParentId };
    customSections.push(newSection);
    sectionData[id] = { fields: { body }, completed: false };
    try { localStorage.setItem('dv_custom_sections', JSON.stringify(customSections)); } catch(e){}
    try { localStorage.setItem('dv_sec_' + id, JSON.stringify(sectionData[id])); } catch(e){}
    closeAddFile();
    renderNav();
    openDocEditor(id, name, body);
  };

  /* ══════════════════════════════════════════
     MEDIA PLAYER — Web Audio ambient engine
  ══════════════════════════════════════════ */
  const PLAYLIST = [
    { title:'Architectural Drift',  root:60, scale:[0,2,4,7,9] },
    { title:'Foundation Pulse',     root:57, scale:[0,3,5,7,10] },
    { title:'Midnight Resonance',   root:55, scale:[0,2,5,7,9]  },
    { title:'Golden Thread',        root:62, scale:[0,2,4,7,9]  },
    { title:'Quiet Blueprint',      root:53, scale:[0,3,5,8,10] },
    { title:'Renewal Cycle',        root:58, scale:[0,2,4,7,9]  }
  ];
  let mpIdx=0, mpPlaying=false, mpACtx=null, mpMaster=null, mpReverb=null;
  const mpOscs=[], mpTimers=[];

  function mtof(m){ return 440*Math.pow(2,(m-69)/12); }

  function mpInit(){
    if(mpACtx) return;
    mpACtx = new(window.AudioContext||window.webkitAudioContext)();
    mpMaster = mpACtx.createGain();
    const vol = document.getElementById('mp-vol');
    mpMaster.gain.value = vol ? vol.value/100*0.35 : 0.12;
    // Simple reverb via convolver
    const revLen = mpACtx.sampleRate*2.5, rev = mpACtx.createBuffer(2,revLen,mpACtx.sampleRate);
    for(let ch=0;ch<2;ch++){ const d=rev.getChannelData(ch); for(let i=0;i<revLen;i++) d[i]=(Math.random()*2-1)*Math.pow(1-i/revLen,2); }
    mpReverb = mpACtx.createConvolver(); mpReverb.buffer=rev;
    const revGain=mpACtx.createGain(); revGain.gain.value=0.45;
    mpReverb.connect(revGain); revGain.connect(mpMaster);
    mpMaster.connect(mpACtx.destination);
  }

  function mpStopAll(){
    mpTimers.forEach(t=>clearTimeout(t)); mpTimers.length=0;
    mpOscs.forEach(({osc})=>{ try{osc.stop();}catch(e){} }); mpOscs.length=0;
  }

  function playNote(freq, dur, vol, wave){
    const osc=mpACtx.createOscillator(), env=mpACtx.createGain(), filt=mpACtx.createBiquadFilter();
    osc.type=wave||'sine'; osc.frequency.value=freq;
    filt.type='lowpass'; filt.frequency.value=freq*4; filt.Q.value=0.5;
    env.gain.setValueAtTime(0,mpACtx.currentTime);
    env.gain.linearRampToValueAtTime(vol,mpACtx.currentTime+0.8);
    env.gain.linearRampToValueAtTime(vol*0.7,mpACtx.currentTime+dur*0.6);
    env.gain.linearRampToValueAtTime(0,mpACtx.currentTime+dur);
    osc.connect(filt); filt.connect(env); env.connect(mpMaster); env.connect(mpReverb);
    osc.start(); osc.stop(mpACtx.currentTime+dur+0.05);
    mpOscs.push({osc});
  }

  function mpStartTrack(idx){
    mpStopAll(); mpInit();
    const track=PLAYLIST[idx];
    document.getElementById('mp-track').textContent='♪ '+track.title;
    document.getElementById('mp-play-btn').textContent='⏸';
    const root=track.root, scale=track.scale;

    // Continuous bass drone
    [root-12, root-5].forEach((m,i)=>{
      const osc=mpACtx.createOscillator(), g=mpACtx.createGain(), lfo=mpACtx.createOscillator(), lg=mpACtx.createGain();
      osc.type='sine'; osc.frequency.value=mtof(m); g.gain.value=0.18-i*0.05;
      lfo.frequency.value=0.07+i*0.04; lg.gain.value=mtof(m)*0.008;
      lfo.connect(lg); lg.connect(osc.frequency); osc.connect(g); g.connect(mpMaster);
      lfo.start(); osc.start(); mpOscs.push({osc}); mpOscs.push({osc:lfo});
    });

    // Pad layer — slow chord
    scale.slice(0,4).forEach((s,i)=>{
      const osc=mpACtx.createOscillator(), g=mpACtx.createGain(), lfo=mpACtx.createOscillator(), lg=mpACtx.createGain();
      osc.type='sine'; osc.frequency.value=mtof(root+s); g.gain.value=0.07;
      lfo.frequency.value=0.05+i*0.02; lg.gain.value=mtof(root+s)*0.003;
      lfo.connect(lg); lg.connect(osc.frequency); osc.connect(g); g.connect(mpReverb);
      lfo.start(); osc.start(); mpOscs.push({osc}); mpOscs.push({osc:lfo});
    });

    // Melodic note sequence
    let step=0;
    function scheduleNote(){
      if(!mpPlaying) return;
      const degree=scale[Math.floor(Math.random()*scale.length)];
      const octave=Math.random()<0.3?1:0;
      const freq=mtof(root+degree+octave*12);
      const dur=2.5+Math.random()*4;
      playNote(freq,dur,0.05+(Math.random()*0.04),'sine');
      const delay=(1200+Math.random()*3500);
      mpTimers.push(setTimeout(scheduleNote,delay));
    }
    mpTimers.push(setTimeout(scheduleNote,800));
    mpPlaying=true;
  }

  window.mpToggle=function(){ if(!mpPlaying){mpStartTrack(mpIdx);}else{mpStopAll();mpPlaying=false;document.getElementById('mp-play-btn').textContent='▶';} };
  window.mpNext=function(){ mpIdx=(mpIdx+1)%PLAYLIST.length; if(mpPlaying)mpStartTrack(mpIdx); else document.getElementById('mp-track').textContent='♪ '+PLAYLIST[mpIdx].title; };
  window.mpPrev=function(){ mpIdx=(mpIdx-1+PLAYLIST.length)%PLAYLIST.length; if(mpPlaying)mpStartTrack(mpIdx); else document.getElementById('mp-track').textContent='♪ '+PLAYLIST[mpIdx].title; };
  window.mpVolume=function(v){ if(mpMaster)mpMaster.gain.value=v/100*0.35; };

  /* ══════════════════════════════════════════
     GLOBALS
  ══════════════════════════════════════════ */
  window.highlightModule = function(key, event) {
    const m = SA_MODULES.find(x => x.key === key);
    if (!m) return;
    let popup = document.getElementById('constellation-popup');
    if (!popup) {
      popup = document.createElement('div');
      popup.id = 'constellation-popup';
      popup.style.cssText = 'position:fixed;z-index:600;background:var(--bg-panel);border:1px solid var(--border);border-radius:12px;padding:16px 18px;box-shadow:0 20px 60px rgba(0,0,0,0.6);min-width:220px;max-width:260px;pointer-events:auto;';
      popup.onclick = e => e.stopPropagation();
      document.body.appendChild(popup);
    }
    popup.innerHTML = `
      <div style="display:flex;align-items:center;gap:8px;margin-bottom:12px;">
        <div style="width:10px;height:10px;border-radius:50%;background:${m.color};flex-shrink:0;"></div>
        <div style="font-family:'Cormorant Garamond',serif;font-size:16px;font-weight:500;color:var(--text);">${m.name}</div>
        <div onclick="document.getElementById('constellation-popup').style.display='none'; if(window._constellationZoom) window._constellationZoom(null);" style="margin-left:auto;cursor:pointer;color:var(--text-dim);font-size:16px;line-height:1;">✕</div>
      </div>
      <div style="display:flex;flex-direction:column;gap:6px;margin-bottom:12px;">
        ${m.items.map(it => `<div style="display:flex;align-items:center;gap:8px;font-size:13px;color:var(--text-dim);font-style:italic;"><div style="width:4px;height:4px;border-radius:50%;background:${m.color};flex-shrink:0;opacity:0.7;"></div>${it}</div>`).join('')}
      </div>
      <div style="display:flex;flex-direction:column;gap:8px;padding-top:10px;border-top:1px solid var(--border);">
        <div onclick="openAddFileFromModule('${key}')" style="display:flex;align-items:center;gap:8px;padding:9px 12px;border:1.5px dashed rgba(212,132,122,0.35);border-radius:8px;cursor:pointer;" onmouseover="this.style.background='rgba(212,132,122,0.07)'" onmouseout="this.style.background='transparent'">
          <span style="font-size:15px;color:rgba(212,132,122,0.8);">+</span>
          <span style="font-family:'JetBrains Mono',monospace;font-size:9px;color:rgba(212,132,122,0.72);">Add file to ${m.name}</span>
        </div>
        <div onclick="highlightCard('${key}')" style="font-family:'JetBrains Mono',monospace;font-size:8.5px;color:var(--gold);cursor:pointer;letter-spacing:0.5px;text-align:center;padding:4px 0;">View module card ↓</div>
      </div>`;
    // Position popup near the SVG — offset from top of content
    // Position near clicked node
    popup.style.display = 'block';
    const vw = window.innerWidth, vh = window.innerHeight, pw = 260, ph = 230;
    let left = event.clientX + 14;
    let top = event.clientY + 14;
    if (left + pw > vw - 8) left = event.clientX - pw - 14;
    if (top + ph > vh - 8) top = event.clientY - ph - 14;
    popup.style.left = left + 'px';
    popup.style.top = top + 'px';
    popup.style.right = '';
    // Auto-hide after 8s
    clearTimeout(window._cpTimer);
    window._cpTimer = setTimeout(() => { popup.style.display = 'none'; }, 8000);
  };

  window.highlightCard = function(key) {
    document.querySelectorAll('.sa-card').forEach(c => c.classList.remove('sa-highlighted'));
    const card = document.getElementById('sa-card-' + key);
    if (!card) return;
    card.classList.add('sa-highlighted');
    const content = document.getElementById('content');
    if (content) content.scrollTop = card.offsetTop - 80;
    setTimeout(() => card.classList.remove('sa-highlighted'), 2200);
    const popup = document.getElementById('constellation-popup');
    if (popup) popup.style.display = 'none';
  };

  window.goHome = function() { currentView = "home"; renderNav(); renderContent(); };

  /* ══════════════════════════════════════════
     INIT
  ══════════════════════════════════════════ */
  // Load section data from localStorage (offline fallback)
  function loadFromLocal() {
    SECTIONS.forEach(sec => {
      try {
        const raw = localStorage.getItem("dv_sec_" + sec.id);
        if (raw) { sectionData[sec.id] = JSON.parse(raw); return; }
      } catch(e) {}
      const fieldsObj = {};
      (sec.fields || []).forEach(f => fieldsObj[f.key] = "");
      sectionData[sec.id] = { fields: fieldsObj, completed: false };
    });
  }

  function init() {
    // Restore theme immediately
    try {
      const saved = localStorage.getItem("dv_theme") || "midnight";
      applyTheme(saved);
    } catch(e) { applyTheme("midnight"); }

    // Restore custom sections
    try {
      const cs = JSON.parse(localStorage.getItem("dv_custom_sections") || "[]");
      customSections = cs;
    } catch(e) {}

    // Always load from local first so the app renders immediately
    loadFromLocal();
    currentView = "home";
    renderNav();
    renderContent();
    document.getElementById("loading-screen").style.display = "none";
    document.getElementById("app").style.display = "flex";
    document.getElementById("status-badge").textContent = "● local";
  }

  init();
</script>
</body>
</html>

```
