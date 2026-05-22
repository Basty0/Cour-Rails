# 16 - Cache et performance

## Objectif

Améliorer les temps de réponse et la tenue en charge sans casser la cohérence du code.

## Premier principe

La performance Rails ne commence pas par le cache.

Elle commence par :

- des requêtes SQL saines
- des payloads JSON raisonnables
- une bonne séparation entre synchrone et asynchrone

## Cache Rails

Rails fournit plusieurs couches de cache :

- fragment cache
- low-level cache
- cache store Redis ou autre

Dans une API, le plus utile est souvent :

- le low-level cache
- le cache de calculs coûteux
- le cache de certaines lectures stables

## Redis

Redis sert souvent à la fois pour :

- le cache
- Sidekiq
- parfois du rate limiting ou des mécanismes d'état léger

## Eager loading

Premier levier de performance très concret :

```ruby
Post.includes(:user, :comments)
```

### Pourquoi

Avant de penser cache, il faut d'abord corriger les requêtes inutiles.

## Optimisation SQL

- bons index
- pagination
- requêtes plus simples
- sélection des associations utiles seulement

## Bullet gem

Bullet détecte :

- les N+1
- les eager loads inutiles

C'est un excellent outil de développement pour voir rapidement où l'application gaspille des requêtes.

## Performance API

Quand tu analyses une API, regarde :

- le temps contrôleur
- le temps SQL
- la taille des payloads JSON
- le nombre de requêtes
- le temps passé dans les services externes

## Puma

Puma est le serveur applicatif standard.

Il faut réfléchir à :

- la mémoire disponible
- le nombre de workers
- le nombre de threads

## Sidekiq et performance perçue

Un backend paraît plus rapide quand les traitements lents sont bien déplacés vers Sidekiq.

### Exemple

Au lieu de :

- envoyer un email dans la requête

tu peux :

- répondre vite
- lancer l'email en arrière-plan

## Ce que tu dois retenir

Le cache est utile, mais ce n'est pas le premier réflexe. Commence par des requêtes propres, une bonne architecture et des traitements asynchrones bien placés.
