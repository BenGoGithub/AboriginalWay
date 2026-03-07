# Suivi SEO — Aboriginal Way

## Dernière mise à jour : 2026-03-07 — Branche `actualisation` déployée (merge vers `main` à faire)

---

## État des actions

| # | Action | État | Fichiers concernés |
|---|--------|------|--------------------|
| 1 | Corriger l'encodage des caractères accentués cassés | ✅ Fait | `index.html`, `home.html` |
| 2 | Reconstruire le sitemap (HTTPS, supprimer artistes individuels, ajouter `home.html`, pages mobiles) | ✅ Fait | `sitemap.xml` |
| 3 | Ajouter un H1 visible sur chaque page de contenu | ✅ Fait | `mobile/*.html` + 8 pages desktop (home, contact, didgeridoo, animation-peinture, cuisine, activites, photo, presentation) |
| 4 | Ajouter `alt` pertinents sur les images principales | ✅ Fait | `mobile/photos.html` (27 photos), `home.html` (4 images corrigées) |
| 5 | Ajouter les balises Open Graph | ✅ Fait | `index.html` + `mobile/index.html` |
| 6 | Supprimer le widget AddThis | ✅ Fait | `index.html` |
| 7 | Ajouter un bloc JSON-LD Organization sur la page d'accueil | ✅ Fait | `index.html` + `mobile/index.html` |
| 8 | Créer les pages mobiles dédiées avec meta SEO complètes | ✅ Fait | `mobile/` (11 pages — cuisine supprimée) |
| 9 | Twitter Cards sur toutes les pages mobiles | ✅ Fait | `mobile/*.html` (11 pages) |
| 10 | Fix menu et pages artistes desktop | ✅ Fait | `site/ref/documents/artistes.html` |
| 11 | Ajout flyer et mise en page contact desktop | ✅ Fait | `site/ref/documents/contact.html` |

---

## Ce qui a été fait sur le mobile

### Pages créées dans `mobile/`

| Page | Title | Description | H1 |
|------|-------|-------------|----|
| `index.html` | Aboriginal Way - Le Chemin Aborigène, cultures australiennes | Association loi 1901 fondée en 2007… | — (hub) |
| `presentation.html` | Présentation - Aboriginal Way, association culturelle fondée en 2007 | ✅ | ✅ |
| `exposition.html` | Exposition An Other Way - Aboriginal Way, art aborigène d'Australie | ✅ | ✅ |
| `artistes.html` | Artistes aborigènes - Aboriginal Way, portraits et vidéos | ✅ (noms dans description) | ✅ |
| `animation-peinture.html` | Animation Peinture Aborigène - Aboriginal Way, ateliers artistiques | ✅ | ✅ |
| `didgeridoo.html` | Cours de Didgeridoo - Aboriginal Way, apprendre le souffle circulaire | ✅ | ✅ |
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

## Actions restantes

Aucune action en cours — site à jour et déployé.
