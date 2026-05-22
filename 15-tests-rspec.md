# 15 - Tests avec RSpec

## Objectif

Mettre en place une stratégie de tests API crédible, lisible et maintenable.

## Pourquoi tester

Les tests servent à :

- sécuriser les évolutions
- détecter les régressions
- documenter le comportement attendu
- donner confiance à l'équipe

Pour une API, les tests sont particulièrement utiles car ils valident le contrat HTTP.

## RSpec

RSpec est le standard le plus répandu pour les tests Rails.

Il est apprécié pour :

- sa lisibilité
- sa maturité
- sa richesse d'écosystème

## Types de tests utiles

- request specs
- model specs
- policy specs
- service specs

## Request specs

Ce sont souvent les tests les plus rentables pour une API.

Ils valident :

- les routes
- l'authentification
- les statuts HTTP
- la structure JSON

### Pourquoi ils sont très importants

Ils testent l'application presque comme un vrai client.

## Model specs

Ils sont utiles pour vérifier :

- les validations
- les scopes
- les petites règles métier du modèle

## FactoryBot

FactoryBot permet de générer des données de test lisibles.

```ruby
FactoryBot.define do
  factory :user do
    email { "user@example.com" }
    password { "password123" }
  end
end
```

### Pourquoi c'est utile

Une factory propre évite de réécrire la même préparation de données dans chaque test.

## Faker

Faker aide à varier les données sans écrire tout à la main.

## Exemple de request spec

```ruby
describe "GET /api/v1/posts" do
  it "returns posts" do
    create_list(:post, 3)

    get "/api/v1/posts"

    expect(response).to have_http_status(:ok)
  end
end
```

### Explication

Ce test :

- prépare des posts
- appelle un endpoint réel
- vérifie le résultat HTTP

## Bonnes pratiques

- tester le comportement, pas l'implémentation interne
- viser d'abord les endpoints critiques
- garder les factories simples
- vérifier les cas d'erreur et d'autorisation

## Comparaison avec Laravel

- c'est proche des feature tests Laravel
- l'objectif reste le même : tester l'API comme un client réel

## Ce que tu dois retenir

Pour une API, les request specs donnent souvent le meilleur retour sur investissement. Commence par elles, puis ajoute d'autres couches de tests là où elles apportent une vraie valeur.
