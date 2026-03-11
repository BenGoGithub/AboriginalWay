# Audit Axe 5 — UX Mobile

Date : 2026-03-10 | Méthode : analyse statique du code source des 11 pages mobiles

---

## Architecture mobile

Le site mobile est un ensemble de **11 pages HTML statiques** dans le dossier `mobile/`, servi
séparément du desktop (redirection JS sur `index.html` si `max-width: 768px`).
Chaque page charge `mobile.css` et le bloc GTM.

---

## Audit page par page

### `mobile/index.html` — Accueil mobile
| Critère | État | Note |
|---|---|---|
| Viewport | ✅ | `width=device-width, initial-scale=1` |
| Canonical | ⚠️ | Pointe vers `/mobile/` — devrait pointer vers `/` |
| OG tags | ✅ | Complets |
| Twitter card | ✅ | Complet |
| JSON-LD | ✅ | `Organization` présent |
| GTM | ✅ | Présent, noscript une seule fois ✅ |
| H1 | ❌ | Absent (tagline en `<p>`, pas de H1) |
| Contenu textuel | ⚠️ | Navigation + image + tagline — pas de contenu SEO |
| Apple touch icon | ✅ | Présent |

---

### `mobile/presentation.html` — Présentation
| Critère | État | Note |
|---|---|---|
| Canonical | ⚠️ | Pointe vers `/mobile/presentation.html` — devrait pointer vers `/presentation` |
| OG tags | ❌ | Absents (uniquement Twitter cards) |
| GTM noscript | 🔴 | **Dupliqué ×2** |
| H1 | ✅ | "Présentation de l'association" |
| H2 | ✅ | "Notre objet", "Nos actions" |
| Contenu | ⚠️ | ~150 mots — mieux que desktop mais encore court |

---

### `mobile/artistes.html` — Artistes
| Critère | État | Note |
|---|---|---|
| Canonical | ⚠️ | Pointe vers `/mobile/artistes.html` |
| OG tags | ❌ | Absents |
| GTM noscript | 🔴 | **Dupliqué ×2** |
| H1 | ✅ | "Les Artistes Aborigènes" |
| H2 | ✅ | Par vidéo |
| Contenu | ⚠️ | Liste de 7 noms, zéro biographie |
| Iframes | ⚠️ | 2 YouTube sans `loading="lazy"` |

---

### `mobile/didgeridoo.html` — Didgeridoo
| Critère | État | Note |
|---|---|---|
| Canonical | ⚠️ | Pointe vers `/mobile/didgeridoo.html` |
| OG tags | ❌ | Absents |
| GTM noscript | 🔴 | **Dupliqué ×2** |
| H1 | ✅ | "Cours de Didgeridoo" |
| H2 | ✅ | "Les ateliers", "Adhésion", "Au programme", "Nous contacter" |
| Contenu | ✅ | ~200 mots, structuré, liste de programme, villes mentionnées |
| CTA | ✅ | Bouton "Prendre contact" |

**Note** : meilleure page mobile du site en termes de contenu.

---

### `mobile/animation-peinture.html` — Animation peinture
| Critère | État | Note |
|---|---|---|
| Canonical | ⚠️ | Pointe vers `/mobile/animation-peinture.html` |
| OG tags | ❌ | Absents |
| GTM noscript | 🔴 | **Dupliqué ×2** |
| H1 | ✅ | "Animation Peinture Aborigène" |
| H2 | ❌ | Absent |
| Contenu | ⚠️ | 2 § (~80 mots) + iframe Vimeo |
| CTA | ✅ | Lien "Organiser une animation" |

---

### `mobile/exposition.html` — Exposition
| Critère | État | Note |
|---|---|---|
| Canonical | ⚠️ | Pointe vers `/mobile/exposition.html` |
| OG tags | ❌ | Absents |
| GTM noscript | 🔴 | **Dupliqué ×2** |
| H1 | ✅ | "Exposition : An Other Way" |
| H2 | ✅ | "L'exposition itinérante", "À découvrir également" |
| Contenu | ⚠️ | ~100 mots, correct mais peu de détails sur les œuvres |
| CTA | ✅ | "Nous contacter pour l'exposition" |

---

### `mobile/activites.html` — Activités
| Critère | État | Note |
|---|---|---|
| Canonical | ⚠️ | Pointe vers `/mobile/activites.html` |
| OG tags | ❌ | Absents |
| GTM noscript | 🔴 | **Dupliqué ×2** |
| H1 | ✅ | "Cultures Aborigènes" |
| H2 | ✅ | 3 sections (peinture, didgeridoo, exposition) |
| Contenu | ✅ | ~200 mots, page hub bien structurée |

---

### `mobile/membres.html` — Membres
| Critère | État | Note |
|---|---|---|
| Canonical | ⚠️ | Pointe vers `/mobile/membres.html` |
| OG tags | ❌ | Absents |
| GTM noscript | 🔴 | **Dupliqué ×2** |
| `noindex` | 🔴 | **ABSENT** — contrairement à desktop qui a `noindex` |
| H1 | ✅ | "Pour nos membres" |
| Contenu | ❌ | "En cours de construction" |

