# Food-waste-management
A system to track reduce and manage food waste
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>FreshTrack – Food Waste Manager</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Mono:wght@300;400;500&display=swap" rel="stylesheet"/>
<style>
  :root {
    --bg: #0e0f0a;
    --surface: #161710;
    --card: #1c1e14;
    --border: #2a2d1e;
    --accent: #b5e550;
    --accent2: #f0a500;
    --accent3: #ff6b6b;
    --text: #e8ead8;
    --muted: #6b6f54;
    --green: #6fcf4a;
    --yellow: #f0c030;
    --red: #ff5050;
  }
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    font-family: 'DM Mono', monospace;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* BACKGROUND TEXTURE */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      radial-gradient(ellipse 80% 60% at 10% 0%, #b5e55012 0%, transparent 60%),
      radial-gradient(ellipse 60% 50% at 90% 100%, #f0a50010 0%, transparent 60%);
    pointer-events: none;
    z-index: 0;
  }

  /* HEADER */
  header {
    position: sticky;
    top: 0;
    z-index: 100;
    background: rgba(14,15,10,0.88);
    backdrop-filter: blur(16px);
    border-bottom: 1px solid var(--border);
    padding: 0 2rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 64px;
  }
  .logo {
    font-family: 'Syne', sans-serif;
    font-weight: 800;
    font-size: 1.3rem;
    letter-spacing: -0.02em;
    color: var(--accent);
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }
  .logo span { color: var(--text); font-weight: 400; }
  .header-stats {
    display: flex;
    gap: 2rem;
    font-size: 0.72rem;
    color: var(--muted);
    letter-spacing: 0.05em;
    text-transform: uppercase;
  }
  .header-stats strong { color: var(--accent); font-size: 1rem; display: block; font-family: 'Syne', sans-serif; font-weight: 700; }

  /* MAIN */
  main {
    position: relative;
    z-index: 1;
    max-width: 1100px;
    margin: 0 auto;
    padding: 2.5rem 1.5rem 4rem;
  }

  /* HERO */
  .hero {
    margin-bottom: 2.5rem;
    display: flex;
    align-items: flex-end;
    justify-content: space-between;
    gap: 1rem;
    flex-wrap: wrap;
  }
  .hero-title {
    font-family: 'Syne', sans-serif;
    font-size: clamp(2rem, 5vw, 3.2rem);
    font-weight: 800;
    line-height: 1.0;
    letter-spacing: -0.04em;
  }
  .hero-title em {
    font-style: normal;
    color: var(--accent);
    display: block;
  }
  .hero-sub {
    color: var(--muted);
    font-size: 0.78rem;
    letter-spacing: 0.05em;
    text-transform: uppercase;
    margin-top: 0.5rem;
  }

  /* TABS */
  .tabs {
    display: flex;
    gap: 0.4rem;
    margin-bottom: 2rem;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 0.35rem;
    width: fit-content;
  }
  .tab-btn {
    background: none;
    border: none;
    color: var(--muted);
    font-family: 'DM Mono', monospace;
    font-size: 0.78rem;
    padding: 0.5rem 1.2rem;
    border-radius: 8px;
    cursor: pointer;
    letter-spacing: 0.04em;
    transition: all 0.2s;
  }
  .tab-btn.active {
    background: var(--accent);
    color: #0e0f0a;
    font-weight: 500;
  }

  /* SECTIONS */
  .section { display: none; }
  .section.active { display: block; }

  /* ADD FORM */
  .form-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 2rem;
    margin-bottom: 2rem;
  }
  .form-title {
    font-family: 'Syne', sans-serif;
    font-size: 1rem;
    font-weight: 700;
    color: var(--accent);
    text-transform: uppercase;
    letter-spacing: 0.08em;
    margin-bottom: 1.5rem;
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }
  .form-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1rem;
    margin-bottom: 1.2rem;
  }
  .field label {
    display: block;
    font-size: 0.7rem;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 0.08em;
    margin-bottom: 0.4rem;
  }
  .field input, .field select {
    width: 100%;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 8px;
    color: var(--text);
    font-family: 'DM Mono', monospace;
    font-size: 0.85rem;
    padding: 0.65rem 0.9rem;
    outline: none;
    transition: border-color 0.2s;
  }
  .field input:focus, .field select:focus { border-color: var(--accent); }
  .field select option { background: var(--surface); }

  .btn-primary {
    background: var(--accent);
    color: #0e0f0a;
    border: none;
    border-radius: 8px;
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 0.85rem;
    letter-spacing: 0.04em;
    padding: 0.75rem 2rem;
    cursor: pointer;
    transition: opacity 0.2s, transform 0.15s;
    text-transform: uppercase;
  }
  .btn-primary:hover { opacity: 0.88; transform: translateY(-1px); }

  /* FILTERS */
  .filter-row {
    display: flex;
    gap: 0.5rem;
    margin-bottom: 1.5rem;
    flex-wrap: wrap;
    align-items: center;
  }
  .filter-btn {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 6px;
    color: var(--muted);
    font-family: 'DM Mono', monospace;
    font-size: 0.72rem;
    padding: 0.4rem 0.9rem;
    cursor: pointer;
    transition: all 0.2s;
    letter-spacing: 0.03em;
  }
  .filter-btn.active, .filter-btn:hover { border-color: var(--accent); color: var(--accent); }
  .search-input {
    margin-left: auto;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 6px;
    color: var(--text);
    font-family: 'DM Mono', monospace;
    font-size: 0.78rem;
    padding: 0.4rem 0.9rem;
    outline: none;
    width: 180px;
    transition: border-color 0.2s;
  }
  .search-input:focus { border-color: var(--accent); }

  /* FOOD GRID */
  .food-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 1rem;
  }

  .food-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 1.3rem;
    display: flex;
    flex-direction: column;
    gap: 0.8rem;
    position: relative;
    transition: border-color 0.2s, transform 0.2s;
    animation: fadeUp 0.3s ease both;
  }
  .food-card:hover { border-color: var(--accent); transform: translateY(-2px); }
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(12px); }
    to   { opacity: 1; transform: translateY(0); }
  }

  .food-card-top {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
  }
  .food-emoji { font-size: 2rem; line-height: 1; }
  .status-badge {
    font-size: 0.62rem;
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    padding: 0.2rem 0.6rem;
    border-radius: 4px;
  }
  .status-good   { background: #6fcf4a20; color: var(--green); border: 1px solid #6fcf4a30; }
  .status-soon   { background: #f0c03020; color: var(--yellow); border: 1px solid #f0c03030; }
  .status-urgent { background: #ff505020; color: var(--red); border: 1px solid #ff505030; }
  .status-expired{ background: #ff000015; color: #ff4444; border: 1px solid #ff000025; }

  .food-name {
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 1.05rem;
    letter-spacing: -0.01em;
  }
  .food-meta {
    display: flex;
    flex-direction: column;
    gap: 0.3rem;
    font-size: 0.72rem;
    color: var(--muted);
  }
  .food-meta span { display: flex; justify-content: space-between; }
  .food-meta span b { color: var(--text); font-weight: 400; }

  .days-bar {
    height: 3px;
    background: var(--border);
    border-radius: 99px;
    overflow: hidden;
  }
  .days-fill {
    height: 100%;
    border-radius: 99px;
    transition: width 0.5s ease;
  }

  .card-actions {
    display: flex;
    gap: 0.5rem;
    margin-top: 0.2rem;
  }
  .btn-sm {
    flex: 1;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 6px;
    color: var(--muted);
    font-family: 'DM Mono', monospace;
    font-size: 0.68rem;
    padding: 0.4rem;
    cursor: pointer;
    transition: all 0.2s;
    letter-spacing: 0.03em;
  }
  .btn-sm:hover { border-color: var(--accent3); color: var(--accent3); }
  .btn-sm.donate:hover { border-color: var(--accent); color: var(--accent); }

  /* EMPTY STATE */
  .empty-state {
    text-align: center;
    padding: 4rem 2rem;
    color: var(--muted);
  }
  .empty-state .icon { font-size: 3.5rem; margin-bottom: 1rem; }
  .empty-state p { font-size: 0.85rem; }

  /* DASHBOARD */
  .dash-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1rem;
    margin-bottom: 2rem;
  }
  .stat-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 1.5rem;
  }
  .stat-label {
    font-size: 0.68rem;
    color: var(--muted);
    text-transform: uppercase;
    letter-spacing: 0.08em;
    margin-bottom: 0.5rem;
  }
  .stat-value {
    font-family: 'Syne', sans-serif;
    font-size: 2.2rem;
    font-weight: 800;
    line-height: 1;
    letter-spacing: -0.04em;
  }
  .stat-value.green { color: var(--green); }
  .stat-value.yellow { color: var(--yellow); }
  .stat-value.red { color: var(--red); }
  .stat-value.accent { color: var(--accent); }
  .stat-sub { font-size: 0.68rem; color: var(--muted); margin-top: 0.3rem; }

  /* CHART */
  .chart-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 1.5rem;
    margin-bottom: 1rem;
  }
  .chart-label {
    font-family: 'Syne', sans-serif;
    font-size: 0.78rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.08em;
    color: var(--muted);
    margin-bottom: 1.2rem;
  }
  .bar-chart { display: flex; flex-direction: column; gap: 0.8rem; }
  .bar-row { display: flex; align-items: center; gap: 1rem; font-size: 0.72rem; }
  .bar-name { width: 90px; color: var(--muted); text-align: right; white-space: nowrap; overflow: hidden; text-overflow: ellipsis; }
  .bar-track { flex: 1; height: 8px; background: var(--border); border-radius: 99px; overflow: hidden; }
  .bar-fill { height: 100%; border-radius: 99px; background: var(--accent); transition: width 0.6s ease; }
  .bar-val { width: 30px; color: var(--text); text-align: right; }

  /* DONATION LOG */
  .log-list { display: flex; flex-direction: column; gap: 0.6rem; }
  .log-item {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 0.9rem 1.2rem;
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 0.78rem;
    animation: fadeUp 0.3s ease both;
  }
  .log-item .log-name { font-family: 'Syne', sans-serif; font-weight: 600; }
  .log-item .log-date { color: var(--muted); font-size: 0.68rem; }
  .log-tag {
    font-size: 0.62rem;
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    letter-spacing: 0.06em;
    text-transform: uppercase;
    background: #b5e55020;
    color: var(--accent);
    border: 1px solid #b5e55030;
    padding: 0.2rem 0.6rem;
    border-radius: 4px;
  }

  /* TOAST */
  #toast {
    position: fixed;
    bottom: 2rem;
    right: 2rem;
    background: var(--accent);
    color: #0e0f0a;
    font-family: 'Syne', sans-serif;
    font-weight: 700;
    font-size: 0.82rem;
    padding: 0.8rem 1.5rem;
    border-radius: 10px;
    z-index: 999;
    transform: translateY(100px);
    opacity: 0;
    transition: all 0.3s ease;
    pointer-events: none;
  }
  #toast.show { transform: translateY(0); opacity: 1; }

  @media (max-width: 600px) {
    header { padding: 0 1rem; }
    .header-stats { gap: 1rem; }
    main { padding: 1.5rem 1rem 3rem; }
    .hero-title { font-size: 1.8rem; }
  }
