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

# 🛠️ Exercice 1.4 — Le Header "Sticky" (Collant)

L'objectif est de créer une barre de navigation qui reste accessible en haut de l'écran, même quand on fait défiler la page vers le bas. Nous allons aussi lui donner un look moderne appelé **"Glassmorphism"** (effet de verre dépoli).

### 1. Comprendre les outils
* **`position: sticky`** : C'est un mélange entre `relative` et `fixed`. L'élément défile normalement jusqu'à ce qu'il touche le bord de l'écran (défini par `top: 0`), puis il y reste "collé".
* **Flexbox (`space-between`)** : On va demander au navigateur de distribuer l'espace automatiquement pour pousser le logo à gauche, les liens au milieu et le bouton à droite.
* **`backdrop-filter: blur()`** : C'est une propriété moderne qui permet de flouter ce qui se trouve *derrière* l'élément. Cela crée l'effet "vitre" très utilisé par Apple ou Microsoft.

---

# 🛠️ Exercice 1.5 — Le Z-Index (L'empilement)

Jusqu'à présent, nous avons travaillé en 2D (haut, bas, gauche, droite). Le **z-index**, c'est la troisième dimension. C'est ce qui permet de décider quel élément passe "par-dessus" l'autre, comme si vous empiliez des cartes de visite sur une table.

### 1. Comprendre les outils
* **`z-index`** : C'est un numéro d'ordre. Plus le chiffre est élevé, plus l'élément est proche de vous (donc au-dessus des autres). *Note : le z-index ne fonctionne que sur les éléments dont la position n'est pas "static" (donc absolute, relative, fixed, ou sticky).*
* **`transform: rotate(deg)`** : Permet de faire pivoter un élément. On utilise `deg` pour degrés (ex: `5deg` ou `-5deg`).
* **Positionnement absolu multiple** : En mettant plusieurs éléments en `absolute` dans un même parent `relative`, ils vont tous s'empiler au même endroit par défaut.



---

### 2. Action : Structure HTML
Ajoutez ce bloc dans votre fichier `index.html`. Nous créons un conteneur avec trois cartes à l'intérieur.

```html
<div class="stack-container">
  <div class="stack-card card-back">Carte arrière (Z: 1)</div>
  <div class="stack-card card-mid">Carte milieu (Z: 2)</div>
  <div class="stack-card card-front">Carte devant (Z: 3)</div>
</div>
```

---

### 3. Action : Créer l'empilement (CSS)
Ouvrez `style.css`. Nous allons d'abord superposer les cartes, puis les décaler une par une.

```css
.stack-container {
  position: relative;
  height: 300px;
  margin: 50px auto;
  width: 200px;
}

.stack-card {
  position: absolute; /* Elles se superposent toutes au même point */
  width: 200px;
  height: 250px;
  border-radius: var(--radius);
  display: flex;
  align-items: center;
  justify-content: center;
  font-weight: bold;
  box-shadow: 0 5px 15px rgba(0,0,0,0.3);
}
```

---

### 4. Action : Gérer la profondeur et la rotation
Maintenant, donnons à chaque carte sa place dans la "pile" et une légère inclinaison.

```css
.card-back {
  background-color: #34495e;
  z-index: 1; /* Le plus bas */
  top: 0;
  left: 0;
  transform: rotate(-10deg);
}

.card-mid {
  background-color: var(--accent);
  z-index: 2; /* Au milieu */
  top: 10px;
  left: 20px;
  transform: rotate(-5deg);
}

.card-front {
  background-color: #fff;
  color: var(--bg);
  z-index: 3; /* Le plus haut, au-dessus de tout le monde */
  top: 20px;
  left: 40px;
  transform: rotate(0deg);
}
```

---

### 👁️ Observation pour l'étudiant
> "Regardez bien comment les cartes se chevauchent. Essayez d'inverser les chiffres du `z-index` (mettez 10 à la carte arrière et 1 à la carte devant). Que se passe-t-il ? La carte sombre passera devant la blanche, même si elle a été écrite avant dans le code HTML !"

**Vérification :**
1. Voyez-vous bien l'effet "éventail" ?
2. Est-ce que la carte blanche est bien au-dessus des deux autres ?

**C'est la fin du Module 1 sur le Positionnement !**

---

### 2. Action : Structure HTML
Ajoutez ce bloc tout en haut, juste après l'ouverture de votre balise `<body>` dans `index.html`.

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

---

### 3. Action : Rendre le Header "Collant" (CSS)
Ouvrez `style.css` et ajoutez les styles de positionnement :

```css
.main-header {
  /* ÉLÉMENT CLÉ : Se colle au sommet quand on scroll */
  position: sticky;
  top: 0;
  z-index: 100; /* Doit être au-dessus du contenu mais sous le bouton flottant */

  /* Alignement des 3 groupes d'éléments */
  display: flex;
  justify-content: space-between;
  align-items: center;

  /* Espacement et taille */
  padding: 15px 5%;
  height: 70px;
}
```

> **À ce stade :** Le header est en haut, mais on ne voit pas encore l'effet de transparence.

---

### 4. Action : L'effet "Glassmorphism"
Ajoutons le style visuel pour créer cet effet de transparence floutée.

```css
.main-header {
  /* ... code précédent ... */
  
  /* Fond semi-transparent (couleur de surface avec opacité 0.8) */
  background-color: rgba(26, 29, 39, 0.8);
  
  /* LE FLOU : On floute ce qui passe derrière le header */
  backdrop-filter: blur(10px);
  
  /* Bordure fine en bas pour délimiter */
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

/* Style rapide pour les liens */
.nav-links a {
  color: var(--text-muted);
  text-decoration: none;
  margin: 0 15px;
  font-weight: 500;
  transition: color 0.3s;
}

.nav-links a:hover {
  color: var(--accent);
}
```

---

### 👁️ Observation pour l'étudiant
> "Pour tester le mode **Sticky**, scrollez votre page vers le bas (assurez-vous d'avoir assez de contenu en dessous, comme vos exercices précédents). Vous remarquerez que le header reste fixé en haut et que, grâce au `blur`, le contenu qui passe derrière devient flou. C'est l'effet 'verre' !"

**Vérification :**
1. Le logo est-il bien à gauche et le bouton à droite ? 
2. Le texte derrière le header devient-il flou quand vous scrollez ?


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

# 🛠️ Exercice 2.2 — Section Pricing (Flexbox & Mise en avant)

L'objectif est d'aligner trois offres tarifaires. Nous allons apprendre à rendre des colonnes parfaitement égales et à utiliser un effet de "zoom" sur l'offre la plus intéressante pour l'utilisateur.

### 1. Comprendre les outils
* **`flex: 1`** : C'est une propriété "magique". Appliquée aux enfants d'un conteneur Flex, elle leur dit : "Prenez tout l'espace disponible et partagez-le de manière égale". Ainsi, vos 3 cartes auront exactement la même largeur.
* **`transform: scale(1.05)`** : Permet d'agrandir un élément. Ici, on augmente la taille de la carte centrale de 5% pour qu'elle dépasse légèrement les autres.
* **`list-style: none`** : Indispensable pour enlever les petits points noirs (`bullets`) par défaut des listes `<ul>`.
* **`position: absolute` (Rappel)** : Nous allons l'utiliser à nouveau pour placer le badge "Populaire" sur le bord de la carte.



---

### 2. Action : Structure HTML
Ajoutez ce bloc dans votre fichier `index.html`. Notez la classe spéciale `featured` sur la deuxième carte.

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
      </ul>
      <button class="btn-outline">Choisir</button>
    </div>

    <div class="price-card featured">
      <span class="badge-popular">Populaire</span>
      <h3>Pro</h3>
      <div class="price">29€<span>/mois</span></div>
      <ul>
        <li>Projets illimités</li>
        <li>50 Go stockage</li>
        <li>Support prioritaire</li>
      </ul>
      <button class="btn-primary">Choisir</button>
    </div>

    <div class="price-card">
      <h3>Enterprise</h3>
      <div class="price">99€<span>/mois</span></div>
      <ul>
        <li>Tout illimité</li>
        <li>SSO & Sécurité</li>
        <li>Support dédié</li>
      </ul>
      <button class="btn-outline">Choisir</button>
    </div>
  </div>
</section>
```

---

### 3. Action : Aligner les colonnes (CSS)
Dans `style.css`, nous allons créer la grille flexible :

```css
.pricing-grid {
  display: flex;
  gap: 30px;
  align-items: center; /* Aligne les cartes sur leur axe central */
  max-width: 1000px;
  margin: 40px auto;
  padding: 20px;
}

.price-card {
  flex: 1; /* Chaque carte prend 1 part égale de l'espace */
  background-color: var(--surface);
  padding: 30px;
  border-radius: var(--radius);
  text-align: center;
  position: relative; /* Pour le badge absolute */
  border: 1px solid rgba(255,255,255,0.05);
}
```

---

### 4. Action : Mise en avant et détails
Ajoutons le style pour la carte "Pro" et nettoyons les listes.

```css
/* La carte mise en avant */
.price-card.featured {
  transform: scale(1.05); /* Agrandissement */
  border: 2px solid var(--accent);
  box-shadow: 0 10px 30px rgba(108, 92, 231, 0.2);
  z-index: 10; /* Pour passer par-dessus les ombres des voisines */
}

/* Le badge "Populaire" */
.badge-popular {
  position: absolute;
  top: -12px;
  left: 50%;
  transform: translateX(-50%); /* Centre le badge parfaitement */
  background-color: var(--accent);
  font-size: 12px;
  padding: 4px 12px;
  border-radius: 20px;
  font-weight: bold;
}

/* Nettoyage de la liste */
.price-card ul {
  list-style: none;
  margin: 20px 0;
  color: var(--text-muted);
}

.price-card li {
  margin-bottom: 10px;
}

.price {
  font-size: 2rem;
  font-weight: bold;
  margin: 15px 0;
}
```

---

### 👁️ Observation pour l'étudiant
> "Regardez la différence de hauteur et de taille entre la carte 'Pro' et les autres. C'est le `scale(1.05)` qui crée cet effet de relief. Essayez de passer la valeur à `scale(1.2)` pour voir l'effet s'accentuer (mais attention, ça risque de déborder !)."

**Vérification :**
1. Les 3 cartes ont-elles bien la même largeur ?
2. Le badge "Populaire" est-il bien à cheval sur le bord haut de la carte centrale ?
3. Les puces de listes ont-elles bien disparu ?

---

# 🛠️ Exercice 2.1 — Navbar complète (Flexbox)

Dans cet exercice, nous allons structurer une barre de navigation professionnelle. Au lieu de calculer des pixels pour espacer les éléments, nous allons laisser le navigateur faire les calculs pour nous.

### 1. Comprendre les outils
* **`display: flex`** : Transforme le conteneur en une ligne (par défaut).
* **`justify-content: space-between`** : C'est l'outil ultime pour les barres de navigation. Il pousse le premier élément à gauche, le dernier à droite, et répartit le reste au milieu.
* **`gap`** : C'est la propriété moderne qui remplace les `margin-right`. Elle définit l'espace exact *entre* les enfants d'un conteneur Flex, sans en ajouter à l'extérieur.
* **`align-items: center`** : Assure que le logo, les liens et les boutons sont tous parfaitement alignés sur la même ligne horizontale, même s'ils n'ont pas la même hauteur.



---

### 2. Action : Structure HTML
Ajoutez ce code dans votre `index.html`. Remarquez qu'il y a trois groupes distincts : le **Brand**, le **Menu**, et les **Actions**.

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

---

### 3. Action : Aligner la barre (CSS)
Ajoutez ceci dans `style.css`. Regardez comment trois lignes de code organisent toute la structure :

```css
.navbar {
  display: flex;
  justify-content: space-between; /* Espace entre les 3 blocs */
  align-items: center;            /* Aligne tout verticalement */
  
  padding: 1rem 5%;
  background-color: var(--surface);
  border-bottom: 1px solid rgba(255,255,255,0.1);
}

/* On organise l'intérieur du menu et des actions */
.nav-menu, .nav-actions {
  display: flex;
  gap: 20px; /* L'espace magique entre les éléments */
  align-items: center;
}
```

---

### 4. Action : Styliser les composants
Pour que la barre ressemble à un vrai produit SaaS, appliquons des styles aux liens et aux boutons.

```css
.nav-link {
  text-decoration: none;
  color: var(--text-muted);
  font-weight: 500;
  transition: color 0.3s;
}

.nav-link:hover {
  color: var(--accent);
}

/* Bouton avec bordure uniquement */
.btn-outline {
  background: transparent;
  border: 1px solid var(--accent);
  color: var(--accent);
  padding: 8px 16px;
  border-radius: var(--radius);
  cursor: pointer;
}

