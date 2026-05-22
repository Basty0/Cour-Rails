# 11 - Services Business Logic

## Objectif

Sortir la logique metier complexe des controllers pour garder une application lisible et scalable.

## Pourquoi `app/services`

Quand une action:

- fait plusieurs ecritures
- appelle des dependances externes
- contient des regles metier complexes

elle doit souvent sortir du controller.

## Exemple simple

```ruby
class PublishPost
  def initialize(post:)
    @post = post
  end

  def call
    @post.update!(published: true, published_at: Time.current)
  end
end
```

## Controller plus propre

```ruby
def publish
  authorize @post
  PublishPost.new(post: @post).call
  render json: @post
end
```

## Separation de logique metier

Un service doit exprimer une intention metier:

- `CreateOrder`
- `ChargeInvoice`
- `InviteUser`

Pas juste `UserService`.

## Transactions

```ruby
ApplicationRecord.transaction do
  order.save!
  payment.save!
  stock.save!
end
```

Des qu'il y a plusieurs ecritures dependantes, pense transaction.

## Architecture scalable

Une structure frequente:

- models pour la persistence
- services pour les use cases
- policies pour l'acces
- serializers pour la sortie

## Organisation projet enterprise

Si l'application grossit, tu peux ajouter:

- `app/queries`
- `app/forms`
- `app/interactors`
- `app/validators`

Mais pas trop tot.

## Comparaison Laravel

- equivalent aux Actions, Services ou Use Cases d'une architecture Laravel propre
- meme principe: nommer des operations metier plutot que gonfler les controllers

## Ce que tu dois retenir

Les services ne sont pas obligatoires partout. Ils deviennent utiles quand ils rendent le code plus clair que le controller ou le model.
