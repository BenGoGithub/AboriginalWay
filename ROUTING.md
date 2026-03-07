# Plan d'action — Routage SEO-friendly (History API / pushState)

## Objectif

Remplacer le système d'iframe qui fige l'URL sur `index.html` par un routeur
JavaScript utilisant `history.pushState()`. Chaque page aura une URL propre et
indexable, sans rechargement complet de la page.

URLs cibles :

| Page | URL actuelle (iframe) | Nouvelle URL |
|------|-----------------------|--------------|
| Accueil | `aboriginalway.fr/` | `aboriginalway.fr/` |
| Exposition | *(aucune)* | `aboriginalway.fr/exposition` |
| Artistes & Vidéos | *(aucune)* | `aboriginalway.fr/artistes` |
| Photos | *(aucune)* | `aboriginalway.fr/photos` |
| Animation Peinture | *(aucune)* | `aboriginalway.fr/animation-peinture` |
| Didgeridoo | *(aucune)* | `aboriginalway.fr/didgeridoo` |
| Activités / Cultures | *(aucune)* | `aboriginalway.fr/activites` |
| Présentation | *(aucune)* | `aboriginalway.fr/presentation` |
| Membres | *(aucune)* | `aboriginalway.fr/membres` |
| Partenaires | *(aucune)* | `aboriginalway.fr/partenaires` |
| Contact | *(aucune)* | `aboriginalway.fr/contact` |

---

## Architecture cible

```
Requête utilisateur : https://aboriginalway.fr/exposition
        │
        ▼
  .htaccess RewriteRule
  → index.html (shell : menu, sidebar, layout)
        │
        ▼
  JS router lit window.location.pathname ("/exposition")
  → fetch("site/ref/documents/exposition.html")
  → extrait <div id="texte"> (ou <body>)
  → injecte dans <div id="content">
  → history.pushState("/exposition", ...)
```

**Accès direct** (partage de lien, retour arrière, F5) : le `.htaccess` renvoie
toujours `index.html`, le router lit l'URL et charge le bon contenu.

**Accès aux pages desktop seules** (ex. : depuis Google) : les pages
`/site/ref/documents/*.html` restent accessibles telles quelles — elles ont
déjà leurs balises SEO complètes.

---

## Étapes détaillées

### Étape 1 — Créer `.htaccess` avec règle de réécriture

Fichier : `/.htaccess` (racine du site)

```apache
Options -MultiViews
RewriteEngine On
RewriteBase /

# Ne pas réécrire les fichiers et dossiers existants
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d

# Ne pas réécrire les ressources statiques
RewriteCond %{REQUEST_URI} !^/site/
RewriteCond %{REQUEST_URI} !^/mobile/
RewriteCond %{REQUEST_URI} !^/logs/

# Tout le reste → index.html
RewriteRule ^ index.html [L]
```

**Pourquoi** : sans cette règle, une requête directe sur
`https://aboriginalway.fr/exposition` retournerait une erreur 404 car ce
fichier n'existe pas sur le disque. Apache doit renvoyer `index.html` pour que
le JS router prenne le relai.

---

### Étape 2 — Modifier `index.html` : remplacer l'iframe par un `<div>`

**Supprimer** (ligne 60) :
```html
<iframe style="width: 100%; height: 100%; background-color: rgb(255, 255, 255);"
        name="texte"
        src="site/ref/documents/home.html"
        frameborder="0" height="100%" width="100%">
</iframe>
```

**Remplacer par** :
```html
<div id="content" style="width: 100%; height: 100%; background-color: rgb(255, 255, 255); overflow-y: auto;"></div>
```

---

### Étape 3 — Supprimer `target="texte"` de tous les liens du menu

Dans `index.html`, chaque lien du menu a `target="texte"`. Il faut les
transformer en liens normaux interceptés par le router JS.

**Avant** :
```html
<a href="site/ref/documents/exposition.html" target="texte" class="menu" onclick="change(...)">
```

**Après** :
```html
<a href="/exposition" class="menu" data-img="site/ref/image/Serpent.jpg">
```

Mapping complet des `href` à appliquer :

| Ancien `href` | Nouveau `href` | `data-img` |
|---------------|----------------|------------|
| `site/ref/documents/activites.html` | `/activites` | `site/ref/image/Gecko.jpg` |
| `site/ref/documents/animation-peinture.html` | `/animation-peinture` | `site/ref/image/Gecko.jpg` |
| `site/ref/documents/didgeridoo.html` | `/didgeridoo` | `site/ref/image/Gecko.jpg` |
| `site/ref/documents/exposition.html` | `/exposition` | `site/ref/image/Serpent.jpg` |
| `site/ref/documents/artistes.html` | `/artistes` | `site/ref/image/Serpent.jpg` |
| `site/ref/documents/photo.html` | `/photos` | `site/ref/image/Serpent.jpg` |
| `site/ref/documents/presentation.html` | `/presentation` | `site/ref/image/Libellule.jpg` |
| `site/ref/documents/membres.html` | `/membres` | `site/ref/image/Libellule.jpg` |
| `site/ref/documents/partenaires.html` | `/partenaires` | `site/ref/image/Libellule.jpg` |
| `site/ref/documents/contact.html` | `/contact` | `site/ref/image/Bhpetit.jpg` |

