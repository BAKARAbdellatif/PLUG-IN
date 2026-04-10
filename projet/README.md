# 🎓 TP CSS — Maîtriser le CSS par la pratique

## Contexte du projet

Vous êtes développeur chez **DevPulse**, une startup SaaS qui propose un dashboard de monitoring pour développeurs. Votre mission : construire l'interface complète du dashboard en **HTML + CSS pur** (aucun framework autorisé).

Le projet sera construit **étape par étape** : d'abord le HTML brut, puis on ajoute le CSS progressivement pour chaque composant.

> **Prérequis** : savoir écrire du HTML basique (balises, attributs, structure d'une page).
> **Livrable** : un fichier `index.html` et un fichier `style.css` liés entre eux.

---

## Structure initiale

Créez les fichiers suivants :

```
projet/
├── index.html
├── style.css
└── images/
    └── (vide pour l'instant)
```

Dans `index.html`, partez de cette base :

```html
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>DevPulse — Dashboard</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <!-- Vous construirez le contenu ici, exercice par exercice -->
</body>
</html>
```

Dans `style.css`, commencez par le reset et les variables :

```css
/* Reset de base */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* Variables — votre design system */
:root {
  --bg: #0f1117;
  --surface: #1a1d27;
  --surface-2: #232734;
  --border: #2e3345;
  --text: #e2e4ed;
  --text-muted: #8b8fa3;
  --accent: #6c5ce7;
  --success: #00cec9;
  --danger: #ff6b6b;
  --warning: #feca57;
  --radius: 8px;
}

body {
  font-family: sans-serif;
  background: var(--bg);
  color: var(--text);
}
```

---

---

# 🧱 MODULE 1 — Layout (mise en page)

---

## Exercice 1.1 — Centrer un élément (horizontal + vertical)

### Objectif
Afficher une boîte de login centrée au milieu de l'écran.

### Étape 1 : HTML
```html
<div class="login-page">
  <div class="login-box">
    <h1>DevPulse</h1>
    <p>Connectez-vous à votre dashboard</p>
    <button>Se connecter</button>
  </div>
</div>
```

### Étape 2 : CSS à implémenter
1. `.login-page` doit prendre toute la hauteur de l'écran (`100vh`)
2. Centrer `.login-box` horizontalement ET verticalement dans `.login-page`
3. Donner à `.login-box` un fond `var(--surface)`, du padding, et des coins arrondis

> **Concepts à utiliser** : `display: flex`, `justify-content`, `align-items`, `min-height`


---

# 🛠️ Exercice 1.1 — Centrer la boîte de Login

Dans cette étape, nous allons créer une page de connexion. Le défi ici est de placer une boîte parfaitement au centre de l'écran, peu importe la taille du moniteur ou du téléphone.

### 1. Comprendre les outils
Avant de coder, voici ce que nous allons utiliser :
* **`display: flex`** : C'est comme activer un mode "aimant" sur un conteneur. Il permet de manipuler facilement l'alignement de tout ce qui se trouve à l'intérieur.
* **`justify-content`** : Gère l'alignement **horizontal** (gauche, centre, droite).
* **`align-items`** : Gère l'alignement **vertical** (haut, centre, bas).
* **`100vh`** : Signifie "100% de la hauteur de l'écran". Par défaut, une `div` ne fait que la hauteur de son texte. Pour centrer quelque chose verticalement dans l'écran, il faut forcer le parent à faire toute la hauteur de l'écran.

---

### 2. Action : Structure HTML
Ajoutez ce bloc à l'intérieur de votre balise `<body>` dans `index.html`. C'est la structure brute de notre page.

```html
<div class="login-page">
  <div class="login-box">
    <h1>DevPulse</h1>
    <p>Connectez-vous à votre dashboard</p>
    <button class="btn-primary">Se connecter</button>
  </div>
</div>
```

> **À ce stade :** Si vous actualisez, tout est en haut à gauche, c'est normal !

---

### 3. Action : Le centrage "Flexbox"
Ouvrez votre fichier `style.css`. Nous allons maintenant transformer la classe `.login-page` en un conteneur qui centre son contenu.

```css
.login-page {
  /* On force la page à faire toute la hauteur du navigateur */
  min-height: 100vh; 
  
  /* On active Flexbox */
  display: flex;
  
  /* On aligne horizontalement ET verticalement */
  justify-content: center;
  align-items: center;
}
```

> **Vérification :** Enregistrez et actualisez votre navigateur. Votre texte doit être passé pile au milieu de la page blanche.

---

### 4. Action : Styliser la boîte
Le texte est centré, mais il n'a pas encore l'air d'une "carte". Ajoutons du style à la `.login-box` :

```css
.login-box {
  /* On utilise la variable de surface définie au début */
  background-color: var(--surface); 
  
  /* On crée de l'espace autour du texte à l'intérieur de la boîte */
  padding: 40px;
  
  /* On arrondit les angles */
  border-radius: var(--radius);
  
  /* On centre le texte à l'intérieur de la boîte elle-même */
  text-align: center;
  
  /* On ajoute une bordure fine pour définir les contours */
  border: 1px solid var(--border);
}

/* Colorons le titre pour qu'il ressorte */
.login-box h1 {
  color: var(--accent);
  margin-bottom: 8px;
}
```

> **Résultat final :** Vous avez maintenant une vraie interface de connexion moderne et centrée. Jouez avec la taille de votre fenêtre de navigateur : la boîte reste toujours parfaitement au milieu.

---

**On passe à l'Exercice 1.2 (L'Avatar avec position absolute) ?**
---

## Exercice 1.2 — Superposition avec position absolute

### Objectif
Créer un avatar utilisateur avec un badge "en ligne" (point vert) positionné en bas à droite.

### Étape 1 : HTML
```html
<div class="avatar-wrapper">
  <img src="https://i.pravatar.cc/64?img=3" alt="Avatar" class="avatar-img">
  <span class="status-badge online"></span>
</div>
```

### Étape 2 : CSS à implémenter
1. `.avatar-wrapper` doit être le **repère** pour le positionnement (quel `position` ?)
2. `.avatar-img` : rond (border-radius 50%), taille 64x64
3. `.status-badge` : petit cercle de 14px, positionné en bas à droite de l'avatar, avec une bordure qui "tranche" visuellement avec l'avatar
4. `.online` : fond vert (`var(--success)`)

> **Concepts à utiliser** : `position: relative` (parent), `position: absolute` (enfant), `bottom`, `right`, `border-radius`

# 🛠️ Exercice 1.2 — Superposition avec position "Absolute"

Dans cet exercice, nous allons apprendre à superposer des éléments. L'objectif est de placer un badge de statut (un petit point vert) par-dessus l'image de profil d'un utilisateur, précisément en bas à droite.

