# 04 - Routing API

## Objectif

Savoir exposer une API propre avec des routes lisibles, versionnees et maintenables.

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

## resources

Rails fournit un DSL tres puissant:

```ruby
resources :posts
```

Cela genere les routes CRUD standards.

## Namespace API

```ruby
namespace :api do
  namespace :v1 do
    resources :posts
  end
end
```

Le controller associe sera `Api::V1::PostsController`.

## Versioning API

Le versioning par namespace est le plus simple au debut:

- `/api/v1/posts`
- `/api/v2/posts`

Il permet de faire evoluer l'API sans casser les clients existants.

## Nested routes

```ruby
resources :posts do
  resources :comments, only: [:index, :create]
end
```

A utiliser quand la relation est vraiment forte.

## Constraints

Tu peux filtrer selon l'host, le format ou des regles custom:

```ruby
constraints format: :json do
  resources :posts
end
```

## Bonnes pratiques

- garder les routes courtes
- eviter les routes RPC si une ressource REST suffit
- versionner des le debut
- limiter les nested routes profondes

## Comparaison Laravel

- `Route::apiResource()` ressemble a `resources`
- Rails concentre plus la logique de structure dans le DSL
- le couplage nommage route/controller/module est plus fort

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

Le routeur Rails doit raconter l'API avec un minimum de bruit. Si tes routes deviennent difficiles a lire, ton design HTTP est probablement en train de se degrader.
