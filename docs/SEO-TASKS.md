# SEO — Suivi des tâches Aboriginal Way

Dernière mise à jour : 2026-03-10

## Légende
- `[ ]` À faire &nbsp;|&nbsp; `[~]` En cours &nbsp;|&nbsp; `[x]` Terminé &nbsp;|&nbsp; `[!]` Bloqué / décision requise

---

## Axe 1 — Qualité et fraîcheur du contenu

### Audit des pages desktop (état au 2026-03-10)

| Page | État contenu | Problèmes |
|---|---|---|
| `home.html` | ✅ Bon (~500 mots, 5 sections H2) | — |
| `presentation.html` | ⚠️ Squelettique (~80 mots, 3 §) | Réécriture complète nécessaire |
| `artistes.html` | ⚠️ Liste de noms + 2 vidéos YT | Aucune biographie, zéro texte indexable |
| `didgeridoo.html` | ⚠️ Très court (4 lignes + image flyer) | Contenu insuffisant pour le SEO |
| `animation-peinture.html` | 🔴 Quasi vide (H1 + iframe Vimeo) | Zéro texte, CSS manquant, background absent |
| `exposition.html` | ⚠️ Court (1 vidéo + 2 lignes) | Pas de description de l'exposition |
| `activites.html` | 🔴 Image GIF = zéro texte indexable | Contenu entièrement invisible pour Google |
| `temps.html` | ⚠️ 1 événement daté de 2011 | URL non propre, contenu périmé, 15 ans |
| `liens.html` | ⚠️ 3 liens HTTP, peu de texte | URL non propre, liens HTTP, contenu minimal |
| `membres.html` | 🔴 "Page en construction" | noindex, aucun contenu |
| `partenaires.html` | ❓ Non audité | — |
| `photo.html` | ❓ Non audité | — |
| `contact.html` | ❓ Non audité | — |

### Tâches par page

- [ ] `presentation.html` — réécriture complète desktop + mobile (priorité 1)
- [ ] `animation-peinture.html` — ajouter contenu textuel + corriger CSS/background
- [ ] `activites.html` — remplacer le GIF par du contenu texte structuré
- [ ] `artistes.html` — ajouter biographies signées pour chaque artiste
- [ ] `didgeridoo.html` — enrichir (technique, programme, tarifs, FAQ)
- [ ] `exposition.html` — décrire l'exposition, les œuvres, la démarche
- [ ] `temps.html` — décider : archive ? page agenda renommée ? corriger URL canonique
- [ ] `liens.html` — enrichir le contexte de chaque lien, corriger URL canonique
- [ ] `membres.html` — décider du contenu ou supprimer du menu
- [ ] Auditer `partenaires.html`, `photo.html`, `contact.html`

### Fraîcheur

- [ ] Créer une section Agenda / Actualités (entrées datées, même minimaliste)
- [ ] Définir une cadence de mise à jour minimale (1 entrée/trimestre)

---

## Axe 2 — Answer Engine Optimization (AEO)

Objectif : être cité dans les réponses IA (Perplexity, SGE, ChatGPT) pour les requêtes liées à l'art aborigène, didgeridoo, ateliers culturels en France.

- [ ] `didgeridoo.html` — structurer autour de la question "Comment apprendre le didgeridoo ?" + bloc FAQ JSON-LD
- [ ] `animation-peinture.html` — structurer autour de "Qu'est-ce qu'un atelier de peinture aborigène ?" + FAQ JSON-LD
- [ ] `exposition.html` — structurer autour de "Où voir une exposition d'art aborigène en France ?" + FAQ JSON-LD
- [ ] Chaque page clé : ajouter un paragraphe d'accroche court (100-150 mots, réponse directe) avant le développement
- [ ] `home.html` — vérifier que les questions/réponses implicites sont explicites (déjà bon, ajustements mineurs)

---

## Axe 3 — EEAT (Expérience, Expertise, Autorité, Confiance)

