# Routage SPA — History API / pushState

## État : ✅ Implémenté et déployé (branche `seo-routing`)

---

## Objectif

Remplacer le système d'iframe (URL figée sur `index.html`) par un routeur
JavaScript utilisant `history.pushState()`. Chaque page a une URL propre et
indexable, sans rechargement complet.

---

## URLs

| Page | URL |
|------|-----|
| Accueil | `aboriginalway.fr/` |
| Exposition | `aboriginalway.fr/exposition` |
| Artistes & Vidéos | `aboriginalway.fr/artistes` |
| Photos | `aboriginalway.fr/photos` |
| Animation Peinture | `aboriginalway.fr/animation-peinture` |
| Didgeridoo | `aboriginalway.fr/didgeridoo` |
| Activités / Cultures | `aboriginalway.fr/activites` |
| Présentation | `aboriginalway.fr/presentation` |
| Membres | `aboriginalway.fr/membres` |
| Partenaires | `aboriginalway.fr/partenaires` |
| Contact | `aboriginalway.fr/contact` |

---

## Architecture

```
Requête : https://aboriginalway.fr/exposition
    │
    ▼
.htaccess RewriteRule → index.html (layout complet)
    │
    ▼
JS router lit window.location.pathname ("/exposition")
→ fetch("/site/ref/documents/exposition.html")
→ extrait <div id="container"> (id supprimé pour éviter conflits CSS)
→ résout tous les attributs [src] en URLs absolues
→ injecte innerHTML dans <div id="content">
→ applique le fond via bodytexte.style.backgroundImage
→ history.pushState("/exposition", ...)
```

**Accès direct / F5 / partage de lien** : `.htaccess` renvoie toujours
`index.html`, le router lit l'URL et charge le bon contenu.

---

## Fichiers modifiés

### `/.htaccess`

```apache
RewriteEngine On
RewriteBase /

# Redirections 301 : uniquement pour les navigations directes (pas les fetch SPA)
RewriteCond %{HTTP:X-Fetch-Content} !1
RewriteRule ^site/ref/documents/home\.html$ / [R=301,L]
# ... (idem pour les 10 autres pages desktop)

# SPA Router
RewriteRule ^index\.html$ - [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.html [L]
```

### `/index.html`

- Iframe supprimée → `<div id="content" style="width:100%;height:100%;overflow-y:auto;">`
- Tous les liens du menu : `target="texte"` → `data-route="/xxx"` + `href="/xxx"`
- Script router complet : `routes{}`, `navigate()`, `popstate`, `DOMContentLoaded`
- `setupLightbox()` : lightbox vanilla JS pour la galerie photos
- `initPhotoGrid()` : attache les handlers de clic directement sur les `<a>` de la grille après injection
- Fond appliqué via JS sur `#bodytexte` (accueil = noir, autres = `url('/site/ref/image/Fond.jpg')`)

### `site/ref/documents/*.html` (11 pages desktop)

- Open Graph, Twitter Cards, `robots` meta ajoutés sur toutes les pages
- Canonicals mis à jour vers URLs propres (`https://aboriginalway.fr/exposition`, etc.)
- `Fond2.jpg` → `Fond.jpg` (Fond2.jpg n'existe pas)
- `type="text/css"`, `frameborder`, `webkitallowfullscreen`, `mozallowfullscreen` supprimés
- `membres.html` : `noindex`

### `site/ref/documents/photo.html`

- VisualLightBox (jQuery) remplacé par grille CSS native + lightbox vanilla JS
- Grille 5 colonnes, miniatures 80px de hauteur, effet hover
- `data-full` et `data-caption` sur chaque `<a>` pour le lightbox
- Chemins résolus via `new URL(data-full, baseUrl).href`

### `site/ref/documents/contact.html`

- Images de brochure : `width:580px; max-width:100%` (pleine largeur de la zone)

### `site/ref/documents/exposition.html`

- Vidéo et textes centrés via styles inline directs

### `mobile/*.html` (11 fichiers)

- Footer : `© Aboriginal Way — fondée en 2007` → `© Aboriginal Way`

### `/sitemap.xml`

- URLs mises à jour : `/site/ref/documents/xxx.html` → URLs propres
- `membres.html`, `liens.html`, `temps.html` retirés

---

## Points techniques notables

### Cohabitation redirects 301 et fetch SPA

Les redirects 301 (`site/ref/documents/*.html` → URLs propres) sont nécessaires
pour le SEO, mais casseraient le router SPA : `fetch('/site/ref/documents/home.html')`
suivrait le redirect vers `/` et injecterait `index.html` entier dans `#content`.

Solution : le `fetch` envoie `X-Fetch-Content: 1`, et chaque RewriteRule de
redirect est précédée de `RewriteCond %{HTTP:X-Fetch-Content} !1`.

```javascript
const response = await fetch(route.src, { headers: { 'X-Fetch-Content': '1' } });
```

```apache
RewriteCond %{HTTP:X-Fetch-Content} !1
RewriteRule ^site/ref/documents/home\.html$ / [R=301,L]
```

### Extraction du contenu

Le router extrait `#container` (et non `#texte` comme prévu initialement) pour
capturer l'ensemble du contenu de chaque page, puis supprime l'id pour éviter
les conflits CSS avec le `#container` de `index.html`.

```javascript
const container = doc.getElementById('container');
if (container) container.removeAttribute('id');
const source = container || doc.body;
content.innerHTML = source.innerHTML;
```

### Résolution des chemins d'images

Les pages desktop utilisent des chemins relatifs (`../image/...`). Après
injection dans `index.html` (à la racine), ces chemins seraient invalides.
Solution : résolution en URLs absolues avant injection.

```javascript
const base = window.location.origin + route.src;
source.querySelectorAll('[src]').forEach(el => {
  try { el.setAttribute('src', new URL(el.getAttribute('src'), base).href); }
  catch (e) {}
});
```

### Fond de page

Le fond `Fond.jpg` est appliqué via JS (pas CSS) pour éviter les problèmes de
résolution de chemin relatif sur le serveur.

```javascript
if (path === '/') {
  bodytexte.style.backgroundImage = 'none';
  bodytexte.style.backgroundColor = 'black';
} else {
  bodytexte.style.backgroundImage = "url('/site/ref/image/Fond.jpg')";
  bodytexte.style.backgroundColor = '';
}
```

### Galerie photos — lightbox vanilla JS

VisualLightBox (jQuery) remplacé par une solution sans dépendance.
`initPhotoGrid()` est appelée par `navigate()` après injection pour attacher
les handlers directement sur les `<a>` (plus fiable que l'event delegation).

```javascript
if (path === '/photos') initPhotoGrid();
```

---

## Tests effectués sur http://tuyo2268.odns.fr/

- [x] Accès direct `/` → accueil (fond noir)
- [x] Navigation entre pages → URL change, fond Fond.jpg s'affiche
- [x] Bouton retour navigateur → URL et contenu corrects
- [x] F5 sur `/exposition` → rechargement correct via `.htaccess`
- [x] Images sidebar changent selon la rubrique
- [x] Menus déroulants (hover) fonctionnent
- [x] Redirection mobile (≤ 768px → `mobile/`)
- [x] Galerie photos : grille + lightbox (clic, flèches, Échap)
- [x] Vidéo exposition centrée
- [x] Brochure contact pleine largeur

