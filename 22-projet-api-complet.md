# 22 - Projet API Complet

## Objectif

Assembler tout le parcours dans un projet final realiste.

## Idee de projet

Construire une API de marketplace ou de gestion de contenu avancee avec:

- authentification JWT
- CRUD de ressources
- roles et permissions
- upload image
- notifications realtime
- jobs async
- tests

## Modules du projet

### 1. Auth JWT

- inscription
- connexion
- deconnexion
- profil courant

### 2. CRUD principal

Exemple:

- users
- posts
- comments
- categories

### 3. Roles permissions

- user
- editor
- admin

### 4. Upload image

- avatar utilisateur
- image de post

### 5. WebSocket

- notification de nouveau commentaire
- notification d'action admin

### 6. Queue

- email de bienvenue
- traitement image
- webhook async

### 7. Pagination

- index pagines
- meta de pagination

### 8. Tests

- request specs pour endpoints critiques
- specs services
- specs policies

## Architecture propre

Le projet doit idealement contenir:

- controllers fins
- models avec validations et relations
- services pour les use cases
- policies pour l'autorisation
- serializers pour les payloads
- jobs pour l'asynchrone

## Definition de done

Le projet est reussi si:

- l'API est versionnee
- les erreurs sont consistentes
- les permissions sont testees
- les uploads sont securises
- les jobs tournent hors HTTP
- le deploiement est preparable sans rework majeur

## Idee de roadmap de realisation

1. Initialiser l'API Rails.
2. Ajouter User + auth JWT.
3. Ajouter une ressource metier principale.
4. Ajouter policies.
5. Ajouter serializers et pagination.
6. Ajouter upload et jobs.
7. Ajouter tests.
8. Nettoyer pour production.

## Ce que tu dois retenir

Ce projet final doit servir de preuve de competence. L'objectif n'est pas seulement que "ca marche", mais que l'architecture soit lisible pour une equipe backend moderne.
