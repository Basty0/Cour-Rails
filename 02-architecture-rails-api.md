# 02 - Architecture Rails API

## Objectif

Comprendre comment une requête traverse Rails et comment les dossiers du projet se répartissent les responsabilités.

## Vue générale

Rails API reste fondé sur les mêmes principes que Rails classique, mais avec un focus backend.

Tu dois retenir le flux principal :

1. une route reçoit la requête
2. un contrôleur traite l'entrée HTTP
3. le contrôleur appelle un modèle ou un service
4. Rails renvoie une réponse JSON

## MVC dans Rails

- `Model` : données, validations, relations et logique liée au domaine
- `View` : beaucoup moins visible en API pure
- `Controller` : point d'entrée HTTP, orchestration courte, rendu de la réponse

Même si une API n'affiche pas de pages HTML, la logique de séparation reste importante.

## Cycle d'une requête HTTP

Quand un client appelle ton API :

1. Rails lit l'URL et le verbe HTTP
2. le routeur choisit un contrôleur et une action
3. les paramètres arrivent dans `params`
4. l'action exécute une logique métier
5. Rails renvoie un JSON et un code HTTP

## Pourquoi ce cycle doit être clair

Si tu ne comprends pas ce flux, tu risques de mettre la logique au mauvais endroit :

- trop de logique dans le contrôleur
- requêtes SQL mal placées
- réponses JSON improvisées
- sécurité dispersée

## Structure des dossiers

- `app/controllers`
- `app/models`
- `app/jobs`
- `app/mailers`
- `app/services` si tu adoptes ce pattern
- `config`
- `db`
- `lib`
- `spec` ou `test`

## Rôle de chaque dossier

`app/controllers`
: reçoit la requête, lit les paramètres, appelle le domaine, renvoie la réponse.

`app/models`
: représente les entités métier, les validations et les relations.

`app/jobs`
: exécute les tâches asynchrones.

`config`
: contient les routes, les environnements et les initializers.

`db`
: contient les migrations, le schéma et les seeds.

## Règle de structure

Chaque dossier doit garder son rôle.

Par exemple :

- un contrôleur ne doit pas contenir toute la logique métier
- un modèle ne doit pas devenir un conteneur de tout le projet
- une réponse JSON ne doit pas être improvisée dans tous les sens

## Architecture API only

Avec `rails new mon_api --api`, Rails retire une partie des couches inutiles pour une API HTML-less.

Tu conserves le cœur utile pour un backend moderne :

- routing
- controllers
- ActiveRecord
- ActiveJob
- caching
- instrumentation

## Convention Rails

Rails repose fortement sur le nommage.

Exemples :

- `Post` correspond généralement à `posts`
- `Api::V1::PostsController` correspond à un chemin de fichier cohérent
- les noms de classes, modules et fichiers doivent rester alignés

## Pourquoi cette convention compte

Quand tu respectes les conventions :

- tu écris moins de configuration
- ton code se lit plus vite
- un autre développeur Rails retrouve immédiatement ses repères

## Différence avec Laravel

- Laravel expose souvent davantage de structures utilitaires dès le départ
- Rails démarre plus compact
- Rails repose plus fortement sur le nommage et la convention
- un projet Rails devient très agréable dès que l'équipe respecte le cadre

## Architecture saine pour une API

- contrôleurs fins
- modèles expressifs
- services pour les cas métiers complexes
- policies pour l'autorisation
- serializers ou presenters pour les réponses stables

## Ce que tu dois retenir

Rails API est simple en apparence, mais très structuré. Le vrai gain vient du respect du flux route -> contrôleur -> domaine -> réponse JSON.
