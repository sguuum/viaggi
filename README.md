<html lang="it">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>I miei Viaggi</title>
<style>
  :root{
    --accent: #38bdf8;
    --text: #ffffff;
    --muted: rgba(255,255,255,0.8);
    --panel: rgba(0,0,0,0.25);
    --page-gray: #1f2937;
  }

  *{box-sizing:border-box;margin:0;padding:0}

  body {
    margin: 0;
    font-family: Arial, sans-serif;
    background-color: var(--page-gray);
    color: var(--text);
    position: relative;
    min-height:100vh;
  }

  body::before{
    content: "";
    position: fixed;
    inset: 0;
    z-index: 0;
    pointer-events: none;
    display: block;
    background:
      linear-gradient(rgba(0,0,0,0.72), rgba(0,0,0,0.72)),
      url("https://i.postimg.cc/nLyGVZ2b/Whats-App-Image-2026-01-22-at-14-06-48.jpg") no-repeat center center fixed;
    background-size: contain;
    background-position: center center;
  }

  .container {
    max-width: 1200px;
    margin: auto;
    padding: 24px;
    position: relative;
    z-index: 1;
  }

  header{
    text-align:center;
    margin-bottom:18px;
  }
  header h1{
    font-size:32px;
    letter-spacing:1.5px;
    text-shadow: 2px 2px 8px rgba(0,0,0,0.6);
  }
  header p{color:var(--muted);margin-top:8px}

  /* Bottoni / menu */
  .buttons {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(140px, 1fr));
    gap: 12px;
    margin: 18px 0 26px;
  }
  .buttons button {
    padding: 12px 18px;
    border: none;
    border-radius: 12px;
    background: rgba(255,255,255,0.08);
    color: var(--text);
    cursor: pointer;
    font-size: 15px;
    transition: 0.25s;
    box-shadow: 0 6px 14px rgba(0,0,0,0.35);
    border: 1px solid rgba(255,255,255,0.06);
  }
  .buttons button:hover{
    background: rgba(255,255,255,0.16);
    transform: translateY(-3px);
    border-color: rgba(255,255,255,0.12);
  }
  .buttons button.active{
    background: linear-gradient(135deg,var(--accent),#818cf8);
    color:#020617;
    border:none;
    box-shadow:0 10px 30px rgba(56,189,248,0.18);
  }

  /* Sezioni */
  .section {
    display: none;
    margin-top: 12px;
    padding: 18px;
    background: var(--panel);
    border-radius: 14px;
    box-shadow: 0 8px 20px rgba(0,0,0,0.45);
    border: 1px solid rgba(255,255,255,0.04);
  }
  .section.active { display:block }
  .section h2{margin-bottom:8px}
  .section p{color:var(--muted);margin-bottom:14px}

  /* Griglia immagini */
  .gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
    gap: 14px;
  }
  .gallery img {
    width:100%;
    height:200px;
    object-fit:cover;
    border-radius:10px;
    cursor:pointer;
    transition: transform .25s, box-shadow .25s, border-color .25s;
    border: 3px solid rgba(255,255,255,0.12);
  }
  .gallery img:hover{
    transform: scale(1.04);
    box-shadow: 0 18px 40px rgba(0,0,0,0.6);
    border-color: rgba(255,255,255,0.28);
  }

  /* Bottone torna ai viaggi */
  .back {
    display: inline-block;
    margin: 18px auto 0;
    padding: 10px 18px;
    border-radius: 12px;
    background: rgba(255,255,255,0.08);
    color: var(--text);
    border: none;
    cursor: pointer;
    font-size: 15px;
    transition: .2s;
    box-shadow: 0 6px 14px rgba(0,0,0,0.35);
  }
  .back:hover{ background: rgba(255,255,255,0.16) }

/* Modal zoom aggiornato */
.modal {
  display: none;
  position: fixed;
  z-index: 100;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.88);
  justify-content: center;
  align-items: center;
  overflow: hidden;
}

.modal img {
  max-width: 92%;
  max-height: 92%;
  border-radius: 12px;
  box-shadow: 0 20px 60px rgba(0,0,0,0.7);
  transition: transform 0.3s ease;
  touch-action: pinch-zoom; /* abilita pinch su mobile */
  cursor: grab;
}

.modal img:active {
  cursor: grabbing;
}

.modal .close {
  position: absolute;
  top: 20px;
  right: 30px;
  font-size: 30px;
  color: #fff;
  cursor: pointer;
}

  .modal .close {
    position: absolute;
    top: 20px;
    right: 30px;
    font-size: 30px;
    color: #fff;
    cursor: pointer;
  }

  /* Responsive tweaks */
  @media (max-width:600px){
    .gallery img{height:160px}
    header h1{font-size:24px}
    .buttons {
      grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
    }
    .buttons button {
      font-size: 14px;
      padding: 12px 10px;
    }
  }
