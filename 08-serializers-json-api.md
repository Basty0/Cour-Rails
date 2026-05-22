# 08 - Serializers JSON API

## Objectif

Produire des reponses JSON propres, stables et predictibles.

## render json

Le plus simple:

```ruby
render json: @post
```

Mais pour une API serieuse, il faut rapidement controler la forme de sortie.

## Pourquoi serialiser

- eviter d'exposer des colonnes internes
- stabiliser le contrat API
- ajouter des meta et relations
- versionner plus facilement

## ActiveModelSerializers

Approche classique:

```ruby
class PostSerializer < ActiveModel::Serializer
  attributes :id, :title, :body, :created_at
end
```

## Blueprinter

Blueprinter est souvent apprecie pour sa simplicite et sa vitesse:

```ruby
class PostBlueprint < Blueprinter::Base
  identifier :id
  fields :title, :body
end
```

## Structure de reponse conseillee

```json
{
  "data": {
    "id": 1,
    "title": "Hello"
  },
  "meta": {
    "request_id": "abc-123"
  }
}
```

## Pagination metadata

Une liste paginee doit exposer au minimum:

- page courante
- total pages
- total items
- taille de page

## Erreurs API

Evite les erreurs vagues.

Structure utile:

```json
{
  "errors": [
    { "field": "title", "message": "can't be blank" }
  ]
}
```

## Bonnes pratiques JSON

- garder une structure consistente
- choisir un style de cles et le conserver
- ne pas melanger payload metier et erreurs
- eviter de serializer des objets trop profonds

## Comparaison Laravel

- equivalent conceptuel des API Resources
- meme besoin de stabiliser le contrat HTTP
- en Rails, beaucoup d'equipes utilisent soit serializers, soit presenters, soit builders maison

## Ce que tu dois retenir

Le JSON n'est pas un detail de sortie. C'est ton contrat produit. Plus il est stable, plus ton API est facile a faire evoluer.
