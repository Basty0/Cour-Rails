# 08 - Serializers et JSON API

## Objectif

Produire des réponses JSON propres, stables, lisibles et adaptées à une vraie API moderne.

## Pourquoi la sortie JSON est importante

Dans une API, le JSON n'est pas un détail d'affichage.

C'est le contrat entre :

- ton backend
- ton frontend
- tes clients mobiles
- d'autres services externes

Si ce contrat change sans discipline, l'API devient difficile à maintenir.

## `render json`

Le plus simple :

```ruby
render json: @post
```

### Limite de cette approche

Pour un petit test, cela suffit. Pour une API sérieuse, il faut rapidement contrôler :

- les champs exposés
- la structure de la réponse
- les relations incluses
- les métadonnées

## Pourquoi sérialiser

- éviter d'exposer des colonnes internes
- stabiliser le contrat API
- ajouter des métadonnées
- contrôler précisément la forme des payloads
- préparer l'évolution future de l'API

## ActiveModelSerializers

Approche classique :

```ruby
class PostSerializer < ActiveModel::Serializer
  attributes :id, :title, :body, :created_at
end
```

### Explication

Le serializer sert d'intermédiaire entre le modèle Ruby et la réponse JSON envoyée au client.

## Blueprinter

Blueprinter est souvent apprécié pour sa simplicité et sa rapidité.

```ruby
class PostBlueprint < Blueprinter::Base
  identifier :id
  fields :title, :body
end
```

### Pourquoi certaines équipes l'aiment

- syntaxe directe
- bon contrôle sur la sortie
- sensation de légèreté

## Structure de réponse conseillée

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

### Explication

Une structure propre sépare :

- les données métier
- les métadonnées
- les erreurs éventuelles

Cela rend l'API plus lisible et plus stable.

## Métadonnées de pagination

Une liste paginée doit exposer au minimum :

- la page courante
- le nombre total de pages
- le nombre total d'éléments
- la taille de page

### Pourquoi

Le client doit pouvoir comprendre comment naviguer dans les résultats sans deviner.

## Erreurs API

Évite les erreurs vagues.

Structure utile :

```json
{
  "errors": [
    { "field": "title", "message": "can't be blank" }
  ]
}
```

### Règle

Une erreur API doit être :

- claire
- cohérente
- exploitable côté client

## Bonnes pratiques JSON

- garder une structure cohérente
- choisir un style de clés et le conserver
- ne pas mélanger payload métier et erreurs
- éviter de sérialiser des objets trop profonds
- renvoyer uniquement ce qui est utile au client

## Comparaison avec Laravel

- l'équivalent conceptuel le plus proche est l'API Resource
- le besoin est le même : contrôler le contrat HTTP
- en Rails, certaines équipes utilisent des serializers, d'autres des presenters ou des builders maison

## Ce que tu dois retenir

Le JSON de sortie doit être pensé comme un contrat produit. Plus il est stable, plus ton API devient fiable, prévisible et agréable à faire évoluer.