| Critère | État actuel | Action |
|---|---|---|
| Expérience | Absent | Témoignages, photos de cours/expo réels |
| Expertise | Partiel (home.html) | Contenus signés, biographies artistes |
| Autorité | Faible | Mentions presse, partenaires avec liens |
| Confiance | Partiel | Mentions légales, liens HTTP à corriger |

- [ ] `artistes.html` — biographies signées : région, style, Dreaming représenté
- [ ] `presentation.html` — nommer fondateurs/responsables + légitimité (parcours Australie)
- [ ] Ajouter témoignages réels (enseignants, participants ateliers, organisateurs d'expo)
- [ ] Créer page `mentions-legales.html` (obligatoire loi 1901 + RGPD + signal confiance Google)
- [ ] Corriger tous les liens `http://` → `https://` (Territory Essence, Burrup, Dauphins)
- [ ] Chercher des mentions presse existantes à citer sur le site

---

## Axe 4 — Core Web Vitals

- [ ] Lancer audit PageSpeed Insights sur `aboriginalway.fr` (desktop + mobile)
- [ ] Lancer audit PageSpeed Insights sur `aboriginalway.fr/animation-peinture` (page la plus légère/fragile)
- [ ] En fonction des résultats :
  - [ ] Convertir images JPEG → WebP
  - [ ] Ajouter `width`/`height` explicites sur toutes les images (réduction CLS)
  - [ ] Ajouter `loading="lazy"` sur images hors-écran
  - [ ] Évaluer `<link rel="preload">` pour l'image hero de `home.html`
  - [ ] Ajouter `title` sur les iframes YouTube/Vimeo (accessibilité + signaux)

---

## Axe 5 — UX Mobile

- [ ] Auditer les 11 pages mobiles : meta description, H1/H2, longueur de contenu
- [ ] Vérifier correspondance contenu desktop ↔ mobile (risque de dérive)
- [ ] Tester rendu sur mobile réel : tap targets, lisibilité, scroll
- [ ] **Règle de workflow** : chaque enrichissement desktop → la même feature branch inclut le mobile

### Pages mobiles à auditer

| Page mobile | Correspondance desktop | Auditée |
|---|---|---|
| `mobile/index.html` | `home.html` | ❓ |
| `mobile/presentation.html` | `presentation.html` | ❓ |
| `mobile/artistes.html` | `artistes.html` | ❓ |
| `mobile/didgeridoo.html` | `didgeridoo.html` | ❓ |
| `mobile/animation-peinture.html` | `animation-peinture.html` | ❓ |
| `mobile/exposition.html` | `exposition.html` | ❓ |
| `mobile/activites.html` | `activites.html` | ❓ |
| `mobile/membres.html` | `membres.html` | ❓ |
| `mobile/partenaires.html` | `partenaires.html` | ❓ |
| `mobile/photos.html` | `photo.html` | ❓ |
| `mobile/contact.html` | `contact.html` | ❓ |

---

## Axe 6 — Backlinks de qualité

- [ ] Lister tous les lieux d'expo passés → leur demander un lien vers aboriginalway.fr
- [ ] Chercher articles de presse existants avec version en ligne → demander correction/ajout lien
- [ ] Annuaires associatifs : data.gouv.fr, associations.gouv.fr, annuaires culturels régionaux
- [ ] Vérifier éligibilité Wikipedia (Territory Essence, artistes partenaires)
- [ ] Sites thématiques : forums australophiles, enseignants didgeridoo, musiques du monde
- [ ] Territory Essence — vérifier s'ils ont un lien vers Aboriginal Way sur leur site

---

## Notes transverses

- **Workflow** : chaque tâche = feature branch dédiée → `actualisation` → `main` → `deploy`
- **Sync mobile** : toute modification desktop inclut son équivalent mobile dans la même branche
- **URLs non propres** : `temps.html` et `liens.html` ont des canonical en `/site/ref/documents/` — à corriger lors de leur réécriture
- **Priorité absolue** : pages à zéro contenu texte d'abord (`animation-peinture`, `activites`, `membres`)
