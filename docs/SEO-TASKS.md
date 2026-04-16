# SEO — Suivi des tâches Aboriginal Way

Dernière mise à jour : 2026-04-16

## Légende
- `[ ]` À faire &nbsp;|&nbsp; `[~]` En cours &nbsp;|&nbsp; `[x]` Terminé &nbsp;|&nbsp; `[!]` Bloqué / décision requise

---

## Axe 1 — Qualité et fraîcheur du contenu

### Audit des pages desktop (état au 2026-03-10)
→ Voir détail complet : `docs/audit-axe1-contenu.md`

| Page | État contenu | Problèmes |
|---|---|---|
| `home.html` | ✅ Bon (~500 mots, 5 H2) | — |
| `presentation.html` | ⚠️ Squelettique (~80 mots) | Réécriture complète nécessaire |
| `artistes.html` | ⚠️ Liste + 2 vidéos YT | Zéro biographie |
| `didgeridoo.html` | ⚠️ Très court (~100 mots) | Image flyer non indexable |
| `animation-peinture.html` | 🔴 Quasi vide | CSS `general.css` absent, background absent |
| `exposition.html` | ⚠️ Court (~50 mots) | Pas de description des œuvres |
| `activites.html` | 🔴 Image GIF seulement | Zéro texte indexable |
| `temps.html` | ⚠️ Événement de 2011 | URL non propre, contenu périmé |
| `liens.html` | ⚠️ 3 liens HTTP | URL non propre, peu de contexte |
| `membres.html` | 🔴 "En construction" | `noindex`, aucun contenu |
| `partenaires.html` | ✅ Correct | Territory Essence en HTTP |
| `photo.html` | ⚠️ Galerie sans texte | 27 photos, bons alt, mais zéro contexte |
| `contact.html` | ⚠️ Pauvre | 1 ligne + 3 GIFs |

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
  - [x] Ajouter `loading="lazy"` sur les 6 iframes YouTube/Vimeo (desktop + mobile)
  - [x] Ajouter `loading="lazy"` sur les 27 miniatures de `photo.html`
  - [ ] Ajouter `width`/`height` sur les miniatures de `photo.html` (CLS)
  - [ ] Évaluer `<link rel="preload">` pour l'image hero de `home.html`

---

## Axe 5 — UX Mobile

- [x] Auditer les 11 pages mobiles : meta description, H1/H2, longueur de contenu
- [x] GTM noscript dupliqué supprimé sur 10 pages mobiles
- [x] OG tags ajoutés sur 10 pages mobiles
- [x] Canonicals corrigés sur 11 pages mobiles (→ URLs propres)
- [ ] Vérifier correspondance contenu desktop ↔ mobile (risque de dérive)
- [ ] Tester rendu sur mobile réel : tap targets, lisibilité, scroll
- [ ] **Règle de workflow** : chaque enrichissement desktop → la même feature branch inclut le mobile

### Pages mobiles à auditer
→ Voir détail complet : `docs/audit-axe5-mobile-ux.md`

| Page mobile | Correspondance desktop | Contenu | GTM dupliqué | OG tags | Canonical |
|---|---|---|---|---|---|
| `mobile/index.html` | `home.html` | ⚠️ Nav seule | ✅ | ✅ | ⚠️ `/mobile/` |
| `mobile/presentation.html` | `presentation.html` | ⚠️ ~150 mots | 🔴 ×2 | ❌ | ⚠️ |
| `mobile/artistes.html` | `artistes.html` | ⚠️ Liste seule | 🔴 ×2 | ❌ | ⚠️ |
| `mobile/didgeridoo.html` | `didgeridoo.html` | ✅ ~200 mots | 🔴 ×2 | ❌ | ⚠️ |
| `mobile/animation-peinture.html` | `animation-peinture.html` | ⚠️ ~80 mots | 🔴 ×2 | ❌ | ⚠️ |
| `mobile/exposition.html` | `exposition.html` | ⚠️ ~100 mots | 🔴 ×2 | ❌ | ⚠️ |
| `mobile/activites.html` | `activites.html` | ✅ ~200 mots | 🔴 ×2 | ❌ | ⚠️ |
| `mobile/membres.html` | `membres.html` | 🔴 Construction | 🔴 ×2 | ❌ | ⚠️ |
| `mobile/partenaires.html` | `partenaires.html` | ✅ ~150 mots | 🔴 ×2 | ❌ | ⚠️ |
| `mobile/photos.html` | `photo.html` | ⚠️ Galerie seule | 🔴 ×2 | ❌ | ⚠️ |
| `mobile/contact.html` | `contact.html` | ✅ tél + email | 🔴 ×2 | ❌ | ⚠️ |

