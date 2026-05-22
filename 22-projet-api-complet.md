# 22 - Projet API complet

## Objectif

Assembler tout le parcours dans un projet final réaliste qui serve de preuve de compétence.

## Idée de projet

Construire une API de marketplace ou de gestion de contenu avancée avec :

- authentification JWT
- CRUD de ressources
- rôles et permissions
- upload d'image
- notifications en temps réel
- jobs asynchrones
- tests

## Pourquoi ce projet final est important

Ce projet doit te forcer à relier toutes les briques du cours.

Le but n'est pas seulement que "ça fonctionne", mais que l'architecture soit lisible, cohérente et prête pour une vraie équipe backend.

## Modules du projet

### 1. Auth JWT

- inscription
- connexion
- déconnexion
- profil courant

### 2. CRUD principal

Exemple :

- users
- posts
- comments
- categories

### 3. Rôles et permissions

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
- traitement d'image
- webhook asynchrone

### 7. Pagination

- index paginés
- métadonnées de pagination

### 8. Tests

- request specs pour les endpoints critiques
- specs de services
- specs de policies

## Architecture propre attendue

Le projet doit idéalement contenir :

- des contrôleurs fins
- des modèles avec validations et relations
- des services pour les use cases
- des policies pour l'autorisation
- des serializers pour les payloads
- des jobs pour l'asynchrone

## Définition de done

Le projet est réussi si :

- l'API est versionnée
- les erreurs sont cohérentes
- les permissions sont testées
- les uploads sont sécurisés
- les jobs tournent hors HTTP
- le déploiement est préparé sans gros rework

## Roadmap de réalisation

1. Initialiser l'API Rails.
2. Ajouter `User` et l'auth JWT.
3. Ajouter une ressource métier principale.
4. Ajouter les policies.
5. Ajouter serializers et pagination.
6. Ajouter upload et jobs.
7. Ajouter les tests.
8. Préparer la production.

## Ce que tu dois retenir

Le projet final doit montrer que tu sais concevoir une API Rails complète, pas seulement additionner des fonctionnalités isolées.