**Supprimer également** les `onclick="change(...)"` inline — ce sera géré par
le router via `data-img`.

---

### Étape 4 — Écrire le router JS dans `index.html`

Remplacer les fonctions `change()`, `showmenu()`, `hidemenu()` et le bloc de
redirection mobile par ce script :

```javascript
// Table de routage : pathname → fichier source + image sidebar
const routes = {
  '/':                    { src: 'site/ref/documents/home.html',             img: 'site/ref/image/Bhgrand.jpg' },
  '/exposition':          { src: 'site/ref/documents/exposition.html',        img: 'site/ref/image/Serpent.jpg' },
  '/artistes':            { src: 'site/ref/documents/artistes.html',          img: 'site/ref/image/Serpent.jpg' },
  '/photos':              { src: 'site/ref/documents/photo.html',             img: 'site/ref/image/Serpent.jpg' },
  '/animation-peinture':  { src: 'site/ref/documents/animation-peinture.html',img: 'site/ref/image/Gecko.jpg'   },
  '/didgeridoo':          { src: 'site/ref/documents/didgeridoo.html',        img: 'site/ref/image/Gecko.jpg'   },
  '/activites':           { src: 'site/ref/documents/activites.html',         img: 'site/ref/image/Gecko.jpg'   },
  '/presentation':        { src: 'site/ref/documents/presentation.html',      img: 'site/ref/image/Libellule.jpg'},
  '/membres':             { src: 'site/ref/documents/membres.html',           img: 'site/ref/image/Libellule.jpg'},
  '/partenaires':         { src: 'site/ref/documents/partenaires.html',       img: 'site/ref/image/Libellule.jpg'},
  '/contact':             { src: 'site/ref/documents/contact.html',           img: 'site/ref/image/Bhpetit.jpg'  },
};

// Charge une page dans #content sans rechargement
async function navigate(path, pushState = true) {
  const route = routes[path] || routes['/'];

  // Mise à jour image sidebar
  document.getElementById('visuel').src = route.img;

  // Chargement du contenu
  const response = await fetch(route.src);
  const html = await response.text();
  const parser = new DOMParser();
  const doc = parser.parseFromString(html, 'text/html');

  // Extraire #texte si disponible, sinon tout le <body>
  const content = doc.getElementById('texte') || doc.body;
  document.getElementById('content').innerHTML = content.innerHTML;

  // Mise à jour de l'URL et du <title>
  const pageTitle = doc.title || 'Aboriginal Way';
  if (pushState) history.pushState({ path }, pageTitle, path);
  document.title = pageTitle;

  // Remonter en haut du contenu
  document.getElementById('content').scrollTop = 0;
}

// Gestion du bouton retour/avant du navigateur
window.addEventListener('popstate', (e) => {
  navigate(e.state?.path || '/', false);
});

// Interception des clics sur les liens du menu
document.addEventListener('DOMContentLoaded', () => {
  // Redirection mobile
  if (window.matchMedia('(max-width: 768px)').matches) {
    window.location.replace('mobile/index.html');
    return;
  }

  // Délégation d'événement sur tous les liens internes
  document.querySelectorAll('a[href^="/"]').forEach(link => {
    link.addEventListener('click', (e) => {
      e.preventDefault();
      navigate(link.getAttribute('href'));
    });
  });

  // Charge la page correspondant à l'URL courante (accès direct ou F5)
  navigate(window.location.pathname, false);
});

// Menus déroulants (inchangé)
function showmenu(elmnt) { document.getElementById(elmnt).style.visibility = 'visible'; }
function hidemenu(elmnt) { document.getElementById(elmnt).style.visibility = 'hidden'; }
```

---

### Étape 5 — Mettre à jour les canonicals dans les pages desktop

Les pages `site/ref/documents/*.html` ont des canonicals qui pointent vers
leurs propres chemins. Il faut les mettre à jour pour pointer vers les
nouvelles URLs propres, afin que Google ne soit pas confus entre les deux
versions.