---

### `mobile/partenaires.html` — Partenaires
| Critère | État | Note |
|---|---|---|
| Canonical | ⚠️ | Pointe vers `/mobile/partenaires.html` |
| OG tags | ❌ | Absents |
| GTM noscript | 🔴 | **Dupliqué ×2** |
| H1 | ✅ | "Nos Partenaires" |
| H2 | ✅ | Un par partenaire |
| Contenu | ✅ | ~150 mots, descriptions présentes |
| Lien HTTP | ⚠️ | Territory Essence en `http://` |

---

### `mobile/photos.html` — Galerie
| Critère | État | Note |
|---|---|---|
| Canonical | ⚠️ | Pointe vers `/mobile/photos.html` |
| OG tags | ❌ | Absents |
| GTM noscript | 🔴 | **Dupliqué ×2** |
| H1 | ✅ | "Galerie Photos" |
| `loading="lazy"` | ✅ | Présent sur toutes les images ✅ |
| Alt texts | ✅ | Tous renseignés |
| Contenu textuel | ⚠️ | Zéro texte autour de la galerie |

---

### `mobile/contact.html` — Contact
| Critère | État | Note |
|---|---|---|
| Canonical | ⚠️ | Pointe vers `/mobile/contact.html` |
| OG tags | ❌ | Absents |
| GTM noscript | 🔴 | **Dupliqué ×2** |
| H1 | ✅ | "Nous Contacter" |
| H2 | ✅ | Sections par type de contact |
| Contenu | ✅ | Téléphone + email + villes |
| `tel:` link | ✅ | Lien cliquable `tel:+33664760730` ✅ |

---

## Tableau récapitulatif

| Page | OG tags | GTM dupliqué | Canonical correct | H1 | noindex manquant |
|---|---|---|---|---|---|
| `index.html` | ✅ | ✅ | ⚠️ | ❌ | — |
| `presentation.html` | ❌ | 🔴 ×2 | ⚠️ | ✅ | — |
| `artistes.html` | ❌ | 🔴 ×2 | ⚠️ | ✅ | — |
| `didgeridoo.html` | ❌ | 🔴 ×2 | ⚠️ | ✅ | — |
| `animation-peinture.html` | ❌ | 🔴 ×2 | ⚠️ | ✅ | — |
| `exposition.html` | ❌ | 🔴 ×2 | ⚠️ | ✅ | — |
| `activites.html` | ❌ | 🔴 ×2 | ⚠️ | ✅ | — |
| `membres.html` | ❌ | 🔴 ×2 | ⚠️ | ✅ | 🔴 MANQUANT |
| `partenaires.html` | ❌ | 🔴 ×2 | ⚠️ | ✅ | — |
| `photos.html` | ❌ | 🔴 ×2 | ⚠️ | ✅ | — |
| `contact.html` | ❌ | 🔴 ×2 | ⚠️ | ✅ | — |

---

## Problèmes systémiques

### 1. GTM noscript dupliqué (×2) sur 10/11 pages
Toutes les pages mobiles sauf `index.html` ont le bloc GTM noscript deux fois.
Impact : données analytics potentiellement doublées.

### 2. OG tags absents sur 10/11 pages mobiles
Seule `index.html` a des `og:title`, `og:description`, `og:type`, etc.
Les autres ont uniquement des Twitter cards.

### 3. Canonical URLs incorrectes
Toutes les pages mobiles pointent leur canonical vers `/mobile/xxx.html`.
Pour le SEO, le canonical devrait pointer vers l'URL canonique principale (`/didgeridoo`, `/artistes`, etc.).
Google peut traiter les versions mobiles comme des pages dupliquées.

### 4. `mobile/membres.html` sans `noindex`
Bug : desktop a `noindex`, mobile non. Google peut indexer une page "en construction".

---

## Actions recommandées

### P0 — Correctifs immédiats
- [x] Ajouter `<meta name="robots" content="noindex, follow">` sur `mobile/membres.html`
- [x] Supprimer le bloc GTM noscript dupliqué sur les 10 pages concernées

### P1 — Canonicals
- [x] Corriger les canonical de toutes les pages mobiles → pointer vers l'URL desktop propre
- [x] `mobile/index.html` → `https://aboriginalway.fr/`

### P2 — OG tags
- [x] Ajouter les balises `og:title`, `og:description`, `og:type`, `og:url`, `og:image` sur les 10 pages sans OG

### P3 — Contenu
- [ ] `mobile/membres.html` : décider du contenu ou retirer du menu
- [ ] `mobile/animation-peinture.html` : ajouter H2 et enrichir le texte
- [ ] `mobile/photos.html` : ajouter un court texte de présentation de la galerie
