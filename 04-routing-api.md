# 04 - Routing API

## Objectif

Savoir exposer une API propre avec des routes lisibles, versionnées et maintenables.

## Le rôle du routing

Le routing sert à faire correspondre une requête HTTP à une action précise dans ton application.

Autrement dit, le routeur répond à la question :

"Quand un client appelle telle URL avec tel verbe HTTP, quel contrôleur et quelle action doivent être exécutés ?"

## Fichier central

Toutes les routes passent par `config/routes.rb`.

```ruby
Rails.application.routes.draw do
end
```

## Verbes HTTP

```ruby
get "/posts", to: "posts#index"
post "/posts", to: "posts#create"
patch "/posts/:id", to: "posts#update"
delete "/posts/:id", to: "posts#destroy"
```

### Explication

Chaque ligne associe :

- un verbe HTTP
- une URL
- une action de contrôleur

Exemples :

- `get` lit une ressource
- `post` crée une ressource
- `patch` modifie une ressource
- `delete` supprime une ressource

## `resources`

Rails fournit une DSL très pratique :

```ruby
resources :posts
```

### Ce que Rails génère

Cette ligne crée automatiquement les routes CRUD principales :

- `index`
- `show`
- `create`
- `update`
- `destroy`

### Règle d'usage

Utilise `resources` dès qu'une ressource suit une logique REST classique. Cela rend le code plus court et plus standard.

## Namespace API

```ruby
namespace :api do
  namespace :v1 do
    resources :posts
  end
end
```

### Explication

Cette structure permet d'obtenir des URLs comme :

- `/api/v1/posts`

Le contrôleur attendu devient alors :

- `Api::V1::PostsController`

## Versioning API

Versionner l'API dès le départ est une bonne discipline.

Pourquoi :

- éviter de casser les clients existants
- faire évoluer l'API proprement
- introduire de nouveaux contrats sans rupture brutale

## Nested routes

```ruby
resources :posts do
  resources :comments, only: [:index, :create]
end
```

### Explication

Ici, les commentaires sont exposés dans le contexte d'un post.

Exemples :

- `/posts/1/comments`

### Règle

Une route imbriquée doit exprimer une vraie relation forte. Si tu imbriques trop profondément, l'API devient plus difficile à lire et à maintenir.

## Constraints

Tu peux ajouter des contraintes sur certains groupes de routes.

```ruby
constraints format: :json do
  resources :posts
end
```

### À quoi ça sert

Les contraintes permettent de limiter ou filtrer certaines routes selon :

- le format
- le host
- des règles personnalisées

## Bonnes pratiques

- garder les routes courtes
- privilégier les ressources REST
- versionner l'API dès le début
- éviter les nested routes trop profondes
- garder le fichier `routes.rb` lisible

## Comparaison avec Laravel

- `Route::apiResource()` ressemble beaucoup à `resources`
- Rails concentre davantage la structure dans son DSL de routing
- le lien entre nom de route, namespace et contrôleur est très fort

## Exemple de routes propres

```ruby
Rails.application.routes.draw do
  namespace :api do
    namespace :v1 do
      resources :users, only: [:index, :show]
      resources :posts do
        resources :comments, only: [:index, :create]
      end
    end
  end
end
```

## Ce que tu dois retenir

Le routeur Rails doit raconter ton API clairement. Si ton fichier de routes devient confus, c'est souvent le signe que la structure HTTP de ton application doit être repensée.