/* Bouton plein (Primary) */
.btn-primary {
  background-color: var(--accent);
  border: none;
  color: white;
  padding: 8px 16px;
  border-radius: var(--radius);
  cursor: pointer;
}
```

---

### 👁️ Observation pour l'étudiant
> "Essayez de supprimer `justify-content: space-between` de la classe `.navbar`. Vous verrez que tous vos blocs se collent à gauche. Remettez-le, puis changez la taille de votre fenêtre : l'espace entre le logo et le menu s'adapte automatiquement. C'est la magie du **Flex**."

**Vérification :**
1. Votre logo est-il bien à gauche et vos boutons à droite ?
2. Y a-t-il bien un espace régulier entre vos liens grâce au `gap` ?


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

# 🛠️ Exercice 2.3 — Barre utilisateur (Flexbox imbriqué)

L'objectif est d'aligner parfaitement des éléments qui ont des tailles différentes (une image, du texte sur deux lignes et des icônes). Nous allons apprendre à utiliser Flexbox pour le conteneur principal, mais aussi pour les petits groupes à l'intérieur.

### 1. Comprendre les outils
* **L'imbrication Flex** : On peut mettre une Flexbox dans une autre Flexbox. Le parent gère les deux grands blocs (gauche/droite), et les blocs enfants gèrent l'alignement de ce qu'ils contiennent (image/texte).
* **Alignement vertical** : Avec `align-items: center`, on s'assure que le petit point vert est bien en face du texte "En ligne" et que l'avatar est bien aligné avec le nom.
* **Le texte en bloc** : Par défaut, les balises `<span>` se mettent côte à côte. On va forcer le rôle de l'administratrice à passer sous son nom.



---

### 2. Action : Structure HTML
Ajoutez ce bloc dans votre fichier `index.html`. Notez comment les éléments sont groupés en deux familles : `.user-info` et `.user-status`.

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

---

### 3. Action : Aligner les deux blocs (CSS)
On commence par la structure globale. On veut que les infos soient à gauche et le statut à droite.

```css
.user-bar {
  display: flex;
  justify-content: space-between; /* Écarte les deux groupes */
  align-items: center;            /* Centre tout verticalement */
  
  background-color: var(--surface);
  padding: 12px 20px;
  border-radius: var(--radius);
  margin: 20px 0;
}
```

---

### 4. Action : Aligner l'intérieur des blocs
Maintenant, on s'occupe de l'alignement interne de chaque groupe.

```css
/* Alignement du groupe de gauche (Photo + Nom) */
.user-info {
  display: flex;
  align-items: center;
  gap: 12px;
}

.user-avatar {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  object-fit: cover;
}

/* On force le titre à passer à la ligne */
.user-details span {
  display: block; 
  font-size: 0.8rem;
  color: var(--text-muted);
}

/* Alignement du groupe de droite (Point vert + Texte + Bouton) */
.user-status {
  display: flex;
  align-items: center;
  gap: 10px;
}

.dot-online {
  width: 8px;
  height: 8px;
  background-color: var(--success);
  border-radius: 50%;
}

.btn-icon {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 1.2rem;
  padding: 5px;
}
```

---

### 👁️ Observation pour l'étudiant
> "Regardez le groupe de gauche (`.user-info`). Si vous enlevez `display: flex`, l'image et le texte vont s'empiler bizarrement. En l'ajoutant, ils se rangent sagement côte à côte. Flexbox est l'outil indispensable pour créer des composants 'en ligne' propres."

**Vérification :**
1. L'avatar est-il bien à gauche du nom de Sarah ?
2. Le statut "En ligne" est-il bien à droite de la barre ?
3. Le petit point vert est-il bien centré verticalement par rapport au texte ?

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

# 🛠️ Exercice 3.1 — Layout Dashboard (CSS Grid)

L'objectif est de diviser votre écran en deux grandes zones : une barre latérale (Sidebar) à gauche qui garde une taille fixe, et une zone de contenu (Main) à droite qui occupe tout l'espace restant.

### 1. Comprendre les outils
* **`display: grid`** : Active le mode grille. Contrairement à Flexbox, vous dessinez d'abord les colonnes et les lignes, puis vous y placez le contenu.
* **`grid-template-columns: 250px 1fr`** : C'est ici que l'on définit nos colonnes. La première fait **250px** (fixe). La deuxième fait **1fr** (fraction), ce qui signifie qu'elle prend "1 part de tout l'espace qui reste".
* **`@media (max-width: 768px)`** : C'est une "Media Query". Elle permet de dire au navigateur : "Si l'écran est plus petit que 768px (tablettes/mobiles), change le style CSS".



---

### 2. Action : Structure HTML
Ajoutez ce bloc dans votre fichier `index.html`. C'est l'organisation classique d'une application SaaS.

```html
<div class="dashboard">
  <aside class="sidebar">
    <h3>DevPulse Menu</h3>
    <ul class="sidebar-menu">
      <li><a href="#">📊 Dashboard</a></li>
      <li><a href="#">👤 Utilisateurs</a></li>
      <li><a href="#">📦 Produits</a></li>
      <li><a href="#">📈 Analytics</a></li>
      <li><a href="#">⚙️ Settings</a></li>
    </ul>
  </aside>

  <main class="main-content">
    <h1>Bienvenue sur DevPulse</h1>
    <p>Votre dashboard de monitoring est prêt.</p>
    </main>
</div>
```

---

### 3. Action : Créer la Grille (CSS)
Ouvrez `style.css`. Nous allons définir la structure pour les grands écrans (ordinateurs).

```css
.dashboard {
  display: grid;
  /* La sidebar fait 250px, le contenu prend le reste (1fr) */
  grid-template-columns: 250px 1fr;
  min-height: 100vh;
}

.sidebar {
  background-color: var(--surface);
  padding: 30px 20px;
  border-right: 1px solid rgba(255,255,255,0.05);
}

.main-content {
  padding: 40px;
  background-color: var(--bg);
}

/* Style du menu sidebar */
.sidebar-menu {
  list-style: none;
  margin-top: 30px;
}

.sidebar-menu li a {
  display: block;
  padding: 12px;
  color: var(--text-muted);
  text-decoration: none;
  border-radius: var(--radius);
  transition: all 0.3s;
}

.sidebar-menu li a:hover {
  background-color: rgba(255,255,255,0.05);
  color: var(--accent);
}
```

---

### 4. Action : Rendre le Layout Responsive
Le problème d'une colonne fixe de 250px, c'est que sur mobile, elle prend toute la place. Ajoutons une règle pour les petits écrans.

```css
@media (max-width: 768px) {
  .dashboard {
    /* Sur mobile, on empile les colonnes l'une sur l'autre */
    grid-template-columns: 1fr;
  }

  .sidebar {
    min-height: auto; /* La sidebar ne fait plus toute la hauteur */
    border-right: none;
    border-bottom: 1px solid rgba(255,255,255,0.05);
  }
}
```

---

### 👁️ Observation pour l'étudiant
> "Jouez avec la largeur de votre navigateur. Quand vous passez en dessous d'une certaine taille, vous voyez la sidebar passer au-dessus du contenu ? C'est le principe du **Responsive Design**. En une seule ligne de CSS (`grid-template-columns: 1fr`), on a totalement changé l'apparence du site pour les mobiles."

**Vérification :**
1. Sur ordinateur, avez-vous bien le menu à gauche et le texte à droite ?
2. Le menu sur la gauche prend-il bien toute la hauteur de la page (`100vh`) ?
3. Les liens changent-ils de couleur au survol ?


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

# 🛠️ Exercice 3.2 — Grille de "Stat Cards" (Grid Responsive)

L'objectif est d'afficher les indicateurs clés (KPI) de DevPulse. Nous voulons que les cartes se rangent intelligemment : sur une seule ligne si l'écran est large, mais qu'elles "sautent" à la ligne suivante si l'espace vient à manquer.

### 1. Comprendre les outils
* **`repeat(auto-fill, ...)`** : On demande au navigateur de créer automatiquement autant de colonnes que possible sans déborder du conteneur.
* **`minmax(220px, 1fr)`** : C'est la règle de survie de la carte. Elle ne peut jamais faire moins de **220px** de large. Si elle a de la place, elle s'étire pour prendre **1 part (1fr)** de l'espace restant.
* **L'imbrication Flex** : Même si les cartes sont placées par une **Grid**, l'intérieur de chaque carte (le texte) sera géré par **Flexbox** pour un alignement vertical facile.



---

### 2. Action : Structure HTML
Ajoutez ce bloc à l'intérieur de la balise `<main class="main-content">` (juste après le paragraphe de bienvenue) :

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

---

### 3. Action : Créer la grille intelligente (CSS)
Ajoutez ceci dans `style.css`. Regardez bien la ligne `grid-template-columns`, c'est elle qui fait tout le travail.

```css
.stat-grid {
  display: grid;
  /* La formule magique pour le responsive automatique */
  grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
  gap: 20px;
  margin-top: 30px;
}

.stat-card {
  background-color: var(--surface);
  padding: 20px;
  border-radius: var(--radius);
  border: 1px solid rgba(255, 255, 255, 0.05);
  
  /* On utilise Flexbox pour empiler le texte verticalement */
  display: flex;
  flex-direction: column;
  gap: 10px;
}
```

---

### 4. Action : Styliser les données
On donne de l'importance aux chiffres et on colore les indicateurs de tendance.

```css
.stat-label {
  color: var(--text-muted);
  font-size: 0.9rem;
  text-transform: uppercase;
  letter-spacing: 1px;
}

.stat-value {
  font-size: 1.8rem;
  font-weight: bold;
  color: var(--text);
}

.stat-change {
  font-size: 0.85rem;
  font-weight: 600;
  padding: 4px 8px;
  border-radius: 4px;
  width: fit-content; /* Le fond s'adapte à la taille du texte */
}

.positive {
  color: var(--success);
  background-color: rgba(0, 184, 148, 0.1);
}

.negative {
  color: #ff7675; /* Rouge */
  background-color: rgba(255, 118, 117, 0.1);
}
```

---

### 👁️ Observation pour l'étudiant
> "Redimensionnez lentement la largeur de votre fenêtre. Vous allez voir les cartes passer de 4 à 3, puis 2, puis 1 colonne de manière fluide. Nous n'avons pas écrit une seule Media Query pour cela ! C'est la force de la fonction `minmax` associée au `auto-fill`."

**Vérification :**
1. Les cartes sont-elles bien alignées avec un espace (`gap`) entre elles ?
2. Le montant des revenus est-il bien plus gros que le libellé ?
3. Les badges +12.5% et +0.1% ont-ils bien des couleurs différentes ?

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

# 🛠️ Exercice 4.1 — Les Media Queries (Adaptation Mobile)

L'objectif est de transformer notre barre de navigation horizontale (conçue pour les ordinateurs) en un menu vertical adapté aux petits écrans des smartphones.

### 1. Comprendre les outils
* **`@media (max-width: 768px)`** : C'est une condition. On dit au navigateur : "Si la largeur de l'écran est inférieure ou égale à 768px, applique ces nouvelles règles CSS".
* **`flex-direction: column`** : Par défaut, Flexbox aligne en ligne (`row`). En passant en `column`, on empile les éléments les uns sous les autres.
* **`width: 100%`** : Sur mobile, les éléments étroits sont difficiles à cliquer. On force les boutons à occuper toute la largeur disponible pour une meilleure ergonomie (UX).



---

### 2. Action : Identifier la cible
Nous allons modifier la structure que nous avons créée à l'**Exercice 2.1** (la `.navbar`). Assurez-vous d'avoir bien ce code HTML dans votre page.

---

### 3. Action : Écrire la Media Query (CSS)
Ajoutez ce bloc **tout à la fin** de votre fichier `style.css`. 

> **Important :** Les Media Queries se placent toujours après les styles par défaut pour pouvoir les "écraser" correctement.

```css
@media (max-width: 768px) {
  .navbar {
    /* On empile les 3 blocs (Logo, Menu, Actions) */
    flex-direction: column;
    gap: 20px;
    padding: 20px;
    text-align: center;
  }

  .nav-menu {
    /* Les liens passent aussi les uns sous les autres */
    flex-direction: column;
    gap: 15px;
  }

  .nav-actions {
    /* Les boutons s'empilent et prennent toute la place */
    flex-direction: column;
    width: 100%;
    gap: 10px;
  }

  .nav-actions button {
    width: 100%; /* Boutons larges pour les pouces */
  }
}
```

---

### 👁️ Observation pour l'étudiant
> "Ouvrez l'inspecteur de votre navigateur (F12), activez le mode 'Responsive' (l'icône de téléphone) et réduisez la largeur. Vous allez voir un point de bascule précis à 768px. À cet instant, votre menu 'saute' d'un design horizontal à un design vertical. C'est ainsi que l'on crée des sites **Mobile-First**."

**Vérification :**
1. Est-ce que les liens du menu sont bien les uns sous les autres sur petit écran ?
2. Les boutons "Se connecter" et "Essai gratuit" occupent-ils bien toute la largeur de la boîte ?
3. Le design reste-t-il propre sur grand écran (il ne doit pas avoir changé) ?

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

# 🛠️ Exercice 4.2 — Cacher/Afficher (Responsive Sidebar)

L'objectif est de transformer notre large barre latérale en une "mini-barre" d'icônes sur mobile. Nous allons apprendre à faire disparaître des éléments précis du HTML sans les supprimer.

### 1. Comprendre les outils
* **`display: none`** : C'est la propriété radicale. Elle retire l'élément de la page. Il est toujours dans le code HTML, mais le navigateur fait comme s'il n'existait pas (il ne prend plus de place).
* **Réduction de la grille** : Nous allons modifier la structure `grid` du dashboard que nous avons créée à l'exercice 3.1 pour rétrécir la première colonne.
* **`text-align: center`** ou **Flexbox** : Pour que les icônes ne flottent pas bizarrement une fois le texte disparu, il faudra s'assurer qu'elles restent bien au milieu de la petite barre.

---

### 2. Action : Modifier le HTML
Pour pouvoir cibler uniquement le texte, nous devons l'envelopper dans une balise `<span>`. Modifiez vos liens dans la `sidebar` comme ceci :

```html
<li>
  <a href="#">
    <span class="icon">📊</span> 
    <span class="link-text">Dashboard</span>
  </a>
