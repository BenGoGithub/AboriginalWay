# Audit Axe 4 — Core Web Vitals (analyse statique)

Date : 2026-03-10 | Méthode : analyse statique du code source
⚠️ Cet audit est **statique** — sans mesure PageSpeed Insights réelle. Il identifie les risques probables.
Un audit dynamique sur https://pagespeed.web.dev est nécessaire pour confirmer les métriques.

---

## Rappel des 3 métriques CWV

- **LCP** (Largest Contentful Paint) : délai d'affichage du plus grand élément visible. Cible : < 2,5 s
- **CLS** (Cumulative Layout Shift) : stabilité visuelle de la page. Cible : < 0,1
- **INP** (Interaction to Next Paint) : réactivité aux interactions. Cible : < 200 ms

---

## Architecture technique (facteurs structurels)

### SPA Router (desktop)
Le site desktop fonctionne en SPA via `index.html` : le contenu est **chargé dynamiquement par JavaScript** après le rendu de la coque HTML. Conséquences :
- **LCP potentiellement dégradé** : Googlebot doit exécuter JS pour voir le contenu. Le LCP réel peut être l'image sidebar ou le spinner.
- Le contenu textuel n'est **pas dans le HTML initial** → risque d'indexation incomplète si Googlebot ne rend pas le JS.
- Chaque navigation interne est fluide (SPA), mais les accès directs par URL dépendent du rendu JS.

### Site mobile (pages HTML statiques)
Les 11 pages mobiles sont du HTML statique classique. Risques CWV différents : moins de JS, mais images et iframes à optimiser.

---

## LCP — Largest Contentful Paint

### Desktop (`index.html`)
| Élément | Taille | Optimisé | Risque |
|---|---|---|---|
| `Bhgrand.jpg` (sidebar) | JPEG, ~280×420px | ❌ Pas de `preload` | LCP probable, JPEG non converti WebP |
| `FinalTransp.gif` (logo) | GIF animé | ❌ GIF = format obsolète | Contribution au poids |
| Contenu textuel | Chargé via JS fetch | ❌ Non disponible au 1er paint | LCP décalé |

### Mobile (pages statiques)
| Page | Élément LCP probable | Format | Risque |
|---|---|---|---|
| `mobile/index.html` | `FinalTransp.gif` (logo) | GIF | Moyen |
| `mobile/photos.html` | Première image grille | PNG thumbnails | Faible (lazy load ✅) |
| Pages avec iframes YT/Vimeo | Iframe (artistes, exposition, animation-peinture) | — | **Élevé** — iframes bloquantes |

---

## CLS — Cumulative Layout Shift

| Source potentielle | Page concernée | Détail |
|---|---|---|
| Images sans `width`/`height` | `photo.html` (desktop) | Aucune dimension déclarée sur les miniatures |
| Images sans `width`/`height` | `home.html` (desktop) | Les 4 images du tableau ont des dimensions déclarées ✅ |
| Chargement dynamique du contenu SPA | Toutes pages desktop | Le `#content` est vide au 1er paint, rempli après fetch JS → saut de mise en page |
| Logo partenaire externe | `partenaires.html` | Image chargée depuis `lerevedelaborigene.org` sans dimensions déclarées |
| `animation-peinture.html` desktop | Corps de page | CSS `general.css` absent, background absent → rendu différent entre 1er paint et final |

---

## INP — Interaction to Next Paint

| Source potentielle | Page concernée | Détail |
|---|---|---|
| GTM en `<head>` (render-blocking) | Toutes pages mobiles | Script GTM synchrone dans `<head>` avant `<meta viewport>` |
| Pas d'`async`/`defer` explicite sur GTM | Toutes pages mobiles | GTM utilise son propre mécanisme async, mais son placement en `<head>` reste suboptimal |
| JS inline SPA dans `index.html` | Desktop | ~200 lignes de JS inline — impact limité car pas de librairie lourde |

---

## Images — Inventaire des problèmes

### Format
| Format actuel | Nb estimé | Recommandation |
|---|---|---|
| JPEG (`.jpg`) | ~90+ | Convertir en WebP → gain ~25-35% de poids |
| GIF (`.gif`) | ~10 (logo, brochures) | Logo → WebP/PNG, brochures → remplacer par texte |
| PNG (`.png`) | ~27 thumbnails | Convertir en WebP |

### Attributs manquants
| Page | Problème | Impact |
|---|---|---|
| `photo.html` (desktop) | Miniatures sans `width`/`height` | CLS |
| `photo.html` (desktop) | Pas de `loading="lazy"` | Chargement initial lourd (27 images) |
| `mobile/photos.html` | `loading="lazy"` ✅ | Bon — à reproduire sur desktop |
| `artistes.html` | Pas de `loading="lazy"` sur les iframes | LCP dégradé |
| `partenaires.html` | Logo externe sans dimensions | CLS |

### Iframes YouTube / Vimeo sans lazy loading
| Page | Iframe | `loading="lazy"` |
|---|---|---|
| `artistes.html` (desktop) | 2 × YouTube | ❌ |
| `exposition.html` (desktop) | 1 × YouTube | ❌ |
| `animation-peinture.html` (desktop) | 1 × Vimeo | ❌ |
| `mobile/artistes.html` | 2 × YouTube | ❌ |
| `mobile/exposition.html` | 1 × YouTube | ❌ |
| `mobile/animation-peinture.html` | 1 × Vimeo | ❌ |

---

## Ce qui fonctionne bien

| Bonne pratique | Détail |
|---|---|
| HTTPS forcé | Redirect 301 HTTP→HTTPS dans `.htaccess` ✅ |
| Compression gzip | `mod_deflate` configuré pour HTML, CSS, JS, SVG ✅ |
| Cache navigateur | `mod_expires` : images 1 an, CSS/JS 1 mois, HTML 1h ✅ |
| Cache-Control immutable | Images marquées `immutable` ✅ |
| ETags | `FileETag MTime Size` ✅ |
| Keep-Alive | Configuré ✅ |
| En-têtes sécurité | `X-Content-Type-Options`, `X-Frame-Options`, `Referrer-Policy` ✅ |
| Lazy load mobile photos | `loading="lazy"` sur toutes les miniatures de `mobile/photos.html` ✅ |
| Dimensions images `home.html` | Les 4 images du tableau ont `width`/`height` déclarés ✅ |

---

## Actions recommandées (après mesure PageSpeed)

### À faire avant mesure (correctifs évidents)
- [ ] Ajouter `loading="lazy"` sur toutes les iframes YouTube/Vimeo
- [ ] Ajouter `width`/`height` sur les miniatures de `photo.html` (desktop)
- [ ] Ajouter `width`/`height` sur le logo partenaire dans `partenaires.html`
- [ ] Corriger `animation-peinture.html` desktop : ajouter `general.css` + background

### À planifier après mesure PageSpeed
- [ ] Lancer PageSpeed Insights sur `aboriginalway.fr` (desktop + mobile)
- [ ] Lancer PageSpeed Insights sur `aboriginalway.fr/animation-peinture`
- [ ] Selon résultats : convertir images JPEG → WebP
- [ ] Selon résultats : évaluer `<link rel="preload">` pour `Bhgrand.jpg` (LCP sidebar)
- [ ] Selon résultats : déplacer GTM mobile après `<meta viewport>`

---

## Mesures à effectuer (outils recommandés)

| Outil | Usage |
|---|---|
| https://pagespeed.web.dev | LCP / CLS / INP mesurés + recommandations |
| https://web.dev/measure | Audit Lighthouse complet |
| Google Search Console → Expérience de la page | Données terrain (CrUX) si trafic suffisant |
