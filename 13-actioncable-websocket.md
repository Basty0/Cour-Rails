# 13 - ActionCable et WebSocket

## Objectif

Comprendre comment Rails gère le temps réel pour des notifications, un chat ou des mises à jour live.

## Pourquoi utiliser du temps réel

Le temps réel permet de pousser une information du serveur vers le client sans attendre un nouveau rafraîchissement manuel.

Exemples :

- nouvelle notification
- nouveau message dans un chat
- changement de statut d'un traitement

## ActionCable

ActionCable est la couche WebSocket native de Rails.

Elle permet :

- une connexion persistante client/serveur
- l'abonnement à des canaux
- la diffusion d'événements

## Cas d'usage

- notifications en temps réel
- chat
- statut de traitement
- dashboard live

## Structure générale

Tu retrouves généralement :

- des channels
- des streams nommés
- des diffusions côté serveur

## Exemple conceptuel

```ruby
class NotificationsChannel < ApplicationCable::Channel
  def subscribed
    stream_from "notifications_#{current_user.id}"
  end
end
```

Puis :

```ruby
ActionCable.server.broadcast("notifications_1", { message: "Nouvelle alerte" })
```

### Explication

Le client s'abonne à un canal. Ensuite, le serveur peut pousser un message sur ce canal.

## Schéma mental du chat ou de la notification

1. le client s'abonne à un channel
2. le serveur diffuse un payload
3. le client met à jour son interface

## Règles d'architecture realtime

- garder un payload simple
- sécuriser la connexion
- déclencher la diffusion depuis une logique métier claire
- surveiller la charge

## Limites à connaître

- tous les projets n'ont pas besoin de WebSocket
- l'exploitation devient plus complexe
- il faut penser scalabilité et état des connexions

## Comparaison avec Laravel Reverb

- la promesse est similaire : temps réel intégré
- Rails bénéficie d'une solution native historique avec ActionCable
- le choix dépend ensuite de la charge, du front et de l'infrastructure

## Ce que tu dois retenir

Le temps réel doit répondre à un vrai besoin produit. Sinon, il ajoute surtout de la complexité technique et opérationnelle.