</li>
```

---

### 3. Action : Ajuster le CSS Mobile
Nous allons retourner dans la **Media Query** créée à l'étape précédente (`@media (max-width: 768px)`) pour ajouter ces instructions spécifiques à la sidebar.

```css
@media (max-width: 768px) {
  /* 1. On réduit la première colonne de la grille de 250px à 70px */
  .dashboard {
    grid-template-columns: 70px 1fr;
  }

  /* 2. On cache le texte des liens */
  .link-text {
    display: none;
  }

  /* 3. On centre les icônes dans la sidebar */
  .sidebar {
    padding: 20px 0; /* On réduit le padding latéral */
    text-align: center;
  }

  .sidebar-menu li a {
    padding: 15px 0;
    font-size: 1.5rem; /* On grossit un peu l'icône pour le tactile */
  }
}
```

---

### 👁️ Observation pour l'étudiant
> "Regardez votre dashboard sur un écran large, puis réduisez la fenêtre. Vous allez voir la sidebar se rétracter d'un coup. Le texte 'Dashboard', 'Utilisateurs', etc., disparaît totalement, ne laissant que les émojis. C'est exactement ce que font des applications comme Slack ou Discord pour s'adapter aux petits écrans !"

**Vérification :**
1. Sur mobile, la sidebar est-elle devenue une fine bande à gauche ?
2. Les icônes sont-elles bien visibles et centrées ?
3. Le texte réapparaît-il bien dès que vous agrandissez la fenêtre ?

---

**Astuce pédagogique :** Expliquez à vos étudiants que `display: none` est différent de `visibility: hidden`. `hidden` cache l'élément mais laisse un trou vide, alors que `none` compacte tout comme si l'élément n'était plus là.


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

# 🛠️ Exercice 4.3 — Images responsives (Object-fit)

L'objectif est d'afficher une bannière élégante dans notre dashboard. Peu importe que l'utilisateur soit sur un écran ultra-large ou sur un petit téléphone, l'image doit toujours remplir son espace proprement, comme un papier peint bien posé.

### 1. Comprendre les outils
* **`width: 100%`** : L'image s'adapte à la largeur de son conteneur parent.
* **`height: 200px`** : On impose une hauteur fixe pour que la bannière ne prenne pas toute la page sur mobile.
* **`object-fit: cover`** : C'est la propriété "magique". Elle dit à l'image : "Remplis tout le cadre de 200px. Si tu es trop grande, coupe tes bords, mais ne te déforme jamais".
* **`object-position: center`** : Indique que si l'image doit être coupée, on veut garder la partie centrale visible.



---

### 2. Action : Structure HTML
Ajoutez ce bloc au début de votre `<main class="main-content">`, juste avant vos cartes de statistiques.

```html
<div class="banner">
  <img src="https://picsum.photos/1200/400" alt="Banner" class="banner-img">
</div>
```

---

### 3. Action : Rendre l'image intelligente (CSS)
Ajoutez ces règles dans votre fichier `style.css` :

```css
.banner {
  width: 100%;
  margin-bottom: 30px;
  border-radius: var(--radius);
  overflow: hidden; /* Pour que l'image respecte les coins arrondis du parent */
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
}

.banner-img {
  display: block; /* Supprime l'espace vide sous l'image */
  width: 100%;
  height: 200px; /* On impose la hauteur de la bannière */
  
  /* ÉLÉMENT CLÉ : Empêche la déformation */
  object-fit: cover;
  
  /* On centre la vue sur le milieu de l'image */
  object-position: center;
}
```

---

### 👁️ Observation pour l'étudiant
> "Amusez-vous à redimensionner votre navigateur. Vous allez remarquer que l'image semble se 'recadrer' toute seule. Elle ne devient jamais toute mince ou toute écrasée. Essayez de remplacer `cover` par `contain` pour voir la différence : avec `contain`, l'image essaie de se montrer en entier, ce qui laisse souvent des espaces vides sur les côtés."

**Vérification :**
1. L'image occupe-t-elle bien toute la largeur de votre zone de contenu ?
2. Fait-elle bien toujours 200px de haut, même sur mobile ?
3. Les coins de la bannière sont-ils bien arrondis ?

---

**C'est la fin du Module 4 sur le Responsive !** Vos étudiants savent maintenant créer des interfaces qui s'adaptent à tous les supports. 


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

# 🛠️ Exercice 5.1 — Texte tronqué (Ellipsis)

L'objectif est de créer une liste de notifications élégante. Si un message de log est trop long, il ne doit pas s'étendre à l'infini : il doit se terminer proprement par "..." tout en restant sur une seule ligne.

### 1. Comprendre les outils
Pour tronquer du texte en CSS, il faut combiner **3 propriétés obligatoires** :
* **`white-space: nowrap`** : Interdit au texte de passer à la ligne. Il reste sur une seule ligne, même s'il dépasse.
* **`overflow: hidden`** : Cache tout ce qui dépasse du cadre de la boîte.
* **`text-overflow: ellipsis`** : Ajoute automatiquement les trois petits points "..." à la fin de la zone visible.

> **Le piège de Flexbox** : Pour que cela fonctionne dans un parent Flex, l'élément qui contient le texte doit avoir un `min-width: 0`. Sans cela, il refuse de rétrécir et poussera les autres éléments hors de l'écran.

---

### 2. Action : Structure HTML
Ajoutez ce bloc dans votre zone de contenu principal (`.main-content`) :

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

---

### 3. Action : Dompter le texte (CSS)
Ajoutez ces règles dans votre fichier `style.css` :

```css
.notification-list {
  background-color: var(--surface);
  border-radius: var(--radius);
  margin-top: 30px;
  border: 1px solid rgba(255, 255, 255, 0.05);
}

.notif-item {
  display: flex;
  align-items: center;
  gap: 15px;
  padding: 12px 20px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
}

.notif-text {
  flex: 1; /* Prend tout l'espace disponible */
  color: var(--text);
  
  /* --- LA MAGIE DE L'ELLIPSIS --- */
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  min-width: 0; /* INDISPENSABLE pour que flex accepte de tronquer */
}

.notif-time {
  color: var(--text-muted);
  font-size: 0.85rem;
  flex-shrink: 0; /* Empêche l'heure d'être écrasée par le texte long */
}
```

---

### 👁️ Observation pour l'étudiant
> "Essayez de réduire la largeur de votre navigateur. Vous verrez le texte de la notification se raccourcir et les '...' apparaître dynamiquement. Sans le `min-width: 0`, vous remarqueriez que le texte 'pousse' le temps (2min, 15min) en dehors de la boîte. C'est une astuce de développeur senior à bien retenir !"

**Vérification :**
1. Toutes les notifications tiennent-elles bien sur une seule ligne ?
2. Voyez-vous bien les "..." à la fin des phrases longues ?
3. Le temps (ex: "2min") est-il toujours visible à droite ?


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

# 🛠️ Exercice 5.2 — Troncature multi-lignes (Line Clamp)

L'objectif est d'afficher un paragraphe de description, mais de forcer l'arrêt à la 3ème ligne avec les trois petits points "...", même si le texte original est beaucoup plus long.

### 1. Comprendre les outils
Cette technique utilise des propriétés un peu particulières (préfixées par `-webkit-`) qui sont devenues un standard pour tous les navigateurs modernes :
* **`display: -webkit-box`** : Transforme l'élément en une boîte flexible spéciale capable de gérer le bridage.
* **`-webkit-line-clamp: 3`** : C'est ici que l'on définit le nombre maximum de lignes visibles.
* **`-webkit-box-orient: vertical`** : Indique au navigateur que l'empilement du texte se fait verticalement.
* **`overflow: hidden`** : Indispensable pour masquer physiquement le texte qui dépasse de la 3ème ligne.

---

### 2. Action : Structure HTML
Ajoutez ce bloc dans votre zone de contenu, par exemple sous vos notifications :

```html
<div class="card-desc">
  <h3>Description du projet</h3>
  <p class="clamp-text">
    Lorem ipsum dolor sit amet, consectetur adipiscing elit. Sed do eiusmod tempor 
    incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud 
    exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure 
    dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
    Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt 
    mollit anim id est laborum.
  </p>
</div>
```

---

### 3. Action : Brider le texte (CSS)
Ajoutez ces règles dans votre fichier `style.css` :

```css
.card-desc {
  background-color: var(--surface);
  padding: 20px;
  border-radius: var(--radius);
  max-width: 400px; /* On limite la largeur pour mieux voir l'effet */
  margin-top: 20px;
}

.clamp-text {
  /* --- LA MAGIE DU MULTI-LIGNE --- */
  display: -webkit-box;
  -webkit-line-clamp: 3;           /* Limite à 3 lignes précisément */
  -webkit-box-orient: vertical;
  overflow: hidden;
  
  /* Style optionnel pour la lisibilité */
  line-height: 1.5; 
  color: var(--text-muted);
}
```

---

### 👁️ Observation pour l'étudiant
> "Comptez les lignes de votre paragraphe. Normalement, il devrait s'arrêter pile à la fin de la troisième ligne. Essayez de changer la valeur `-webkit-line-clamp: 3` par `2` ou `1`. C'est une méthode extrêmement puissante pour garder des cartes de même hauteur dans un dashboard, quel que soit le contenu envoyé par la base de données !"

**Vérification :**
1. Votre texte s'arrête-t-il bien à la 3ème ligne ?
2. Voyez-vous les "..." à la fin de la dernière ligne visible ?
3. Si vous agrandissez la largeur de la fenêtre, le texte s'adapte-t-il toujours à cette limite ?


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

# 🛠️ Exercice 5.3 — Scroll interne et Scrollbar custom

L'objectif est de créer un journal d'activité (logs) qui ne s'étend pas à l'infini vers le bas. Nous allons limiter sa hauteur et personnaliser la barre de défilement pour qu'elle s'intègre parfaitement au design sombre de **DevPulse**.

### 1. Comprendre les outils
* **`max-height`** : On définit une limite de hauteur. Si le contenu est plus petit, la boîte s'adapte. S'il est plus grand, la boîte s'arrête là.
* **`overflow-y: auto`** : Indique au navigateur d'ajouter une barre de défilement verticale uniquement si le contenu dépasse la hauteur fixée.
* **`::-webkit-scrollbar`** : Une famille de propriétés spéciales qui permettent de styliser la barre de défilement (largeur, couleur du fond, couleur du curseur).

---

### 2. Action : Structure HTML
Ajoutez ce panel dans votre zone de contenu principal (`.main-content`) :

```html
<div class="activity-panel">
  <h3>Activité récente</h3>
  <div class="activity-scroll">
    <div class="activity-item"><span>🔔 Déploiement v2.4.1 réussi</span><span class="badge badge-success">OK</span></div>
    <div class="activity-item"><span>⚠️ CPU > 80% sur worker-03</span><span class="badge badge-warning">Warn</span></div>
    <div class="activity-item"><span>🔔 PR #847 mergé par Alice</span><span class="badge badge-success">OK</span></div>
    <div class="activity-item"><span>❌ Build failed sur staging</span><span class="badge badge-danger">Fail</span></div>
    <div class="activity-item"><span>🔔 Migration DB terminée</span><span class="badge badge-success">OK</span></div>
    <div class="activity-item"><span>⚠️ SSL expire dans 7 jours</span><span class="badge badge-warning">Warn</span></div>
    <div class="activity-item"><span>🔔 Backup quotidien OK</span><span class="badge badge-success">OK</span></div>
    <div class="activity-item"><span>❌ Timeout /api/reports</span><span class="badge badge-danger">Fail</span></div>
    <div class="activity-item"><span>🔔 Scale up: 3→5 replicas</span><span class="badge badge-success">OK</span></div>
    <div class="activity-item"><span>⚠️ Rate limit client-42</span><span class="badge badge-warning">Warn</span></div>
  </div>
</div>
```

---

### 3. Action : Créer la zone de scroll (CSS)
Ajoutez ces règles pour limiter la hauteur et styliser les éléments :

```css
.activity-panel {
  background-color: var(--surface);
  border-radius: var(--radius);
  padding: 20px;
  max-width: 500px;
  margin-top: 30px;
}

.activity-scroll {
  /* On limite la hauteur et on active le scroll */
  max-height: 280px;
  overflow-y: auto;
  margin-top: 15px;
  padding-right: 10px; /* Espace pour la scrollbar */
}

.activity-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 0;
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
  transition: background 0.2s;
}

.activity-item:hover {
  background-color: rgba(255, 255, 255, 0.02);
}
```

---

### 4. Action : Personnaliser la barre de défilement
Par défaut, la scrollbar est grise et épaisse. Rendons-la plus discrète :

```css
/* 1. Largeur de la barre */
.activity-scroll::-webkit-scrollbar {
  width: 6px;
}