</style>
</head>
<body>

<header>
  <div class="logo">🌿 Fresh<span>Track</span></div>
  <div class="header-stats">
    <div><strong id="h-total">0</strong>items tracked</div>
    <div><strong id="h-expiring">0</strong>expiring soon</div>
    <div><strong id="h-donated">0</strong>donated</div>
  </div>
</header>

<main>
  <div class="hero">
    <div>
      <div class="hero-title">Reduce<em>Food Waste.</em></div>
      <div class="hero-sub">Track · Alert · Donate · Analyse</div>
    </div>
  </div>

  <!-- TABS -->
  <div class="tabs">
    <button class="tab-btn active" onclick="switchTab('inventory')">📦 Inventory</button>
    <button class="tab-btn" onclick="switchTab('add')">➕ Add Item</button>
    <button class="tab-btn" onclick="switchTab('dashboard')">📊 Dashboard</button>
    <button class="tab-btn" onclick="switchTab('donations')">🤝 Donations</button>
  </div>

  <!-- INVENTORY SECTION -->
  <div class="section active" id="sec-inventory">
    <div class="filter-row">
      <button class="filter-btn active" onclick="setFilter('all', this)">All</button>
      <button class="filter-btn" onclick="setFilter('good', this)">✅ Fresh</button>
      <button class="filter-btn" onclick="setFilter('soon', this)">⚠️ Use Soon</button>
      <button class="filter-btn" onclick="setFilter('urgent', this)">🔴 Urgent</button>
      <button class="filter-btn" onclick="setFilter('expired', this)">💀 Expired</button>
      <input class="search-input" type="text" placeholder="search items..." oninput="renderInventory()" id="searchInput"/>
    </div>
    <div class="food-grid" id="foodGrid"></div>
  </div>

  <!-- ADD SECTION -->
  <div class="section" id="sec-add">
    <div class="form-card">
      <div class="form-title">📥 Add Food Item</div>
      <div class="form-grid">
        <div class="field">
          <label>Food Name</label>
          <input type="text" id="f-name" placeholder="e.g. Milk, Apples…"/>
        </div>
        <div class="field">
          <label>Category</label>
          <select id="f-cat">
            <option value="🥛 Dairy">🥛 Dairy</option>
            <option value="🥩 Meat">🥩 Meat</option>
            <option value="🥦 Vegetables">🥦 Vegetables</option>
            <option value="🍎 Fruits">🍎 Fruits</option>
            <option value="🍞 Bakery">🍞 Bakery</option>
            <option value="🥫 Canned">🥫 Canned</option>
            <option value="🍳 Cooked">🍳 Cooked</option>
            <option value="🧊 Frozen">🧊 Frozen</option>
            <option value="🫙 Other">🫙 Other</option>
          </select>
        </div>
        <div class="field">
          <label>Quantity</label>
          <input type="text" id="f-qty" placeholder="e.g. 500g, 2 pcs"/>
        </div>
        <div class="field">
          <label>Expiry Date</label>
          <input type="date" id="f-expiry"/>
        </div>
        <div class="field">
          <label>Storage Location</label>
          <select id="f-loc">
            <option>Fridge</option>
            <option>Freezer</option>
            <option>Pantry</option>
            <option>Counter</option>
          </select>
        </div>
        <div class="field">
          <label>Notes</label>
          <input type="text" id="f-notes" placeholder="optional notes…"/>
        </div>
      </div>
      <button class="btn-primary" onclick="addItem()">+ Add to Inventory</button>
    </div>
  </div>

  <!-- DASHBOARD SECTION -->
  <div class="section" id="sec-dashboard">
    <div class="dash-grid">
      <div class="stat-card">
        <div class="stat-label">Total Items</div>
        <div class="stat-value accent" id="d-total">0</div>
        <div class="stat-sub">in inventory</div>
      </div>
      <div class="stat-card">
        <div class="stat-label">Fresh Items</div>
        <div class="stat-value green" id="d-good">0</div>
        <div class="stat-sub">more than 5 days left</div>
      </div>
      <div class="stat-card">
        <div class="stat-label">Expiring Soon</div>
        <div class="stat-value yellow" id="d-soon">0</div>
        <div class="stat-sub">within 5 days</div>
      </div>
      <div class="stat-card">
        <div class="stat-label">Expired</div>
        <div class="stat-value red" id="d-expired">0</div>
        <div class="stat-sub">past expiry date</div>
      </div>
      <div class="stat-card">
        <div class="stat-label">Total Donated</div>
        <div class="stat-value accent" id="d-donated">0</div>
        <div class="stat-sub">items saved from waste</div>
      </div>
    </div>
    <div class="chart-card">
      <div class="chart-label">📦 Items by Category</div>
      <div class="bar-chart" id="catChart"></div>
    </div>
    <div class="chart-card">
      <div class="chart-label">📍 Items by Location</div>
      <div class="bar-chart" id="locChart"></div>
    </div>
  </div>

  <!-- DONATIONS SECTION -->
  <div class="section" id="sec-donations">
    <div class="form-card" style="margin-bottom:1.5rem;">
      <div class="form-title">🤝 Donation Log</div>
      <p style="font-size:0.78rem;color:var(--muted);">Items marked as donated from inventory appear here. Every item donated is food saved from the bin.</p>
    </div>
    <div class="log-list" id="donationLog"></div>
  </div>
