# 20 - Gems indispensables

## Objectif

Connaître les gems les plus utiles pour une API Rails moderne sans tomber dans l'accumulation inutile de dépendances.

## Pourquoi bien choisir ses gems

Une gem peut faire gagner beaucoup de temps.

Mais chaque gem ajoute aussi :

- une dépendance
- une maintenance potentielle
- un risque de compatibilité

Il faut donc choisir avec discipline.

## Gems API

- `rack-cors` pour les politiques CORS
- `kaminari` ou `pagy` pour la pagination
- `blueprinter` ou un autre serializer pour la sortie JSON

## Gems sécurité

- `devise`
- `devise-jwt`
- `pundit`
- `brakeman`

## Gems performance

- `bullet`
- `rack-mini-profiler` en développement selon le contexte

## Gems auth avancée

- `devise`
- `doorkeeper` si tu as besoin d'OAuth2

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

Selon le produit, un back-office sur mesure peut aussi être un meilleur choix.

## Gems monitoring

- `sentry-ruby`
- `newrelic_rpm`
- `skylight`

## Règle de sélection

Avant d'ajouter une gem, demande-toi :

- le besoin est-il récurrent ?
- la gem est-elle maintenue ?
- est-elle idiomatique dans l'écosystème Rails ?
- le coût de lock-in est-il acceptable ?

## Ce que tu dois retenir

La bonne stack Rails n'est pas celle qui a le plus de gems. C'est celle qui garde un noyau simple et des dépendances vraiment justifiées.
