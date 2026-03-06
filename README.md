# Aboriginal Way - Analyse & Plan d'Améliorations

Site web vitrine pour l'association **Aboriginal Way**, fondée en **2007**, dédiée à la promotion de l'art et de la culture aborigène australienne (expositions, ateliers peinture, didgeridoo, cuisine bush tucker).

Le site date d'environ 2008-2012 et a été archivé via HTTrack. Il repose sur des technologies obsolètes (HTML 4.01, iframes, Flash) et nécessite une refonte complète pour répondre aux standards actuels.

---

## Changements réalisés

| Fichier | Modification |
|---------|-------------|
| `site/ref/documents/partenaires.html` | Réécriture complète : suppression Territory Essence (ancienne), Burrup ; ajout Le Rêve de l'Aborigène (logo, description, dates 24-26 juillet 2026, bouton billetterie) ; réintégration Territory Essence avec image locale |
| `site/ref/documents/artistes.html` | Suppression des liens vers les pages individuelles d'artistes ; ajout warning en anglais sur les artistes décédés ; vidéo Penny Green ajoutée sous la vidéo principale |
| `site/ref/documents/exposition.html` | Ajout warning artistes décédés ; correction lien contact (`mailto:` manquant) |
| `site/ref/documents/photo.html` | Ajout warning artistes décédés |
| `site/ref/documents/presentation.html` | Ajout de la date de fondation de l'association : 2007 |
| `index.html` | Suppression widget AddThis et iframe Facebook Like obsolètes |
| `sitemap.xml` | Correction XML invalide, ajout pages manquantes |
| `pinterest-d243d.html` | Correction attribut `lang` |

---

## Structure actuelle

```
AboriginalWay/
├── index.html              # Point d'entrée (layout iframe)
├── general.css             # CSS racine (dupliqué)
├── sitemap.xml             # Sitemap basique (15 URLs)
├── robots.txt              # Minimal (référence sitemap uniquement)
├── site/ref/
│   ├── documents/          # Pages de contenu (~15 pages)
│   │   ├── artiste/        # Fiches artistes (7 biographies)
│   │   └── engine/         # VisualLightBox (jQuery plugin galerie)
│   ├── style/general.css   # CSS dupliqué
│   └── image/              # Images (~94 fichiers)
└── logs/traffic.html/      # Statistiques de trafic
```

---

## Problèmes identifiés

### CRITIQUE - Accessibilité

| Problème | Exemple |
|----------|---------|
| Pas de navigation clavier | Menus basés sur `onmouseover`/`onmouseout` uniquement |
| Attribut `lang` manquant | Absent sur la quasi-totalité des pages |
| Textes alternatifs manquants | Images de la galerie sans `alt` |
| Pas de HTML sémantique | Aucun `<nav>`, `<main>`, `<header>`, `<section>` |
| Pas de skip links | Impossible de passer la navigation |
| Contrastes non vérifiés | Couleurs hardcodées (`#9B1A1B`, `#8A97B3`) sans test WCAG |

### CRITIQUE - Mobile

> **Approche retenue : page mobile dédiée** (`/mobile/index.html`) avec redirection automatique depuis `index.html`. Le site desktop existant n'est pas refondu en responsive.

| Problème | Exemple |
|----------|---------|
| Pas de version mobile | Layout fixe 920px, inutilisable sur smartphone |
| Pas de redirection device | Aucune détection User-Agent ou `matchMedia` |
| Layout en positionnement absolu | `#bodytexte { top:70px; left:300px; width:620px; }` |
| Images non responsives | Pas de `srcset`, pas de `<picture>`, pas de lazy loading |
| Layout principal en iframe | Le contenu est chargé dans un `<iframe>` rigide |

### CRITIQUE - Sécurité