</main>

<div id="toast">✅ Done!</div>

<script>
// ─── STATE ───────────────────────────────────────────────────
let items = JSON.parse(localStorage.getItem('fw_items') || '[]');
let donations = JSON.parse(localStorage.getItem('fw_donations') || '[]');
let currentFilter = 'all';

const EMOJIS = {
  '🥛 Dairy':'🥛','🥩 Meat':'🥩','🥦 Vegetables':'🥦','🍎 Fruits':'🍎',
  '🍞 Bakery':'🍞','🥫 Canned':'🥫','🍳 Cooked':'🍳','🧊 Frozen':'🧊','🫙 Other':'🫙'
};

// ─── UTILS ───────────────────────────────────────────────────
function save() {
  localStorage.setItem('fw_items', JSON.stringify(items));
  localStorage.setItem('fw_donations', JSON.stringify(donations));
  updateHeader();
}

function daysLeft(expiry) {
  const today = new Date(); today.setHours(0,0,0,0);
  const exp = new Date(expiry); exp.setHours(0,0,0,0);
  return Math.round((exp - today) / 86400000);
}

function getStatus(days) {
  if (days < 0)  return 'expired';
  if (days <= 2) return 'urgent';
  if (days <= 5) return 'soon';
  return 'good';
}

function statusLabel(days) {
  if (days < 0)  return { label: 'EXPIRED', cls: 'status-expired' };
  if (days <= 2) return { label: `${days}d LEFT`, cls: 'status-urgent' };
  if (days <= 5) return { label: `${days}d LEFT`, cls: 'status-soon' };
  return { label: 'FRESH', cls: 'status-good' };
}

