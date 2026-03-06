# Suivi SEO — Aboriginal Way

## Audit réalisé le 2026-03-06

---

## État des actions

| # | Action | État | Fichiers concernés |
|---|--------|------|--------------------|
| 1 | Corriger l'encodage des caractères accentués cassés | ✅ Fait | `index.html`, `home.html` |
| 2 | Reconstruire le sitemap (HTTPS, supprimer artistes individuels, ajouter `home.html`, pages mobiles) | ✅ Fait | `sitemap.xml` |
| 3 | Ajouter un H1 visible sur chaque page de contenu | ✅ Fait (mobile) / ❌ Desktop | `mobile/*.html` (tous) — desktop non traité |
| 4 | Ajouter `alt` pertinents sur les images principales | ✅ Fait | `mobile/photos.html` (27 photos), `home.html` (4 images corrigées) |
| 5 | Ajouter les balises Open Graph | ✅ Fait | `index.html` + `mobile/index.html` |
| 6 | Supprimer le widget AddThis | ✅ Fait | `index.html` |
| 7 | Ajouter un bloc JSON-LD Organization sur la page d'accueil | ✅ Fait | `index.html` + `mobile/index.html` |
| 8 | Créer les pages mobiles dédiées avec meta SEO complètes | ✅ Fait | `mobile/` (12 pages) |

---

## Détail des actions restantes

### 2 — Sitemap
- Supprimer les 7 URLs des pages artistes individuelles (plus accessibles depuis `artistes.html`)
- Ajouter `home.html`
- Ajouter les URLs des pages `mobile/`
- Vérifier que toutes les pages actives sont listées

### 3 — H1 manquants (desktop uniquement)
Pages desktop sans `<h1>` visible :
- `animation-peinture.html`
- `didgeridoo.html`
- `cuisine.html`
- `home.html`
- `presentation.html`
- `contact.html`
- `activites.html`
- `photo.html`

> Les équivalents mobiles ont tous un H1. Le desktop reste à traiter si une refonte est envisagée.

### 4 — Alt images (desktop uniquement)
- `home.html` : 4 images (`Geckomini.jpg`, `Serpentmini.jpg`, `Libellulemini.jpg`, `Bhpetitmini.jpg`) sans attribut `alt`
- `photo.html` : alt = noms de fichiers bruts, à remplacer par des descriptions lisibles

> Les photos mobiles (`mobile/photos.html`) ont toutes des `alt` descriptifs.

---

## Ce qui a été fait sur le mobile (2026-03-06)

### Pages créées dans `mobile/`

| Page | Title | Description | H1 |
|------|-------|-------------|----|
| `index.html` | Aboriginal Way - Le Chemin Aborigène, cultures australiennes | Association loi 1901 fondée en 2007… | — (hub) |
| `presentation.html` | Présentation - Aboriginal Way, association culturelle fondée en 2007 | ✅ | ✅ |
| `exposition.html` | Exposition An Other Way - Aboriginal Way, art aborigène d'Australie | ✅ | ✅ |
| `artistes.html` | Artistes aborigènes - Aboriginal Way, portraits et vidéos | ✅ (noms dans description) | ✅ |
| `animation-peinture.html` | Animation Peinture Aborigène - Aboriginal Way, ateliers artistiques | ✅ | ✅ |
| `didgeridoo.html` | Cours de Didgeridoo - Aboriginal Way, apprendre le souffle circulaire | ✅ | ✅ |
| `cuisine.html` | Cuisine Aborigène - Aboriginal Way, saveurs bush tucker d'Australie | ✅ | ✅ |
| `activites.html` | Activités Culturelles - Aboriginal Way, cultures aborigènes d'Australie | ✅ | ✅ |
| `contact.html` | Contacter Aboriginal Way - Expositions, cours didgeridoo, animations | ✅ | ✅ |
| `partenaires.html` | Partenaires - Aboriginal Way, nos soutiens et associations | ✅ | ✅ |
| `membres.html` | Espace Membres - Aboriginal Way | ✅ | ✅ |
| `photos.html` | Galerie Photos - Aboriginal Way, œuvres et expositions aborigènes | ✅ (noms artistes) | ✅ |

### Open Graph (`mobile/index.html`)
```html
<meta property="og:title" content="Aboriginal Way - Le Chemin Aborigène">
<meta property="og:description" content="Association de promotion des cultures aborigènes d'Australie — art, expositions, didgeridoo, animations.">
<meta property="og:type" content="website">
<meta property="og:url" content="https://aboriginalway.fr/mobile/">
<meta property="og:image" content="https://aboriginalway.fr/site/ref/image/Bhgrand.jpg">
<meta property="og:locale" content="fr_FR">
```

### JSON-LD Organization (`mobile/index.html`)
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

---

## Actions SEO restantes (priorité)

| Priorité | Action | Périmètre |
|----------|--------|-----------|
| Moyenne | Supprimer les mentions Atelier du Héron | Pages desktop (recherche : aucune occurrence trouvée dans le HTML — à confirmer sur le site live) |
| Moyenne | Supprimer les mentions Yourtes | Pages desktop (recherche : aucune occurrence trouvée dans le HTML — à confirmer sur le site live) |
| Basse | Ajouter des URLs canoniques (`<link rel="canonical">`) | Toutes les pages (desktop + mobile) |
| Basse | Ajouter H1 sur les pages desktop sans H1 | `animation-peinture.html`, `didgeridoo.html`, `cuisine.html`, `home.html`, `presentation.html`, `contact.html`, `activites.html`, `photo.html` |
