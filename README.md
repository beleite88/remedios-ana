<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>Remédios Ana</title>
<style>
:root {
  --bg:#f5f3fb; --surf:#fff; --pri:#9b7ec8; --pl:#ede8f7; --pm:#c9b8e8;
  --tx:#3a2d52; --ts:#7a6a96; --tm:#a899c0; --bd:#ddd4f0; --sh:rgba(155,126,200,.13);
  --mc:#c07a2a; --mb:#fff7ee; --mbd:#fde5c0;
  --dc:#4a9bbf; --db:#eef8fc; --dbd:#c6e8f4;
  --nc:#7b5eaa; --nb:#f0ebfa; --nbd:#d9ceee;
}
*{box-sizing:border-box;margin:0;padding:0}
body{font-family:-apple-system,BlinkMacSystemFont,'Segoe UI',sans-serif;background:var(--bg);color:var(--tx);min-height:100vh;padding-bottom:72px}
#loading{position:fixed;inset:0;background:var(--bg);display:flex;flex-direction:column;align-items:center;justify-content:center;z-index:999;gap:12px}
.spin{width:36px;height:36px;border:3px solid var(--bd);border-top-color:var(--pri);border-radius:50%;animation:sp .8s linear infinite}
@keyframes sp{to{transform:rotate(360deg)}}
#loading p{font-size:13px;color:var(--tm)}
header{background:linear-gradient(135deg,#c9b8e8,#a88fd0);padding:18px 20px 14px;text-align:center}
header h1{font-size:21px;font-weight:700;color:#fff}
.hico{font-size:26px;display:block;margin-bottom:3px}
.sbadge{display:inline-flex;align-items:center;gap:5px;font-size:11px;color:rgba(255,255,255,.85);margin-top:4px;cursor:pointer}
.sdot{width:7px;height:7px;border-radius:50%;background:#bbb;transition:background .3s;flex-shrink:0}
.sdot.ok{background:#a8e6a8}.sdot.saving{background:#f9c74f}.sdot.err{background:#e07070}
.tabs{display:flex;background:var(--surf);border-bottom:1px solid var(--bd);position:sticky;top:0;z-index:50}
.tbtn{flex:1;padding:10px 4px 8px;font-size:11px;font-weight:600;color:var(--tm);background:none;border:none;border-bottom:2.5px solid transparent;cursor:pointer;display:flex;flex-direction:column;align-items:center;gap:2px;text-transform:uppercase;letter-spacing:.2px;transition:color .15s,border-color .15s}
.tbtn em{font-size:17px;font-style:normal}
.tbtn.on{color:var(--pri);border-bottom-color:var(--pri)}
.pnl{display:none}.pnl.on{display:block}
.dbar{background:var(--surf);border-bottom:1px solid var(--bd);padding:9px 16px;display:flex;align-items:center;justify-content:space-between;gap:8px}
.dbar input[type=date]{font-size:14px;font-weight:600;color:var(--tx);border:1.5px solid var(--bd);border-radius:8px;padding:5px 10px;background:var(--bg);outline:none;cursor:pointer}
.dbar input[type=date]:focus{border-color:var(--pri)}
.gbtn{font-size:12px;color:var(--ts);background:none;border:1.5px solid var(--bd);border-radius:8px;padding:5px 11px;cursor:pointer}
.pw{padding:12px 16px 6px}
.pl{display:flex;justify-content:space-between;font-size:12px;color:var(--ts);margin-bottom:5px;font-weight:600}
.pbar{height:7px;background:var(--bd);border-radius:99px;overflow:hidden}
.pfill{height:100%;background:linear-gradient(90deg,var(--pm),var(--pri));border-radius:99px;transition:width .4s}
.sec{margin:10px 14px 0;border-radius:16px;overflow:hidden;box-shadow:0 2px 10px var(--sh)}
.shd{display:flex;align-items:center;gap:9px;padding:11px 14px;font-size:12px;font-weight:700;letter-spacing:.4px;text-transform:uppercase}
.shd .ico{font-size:17px}.shd .lbl{flex:1}
.shd .cnt{font-size:11px;font-weight:600;padding:2px 8px;border-radius:99px;opacity:.85}
.pm .shd{background:var(--mb);color:var(--mc);border-bottom:1px solid var(--mbd)}.pm .cnt{background:var(--mbd)}
.pd .shd{background:var(--db);color:var(--dc);border-bottom:1px solid var(--dbd)}.pd .cnt{background:var(--dbd)}
.pn .shd{background:var(--nb);color:var(--nc);border-bottom:1px solid var(--nbd)}.pn .cnt{background:var(--nbd)}
.item{background:var(--surf);display:flex;align-items:flex-start;gap:11px;padding:13px 14px;border-bottom:1px solid var(--bg)}
.item:last-of-type{border-bottom:none}
.item.chk{background:#f7f4fd}.item.dis{opacity:.42}
.circle{width:25px;height:25px;border-radius:50%;border:2px solid var(--pm);flex-shrink:0;display:flex;align-items:center;justify-content:center;margin-top:1px;background:#fff;cursor:pointer;transition:all .18s}
.item.chk .circle{background:var(--pri);border-color:var(--pri)}
.tick{display:none}.item.chk .tick{display:block}
.ib{flex:1;min-width:0}
.iname{font-size:15px;font-weight:600;color:var(--tx);line-height:1.3}
.item.chk .iname{color:var(--tm);text-decoration:line-through}
.item.dis .iname::after{content:' · encerrado';font-size:11px;font-weight:500;color:#c97a7a;text-decoration:none}
.inote{font-size:12px;color:var(--tm);margin-top:3px;line-height:1.4}
.item.chk .inote{color:var(--pm)}
.edbtn{opacity:0;background:none;border:none;cursor:pointer;padding:4px;border-radius:6px;color:var(--tm);font-size:14px;flex-shrink:0}
.item:hover .edbtn,.item:focus-within .edbtn{opacity:1}
.ef{display:none;width:100%;margin-top:9px;flex-direction:column;gap:6px}
.item.editing{background:var(--pl)}.item.editing .ef{display:flex}
.ef input{font-size:13px;border:1.5px solid var(--pm);border-radius:8px;padding:7px 10px;background:#fff;color:var(--tx);outline:none;font-family:inherit;width:100%}
.ef input:focus{border-color:var(--pri)}
.ea{display:flex;gap:6px;flex-wrap:wrap;margin-top:2px}
.sbtn{font-size:12px;font-weight:600;background:var(--pri);color:#fff;border:none;border-radius:8px;padding:7px 14px;cursor:pointer}
.cbtn{font-size:12px;background:none;color:var(--ts);border:1.5px solid var(--bd);border-radius:8px;padding:7px 12px;cursor:pointer}
.dbtn{font-size:12px;background:none;color:#c97a7a;border:1.5px solid #f0c0c0;border-radius:8px;padding:7px 12px;cursor:pointer}
.wbtn{font-size:12px;background:none;color:#b07a30;border:1.5px solid #f0d8b0;border-radius:8px;padding:7px 12px;cursor:pointer}
.arow{display:flex;align-items:center;gap:9px;padding:10px 14px;background:var(--surf);border-top:1px dashed var(--bd);cursor:pointer;color:var(--tm);font-size:13px}
.aform{display:none;flex-direction:column;gap:7px;padding:12px 14px;background:var(--pl);border-top:1px solid var(--bd)}
.aform.open{display:flex}
.aform input{font-size:13px;border:1.5px solid var(--pm);border-radius:8px;padding:7px 11px;background:#fff;color:var(--tx);outline:none;font-family:inherit}
.aform input:focus{border-color:var(--pri)}
.nw{margin:12px 14px 0}
.nl{font-size:11px;font-weight:700;text-transform:uppercase;letter-spacing:.5px;color:var(--tm);margin-bottom:5px}
textarea.nt{width:100%;min-height:66px;background:var(--surf);border:1.5px solid var(--bd);border-radius:12px;padding:10px 13px;font-size:13px;color:var(--tx);font-family:inherit;resize:none;outline:none;box-shadow:0 1px 6px var(--sh)}
textarea.nt:focus{border-color:var(--pri)}
.cw{padding:14px}
.cnav{display:flex;align-items:center;justify-content:space-between;margin-bottom:12px}
.cnav h2{font-size:16px;font-weight:700}
.nvb{background:none;border:1.5px solid var(--bd);border-radius:8px;padding:5px 14px;cursor:pointer;color:var(--ts);font-size:16px}
.cgrid{display:grid;grid-template-columns:repeat(7,1fr);gap:4px;margin-bottom:12px}
.cdn{text-align:center;font-size:10px;font-weight:700;color:var(--tm);text-transform:uppercase;padding:4px 0}
.cc{aspect-ratio:1;border-radius:10px;display:flex;flex-direction:column;align-items:center;justify-content:center;cursor:pointer;position:relative;font-size:13px;font-weight:500;color:var(--ts);border:1.5px solid transparent}
.cc.today{border-color:var(--pri);color:var(--pri);font-weight:700}
.cc.sel{background:var(--pri)!important;color:#fff!important}
.cc.full{background:#d4f0d4}.cc.partial{background:#fef3d4}.cc.noday{background:#fde0e0}
.cc.future{opacity:.28;cursor:default}
.cc .dot{width:5px;height:5px;border-radius:50%;background:var(--pri);position:absolute;bottom:3px}
.cdet{background:var(--surf);border-radius:14px;padding:14px;box-shadow:0 2px 10px var(--sh)}
.cdet h3{font-size:14px;font-weight:700;margin-bottom:10px}
.cemp{font-size:13px;color:var(--tm);text-align:center;padding:16px 0}
.crow{display:flex;align-items:center;gap:9px;padding:7px 0;border-bottom:1px solid var(--bg)}
.crow:last-child{border-bottom:none}
.cchk{width:20px;height:20px;border-radius:50%;flex-shrink:0;display:flex;align-items:center;justify-content:center;font-size:11px}
.cchk.y{background:var(--pri);color:#fff}.cchk.n{background:#f0e8f8;color:var(--tm);border:1.5px solid var(--bd)}
.cmn{font-size:13px;font-weight:500;color:var(--tx);flex:1}
.cper{font-size:11px;color:var(--tm)}
.sw{padding:14px}
.scard{background:var(--surf);border-radius:14px;margin-bottom:10px;overflow:hidden;box-shadow:0 2px 10px var(--sh)}
.sper{font-size:11px;font-weight:700;text-transform:uppercase;letter-spacing:.4px;padding:9px 14px 7px}
.pm .sper{background:var(--mb);color:var(--mc);border-bottom:1px solid var(--mbd)}
.pd .sper{background:var(--db);color:var(--dc);border-bottom:1px solid var(--dbd)}
.pn .sper{background:var(--nb);color:var(--nc);border-bottom:1px solid var(--nbd)}
.sitem{padding:12px 14px;border-bottom:1px solid var(--bg);display:flex;gap:10px;align-items:flex-start}
.sitem:last-child{border-bottom:none}
.sitem.dis{opacity:.42}
.pill{font-size:11px;font-weight:600;padding:2px 9px;border-radius:99px;flex-shrink:0;margin-top:2px;background:var(--pl);color:var(--pri)}
.sitem.dis .pill{background:#fde8e8;color:#c97a7a}
.snm{font-size:15px;font-weight:600;color:var(--tx);line-height:1.3}
.sitem.dis .snm{text-decoration:line-through;color:var(--tm)}
.spos{font-size:12px;color:var(--ts);margin-top:3px;line-height:1.4}
.sdlb{font-size:11px;color:#c97a7a;margin-top:3px}
.toast{position:fixed;bottom:22px;left:50%;transform:translateX(-50%) translateY(12px);background:#3a2d52;color:#fff;font-size:13px;font-weight:500;padding:10px 20px;border-radius:99px;opacity:0;pointer-events:none;transition:all .22s;z-index:300;white-space:nowrap}
.toast.on{opacity:1;transform:translateX(-50%) translateY(0)}
</style>
</head>
<body>

<div id="loading"><div class="spin"></div><p>Conectando…</p></div>

<header>
  <span class="hico">💊</span>
  <h1>Remédios da Ana</h1>
  <div class="sbadge" id="sbadge">
    <span class="sdot" id="sdot"></span>
    <span id="slbl">Conectando…</span>
  </div>
</header>

<div class="tabs">
  <button class="tbtn on" id="tb-daily" onclick="switchTab('daily')"><em>💊</em>Hoje</button>
  <button class="tbtn" id="tb-calendar" onclick="switchTab('calendar')"><em>📅</em>Histórico</button>
  <button class="tbtn" id="tb-summary" onclick="switchTab('summary')"><em>📋</em>Resumo</button>
</div>

<div class="pnl on" id="pnl-daily">
  <div class="dbar">
    <input type="date" id="date-inp">
    <button class="gbtn" onclick="resetDay()">Limpar dia</button>
  </div>
  <div class="pw">
    <div class="pl"><span>Progresso</span><span id="ptxt">0 / 0</span></div>
    <div class="pbar"><div class="pfill" id="pfill" style="width:0%"></div></div>
  </div>
  <div id="secs"></div>
  <div class="nw" style="margin-bottom:8px">
    <div class="nl">Observações</div>
    <textarea class="nt" id="notes" placeholder="Sintomas, reações, horários reais…"></textarea>
  </div>
</div>

<div class="pnl" id="pnl-calendar">
  <div class="cw">
    <div class="cnav">
      <button class="nvb" onclick="calNav(-1)">&#8249;</button>
      <h2 id="cal-title"></h2>
      <button class="nvb" onclick="calNav(1)">&#8250;</button>
    </div>
    <div class="cgrid" id="cgrid"></div>
    <div class="cdet" id="cdet"><p class="cemp">Selecione um dia para ver o detalhe.</p></div>
  </div>
</div>

<div class="pnl" id="pnl-summary">
  <div class="sw" id="sum"></div>
</div>

<div class="toast" id="toast"></div>

<!-- Firebase carregado ANTES do script do app -->
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-app-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-auth-compat.js"></script>
<script src="https://www.gstatic.com/firebasejs/9.23.0/firebase-firestore-compat.js"></script>

<script>
var PERIODS = {
  manha:{label:'Manha',icon:'🌅',cls:'pm'},
  dia:  {label:'Ao longo do dia',icon:'☀️',cls:'pd'},
  noite:{label:'Antes de dormir',icon:'🌙',cls:'pn'}
};
var DEFAULT = [
  {id:'m1',period:'manha',name:'Puran',note:'1 comprimido — ainda deitada, em jejum. Permanecer deitada >25 min',discontinued:false},
  {id:'m2',period:'manha',name:'Vitamina D3',note:'No café da manhã — 5 gotas',discontinued:false},
  {id:'m3',period:'manha',name:'Vitamina manipulada',note:'3 cápsulas — pela manhã',discontinued:false},
  {id:'n1',period:'noite',name:'Slim Fort',note:'2 cápsulas — por 30 dias',discontinued:false},
  {id:'n2',period:'noite',name:'Ômega 3',note:'5 gotas — congelar antes de tomar',discontinued:false}
];

var tmpl=[],days={},cur='',today='',calY=null,calM=null,calSel=null,saveTimer=null;
var auth,db,fbReady=false;

function setSync(s,msg){
  document.getElementById('sdot').className='sdot '+s;
  document.getElementById('slbl').textContent=msg||{ok:'Sincronizado',saving:'Salvando…',err:'Erro de sync'}[s]||s;
}
function pad(n){return String(n).padStart(2,'0')}
function todayStr(){var n=new Date();return n.getFullYear()+'-'+pad(n.getMonth()+1)+'-'+pad(n.getDate())}
function esc(s){return String(s).replace(/&/g,'&amp;').replace(/</g,'&lt;').replace(/>/g,'&gt;').replace(/"/g,'&quot;')}
function toast(m){var t=document.getElementById('toast');t.textContent=m;t.classList.add('on');clearTimeout(t._t);t._t=setTimeout(function(){t.classList.remove('on')},2200)}
function actives(){return tmpl.filter(function(m){return !m.discontinued})}
function getChks(d){return(days[d]||{}).checks||{}}
function setChk(d,id,v){if(!days[d])days[d]={checks:{},notes:''};if(!days[d].checks)days[d].checks={};days[d].checks[id]=v;schedSave(d)}
function getNotes(d){return(days[d]||{}).notes||''}
function setNotes(d,v){if(!days[d])days[d]={checks:{},notes:''};days[d].notes=v;schedSave(d)}
function fmtDate(s){var p=s.split('-');return new Date(+p[0],+p[1]-1,+p[2]).toLocaleDateString('pt-BR',{weekday:'long',day:'numeric',month:'long',year:'numeric'})}

function fbSaveTmpl(){
  if(!fbReady||!db){setSync('err','Sem sync');return;}
  setSync('saving');
  db.collection('config').doc('template').set({items:tmpl})
    .then(function(){setSync('ok')}).catch(function(e){setSync('err');console.error(e)});
}
function schedSave(dateStr){
  if(!fbReady||!db){setSync('err','Sem sync');return;}
  clearTimeout(saveTimer);
  saveTimer=setTimeout(function(){
    setSync('saving');
    db.collection('days').doc(dateStr).set(days[dateStr]||{})
      .then(function(){setSync('ok')}).catch(function(e){setSync('err');console.error(e)});
  },900);
}

function renderDaily(){
  var secs=document.getElementById('secs');secs.innerHTML='';
  var chks=getChks(cur);
  ['manha','dia','noite'].forEach(function(pk){
    var meds=tmpl.filter(function(m){return m.period===pk});
    if(!meds.length)return;
    var p=PERIODS[pk];
    var act=meds.filter(function(m){return !m.discontinued});
    var done=act.filter(function(m){return chks[m.id]}).length;
    var sec=document.createElement('div');sec.className='sec '+p.cls;
    sec.innerHTML='<div class="shd"><span class="ico">'+p.icon+'</span><span class="lbl">'+p.label+'</span><span class="cnt">'+done+'/'+act.length+'</span></div>';
    meds.forEach(function(med){
      var isC=!!chks[med.id];
      var d=document.createElement('div');
      d.className='item'+(isC?' chk':'')+(med.discontinued?' dis':'');
      d.dataset.id=med.id;
      d.innerHTML='<div class="circle" data-id="'+med.id+'"><svg class="tick" width="13" height="13" viewBox="0 0 14 14" fill="none"><path d="M2.5 7L5.5 10L11.5 4" stroke="white" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/></svg></div>'
        +'<div class="ib"><div class="iname">'+esc(med.name)+'</div>'+(med.note?'<div class="inote">'+esc(med.note)+'</div>':'')
        +'<div class="ef"><input class="en" type="text" value="'+esc(med.name)+'" placeholder="Nome"><input class="eo" type="text" value="'+esc(med.note||'')+'" placeholder="Posologia">'
        +'<div class="ea"><button class="sbtn" data-a="save" data-id="'+med.id+'">Salvar</button><button class="cbtn" data-a="cancel">Cancelar</button>'
        +'<button class="'+(med.discontinued?'sbtn':'wbtn')+'" data-a="disc" data-id="'+med.id+'">'+(med.discontinued?'&#8629; Reativar':'&#9646; Encerrar uso')+'</button>'
        +'<button class="dbtn" data-a="del" data-id="'+med.id+'">Remover</button></div></div></div>'
        +'<button class="edbtn" data-a="edit">&#9998;</button>';
      sec.appendChild(d);
    });
    var ar=document.createElement('div');ar.className='arow';ar.dataset.period=pk;
    ar.innerHTML='<span style="font-size:17px;font-weight:300;line-height:1">+</span> Adicionar remédio';
    sec.appendChild(ar);
    var af=document.createElement('div');af.className='aform';af.dataset.period=pk;
    af.innerHTML='<input class="an" type="text" placeholder="Nome do remédio"><input class="ao" type="text" placeholder="Posologia / observação">'
      +'<div class="ea"><button class="sbtn" data-a="addok">Adicionar</button><button class="cbtn" data-a="addx">Cancelar</button></div>';
    sec.appendChild(af);
    secs.appendChild(sec);
  });
  updProg();
  document.getElementById('notes').value=getNotes(cur);
}

function updProg(){
  var chks=getChks(cur),act=actives();
  var done=act.filter(function(m){return chks[m.id]}).length;
  document.getElementById('ptxt').textContent=done+' / '+act.length;
  document.getElementById('pfill').style.width=act.length?Math.round(done/act.length*100)+'%':'0%';
}

document.getElementById('secs').addEventListener('click',function(e){
  var circle=e.target.closest('.circle');
  var btn=e.target.closest('[data-a]');
  var ar=e.target.closest('.arow');
  if(circle&&!btn){
    var id=circle.dataset.id,med=tmpl.find(function(m){return m.id===id});
    if(med&&med.discontinued)return;
    var v=!getChks(cur)[id];setChk(cur,id,v);renderDaily();
    if(v)toast('&#10003; '+med.name);
    return;
  }
  if(btn){
    var a=btn.dataset.a,id=btn.dataset.id;
    var item=btn.closest('.item');
    var idx=id?tmpl.findIndex(function(m){return m.id===id}):-1;
    if(a==='edit'){
      document.querySelectorAll('.item.editing').forEach(function(d){if(d!==item)d.classList.remove('editing')});
      item.classList.toggle('editing');
      if(item.classList.contains('editing'))item.querySelector('.en').focus();
      return;
    }
    if(a==='cancel'){item.classList.remove('editing');return}
    if(a==='save'&&idx>-1){
      tmpl[idx].name=item.querySelector('.en').value.trim()||tmpl[idx].name;
      tmpl[idx].note=item.querySelector('.eo').value.trim();
      fbSaveTmpl();renderDaily();renderSummary();toast('Salvo');return;
    }
    if(a==='disc'&&idx>-1){
      var isD=tmpl[idx].discontinued;
      if(!confirm(isD?'Reativar '+tmpl[idx].name+'?':'Encerrar uso de '+tmpl[idx].name+'?'))return;
      tmpl[idx].discontinued=!isD;
      fbSaveTmpl();renderDaily();renderSummary();
      toast(isD?'Reativado':'Uso encerrado');return;
    }
    if(a==='del'&&idx>-1){
      if(!confirm('Remover '+tmpl[idx].name+'?'))return;
      tmpl.splice(idx,1);fbSaveTmpl();renderDaily();renderSummary();toast('Removido');return;
    }
    if(a==='addok'){
      var form=btn.closest('.aform');
      var name=form.querySelector('.an').value.trim();if(!name)return;
      var note=form.querySelector('.ao').value.trim();
      var per=form.dataset.period;
      tmpl.push({id:per[0]+Date.now(),period:per,name:name,note:note,discontinued:false});
      fbSaveTmpl();form.classList.remove('open');renderDaily();renderSummary();toast('Adicionado');return;
    }
    if(a==='addx'){btn.closest('.aform').classList.remove('open');return}
  }
  if(ar){
    var per=ar.dataset.period,form=ar.nextElementSibling;
    form.classList.toggle('open');
    if(form.classList.contains('open'))form.querySelector('.an').focus();
  }
});

document.getElementById('notes').addEventListener('input',function(e){setNotes(cur,e.target.value)});

function resetDay(){
  if(!confirm('Desmarcar todos os itens?'))return;
  if(days[cur])days[cur].checks={};
  schedSave(cur);renderDaily();toast('Dia resetado');
}

function renderCal(){
  var now=new Date();
  if(!calY){calY=now.getFullYear();calM=now.getMonth()}
  var tit=new Date(calY,calM,1).toLocaleDateString('pt-BR',{month:'long',year:'numeric'});
  document.getElementById('cal-title').textContent=tit.charAt(0).toUpperCase()+tit.slice(1);
  var grid=document.getElementById('cgrid');grid.innerHTML='';
  ['D','S','T','Q','Q','S','S'].forEach(function(d){var e=document.createElement('div');e.className='cdn';e.textContent=d;grid.appendChild(e)});
  var first=new Date(calY,calM,1).getDay(),dim=new Date(calY,calM+1,0).getDate(),tds=todayStr();
  for(var i=0;i<first;i++)grid.appendChild(document.createElement('div'));
  for(var d=1;d<=dim;d++){
    var ds=calY+'-'+pad(calM+1)+'-'+pad(d);
    var cell=document.createElement('div');cell.className='cc';cell.textContent=d;
    if(ds>tds){cell.classList.add('future')}
    else{
      var data=days[ds];
      if(data&&data.checks){
        var act=actives(),done=act.filter(function(m){return data.checks[m.id]}).length;
        if(act.length>0){
          if(done===act.length)cell.classList.add('full');
          else if(done>0)cell.classList.add('partial');
          else cell.classList.add('noday');
        }
        if(done>0){var dot=document.createElement('div');dot.className='dot';cell.appendChild(dot)}
      }
      (function(s,c){c.onclick=function(){calSel=s;document.querySelectorAll('.cc.sel').forEach(function(x){x.classList.remove('sel')});c.classList.add('sel');renderCalDet(s)}})(ds,cell);
    }
    if(ds===tds)cell.classList.add('today');
    if(ds===calSel)cell.classList.add('sel');
    grid.appendChild(cell);
  }
  if(calSel)renderCalDet(calSel);
}

function renderCalDet(ds){
  var det=document.getElementById('cdet');
  var chks=(days[ds]||{}).checks||{},notes=(days[ds]||{}).notes||'';
  det.innerHTML='<h3>'+esc(fmtDate(ds))+'</h3>';
  if(!Object.keys(chks).length&&!notes){det.innerHTML+='<p class="cemp">Nenhum dado registrado.</p>';return}
  ['manha','dia','noite'].forEach(function(pk){
    var meds=tmpl.filter(function(m){return m.period===pk&&!m.discontinued});
    var p=PERIODS[pk];
    meds.forEach(function(med){
      var done=!!chks[med.id];
      var row=document.createElement('div');row.className='crow';
      row.innerHTML='<div class="cchk '+(done?'y':'n')+'">'+(done?'&#10003;':'–')+'</div>'
        +'<div class="cmn">'+esc(med.name)+'</div><div class="cper">'+p.icon+' '+p.label+'</div>';
      det.appendChild(row);
    });
  });
  if(notes){
    var nb=document.createElement('div');
    nb.style.cssText='margin-top:10px;padding:9px 12px;background:var(--bg);border-radius:10px;font-size:12px;color:var(--ts);line-height:1.5';
    nb.innerHTML='<strong>Obs.:</strong> '+esc(notes);
    det.appendChild(nb);
  }
}

function calNav(dir){
  calM+=dir;if(calM<0){calM=11;calY--}if(calM>11){calM=0;calY++}renderCal();
}

function renderSummary(){
  var c=document.getElementById('sum');c.innerHTML='';
  ['manha','dia','noite'].forEach(function(pk){
    var meds=tmpl.filter(function(m){return m.period===pk});
    if(!meds.length)return;
    var p=PERIODS[pk];
    var card=document.createElement('div');card.className='scard '+p.cls;
    card.innerHTML='<div class="sper">'+p.icon+'  '+p.label+'</div>';
    meds.forEach(function(med){
      var row=document.createElement('div');row.className='sitem'+(med.discontinued?' dis':'');
      row.innerHTML='<div class="pill">'+(med.discontinued?'Encerrado':'Ativo')+'</div>'
        +'<div><div class="snm">'+esc(med.name)+'</div>'
        +(med.note?'<div class="spos">'+esc(med.note)+'</div>':'')
        +(med.discontinued?'<div class="sdlb">Uso encerrado</div>':'')+'</div>';
      card.appendChild(row);
    });
    c.appendChild(card);
  });
}

function switchTab(tab){
  document.querySelectorAll('.pnl').forEach(function(p){p.classList.remove('on')});
  document.querySelectorAll('.tbtn').forEach(function(b){b.classList.remove('on')});
  document.getElementById('pnl-'+tab).classList.add('on');
  document.getElementById('tb-'+tab).classList.add('on');
  if(tab==='calendar')renderCal();
  if(tab==='summary')renderSummary();
}

document.getElementById('sbadge').addEventListener('click',function(){
  // Se houve erro, mostra o diagnóstico completo
  if(document.getElementById('sdot').classList.contains('err')){
    alert('DIAGNÓSTICO\n\n'+(window._lastErr||'Login anônimo não retornou. Verifique se "Anonymous" está ativado em Authentication > Sign-in method.'));
    return;
  }
  if(!fbReady){alert('Firebase não conectou.');return;}
  setSync('saving');
  Promise.all([
    db.collection('config').doc('template').set({items:tmpl}),
    db.collection('days').doc(cur).set(days[cur]||{})
  ]).then(function(){setSync('ok');toast('Sincronizado')})
    .catch(function(){setSync('err')});
});

// Mostra a interface imediatamente (não espera o Firebase)
function showApp(){
  if(document.getElementById('loading').style.display==='none')return;
  document.getElementById('loading').style.display='none';
  today=todayStr();cur=today;
  var inp=document.getElementById('date-inp');
  inp.value=today;
  inp.addEventListener('change',function(){cur=inp.value;renderDaily()});
  renderDaily();
  renderSummary();
}

// BOOT — roda depois que todos os scripts carregaram
window.addEventListener('load', function() {
  // Verifica se o SDK Firebase carregou
  if(typeof firebase==='undefined'){
    tmpl=JSON.parse(JSON.stringify(DEFAULT));
    setSync('err','Sem internet');
    showApp();
    return;
  }

  // Carrega a interface com dados padrão após no máximo 15s, mesmo sem Firebase
  var fallbackTimer=setTimeout(function(){
    if(!fbReady){
      if(!tmpl.length)tmpl=JSON.parse(JSON.stringify(DEFAULT));
      setSync('err','Sem conexão');
      showApp();
    }
  },15000);

  try{
    firebase.initializeApp({
      apiKey:"AIzaSyCh8HMgWpPRAVoqxFT_b_Eq8lwAKM8Lz6M",
      authDomain:"remedios-tikinha.firebaseapp.com",
      projectId:"remedios-tikinha",
      storageBucket:"remedios-tikinha.firebasestorage.app",
      messagingSenderId:"548262095812",
      appId:"1:548262095812:web:2994f40d787e55d2bf5291"
    });
    auth=firebase.auth();
    db=firebase.firestore();
  }catch(e){
    clearTimeout(fallbackTimer);
    tmpl=JSON.parse(JSON.stringify(DEFAULT));
    setSync('err','Erro Firebase');
    showApp();
    console.error(e);
    return;
  }

  var authTimeout=new Promise(function(_,reject){
    setTimeout(function(){reject({code:'timeout',message:'Login anônimo não respondeu em 8s. Verifique se Anonymous está ativado em Authentication.'});},8000);
  });

  Promise.race([auth.signInAnonymously(), authTimeout])
    .then(function(){
      return db.collection('config').doc('template').get();
    })
    .then(function(snap){
      if(snap.exists && snap.data().items && snap.data().items.length){
        tmpl=snap.data().items;
      } else {
        tmpl=JSON.parse(JSON.stringify(DEFAULT));
        return db.collection('config').doc('template').set({items:tmpl});
      }
    })
    .then(function(){
      return db.collection('days').get();
    })
    .then(function(snap){
      snap.forEach(function(d){days[d.id]=d.data()});
      fbReady=true;
      clearTimeout(fallbackTimer);
      setSync('ok');
      showApp();
    })
    .catch(function(e){
      clearTimeout(fallbackTimer);
      // App ainda funciona em modo local com os defaults
      if(!tmpl.length)tmpl=JSON.parse(JSON.stringify(DEFAULT));
      window._lastErr=(e.code||'')+' | '+(e.message||e);
      setSync('err', e.code==='permission-denied'?'Regras bloqueadas':'Sem sync');
      showApp();
      console.error('Firebase erro:',e.code,e.message);
    });
});
</script>
</body>
</html>