| Fichier | Canonical actuel | Canonical cible |
|---------|-----------------|----------------|
| `home.html` | `…/site/ref/documents/home.html` | `https://aboriginalway.fr/` |
| `exposition.html` | `…/site/ref/documents/exposition.html` | `https://aboriginalway.fr/exposition` |
| `artistes.html` | `…/site/ref/documents/artistes.html` | `https://aboriginalway.fr/artistes` |
| `photo.html` | `…/site/ref/documents/photo.html` | `https://aboriginalway.fr/photos` |
| `animation-peinture.html` | `…/animation-peinture.html` | `https://aboriginalway.fr/animation-peinture` |
| `didgeridoo.html` | `…/didgeridoo.html` | `https://aboriginalway.fr/didgeridoo` |
| `activites.html` | `…/activites.html` | `https://aboriginalway.fr/activites` |
| `presentation.html` | `…/presentation.html` | `https://aboriginalway.fr/presentation` |
| `membres.html` | `…/membres.html` | `https://aboriginalway.fr/membres` |
| `partenaires.html` | `…/partenaires.html` | `https://aboriginalway.fr/partenaires` |
| `contact.html` | `…/contact.html` | `https://aboriginalway.fr/contact` |

> **Note** : `liens.html` et `temps.html` ne sont pas dans le menu principal —
> garder leurs canonicals actuels ou les retirer du sitemap si elles ne sont
> plus liées.

---

### Étape 6 — Mettre à jour `sitemap.xml`

Remplacer les URLs `/site/ref/documents/xxx.html` par les nouvelles URLs
propres. Le sitemap doit lister uniquement les URLs canoniques.

```xml
<!-- Avant -->
<loc>https://aboriginalway.fr/site/ref/documents/exposition.html</loc>

<!-- Après -->
<loc>https://aboriginalway.fr/exposition</loc>
```

---

### Étape 7 — Mettre à jour les balises Open Graph dans `index.html`

Les balises OG de `index.html` servent pour les partages sociaux sur la page
d'accueil. Pour les autres pages, les OG sont dans les fichiers desktop — ils
resteront corrects pour les accès directs aux fichiers. Pour les accès via le
router, le `document.title` est mis à jour dynamiquement (étape 4).

---

### Étape 8 — Tests à effectuer avant merge

- [ ] Accès direct `https://aboriginalway.fr/` → affiche l'accueil
- [ ] Clic sur "Exposition" → URL devient `/exposition`, contenu chargé
- [ ] Bouton retour navigateur → URL et contenu reviennent à la page précédente
- [ ] F5 sur `/exposition` → page se recharge correctement (grâce au `.htaccess`)
- [ ] Partage du lien `/artistes` → ouvre directement la bonne page
- [ ] Image sidebar change au clic sur les différentes rubriques
- [ ] Menus déroulants fonctionnent toujours (hover)
- [ ] Redirection mobile fonctionne toujours (≤ 768px → `/mobile/`)
- [ ] Galerie photo (`/photos`) : le lightbox jQuery se réinitialise correctement
      après injection dans le DOM *(point délicat — voir note ci-dessous)*
- [ ] Vérifier avec Google Search Console (après déploiement)

> **Point délicat — Galerie photo** : `photo.html` utilise jQuery + le plugin
> VisualLightBox, initialisés au chargement de la page. Après injection via
> `innerHTML`, ces scripts ne se ré-exécutent pas automatiquement. Il faudra,
> après injection du contenu de `photo.html`, ré-exécuter le script du plugin :
> ```javascript
> if (path === '/photos') {
>   const script = document.createElement('script');
>   script.src = 'site/ref/documents/engine/js/visuallightbox.js';
>   document.body.appendChild(script);
> }
> ```

---

## Résumé des fichiers à créer / modifier

| Fichier | Action |
|---------|--------|
| `/.htaccess` | **Créer** — règle RewriteRule pour le SPA |
| `/index.html` | **Modifier** — iframe → div, liens → href propres, script router |
| `/sitemap.xml` | **Modifier** — URLs propres |
| `site/ref/documents/*.html` (11 fichiers) | **Modifier** — balises canonical |

---

## Ordre d'exécution recommandé

```
1. .htaccess          (prérequis serveur)
2. index.html         (cœur du changement)
3. canonicals         (SEO)
4. sitemap.xml        (SEO)
5. Tests locaux
6. Merge seo-routing → actualisation → main
```

---

## Notes de déploiement

- Tester en local avec un serveur Apache (`php -S localhost:8000` ne supporte
  pas `.htaccess` — utiliser `python3 -m http.server` non plus). Utiliser
  **XAMPP**, **MAMP** ou pousser directement sur le serveur de test.
- Si l'hébergeur est **OVH mutualisé** : le `mod_rewrite` est activé par
  défaut, le `.htaccess` fonctionnera sans configuration supplémentaire.
- Si l'hébergeur est **Nginx** : remplacer le `.htaccess` par une règle
  `try_files $uri $uri/ /index.html;` dans la config du vhost.
