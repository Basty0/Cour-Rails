# 02 - Architecture Rails API

## Objectif

Comprendre comment une requete traverse Rails et comment les dossiers du projet se repartissent les responsabilites.

## MVC dans Rails

- `Model`: donnees, validations, relations, logique liee au domaine
- `View`: faible ou absente dans une API pure
- `Controller`: reception HTTP, orchestration courte, rendu JSON

Dans une API Rails, la vue HTML disparait presque, mais l'idee de separation reste.

## Cycle d'une requete HTTP

1. La requete entre par le routeur.
2. Une route selectionne un controller et une action.
3. Le controller lit `params`.
4. Il delegue au model ou a un service.
5. Rails serialize la reponse en JSON.
6. Le client recoit le status HTTP et le body.

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

## Role de chaque dossier

`app/controllers`
: entree HTTP, auth, rendu, erreurs.

`app/models`
: persistence, validations, associations, scopes.

`app/jobs`
: taches asynchrones.

`config`
: routes, environnement, initializers.

`db`
: schema, migrations, seeds.

## Architecture API only

Avec `rails new mon_api --api`, Rails retire plusieurs middlewares et briques HTML inutiles. Tu gardes le coeur backend:

- routing
- controllers
- ActiveRecord
- ActiveJob
- caching
- instrumentation

## Convention Rails

Rails repose sur le nommage:

- classe `Post` -> table `posts`
- `Api::V1::PostsController` -> chemin de fichier associe
- fichier et nom de constante doivent rester alignes

Quand tu respectes ces conventions, tu configures presque rien.

## Difference avec Laravel

- Laravel expose souvent plus de dossiers "utilitaires" des le depart.
- Rails est plus compact au debut.
- Les controllers Rails sont souvent plus courts.
- ActiveRecord encourage parfois plus de logique model-centree que les pratiques Laravel modernes.

## Architecture saine pour une API

- controllers fins
- models expressifs
- services pour les cas metier complexes
- policies pour l'autorisation
- serializers ou presenters pour des reponses stables

## Ce que tu dois retenir

Rails API est simple en surface mais tres structure. Le vrai gain vient du respect du flux route -> controller -> model/service -> JSON.
