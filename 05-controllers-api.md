# 05 - Controllers API

## Objectif

Construire des contrôleurs Rails lisibles, fins et centrés sur la couche HTTP.

## Le rôle d'un contrôleur

Un contrôleur reçoit la requête, lit les paramètres, appelle la logique utile, puis renvoie une réponse.

Un bon contrôleur ne doit pas devenir un gros bloc métier.

Il doit surtout :

- recevoir l'entrée HTTP
- faire une orchestration courte
- renvoyer un JSON propre

## Base d'un contrôleur API

```ruby
class Api::V1::PostsController < ApplicationController
  def index
    posts = Post.order(created_at: :desc)
    render json: posts
  end
end
```

### Explication

Dans cet exemple :

- la classe hérite de `ApplicationController`
- l'action `index` récupère les posts
- `render json:` renvoie la réponse au format JSON

## Actions CRUD

Les actions classiques sont :

- `index`
- `show`
- `create`
- `update`
- `destroy`

### Règle

Chaque action doit faire une chose claire. Si une action commence à contenir trop de branches, trop de validations ou trop de logique métier, elle doit être simplifiée.

## `params`

Rails centralise les paramètres dans `params`.

```ruby
params[:id]
params[:title]
```

### Explication

`params` contient les données provenant :

- de l'URL
- du body de la requête
- parfois de la query string

## Strong params

```ruby
def post_params
  params.require(:post).permit(:title, :body)
end
```

### Pourquoi c'est important

Les strong params servent à contrôler les champs autorisés.

C'est une règle de sécurité essentielle : on n'autorise pas automatiquement tout ce que le client envoie.

### Lecture détaillée

- `require(:post)` impose la présence de la clé `post`
- `permit(:title, :body)` autorise seulement ces champs

## `render json`

```ruby
render json: @post
render json: { error: "Not found" }, status: :not_found
```

### Explication

`render` fabrique la réponse HTTP. Dans une API, tu l'utiliseras très souvent avec :

- un payload JSON
- un code de statut HTTP

## Statuts HTTP

Rails accepte les symboles standards :

- `:ok`
- `:created`
- `:unprocessable_entity`
- `:not_found`
- `:no_content`

### Règle

Le statut HTTP doit correspondre au résultat réel de l'action. Une API propre ne renvoie pas toujours `200` par habitude.

## `before_action`

```ruby
before_action :set_post, only: [:show, :update, :destroy]
```

### Explication

`before_action` permet d'exécuter une méthode avant certaines actions.

Exemples d'usages :

- charger une ressource
- vérifier une authentification
- préparer un contexte commun

## `rescue_from`

```ruby
rescue_from ActiveRecord::RecordNotFound, with: :render_not_found
```

### Explication

`rescue_from` permet d'intercepter proprement certaines exceptions et de renvoyer une réponse API cohérente.

## Exemple de contrôleur propre

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

## Règles pour un contrôleur propre

- une action doit rester courte
- la logique métier lourde doit partir dans un service ou dans le domaine
- les erreurs doivent être cohérentes
- les statuts HTTP doivent être corrects
- les paramètres doivent être filtrés proprement

## Comparaison avec Laravel

- `FormRequest` n'a pas un équivalent strict natif, mais Rails permet de structurer proprement la validation et les paramètres
- les contrôleurs Rails sont souvent plus légers
- `rescue_from` remplace une partie de la gestion centralisée des exceptions

## Ce que tu dois retenir

Le contrôleur Rails n'est pas la maison de la logique métier. Il doit rester une couche de transport HTTP claire, propre et prévisible.
