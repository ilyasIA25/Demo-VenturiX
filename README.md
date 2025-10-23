<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <title>VenturiX – Simulation d’écoulements fluides</title>
  <meta name="viewport" content="width=device-width, initial-scale=1" />

  <!-- Polices -->
  <link href="https://fonts.googleapis.com/css2?family=Lato:wght@300;400;600;700&family=Merriweather:wght@300;400;700&display=swap" rel="stylesheet">

  <!-- MathJax pour les équations -->
  <script>
    window.MathJax = { tex: { inlineMath: [['$', '$'], ['\\(', '\\)']] } };
  </script>
  <script defer src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>

  <style>
    :root{
      --bg-start:#f6f9fc;
      --bg-end:#e8f1f8;
      --ink:#1b1f23;
      --blue:#0b4f91;
      --blue-2:#136fb2;
      --accent:#22a7f0;
      --card:#ffffff;
      --shadow:0 8px 22px rgba(0,0,0,.06);
      --radius:14px;
    }

    *{box-sizing:border-box}
    html,body{height:100%}
    body{
      margin:0;
      font-family:'Lato',system-ui,-apple-system,Segoe UI,Roboto,Arial,sans-serif;
      color:var(--ink);
      background:linear-gradient(180deg,var(--bg-start) 0%,var(--bg-end) 100%);
      -webkit-font-smoothing:antialiased;
      line-height:1.7;
    }

    /* Header / Brand */
    .site-header{
      position:sticky; top:0; z-index:50;
      backdrop-filter:saturate(1.2) blur(6px);
      background:linear-gradient(120deg, rgba(11,79,145,.92), rgba(19,111,178,.92));
      color:#fff;
      border-bottom:1px solid rgba(255,255,255,.12);
    }
    .container{
      max-width:1100px; margin:0 auto; padding:0 20px;
    }
    .brand{
      display:flex; align-items:center; gap:14px; padding:14px 0;
    }
    .brand img{
      width:40px; height:40px; object-fit:contain; border-radius:8px; background:#ffffff10;
      box-shadow:0 4px 10px rgba(0,0,0,.15);
    }
    .brand .title{
      display:flex; flex-direction:column; line-height:1.2;
    }
    .brand .title h1{
      margin:0; font-size:1.35rem; letter-spacing:.3px; font-family:'Merriweather',serif; font-weight:700;
    }
    .brand .subtitle{
      font-size:.92rem; opacity:.9;
    }

    /* Nav */
    .nav{
      display:flex; gap:8px; flex-wrap:wrap; padding:0 0 14px 0;
    }
    .tab{
      appearance:none; border:none; background:#ffffff15; color:#fff;
      padding:10px 14px; border-radius:10px; font-weight:600; letter-spacing:.2px;
      cursor:pointer; transition:transform .15s ease, background .2s ease, box-shadow .2s ease;
      box-shadow:0 2px 10px rgba(0,0,0,.1);
    }
    .tab:hover{ background:#ffffff25; transform:translateY(-1px) }
    .tab:focus-visible{ outline:2px solid #fff; outline-offset:2px }
    .tab.active{ background:#fff; color:var(--blue); box-shadow:var(--shadow) }

    /* Hero */
    .hero{
      margin:26px 0 0;
      background:linear-gradient(135deg,#ffffffbb,#ffffff60);
      border-radius:var(--radius);
      box-shadow:var(--shadow);
      padding:26px;
    }
    .hero h2{
      margin:0 0 8px; color:var(--blue); font-family:'Merriweather',serif; font-weight:700;
    }
    .hero p{ margin:0; max-width:72ch }

    /* Sections */
    main{ padding:22px 0 60px }
    .panel{
      display:none;
      background:var(--card);
      border-radius:var(--radius);
      box-shadow:var(--shadow);
      padding:28px;
      margin:18px 0;
      animation:fadeIn .35s ease;
    }
    .panel.active{ display:block }

    @keyframes fadeIn{
      from{opacity:0; transform:translateY(10px)}
      to{opacity:1; transform:translateY(0)}
    }

    h3{ color:var(--blue); font-family:'Merriweather',serif; margin-top:0 }
    .underline{
      width:70px; height:3px; background:var(--accent); border-radius:3px; margin:6px 0 18px
    }

    .grid{
      display:grid; gap:18px;
      grid-template-columns:repeat(12,1fr);
    }
    .col-6{ grid-column:span 6 }
    .col-12{ grid-column:span 12 }

    @media (max-width:860px){
      .col-6{ grid-column:span 12 }
    }

    .video-card{
      background:#f8fbfe; border:1px solid #e6edf5; border-radius:12px; padding:14px;
      transition:transform .2s ease, box-shadow .2s ease;
    }
    .video-card:hover{ transform:translateY(-2px); box-shadow:0 10px 20px rgba(0,0,0,.06) }
    video, .video-placeholder{
      width:100%; aspect-ratio:16/9; border-radius:8px; background:#e8f1f8; border:1px dashed #cbd8e6;
    }
    .video-placeholder{
      display:flex; align-items:center; justify-content:center; color:#678; font-size:.95rem;
    }

    .callout{
      background:linear-gradient(180deg,#f2f7fc,#eef5fb);
      border:1px solid #e2edf7;
      border-radius:12px; padding:16px; margin-top:8px; color:#213;
    }

    footer{
      margin-top:36px; text-align:center; color:#345; font-size:.95rem; padding-bottom:24px;
    }
    a.link{ color:var(--blue); text-decoration:none; border-bottom:1px solid #d3e6f7 }
    a.link:hover{ color:var(--blue-2); border-bottom-color:var(--blue-2) }

    /* Figure style (pour futurs graphes) */
    .figure{
      background:#fbfdff; border:1px solid #e7eef7; border-radius:12px; padding:14px;
      font-size:.95rem;
    }
    .figure h4{ margin:0 0 8px; font-size:1rem; color:#244 }
    .muted{ color:#5b6b7a }
  </style>
</head>

<body>
  <!-- HEADER + NAV -->
  <header class="site-header">
    <div class="container">
      <div class="brand" aria-label="VenturiX">
        <!-- Remplace src par ton fichier logo -->
        <img src="logo-venturix.png" alt="Logo VenturiX" />
        <div class="title">
          <h1>VenturiX</h1>
          <span class="subtitle">Simulation d’écoulements – rigueur physique & visualisation</span>
        </div>
      </div>

      <nav class="nav" role="tablist" aria-label="Navigation des vues">
        <button class="tab active" data-target="home" role="tab" aria-selected="true">Présentation</button>
        <button class="tab" data-target="conduit" role="tab" aria-selected="false">Conduit simple</button>
        <button class="tab" data-target="venturi" role="tab" aria-selected="false">Venturi</button>
        <button class="tab" data-target="obstacle" role="tab" aria-selected="false">Obstacle</button>
      </nav>
    </div>
  </header>

  <!-- HERO -->
  <div class="container">
    <div class="hero" id="hero">
      <h2>Modéliser, visualiser, comprendre.</h2>
      <p>
        VenturiX est une plateforme de simulation fondée sur la méthode de Boltzmann sur réseau (LBM).
        L’outil propose une interface claire, des scénarios reproductibles et des visualisations soignées,
        pour relier la physique des équations aux phénomènes observés. Les sections ci-dessous présentent trois cas d’étude :
        écoulement dans un conduit simple, effet Venturi, et sillage derrière obstacle.
      </p>
    </div>
  </div>

  <!-- PANELS -->
  <main class="container">

    <!-- Présentation -->
    <section class="panel active" id="home" role="tabpanel" aria-labelledby="tab-home">
      <h3>Présentation générale</h3>
      <div class="underline"></div>
      <p>
        Conçu pour être scientifiquement rigoureux et visuellement lisible, VenturiX relie la
        cinétique particulaire (LBM) au comportement macroscopique ($\\rho,\\ \\mathbf{u},\\ p$) des écoulements.
        Les scénarios sont configurés avant exécution (géométrie, conditions aux limites, viscosité cinématique $\\nu$, vitesse d’entrée),
        puis simulés et visualisés avec des cartes de vitesse et de pression.
      </p>
      <div class="callout">
        <strong>Base physique.</strong> Le schéma BGK à temps de relaxation unique (~$\\tau$) relie la fonction de distribution
        $f_i(\\mathbf{x},t)$ au quasi-équilibre $f_i^{eq}$ : $\\; f_i(\\mathbf{x}+\\mathbf{e}_i\\Delta t,t+\\Delta t)-f_i(\\mathbf{x},t)= -\\dfrac{\\Delta t}{\\tau}\\big(f_i-f_i^{eq}\\big)$.
        Les grandeurs macroscopiques s’obtiennent par moments : $\\rho=\\sum_i f_i$, $\\rho\\mathbf{u}=\\sum_i f_i\\mathbf{e}_i$.
      </div>
    </section>

    <!-- Conduit simple -->
    <section class="panel" id="conduit" role="tabpanel" aria-labelledby="tab-conduit">
      <h3>Écoulement dans un conduit simple</h3>
      <div class="underline"></div>

      <div class="grid">
        <div class="col-6">
          <div class="video-card">
            <div class="video-placeholder">Vidéo 1 — petit nombre de Reynolds (profil parabolique)</div>
            <!-- Remplace par ta vidéo :
            <video controls src="conduit_re_petit.mp4"></video> -->
          </div>
        </div>
        <div class="col-6">
          <div class="video-card">
            <div class="video-placeholder">Vidéo 2 — grand nombre de Reynolds (profil aplati)</div>
            <!-- <video controls src="conduit_re_grand.mp4"></video> -->
          </div>
        </div>

        <div class="col-12">
          <div class="callout">
            <strong>Régime laminaire & loi de Poiseuille.</strong>
            Dans un tube de rayon $R$ et de longueur $L$, sous hypothèses newtoniennes, incompressibles et stationnaires, le profil est
            parabolique : $\\; u(r)=u_{max}\\big(1-(r/R)^2\\big)$, et la perte de charge linéaire suit
            $\\; \\Delta P = \\dfrac{8\\mu L Q}{\\pi R^4}$ (équivalent à $\\Delta P=\\lambda\\,\\dfrac{L}{D}\\,\\dfrac{\\rho U_m^2}{2}$ avec $\\lambda=64/Re$ en laminaire).
          </div>
        </div>

        <div class="col-12">
          <div class="figure">
            <h4>Pourquoi le profil s’aplatit à grand $Re$ ?</h4>
            <p class="muted">
              Quand le nombre de Reynolds $Re=\\dfrac{\\rho U D}{\\mu}$ augmente, l’advection ($\\mathbf{u}\\cdot\\nabla\\mathbf{u}$) domine la diffusion visqueuse ($\\nu\\nabla^2\\mathbf{u}$)
              dans Navier–Stokes. L’effet est une **couche limite** plus fine et un cœur d’écoulement quasi-isovitesse : le profil s’aplatit.
              Mathématiquement, la solution stationnaire s’écarte de la parabole de Poiseuille car le terme non linéaire n’est plus négligeable.
              En turbulence pleinement développée (au-delà d’un seuil dépendant des conditions), le profil moyen suit des lois de type puissance ou logarithmique près des parois,
              ce qui renforce l’aplatissement relatif du cœur.
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- Venturi -->
    <section class="panel" id="venturi" role="tabpanel" aria-labelledby="tab-venturi">
      <h3>Écoulement dans un conduit avec goulot d’étranglement (Venturi)</h3>
      <div class="underline"></div>

      <div class="grid">
        <div class="col-12">
          <div class="video-card">
            <div class="video-placeholder">Vidéo — effet Venturi (accélération dans la gorge, chute de pression locale)</div>
            <!-- <video controls src="venturi_demo.mp4"></video> -->
          </div>
        </div>

        <div class="col-12">
          <div class="callout">
            <strong>Bernoulli idéalisé.</strong>
            Sous hypothèses d’écoulement **stationnaire**, **incompressible**, **sans viscosité** et le long d’une même ligne de courant,
            $\\; p + \\tfrac{1}{2}\\rho u^2 + \\rho g z = \\text{const}$. La réduction de section impose une **augmentation de vitesse**
            et donc une **diminution de pression statique** dans la gorge.
          </div>
        </div>

        <div class="col-12">
          <div class="figure">
            <h4>Cas réel : pertes de charge et décollement</h4>
            <p class="muted">
              Dans les conditions réelles, la viscosité et les gradients accentués de vitesse induisent des **pertes de charge** (linéaires + singulières).
              À l’entrée/sortie du Venturi, les pertes singulières s’évaluent via des coefficients $\\zeta$ (géométrie-dépendants) :
              $\\Delta P_{sing}=\\zeta\\,\\dfrac{\\rho U^2}{2}$.
              En sortie de gorge, la **dilatation** du jet peut induire un **décollement** et une zone de recirculation, modifiant la récupération de pression.
              Le champ de $p$ apparaît donc asymétrique : chute nette dans la gorge, remontée partielle, puis alignement avec la perte linéaire globale.
            </p>
          </div>
        </div>
      </div>
    </section>

    <!-- Obstacle -->
    <section class="panel" id="obstacle" role="tabpanel" aria-labelledby="tab-obstacle">
      <h3>Écoulement dans un conduit avec obstacle</h3>
      <div class="underline"></div>

      <div class="grid">
        <div class="col-12">
          <div class="video-card">
            <div class="video-placeholder">Vidéo — sillage derrière l’obstacle (détachement et vortex)</div>
            <!-- <video controls src="obstacle_demo.mp4"></video> -->
          </div>
        </div>

        <div class="col-12">
          <div class="callout">
            <strong>Pourquoi des tourbillons ?</strong>
            Le cisaillement élevé et la séparation de couche limite au bord de fuite génèrent un **détachement périodique de tourbillons** :
            la **rue de Kármán**. La fréquence $f$ du détachement suit approximativement $St=\\dfrac{f D}{U}\\approx \\text{cste}$ (selon $Re$ et géométrie),
            où $D$ est la taille caractéristique de l’obstacle. On observe des zones de pression plus basse alternées dans le sillage et un traînée accrue.
          </div>
        </div>

        <div class="col-12">
          <div class="figure">
            <h4>Lecture des courbes et champs</h4>
            <p class="muted">
              Les cartes de vitesse révèlent les **zones de recirculation** et le **sillage** allongé en aval. Les champs de pression montrent
              un **déficit dans la poche tourbillonnaire**. En augmentant $Re$, la fréquence de détachement croît (selon $St$) et le sillage devient plus instationnaire ;
              les profils de vitesse transverses affichent des inversions locales (vitesses négatives) au cœur de la recirculation.
            </p>
          </div>
        </div>
      </div>
    </section>

    <footer>
      © 2025 VenturiX — Méthode de Boltzmann sur réseau · Python · Taichi
    </footer>
  </main>

  <script>
    // Tabs (navigation sans rechargement)
    const tabs = document.querySelectorAll('.tab');
    const panels = document.querySelectorAll('.panel');

    function activate(target){
      tabs.forEach(t=>{
        const is = t.dataset.target===target;
        t.classList.toggle('active', is);
        t.setAttribute('aria-selected', is ? 'true' : 'false');
      });
      panels.forEach(p=>p.classList.toggle('active', p.id===target));
      // Focus accessible
      const activePanel = document.getElementById(target);
      if(activePanel) activePanel.setAttribute('tabindex','-1'), activePanel.focus({preventScroll:true});
    }

    tabs.forEach(t=>t.addEventListener('click', ()=>activate(t.dataset.target)));

    // Deep-link via hash (#venturi etc.)
    const hash = (location.hash||'').replace('#','');
    if(hash && document.getElementById(hash)) activate(hash);

    // Clique sur le logo renvoie à la présentation
    document.querySelector('.brand')?.addEventListener('click', ()=>activate('home'));
  </script>
</body>
</html>
