<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1" />
  <title>VenturiX – Simulation d'écoulements internes</title>

  <!-- Polices -->
  <link href="https://fonts.googleapis.com/css2?family=Lato:wght@300;400;600&family=Merriweather:wght@400;700&display=swap" rel="stylesheet">

  <!-- Style -->
  <style>
    :root {
      --marine: #0A2740;
      --orange: #F38B00;
      --cyan: #1da9b3;
      --gris: #f4f7fa;
      --ombre: 0 4px 14px rgba(0,0,0,.06);
      --rayon: 12px;
    }

    * { box-sizing: border-box; }
    body {
      margin: 0;
      font-family: 'Lato', sans-serif;
      background: var(--gris);
      color: var(--marine);
      line-height: 1.6;
      -webkit-font-smoothing: antialiased;
    }

    header {
      background: linear-gradient(120deg, var(--marine), #12345a);
      color: white;
      padding: 1.2rem 1rem;
      position: sticky; top: 0; z-index: 10;
      box-shadow: 0 2px 10px rgba(0,0,0,0.15);
    }

    .brand {
      display: flex; align-items: center; justify-content: center; gap: 10px;
    }
    .brand img { width: 42px; height: 42px; object-fit: contain; border-radius: 8px; }
    .brand h1 {
      font-family: 'Merriweather', serif;
      font-size: 1.6rem; margin: 0;
    }
    .brand span:nth-child(1){color: white;}
    .brand span:nth-child(2){color: var(--orange);}

    nav {
      display: flex; overflow-x: auto; gap: 8px;
      padding: .8rem .4rem .6rem;
      scrollbar-width: none;
    }
    nav::-webkit-scrollbar{display:none;}
    .tab {
      flex-shrink: 0;
      border: none; border-radius: 8px;
      background: white; color: var(--marine);
      padding: .6rem 1rem;
      font-weight: 600;
      font-size: .95rem;
      box-shadow: var(--ombre);
      transition: all .25s ease;
    }
    .tab:hover { background: var(--cyan); color: white; }
    .tab:active { transform: scale(1.08); }
    .tab.active { background: var(--orange); color: white; }

    main { padding: 1rem; }
    section {
      display: none;
      background: white;
      border-radius: var(--rayon);
      box-shadow: var(--ombre);
      padding: 1.5rem;
      margin-bottom: 1.2rem;
      animation: fade .3s ease;
    }
    section.active { display: block; }
    @keyframes fade { from {opacity:0; transform:translateY(10px);} to {opacity:1; transform:translateY(0);} }

    h2 {
      font-family: 'Merriweather', serif;
      font-size: 1.3rem;
      color: var(--marine);
      margin-top: 0;
    }

    p { margin-bottom: 1rem; text-align: justify; }

    video, .graph, .placeholder {
      width: 100%;
      border-radius: 10px;
      background: #eaf1f6;
      border: 1px solid #d3dde8;
      min-height: 180px;
      display: flex; align-items: center; justify-content: center;
      font-size: .9rem; color: #567;
      margin: .6rem 0 1rem;
    }

    .callout {
      background: linear-gradient(180deg,#f8fafc,#edf3f7);
      border-left: 4px solid var(--cyan);
      padding: 1rem;
      border-radius: 8px;
      font-size: .95rem;
      margin: 1rem 0;
    }

    footer {
      text-align: center;
      padding: 1rem;
      font-size: .85rem;
      color: #345;
    }
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
      <h2>Présentation de l’outil</h2>
      <p>
        <strong>VenturiX</strong> est un outil numérique de simulation et de visualisation d’écoulements internes.
        Fondé sur la méthode de Boltzmann sur réseau (LBM), il établit le lien entre la cinétique microscopique des particules
        et les comportements macroscopiques des fluides, dans des géométries telles que les conduits, venturis et obstacles.
      </p>
      <p>
        L’objectif est de rendre les phénomènes physiques perceptibles, en s’appuyant sur des calculs rigoureux,
        des représentations intuitives et une interface pensée pour la clarté.
      </p>
      <div class="callout">
        Trois configurations sont présentées : l’écoulement laminaire dans un conduit,
        l’effet Venturi, et le sillage derrière un obstacle.
      </div>
    </section>

    <!-- Conduit simple -->
    <section id="conduit">
      <h2>Écoulement dans un conduit simple</h2>
      <div class="graph">Graphique – Profil de Poiseuille (courbe parabolique)</div>
      <div class="video">Vidéo 1 – Petit nombre de Reynolds (profil parabolique)</div>
      <div class="video">Vidéo 2 – Grand nombre de Reynolds (profil aplati)</div>

      <p>
        À faible nombre de Reynolds, les forces visqueuses dominent : le profil de vitesse est parabolique, décrit par la
        <strong>loi de Poiseuille</strong> :
      </p>
      <p style="text-align:center;">
        $u(r)=u_{max}\!\left(1-\dfrac{r^2}{R^2}\right)$
      </p>
      <p>
        La perte de charge linéaire s’exprime par :
        $\\Delta P = \\dfrac{8\\mu L Q}{\\pi R^4}$, ou encore
        $\\Delta P = \\lambda\\dfrac{L}{D}\\dfrac{\\rho U_m^2}{2}$ avec $\\lambda = 64/Re$ en laminaire.
      </p>
      <div class="callout">
        À grand Reynolds, l’advection ($\\mathbf{u}\\cdot\\nabla\\mathbf{u}$) devient dominante.
        La couche limite se réduit et le profil s’aplatit : l’écoulement tend vers un cœur quasi-isovitesse.
      </div>
      <div class="graph">Graphique – Comparaison profil laminaire / aplati</div>
    </section>

    <!-- Venturi -->
    <section id="venturi">
      <h2>Écoulement dans un Venturi</h2>
      <div class="video">Vidéo – Accélération et chute de pression dans la gorge</div>
      <p>
        Dans un conduit convergent-divergent, la réduction de section entraîne une accélération du fluide
        et une chute de pression locale. L’équation de <strong>Bernoulli</strong> pour un fluide idéal s’écrit :
      </p>
      <p style="text-align:center;">
        $p + \dfrac{1}{2}\rho u^2 + \rho g z = \text{constante}$
      </p>
      <p>
        En conditions réelles, les pertes visqueuses modifient cette relation : on observe une asymétrie de pression
        et parfois un décollement en sortie de gorge.
      </p>
      <div class="graph">Graphique – Évolution pression / vitesse dans la gorge</div>
      <div class="callout">
        Les pertes de charge totales combinent les pertes linéaires le long du conduit et
        les pertes singulières liées aux variations brusques de géométrie.
      </div>
    </section>

    <!-- Obstacle -->
    <section id="obstacle">
      <h2>Écoulement autour d’un obstacle</h2>
      <div class="video">Vidéo – Formation de la rue de Kármán</div>
      <p>
        Le passage d’un fluide autour d’un obstacle crée un détachement périodique de tourbillons :
        la <strong>rue de Kármán</strong>. Ces structures alternées apparaissent dès que le
        nombre de Reynolds dépasse une valeur critique.
      </p>
      <p style="text-align:center;">
        $St = \dfrac{f D}{U} \approx \text{constante}$
      </p>
      <div class="graph">Graphique – Distribution de pression et sillage tourbillonnaire</div>
      <div class="callout">
        Le champ de vitesse révèle des zones de recirculation et un sillage instationnaire.
        L’alternance des tourbillons provoque des variations périodiques de pression en aval.
      </div>
    </section>
  </main>

  <footer>
    © 2025 VenturiX — Modélisation et Simulation d’Écoulements Internes
  </footer>

  <!-- Navigation JS -->
  <script>
    const tabs=document.querySelectorAll('.tab');
    const sections=document.querySelectorAll('section');
    tabs.forEach(btn=>{
      btn.addEventListener('click',()=>{
        tabs.forEach(b=>b.classList.remove('active'));
        btn.classList.add('active');
        const t=btn.dataset.target;
        sections.forEach(s=>s.classList.toggle('active',s.id===t));
        window.scrollTo({top:0,behavior:'smooth'});
      });
    });
  </script>

  <!-- MathJax stable -->
  <script>
    window.MathJax = {
      tex: { inlineMath: [['$', '$'], ['\\(', '\\)']] },
      options: { renderActions: { addMenu: [] } }
    };
  </script>
  <script async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-mml-chtml.js"></script>
</body>
</html>
