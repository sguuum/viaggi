<html lang="it">
<head>
  <meta charset="UTF-8" />
  <!-- Apertura “giusta” su mobile (come ora ti va bene) -->
  <meta name="viewport" content="width=device-width, initial-scale=1, minimum-scale=1, maximum-scale=1, viewport-fit=cover" />
  <title>I miei Viaggi</title>

  <style>
    :root{
      --accent: #38bdf8;
      --text: #ffffff;
      --muted: rgba(255,255,255,0.82);

      --panel: rgba(0,0,0,0.30);
      --panel2: rgba(0,0,0,0.40);
      --border: rgba(255,255,255,0.08);

      --page: #1f2937;
    }

    *{box-sizing:border-box;margin:0;padding:0}
    html,body{height:100%}

    /* evita “auto zoom” testo nei browser interni */
    html{
      -webkit-text-size-adjust: 100%;
      text-size-adjust: 100%;
    }

    body{
      font-family: Arial, sans-serif;
      background: var(--page);
      color: var(--text);
      min-height:100vh;
      overflow-x:hidden;
      font-size: 18px; /* base buona (mobile ok) */
    }

    /* Sfondo ben visibile come nel tuo originale */
    body::before{
      content:"";
      position: fixed;
      inset: 0;
      z-index: 0;
      pointer-events: none;
      background:
        linear-gradient(rgba(0,0,0,0.62), rgba(0,0,0,0.62)),
        url("https://i.postimg.cc/nLyGVZ2b/Whats-App-Image-2026-01-22-at-14-06-48.jpg") no-repeat center center fixed;
      background-size: contain;
      background-position: center center;
      transform: translateZ(0);
    }

    /* Container: su PC deve riempire (niente “cornice piccola”) */
    .container{
      width: min(1680px, 96vw);
      margin: 0 auto;
      padding: 28px;
      position: relative;
      z-index: 1;
    }

    /* Header più “bello” ma sempre dark */
    header{
      text-align:center;
      margin-bottom: 18px;
      padding: 18px 14px;
      background: linear-gradient(180deg, rgba(0,0,0,0.22), rgba(0,0,0,0.12));
      border: 1px solid var(--border);
      border-radius: 16px;
      backdrop-filter: blur(4px);
      box-shadow: 0 10px 26px rgba(0,0,0,0.35);
    }
    header h1{
      font-size: 44px; /* PC bello grande */
      letter-spacing: 1.6px;
      text-shadow: 2px 2px 12px rgba(0,0,0,0.75);
    }
    header p{
      margin-top: 10px;
      color: var(--muted);
      font-size: 1.05rem;
    }

    /* MENU */
    .buttons{
      display:grid;
      grid-template-columns: repeat(auto-fit, minmax(210px, 1fr));
      gap: 12px;
      margin: 18px 0 26px;
    }

    .buttons button{
      padding: 14px 16px;
      border-radius: 14px;
      border: 1px solid var(--border);
      background: rgba(255,255,255,0.08);
      color: var(--text);
      cursor:pointer;

      font-size: 1.02rem;
      font-weight: 700;
      letter-spacing: 0.2px;

      transition: transform .18s ease, background .18s ease, box-shadow .18s ease, border-color .18s ease;
      box-shadow: 0 8px 18px rgba(0,0,0,0.35);
    }

    .buttons button:hover{
      background: rgba(255,255,255,0.14);
      transform: translateY(-2px);
      border-color: rgba(255,255,255,0.14);
      box-shadow: 0 12px 26px rgba(0,0,0,0.42);
    }

    .buttons button.active{
      background: linear-gradient(135deg, var(--accent), #818cf8);
      color: #061018;
      border: none;
      box-shadow: 0 14px 34px rgba(56,189,248,0.18);
    }

    /* SEZIONI */
    .section{
      display:none;
      margin-top: 12px;
      padding: 20px;
      background: var(--panel);
      border-radius: 16px;
      border: 1px solid var(--border);
      box-shadow: 0 12px 28px rgba(0,0,0,0.45);
      backdrop-filter: blur(4px);
    }
    .section.active{display:block}

    .section h2{
      margin-bottom: 8px;
      font-size: 1.55rem;
      text-shadow: 1px 1px 10px rgba(0,0,0,0.55);
    }
    .section p{
      color: var(--muted);
      margin-bottom: 14px;
      font-size: 1.05rem;
    }

    /* GALLERY */
    .gallery{
      display:grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 14px;
    }
    .gallery img{
      width:100%;
      height: 260px;       /* su PC più “piena” e bella */
      object-fit: cover;
      border-radius: 12px;
      cursor:pointer;
      border: 3px solid rgba(255,255,255,0.12);
      box-shadow: 0 14px 32px rgba(0,0,0,0.55);
      transition: transform .18s ease, box-shadow .18s ease, border-color .18s ease;
      background: rgba(255,255,255,0.06);
    }
    .gallery img:hover{
      transform: scale(1.025);
      box-shadow: 0 20px 46px rgba(0,0,0,0.65);
      border-color: rgba(255,255,255,0.28);
    }

    /* BACK */
    .back{
      display:inline-block;
      margin: 18px auto 0;
      padding: 12px 18px;
      border-radius: 14px;
      background: rgba(255,255,255,0.10);
      color: var(--text);
      border: 1px solid rgba(255,255,255,0.10);
      cursor:pointer;
      font-size: 1.02rem;
      font-weight: 800;
      letter-spacing: 0.4px;
      transition: transform .16s ease, background .16s ease;
      box-shadow: 0 10px 22px rgba(0,0,0,0.38);
    }
    .back:hover{
      background: rgba(255,255,255,0.16);
      transform: translateY(-1px);
    }

    /* MODAL */
    .modal{
      display:none;
      position:fixed;
      inset:0;
      z-index:1000;
      background: rgba(0,0,0,0.88);
      justify-content:center;
      align-items:center;
      overflow:hidden;
      padding: 14px;
    }
    .modal.open{display:flex}

    .modal .close{
      position:absolute;
      top: 16px;
      right: 18px;
      font-size: 34px;
      color:#fff;
      cursor:pointer;
      padding: 8px 12px;
      border-radius: 14px;
      background: rgba(255,255,255,0.10);
      border: 1px solid rgba(255,255,255,0.14);
      user-select:none;
    }

    .modal img{
      max-width: 92%;
      max-height: 92%;
      border-radius: 14px;
      box-shadow: 0 24px 80px rgba(0,0,0,0.75);
      transition: transform 0.18s ease;
      touch-action: pinch-zoom;
      cursor: grab;
      user-select:none;
      -webkit-user-drag:none;
      transform: translate3d(0,0,0) scale(1);
    }
    .modal img:active{cursor:grabbing}

    /* ======== RESPONSIVE ======== */

    /* Tablet */
    @media (max-width: 900px){
      .container{ width: 96vw; padding: 18px; }
      header h1{ font-size: 34px; }
      .buttons{ grid-template-columns: repeat(auto-fit, minmax(180px, 1fr)); }
      .gallery{ grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); }
      .gallery img{ height: 220px; }
    }

    /* Telefono (ti deve restare come ora “giusto”) */
    @media (max-width: 600px){
      body{ font-size: 18px; }
      .container{ width: 96vw; padding: 16px; }
      header{ padding: 16px 12px; }
      header h1{ font-size: 28px; }
      header p{ font-size: 1rem; }

      .buttons{
        grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
      }
      .buttons button{
        padding: 12px 10px;
        font-size: 1rem;
      }

      .section{ padding: 18px; }
      .gallery img{ height: 200px; }
    }

    @media (prefers-reduced-motion: reduce){
      *{ transition:none !important; scroll-behavior:auto !important; }
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
      <div style="text-align:center"><button class="back" type="button">TORNA AI VIAGGI</button></div>
    </div>

    <div id="verdon" class="section">
      <h2>Verdon – Francia 2025</h2>
      <p>In attesa delle foto.</p>
      <div class="gallery"></div>
      <div style="text-align:center"><button class="back" type="button">TORNA AI VIAGGI</button></div>
    </div>

    <div id="toscana" class="section">
      <h2>Toscana 2025</h2>
      <p>In attesa delle foto.</p>
      <div class="gallery"></div>
      <div style="text-align:center"><button class="back" type="button">TORNA AI VIAGGI</button></div>
    </div>

    <div id="marocco2024" class="section">
      <h2>Marocco 2024</h2>
      <p>In attesa delle foto.</p>
      <div class="gallery"></div>
      <div style="text-align:center"><button class="back" type="button">TORNA AI VIAGGI</button></div>
    </div>

    <div id="malta" class="section">
      <h2>Malta 2023</h2>
      <div class="gallery">
        <img loading="lazy" src="https://i.postimg.cc/2jL3WnBY/Whats-App-Image-2026-02-02-at-08-23-05.jpg" alt="Malta 2023 - 1">
        <img loading="lazy" src="https://i.postimg.cc/G3T9Dvsr/Whats-App-Image-2026-02-02-at-08-23-05-(1).jpg" alt="Malta 2023 - 2">
        <img loading="lazy" src="https://i.postimg.cc/BbF6GGGQ/Whats-App-Image-2026-02-02-at-08-23-05-(2).jpg" alt="Malta 2023 - 3">
        <img loading="lazy" src="https://i.postimg.cc/ryRz45t6/Whats-App-Image-2026-02-02-at-08-23-05-(3).jpg" alt="Malta 2023 - 4">
      </div>
      <div style="text-align:center"><button class="back" type="button">TORNA AI VIAGGI</button></div>
    </div>

    <div id="polonia" class="section">
      <h2>Polonia 2022</h2>
      <p>In attesa delle foto.</p>
      <div class="gallery"></div>
      <div style="text-align:center"><button class="back" type="button">TORNA AI VIAGGI</button></div>
    </div>

    <div id="barcellona" class="section">
      <h2>Barcellona 2022</h2>
      <p>In attesa delle foto.</p>
      <div class="gallery"></div>
      <div style="text-align:center"><button class="back" type="button">TORNA AI VIAGGI</button></div>
    </div>

    <div id="messico" class="section">
      <h2>Cuba – Messico 2019</h2>
      <p>Colori, musica e spiagge.</p>
      <div class="gallery">
        <img loading="lazy" src="https://i.postimg.cc/X7NyZY1T/Whats-App-Image-2026-01-26-at-09-46-26.jpg" alt="Cuba Messico 2019 - 1">
        <img loading="lazy" src="https://i.postimg.cc/28HLnNPN/Whats-App-Image-2026-01-26-at-09-46-27.jpg" alt="Cuba Messico 2019 - 2">
        <img loading="lazy" src="https://i.postimg.cc/7YPTCZQk/Whats-App-Image-2026-01-26-at-09-46-27-(1).jpg" alt="Cuba Messico 2019 - 3">
        <img loading="lazy" src="https://i.postimg.cc/qMm62H9T/Whats-App-Image-2026-01-26-at-09-46-27-(2).jpg" alt="Cuba Messico 2019 - 4">
        <img loading="lazy" src="https://i.postimg.cc/gkML3bfm/Whats-App-Image-2026-01-26-at-09-46-28.jpg" alt="Cuba Messico 2019 - 5">
        <img loading="lazy" src="https://i.postimg.cc/jd8nyYGx/Whats-App-Image-2026-01-26-at-09-46-28-(1).jpg" alt="Cuba Messico 2019 - 6">
        <img loading="lazy" src="https://i.postimg.cc/VL70XP3n/Whats-App-Image-2026-01-26-at-09-46-28-(2).jpg" alt="Cuba Messico 2019 - 7">
        <img loading="lazy" src="https://i.postimg.cc/Kv93thd3/Whats-App-Image-2026-01-26-at-09-46-29.jpg" alt="Cuba Messico 2019 - 8">
        <img loading="lazy" src="https://i.postimg.cc/jd8nyYG7/Whats-App-Image-2026-01-26-at-09-46-29-(1).jpg" alt="Cuba Messico 2019 - 9">
        <img loading="lazy" src="https://i.postimg.cc/T3pL9H6t/Whats-App-Image-2026-01-26-at-09-46-30.jpg" alt="Cuba Messico 2019 - 10">
        <img loading="lazy" src="https://i.postimg.cc/4xm75Fgv/Whats-App-Image-2026-01-26-at-09-46-30-(1).jpg" alt="Cuba Messico 2019 - 11">
        <img loading="lazy" src="https://i.postimg.cc/6py201X8/Whats-App-Image-2026-01-26-at-09-46-30-(2).jpg" alt="Cuba Messico 2019 - 12">
        <img loading="lazy" src="https://i.postimg.cc/9QrRpNhb/Whats-App-Image-2026-01-26-at-09-46-30-(3).jpg" alt="Cuba Messico 2019 - 13">
      </div>
      <div style="text-align:center"><button class="back" type="button">TORNA AI VIAGGI</button></div>
    </div>

    <div id="usa" class="section">
      <h2>USA 2017</h2>
      <p>Metropoli e grandi spazi.</p>
      <div class="gallery">
        <img loading="lazy" src="https://i.postimg.cc/Zqtgc2dH/Whats-App-Image-2026-01-26-at-09-46-22.jpg" alt="USA 2017 - 1">
        <img loading="lazy" src="https://i.postimg.cc/X7PtZp7r/Whats-App-Image-2026-01-26-at-09-46-22-(1).jpg" alt="USA 2017 - 2">
        <img loading="lazy" src="https://i.postimg.cc/K8gwtxRB/Whats-App-Image-2026-01-26-at-09-46-22-(2).jpg" alt="USA 2017 - 3">
        <img loading="lazy" src="https://i.postimg.cc/DwbH1n8G/Whats-App-Image-2026-01-26-at-09-46-23.jpg" alt="USA 2017 - 4">
        <img loading="lazy" src="https://i.postimg.cc/VkbpXmd0/Whats-App-Image-2026-01-26-at-09-46-23-(1).jpg" alt="USA 2017 - 5">
        <img loading="lazy" src="https://i.postimg.cc/7ZTdSwfg/Whats-App-Image-2026-01-26-at-09-46-23-(2).jpg" alt="USA 2017 - 6">
        <img loading="lazy" src="https://i.postimg.cc/GmsVvdHz/Whats-App-Image-2026-01-26-at-09-46-23-(3).jpg" alt="USA 2017 - 7">
        <img loading="lazy" src="https://i.postimg.cc/3xDV2Ydq/Whats-App-Image-2026-01-26-at-09-46-24.jpg" alt="USA 2017 - 8">
      </div>
      <div style="text-align:center"><button class="back" type="button">TORNA AI VIAGGI</button></div>
    </div>

    <div id="marocco" class="section">
      <h2>Marocco 2010</h2>
      <p>Deserti e città storiche.</p>
      <div class="gallery">
        <img loading="lazy" src="https://i.postimg.cc/R0YWy1MF/Whats-App-Image-2026-01-26-at-09-46-25.jpg" alt="Marocco 2010 - 1">
        <img loading="lazy" src="https://i.postimg.cc/FRJY4fRs/Whats-App-Image-2026-01-26-at-09-46-25-(1).jpg" alt="Marocco 2010 - 2">
        <img loading="lazy" src="https://i.postimg.cc/vB64s1B8/Whats-App-Image-2026-01-26-at-09-46-25-(2).jpg" alt="Marocco 2010 - 3">
        <img loading="lazy" src="https://i.postimg.cc/hj7XBJjS/Whats-App-Image-2026-01-26-at-09-46-25-(3).jpg" alt="Marocco 2010 - 4">
        <img loading="lazy" src="https://i.postimg.cc/gJ6xWwJ0/Whats-App-Image-2026-01-26-at-09-46-25-(4).jpg" alt="Marocco 2010 - 5">
        <img loading="lazy" src="https://i.postimg.cc/ydSDHJdd/Whats-App-Image-2026-01-26-at-09-46-26.jpg" alt="Marocco 2010 - 6">
        <img loading="lazy" src="https://i.postimg.cc/bJ2ZhGJG/Whats-App-Image-2026-01-26-at-09-46-26-(1).jpg" alt="Marocco 2010 - 7">
        <img loading="lazy" src="https://i.postimg.cc/26B1Dq6y/Whats-App-Image-2026-01-26-at-09-46-26-(2).jpg" alt="Marocco 2010 - 8">
      </div>
      <div style="text-align:center"><button class="back" type="button">TORNA AI VIAGGI</button></div>
    </div>

    <div id="tunisia" class="section">
      <h2>Tunisia 2008</h2>
      <p>Mare e storia.</p>
      <div class="gallery">
        <img loading="lazy" src="https://i.postimg.cc/Y2xkFzVW/Whats-App-Image-2026-01-22-at-14-46-09.jpg" alt="Tunisia 2008 - 1">
        <img loading="lazy" src="https://i.postimg.cc/0ybvQqkq/Whats-App-Image-2026-01-26-at-09-46-19.jpg" alt="Tunisia 2008 - 2">
        <img loading="lazy" src="https://i.postimg.cc/0ybvQqky/Whats-App-Image-2026-01-26-at-09-46-20.jpg" alt="Tunisia 2008 - 3">
        <img loading="lazy" src="https://i.postimg.cc/4xmGdTfX/Whats-App-Image-2026-01-26-at-09-46-20-(1).jpg" alt="Tunisia 2008 - 4">
        <img loading="lazy" src="https://i.postimg.cc/g2npJPzJ/Whats-App-Image-2026-01-26-at-09-46-21.jpg" alt="Tunisia 2008 - 5">
        <img loading="lazy" src="https://i.postimg.cc/QdHDtr8N/Whats-App-Image-2026-01-26-at-09-46-21-(1).jpg" alt="Tunisia 2008 - 6">
        <img loading="lazy" src="https://i.postimg.cc/BnX36GSq/Whats-App-Image-2026-01-26-at-09-46-21-(2).jpg" alt="Tunisia 2008 - 7">
        <img loading="lazy" src="https://i.postimg.cc/P5PHxkXq/Whats-App-Image-2026-01-26-at-09-46-21-(3).jpg" alt="Tunisia 2008 - 8">
      </div>
      <div style="text-align:center"><button class="back" type="button">TORNA AI VIAGGI</button></div>
    </div>

  </div>

  <!-- MODAL -->
  <div class="modal" id="modal" aria-hidden="true">
    <div class="close" id="closeModal" aria-label="Chiudi">&times;</div>
    <img id="modalImg" src="" alt="Zoom immagine">
  </div>

  <script>
    // MENU
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
        if(sec){
          sec.classList.add('active');
          sec.scrollIntoView({behavior:'smooth', block:'start'});
        }
        btn.classList.add('active');
      });
    });

    // TORNA AI VIAGGI
    document.querySelectorAll('.back').forEach(back => {
      back.addEventListener('click', () => {
        resetSections();
        window.scrollTo({top:0, behavior:'smooth'});
      });
    });

    // MODAL
    const modal = document.getElementById('modal');
    const modalImg = document.getElementById('modalImg');
    const closeModal = document.getElementById('closeModal');

    let scale = 1, originX = 0, originY = 0;
    let startX = 0, startY = 0, isDragging = false;
    let initialDistance = 0;

    function setTransform(){
      modalImg.style.transform = `translate3d(${originX}px, ${originY}px, 0) scale(${scale})`;
    }

    function openModal(src, alt){
      modal.classList.add('open');
      modal.setAttribute('aria-hidden','false');
      document.body.style.overflow = 'hidden';
      modalImg.src = src;
      modalImg.alt = alt || 'Zoom immagine';
      scale = 1; originX = 0; originY = 0;
      setTransform();
    }

    function closeModalFn(){
      modal.classList.remove('open');
      modal.setAttribute('aria-hidden','true');
      document.body.style.overflow = '';
      modalImg.src = '';
    }

    document.addEventListener('click', (e) => {
      const img = e.target.closest('.gallery img');
      if(img) openModal(img.src, img.alt);
    });

    closeModal.addEventListener('click', closeModalFn);
    modal.addEventListener('click', (e) => { if(e.target === modal) closeModalFn(); });

    document.addEventListener('keydown', (e) => {
      if(e.key === 'Escape' && modal.classList.contains('open')) closeModalFn();
    });

    // Wheel zoom (PC)
    modalImg.addEventListener('wheel', (e) => {
      if(!modal.classList.contains('open')) return;
      e.preventDefault();
      const delta = e.deltaY > 0 ? -0.12 : 0.12;
      scale = Math.min(Math.max(1, scale + delta), 5);
      setTransform();
    }, { passive:false });

    // Drag (PC)
    modalImg.addEventListener('mousedown', (e) => {
      if(!modal.classList.contains('open')) return;
      e.preventDefault();
      isDragging = true;
      startX = e.clientX - originX;
      startY = e.clientY - originY;
    });
    window.addEventListener('mouseup', () => isDragging = false);
    window.addEventListener('mousemove', (e) => {
      if(!isDragging || !modal.classList.contains('open')) return;
      originX = e.clientX - startX;
      originY = e.clientY - startY;
      setTransform();
    });

    // Pinch zoom (mobile)
    modalImg.addEventListener('touchstart', (e) => {
      if(!modal.classList.contains('open')) return;
      if(e.touches.length === 2){
        initialDistance = Math.hypot(
          e.touches[0].clientX - e.touches[1].clientX,
          e.touches[0].clientY - e.touches[1].clientY
        );
      }
    }, { passive:true });

    modalImg.addEventListener('touchmove', (e) => {
      if(!modal.classList.contains('open')) return;
      if(e.touches.length === 2){
        e.preventDefault();
        const newDistance = Math.hypot(
          e.touches[0].clientX - e.touches[1].clientX,
          e.touches[0].clientY - e.touches[1].clientY
        );
        const delta = (newDistance - initialDistance) / 220;
        scale = Math.min(Math.max(1, scale + delta), 5);
        setTransform();
        initialDistance = newDistance;
      }
    }, { passive:false });
  </script>
</body>
</html>
