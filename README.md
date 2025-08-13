<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover" />
  <meta name="apple-mobile-web-app-capable" content="yes" />
  <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent" />
  <meta name="apple-mobile-web-app-title" content="Su tienda" />
  <link id="manifestLink" rel="manifest" href="#" />
  <!-- Título ajustado con estilo y redacción en español -->
  <title>Su Tienda | Neon, categorías, editor y combos opcionales</title>
  <style>
    :root{
      --bg:#0b1220;--panel:#0f172a;--card:#0c1424;--text:#e6edf7;--muted:#93a1b4;
      --border:#1f2a44;--ring:#3b82f6;--green:#22c55e;--blue:#3b82f6;--amber:#f59e0b;--red:#ef4444;
    }
    *{box-sizing:border-box}
    html,body{height:100%}
    body{margin:0;background:linear-gradient(180deg,#0a0f1d,#0b1220);color:var(--text);font-family:system-ui,-apple-system,Segoe UI,Roboto,Helvetica,Arial,sans-serif;-webkit-tap-highlight-color:transparent}
    .safe{padding:calc(14px + env(safe-area-inset-top)) 14px calc(14px + env(safe-area-inset-bottom))}
    header{padding:12px 16px;border-bottom:1px solid var(--border);background:rgba(4,8,20,.55);backdrop-filter:blur(10px);position:sticky;top:0;z-index:20}
    h1{margin:0;font-size:18px;letter-spacing:.3px}
    .wrap{max-width:1100px;margin:0 auto;padding:16px}
    button,input,select{border:1px solid var(--border);background:#0e162a;color:var(--text);border-radius:14px;padding:12px 14px;font-size:16px}
    button{cursor:pointer;display:inline-flex;gap:8px;align-items:center;transition:transform .05s ease,opacity .2s}
    button:active{transform:scale(.98)}
    .primary{background:linear-gradient(180deg,#16a34a,var(--green));border-color:#16a34a;font-weight:700}
    .blue{background:linear-gradient(180deg,#2563eb,var(--blue));border-color:#2563eb}
    /* botones fantasma con degradado sutil */
    .ghost{
      background:linear-gradient(180deg, rgba(17,27,46,.85), rgba(10,18,33,.85));
    }
    .ghost:hover{
      background:linear-gradient(180deg, rgba(10,18,33,.9), rgba(17,27,46,.9));
    }
    .grid{display:grid;grid-template-columns:repeat(auto-fill,minmax(330px,1fr));gap:14px}
    .card{background:linear-gradient(180deg,rgba(13,20,36,.9),rgba(9,15,28,.9));border:1px solid var(--border);border-radius:18px;padding:14px;box-shadow:0 12px 36px rgba(0,0,0,.35)}
    .row{display:flex;gap:10px;align-items:center;flex-wrap:wrap}
    .sp{display:flex;justify-content:space-between;align-items:center;gap:12px}
    .muted{color:var(--muted);font-size:12px}
    .kpi{display:grid;grid-template-columns:repeat(6,minmax(120px,1fr));gap:10px;margin:12px 0 18px}
    .kpi .card{padding:12px}
    .kpi h3{margin:0 0 6px 0;font-size:12px;color:var(--muted);font-weight:500}
    .kpi .val{font-size:22px;font-weight:800}
    .qty{font-variant-numeric:tabular-nums}
    .tag{padding:6px 10px;border-radius:999px;background:#101a32;border:1px solid var(--border);font-size:13px;position:relative}
    .save-dot{position:absolute;top:-4px;right:-4px;width:8px;height:8px;border-radius:50%;background:#22c55e;opacity:0;transition:opacity .25s}
    /* Ajustes estéticos para las pastillas de categoría */
    .chip{
      padding:8px 14px;
      border-radius:999px;
      border:1px solid var(--border);
      background:#0e162a;
      font-size:14px;
      cursor:pointer;
      user-select:none;
      transition:background .15s,border-color .15s,box-shadow .2s;
    }
    .chip:hover{
      background:#152341;
    }
    .chip.active{
      border-color:var(--ring);
      box-shadow:0 0 0 2px var(--ring);
    }
    .right{text-align:right}
    .badge{padding:4px 8px;border-radius:999px;font-size:12px;border:1px solid var(--border)}
    .badge-red{background:#3b0f14;color:#fecaca}
    .badge-yellow{background:#3b2f0f;color:#fde68a}
    .badge-green{background:#0f3b21;color:#bbf7d0}
    .toast{position:fixed;left:50%;bottom:18px;transform:translateX(-50%);background:#0b1220;border:1px solid var(--border);border-radius:999px;padding:10px 14px;font-size:14px;color:var(--text);opacity:0;pointer-events:none;transition:opacity .25s, transform .25s;box-shadow:0 8px 24px rgba(0,0,0,.35);z-index:50}
    .toast.show{opacity:1;transform:translateX(-50%) translateY(0)}
    .toast.ok{border-color:#16a34a}
    .toast.edit{border-color:#2563eb}
    .card.editing{outline:2px dashed #2563eb; outline-offset:4px}
    /* pill inputs for editor */
    .pill{background:#0f182c;border:1px solid var(--border);color:var(--text);border-radius:999px;padding:10px 14px;font-size:14px}
    .editor{margin-top:10px;border-top:1px dashed var(--border);padding-top:10px;display:none}
    .editor.open{display:block}
    .editor .row{gap:8px}
    .btn-mini{padding:10px 12px;border-radius:12px}
    .toggle{position:relative;width:54px;height:32px;border-radius:999px;background:#0e162a;border:1px solid var(--border);cursor:pointer}
    .toggle i{position:absolute;top:3px;left:3px;width:26px;height:26px;border-radius:50%;background:#94a3b8;transition:left .2s, background .2s}
    .toggle.on{background:#063a1e;border-color:#16a34a}
    .toggle.on i{left:25px;background:#22c55e}
    /* beams */
    :root{
      --beam1: radial-gradient(1200px 400px at -10% -10%, rgba(59,130,246,.32), transparent 60%);
      --beam2: radial-gradient(900px 400px at 110% -20%, rgba(99,102,241,.28), transparent 60%);
      --beam3: radial-gradient(700px 400px at 50% -10%, rgba(16,185,129,.28), transparent 60%);
    }
    .beams::before,
    .beams::after{content:""; position:fixed; inset:0; pointer-events:none; z-index:0;}
    .beams::before{ background: var(--beam1), var(--beam2), var(--beam3); filter: blur(.5px); opacity:.85 }
    .beams::after{ background: radial-gradient(800px 300px at 50% -10%, rgba(255,255,255,.06), transparent 60%) }
    /* table */
    .log{max-height:260px;overflow:auto;border-radius:12px;border:1px solid var(--border);background:#0e162a}
    table{width:100%;border-collapse:separate;border-spacing:0}
    th,td{padding:12px;border-bottom:1px solid var(--border);font-size:14px}
    th{position:sticky;top:0;background:#0e162a;text-align:left;z-index:1}
    /* brand header */
    .brand{display:flex;align-items:center;gap:10px;min-width:0}
    .brand img{width:28px;height:28px;object-fit:contain;display:block}
    .brand .title{font-weight:800;letter-spacing:.3px;white-space:nowrap}
    @media (min-width:768px){
      .brand img{width:32px;height:32px}
      .brand .title{font-size:18px}
    }
    @media (max-width:767px){
      .brand .title{font-size:16px}
    }
    /* category bar */
    .cats-wrap{display:flex;flex-direction:column;gap:6px;margin-left:8px}
    .cats-title{margin:0;color:var(--muted);font-size:12px;font-weight:600;letter-spacing:.4px}
    .cats{display:flex;gap:8px;flex-wrap:wrap}

    /* ===== Responsive adjustments for mobile ===== */
    @media (max-width: 640px){
      /* Stack the header controls vertically */
      header .row{
        flex-direction:column;
        align-items:stretch;
        gap:8px;
      }
      header .row > *{
        width:100%;
      }
      /* Remove left margin on the categories wrapper */
      .cats-wrap{ margin-left:0; }
      /* Adjust chip layout on mobile */
      .cats{ gap:6px; }
      .chip{
        flex:1 1 auto;
        justify-content:center;
        padding:10px 12px;
      }
      /* Make mini buttons full width for easier tapping */
      .btn-mini{ width:100%; }
      /* Adjust KPI grid to fewer columns on small screens */
      .kpi{ grid-template-columns: repeat(auto-fill, minmax(160px, 1fr)); }
      /* Display product cards in a single column */
      .grid{ grid-template-columns:1fr; }
    }
  
/* === Top header estilo pastillas === */
.topbar{display:flex;align-items:center;justify-content:space-between;gap:14px}
.navwrap{display:flex;align-items:center;gap:18px}
.menu{display:flex;align-items:center;gap:10px;background:rgba(16,23,42,.65);border:1px solid var(--border);border-radius:18px;padding:6px}
.menu a{
  display:inline-flex;align-items:center;justify-content:center;
  padding:10px 16px;border-radius:14px;font-weight:600;font-size:14px;
  color:var(--text);text-decoration:none;opacity:.85;transition:all .2s ease;
}
.menu a:hover{opacity:1}
.menu a.active{
  background:#0b1220;color:#e6edf7;
  border:1px solid var(--ring);
  box-shadow:0 0 0 2px var(--ring) inset, 0 8px 28px rgba(0,0,0,.35);
}
.menu a:active{transform:translateY(1px)}
.top-actions{display:flex;align-items:center;gap:12px}
.pilllink{
  display:inline-flex;align-items:center;justify-content:center;
  padding:10px 16px;border-radius:14px;font-weight:600;font-size:14px;
  color:var(--text);text-decoration:none;background:rgba(21,33,65,.35);
  border:1px solid var(--border);opacity:.9;transition:all .2s ease;
}
.pilllink:hover{opacity:1}
@media (max-width:820px){
  .menu{overflow:auto;max-width:60vw}
  .menu a{white-space:nowrap}
}
/* Ocultar barra antigua cuando usemos la superior */
header .cats-wrap .cats.is-hidden{display:none}

</style>
</head>
<body class="safe beams">

<header>
  <div class="wrap topbar">
    <div class="brand">
      <img src="Objeto-inteligente-vectorial.png" alt="Logo de Su Tienda" />
      <div class="title">SU TIENDA</div>
    </div>
    <div class="navwrap" style="flex:1;justify-content:center;">
      <nav class="menu" role="tablist" aria-label="Categorías">
        <a href="#c-todos" data-cat="Todos" class="active" aria-selected="true">Todos (0)</a>
        <a href="#c-bebidas" data-cat="Bebidas" aria-selected="false">Bebidas (0)</a>
        <a href="#c-snacks" data-cat="Snacks" aria-selected="false">Snacks (0)</a>
        <a href="#c-tabaco" data-cat="Tabaco" aria-selected="false">Tabaco (0)</a>
        <a href="#c-otros" data-cat="Otros" aria-selected="false">Otros (0)</a>
      </nav>
    </div>
    <div class="top-actions">
      <button id="btnBackupTop" class="pilllink">Respaldar</button>
      <label class="pilllink" style="cursor:pointer">Restaurar
        <input type="file" id="restoreFileTop" accept="application/json" style="display:none" />
      </label>
      <button id="btnCombosPanel" class="pilllink">Combos</button>
    </div>
  </div>
  <!-- Controles originales (se conservan) -->
  <div class="wrap" style="margin-top:10px">
    <div class="row">
      <input id="search" class="pill" placeholder="Buscar producto…" />
      <select id="sortSel" class="pill">
        <option value="name">A–Z</option>
        <option value="stock">Stock</option>
        <option value="sold">Vendidos</option>
        <option value="price">Precio activo</option>
      </select>
      <div class="cats-wrap">
        <h3 class="cats-title">Categorías</h3>
        <div class="cats is-hidden" id="catBar" role="tablist" aria-label="Filtrar por categoría">
          <span class="chip" data-cat="Todos" role="tab" aria-selected="false">Todos</span>
          <span class="chip" data-cat="Bebidas" role="tab" aria-selected="false">Bebidas</span>
          <span class="chip" data-cat="Snacks" role="tab" aria-selected="false">Snacks</span>
          <span class="chip" data-cat="Tabaco" role="tab" aria-selected="false">Tabaco</span>
          <span class="chip" data-cat="Otros" role="tab" aria-selected="false">Otros</span>
        </div>
      </div>
      <button id="btnBackup" class="ghost btn-mini">Respaldar</button>
      <label class="ghost btn-mini" style="cursor:pointer">Restaurar <input type="file" id="restoreFile" accept="application/json" style="display:none" /></label>
      <button id="undoBtn" class="ghost btn-mini">Deshacer</button>
    </div>
  </div>
</header>



<main class="wrap">
  <section class="card" id="comboSettings" style="display:none;margin-top:8px">
    <div class="sp">
      <strong style="font-size:18px">Configuración de combos</strong>
      <span class="muted">Afecta a todos los productos con “Combos” activados</span>
    </div>
    <div class="row" style="margin-top:8px">
      <label class="pill" style="display:flex;gap:8px;align-items:center">
        Cantidad fija
        <input id="comboFixedQty" type="number" min="1" step="1" value="3" style="width:90px;margin-left:8px" />
      </label>
      <input id="comboFixedLabel" class="pill" placeholder="Etiqueta cantidad fija (p.ej. ×3)" style="min-width:200px" />
      <label class="pill" style="display:flex;gap:8px;align-items:center">
        % media caja
        <input id="comboHalfPercent" type="number" min="0.1" max="1" step="0.05" value="0.5" style="width:110px;margin-left:8px" />
      </label>
      <input id="comboHalfLabel" class="pill" placeholder="Etiqueta media caja (p.ej. ½ caja)" style="min-width:200px" />
      <input id="comboFullLabel" class="pill" placeholder="Etiqueta caja entera" style="min-width:200px" />
      <select id="comboRounding" class="pill" title="Redondeo">
        <option value="floor">Redondear hacia abajo</option>
        <option value="round">Redondeo normal</option>
        <option value="ceil">Redondear hacia arriba</option>
      </select>
    </div>
    <p class="muted">La media caja calcula: tamaño de caja × porcentaje, con el redondeo seleccionado.</p>
  </section>

  <section class="kpi">
    <div class="card"><h3>Productos</h3><div class="val" id="kpiItems">0</div></div>
    <div class="card"><h3>Unidades en stock</h3><div class="val qty" id="kpiUnits">0</div></div>
    <div class="card"><h3>Ventas (hoy)</h3><div class="val qty" id="kpiSalesToday">0</div></div>
    <div class="card"><h3>Ingresos (hoy)</h3><div class="val" id="kpiRevenueToday">$0.00</div></div>
    <div class="card"><h3>Costo inventario</h3><div class="val" id="kpiInvCost">$0.00</div></div>
    <div class="card"><h3>Utilidad (hoy)</h3><div class="val" id="kpiProfitToday">$0.00</div></div>
  </section>

  <section class="card">
    <div class="row">
      <input id="newName" class="pill" placeholder="Nombre (p.ej., Club)" autocomplete="off" />
      <select id="newCat" class="pill" title="Categoría">
        <option value="Bebidas">Bebidas</option>
        <option value="Snacks">Snacks</option>
        <option value="Tabaco">Tabaco</option>
        <option value="Otros" selected>Otros</option>
      </select>
      <input id="newCost" class="pill" pattern="^\\d*[\\.,]?\\d*$" placeholder="Costo" type="text" inputmode="decimal" />
      <input id="newStock" class="pill" placeholder="Stock" type="number" inputmode="numeric" />
      <input id="newPriceBase" class="pill" pattern="^\\d*[\\.,]?\\d*$" placeholder="Precio base" type="text" inputmode="decimal" />
      <input id="newPrice1" class="pill" pattern="^\\d*[\\.,]?\\d*$" placeholder="Precio 2" type="text" inputmode="decimal" />
      <input id="newPrice2" class="pill" pattern="^\\d*[\\.,]?\\d*$" placeholder="Precio 3" type="text" inputmode="decimal" />
      <input id="newPrice3" class="pill" pattern="^\\d*[\\.,]?\\d*$" placeholder="Precio 4" type="text" inputmode="decimal" />
      <button class="primary" id="addBtn">Agregar</button>
    </div>
    <p class="muted">El guardado es automático al salir del campo. Usa coma o punto para los decimales. Toda la información se guarda en este dispositivo. Los combos son opcionales por producto.</p>
  </section>

  <section id="cards" class="grid"></section>

  <h3 style="margin-top:16px">Registro de ventas</h3>
  <div class="log">
    <table>
      <thead><tr><th>Hora</th><th>Producto</th><th class="right">Cant.</th><th class="right">Precio</th><th class="right">Costo</th><th class="right">Total</th><th class="right">Utilidad</th><th class="right">Acciones</th></tr></thead>
      <tbody id="salesBody"><tr><td class="empty" colspan="8">Sin ventas aún.</td></tr></tbody>
    </table>
  </div>
  <div class="row" style="margin-top:10px">
    <button class="ghost btn-mini" id="exportCsv">Exportar CSV</button>
    <button class="ghost btn-mini" id="clearToday">Eliminar ventas de hoy</button>
    <button class="ghost btn-mini" id="resetBtn">Reiniciar vendidos</button>
  </div>
</main>
<div id="toast" class="toast" role="status" aria-live="polite"></div>

<script>
/* === Utils === */
const $ = s => document.querySelector(s);
const $$ = s => document.querySelectorAll(s);
const fmtMoney = n => new Intl.NumberFormat('es-EC',{style:'currency',currency:'USD',minimumFractionDigits:2}).format(n||0);
const todayKey = () => new Date().toISOString().slice(0,10);
const num = v => { if(v==null) return null; const s = String(v).replace(/,/g,'.'); const n = parseFloat(s); return Number.isFinite(n) ? n : null; };
const clamp = (v, a, b) => Math.min(Math.max(v,a),b);
function uid(){ return Math.random().toString(36).slice(2,9); }

function isEditing(){ const el=document.activeElement; if(!el) return false; if(!(el instanceof HTMLElement)) return false; return el.matches('input,textarea,select'); }

/* manifest + sw */
(function makeManifest(){
  const manifest = {name:"Su tienda",short_name:"Tienda",start_url:".",display:"standalone",background_color:"#0f172a",theme_color:"#0f172a"};
  const blob = new Blob([JSON.stringify(manifest)],{type:'application/json'});
  const url = URL.createObjectURL(blob);
  document.getElementById('manifestLink').setAttribute('href', url);
})();
(async function sw(){
  if('serviceWorker' in navigator){
    const swCode = `const CACHE='inv-v4';self.addEventListener('install',e=>{e.waitUntil(caches.open(CACHE).then(c=>c.addAll(['./'])));self.skipWaiting()});self.addEventListener('activate',e=>{e.waitUntil(self.clients.claim())});self.addEventListener('fetch',e=>{e.respondWith(caches.match(e.request).then(r=>r||fetch(e.request)))})`;
    const blob = new Blob([swCode],{type:'text/javascript'});
    const url = URL.createObjectURL(blob);
    try{ await navigator.serviceWorker.register(url,{scope:'./'});}catch(e){}
  }
})();

/* === State === */
const store = {
  load(){
    try{
      const raw = localStorage.getItem('qr-inv-data');
      const data = raw ? JSON.parse(raw) : {};
      if(!data.products) data.products = [];
      if(!data.sales) data.sales = {};
      if(!data.settings) data.settings = {};
      if(!data.settings.combos) data.settings.combos = {fixedQty:3,fixedLabel:'×3',halfPercent:0.5,halfLabel:'½ caja',fullLabel:'Caja entera',rounding:'floor'};
      data.products.forEach(p=>{
        if(!Array.isArray(p.tiers)) p.tiers=[];
        if(typeof p.selectedPriceIndex!=='number') p.selectedPriceIndex=0;
        if(typeof p.cost!=='number') p.cost = 0;
        if(typeof p.sold!=='number') p.sold = p.sold||0;
        if(typeof p.stock!=='number') p.stock = p.stock||0;
        if(typeof p.boxSize!=='number') p.boxSize = 10;
        if(typeof p.combosEnabled!=='boolean') p.combosEnabled=false; // combos opcionales
        if(typeof p.category!=='string' || !p.category) p.category='Otros';
      });
      if(!data.sales[todayKey()]) data.sales[todayKey()] = [];
      return data;
    }catch(e){ return {products:[], sales:{[todayKey()]:[]}}; }
  },
  save(){ localStorage.setItem('qr-inv-data', JSON.stringify(state)); pulseSaved(); setToast('✓ Guardado','ok'); }
};
let state = store.load();
let lastSaleId=null;

// UI prefs persistence (selected category)
const uiKey = 'qr-inv-ui';
function loadUI(){ try{ return JSON.parse(localStorage.getItem(uiKey)||'{}'); }catch(_){ return {}; } }
function saveUI(u){ localStorage.setItem(uiKey, JSON.stringify(u)); }
let selectedCategory = loadUI().selectedCategory || 'Todos';

/* price helpers */
function allPrices(p){ return [parseFloat(p.price)||0, ...(p.tiers||[]).map(v=>parseFloat(v)||0)].filter(v=>Number.isFinite(v)); }
function activePrice(p){ const all = allPrices(p); const idx = clamp(p.selectedPriceIndex||0,0,Math.max(0,all.length-1)); return all[idx]||0; }

/* === Combo settings === */
function getComboSettings(){ return (state.settings && state.settings.combos) || {fixedQty:3,fixedLabel:'×3',halfPercent:0.5,halfLabel:'½ caja',fullLabel:'Caja entera',rounding:'floor'}; }
function applyRounding(val,mode){ if(mode==='ceil')return Math.ceil(val); if(mode==='round')return Math.round(val); return Math.floor(val); }

/* KPIs */
function renderKPIs(){
  $('#kpiItems').textContent = state.products.length;
  $('#kpiUnits').textContent = state.products.reduce((a,b)=>a+(b.stock||0),0);
  const today = state.sales[todayKey()]||[];
  $('#kpiSalesToday').textContent = today.reduce((a,b)=>a+(b.qty||0),0);
  $('#kpiRevenueToday').textContent = fmtMoney(today.reduce((a,b)=>a+(b.total||0),0));
  $('#kpiProfitToday').textContent = fmtMoney(today.reduce((a,b)=>a+(b.profit||0),0));
  const invCost = state.products.reduce((a,b)=>a+((b.stock||0)*(parseFloat(b.cost)||0)),0);
  $('#kpiInvCost').textContent = fmtMoney(invCost);
}

/* Sales */
function sell(id, qty=1){
  const p = state.products.find(x=>x.id===id); if(!p) return;
  qty = parseInt(qty)||1; if(p.stock < qty){ alert('Stock insuficiente'); return; }
  p.stock -= qty; p.sold += qty;
  const price = activePrice(p);
  const cost = parseFloat(p.cost)||0;
  const total = +(price*qty).toFixed(2);
  const profit = +((price - cost) * qty).toFixed(2);
  const sale = { id:uid(), productId:id, name:p.name, qty, price, cost, total, profit, ts:Date.now(), priceIndex:p.selectedPriceIndex||0 };
  lastSaleId = sale.id;
  if(!state.sales[todayKey()]) state.sales[todayKey()] = [];
  state.sales[todayKey()].push(sale);
  store.save(); renderKPIs(); renderSales(); renderCard(id);
}
function deleteSaleById(saleId, {silent=false}={}){
  const day = todayKey(); const list = state.sales[day] || [];
  const idx = list.findIndex(x=>x.id===saleId); if(idx===-1){ if(!silent) alert('Venta no encontrada'); return; }
  if(!silent && !confirm('¿Eliminar esta venta?')) return;
  const s = list[idx]; const p = state.products.find(x=>x.id===s.productId);
  if(p){ p.stock += (s.qty||0); p.sold -= (s.qty||0); if(p.sold<0) p.sold=0; }
  list.splice(idx,1); store.save(); renderKPIs(); renderSales(); if(p) renderCard(p.id);
}
function clearTodaySales(){
  const day = todayKey(); const list = state.sales[day] || [];
  if(!list.length){ alert('No hay ventas hoy.'); return; }
  if(!confirm('¿Eliminar TODAS las ventas de HOY?')) return;
  list.forEach(s=>{ const p=state.products.find(x=>x.id===s.productId); if(p){ p.stock += (s.qty||0); p.sold -= (s.qty||0); if(p.sold<0) p.sold=0; } });
  state.sales[day] = []; store.save(); renderKPIs(); renderSales(); renderCards();
}
function undoLastSale(){
  if(!lastSaleId){
    alert('No hay venta reciente.');
    return;
  }
  // Revertir la última venta eliminándola silenciosamente
  deleteSaleById(lastSaleId,{silent:true});
  lastSaleId = null;
  // Mensaje de confirmación más claro
  setToast('Venta revertida','ok');
}

/* Editor save on blur / change */
document.addEventListener('blur', (e)=>{
  const t = e.target; if(!(t instanceof HTMLElement)) return;
  if(!t.id) return;
  const m = t.id.match(/^(n|co|st|pr|t1|t2|t3|bx|ca)-(.+)$/); if(!m) return;
  const [, field, pid] = m; const p = state.products.find(x=>x.id===pid); if(!p) return;
  const asNum = (val) => { const n = num(val); return n==null?null:+n; };
  if(field==='n'){ p.name=(t.value||'').trim()||p.name; }
  else if(field==='co'){ const v=asNum(t.value); p.cost=v??0; }
  else if(field==='st'){ const v=parseInt(String(t.value).replace(/[^\d-]/g,''),10); p.stock=Number.isFinite(v)?v:0; }
  else if(field==='pr'){ const v=asNum(t.value); p.price=v??0; }
  else if(field==='t1'){ const v=asNum(t.value); p.tiers[0]=(v==null?undefined:v); }
  else if(field==='t2'){ const v=asNum(t.value); p.tiers[1]=(v==null?undefined:v); }
  else if(field==='t3'){ const v=asNum(t.value); p.tiers[2]=(v==null?undefined:v); }
  else if(field==='bx'){ const v=parseInt(String(t.value).replace(/[^\d-]/g,''),10); p.boxSize = Number.isFinite(v)?v:10; }
  else if(field==='ca'){ p.category = t.value || 'Otros'; }
  p.tiers=(p.tiers||[]).filter(v=>v!=null);
  store.save(); renderCard(p.id); renderKPIs(); updateCatCounts();
}, true);

/* Add / Remove products */
function addProduct(name, category, cost, stock, priceBase, p1, p2, p3){
  if(!name || num(stock)===null){ alert('Completa nombre y stock.'); return; }
  const tiers=[]; [p1,p2,p3].forEach(v=>{ const n=num(v); if(n!==null) tiers.push(n); });
  const price = num(priceBase) ?? 0;
  state.products.push({ id:uid(), name:String(name).trim(), category:category||'Otros', price, tiers, selectedPriceIndex:0, cost:num(cost)??0, stock:parseInt(stock)||0, sold:0, boxSize:10, combosEnabled:false });
  store.save(); render();
}

/* render */
function priceChips(p){ return allPrices(p).map((val,idx)=>`<span class="chip ${idx===p.selectedPriceIndex?'active':''}" data-price-index="${idx}" data-id="${p.id}">$${val.toFixed(2)}</span>`).join(' '); }
function saleRow(s){
  const t=new Date(s.ts); const hh=String(t.getHours()).padStart(2,'0'); const mm=String(t.getMinutes()).padStart(2,'0');
  const profitClass = (s.profit||0)<0 ? 'badge badge-red' : (s.profit||0)===0 ? 'badge badge-yellow':'badge badge-green';
  return `<tr>
    <td>${hh}:${mm}</td><td>${s.name}</td>
    <td class="right qty">${s.qty}</td>
    <td class="right">${fmtMoney(s.price)}</td>
    <td class="right">${fmtMoney(s.cost||0)}</td>
    <td class="right">${fmtMoney(s.total)}</td>
    <td class="right"><span class="${profitClass}">${fmtMoney(s.profit||0)}</span></td>
    <td class="right"><button class="ghost btn-mini" data-del-sale="${s.id}">Eliminar</button></td>
  </tr>`;
}
function renderSales(){
  const tbody = $('#salesBody'); tbody.innerHTML='';
  const list = state.sales[todayKey()]||[];
  if(list.length===0){ const tr=document.createElement('tr'); const td=document.createElement('td'); td.colSpan=8; td.className='empty'; td.textContent='Sin ventas aún.'; tr.appendChild(td); tbody.appendChild(tr); return; }
  for(const s of [...list].reverse()){ tbody.insertAdjacentHTML('beforeend', saleRow(s)); }
}
function catOptions(val){
  const cats=['Bebidas','Snacks','Tabaco','Otros'];
  return '<select class="pill" id="ca-'+val.id+'">'+cats.map(c=>`<option value="${c}" ${val.category===c?'selected':''}>${c}</option>`).join('')+'</select>';
}
function editorBlock(p){
  // editor con categoría y combos opcionales
  return `<div class="editor ${p.__open?'open':''}" id="ed-${p.id}">
    <div class="row">
      <input class="pill" id="n-${p.id}" value="${p.name}" />
      ${catOptions(p)}
      <input class="pill" id="pr-${p.id}" type="text" inputmode="decimal" pattern="^\\d*[\\.,]?\\d*$" value="${p.price??''}" placeholder="Precio base" />
      <input class="pill" id="t1-${p.id}" type="text" inputmode="decimal" pattern="^\\d*[\\.,]?\\d*$" value="${p.tiers[0]??''}" placeholder="Precio 2" />
    </div>
    <div class="row" style="margin-top:8px">
      <input class="pill" id="t2-${p.id}" type="text" inputmode="decimal" pattern="^\\d*[\\.,]?\\d*$" value="${p.tiers[1]??''}" placeholder="Precio 3" />
      <input class="pill" id="t3-${p.id}" type="text" inputmode="decimal" pattern="^\\d*[\\.,]?\\d*$" value="${p.tiers[2]??''}" placeholder="Precio 4" />
      <input class="pill" id="co-${p.id}" type="text" inputmode="decimal" pattern="^\\d*[\\.,]?\\d*$" value="${p.cost||0}" placeholder="Costo" />
      <input class="pill" id="st-${p.id}" type="number" step="1" value="${p.stock}" placeholder="Stock" />
      <input class="pill" id="bx-${p.id}" type="number" step="1" value="${p.boxSize||10}" placeholder="Tamaño caja" />
    </div>
    <div class="row" style="margin-top:8px;justify-content:space-between">
      <div class="row" style="gap:8px">
        <span class="muted">Combos</span>
        <div class="toggle ${p.combosEnabled?'on':''}" data-toggle-combos="${p.id}"><i></i></div>
      </div>
      <div class="row">
        <button class="ghost btn-mini" data-del="${p.id}">Eliminar</button>
        <button class="ghost btn-mini" data-close="${p.id}">Cerrar</button>
      </div>
    </div>
  </div>`;
}
function combosButtons(p){
  if(!p.combosEnabled) return '';
  const cfg = getComboSettings();
  const box = Math.max(1, parseInt(p.boxSize||10));
  const fixedQty = Math.max(1, parseInt(cfg.fixedQty||3));
  const halfQty = Math.max(1, applyRounding(box * (parseFloat(cfg.halfPercent)||0.5), cfg.rounding||'floor'));
  const lblFixed = (cfg.fixedLabel && cfg.fixedLabel.trim()) || `×${fixedQty}`;
  const lblHalf = (cfg.halfLabel && cfg.halfLabel.trim()) || '½ caja';
  const lblFull = (cfg.fullLabel && cfg.fullLabel.trim()) || 'Caja entera';
  return `<div class="row" style="margin-top:8px">
    <button class="ghost btn-mini" data-combo="${fixedQty}" data-id="${p.id}">${lblFixed}</button>
    <button class="ghost btn-mini" data-combo="${halfQty}" data-id="${p.id}">${lblHalf}</button>
    <button class="ghost btn-mini" data-combo="${box}" data-id="${p.id}">${lblFull}</button>
  </div>`;
}
function cardTemplate(p){
  const price = activePrice(p);
  const margin = price - (parseFloat(p.cost)||0);
  const badgeClass = margin < 0 ? 'badge badge-red' : margin === 0 ? 'badge badge-yellow' : 'badge badge-green';
  return `<div class="card" id="card-${p.id}">
    <div class="sp">
      <strong style="font-size:18px">${p.name}</strong>
      <div class="row">
        <span class="tag">${p.category}</span>
        <span class="tag">Precio activo: $${price.toFixed(2)}<i class="save-dot" id="sd-${p.id}"></i></span>
        <button class="ghost btn-mini" data-edit="${p.id}">✎ Editar</button>
      </div>
    </div>
    <div class="row" style="margin-top:8px">${priceChips(p)}</div>
    <div class="sp" style="margin-top:8px">
      <div class="row">
        <span class="muted">Stock:</span><span class="qty"><strong id="stock-${p.id}">${p.stock}</strong></span>
        <span class="muted">Vendidos:</span><span class="qty"><strong id="sold-${p.id}">${p.sold||0}</strong></span>
        <span class="${badgeClass}" title="Margen unitario">Margen: $${margin.toFixed(2)}</span>
      </div>
      <div class="row">
        <button style="min-width:120px" class="primary" data-sell="${p.id}">Vender 1</button>
        <input class="pill" style="width:80px" type="number" min="1" step="1" value="6" id="q-${p.id}" title="Cantidad rápida" />
        <button class="blue btn-mini" data-sellq="${p.id}">Vender ×</button>
      </div>
    </div>
    ${combosButtons(p)}
    ${editorBlock(p)}
  </div>`;
}
function renderCards(){
  const grid = $('#cards');
  const term = ($('#search').value||'').toLowerCase().trim();
  const sort = $('#sortSel').value;
  let items = [...state.products];
  // filtro por categoría
  if(selectedCategory && selectedCategory!=='Todos'){
    items = items.filter(p=> (p.category||'Otros') === selectedCategory);
  }
  if(term) items = items.filter(p=> p.name.toLowerCase().includes(term));
  const sorters = {
    name:(a,b)=>a.name.localeCompare(b.name,'es'),
    stock:(a,b)=>(b.stock||0)-(a.stock||0),
    sold:(a,b)=>(b.sold||0)-(a.sold||0),
    price:(a,b)=>activePrice(b)-activePrice(a)
  };
  items.sort(sorters[sort]||sorters.name);
  grid.innerHTML = items.map(cardTemplate).join('');
}
function renderCard(id){ const p=state.products.find(x=>x.id===id); if(!p) return; const el=document.getElementById('card-'+id); if(el) el.outerHTML=cardTemplate(p); }

/* Category bar helpers with counts */
function catNames(){ return ['Todos','Bebidas','Snacks','Tabaco','Otros']; }
function countByCategory(){
  const counts = {Bebidas:0,Snacks:0,Tabaco:0,Otros:0};
  state.products.forEach(p=>{ const c=(p.category||'Otros'); if(counts[c]!=null) counts[c]++; else counts.Otros++; });
  const total = Object.values(counts).reduce((a,b)=>a+b,0);
  return {counts,total};
}
function updateCatCounts(){
  const {counts,total} = countByCategory();
  $$('#catBar .chip').forEach(c=>{
    const cat = c.dataset.cat;
    const n = cat==='Todos' ? total : (counts[cat]||0);
    c.textContent = `${cat} (${n})`;
    c.classList.toggle('active', cat===selectedCategory);
    c.setAttribute('aria-selected', cat===selectedCategory ? 'true':'false');
  });
}

/* events */
let toastTimer=null;
function setToast(msg, type){ const t=$('#toast'); t.textContent=msg; t.classList.remove('ok','edit'); if(type) t.classList.add(type); t.classList.add('show'); clearTimeout(toastTimer); toastTimer=setTimeout(()=>t.classList.remove('show'),1200); }
function pulseSaved(){ document.querySelectorAll('.save-dot').forEach(el=>{ el.style.opacity='1'; setTimeout(()=>el.style.opacity='0',300); }); }

document.addEventListener('focusin', (e)=>{ const t=e.target; if(!(t instanceof HTMLElement)) return; if(t.matches('input,textarea,select')){ setToast('Editando…','edit'); const card=t.closest('.card'); if(card) card.classList.add('editing'); } });
document.addEventListener('focusout', (e)=>{ const t=e.target; if(!(t instanceof HTMLElement)) return; if(t.matches('input,textarea,select')){ const card=t.closest('.card'); if(card) card.classList.remove('editing'); } });

document.addEventListener('click', (e)=>{
  const t=e.target; if(!(t instanceof HTMLElement)) return;
  if(t.matches('button[data-sell]')) sell(t.dataset.sell,1);
  if(t.matches('button[data-sellq]')){ const id=t.dataset.sellq; const q=parseInt($('#q-'+id).value)||1; sell(id,q); }
  if(t.matches('button[data-del]')){ if(confirm('¿Eliminar producto? (no borra ventas históricas)')){ const id=t.dataset.del; state.products = state.products.filter(p=>p.id!==id); store.save(); render(); updateCatCounts(); } }
  if(t.matches('[data-del-sale]')) deleteSaleById(t.getAttribute('data-del-sale'));
  if(t.matches('.chip[data-price-index]')){ const id=t.getAttribute('data-id'); const idx=parseInt(t.getAttribute('data-price-index'))||0; const p=state.products.find(x=>x.id===id); p.selectedPriceIndex=idx; store.save(); renderCard(id); renderKPIs(); }
  if(t.matches('[data-edit]')){ const id=t.getAttribute('data-edit'); const p=state.products.find(x=>x.id===id); p.__open = !p.__open; renderCard(id); }
  if(t.matches('[data-close]')){ const id=t.getAttribute('data-close'); const p=state.products.find(x=>x.id===id); p.__open=false; renderCard(id); }
  if(t.matches('[data-combo]')){ const id=t.getAttribute('data-id'); const qty=parseInt(t.getAttribute('data-combo'))||1; sell(id, qty); }
  if(t.matches('[data-toggle-combos]')){ const id=t.getAttribute('data-toggle-combos'); const p=state.products.find(x=>x.id===id); p.combosEnabled = !p.combosEnabled; store.save(); renderCard(id); }
  if(t.matches('#btnBackup')) backupJSON();
  if(t.matches('#undoBtn')) undoLastSale();
  // categoría chips
  if(t.closest('#catBar') && t.dataset.cat){
    selectedCategory = t.dataset.cat;
    saveUI({...loadUI(), selectedCategory});
    renderCards();
    updateCatCounts();
  }
});

/* Search & Sort */
$('#search').addEventListener('input', renderCards);
$('#sortSel').addEventListener('change', renderCards);

/* backup/restore/export */
function backupJSON(){ const blob=new Blob([JSON.stringify(state,null,2)],{type:'application/json'}); const a=document.createElement('a'); a.href=URL.createObjectURL(blob); a.download='su_tienda_backup.json'; a.click(); URL.revokeObjectURL(a.href); }
$('#restoreFile').addEventListener('change', async (e)=>{ const f=e.target.files?.[0]; if(!f) return; try{ const text=await f.text(); const data=JSON.parse(text); localStorage.setItem('qr-inv-data', JSON.stringify(data)); state=store.load(); render(); updateCatCounts(); setToast('Datos restaurados','ok'); }catch(err){ alert('No se pudo restaurar: '+err.message); } });
function exportCSV(){
  const rows=[["fecha","hora","producto","categoria","cantidad","precio","costo","total","utilidad","precio_idx"]];
  Object.entries(state.sales).forEach(([date,list])=>{ (list||[]).forEach(s=>{ const p = state.products.find(x=>x.id===s.productId) || {}; const cat = p.category || ''; const t=new Date(s.ts); const hh=String(t.getHours()).padStart(2,'0'); const mm=String(t.getMinutes()).padStart(2,'0'); rows.push([date,`${hh}:${mm}`,s.name,cat,s.qty,s.price,s.cost,s.total,s.profit,s.priceIndex||0]); }); });
  const csv = rows.map(r=>r.join(',')).join('\n'); const blob=new Blob([csv],{type:'text/csv;charset=utf-8;'}); const a=document.createElement('a'); a.href=URL.createObjectURL(blob); a.download='ventas_autosave.csv'; a.click(); URL.revokeObjectURL(a.href);
}
$('#exportCsv').addEventListener('click', exportCSV);
$('#clearToday').addEventListener('click', clearTodaySales);
$('#resetBtn').addEventListener('click', ()=>{
  // Mensaje claro al restablecer el contador de vendidos
  if(!confirm('Restablece el conteo de vendidos a 0. ¿Continuar?')) return;
  state.products.forEach(p=>p.sold=0);
  store.save();
  render();
});

/* initial render */
function render(){ renderKPIs(); if(!isEditing()) renderCards(); renderSales(); updateCatCounts(); }
// Add product
$('#addBtn').addEventListener('click', ()=>{
  addProduct($('#newName').value,$('#newCat').value,$('#newCost').value,$('#newStock').value,$('#newPriceBase').value,$('#newPrice1').value,$('#newPrice2').value,$('#newPrice3').value);
  ['newName','newCost','newStock','newPriceBase','newPrice1','newPrice2','newPrice3'].forEach(id=>$('#'+id).value='');
  updateCatCounts();
});
// Initialize selected category UI state
(function initCatSelection(){
  // Set active state based on persisted selection
  $$('#catBar .chip').forEach(c=>{
    const isActive = c.dataset.cat === selectedCategory;
    c.classList.toggle('active', isActive);
    c.setAttribute('aria-selected', isActive ? 'true' : 'false');
  });
})();

render();

/* seed if empty */
document.addEventListener('DOMContentLoaded', ()=>{
  let data=store.load();
  if(!data.products || data.products.length===0){
    data.products=[{id:uid(),name:"Club",category:"Bebidas",price:2.50,tiers:[2.75,3.00],selectedPriceIndex:0,cost:0,stock:892,sold:8,boxSize:10,combosEnabled:true,__open:true}];
    data.sales=data.sales||{}; localStorage.setItem('qr-inv-data', JSON.stringify(data)); state=data; render();
  } else {
    updateCatCounts();
  }
});

/* === Sync categorías en el header superior === */
function countByCategoryTop(){ const c={Bebidas:0,Snacks:0,Tabaco:0,Otros:0}; state.products.forEach(p=>{const k=p.category||'Otros'; if(c[k]!=null) c[k]++; else c.Otros++;}); return {c,total:Object.values(c).reduce((a,b)=>a+b,0)};}
function updateTopMenu(){
  const {c,total} = countByCategoryTop();
  document.querySelectorAll('.menu a[data-cat]').forEach(a=>{
    const k=a.getAttribute('data-cat'); const n = k==='Todos' ? total : (c[k]||0);
    a.textContent = `${k} (${n})`;
    const active = (k===selectedCategory);
    a.classList.toggle('active', active);
    a.setAttribute('aria-selected', active? 'true':'false');
  });
}
document.addEventListener('click', (e)=>{
  const tab = e.target.closest('.menu a[data-cat]');
  if(tab){
    e.preventDefault();
    selectedCategory = tab.getAttribute('data-cat');
    saveUI({...loadUI(), selectedCategory});
    renderCards();
    updateCatCounts();
    updateTopMenu();
  }
  if(e.target && e.target.id==='btnBackupTop'){ backupJSON(); }
  if(e.target && e.target.id==='btnCombosPanel'){
    const sec = document.getElementById('comboSettings');
    const isOpen = sec.style.display !== 'none';
    sec.style.display = isOpen ? 'none' : 'block';
    if(!isOpen) sec.scrollIntoView({behavior:'smooth',block:'start'});
  }
});
document.getElementById('restoreFileTop')?.addEventListener('change', async (e)=>{
  const f=e.target.files?.[0]; if(!f) return;
  try{
    const text=await f.text();
    const data=JSON.parse(text);
    localStorage.setItem('qr-inv-data', JSON.stringify(data));
    state=store.load();
    render(); updateCatCounts(); updateTopMenu(); bindComboSettings();
    setToast('Datos restaurados','ok');
  }catch(err){ alert('No se pudo restaurar: '+err.message); }
});
const _updateCatCounts = updateCatCounts;
updateCatCounts = function(){ _updateCatCounts(); updateTopMenu(); };

/* === Panel Combos: binding y guardado === */
function bindComboSettings(){
  const cfg = getComboSettings();
  const fxQty = document.getElementById('comboFixedQty');
  const fxLab = document.getElementById('comboFixedLabel');
  const hp = document.getElementById('comboHalfPercent');
  const hpLab = document.getElementById('comboHalfLabel');
  const fullLab = document.getElementById('comboFullLabel');
  const rnd = document.getElementById('comboRounding');
  if(!fxQty) return;
  fxQty.value = cfg.fixedQty ?? 3;
  fxLab.value = cfg.fixedLabel ?? '×3';
  hp.value = cfg.halfPercent ?? 0.5;
  hpLab.value = cfg.halfLabel ?? '½ caja';
  fullLab.value = cfg.fullLabel ?? 'Caja entera';
  rnd.value = cfg.rounding ?? 'floor';
  const save = ()=>{
    state.settings = state.settings || {};
    state.settings.combos = {
      fixedQty: Math.max(1, parseInt(fxQty.value||3)),
      fixedLabel: fxLab.value||'×3',
      halfPercent: Math.min(1, Math.max(0.1, parseFloat(hp.value||0.5))),
      halfLabel: hpLab.value||'½ caja',
      fullLabel: fullLab.value||'Caja entera',
      rounding: rnd.value||'floor'
    };
    store.save(); renderCards();
  };
  [fxQty,fxLab,hp,hpLab,fullLab,rnd].forEach(el=>{ el.addEventListener('change', save); el.addEventListener('blur', save); });
}
bindComboSettings();
updateTopMenu();

</script>
</body>
</html>