function barColor(days) {
  if (days < 0)  return '#ff4444';
  if (days <= 2) return '#ff5050';
  if (days <= 5) return '#f0c030';
  return '#6fcf4a';
}

function toast(msg) {
  const t = document.getElementById('toast');
  t.textContent = msg;
  t.classList.add('show');
  setTimeout(() => t.classList.remove('show'), 2500);
}

function updateHeader() {
  document.getElementById('h-total').textContent = items.length;
  document.getElementById('h-expiring').textContent = items.filter(i => {
    const d = daysLeft(i.expiry); return d >= 0 && d <= 5;
  }).length;
  document.getElementById('h-donated').textContent = donations.length;
}

// ─── TAB ─────────────────────────────────────────────────────
function switchTab(id) {
  document.querySelectorAll('.section').forEach(s => s.classList.remove('active'));
  document.querySelectorAll('.tab-btn').forEach(b => b.classList.remove('active'));
  document.getElementById('sec-' + id).classList.add('active');
  event.target.classList.add('active');
  if (id === 'dashboard') renderDashboard();
  if (id === 'inventory') renderInventory();
  if (id === 'donations') renderDonations();
}

// ─── ADD ITEM ─────────────────────────────────────────────────
function addItem() {
  const name   = document.getElementById('f-name').value.trim();
  const cat    = document.getElementById('f-cat').value;
  const qty    = document.g
