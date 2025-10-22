<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>VenturiX – Simulation d’écoulements fluides</title>

  <style>
    body {
      margin: 0;
      font-family: "Segoe UI", Roboto, sans-serif;
      background: linear-gradient(180deg, #f5fbff 0%, #e8f3fa 100%);
      color: #1b2733;
      line-height: 1.6;
    }

    header {
      background-color: #0b5fa5;
      color: white;
      text-align: center;
      padding: 2rem 1rem;
      box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
    }

    header h1 {
      font-size: 2.2rem;
      letter-spacing: 1px;
      margin-bottom: 0.4rem;
    }

    header p {
      font-size: 1rem;
      opacity: 0.9;
    }

    main {
      max-width: 900px;
      margin: 3rem auto;
      padding: 0 1.5rem;
    }

    section {
      background: white;
      border-radius: 12px;
      box-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
      padding: 2rem;
      margin-bottom: 2rem;
      transition: transform 0.2s ease;
    }

    section:hover {
      transform: translateY(-3px);
    }

    h2 {
      color: #0b5fa5;
      margin-top: 0;
    }

    footer {
      text-align: center;
      background-color: #0b5fa5;
      color: white;
      padding: 1rem 0.5rem;
      font-size: 0.9rem;
      letter-spacing: 0.3px;
    }

    /* Accent line under titles */
    .underline {
      width: 60px;
      height: 3px;
      background-color: #22a7f0;
      border-radius: 3px;
      margin: 0.5rem auto 1.5rem;
    }

    @media (max-width: 600px) {
      header h1 { font-size: 1.7rem; }
      main { padding: 0 1rem; }
      section { padding: 1.5rem; }
    }
  </style>
</head>

<body>
  <header>
    <h1>🌊 VenturiX</h1>
    <p>Plateforme interactive de simulation d’écoulements fluides</p>
  </header>

  <main>
    <section>
      <h2>Présentation du projet</h2>
      <div class="underline"></div>
      <p>
        <strong>VenturiX</strong> est un outil de visualisation et de simulation
        développé pour explorer la dynamique des fluides dans des géométries variées
        (conduits, obstacles, venturis…). Basé sur la <em>méthode de Boltzmann sur réseau (LBM)</em>,
        il relie la physique microscopique des particules au comportement macroscopique du fluide.
      </p>
      <p>
        Ce projet allie rigueur scientifique et interactivité : un panneau de configuration
        permet de contrôler les paramètres physiques (vitesse, viscosité, géométrie)
        avant chaque simulation, pour visualiser les champs de vitesse et de pression
        avec réalisme et précision.
      </p>
    </section>

    <section>
      <h2>Objectif et vision</h2>
      <div class="underline"></div>
      <p>
        VenturiX a pour ambition de devenir une plateforme intuitive et évolutive
        permettant aux ingénieurs, étudiants et industriels d’explorer le comportement
        des fluides en temps réel. En combinant modélisation physique, calcul GPU et
        visualisation interactive, l’outil offre une passerelle directe entre la
        théorie et la pratique.
      </p>
    </section>
  </main>

  <footer>
    © 2025 VenturiX – Simulation Fluide & Innovation Numérique  
  </footer>
</body>
</html>
