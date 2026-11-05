<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PANDA-BOT | Tu Asistente Matemático</title>
<style>
:root{--bg:#f4f7fb;--panel:#fff;--ink:#17243a;--muted:#718096;--line:#e5ebf3;--blue:#2869d8;--blue2:#eaf1ff;--nav:#111d32;--green:#15966b;--shadow:0 12px 35px rgba(25,45,78,.08)}
*{box-sizing:border-box}body{margin:0;font-family:Inter,ui-sans-serif,system-ui,-apple-system,"Segoe UI",sans-serif;background:var(--bg);color:var(--ink)}
button,input,select{font:inherit}button{cursor:pointer}
.app{min-height:100vh;display:grid;grid-template-columns:255px 1fr}
.sidebar{background:var(--nav);color:#fff;padding:24px 16px;display:flex;flex-direction:column;gap:28px}
.brand{display:flex;align-items:center;gap:11px;padding:0 9px}.logo{width:42px;height:42px;border-radius:13px;background:linear-gradient(135deg,#3688ff,#635bdb);display:grid;place-items:center;font-size:22px;font-weight:800}.brand strong{font-size:19px;letter-spacing:.4px}.brand small{display:block;color:#9eacc2;font-size:11px;margin-top:2px}
.nav-label{color:#8190a8;text-transform:uppercase;letter-spacing:1.2px;font-size:10px;font-weight:800;padding:0 12px;margin-bottom:8px}
.nav{display:grid;gap:5px}.nav button{border:0;background:transparent;color:#c4cee0;text-align:left;padding:11px 12px;border-radius:10px;display:flex;align-items:center;gap:12px;font-size:13px}.nav button:hover,.nav button.active{background:#233653;color:#fff}.nav .ico{width:19px;text-align:center;font-size:16px}
.sidebar-bottom{margin-top:auto;background:#1b2b45;border:1px solid #2c3c56;padding:14px;border-radius:13px}.sidebar-bottom b{font-size:12px}.sidebar-bottom p{color:#aebbd0;font-size:11px;line-height:1.5;margin:7px 0 0}
main{padding:30px clamp(18px,4vw,54px);max-width:1440px;width:100%;margin:auto}
.topbar{display:flex;justify-content:space-between;align-items:center;margin-bottom:30px}.crumb{font-size:12px;color:var(--muted)}.profile{display:flex;align-items:center;gap:9px;font-size:12px;color:var(--muted)}.avatar{width:34px;height:34px;border-radius:50%;background:#dce8ff;color:var(--blue);display:grid;place-items:center;font-weight:800}
.page{display:none}.page.active{display:block}
.eyebrow{color:var(--blue);font-size:11px;text-transform:uppercase;letter-spacing:1.5px;font-weight:800}
h1{font-size:clamp(28px,4vw,42px);letter-spacing:-1.3px;margin:9px 0 10px;line-height:1.12}h2{font-size:20px;margin:0 0 7px}h3{font-size:15px;margin:0 0 7px}.sub{color:var(--muted);font-size:14px;line-height:1.6;margin:0}
.hero{background:linear-gradient(115deg,#122544,#1d477f 70%,#315fae);border-radius:22px;padding:clamp(24px,4vw,42px);color:#fff;position:relative;overflow:hidden;box-shadow:var(--shadow)}
.hero:after{content:"🐼";position:absolute;right:7%;top:-10px;font-size:140px;opacity:0.15;pointer-events:none}
.hero .eyebrow{color:#a8c8ff}.hero h1{max-width:640px}.hero .sub{color:#c7d7ef;max-width:590px}
.searchbox{margin-top:24px;background:#fff;border-radius:14px;padding:8px;display:flex;gap:8px;max-width:720px;position:relative;z-index:1}.searchbox input{border:0;outline:0;flex:1;min-width:0;padding:10px 12px;color:var(--ink);font-size:13px}.primary{background:var(--blue);color:#fff;border:0;border-radius:10px;padding:11px 16px;font-weight:700;font-size:12px}.primary:hover{filter:brightness(1.08)}.hero .primary{background:#2869d8}
.quick{display:flex;gap:8px;flex-wrap:wrap;margin-top:14px;position:relative;z-index:1}.chip{border:1px solid #ffffff45;background:#ffffff12;color:#e9f1ff;border-radius:20px;padding:7px 11px;font-size:11px}
.section-head{display:flex;justify-content:space-between;align-items:end;margin:30px 0 14px}.section-head p{margin:0;color:var(--muted);font-size:12px}
.grid{display:grid;grid-template-columns:repeat(4,minmax(0,1fr));gap:14px}.card{background:var(--panel);border:1px solid var(--line);border-radius:16px;padding:18px;box-shadow:0 3px 15px rgba(25,45,78,.025)}.tool{transition:.18s;cursor:pointer}.tool:hover{transform:translateY(-3px);box-shadow:var(--shadow);border-color:#c8d8f5}.tool-icon{width:42px;height:42px;border-radius:12px;background:var(--blue2);display:grid;place-items:center;font-size:20px;margin-bottom:14px}.tool p{font-size:11px;color:var(--muted);line-height:1.5;margin:5px 0 0}.tool .go{color:var(--blue);font-size:11px;font-weight:800;margin-top:14px;display:block}
.lower{display:grid;grid-template-columns:1.3fr .7fr;gap:14px;margin-top:16px}.steps{display:grid;gap:13px;margin-top:15px}.step{display:flex;gap:11px;align-items:flex-start}.num{width:25px;height:25px;border-radius:8px;background:#edf3ff;color:var(--blue);display:grid;place-items:center;font-size:11px;font-weight:800;flex-shrink:0}.step p{margin:2px 0 0;color:var(--muted);font-size:11px;line-height:1.5}
.tag{font-size:10px;background:#e9f7f1;color:#137a58;border-radius:20px;padding:5px 8px;font-weight:800}
.formgrid{display:grid;grid-template-columns:repeat(2,minmax(0,1fr));gap:12px;margin-top:18px}.field label{display:block;font-size:11px;color:var(--muted);margin-bottom:6px}.field input,.field select,.chat-input input{width:100%;padding:11px 12px;border:1px solid var(--line);border-radius:10px;background:#fff;outline:none;color:var(--ink)}.field input:focus,.chat-input input:focus{border-color:#8eb2f5;box-shadow:0 0 0 3px #2869d812}
.result{margin-top:16px;padding:15px;border-radius:12px;background:#eff8f4;border:1px solid #d4eee2;display:none}.result strong{font-size:21px;color:#117451}.result p{font-size:11px;color:#477461;margin:5px 0 0}
.chatbox{background:#fff;border:1px solid var(--line);border-radius:16px;min-height:420px;display:flex;flex-direction:column;overflow:hidden;margin-top:18px}.chat-messages{padding:20px;display:grid;gap:14px;align-content:start;flex:1}.bubble{max-width:80%;padding:12px 14px;border-radius:13px;font-size:12px;line-height:1.6;white-space:pre-wrap}.bot{background:#f0f4fa;justify-self:start}.user{background:#e8f0ff;color:#234d94;justify-self:end}.chat-input{display:flex;gap:8px;padding:12px;border-top:1px solid var(--line)}.chat-input input{flex:1}
.empty{padding:25px;text-align:center;color:var(--muted);font-size:12px}
@media(max-width:1000px){.grid{grid-template-columns:repeat(2,minmax(0,1fr))}.app{grid-template-columns:220px 1fr}}
@media(max-width:700px){.app{display:block}.sidebar{padding:12px 14px;gap:12px}.brand{padding:0 4px}.sidebar .nav-label,.sidebar-bottom{display:none}.nav{display:flex;overflow:auto;gap:4px}.nav button{white-space:nowrap;padding:9px;font-size:11px}.nav .ico{display:none}main{padding:20px 15px}.topbar{margin-bottom:18px}.grid{grid-template-columns:repeat(2,minmax(0,1fr));gap:9px}.card{padding:14px}.lower{grid-template-columns:1fr}.searchbox{flex-wrap:wrap}.searchbox input{flex-basis:100%}.searchbox button{width:100%}.formgrid{grid-template-columns:1fr}}
</style>
</head>
<body>
<div class="app">
<aside class="sidebar">
<div class="brand"><div class="logo">🐼</div><div><strong>PANDA-BOT</strong><small>Tu asistente matemático</small></div></div>
<div><div class="nav-label">MENÚ PRINCIPAL</div><nav class="nav">
<button class="active" data-page="inicio"><span class="ico">⌂</span>Inicio</button>
<button data-page="asistente"><span class="ico">✦</span>Asistente IA</button>
<button data-page="herramientas"><span class="ico">▦</span>Herramientas</button>
<button data-page="ohm"><span class="ico">ϟ</span>Ley de Ohm</button>
<button data-page="conversiones"><span class="ico">⇄</span>Conversiones</button>
<button data-page="historial"><span class="ico">◷</span>Historial</button>
</nav></div>
<div class="sidebar-bottom"><b>✦ Aprende a tu ritmo</b><p>Resuelve tus ejercicios paso a paso con PANDA-BOT.</p></div>
</aside>
<main>
<div class="topbar"><div class="crumb">PANDA-BOT <span style="color:#b8c3d3"> / </span> <span id="crumb">Inicio</span></div><div class="profile"><div class="avatar">🐼</div><span>Mi espacio de aprendizaje</span></div></div>
 
  <section class="page active" id="inicio">
<div class="hero">
<div class="eyebrow">Tu espacio para aprender y resolver</div>
<h1>Las matemáticas, más fáciles con PANDA-BOT.</h1>
<p class="sub">Resuelve ejercicios, comprende procedimientos y encuentra herramientas para tus materias técnicas.</p>
<div class="searchbox"><input id="homeQuestion" placeholder="Escribe un problema o una operación..."><button class="primary" onclick="sendHome()">Resolver problema&nbsp; →</button></div>
<div class="quick"><button class="chip" onclick="openPage('ohm')">⚡ Ley de Ohm</button><button class="chip" onclick="openPage('herramientas')">∑ Álgebra</button><button class="chip" onclick="openPage('conversiones')">⇄ Conversiones</button></div>
</div>
<div class="section-head"><div><h2>¿Qué necesitas resolver?</h2><p>Entra directamente a una herramienta.</p></div></div>
<div class="grid">
<div class="card tool" onclick="openPage('asistente')"><div class="tool-icon">✦</div><h3>Asistente IA</h3><p>Escribe un problema y recibe ayuda paso a paso.</p><span class="go">Abrir asistente →</span></div>
<div class="card tool" onclick="openPage('ohm')"><div class="tool-icon">ϟ</div><h3>Electricidad</h3><p>Calcula voltaje, corriente y resistencia.</p><span class="go">Calcular →</span></div>
<div class="card tool" onclick="openPage('conversiones')"><div class="tool-icon">⇄</div><h3>Conversiones</h3><p>Convierte unidades de longitud y masa.</p><span class="go">Convertir →</span></div>
<div class="card tool" onclick="openPage('herramientas')"><div class="tool-icon">∑</div><h3>Álgebra y geometría</h3><p>Explora operaciones y fórmulas.</p><span class="go">Explorar →</span></div>
</div>
</section>
 
  <section class="page" id="asistente">
<div class="eyebrow">Asistente Inteligente</div><h1>¿Qué vamos a resolver hoy?</h1><p class="sub">Escribe tu problema de álgebra o electrónica. PANDA-BOT te ayudará a resolverlo paso a paso.</p>
<div class="chatbox">
<div class="chat-messages" id="messages">
<div class="bubble bot">¡Hola! Soy PANDA-BOT 🐼. Puedo ayudarte con álgebra, electrónica, conversiones y otros problemas matemáticos. ¿Qué ejercicio quieres resolver?</div>
</div>
<div class="chat-input">
<input id="chatQuestion" placeholder="Escribe aquí tu problema..." onkeydown="if(event.key==='Enter')sendChat()">
<button class="primary" onclick="sendChat()">Enviar ↑</button>
</div>
</div>
</section>
 
  <section class="page" id="herramientas">
<div class="eyebrow">Centro de herramientas</div><h1>Encuentra lo que necesitas.</h1><p class="sub">Selecciona una categoría para explorar sus funciones.</p>
<div class="grid" style="margin-top:22px">
<div class="card tool"><div class="tool-icon">∑</div><h3>Álgebra</h3><p>Ecuaciones, despejes, fracciones y sistemas.</p></div>
<div class="card tool" onclick="openPage('ohm')"><div class="tool-icon">ϟ</div><h3>Principios eléctricos</h3><p>Ley de Ohm y cálculos eléctricos.</p><span class="go">Abrir calculadora →</span></div>
<div class="card tool"><div class="tool-icon">⚙</div><h3>Torno y CNC</h3><p>Pasadas, medidas, cortes y tolerancias.</p></div>
<div class="card tool" onclick="openPage('conversiones')"><div class="tool-icon">⇄</div><h3>Metrología</h3><p>Unidades, pulgadas, milímetros y masa.</p><span class="go">Abrir conversiones →</span></div>
<div class="card tool"><div class="tool-icon">△</div><h3>Geometría</h3><p>Áreas, volúmenes y teorema de Pitágoras.</p></div>
<div class="card tool"><div class="tool-icon">▤</div><h3>Producción industrial</h3><p>Tiempo, cantidades y proporciones.</p></div>
</div>
</section>
 
  <section class="page" id="ohm">
<div class="eyebrow">Calculadora técnica</div><h1>Ley de Ohm</h1><p class="sub">Completa dos valores y selecciona qué dato quieres calcular.</p>
<div class="card" style="max-width:720px;margin-top:20px">
<div class="formgrid">
<div class="field"><label>Voltaje (V)</label><input id="volt" type="number" step="any" placeholder="Ej. 24"></div>
<div class="field"><label>Corriente (A)</label><input id="amp" type="number" step="any" placeholder="Ej. 2"></div>
<div class="field"><label>Resistencia (Ω)</label><input id="ohm" type="number" step="any" placeholder="Ej. 12"></div>
<div class="field"><label>¿Qué deseas calcular?</label><select id="target"><option value="v">Voltaje</option><option value="i">Corriente</option><option value="r">Resistencia</option></select></div>
</div>
<button class="primary" style="margin-top:16px" onclick="calculateOhm()">Calcular resultado</button>
<div class="result" id="ohmResult"></div>
</div>
</section>
 
  <section class="page" id="conversiones">
<div class="eyebrow">Calculadora de unidades</div><h1>Conversiones rápidas</h1><p class="sub">Convierte medidas comunes utilizadas en el taller.</p>
<div class="card" style="max-width:720px;margin-top:20px">
<div class="formgrid">
<div class="field"><label>Valor</label><input id="convValue" type="number" step="any" placeholder="Ej. 25.4"></div>
<div class="field"><label>Conversión</label><select id="convType"><option value="cm-in">Centímetros → pulgadas</option><option value="in-cm">Pulgadas → centímetros</option><option value="mm-in">Milímetros → pulgadas</option><option value="in-mm">Pulgadas → milímetros</option><option value="lb-kg">Libras → kilogramos</option><option value="kg-lb">Kilogramos → libras</option></select></div>
</div>
<button class="primary" style="margin-top:16px" onclick="convert()">Convertir</button>
<div class="result" id="convResult"></div>
</div>
</section>
 
  <section class="page" id="historial">
<div class="eyebrow">Tu actividad</div><h1>Historial de consultas</h1><p class="sub">En esta versión, tus consultas se muestran mientras mantengas abierta esta página.</p>
<div class="card" style="margin-top:20px" id="historyList"><div class="empty">Todavía no hay consultas. Cuando resuelvas un ejercicio aparecerá aquí.</div></div>
</section>
</main>
</div>
 
<script>
const names={inicio:"Inicio",asistente:"Asistente IA",herramientas:"Herramientas",ohm:"Ley de Ohm",conversiones:"Conversiones",historial:"Historial"};
let history=[];
 
function openPage(id){
  document.querySelectorAll('.page').forEach(p=>p.classList.remove('active'));
  document.getElementById(id).classList.add('active');
  document.querySelectorAll('.nav button').forEach(b=>b.classList.toggle('active',b.dataset.page===id));
  document.getElementById('crumb').textContent=names[id];
  window.scrollTo({top:0,behavior:'smooth'});
}
 
document.querySelectorAll('.nav button').forEach(b=>b.addEventListener('click',()=>openPage(b.dataset.page)));
 
function addHistory(s){
  history.unshift(s);
  document.getElementById('historyList').innerHTML=history.map(x=>`<div style="padding:12px 4px;border-bottom:1px solid var(--line);font-size:12px">◷ &nbsp;${escapeHtml(x)}</div>`).join('');
}
 
function escapeHtml(s){
  return s.replace(/[&<>"']/g,c=>({'&':'&amp;','<':'&lt;','>':'&gt;','"':'&quot;',"'":'&#39;'}[c]));
}
 
function sendHome(){
  let v=document.getElementById('homeQuestion').value.trim();
  if(!v)return;
  document.getElementById('chatQuestion').value=v;
  openPage('asistente');
  sendChat();
}
 
async function sendChat(){
  let input=document.getElementById('chatQuestion');
  let v=input.value.trim();
  if(!v)return;
 
  let box=document.getElementById('messages');
  box.insertAdjacentHTML('beforeend',`<div class="bubble user">${escapeHtml(v)}</div>`);
  input.value='';
  box.scrollTop=box.scrollHeight;
 
  let botId = 'bot-' + Date.now();
  box.insertAdjacentHTML('beforeend',`<div class="bubble bot" id="${botId}">🐼 PANDA-BOT está resolviendo tu problema...</div>`);
  box.scrollTop=box.scrollHeight;
 
  try {
    const respuesta = await pedirRespuestaIA(v);
    document.getElementById(botId).textContent = respuesta;
  } catch(e) {
    document.getElementById(botId).textContent = "Ocurrió un error al procesar tu pregunta. Revisa tu clave de API o tu conexión a internet.";
  }
 
  box.scrollTop=box.scrollHeight;
  addHistory(v);
}
 
// CONEXIÓN CON LA IA CONFIGURADA CON TU TOKEN AQ...
async function pedirRespuestaIA(pregunta){
  const TOKEN = "AQ.Ab8RN6IoTfBbCmkeq63EJOE5kLB-RyhF6XPq_D5rEoUWncF9jw"; 
  const url = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3.5-flash:generateContent`;
 
  const prompt = `Eres PANDA-BOT, un asistente matemático claro y amigable enfocado en álgebra, electrónica y metrología. Explica los problemas paso a paso de forma sencilla.\n\nProblema a resolver: ${pregunta}`;
 
  const res = await fetch(url, {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
      'Authorization': `Bearer ${TOKEN}`
    },
    body: JSON.stringify({
      contents: [{ parts: [{ text: prompt }] }]
    })
  });
 
  const data = await res.json();
  if (data.error) {
    throw new Error(data.error.message);
  }
  return data.candidates[0].content.parts[0].text;
}
 
function showResult(id,title,detail){
  let el=document.getElementById(id);
  el.style.display='block';
  el.innerHTML=`<strong>${title}</strong><p>${detail}</p>`;
}
 
function calculateOhm(){
  let v=parseFloat(document.getElementById('volt').value),i=parseFloat(document.getElementById('amp').value),r=parseFloat(document.getElementById('ohm').value),t=document.getElementById('target').value;
  let n=0,formula='',sub='';
  if(t==='v'){if(!Number.isFinite(i)||!Number.isFinite(r)||i<0||r<=0)return alert('Ingresa una corriente y una resistencia válidas.');n=i*r;formula='V = I × R';sub=`V = ${i} × ${r}`;}
  if(t==='i'){if(!Number.isFinite(v)||!Number.isFinite(r)||v<0||r<=0)return alert('Ingresa un voltaje y una resistencia válidas.');n=v/r;formula='I = V / R';sub=`I = ${v} / ${r}`;}
  if(t==='r'){if(!Number.isFinite(v)||!Number.isFinite(i)||v<0||i<=0)return alert('Ingresa un voltaje y una corriente válidas.');n=v/i;formula='R = V / I';sub=`R = ${v} / ${i}`;}
  let unit=t==='v'?'V':t==='i'?'A':'Ω';
  showResult('ohmResult',`${Number(n.toFixed(6))} ${unit}`,`Fórmula: ${formula}. Sustitución: ${sub}.`);
  addHistory(`Ley de Ohm: ${formula} = ${n} ${unit}`);
}
 
function convert(){
  let x=parseFloat(document.getElementById('convValue').value),type=document.getElementById('convType').value;
  if(!Number.isFinite(x))return alert('Ingresa un valor válido.');
  let factors={'cm-in':1/2.54,'in-cm':2.54,'mm-in':1/25.4,'in-mm':25.4,'lb-kg':1/2.20462,'kg-lb':2.20462};
  let labels={'cm-in':'pulgadas','in-cm':'centímetros','mm-in':'pulgadas','in-mm':'milímetros','lb-kg':'kilogramos','kg-lb':'libras'};
  let n=x*factors[type];
  showResult('convResult',`${Number(n.toFixed(6))} ${labels[type]}`,`Operación: ${x} × ${factors[type].toPrecision(7)} = ${n}.`);
  addHistory(`Conversión ${type}: ${x} = ${n} ${labels[type]}`);
}
</script>
</body>
</html>
