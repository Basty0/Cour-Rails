# 07 - Migrations Schema Seeds

## Objectif

Comprendre comment Rails fait vivre le schema de base de donnees dans le temps.

## Migrations

Une migration decrit une evolution de schema:

```bash
bin/rails generate migration AddSlugToPosts slug:string
bin/rails db:migrate
```

## Exemple de migration

```ruby
class AddSlugToPosts < ActiveRecord::Migration[8.0]
  def change
    add_column :posts, :slug, :string
    add_index :posts, :slug, unique: true
  end
end
```

## schema.rb

`db/schema.rb` est la photo actuelle du schema Ruby. Il ne remplace pas les migrations, il resume leur resultat.

## seeds.rb

`db/seeds.rb` sert a injecter des donnees de base ou de demo:

```ruby
admin = User.find_or_create_by!(email: "admin@example.com") do |user|
  user.password = "password123"
end
```

## Rollback

```bash
bin/rails db:rollback
bin/rails db:migrate:status
```

Il faut savoir revenir en arriere proprement.

## Relations SQL

Pense toujours schema avant model:

- `belongs_to` implique souvent une foreign key
- `has_many` implique une table enfant
- les contraintes SQL restent importantes meme si Rails valide au niveau app

## Index

Ajoute des index pour:

- foreign keys
- colonnes recherchees
- unicite fonctionnelle

Un backend lent est souvent un backend mal indexe.

## Foreign keys

```ruby
add_reference :posts, :user, null: false, foreign_key: true
```

Ne laisse pas l'integrite referentielle uniquement au code Ruby.

## Workflow sain

1. Ecrire la migration.
2. Migrer en local.
3. Verifier le schema.
4. Tester le rollback si la migration est sensible.
5. Committer migration et schema ensemble.

## Comparaison Laravel

- `php artisan make:migration` devient `bin/rails generate migration`
- les deux sont proches en ergonomie
- Rails s'appuie fortement sur `schema.rb`

## Ce que tu dois retenir

Une migration n'est pas juste un script technique. C'est un contrat d'evolution de ta base. Ecris-la comme si tu devais la relire en production sous pression.
