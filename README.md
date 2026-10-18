<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Brendon Barber</title>
<script src="https://cdn.tailwindcss.com/3.4.17"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-auth-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/10.12.2/firebase-firestore-compat.js"></script>
<link rel="preconnect" href="https://fonts.googleapis.com"><link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Oswald:wght@500;700&family=Playfair+Display:ital,wght@1,600&display=swap" rel="stylesheet">
<style>
:root{box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px);--red:#b22234;--navy:#0a3161;--cream:#f3ead8;--ink:#1b1712;--gold:#d4a63a}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
body{background-color:#14110e;background-image:radial-gradient(circle at 20% 0,#2b2119 0,transparent 55%),repeating-linear-gradient(90deg,rgba(255,255,255,.018) 0 2px,transparent 2px 7px);color:var(--cream);font-family:"Helvetica Neue",system-ui,-apple-system,"Segoe UI",Roboto,sans-serif}
h1,h2,#tabs button,button.bg-emerald-600{font-family:Oswald,Impact,"Arial Narrow",sans-serif;text-transform:uppercase;letter-spacing:.08em}
body .bg-white{background:#f3ead8;color:var(--ink)}
body .bg-gray-50{background:#ebe0c8}
body .bg-gray-100{background:#e2d5b8}
body .border-gray-200,body .border-gray-100{border-color:#cbbd9b}
body .divide-gray-100>:not([hidden])~:not([hidden]){border-color:#d8ccae}
body .text-gray-500,body .text-gray-400{color:#7a6a52}
body .bg-gray-900{background:var(--navy);border-color:var(--navy);color:var(--cream)}
body .border-gray-900,body .focus\:border-gray-900:focus{border-color:var(--navy)}
body .bg-emerald-600{background:var(--red);color:#fff}
body .shadow-sm{box-shadow:0 2px 0 rgba(0,0,0,.4),0 8px 20px rgba(0,0,0,.35)}
body .rounded-xl{border-radius:6px}body .rounded-lg{border-radius:4px}
#tabs button{font-weight:500;letter-spacing:.1em}
#brand{color:#ffd53d;font-weight:700;letter-spacing:.06em;text-shadow:0 1px 0 #e5283b,0 3px 0 #1f63d8,0 0 14px rgba(255,213,61,.35)}
#shopName{color:#fff}
body #hdrR a,body #hdrR button{color:#d9cdb0}
.pole{height:10px;background:repeating-linear-gradient(-45deg,#e5283b 0 12px,var(--cream) 12px 24px,#1f63d8 24px 36px,var(--cream) 36px 48px)}
.mini-pole{width:14px;height:66px;border-radius:7px;border:2px solid var(--cream);background:repeating-linear-gradient(-45deg,#e5283b 0 8px,var(--cream) 8px 16px,#1f63d8 16px 24px,var(--cream) 24px 32px)}
.hero{text-align:center;padding:26px 0 4px}
.hero .est{font-family:Oswald,sans-serif;letter-spacing:.35em;font-size:.8rem;font-weight:700;color:#fff}
.hero .brand{font-family:Oswald,Impact,sans-serif;font-weight:700;font-size:clamp(2.1rem,10vw,3.5rem);line-height:1.05;letter-spacing:.06em;text-transform:uppercase;color:#ffd53d;text-shadow:0 2px 0 #e5283b,0 5px 0 #1f63d8,0 8px 18px rgba(0,0,0,.6),0 0 22px rgba(255,213,61,.35)}
.hero .sub{font-family:"Playfair Display",Georgia,serif;font-style:italic;color:#fff;font-size:1.05rem;margin-top:12px}
.hero .rule{display:flex;align-items:center;justify-content:center;gap:10px;color:#ffd53d;font-size:.8rem;margin-top:10px}
.hero .rule::before,.hero .rule::after{content:"";height:1px;width:60px;background:var(--gold)}
.ribbon{margin:18px 0 26px;background:var(--gold);color:var(--ink);text-align:center;font-family:Oswald,Impact,sans-serif;font-weight:700;text-transform:uppercase;letter-spacing:.12em;font-size:1.05rem;padding:12px 14px;border-top:3px double var(--ink);border-bottom:3px double var(--ink)}
.leader{flex:1;border-bottom:2px dotted currentColor;opacity:.35;margin:0 10px;align-self:flex-end;transform:translateY(-7px)}
.price{font-family:Oswald,sans-serif;font-size:1.15rem;font-weight:700;letter-spacing:.04em}
</style>
</head>
<body class="text-gray-900">
<div class="pole"></div>
<div class="mx-auto max-w-3xl px-4 pb-16">
  <header id="hdr" class="flex items-center justify-between py-4">
    <h1 class="text-xl font-bold">✂️ <span id="brand"></span><span id="shopName" class="ml-1 text-sm font-normal text-gray-500"></span></h1>
    <div id="hdrR" class="text-xs"></div>
  </header>
  <nav id="tabs" class="mb-5 grid grid-cols-4 gap-1 rounded-xl bg-black/50 p-1 text-sm font-medium"></nav>
  <main id="app"></main>
</div>
<div class="pole mt-8"></div>

<script>
/* =====================================================================
   npm install firebase

// Import the functions you need from the SDKs you need
import { initializeApp } from "firebase/app";
// TODO: Add SDKs for Firebase products that you want to use
// https://firebase.google.com/docs/web/setup#available-libraries


   ===================================================================== */
const FIREBASE_CONFIG={
  apiKey: "AIzaSyDvNp9zP1K986aOYaqOwNZJ10xNihhAgxo",
  authDomain: "barbearia-931aa.firebaseapp.com",
  projectId: "barbearia-931aa",
  storageBucket: "barbearia-931aa.firebasestorage.app",
  messagingSenderId: "202716950736",
  appId: "1:202716950736:web:8f82f59b51202d26452ed5"
};
const READY=!String(FIREBASE_CONFIG.apiKey).startsWith('COLE');
let auth=null,db=null;
if(READY){firebase.initializeApp(FIREBASE_CONFIG);auth=firebase.auth();db=firebase.firestore()}

/* ---------- Utilidades ---------- */
const $=s=>document.querySelector(s);
const uid=()=>Math.random().toString(36).slice(2,9);
const brl=c=>(c/100).toLocaleString('pt-BR',{style:'currency',currency:'BRL'});
const esc=s=>String(s??'').replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
const dkey=d=>`${d.getFullYear()}-${String(d.getMonth()+1).padStart(2,'0')}-${String(d.getDate()).padStart(2,'0')}`;
const hhmm=ms=>new Date(ms).toLocaleTimeString('pt-BR',{hour:'2-digit',minute:'2-digit'});
const cmb=()=>{try{return localStorage.getItem('bf_cmb')||''}catch(e){return''}};
const clone=o=>JSON.parse(JSON.stringify(o));
const defaultWeek=(o,c)=>Array.from({length:7},()=>({on:true,open:o||'09:00',close:c||'19:00'}));
const REM_DEF={
  remind1d:'Olá, {nome}! Lembrete do seu horário na {barbearia}: {servico}, {data}, às {hora}. Se precisar remarcar, é só responder aqui. ✂️',
  remind1h:'Olá, {nome}! Seu horário na {barbearia} é daqui a pouco, às {hora} ({servico}). Te esperamos! ✂️'
};

/* ---------- Estado (vem do Firestore, em tempo real) ---------- */
const DEF={brand:'Brendon Barber',name:'Barbearia do Brenin',phone:'5524998297267',open:'09:00',close:'19:00',waAuto:true,
  pros:[{id:'p1',name:'Brenin',pct:50}],
  services:[{id:'s1',name:'Corte',price:4000,dur:30},{id:'s2',name:'Corte + Barba',price:6500,dur:60},{id:'s3',name:'Barba',price:3000,dur:30}],
  addons:[{id:'a1',name:'Sobrancelha',price:1500,dur:15,active:true},{id:'a2',name:'Pigmentação',price:2000,dur:15,active:true}]};
const S={shop:{},pros:[],services:[],addons:[],week:[],appts:[],commissions:[],busy:new Set()};
let user=null,authReady=false,cfgReady=false,busyReady=false,dirty=false,saveT=null,unsubs=[];
function applyCfg(d){
  S.shop={brand:d.brand,name:d.name,phone:d.phone,open:d.open,close:d.close,waAuto:d.waAuto!==false,remind1d:d.remind1d||REM_DEF.remind1d,remind1h:d.remind1h||REM_DEF.remind1h};
  S.pros=d.pros||[];S.services=d.services||[];S.addons=d.addons||clone(DEF.addons);
  S.week=(Array.isArray(d.week)&&d.week.length===7)?d.week:defaultWeek(d.open,d.close);
}
applyCfg(DEF);
/* Última configuração conhecida (cache local): evita mostrar valores antigos enquanto o Firestore responde */
try{const c=JSON.parse(localStorage.getItem('bf_cfg'));if(c&&c.brand){applyCfg(c);cfgReady=true}}catch(e){}
const isOn=x=>x.active!==false;
const isAuth=()=>!!user;
const isAdminUrl=()=>location.hash==='#admin';
function softRender(){const a=document.activeElement;if(a&&/INPUT|SELECT|TEXTAREA/.test(a.tagName))return;render()}

function startPublic(){
  db.doc('config/shop').onSnapshot(s=>{
    const c=s.exists?s.data():DEF;
    try{localStorage.setItem('bf_cfg',JSON.stringify(c))}catch(e){}
    cfgReady=true;if(!dirty)applyCfg(c);softRender();
  },e=>{console.error(e);cfgReady=true;softRender()});
  db.collection('busy').where('t','>=',Date.now()-86400000).onSnapshot(q=>{S.busy=new Set(q.docs.map(d=>d.id));busyReady=true;softRender()},e=>{console.error(e);busyReady=true;softRender()});
  /* se o Firestore demorar demais (sem internet), mostra mesmo assim */
  setTimeout(()=>{if(!cfgReady||!busyReady){cfgReady=busyReady=true;render()}},8000);
}
function startStaff(){
  unsubs.push(db.collection('appointments').onSnapshot(q=>{S.appts=q.docs.map(d=>({id:d.id,...d.data()}));softRender()},e=>console.error(e)));
  unsubs.push(db.collection('commissions').onSnapshot(q=>{S.commissions=q.docs.map(d=>({id:d.id,...d.data()}));softRender()},e=>console.error(e)));
}
function stopStaff(){unsubs.forEach(f=>f());unsubs=[];S.appts=[];S.commissions=[]}

/* Salva os ajustes automaticamente (com pequena espera para agrupar edições) */
function touch(){dirty=true;clearTimeout(saveT);saveT=setTimeout(saveCfg,600)}
async function saveCfg(){
  saveT=null;
  const data={...S.shop,pros:S.pros,services:S.services,addons:S.addons,week:S.week};
  try{await db.doc('config/shop').set(data)}
  catch(e){alert('Não foi possível salvar os ajustes: '+e.message)}
  if(!saveT)dirty=false;
}

/* ---------- Regras de negócio ---------- */
const STEP=60,NOTICE=30,BLK=1800000;
const active=a=>!['cancelled','no_show'].includes(a.status);
const tm=t=>{const[h,m]=t.split(':').map(Number);return h*60+m};
/* cada meia hora ocupada vira um documento "busy"; criar um que já existe é negado => sem horário duplicado */
const blocks=(p,s,e)=>{const r=[];for(let t=Math.floor(s/BLK)*BLK;t<e;t+=BLK)r.push(p+'_'+t);return r};

function slotsFor(dateStr,svc,proId){
  const [y,mo,d]=dateStr.split('-').map(Number);
  const w=S.week[new Date(y,mo-1,d).getDay()];
  if(!w||!w.on)return[];
  const pros=S.pros.filter(isOn).filter(p=>proId==='any'||p.id===proId);
  const map=new Map(), earliest=Date.now()+NOTICE*60000;
  for(const p of pros){
    for(let m=tm(w.open);m+svc.dur<=tm(w.close);m+=STEP){
      const start=new Date(y,mo-1,d,Math.floor(m/60),m%60).getTime(), end=start+svc.dur*60000;
      if(start<earliest||blocks(p.id,start,end).some(k=>S.busy.has(k)))continue;
      const t=`${String(Math.floor(m/60)).padStart(2,'0')}:${String(m%60).padStart(2,'0')}`;
      if(!map.has(t))map.set(t,{time:t,start,proId:p.id});
    }
  }
  return[...map.values()].sort((a,b)=>a.time.localeCompare(b.time));
}
async function book(){
  const t=calc(b.svc,b.addons), svc=t.svc, sl=b.slot, end=sl.start+t.dur*60000;
  /* price = total (serviço + adicionais): é a base da comissão em setStatus() */
  const a={client:b.name.trim(),phone:b.phone.replace(/\D/g,''),proId:sl.proId,svcId:svc.id,start:sl.start,end,price:t.price,dur:t.dur,svcPrice:svc.price,
    addonIds:t.adds.map(x=>x.id),addonNames:t.adds.map(x=>x.name),addonPrices:t.adds.map(x=>x.price),status:'scheduled',created:Date.now()};
  const ks=blocks(sl.proId,sl.start,end), id=uid();
  try{
    await db.runTransaction(async tx=>{
      const snaps=await Promise.all(ks.map(k=>tx.get(db.doc('busy/'+k))));
      if(snaps.some(s=>s.exists))throw new Error('busy');
      ks.forEach(k=>tx.set(db.doc('busy/'+k),{proId:sl.proId,t:+k.slice(k.lastIndexOf('_')+1)}));
      tx.set(db.doc('appointments/'+id),a);
    });
    return{id,...a};
  }catch(e){console.error(e);return null}
}
async function setStatus(id,status){
  const a=S.appts.find(x=>x.id===id);if(!a)return;
  if(status==='cancelled'||status==='no_show'){
    const msg=status==='cancelled'?'Cancelar o agendamento de '+a.client+' às '+hhmm(a.start)+'?':'Marcar que '+a.client+' faltou ('+hhmm(a.start)+')?';
    if(!confirm(msg+' O horário será liberado para outros clientes.'))return;
  }
  const batch=db.batch();
  batch.update(db.doc('appointments/'+id),{status});
  if(status==='cancelled'||status==='no_show')blocks(a.proId,a.start,a.end).forEach(k=>batch.delete(db.doc('busy/'+k)));
  if(status==='completed'&&!S.commissions.some(c=>c.apptId===id)){
    const p=S.pros.find(x=>x.id===a.proId);
    batch.set(db.doc('commissions/'+uid()),{apptId:id,proId:a.proId,base:a.price,pct:p.pct,amount:Math.round(a.price*p.pct/100),paid:false,at:Date.now()});
  }
  try{await batch.commit()}catch(e){alert('Erro: '+e.message)}
}
async function payCom(id){try{await db.doc('commissions/'+id).update({paid:true})}catch(e){alert('Erro: '+e.message)}}

/* ---------- Navegação / login ---------- */
const TABS=[['dash','Agenda'],['book','Agendar'],['com','Comissões'],['cfg','Ajustes']];
let tab='dash';
function go(t){tab=t;render()}
function vLogin(){
  const i='w-full rounded-xl border border-gray-200 bg-white px-4 py-3 outline-none focus:border-gray-900';
  return`<div class="${card} mx-auto mt-6 max-w-sm space-y-3 p-6"><h2 class="text-lg font-bold">Acesso da equipe</h2>
  <input id="lu" type="email" placeholder="E-mail" autocapitalize="none" autocomplete="username" onkeydown="if(event.key==='Enter')doLogin()" class="${i}">
  <input id="lp" type="password" placeholder="Senha" autocomplete="current-password" onkeydown="if(event.key==='Enter')doLogin()" class="${i}">
  <p id="lerr" class="hidden rounded-lg bg-red-50 p-3 text-sm text-red-700"></p>
  <button onclick="doLogin()" class="w-full rounded-xl bg-gray-900 py-3 font-semibold text-white">Entrar</button>
  <a href="#" class="block text-center text-xs text-gray-400">← Voltar para a página do cliente</a></div>`;
}
async function doLogin(){
  const err=$('#lerr'),show=m=>{err.textContent=m;err.classList.remove('hidden')};
  try{await auth.signInWithEmailAndPassword($('#lu').value.trim(),$('#lp').value);tab='dash'}
  catch(e){show('E-mail ou senha incorretos.')}
}
function logout(){auth.signOut();location.hash=''}
window.addEventListener('hashchange',()=>{b=newB();render()});

function render(){
  paintHead();
  const tabs=$('#tabs'),hr=$('#hdrR');$('#hdr').style.display=isAdminUrl()?'':'none';
  if(!READY){tabs.style.display='none';hr.innerHTML='';$('#hdr').style.display='none';
    $('#app').innerHTML=`<div class="${card} mt-8 space-y-2 p-6"><h2 class="text-lg font-bold">Falta configurar o Firebase</h2><p class="text-sm">Abra este arquivo, procure por <b>FIREBASE_CONFIG</b> e cole os dados do seu projeto Firebase.</p></div>`;return}
  if(!(cfgReady&&busyReady)){tabs.style.display='none';hr.innerHTML='';$('#hdr').style.display='none';$('#app').innerHTML='<p class="py-24 text-center text-sm text-stone-400">Carregando…</p>';return}
  if(!isAdminUrl()){
    tabs.style.display='none';hr.innerHTML='';
    $('#app').innerHTML=`<div class="hero"><div class="flex items-center justify-center gap-5"><div class="mini-pole"></div><div><p class="est">★ BARBER SHOP ★</p><div class="brand">${esc(S.shop.brand)}</div></div><div class="mini-pole"></div></div><p class="sub">${esc(S.shop.name)} · Onde estilo e confiança se encontram</p><div class="rule">★ ★ ★</div></div><p class="ribbon">Agende seu horário em poucos toques</p>`+vBook()+`<p class="mt-10 text-center text-xs text-stone-500">★ ★ ★<br><a href="#admin" class="underline">Acesso da equipe</a></p>`;
    updBtn();return;
  }
  if(!authReady){tabs.style.display='none';hr.innerHTML='';$('#app').innerHTML='<p class="py-12 text-center text-sm text-stone-400">Carregando…</p>';return}
  if(!isAuth()){tabs.style.display='none';hr.innerHTML='';$('#app').innerHTML=vLogin();return}
  tabs.style.display='';
  hr.innerHTML=`<a href="#" class="mr-3 text-gray-500 underline">Ver como cliente</a><button onclick="logout()" class="text-gray-500 underline">Sair</button>`;
  tabs.innerHTML=TABS.map(([k,l])=>`<button onclick="go('${k}')" class="rounded-lg py-2 ${tab===k?'bg-white shadow-sm':'text-stone-300'}">${l}${k==='dash'&&dueReminders().length?' ●':''}</button>`).join('');
  $('#app').innerHTML={dash:vDash,book:vBook,com:vCom,cfg:vCfg}[tab]();
  updBtn();
}

const card='rounded-xl border border-gray-200 bg-white shadow-sm';
const ST={scheduled:['Agendado','bg-amber-100 text-amber-800'],completed:['Concluído','bg-emerald-100 text-emerald-800'],cancelled:['Cancelado','bg-gray-100 text-gray-500'],no_show:['Faltou','bg-red-100 text-red-800']};

/* ---------- Agenda: dia / semana / próximos ---------- */
let dv={mode:'day',date:dkey(new Date())};
const keyDate=k=>{const[y,m,d]=k.split('-').map(Number);return new Date(y,m-1,d)};
const addDays=(k,n)=>{const d=keyDate(k);d.setDate(d.getDate()+n);return dkey(d)};
const monday=k=>{const d=keyDate(k);d.setDate(d.getDate()-((d.getDay()+6)%7));return dkey(d)};
const cap=s=>s.charAt(0).toUpperCase()+s.slice(1);
const dayName=k=>cap(keyDate(k).toLocaleDateString('pt-BR',{weekday:'long',day:'numeric',month:'long'}));
const shortDay=k=>keyDate(k).toLocaleDateString('pt-BR',{day:'2-digit',month:'2-digit'});
function setMode(m){dv.mode=m;render()}
function setDay(v){if(v){dv.date=v;render()}}
function shiftDv(n){dv.date=addDays(dv.date,n*(dv.mode==='week'?7:1));render()}
function goToday(){dv.date=dkey(new Date());render()}
const apptsOn=k=>S.appts.filter(a=>dkey(new Date(a.start))===k).sort((a,b)=>a.start-b.start);
function apptRow(a){
  const p=S.pros.find(x=>x.id===a.proId),st=ST[a.status];
  return`<li class="flex flex-wrap items-center gap-3 px-4 py-3">
      <div class="w-14 shrink-0 text-center"><p class="text-lg font-bold">${hhmm(a.start)}</p><p class="text-xs text-gray-400">até ${hhmm(a.end)}</p></div>
      <div class="min-w-0 flex-1"><p class="truncate font-medium">${esc(a.client)}</p><p class="truncate text-sm text-gray-500">${esc(apptLabel(a))} · com ${esc(p?.name)} · ${brl(a.price)}</p></div>
      <span class="rounded-full px-2.5 py-1 text-xs font-medium ${st[1]}">${st[0]}</span>
      ${a.status==='scheduled'?`<div class="flex w-full gap-2 sm:w-auto">
        <button onclick="setStatus('${a.id}','completed')" class="flex-1 rounded-lg bg-green-700 px-3 py-1.5 text-xs font-semibold text-white">Concluir</button>
        <button onclick="setStatus('${a.id}','no_show')" class="rounded-lg border px-3 py-1.5 text-xs">Faltou</button>
        <button onclick="setStatus('${a.id}','cancelled')" class="rounded-lg border px-3 py-1.5 text-xs">Cancelar</button></div>`:''}
    </li>`;
}
/* ---------- Liberar / bloquear horários (o cliente deixa de ver os bloqueados) ---------- */
/* Um bloqueio manual é um documento "busy" sem agendamento por trás: some para o cliente e volta ao ser apagado. */
const apptKeySet=()=>{const s=new Set();S.appts.filter(active).forEach(a=>blocks(a.proId,a.start,a.end).forEach(k=>s.add(k)));return s};
function slotStarts(k){
  const w=S.week[keyDate(k).getDay()];if(!w||!w.on)return[];
  const r=[],d=keyDate(k);
  for(let m=tm(w.open);m+STEP<=tm(w.close);m+=STEP)r.push(new Date(d.getFullYear(),d.getMonth(),d.getDate(),Math.floor(m/60),m%60).getTime());
  return r;
}
function slotInfo(start,ak){
  const free=[];
  S.pros.filter(isOn).forEach(p=>{const ks=blocks(p.id,start,start+STEP*60000);if(!ks.some(x=>ak.has(x)))free.push({p,ks})});
  const blocked=free.length>0&&free.every(f=>f.ks.every(x=>S.busy.has(x)));
  return{state:free.length===0?'booked':blocked?'blocked':'free',free};
}
async function applySlots(starts,block){
  const ak=apptKeySet(),batch=db.batch();let n=0;
  starts.forEach(st=>slotInfo(st,ak).free.forEach(f=>f.ks.forEach(k=>{
    if(block&&!S.busy.has(k)){batch.set(db.doc('busy/'+k),{proId:f.p.id,t:+k.slice(k.lastIndexOf('_')+1)});n++}
    if(!block&&S.busy.has(k)){batch.delete(db.doc('busy/'+k));n++}
  })));
  if(!n)return;
  try{await batch.commit()}catch(e){alert('Erro: '+e.message)}
}
function toggleSlot(st){applySlots([st],slotInfo(st,apptKeySet()).state!=='blocked')}
function closeDay(k){if(confirm('Bloquear todos os horários livres deste dia? O cliente deixa de vê-los.'))applySlots(slotStarts(k),true)}
function openDay(k){applySlots(slotStarts(k),false)}
function slotPanel(k){
  const sts=slotStarts(k);
  const head=`<h2 class="border-b border-gray-100 px-4 py-3 font-semibold">Horários para o cliente · ${dayName(k)}</h2>`;
  if(!sts.length)return`<section class="${card} mt-5">${head}<p class="px-4 py-6 text-sm text-gray-500">Este dia está fechado na configuração semanal (Ajustes → Dias e horários de funcionamento).</p></section>`;
  const ak=apptKeySet();
  const chips=sts.map(st=>{const i=slotInfo(st,ak),t=hhmm(st);
    if(i.state==='booked')return`<span class="rounded-lg border border-gray-200 bg-gray-100 py-2 text-center text-sm text-gray-400">${t}<br><span class="text-[10px]">ocupado</span></span>`;
    if(i.state==='blocked')return`<button onclick="toggleSlot(${st})" class="rounded-lg border border-red-300 bg-red-50 py-2 text-center text-sm font-medium text-red-700">${t}<br><span class="text-[10px]">bloqueado</span></button>`;
    return`<button onclick="toggleSlot(${st})" class="rounded-lg border border-green-600 bg-white py-2 text-center text-sm font-medium text-green-800">${t}<br><span class="text-[10px]">disponível</span></button>`}).join('');
  return`<section class="${card} mt-5">${head}<div class="space-y-3 p-4"><p class="text-xs text-gray-500">Toque num horário para bloquear (o cliente deixa de ver) ou para liberar de novo.</p><div class="grid grid-cols-4 gap-2 sm:grid-cols-5">${chips}</div><div class="flex gap-2"><button onclick="closeDay('${k}')" class="rounded-lg border border-red-200 px-3 py-2 text-xs text-red-600">Bloquear dia todo</button><button onclick="openDay('${k}')" class="rounded-lg border px-3 py-2 text-xs">Liberar dia todo</button></div></div></section>`;
}
/* ---------- Lembretes: 1 dia antes e 1 hora antes (você toca em enviar no WhatsApp) ---------- */
function remMsg(a,t){
  const tpl=S.shop[t==='1d'?'remind1d':'remind1h']||REM_DEF[t==='1d'?'remind1d':'remind1h'];
  const d=new Date(a.start);
  const vars={nome:(a.client||'').trim().split(/\s+/)[0],servico:apptLabel(a),hora:hhmm(a.start),barbearia:S.shop.name,
    data:d.toLocaleDateString('pt-BR',{weekday:'long',day:'numeric',month:'long'})};
  return tpl.replace(/\{(nome|servico|hora|barbearia|data)\}/g,(m,k)=>vars[k]);
}
/* 1 dia: agendamentos de amanhã (ou nas próximas 24 h) feitos com mais de 24 h de antecedência. 1 hora: nos 75 min antes. */
function dueReminders(){
  const now=Date.now(),tom=dkey(new Date(now+86400000)),out=[];
  S.appts.forEach(a=>{
    if(a.status!=='scheduled')return;
    const dt=a.start-now;if(dt<=0)return;
    if(dt<=75*60000){if(!a.r1h)out.push({a,t:'1h'});return}
    const early=!a.created||(a.start-a.created)>=86400000;
    if(early&&!a.r1d&&dt>3*3600000&&(dt<=86400000||dkey(new Date(a.start))===tom))out.push({a,t:'1d'});
  });
  return out.sort((x,y)=>x.a.start-y.a.start);
}
async function sendRemind(id,t){
  const a=S.appts.find(x=>x.id===id);if(!a)return;
  const n=waNum(a.phone);if(!n)return alert('O telefone deste cliente não parece válido.');
  window.open('https://wa.me/'+n+'?text='+encodeURIComponent(remMsg(a,t)),'_blank');
  try{await db.doc('appointments/'+id).update(t==='1d'?{r1d:Date.now()}:{r1h:Date.now()})}catch(e){alert('Erro: '+e.message)}
}
function reminderPanel(){
  const due=dueReminders();if(!due.length)return'';
  return`<section class="${card} mb-5"><h2 class="border-b border-gray-100 px-4 py-3 font-semibold">Lembretes para enviar <span class="text-xs font-normal text-gray-500">(${due.length})</span></h2><ul class="divide-y divide-gray-100">${due.map(({a,t})=>`<li class="flex flex-wrap items-center gap-3 px-4 py-3"><div class="min-w-0 flex-1"><p class="truncate font-medium">${esc(a.client)}</p><p class="truncate text-sm text-gray-500">${t==='1h'?'Daqui a cerca de 1 hora':'Lembrete de 1 dia antes'} · ${dayName(dkey(new Date(a.start)))} às ${hhmm(a.start)}</p></div><button onclick="sendRemind('${a.id}','${t}')" class="rounded-lg px-3 py-2 text-xs font-semibold" style="background:#25D366;color:#0b3d1f">Enviar no WhatsApp</button></li>`).join('')}</ul></section>`;
}
/* Cliente: arquivo de calendário (.ics) com alarmes 1 dia e 1 hora antes, que o próprio celular dispara */
const icsEsc=s=>String(s).replace(/\\/g,'\\\\').replace(/[,;]/g,m=>'\\'+m).replace(/\r?\n/g,'\\n');
const icsDate=ms=>new Date(ms).toISOString().replace(/[-:]/g,'').replace(/\.\d{3}/,'');
function buildIcs(a){
  const p=S.pros.find(x=>x.id===a.proId),what=apptLabel(a)+' · '+S.shop.name,alarm=(t,txt)=>['BEGIN:VALARM','TRIGGER:'+t,'ACTION:DISPLAY','DESCRIPTION:'+icsEsc(txt),'END:VALARM'];
  return['BEGIN:VCALENDAR','VERSION:2.0','PRODID:-//Agendamento//PT-BR','BEGIN:VEVENT','UID:'+a.id+'@agendamento','DTSTAMP:'+icsDate(Date.now()),'DTSTART:'+icsDate(a.start),'DTEND:'+icsDate(a.end),
    'SUMMARY:'+icsEsc(what),'DESCRIPTION:'+icsEsc('Com '+(p?.name||'')+' · Total '+brl(a.price)),
    ...alarm('-P1D','Amanhã: '+what),...alarm('-PT1H','Daqui a 1 hora: '+what),'END:VEVENT','END:VCALENDAR'].join('\r\n');
}
/* Google Agenda: abre já preenchido, sem baixar nada (o alerta é o padrão da agenda do cliente) */
function gcalUrl(a){
  const p=S.pros.find(x=>x.id===a.proId);
  return'https://calendar.google.com/calendar/render?'+new URLSearchParams({action:'TEMPLATE',text:apptLabel(a)+' · '+S.shop.name,dates:icsDate(a.start)+'/'+icsDate(a.end),details:'Com '+(p?.name||'')+' · Total '+brl(a.price)}).toString();
}
function downloadIcs(){
  if(!b.done)return;
  b.icsDone=true;
  const a=document.createElement('a');
  a.href=URL.createObjectURL(new Blob([buildIcs(b.done)],{type:'text/calendar'}));
  a.download='agendamento.ics';a.click();
}
function vDash(){
  const todayK=dkey(new Date());
  const seg=(m,l)=>`<button onclick="setMode('${m}')" class="flex-1 rounded-lg py-2 text-sm font-medium ${dv.mode===m?'bg-gray-900 text-white':'border border-stone-600 text-stone-200'}">${l}</button>`;
  const nb='rounded-lg border border-stone-600 px-3 py-2 text-stone-200';
  const group=(k,l)=>`<section class="${card} mb-4"><h2 class="border-b border-gray-100 px-4 py-3 font-semibold">${dayName(k)}${k===todayK?' · hoje':''} <span class="text-xs font-normal text-gray-500">(${l.length})</span></h2><ul class="divide-y divide-gray-100">${l.map(apptRow).join('')}</ul></section>`;
  const empty=t=>`<section class="${card}"><p class="px-4 py-12 text-center text-sm text-gray-500">${t}</p></section>`;
  let list,nav,body;
  if(dv.mode==='day'){
    list=apptsOn(dv.date);
    nav=`<div class="mb-4 flex items-center gap-2"><button onclick="shiftDv(-1)" class="${nb}" aria-label="Dia anterior">‹</button><input type="date" value="${dv.date}" onchange="setDay(this.value)" class="${inpC} min-w-0 flex-1 text-center"><button onclick="shiftDv(1)" class="${nb}" aria-label="Próximo dia">›</button><button onclick="goToday()" class="${nb} text-xs">Hoje</button></div>`;
    body=list.length?group(dv.date,list):empty(dv.date===todayK?'Nenhum agendamento hoje. Compartilhe seu link! ✂️':'Nenhum agendamento neste dia.');
    body+=slotPanel(dv.date);
  }else if(dv.mode==='week'){
    const m0=monday(dv.date),ds=[0,1,2,3,4,5,6].map(i=>addDays(m0,i));
    list=ds.flatMap(apptsOn);
    nav=`<div class="mb-4 flex items-center gap-2"><button onclick="shiftDv(-1)" class="${nb}" aria-label="Semana anterior">‹</button><p class="flex-1 text-center text-sm text-stone-200">Semana de ${shortDay(ds[0])} a ${shortDay(ds[6])}</p><button onclick="shiftDv(1)" class="${nb}" aria-label="Próxima semana">›</button><button onclick="goToday()" class="${nb} text-xs">Hoje</button></div>`;
    body=ds.map(k=>{const l=apptsOn(k);return l.length?group(k,l):`<div class="mb-2 flex justify-between rounded-lg border border-stone-700 px-4 py-2 text-sm text-stone-400"><span>${dayName(k)}${k===todayK?' · hoje':''}</span><span>Sem agendamentos</span></div>`}).join('');
  }else{
    const t0=keyDate(todayK).getTime();
    list=S.appts.filter(a=>a.start>=t0&&active(a)).sort((a,b)=>a.start-b.start);
    nav=`<p class="mb-4 text-sm text-stone-400">Todos os agendamentos de hoje em diante, em ordem.</p>`;
    const g=new Map();list.forEach(a=>{const k=dkey(new Date(a.start));if(!g.has(k))g.set(k,[]);g.get(k).push(a)});
    body=g.size?[...g].map(([k,l])=>group(k,l)).join(''):empty('Nenhum agendamento futuro.');
  }
  const act=list.filter(active), done=list.filter(a=>a.status==='completed');
  const prev=act.reduce((s,a)=>s+a.price,0);
  const stat=(l,v,c='')=>`<div class="${card} p-4 ${c}"><p class="text-xs font-medium uppercase tracking-wide text-gray-500">${l}</p><p class="mt-1 text-2xl font-bold">${v}</p></div>`;
  return`${reminderPanel()}<div class="mb-4 flex gap-2">${seg('day','Dia')}${seg('week','Semana')}${seg('next','Próximos')}</div>${nav}
  <section class="mb-5 grid grid-cols-2 gap-3 sm:grid-cols-3">${stat('Atendimentos',act.length)}${stat('Concluídos',done.length)}${stat('Faturamento previsto',brl(prev),'col-span-2 sm:col-span-1')}</section>
  ${body}
  <p class="mt-3 text-xs text-stone-500">Ao clicar em “Concluir”, a comissão do profissional é calculada e registrada automaticamente. “Faltou” e “Cancelar” liberam o horário para outros clientes marcarem.</p>`;
}

/* ---------- Agendamento público ---------- */
const days=Array.from({length:14},(_,i)=>{const d=new Date();d.setDate(d.getDate()+i);return d});
const newB=()=>({svc:null,addons:[],pro:'any',date:dkey(new Date()),slot:null,name:'',phone:'',err:'',done:null});
let b=newB();
/* Totais: serviço principal + adicionais ativos selecionados */
function calc(svcId,addIds){
  const svc=S.services.find(s=>s.id===svcId);
  const adds=(addIds||[]).map(id=>S.addons.find(a=>a.id===id)).filter(a=>a&&isOn(a));
  return{svc,adds,price:(svc?svc.price:0)+adds.reduce((s,a)=>s+a.price,0),dur:(svc?svc.dur:0)+adds.reduce((s,a)=>s+a.dur,0)};
}
const apptLabel=a=>{if(!a)return'';const s=S.services.find(x=>x.id===a.svcId);return[s?.name,...(a.addonNames||[])].filter(Boolean).join(' + ')};
function itemRows(svcName,svcPrice,names,prices){
  const row=(n,p,x='')=>`<div class="flex justify-between gap-3"><span>${x}${esc(n)}</span><span>${brl(p)}</span></div>`;
  return row(svcName,svcPrice)+names.map((n,i)=>row(n,prices[i]??0,'+ ')).join('');
}
function toggleAddon(id){const i=b.addons.indexOf(id);if(i<0)b.addons.push(id);else b.addons.splice(i,1);b.slot=null;b.err='';render()}
function addonsBox(){
  const list=S.addons.filter(isOn);if(!b.svc||!list.length)return'';
  const t=calc(b.svc,b.addons);
  return`<div class="mt-4"><p class="mb-2 text-sm font-medium">Adicionais <span class="font-normal text-gray-500">(opcional)</span></p><div class="space-y-2">${list.map(a=>{const sel=b.addons.includes(a.id);
    return`<label class="flex cursor-pointer items-center gap-3 rounded-xl border p-3 ${sel?'border-gray-900 bg-gray-50':'border-gray-200 bg-white'}"><input type="checkbox" ${sel?'checked':''} onchange="toggleAddon('${a.id}')" class="h-5 w-5"><span class="flex-1 font-medium">${esc(a.name)}</span><span class="text-sm text-gray-500">+${a.dur} min</span><span class="price">+ ${brl(a.price)}</span></label>`}).join('')}</div>
  <p class="mt-2 text-right text-sm">Total: <b>${brl(t.price)}</b> · ${t.dur} min</p></div>`;
}
function vBook(){
  if(b.done){const a=b.done,s=S.services.find(x=>x.id===a.svcId),p=S.pros.find(x=>x.id===a.proId);
    return`<div class="${card} p-6 text-center"><p class="text-5xl">✅</p><h2 class="mt-3 text-2xl font-bold">Agendado!</h2>
    <p class="text-gray-500">Te esperamos na ${esc(S.shop.name)}.</p>
    <div class="mt-5 space-y-2 rounded-xl bg-gray-50 p-4 text-left text-sm">
    <p class="font-medium">com ${esc(p.name)}</p><p>${new Date(a.start).toLocaleString('pt-BR',{weekday:'long',day:'numeric',month:'long',hour:'2-digit',minute:'2-digit'})}</p><div class="space-y-1 border-t border-gray-200 pt-2">${itemRows(s.name,a.svcPrice??s.price,a.addonNames||[],a.addonPrices||[])}<div class="flex justify-between gap-3 border-t border-gray-200 pt-1 font-bold"><span>Total · ${a.dur||s.dur} min</span><span>${brl(a.price)}</span></div></div></div>
    ${waBtn(a,s)}<a target="_blank" rel="noopener" href="${gcalUrl(a)}" class="mt-3 block w-full rounded-md border border-gray-300 py-3 text-center text-sm font-semibold">📅 Adicionar ao Google Agenda</a><button onclick="downloadIcs()" class="mt-2 block w-full rounded-md border border-gray-300 py-3 text-center text-sm font-semibold">🔔 Calendário do celular, com alerta 1 dia e 1 hora antes</button><button onclick="b=newB();render()" class="mt-4 text-sm text-gray-500 underline">Fazer outro agendamento</button></div>`}
  const svc=S.services.find(s=>s.id===b.svc);
  const t=calc(b.svc,b.addons);
  const slots=svc?slotsFor(b.date,{dur:t.dur},b.pro):[];
  const on='border-gray-900 bg-gray-900 text-white',off='border-gray-200 bg-white hover:border-gray-400';
  const step=(n,t,body)=>`<section class="mb-7"><h2 class="mb-3 flex items-center gap-2 font-semibold"><span class="flex h-6 w-6 items-center justify-center rounded-full bg-gray-900 text-xs text-white">${n}</span>${t}</h2>${body}</section>`;
  let h=isAdminUrl()?`<p class="mb-5 rounded-lg bg-blue-50 p-3 text-xs text-blue-800">Novo agendamento: use para clientes que chegam ou ligam.</p>`:'';
  h+=step(1,'Escolha o serviço',`<div class="space-y-2">${S.services.filter(isOn).map(s=>`<button onclick="pickSvc('${s.id}')" class="flex w-full items-center justify-between rounded-xl border p-4 text-left ${b.svc===s.id?on:off}"><div><p class="font-medium">${esc(s.name)}</p><p class="text-sm ${b.svc===s.id?'text-gray-300':'text-gray-500'}">${s.dur} min</p></div><span class="leader"></span><p class="price">${brl(s.price)}</p></button>`).join('')}</div>${addonsBox()}`);
  if(svc){
    h+=step(2,'Com quem?',`<div class="flex flex-wrap gap-2">${[...(S.pros.filter(isOn).length>1?[{id:'any',name:'Sem preferência'}]:[]),...S.pros.filter(isOn)].map(p=>`<button onclick="b.pro='${p.id}';b.slot=null;render()" class="rounded-full border px-4 py-2 text-sm font-medium ${(b.pro===p.id||(b.pro==='any'&&S.pros.filter(isOn).length===1))?on:off}">${esc(p.name)}</button>`).join('')}</div>`);
    h+=step(3,'Dia e horário',`<div class="-mx-4 flex gap-2 overflow-x-auto px-4 pb-2">${days.map(d=>{const k=dkey(d);return`<button onclick="b.date='${k}';b.slot=null;render()" class="flex w-16 shrink-0 flex-col items-center rounded-xl border py-2 ${b.date===k?on:off}"><span class="text-xs uppercase">${d.toLocaleDateString('pt-BR',{weekday:'short'}).replace('.','')}</span><span class="text-lg font-bold">${d.getDate()}</span></button>`}).join('')}</div>
    <div class="mt-3">${slots.length?`<div class="grid grid-cols-4 gap-2">${slots.map(s=>`<button onclick="pickSlot('${s.time}')" class="rounded-lg border py-2 text-sm font-medium ${b.slot?.time===s.time?on:off}">${s.time}</button>`).join('')}</div>`:`<p class="rounded-lg bg-amber-50 p-3 text-sm text-amber-800">Sem horários livres neste dia. Tente outra data.</p>`}</div>`);
  }
  if(b.slot&&svc){
    const inp='w-full rounded-xl border border-gray-200 bg-white px-4 py-3 text-base outline-none focus:border-gray-900';
    h+=step(4,'Seus dados',`<div class="space-y-3">
    <input id="fName" value="${esc(b.name)}" oninput="b.name=this.value;updBtn()" placeholder="Seu nome" autocomplete="name" maxlength="80" class="${inp}">
    <input id="fPhone" value="${esc(b.phone)}" oninput="b.phone=this.value;updBtn()" placeholder="WhatsApp com DDD" inputmode="tel" autocomplete="tel" maxlength="20" class="${inp}">
    <div class="space-y-1 rounded-xl bg-gray-100 p-4 text-sm"><p class="mb-1">${b.date.split('-').reverse().slice(0,2).join('/')} às ${b.slot.time}</p>${itemRows(svc.name,svc.price,t.adds.map(x=>x.name),t.adds.map(x=>x.price))}<div class="flex justify-between gap-3 border-t border-gray-300 pt-1 font-bold"><span>Total · ${t.dur} min</span><span>${brl(t.price)}</span></div></div>
    ${b.err?`<p class="rounded-lg bg-red-50 p-3 text-sm text-red-700">${esc(b.err)}</p>`:''}
    <button id="btnOk" onclick="submitBook()" class="w-full rounded-xl bg-emerald-600 py-3.5 font-semibold text-white disabled:cursor-not-allowed disabled:opacity-40">Confirmar agendamento</button></div>`);
  }
  return h;
}
const waNum=p=>{const d=String(p||'').replace(/\D/g,'');return!d?'':(d.length<=11?'55'+d:d)};
function bookingMsg(a){
  const s=S.services.find(x=>x.id===a.svcId),p=S.pros.find(x=>x.id===a.proId);
  const q=new Date(a.start).toLocaleString('pt-BR',{weekday:'long',day:'numeric',month:'long',hour:'2-digit',minute:'2-digit'});
  const ad=(a.addonNames||[]).map((n,i)=>`${n} (${brl((a.addonPrices||[])[i]||0)})`).join(', ');
  return`✂️ *Novo agendamento* · ${S.shop.brand}\n👤 ${a.client} (${a.phone})\n💈 Serviço: ${s?.name} (${brl(a.svcPrice??s?.price??0)})\n`+(ad?`➕ Adicionais: ${ad}\n`:'')+`🧔 Profissional: ${p?.name}\n📅 ${q}\n⏱ Duração: ${a.dur||s?.dur} min\n💰 Total: ${brl(a.price)}`;
}
/* Com chave CallMeBot: envio automático. Sem chave: abre o WhatsApp com a mensagem pronta. */
function sendWa(msg){
  const n=waNum(S.shop.phone);if(!n)return null;
  if(cmb()){
    new Image().src=`https://api.callmebot.com/whatsapp.php?phone=%2B${n}&text=${encodeURIComponent(msg)}&apikey=${encodeURIComponent(cmb())}`;
    return'auto';
  }
  if(S.shop.waAuto!==false){window.open(`https://wa.me/${n}?text=${encodeURIComponent(msg)}`,'_blank');return'open'}
  return null;
}
function testWa(){
  const r=sendWa('✂️ Teste: o aviso por WhatsApp da '+S.shop.brand+' está funcionando!');
  if(r==='auto')alert('Pedido enviado. A mensagem pode levar até 1 minuto para chegar.');
  else if(!r)alert('Informe o WhatsApp da barbearia e ative a opção de abrir o WhatsApp (ou coloque a chave CallMeBot).');
}
function waBtn(a){
  if(isAdminUrl())return'';const n=waNum(S.shop.phone);if(!n)return'';
  return`<a target="_blank" href="https://wa.me/${n}?text=${encodeURIComponent(bookingMsg(a))}" onclick="if(!b.icsDone)downloadIcs()" class="mt-4 block rounded-md py-3 text-center font-semibold" style="background:#25D366;color:#0b3d1f">Confirmar no WhatsApp e salvar na minha agenda</a>`;
}
function pickSvc(id){b.svc=id;b.pro='any';b.slot=null;b.err='';render()}
function pickSlot(t){const s=slotsFor(b.date,{dur:calc(b.svc,b.addons).dur},b.pro).find(x=>x.time===t);b.slot=s;b.err='';render()}
function updBtn(){const el=$('#btnOk');if(el)el.disabled=!(b.name.trim().length>=2&&b.phone.replace(/\D/g,'').length>=10)}
async function submitBook(){
  const btn=$('#btnOk');if(btn)btn.disabled=true;
  const a=await book();
  if(a){b.done=a;sendWa(bookingMsg(a));if(!isAdminUrl()){try{downloadIcs()}catch(e){console.error(e)}}}
  else{b.err='Esse horário acabou de ser ocupado (ou a conexão falhou). Escolha outro.';b.slot=null}
  render();
}

/* ---------- Comissões ---------- */
function vCom(){
  const rows=S.pros.filter(p=>isOn(p)||S.commissions.some(c=>c.proId===p.id)).map(p=>{
    const cs=S.commissions.filter(c=>c.proId===p.id).sort((x,y)=>x.at-y.at);
    const pend=cs.filter(c=>!c.paid).reduce((s,c)=>s+c.amount,0), paid=cs.filter(c=>c.paid).reduce((s,c)=>s+c.amount,0);
    return{p,cs,pend,paid};
  });
  return`<div class="space-y-4">${rows.map(({p,cs,pend,paid})=>`<section class="${card}">
    <div class="flex items-center justify-between border-b border-gray-100 px-4 py-3"><div><h2 class="font-semibold">${esc(p.name)}</h2><p class="text-xs text-gray-500">Comissão padrão: ${p.pct}%</p></div>
    <div class="text-right text-sm"><p class="font-bold text-amber-700">${brl(pend)} <span class="font-normal text-gray-500">a pagar</span></p><p class="text-xs text-gray-500">${brl(paid)} pago</p></div></div>
    ${cs.length?`<ul class="divide-y divide-gray-100">${cs.slice().reverse().map(c=>{const a=S.appts.find(x=>x.id===c.apptId),s=S.services.find(x=>x.id===a?.svcId);
      return`<li class="flex items-center gap-3 px-4 py-2.5 text-sm"><div class="min-w-0 flex-1"><p class="truncate">${esc(apptLabel(a))} · ${esc(a?.client)}</p><p class="text-xs text-gray-500">${brl(c.base)} × ${c.pct}%</p></div><p class="font-semibold">${brl(c.amount)}</p>
      ${c.paid?'<span class="rounded-full bg-emerald-100 px-2 py-0.5 text-xs text-emerald-800">Pago</span>':`<button onclick="payCom('${c.id}')" class="rounded-lg border px-2.5 py-1 text-xs">Marcar pago</button>`}</li>`}).join('')}</ul>`
    :'<p class="px-4 py-6 text-center text-sm text-gray-400">Nenhuma comissão ainda. Conclua um atendimento na aba “Agenda”.</p>'}</section>`).join('')}</div>`;
}

/* ---------- Ajustes (salvos automaticamente no Firebase) ---------- */
const inpC='rounded-lg border border-gray-200 bg-white px-3 py-2 text-sm outline-none focus:border-gray-900';
const btnX='rounded-lg border border-red-200 px-2.5 py-2 text-xs text-red-600 hover:bg-red-50';
const clamp=v=>Math.min(100,Math.max(0,+v||0));
function paintHead(){$('#brand').textContent=S.shop.brand;$('#shopName').textContent=S.shop.name;document.title=S.shop.brand}
function setShop(f,v){
  v=v.trim();
  if(!v&&f!=='phone'){render();return}
  S.shop[f]=v;touch();paintHead();
}
function updPro(id,f,v){
  const p=S.pros.find(x=>x.id===id);if(!p)return;
  if(f==='pct')p.pct=clamp(v);
  else if(v.trim())p.name=v.trim();
  touch();render();
}
function updSvc(id,f,v){
  const s=S.services.find(x=>x.id===id);if(!s)return;
  if(f==='name'&&v.trim())s.name=v.trim();
  if(f==='price'){const n=Math.round(parseFloat(String(v).replace(',','.'))*100);if(n>=0)s.price=n}
  if(f==='dur'){const n=parseInt(v);if(n>0)s.dur=n}
  touch();render();
}
function rmPro(id){
  if(S.pros.filter(isOn).length<=1)return alert('Mantenha pelo menos um profissional.');
  if(!confirm('Remover este profissional? Os agendamentos e comissões antigos continuam no histórico.'))return;
  S.pros.find(x=>x.id===id).active=false;touch();render();
}
function rmSvc(id){
  if(S.services.filter(isOn).length<=1)return alert('Mantenha pelo menos um serviço.');
  if(!confirm('Remover este serviço? Os agendamentos antigos continuam no histórico.'))return;
  S.services.find(x=>x.id===id).active=false;touch();render();
}
function addPro(){const n=$('#npName').value.trim();if(!n)return;S.pros.push({id:uid(),name:n,pct:clamp($('#npPct').value)});touch();render()}
function addSvc(){
  const n=$('#nsName').value.trim(),pr=Math.round(parseFloat(String($('#nsPrice').value).replace(',','.'))*100),d=parseInt($('#nsDur').value);
  if(!n||!(pr>=0)||!(d>0))return alert('Preencha nome, preço e duração.');
  S.services.push({id:uid(),name:n,price:pr,dur:d});touch();render();
}

const DOW=['Domingo','Segunda','Terça','Quarta','Quinta','Sexta','Sábado'];
function setWeek(i,f,v){
  const w=S.week[i],n={...w};
  if(f==='on')n.on=!!v;else if(v)n[f]=v;
  if(n.on&&tm(n.open)>=tm(n.close)){alert('A hora de abrir precisa ser antes da hora de fechar.');render();return}
  S.week[i]=n;touch();render();
}
function updAdd(id,f,v){
  const s=S.addons.find(x=>x.id===id);if(!s)return;
  if(f==='name'&&v.trim())s.name=v.trim();
  if(f==='price'){const n=Math.round(parseFloat(String(v).replace(',','.'))*100);if(n>=0)s.price=n}
  if(f==='dur'){const n=parseInt(v);if(n>0)s.dur=n}
  touch();render();
}
function rmAdd(id){
  if(!confirm('Remover este adicional? Os agendamentos antigos continuam no histórico.'))return;
  S.addons.find(x=>x.id===id).active=false;touch();render();
}
function addAdd(){
  const n=$('#naName').value.trim(),pr=Math.round(parseFloat(String($('#naPrice').value).replace(',','.'))*100),d=parseInt($('#naDur').value);
  if(!n||!(pr>=0)||!(d>0))return alert('Preencha nome, preço e duração.');
  S.addons.push({id:uid(),name:n,price:pr,dur:d,active:true});touch();render();
}

function vCfg(){
  const sec=(t,body)=>`<section class="${card} mb-5"><h2 class="border-b border-gray-100 px-4 py-3 font-semibold">${t}</h2>${body}</section>`;
  const lab='block text-xs font-medium text-gray-500';
  const shop=sec('Dados da barbearia',`<div class="grid gap-3 p-4 sm:grid-cols-2">
    <p class="text-xs text-gray-500 sm:col-span-2">As alterações são salvas automaticamente e aparecem para todos, em qualquer navegador.</p>
    <label class="${lab}">Nome da marca (topo)<input value="${esc(S.shop.brand)}" onchange="setShop('brand',this.value)" class="${inpC} mt-1 w-full"></label>
    <label class="${lab}">Nome da barbearia<input value="${esc(S.shop.name)}" onchange="setShop('name',this.value)" class="${inpC} mt-1 w-full"></label>
    <label class="${lab}">WhatsApp da barbearia<input value="${esc(S.shop.phone)}" inputmode="tel" placeholder="22999990000" onchange="setShop('phone',this.value)" class="${inpC} mt-1 w-full"></label>
</div>`);
  const weekSec=sec('Dias e horários de funcionamento',`<ul class="divide-y divide-gray-100">${[1,2,3,4,5,6,0].map(i=>{const w=S.week[i];return`<li class="flex flex-wrap items-center gap-3 px-4 py-3"><label class="flex w-32 items-center gap-2 font-medium"><input type="checkbox" ${w.on?'checked':''} onchange="setWeek(${i},'on',this.checked)" class="h-5 w-5">${DOW[i]}</label>${w.on?`<input type="time" value="${w.open}" onchange="setWeek(${i},'open',this.value)" class="${inpC}"><span class="text-sm text-gray-500">às</span><input type="time" value="${w.close}" onchange="setWeek(${i},'close',this.value)" class="${inpC}">`:'<span class="text-sm text-gray-500">Fechado: o cliente não vê horários</span>'}</li>`}).join('')}</ul>
    <p class="px-4 pb-3 text-xs text-gray-400">Vale toda semana. Para bloquear só um dia ou horário específico, use a aba Agenda.</p>`);
  const pros=sec('Profissionais',`<ul class="divide-y divide-gray-100">${S.pros.filter(isOn).map(p=>`<li class="flex items-center gap-2 px-4 py-3">
    <input value="${esc(p.name)}" onchange="updPro('${p.id}','name',this.value)" class="${inpC} min-w-0 flex-1" aria-label="Nome">
    <input type="number" min="0" max="100" value="${p.pct}" onchange="updPro('${p.id}','pct',this.value)" class="${inpC} w-16 text-right" aria-label="Comissão %"><span class="text-sm text-gray-500">%</span>
    <button onclick="rmPro('${p.id}')" class="${btnX}">Remover</button></li>`).join('')}</ul>
    <div class="flex gap-2 border-t border-gray-100 p-3"><input id="npName" placeholder="Novo profissional" class="${inpC} min-w-0 flex-1"><input id="npPct" type="number" value="50" class="${inpC} w-16"><button onclick="addPro()" class="rounded-lg bg-gray-900 px-3 text-sm font-medium text-white">Adicionar</button></div>`);
  const svcs=sec('Serviços',`<ul class="divide-y divide-gray-100">${S.services.filter(isOn).map(s=>`<li class="grid grid-cols-[1fr_5rem_4rem_auto] items-center gap-2 px-4 py-3">
    <input value="${esc(s.name)}" onchange="updSvc('${s.id}','name',this.value)" class="${inpC} min-w-0" aria-label="Nome">
    <input value="${(s.price/100).toFixed(2)}" inputmode="decimal" onchange="updSvc('${s.id}','price',this.value)" class="${inpC} text-right" aria-label="Preço em reais">
    <input type="number" value="${s.dur}" onchange="updSvc('${s.id}','dur',this.value)" class="${inpC} text-right" aria-label="Duração em minutos">
    <button onclick="rmSvc('${s.id}')" class="${btnX}">✕</button></li>`).join('')}</ul>
    <p class="px-4 pb-2 text-xs text-gray-400">Colunas: nome · preço (R$) · duração (min)</p>
    <div class="grid grid-cols-[1fr_5rem_4rem_auto] gap-2 border-t border-gray-100 p-3"><input id="nsName" placeholder="Novo serviço" class="${inpC} min-w-0"><input id="nsPrice" placeholder="R$" inputmode="decimal" class="${inpC}"><input id="nsDur" type="number" placeholder="min" class="${inpC}"><button onclick="addSvc()" class="rounded-lg bg-gray-900 px-3 text-sm font-medium text-white">+</button></div>`);
  const adds=sec('Adicionais (extras)',`<ul class="divide-y divide-gray-100">${S.addons.filter(isOn).map(s=>`<li class="grid grid-cols-[1fr_5rem_4rem_auto] items-center gap-2 px-4 py-3">
    <input value="${esc(s.name)}" onchange="updAdd('${s.id}','name',this.value)" class="${inpC} min-w-0" aria-label="Nome">
    <input value="${(s.price/100).toFixed(2)}" inputmode="decimal" onchange="updAdd('${s.id}','price',this.value)" class="${inpC} text-right" aria-label="Preço em reais">
    <input type="number" value="${s.dur}" onchange="updAdd('${s.id}','dur',this.value)" class="${inpC} text-right" aria-label="Duração em minutos">
    <button onclick="rmAdd('${s.id}')" class="${btnX}">✕</button></li>`).join('')}</ul>
    <p class="px-4 pb-2 text-xs text-gray-400">Colunas: nome · preço (R$) · duração (min). Aparecem como opcionais depois que o cliente escolhe o serviço.</p>
    <div class="grid grid-cols-[1fr_5rem_4rem_auto] gap-2 border-t border-gray-100 p-3"><input id="naName" placeholder="Novo adicional" class="${inpC} min-w-0"><input id="naPrice" placeholder="R$" inputmode="decimal" class="${inpC}"><input id="naDur" type="number" placeholder="min" class="${inpC}"><button onclick="addAdd()" class="rounded-lg bg-gray-900 px-3 text-sm font-medium text-white">+</button></div>`);
  const rem=sec('Mensagens de lembrete (WhatsApp)',`<div class="space-y-3 p-4 text-sm">
    <p class="text-xs text-gray-500">Na aba Agenda aparece o aviso “Lembretes para enviar”: 1 dia antes e 1 hora antes. Você toca em “Enviar no WhatsApp” e a mensagem abre pronta para o cliente. Use {nome} {servico} {data} {hora} {barbearia}.</p>
    <label class="${lab}">Lembrete de 1 dia antes<textarea rows="3" onchange="setShop('remind1d',this.value)" class="${inpC} mt-1 w-full">${esc(S.shop.remind1d)}</textarea></label>
    <label class="${lab}">Lembrete de 1 hora antes<textarea rows="3" onchange="setShop('remind1h',this.value)" class="${inpC} mt-1 w-full">${esc(S.shop.remind1h)}</textarea></label></div>`);
  const base=location.href.split('#')[0];
  const links=sec('Seus links',`<div class="space-y-2 p-4 text-sm"><p class="text-xs text-gray-500">Link para enviar aos clientes:</p><input readonly value="${esc(base)}" onclick="this.select()" class="${inpC} w-full"><p class="pt-1 text-xs text-gray-500">Seu acesso (não divulgue):</p><input readonly value="${esc(base)}#admin" onclick="this.select()" class="${inpC} w-full"></div>`);
  const wa=sec('Aviso por WhatsApp',`<div class="space-y-3 p-4 text-sm">
    <p class="text-xs text-gray-500">Quando alguém agenda, a mensagem é enviada para o número de “WhatsApp da barbearia” (acima).</p>
    <label class="flex items-start gap-2"><input type="checkbox" class="mt-1" ${S.shop.waAuto!==false?'checked':''} onchange="S.shop.waAuto=this.checked;touch()"> <span>Abrir o WhatsApp com a mensagem pronta após agendar (você só toca em enviar)</span></label>
    <label class="${lab}">Chave CallMeBot (opcional: envio 100% automático; fica só neste navegador)<input value="${esc(cmb())}" placeholder="apikey" onchange="try{localStorage.setItem('bf_cmb',this.value.trim())}catch(e){}" class="${inpC} mt-1 w-full"></label>
    <p class="text-xs text-gray-500">Para obter a chave grátis, siga as instruções em callmebot.com/blog/free-api-whatsapp-messages.</p>
    <button onclick="testWa()" class="rounded-lg bg-gray-900 px-3 py-2 text-sm font-medium text-white">Enviar mensagem de teste</button></div>`);
  return links+shop+weekSec+pros+svcs+adds+rem+wa;
}

/* ---------- Início ---------- */
if(READY){
  startPublic();
  auth.onAuthStateChanged(u=>{user=u;authReady=true;stopStaff();if(u)startStaff();render()});
}
setInterval(()=>{if(isAuth()&&isAdminUrl())softRender()},60000);
render();
</script>
</body>
</html>
