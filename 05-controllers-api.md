# 05 - Controllers API

## Objectif

Construire des controllers Rails lisibles, fins et centres sur la couche HTTP.

## Base d'un controller API

```ruby
class Api::V1::PostsController < ApplicationController
  def index
    posts = Post.order(created_at: :desc)
    render json: posts
  end
end
```

## Actions CRUD

- `index`
- `show`
- `create`
- `update`
- `destroy`

Ces actions doivent rester courtes.

## params

Rails centralise les parametres dans `params`.

```ruby
params[:id]
params[:title]
```

Pour la securite, utilise les strong params:

```ruby
def post_params
  params.require(:post).permit(:title, :body)
end
```

## render json

```ruby
render json: @post
render json: { error: "Not found" }, status: :not_found
```

## Status HTTP

Rails accepte les symboles standards:

- `:ok`
- `:created`
- `:unprocessable_entity`
- `:not_found`
- `:no_content`

## before_action

```ruby
before_action :set_post, only: [:show, :update, :destroy]
```

Utile pour mutualiser la recherche de ressource ou l'authentification.

## rescue_from

```ruby
rescue_from ActiveRecord::RecordNotFound, with: :render_not_found
```

Tres pratique pour uniformiser les erreurs API.

## Architecture controller propre

Un bon controller:

- lit les params
- appelle un service ou un model
- renvoie un JSON stable
- ne contient pas 80 lignes de logique metier

## Exemple propre

```ruby
class Api::V1::PostsController < ApplicationController
  before_action :set_post, only: [:show, :update, :destroy]

  def create
    post = Post.new(post_params)

    if post.save
      render json: post, status: :created
    else
      render json: { errors: post.errors.full_messages }, status: :unprocessable_entity
    end
  end

  private

  def set_post
    @post = Post.find(params[:id])
  end

  def post_params
    params.require(:post).permit(:title, :body)
  end
end
```

## Comparaison Laravel

- `FormRequest` n'a pas d'equivalent strict natif, mais on peut structurer validation et params autrement
- les controllers Rails sont souvent plus legers
- `rescue_from` remplace une partie de la gestion centralisee d'exceptions

## Ce que tu dois retenir

Le controller Rails n'est pas la maison de la logique metier. Il doit rester une couche de transport HTTP elegante.