---

## Axe 6 — Backlinks de qualité

- [ ] Lister tous les lieux d'expo passés → leur demander un lien vers aboriginalway.fr
- [ ] Chercher articles de presse existants avec version en ligne → demander correction/ajout lien
- [ ] Annuaires associatifs : data.gouv.fr, associations.gouv.fr, annuaires culturels régionaux
- [ ] Vérifier éligibilité Wikipedia (Territory Essence, artistes partenaires)
- [ ] Sites thématiques : forums australophiles, enseignants didgeridoo, musiques du monde
- [ ] Territory Essence — vérifier s'ils ont un lien vers Aboriginal Way sur leur site

---

## Liens vers les audits détaillés

| Axe | Document |
|---|---|
| Axe 1 — Qualité et fraîcheur du contenu | `docs/audit-axe1-contenu.md` |
| Axe 2 — Answer Engine Optimization | `docs/audit-axe2-aeo.md` |
| Axe 3 — EEAT | `docs/audit-axe3-eeat.md` |
| Axe 4 — Core Web Vitals | `docs/audit-axe4-cwv.md` |
| Axe 5 — UX Mobile | `docs/audit-axe5-mobile-ux.md` |
| Axe 6 — Backlinks | `docs/audit-axe6-backlinks.md` |

---

## Session 2026-04-16 — Réalisé

- `fix-seo-canonicalisation` : correction des 3 problèmes de canonisation détectés via Search Console
  - `.htaccess` : ajout redirection 301 `www.aboriginalway.fr` → `aboriginalway.fr`
  - `.htaccess` : ajout redirection 301 `/index.html` → `/`
  - `sitemap.xml` : suppression des 10 pages `/mobile/*.html` (canonical ≠ URL soumise)

**Prochaine priorité** : merger `fix-seo-canonicalisation` → `actualisation` → `main` → `deploy`, puis soumettre le sitemap mis à jour en Search Console

---

## Session 2026-03-10 — Réalisé

- Création de `docs/` + `SEO-TASKS.md` (suivi des tâches SEO)
- Audits complets des 6 axes → 6 documents dans `docs/`
- `fix-mobile-meta` : GTM dupliqué supprimé, OG tags + canonicals corrigés sur 11 pages mobiles
- `fix-desktop-perf` : `loading="lazy"` sur 6 iframes + 27 miniatures, correction `animation-peinture.html`
- `CLAUDE.md` : règle workflow Git clarifiée (`actualisation` = docs uniquement)

**Prochaine priorité** : réécriture contenu `presentation.html` (desktop + mobile) — axe 1 + EEAT

---

## Notes transverses

- **Workflow** : chaque tâche = feature branch dédiée → `actualisation` → `main` → `deploy`
- **Sync mobile** : toute modification desktop inclut son équivalent mobile dans la même branche
- **URLs non propres** : `temps.html` et `liens.html` ont des canonical en `/site/ref/documents/` — à corriger lors de leur réécriture
- **Priorité absolue** : pages à zéro contenu texte d'abord (`animation-peinture`, `activites`, `membres`)
