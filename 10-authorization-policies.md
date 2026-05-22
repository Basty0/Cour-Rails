# 10 - Authorization et policies

## Objectif

Contrôler qui peut faire quoi dans l'API sans mélanger sécurité, règles d'accès et logique métier.

## Authentification vs autorisation

Il faut bien distinguer les deux notions :

- l'authentification répond à "qui es-tu ?"
- l'autorisation répond à "as-tu le droit de faire cela ?"

Tu peux être authentifié et ne pas avoir le droit de modifier une ressource.

## Pundit

Pundit est la solution la plus courante pour l'autorisation dans Rails.

Il repose sur :

- une policy par ressource
- des méthodes comme `show?`, `update?`, `destroy?`
- des scopes pour filtrer ce qui est visible

## Exemple de policy

```ruby
class PostPolicy < ApplicationPolicy
  def update?
    user.admin? || record.user_id == user.id
  end
end
```

### Explication

Ici, la règle est simple :

- un administrateur peut modifier
- le propriétaire du post peut modifier
- les autres ne peuvent pas

## Utilisation dans le contrôleur

```ruby
def update
  authorize @post
  @post.update!(post_params)
  render json: @post
end
```

### Explication

`authorize @post` demande à Pundit de vérifier la policy correspondant à l'action en cours.

## Rôles et permissions

Structure simple et saine :

- `user`
- `manager`
- `admin`

### Règle

Évite de disperser les vérifications de rôle partout dans les contrôleurs. Les règles doivent rester centralisées.

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

### Explication

Le scope décide quelles ressources l'utilisateur a le droit de voir dans une liste.

C'est essentiel pour sécuriser les endpoints d'index.

## Sécurité des endpoints

Vérifie toujours :

- l'accès à la ressource
- la portée des listes
- les actions sensibles
- les endpoints d'administration

## Bonnes pratiques

- toujours autoriser explicitement
- tester les policies
- centraliser les règles
- éviter les `if role == ...` dispersés partout

## Comparaison avec Laravel

- conceptuellement, c'est très proche des Policies Laravel
- la logique est familière si tu viens de Laravel
- la discipline reste la même : ne pas laisser les règles d'accès se répandre dans tout le code

## Ce que tu dois retenir

Une API propre se sécurise avec une couche d'autorisation explicite. Les policies rendent l'intention lisible, centralisée et testable.
