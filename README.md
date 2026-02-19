<html lang="it">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1, minimum-scale=1, maximum-scale=1, viewport-fit=cover" />
  <title>I miei Viaggi</title>

  <style>
    :root{
      --accent: #38bdf8;
      --text: #ffffff;
      --muted: rgba(255,255,255,0.82);
      --panel: rgba(0,0,0,0.28);
      --page-gray: #1f2937;
    }

    *{ box-sizing:border-box; margin:0; padding:0; }
    html,body{ height:100%; }

    html{
      -webkit-text-size-adjust: 100%;
      text-size-adjust: 100%;
    }

    body{
      font-family: Arial, sans-serif;
      background-color: var(--page-gray);
      color: var(--text);
      min-height:100vh;
      overflow-x:hidden;
      font-size: 18px; /* come il tuo */
    }

    /* Sfondo */
    body::before{
      content:"";
      position: fixed;
      inset: 0;
      z-index: 0;
      pointer-events: none;
      background:
        linear-gradient(rgba(0,0,0,0.66), rgba(0,0,0,0.66)),
        url("https://i.postimg.cc/nLyGVZ2b/Whats-App-Image-2026-01-22-at-14-06-48.jpg") no-repeat center center fixed;
      background-size: contain;
      background-position: center center;
    }

    /* Container */
    .container{
      width: min(1480px, 53vw);
      margin: auto;
      padding: 28px;
      position: relative;
      z-index: 1;
    }

    header{
      text-align:center;
      margin-bottom:16px;
    }
    header h1{
      font-size: 40px;
      letter-spacing: 1.5px;
      text-shadow: 2px 2px 10px rgba(0,0,0,0.75);
    }
    header p{
      color: var(--muted);
      margin-top: 8px;
      font-size: 1rem;
    }

    /* Menu */
    .buttons{
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(170px, 1fr));
      gap: 12px;
      margin: 18px 0 26px;
    }
    .buttons button{
      padding: 12px 16px;
      border: 1px solid rgba(255,255,255,0.08);
      border-radius: 12px;
      background: rgba(255,255,255,0.08);
      color: var(--text);
      cursor: pointer;
      font-size: 1rem;
      transition: 0.22s;
      box-shadow: 0 6px 14px rgba(0,0,0,0.35);
    }
    .buttons button:hover{
      background: rgba(255,255,255,0.14);
      transform: translateY(-2px);
      border-color: rgba(255,255,255,0.14);
    }
    .buttons button.active{
      background: linear-gradient(135deg,var(--accent),#818cf8);
      color:#020617;
      border:none;
      box-shadow:0 10px 30px rgba(56,189,248,0.18);
    }

    /* Sezioni */
    .section{
      display:none;
      margin-top: 12px;
      padding: 18px;
      background: var(--panel);
      border-radius: 14px;
      box-shadow: 0 8px 20px rgba(0,0,0,0.45);
      border: 1px solid rgba(255,255,255,0.05);
      backdrop-filter: blur(4px);
    }
    .section.active{display:block}
    .section h2{margin-bottom:8px;font-size:1.35rem}
    .section p{color:var(--muted);margin-bottom:14px;font-size:1rem}

    /* Gallery */
    .gallery{
      display:grid;
      grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
      gap: 14px;
    }
    .gallery img{
      width:100%;
      height: 220px;
      object-fit: cover;
      border-radius: 10px;
      cursor: pointer;
      transition: transform .22s, box-shadow .22s, border-color .22s;
      border: 3px solid rgba(255,255,255,0.12);
      background: rgba(255,255,255,0.06);
    }
    .gallery img:hover{
      transform: scale(1.03);
      box-shadow: 0 18px 40px rgba(0,0,0,0.60);
      border-color: rgba(255,255,255,0.28);
    }

    .back{
      display:inline-block;
      margin: 18px auto 0;
      padding: 10px 18px;
      border-radius: 12px;
      background: rgba(255,255,255,0.08);
      color: var(--text);
      border: 1px solid rgba(255,255,255,0.08);
      cursor: pointer;
      font-size: 1rem;
      transition: .2s;
      box-shadow: 0 6px 14px rgba(0,0,0,0.35);
    }
    .back:hover{ background: rgba(255,255,255,0.14); }

    /* MODAL */
    .modal{
      display:none;
      position:fixed;
      inset:0;
      z-index: 1000;
      background: rgba(0,0,0,0.88);
      justify-content:center;
      align-items:center;
      overflow:hidden;
      padding: 14px;
    }
    .modal.open{ display:flex; }

    .modal img{
      max-width: 92%;
      max-height: 92%;
      border-radius: 12px;
      box-shadow: 0 20px 60px rgba(0,0,0,0.70);
      transition: transform 0.2s ease;
      touch-action: pinch-zoom;
      cursor: grab;
      user-select:none;
      -webkit-user-drag:none;
      transform: translate3d(0,0,0) scale(1);
    }
    .modal img:active{ cursor: grabbing; }

    .modal .close{
      position:absolute;
      top: 16px;
      right: 18px;
      font-size: 34px;
      color:#fff;
      cursor:pointer;
      padding: 6px 12px;
      border-radius: 12px;
      background: rgba(255,255,255,0.10);
      border: 1px solid rgba(255,255,255,0.14);
      user-select:none;
    }

    /* Tablet */
    @media (max-width: 900px){
      body{ font-size: 18px; }
      header h1{ font-size: 32px; }
      .gallery img{ height: 200px; }
      .buttons{ grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); }
      .gallery{ grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); }
    }

    /* Telefono */
    @media (max-width: 600px){
      body{ font-size: 18px; }
      .container{ padding: 16px; width: 96vw; }
      header h1{ font-size: 28px; }
      .buttons button{ font-size: 1rem; padding: 12px 10px; }
      .gallery img{ height: 200px; }
      .buttons{ grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); }
    }

    @media (prefers-reduced-motion: reduce){
      *{ transition:none !important; scroll-behavior:auto !important; }
    }

    /* ====== SOLO PC: SISTEMA SOLO LE SCRITTE (posizione/leggibilità) ======
       Non cambia font (resta Arial), non mette grassetto, non tocca layout. */
    @media (min-width: 901px){
      body{
        line-height: 1.55;
      }

      header{
        margin-bottom: 22px;
      }
      header h1{
        font-size: 44px;        /* più bello su PC ma non “gigante” */
        line-height: 1.12;
        letter-spacing: 0.6px;  /* meno “squadrato” del 1.5px */
        margin-bottom: 8px;
      }
      header p{
        max-width: 70ch;        /* evita riga lunghissima su PC */
        margin: 0 auto;
        line-height: 1.6;
      }

      .section h2{
        line-height: 1.2;
        margin-bottom: 10px;
      }
      .section p{
        max-width: 75ch;
        line-height: 1.7;
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
       <button data-target="croazia">Croazia</button>
    </div>

    <div id="sardegna" class="section">
      <h2>Sardegna 2025</h2>
      <p>In attesa delle foto.</p>
      <div class="gallery"></div>
      <div style="text-align:center"><button class="back" type="button">TORNA AI VIAGGI</button></div>
    </div>

    <div id="croazia" class="section">
      <h2>Croazia</h2>
      <div class="gallery">
       <img loading="lazy" src="https://i.postimg.cc/2jL3WnBY/Whats-App-Image-2026-02-02-at-08-23-05.jpg" alt="Croazia - 1">
      </div>
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
