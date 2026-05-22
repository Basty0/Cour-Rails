# 20 - Gems Indispensables

## Objectif

Connaitre les gems les plus utiles pour une API Rails moderne sans tomber dans la dependance inutile.

## Gems API

- `rack-cors` pour les politiques CORS
- `kaminari` ou `pagy` pour la pagination
- `blueprinter` ou autre serializer pour la sortie JSON

## Gems securite

- `devise`
- `devise-jwt`
- `pundit`
- `brakeman`

## Gems performance

- `bullet`
- `rack-mini-profiler` en dev selon le contexte

## Gems auth

- `devise`
- `doorkeeper` si besoin OAuth2

## Gems upload

- `image_processing`
- parfois `aws-sdk-s3` avec Active Storage

## Gems testing

- `rspec-rails`
- `factory_bot_rails`
- `faker`
- `shoulda-matchers`

## Gems admin

- `administrate`
- `activeadmin`

Selon le type de back-office, tu peux aussi preferer un front sur mesure.

## Gems monitoring

- `sentry-ruby`
- `newrelic_rpm`
- `skylight`

## Regle de selection

Avant d'ajouter une gem, demande-toi:

- le besoin est-il recurrent
- la gem est-elle maintenue
- est-elle idiomatique Rails
- le cout de lock-in est-il acceptable

## Ce que tu dois retenir

La bonne stack Rails n'est pas celle qui a le plus de gems. C'est celle qui garde un noyau simple et des dependances vraiment justifiees.
