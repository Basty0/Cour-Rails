# 12 - Background Jobs Queues

## Objectif

Executer les taches lentes hors du cycle HTTP pour garder une API rapide.

## ActiveJob

ActiveJob est l'interface standard des jobs Rails.

```ruby
class SendWelcomeEmailJob < ApplicationJob
  queue_as :default

  def perform(user_id)
    user = User.find(user_id)
    UserMailer.welcome(user).deliver_now
  end
end
```

## Sidekiq

Pour la production, Sidekiq est une reference frequente:

- robuste
- rapide
- bien integre a Redis

## Redis

Redis sert de backend de queue pour Sidekiq dans la plupart des setups.

## Jobs async

```ruby
SendWelcomeEmailJob.perform_later(user.id)
```

Le job est planifie sans bloquer la reponse HTTP.

## Cas typiques

- envoi d'email
- generation de PDF
- import CSV
- webhooks
- traitement d'image

## Retry

Une bonne queue doit gerer les echecs temporaires. Sidekiq offre des retries automatiques tres utiles.

## Scheduling

Tu peux planifier:

- nettoyage
- synchronisations
- relances

Avec Sidekiq, cron jobs ou outils complementaires.

## Architecture queue

Bon reflexe:

- jobs petits
- payload minimal
- id plutot qu'objet complet
- idempotence si possible

## Comparaison Laravel

- `ShouldQueue` et les jobs Laravel sont tres proches en idee
- Rails se repose sur ActiveJob comme facade commune

## Ce que tu dois retenir

Ce qui est lent, fragile ou non critique pour la reponse HTTP doit sortir vers une queue. La performance percue d'une API depend beaucoup de cette discipline.
