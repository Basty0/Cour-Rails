# 06 - ActiveRecord et les modèles

## Objectif

Maîtriser ActiveRecord pour manipuler les données proprement, comprendre les relations entre les tables, et éviter les erreurs classiques de performance.

## Qu'est-ce qu'ActiveRecord

ActiveRecord est l'ORM de Rails.

ORM signifie "Object-Relational Mapping". En pratique, cela veut dire qu'ActiveRecord fait le lien entre :

- les objets Ruby
- les tables SQL
- les lignes de base de données

Avec ActiveRecord, tu manipules un objet Ruby comme `Post`, mais derrière, Rails traduit cela en requêtes SQL.

## Pourquoi c'est important

Quand tu travailles avec Rails, ActiveRecord est partout :

- dans les modèles
- dans les contrôleurs
- dans les relations entre ressources
- dans les validations
- dans les filtres et les requêtes

Tu dois donc comprendre non seulement "comment écrire du code ActiveRecord", mais aussi "ce que ce code coûte en base de données".

## CRUD

```ruby
post = Post.create(title: "Hello", body: "World")
post.update(title: "Updated")
post.destroy
```

### Explication

Ces trois lignes représentent les opérations de base :

- `create` crée un enregistrement
- `update` modifie un enregistrement existant
- `destroy` supprime un enregistrement

### Règle

Le CRUD est la base, mais il ne suffit pas. Un bon développeur Rails doit toujours se demander :

- cette requête est-elle claire ?
- est-elle efficace ?
- respecte-t-elle les règles métier ?

## Requêtes essentielles

```ruby
Post.find(1)
Post.where(published: true)
Post.order(created_at: :desc)
Post.limit(10)
```

### Explication

- `find(1)` récupère un enregistrement par son identifiant
- `where(...)` filtre les résultats
- `order(...)` trie les résultats
- `limit(10)` limite le nombre de lignes renvoyées

Ces appels retournent souvent une relation chaînable, ce qui permet de composer des requêtes.

Exemple :

```ruby
Post.where(published: true).order(created_at: :desc).limit(10)
```

## Scopes

```ruby
scope :published, -> { where(published: true) }
scope :recent, -> { order(created_at: :desc) }
```

### Explication

Un scope est une requête nommée et réutilisable.

Il sert à :

- éviter de répéter la même logique de filtrage
- clarifier l'intention du code
- rendre les requêtes plus lisibles

### Règle

Un scope doit rester :

- simple
- lisible
- prévisible

Si un scope devient trop complexe, il vaut souvent mieux le déplacer dans un objet de requête.

## Validations

```ruby
validates :title, presence: true
validates :slug, uniqueness: true
```

### Explication

Les validations servent à empêcher l'enregistrement de données invalides.

Exemples :

- un titre ne doit pas être vide
- un slug doit être unique

### Règle importante

Les validations Ruby protègent l'application, mais elles ne remplacent pas les contraintes SQL.

Par exemple :

- une validation `uniqueness` doit souvent être renforcée par un index unique en base

## Callbacks

```ruby
before_validation :generate_slug
after_create :send_notification
```

### Explication

Les callbacks permettent d'exécuter une méthode automatiquement avant ou après certains événements du cycle de vie du modèle.

### Quand les utiliser

- pour préparer une donnée
- pour normaliser un champ
- pour déclencher une petite action cohérente avec le modèle

### Règle

Les callbacks doivent rester courts et prévisibles.

Trop de callbacks rendent le comportement du modèle difficile à suivre, parce que des actions se déclenchent "en cachette".

## Relations

```ruby
class Post < ApplicationRecord
  belongs_to :user
  has_many :comments, dependent: :destroy
end
```

### Explication

Les relations décrivent les liens entre les modèles et les tables.

Ici :

- un `Post` appartient à un `User`
- un `Post` possède plusieurs `Comment`

### Pourquoi c'est important

Les relations permettent d'écrire un code expressif :

- `post.user`
- `post.comments`

Mais elles peuvent aussi déclencher des requêtes SQL invisibles si tu ne fais pas attention.

## Eager loading

```ruby
Post.includes(:user, :comments)
```

### Explication

`includes` demande à Rails de charger à l'avance certaines associations.

Cela évite que Rails fasse une requête supplémentaire à chaque accès à la relation.

## N+1

Problème classique :

```ruby
posts = Post.all
posts.each { |post| puts post.user.name }
```

### Ce qui se passe

Si chaque `post.user` déclenche une requête, tu obtiens :

- 1 requête pour charger les posts
- puis 1 requête par post pour charger l'utilisateur

C'est ce qu'on appelle un problème N+1.

### Pourquoi c'est grave

Sur peu de données, tu ne le sens pas. En production, cela peut dégrader fortement la performance.

## Optimisation des requêtes

- utiliser `includes` quand une association sera lue
- sélectionner seulement ce qui est utile
- paginer les listes
- analyser les logs SQL
- ajouter les bons index

## ActiveRecord vs Eloquent

- les deux ORM sont très productifs
- ActiveRecord est plus central dans l'identité Rails
- Eloquent semble souvent plus explicite pour un développeur PHP
- ActiveRecord paraît très naturel quand on adopte vraiment la convention Rails

## Ce que tu dois retenir

ActiveRecord n'est pas seulement une syntaxe pratique. C'est le cœur de la relation entre Rails et SQL. La vraie compétence consiste à écrire du code lisible tout en gardant la maîtrise du coût des requêtes.
