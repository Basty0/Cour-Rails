# 10 - Authorization Policies

## Objectif

Controler qui peut faire quoi dans l'API sans melanger securite et logique metier.

## Pundit

Pundit est la solution la plus courante pour l'autorisation Rails.

Il repose sur:

- une policy par ressource
- des methodes comme `show?`, `update?`, `destroy?`
- des scopes pour filtrer ce qui est visible

## Exemple de policy

```ruby
class PostPolicy < ApplicationPolicy
  def update?
    user.admin? || record.user_id == user.id
  end
end
```

## Utilisation controller

```ruby
def update
  authorize @post
  @post.update!(post_params)
  render json: @post
end
```

## Roles et permissions

Structure simple et saine:

- `user`
- `manager`
- `admin`

Evite de disperser les checks de role partout dans les controllers.

## Policy scopes

```ruby
class PostPolicy < ApplicationPolicy
  class Scope < Scope
    def resolve
      user.admin? ? scope.all : scope.where(user_id: user.id)
    end
  end
end
```

Tres utile pour securiser les listes.

## Securite des endpoints

Verifier:

- acces a la ressource
- portee des listes
- actions sensibles
- admin endpoints

## Comparaison Laravel

- conceptuellement proche des Policies Laravel
- integration tres directe
- impose une discipline utile si l'equipe la respecte partout

## Bonnes pratiques

- toujours autoriser explicitement
- tester les policies
- centraliser les regles
- ne pas cacher l'autorisation dans des if disperses

## Ce que tu dois retenir

Une API propre se securise en couche explicite. Les policies rendent l'intention lisible et testable.
