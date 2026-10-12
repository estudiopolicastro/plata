[index (1).html](https://github.com/user-attachments/files/33316585/index.1.html)
<!doctype html>
<html lang="es">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width,initial-scale=1,viewport-fit=cover">
<meta name="description" content="Plata: gastos, ingresos, cuotas, metas y un simulador de inversión. Cargá tus gastos hablando.">
<meta name="theme-color" content="#16739F">
<title>Plata</title>
<link rel="icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 32 32'%3E%3Crect width='32' height='32' rx='7' fill='%2316739F'/%3E%3Cpath d='M11 24V8h6.5a4.5 4.5 0 0 1 0 9H11' fill='none' stroke='white' stroke-width='3'/%3E%3C/svg%3E">
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link rel="stylesheet" href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:wght@600;700&family=Instrument+Sans:wght@400;500;600&family=IBM+Plex+Mono:wght@400;500&display=swap">
<style>
/* Layout: una columna de hasta 720px, barra de pestañas fija abajo, tarjetas solo donde hace falta separar */
:root{
  --bg:#F2F5F7; --surface:#FFFFFF; --surface2:#E7EDF1; --ink:#12212B; --muted:#56677A;
  --line:#D3DDE4; --accent:#16739F; --accent-ink:#FFFFFF; --pos:#1B7F52; --neg:#BE3B28; --warn:#9A6208;
  --f-display:'Bricolage Grotesque','Segoe UI',system-ui,sans-serif;
  --f-body:'Instrument Sans',system-ui,-apple-system,'Segoe UI',sans-serif;
  --f-mono:'IBM Plex Mono',ui-monospace,SFMono-Regular,Menlo,monospace;
}
@media (prefers-color-scheme: dark){
  :root:not([data-theme="light"]){
    --bg:#0D151B; --surface:#15212A; --surface2:#1E2D38; --ink:#E5EDF2; --muted:#93A5B3;
    --line:#29394A; --accent:#5DB4E5; --accent-ink:#06202F; --pos:#4CC38A; --neg:#F0846F; --warn:#E0A94B;
    color-scheme:dark;
  }
}
:root[data-theme="dark"]{
  --bg:#0D151B; --surface:#15212A; --surface2:#1E2D38; --ink:#E5EDF2; --muted:#93A5B3;
  --line:#29394A; --accent:#5DB4E5; --accent-ink:#06202F; --pos:#4CC38A; --neg:#F0846F; --warn:#E0A94B;
  color-scheme:dark;
}
*{box-sizing:border-box}
:root{color-scheme:light}
[hidden]{display:none!important}
body{margin:0}
body{background:var(--bg);color:var(--ink);font-family:var(--f-body);font-size:15px;line-height:1.45;padding-inline:16px;padding-block:0 96px}
.app{max-width:720px;margin-inline:auto;display:flex;flex-direction:column;gap:16px}
h1,h2,h3{font-family:var(--f-display);margin:0;text-wrap:balance;line-height:1.15}
h2{font-size:1.15rem}
h3{font-size:1rem}
p{margin:0}
.num{font-family:var(--f-mono);font-variant-numeric:tabular-nums}
.muted{color:var(--muted)}
.small{font-size:.85rem}
.pos{color:var(--pos)} .neg{color:var(--neg)} .warn{color:var(--warn)}

header.top{display:flex;align-items:center;justify-content:space-between;gap:12px;padding-top:16px}
.brand{font-family:var(--f-display);font-weight:700;font-size:1.6rem;letter-spacing:-.02em}
.top-right{display:flex;align-items:center;gap:10px;min-width:0}
.sync{font-size:.78rem;color:var(--muted);white-space:nowrap}
.monthbar{display:flex;align-items:center;justify-content:space-between;gap:8px;background:var(--surface);border:1px solid var(--line);border-radius:10px;padding:6px}
.monthbar .lbl{font-family:var(--f-display);font-weight:600;font-size:1.05rem;text-transform:capitalize;text-align:center;flex:1}
.demo{display:flex;flex-wrap:wrap;align-items:center;justify-content:space-between;gap:8px 12px;background:var(--surface2);border:1px dashed var(--muted);border-radius:10px;padding:10px 12px}
.demo span{flex:1 1 220px;min-width:0}

.card{background:var(--surface);border:1px solid var(--line);border-radius:12px;padding:16px;display:flex;flex-direction:column;gap:12px;min-width:0}
.card > header{display:flex;align-items:baseline;justify-content:space-between;gap:8px}
.hero{display:flex;flex-direction:column;gap:14px}
.hero .big{font-family:var(--f-mono);font-variant-numeric:tabular-nums;font-size:2.1rem;font-weight:500;letter-spacing:-.02em;line-height:1.1;overflow-wrap:anywhere}
.stats{display:grid;grid-template-columns:repeat(auto-fit,minmax(140px,1fr));gap:12px}
.stat{display:flex;flex-direction:column;gap:2px;min-width:0;padding-top:10px;border-top:1px solid var(--line)}
.stat .v{font-family:var(--f-mono);font-variant-numeric:tabular-nums;font-size:1.05rem;overflow-wrap:anywhere}
.stat .k{font-size:.8rem;color:var(--muted);text-transform:uppercase;letter-spacing:.06em}

.btn{font:inherit;font-weight:600;background:var(--accent);color:var(--accent-ink);border:0;border-radius:8px;padding:10px 14px;cursor:pointer;min-height:40px}
.btn.small{padding:6px 10px;min-height:32px;font-size:.85rem}
.btn.sec{background:transparent;color:var(--accent);border:1px solid var(--accent)}
.btn.danger{background:var(--neg);color:#fff}
.ghost{font:inherit;font-size:.85rem;background:transparent;color:var(--muted);border:0;padding:6px 8px;cursor:pointer;border-radius:6px;text-decoration:underline;text-underline-offset:3px}
.ghost:hover{color:var(--ink)}
.iconbtn{font:inherit;font-size:1.3rem;line-height:1;width:40px;height:36px;background:transparent;border:0;color:var(--ink);cursor:pointer;border-radius:8px}
.iconbtn:hover{background:var(--surface2)}
:focus-visible{outline:2px solid var(--accent);outline-offset:2px}

form{display:flex;flex-direction:column;gap:12px}
.grid{display:grid;grid-template-columns:repeat(auto-fit,minmax(150px,1fr));gap:12px}
label.f{display:flex;flex-direction:column;gap:4px;font-size:.82rem;color:var(--muted);min-width:0}
input,select{font:inherit;font-size:16px;color:var(--ink);background:var(--bg);border:1px solid var(--line);border-radius:8px;padding:9px 10px;min-height:40px;width:100%;min-width:0}
input:focus,select:focus{border-color:var(--accent)}
.seg{display:grid;grid-template-columns:1fr 1fr;background:var(--surface2);border-radius:10px;padding:3px;gap:3px}
.seg button{font:inherit;font-weight:600;background:transparent;color:var(--muted);border:0;border-radius:8px;padding:8px;cursor:pointer;min-height:38px}
.seg button[aria-pressed="true"]{background:var(--surface);color:var(--ink);box-shadow:0 0 0 1px var(--line)}

ul.list{list-style:none;margin:0;padding:0;display:flex;flex-direction:column}
ul.list > li{display:grid;grid-template-columns:1fr auto;gap:2px 12px;padding:10px 0;border-top:1px solid var(--line);align-items:center}
ul.list > li:first-child{border-top:0}
.li-main{display:flex;flex-direction:column;min-width:0}
.li-main b{font-weight:600;overflow-wrap:anywhere}
.li-amt{text-align:right;font-family:var(--f-mono);font-variant-numeric:tabular-nums;white-space:nowrap}
.li-act{grid-column:1 / -1;display:flex;justify-content:flex-end;gap:6px;align-items:center}
.day{font-size:.78rem;text-transform:uppercase;letter-spacing:.07em;color:var(--muted);padding:12px 0 4px;border-top:1px solid var(--line)}
.day:first-child{border-top:0;padding-top:0}
.pill{display:inline-block;font-size:.76rem;font-weight:600;padding:2px 8px;border-radius:99px;background:var(--surface2);color:var(--muted)}
.pill.ok{color:var(--pos)} .pill.bad{color:var(--neg)} .pill.warn{color:var(--warn)}

.bar{height:8px;background:var(--surface2);border-radius:99px;overflow:hidden}
.bar > i{display:block;height:100%;background:var(--accent);border-radius:99px}
.bar.warn > i{background:var(--warn)} .bar.bad > i{background:var(--neg)} .bar.ok > i{background:var(--pos)}
.catrow{display:flex;flex-direction:column;gap:6px}
.catrow .l{display:flex;justify-content:space-between;gap:12px;align-items:baseline}
.catrow .l span:last-child{font-family:var(--f-mono);font-variant-numeric:tabular-nums;font-size:.9rem;text-align:right}

.cols{display:grid;grid-template-columns:repeat(6,1fr);gap:8px;align-items:end;height:140px}
.col{display:flex;flex-direction:column;align-items:center;justify-content:flex-end;gap:4px;height:100%;min-width:0}
.col .b{width:100%;background:var(--accent);border-radius:4px 4px 0 0;min-height:2px}
.col .t{font-size:.7rem;font-family:var(--f-mono);color:var(--muted);white-space:nowrap}
.col .m{font-size:.74rem;color:var(--muted);text-transform:capitalize}

details{border-top:1px solid var(--line);padding-top:10px}
details > summary{cursor:pointer;font-weight:600;list-style:none;display:flex;justify-content:space-between;gap:8px}
details > summary::-webkit-details-marker{display:none}
details > summary::after{content:'+';font-family:var(--f-mono);color:var(--muted)}
details[open] > summary::after{content:'−'}
details > .in{display:flex;flex-direction:column;gap:12px;padding-top:12px}

table{width:100%;border-collapse:collapse;font-size:.9rem}
th,td{text-align:right;padding:8px 6px;border-top:1px solid var(--line);vertical-align:top}
th:first-child,td:first-child{text-align:left}
th{font-size:.76rem;color:var(--muted);font-weight:500;text-transform:uppercase;letter-spacing:.05em;border-top:0}
.tw{overflow-x:auto}

nav.nav{position:fixed;left:0;right:0;bottom:0;background:var(--surface);border-top:1px solid var(--line);padding:6px 8px calc(6px + env(safe-area-inset-bottom,0px));z-index:5}
nav.nav .in{max-width:720px;margin-inline:auto;display:grid;grid-template-columns:repeat(5,1fr);gap:4px}
nav.nav button{font:inherit;font-size:.78rem;font-weight:600;color:var(--muted);background:transparent;border:0;border-radius:8px;padding:10px 2px;cursor:pointer;min-height:44px;overflow:hidden;text-overflow:ellipsis;white-space:nowrap}
nav.nav button[aria-current="page"]{color:var(--accent);background:var(--surface2)}

.toast{position:fixed;left:16px;right:16px;bottom:calc(140px + env(safe-area-inset-bottom,0px));max-width:480px;margin-inline:auto;background:var(--ink);color:var(--bg);border-radius:10px;padding:10px 14px;display:flex;align-items:center;justify-content:space-between;gap:12px;z-index:6;box-shadow:0 4px 18px rgba(0,0,0,.25)}
.toast button{font:inherit;font-weight:600;background:transparent;border:0;color:var(--bg);text-decoration:underline;cursor:pointer;padding:4px}
.empty{padding:6px 0;color:var(--muted)}
.note{font-size:.82rem;color:var(--muted)}
.mic{position:fixed;right:16px;bottom:calc(76px + env(safe-area-inset-bottom,0px));width:56px;height:56px;border-radius:50%;border:0;background:var(--accent);color:var(--accent-ink);cursor:pointer;display:grid;place-items:center;box-shadow:0 4px 14px rgba(0,0,0,.25);z-index:7}
.mic[aria-pressed="true"]{background:var(--neg);color:#fff}
@keyframes pulse{0%,100%{box-shadow:0 0 0 0 rgba(190,59,40,.5)}50%{box-shadow:0 0 0 12px rgba(190,59,40,0)}}
@media (prefers-reduced-motion: no-preference){ .mic[aria-pressed="true"]{animation:pulse 1.2s infinite} }
@media (prefers-reduced-motion: no-preference){ .bar > i,.col .b{transition:width .3s ease,height .3s ease} }
@media (min-width:560px){ .hero .big{font-size:2.6rem} ul.list > li{grid-template-columns:1fr auto auto} .li-act{grid-column:auto} }
</style>
</head>
<body>
<div class="app">
  <header class="top">
    <div class="brand">Plata</div>
    <div class="top-right">
      <span class="sync" id="sync" role="status"></span>
      <button class="btn sec small" data-act="view" data-v="ajustes">Ajustes</button>
    </div>
  </header>
  <div id="banner"></div>
  <div class="monthbar" id="monthbar">
    <button class="iconbtn" data-act="prev" aria-label="Mes anterior">‹</button>
    <div class="lbl" id="mlabel"></div>
    <button class="iconbtn" data-act="next" aria-label="Mes siguiente">›</button>
  </div>
  <main id="view" class="app" style="gap:16px"></main>
</div>

<nav class="nav" aria-label="Secciones"><div class="in">
  <button data-act="view" data-v="resumen">Resumen</button>
  <button data-act="view" data-v="movs">Movimientos</button>
  <button data-act="view" data-v="cuotas">Cuotas</button>
  <button data-act="view" data-v="metas">Metas</button>
  <button data-act="view" data-v="inv">Inversión</button>
</div></nav>
<div id="toast" class="toast" hidden role="status"></div>
<button id="mic" class="mic" type="button" data-act="voice" aria-pressed="false" aria-label="Cargar un movimiento hablando"><svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true"><rect x="9" y="2" width="6" height="12" rx="3"/><path d="M5 11a7 7 0 0 0 14 0M12 18v4"/></svg></button>

<script>
(function(){
'use strict';

/* ---------- utilidades ---------- */
var $=function(s,el){return (el||document).querySelector(s)};
var $$=function(s,el){return Array.prototype.slice.call((el||document).querySelectorAll(s))};
var esc=function(s){return String(s==null?'':s).replace(/[&<>"']/g,function(c){return {'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]})};
var rid=function(){return Math.random().toString(36).slice(2,9)};
var pad=function(n){return String(n).padStart(2,'0')};
var clone=function(o){return JSON.parse(JSON.stringify(o))};
var use=function(n){try{return window.claude&&window.claude.use?window.claude.use(n):Promise.resolve(null)}catch(e){return Promise.resolve(null)}};

var NOW=new Date();
var TODAY_D=NOW.getDate();
var TODAY=NOW.getFullYear()+'-'+pad(NOW.getMonth()+1)+'-'+pad(TODAY_D);
var CUR=TODAY.slice(0,7);
function ymAdd(ym,n){var p=ym.split('-').map(Number);var d=new Date(p[0],p[1]-1+n,1);return d.getFullYear()+'-'+pad(d.getMonth()+1)}
function ymDiff(a,b){var x=a.split('-').map(Number),y=b.split('-').map(Number);return (x[0]-y[0])*12+(x[1]-y[1])}
function dim(ym){var p=ym.split('-').map(Number);return new Date(p[0],p[1],0).getDate()}
function monthLabel(ym){var p=ym.split('-').map(Number);return new Date(p[0],p[1]-1,1).toLocaleDateString('es-AR',{month:'long',year:'numeric'}).replace(' de ',' ')}
function monthShort(ym){var p=ym.split('-').map(Number);return new Date(p[0],p[1]-1,1).toLocaleDateString('es-AR',{month:'short'}).replace('.','')}

var nfARS=new Intl.NumberFormat('es-AR',{style:'currency',currency:'ARS',maximumFractionDigits:0});
var nfUSD=new Intl.NumberFormat('es-AR',{style:'currency',currency:'USD',maximumFractionDigits:2});
var nfCmp=new Intl.NumberFormat('es-AR',{notation:'compact',maximumFractionDigits:1});
var nfPct=new Intl.NumberFormat('es-AR',{maximumFractionDigits:1});
var fARS=function(n){return nfARS.format(Math.round(n))};
var fUSD=function(n){return nfUSD.format(n)};
var fMoney=function(n,cur){return cur==='USD'?fUSD(n):fARS(n)};
var fPct=function(n){return (n>0?'+':n<0?'−':'')+nfPct.format(Math.abs(n))+'%'};

function parseAmt(v){
  var s=String(v==null?'':v).replace(/[^\d.,-]/g,'');
  if(!s) return NaN;
  if(s.indexOf(',')>-1&&s.indexOf('.')>-1) s=s.replace(/\./g,'').replace(',','.');
  else if(s.indexOf(',')>-1) s=s.replace(',','.');
  else if(/^-?\d{1,3}(\.\d{3})+$/.test(s)) s=s.replace(/\./g,'');
  return parseFloat(s);
}

var OUT_CATS=['Comida','Transporte','Vivienda','Servicios','Salud','Ocio','Educación','Compras','Impuestos','Otros'];
var IN_CATS=['Sueldo','Freelance','Inversiones','Otros ingresos'];
var PAYS=['Efectivo','Débito','Tarjeta','Transferencia'];
var FX_LABELS=['Oficial','MEP','Blue','CCL'];

/* ---------- estado ---------- */
var S={cfg:null,months:{},ym:CUR,view:'resumen',demo:false,store:'local',db:null,uid:null,dl:true,formType:'out',confirmDel:false,undo:null,undoAdd:null};

function defaultCfg(){
  var rate=1200;
  return {fx:{rate:rate,label:'MEP',date:TODAY,set:false},infl:null,budgets:{},fijos:[],cuotas:[],metas:[],
    sim:{monto:1000000,dias:30,tna:35,fx1:Math.round(rate*1.02),infl:2.5}};
}
function normCfg(c){
  var d=defaultCfg();c=c||{};
  return {fx:Object.assign(d.fx,c.fx||{}),infl:c.infl==null?null:c.infl,budgets:c.budgets||{},fijos:c.fijos||[],cuotas:c.cuotas||[],metas:c.metas||[],sim:Object.assign(d.sim,c.sim||{})};
}

/* ---------- datos de ejemplo (solo en memoria) ---------- */
function demoCfg(){
  var c=defaultCfg();
  c.budgets={Comida:250000,Ocio:80000,Transporte:60000};
  var f1=rid(),f2=rid(),f3=rid(),f4=rid();
  c.fijos=[
    {id:f1,name:'Alquiler',amt:380000,cur:'ARS',day:5,cat:'Vivienda',from:ymAdd(CUR,-2)},
    {id:f2,name:'Internet',amt:28000,cur:'ARS',day:10,cat:'Servicios',from:ymAdd(CUR,-2)},
    {id:f3,name:'Streaming',amt:4.99,cur:'USD',day:15,cat:'Ocio',from:ymAdd(CUR,-2)},
    {id:f4,name:'Gimnasio',amt:35000,cur:'ARS',day:3,cat:'Salud',from:ymAdd(CUR,-2)}
  ];
  c.cuotas=[
    {id:rid(),name:'Notebook',amt:85000,cur:'ARS',total:12,start:ymAdd(CUR,-3),day:20,cat:'Compras'},
    {id:rid(),name:'Zapatillas',amt:32000,cur:'ARS',total:6,start:ymAdd(CUR,-1),day:12,cat:'Compras'}
  ];
  c.metas=[
    {id:rid(),name:'Viaje',target:1500,saved:400,cur:'USD',monthly:150},
    {id:rid(),name:'Fondo de emergencia',target:2000000,saved:650000,cur:'ARS',monthly:200000}
  ];
  return c;
}
function demoMonths(){
  var cfg=S.cfg,res={};
  [ymAdd(CUR,-1),CUR].forEach(function(ym){
    var cap=ym===CUR?TODAY_D:dim(ym);
    var dd=function(d){return ym+'-'+pad(Math.min(d,cap,dim(ym)))};
    var tx=[];
    var add=function(d,type,amt,cat,note,pay,link,cur){ if(d>cap) return; tx.push({id:rid(),d:dd(d),type:type,amt:amt,cur:cur||'ARS',cat:cat,note:note,pay:pay||'',link:link||''}) };
    add(1,'in',1450000,'Sueldo','Sueldo');
    if(ym!==CUR) add(18,'in',220000,'Freelance','Trabajo freelance','Transferencia');
    cfg.fijos.forEach(function(f){ add(f.day,'out',f.amt,f.cat,f.name,'',('fijo:'+f.id),f.cur) });
    cfg.cuotas.forEach(function(c){ var i=ymDiff(ym,c.start); if(i>=0&&i<c.total) add(c.day,'out',c.amt,c.cat,c.name+' cuota '+(i+1)+'/'+c.total,'',('cuota:'+c.id)) });
    add(2,'out',48500,'Comida','Supermercado','Débito');
    add(4,'out',12300,'Comida','Verdulería','Efectivo');
    add(6,'out',18900,'Comida','Delivery','Tarjeta');
    add(8,'out',9500,'Transporte','Carga SUBE','Débito');
    add(9,'out',27000,'Ocio','Cine y cena','Tarjeta');
    if(ym!==CUR){ add(14,'out',61000,'Comida','Supermercado','Débito'); add(20,'out',22000,'Transporte','Nafta','Efectivo'); add(24,'out',15000,'Salud','Farmacia','Débito'); add(26,'out',54000,'Comida','Supermercado','Débito'); add(27,'out',31000,'Ocio','Salida','Tarjeta') }
    res[ym]={tx:tx};
  });
  return res;
}

/* ---------- persistencia (solo en este dispositivo) ---------- */
var LS='plata-v1';
function loadLocal(){
  try{
    var raw=localStorage.getItem(LS);
    if(raw){var d=JSON.parse(raw);if(d&&d.cfg){S.cfg=normCfg(d.cfg);S.months=d.months||{};S.demo=false;return}}
  }catch(e){}
  S.cfg=demoCfg();S.months=demoMonths();S.demo=true;
}
function persist(){
  if(S.demo) return;
  try{localStorage.setItem(LS,JSON.stringify({v:1,cfg:S.cfg,months:S.months}));S.store='local'}
  catch(e){S.store='error';toast('No se pudo guardar en este navegador. Descargá una copia desde Ajustes.',false,7000)}
  syncText();
}
function ensureMonth(ym){
  if(S.months[ym]===undefined) S.months[ym]={tx:[]};
  return Promise.resolve();
}
function syncText(){
  var el=$('#sync');if(!el) return;
  el.textContent=S.demo?'Datos de ejemplo':(S.store==='error'?'No se pudo guardar':'Guardado en este dispositivo');
}
function saveFile(name,data,type){
  var b=new Blob([data],{type:type});var u=URL.createObjectURL(b);
  var a=document.createElement('a');a.href=u;a.download=name;document.body.appendChild(a);a.click();a.remove();
  setTimeout(function(){URL.revokeObjectURL(u)},4000);
}
function backup(){saveFile('plata-copia-'+TODAY+'.json',JSON.stringify({v:1,cfg:S.cfg,months:S.months}),'application/json');toast('Copia descargada')}
function importBackup(inp){
  var f=inp.files&&inp.files[0];if(!f) return;
  var r=new FileReader();
  r.onload=function(){
    try{
      var d=JSON.parse(r.result);
      if(!d||!d.cfg||typeof d.months!=='object') throw 0;
      S.cfg=normCfg(d.cfg);S.months=d.months;S.demo=false;persist();render();toast('Copia restaurada');
    }catch(e){toast('Ese archivo no es una copia de Plata',false,6000)}
  };
  r.readAsText(f);inp.value='';
}
function backupUi(){
  return '<p class="note">Los datos viven en este dispositivo. Si borrás los datos del navegador se pierden, así que descargá una copia de vez en cuando. También sirve para pasar tus datos a otro dispositivo.</p>'+
    '<div style="display:flex;gap:8px;flex-wrap:wrap"><button class="btn sec" data-act="backup">Descargar copia</button><label class="btn sec" style="cursor:pointer">Restaurar copia<input id="imp" type="file" accept="application/json,.json" hidden></label></div>'+
    '<p class="note">Dictado por voz: lo hace el navegador. En Chrome el audio se procesa en servidores de Google. Plata no guarda el audio, solo el movimiento que interpreta.</p>';
}

/* ---------- cálculos ---------- */
function ars(amt,cur){return cur==='USD'?amt*S.cfg.fx.rate:amt}
function monthData(ym){return S.months[ym]||{tx:[]}}
function obligations(ym){
  var out=[];var paid={};
  monthData(ym).tx.forEach(function(t){if(t.link)paid[t.link]=true});
  S.cfg.fijos.forEach(function(f){
    if(ym>=f.from) out.push({kind:'fijo',id:f.id,name:f.name,amt:f.amt,cur:f.cur,day:Math.min(f.day,dim(ym)),cat:f.cat,link:'fijo:'+f.id});
  });
  S.cfg.cuotas.forEach(function(c){
    var i=ymDiff(ym,c.start);
    if(i>=0&&i<c.total) out.push({kind:'cuota',id:c.id,name:c.name,amt:c.amt,cur:c.cur,day:Math.min(c.day,dim(ym)),cat:c.cat,link:'cuota:'+c.id,nro:i+1,total:c.total});
  });
  out.forEach(function(o){o.paid=!!paid[o.link]});
  return out.sort(function(a,b){return a.day-b.day});
}
function totals(ym){
  var ing=0,gas=0,cats={};
  monthData(ym).tx.forEach(function(t){
    var v=ars(t.amt,t.cur);
    if(t.type==='in') ing+=v; else {gas+=v;cats[t.cat]=(cats[t.cat]||0)+v}
  });
  var ob=obligations(ym);
  var pend=ob.filter(function(o){return !o.paid}).reduce(function(s,o){return s+ars(o.amt,o.cur)},0);
  return {ing:ing,gas:gas,cats:cats,pend:pend,ob:ob};
}
function dueInfo(o,ym){
  if(o.paid) return {t:'Pagado',c:'ok'};
  if(ym<CUR) return {t:'Sin registrar',c:'bad'};
  if(ym>CUR) return {t:'Día '+o.day,c:''};
  var d=o.day-TODAY_D;
  if(d<0) return {t:'Venció hace '+(-d)+(d===-1?' día':' días'),c:'bad'};
  if(d===0) return {t:'Vence hoy',c:'warn'};
  if(d===1) return {t:'Vence mañana',c:'warn'};
  return {t:'Vence en '+d+' días',c:d<=5?'warn':''};
}
function fxLine(){
  var f=S.cfg.fx;
  return 'Dólar '+esc(f.label)+' a '+fARS(f.rate)+(f.set?' · cargado el '+esc(f.date.split('-').reverse().join('/')):' · valor de ejemplo, cargalo en Ajustes');
}

/* ---------- vistas ---------- */
function catOptions(list,sel){return list.map(function(c){return '<option'+(c===sel?' selected':'')+'>'+esc(c)+'</option>'}).join('')}

function vResumen(){
  var T=totals(S.ym),bal=T.ing-T.gas,disp=bal-T.pend,rate=S.cfg.fx.rate;
  var nothing=!monthData(S.ym).tx.length&&!T.ob.length;
  var h='<section class="card hero"><div><div class="note">Balance de '+esc(monthLabel(S.ym))+'</div>'+
    '<div class="big '+(bal>=0?'pos':'neg')+'">'+(bal<0?'−':'')+fARS(Math.abs(bal))+'</div></div>'+
    '<div class="stats">'+
    '<div class="stat"><span class="k">Ingresos</span><span class="v pos">'+fARS(T.ing)+'</span></div>'+
    '<div class="stat"><span class="k">Gastos</span><span class="v">'+fARS(T.gas)+'</span></div>'+
    '<div class="stat"><span class="k">Por pagar</span><span class="v '+(T.pend>0?'warn':'')+'">'+fARS(T.pend)+'</span></div>'+
    '</div>'+
    '<div><div>Disponible estimado: <b class="num '+(disp>=0?'':'neg')+'">'+(disp<0?'−':'')+fARS(Math.abs(disp))+'</b> <span class="muted">(≈ '+(disp<0?'−':'')+fUSD(Math.abs(disp)/rate)+')</span></div>'+
    '<div class="note">Ingresos menos gastos menos los vencimientos que todavía no registraste. '+fxLine()+'.</div></div></section>';
  if(nothing && !S.demo) h+='<section class="card"><h3>Todavía no hay nada en este mes</h3><p class="muted">Cargá tu primer movimiento en la pestaña Movimientos. Los gastos fijos y las cuotas se cargan en Cuotas y aparecen acá como vencimientos.</p></section>';

  var pend=T.ob.filter(function(o){return !o.paid});
  if(pend.length){
    h+='<section class="card"><header><h2>Vencimientos pendientes</h2><button class="ghost" data-act="view" data-v="cuotas">Ver todos</button></header><ul class="list">'+
      pend.slice(0,5).map(function(o){var di=dueInfo(o,S.ym);return '<li><div class="li-main"><b>'+esc(o.name)+'</b><span class="small muted">'+(o.kind==='cuota'?'Cuota '+o.nro+'/'+o.total+' · ':'')+'día '+o.day+' · <span class="'+di.c+'">'+esc(di.t)+'</span></span></div><div class="li-amt">'+fMoney(o.amt,o.cur)+'</div></li>'}).join('')+
      '</ul>'+(pend.length>5?'<div class="note">y '+(pend.length-5)+' más en Cuotas</div>':'')+'</section>';
  }

  var keys=Object.keys(T.cats);
  Object.keys(S.cfg.budgets).forEach(function(k){if(S.cfg.budgets[k]>0&&keys.indexOf(k)<0)keys.push(k)});
  keys.sort(function(a,b){return (T.cats[b]||0)-(T.cats[a]||0)});
  if(keys.length){
    var mx=Math.max.apply(null,keys.map(function(k){return T.cats[k]||0}))||1;
    h+='<section class="card"><header><h2>Gastos por categoría</h2><span class="note">Presupuestos en Ajustes</span></header>'+keys.map(function(k){
      var sp=T.cats[k]||0,b=S.cfg.budgets[k]||0,pct=b?sp/b:null,cls='',msg='';
      if(b){ if(pct>1){cls='bad';msg='Te pasaste por '+fARS(sp-b)} else if(pct>=.8){cls='warn';msg='Cerca del límite'} }
      var w=b?Math.min(pct,1)*100:(sp/mx)*100;
      return '<div class="catrow"><div class="l"><span>'+esc(k)+'</span><span>'+fARS(sp)+(b?' de '+fARS(b):'')+'</span></div><div class="bar '+cls+'"><i style="width:'+w.toFixed(1)+'%"></i></div>'+(msg?'<div class="small '+cls+'">'+msg+'</div>':'')+'</div>';
    }).join('')+'</section>';
  }

  var prev=ymAdd(S.ym,-1),pm=monthData(prev),pg=0;
  pm.tx.forEach(function(t){ if(t.type==='out'&&(S.ym!==CUR||parseInt(t.d.slice(8),10)<=TODAY_D)) pg+=ars(t.amt,t.cur) });
  if(pg>0&&T.gas>0){
    var v=(T.gas/pg-1)*100,inf=S.cfg.infl;
    var real=inf!=null?(((1+v/100)/(1+inf/100))-1)*100:null;
    h+='<section class="card"><h2>Contra el mes anterior</h2><p>Gastaste <b class="num">'+fARS(T.gas)+'</b> '+(S.ym===CUR?'hasta hoy, contra ':'contra ')+'<span class="num">'+fARS(pg)+'</span> '+(S.ym===CUR?'en el mismo punto de '+esc(monthLabel(prev)):'en '+esc(monthLabel(prev)))+': <b class="'+(v>0?'neg':'pos')+'">'+fPct(v)+'</b>.</p>'+
      (real!=null?'<p class="muted">Con una inflación mensual de '+nfPct.format(inf)+'%, en términos reales gastaste <b class="'+(real>0?'neg':'pos')+'">'+fPct(real)+'</b>.</p>':'<p class="note">Cargá la inflación mensual en Ajustes para ver la variación real.</p>')+'</section>';
  }

  var vals=[];for(var i=0;i<6;i++){var m=ymAdd(S.ym,i),s=0;S.cfg.cuotas.forEach(function(c){var k=ymDiff(m,c.start);if(k>=0&&k<c.total)s+=ars(c.amt,c.cur)});vals.push({m:m,v:s})}
  var vm=Math.max.apply(null,vals.map(function(x){return x.v}));
  if(vm>0){
    h+='<section class="card"><header><h2>Cuotas que se vienen</h2><span class="note">Próximos 6 meses</span></header><div class="cols" role="img" aria-label="Monto de cuotas por mes">'+vals.map(function(x){
      return '<div class="col"><span class="t">'+(x.v?'$'+nfCmp.format(x.v):'—')+'</span><div class="b" style="height:'+(x.v/vm*92).toFixed(0)+'px"></div><span class="m">'+esc(monthShort(x.m))+'</span></div>';
    }).join('')+'</div><p class="note">Es lo que ya tenés comprometido antes de gastar en cualquier otra cosa.</p></section>';
  }
  return h;
}

function vMovs(){
  var isOut=S.formType==='out';
  var dmin=S.ym+'-01',dmax=S.ym+'-'+pad(dim(S.ym));
  var dval=S.ym===CUR?TODAY:dmin;
  var h='<section class="card"><form data-form="quick" autocomplete="off" style="flex-direction:row;gap:8px;align-items:flex-end"><label class="f" style="flex:1">Carga rápida<input id="q-text" name="text" placeholder="Ej: gasté 500 pesos en comida" maxlength="120"></label><button class="btn" type="submit">Sumar</button></form><div class="note">También podés tocar el micrófono y decirlo.</div></section><section class="card"><form data-form="addtx" autocomplete="off">'+
    '<div class="seg" role="group" aria-label="Tipo de movimiento"><button type="button" data-act="ftype" data-v="out" aria-pressed="'+isOut+'">Gasto</button><button type="button" data-act="ftype" data-v="in" aria-pressed="'+!isOut+'">Ingreso</button></div>'+
    '<div class="grid">'+
    '<label class="f">Monto<input id="tx-amt" name="amt" inputmode="decimal" placeholder="0" required></label>'+
    '<label class="f">Moneda<select id="tx-cur" name="cur"><option>ARS</option><option>USD</option></select></label>'+
    '<label class="f">Categoría<select id="tx-cat" name="cat">'+catOptions(isOut?OUT_CATS:IN_CATS)+'</select></label>'+
    '<label class="f">Fecha<input id="tx-date" name="date" type="date" min="'+dmin+'" max="'+dmax+'" value="'+dval+'" required></label>'+
    (isOut?'<label class="f">Medio de pago<select id="tx-pay" name="pay">'+catOptions(PAYS)+'</select></label>':'')+
    '<label class="f">Descripción<input id="tx-note" name="note" maxlength="80" placeholder="Opcional"></label>'+
    '</div><button class="btn" type="submit">Agregar '+(isOut?'gasto':'ingreso')+'</button></form></section>';

  var rows=monthData(S.ym).tx.map(function(t,i){return {t:t,i:i}}).sort(function(a,b){return b.t.d.localeCompare(a.t.d)||b.i-a.i});
  h+='<section class="card"><header><h2>Movimientos de '+esc(monthLabel(S.ym))+'</h2><button class="ghost" data-act="export" data-needs-dl hidden>Exportar CSV</button></header>';
  if(!rows.length) h+='<p class="empty">No hay movimientos en este mes.</p>';
  else{
    var last='',body='';
    rows.forEach(function(r){
      var t=r.t;
      if(t.d!==last){last=t.d;body+='<div class="day">'+esc(new Date(t.d+'T12:00:00').toLocaleDateString('es-AR',{weekday:'short',day:'numeric',month:'short'}))+'</div><ul class="list">'}
      body+='<li><div class="li-main"><b>'+esc(t.note||t.cat)+'</b><span class="small muted">'+esc(t.cat)+(t.pay?' · '+esc(t.pay):'')+(t.link?' · vencimiento':'')+'</span></div>'+
        '<div class="li-amt '+(t.type==='in'?'pos':'')+'">'+(t.type==='in'?'+':'−')+fMoney(t.amt,t.cur)+(t.cur==='USD'?'<div class="small muted">≈ '+fARS(ars(t.amt,t.cur))+'</div>':'')+'</div>'+
        '<div class="li-act"><button class="ghost" data-act="deltx" data-id="'+esc(t.id)+'" aria-label="Borrar '+esc(t.note||t.cat)+'">Borrar</button></div></li>';
      var nx=rows[rows.indexOf(r)+1];
      if(!nx||nx.t.d!==t.d) body+='</ul>';
    });
    h+=body;
  }
  return h+'</section>';
}

function vCuotas(){
  var T=totals(S.ym),ob=T.ob;
  var rest=0;
  S.cfg.cuotas.forEach(function(c){var i=ymDiff(S.ym,c.start);if(i<c.total){var left=c.total-Math.max(i,0);if(left>0)rest+=left*ars(c.amt,c.cur)}});
  var h='<section class="card"><header><h2>Vencimientos de '+esc(monthLabel(S.ym))+'</h2></header>';
  if(!ob.length) h+='<p class="empty">No hay gastos fijos ni cuotas para este mes. Agregalos abajo.</p>';
  else h+='<ul class="list">'+ob.map(function(o){
    var di=dueInfo(o,S.ym);
    return '<li><div class="li-main"><b>'+esc(o.name)+'</b><span class="small muted">'+(o.kind==='cuota'?'Cuota '+o.nro+'/'+o.total+' · faltan '+(o.total-o.nro)+' · ':'Gasto fijo · ')+'día '+o.day+'</span><span class="small pill '+di.c+'" style="align-self:flex-start;margin-top:4px">'+esc(di.t)+'</span></div>'+
      '<div class="li-amt">'+fMoney(o.amt,o.cur)+'</div>'+
      '<div class="li-act">'+(o.paid?'<button class="ghost" data-act="unpay" data-link="'+esc(o.link)+'">Deshacer</button>':'<button class="btn small" data-act="pay" data-link="'+esc(o.link)+'">Registrar pago</button>')+'</div></li>';
  }).join('')+'</ul>';
  if(S.cfg.cuotas.length) h+='<p class="note">Te quedan por pagar <b class="num">'+fARS(rest)+'</b> en cuotas, contando este mes.</p>';
  h+='</section>';

  h+='<section class="card"><h2>Gastos fijos</h2><p class="muted small">Alquiler, expensas, internet, suscripciones. Se repiten todos los meses desde el mes que estás viendo.</p>'+
    (S.cfg.fijos.length?'<ul class="list">'+S.cfg.fijos.map(function(f){return '<li><div class="li-main"><b>'+esc(f.name)+'</b><span class="small muted">'+esc(f.cat)+' · día '+f.day+'</span></div><div class="li-amt">'+fMoney(f.amt,f.cur)+'</div><div class="li-act"><button class="ghost" data-act="delfijo" data-id="'+esc(f.id)+'">Quitar</button></div></li>'}).join('')+'</ul>':'')+
    '<details><summary>Agregar gasto fijo</summary><div class="in"><form data-form="addfijo" autocomplete="off"><div class="grid">'+
    '<label class="f">Nombre<input id="fj-name" name="name" maxlength="60" required></label>'+
    '<label class="f">Monto<input id="fj-amt" name="amt" inputmode="decimal" required></label>'+
    '<label class="f">Moneda<select id="fj-cur" name="cur"><option>ARS</option><option>USD</option></select></label>'+
    '<label class="f">Día de vencimiento<input id="fj-day" name="day" type="number" min="1" max="31" value="10" required></label>'+
    '<label class="f">Categoría<select id="fj-cat" name="cat">'+catOptions(OUT_CATS)+'</select></label>'+
    '</div><button class="btn" type="submit">Agregar gasto fijo</button></form></div></details></section>';

  h+='<section class="card"><h2>Compras en cuotas</h2><p class="muted small">Cargá la cuota en la que estás este mes y la app calcula cuántas faltan y cuánto tenés comprometido.</p>'+
    (S.cfg.cuotas.length?'<ul class="list">'+S.cfg.cuotas.map(function(c){var i=ymDiff(S.ym,c.start);var st=i<0?'empieza en '+monthLabel(c.start):(i>=c.total?'terminada':'cuota '+(i+1)+'/'+c.total);return '<li><div class="li-main"><b>'+esc(c.name)+'</b><span class="small muted">'+esc(c.cat)+' · '+st+' · día '+c.day+'</span></div><div class="li-amt">'+fMoney(c.amt,c.cur)+'</div><div class="li-act"><button class="ghost" data-act="delcuota" data-id="'+esc(c.id)+'">Quitar</button></div></li>'}).join('')+'</ul>':'')+
    '<details><summary>Agregar compra en cuotas</summary><div class="in"><form data-form="addcuota" autocomplete="off"><div class="grid">'+
    '<label class="f">Qué compraste<input id="cu-name" name="name" maxlength="60" required></label>'+
    '<label class="f">Valor de cada cuota<input id="cu-amt" name="amt" inputmode="decimal" required></label>'+
    '<label class="f">Moneda<select id="cu-cur" name="cur"><option>ARS</option><option>USD</option></select></label>'+
    '<label class="f">Cantidad de cuotas<input id="cu-total" name="total" type="number" min="1" max="60" value="12" required></label>'+
    '<label class="f">Cuota de este mes<input id="cu-now" name="now" type="number" min="1" max="60" value="1" required></label>'+
    '<label class="f">Día de vencimiento<input id="cu-day" name="day" type="number" min="1" max="31" value="10" required></label>'+
    '<label class="f">Categoría<select id="cu-cat" name="cat">'+catOptions(OUT_CATS,'Compras')+'</select></label>'+
    '</div><button class="btn" type="submit">Agregar cuotas</button></form></div></details></section>';
  return h;
}

function vMetas(){
  var h='<section class="card"><h2>Metas de ahorro</h2>';
  if(!S.cfg.metas.length) h+='<p class="empty">Todavía no tenés metas. Agregá una abajo, por ejemplo un viaje o un fondo de emergencia.</p>';
  else h+=S.cfg.metas.map(function(m){
    var pct=Math.min(m.saved/m.target,1),done=m.saved>=m.target,left=Math.max(m.target-m.saved,0),eta='';
    if(done) eta='Meta cumplida.';
    else if(m.monthly>0){var n=Math.ceil(left/m.monthly);eta='Con '+fMoney(m.monthly,m.cur)+' por mes llegás en '+n+(n===1?' mes':' meses')+' ('+monthLabel(ymAdd(CUR,n))+').'}
    else eta='Cargá un aporte mensual para ver cuándo llegás.';
    return '<div class="catrow" style="border-top:1px solid var(--line);padding-top:12px"><div class="l"><b>'+esc(m.name)+'</b><span>'+fMoney(m.saved,m.cur)+' de '+fMoney(m.target,m.cur)+'</span></div>'+
      '<div class="bar '+(done?'ok':'')+'"><i style="width:'+(pct*100).toFixed(1)+'%"></i></div>'+
      '<div class="small muted">'+nfPct.format(pct*100)+'% · '+esc(eta)+'</div>'+
      '<form data-form="aportar" data-id="'+esc(m.id)+'" style="flex-direction:row;gap:8px;align-items:flex-end" autocomplete="off"><label class="f" style="flex:1">Sumar aporte ('+esc(m.cur)+')<input name="amt" inputmode="decimal" required></label><button class="btn small" type="submit">Sumar</button></form>'+
      '<div style="text-align:right"><button class="ghost" data-act="delmeta" data-id="'+esc(m.id)+'">Quitar meta</button></div></div>';
  }).join('');
  h+='<details><summary>Agregar meta</summary><div class="in"><form data-form="addmeta" autocomplete="off"><div class="grid">'+
    '<label class="f">Nombre<input id="mt-name" name="name" maxlength="60" required></label>'+
    '<label class="f">Objetivo<input id="mt-target" name="target" inputmode="decimal" required></label>'+
    '<label class="f">Moneda<select id="mt-cur" name="cur"><option>ARS</option><option>USD</option></select></label>'+
    '<label class="f">Ya ahorrado<input id="mt-saved" name="saved" inputmode="decimal" value="0"></label>'+
    '<label class="f">Aporte por mes<input id="mt-monthly" name="monthly" inputmode="decimal" placeholder="Opcional"></label>'+
    '</div><button class="btn" type="submit">Agregar meta</button></form></div></details></section>';
  return h;
}

function vInv(){
  var s=S.cfg.sim;
  return '<section class="card"><h2>Simulador: pesos, plazo fijo o dólar</h2><p class="muted small">Compará qué pasaría con una suma en tres caminos, con los números que vos cargues. Los valores iniciales son de ejemplo: reemplazalos por las tasas y cotizaciones de hoy. Es una simulación, no una recomendación de inversión.</p>'+
    '<div class="grid">'+
    '<label class="f">Monto en pesos<input id="sim-monto" type="number" min="0" step="any" inputmode="decimal" value="'+s.monto+'"></label>'+
    '<label class="f">Plazo en días<input id="sim-dias" type="number" min="1" step="1" inputmode="numeric" value="'+s.dias+'"></label>'+
    '<label class="f">TNA del plazo fijo (%)<input id="sim-tna" type="number" min="0" step="any" inputmode="decimal" value="'+s.tna+'"></label>'+
    '<label class="f">Inflación mensual esperada (%)<input id="sim-infl" type="number" min="0" step="any" inputmode="decimal" value="'+s.infl+'"></label>'+
    '<label class="f">Dólar al final del plazo<input id="sim-fx1" type="number" min="0" step="any" inputmode="decimal" value="'+s.fx1+'"></label>'+
    '</div><p class="note">Dólar de hoy para el cálculo: '+fxLine()+'.</p></section>'+
    '<section class="card" id="simout" aria-live="polite"></section>';
}
function runSim(){
  var el=$('#simout');if(!el) return;
  var s=S.cfg.sim;
  var read=function(id,k){var n=parseFloat($('#'+id).value);if(isFinite(n)&&n>=0)s[k]=n};
  read('sim-monto','monto');read('sim-dias','dias');read('sim-tna','tna');read('sim-infl','infl');read('sim-fx1','fx1');
  var fx0=S.cfg.fx.rate,m=s.monto,d=Math.max(s.dias,1);
  if(!(m>0)||!(fx0>0)||!(s.fx1>0)){el.innerHTML='<p class="empty">Completá monto, plazo y cotizaciones para ver el resultado.</p>';return}
  var inflF=Math.pow(1+s.infl/100,d/30);
  var rows=[
    {n:'Plazo fijo en pesos',v:m*(1+s.tna/100*d/365)},
    {n:'Pasar a dólares',v:m/fx0*s.fx1},
    {n:'Dejar los pesos quietos',v:m}
  ].map(function(r){r.real=r.v/inflF;r.nom=(r.v/m-1)*100;r.rr=(r.real/m-1)*100;return r});
  var mx=Math.max.apply(null,rows.map(function(r){return r.real}).concat([m]));
  var be=rows[0].v/(m/fx0);
  el.innerHTML='<h2>Resultado a '+d+(d===1?' día':' días')+'</h2>'+
    '<div class="tw"><table><thead><tr><th></th><th>Valor final</th><th>Nominal</th><th>Contra inflación</th></tr></thead><tbody>'+rows.map(function(r){
      return '<tr><td>'+esc(r.n)+'</td><td class="num">'+fARS(r.v)+'</td><td class="num">'+fPct(r.nom)+'</td><td class="num '+(r.rr>=0?'pos':'neg')+'">'+fPct(r.rr)+'<div class="small">'+(r.rr>=0?'Le gana':'Pierde')+'</div></td></tr>';
    }).join('')+'</tbody></table></div>'+
    '<div><div class="note" style="margin-bottom:6px">Poder de compra al final, medido en pesos de hoy (la línea de abajo es lo que pusiste)</div>'+
    rows.map(function(r){return '<div class="catrow" style="margin-bottom:8px"><div class="l"><span class="small">'+esc(r.n)+'</span><span>'+fARS(r.real)+'</span></div><div class="bar '+(r.real>=m?'ok':'bad')+'"><i style="width:'+(r.real/mx*100).toFixed(1)+'%"></i></div></div>'}).join('')+'</div>'+
    '<p>Para que pasar a dólares iguale al plazo fijo, el dólar tendría que llegar a <b class="num">'+fARS(be)+'</b> al final del plazo.</p>';
}

function vAjustes(){
  var c=S.cfg,f=c.fx;
  var h='<section class="card"><h2>Cotización e inflación</h2><p class="muted small">Esta app no consulta precios en internet: el dólar y la inflación los cargás vos, y todas las cuentas en dólares usan estos valores.</p>'+
    '<form data-form="settings" autocomplete="off"><div class="grid">'+
    '<label class="f">Tipo de dólar<select id="st-label" name="label">'+catOptions(FX_LABELS,f.label)+'</select></label>'+
    '<label class="f">Cotización (pesos por dólar)<input id="st-rate" name="rate" inputmode="decimal" value="'+f.rate+'" required></label>'+
    '<label class="f">Inflación mensual estimada (%)<input id="st-infl" name="infl" inputmode="decimal" value="'+(c.infl==null?'':c.infl)+'" placeholder="Opcional"></label>'+
    '</div><h3>Presupuesto mensual por categoría</h3><div class="grid">'+
    OUT_CATS.map(function(k,i){return '<label class="f">'+esc(k)+'<input id="st-b'+i+'" data-cat="'+esc(k)+'" name="b" inputmode="decimal" value="'+(c.budgets[k]||'')+'" placeholder="Sin límite"></label>'}).join('')+
    '</div><button class="btn" type="submit">Guardar ajustes</button></form></section>';
  h+='<section class="card"><h2>Tus datos</h2><p>'+({db:'Se guardan en tu cuenta de Claude y los ves desde cualquier dispositivo donde abras esta página con tu sesión.',saving:'Guardando en tu cuenta…',error:'No se pudo sincronizar con tu cuenta. Los datos quedan en este navegador.',local:'Se guardan en este dispositivo.'}[S.store]||'')+'</p>'+backupUi()+(S.confirmDel?'<p class="neg"><b>Esto borra todos tus movimientos, cuotas, metas y ajustes. No se puede deshacer.</b></p><div style="display:flex;gap:8px;flex-wrap:wrap"><button class="btn danger" data-act="wipe">Sí, borrar todo</button><button class="btn sec" data-act="wipe-cancel">Cancelar</button></div>':'<div><button class="btn sec" data-act="wipe-ask">Borrar todos mis datos</button></div>')+'</section>';
  return h;
}

/* ---------- render ---------- */
function render(){
  var v=S.view;
  $('#banner').innerHTML=S.demo?'<div class="demo"><span>Estás viendo datos de ejemplo. Se borran apenas cargues algo propio.</span><button class="btn small" data-act="leave-demo">Empezar con mis datos</button></div>':'';
  $('#monthbar').hidden=['resumen','movs','cuotas'].indexOf(v)<0;
  $('#mlabel').textContent=monthLabel(S.ym);
  $$('.nav button').forEach(function(b){b.setAttribute('aria-current',b.dataset.v===v?'page':'false')});
  var fn={resumen:vResumen,movs:vMovs,cuotas:vCuotas,metas:vMetas,inv:vInv,ajustes:vAjustes}[v];
  $('#view').innerHTML=fn();
  $$('[data-needs-dl]').forEach(function(e){e.hidden=!S.dl});
  syncText();
  if(v==='inv') runSim();
}
var toastT=null;
function toast(msg,undo,ms,act){
  var el=$('#toast');
  el.innerHTML='<span>'+esc(msg)+'</span>'+(undo?'<button data-act="'+(act||'undo')+'">Deshacer</button>':'');
  el.hidden=false;clearTimeout(toastT);
  toastT=setTimeout(function(){el.hidden=true;S.undo=null;S.undoAdd=null},ms||6000);
}

/* ---------- acciones ---------- */
function leaveDemo(){
  if(!S.demo) return;
  S.cfg=defaultCfg();S.months={};S.demo=false;
  persist('cfg');
}
function go(ym){
  S.ym=ym;
  Promise.all([ensureMonth(ym),ensureMonth(ymAdd(ym,-1))]).then(render);
}
function csvCell(v){v=String(v==null?'':v);return /[;"\n]/.test(v)?'"'+v.replace(/"/g,'""')+'"':v}
function exportCsv(){
  if(!S.dl) return;
  var rows=[['Fecha','Tipo','Categoría','Descripción','Medio','Moneda','Monto','Monto en ARS']];
  monthData(S.ym).tx.slice().sort(function(a,b){return a.d.localeCompare(b.d)}).forEach(function(t){
    rows.push([t.d,t.type==='in'?'Ingreso':'Gasto',t.cat,t.note||'',t.pay||'',t.cur,String(t.amt).replace('.',','),String(Math.round(ars(t.amt,t.cur))).replace('.',',')]);
  });
  var csv='﻿'+rows.map(function(r){return r.map(csvCell).join(';')}).join('\r\n');
  saveFile('plata-'+S.ym+'.csv',csv,'text/csv;charset=utf-8');toast('Archivo descargado');
}
function wipe(){
  var done=function(){
    try{localStorage.removeItem(LS)}catch(e){}
    S.cfg=defaultCfg();S.months={};S.demo=false;S.confirmDel=false;S.ym=CUR;
    toast('Se borraron todos tus datos');render();
  };
  if(!S.db){done();return}
  S.db.collection('data/users/'+S.uid).get().then(function(snap){
    return Promise.all(snap.docs.map(function(d){return docRef(d.id).delete()}));
  }).then(done,function(){toast('No se pudieron borrar los datos de tu cuenta. Probá de nuevo.')});
}
function removeTx(id){
  var md=S.months[S.ym];if(!md) return null;
  var i=md.tx.findIndex(function(t){return t.id===id});
  if(i<0) return null;
  return {ym:S.ym,tx:md.tx.splice(i,1)[0],i:i};
}

document.addEventListener('click',function(e){
  var b=e.target.closest('[data-act]');if(!b) return;
  var a=b.dataset.act;
  if(a==='view'){S.view=b.dataset.v;S.confirmDel=false;render();window.scrollTo(0,0)}
  else if(a==='prev') go(ymAdd(S.ym,-1));
  else if(a==='next') go(ymAdd(S.ym,1));
  else if(a==='ftype'){S.formType=b.dataset.v;render()}
  else if(a==='leave-demo'){leaveDemo();render()}
  else if(a==='deltx'){
    leaveDemo();
    var r=removeTx(b.dataset.id);
    if(r){S.undo=r;persist(r.ym);render();toast('Movimiento borrado',true)}
  }
  else if(a==='undo'){
    var u=S.undo;
    if(u){var md=S.months[u.ym]||(S.months[u.ym]={tx:[]});md.tx.splice(Math.min(u.i,md.tx.length),0,u.tx);S.undo=null;persist(u.ym);render()}
    $('#toast').hidden=true;
  }
  else if(a==='pay'){
    leaveDemo();
    var o=obligations(S.ym).filter(function(x){return x.link===b.dataset.link})[0];
    if(o){
      var d=S.ym===CUR?TODAY:S.ym+'-'+pad(o.day);
      var md2=S.months[S.ym]||(S.months[S.ym]={tx:[]});
      md2.tx.push({id:rid(),d:d,type:'out',amt:o.amt,cur:o.cur,cat:o.cat,note:o.name+(o.kind==='cuota'?' cuota '+o.nro+'/'+o.total:''),pay:'',link:o.link});
      persist(S.ym);render();toast('Pago registrado en Movimientos');
    }
  }
  else if(a==='unpay'){
    leaveDemo();
    var md3=S.months[S.ym];
    if(md3){md3.tx=md3.tx.filter(function(t){return t.link!==b.dataset.link});persist(S.ym);render()}
  }
  else if(a==='delfijo'){leaveDemo();S.cfg.fijos=S.cfg.fijos.filter(function(x){return x.id!==b.dataset.id});persist('cfg');render()}
  else if(a==='delcuota'){leaveDemo();S.cfg.cuotas=S.cfg.cuotas.filter(function(x){return x.id!==b.dataset.id});persist('cfg');render()}
  else if(a==='delmeta'){leaveDemo();S.cfg.metas=S.cfg.metas.filter(function(x){return x.id!==b.dataset.id});persist('cfg');render()}
  else if(a==='export') exportCsv();
  else if(a==='backup') backup();
  else if(a==='voice') startVoice();
  else if(a==='undoadd'){var ua=S.undoAdd;if(ua&&S.months[ua.ym]){S.months[ua.ym].tx=S.months[ua.ym].tx.filter(function(t){return t.id!==ua.id});persist(ua.ym);render()}S.undoAdd=null;$('#toast').hidden=true}
  else if(a==='wipe-ask'){S.confirmDel=true;render()}
  else if(a==='wipe-cancel'){S.confirmDel=false;render()}
  else if(a==='wipe') wipe();
});

document.addEventListener('submit',function(e){
  var f=e.target;e.preventDefault();
  var k=f.dataset.form;if(!k) return;
  var g=function(n){return f.elements[n]?f.elements[n].value:''};
  if(k==='quick'){var qt=g('text').trim();if(qt){addFromPhrase(qt);f.reset()}return}
  if(k==='addtx'){
    var amt=parseAmt(g('amt'));
    if(!(amt>0)){toast('Ingresá un monto mayor a cero');return}
    var date=g('date');
    if(!date||date.slice(0,7)!==S.ym){toast('La fecha tiene que estar dentro de '+monthLabel(S.ym));return}
    leaveDemo();
    var type=S.formType;
    var md=S.months[S.ym]||(S.months[S.ym]={tx:[]});
    md.tx.push({id:rid(),d:date,type:type,amt:amt,cur:g('cur'),cat:g('cat'),note:g('note').trim(),pay:type==='out'?g('pay'):'',link:''});
    persist(S.ym);render();toast(type==='out'?'Gasto agregado':'Ingreso agregado');
  }
  else if(k==='addfijo'){
    var a1=parseAmt(g('amt')),day=parseInt(g('day'),10);
    if(!(a1>0)||!(day>=1&&day<=31)){toast('Revisá el monto y el día');return}
    leaveDemo();
    S.cfg.fijos.push({id:rid(),name:g('name').trim(),amt:a1,cur:g('cur'),day:day,cat:g('cat'),from:S.ym});
    persist('cfg');render();toast('Gasto fijo agregado');
  }
  else if(k==='addcuota'){
    var a2=parseAmt(g('amt')),total=parseInt(g('total'),10),now=parseInt(g('now'),10),day2=parseInt(g('day'),10);
    if(!(a2>0)||!(total>=1)||!(now>=1&&now<=total)||!(day2>=1&&day2<=31)){toast('Revisá los datos: la cuota actual no puede pasar del total');return}
    leaveDemo();
    S.cfg.cuotas.push({id:rid(),name:g('name').trim(),amt:a2,cur:g('cur'),total:total,start:ymAdd(S.ym,-(now-1)),day:day2,cat:g('cat')});
    persist('cfg');render();toast('Cuotas agregadas');
  }
  else if(k==='addmeta'){
    var tg=parseAmt(g('target')),sv=parseAmt(g('saved')),mo=parseAmt(g('monthly'));
    if(!(tg>0)){toast('Ingresá un objetivo mayor a cero');return}
    leaveDemo();
    S.cfg.metas.push({id:rid(),name:g('name').trim(),target:tg,saved:isFinite(sv)&&sv>0?sv:0,cur:g('cur'),monthly:isFinite(mo)&&mo>0?mo:0});
    persist('cfg');render();toast('Meta agregada');
  }
  else if(k==='aportar'){
    var ap=parseAmt(g('amt'));
    if(!(ap>0)){toast('Ingresá un monto mayor a cero');return}
    leaveDemo();
    var m=S.cfg.metas.filter(function(x){return x.id===f.dataset.id})[0];
    if(m){m.saved+=ap;persist('cfg');render();toast('Aporte sumado')}
  }
  else if(k==='settings'){
    var rate=parseAmt(g('rate')),inf=g('infl').trim()===''?null:parseAmt(g('infl'));
    if(!(rate>0)){toast('Ingresá una cotización válida');return}
    leaveDemo();
    S.cfg.fx={rate:rate,label:g('label'),date:TODAY,set:true};
    S.cfg.infl=(inf!=null&&isFinite(inf))?inf:null;
    var bud={};
    $$('input[name="b"]',f).forEach(function(i){var v=parseAmt(i.value);if(v>0)bud[i.dataset.cat]=v});
    S.cfg.budgets=bud;
    persist('cfg');render();toast('Ajustes guardados');
  }
});

var simT=null;
document.addEventListener('input',function(e){
  if(e.target.id&&e.target.id.indexOf('sim-')===0) runSim();
});
document.addEventListener('change',function(e){
  if(e.target.id==='imp'){importBackup(e.target);return}
  if(e.target.id&&e.target.id.indexOf('sim-')===0){runSim();persist('cfg')}
});

/* ---------- carga por voz ---------- */
/* PARSER START */
var N_UN={cero:0,un:1,uno:1,una:1,dos:2,tres:3,cuatro:4,cinco:5,seis:6,siete:7,ocho:8,nueve:9,diez:10,once:11,doce:12,trece:13,catorce:14,quince:15,dieciseis:16,diecisiete:17,dieciocho:18,diecinueve:19,veinte:20,veintiun:21,veintiuno:21,veintiuna:21,veintidos:22,veintitres:23,veinticuatro:24,veinticinco:25,veintiseis:26,veintisiete:27,veintiocho:28,veintinueve:29};
var N_TE={treinta:30,cuarenta:40,cincuenta:50,sesenta:60,setenta:70,ochenta:80,noventa:90};
var N_HU={cien:100,ciento:100,doscientos:200,trescientos:300,cuatrocientos:400,quinientos:500,seiscientos:600,setecientos:700,ochocientos:800,novecientos:900};
var CAT_OUT=[
  ['Comida','comida|comer|comi|super|supermercado|almuerzo|cena|desayuno|merienda|delivery|restaurante|verduleria|carniceria|panaderia|cafe|pizza|empanadas|kiosco|helado|cerveza|birra|almacen|rotiseria'],
  ['Transporte','nafta|colectivo|sube|uber|taxi|cabify|peaje|estacionamiento|subte|tren|remis|combustible|bondi|cochera'],
  ['Vivienda','alquiler|expensas|hipoteca|plomero|electricista'],
  ['Servicios','luz|gas|agua|internet|celular|wifi|telefono|cable|edesur|edenor|epec|servicio|servicios'],
  ['Salud','farmacia|medico|doctor|remedio|remedios|obra social|prepaga|dentista|psicologo|analisis|salud|kinesiologo'],
  ['Ocio','cine|salida|boliche|netflix|spotify|juego|juegos|streaming|recital|teatro|bar|fiesta|viaje|vacaciones|disney|youtube'],
  ['Educación','facultad|utn|curso|libro|libros|fotocopias|apuntes|universidad|colegio|clase|clases'],
  ['Compras','ropa|zapatillas|regalo|compra|mercadolibre|remera|pantalon|campera|auriculares'],
  ['Impuestos','monotributo|impuesto|impuestos|afip|arba|rentas|patente|municipal|abl|multa']
];
var CAT_IN=[
  ['Sueldo','sueldo|aguinaldo|salario|quincena|haberes'],
  ['Freelance','freelance|cliente|proyecto|trabajo|changa'],
  ['Inversiones','intereses|interes|dividendos|plazo fijo|rendimiento|inversion']
];
function normTxt(t){return String(t).toLowerCase().normalize('NFD').replace(/[̀-ͯ]/g,'')}
function isoPlus(n){var d=new Date();d.setDate(d.getDate()+n);return d.getFullYear()+'-'+pad(d.getMonth()+1)+'-'+pad(d.getDate())}
function findCat(list,txt,def){
  for(var i=0;i<list.length;i++){ if(new RegExp('\\b('+list[i][1]+')\\b').test(txt)) return list[i][0] }
  return def;
}
function parsePhrase(raw){
  var clean=String(raw||'').replace(/[^\p{L}\p{N}.,\s]/gu,' ');
  var rt=clean.split(/\s+/).filter(Boolean);
  var nt=rt.map(normTxt);
  var CURW=/^(peso|pesos|mango|mangos|dolar|dolares|usd|verdes|verde)$/;
  var runs=[],k=0;
  var isStart=function(t){t=t.replace(/[.,]+$/,'');return /^\d/.test(t)||N_UN[t]!=null||N_TE[t]!=null||N_HU[t]!=null||t==='mil'||t==='millon'||t==='millones'||t==='luca'||t==='lucas'||t==='palo'||t==='palos'};
  while(k<nt.length){
    if(!isStart(nt[k])){k++;continue}
    var total=0,cur=0,j=k,hasD=false;
    while(j<nt.length){
      var u=nt[j].replace(/[.,]+$/,'');
      if(/^\d[\d.,]*$/.test(u)){var v=parseAmt(u);if(!isFinite(v))break;cur+=v;hasD=true}
      else if(/^\d[\d.,]*k$/.test(u)){var v2=parseAmt(u.slice(0,-1));if(!isFinite(v2))break;total+=v2*1000;hasD=true}
      else if(N_UN[u]!=null){cur+=N_UN[u]}
      else if(N_TE[u]!=null){cur+=N_TE[u]}
      else if(N_HU[u]!=null){cur+=N_HU[u]}
      else if(u==='mil'||u==='luca'||u==='lucas'){total+=(cur||1)*1000;cur=0}
      else if(u==='millon'||u==='millones'||u==='palo'||u==='palos'){total+=(cur||1)*1000000;cur=0}
      else if(u==='y'&&j>k&&N_UN[nt[j+1]]!=null){}
      else break;
      j++;
    }
    var nx=(nt[j]||'').replace(/[.,]+$/,'');
    runs.push({v:total+cur,s:k,e:j,pr:CURW.test(nx)?3:(hasD?2:1)});
    k=j>k?j:k+1;
  }
  runs=runs.filter(function(r){return r.v>0&&(r.pr>=2||r.v>=10)});
  if(!runs.length) return null;
  runs.sort(function(a,b){return b.pr-a.pr||b.v-a.v});
  var best=runs[0];
  var txt=nt.join(' ');
  var cur=/\b(dolar|dolares|usd|verdes)\b/.test(txt)?'USD':'ARS';
  var isOut=/\b(gaste|gastamos|gasto|compre|compramos|pague|pagamos|abone|puse|saque)\b/.test(txt);
  var isIn=!isOut&&/\b(cobre|cobramos|gane|ingreso|me pagaron|me depositaron|me entraron|me entro|recibi|vendi|me transfirieron|aguinaldo)\b/.test(txt);
  var type=isIn?'in':'out';
  var cat=type==='in'?findCat(CAT_IN,txt,'Otros ingresos'):findCat(CAT_OUT,txt,'Otros');
  var date=/\b(anteayer|antes de ayer)\b/.test(txt)?isoPlus(-2):(/\bayer\b/.test(txt)?isoPlus(-1):TODAY);
  var pay='';
  if(type==='out'){
    if(/\b(tarjeta|credito)\b/.test(txt)) pay='Tarjeta';
    else if(/\bdebito\b/.test(txt)) pay='Débito';
    else if(/\befectivo\b/.test(txt)) pay='Efectivo';
    else if(/\b(transferencia|mercado pago|mp)\b/.test(txt)) pay='Transferencia';
  }
  var note='',p=best.e;
  while(p<nt.length&&CURW.test(nt[p].replace(/[.,]+$/,''))) p++;
  while(p<nt.length&&['en','de','por','para','a','al'].indexOf(nt[p])<0) p++;
  if(p<nt.length){
    var out=[];
    for(var q=p+1;q<nt.length&&out.length<6;q++){
      if(['con','ayer','hoy','anteayer','y','pagando','pague'].indexOf(nt[q])>-1) break;
      if(out.length&&nt[q]==='en') break;
      if(!out.length&&['el','la','los','las','un','una','mi','mis','lo'].indexOf(nt[q])>-1) continue;
      out.push(rt[q].replace(/[.,]+$/,''));
    }
    note=out.join(' ');
    if(normTxt(note)===normTxt(cat)) note='';
    if(note) note=note.charAt(0).toUpperCase()+note.slice(1,60);
  }
  return {type:type,amt:best.v,cur:cur,cat:cat,note:note,pay:pay,date:date};
}
/* PARSER END */
function addFromPhrase(text){
  var p=parsePhrase(text);
  if(!p){toast('Entendí “'+text+'” pero no encontré un monto. Probá: “gasté 500 pesos en comida”.',false,8000);return}
  leaveDemo();
  var m=p.date.slice(0,7);
  ensureMonth(m).then(function(){
    var md=S.months[m]||(S.months[m]={tx:[]});
    var id=rid();
    md.tx.push({id:id,d:p.date,type:p.type,amt:p.amt,cur:p.cur,cat:p.cat,note:p.note,pay:p.pay,link:''});
    S.undoAdd={ym:m,id:id};
    persist(m);render();
    toast((p.type==='in'?'Ingreso de ':'Gasto de ')+fMoney(p.amt,p.cur)+' en '+p.cat+' agregado',true,8000,'undoadd');
  });
}
var SR=window.SpeechRecognition||window.webkitSpeechRecognition;
var rec=null,listening=false;
function startVoice(){
  if(!SR){toast('Tu navegador no permite dictado por voz. Probá con Chrome o Safari, o escribí la frase en Carga rápida.',false,8000);return}
  if(listening&&rec){rec.stop();return}
  var heard='',failed=false;
  rec=new SR();rec.lang='es-AR';rec.interimResults=true;rec.maxAlternatives=1;rec.continuous=false;
  rec.onstart=function(){listening=true;$('#mic').setAttribute('aria-pressed','true');toast('Escuchando… decí por ejemplo: “gasté 500 pesos en comida”',false,20000)};
  rec.onresult=function(e){var t='';for(var i=0;i<e.results.length;i++)t+=e.results[i][0].transcript;heard=t;toast('“'+t+'”',false,20000)};
  rec.onerror=function(e){
    failed=true;
    var m={'not-allowed':'Necesito permiso para usar el micrófono. Habilitalo en la configuración del navegador.','service-not-allowed':'Necesito permiso para usar el micrófono. Habilitalo en la configuración del navegador.','no-speech':'No te escuché. Probá de nuevo.','audio-capture':'No encuentro un micrófono.','network':'El dictado necesita conexión a internet.'}[e.error]||'No se pudo usar el micrófono.';
    toast(m,false,7000);
  };
  rec.onend=function(){listening=false;$('#mic').setAttribute('aria-pressed','false');if(heard&&!failed)addFromPhrase(heard);else if(!heard&&!failed)toast('No te escuché. Probá de nuevo.',false,5000)};
  try{rec.start()}catch(err){listening=false;toast('No se pudo iniciar el micrófono.',false,5000)}
}
function initVoice(){}

/* ---------- arranque ---------- */
loadLocal();
render();
initVoice();
})();
</script>
</body>
</html>
