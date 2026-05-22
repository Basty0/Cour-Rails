# 13 - ActionCable WebSocket

## Objectif

Comprendre comment Rails gere le temps reel pour des notifications, un chat ou des mises a jour live.

## ActionCable

ActionCable est la couche WebSocket native de Rails.

Elle permet:

- connexion persistante client/serveur
- abonnement a des canaux
- diffusion d'evenements

## Cas d'usage

- notifications temps reel
- chat
- statut de traitement
- dashboard live

## Structure generale

- channels
- stream nommes
- diffusion depuis le serveur

## Exemple conceptuel

```ruby
class NotificationsChannel < ApplicationCable::Channel
  def subscribed
    stream_from "notifications_#{current_user.id}"
  end
end
```

Puis:

```ruby
ActionCable.server.broadcast("notifications_1", { message: "Nouvelle alerte" })
```

## Chat

Le schema mental:

1. le client s'abonne a un channel
2. le serveur diffuse un payload
3. le client met a jour son interface

## Architecture realtime

Pour rester propre:

- payload simple
- auth de connexion claire
- diffusion declenchee depuis le domaine metier
- monitoring de charge

## Comparaison Laravel Reverb

- meme promesse: temps reel integre
- Rails profite d'une integration native historique avec ActionCable
- le choix depend ensuite de la charge, de l'ecosysteme et de l'architecture front

## Limites a connaitre

- tous les projets n'ont pas besoin de WebSocket
- la complexite d'exploitation augmente
- il faut penser scalabilite et state des connexions

## Ce que tu dois retenir

Le temps reel doit repondre a un vrai besoin produit. Sinon, il ajoute surtout de la complexite operationnelle.
