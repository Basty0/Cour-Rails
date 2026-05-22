# 18 - Hotwire Turbo Stimulus

## Objectif

Comprendre ce que Rails propose nativement pour construire des interfaces dynamiques sans SPA classique.

## Hotwire

Hotwire regroupe surtout:

- Turbo
- Stimulus

## Turbo

Turbo accelere les interactions HTML sans recharger toute la page:

- navigation rapide
- formulaires
- partial updates
- streams

## Stimulus

Stimulus apporte une couche JavaScript legere, ciblee sur le comportement.

## SPA sans React

Pour beaucoup de produits internes ou apps CRUD, Hotwire permet:

- moins de JavaScript
- moins de duplication front/back
- integration naturelle avec Rails

## Realtime frontend Rails

Turbo Streams + ActionCable peuvent pousser des mises a jour en direct.

## Quand c'est utile

- dashboards admin
- outils internes
- produits CRUD
- interfaces ou le SEO ou la simplicite priment

## Quand eviter

- front tres interactif type produit design complexe
- equipe frontend separee avec stack JS dediee
- besoin fort de client state complexe

## Difference avec Livewire ou Inertia

- proche de Livewire dans l'esprit de productivite
- moins "SPA framework centric" qu'Inertia
- tres coherent si Rails pilote tout le produit

## Ce que tu dois retenir

Meme si ton focus est API, comprendre Hotwire aide a voir la force globale de Rails: livrer vite avec tres peu de couches techniques.