| Problème | Exemple |
|----------|---------|
| Contenu mixte HTTP/HTTPS | Scripts externes en `http://` (addthis, Facebook) |
| Embeds Flash obsolètes | `<embed type="application/x-shockwave-flash">` (YouTube, Dailymotion) |
| Handlers inline | `onclick="change(...)"`, `onmouseover="showmenu(...)"` |
| Chemin local exposé | `href="file:///C:/Documents%20and%20Settings/BEN/Bureau/..."` |
| Aucun CSP | Pas d'en-tête Content-Security-Policy |
| API JS dépréciée | `document.getElementById('menu1').fontcolor("Red")` |

### HAUTE - SEO

| Problème | Exemple |
|----------|---------|
| Meta descriptions absentes | Aucune page n'a de `<meta name="description">` |
| Contenu dans un iframe | Les moteurs ne peuvent pas indexer le contenu principal |
| Pas de balises Open Graph | Aucune metadata pour le partage social |
| Hiérarchie de titres cassée | Pages sans `<h1>`, ou saut de niveaux |
| URLs problématiques | `Activités..html` (double point), `Animation Peinture.html` (espace) |
| Liens internes cassés | Références à `artistes3.html` inexistant |
| DOCTYPE incohérent | Mix de HTML 4.01 Transitional, Strict, et XHTML 1.0 |
| Sitemap incomplet | Pages artistes manquantes |

### HAUTE - Performance

| Problème | Exemple |
|----------|---------|
| Images non optimisées | 94 images en JPG/PNG, pas de WebP, pas de compression |
| Scripts bloquants | `<script src="...">` sans `async`/`defer` |
| jQuery pour usage minimal | ~30 KB pour 3 fonctions simples |
| Pas de cache configuré | Aucun en-tête cache visible |
| CSS non minifié | Double fichier CSS identique |

### HAUTE - Qualité du code

| Problème | Exemple |
|----------|---------|
| CSS dupliqué | `general.css` identique à la racine et dans `site/ref/style/` |
| Balises dépréciées | `<font>`, `bgcolor`, `border`, `valign`, `align` |
| Styles inline massifs | `style="left: 548px; width: 372px;"` sur de nombreux éléments |
| Encodage incohérent | Mix ISO-8859-1 / UTF-8 |
| Nommage non sémantique | Classes `.home1`, `.home2`, `.home3` sans signification |
| Unités CSS manquantes | `width:920;` au lieu de `width:920px;` |
| Polices sans fallback | `font-family: Century gothic;` sans générique |
| Fonctions JS globales | `change()`, `showmenu()`, `hidemenu()` sans namespace |
| Attributs sans guillemets | `<div id=container>` |

### HAUTE - Infrastructure & SEO technique

| Problème | Détail |
|----------|--------|
| Aucun CDN | Aucun Content Delivery Network activé ; les ressources statiques (images, CSS, JS) sont servies directement sans cache distribué, impactant les temps de chargement |
| Description de page absente | Aucune `<meta name="description">` sur le site ; le site n'affiche aucun extrait pertinent dans les résultats de recherche |
| Titre de page trop court | Le `<title>` actuel (`Aboriginal Way`, 14 caractères) manque de pertinence ; un titre optimal se situe entre 50 et 60 caractères |
| Favicon non optimisé | Le favicon actuel n'est pas décliné aux formats modernes (SVG, Apple Touch Icon, manifeste PWA) |
| Aucune optimisation mobile | Pas de viewport, pas de media queries, layout fixe 920px ; le site est inutilisable sur smartphones et tablettes |

---

## Plan d'améliorations recommandé

### Phase 1 - Refonte structurelle

> **Approche mobile retenue :** pas de refonte responsive du site existant. Une page dédiée `/mobile/index.html` sera créée, avec une redirection automatique depuis `index.html` selon le type d'appareil détecté (User-Agent / `matchMedia`).

- [x] Migrer vers **HTML5** avec DOCTYPE uniforme *(partenaires, artistes)*
- [ ] Remplacer le layout iframe par une **architecture SPA ou multi-pages** classique
- [ ] Créer `/mobile/index.html` — version mobile dédiée du site
- [ ] Ajouter dans `index.html` une redirection JS vers `/mobile/index.html` pour les appareils mobiles
- [ ] Restructurer avec des balises sémantiques (`<header>`, `<nav>`, `<main>`, `<footer>`, `<article>`)
- [ ] Unifier l'encodage en **UTF-8**
- [ ] Corriger les noms de fichiers (supprimer espaces, accents, doubles points)
- [ ] Supprimer le CSS dupliqué