/* 2. Fond de la barre (piste) */
.activity-scroll::-webkit-scrollbar-track {
  background: rgba(255, 255, 255, 0.05);
  border-radius: 10px;
}

/* 3. La partie qui bouge (curseur) */
.activity-scroll::-webkit-scrollbar-thumb {
  background: var(--accent);
  border-radius: 10px;
}

/* Style des badges */
.badge {
  padding: 2px 8px;
  border-radius: 4px;
  font-size: 0.75rem;
  font-weight: bold;
}
.badge-success { background: rgba(0, 184, 148, 0.2); color: var(--success); }
.badge-warning { background: rgba(253, 203, 110, 0.2); color: #fdcb6e; }
.badge-danger { background: rgba(214, 48, 49, 0.2); color: #d63031; }
```

---

### 👁️ Observation pour l'étudiant
> "Essayez de faire défiler la liste avec votre souris. Vous voyez la fine barre violette ? C'est beaucoup plus élégant que la barre grise standard du navigateur. Notez aussi que le titre 'Activité récente' reste fixe en haut car il n'est pas dans la zone `.activity-scroll` : c'est un excellent moyen de garder le contexte visible."

**Vérification :**
1. Votre panel s'arrête-t-il bien à une certaine hauteur ?
2. La scrollbar est-elle bien colorée (couleur accent) ?
3. Le défilement est-il fluide ?


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

# 🛠️ Exercice 6.1 — Gradients et Ombres (Le relief)

Dans cet exercice, nous allons créer une pièce maîtresse pour notre dashboard : une carte "Hero". Contrairement aux cartes classiques, celle-ci doit attirer l'œil immédiatement grâce à un dégradé de couleurs dynamique et une ombre qui donne l'impression qu'elle flotte au-dessus de la page.

### 1. Comprendre les outils
* **`linear-gradient`** : Permet de créer une transition douce entre deux ou plusieurs couleurs. L'angle `135deg` permet d'orienter le dégradé en diagonale (du haut à gauche vers le bas à droite).
* **`box-shadow`** : Cette propriété prend 4 valeurs principales :
    1.  Le décalage horizontal (X).
    2.  Le décalage vertical (Y).
    3.  Le flou (Blur).
    4.  La couleur (souvent avec de la transparence via `rgba`).
* **La hiérarchie visuelle** : Un fond coloré impose d'utiliser une couleur de texte contrastée (souvent blanc pur) pour garantir la lisibilité.

---

### 2. Action : Structure HTML
Ajoutez ce bloc en haut de votre zone `.main-content`. C'est l'élément qui accueillera vos utilisateurs.

```html
<div class="hero-card">
  <h2>Bienvenue sur DevPulse</h2>
  <p>Monitorez vos services et vos déploiements en temps réel avec une précision chirurgicale.</p>
  <button class="btn-hero">Commencer l'analyse</button>
</div>
```

---

### 3. Action : Ajouter du style et du relief (CSS)
Ajoutez ces règles dans votre fichier `style.css` :

```css
.hero-card {
  /* 1. Le dégradé : de la couleur accent vers la couleur success en diagonale */
  background: linear-gradient(135deg, var(--accent) 0%, var(--success) 100%);
  
  /* 2. L'ombre : décalée vers le bas pour l'effet de hauteur */
  box-shadow: 0 20px 40px rgba(108, 92, 231, 0.3);
  
  /* 3. Mise en forme */
  padding: 40px;
  border-radius: calc(var(--radius) * 2); /* On accentue l'arrondi pour le style */
  color: white;
  margin-bottom: 30px;
}

.hero-card h2 {
  font-size: 2rem;
  margin-bottom: 10px;
}

.hero-card p {
  opacity: 0.9;
  margin-bottom: 25px;
  max-width: 500px;
}

.btn-hero {
  background-color: white;
  color: var(--accent);
  border: none;
  padding: 12px 24px;
  border-radius: var(--radius);
  font-weight: bold;
  cursor: pointer;
  transition: transform 0.2s;
}

.btn-hero:hover {
  transform: translateY(-3px); /* Petit effet de saut au survol */
}
```

---

### 👁️ Observation pour l'étudiant
> "Regardez comment l'ombre (`box-shadow`) utilise une version transparente de la couleur violette (`rgba`) au lieu d'un noir pur. C'est le secret des designs professionnels : les ombres colorées paraissent beaucoup plus naturelles et moins 'sales' que les ombres grises. L'effet de profondeur est ainsi bien plus convaincant."

**Vérification :**
1. Votre carte affiche-t-elle bien une transition du violet vers le vert ?
2. L'ombre est-elle bien visible sous la carte, lui donnant un effet de relief ?
3. Le texte blanc est-il bien lisible sur le fond coloré ?


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

# 🛠️ Exercice 6.2 — Filtres et Transparence (L'effet Overlay)

L'objectif est de placer du texte par-dessus une image sans que celle-ci ne gêne la lecture. Pour y arriver, nous allons "préparer" l'image avec des filtres (flou et assombrissement) avant de poser le texte au centre.

### 1. Comprendre les outils
* **`filter: brightness(0.5)`** : Réduit la luminosité de l'image (ici à 50%). Cela permet au texte blanc de ressortir (contraste).
* **`filter: blur(2px)`** : Ajoute un léger flou. Cela aide l'œil à ignorer les détails de l'image pour se concentrer sur le texte.
* **`position: absolute` + `inset: 0`** : `inset: 0` est un raccourci moderne pour dire `top: 0; right: 0; bottom: 0; left: 0;`. Cela force l'overlay à recouvrir exactement toute la surface de son parent.
* **`pointer-events: none`** (optionnel) : Permet aux clics de traverser l'overlay pour atteindre l'image ou les liens en dessous si besoin.

---

### 2. Action : Structure HTML
Ajoutez ce bloc dans votre zone `.main-content`. Il contient l'image et la couche (l'overlay) qui portera le texte.

```html
<div class="image-overlay-container">
  <img src="https://picsum.photos/800/300" alt="Cover" class="cover-img">
  <div class="overlay">
    <h2>Dashboard Analytics</h2>
    <p>Vue d'ensemble de vos métriques et performances</p>
  </div>
</div>
```

---

### 3. Action : Superposer et Filtrer (CSS)
Ajoutez ces règles dans votre fichier `style.css` :

```css
.image-overlay-container {
  position: relative; /* Indispensable pour que l'overlay se cale dessus */
  width: 100%;
  height: 300px;
  border-radius: var(--radius);
  overflow: hidden;
  margin-top: 30px;
}

.cover-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  
  /* --- FILTRES : Assombrir et Flouter --- */
  filter: brightness(0.5) blur(2px);
  
  /* On augmente légèrement l'échelle pour éviter les bords blancs du flou */
  transform: scale(1.05); 
}

.overlay {
  /* On couvre toute la zone */
  position: absolute;
  inset: 0; 
  
  /* On centre le texte horizontalement et verticalement */
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  
  color: white;
  text-align: center;
  padding: 20px;
}

.overlay h2 {
  font-size: 2.5rem;
  margin-bottom: 10px;
  text-shadow: 0 2px 10px rgba(0,0,0,0.5); /* Sécurité supplémentaire pour la lisibilité */
}
```

---

### 👁️ Observation pour l'étudiant
> "Essayez de retirer temporairement la ligne `filter: brightness(0.5)`. Vous verrez que si l'image générée par Picsum est claire, votre texte blanc devient soudainement illisible. Les filtres CSS sont vos meilleurs alliés pour garantir l'accessibilité de vos interfaces sans avoir à modifier vos images manuellement dans Photoshop."

**Vérification :**
1. L'image remplit-elle bien tout le conteneur ?
2. Le texte est-il parfaitement centré sur l'image ?
3. L'image paraît-elle un peu sombre et floue par rapport à une image normale ?

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

# 🛠️ Exercice 7.1 — Les états d'interaction (Boutons)

L'objectif est de styliser les quatre moments clés de la vie d'un bouton. Un bon bouton doit "répondre" visuellement à chaque action de l'utilisateur.

### 1. Comprendre les outils
* **`:hover`** : L'utilisateur survole l'élément avec sa souris. C'est l'indice visuel que l'élément est cliquable.
* **`:focus`** : L'élément est sélectionné (souvent via la touche `Tab`). C'est **crucial pour l'accessibilité**.
* **`:active`** : Le moment précis où l'on clique (le bouton est enfoncé).
* **`:disabled`** : Le bouton est présent mais inutilisable (ex: formulaire incomplet).
* **`transition`** : Permet d'éviter les changements de couleur trop "bruts" en animant le passage d'un état à l'autre.

---

### 2. Action : Structure HTML
Ajoutez cette vitrine de boutons dans votre zone de contenu :

```html
<div class="btn-showcase">
  <button class="btn btn-primary">Primary</button>
  <button class="btn btn-outline">Outline</button>
  <button class="btn btn-danger">Supprimer</button>
  <button class="btn btn-primary" disabled>Désactivé</button>
</div>
```

---

### 3. Action : Animer les interactions (CSS)
Ajoutez ces règles dans votre fichier `style.css` :

```css
.btn-showcase {
  display: flex;
  gap: 15px;
  padding: 30px;
  background-color: var(--surface);
  border-radius: var(--radius);
}

.btn {
  padding: 10px 20px;
  border-radius: var(--radius);
  font-weight: 600;
  cursor: pointer;
  border: none;
  /* ÉLÉMENT CLÉ : On anime toutes les propriétés sur 0.2 seconde */
  transition: all 0.2s ease;
  outline: none; /* On enlève l'outline par défaut pour le personnaliser */
}

/* --- ÉTAT : HOVER (Survol) --- */
.btn:hover:not(:disabled) {
  transform: translateY(-2px); /* Le bouton monte légèrement */
  filter: brightness(1.1);      /* Il devient un peu plus clair */
  box-shadow: 0 5px 15px rgba(0,0,0,0.3);
}

/* --- ÉTAT : FOCUS (Accessibilité Clavier) --- */
.btn:focus {
  box-shadow: 0 0 0 3px rgba(108, 92, 231, 0.5); /* "Ring" autour du bouton */
}

/* --- ÉTAT : ACTIVE (Clic enfoncé) --- */
.btn:active:not(:disabled) {
  transform: translateY(0); /* Il redescend */
  scale: 0.96;              /* Il rétrécit légèrement (effet de pression) */
}

/* --- ÉTAT : DISABLED (Désactivé) --- */
.btn:disabled {
  opacity: 0.5;
  cursor: not-allowed;
  filter: grayscale(1);     /* On enlève la couleur */
}

/* Couleurs spécifiques */
.btn-primary { background-color: var(--accent); color: white; }
.btn-outline { background: transparent; border: 1px solid var(--accent); color: var(--accent); }
.btn-danger  { background-color: #ff7675; color: white; }
```

---

### 👁️ Observation pour l'étudiant
> "Testez chaque bouton un par un. Survoler-les, cliquez sans relâcher la souris (état `active`), et essayez d'utiliser la touche **Tab** de votre clavier pour voir l'état `focus`. Notez que le bouton 'Désactivé' ne réagit à rien : c'est grâce au sélecteur `:not(:disabled)` qui empêche les effets de survol de s'appliquer."

**Vérification :**
1. Vos boutons montent-ils d'un pixel ou deux quand vous les survolez ?
2. Le bouton "Désactivé" affiche-t-il bien un curseur d'interdiction 🚫 ?
3. Le clic donne-t-il bien une impression de "bouton physique" qui s'enfonce ?

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

# 🛠️ Exercice 7.2 — Inputs et Validation (Feedback visuel)

L'objectif est de styliser des champs de saisie qui réagissent à l'utilisateur. Nous allons apprendre à créer cet effet de "halo lumineux" (le ring) lors du clic, très commun dans les designs modernes comme ceux de Tailwind ou de GitHub.

### 1. Comprendre les outils
* **`outline: none`** : On retire la bordure bleue par défaut des navigateurs pour la remplacer par quelque chose de plus esthétique.
* **`box-shadow` avec "spread"** : Pour créer le halo, on utilise une ombre sans décalage (X=0, Y=0) mais avec un étalement (4ème valeur). Cela crée une bordure extérieure fluide.
* **Transitions ciblées** : On ne fait pas seulement varier la couleur de la bordure, mais aussi l'ombre pour un effet de "douceur".

---

### 2. Action : Structure HTML
Ajoutez ce formulaire de démonstration dans votre zone de contenu. Il présente trois états : normal, erreur et succès.

```html
<div class="form-demo">
  <div class="form-group">
    <label>Email professionnel</label>
    <input type="email" placeholder="nom@entreprise.com" class="input">
  </div>

  <div class="form-group">
    <label>Email (erreur)</label>
    <input type="email" value="abakar.dev" class="input input-error">
    <span class="error-msg">Format d'adresse invalide</span>
  </div>

  <div class="form-group">
    <label>Email (succès)</label>
    <input type="email" value="contact@devpulse.ma" class="input input-success">
    <span class="success-msg">Email vérifié ✓</span>
  </div>
</div>
```

---

### 3. Action : Styliser les champs (CSS)
Ajoutez ces règles dans votre fichier `style.css`. Notez l'utilisation du "halo" sur le focus.

```css
.form-demo {
  max-width: 400px;
  background-color: var(--surface);
  padding: 30px;
  border-radius: var(--radius);
  margin-top: 30px;
}

.form-group {
  margin-bottom: 20px;
  display: flex;
  flex-direction: column;
  gap: 8px;
}

.form-group label {
  font-size: 0.9rem;
  color: var(--text-muted);
}

.input {
  background-color: var(--bg);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: white;
  padding: 12px 15px;
  border-radius: var(--radius);
  outline: none;
  transition: all 0.2s ease;
}

/* --- ÉTAT : FOCUS (Le halo) --- */
.input:focus {
  border-color: var(--accent);
  /* box-shadow: X Y Blur Spread Color */
  box-shadow: 0 0 0 3px rgba(108, 92, 231, 0.2);
}

/* --- ÉTAT : ERREUR --- */
.input-error {
  border-color: #ff7675;
}
.input-error:focus {
  box-shadow: 0 0 0 3px rgba(255, 118, 117, 0.2);
}
.error-msg { color: #ff7675; font-size: 0.8rem; }

/* --- ÉTAT : SUCCÈS --- */
.input-success {
  border-color: var(--success);
}
.success-msg { color: var(--success); font-size: 0.8rem; }
```

---

### 👁️ Observation pour l'étudiant
> "Cliquez dans le premier champ. Vous voyez comment la bordure s'illumine doucement ? C'est le mélange entre `border-color` et `box-shadow`. Remarquez aussi que pour l'état d'erreur, nous avons changé la couleur du halo en rouge. C'est ce qu'on appelle la **cohérence visuelle** : la couleur doit toujours porter le sens de l'action."

**Vérification :**
1. Vos champs de saisie sont-ils bien alignés verticalement ?
2. Le halo (ring) apparaît-il bien au clic (focus) ?
3. Les messages d'erreur et de succès sont-ils bien positionnés sous les inputs ?

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

# 🛠️ Exercice 8.1 — Transitions "Smooth" (Effets au survol)

L'objectif est d'ajouter une sensation de légèreté à nos cartes de statistiques. Au lieu d'un changement brutal, la carte va sembler "décoller" du tableau de bord lorsque la souris passe dessus.

### 1. Comprendre les outils
* **`transition`** : C'est le chef d'orchestre. Elle définit **quelle** propriété doit s'animer (ex: `transform`), pendant **combien de temps** (`0.2s`) et selon **quel rythme** (`ease`).
* **`transform: translateY(-4px)`** : Déplace l'élément sur l'axe vertical. Une valeur négative fait "monter" l'élément vers le haut de l'écran.
* **`ease`** : C'est un timing-function qui commence doucement, accélère, puis finit doucement. C'est ce qui rend l'animation plus "humaine" et moins mécanique.



---

### 2. Action : Cibler les cartes de l'exercice 3.2
Nous allons reprendre la classe `.stat-card`. Assurez-vous d'ajouter la transition sur l'état **par défaut** de la carte (pas sur le hover), sinon l'animation ne fonctionnera que dans un sens !

---

### 3. Action : Animer l'élévation (CSS)
Ajoutez ces propriétés à vos styles existants dans `style.css` :

```css
.stat-card {
  /* ... vos styles précédents (background, padding, etc.) ... */

  /* ÉLÉMENT CLÉ : On prépare le terrain pour l'animation */
  /* On liste les propriétés à animer pour de meilleures performances */
  transition: transform 0.2s ease, box-shadow 0.2s ease, border-color 0.2s ease;
  
  cursor: pointer;
  will-change: transform; /* Astuce pour aider le navigateur à fluidifier l'animation */
}

/* --- ÉTAT AU SURVOL (Hover) --- */
.stat-card:hover {
  /* La carte monte de 4 pixels */
  transform: translateY(-4px);
  
  /* L'ombre devient plus floue et plus large pour simuler l'éloignement du fond */
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.4);
  
  /* On peut aussi colorer légèrement la bordure */
  border-color: var(--accent);
}
```

---

### 👁️ Observation pour l'étudiant
> "Passez votre souris rapidement sur les différentes cartes. Voyez-vous comment elles semblent flotter ? Essayez de changer `0.2s` par `1s`. Vous verrez que l'effet devient très lent, presque lourd. Le secret d'une bonne interface utilisateur (UI), c'est de rester entre **0.1s et 0.3s** : l'utilisateur doit sentir le mouvement sans avoir à l'attendre."

**Vérification :**
1. Vos cartes montent-elles bien au survol ?
2. Redescendent-elles avec la même fluidité quand vous retirez la souris ?
3. L'ombre s'accentue-t-elle bien pendant le mouvement ?

## Exercice 8.2 — Fade in / Slide in (animations d'entrée)

### Objectif
Les stat cards apparaissent avec une animation de fade + slide au chargement de la page.

### CSS à implémenter
1. Créer un `@keyframes fadeSlideUp` : de `opacity: 0; transform: translateY(20px)` vers `opacity: 1; transform: translateY(0)`
2. Appliquer sur `.stat-card` avec un `animation-delay` décalé pour chaque carte (staggered)
3. Durée : 0.5s, easing : `ease-out`

> **Concepts à utiliser** : `@keyframes`, `animation`, `animation-delay`, `animation-fill-mode: forwards`


---

# 🛠️ Exercice 8.2 — Fade & Slide (Animations d'entrée)

L'objectif est de faire apparaître nos cartes de statistiques de manière progressive. Au lieu de s'afficher brutalement, elles vont "glisser" du bas vers le haut tout en devenant opaques. Pour un effet encore plus premium, nous allons les faire apparaître les unes après les autres (**effet Staggered**).

### 1. Comprendre les outils
* **`@keyframes`** : C'est le script de votre animation. On définit l'état de départ (`from`) et l'état d'arrivée (`to`).
* **`animation-fill-mode: forwards`** : Très important ! Cela dit à l'élément de rester dans l'état final de l'animation (opaque et placé) au lieu de revenir à son état initial (invisible).
* **`animation-delay`** : Permet de retarder le début de l'animation. C'est ce qui crée l'effet de cascade.



---

### 2. Action : Définir l'animation (CSS)
Ajoutez d'abord la "recette" de l'animation en haut ou en bas de votre fichier `style.css` :

```css
@keyframes fadeSlideUp {
  from {
    opacity: 0;
    transform: translateY(20px); /* Part de 20px plus bas */
  }
  to {
    opacity: 1;
    transform: translateY(0);    /* Arrive à sa place réelle */
  }
}
```

---

### 3. Action : Appliquer l'animation aux cartes
Maintenant, lions cette animation aux `.stat-card` :

```css
.stat-card {
  /* ... vos styles précédents ... */

  /* On cache la carte par défaut pour que l'animation la révèle */
  opacity: 0; 
  
  /* Nom | Durée | Rythme | Direction finale */
  animation: fadeSlideUp 0.5s ease-out forwards;
}
```

---

### 4. Action : Créer l'effet de cascade (Stagger)
Pour que les cartes ne montent pas toutes en même temps, nous allons ajouter un petit délai différent pour chacune :

```css
/* La 1ère carte part tout de suite (déjà défini) */

.stat-card:nth-child(2) {
  animation-delay: 0.1s;
}

.stat-card:nth-child(3) {
  animation-delay: 0.2s;
}

.stat-card:nth-child(4) {
  animation-delay: 0.3s;
}
```

---

### 👁️ Observation pour l'étudiant
> "Actualisez votre page (F5). Vous voyez ce mouvement fluide ? Les cartes semblent 'pleuvoir' sur l'écran. C'est l'utilisation du `nth-child` qui permet de créer ce rythme sans avoir à créer 4 classes différentes dans votre HTML. C'est propre, efficace et très agréable pour l'utilisateur."

**Vérification :**
1. Les cartes sont-elles invisibles au tout début du chargement ?
2. Est-ce qu'elles montent bien vers le haut ?
3. Est-ce qu'elles apparaissent avec un léger décalage entre elles ?

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

# 🛠️ Exercice 8.3 — Loader Spinner (Animation Infinie)

L'objectif est de créer un indicateur de chargement ("spinner") qui tourne sur lui-même indéfiniment. C'est l'élément indispensable pour faire patienter l'utilisateur pendant qu'une requête API récupère les données de votre dashboard.

### 1. Comprendre les outils
* **Le cercle par les bordures** : Pour créer un spinner, on crée un carré parfait, on lui donne un `border-radius: 50%` pour le transformer en cercle, et on colore une seule de ses quatre bordures (`border-top-color`).
* **`@keyframes spin`** : Cette animation ne change pas de position, elle change d'angle. On utilise `transform: rotate()`.
* **`linear`** : Contrairement au `ease` que nous avons utilisé pour les cartes, un spinner doit tourner à une vitesse constante pour paraître fluide et mécanique.
* **`infinite`** : On demande à l'animation de recommencer dès qu'elle se termine, sans jamais s'arrêter.



---

### 2. Action : Structure HTML
Ajoutez ce bloc à l'endroit où vous souhaitez simuler un chargement (par exemple, dans une zone vide de votre dashboard) :

```html
<div class="loader-container">
  <div class="spinner"></div>
  <p>Synchronisation avec le serveur...</p>
</div>
```

---

### 3. Action : Créer et Animer le Spinner (CSS)
Ajoutez ces règles dans votre fichier `style.css` :

```css
.loader-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 15px;
  padding: 40px;
}

.spinner {
  width: 40px;
  height: 40px;
  
  /* On crée un cercle avec une bordure grise très légère */
  border: 4px solid rgba(255, 255, 255, 0.1);
  border-radius: 50%;
  
  /* On colore uniquement le haut pour créer l'effet de "crochet" */
  border-top-color: var(--accent);
  
  /* Lancement de l'animation */
  animation: spin 0.8s linear infinite;
}

.loader-container p {
  color: var(--text-muted);
  font-size: 0.9rem;
  letter-spacing: 0.5px;
}

/* --- LA ROTATION --- */
@keyframes spin {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}
```

---

### 👁️ Observation pour l'étudiant
> "Regardez bien votre spinner. Si vous changez `border-top-color` en `border-left-color` aussi, votre spinner aura deux côtés colorés. Si vous changez `0.8s` par `2s`, il aura l'air beaucoup plus lent et 'fatigué'. La fluidité d'un spinner est souvent ce qui donne l'impression qu'une application est performante."

**Vérification :**
1. Le cercle tourne-t-il sans aucune saccade ?
2. Le texte est-il bien centré sous le spinner ?
3. Le spinner s'intègre-t-il bien dans le thème sombre de DevPulse ?

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

# 🛠️ Exercice 8.4 — Skeleton Loading (Shimmer effect)

L'objectif est de créer un faux contenu qui "brille". Au lieu d'un spinner central, on montre à l'utilisateur la forme de ce qui va arriver (un avatar, un titre, des lignes de texte).

### 1. Comprendre les outils
* **Le dégradé dynamique** : On utilise un `linear-gradient` avec trois couleurs : `gris -> blanc translucide -> gris`. 
* **`background-size: 200%`** : On rend le fond deux fois plus large que l'élément pour pouvoir faire glisser le reflet de gauche à droite.
* **`animation`** : On fait bouger la `background-position` en boucle pour créer cet effet de balayage lumineux.

---

### 2. Action : Structure HTML
Ajoutez ce bloc de squelette dans votre page. Il simule la structure d'un profil utilisateur ou d'une carte d'activité.

```html
<div class="skeleton-card">
  <div class="skeleton skeleton-avatar"></div>
  <div class="skeleton skeleton-title"></div>
  <div class="skeleton skeleton-text"></div>
  <div class="skeleton skeleton-text short"></div>
</div>
```

---

### 3. Action : Créer l'effet de brillance (CSS)
Ajoutez ces règles dans votre fichier `style.css` :

```css
.skeleton-card {
  background-color: var(--surface);
  padding: 20px;
  border-radius: var(--radius);
  width: 300px;
  margin-top: 30px;
}

.skeleton {
  /* Fond de base gris + dégradé de brillance */
  background: linear-gradient(
    90deg, 
    rgba(255, 255, 255, 0.05) 25%, 
    rgba(255, 255, 255, 0.1) 50%, 
    rgba(255, 255, 255, 0.05) 75%
  );
  background-size: 200% 100%;
  border-radius: 4px;
  margin-bottom: 12px;
  
  /* Lancement de l'animation de balayage */
  animation: shimmer 1.5s infinite linear;
}

/* Tailles spécifiques */
.skeleton-avatar {
  width: 50px;
  height: 50px;
  border-radius: 50%;
}

.skeleton-title {
  width: 70%;
  height: 18px;
  margin-top: 15px;
}

.skeleton-text {
  width: 100%;
  height: 12px;
}

.skeleton-text.short {
  width: 40%;
}

/* --- L'ANIMATION DU REFLET --- */
@keyframes shimmer {
  0% {
    background-position: 200% 0;
  }
  100% {
    background-position: -200% 0;
  }
}
```

---

### 👁️ Observation pour l'étudiant
> "Observez le mouvement de la lumière. Elle semble traverser tous les éléments en même temps. C'est l'un des secrets pour rendre une interface fluide : donner l'impression que le contenu est déjà là, sous une couche de verre. Si vous changez `1.5s` par `0.8s`, la brillance passera beaucoup plus vite, ce qui peut donner une sensation d'urgence ou de stress."

**Vérification :**
1. L'avatar est-il bien un cercle ?
2. Le reflet glisse-t-il bien de façon continue sur les éléments ?
3. Le squelette s'arrête-t-il bien aux bords de la carte ?


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

<form class="register-form">
  <h2>Créer un compte</h2>

  <div class="form-row">
    <div class="form-group">
      <label>Prénom <span class="required">*</span></label>
      <input type="text" class="input" placeholder="Jean" required>
    </div>
    <div class="form-group">
      <label>Nom <span class="required">*</span></label>
      <input type="text" class="input" placeholder="Dupont" required>
    </div>
  </div>

  <div class="form-group">
    <label>Email <span class="required">*</span></label>
    <input type="email" class="input" placeholder="jean@exemple.com" required>
    <span class="hint">On ne partagera jamais votre email.</span>
  </div>

  <div class="form-group">
    <label>Mot de passe <span class="required">*</span></label>
    <input type="password" class="input" placeholder="Min. 8 caractères" required>
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
      <label class="checkbox">
        <input type="checkbox" checked>
        <span>React / Vue</span>
      </label>
      <label class="checkbox">
        <input type="checkbox">
        <span>Node.js</span>
      </label>
      <label class="checkbox">
        <input type="checkbox" checked>
        <span>Python</span>
      </label>
    </div>

    <div class="form-group">
      <label>Type de contrat</label>
      <label class="radio">
        <input type="radio" name="contract">
        <span>CDI</span>
      </label>
      <label class="radio">
        <input type="radio" name="contract" checked>
        <span>Freelance</span>
      </label>
      <label class="radio">
        <input type="radio" name="contract">
        <span>CDD</span>
      </label>
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
---

# 🛠️ Exercice 9.1 — Formulaire d'inscription (Mastering Inputs)

L'objectif est de transformer des éléments de formulaire bruts en une interface élégante. Le plus grand défi ici est de "tuer" le style par défaut des navigateurs pour imposer le nôtre, notamment pour les Checkbox, Radio et Select.

### 1. Comprendre les outils
* **`appearance: none`** : C'est la commande qui dit au navigateur : "Oublie ton style par défaut pour cette case ou ce menu, je m'en occupe".
* **`::after` / `::before`** : On utilise ces pseudo-éléments pour dessiner manuellement la coche (V) du checkbox ou le point du bouton radio.
* **Le Switch (Toggle)** : C'est une checkbox cachée. Le "slider" est un `<span>` que l'on déplace selon que la checkbox est `:checked` ou non.

---

### 2. Action : Mise en page globale (CSS)
On commence par structurer les rangées et les groupes.

```css
.register-form {
  background-color: var(--surface);
  padding: 40px;
  border-radius: var(--radius);
  max-width: 700px;
  margin: 20px auto;
  border: 1px solid rgba(255, 255, 255, 0.05);
}

.form-row {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
  margin-bottom: 20px;
}

@media (max-width: 600px) {
  .form-row { grid-template-columns: 1fr; }
}

.form-group {
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin-bottom: 20px;
}

.required { color: #ff7675; }
.hint { font-size: 0.8rem; color: var(--text-muted); }
```

---

### 3. Action : Customisation des Inputs (CSS)
On applique le design système de **DevPulse**.

```css
/* Style commun : Input, Textarea, Select */
.input {
  background-color: var(--bg);
  border: 1px solid rgba(255, 255, 255, 0.1);
  color: white;
  padding: 12px;
  border-radius: var(--radius);
  outline: none;
  transition: all 0.2s;
}

.input:focus {
  border-color: var(--accent);
  box-shadow: 0 0 0 3px rgba(108, 92, 231, 0.2);
}

.textarea { resize: vertical; min-height: 80px; }

/* Custom Checkbox & Radio */
.checkbox, .radio {
  display: flex;
  align-items: center;
  gap: 10px;
  cursor: pointer;
  font-size: 0.95rem;
}

.checkbox input, .radio input {
  appearance: none;
  width: 18px;
  height: 18px;
  border: 2px solid var(--accent);
  background-color: transparent;
  position: relative;
  cursor: pointer;
}

.checkbox input { border-radius: 4px; }
.radio input { border-radius: 50%; }

.checkbox input:checked::after {
  content: "✓";
  position: absolute;
  top: -2px; left: 2px;
  color: var(--accent);
  font-weight: bold;
}

.radio input:checked::after {
  content: "";
  position: absolute;
  width: 10px; height: 10px;
  background: var(--accent);
  border-radius: 50%;
  top: 2px; left: 2px;
}
```

---

### 4. Action : Le Switch Animé (Toggle)
C'est la partie la plus "visuelle" de l'exercice.

```css
.toggle-label {
  display: flex;
  align-items: center;
  gap: 15px;
  cursor: pointer;
}

.toggle {
  position: relative;
  width: 40px;
  height: 20px;
}

.toggle input { opacity: 0; width: 0; height: 0; }

.toggle-slider {
  position: absolute;
  inset: 0;
  background-color: #444;
  border-radius: 20px;
  transition: 0.3s;
}

.toggle-slider::before {
  content: "";
  position: absolute;
  height: 14px; width: 14px;
  left: 3px; bottom: 3px;
  background-color: white;
  border-radius: 50%;
  transition: 0.3s;
}

.toggle input:checked + .toggle-slider { background-color: var(--success); }
.toggle input:checked + .toggle-slider::before { transform: translateX(20px); }

.form-actions {
  display: flex;
  gap: 15px;
  margin-top: 30px;
}
```

---

### 👁️ Observation pour l'étudiant
> "Regardez le **Toggle**. Ce n'est qu'une simple case à cocher cachée. Mais avec un peu de CSS, on la transforme en un composant interactif digne d'une application mobile. Notez aussi l'usage de `+` (sélecteur adjacent) : il permet de dire 'Si l'input est coché, alors change le style du span juste après lui'."

**Vérification :**
1. Votre formulaire est-il bien sur 2 colonnes sur PC et 1 seule sur mobile ?
2. Vos cases à cocher et boutons radios ont-ils bien la couleur violette ?
3. Le switch passe-t-il bien au vert quand vous l'activez ?


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

# 🛠️ Exercice 10.2 — Header Sticky (Tableau de Logs)

L'objectif est de créer une zone de logs API compacte. Le défi technique ici est le `position: sticky` : il permet à l'en-tête de "coller" au sommet du conteneur pendant que le contenu défile en dessous.

### 1. Comprendre les outils
* **`position: sticky`** : Un mélange entre `relative` et `fixed`. L'élément défile normalement jusqu'à ce qu'il atteigne une position donnée (ici `top: 0`), puis il s'y bloque.
* **`z-index: 1`** : Nécessaire pour s'assurer que l'en-tête passe *au-dessus* des lignes de données lors du défilement.
* **Le fond solide** : Par défaut, les cellules `<th>` peuvent avoir un fond transparent. Si vous ne mettez pas de `background-color` sur le header, vous verrez les lignes de données passer "à travers" le texte de l'en-tête.



---

### 2. Action : Structure HTML
Ajoutez ce bloc. Pour bien tester l'effet, n'hésitez pas à copier-coller la ligne `<tr>` une vingtaine de fois.

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
      <tr><td>1</td><td>/api/users</td><td><span class="txt-bold">GET</span></td><td><span class="badge badge-success">200</span></td><td>45ms</td></tr>
      <tr><td>2</td><td>/api/auth/login</td><td><span class="txt-bold">POST</span></td><td><span class="badge badge-success">200</span></td><td>95ms</td></tr>
      <tr><td>3</td><td>/api/reports/v1</td><td><span class="txt-bold">GET</span></td><td><span class="badge badge-danger">500</span></td><td>1250ms</td></tr>
      <tr><td>4</td><td>/api/users/42</td><td><span class="txt-bold">PUT</span></td><td><span class="badge badge-success">200</span></td><td>62ms</td></tr>
      </tbody>
  </table>
</div>
```

---

### 3. Action : Fixer le header (CSS)
Ajoutez ces règles. Notez bien l'application du fond sur les `th`.

```css
.table-scroll-wrapper {
  max-height: 350px;
  overflow-y: auto;
  background-color: var(--surface);
  border-radius: var(--radius);
  margin-top: 20px;
  border: 1px solid rgba(255, 255, 255, 0.05);
}

/* --- LA MAGIE DU STICKY --- */
.table-scroll-wrapper thead th {
  position: sticky;
  top: 0;
  z-index: 1;
  /* Fond solide obligatoire pour ne pas voir le texte défiler derrière */
  background-color: #2d3436; 
  box-shadow: inset 0 -1px 0 rgba(255, 255, 255, 0.1); /* Ligne de séparation */
}

/* Personnalisation de la scrollbar pour le wrapper */
.table-scroll-wrapper::-webkit-scrollbar {
  width: 5px;
}

.table-scroll-wrapper::-webkit-scrollbar-thumb {
  background: var(--accent);
  border-radius: 10px;
}

/* Styles pour les logs */
.txt-bold { font-weight: bold; font-family: monospace; }
.data-table td { font-family: 'Courier New', Courier, monospace; font-size: 0.85rem; }
```

---

### 👁️ Observation pour l'étudiant
> "Faites défiler le tableau. Vous voyez comme l'en-tête gris reste figé en haut ? C'est le `position: sticky`. Notez que nous avons appliqué le `sticky` sur les balises `th` et non sur le `thead` directement. C'est une particularité des tableaux en CSS : pour une compatibilité maximale sur tous les navigateurs, il vaut mieux fixer les cellules d'en-tête individuellement."

**Vérification :**
1. L'en-tête reste-t-il bien visible même tout en bas de la liste ?
2. Les données sont-elles bien lisibles lorsqu'elles passent sous l'en-tête ?
3. La scrollbar est-elle bien fine et colorée ?

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

# 🛠️ Exercice 11.1 — Modal (Popup & Overlay)

L'objectif est de créer une boîte de dialogue qui demande une confirmation. Pour cela, nous utilisons le positionnement **fixed** qui permet de bloquer l'overlay sur tout l'écran, même si l'utilisateur fait défiler la page en arrière-plan.

### 1. Comprendre les outils
* **`position: fixed`** : Contrairement à `absolute`, cet élément est positionné par rapport à la fenêtre du navigateur (le viewport). Il reste en place même au scroll.
* **`inset: 0`** : Un raccourci crucial qui force l'overlay à s'étirer sur les 4 bords de l'écran.
* **`background: rgba(0, 0, 0, 0.6)`** : On utilise l'alpha (0.6) pour créer cet effet de "voile" sombre qui met en valeur la modal et indique que le reste de l'interface est temporairement inaccessible.
* **Centrage Flexbox** : L'overlay devient un conteneur Flex pour aligner la `.modal-box` parfaitement au milieu de l'écran.

---

### 2. Action : Structure HTML
Ajoutez ce bloc à la fin de votre fichier HTML (juste avant la fermeture de `</body>`).

```html
<div style="padding: 20px;">
  <button class="btn btn-primary" onclick="document.getElementById('modal').style.display='flex'">
    Ouvrir la modal
  </button>
</div>

<div class="modal-overlay" id="modal">
  <div class="modal-box">
    <div class="modal-header">
      <h3>Confirmer la suppression</h3>
      <button class="modal-close" onclick="document.getElementById('modal').style.display='none'">✕</button>
    </div>
    <div class="modal-body">
      <p>Êtes-vous sûr de vouloir supprimer cet utilisateur ? Cette action est irréversible et supprimera toutes les données associées.</p>
    </div>
    <div class="modal-footer">
      <button class="btn btn-outline" onclick="document.getElementById('modal').style.display='none'">Annuler</button>
      <button class="btn btn-danger">Supprimer</button>
    </div>
  </div>
</div>
```

---

### 3. Action : Superposer et Centrer (CSS)
Ajoutez ces règles dans votre fichier `style.css` :

```css
/* 1. L'arrière-plan sombre */
.modal-overlay {
  position: fixed;
  inset: 0;
  background-color: rgba(0, 0, 0, 0.75);
  backdrop-filter: blur(4px); /* Petit bonus : floute l'arrière-plan */
  display: none; /* Caché par défaut */
  justify-content: center;
  align-items: center;
  z-index: 9999; /* Toujours au-dessus de tout */
}

/* 2. La boîte blanche/sombre centrale */
.modal-box {
  background-color: var(--surface);
  width: 90%;
  max-width: 500px;
  border-radius: var(--radius);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.5);
  animation: modalIn 0.3s ease-out; /* Animation d'entrée */
}

/* 3. Sections internes */
.modal-header {
  padding: 20px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.modal-close {
  background: none;
  border: none;
  color: var(--text-muted);
  font-size: 1.5rem;
  cursor: pointer;
}

.modal-body {
  padding: 20px;
  line-height: 1.6;
  color: var(--text-muted);
}

.modal-footer {
  padding: 20px;
  display: flex;
  justify-content: flex-end; /* Boutons à droite */
  gap: 12px;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
}

/* Petite animation d'apparition */
@keyframes modalIn {
  from { opacity: 0; transform: translateY(-30px); }
  to { opacity: 1; transform: translateY(0); }
}
```

---

### 👁️ Observation pour l'étudiant
> "Cliquez sur le bouton. Remarquez comment l'overlay bloque toute interaction avec le reste du dashboard. C'est l'essence même d'une modal : capturer l'attention. Notez aussi l'usage de `backdrop-filter: blur()`. C'est une propriété moderne qui donne cet aspect 'verre dépoli' très élégant à l'overlay."

**Vérification :**
1. La modal est-elle bien centrée horizontalement et verticalement ?
2. Le fond est-il assez sombre pour que le texte de la modal ressorte ?
3. Le bouton "Annuler" et la croix ferment-ils bien la fenêtre ?


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

# 🛠️ Exercice 11.2 — Dropdown Menu (Positionnement Absolu)

L'objectif est de créer un menu qui "apparaît" sous un bouton. Pour un rendu professionnel, on évite le `display: none` qui empêche les animations. À la place, on joue sur l'**opacité** et la **translation** pour créer un effet de glissement fluide.

### 1. Comprendre les outils
* **`position: relative` (sur le parent)** : Il sert de point d'ancrage. Le menu saura qu'il doit se placer par rapport à ce bloc et non par rapport à la page entière.
* **`position: absolute` (sur le menu)** : Permet de sortir le menu du flux pour qu'il "flotte" au-dessus du reste du contenu.
* **`pointer-events: none`** : Indispensable quand on utilise `opacity: 0`. Cela indique au navigateur d'ignorer les clics sur le menu tant qu'il est invisible (pour éviter de cliquer sur un lien caché par erreur).
* **Le sélecteur de survol** : `.dropdown:hover .dropdown-menu` permet de changer l'état du menu dès que la souris entre dans la zone du parent.

---

### 2. Action : Structure HTML
Ajoutez ce bloc, idéalement dans votre `header` ou une barre d'outils.

```html
<div class="dropdown">
  <button class="dropdown-trigger">Mon compte ▾</button>
  <div class="dropdown-menu">
    <a href="#" class="dropdown-item">👤 Profil</a>
    <a href="#" class="dropdown-item">⚙️ Paramètres</a>
    <a href="#" class="dropdown-item">📊 Statistiques</a>
    <div class="dropdown-divider"></div>
    <a href="#" class="dropdown-item danger">🚪 Déconnexion</a>
  </div>
</div>
```

---

### 3. Action : Animer l'apparition (CSS)
Ajoutez ces règles dans votre fichier `style.css` :

```css
/* 1. Le conteneur parent */
.dropdown {
  position: relative;
  display: inline-block;
}

/* 2. Le menu caché */
.dropdown-menu {
  position: absolute;
  top: 100%; /* Se place juste en dessous du bouton */
  right: 0;   /* Aligné sur le bord droit */
  width: 200px;
  background-color: var(--surface);
  border-radius: var(--radius);
  border: 1px solid rgba(255, 255, 255, 0.1);
  box-shadow: 0 10px 25px rgba(0, 0, 0, 0.5);
  margin-top: 10px;
  padding: 8px 0;
  z-index: 100;

  /* --- ÉTAT INITIAL (Caché) --- */
  opacity: 0;
  pointer-events: none;
  transform: translateY(-10px);
  transition: all 0.3s ease;
}

/* 3. ÉTAT AU SURVOL */
.dropdown:hover .dropdown-menu {
  opacity: 1;
  pointer-events: auto;
  transform: translateY(0);
}

/* 4. Éléments du menu */
.dropdown-item {
  display: block;
  padding: 10px 20px;
  color: var(--text);
  text-decoration: none;
  font-size: 0.9rem;
  transition: background 0.2s;
}

.dropdown-item:hover {
  background-color: rgba(255, 255, 255, 0.05);
  color: var(--accent);
}

.dropdown-item.danger:hover {
  color: #ff7675;
  background-color: rgba(255, 118, 117, 0.1);
}

.dropdown-divider {
  height: 1px;
  background-color: rgba(255, 255, 255, 0.1);
  margin: 8px 0;
}
```

---

### 👁️ Observation pour l'étudiant
> "Passez votre souris sur 'Mon compte'. Vous voyez comment le menu semble descendre doucement ? C'est le mélange de `opacity` et `translateY`. Notez l'importance du `margin-top: 10px` sur le menu : il crée un petit espace visuel, mais comme le conteneur `.dropdown` englobe tout, le menu ne disparaît pas quand vous déplacez la souris vers lui."

**Vérification :**
1. Le menu apparaît-il bien de manière fluide ?
2. Les liens changent-ils de couleur quand vous passez dessus ?
3. Le menu est-il bien positionné par rapport au bouton ?



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

# 🛠️ Exercice 11.3 — Tooltip (Pseudo-éléments & Attributs)

L'objectif est de créer un tooltip **sans ajouter de balises HTML supplémentaires**. Nous allons utiliser la puissance des pseudo-éléments et la fonction CSS `attr()` qui permet de récupérer du texte directement depuis le HTML.

### 1. Comprendre les outils
* **`content: attr(data-tooltip)`** : C'est l'astuce magique. Le CSS va lire ce qui est écrit dans l'attribut `data-tooltip` de votre bouton pour l'afficher dans le pseudo-élément `::before`.
* **Le Triangle CSS (`::after`)** : On crée une flèche sans image en utilisant des bordures. Un élément de 0px de large avec des bordures transparentes sauf une produit un triangle parfait.
* **Positionnement Centré** : Pour centrer le tooltip au-dessus du bouton, on utilise `left: 50%` combiné à `transform: translateX(-50%)`.

---

### 2. Action : Structure HTML
Ajoutez ces boutons. Notez l'utilisation de l'attribut personnalisé `data-tooltip`.

```html
<div class="tooltip-demo">
  <button class="btn btn-outline tooltip-trigger" data-tooltip="Copier dans le presse-papier">📋 Copier</button>
  <button class="btn btn-outline tooltip-trigger" data-tooltip="Rafraîchir les données">🔄 Refresh</button>
  <button class="btn btn-outline tooltip-trigger" data-tooltip="Télécharger en CSV">📥 Export</button>
</div>
```

---

### 3. Action : Designer l'infobulle (CSS)
Ajoutez ces règles dans votre fichier `style.css` :

```css
.tooltip-demo {
  display: flex;
  gap: 20px;
  padding: 50px; /* Espace pour voir le tooltip au-dessus */
}

.tooltip-trigger {
  position: relative; /* Point d'ancrage pour ::before et ::after */
}

/* --- LE CORPS DU TOOLTIP --- */
.tooltip-trigger::before {
  content: attr(data-tooltip); /* Récupère le texte du HTML */
  position: absolute;
  bottom: 125%; /* Se place au-dessus du bouton */
  left: 50%;
  transform: translateX(-50%) translateY(10px);
  
  background-color: #1e272e;
  color: white;
  padding: 8px 12px;
  border-radius: 4px;
  font-size: 0.75rem;
  white-space: nowrap;
  
  opacity: 0;
  pointer-events: none;
  transition: all 0.2s ease;
  z-index: 10;
}

/* --- LA PETITE FLÈCHE (TRIANGLE) --- */
.tooltip-trigger::after {
  content: "";
  position: absolute;
  bottom: 110%;
  left: 50%;
  transform: translateX(-50%) translateY(10px);
  
  /* Technique du triangle CSS */
  border-width: 6px;
  border-style: solid;
  border-color: #1e272e transparent transparent transparent;
  
  opacity: 0;
  transition: all 0.2s ease;
}

/* --- AFFICHAGE AU HOVER --- */
.tooltip-trigger:hover::before,
.tooltip-trigger:hover::after {
  opacity: 1;
  transform: translateX(-50%) translateY(0);
}
```

---

### 👁️ Observation pour l'étudiant
> "Survolez les boutons. Vous voyez comme le texte change alors que le code CSS est le même pour les trois ? C'est grâce au `attr(data-tooltip)`. Cette méthode est extrêmement performante car elle évite d'alourdir le DOM avec des dizaines de balises `<div>` cachées. Notez aussi le petit mouvement de 'montée' lors de l'apparition, rendu possible par le `translateY`."

**Vérification :**
1. Le texte affiché correspond-il bien à l'attribut du bouton ?
2. Le tooltip est-il bien centré par rapport au bouton ?
3. La petite flèche pointe-t-elle bien vers le bouton ?


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

# 🛠️ Exercice 11.4 — Onglets (Tabs) en pur CSS

L'objectif est de créer un système de navigation interne où le clic sur un label active un panneau de contenu spécifique. Le secret réside dans le sélecteur adjacent (`~`) qui permet de modifier un élément situé plus loin dans le code en fonction de l'état d'une case cochée.

### 1. Comprendre les outils
* **`:checked`** : Ce pseudo-sélecteur détecte quel bouton radio est actuellement sélectionné par l'utilisateur.
* **Sélecteur `~` (Frère général)** : Il permet de cibler un élément qui partage le même parent, même s'il n'est pas placé juste après.
* **Liaison `label for=""`** : Comme les boutons radio sont cachés (`display: none`), on utilise les labels pour "cliquer" à leur place. Cliquer sur le label active la radio correspondante.

---

### 2. Action : Structure HTML
Ajoutez ce bloc. Notez bien que les `input` doivent être **avant** les panels pour que le sélecteur CSS puisse les atteindre.

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
    <div class="tab-panel" id="panel1">
      <h4>Paramètres Généraux</h4>
      <p>Configurez ici les informations de base de votre profil.</p>
    </div>
    <div class="tab-panel" id="panel2">
      <h4>Sécurité</h4>
      <p>Gérez votre mot de passe et l'authentification à deux facteurs.</p>
    </div>
    <div class="tab-panel" id="panel3">
      <h4>Notifications</h4>
      <p>Choisissez comment vous souhaitez être alerté des activités.</p>
    </div>
  </div>
</div>
```

---

### 3. Action : Logique d'affichage (CSS)
Ajoutez ces règles dans votre fichier `style.css` :

```css
.tabs {
  background-color: var(--surface);
  border-radius: var(--radius);
  padding: 20px;
  margin-top: 30px;
}

/* 1. On cache les vrais boutons radio */
.tab-input {
  display: none;
}

/* 2. Style des onglets */
.tab-labels {
  display: flex;
  gap: 20px;
  border-bottom: 2px solid rgba(255, 255, 255, 0.05);
  margin-bottom: 20px;
}

.tab-label {
  padding: 10px 0;
  cursor: pointer;
  color: var(--text-muted);
  font-weight: 600;
  border-bottom: 2px solid transparent;
  margin-bottom: -2px; /* Pour chevaucher la bordure du parent */
  transition: all 0.3s;
}

/* 3. Style de l'onglet actif (quand la radio est cochée) */
#tab1:checked ~ .tab-labels label[for="tab1"],
#tab2:checked ~ .tab-labels label[for="tab2"],
#tab3:checked ~ .tab-labels label[for="tab3"] {
  color: var(--accent);
  border-bottom-color: var(--accent);
}

/* 4. Gestion des panneaux */
.tab-panel {
  display: none; /* Tout est caché par défaut */
  animation: fadeIn 0.4s ease;
}

/* Affichage du panel correspondant au radio coché */
#tab1:checked ~ .tab-panels #panel1,
#tab2:checked ~ .tab-panels #panel2,
#tab3:checked ~ .tab-panels #panel3 {
  display: block;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(5px); }
  to { opacity: 1; transform: translateY(0); }
}
```

---

### 👁️ Observation pour l'étudiant
> "C'est l'un des usages les plus intelligents du CSS. En utilisant les ID et les labels, on crée une véritable logique applicative sans une seule ligne de JS. Regardez comment le panneau semble 'apparaître' grâce à la petite animation `fadeIn` que nous avons ajoutée."

**Vérification :**
1. Est-ce que le texte change bien quand vous cliquez sur un autre onglet ?
2. L'onglet actif a-t-il bien sa bordure violette ?
3. Le contenu des autres onglets est-il bien invisible ?


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

# 🛠️ Exercice 11.5 — Accordéon FAQ (Balises Natives)

L'objectif est de styliser ces balises pour qu'elles s'intègrent au design **DevPulse**. Nous allons remplacer la petite flèche standard du navigateur par une icône personnalisée et animée.

### 1. Comprendre les outils
* **`<details>`** : Le conteneur qui gère l'état (ouvert ou fermé).
* **`<summary>`** : La partie toujours visible. Cliquer dessus bascule l'état du parent.
* **`details[open]`** : Un sélecteur d'attribut CSS qui permet d'appliquer des styles spécifiques uniquement quand l'accordéon est ouvert.
* **`list-style: none`** : Utilisé sur le `summary` pour cacher le triangle gris par défaut (Chrome/Safari). Sur Firefox, on utilise souvent le sélecteur non-standard `::-webkit-details-marker`.

---

### 2. Action : Structure HTML
Voici la structure à intégrer. Elle est très légère car le comportement est déjà inclus dans le HTML.

```html
<div class="accordion">
  <details class="accordion-item">
    <summary class="accordion-header">Comment déployer mon application ?</summary>
    <div class="accordion-body">
      <p>Connectez votre repo GitHub, configurez votre pipeline CI/CD, et lancez le déploiement depuis le dashboard.</p>
    </div>
  </details>

  <details class="accordion-item" open> <summary class="accordion-header">Quels langages sont supportés ?</summary>
    <div class="accordion-body">
      <p>Nous supportons Node.js, Python, Go, Rust, Java, et PHP. Docker est aussi supporté pour les stacks custom.</p>
    </div>
  </details>

  <details class="accordion-item">
    <summary class="accordion-header">Comment contacter le support ?</summary>
    <div class="accordion-body">
      <p>Via le chat en direct, par email à support@devpulse.ma, ou via le canal Slack dédié.</p>
    </div>
  </details>
