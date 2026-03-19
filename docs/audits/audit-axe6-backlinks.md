# Audit Axe 6 — Backlinks de qualité

Date : 2026-03-10 | Méthode : inventaire statique (code source) + recommandations stratégiques
⚠️ L'inventaire des **backlinks entrants** nécessite Google Search Console ou un outil externe (Ahrefs, Majestic).
Cet audit couvre : liens sortants, mentions de lieux/partenaires exploitables, stratégie d'acquisition.

---

## Liens sortants existants (inventaire complet)

| URL | Page source | Protocol | Texte d'ancre |
|---|---|---|---|
| `http://www.territoryessence.com/` | `partenaires.html`, `liens.html`, `présentation.html`, `mobile/partenaires.html` | ⚠️ HTTP | "Territory Essence" |
| `http://www.standupfortheburrup.com` | `liens.html` | ⚠️ HTTP | "Stand Up For The Burrup" |
| `http://www.compagnie-dauphins.com` | `liens.html` | ⚠️ HTTP | "La Compagnie des Dauphins" |
| `https://www.lerevedelaborigene.org/` | `partenaires.html`, `mobile/partenaires.html` | ✅ HTTPS | "Le Rêve de l'Aborigène" |
| `https://www.lerevedelaborigene.org/billetterie/…` | `partenaires.html`, `mobile/partenaires.html` | ✅ HTTPS | "Billetterie →" |
| `https://www.youtube.com/embed/tlGMBwVpvzs` | `artistes.html` + mobile | ✅ | iframe |
| `https://www.youtube.com/embed/jqJsmVfeMXo` | `artistes.html` + mobile | ✅ | iframe |
| `https://www.youtube.com/embed/7xKjb7XKOv0` | `exposition.html` + mobile | ✅ | iframe |
| `https://player.vimeo.com/video/128914515` | `animation-peinture.html` + mobile | ✅ | iframe |
| `https://vimeo.com/128914515` | `animation-peinture.html` (desktop) | ✅ | Lien texte sous iframe |

**Correctifs liens sortants HTTP :**
- Territory Essence : vérifier si `https://www.territoryessence.com` est accessible (le site peut avoir évolué)
- Burrup : `http://www.standupfortheburrup.com` — vérifier si le site existe encore
- Dauphins : `http://www.compagnie-dauphins.com` — vérifier disponibilité

---

## Lieux et entités mentionnés (capital d'autorité non exploité)

Ces lieux apparaissent dans le contenu ou les photos mais ne sont **pas liés** et ne génèrent pas de backlinks :

| Entité | Source | Type | Potentiel lien |
|---|---|---|---|
| MJC Louis Aragon | `photo.html` (photos) | Lieu d'exposition | Demander lien sur leur site |
| Maison des Carmélites, Chaumont | `temps.html` | Lieu d'exposition 2011 | Peut-être trop ancien |
| Eskapad | `photo.html` (photos) | Lieu d'exposition | Identifier la structure, demander lien |
| Territory Essence | `partenaires.html` | Partenaire commercial | Vérifier s'ils ont un lien entrant vers aboriginalway.fr |
| Le Rêve de l'Aborigène | `partenaires.html` | Partenaire festival | Vérifier lien entrant sur lerevedelaborigene.org |

---

## Stratégie d'acquisition — Sources par priorité

### P1 — Partenaires actifs (gain rapide, relation existante)

| Source | Action | Effort |
|---|---|---|
| **Le Rêve de l'Aborigène** | Vérifier si `lerevedelaborigene.org` liste Aboriginal Way comme partenaire avec lien | Faible |
| **Territory Essence** | Demander un lien vers `aboriginalway.fr` sur leur site | Faible |
| **MJC Louis Aragon** | Identifier la MJC (à vérifier : laquelle ? Massy ? Stains ?), demander un lien dans leurs archives d'événements | Moyen |

### P2 — Lieux d'exposition passés

Chaque lieu où Aboriginal Way a exposé est un backlink potentiel de qualité (sites institutionnels = autorité élevée).

- [ ] Recenser **tous** les lieux d'exposition depuis 2007 (médiathèques, galeries, écoles, MJC, maisons de quartier)
- [ ] Contacter leur webmaster pour ajouter un lien dans leurs archives d'événements culturels
- [ ] Modèle de message type à préparer

### P3 — Annuaires institutionnels

| Source | URL à vérifier | Pertinence |
|---|---|---|
| Journal Officiel associations | journal-officiel.gouv.fr | Fort (officiel) |
| data.gouv.fr | data.gouv.fr | Moyen |
| Annuaire associations.gouv.fr | — | Moyen |
| Annuaire culture DRAC | Selon région | Fort |
| Annuaire festivals musiques du monde | — | Moyen |
| Portail peuples autochtones / Survie | — | Moyen |

### P4 — Médias et presse

- [ ] Rechercher les articles de presse existants sur Aboriginal Way (Google : `"Aboriginal Way" site:.fr`)
- [ ] Si articles web existants sans lien : contacter les rédactions pour ajouter le lien
- [ ] Proposer un communiqué de presse pour les prochains événements (festival juillet 2026)

### P5 — Sites thématiques et communautés

| Type | Exemples | Action |
|---|---|---|
| Forums didgeridoo | didgeridoo-dream.com, forums spécialisés | Profil de membre avec lien site |
| Communautés australophiles | France-Australie, associations franco-australiennes | Annuaire membre |
| Sites musiques du monde | — | Contact éditorial |
| Enseignants EDD / education artistique | — | Ressource pédagogique à proposer |

---

## Ce qu'il ne faut PAS faire

- ❌ Annuaires généralistes de faible qualité (lien payant ou gratuit sur des annuaires spam)
- ❌ Échanges de liens artificiels ("tu me mets un lien, je t'en mets un")
- ❌ Acheter des backlinks
- ❌ Commentaires de blog avec lien (footprint de spam)

---

## Vérifications techniques à effectuer

- [ ] Google Search Console → rapport "Liens" → inventaire backlinks actuels
- [ ] Vérifier si `lerevedelaborigene.org` liste Aboriginal Way avec lien actif
- [ ] Vérifier accessibilité des 3 liens HTTP sortants (Territory Essence, Burrup, Dauphins)
- [ ] Recherche Google : `"Aboriginal Way" -site:aboriginalway.fr` → mentions non liées à transformer en backlinks

---

## Note sur les réseaux sociaux

Aucun lien vers des réseaux sociaux n'est présent sur le site. Si Aboriginal Way a une page Facebook, Instagram ou YouTube, les lier depuis le site :
1. Crée des signaux d'entité pour Google
2. Permet de centraliser l'audience
3. Les profils RS bien alimentés peuvent générer des backlinks indirects (partages, citations)
