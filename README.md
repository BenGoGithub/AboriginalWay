# Aboriginal Way

Site vitrine pour l'association **Aboriginal Way** (loi 1901, fondée en 2007), dédiée à la promotion de l'art et de la culture aborigène australienne (expositions, ateliers peinture, didgeridoo, bush tucker).

- Site : [aboriginalway.fr](https://aboriginalway.fr)
- Déploiement de test : [tuyo2268.odns.fr](http://tuyo2268.odns.fr/)
- Repo : `BenGoGithub/AboriginalWay`

---

## Architecture technique

Le site est **100 % statique** (HTML/CSS/JS), hébergé sur Apache.

### Desktop

Routeur SPA History API / `pushState` : `index.html` sert de layout principal, le contenu de chaque page est chargé dynamiquement depuis `site/ref/documents/` via `fetch` et injecté dans `#content`. Chaque page dispose d'une URL propre et indexable. Voir `ROUTING.md` pour le détail technique.

### Mobile

Site mobile dédié dans `mobile/` (11 pages HTML5 + `mobile.css`), accessible via redirection automatique depuis `index.html` pour les appareils `≤ 768px`. Voir `mobile/README.md`.

---

## Structure

```
AboriginalWay/
├── index.html                          # Point d'entrée desktop (SPA router + redirection mobile)
├── sitemap.xml                         # Sitemap HTTPS (URLs propres)
├── robots.txt                          # Disallow /logs/, référence sitemap
├── .htaccess                           # Compression, cache, redirects 301, SPA rewrite
├── mobile/                             # Site mobile dédié (≤ 768px)
│   ├── mobile.css
│   ├── index.html
│   ├── activites.html
│   ├── animation-peinture.html
│   ├── artistes.html
│   ├── contact.html
│   ├── didgeridoo.html
│   ├── exposition.html
│   ├── membres.html
│   ├── partenaires.html
│   ├── photos.html
│   └── presentation.html
├── site/ref/
│   ├── documents/                      # Pages de contenu desktop (13 fichiers HTML)
│   ├── style/general.css               # CSS desktop
│   └── image/                          # Images partagées (~94 fichiers)
└── logs/                               # Statistiques de trafic (exclues de l'indexation)
```

---

## Organisation Git

| Branche | Rôle |
|---------|------|
| `main` | Production — code stable |
| `actualisation` | Staging — code finalisé en attente de merge dans `main` |
| `deploy` | Branche de déploiement — sans fichiers de documentation |
| `feature/*` | Une branche par tâche, mergée dans `actualisation` |

**Flux :** `feature-branch` → `actualisation` → `main`

---

## SEO — État actuel

Toutes les actions SEO sont tracées dans `SEO.md`. Résumé :

- Routeur SPA avec URLs propres + redirects 301 depuis les anciennes URLs
- Balises `<title>`, `<meta description>`, `<h1>` sur toutes les pages (desktop + mobile)
- Open Graph + Twitter Cards sur toutes les pages
- JSON-LD `Organization` sur `index.html` et `mobile/index.html`
- Canonical sur toutes les pages
- Google Tag Manager (GTM-5P7M6QCB)
- `sitemap.xml` complet (URLs propres, sans pages artistes individuelles)
- `membres.html` en `noindex` (page en construction)

---

## Reste à faire

- [ ] Migrer l'hébergeur : **1&1 → o2switch** — DNS déjà redirigés vers o2switch ✅, activer TigerCache (OpenLiteSpeed) depuis cPanel
- [ ] Supprimer les mentions à l'**Atelier du Héron** (références, liens)
- [ ] Supprimer la page **Yourtes** et ses références dans la navigation
- [ ] Passer `membres.html` en page "En construction" avec adresse e-mail
- [ ] Optimiser les images (WebP, lazy loading)
- [ ] Ajouter des en-têtes de sécurité (CSP, X-Frame-Options)