</div>
```

---

### 3. Action : Styliser et Animer (CSS)
Ajoutez ces règles dans votre fichier `style.css` :

```css
.accordion {
  max-width: 600px;
  margin-top: 30px;
}

.accordion-item {
  background-color: var(--surface);
  border: 1px solid rgba(255, 255, 255, 0.05);
  border-radius: var(--radius);
  margin-bottom: 12px;
  overflow: hidden; /* Pour que le body ne dépasse pas des coins arrondis */
  transition: border-color 0.3s;
}

.accordion-item[open] {
  border-color: var(--accent);
}

/* 1. L'en-tête cliquable */
.accordion-header {
  padding: 18px 20px;
  cursor: pointer;
  font-weight: 600;
  list-style: none; /* Cache la flèche par défaut */
  display: flex;
  justify-content: space-between;
  align-items: center;
  user-select: none;
}

/* Pour Safari (webkit) */
.accordion-header::-webkit-details-marker {
  display: none;
}

/* 2. Création de notre flèche personnalisée */
.accordion-header::after {
  content: "→";
  color: var(--accent);
  transition: transform 0.3s ease;
  font-size: 1.2rem;
}

/* Rotation de la flèche quand ouvert */
.accordion-item[open] .accordion-header::after {
  transform: rotate(90deg);
}

