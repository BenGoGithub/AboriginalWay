# CLAUDE.md — Aboriginal Way

Fichier de référence lu à chaque session. Contient les préférences du projet et l'index de la documentation.

---

## Préférences générales

- **Commits Git** : ne jamais inclure `Co-Authored-By: Claude...` dans les messages de commit.
- **Langue** : répondre en français.

## Workflow Git

- **Ne jamais produire de code sans accord préalable.** Avant tout changement, proposer une stratégie (les étapes), attendre la validation, puis implémenter.
- **Une branche par feature/tâche.** Créer une branche dédiée (ex. `seo-homepage-content`) pour chaque tâche. La finaliser et la valider avant de merger sur `actualisation`.
- **`actualisation` ne reçoit que du code finalisé.** C'est la branche de staging, pas de travail en cours.
- Flux : `feature-branch` → `actualisation` → `main` (prod)

---

## Documentation du projet

| Fichier | Contenu |
|---------|---------|
| `README.md` | Vue d'ensemble du projet, structure des dossiers, déploiement |
| `ROUTING.md` | Architecture du routeur SPA (History API / pushState), fichiers modifiés, points techniques |
| `SEO.md` | Journal de bord des actions SEO (tableau de suivi numéroté), notes techniques |
| `mobile/README.md` | Documentation spécifique au site mobile (`mobile/`) |

---

## Migration hébergeur (à faire)

Migrer de **1&1** vers **o2switch** (CDN Cloudflare inclus, sans surcoût).

Étapes : créer compte o2switch → copier fichiers dans `public_html/` via FTP → tester sur domaine temporaire → changer les DNS chez 1&1 → activer CDN Cloudflare depuis cPanel → résilier 1&1.

Le site est 100% statique, pas de base de données. Le `.htaccess` est compatible Apache/cPanel sans modification.

---

## Contexte projet

Site vitrine pour l'association **Aboriginal Way** (loi 1901, fondée en 2007).
Promotion de l'art et de la culture aborigène australienne.

- Repo : `BenGoGithub/AboriginalWay`
- Branche principale : `main`
- Branche active : `seo-homepage-content` (à merger vers `actualisation` → `main`)
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
