<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>El Cubo de la Comunicación · Econotopía</title>
<meta name="author" content="Víctor Hugo Ramírez Salgado">
<style>
:root{--bg:#f6f4ef;--card:#fff;--tx:#1d1d1f;--mu:#6b6b70;--ln:#d9d6cf;--ac:#1f5fbf;--ok:#1a8a4a;--bad:#c0392b;--hi:#ffe08a}
@media (prefers-color-scheme:dark){:root{--bg:#141416;--card:#1e1e22;--tx:#eee;--mu:#9a9aa2;--ln:#34343a;--ac:#6ea3ff;--ok:#3fcf7d;--bad:#ff6b5b;--hi:#5a4a10}}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--tx);font:16px/1.5 -apple-system,system-ui,Segoe UI,Roboto,sans-serif}
header,main,footer{max-width:980px;margin:auto;padding:16px}
h1{font-size:1.6rem;margin:.2em 0}h2{font-size:1.2rem;margin:0 0 .5em}
.mu{color:var(--mu);font-size:.9rem}
.card{background:var(--card);border:1px solid var(--ln);border-radius:12px;padding:16px;margin:14px 0}
textarea,select,input,button{font:inherit;color:inherit}
textarea,select,input{background:var(--bg);border:1px solid var(--ln);border-radius:8px;padding:8px;width:100%}
textarea{min-height:60px;resize:vertical}
button{background:var(--ac);color:#fff;border:0;border-radius:8px;padding:10px 14px;margin:4px 4px 4px 0;cursor:pointer}
button.sec{background:transparent;color:var(--ac);border:1px solid var(--ac)}
.row{display:grid;grid-template-columns:1fr 110px;gap:8px;margin:8px 0}
.out{font-family:ui-monospace,Menlo,monospace;font-size:.9rem;white-space:pre-wrap;word-break:break-word;background:var(--bg);border:1px solid var(--ln);border-radius:8px;padding:10px;min-height:44px}
.tabs button{padding:8px 12px}
.tabs button.on{background:var(--tx);color:var(--bg)}
.gridwrap{overflow:auto;max-height:70vh;border:1px solid var(--ln);border-radius:8px}
table{border-collapse:collapse;font-family:ui-monospace,Menlo,monospace}
td,th{border:1px solid var(--ln);min-width:38px;height:30px;text-align:center;font-size:11px;padding:0 2px}
th{background:var(--tx);color:var(--bg);font-size:13px;font-weight:700}
td.u{background:var(--hi);font-weight:700}
td.ini{outline:3px solid var(--ok);outline-offset:-3px}
td.fin{outline:3px solid var(--bad);outline-offset:-3px}
.key{font-family:ui-monospace,Menlo,monospace;font-size:.8rem;word-break:break-all}
.legend span{display:inline-block;padding:2px 8px;border-radius:6px;margin-right:6px;font-size:.85rem}
.beta{font-size:.75rem;background:var(--hi);padding:1px 6px;border-radius:6px}
#recibido{display:none;border-color:var(--ok)}
.escena{perspective:900px;height:340px;display:flex;align-items:center;justify-content:center;touch-action:none;user-select:none;-webkit-user-select:none}
.cubo{width:220px;height:220px;position:relative;transform-style:preserve-3d}
.cubo .cara{position:absolute;inset:0;width:220px;height:220px;border:1px solid var(--tx);box-shadow:0 0 0 1px var(--ln)}
.cubo canvas{width:100%;height:100%;display:block}
.cubo .c1{transform:translateZ(110px)}.cubo .c2{transform:rotateY(90deg) translateZ(110px)}
.cubo .c3{transform:rotateY(180deg) translateZ(110px)}.cubo .c4{transform:rotateY(-90deg) translateZ(110px)}
.cubo .c5{transform:rotateX(90deg) translateZ(110px)}.cubo .c6{transform:rotateX(-90deg) translateZ(110px)}
.escena.cruz{perspective:none;height:auto;padding:8px 0}
.escena.cruz .cubo{transform:none!important;display:grid;grid-template-columns:repeat(4,1fr);gap:2px;width:min(100%,440px);height:auto}
.escena.cruz .cara{position:static;transform:none;width:auto;height:auto;aspect-ratio:1}
.escena.cruz .c5{grid-column:2;grid-row:1}.escena.cruz .c4{grid-column:1;grid-row:2}.escena.cruz .c1{grid-column:2;grid-row:2}
.escena.cruz .c2{grid-column:3;grid-row:2}.escena.cruz .c3{grid-column:4;grid-row:2}.escena.cruz .c6{grid-column:2;grid-row:3}
</style>
</head>
<body>
<header>
  <p class="mu">Econotopía · por Víctor Hugo Ramírez Salgado</p>
  <h1>El Cubo de la Comunicación</h1>
  <p>Cubo de 6 caras de 26 × 26 con letras A–Z en los cuatro bordes y numeración secuencial del 1 al 4056. Cada par de letras ocupa una casilla numerada.</p>
  <div class="card">
    <strong>Autor en clave del cubo</strong> <span class="mu">(lados 1 a 6, separados con “L”)</span>
    <div id="clave" class="key"></div>
  </div>
</header>

<main>
<section id="recibido" class="card">
  <h2>Mensaje recibido</h2>
  <div id="recTxt" class="out"></div>
  <p class="mu">Este mensaje se muestra una sola vez en este dispositivo.</p>
</section>

<section class="card">
  <h2>1 · Tu alfabeto</h2>
  <label>Letra de inicio del alfabeto (tu clave personal)</label>
  <select id="inicio"></select>
  <p class="mu">Quien reciba tu mensaje debe usar la misma letra de inicio. Acentos y ñ se convierten a su letra base (á→A, ñ→N).</p>
</section>

<section class="card">
  <h2>2 · Escribe hasta 4 frases</h2>
  <label><input type="checkbox" id="todos" style="width:auto"> Escribir la frase 1 en los 6 lados</label>
  <div id="frases"></div>
  <button id="cifrar">Convertir a números</button>
  <div id="salida" class="out"></div>
  <button class="sec" id="copiarNum">Copiar números</button>
  <button class="sec" id="copiarLiga">Copiar liga para enviar</button>
  <p class="mu">La liga abre el mensaje una vez por dispositivo y después se borra de la dirección.</p>
</section>

<section class="card">
  <h2>3 · Ver el cubo</h2>
  <div class="escena" id="escena"><div class="cubo" id="cubo"></div></div>
  <button class="sec" id="vista">Ver desarrollo en cruz</button>
  <p class="mu">Gira el cubo con el dedo. Toca una cara para ver sus números abajo.</p>
  <div class="tabs" id="tabs"></div>
  <p class="legend"><span style="background:var(--hi)">casilla usada</span><span style="outline:2px solid var(--ok)">inicio</span><span style="outline:2px solid var(--bad)">final</span></p>
  <p id="marcas" class="mu"></p>
  <div class="gridwrap"><table id="grid"></table></div>
  <p id="celdaInfo" class="mu">Toca una casilla para ver sus letras.</p>
</section>

<section class="card">
  <h2>4 · Leer un mensaje</h2>
  <textarea id="entrada" placeholder="Pega aquí los números"></textarea>
  <button id="descifrar">Convertir a texto</button>
  <div id="texto" class="out"></div>
  <label>Recibir en el idioma:</label>
  <select id="idioma">
    <option value="es">Español</option><option value="en">English</option><option value="fr">Français</option>
    <option value="ru">Русский</option><option value="ar">العربية</option>
    <option value="zh-CN">中文 simplificado (mandarín)</option><option value="zh-TW">中文 tradicional</option>
    <option value="yue">粵語 cantonés (beta)</option><option value="pt">Português</option>
    <option value="de">Deutsch</option><option value="it">Italiano</option>
    <option value="lsm" disabled>Lengua de Señas Mexicana – Ensenada (beta, próximamente)</option>
  </select>
  <button class="sec" id="traducir">Traducir</button>
  <p class="mu">Idiomas oficiales de la ONU, lenguas regionales y LSM en desarrollo. Los caracteres chinos y otros no latinos se cifran en modo <span class="beta">beta</span>.</p>
</section>

<section class="card">
  <h2>Fondo educativo del Cubo de la Comunicación · Econotopía</h2>
  <p>Donativos voluntarios para servidores, mejoras, sugerencias, educación, viajes, propuestas, presentaciones, impresiones, módulos y libros.</p>
  <ul>
    <li>Todos los donativos y salidas son visibles en todo momento.</li>
    <li>Las salidas las solicita el administrador y requieren la aprobación de al menos 2 personas usuarias.</li>
  </ul>
  <p class="mu">Enlace bancario para donativos: próximamente.</p>
</section>

<section class="card">
  <h2>Acerca de Econotopía</h2>
  <p>Econotopía es el proyecto de Víctor Hugo Ramírez Salgado que reúne el modelo de comunicación del Cubo, su dimensión numérica, las letras, el diseño tecnológico y la programación. Su propósito central es ofrecer una herramienta para trasladar idiomas o crear una forma propia de comunicarse y aprender a nivel global. El fondo educativo se destina directamente al sistema del Cubo de la Comunicación.</p>
  <p><strong>En 3 líneas:</strong><br>
  Un cubo de 6 caras, 26 × 26 y 4056 casillas que convierte letras en números.<br>
  Cada persona elige su idioma y su alfabeto para comunicarse de forma propia y segura.<br>
  Un proyecto educativo y abierto, sostenido por donativos transparentes.</p>
</section>
</main>

<footer class="mu">© Víctor Hugo Ramírez Salgado · Econotopía · El Cubo de la Comunicación</footer>

<script>
const BASE='ABCDEFGHIJKLMNOPQRSTUVWXYZ';
const AUTOR='VICTOR HUGO RAMIREZ SALGADO';
let inicio=0, cara=1, usadas=[];
const $=id=>document.getElementById(id);
const alfa=()=>BASE.slice(inicio)+BASE.slice(0,inicio);
const norm=s=>s.normalize('NFD').replace(/[\u0300-\u036f]/g,'').toUpperCase();
const celda=(f,a,b)=>(f-1)*676+a*26+b+1;
const parte=n=>{n-=1;return{f:Math.floor(n/676)+1,r:Math.floor(n%676/26),c:n%26}};

function cifrar(texto,f){
  const A=alfa();
  return texto.trim().split(/\s+/).filter(Boolean).map(w=>{
    const out=[];let buf=[];
    const vaciar=()=>{for(let i=0;i<buf.length;i+=2){const a=buf[i],b=buf[i+1];
      out.push(b===undefined?celda(f,a,a)+'*':String(celda(f,a,b)));}buf=[];};
    for(const ch of w){
      const n=norm(ch);
      if(/[0-9]/.test(ch)){vaciar();out.push('['+ch+']');}
      else if(n&&[...n].every(c=>A.includes(c))){[...n].forEach(c=>buf.push(A.indexOf(c)));}
      else if(/\p{L}/u.test(ch)){vaciar();let x=ch.codePointAt(0),d=[];
        for(let k=0;k<4;k++){d.unshift(x%26);x=Math.floor(x/26);}
        out.push('^'+celda(f,d[0],d[1])+'-'+celda(f,d[2],d[3]));}
    }
    vaciar();return out.join(' ');
  }).join(' / ');
}

function descifrar(s){
  const A=alfa();
  return s.split('|').map(fr=>fr.trim().split(/\s*\/\s*/).map(w=>w.split(/\s+/).filter(Boolean).map(t=>{
    let m;
    if(m=t.match(/^\[(\d)\]$/))return m[1];
    if(m=t.match(/^\^(\d+)-(\d+)$/)){const p=parte(+m[1]),q=parte(+m[2]);
      return String.fromCodePoint(((p.r*26+p.c)*26+q.r)*26+q.c);}
    if(m=t.match(/^(\d+)(\*?)$/)){const n=+m[1];if(n<1||n>4056)return '?';
      const p=parte(n);return m[2]?A[p.r]:A[p.r]+A[p.c];}
    return '';
  }).join('')).join(' ')).join('\n');
}

function numeros(s){return (s.match(/\d+/g)||[]).map(Number).filter(n=>n>=1&&n<=4056);}

function verClave(){
  $('clave').textContent=[1,2,3,4,5,6].map(f=>cifrar(AUTOR,f)).join('  L  ');
}

function armarFrases(){
  let h='';for(let i=1;i<=4;i++){
    h+=`<div class="row"><textarea id="f${i}" placeholder="Frase ${i}"></textarea><select id="l${i}">`+
      [1,2,3,4,5,6].map(f=>`<option value="${f}"${f===i?' selected':''}>Lado ${f}</option>`).join('')+'</select></div>';}
  $('frases').innerHTML=h;
}

let mensaje='';
function convertir(){
  const partes=[],vista=[];
  if($('todos').checked){
    const t=$('f1').value;if(t.trim())for(let f=1;f<=6;f++){const c=cifrar(t,f);partes.push(c);vista.push('Lado '+f+': '+c);}
  }else for(let i=1;i<=4;i++){
    const t=$('f'+i).value,f=+$('l'+i).value;
    if(t.trim()){const c=cifrar(t,f);partes.push(c);vista.push('Lado '+f+': '+c);}
  }
  mensaje=partes.join(' | ');
  $('salida').textContent=vista.join('\n')||'Escribe al menos una frase.';
  marcar(mensaje);
}

function marcar(s){
  usadas=numeros(s.replace(/\[\d\]/g,''));
  if(usadas.length){const a=parte(usadas[0]),z=parte(usadas[usadas.length-1]),A=alfa();
    $('marcas').textContent=`Inicio: casilla ${usadas[0]} (lado ${a.f}, ${A[a.r]}${A[a.c]}) · Final: casilla ${usadas[usadas.length-1]} (lado ${z.f}, ${A[z.r]}${A[z.c]})`;
    cara=a.f;}
  else $('marcas').textContent='';
  tabs();grid();
}

function tabs(){
  $('tabs').innerHTML=[1,2,3,4,5,6].map(f=>`<button class="${f===cara?'on':''}" data-f="${f}">Lado ${f}</button>`).join('');
  $('tabs').querySelectorAll('button').forEach(b=>b.onclick=()=>{cara=+b.dataset.f;tabs();grid();});
}

function grid(){
  const A=alfa(),set=new Set(usadas),ini=usadas[0],fin=usadas[usadas.length-1];
  const cab='<tr><th></th>'+[...A].map(l=>`<th>${l}</th>`).join('')+'<th></th></tr>';
  let h=cab;
  for(let r=0;r<26;r++){
    h+=`<tr><th>${A[r]}</th>`;
    for(let c=0;c<26;c++){const n=celda(cara,r,c);
      let k=set.has(n)?'u':'';if(n===ini)k+=' ini';if(n===fin)k+=' fin';
      h+=`<td class="${k}" data-n="${n}">${n}</td>`;}
    h+=`<th>${A[r]}</th></tr>`;
  }
  $('grid').innerHTML=h+cab;
  dibujarCubo();
}

function dibujarCubo(){
  const cubo=$('cubo');if(!cubo)return;
  if(!cubo.children.length)for(let f=1;f<=6;f++){const d=document.createElement('div');
    d.className='cara c'+f;d.dataset.f=f;d.innerHTML='<canvas width="440" height="440"></canvas>';cubo.appendChild(d);}
  const A=alfa(),set=new Set(usadas),ini=usadas[0],fin=usadas[usadas.length-1];
  const st=getComputedStyle(document.documentElement),v=k=>st.getPropertyValue(k).trim();
  for(let f=1;f<=6;f++){
    const cv=cubo.querySelector('.c'+f+' canvas'),x=cv.getContext('2d'),S=440,c=S/28;
    x.fillStyle=v('--card');x.fillRect(0,0,S,S);
    x.fillStyle=v('--tx');x.font='bold '+(c*0.75)+'px -apple-system,sans-serif';x.textAlign='center';x.textBaseline='middle';
    for(let i=0;i<26;i++){const p=c*(i+1.5);
      x.fillText(A[i],p,c/2);x.fillText(A[i],p,S-c/2);x.fillText(A[i],c/2,p);x.fillText(A[i],S-c/2,p);}
    for(let r=0;r<26;r++)for(let k=0;k<26;k++){const n=celda(f,r,k),px=c*(k+1),py=c*(r+1);
      if(set.has(n)){x.fillStyle=n===ini?v('--ok'):n===fin?v('--bad'):'#f2b705';x.fillRect(px,py,c,c);}}
    x.strokeStyle=v('--ln');x.lineWidth=1;x.beginPath();
    for(let i=0;i<=26;i++){x.moveTo(c,c*(i+1));x.lineTo(S-c,c*(i+1));x.moveTo(c*(i+1),c);x.lineTo(c*(i+1),S-c);}
    x.stroke();
    x.globalAlpha=f===cara?.35:.18;x.fillStyle=v('--ac');x.font='bold 150px -apple-system,sans-serif';x.fillText(f,S/2,S/2+8);
    x.globalAlpha=1;
  }
}

let rx=-22,ry=35,arrastre=null,auto=true;
function girar(){const cubo=$('cubo');if(cubo)cubo.style.transform=`rotateX(${rx}deg) rotateY(${ry}deg)`;}
function animar(){if(auto&&!arrastre&&!$('escena').classList.contains('cruz')){ry+=0.25;girar();}requestAnimationFrame(animar);}
function elegirCara(f){cara=f;tabs();grid();$('grid').scrollIntoView({behavior:'smooth',block:'nearest'});}
$('escena').addEventListener('pointerdown',e=>{arrastre={x:e.clientX,y:e.clientY,rx,ry,mov:false};auto=false;});
window.addEventListener('pointermove',e=>{if(!arrastre||$('escena').classList.contains('cruz'))return;
  const dx=e.clientX-arrastre.x,dy=e.clientY-arrastre.y;if(Math.abs(dx)+Math.abs(dy)>6)arrastre.mov=true;
  ry=arrastre.ry+dx*0.5;rx=Math.max(-89,Math.min(89,arrastre.rx-dy*0.5));girar();});
window.addEventListener('pointerup',e=>{if(!arrastre)return;const mov=arrastre.mov;arrastre=null;
  if(!mov){const el=document.elementFromPoint(e.clientX,e.clientY),cd=el&&el.closest('.cara');if(cd)elegirCara(+cd.dataset.f);}});
$('vista').onclick=()=>{const es=$('escena').classList.toggle('cruz');
  $('vista').textContent=es?'Ver cubo en 3D':'Ver desarrollo en cruz';if(!es)girar();};

function copiar(t){
  if(navigator.clipboard)navigator.clipboard.writeText(t).then(()=>alert('Copiado'),()=>prompt('Copia:',t));
  else prompt('Copia:',t);
}

function liga(){
  if(!mensaje){alert('Primero convierte tus frases.');return;}
  const datos=btoa(JSON.stringify({s:inicio,m:mensaje,id:Date.now().toString(36)})).replace(/\+/g,'-').replace(/\//g,'_').replace(/=+$/,'');
  copiar(location.origin+location.pathname+'#m='+datos);
}

function recibir(){
  const m=location.hash.match(/^#m=(.+)$/);if(!m)return;
  history.replaceState(null,'',location.pathname);
  $('recibido').style.display='block';
  let d;try{d=JSON.parse(atob(m[1].replace(/-/g,'+').replace(/_/g,'/')));}catch(e){$('recTxt').textContent='Liga no válida.';return;}
  const llave='visto_'+d.id;let visto=false;
  try{visto=localStorage.getItem(llave)==='1';localStorage.setItem(llave,'1');}catch(e){}
  if(visto){$('recTxt').textContent='Este mensaje ya fue visto en este dispositivo.';return;}
  inicio=d.s|0;$('inicio').value=inicio;verClave();
  $('recTxt').textContent=descifrar(d.m);
  $('entrada').value=d.m;marcar(d.m);
}

$('inicio').innerHTML=[...BASE].map((l,i)=>`<option value="${i}">${l}</option>`).join('');
$('inicio').onchange=e=>{inicio=+e.target.value;verClave();grid();};
$('cifrar').onclick=convertir;
$('copiarNum').onclick=()=>mensaje?copiar(mensaje):alert('Primero convierte tus frases.');
$('copiarLiga').onclick=liga;
$('descifrar').onclick=()=>{const s=$('entrada').value;$('texto').textContent=descifrar(s);marcar(s);};
$('traducir').onclick=()=>{const t=$('texto').textContent.trim();if(!t){alert('Primero convierte los números a texto.');return;}
  window.open('https://translate.google.com/?sl=auto&tl='+$('idioma').value+'&text='+encodeURIComponent(t)+'&op=translate','_blank');};
$('grid').onclick=e=>{const n=+e.target.dataset.n;if(!n)return;const p=parte(n),A=alfa();
  $('celdaInfo').textContent=`Casilla ${n} · lado ${p.f} · fila ${A[p.r]} · columna ${A[p.c]} → “${A[p.r]}${A[p.c]}”`;};

armarFrases();verClave();tabs();grid();recibir();girar();animar();
</script>
</body>
</html>
# El Cubo de la Comunicación · Econotopía

**Autor:** Víctor Hugo Ramírez Salgado

Cubo de 6 caras de 26 × 26, con las letras A–Z en los cuatro bordes de cada cara y numeración secuencial del 1 al 4056. Cada par de letras ocupa una casilla numerada, lo que convierte cualquier texto en números y los números de vuelta en texto.

## Página

https://victorhugoramirezsalgado-boop.github.io/Econotop-a-cubo/

## Qué hace

- Escribe hasta 4 frases y elige en qué lado (1–6) va cada una, o una sola frase en los 6 lados.
- Cada persona elige la letra de inicio de su alfabeto como clave personal.
- Marca la casilla de inicio y la de final de cada mensaje.
- Genera una liga para enviar el mensaje, que se ve una sola vez por dispositivo.
- Lee mensajes en números y los traduce al idioma elegido: idiomas oficiales de la ONU, mandarín (simplificado y tradicional) y cantonés.
- En beta: Lengua de Señas Mexicana (variante de Ensenada, B.C.) y lenguas regionales.

## Econotopía

Econotopía reúne el modelo de comunicación del Cubo, su dimensión numérica, las letras, el diseño tecnológico y la programación. Es una herramienta para trasladar idiomas o crear una forma propia de comunicarse y aprender a nivel global.

**En 3 líneas:**
Un cubo de 6 caras, 26 × 26 y 4056 casillas que convierte letras en números.
Cada persona elige su idioma y su alfabeto para comunicarse de forma propia y segura.
Un proyecto educativo y abierto, sostenido por donativos transparentes.

## Fondo educativo del Cubo de la Comunicación · Econotopía

Donativos voluntarios para servidores, mejoras, educación, materiales y difusión. Todos los movimientos son públicos. Las salidas las solicita el administrador y requieren la aprobación de al menos 2 personas usuarias.

## Archivos

- `index.html`: la página completa (HTML, CSS y JavaScript en un solo archivo).

© Víctor Hugo Ramírez Salgado · Econotopía