/* 3. Le contenu */
.accordion-body {
  padding: 0 20px 20px 20px;
  color: var(--text-muted);
  line-height: 1.6;
  font-size: 0.95rem;
  /* Animation simple d'entrée */
  animation: slideDown 0.3s ease-out;
}

@keyframes slideDown {
  from { opacity: 0; transform: translateY(-10px); }
  to { opacity: 1; transform: translateY(0); }
}
```

---

### 👁️ Observation pour l'étudiant
> "Remarquez que nous n'avons pas besoin de JS pour l'ouverture. Le navigateur gère tout. Notez aussi l'usage de `details[open]`. C'est extrêmement puissant pour changer l'apparence de l'en-tête (comme mettre le texte en gras ou changer la couleur de la bordure) uniquement lorsque le contenu est révélé."

**Vérification :**
1. Les flèches tournent-elles bien de 90 degrés à l'ouverture ?
2. Le contenu s'affiche-t-il avec une légère transition ?
3. Le triangle gris par défaut du navigateur a-t-il bien disparu ?



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

# 🛠️ Exercice 12.1 — Theming (Variables CSS & Switch)

L'objectif est d'implémenter un mode clair. Au lieu de réécrire le CSS pour chaque composant (boutons, cartes, tableaux), nous allons simplement **redéfinir la valeur des variables** à la racine du document.

### 1. Comprendre les outils
* **`:root`** : C'est le sélecteur de plus haut niveau (l'élément `<html>`). Les variables définies ici sont disponibles partout.
* **`:root.light`** : Lorsque nous ajoutons la classe `.light` à la balise `<html>`, le navigateur écrase les anciennes valeurs des variables par les nouvelles.
* **Héritage automatique** : Tous vos composants (cards, inputs, tables) qui utilisent `var(--surface)` se mettront à jour instantanément sans effort supplémentaire.

---

### 2. Action : Définir les palettes (CSS)
Mettez à jour le haut de votre fichier `style.css` pour inclure les deux thèmes.

```css
/* --- THÈME DARK (Par défaut) --- */
:root {
  --bg: #0f172a;
  --surface: #1e293b;
  --surface-2: #334155;
  --border: rgba(255, 255, 255, 0.05);
  --text: #f8fafc;
  --text-muted: #94a3b8;
  
  /* Couleurs d'accent (ne changent pas) */
  --accent: #6c5ce7;
  --success: #00b894;
  --danger: #ff7675;
  --radius: 12px;
}

