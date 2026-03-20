# Audit Axe 3 — EEAT (Expérience, Expertise, Autorité, Confiance)

Date : 2026-03-10 | Méthode : analyse statique du code source

---

## Rappel des critères EEAT

- **E**xpérience : le site témoigne-t-il d'une expérience vécue, concrète et documentée ?
- **E**xpertise : le contenu démontre-t-il une maîtrise du sujet ?
- **A**utorité : le site est-il reconnu par d'autres sources ? Y a-t-il des signaux d'autorité ?
- **T**rust (Confiance) : le site est-il transparent, fiable, sécurisé ?

---

## E — Expérience

| Signal | Présent | Détail |
|---|---|---|
| Témoignages de participants | ❌ | Aucun sur aucune page |
| Photos de cours / ateliers réels | ❌ | Galerie = œuvres uniquement, pas d'ateliers en action |
| Photos d'expositions avec public | ⚠️ | `mjc_louis_aragon.jpg`, `eskapad.jpg` dans galerie, mais sans contexte narratif |
| Récits d'événements passés | ⚠️ | `temps.html` décrit Chaumont 2011 mais sans témoignage ni retour |
| Nombre de participants / stats | ❌ | — |
| Durée d'activité mise en avant | ⚠️ | "Fondée en 2007" présent mais pas exploité (18 ans d'expérience) |

**Score Expérience : 1/6** — Critique. Le site ne documente pas le vécu de l'association.

---

## E — Expertise

| Signal | Présent | Détail |
|---|---|---|
| Contenu expert sur l'art aborigène | ✅ | `home.html` : explication du Dreaming, dot painting, 60 000 ans — correct |
| Contenu expert sur le didgeridoo | ❌ | `didgeridoo.html` : 4 lignes, aucun contenu technique |
| Contenu expert sur la peinture | ❌ | `animation-peinture.html` : vide |
| Auteur / signataire des contenus | ❌ | Aucune page n'est signée |
| Références culturelles citées | ⚠️ | Territory Essence, Burrup — mais sans contextualisation |
| Vocabulaire spécialisé utilisé | ✅ | "Dreaming", "Dot painting", "Arnhem Land", "Japanardi" (nom de peau) |

**Score Expertise : 2/6** — Partiel. La page d'accueil est bonne mais c'est la seule.

---

## A — Autorité

| Signal | Présent | Détail |
|---|---|---|
| Mentions de lieux partenaires | ⚠️ | MJC Louis Aragon, Maison des Carmélites (Chaumont), Eskapad — dans galerie mais non contextualisés |
| Liens entrants connus | ❌ | Non mesurable statiquement (nécessite Search Console) |
| Partenaires avec liens actifs | ⚠️ | Le Rêve de l'Aborigène (HTTPS ✅), Territory Essence (HTTP ⚠️) |
| Mentions presse citées | ❌ | Aucune |
| Réseaux sociaux liés | ❌ | Aucun lien vers RS sur le site |
| Association référencée (data.gouv…) | ❓ | Non vérifié (nécessite recherche externe) |
| Wikipedia / sources tierces | ❌ | Aucune mention |

**Score Autorité : 1/7** — Très faible. Le capital d'autorité acquis depuis 2007 n'est pas documenté sur le site.

---

## T — Trust (Confiance)

| Signal | Présent | Détail |
|---|---|---|
| HTTPS | ✅ | Redirect 301 HTTP→HTTPS dans `.htaccess` |
| Mentions légales | ❌ | **Absentes** — obligatoires (loi française + RGPD) pour une association loi 1901 |
| Politique de confidentialité | ❌ | Absente — GTM est installé, collecte de données sans mention |
| Adresse e-mail visible | ✅ | `aboriginalway@free.fr` — mais domaine `@free.fr` peu professionnel |
| Numéro de téléphone | ✅ | `06 64 76 07 30` dans `contact.html` (desktop) + `mobile/contact.html` |
| Adresse postale | ❌ | Absente |
| N° RNA / SIRET association | ❌ | Absent |
| Liens sortants HTTP (non sécurisés) | ❌ | Territory Essence, Burrup, Compagnie des Dauphins = tous en `http://` |
| En-têtes de sécurité | ✅ | `X-Content-Type-Options`, `X-Frame-Options`, `Referrer-Policy` dans `.htaccess` |
| Transparence sur les artistes | ⚠️ | Warning décès artistes présent sur artistes/expo/galerie — bonne pratique culturelle ✅ |

**Score Trust : 4/10** — Insuffisant. L'absence de mentions légales est un problème légal ET de confiance Google.

---

## Synthèse EEAT

| Dimension | Score | Priorité |
|---|---|---|
| Expérience | 🔴 1/6 | P1 |
| Expertise | 🟡 2/6 | P2 |
| Autorité | 🔴 1/7 | P1 |
| Confiance | 🟡 4/10 | P0 |

---

## Actions recommandées par priorité

### P0 — Légal / Trust
- [ ] Créer `mentions-legales.html` : nom de l'association, RNA, siège social, directeur de publication, hébergeur
- [ ] Créer ou lier une politique de confidentialité (GTM implique collecte de données)
- [ ] Corriger tous les liens HTTP → HTTPS (Territory Essence, Burrup, Dauphins)

### P1 — Expérience
- [ ] Ajouter une section témoignages sur les pages d'activités (1-2 témoignages suffisent)
- [ ] Ajouter des photos d'ateliers en action (participants, pas seulement les œuvres)
- [ ] Sur `temps.html` / future page Agenda : raconter les événements passés avec photos et retours
- [ ] Exploiter "18 ans d'expérience" comme argument fort sur `présentation.html`

### P1 — Autorité
- [ ] Créer une section "Ils nous ont accueillis" sur `présentation.html` ou `exposition.html` (MJC Louis Aragon, Maison des Carmélites, Eskapad, etc.)
- [ ] Chercher les articles de presse existants et les citer avec source
- [ ] Vérifier si l'association est référencée sur data.gouv.fr / Journal Officiel associations

### P2 — Expertise
- [ ] Signer les contenus : nommer l'auteur/responsable sur `présentation.html`
- [ ] `artistes.html` : biographies des 7 artistes (région, style, Dreaming représenté, parcours)
- [ ] `didgeridoo.html` : contenu technique (technique, histoire de l'instrument, souffle circulaire)
- [ ] `animation-peinture.html` : décrire les techniques enseignées, les symboles, le contexte culturel
