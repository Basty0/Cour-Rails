# 12 - Background jobs et files d'attente

## Objectif

Exécuter les tâches lentes hors du cycle HTTP pour garder une API rapide et agréable à utiliser.

## Pourquoi sortir certaines tâches de la requête

Une requête HTTP doit idéalement répondre vite.

Si tu fais dans la requête :

- un envoi d'email
- un traitement d'image
- un appel externe lent
- une génération de document

tu risques de ralentir inutilement l'expérience utilisateur.

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

### Explication

Un job représente une tâche différée.

Ici :

- le job reçoit l'identifiant d'un utilisateur
- il recharge l'utilisateur
- il envoie un email de bienvenue

## Pourquoi passer l'ID et non l'objet

Bonne règle :

- passer un identifiant
- recharger la donnée dans le job

Cela évite de transporter un objet potentiellement périmé ou lourd.

## Sidekiq

En production, Sidekiq est une référence fréquente.

Il est apprécié pour :

- sa robustesse
- sa rapidité
- sa bonne intégration avec Redis

## Redis

Redis sert souvent de backend de queue pour Sidekiq.

Il stocke les jobs en attente et permet leur traitement asynchrone.

## Jobs asynchrones

```ruby
SendWelcomeEmailJob.perform_later(user.id)
```

### Explication

`perform_later` planifie le job sans bloquer la réponse HTTP.

Le client reçoit donc une réponse plus rapidement.

## Cas typiques

- envoi d'email
- génération de PDF
- import CSV
- traitement d'image
- webhooks

## Retry

Une bonne file d'attente doit gérer les échecs temporaires.

Sidekiq offre des retries automatiques très utiles si :

- un service externe répond mal
- un timeout survient
- une ressource n'est pas encore disponible

## Scheduling

Tu peux planifier :

- du nettoyage
- des synchronisations
- des relances

Cela peut se faire avec Sidekiq et des outils complémentaires de planification.

## Règles d'architecture

- faire des jobs petits
- garder un payload minimal
- passer des IDs plutôt que des objets complets
- viser l'idempotence quand c'est possible

### Que veut dire "idempotent"

Un job idempotent peut être rejoué sans créer de dégâts fonctionnels.

C'est très important quand un retry automatique se produit.

## Comparaison avec Laravel

- `ShouldQueue` et les jobs Laravel sont très proches dans l'idée
- Rails se repose sur ActiveJob comme interface commune
- Sidekiq joue souvent un rôle comparable à l'outillage queue sérieux côté production

## Ce que tu dois retenir

Ce qui est lent, fragile ou non critique pour la réponse HTTP doit souvent partir dans une file d'attente. Une API perçue comme rapide dépend énormément de cette discipline.