/* --- THÈME LIGHT (Activé par la classe .light) --- */
:root.light {
  --bg: #f1f5f9;
  --surface: #ffffff;
  --surface-2: #e2e8f0;
  --border: #cbd5e1;
  --text: #0f172a;
  --text-muted: #64748b;
  
  /* On peut ajuster l'accent pour le mode clair si besoin */
  --accent: #5849c4; 
}
```

---

### 3. Action : Ajouter le bouton de contrôle (HTML)
Placez ce bouton dans votre barre de navigation (ou en haut de la page).

```html
<div class="theme-switcher">
  <button class="btn btn-outline" onclick="document.documentElement.classList.toggle('light')">
    🌗 Changer de thème
  </button>
</div>
```

---

### 4. Action : Assurer la fluidité (CSS)
Pour éviter un changement trop brutal pour les yeux, ajoutez cette règle globale :

```css
body {
  background-color: var(--bg);
  color: var(--text);
  /* Transition douce sur les couleurs de fond et de texte */
  transition: background-color 0.3s ease, color 0.3s ease;
  font-family: 'Inter', sans-serif;
  margin: 0;
}

/* On applique aussi la transition sur les conteneurs principaux */
.stat-card, .table-container, .register-form, .modal-box {
  transition: background-color 0.3s ease, border-color 0.3s ease, box-shadow 0.3s ease;
}
```

---

### 👁️ Observation pour l'étudiant
> "Cliquez sur le bouton. Magique, non ? C'est le principe du **Single Source of Truth** (Source de vérité unique). En mode clair, l'ombre de vos cartes (box-shadow) pourrait paraître trop sombre ; c'est le moment d'ajuster une variable `--shadow` pour parfaire le rendu. Cette méthode est exactement celle utilisée par les frameworks modernes comme Tailwind ou Bootstrap."

**Vérification :**
1. Toutes les zones de texte sont-elles lisibles en mode clair ?
2. Le fond de la page passe-t-il bien d'un bleu nuit à un gris très clair ?
3. Les bordures de vos tableaux et inputs sont-elles toujours visibles ?



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


---

# 🛠️ Exercice 12.2 — Les Classes Utilitaires (Système "Atomique")

L'objectif est d'écrire ces règles une seule fois dans ton fichier CSS pour ne plus jamais avoir à ouvrir ton `style.css` juste pour ajouter une marge ou centrer un texte.

### 1. Comprendre l'intérêt
* **DRY (Don't Repeat Yourself)** : Tu évites de réécrire `display: flex; align-items: center;` 50 fois dans ton code.
* **Rapidité** : Tu ajustes ton design directement dans le HTML.
* **Maintenance** : Si tu décides que `mt-2` doit être un peu plus grand, tu le changes à un seul endroit.

---

### 2. Action : Implémenter la boîte à outils (CSS)
Ajoute ce bloc à la toute fin de ton fichier `style.css`. Ce sont des classes "prioritaires".

```css
/* --- ESPACEMENT (Margins & Paddings) --- */
.mt-1 { margin-top: 0.5rem !important; }
.mt-2 { margin-top: 1rem !important; }
.mb-1 { margin-bottom: 0.5rem !important; }
.mb-2 { margin-bottom: 1rem !important; }
.p-1 { padding: 0.5rem !important; }
.p-2 { padding: 1rem !important; }