</style>
</head>
<body>
<div class="container">
  <header>
    <h1>I miei Viaggi</h1>
    <p>Galleria fotografica personale — ordinata per anno</p>
  </header>

  <!-- MENU -->
  <div class="buttons">
    <button data-target="sardegna">Sardegna 2025</button>
    <button data-target="verdon">Verdon – Francia 2025</button>
    <button data-target="toscana">Toscana 2025</button>
    <button data-target="marocco2024">Marocco 2024</button>
    <button data-target="malta">Malta 2023</button>
    <button data-target="polonia">Polonia 2022</button>
    <button data-target="barcellona">Barcellona 2022</button>
    <button data-target="messico">Cuba – Messico 2019</button>
    <button data-target="usa">USA 2017</button>
    <button data-target="marocco">Marocco 2010</button>
    <button data-target="tunisia">Tunisia 2008</button>
  </div>

  <!-- SEZIONI -->
  <div id="sardegna" class="section">
    <h2>Sardegna 2025</h2>
    <p>In attesa delle foto.</p>
    <div class="gallery"></div>
    <div style="text-align:center"><button class="back">TORNA AI VIAGGI</button></div>
  </div>

  <div id="verdon" class="section">
    <h2>Verdon – Francia 2025</h2>
    <p>In attesa delle foto.</p>
    <div class="gallery"></div>
    <div style="text-align:center"><button class="back">TORNA AI VIAGGI</button></div>
  </div>

  <div id="toscana" class="section">
    <h2>Toscana 2025</h2>
    <p>In attesa delle foto.</p>
    <div class="gallery"></div>
    <div style="text-align:center"><button class="back">TORNA AI VIAGGI</button></div>
  </div>

  <div id="marocco2024" class="section">
    <h2>Marocco 2024</h2>
    <p>In attesa delle foto.</p>
    <div class="gallery"></div>
    <div style="text-align:center"><button class="back">TORNA AI VIAGGI</button></div>
  </div>

  <div id="malta" class="section">
    <h2>Malta 2023</h2>
    <div class="gallery">
      <img src="https://i.postimg.cc/2jL3WnBY/Whats-App-Image-2026-02-02-at-08-23-05.jpg" alt="">
      <img src="https://i.postimg.cc/G3T9Dvsr/Whats-App-Image-2026-02-02-at-08-23-05-(1).jpg" alt="">
      <img src="https://i.postimg.cc/BbF6GGGQ/Whats-App-Image-2026-02-02-at-08-23-05-(2).jpg" alt="">
      <img src="https://i.postimg.cc/ryRz45t6/Whats-App-Image-2026-02-02-at-08-23-05-(3).jpg" alt="">
    </div>
    <div style="text-align:center"><button class="back">TORNA AI VIAGGI</button></div>
  </div>

  <div id="polonia" class="section">
    <h2>Polonia 2022</h2>
    <p>In attesa delle foto.</p>
    <div class="gallery"></div>
    <div style="text-align:center"><button class="back">TORNA AI VIAGGI</button></div>
  </div>

  <div id="barcellona" class="section">
    <h2>Barcellona 2022</h2>
    <p>In attesa delle foto.</p>
    <div class="gallery"></div>
    <div style="text-align:center"><button class="back">TORNA AI VIAGGI</button></div>
  </div>

  <div id="messico" class="section">
    <h2>Cuba – Messico 2019</h2>
    <p>Colori, musica e spiagge.</p>
    <div class="gallery">
      <img src="https://i.postimg.cc/X7NyZY1T/Whats-App-Image-2026-01-26-at-09-46-26.jpg" alt="">
      <img src="https://i.postimg.cc/28HLnNPN/Whats-App-Image-2026-01-26-at-09-46-27.jpg" alt="">
      <img src="https://i.postimg.cc/7YPTCZQk/Whats-App-Image-2026-01-26-at-09-46-27-(1).jpg" alt="">
      <img src="https://i.postimg.cc/qMm62H9T/Whats-App-Image-2026-01-26-at-09-46-27-(2).jpg" alt="">
      <img src="https://i.postimg.cc/gkML3bfm/Whats-App-Image-2026-01-26-at-09-46-28.jpg" alt="">
      <img src="https://i.postimg.cc/jd8nyYGx/Whats-App-Image-2026-01-26-at-09-46-28-(1).jpg" alt="">
      <img src="https://i.postimg.cc/VL70XP3n/Whats-App-Image-2026-01-26-at-09-46-28-(2).jpg" alt="">
      <img src="https://i.postimg.cc/Kv93thd3/Whats-App-Image-2026-01-26-at-09-46-29.jpg" alt="">
      <img src="https://i.postimg.cc/jd8nyYG7/Whats-App-Image-2026-01-26-at-09-46-29-(1).jpg" alt="">
      <img src="https://i.postimg.cc/T3pL9H6t/Whats-App-Image-2026-01-26-at-09-46-30.jpg" alt="">
      <img src="https://i.postimg.cc/4xm75Fgv/Whats-App-Image-2026-01-26-at-09-46-30-(1).jpg" alt="">
      <img src="https://i.postimg.cc/6py201X8/Whats-App-Image-2026-01-26-at-09-46-30-(2).jpg" alt="">
      <img src="https://i.postimg.cc/9QrRpNhb/Whats-App-Image-2026-01-26-at-09-46-30-(3).jpg" alt="">
    </div>
    <div style="text-align:center"><button class="back">TORNA AI VIAGGI</button></div>
  </div>

  <div id="usa" class="section">
    <h2>USA 2017</h2>
    <p>Metropoli e grandi spazi.</p>
    <div class="gallery">
      <img src="https://i.postimg.cc/Zqtgc2dH/Whats-App-Image-2026-01-26-at-09-46-22.jpg" alt="">
      <img src="https://i.postimg.cc/X7PtZp7r/Whats-App-Image-2026-01-26-at-09-46-22-(1).jpg" alt="">
      <img src="https://i.postimg.cc/K8gwtxRB/Whats-App-Image-2026-01-26-at-09-46-22-(2).jpg" alt="">
      <img src="https://i.postimg.cc/DwbH1n8G/Whats-App-Image-2026-01-26-at-09-46-23.jpg" alt="">
      <img src="https://i.postimg.cc/VkbpXmd0/Whats-App-Image-2026-01-26-at-09-46-23-(1).jpg" alt="">
      <img src="https://i.postimg.cc/7ZTdSwfg/Whats-App-Image-2026-01-26-at-09-46-23-(2).jpg" alt="">
      <img src="https://i.postimg.cc/GmsVvdHz/Whats-App-Image-2026-01-26-at-09-46-23-(3).jpg" alt="">
      <img src="https://i.postimg.cc/3xDV2Ydq/Whats-App-Image-2026-01-26-at-09-46-24.jpg" alt="">
    </div>
    <div style="text-align:center"><button class="back">TORNA AI VIAGGI</button></div>
  </div>

  <div id="marocco" class="section">
    <h2>Marocco 2010</h2>
    <p>Deserti e città storiche.</p>
    <div class="gallery">
      <img src="https://i.postimg.cc/R0YWy1MF/Whats-App-Image-2026-01-26-at-09-46-25.jpg" alt="">
      <img src="https://i.postimg.cc/FRJY4fRs/Whats-App-Image-2026-01-26-at-09-46-25-(1).jpg" alt="">
      <img src="https://i.postimg.cc/vB64s1B8/Whats-App-Image-2026-01-26-at-09-46-25-(2).jpg" alt="">
      <img src="https://i.postimg.cc/hj7XBJjS/Whats-App-Image-2026-01-26-at-09-46-25-(3).jpg" alt="">
      <img src="https://i.postimg.cc/gJ6xWwJ0/Whats-App-Image-2026-01-26-at-09-46-25-(4).jpg" alt="">
      <img src="https://i.postimg.cc/ydSDHJdd/Whats-App-Image-2026-01-26-at-09-46-26.jpg" alt="">
      <img src="https://i.postimg.cc/bJ2ZhGJG/Whats-App-Image-2026-01-26-at-09-46-26-(1).jpg" alt="">
      <img src="https://i.postimg.cc/26B1Dq6y/Whats-App-Image-2026-01-26-at-09-46-26-(2).jpg" alt="">
    </div>
    <div style="text-align:center"><button class="back">TORNA AI VIAGGI</button></div>
  </div>

  <div id="tunisia" class="section">
    <h2>Tunisia 2008</h2>
    <p>Mare e storia.</p>
    <div class="gallery">
      <img src="https://i.postimg.cc/Y2xkFzVW/Whats-App-Image-2026-01-22-at-14-46-09.jpg" alt="">
      <img src="https://i.postimg.cc/0ybvQqkq/Whats-App-Image-2026-01-26-at-09-46-19.jpg" 
      <img src="https://i.postimg.cc/0ybvQqky/Whats-App-Image-2026-01-26-at-09-46-20.jpg" alt="">
      <img src="https://i.postimg.cc/4xmGdTfX/Whats-App-Image-2026-01-26-at-09-46-20-(1).jpg" alt="">
      <img src="https://i.postimg.cc/g2npJPzJ/Whats-App-Image-2026-01-26-at-09-46-21.jpg" alt="">
      <img src="https://i.postimg.cc/QdHDtr8N/Whats-App-Image-2026-01-26-at-09-46-21-(1).jpg" alt="">
      <img src="https://i.postimg.cc/BnX36GSq/Whats-App-Image-2026-01-26-at-09-46-21-(2).jpg" alt="">
      <img src="https://i.postimg.cc/P5PHxkXq/Whats-App-Image-2026-01-26-at-09-46-21-(3).jpg" alt="">
    </div>
    <div style="text-align:center"><button class="back">TORNA AI VIAGGI</button></div>
  </div>

