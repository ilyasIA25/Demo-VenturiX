
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1" />
  <title>VenturiX – Simulation d'écoulements internes</title>

  <link href="https://fonts.googleapis.com/css2?family=Lato:wght@300;400;600&family=Merriweather:wght@400;700&display=swap" rel="stylesheet">

  <style>
    :root {
      --marine:#0A2740;
      --orange:#F38B00;
      --cyan:#1da9b3;
      --gris:#f4f7fa;
      --ombre:0 4px 12px rgba(0,0,0,.08);
    }

    body {
      margin:0;
      font-family:'Lato',sans-serif;
      background:var(--gris);
      color:var(--marine);
      line-height:1.6;
      -webkit-font-smoothing:antialiased;
    }

    header {
      background:linear-gradient(120deg,var(--marine),#12345a);
      color:white;
      padding:1.1rem 1rem;
      position:sticky;top:0;z-index:10;
      box-shadow:0 2px 8px rgba(0,0,0,0.15);
    }
    .brand {display:flex;align-items:center;justify-content:center;gap:10px;}
    .brand img {width:38px;height:38px;border-radius:6px;object-fit:contain;}
    .brand h1 {font-family:'Merriweather',serif;font-size:1.5rem;margin:0;}
    .brand span:first-child{color:white;}
    .brand span:last-child{color:var(--orange);}

    nav{display:flex;overflow-x:auto;gap:8px;padding:.6rem .4rem .8rem;scrollbar-width:none;}
    nav::-webkit-scrollbar{display:none;}
    .tab{
      flex-shrink:0;background:white;color:var(--marine);
      border:none;border-radius:8px;padding:.55rem 1rem;
      font-weight:600;font-size:.95rem;box-shadow:var(--ombre);
      transition:all .25s ease;
    }
    .tab:hover{background:var(--cyan);color:white;}
    .tab:active{transform:scale(1.06);}
    .tab.active{background:var(--orange);color:white;}

    main{padding:1rem;}
    section{
      display:none;background:white;border-radius:12px;
      box-shadow:var(--ombre);padding:1.3rem;margin-bottom:1rem;
      animation:fade .3s ease;
    }
    section.active{display:block;}
    @keyframes fade{from{opacity:0;transform:translateY(8px);}to{opacity:1;transform:translateY(0);}}

    h2{font-family:'Merriweather',serif;font-size:1.25rem;margin-top:0;color:var(--marine);}
    p{text-align:justify;margin-bottom:.9rem;}
    .subtitle{font-size:.9rem;color:#555;font-style:italic;margin:.2rem 0 .6rem;}

    .eq{
      display:flex;justify-content:center;align-items:center;
      background:#f8fbff;border-left:4px solid var(--orange);
      border-radius:8px;padding:.7rem;margin:1rem 0;
      font-size:1.05rem;
    }
    .graph{
      background:#f9fcfe;border:1px solid #e0e9f0;border-radius:8px;
      padding:.6rem;margin:1rem 0;text-align:center;
    }
    .graph svg{text-align:center;width:100%;height:auto;}
    .callout{
      background:linear-gradient(180deg,#f8fafc,#edf3f7);
      border-left:4px solid var(--cyan);
      padding:.9rem;border-radius:8px;
      font-size:.95rem;margin:1rem 0;
    }
    .video-block{margin:1rem 0;}
    .video-title{font-weight:700;font-size:.95rem;margin-bottom:.2rem;}
    .video-caption{font-size:.85rem;color:#444;margin-bottom:.4rem;}
    .video{
      width:100%;border-radius:8px;background:#e8f0f7;
      min-height:180px;display:flex;align-items:center;justify-content:center;
      color:#567;font-size:.9rem;
    }

    footer{text-align:center;padding:1rem;font-size:.85rem;color:#345;}
  </style>
</head>

<body>
  <header>
    <div class="brand">
      <img src="logo-venturix.png" alt="Logo VenturiX">
      <h1><span>Venturi</span><span>X</span></h1>
    </div>
    <nav>
      <button class="tab active" data-target="intro">Présentation</button>
      <button class="tab" data-target="conduit">Conduit simple</button>
      <button class="tab" data-target="venturi">Venturi</button>
      <button class="tab" data-target="obstacle">Obstacle</button>
    </nav>
  </header>

  <main>
    <!-- Présentation -->
    <section id="intro" class="active">
      <h2>Découvrir VenturiX</h2>
      <p>
        <strong>VenturiX</strong> est un outil de simulation qui transforme la physique des fluides en images.  
        Basé sur la méthode de Boltzmann sur réseau, il modélise les écoulements internes avec précision et clarté.
      </p>
      <p>
        Chaque scène révèle la logique cachée des équations :  
        comment la vitesse se distribue, la pression chute, et les tourbillons naissent.
      </p>
      <div class="callout">
        Trois expériences à explorer : le conduit laminaire, l’effet Venturi et la rue de Kármán.
      </div>
    </section>

    <!-- Conduit simple -->
    <section id="conduit">
      <h2>Écoulement dans un conduit simple</h2>

      <div class="video-block">
        <p class="video-title">Vidéo 1 – Petit nombre de Reynolds</p>
        <p class="video-caption">Le profil de vitesse suit la loi de Poiseuille.</p>
        <div class="video">Vidéo</div>
      </div>

      <div class="video-block">
        <p class="video-title">Vidéo 2 – Grand nombre de Reynolds</p>
        <p class="video-caption">Le profil devient plus plat lorsque l’inertie domine.</p>
        <div class="video">Vidéo</div>
      </div>

      <p class="subtitle"><strong>Profil parabolique de Poiseuille</strong></p>
      <div class="eq">$u(r)=u_{max}\!\left(1-\dfrac{r^2}{R^2}\right)$</div>

      <div class="graph">
        <svg viewBox="0 0 200 100">
          <path d="M10,90 Q100,10 190,90" fill="none" stroke="#1da9b3" stroke-width="3"/>
          <text x="60" y="25" font-size="10" fill="#1da9b3">Profil laminaire</text>
        </svg>
      </div>

      <div class="eq">$\Delta P = \dfrac{8\mu L Q}{\pi R^4}$</div>
      <div class="graph">
        <svg viewBox="0 0 200 100">
          <line x1="10" y1="80" x2="190" y2="30" stroke="#F38B00" stroke-width="3"/>
          <text x="60" y="45" font-size="10" fill="#F38B00">Perte de charge linéaire</text>
        </svg>
      </div>

      <div class="callout">
        Plus le nombre de Reynolds augmente, plus la courbe s’aplatit :  
        le fluide accélère, la diffusion visqueuse cède face à l’inertie.
      </div>
    </section>

    <!-- Venturi -->
    <section id="venturi">
      <h2>Écoulement dans un Venturi</h2>
      <div class="video-block">
        <p class="video-title">Vidéo – Accélération et chute de pression</p>
        <p class="video-caption">L’effet Venturi en action : vitesse et pression s’opposent.</p>
        <div class="video">Vidéo</div>
      </div>

      <p class="subtitle"><strong>Principe de Bernoulli</strong></p>
      <div class="eq">$p + \dfrac{1}{2}\rho u^2 + \rho g z = \text{constante}$</div>
      <p>
        La pression chute dans la gorge, puis se rétablit partiellement.  
        En réalité, les pertes visqueuses et les décollements perturbent cet équilibre idéal.
      </p>
      <div class="callout">
        Ce contraste entre théorie et réalité révèle la beauté de la mécanique des fluides.
      </div>
    </section>

    <!-- Obstacle -->
    <section id="obstacle">
      <h2>Écoulement autour d’un obstacle</h2>
      <div class="video-block">
        <p class="video-title">Vidéo – Formation de la rue de Kármán</p>
        <p class="video-caption">Derrière l’obstacle, des tourbillons se détachent en cadence.</p>
        <div class="video">Vidéo</div>
      </div>

      <p class="subtitle"><strong>Relation de Strouhal</strong></p>
      <div class="eq">$St = \dfrac{f D}{U} \approx \text{constante}$</div>
      <p>
        Les tourbillons alternés créent des zones de pression variable :  
        le sillage devient vivant, instable, presque musical.
      </p>
      <div class="callout">
        Cette alternance, appelée <em>rue de Kármán</em>, illustre la transition du calme à la turbulence.
      </div>
    </section>
  </main>

  <footer>© 2025 VenturiX — Simulation et visualisation d’écoulements internes</footer>

  <script>
    const tabs=document.querySelectorAll('.tab');
    const sections=document.querySelectorAll('section');
    tabs.forEach(btn=>{
      btn.addEventListener('click',()=>{
        tabs.forEach(b=>b.classList.remove('active'));
        btn.classList.add('active');
        const target=btn.dataset.target;
        sections.forEach(s=>s.classList.toggle('active',s.id===target));
        window.scrollTo({top:0,behavior:'smooth'});
      });
    });
  </script>

  <script>
  window.MathJax={tex:{inlineMath:[['$','$'],['\\(','\\)']]},options:{renderActions:{addMenu:[]}}};
  </script>
  <script async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
</body>
</html>
