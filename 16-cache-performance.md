# 16 - Cache Performance

## Objectif

Ameliorer les temps de reponse et la tenue en charge sans casser la coherence du code.

## Cache Rails

Rails fournit plusieurs couches de cache:

- fragment cache
- low-level cache
- cache store Redis ou autre

Dans une API, le plus utile est souvent le low-level cache et le cache de requetes ou de calculs couteux.

## Redis

Redis sert souvent a la fois pour:

- cache
- queue Sidekiq
- rate limiting selon l'architecture

## Eager loading

Premier levier de performance tres concret:

```ruby
Post.includes(:user, :comments)
```

## Optimisation SQL

- bons index
- pagination
- requetes plus simples
- selection des associations utiles seulement

## Bullet gem

Bullet detecte les N+1 et les eager loads inutiles pendant le developpement.

## Performance API

Verifier:

- temps controller
- temps SQL
- taille des payloads JSON
- nombre de requetes
- temps des services externes

## Puma

Puma est le serveur applicatif standard. Il faut regler:

- workers
- threads
- memoire disponible

## Sidekiq optimization

Un backend parait plus rapide quand les traitements lents sont bien deportes vers Sidekiq.

## Ce que tu dois retenir

La performance Rails ne commence pas par le cache. Elle commence par des requetes saines, des payloads maitrises et une bonne separation synchrone/asynchrone.