</div>

<!-- MODAL -->
<div class="modal" id="modal">
  <div class="close" id="closeModal">&times;</div>
  <img id="modalImg" src="" alt="Zoom immagine">
</div>

<script>
  // MENU: mostra sezione corrispondente e scrolla
  const buttons = document.querySelectorAll('.buttons button');
  const sections = document.querySelectorAll('.section');

  function resetSections(){
    sections.forEach(s => s.classList.remove('active'));
    buttons.forEach(b => b.classList.remove('active'));
  }

  buttons.forEach(btn => {
    btn.addEventListener('click', () => {
      resetSections();
      const id = btn.dataset.target;
      const sec = document.getElementById(id);
      if(sec) {
        sec.classList.add('active');
        sec.scrollIntoView({behavior: 'smooth', block: 'start'});
      }
      btn.classList.add('active');
    });
  });

  // Bottone torna ai viaggi
  const backButtons = document.querySelectorAll('.back');
  backButtons.forEach(back => {
    back.addEventListener('click', () => {
      resetSections();
      window.scrollTo({top:0,behavior:'smooth'});
    });
  });


 // Modal zoom con drag e pinch
const modal = document.getElementById('modal');
const modalImg = document.getElementById('modalImg');
const closeModal = document.getElementById('closeModal');

