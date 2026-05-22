# 09 - Authentification API JWT

## Objectif

Mettre en place une authentification moderne pour une API Rails stateless et comprendre ce que signifie réellement sécuriser un accès API.

## Pourquoi l'authentification est importante

Une API expose souvent :

- des données privées
- des opérations sensibles
- des actions réservées à certains utilisateurs

Sans authentification claire, il est impossible de savoir qui appelle l'API.

## Stack fréquente

- `devise` pour la gestion utilisateur
- `devise-jwt` pour l'authentification par token

## Devise

Devise fournit :

- l'inscription
- la connexion
- le hash des mots de passe
- des helpers d'authentification

### Pourquoi Devise est utile

Devise évite de réécrire toute la base de l'authentification à la main.

Il permet de partir sur une solution éprouvée, à condition de comprendre ce qu'il fait.

## `devise-jwt`

Avec `devise-jwt`, l'API peut émettre un token JWT après connexion.

### Ce qu'est un JWT

Un JWT est un token signé que le client envoie ensuite à chaque requête protégée.

Cela permet à l'API de reconnaître l'utilisateur sans session serveur classique.

## Register API

Tu exposes une route d'inscription qui crée l'utilisateur avec des validations claires.

### Règle

L'inscription ne doit pas seulement créer un utilisateur. Elle doit aussi :

- valider correctement les données
- renvoyer une réponse propre
- éviter les messages trop bavards sur la sécurité

## Login API

Flux classique :

1. le client envoie email + mot de passe
2. Rails valide les identifiants
3. un JWT est renvoyé
4. le client stocke ce token

## Header d'autorisation

Le client renvoie généralement :

```http
Authorization: Bearer <token>
```

### Explication

À chaque requête protégée, le token permet à Rails de retrouver l'utilisateur authentifié.

## `current_user`

Une fois le token valide, Rails peut identifier `current_user` dans les contrôleurs.

### Pourquoi c'est central

`current_user` sert ensuite à :

- savoir qui appelle l'API
- limiter l'accès à certaines ressources
- appliquer des policies

## Refresh token

Le JWT pur sans refresh impose souvent des tokens courts.

Pour une application sérieuse, pense à :

- un access token court
- un refresh token géré séparément
- une logique de rotation ou de révocation

### Règle

Ne pense pas uniquement "connexion". Pense cycle de vie complet du token.

## Sécurisation API

- mot de passe fort
- expiration de token
- révocation si nécessaire
- HTTPS obligatoire
- messages d'erreur sobres

## Comparaison avec Laravel

- l'équivalent conceptuel peut être Sanctum ou un package JWT
- Devise est très puissant mais demande d'accepter son cadre
- il faut comprendre le flux, pas seulement copier une configuration

## Ce que tu dois retenir

L'authentification API ne se résume pas à générer un token. Il faut penser identité, durée de vie, révocation, sécurité du transport et cohérence de tout le flux de connexion.
