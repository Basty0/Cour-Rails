# 06 - ActiveRecord Models

## Objectif

Maitriser ActiveRecord pour manipuler les donnees proprement sans tomber dans les requetes inutiles.

## ActiveRecord

ActiveRecord est l'ORM de Rails. Il combine representation objet, requetes SQL et conventions de persistence.

## CRUD

```ruby
post = Post.create(title: "Hello", body: "World")
post.update(title: "Updated")
post.destroy
```

## Requetes essentielles

```ruby
Post.find(1)
Post.where(published: true)
Post.order(created_at: :desc)
Post.limit(10)
```

Ces appels retournent souvent une relation chainable.

## Scopes

```ruby
scope :published, -> { where(published: true) }
scope :recent, -> { order(created_at: :desc) }
```

Un scope doit rester simple et lisible.

## Validations

```ruby
validates :title, presence: true
validates :slug, uniqueness: true
```

Les validations protegent le domaine, mais ne remplacent pas les contraintes SQL.

## Callbacks

```ruby
before_validation :generate_slug
after_create :send_notification
```

Utiles avec moderation. Trop de callbacks rendent les effets de bord invisibles.

## Relations

```ruby
class Post < ApplicationRecord
  belongs_to :user
  has_many :comments, dependent: :destroy
end
```

## Eager loading

```ruby
Post.includes(:user, :comments)
```

Indispensable pour eviter les requetes multiples.

## N+1

Probleme classique:

```ruby
posts = Post.all
posts.each { |post| puts post.user.name }
```

Si chaque `post.user` declenche une requete, tu as un N+1.

## Optimisation de requetes

- utiliser `includes`
- selectionner moins de colonnes si necessaire
- paginer
- analyser les logs SQL
- ajouter les bons index

## ActiveRecord vs Eloquent

- les deux sont tres productifs
- ActiveRecord est plus central dans l'identite Rails
- Eloquent semble souvent plus "explicite", ActiveRecord plus "naturel" dans l'ecosysteme Rails

## Ce que tu dois retenir

ActiveRecord est puissant, mais il faut surveiller les relations, les callbacks et les requetes implicites. La vraie competence n'est pas le CRUD, c'est la maitrise du cout SQL.
