# Suivi SEO — Aboriginal Way

## Dernière mise à jour : 2026-03-10 — Analyse Haloscan : audit mots-clés organiques aboriginalway.fr

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
| 12 | SEO activites.html : title, description, Open Graph, Twitter Card, alt image, H1 | ✅ Fait | `site/ref/documents/activites.html` |
| 13 | SEO toutes les pages desktop : Open Graph, Twitter Card, canonical, robots, titles, descriptions | ✅ Fait | `home`, `exposition`, `contact`, `artistes`, `didgeridoo`, `animation-peinture`, `photo`, `membres`, `partenaires`, `presentation`, `liens`, `temps` |
| 14 | Alt descriptifs sur les 26 images de la galerie photo | ✅ Fait | `site/ref/documents/photo.html` |
| 15 | H1 descriptif sur liens.html | ✅ Fait | `site/ref/documents/liens.html` |
| 16 | membres.html : noindex (page en construction) | ✅ Fait | `site/ref/documents/membres.html` |
| 17 | Routage SPA History API / pushState — URLs propres indexables | ✅ Fait | `index.html`, `.htaccess`, `sitemap.xml` |
| 18 | Galerie photos : remplacement VisualLightBox/jQuery par CSS grid + lightbox vanilla JS | ✅ Fait | `site/ref/documents/photo.html`, `index.html` |
| 19 | Fond de page (Fond.jpg) appliqué via JS avec chemin absolu | ✅ Fait | `index.html`, `site/ref/style/general.css` |
| 20 | Exposition : vidéo et textes centrés | ✅ Fait | `site/ref/documents/exposition.html` |
| 21 | Contact : brochure pleine largeur (580px) | ✅ Fait | `site/ref/documents/contact.html` |
| 22 | Mobile footer : suppression "fondée en 2007" | ✅ Fait | `mobile/*.html` (11 fichiers) |
| 23 | Google Tag Manager (GTM-5P7M6QCB) installé | ✅ Fait | `index.html`, `mobile/*.html` (11 fichiers) |
| 24 | Fix affichage desktop : header `X-Fetch-Content` pour bypasser les redirects 301 dans le fetch SPA | ✅ Fait | `index.html`, `.htaccess` |
| 25 | Structure de titres : suppression du double h1 (logo → `<p>`) | ✅ Fait | `index.html` |
| 26 | Page d'accueil : meta description portée à 157 chars + correction `og:url` | ✅ Fait | `site/ref/documents/home.html` |
| 27 | Page d'accueil : contenu enrichi (~520 mots, 4 sections h2) pour atteindre le seuil SEO des 500 mots | ✅ Fait | `site/ref/documents/home.html`, `site/ref/style/general.css` |
| 28 | og:url corrigés : chemins de fichier → URLs propres sur 10 pages desktop | ✅ Fait | `activites`, `animation-peinture`, `artistes`, `contact`, `didgeridoo`, `exposition`, `partenaires`, `photo`, `presentation`, `membres` |
| 29 | Descriptions trop longues (>160 chars) raccourcies à 148–159 chars sur 7 pages desktop | ✅ Fait | `artistes`, `partenaires`, `photo`, `contact`, `didgeridoo`, `presentation`, `activites` |
| 30 | Apple Touch Icon (180×180) — icône pour ajout à l'écran d'accueil iOS/Android | ✅ Fait | `apple-touch-icon.png`, `index.html`, `mobile/*.html` (11 fichiers) |

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

### En cours — Audit mots-clés Haloscan (2026-03-10)

**Outil utilisé** : Haloscan — module "Domaine × Mots-clés"
**Domaine analysé** : aboriginalway.fr
**Statut** : analyse faite, implémentation à planifier

#### Résultats de l'analyse (7 MC testés)

| Mot-clé | Volume/mois | KGR | Compétition | Priorité |
|---------|-------------|-----|-------------|----------|
| peinture aborigène | 900 | 6.31 | 0.31 (faible) | **P1** |
| art aborigène | 2 000 | 8.4 | 0.29 (faible) | **P1** |
| didgeridoo | 7 700 | 28.7 | 0.99 (élevée) | P2 |
| culture aborigène | 140 | NA | NA | P3 |
| apprendre | 14 600 | 304 | 0.01 | ❌ trop générique |
| animation | 12 500 | 2 488 | 0.03 | ❌ hors sujet |
| aboriginal way | NA | NA | NA | Marque |

#### Constat principal

Le domaine n'est positionné sur **aucun** de ces mots-clés (Trafic = NA, Position = NA pour tous).

#### Prochaine étape à réaliser

Auditer les pages existantes (`site/ref/documents/`) pour vérifier la présence de "art aborigène" et "peinture aborigène" dans les balises `<title>`, `<h1>` et `<meta name="description">`, puis optimiser en conséquence.

---

## Notes techniques

### Fix redirects 301 vs fetch SPA (2026-03-08)

Les redirects 301 ajoutés en action #23 cassaient l'affichage desktop : le router
faisait `fetch('/site/ref/documents/home.html')`, recevait un 301 vers `/`, et
injectait le contenu d'`index.html` complet dans `#content` (layout doublé).

**Solution** : le `fetch` envoie un header personnalisé `X-Fetch-Content: 1`, et
chaque règle de redirect dans `.htaccess` est conditionnée par
`RewriteCond %{HTTP:X-Fetch-Content} !1`. Les redirects 301 s'appliquent
uniquement aux navigations directes (SEO), pas aux requêtes internes du SPA.
