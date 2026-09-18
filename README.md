# Djonanko Pay — Documentation développeur

Documentation publique de l'API et du dashboard marchand, construite avec [Mintlify](https://mintlify.com).

## Lancer en local

```bash
npm install
npm run dev
```

Puis ouvrir http://localhost:3000.

## Structure

| Chemin | Contenu |
|---|---|
| `docs.json` | Configuration Mintlify : thème, navigation, playground |
| `openapi.yaml` | Spécification OpenAPI 3.1 — **source de vérité** du playground et des pages d'endpoint |
| `introduction.mdx`, `demarrage-rapide.mdx` | Pages d'accueil |
| `concepts/` | Authentification, flux de paiement, pays & opérateurs, erreurs |
| `guides/` | Guides d'intégration (liens, QR, webhooks, reversements, IP, clés, Postman, prod) |
| `dashboard/` | Un onglet du dashboard marchand = une page |
| `api-reference/` | Une page MDX par endpoint, chacune liée à une opération de `openapi.yaml` via le frontmatter `openapi:` |
| `DjonankoPay.postman_collection.json` | Collection Postman téléchargeable (identifiants remplacés par des variables) |

## Mettre à jour un endpoint

1. Modifier l'opération dans `openapi.yaml` (paramètres, schémas, exemples).
2. Si l'endpoint est nouveau : créer `api-reference/<groupe>/<nom>.mdx` avec `openapi: "METHOD /path"` et l'ajouter dans `docs.json`.
3. Vérifier : `npm run validate` puis `npm run check`.

## Sources

Le contenu a été rédigé à partir de `djonanko-core-api/src/web-merchant` (contrôleur, DTOs, services), de `djonanko-core-api/MERCHANT_WEBHOOK_DELIVERY.md` et du dashboard `mobilepay-africa-gateway`.

## Points à confirmer avant publication

- `GET /web-merchant/payment/status`, `/payments`, `/get-balance` et `/set-webhook-url` sont documentés avec le **jeton marchand** (`authenticationtoken`), conformément aux guards du contrôleur. L'ancienne collection Postman les appelait avec la clé API : à vérifier sur la prod.

## Déploiement

Connecter le dépôt à Mintlify (dashboard Mintlify → GitHub app). Chaque push sur la branche principale redéploie le site.
