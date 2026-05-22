# 23 - Roadmap d'apprentissage

## Objectif

Savoir dans quel ordre progresser pour devenir solide en Rails API en venant de Laravel.

## Ordre recommandé

1. Comprendre la philosophie Rails.
2. Installer correctement l'environnement.
3. Apprendre le Ruby utile.
4. Maîtriser routing, contrôleurs et ActiveRecord.
5. Travailler les migrations et la base.
6. Stabiliser les réponses JSON.
7. Ajouter auth et authorization.
8. Structurer la logique métier.
9. Ajouter tests, jobs et performance.
10. Finir par un projet complet.

## Ce qu'il faut maîtriser en premier

- `config/routes.rb`
- `ApplicationController`
- `params.require(...).permit(...)`
- ActiveRecord CRUD + relations
- migrations + schéma

## Erreurs fréquentes

- vouloir coder du Laravel en Ruby
- trop abstraire trop tôt
- ignorer les conventions Rails
- ne pas surveiller les requêtes SQL
- ne pas tester les endpoints critiques

## Bonnes pratiques Rails

- utiliser des noms clairs et conventionnels
- garder les contrôleurs fins
- laisser les modèles et services porter les intentions
- rester cohérent sur les payloads JSON
- sécuriser tôt avec policies et auth

## Ressources à poursuivre

- les guides officiels Rails
- la documentation des gems majeures
- le code de vraies applications Rails
- des exercices de refactor et de tests

## Roadmap senior Rails API

Pour passer au niveau suivant :

- maîtriser la performance SQL
- comprendre Sidekiq en production
- structurer une application large
- savoir déployer et monitorer
- modéliser proprement le domaine métier

## Stack moderne Rails 2026

Une stack pragmatique peut ressembler à :

- Rails API
- PostgreSQL
- Redis
- Sidekiq
- Devise ou une auth adaptée
- Pundit
- Blueprinter
- RSpec
- Sentry
- Render, Railway ou VPS selon le besoin

## Conclusion

Si tu suis ce parcours dans l'ordre et que tu pratiques sur un vrai projet, tu peux devenir rapidement opérationnel sur Rails API. La clé est simple : respecter les conventions, pratiquer régulièrement, puis monter progressivement en architecture.
