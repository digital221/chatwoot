# Digital Factory

Plateforme de support client omicanale auto-hébergée de [Digital Factory](https://digitalfactory.sn), destinée à centraliser les conversations (chat en direct, e-mail, WhatsApp, Facebook, Instagram, etc.) et l’application mobile associée.

Ce dépôt est une copie de [Chatwoot](https://github.com/chatwoot/chatwoot) (branche `develop`), personnalisée à la marque Digital Factory sur la branche `dfactory-branding`.

**Chatwoot** © 2017-2026, Chatwoot Inc. — publié sous licence MIT (voir [LICENSE](./LICENSE)). Le dossier [`enterprise/`](./enterprise) reste sous la [licence propriétaire Chatwoot](./enterprise/LICENSE) et n’est pas modifié dans cette branche.

## Marque

- Nom affiché : **Digital Factory**
- Couleurs officielles : bleu `#163F83`, jaune `#F4C644`
- Logos : originaux de la charte, proportions conservées (pas de redessin)
- Identifiants d’installation par défaut : `INSTALLATION_NAME`, `BRAND_NAME`, `LOGO`, `LOGO_DARK`, `LOGO_THUMBNAIL`, `BRAND_URL`, `WIDGET_BRAND_URL`, `TERMS_URL`, `PRIVACY_URL`, `DISPLAY_MANIFEST` dans [`config/installation_config.yml`](./config/installation_config.yml)

L’application mobile rebrandée se trouve sur [`digital221/chatwoot-mobile-app`](https://github.com/digital221/chatwoot-mobile-app), branche `dfactory-branding` (identifiant `sn.digitalfactory.support`, aide : https://digitalfactory.sn).

Le bandeau « Propulsé par / Powered by » du widget et des e-mails est conservé (fonctionnalité de masquage réservée à l’édition Enterprise). Le nom affiché est Digital Factory.

## Licence

- **Édition communautaire** (tout le dépôt hors `enterprise/`) : licence MIT. Vous pouvez l’utiliser, la modifier, la déployer et la redistribuer, à condition de conserver la notice de copyright et la licence.
- **Dossier `enterprise/`** : licence propriétaire Chatwoot. Son usage en production exige un abonnement Enterprise Chatwoot valide. Cette branche ne modifie pas ce dossier et ne débloque aucune fonction payante (`disable_branding`, plans, etc.).

Voir aussi la [FAQ officielle Chatwoot](https://developers.chatwoot.com/self-hosted/faq) sur la personnalisation de la marque et les usages encouragés.

## Déploiement (auto-hébergé)

Aucun déploiement n’est effectué depuis cette branche. Pour un premier environnement, prévoir :

1. Un serveur Linux avec Docker et Docker Compose
2. PostgreSQL 16 avec l’extension pgvector (l’image `pgvector/pgvector:pg16` est déjà référencée dans `docker-compose.production.yaml`)
3. Redis
4. Un sous-domaine suggéré : `support.digitalfactory.sn` (à pointer vers le service, puis renseigner `FRONTEND_URL`)
5. Un service SMTP (variables `SMTP_*` et `MAILER_SENDER_EMAIL` dans `.env`)
6. Un stockage des pièces jointes : local (`ACTIVE_STORAGE_SERVICE=local`) ou objet compatible S3
7. Une clé secrète Rails (`SECRET_KEY_BASE`) et un mot de passe Redis

Point de départ : copier [`.env.example`](./.env.example) vers `.env`, construire l’image à partir de ce dépôt (ne pas utiliser l’image publique `chatwoot/chatwoot` si l’on veut la marque Digital Factory), puis suivre le [guide officiel de déploiement](https://developers.chatwoot.com/self-hosted/deployment/requirements).

```bash
# Exemple — construire l’image depuis cette branche, puis lancer la stack de production
docker compose -f docker-compose.production.yaml build
docker compose -f docker-compose.production.yaml up -d
```

Le fichier `docker-compose.production.yaml` d’origine pointe vers `chatwoot/chatwoot:latest` : il faudra le faire pointer vers l’image construite localement avant un vrai déploiement.

Documentation amont : [developers.chatwoot.com](https://developers.chatwoot.com/).

## Branches

Le modèle de branches amont est git-flow. La branche de base du fork est `develop`. Les personnalisations Digital Factory sont isolées sur `dfactory-branding`.
