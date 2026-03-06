# Suivi SEO — Aboriginal Way

## Audit réalisé le 2026-03-06

---

## État des actions

| # | Action | État | Fichiers concernés |
|---|--------|------|--------------------|
| 1 | Corriger l'encodage des caractères accentués cassés | ✅ Fait | `index.html`, `home.html` |
| 2 | Reconstruire le sitemap (HTTPS, supprimer artistes individuels, ajouter `home.html`, `<lastmod>`) | ⚠️ Partiel | `sitemap.xml` |
| 3 | Ajouter un H1 visible sur chaque page de contenu | ❌ À faire | `animation-peinture.html`, `didgeridoo.html`, `cuisine.html`, `home.html`, `presentation.html`, `contact.html`, `activites.html`, `photo.html` |
| 4 | Ajouter `alt` pertinents sur les images principales | ⚠️ Partiel | `home.html` (4 images sans alt), galerie `photo.html` (alt = noms de fichiers) |
| 5 | Ajouter les balises Open Graph (index.html et home.html) | ❌ À faire | `index.html`, `home.html` |
| 6 | Supprimer le widget AddThis | ✅ Fait | `index.html` |
| 7 | Ajouter un bloc JSON-LD Organization sur la page d'accueil | ❌ À faire | `index.html` |

---

## Détail des actions restantes

### 2 — Sitemap
- Supprimer les 7 URLs des pages artistes individuelles (plus accessibles depuis `artistes.html`)
- Ajouter `home.html`
- Vérifier que toutes les pages actives sont listées

### 3 — H1 manquants
Pages sans `<h1>` visible :
- `animation-peinture.html`
- `didgeridoo.html`
- `cuisine.html`
- `home.html`
- `presentation.html`
- `contact.html`
- `activites.html`
- `photo.html`

### 4 — Alt images
- `home.html` : 4 images (`Geckomini.jpg`, `Serpentmini.jpg`, `Libellulemini.jpg`, `Bhpetitmini.jpg`) sans attribut `alt`
- `photo.html` : alt = noms de fichiers bruts (ex. `lindsay_bunn_-_lightning_man`), à remplacer par des descriptions lisibles

### 5 — Open Graph
Balises à ajouter sur `index.html` et `home.html` :
```html
<meta property="og:title" content="Aboriginal Way - Le Chemin Aborigène">
<meta property="og:description" content="Association de promotion des cultures aborigènes d'Australie">
<meta property="og:type" content="website">
<meta property="og:url" content="https://aboriginalway.fr/">
<meta property="og:image" content="https://aboriginalway.fr/site/ref/image/Bhgrand.jpg">
<meta property="og:locale" content="fr_FR">
```

### 7 — JSON-LD Organization
Bloc à ajouter dans le `<head>` de `index.html` :
```json
{
  "@context": "https://schema.org",
  "@type": "Organization",
  "name": "Aboriginal Way",
  "url": "https://aboriginalway.fr",
  "foundingDate": "2007",
  "description": "Association loi 1901 de promotion des cultures aborigènes d'Australie",
  "contactPoint": {
    "@type": "ContactPoint",
    "email": "aboriginalway@free.fr",
    "contactType": "customer support"
  }
}
```
