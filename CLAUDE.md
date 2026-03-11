# CLAUDE.md — Aboriginal Way

Fichier de référence lu à chaque session. Contient les préférences du projet et l'index de la documentation.

---

## Préférences générales

- **Commits Git** : ne jamais inclure `Co-Authored-By: Claude...` dans les messages de commit.
- **Langue** : répondre en français.

## Workflow Git

- **Ne jamais produire de code sans accord préalable.** Avant tout changement, proposer une stratégie (les étapes), attendre la validation, puis implémenter.
- **`actualisation` = documentation uniquement.** Seuls les fichiers `docs/`, `CLAUDE.md`, `README.md` peuvent être commités directement sur `actualisation`. Tout fichier HTML/CSS/JS/`.htaccess` doit transiter par une feature branch.
- **Une branche par feature/tâche.** Créer une branche dédiée avant toute modification de code. Plusieurs correctifs liés peuvent être regroupés sur une même branche (ex. `fix-mobile-meta`). La finaliser et la valider avant de merger sur `actualisation`.
- Flux : `feature-branch` → `actualisation` → `main` → `deploy` (prod)
- **Après chaque merge `main` → `deploy`** : supprimer les fichiers `.md` du tracking (`git rm --cached *.md docs/*.md`) et commiter. Le `.gitignore` de `deploy` contient déjà `*.md` mais ne désuite pas les fichiers déjà suivis.

## Workflow de collaboration

- **réflexion** : on discute stratégie avant de faire.
- **go** : validation explicite reçue ("go", "exécute", "c'est bon"). Claude implémente.
- **Modification du CLAUDE.md** : toujours présenter un avant/après sur les sections concernées avant d'écrire. Ne jamais modifier sans validation explicite.

---

## Documentation du projet

| Fichier | Rôle | Mettre à jour quand |
|---------|------|---------------------|
| `SEO.md` | Journal des actions SEO | À chaque action SEO mergée dans `actualisation` |
| `CLAUDE.md` | Référence session IA | À chaque merge dans `actualisation` (branches, règles) |
| `README.md` | Vue d'ensemble projet | Changement de structure, déploiement, hébergeur |
| `ROUTING.md` | Architecture SPA | Modification du routeur ou des redirections |
| `mobile/README.md` | Spécifique site mobile | Modification des pages ou CSS mobile |

**Règle transversale** : la documentation se met à jour dans l'étape 2 du workflow Git, avant le merge `actualisation` → `main`, jamais après.

---

## Migration hébergeur

- DNS : 1&1 redirige désormais vers o2switch ✅
- Cache : **TigerCache** (OpenLiteSpeed) — fonctionne sur domaine
- Le site est 100% statique, pas de base de données. Le `.htaccess` est compatible Apache/cPanel sans modification.

---

## Contexte projet

Site vitrine pour l'association **Aboriginal Way** (loi 1901, fondée en 2007). Promotion de l'art et de la culture aborigène australienne.

- Repo : `BenGoGithub/AboriginalWay`
- Branche principale : `main`
- Branches mergées dans `actualisation` : `seo-homepage-content`, `seo-og-url`, `seo-descriptions`, `fix-layout-940px`, `claude/add-touch-icon-U3XyO`, `fix-mobile-meta`, `fix-desktop-perf`
- Branches en attente : `fix-seo-balises-desktop` (relecture), `claude/haloscan-integration-evaluation-PhEnb` (en cours)
- Déploiement de test : `http://tuyo2268.odns.fr/`

### Structure clé

```
index.html              # Point d'entrée desktop (SPA router + redirection mobile)
mobile/                 # Site mobile dédié (11 pages + mobile.css)
site/ref/documents/     # Pages de contenu desktop (13 fichiers HTML)
site/ref/image/         # Images partagées (~94 fichiers)
site/ref/style/         # CSS desktop (general.css)
.htaccess               # Compression, cache, redirects 301, SPA rewrite
sitemap.xml             # Sitemap HTTPS (URLs propres)
```