/* --- FLEXBOX (Raccourcis de mise en page) --- */
.flex { display: flex !important; }
.flex-center { 
  display: flex !important; 
  align-items: center !important; 
  justify-content: center !important; 
}
.flex-between { 
  display: flex !important; 
  align-items: center !important; 
  justify-content: space-between !important; 
}
.gap-1 { gap: 0.5rem !important; }
.gap-2 { gap: 1rem !important; }

/* --- TYPOGRAPHIE --- */
.text-muted { color: var(--text-muted) !important; }
.text-sm { font-size: 0.85rem !important; }
.text-center { text-align: center !important; }
.font-bold { font-weight: 700 !important; }

/* --- ACCESSIBILITÉ & VISIBILITÉ --- */
.hidden { display: none !important; }

/* SR-ONLY : Cache l'élément visuellement mais le laisse lisible par les lecteurs d'écran */
.sr-only { 
  position: absolute !absolute; 
  width: 1px !important; 
  height: 1px !important; 
  padding: 0 !important; 
  margin: -1px !important; 
  overflow: hidden !important; 
  clip: rect(0,0,0,0) !important; 
  border: 0 !important; 
}
```

---

### 3. Comment utiliser cette implémentation ?
Désormais, dans ton HTML, tu peux "composer" tes éléments comme ceci :

```html
<div class="flex-center mt-2 p-1 text-muted text-sm">
  <p>Dernière mise à jour : il y a 5 minutes</p>
</div>
```

### 👁️ Observation pour l'étudiant
> "Remarque l'utilisation du `!important`. Habituellement, on l'évite, mais pour les classes utilitaires, c'est une bonne pratique. Pourquoi ? Parce qu'une classe nommée `.hidden` **doit** cacher l'élément, peu importe les autres règles CSS qui pourraient s'appliquer dessus."

**Vérification :**
1. Est-ce que tes classes sont bien regroupées par catégorie ?
2. As-tu bien utilisé `rem` plutôt que `px` pour rester flexible ?
3. La classe `.sr-only` est-elle bien présente ? (C'est la base de l'accessibilité moderne).


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

C’est la phase de "polissage" final. Ces détails ne changent pas la structure de ton application **DevPulse**, mais ils transforment radicalement le ressenti de l'utilisateur (le fameux *UX*). Un site qui réagit bien au clic et qui gère proprement le focus est ce qui différencie un projet amateur d'un produit professionnel.

---

# 🛠️ Exercice 12.3 — Micro-Interactions & Finitions Pro

L'objectif est d'harmoniser le comportement global de ton interface. Ces règles s'appliquent généralement de manière globale (sur des balises comme `html`, `a`, ou des classes génériques).

### 1. Comprendre les outils
* **`user-select: none`** : Évite que le texte ne se surligne en bleu quand l'utilisateur clique frénétiquement sur un bouton ou un onglet.
* **`aspect-ratio`** : Une propriété moderne qui force un élément à garder ses proportions (ex: 16/9) sans avoir à calculer sa hauteur manuellement.
* **`focus-visible`** : C'est le "Graal" de l'accessibilité. Il affiche une bordure de focus uniquement quand on navigue au **clavier** (touche Tab), mais la cache pour les utilisateurs de souris.

---

### 2. Action : Implémenter les finitions (CSS)

Ajoute ces règles éparpillées selon leur importance (le `scroll-behavior` en haut, le reste avec tes composants) :

```css
/* --- 1. COMPORTEMENT GLOBAL --- */
html {
  scroll-behavior: smooth; /* Pour les ancres internes */
}

/* --- 2. ACCESSIBILITÉ MODERNE (Focus) --- */
/* On remplace l'outline moche par défaut par un style cohérent */
:focus-visible {
  outline: 2px solid var(--accent);
  outline-offset: 2px;
}

/* On retire l'outline pour les clics souris (car inutile visuellement) */
:focus:not(:focus-visible) {
  outline: none;
}

/* --- 3. CONFORT DE NAVIGATION --- */
a {
  transition: color 0.2s ease;
  color: var(--accent);
  text-decoration: none;
}

.btn, .tab-label, .accordion-header, .dropdown-trigger {
  user-select: none; /* Évite la sélection de texte accidentelle */
  cursor: pointer;   /* Force la main sur tout ce qui se clique */
}

/* --- 4. GESTION DES MÉDIAS --- */
/* Utile pour tes futures cards d'articles ou de projets */
.card-image {
  width: 100%;
  aspect-ratio: 16 / 9; /* Format cinéma */
  object-fit: cover;    /* L'image remplit l'espace sans se déformer */
  border-radius: var(--radius) var(--radius) 0 0;
}
```

---

### 3. Action : Mise en pratique (HTML)

Tu peux tester l'aspect-ratio avec une image fictive dans une carte :

```html
<div class="stat-card p-0" style="overflow:hidden">
  <img src="https://images.unsplash.com/photo-1461749280684-dccba630e2f6" class="card-image" alt="Code">
  <div class="p-2">
    <h4 class="mb-1">Aperçu du projet</h4>
    <p class="text-muted text-sm">Développement de l'API v2 en cours.</p>
  </div>
</div>
```

---

### 👁️ Observation pour l'étudiant
> "Essaye de naviguer sur ton dashboard en utilisant uniquement la touche **Tab** de ton clavier. Tu verras l'anneau de focus (outline) se déplacer proprement d'un élément à l'autre. C'est ce qui rend ton dashboard utilisable par tout le monde. Sans le `focus-visible`, un utilisateur au clavier est totalement perdu."

**Vérification :**
1. Quand tu cliques plusieurs fois sur un onglet, est-ce que le texte reste propre (pas de bleu) ?
2. L'image de test garde-t-elle bien ses proportions sans être écrasée ?
3. Le changement de couleur sur les liens est-il fluide ?

