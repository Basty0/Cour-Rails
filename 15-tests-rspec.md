# 15 - Tests RSpec

## Objectif

Mettre en place une strategie de tests API credible et maintenable.

## RSpec

RSpec est le standard le plus repandu pour les tests Rails.

## Types de tests utiles

- request specs
- model specs
- policy specs
- service specs

## Request specs

Ce sont les tests les plus rentables pour une API.

Ils valident:

- routes
- auth
- status HTTP
- structure JSON

## Model specs

Utiles pour:

- validations
- scopes
- petites regles metier

## FactoryBot

FactoryBot permet de generer des donnees test lisibles.

```ruby
FactoryBot.define do
  factory :user do
    email { "user@example.com" }
    password { "password123" }
  end
end
```

## Faker

Faker aide a varier les donnees sans ecrire tout a la main.

## Exemple request spec

```ruby
describe "GET /api/v1/posts" do
  it "returns posts" do
    create_list(:post, 3)

    get "/api/v1/posts"

    expect(response).to have_http_status(:ok)
  end
end
```

## Bonnes pratiques

- tester le comportement, pas l'implementation
- viser d'abord les endpoints critiques
- garder les factories simples
- verifier les cas d'erreur et d'autorisation

## Comparaison Laravel

- proche des feature tests Laravel
- meme objectif: tester l'API comme un client reel

## Ce que tu dois retenir

Pour une API, les request specs donnent souvent le meilleur retour sur investissement. Commence par elles, puis ajoute le reste la ou il y a une vraie valeur.
