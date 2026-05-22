# 07 - Migrations, schéma et seeds

## Objectif

Comprendre comment Rails fait évoluer la base de données dans le temps et comment garder un schéma propre, cohérent et reproductible.

## Les migrations

Une migration décrit une évolution de base de données.

```bash
bin/rails generate migration AddSlugToPosts slug:string
bin/rails db:migrate
```

### Explication

Une migration permet par exemple de :

- créer une table
- ajouter une colonne
- supprimer une colonne
- créer un index
- ajouter une clé étrangère

En pratique, une migration raconte comment le schéma change.

## Exemple de migration

```ruby
class AddSlugToPosts < ActiveRecord::Migration[8.0]
  def change
    add_column :posts, :slug, :string
    add_index :posts, :slug, unique: true
  end
end
```

### Lecture détaillée

- `add_column` ajoute une nouvelle colonne
- `add_index` améliore la recherche et garantit ici l'unicité

## Pourquoi les migrations sont importantes

Sans migration propre :

- les environnements divergent
- la base devient difficile à faire évoluer
- les déploiements deviennent risqués

Une migration n'est donc pas un simple script technique. C'est un morceau de l'histoire de ton application.

## `schema.rb`

`db/schema.rb` est la photo actuelle du schéma Ruby.

### À quoi il sert

Il permet de voir rapidement l'état final de la base sans relire toutes les migrations une à une.

### Règle

Il ne remplace pas les migrations. Il résume leur résultat.

## `seeds.rb`

`db/seeds.rb` sert à injecter des données de base ou de démonstration.

```ruby
admin = User.find_or_create_by!(email: "admin@example.com") do |user|
  user.password = "password123"
end
```

### Cas d'usage

- créer un compte administrateur initial
- charger des données de test local
- préparer un environnement de démonstration

## Rollback

```bash
bin/rails db:rollback
bin/rails db:migrate:status
```

### Explication

Le rollback permet de revenir en arrière sur une migration récente.

Tu dois savoir l'utiliser, surtout quand tu modifies une structure sensible en base.

## Relations SQL

Il faut toujours penser schéma avant modèle.

- `belongs_to` implique souvent une clé étrangère
- `has_many` implique une relation entre une table parent et une table enfant
- les contraintes SQL restent importantes même si Rails valide déjà au niveau applicatif

## Index

Ajoute des index pour :

- les clés étrangères
- les colonnes souvent recherchées
- les colonnes d'unicité

### Pourquoi

Un backend lent est souvent un backend mal indexé.

## Clés étrangères

```ruby
add_reference :posts, :user, null: false, foreign_key: true
```

### Explication

Une clé étrangère protège l'intégrité entre tables.

Cela évite par exemple qu'un post pointe vers un utilisateur qui n'existe plus.

## Workflow sain

1. Écrire la migration.
2. Migrer en local.
3. Vérifier le schéma généré.
4. Tester le rollback si la migration est sensible.
5. Committer la migration et le schéma ensemble.

## Comparaison avec Laravel

- `php artisan make:migration` devient `bin/rails generate migration`
- les deux frameworks offrent une bonne ergonomie
- Rails s'appuie fortement sur `schema.rb` pour représenter l'état courant

## Ce que tu dois retenir

Une migration doit être lisible, sûre et logique. Tu dois pouvoir la relire plus tard et comprendre immédiatement ce qu'elle change et pourquoi.
