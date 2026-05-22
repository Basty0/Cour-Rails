# 09 - Authentification API JWT

## Objectif

Mettre en place une authentification moderne pour une API Rails stateless.

## Stack frequente

- `devise` pour la gestion utilisateur
- `devise-jwt` pour l'authentification par token

## Devise

Devise fournit:

- inscription
- connexion
- hash de mot de passe
- helpers d'authentification

## devise-jwt

Avec `devise-jwt`, l'API peut emettre un token JWT apres connexion.

## Register API

Tu exposes une route d'inscription qui cree l'utilisateur avec validations claires.

## Login API

Flux classique:

1. le client envoie email + mot de passe
2. Rails valide les credentials
3. un JWT est renvoye
4. le client stocke ce token

## Authorization header

Le client renvoie:

```http
Authorization: Bearer <token>
```

## current_user

Une fois le token valide, Rails peut identifier `current_user` dans les controllers.

## Refresh token

Le JWT pur sans refresh impose souvent des tokens courts. Pour une app serieuse, pense a:

- access token court
- refresh token gere separement
- rotation ou revocation

Selon le besoin, certaines equipes preferent une solution sur mesure plutot qu'une config magique.

## Securisation API

- mot de passe fort
- expiration de token
- revocation si necessaire
- HTTPS obligatoire
- messages d'erreur sobres

## Comparaison Laravel

- equivalent conceptuel de Sanctum ou JWT packages
- Devise est tres puissant mais peut sembler plus "framework-first"
- il faut comprendre le flux, pas juste copier une config

## Ce que tu dois retenir

L'auth ne se limite pas a "generer un token". Il faut penser cycle de vie du token, revocation, expiration et lisibilite du flux de connexion.
