# 01 - Installation Environnement

## Objectif

Mettre en place un environnement Rails API propre, stable et reproductible.

## Installer Ruby

Rails depend fortement de la version de Ruby. Evite l'installation systeme et utilise un gestionnaire de versions.

Options classiques:

- `rbenv` pour une gestion simple et discrete
- `rvm` pour une gestion plus complete

Pour un profil backend propre, `rbenv` est souvent suffisant.

## Verifier les prerequis

- Ruby recent
- Bundler
- PostgreSQL
- Node.js si certaines gems ou outils frontend en ont besoin
- Git

## Installer Rails

```bash
gem install rails
rails -v
```

## Installer PostgreSQL

Rails API travaille tres bien avec PostgreSQL. C'est le choix par defaut le plus solide pour un projet serieux.

Verifications utiles:

```bash
psql --version
pg_isready
```

## Creer un premier projet API

```bash
rails new blog_api --api -d postgresql
cd blog_api
bin/rails db:create
bin/rails server
```

Le flag `--api` retire plusieurs couches HTML inutiles pour une API pure.

## Structure initiale a connaitre

- `app/controllers` pour la couche HTTP
- `app/models` pour les entites et la persistence
- `config/routes.rb` pour les routes
- `db/migrate` pour les migrations
- `config/database.yml` pour la base

## Commandes Rails importantes

```bash
bin/rails routes
bin/rails console
bin/rails generate model Post title:string
bin/rails db:migrate
bin/rails test
```

Si tu utilises RSpec, `bin/rails test` sera souvent remplace par `bundle exec rspec`.

## Reflexe de travail

- lancer le serveur avec `bin/rails s`
- verifier les routes avec `bin/rails routes`
- explorer les models dans `bin/rails console`
- versionner les migrations des qu'elles sont stables

## Comparaison Laravel

- `php artisan` devient `bin/rails`
- `.env` existe souvent aussi, mais Rails s'appuie plus sur `credentials` et les conventions config
- les generateurs Rails sont plus centraux dans le workflow

## Erreurs frequentes

- utiliser une mauvaise version Ruby
- oublier `bundle install`
- ne pas creer la base PostgreSQL
- confondre `rails` global et `bin/rails` du projet

## Ce que tu dois retenir

Travaille toujours avec `bin/rails`, une version Ruby controlee, et PostgreSQL. Un environnement propre t'evite la moitie des problemes de demarrage.
