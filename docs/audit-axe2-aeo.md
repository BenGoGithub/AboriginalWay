# Audit Axe 2 — Answer Engine Optimization (AEO)

Date : 2026-03-10 | Méthode : analyse statique du code source

Objectif : être cité dans les réponses directes des moteurs IA (Perplexity, Google SGE, ChatGPT)
pour les requêtes liées à l'art aborigène, au didgeridoo, aux ateliers culturels en France.

---

## Principes AEO évalués

1. **Question centrale explicite** — La page répond-elle à une question claire dès le H1 ?
2. **Réponse directe en tête** — Y a-t-il un paragraphe d'accroche court (~100-150 mots) donnant la réponse avant le développement ?
3. **Structure FAQ** — Y a-t-il des paires question/réponse balisables en `FAQPage` JSON-LD ?
4. **Données structurées** — JSON-LD présent et pertinent ?
5. **Clarté sémantique** — Les H2/H3 formulent-ils des sous-questions ou des réponses partielles ?

---

## Analyse page par page

### `home.html` — Accueil
| Critère | État | Note |
|---|---|---|
| Question centrale | ⚠️ Partiel | H1 = nom de l'asso, pas une question |
| Réponse directe | ✅ Oui | 1er § du `#home-intro` introduit bien l'asso |
| FAQ | ❌ Absent | — |
| JSON-LD | ✅ `Organization` sur `index.html` | Minimal (nom, url, email) |
| Clarté sémantique | ✅ Bon | H2 : "L'art aborigène australien", "Nos activités", etc. |

**Potentiel AEO** : moyen. La page répond bien à "Qu'est-ce qu'Aboriginal Way ?" mais pas à des questions factuelles précises.

---

### `didgeridoo.html` — Cours de Didgeridoo
| Critère | État | Note |
|---|---|---|
| Question centrale | ❌ Non | H1 = "Cours de Didgeridoo" (titre, pas une question) |
| Réponse directe | ❌ Non | Le 1er § est une invitation, pas une réponse |
| FAQ | ❌ Absent | — |
| JSON-LD | ❌ Absent | — |
| Clarté sémantique | ❌ Pauvre | Aucun H2, contenu minimal |

**Requêtes cibles manquées** :
- "Comment apprendre le didgeridoo ?"
- "Où prendre des cours de didgeridoo en France ?"
- "C'est quoi le souffle circulaire ?"
- "Combien coûte un cours de didgeridoo ?"

---

### `animation-peinture.html` — Ateliers peinture
| Critère | État | Note |
|---|---|---|
| Question centrale | ❌ Non | H1 = titre, pas une question |
| Réponse directe | ❌ Non | Page quasi vide |
| FAQ | ❌ Absent | — |
| JSON-LD | ❌ Absent | — |
| Clarté sémantique | ❌ Nulle | Pas de structure textuelle |

**Requêtes cibles manquées** :
- "Qu'est-ce qu'un atelier de peinture aborigène ?"
- "Comment organiser un atelier peinture aborigène pour scolaires ?"
- "Atelier dot painting pour enfants"

---

### `exposition.html` — Exposition An Other Way
| Critère | État | Note |
|---|---|---|
| Question centrale | ❌ Non | H1 = titre d'exposition |
| Réponse directe | ❌ Non | 2 lignes de texte insuffisantes |
| FAQ | ❌ Absent | — |
| JSON-LD | ❌ Absent | — |
| Clarté sémantique | ❌ Pauvre | Aucun H2 |

**Requêtes cibles manquées** :
- "Où voir une exposition d'art aborigène en France ?"
- "Comment accueillir une exposition itinérante ?"
- "Exposition art australien"

---

### `artistes.html` — Les Artistes
| Critère | État | Note |
|---|---|---|
| Question centrale | ❌ Non | H1 = "Les Artistes" |
| Réponse directe | ❌ Non | Liste de noms sans contexte |
| FAQ | ❌ Absent | — |
| JSON-LD | ❌ Absent | Aucun `Person` schema |
| Clarté sémantique | ❌ Nulle | — |

**Requêtes cibles manquées** :
- "Qui est Sandy Walker Japanardi ?"
- "Artistes aborigènes contemporains australiens"
- "Dot painting artiste australien"

---

### `presentation.html` — Présentation
| Critère | État | Note |
|---|---|---|
| Question centrale | ❌ Non | H1 = titre |
| Réponse directe | ⚠️ Partiel | Courte intro, mais insuffisante |
| FAQ | ❌ Absent | — |
| JSON-LD | ❌ Absent | — |
| Clarté sémantique | ⚠️ Partiel | H1 nommés mais non interrogatifs |

---

### `partenaires.html` — Partenaires
| Critère | État | Note |
|---|---|---|
| Question centrale | ❌ Non | — |
| Réponse directe | ✅ Correct | Description de chaque partenaire présente |
| FAQ | ❌ Absent | — |
| JSON-LD | ❌ Absent | Aucun `Organization` pour les partenaires |
| Clarté sémantique | ✅ Bon | H2 par partenaire |

---

## Données structurées existantes

| Élément | Présent | Emplacement | Qualité |
|---|---|---|---|
| `Organization` JSON-LD | ✅ | `index.html` + `mobile/index.html` | Minimal : nom, url, email uniquement |
| `FAQPage` | ❌ | — | — |
| `Event` | ❌ | — | `temps.html` décrit un événement mais sans schema |
| `Person` | ❌ | — | 7 artistes sans schema |
| `LocalBusiness` / `NGO` | ❌ | — | Pertinent pour une association loi 1901 |

---

## Recommandations prioritaires

### 1. Enrichir le JSON-LD `Organization` sur `index.html`
Ajouter : `sameAs` (réseaux sociaux si existants), `logo`, `address`, `areaServed`.

### 2. Ajouter `FAQPage` JSON-LD sur 3 pages clés

**`didgeridoo.html`** — Questions suggérées :
- "Qu'est-ce que le didgeridoo ?"
- "Comment apprendre le souffle circulaire ?"
- "Les cours sont-ils ouverts aux débutants ?"
- "Où se déroulent les ateliers ?"

**`animation-peinture.html`** — Questions suggérées :
- "Qu'est-ce que la peinture aborigène ?"
- "L'atelier est-il adapté aux enfants ?"
- "Comment organiser une animation dans mon établissement ?"

**`exposition.html`** — Questions suggérées :
- "L'exposition peut-elle se déplacer ?"
- "Combien d'œuvres comprend l'exposition ?"
- "Comment accueillir l'exposition ?"

### 3. Ajouter `Person` schema sur `artistes.html`
Pour chaque artiste : `name`, `nationality`, `description`, `sameAs` si page Wikipedia.

### 4. Ajouter `Event` schema sur `temps.html` / future page Agenda

### 5. Rédiger des paragraphes d'accroche directs
Chaque page clé doit commencer par une réponse en 2-3 phrases à la question implicite du visiteur, **avant** tout développement.
