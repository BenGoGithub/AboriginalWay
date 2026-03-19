# Audit Axe 1 — Qualité et fraîcheur du contenu

Date : 2026-03-10 | Méthode : lecture directe du code source

---

## Pages desktop (`site/ref/documents/`)

| Page | URL propre | Mots estimés | H1 | H2+ | État | Problèmes |
|---|---|---|---|---|---|---|
| `home.html` | `/` | ~500 | ✅ | 5 | ✅ Bon | — |
| `presentation.html` | `/presentation` | ~80 | ✅ | 0 | ⚠️ Squelettique | Réécriture complète requise |
| `artistes.html` | `/artistes` | ~20 | ✅ | 0 | ⚠️ Vide | 7 noms listés, zéro biographie |
| `didgeridoo.html` | `/didgeridoo` | ~100 | ✅ | 0 | ⚠️ Court | Image flyer non indexable, peu de texte |
| `animation-peinture.html` | `/animation-peinture` | ~5 | ✅ | 0 | 🔴 Quasi vide | Iframe Vimeo seule, CSS `general.css` absent, background absent |
| `exposition.html` | `/exposition` | ~50 | ✅ | 0 | ⚠️ Court | 1 vidéo + 2 lignes de texte |
| `activites.html` | `/activites` | 0 | ✅ | 0 | 🔴 Nul | Contenu = image GIF, rien d'indexable |
| `temps.html` | `/site/ref/documents/temps.html` ⚠️ | ~120 | ✅ | 0 | ⚠️ Périmé | 1 seul événement daté de **mars 2011**, URL canonique incorrecte |
| `liens.html` | `/site/ref/documents/liens.html` ⚠️ | ~60 | ✅ | 2 | ⚠️ Pauvre | 3 liens HTTP, peu de contexte, URL canonique incorrecte |
| `membres.html` | `/membres` | ~10 | ✅ | 0 | 🔴 Vide | "En construction", `noindex` |
| `partenaires.html` | `/partenaires` | ~100 | ✅ | 2 | ✅ Correct | Territory Essence lien HTTP, pas de description de la relation |
| `photo.html` | `/photos` | ~10 | ✅ | 0 | ⚠️ Sans texte | 27 photos avec bons `alt`, mais zéro texte contextuel autour de la galerie |
| `contact.html` | `/contact` | ~15 | ✅ | 0 | ⚠️ Pauvre | 1 ligne + 3 images GIF, pas de contenu textuel réel |

---

## Pages mobiles (`mobile/`)

| Page | Contenu vs desktop | Mots estimés | Écart | Problèmes |
|---|---|---|---|---|
| `mobile/index.html` | Différent (navigation) | — | Normal | Canonical → `/mobile/` (non idéal) |
| `mobile/presentation.html` | **Meilleur** que desktop | ~150 | Desktop à aligner | GTM noscript dupliqué (×2) |
| `mobile/artistes.html` | Équivalent | ~30 | Même problème | GTM dupliqué, zéro biographie |
| `mobile/didgeridoo.html` | **Meilleur** que desktop | ~200 | Desktop à aligner | GTM dupliqué |
| `mobile/animation-peinture.html` | **Meilleur** que desktop | ~100 | Desktop à corriger d'abord | GTM dupliqué |
| `mobile/exposition.html` | **Meilleur** que desktop | ~100 | Desktop à aligner | GTM dupliqué |
| `mobile/activites.html` | **Beaucoup mieux** que desktop | ~200 | Desktop à reconstruire | GTM dupliqué |
| `mobile/membres.html` | Équivalent | ~20 | — | **Pas de `noindex`** contrairement au desktop → crawlé par Google |
| `mobile/partenaires.html` | Équivalent | ~100 | — | Territory Essence HTTP, GTM dupliqué |
| `mobile/photos.html` | Équivalent | ~10 | — | `loading="lazy"` ✅, mais zéro contexte textuel |
| `mobile/contact.html` | **Meilleur** que desktop | ~60 | Desktop à aligner | GTM dupliqué |

---

## Observations transverses

### Déséquilibre desktop / mobile
Le site mobile est globalement **mieux rédigé** que le desktop pour 6 pages sur 11.
Les pages desktop `activites`, `animation-peinture`, `exposition`, `didgeridoo` doivent s'inspirer du mobile pour leur réécriture.

### Pages sans URL propre (canonical incorrect)
- `temps.html` → canonical pointe vers `/site/ref/documents/temps.html` au lieu de `/temps`
- `liens.html` → même problème

Ces pages ne sont pas dans la table de routage SPA (`index.html`) et n'ont pas de redirect 301 dans `.htaccess`. Elles sont accessibles à leur URL native mais non réécrites.

### Fraîcheur
- Aucun mécanisme de fraîcheur : pas de blog, pas d'agenda, pas de date de dernière mise à jour visible.
- `temps.html` est la seule page "actualité" du site, et son événement date de **2011** (15 ans).
- Les partenaires mentionnent un festival en **juillet 2026** — seule information datée récente.

### Bug critique — `mobile/membres.html`
La page desktop `membres.html` est en `noindex`. La page mobile équivalente n'a **pas** de `noindex`. Google peut indexer une page vide "en construction".

---

## Priorités d'action

| Priorité | Page | Action |
|---|---|---|
| P0 | `mobile/membres.html` | Ajouter `noindex` (correctif immédiat) |
| P1 | `activites.html` (desktop) | Reconstruire avec du texte (s'inspirer du mobile) |
| P1 | `animation-peinture.html` (desktop) | Réécriture + corriger CSS/background |
| P1 | `présentation.html` (desktop + mobile) | Réécriture complète |
| P2 | `artistes.html` (desktop + mobile) | Biographies des 7 artistes |
| P2 | `didgeridoo.html` (desktop) | Enrichir (s'inspirer du mobile) |
| P2 | `exposition.html` (desktop) | Enrichir (s'inspirer du mobile) |
| P3 | `contact.html` (desktop) | Remplacer les GIFs par du texte |
| P3 | `photo.html` | Ajouter contexte textuel autour de la galerie |
| P3 | `temps.html` | Décider : archiver ou transformer en page Agenda |
| P3 | `liens.html` | Enrichir le contexte, corriger URL canonique |
| P4 | Toutes pages | Créer une section Agenda/Actualités |
