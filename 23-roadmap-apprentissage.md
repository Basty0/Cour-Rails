# 23 - Roadmap Apprentissage

## Objectif

Savoir dans quel ordre progresser pour devenir solide en Rails API en venant de Laravel.

## Ordre recommande

1. Comprendre la philosophie Rails.
2. Installer correctement l'environnement.
3. Apprendre le Ruby utile.
4. Maitriser routing, controllers et ActiveRecord.
5. Travailler les migrations et la base.
6. Stabiliser les reponses JSON.
7. Ajouter auth et authorization.
8. Structurer la logique metier.
9. Ajouter tests, jobs et performance.
10. Finir par un projet complet.

## Ce qu'il faut maitriser en premier

- `config/routes.rb`
- `ApplicationController`
- `params.require(...).permit(...)`
- ActiveRecord CRUD + relations
- migrations + schema

## Erreurs frequentes

- vouloir coder du Laravel en Ruby
- trop abstraire trop tot
- ignorer les conventions Rails
- ne pas surveiller les requetes SQL
- ne pas tester les endpoints critiques

## Bonnes pratiques Rails

- utiliser des noms clairs et conventionnels
- garder les controllers fins
- laisser les models et services porter les intentions
- rester coherent sur les payloads JSON
- securiser tot avec policies et auth

## Ressources a poursuivre

- guides officiels Rails
- documentation des gems majeures
- code de vraies applications Rails
- exercices de refactor et tests

## Roadmap senior Rails API

Pour passer au niveau suivant:

- maitriser performance SQL
- comprendre Sidekiq en production
- structurer une app large
- savoir deployer et monitorer
- modeler proprement le domaine metier

## Stack moderne Rails 2026

Une stack pragmatique peut ressembler a:

- Rails API
- PostgreSQL
- Redis
- Sidekiq
- Devise ou auth adaptee
- Pundit
- Blueprinter
- RSpec
- Sentry
- Render, Railway ou infra VPS selon le besoin

## Conclusion

Si tu suis ce parcours dans l'ordre, tu peux rapidement devenir operationnel sur Rails API. La cle est simple: respecter la convention, pratiquer sur un vrai projet, puis monter progressivement en architecture.
