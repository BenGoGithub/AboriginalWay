# Mobile — Aboriginal Way

Version mobile dédiée du site Aboriginal Way. Accessible via redirection automatique depuis `index.html` pour les appareils `≤ 768px`.

---

## Structure

```
mobile/
├── mobile.css              # CSS partagé pour toutes les pages
├── index.html              # Accueil mobile (hub de navigation)
├── activites.html          # Hub des activités culturelles
├── animation-peinture.html # Atelier peinture aborigène + vidéo Vimeo
├── artistes.html           # Artistes + 2 vidéos YouTube
├── contact.html            # Contact (tel: cliquable + mailto:)
├── cuisine.html            # Cuisine bush tucker + vidéo Dailymotion
├── didgeridoo.html         # Cours de didgeridoo
├── exposition.html         # Exposition An Other Way + vidéo YouTube
├── membres.html            # Espace membres (En construction)
├── partenaires.html        # Le Rêve de l'Aborigène + Territory Essence
├── photos.html             # Galerie photos CSS grid (27 photos)
└── presentation.html       # Présentation de l'association
```

---

## Architecture technique

### CSS partagé (`mobile.css`)

Un seul fichier CSS pour toutes les pages. Composants disponibles :

| Classe | Usage |
|--------|-------|
| `.card` | Bloc de contenu sur fond semi-transparent |
| `.back-btn` | Bouton retour dans le header |
| `.warning` | Avertissement artistes décédés |
| `.video-wrapper` | Conteneur vidéo responsive 16:9 |
| `.artist-list` | Liste d'artistes sans puces |
| `.contact-link` | Lien d'action (tel/email) avec icône |
| `.btn` | Bouton rouge d'action |
| `.photo-grid` | Grille photos 3 colonnes |
| `.partner` | Bloc partenaire centré |
| `.construction` | Page en construction |
| `.intro` / `.home-photos` / `nav` | Spécifiques à `index.html` |

### Vidéos responsives

Toutes les vidéos utilisent la technique padding-bottom 56.25% (ratio 16:9) :

```html
<div class="video-wrapper">
  <iframe src="..." allowfullscreen title="..."></iframe>
</div>
```

Pas de Flash, pas de jQuery.

---

## SEO

Chaque page respecte les règles suivantes :

- `lang="fr"` sur `<html>`
- `<title>` entre 50 et 65 caractères
- `<meta name="description">` pertinente
- `<h1>` visible et unique
- HTML sémantique : `<header>`, `<main>`, `<footer>`
- `loading="lazy"` sur toutes les images de la galerie

### Données structurées

`index.html` contient un bloc JSON-LD `Organization` et les balises Open Graph :

```html
<meta property="og:title" content="Aboriginal Way - Le Chemin Aborigène">
<meta property="og:description" content="...">
<meta property="og:type" content="website">
<meta property="og:url" content="https://aboriginalway.fr/mobile/">
<meta property="og:image" content="https://aboriginalway.fr/site/ref/image/Bhgrand.jpg">
```

---

## Redirection

La redirection est gérée dans `index.html` (racine du site) :

```js
if (window.matchMedia("(max-width: 768px)").matches) {
  window.location.replace("mobile/index.html");
}
```

---

## Liens desktop

Les pages mobiles sont **autonomes** et n'embarquent pas les pages desktop. Aucune dépendance aux iframes ni au CSS `site/ref/style/general.css`.

Les ressources statiques (images, favicon) sont partagées avec le site desktop via des chemins relatifs vers `../site/ref/image/`.
