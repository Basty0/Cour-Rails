# 03 - Ruby : les bases pour développeur Laravel

## Objectif

Apprendre le Ruby réellement utile pour lire et écrire du Rails sans blocage.

L'idée n'est pas de devenir expert Ruby avant de toucher Rails. L'objectif est d'acquérir les bases qui te permettent de comprendre les fichiers du framework, les modèles, les contrôleurs, les callbacks et les relations.

## Comment lire ce chapitre

Pour chaque notion, pose-toi trois questions :

- qu'est-ce que c'est
- à quoi ça sert dans Rails
- quelles règles faut-il respecter

## Syntaxe Ruby

Ruby est plus concis que PHP sur beaucoup de points.

```ruby
name = "Mora"
puts name
```

### Explication

Dans cet exemple :

- `name` est une variable
- `"Mora"` est une chaîne de caractères
- `puts` affiche une valeur dans la console

Ruby supprime beaucoup de bruit syntaxique. Il n'impose pas de point-virgule à la fin des lignes et les parenthèses sont souvent facultatives.

### Règle à retenir

En Ruby, le code cherche à être lisible. Quand deux écritures sont possibles, on choisit généralement la plus claire.

## Variables

```ruby
name = "Rails"
version = 8
api_only = true
```

### Qu'est-ce qu'une variable

Une variable est un nom qui permet de stocker une valeur pour la réutiliser plus tard.

Dans l'exemple :

- `name` contient une chaîne
- `version` contient un nombre
- `api_only` contient un booléen

### À quoi sert une variable

Une variable sert à :

- mémoriser une information
- rendre le code plus lisible
- éviter de répéter une même valeur
- transmettre une donnée entre plusieurs lignes de code

### Comment Ruby gère les variables

Ruby est un langage dynamiquement typé. Cela veut dire que tu n'écris pas le type de la variable au moment de la déclaration.

Exemple :

```ruby
count = 10
count = "dix"
```

Techniquement, Ruby l'autorise. En pratique, il faut éviter ce genre de confusion dans un vrai projet.

### Règles de base sur les variables

- donner un nom clair à la variable
- éviter les noms trop courts comme `x`, `tmp`, `a`
- ne pas réutiliser une variable pour changer complètement son sens
- garder une variable proche de l'endroit où elle est utilisée

### Mauvais exemple

```ruby
a = "Rails"
```

Ici, on ne comprend pas ce que représente `a`.

### Bon exemple

```ruby
framework_name = "Rails"
```

Le rôle de la donnée est immédiatement compréhensible.

## Méthodes

```ruby
def full_name(first_name, last_name)
  "#{first_name} #{last_name}"
end
```

### Explication

Une méthode regroupe une action ou un calcul réutilisable.

Ici :

- `full_name` est le nom de la méthode
- `first_name` et `last_name` sont des paramètres
- la dernière ligne est renvoyée automatiquement

### Règle importante

En Ruby, la dernière expression d'une méthode devient sa valeur de retour si aucun `return` explicite n'est utilisé.

### Quand créer une méthode

Tu crées une méthode quand :

- un bloc de logique doit être réutilisé
- un nom peut clarifier une intention
- tu veux éviter de répéter du code

## Classes

```ruby
class User
  def admin?
    true
  end
end
```

### Explication

Une classe sert à définir la structure et le comportement d'un objet.

Dans Rails :

- les modèles sont des classes
- les contrôleurs sont des classes
- les jobs sont des classes

### Règle à retenir

En Ruby et en Rails, tout repose énormément sur les classes. Il faut donc comprendre qu'une classe n'est pas juste un fichier : c'est une définition de comportement.

## Modules

Les modules servent à organiser le code ou à partager un comportement entre plusieurs classes.

```ruby
module Sluggable
  def slug
    name.downcase.gsub(" ", "-")
  end
end
```

### Explication

Ici, le module fournit une méthode `slug` qui transforme un nom en version URL-friendly.

### Quand utiliser un module

- pour partager une logique réutilisable
- pour regrouper du code par namespace
- pour éviter certaines duplications entre classes

### Règle

Un module doit rester clair et ciblé. Si tu y mets trop de responsabilités, tu crées juste un autre endroit confus.

## Blocks

Les blocks sont partout en Ruby.

```ruby
[1, 2, 3].each do |number|
  puts number
end
```

### Explication

Le block est le morceau de code transmis à la méthode `each`.

Ici, Ruby dit :

- prends chaque élément du tableau
- place-le dans `number`
- exécute le code du block

### Pourquoi c'est important en Rails

Les blocks apparaissent dans :

- les itérations
- les scopes
- les callbacks
- les transactions
- les routes

### Règle

Quand tu lis Ruby, apprends à repérer immédiatement où la méthode se termine et où le block commence.

## Symbols

```ruby
:name
:email
```

### Explication

Un symbol est une étiquette immuable très utilisée pour représenter un nom, une clé ou une option.

Dans Rails, tu en verras partout :

- `params.require(:post)`
- `status: :created`
- `has_many :comments`

### Règle pratique

Quand tu fais référence à un identifiant stable, un symbol est souvent plus naturel qu'une chaîne.

## Arrays et Hashes

```ruby
tags = ["api", "rails"]
user = { name: "Mora", role: "admin" }
```

### Explication

- un `Array` est une liste ordonnée
- un `Hash` est une structure clé/valeur

Le `Hash` Ruby moderne ressemble beaucoup à un tableau associatif élégant.

### Pourquoi c'est important

Rails manipule constamment :

- des listes d'enregistrements
- des options de méthodes
- des structures JSON proches des hashes Ruby

## Héritage

```ruby
class ApplicationController < ActionController::API
end
```

### Explication

L'héritage permet à une classe de récupérer le comportement d'une autre.

Ici, `ApplicationController` hérite de `ActionController::API`. Cela veut dire qu'il obtient déjà des outils utiles pour gérer des requêtes API.

### Règle

L'héritage doit servir à prolonger un comportement cohérent, pas à cacher une architecture confuse.

## Différences PHP vs Ruby

- Ruby se lit souvent comme une petite DSL
- les parenthèses sont souvent optionnelles
- les méthodes peuvent finir par `?` ou `!`
- le style général est plus expressif et plus compact

### Signification de `?` et `!`

- une méthode finissant par `?` renvoie généralement un booléen ou une réponse de type vrai/faux
- une méthode finissant par `!` signale souvent une version plus stricte, plus risquée ou qui lève une exception

Exemples :

- `admin?`
- `save!`

## Syntaxes Rails importantes

```ruby
before_action :authenticate_user!
render json: @post, status: :created
params.require(:post).permit(:title, :body)
has_many :comments
scope :published, -> { where(published: true) }
```

### Ce qu'il faut comprendre ici

- `before_action` déclare une action à exécuter avant certaines méthodes du contrôleur
- `render json:` renvoie une réponse JSON
- `params.require(...).permit(...)` sécurise les paramètres autorisés
- `has_many` définit une relation
- `scope` crée une requête réutilisable

## Ce que tu dois retenir

Tu n'as pas besoin d'être expert Ruby avant Rails. Tu dois surtout savoir lire rapidement la syntaxe, comprendre les variables, les méthodes, les blocks, les symbols et les conventions qui reviennent partout dans le framework.

## Exercice

Traduis mentalement ces idées Laravel en Ruby :

- collection `map`
- méthode de modèle
- relation `hasMany`
- callback avant sauvegarde

Ensuite, essaie d'écrire un petit modèle Ruby avec :

- une variable
- une méthode
- une relation imaginée
- un nom de méthode finissant par `?`