### 1. Comprendre les outils
Pour superposer des éléments, on utilise le système de positionnement :
* **`position: relative` (Le Parent)** : On définit l'élément parent comme le "cadre" de référence. C'est l'ancre. Tout ce qui sera à l'intérieur se positionnera par rapport aux bords de ce cadre.
* **`position: absolute` (L'Enfant)** : On retire l'élément du flux normal de la page pour le faire "flotter". On utilise ensuite `top`, `bottom`, `left` ou `right` pour lui dire exactement où se placer par rapport à son parent.
* **`border-radius: 50%`** : Transforme n'importe quel carré parfait en un cercle parfait.

---

### 2. Action : Structure HTML
Ajoutez ce code dans votre fichier `index.html` (vous pouvez le mettre à la suite de l'exercice précédent ou dans une nouvelle section) :

```html
<div class="avatar-wrapper">
  <img src="https://i.pravatar.cc/64?img=3" alt="Avatar" class="avatar-img">
  <span class="status-badge online"></span>
</div>
```

---

### 3. Action : Préparer l'Avatar (CSS)
Ouvrez `style.css`. Nous allons d'abord donner sa forme à l'image et préparer son conteneur.

```css
.avatar-wrapper {
  /* ÉLÉMENT CLÉ : On définit le repère pour le badge */
  position: relative; 
  
  width: 64px;
  height: 64px;
  margin: 20px; /* Un peu d'espace autour */
}

.avatar-img {
  width: 100%;
  height: 100%;
  
  /* On transforme l'image carrée en rond */
  border-radius: 50%; 
  object-fit: cover;
}
```

> **Observation :** Pour l'instant, vous ne voyez pas le badge. C'est normal, il fait 0 pixel de large et n'a pas de couleur !

---

### 4. Action : Positionner le Badge (Absolute)
C'est ici que la magie opère. Nous allons forcer le badge à se placer par-dessus l'image.

```css
.status-badge {
  /* On détache le badge pour le placer librement */
  position: absolute; 
  
  /* On le place en bas à droite du parent (.avatar-wrapper) */
  bottom: 2px;
  right: 2px;
  
  /* On définit sa forme de petit cercle */
  width: 14px;
  height: 14px;
  border-radius: 50%;
  
  /* On ajoute une bordure pour qu'il se détache de l'image */
  border: 2px solid var(--surface);
}

/* On applique la couleur verte uniquement si la classe .online est présente */
.online {
  background-color: var(--success);
}
```

---

### 💡 Le saviez-vous ? (Note pour l'étudiant)
Si vous oubliez de mettre `position: relative` sur le parent (`.avatar-wrapper`), votre badge ne saura plus où se fixer. Il remontera de parent en parent jusqu'à se coller tout en bas à droite de votre **page entière** (le `body`) ! 

**Retenez bien :** L'enfant *Absolute* cherche toujours le premier parent *Relative* qu'il trouve pour s'y accrocher.

---

**Actualisez votre page !** Vous devriez voir l'avatar de l'utilisateur avec son petit témoin vert indiquant qu'il est connecté. 
---

## Exercice 1.3 — Élément fixe (bouton flottant)

### Objectif
Ajouter un bouton de chat flottant fixé en bas à droite de l'écran, qui reste visible même en scrollant.

### Étape 1 : HTML
```html
<button class="float-btn">💬 Support</button>
```

### Étape 2 : CSS à implémenter
1. Le bouton doit rester fixé en bas à droite, même quand on scroll
2. Il doit avoir un z-index élevé pour toujours rester au-dessus
3. Ajoutez un fond `var(--accent)`, du padding, des coins arrondis, et une ombre

> **Concepts à utiliser** : `position: fixed`, `bottom`, `right`, `z-index`, `box-shadow`

---

# 🛠️ Exercice 1.3 — Élément fixe (Bouton flottant)

L'objectif est de créer un bouton de support qui "flotte" au-dessus du contenu. Peu importe si l'utilisateur descend tout en bas de la page, ce bouton doit rester immobile et visible en bas à droite de son écran.

### 1. Comprendre les outils
Pour réussir cet effet, nous allons découvrir trois propriétés majeures :
* **`position: fixed`** : Contrairement à `absolute`, cet élément ne se fixe pas par rapport à un parent, mais par rapport à la **fenêtre du navigateur** (le viewport). Il ne bouge jamais, même au scroll.
* **`z-index`** : C'est l'ordre d'empilement. Imaginez des feuilles de papier : un élément avec un `z-index` de 100 sera "au-dessus" d'un élément avec un `z-index` de 1.
* **`box-shadow`** : Permet d'ajouter une ombre pour donner l'impression que le bouton décolle de la page.



---

### 2. Action : Structure HTML
Ajoutez le bouton n'importe où dans votre fichier `index.html` (généralement juste avant la fermeture de la balise `</body>`).

```html
<button class="float-btn">💬 Support</button>
```

---

### 3. Action : Fixer et styliser (CSS)
Ajoutez ce code dans `style.css`. Nous allons d'abord le placer, puis lui donner son aspect "Premium".

```css
.float-btn {
  /* ÉLÉMENT CLÉ : Le bouton ne suit plus le scroll de la page */
  position: fixed;
  
  /* On le place à 30px du bord bas et 30px du bord droit de l'écran */
  bottom: 30px;
  right: 30px;
  
  /* On s'assure qu'il passe par-dessus tout le reste */
  z-index: 1000;

  /* Style visuel */
  background-color: var(--accent);
  color: white;
  border: none;
  padding: 12px 20px;
  border-radius: 50px; /* Forme pilule */
  font-weight: bold;
  cursor: pointer;

  /* Ombre pour l'effet de flottement (X Y Flou Couleur) */
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.4);
}
```

---

### 4. Action : Ajouter un effet interactif
Pour que le bouton paraisse "vivant", ajoutons une petite transition simple.

```css
.float-btn {
  /* ... code précédent ... */
  transition: transform 0.2s ease, background-color 0.2s ease;
}

.float-btn:hover {
  background-color: #7d6cf0; /* Une version légèrement plus claire de l'accent */
  transform: scale(1.05);    /* Grossit très légèrement au survol */
}
```

---

### 👁️ Observation pour l'étudiant
> "Pour bien voir l'effet `fixed`, vous avez besoin que votre page soit assez longue pour pouvoir scroller. Si votre page est trop courte, essayez d'ajouter plusieurs fois le bloc de l'avatar de l'exercice précédent pour créer de la hauteur. Vous verrez alors que tout défile, sauf votre bouton Support !"

**Vérification :** Votre bouton est-il bien en bas à droite ? Est-ce qu'il reste là même si vous redimensionnez la fenêtre ? Si oui, bravo !


## Exercice 1.4 — Header sticky

### Objectif
Créer un header de navigation qui reste collé en haut de la page quand on scroll.

### Étape 1 : HTML
```html
<header class="main-header">
  <span class="logo">🚀 DevPulse</span>
  <nav class="nav-links">
    <a href="#dashboard">Dashboard</a>
    <a href="#users">Utilisateurs</a>
    <a href="#settings">Settings</a>
  </nav>
  <button class="btn-login">Connexion</button>
</header>
```

### Étape 2 : CSS à implémenter
1. Le header doit coller en haut de la page au scroll (`sticky`)
2. Les éléments à l'intérieur doivent être alignés horizontalement : logo à gauche, liens au centre, bouton à droite
3. Ajoutez un fond semi-transparent avec un `backdrop-filter: blur` pour un effet glassmorphism
4. Bordure fine en bas

> **Concepts à utiliser** : `position: sticky`, `top: 0`, `display: flex`, `justify-content: space-between`, `backdrop-filter`

---

## Exercice 1.5 — Z-index (empilement)

### Objectif
Créer 3 cartes empilées visuellement (comme un éventail) pour comprendre le z-index.

### Étape 1 : HTML
```html
<div class="stack-container">
  <div class="stack-card card-back">Carte arrière</div>
  <div class="stack-card card-mid">Carte milieu</div>
  <div class="stack-card card-front">Carte devant</div>
</div>
```

### Étape 2 : CSS à implémenter
1. `.stack-container` : position relative, hauteur suffisante
2. Les 3 cartes : position absolute, avec des décalages différents (`top`, `left`)
3. Chaque carte a un `z-index` croissant (1, 2, 3)
4. Ajoutez une rotation légère (`transform: rotate`) pour l'effet éventail

> **Concepts à utiliser** : `position: relative/absolute`, `z-index`, `transform: rotate()`

---

---

# 📐 MODULE 2 — Flexbox

---

## Exercice 2.1 — Navbar complète

### Objectif
Construire une barre de navigation avec logo, liens, et bouton — alignés avec Flexbox.

### Étape 1 : HTML
```html
<nav class="navbar">
  <div class="nav-brand">DevPulse</div>
  <div class="nav-menu">
    <a href="#" class="nav-link">Accueil</a>
    <a href="#" class="nav-link">Fonctionnalités</a>
    <a href="#" class="nav-link">Tarifs</a>
    <a href="#" class="nav-link">Blog</a>
  </div>
  <div class="nav-actions">
    <button class="btn-outline">Se connecter</button>
    <button class="btn-primary">Essai gratuit</button>
  </div>
</nav>
```

### Étape 2 : CSS à implémenter
1. `.navbar` : flex, alignement vertical centré, espacement entre les 3 blocs
2. `.nav-menu` : flex avec un gap entre les liens
3. `.nav-actions` : flex avec un gap entre les boutons
4. Stylisez les boutons (un outline, un plein)

> **Concepts à utiliser** : `display: flex`, `align-items: center`, `justify-content: space-between`, `gap`

---

## Exercice 2.2 — Section pricing (3 colonnes)

### Objectif
Créer une section tarification avec 3 cartes côte à côte, celle du milieu mise en avant.

### Étape 1 : HTML
```html
<section class="pricing">
  <h2>Nos tarifs</h2>
  <div class="pricing-grid">
    <div class="price-card">
      <h3>Starter</h3>
      <div class="price">9€<span>/mois</span></div>
      <ul>
        <li>5 projets</li>
        <li>1 Go stockage</li>
        <li>Support email</li>
      </ul>
      <button>Choisir</button>
    </div>
    <div class="price-card featured">
      <span class="badge-popular">Populaire</span>
      <h3>Pro</h3>
      <div class="price">29€<span>/mois</span></div>
      <ul>
        <li>Projets illimités</li>
        <li>50 Go stockage</li>
        <li>Support prioritaire</li>
        <li>API access</li>
      </ul>
      <button>Choisir</button>
    </div>
    <div class="price-card">
      <h3>Enterprise</h3>
      <div class="price">99€<span>/mois</span></div>
      <ul>
        <li>Tout illimité</li>
        <li>SSO</li>
        <li>SLA 99.9%</li>
        <li>Support dédié</li>
      </ul>
      <button>Choisir</button>
    </div>
  </div>
</section>
```

### Étape 2 : CSS à implémenter
1. `.pricing-grid` : flex, les 3 cartes côte à côte avec gap
2. Chaque `.price-card` prend la même largeur (`flex: 1`)
3. `.featured` : légèrement plus grande (`transform: scale(1.05)`), bordure accent, ombre plus forte
4. `.badge-popular` : positionné en haut de la carte (absolute)
5. Stylisez les `<li>` sans bullet par défaut

> **Concepts à utiliser** : `display: flex`, `flex: 1`, `gap`, `transform: scale()`, `list-style: none`

---

## Exercice 2.3 — Barre utilisateur (infos alignées)

### Objectif
Créer une barre d'info utilisateur : avatar + nom à gauche, statut + bouton settings à droite.

### Étape 1 : HTML
```html
<div class="user-bar">
  <div class="user-info">
    <img src="https://i.pravatar.cc/36?img=8" alt="User" class="user-avatar">
    <div class="user-details">
      <strong>Sarah Connor</strong>
      <span>Administratrice</span>
    </div>
  </div>
  <div class="user-status">
    <span class="dot-online"></span>
    <span>En ligne</span>
    <button class="btn-icon">⚙️</button>
  </div>
</div>
```

### Étape 2 : CSS à implémenter
1. `.user-bar` : flex, `space-between`, aligné au centre vertical
2. `.user-info` : flex, avatar + texte côte à côte
3. `.user-details span` : plus petit, couleur muted, affiché en bloc sous le nom
4. `.user-status` : flex, gap, items centrés
5. `.dot-online` : petit cercle vert de 8px

> **Concepts à utiliser** : `display: flex`, `align-items: center`, `gap`, `flex direction implicite`

---

---

# 📐 MODULE 3 — Grid

---

## Exercice 3.1 — Layout dashboard (sidebar + contenu)

### Objectif
Créer un layout type dashboard : sidebar fixe à gauche (250px), contenu principal à droite.

### Étape 1 : HTML
```html
<div class="dashboard">
  <aside class="sidebar">
    <h3>Menu</h3>
    <ul>
      <li><a href="#">📊 Dashboard</a></li>
      <li><a href="#">👤 Utilisateurs</a></li>
      <li><a href="#">📦 Produits</a></li>
      <li><a href="#">📈 Analytics</a></li>
      <li><a href="#">⚙️ Settings</a></li>
    </ul>
  </aside>
  <main class="main-content">
    <h1>Bienvenue sur DevPulse</h1>
    <p>Votre dashboard de monitoring.</p>
    <!-- Les stat cards iront ici -->
  </main>
</div>
```

### Étape 2 : CSS à implémenter
1. `.dashboard` : grid avec 2 colonnes — `250px` pour la sidebar, `1fr` pour le contenu
2. `.sidebar` : fond `var(--surface)`, hauteur minimum `100vh`, padding
3. Les liens du menu : sans bullet, padding vertical, hover avec fond léger
4. **Responsive** : sur mobile (< 768px), passez en une seule colonne (sidebar au-dessus)

> **Concepts à utiliser** : `display: grid`, `grid-template-columns`, `min-height: 100vh`, `@media`

---

## Exercice 3.2 — Grille de stat cards

### Objectif
À l'intérieur du `main-content`, afficher 4 cartes de statistiques en grille responsive.

### Étape 1 : HTML (à ajouter dans `.main-content`)
```html
<div class="stat-grid">
  <div class="stat-card">
    <span class="stat-label">Revenus</span>
    <span class="stat-value">€47,200</span>
    <span class="stat-change positive">+12.5%</span>
  </div>
  <div class="stat-card">
    <span class="stat-label">Utilisateurs</span>
    <span class="stat-value">3,842</span>
    <span class="stat-change positive">+8.2%</span>
  </div>
  <div class="stat-card">
    <span class="stat-label">Taux d'erreur</span>
    <span class="stat-value">0.42%</span>
    <span class="stat-change negative">+0.1%</span>
  </div>
  <div class="stat-card">
    <span class="stat-label">Uptime</span>
    <span class="stat-value">99.98%</span>
    <span class="stat-change positive">stable</span>
  </div>
</div>
```

### Étape 2 : CSS à implémenter
1. `.stat-grid` : grid auto-responsive — les cards passent de 4 colonnes à 2 puis 1 selon l'écran
2. Chaque `.stat-card` : fond surface, padding, coins arrondis, bordure
3. `.stat-value` : grande taille, gras
4. `.stat-change.positive` : vert, `.stat-change.negative` : rouge

> **Concepts à utiliser** : `grid-template-columns: repeat(auto-fill, minmax(220px, 1fr))`, `gap`

---

---

# 📱 MODULE 4 — Responsive Design

---

## Exercice 4.1 — Media queries

### Objectif
Adapter la navbar (exercice 2.1) pour mobile : les liens passent en colonne, le bouton prend toute la largeur.

### CSS à implémenter
```
@media (max-width: 768px) {
  /* 1. La navbar passe en flex-direction: column */
  /* 2. Le nav-menu s'affiche en colonne aussi */
  /* 3. Les boutons prennent toute la largeur (width: 100%) */
  /* 4. Ajoutez un gap vertical */
}
```

> **Concepts à utiliser** : `@media (max-width: ...)`, `flex-direction: column`, `width: 100%`

---

## Exercice 4.2 — Cacher/afficher selon l'écran

### Objectif
Sur mobile, cacher le texte des liens de la sidebar et ne garder que les icônes.

### Étape 1 : HTML (modifier la sidebar)
```html
<li><a href="#"><span class="icon">📊</span> <span class="link-text">Dashboard</span></a></li>
```

### Étape 2 : CSS à implémenter
1. Sur desktop (> 768px) : tout est visible
2. Sur mobile (< 768px) : `.link-text` est masqué, la sidebar se réduit à ~60px
3. Les icônes restent centrées

> **Concepts à utiliser** : `display: none`, `@media`, ajuster `grid-template-columns`

---

## Exercice 4.3 — Images responsives

### Objectif
Afficher une image de bannière qui s'adapte à toutes les tailles d'écran sans se déformer.

### Étape 1 : HTML
```html
<div class="banner">
  <img src="https://picsum.photos/1200/400" alt="Banner" class="banner-img">
</div>
```

### Étape 2 : CSS à implémenter
1. `.banner-img` : prend toute la largeur disponible (`width: 100%`)
2. Hauteur fixe (200px), l'image ne se déforme pas
3. L'image est cadrée au centre

> **Concepts à utiliser** : `width: 100%`, `height`, `object-fit: cover`, `object-position: center`

---

---

# 🎯 MODULE 5 — Gestion du contenu

---

## Exercice 5.1 — Texte tronqué (ellipsis)

### Objectif
Dans une liste de notifications, le texte long est tronqué avec "..." sur une seule ligne.

### Étape 1 : HTML
```html
<div class="notification-list">
  <div class="notif-item">
    <span class="notif-icon">🔔</span>
    <span class="notif-text">Déploiement v2.4.1 réussi sur le serveur de production EU-West après la migration</span>
    <span class="notif-time">2min</span>
  </div>
  <div class="notif-item">
    <span class="notif-icon">⚠️</span>
    <span class="notif-text">Alerte CPU : le worker-03 a dépassé 80% d'utilisation pendant plus de 5 minutes consécutives</span>
    <span class="notif-time">15min</span>
  </div>
  <div class="notif-item">
    <span class="notif-icon">❌</span>
    <span class="notif-text">Build failed sur la branche feature/auth-oauth2 — 3 tests en erreur</span>
    <span class="notif-time">1h</span>
  </div>
</div>
```

### Étape 2 : CSS à implémenter
1. `.notif-item` : flex, items centrés, gap
2. `.notif-text` : tronqué avec ellipsis si trop long (une seule ligne)
3. `.notif-time` : couleur muted, ne se réduit jamais (`flex-shrink: 0`)

> **Concepts à utiliser** : `white-space: nowrap`, `overflow: hidden`, `text-overflow: ellipsis`, `flex: 1`, `min-width: 0`

---

## Exercice 5.2 — Troncature multi-lignes

### Objectif
Afficher des descriptions de cartes limitées à 3 lignes maximum.

### Étape 1 : HTML
```html
<div class="card-desc">
  <p class="clamp-text">
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor 
    incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud 
    exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure 
    dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
  </p>
</div>
```

### Étape 2 : CSS à implémenter
1. `.clamp-text` : limité à 3 lignes, avec "..." à la fin

> **Concepts à utiliser** : `display: -webkit-box`, `-webkit-line-clamp: 3`, `-webkit-box-orient: vertical`, `overflow: hidden`

---

## Exercice 5.3 — Scroll interne (liste d'activité)

### Objectif
Créer un panel d'activité récente avec scroll interne et scrollbar custom.

### Étape 1 : HTML
```html
<div class="activity-panel">
  <h3>Activité récente</h3>
  <div class="activity-scroll">
    <div class="activity-item"><span>🔔 Déploiement v2.4.1 réussi</span><span class="badge-success">OK</span></div>
    <div class="activity-item"><span>⚠️ CPU > 80% sur worker-03</span><span class="badge-warning">Warn</span></div>
    <div class="activity-item"><span>🔔 PR #847 mergé par Alice</span><span class="badge-success">OK</span></div>
    <div class="activity-item"><span>❌ Build failed sur staging</span><span class="badge-danger">Fail</span></div>
    <div class="activity-item"><span>🔔 Migration DB terminée</span><span class="badge-success">OK</span></div>
    <div class="activity-item"><span>⚠️ SSL expire dans 7 jours</span><span class="badge-warning">Warn</span></div>
    <div class="activity-item"><span>🔔 Backup quotidien OK</span><span class="badge-success">OK</span></div>
    <div class="activity-item"><span>❌ Timeout /api/reports</span><span class="badge-danger">Fail</span></div>
    <div class="activity-item"><span>🔔 Scale up: 3→5 replicas</span><span class="badge-success">OK</span></div>
    <div class="activity-item"><span>⚠️ Rate limit client-42</span><span class="badge-warning">Warn</span></div>
  </div>
</div>
```

### Étape 2 : CSS à implémenter
1. `.activity-scroll` : hauteur max de 280px, scroll vertical
2. Custom scrollbar (fine, couleur discrète)
3. `.activity-item` : flex, space-between, bordure en bas, hover léger
4. Badges colorés (success, warning, danger)

> **Concepts à utiliser** : `max-height`, `overflow-y: auto`, `::-webkit-scrollbar`, `border-bottom`

---

---

# 🎨 MODULE 6 — Styles visuels

---

## Exercice 6.1 — Gradients et ombres

### Objectif
Créer une carte "hero" avec un dégradé en fond et une ombre portée.

### Étape 1 : HTML
```html
<div class="hero-card">
  <h2>Bienvenue sur DevPulse</h2>
  <p>Monitorez vos services en temps réel.</p>
  <button>Commencer</button>
</div>
```

### Étape 2 : CSS à implémenter
1. `.hero-card` : background gradient (du accent vers le success, en diagonale)
2. Ombre portée (`box-shadow`) avec couleur semi-transparente
3. Coins arrondis, padding confortable
4. Texte blanc

> **Concepts à utiliser** : `background: linear-gradient(135deg, ...)`, `box-shadow`, `border-radius`, `color`

---

## Exercice 6.2 — Filtres et transparence

### Objectif
Créer un overlay sombre sur une image, avec du texte par-dessus et un effet blur en arrière-plan.

### Étape 1 : HTML
```html
<div class="image-overlay-container">
  <img src="https://picsum.photos/800/300" alt="Cover" class="cover-img">
  <div class="overlay">
    <h2>Dashboard Analytics</h2>
    <p>Vue d'ensemble de vos métriques</p>
  </div>
</div>
```

### Étape 2 : CSS à implémenter
1. `.image-overlay-container` : position relative
2. `.cover-img` : prend toute la largeur, avec un `filter: blur(2px)` et `brightness(0.5)`
3. `.overlay` : positionné par-dessus l'image (absolute), centré, texte blanc

> **Concepts à utiliser** : `position: relative/absolute`, `filter: blur() brightness()`, `inset: 0`

---

---

# ⚡ MODULE 7 — Interactions

---

## Exercice 7.1 — États hover, focus, active, disabled

### Objectif
Créer une série de boutons qui montrent chaque état d'interaction.

### Étape 1 : HTML
```html
<div class="btn-showcase">
  <button class="btn btn-primary">Primary</button>
  <button class="btn btn-outline">Outline</button>
  <button class="btn btn-danger">Supprimer</button>
  <button class="btn btn-primary" disabled>Désactivé</button>
</div>
```

### Étape 2 : CSS à implémenter
1. `.btn` : styles de base (padding, radius, transition)
2. `.btn:hover` : changement de couleur, légère translation vers le haut
3. `.btn:focus` : ring outline visible (accessibilité)
4. `.btn:active` : effet "pressé" (scale légèrement réduit)
5. `.btn:disabled` : opacité réduite, curseur `not-allowed`

> **Concepts à utiliser** : `:hover`, `:focus`, `:active`, `:disabled`, `transition`, `transform`, `opacity`, `cursor`

---

## Exercice 7.2 — Inputs avec états de focus et validation

### Objectif
Styliser des inputs de formulaire avec des états visuels clairs.

### Étape 1 : HTML
```html
<div class="form-demo">
  <div class="form-group">
    <label>Email</label>
    <input type="email" placeholder="john@exemple.com" class="input">
  </div>
  <div class="form-group">
    <label>Email (erreur)</label>
    <input type="email" value="invalide" class="input input-error">
    <span class="error-msg">Adresse email invalide</span>
  </div>
  <div class="form-group">
    <label>Email (succès)</label>
    <input type="email" value="john@ok.com" class="input input-success">
    <span class="success-msg">Email vérifié ✓</span>
  </div>
</div>
```

### Étape 2 : CSS à implémenter
1. `.input` : fond sombre, bordure, transition sur la bordure
2. `.input:focus` : bordure accent + shadow ring (box-shadow avec spread)
3. `.input-error` : bordure rouge, shadow rouge
4. `.input-success` : bordure verte
5. Messages d'erreur/succès : petite taille, couleur correspondante

> **Concepts à utiliser** : `:focus`, `box-shadow: 0 0 0 3px rgba(...)`, `transition`, `border-color`

---

---

# 🎬 MODULE 8 — Animations & Transitions

---

## Exercice 8.1 — Transitions smooth (hover effects)

### Objectif
Les cards de stats (exercice 3.2) ont un hover animé : translation vers le haut + ombre.

### CSS à implémenter
1. `.stat-card` : `transition` sur transform et box-shadow
2. `.stat-card:hover` : `translateY(-4px)` + ombre plus prononcée
3. Durée : 0.2s, easing : `ease`

> **Concepts à utiliser** : `transition: property duration easing`, `transform: translateY()`, `box-shadow`

---

## Exercice 8.2 — Fade in / Slide in (animations d'entrée)

### Objectif
Les stat cards apparaissent avec une animation de fade + slide au chargement de la page.

### CSS à implémenter
1. Créer un `@keyframes fadeSlideUp` : de `opacity: 0; transform: translateY(20px)` vers `opacity: 1; transform: translateY(0)`
2. Appliquer sur `.stat-card` avec un `animation-delay` décalé pour chaque carte (staggered)
3. Durée : 0.5s, easing : `ease-out`

> **Concepts à utiliser** : `@keyframes`, `animation`, `animation-delay`, `animation-fill-mode: forwards`

---

## Exercice 8.3 — Loader spinner

### Objectif
Créer un spinner de chargement en CSS pur.

### Étape 1 : HTML
```html
<div class="loader-container">
  <div class="spinner"></div>
  <p>Chargement des données...</p>
</div>
```

### Étape 2 : CSS à implémenter
1. `.spinner` : cercle de 40px, bordure transparente sauf un côté coloré
2. Animation `@keyframes spin` : rotation de 0 à 360deg en boucle infinie
3. Centré dans son container

> **Concepts à utiliser** : `border`, `border-top-color`, `border-radius: 50%`, `@keyframes`, `animation: spin 0.8s linear infinite`

---

## Exercice 8.4 — Skeleton loading

### Objectif
Créer un skeleton (placeholder grisé animé) qui s'affiche avant le chargement du contenu.

### Étape 1 : HTML
```html
<div class="skeleton-card">
  <div class="skeleton skeleton-avatar"></div>
  <div class="skeleton skeleton-title"></div>
  <div class="skeleton skeleton-text"></div>
  <div class="skeleton skeleton-text short"></div>
</div>
```

### Étape 2 : CSS à implémenter
1. `.skeleton` : fond gris, coins arrondis
2. Animation `@keyframes shimmer` : un gradient qui glisse de gauche à droite (effet de brillance)
3. Tailles variées pour avatar (cercle), titre (large), texte (lignes)

> **Concepts à utiliser** : `@keyframes`, `background: linear-gradient`, `background-size`, `background-position`, `animation`

---

---

# 🧾 MODULE 9 — Formulaires complets

---

## Exercice 9.1 — Formulaire d'inscription complet

### Objectif
Construire un vrai formulaire d'inscription avec tous les types d'inputs stylés.

### Étape 1 : HTML
```html
<form class="register-form">
  <h2>Créer un compte</h2>

  <div class="form-row">
    <div class="form-group">
      <label>Prénom <span class="required">*</span></label>
      <input type="text" class="input" placeholder="Jean">
    </div>
    <div class="form-group">
      <label>Nom <span class="required">*</span></label>
      <input type="text" class="input" placeholder="Dupont">
    </div>
  </div>

  <div class="form-group">
    <label>Email <span class="required">*</span></label>
    <input type="email" class="input" placeholder="jean@exemple.com">
    <span class="hint">On ne partagera jamais votre email.</span>
  </div>

  <div class="form-group">
    <label>Mot de passe <span class="required">*</span></label>
    <input type="password" class="input" placeholder="Min. 8 caractères">
  </div>

  <div class="form-row">
    <div class="form-group">
      <label>Rôle</label>
      <select class="input select">
        <option>Développeur</option>
        <option>Designer</option>
        <option>Product Manager</option>
        <option>DevOps</option>
      </select>
    </div>
    <div class="form-group">
      <label>Expérience</label>
      <select class="input select">
        <option>Junior (0-2 ans)</option>
        <option>Mid (2-5 ans)</option>
        <option>Senior (5+ ans)</option>
      </select>
    </div>
  </div>

  <div class="form-group">
    <label>Bio</label>
    <textarea class="input textarea" rows="3" placeholder="Parlez-nous de vous..."></textarea>
  </div>

  <div class="form-row">
    <div class="form-group">
      <label>Stack technique</label>
      <label class="checkbox"><input type="checkbox" checked> React / Vue</label>
      <label class="checkbox"><input type="checkbox"> Node.js</label>
      <label class="checkbox"><input type="checkbox" checked> Python</label>
      <label class="checkbox"><input type="checkbox"> Go</label>
    </div>
    <div class="form-group">
      <label>Type de contrat</label>
      <label class="radio"><input type="radio" name="contract"> CDI</label>
      <label class="radio"><input type="radio" name="contract" checked> Freelance</label>
      <label class="radio"><input type="radio" name="contract"> CDD</label>
    </div>
  </div>

  <div class="form-group">
    <label class="toggle-label">
      <span class="toggle">
        <input type="checkbox" checked>
        <span class="toggle-slider"></span>
      </span>
      Recevoir les notifications par email
    </label>
  </div>

  <div class="form-actions">
    <button type="submit" class="btn btn-primary">Créer mon compte</button>
    <button type="reset" class="btn btn-outline">Annuler</button>
  </div>
</form>
```

### Étape 2 : CSS à implémenter
1. `.form-row` : grid 2 colonnes, responsive (1 colonne sur mobile)
2. `.input` : style complet (fond, bordure, padding, focus ring)
3. `.select` : custom arrow avec `appearance: none` + background-image SVG
4. `.checkbox` / `.radio` : custom avec `appearance: none`, carré/rond, checkmark en `::after`
5. `.toggle` : switch on/off avec slider animé
6. `.form-actions` : flex, gap entre les boutons
7. `.required` : rouge
8. `.hint` : petite taille, couleur muted

> **Concepts à utiliser** : tout ce qu'on a vu + `appearance: none`, `::after`, pseudo-éléments

---

---

# 📊 MODULE 10 — Tables

---

## Exercice 10.1 — Table d'utilisateurs (scroll horizontal)

### Objectif
Créer une table complète d'utilisateurs avec scroll horizontal sur mobile.

### Étape 1 : HTML
```html
<div class="table-container">
  <table class="data-table">
    <thead>
      <tr>
        <th>Utilisateur</th>
        <th>Rôle</th>
        <th>Status</th>
        <th>Dernière activité</th>
        <th>Actions</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>
          <div class="user-cell">
            <div class="table-avatar">AM</div>
            <div>
              <strong>Alice Martin</strong>
              <span>alice@dev.io</span>
            </div>
          </div>
        </td>
        <td>Admin</td>
        <td><span class="badge badge-success">Actif</span></td>
        <td>Il y a 2 min</td>
        <td><button class="btn-sm">Éditer</button></td>
      </tr>
      <tr>
        <td>
          <div class="user-cell">
            <div class="table-avatar">BK</div>
            <div>
              <strong>Bob Kumar</strong>
              <span>bob@dev.io</span>
            </div>
          </div>
        </td>
        <td>Développeur</td>
        <td><span class="badge badge-success">Actif</span></td>
        <td>Il y a 1h</td>
        <td><button class="btn-sm">Éditer</button></td>
      </tr>
      <tr>
        <td>
          <div class="user-cell">
            <div class="table-avatar">CL</div>
            <div>
              <strong>Clara Lopez</strong>
              <span>clara@dev.io</span>
            </div>
          </div>
        </td>
        <td>Designer</td>
        <td><span class="badge badge-warning">En attente</span></td>
        <td>Il y a 3 jours</td>
        <td><button class="btn-sm">Éditer</button></td>
      </tr>
      <tr>
        <td>
          <div class="user-cell">
            <div class="table-avatar">DT</div>
            <div>
              <strong>David Tanaka</strong>
              <span>david@dev.io</span>
            </div>
          </div>
        </td>
        <td>DevOps</td>
        <td><span class="badge badge-danger">Inactif</span></td>
        <td>Il y a 30 jours</td>
        <td><button class="btn-sm">Éditer</button></td>
      </tr>
    </tbody>
  </table>
</div>
```

### Étape 2 : CSS à implémenter
1. `.table-container` : `overflow-x: auto` (scroll horizontal mobile)
2. `.data-table` : width 100%, `min-width: 650px`, `border-collapse: collapse`
3. `thead` : fond surface-2, texte uppercase, petite taille, lettre-spacing
4. `td` : padding, bordure en bas, hover sur la ligne
5. `.table-avatar` : cercle coloré avec initiales
6. `.user-cell span` : email en petit, couleur muted
7. Badges : pill shape, couleurs par status

> **Concepts à utiliser** : `overflow-x: auto`, `border-collapse`, `:hover` sur `tr`, `min-width`

---

## Exercice 10.2 — Table scrollable avec header sticky

### Objectif
Une table de logs API avec scroll vertical et header qui reste collé.

### Étape 1 : HTML
```html
<div class="table-scroll-wrapper">
  <table class="data-table">
    <thead>
      <tr>
        <th>#</th>
        <th>Endpoint</th>
        <th>Méthode</th>
        <th>Status</th>
        <th>Temps (ms)</th>
      </tr>
    </thead>
    <tbody>
      <!-- Remplissez avec 15-20 lignes de données fictives -->
      <tr><td>1</td><td>/api/users</td><td>GET</td><td>200</td><td>45</td></tr>
      <tr><td>2</td><td>/api/auth/login</td><td>POST</td><td>200</td><td>95</td></tr>
      <!-- ... continuez avec plus de lignes pour activer le scroll -->
    </tbody>
  </table>
</div>
```

### Étape 2 : CSS à implémenter
1. `.table-scroll-wrapper` : `max-height: 350px`, `overflow-y: auto`
2. `thead` : `position: sticky`, `top: 0`, `z-index: 1`, fond solide (sinon transparent au scroll)
3. Scrollbar custom (fine)

> **Concepts à utiliser** : `max-height`, `overflow-y: auto`, `position: sticky`, `::-webkit-scrollbar`

---

---

# 🧩 MODULE 11 — Composants UI

---

## Exercice 11.1 — Modal / Popup

### Objectif
Créer un overlay sombre avec une modal centrée (sans JavaScript pour le style, JS juste pour le toggle).

### Étape 1 : HTML
```html
<div class="modal-overlay" id="modal">
  <div class="modal-box">
    <div class="modal-header">
      <h3>Confirmer la suppression</h3>
      <button class="modal-close" onclick="document.getElementById('modal').style.display='none'">✕</button>
    </div>
    <div class="modal-body">
      <p>Êtes-vous sûr de vouloir supprimer cet utilisateur ? Cette action est irréversible.</p>
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="document.getElementById('modal').style.display='none'">Annuler</button>
      <button class="btn btn-danger">Supprimer</button>
    </div>
  </div>
</div>

<button class="btn btn-primary" onclick="document.getElementById('modal').style.display='flex'">Ouvrir la modal</button>
```

### Étape 2 : CSS à implémenter
1. `.modal-overlay` : fixed, couvre tout l'écran (`inset: 0`), fond noir semi-transparent, flex centré, `display: none` par défaut
2. `.modal-box` : fond surface, coins arrondis, ombre, largeur max 500px
3. `.modal-header` : flex space-between, bordure en bas
4. `.modal-footer` : flex, boutons à droite, bordure en haut

> **Concepts à utiliser** : `position: fixed`, `inset: 0`, `background: rgba(0,0,0,0.6)`, `display: flex`

---

## Exercice 11.2 — Dropdown menu

### Objectif
Un bouton qui révèle un menu déroulant au hover.

### Étape 1 : HTML
```html
<div class="dropdown">
  <button class="dropdown-trigger">Mon compte ▾</button>
  <div class="dropdown-menu">
    <a href="#" class="dropdown-item">👤 Profil</a>
    <a href="#" class="dropdown-item">⚙️ Settings</a>
    <a href="#" class="dropdown-item">📊 Dashboard</a>
    <div class="dropdown-divider"></div>
    <a href="#" class="dropdown-item danger">🚪 Déconnexion</a>
  </div>
</div>
```

### Étape 2 : CSS à implémenter
1. `.dropdown` : position relative
2. `.dropdown-menu` : position absolute, caché par défaut (`opacity: 0`, `pointer-events: none`, `transform: translateY(-10px)`)
3. `.dropdown:hover .dropdown-menu` : visible, `translateY(0)`, avec transition smooth
4. `.dropdown-item` : padding, hover avec fond léger
5. `.dropdown-divider` : ligne fine horizontale

> **Concepts à utiliser** : `position: absolute`, `opacity`, `pointer-events`, `transition`, `transform`

---

## Exercice 11.3 — Tooltip

### Objectif
Au hover sur un élément, afficher un tooltip au-dessus avec une petite flèche.

### Étape 1 : HTML
```html
<div class="tooltip-demo">
  <button class="btn btn-outline tooltip-trigger" data-tooltip="Copier dans le presse-papier">📋 Copier</button>
  <button class="btn btn-outline tooltip-trigger" data-tooltip="Rafraîchir les données">🔄 Refresh</button>
  <button class="btn btn-outline tooltip-trigger" data-tooltip="Télécharger en CSV">📥 Export</button>
</div>
```

### Étape 2 : CSS à implémenter
1. `.tooltip-trigger` : position relative
2. `.tooltip-trigger::before` (le tooltip) : contenu via `attr(data-tooltip)`, position absolute au-dessus, fond sombre, texte blanc, caché par défaut
3. `.tooltip-trigger::after` (la flèche) : petit triangle CSS en dessous du tooltip
4. Au hover : les deux apparaissent avec transition

> **Concepts à utiliser** : `::before`, `::after`, `content: attr(...)`, `position: absolute`, `border` (triangle CSS)

---

## Exercice 11.4 — Tabs (onglets)

### Objectif
Créer des onglets de navigation avec contenu qui change (CSS only avec `:checked`).

### Étape 1 : HTML
```html
<div class="tabs">
  <input type="radio" name="tab" id="tab1" checked class="tab-input">
  <input type="radio" name="tab" id="tab2" class="tab-input">
  <input type="radio" name="tab" id="tab3" class="tab-input">

  <div class="tab-labels">
    <label for="tab1" class="tab-label">Général</label>
    <label for="tab2" class="tab-label">Sécurité</label>
    <label for="tab3" class="tab-label">Notifications</label>
  </div>

  <div class="tab-panels">
    <div class="tab-panel" id="panel1">Contenu des paramètres généraux...</div>
    <div class="tab-panel" id="panel2">Contenu de la sécurité : mot de passe, 2FA...</div>
    <div class="tab-panel" id="panel3">Contenu des notifications : email, push...</div>
  </div>
</div>
```

### Étape 2 : CSS à implémenter
1. `.tab-input` : caché (`display: none`)
2. `.tab-labels` : flex, bordure en bas
3. `.tab-label` : padding, curseur pointer, bordure en bas transparente
4. Quand le radio est checked, le label correspondant a une bordure colorée et un texte accent
5. Les panels sont tous cachés sauf celui qui correspond au radio checked
6. Astuce : utiliser les sélecteurs `#tab1:checked ~ .tab-panels #panel1`

> **Concepts à utiliser** : `:checked`, sélecteur `~` (general sibling), `display: none/block`, `border-bottom`

---

## Exercice 11.5 — Accordéon

### Objectif
Un accordéon FAQ qui s'ouvre/ferme sans JavaScript.

### Étape 1 : HTML
```html
<div class="accordion">
  <details class="accordion-item">
    <summary class="accordion-header">Comment déployer mon application ?</summary>
    <div class="accordion-body">
      <p>Connectez votre repo GitHub, configurez votre pipeline CI/CD, et lancez le déploiement depuis le dashboard. Le process prend en moyenne 2 minutes.</p>
    </div>
  </details>
  <details class="accordion-item">
    <summary class="accordion-header">Quels langages sont supportés ?</summary>
    <div class="accordion-body">
      <p>Nous supportons Node.js, Python, Go, Rust, Java, et PHP. Docker est aussi supporté pour les stacks custom.</p>
    </div>
  </details>
  <details class="accordion-item">
    <summary class="accordion-header">Comment contacter le support ?</summary>
    <div class="accordion-body">
      <p>Via le chat en direct (bouton en bas à droite), par email à support@devpulse.io, ou via le canal Slack dédié pour les plans Enterprise.</p>
    </div>
  </details>
</div>
```

### Étape 2 : CSS à implémenter
1. `.accordion-item` : bordure, coins arrondis, margin-bottom
2. `.accordion-header` : padding, curseur pointer, `list-style: none` (supprimer le triangle par défaut)
3. Ajouter votre propre icône flèche avec `::after` qui tourne quand ouvert (`details[open] summary::after { rotate }`)
4. `.accordion-body` : padding, animation de slide (optionnel avec `grid-template-rows`)

> **Concepts à utiliser** : `<details>/<summary>`, `list-style: none`, `::after`, `transform: rotate()`, `details[open]`

---

---

# 📋 MODULE 12 — Bonnes pratiques & Trucs pro

---

## Exercice 12.1 — Variables CSS & Theming (Dark/Light mode)

### Objectif
Ajouter un toggle dark/light mode à votre dashboard en utilisant uniquement les variables CSS.

### Étape 1 : CSS à implémenter
```css
/* Thème dark (par défaut) */
:root { ... vos variables actuelles ... }

/* Thème light */
:root.light {
  --bg: #f5f6fa;
  --surface: #ffffff;
  --surface-2: #f0f1f5;
  --border: #e0e2e9;
  --text: #1a1d27;
  --text-muted: #6b7084;
  /* accent, success, danger, warning restent les mêmes */
}
```

### Étape 2 : HTML
```html
<button onclick="document.documentElement.classList.toggle('light')">🌗 Toggle Theme</button>
```

> **Concepts à utiliser** : variables CSS, `.classList.toggle()`, tout le design s'adapte automatiquement si vous avez bien utilisé `var(--xxx)` partout

---

## Exercice 12.2 — Classes utilitaires

### Objectif
Créer un petit set de classes utilitaires (inspiration Tailwind) pour les cas rapides.

### CSS à implémenter
```css
/* Spacing */
.mt-1 { margin-top: 0.5rem; }
.mt-2 { margin-top: 1rem; }
.mb-1 { margin-bottom: 0.5rem; }
.p-1 { padding: 0.5rem; }
.p-2 { padding: 1rem; }

/* Flex raccourcis */
.flex { display: flex; }
.flex-center { display: flex; align-items: center; justify-content: center; }
.flex-between { display: flex; align-items: center; justify-content: space-between; }
.gap-1 { gap: 0.5rem; }
.gap-2 { gap: 1rem; }

/* Text */
.text-muted { color: var(--text-muted); }
.text-sm { font-size: 0.85rem; }
.text-center { text-align: center; }
.font-bold { font-weight: 700; }

/* Visibility */
.hidden { display: none; }
.sr-only { position: absolute; width: 1px; height: 1px; overflow: hidden; clip: rect(0,0,0,0); }
```

> **Concepts à utiliser** : classes réutilisables, composition, DRY

---

## Exercice 12.3 — Petits trucs qui font la différence

### Objectif
Ajoutez ces micro-détails à votre projet pour un rendu "pro".

### CSS à implémenter
```css
/* 1. Curseur sur les éléments cliquables */
/* Appliquez cursor: pointer sur TOUT ce qui est cliquable */

/* 2. Sélection de texte */
/* Empêcher la sélection sur les labels de tabs, boutons */
.btn, .tab-label { user-select: none; }

/* 3. Aspect ratio pour les images de cards */
.card-image { aspect-ratio: 16/9; object-fit: cover; }

/* 4. Smooth scroll global */
html { scroll-behavior: smooth; }

/* 5. Transition globale sur les liens */
a { transition: color 0.2s ease; }

/* 6. Focus visible (accessibilité moderne) */
:focus-visible { outline: 2px solid var(--accent); outline-offset: 2px; }
:focus:not(:focus-visible) { outline: none; }
```

---

---

# 🏁 Projet final — Assembler le tout

### Objectif
Assemblez tous les exercices dans un dashboard complet et fonctionnel :

1. **Header sticky** avec navbar, logo, liens, bouton login, toggle theme
2. **Layout** sidebar + contenu principal (Grid)
3. **Sidebar** avec menu icônes + texte, responsive (icônes seules sur mobile)
4. **Stat cards** en grille responsive avec animations d'entrée
5. **Table d'utilisateurs** avec scroll horizontal, badges, avatars
6. **Panel d'activité** scrollable avec scrollbar custom
7. **Formulaire** de création d'utilisateur dans une modal
8. **Dropdown** dans le header pour le menu utilisateur
9. **Tabs** dans le contenu principal (Dashboard / Users / Settings)
10. **Bouton flottant** de support en bas à droite
11. **Dark/Light mode** toggle

### Critères d'évaluation
- ✅ Aucun framework CSS utilisé (tout en CSS pur)
- ✅ Responsive (fonctionne sur mobile, tablette, desktop)
- ✅ Variables CSS utilisées partout (pas de couleurs en dur)
- ✅ Transitions/animations fluides
- ✅ Accessibilité (focus visible, contrastes, curseurs)
- ✅ Code propre et organisé (sections commentées)

---

> **Rappel** : ce TP n'est pas un exercice de JavaScript. Le JS est utilisé uniquement pour les toggles (modal, theme). Tout le styling est en CSS pur.