let scale = 1, originX = 0, originY = 0;
let startX = 0, startY = 0, isDragging = false;

// Apri modal
document.addEventListener('click', (e) => {
  if(e.target.matches('.gallery img')){
    modal.style.display = 'flex';
    modalImg.src = e.target.src;
    scale = 1;
    originX = 0;
    originY = 0;
    modalImg.style.transform = `scale(${scale}) translate(0px,0px)`;
  }
});

// Chiudi modal
closeModal.addEventListener('click', () => modal.style.display = 'none');
modal.addEventListener('click', (e) => { if(e.target === modal) modal.style.display = 'none'; });

// Zoom con mouse wheel su PC
modalImg.addEventListener('wheel', (e) => {
  e.preventDefault();
  const delta = e.deltaY > 0 ? -0.1 : 0.1;
  scale = Math.min(Math.max(1, scale + delta), 5);
  modalImg.style.transform = `scale(${scale}) translate(${originX}px, ${originY}px)`;
});

// Drag immagine
modalImg.addEventListener('mousedown', (e) => {
  e.preventDefault();
  isDragging = true;
  startX = e.clientX - originX;
  startY = e.clientY - originY;
});
window.addEventListener('mouseup', () => isDragging = false);
window.addEventListener('mousemove', (e) => {
  if(!isDragging) return;
  originX = e.clientX - startX;
  originY = e.clientY - startY;
  modalImg.style.transform = `scale(${scale}) translate(${originX}px, ${originY}px)`;
});

// Zoom touch su mobile (pinch)
let initialDistance = 0;
modalImg.addEventListener('touchstart', (e) => {
  if(e.touches.length === 2){
    initialDistance = Math.hypot(
      e.touches[0].clientX - e.touches[1].clientX,
      e.touches[0].clientY - e.touches[1].clientY
    );
  }
});

modalImg.addEventListener('touchmove', (e) => {
  if(e.touches.length === 2){
    const newDistance = Math.hypot(
      e.touches[0].clientX - e.touches[1].clientX,
      e.touches[0].clientY - e.touches[1].clientY
    );
    const delta = (newDistance - initialDistance) / 200;
    scale = Math.min(Math.max(1, scale + delta), 5);
    modalImg.style.transform = `scale(${scale}) translate(${originX}px, ${originY}px)`;
    initialDistance = newDistance;
  }
});


  // Facoltativo: apri prima sezione di default
  // buttons[0]?.click();
</script>
</body>
</html>

