<html lang="es">
<head>
<meta charset="utf-8" />
<meta name="viewport" content="width=device-width,initial-scale=1" />
<title>Página sorpresa</title>
<style>
:root{--bg:#fff7f8;--accent:#e64a6b;--muted:#6b6b6b}
html,body{height:100%;margin:0;font-family:Inter, system-ui, -apple-system, 'Segoe UI', Roboto, 'Helvetica Neue', Arial}
.stage{height:100vh;display:flex;align-items:center;justify-content:center;background:linear-gradient(180deg,#fff 0%, #fff7f8 100%);overflow:hidden}

/* Intro */
.intro{position:relative;width:90%;max-width:760px;padding:40px;border-radius:18px;background:rgba(255,255,255,0.9);box-shadow:0 8px 30px rgba(0,0,0,0.08);text-align:center}
.heart-svg{width:180px;height:180px;margin:0 auto 20px;filter:drop-shadow(0 8px 20px rgba(230,74,107,0.18))}
h1{font-size:28px;margin:6px 0;color:var(--accent)}
p.lead{margin:0 0 18px;color:var(--muted)}
button.btn{background:var(--accent);color:white;border:0;padding:12px 20px;border-radius:12px;font-weight:600;cursor:pointer}

/* Code screen */
.code-area{margin-top:18px;display:none;gap:10px;justify-content:center;align-items:center}
.code-input{padding:12px 16px;border-radius:12px;border:2px solid rgba(0,0,0,0.06);font-size:16px;width:180px;text-align:center}
.hint{font-size:13px;color:#999;margin-top:10px}

/* Carousel */
.carousel-wrap{position:relative;width:100%;max-width:880px;margin:28px auto;display:none}
.carousel{overflow:hidden;border-radius:14px;height:220px;background:linear-gradient(90deg,#fff,#fff0f2)}
.track{display:flex;gap:16px;padding:18px;will-change:transform;animation:slide 12s linear infinite}
.card{min-width:260px;height:160px;border-radius:12px;display:flex;align-items:center;justify-content:center;font-weight:700;font-size:18px;user-select:none;cursor:pointer;box-shadow:0 6px 22px rgba(0,0,0,0.07);transition:transform .18s ease}
.card:active{transform:scale(.98)}

@keyframes slide{
  0%{transform:translateX(0)}
  33%{transform:translateX(-276px)}
  66%{transform:translateX(-552px)}
  100%{transform:translateX(0)}
}

/* squash animation */
.squash{animation:squash .45s ease forwards}
@keyframes squash{0%{transform:scale(1)}50%{transform:scale(1.05,0.75)}100%{transform:scale(1,1)}}

/* Slide to surprise */
.surprise{position:fixed;inset:0;background:linear-gradient(180deg,#fff7f8,#ffeef4);display:flex;align-items:center;justify-content:center;flex-direction:column;transform:translateY(110vh);transition:transform .7s cubic-bezier(.22,1,.36,1)}
.surprise.show{transform:translateY(0)}
.surprise .box{background:white;padding:28px;border-radius:18px;box-shadow:0 18px 50px rgba(230,74,107,0.12);text-align:center}
.surprise h2{color:var(--accent);margin:0 0 8px}
.surprise p{color:var(--muted);margin:0 0 12px}

/* small */
@media (max-width:600px){.track{padding:12px}.card{min-width:200px}}

/* Reproductor estilo dibujo debajo */
.player-dibujo {
  width:10cm;
  height:5cm;
  background:#fff0f2;
  border:3px dashed #e64a6b;
  border-radius:12px;
  display:flex;
  flex-direction:column;
  justify-content:center;
  align-items:center;
  box-shadow:0 6px 16px rgba(230,74,107,0.3);
  margin-top:15px;
}
.player-dibujo audio {
  width:90%;
  border-radius:8px;
}
.play-icon {
  width:30px;
  height:30px;
  margin-bottom:8px;
  clip-path: polygon(0% 0%, 100% 50%, 0% 100%);
  background:#e64a6b;
}

/* Buzón tarjeta carta */
.buzon-container { position: relative; width:300px; margin:20px auto; }
.buzon { width:100%; height:150px; background:#e64a6b; border-radius:12px; display:flex; justify-content:center; align-items:flex-end; cursor:pointer; position:relative; }
.tarjeta-cerrada { width:80px; height:50px; background:#fff0f2; border:2px dashed #fff; border-radius:6px; margin-bottom:10px; transition: transform 0.3s; }
.tarjeta-abierta { position:absolute; top:0; left:50%; transform:translateX(-50%) scale(0); width:320px; height:150px; display:flex; border-radius:12px; overflow:hidden; box-shadow:0 8px 20px rgba(0,0,0,0.2); transition:transform 0.5s; }
.tarjeta-abierta.show { transform:translateX(-50%) scale(1); }
.tarjeta-abierta .lado { width:50%; height:100%; }
.tarjeta-abierta .foto { background:#fff0f2; }
.tarjeta-abierta .foto img { width:100%; height:100%; object-fit:cover; }
.tarjeta-abierta .texto { background:#fff; display:flex; align-items:center; justify-content:center; padding:10px; font-size:14px; }
.tarjeta-abierta button { position:absolute; bottom:5px; right:5px; padding:4px 8px; background:#e64a6b; color:white; border:none; border-radius:6px; cursor:pointer; }

/* Botón volver */
.volver-btn {
  display:flex;
  align-items:center;
  gap:6px;
  background-color:#f8c8d8;
  color:#fff;
  border:none;
  padding:6px 12px;
  border-radius:8px;
  font-size:14px;
  cursor:pointer;
  margin:20px auto;
}
.volver-btn span { display:inline-block; transform:rotate(180deg); font-weight:bold; font-size:16px; }
</style>
</head>
<body>
<main class="stage">

<section class="intro" id="intro">
<img class="heart-svg" src="Snoppy.png" alt="Snoopy con corazón" />
<h1>Tienes un mensaje 💌</h1>
<p class="lead">Haz clic en abrir y sigue las pistas para ver la sorpresa.</p>

<div style="display:flex;gap:10px;justify-content:center;align-items:center;flex-direction:column">
  <button class="btn" id="openBtn">Abrir</button>
  <div class="code-area" id="codeArea">
    <input class="code-input" id="codeInput" placeholder="Ingresa el código" aria-label="Código" />
    <button class="btn" id="checkBtn">Enviar</button>
  </div>
  <div class="hint">Pista: Es una fecha muy importante para los dos.</div>
</div>

<div class="carousel-wrap" id="carouselWrap">
  <div class="carousel" aria-hidden="false">
    <div class="track" id="track">
      <div class="card" data-index="1" style="background:white;padding:10px"><img src="sonido.png" alt="sonido" style="max-width:100%;max-height:100%;object-fit:contain;border-radius:10px"></div>
      <div class="card" data-index="2" style="background:white;padding:10px"><img src="carta.png" alt="carta" style="max-width:100%;max-height:100%;object-fit:contain;border-radius:10px"></div>
    </div>
  </div>
</div>
</section>

<!-- Página sorpresa -->
<div class="surprise" id="surprise" style="display:none; flex-direction:column; align-items:center;">

<!-- Contenido Sonido -->
<div id="contenidoSonido" style="display:none;">
  <div style="display:flex; gap:15px; justify-content:center; align-items:stretch; flex-wrap:wrap; max-width:600px; margin:auto; position:relative; z-index:10;">
    <div class="box" style="width:45%; text-align:center;min-height:400px;">
      <img src="foto.png" alt="Imagen sorpresa" style="width:100%; max-height:400px; object-fit:cover; border-radius:12px;">
    </div>
    <div class="box" style="width:45%; text-align:center; min-height:400px;">
      <video src="tocadiscos.mp4" autoplay loop muted style="width:100%; height:400px; border-radius:12px; object-fit:cover;"></video>
    </div>
  </div>
  <div class="player-dibujo">
    <div class="play-icon"></div>
    <audio src="lala.mp3" controls></audio>
  </div>
</div>

<!-- Contenido Carta -->
<div id="contenidoCarta" style="display:none;">
  <div class="buzon-container">
    <div class="buzon" onclick="abrirTarjeta()">
      <div class="tarjeta-cerrada"></div>
    </div>
    <div class="tarjeta-abierta" id="tarjetaAbierta">
      <div class="lado foto">
        <img src="foto.png" alt="Foto" />
      </div>
      <div class="lado texto">
        <p>Este es el mensaje secreto de la tarjeta.</p>
      </div>
      <button onclick="cerrarTarjeta()">Cerrar</button>
    </div>
  </div>
</div>

<button class="volver-btn" onclick="regresar();"><span>&#10148;</span>Volver</button>

</div>
</main>

<script>
const SECRET_CODE = '23/11/2024';
const openBtn = document.getElementById('openBtn');
const codeArea = document.getElementById('codeArea');
const checkBtn = document.getElementById('checkBtn');
const codeInput = document.getElementById('codeInput');
const carouselWrap = document.getElementById('carouselWrap');
const track = document.getElementById('track');
const surprise = document.getElementById('surprise');
const backBtn = document.querySelector('.volver-btn');
const contenidoSonido = document.getElementById('contenidoSonido');
const contenidoCarta = document.getElementById('contenidoCarta');

openBtn.addEventListener('click', ()=>{
  openBtn.style.display='none';
  codeArea.style.display='flex';
  codeInput.focus();
});

checkBtn.addEventListener('click', ()=>{
  const val = (codeInput.value || '').trim().toUpperCase();
  if(val === SECRET_CODE.toUpperCase()){
    codeArea.style.display='none';
    carouselWrap.style.display='block';
    track.addEventListener('mouseenter', ()=> track.style.animationPlayState='paused');
    track.addEventListener('mouseleave', ()=> track.style.animationPlayState='running');
  } else {
    codeInput.classList.add('squash');
    setTimeout(()=> codeInput.classList.remove('squash'),400);
    codeInput.value='';
    codeInput.placeholder = 'Código incorrecto, inténtalo de nuevo';
  }
});

codeInput.addEventListener('keyup',(e)=>{ if(e.key==='Enter') checkBtn.click(); });

// Click en tarjetas
document.querySelectorAll('.card').forEach(card => {
  card.addEventListener('click', ()=>{
    const index = card.dataset.index;
    if(index=='1'){ // sonido
      contenidoSonido.style.display='block';
      contenidoCarta.style.display='none';
      carouselWrap.style.display='none';
      surprise.style.display='flex';
      surprise.classList.add('show');
      track.style.animationPlayState='paused';
    } else if(index=='2'){ // carta
      contenidoCarta.style.display='block';
      contenidoSonido.style.display='none';
      carouselWrap.style.display='none';
      surprise.style.display='flex';
      surprise.classList.add('show');
      track.style.animationPlayState='paused';
    }
  });
});

// Tarjeta carta
function abrirTarjeta() { document.getElementById('tarjetaAbierta').classList.add('show'); }
function cerrarTarjeta() { document.getElementById('tarjetaAbierta').classList.remove('show'); }

// Botón volver
function regresar(){
  contenidoSonido.style.display='none';
  contenidoCarta.style.display='none';
  surprise.style.display='none';
  carouselWrap.style.display='block';
  track.style.animationPlayState='running';
  setTimeout(()=>{carouselWrap.scrollIntoView({behavior:'smooth'});},50);
}
</script>
</body>
</html>
