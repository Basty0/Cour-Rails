# 11 - Services et logique métier

## Objectif

Sortir la logique métier complexe des contrôleurs pour garder une application lisible, testable et capable de grandir.

## Pourquoi utiliser des services

Quand une action :

- effectue plusieurs écritures
- appelle des dépendances externes
- contient des règles métier complexes
- doit être réutilisée ailleurs

elle mérite souvent de sortir du contrôleur.

## Pourquoi ce n'est pas automatique

Il ne faut pas mettre toute logique dans `app/services` par réflexe.

La bonne règle est :

- si le service rend le code plus clair, il est utile
- s'il ajoute juste une couche vide, il complique inutilement

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

### Explication

Le service exprime ici une intention métier claire : publier un post.

Ce nom vaut mieux que :

- `PostService`
- `CommonService`
- `UtilityService`

## Contrôleur plus propre

```ruby
def publish
  authorize @post
  PublishPost.new(post: @post).call
  render json: @post
end
```

### Pourquoi c'est mieux

Le contrôleur reste centré sur :

- l'autorisation
- l'orchestration
- la réponse HTTP

La vraie règle métier est déplacée dans un objet dédié.

## Séparation de logique métier

Un service doit exprimer une intention métier comme :

- `CreateOrder`
- `ChargeInvoice`
- `InviteUser`

### Règle de nommage

Un bon nom de service décrit une action métier. Il ne doit pas être vague.

## Transactions

```ruby
ApplicationRecord.transaction do
  order.save!
  payment.save!
  stock.save!
end
```

### Explication

Une transaction garantit que plusieurs écritures liées réussissent ensemble ou échouent ensemble.

### Quand l'utiliser

Dès qu'il y a plusieurs modifications dépendantes, pense transaction.

## Architecture scalable

Une structure fréquente :

- modèles pour la persistance
- services pour les use cases
- policies pour l'accès
- serializers pour la sortie

## Organisation d'un projet plus grand

Si l'application grossit, tu peux ajouter :

- `app/queries`
- `app/forms`
- `app/interactors`
- `app/validators`

### Règle

Ne crée pas ces couches trop tôt. Ajoute-les seulement si elles résolvent une vraie douleur.

## Comparaison avec Laravel

- c'est proche des Actions, Services ou Use Cases dans une architecture Laravel propre
- le principe est le même : éviter des contrôleurs énormes et mieux nommer la logique métier

## Ce que tu dois retenir

Les services ne sont pas obligatoires partout. Ils deviennent précieux quand ils rendent l'intention plus claire, la logique plus testable et le code plus facile à faire évoluer.
