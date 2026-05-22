# 03 - Ruby Les Bases Pour Developpeur Laravel

## Objectif

Apprendre uniquement le Ruby utile pour lire et ecrire du Rails sans douleur.

## Syntaxe Ruby

Ruby est plus concis que PHP sur beaucoup de points:

```ruby
name = "Mora"
puts name
```

Pas de point-virgule obligatoire. Peu de bruit syntaxique.

## Variables

```ruby
name = "Rails"
version = 8
api_only = true
```

Ruby est dynamiquement type.

## Methodes

```ruby
def full_name(first_name, last_name)
  "#{first_name} #{last_name}"
end
```

Le dernier element retourne implicitement la valeur.

## Classes

```ruby
class User
  def admin?
    true
  end
end
```

## Modules

Les modules servent a partager du comportement ou a organiser le code.

```ruby
module Sluggable
  def slug
    name.downcase.gsub(" ", "-")
  end
end
```

## Blocks

Les blocks sont partout en Ruby:

```ruby
[1, 2, 3].each do |number|
  puts number
end
```

Pense-les comme des closures tres naturelles.

## Symbols

```ruby
:name
:email
```

Un symbol est une etiquette immuable tres utilisee pour les cles et options.

## Arrays et Hashes

```ruby
tags = ["api", "rails"]
user = { name: "Mora", role: "admin" }
```

Le hash Ruby moderne ressemble beaucoup a un tableau associatif elegant.

## Heritage

```ruby
class ApplicationController < ActionController::API
end
```

Rails utilise l'heritage partout.

## Differences PHP vs Ruby

- Ruby lit plus comme une DSL.
- Les parentheses sont souvent optionnelles.
- Les methodes finissent parfois par `?` ou `!`.
- Tout est vraiment objet ou presque.

## Syntaxes Rails importantes

```ruby
before_action :authenticate_user!
render json: @post, status: :created
params.require(:post).permit(:title, :body)
has_many :comments
scope :published, -> { where(published: true) }
```

## Ce que tu dois retenir

Tu n'as pas besoin de devenir expert Ruby avant Rails. Tu dois surtout reconnaitre rapidement la syntaxe, les blocks, les symbols et le style expressif du framework.

## Exercice

Traduis mentalement ces idees Laravel en Ruby:

- collection `map`
- methode de model
- relation `hasMany`
- callback avant sauvegarde