### Phase 2 - Accessibilité (WCAG 2.1 AA)

- [ ] Ajouter `lang="fr"` sur toutes les balises `<html>`
- [ ] Implémenter la navigation clavier complète
- [ ] Ajouter des skip links
- [ ] Vérifier et corriger les contrastes de couleurs
- [ ] Ajouter des `alt` descriptifs sur toutes les images
- [ ] Remplacer les menus hover-only par des menus accessibles (focus + aria)

### Phase 3 - SEO & Contenu

- [x] Ajouter `<meta name="description">` et `<title>` pertinents sur chaque page *(fait sur les pages réécrites)*
- [ ] Implémenter les balises Open Graph et Twitter Card
- [ ] Construire une hiérarchie de titres cohérente (H1 > H2 > H3)
- [x] Régénérer le `sitemap.xml` complet
- [ ] Configurer `robots.txt` avec directives appropriées
- [ ] Ajouter des URLs canoniques
- [ ] Ajouter des données structurées Schema.org (artistes, expositions, organisation)
- [x] Corriger ou supprimer les liens cassés *(liens artistes, mailto contact)*

### Phase 3b - Contenu à modifier

- [ ] **Supprimer toute mention à l'Atelier du Héron** : retirer les références, pages et liens associés
- [ ] **Supprimer toute mention aux yourtes** : retirer la page `Yourtes.html` et les références associées dans la navigation et le contenu
- [ ] **Section Membres** : remplacer le contenu actuel par une page **"En construction"** affichant une adresse e-mail de contact

### Phase 4 - Sécurité & Performance

- [x] Migrer tous les liens externes vers **HTTPS** *(partenaires, artistes)*
- [ ] Remplacer les embeds Flash par des **iframes YouTube/Vimeo modernes**
- [ ] Supprimer les handlers inline, utiliser `addEventListener`
- [ ] Ajouter des en-têtes de sécurité (CSP, X-Frame-Options, X-Content-Type-Options)
- [ ] Optimiser les images (WebP, compression, lazy loading avec `loading="lazy"`)
- [ ] Supprimer jQuery, réécrire en **vanilla JS** moderne
- [ ] Ajouter `async` ou `defer` sur les scripts
- [ ] Configurer le cache HTTP

### Phase 5 - Modernisation optionnelle

- [ ] Envisager un **générateur de site statique** (Hugo, Eleventy, Astro) pour faciliter la maintenance
- [ ] Mettre en place un **système de templates** pour éliminer la duplication HTML
- [ ] Ajouter une galerie photo moderne (sans dépendance lourde)
- [ ] Intégrer un outil d'analytics respectueux (Matomo, Plausible)
- [ ] Mettre en place un formulaire de contact fonctionnel (au lieu de l'email obfusqué)
- [x] Initialiser un dépôt **Git** pour le suivi des modifications

---

## Technologies actuelles vs. recommandées

| Aspect | Actuel | Recommandé |
|--------|--------|------------|
| HTML | 4.01 Transitional (mix) | HTML5 |
| Layout | Tables + position absolute + iframes | CSS Grid / Flexbox |
| CSS | Un fichier dupliqué, pas de variables | CSS custom properties, méthodologie BEM |
| JavaScript | Inline handlers, jQuery, Flash | Vanilla JS ES6+, modules |
| Images | JPG/PNG non optimisés | WebP + fallback, lazy loading |
| Responsive | Aucun | Page mobile dédiée `/mobile/index.html` + redirection JS |
| SEO | Minimal | Meta tags, Open Graph, Schema.org, sitemap complet |
| Accessibilité | Non conforme | WCAG 2.1 AA |
| Sécurité | HTTP, inline scripts, Flash | HTTPS, CSP, SRI |
| Outils | HTTrack (archivage) | Git, SSG (Eleventy/Astro), CI/CD |