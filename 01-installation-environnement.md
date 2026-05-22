# 01 - Installation et environnement

## Objectif

Mettre en place un environnement Rails API propre, stable et reproductible.

## Pourquoi l'environnement est important

Beaucoup de problèmes Rails au démarrage ne viennent pas du code, mais de l'environnement :

- mauvaise version de Ruby
- conflit entre plusieurs installations
- PostgreSQL mal configuré
- confusion entre les commandes globales et celles du projet

Si la base est propre, tout le reste devient plus fluide.

## Installer Ruby

Rails dépend fortement de la version de Ruby. Il ne faut pas se contenter de la version système.

Les deux gestionnaires les plus connus sont :

- `rbenv`
- `rvm`

Dans la plupart des cas, `rbenv` est suffisant, simple et discret.

## Règle à retenir

Travaille toujours avec une version Ruby contrôlée.

Cela permet :

- d'éviter les différences entre machines
- de reproduire facilement le projet dans une équipe
- de garder une compatibilité propre avec Rails et les gems

## Vérifier les prérequis

Avant de créer un projet Rails API, vérifie :

- Ruby
- Bundler
- PostgreSQL
- Git
- éventuellement Node.js selon les gems ou les outils utilisés

## Installer Rails

```bash
gem install rails
rails -v
```

## Installer PostgreSQL

PostgreSQL est le choix le plus naturel pour une API Rails sérieuse.

Commandes utiles :

```bash
psql --version
pg_isready
```

## Créer un premier projet API

```bash
rails new blog_api --api -d postgresql
cd blog_api
bin/rails db:create
bin/rails server
```

## Pourquoi `--api` est important

Le flag `--api` indique à Rails que tu veux construire une API pure.

Rails enlève alors une partie de l'outillage lié au rendu HTML classique et garde surtout :

- le routage
- les contrôleurs
- ActiveRecord
- les jobs
- le cache
- l'instrumentation

## Structure minimale à connaître

- `app/controllers` : couche HTTP
- `app/models` : données, validations, relations
- `config/routes.rb` : routes de l'application
- `db/migrate` : migrations de base de données
- `config/database.yml` : configuration de la base

## Commandes Rails importantes

```bash
bin/rails routes
bin/rails console
bin/rails generate model Post title:string
bin/rails db:migrate
bin/rails test
```

## Pourquoi utiliser `bin/rails`

`bin/rails` exécute Rails dans le contexte exact du projet courant.

C'est une règle importante, parce que cette commande :

- utilise les bonnes gems du projet
- respecte la version installée localement
- évite les surprises liées à une installation globale différente

## Comparaison avec Laravel

- `php artisan` devient `bin/rails`
- `.env` peut exister, mais Rails s'appuie aussi fortement sur ses conventions de configuration
- les générateurs Rails sont très présents dans le workflow quotidien

## Erreurs fréquentes

- utiliser une mauvaise version de Ruby
- oublier `bundle install`
- ne pas créer la base PostgreSQL
- lancer `rails` au lieu de `bin/rails` dans le projet

## Ce que tu dois retenir

Un environnement propre n'est pas un détail. C'est la condition pour apprendre Rails dans de bonnes conditions et éviter de perdre du temps sur de faux problèmes.
