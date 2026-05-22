# 18 - Hotwire, Turbo et Stimulus

## Objectif

Comprendre ce que Rails propose nativement pour construire des interfaces dynamiques sans SPA classique.

## Pourquoi ce chapitre existe dans un cours API

Même si ton focus principal est l'API, comprendre Hotwire aide à voir la vision globale de Rails.

Rails n'est pas seulement bon pour les API. Il est aussi fort pour livrer rapidement des interfaces modernes avec peu de JavaScript.

## Hotwire

Hotwire regroupe principalement :

- Turbo
- Stimulus

## Turbo

Turbo accélère les interactions HTML sans recharger toute la page.

Il peut gérer :

- la navigation rapide
- les formulaires
- les mises à jour partielles
- les streams

## Stimulus

Stimulus apporte une couche JavaScript légère, ciblée sur le comportement.

### Idée centrale

Tu n'écris pas une grosse application frontend complète. Tu ajoutes seulement le JavaScript nécessaire là où le comportement l'exige.

## Une SPA sans React ?

Pour beaucoup de produits internes ou d'applications CRUD, Hotwire permet :

- moins de JavaScript
- moins de duplication front/back
- une intégration très naturelle avec Rails

## Realtime frontend Rails

Turbo Streams et ActionCable peuvent pousser des mises à jour en direct.

## Quand c'est utile

- dashboards admin
- outils internes
- produits CRUD
- interfaces où la simplicité prime

## Quand éviter

- front très interactif type produit riche côté client
- équipe frontend séparée avec stack JavaScript dédiée
- besoin fort de state client complexe

## Différence avec Livewire ou Inertia

- l'esprit est proche de Livewire sur la productivité
- l'approche est moins centrée SPA qu'Inertia
- la cohérence est très forte quand Rails pilote toute l'application

## Ce que tu dois retenir

Hotwire montre bien la force de Rails : réduire le nombre de couches techniques quand le produit n'a pas besoin d'une grosse SPA complexe.
