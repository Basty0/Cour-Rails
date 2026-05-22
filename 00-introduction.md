# 00 - Introduction

## Objectif

Comprendre ce qu'est Rails, pourquoi il reste tres fort pour construire une API backend moderne, et comment un developpeur Laravel doit ajuster sa facon de penser.

## Ruby en une phrase

Ruby est un langage oriente objet, tres expressif, avec une syntaxe pensee pour etre lisible par des humains avant d'etre impressionnante pour le compilateur.

## Rails en une phrase

Rails est un framework full-stack qui fournit une structure forte, des conventions stables et une enorme productivite pour construire rapidement des applications robustes.

## Philosophie Rails

- Optimiser le temps developpeur.
- Faire gagner du temps sur les decisions repetitives.
- Favoriser une structure standard.
- Encourager le code lisible et intentionnel.
- Livrer vite sans sacrifier la maintenabilite.

## Convention Over Configuration

Rails suppose beaucoup de choses pour toi:

- un model `User` mappe par defaut sur la table `users`
- un controller `UsersController` expose des actions standard
- les dossiers `app/models`, `app/controllers`, `app/jobs` ont un sens fort

En pratique, Rails te demande moins de configuration manuelle que beaucoup de stacks.

## Laravel vs Rails

Laravel et Rails visent une excellente DX, mais l'approche differe:

- Laravel donne souvent plus d'outils explicites.
- Rails pousse plus fort vers une facon de faire standard.
- Laravel est tres confortable si tu viens du monde PHP.
- Rails est tres rapide des que tu acceptes la "Rails Way".

## Ce que Rails fait souvent mieux

- Cohesion globale du framework.
- Convention forte sur l'architecture.
- Integration native entre ORM, jobs, mailers, realtime et storage.
- Ecosysteme mature pour les applications CRUD et metier.

## Ce que Laravel fait souvent mieux

- Prise en main plus douce pour les developpeurs PHP.
- Documentation tres pedagogique.
- Ecosysteme moderne autour d'Inertia, Livewire, Filament et l'outillage DX.
- Plus de confort si ton equipe est deja 100% PHP.

## Penser "Rails Way"

Pour bien apprendre Rails:

- n'essaie pas de reimplementer Laravel en Ruby
- accepte la convention avant de personnaliser
- laisse les noms, dossiers et patterns Rails travailler pour toi
- garde les controllers fins et les models coherents
- ajoute des abstractions seulement quand la pression du code l'exige

## Ce que tu dois retenir

Rails n'est pas seulement un framework Ruby. C'est une facon structuree de construire une application. Plus tu respectes cette structure, plus tu avances vite.

## Exercice

Note sur papier les equivalents suivants:

- `routes/api.php` vs `config/routes.rb`
- `app/Models` vs `app/models`
- `Eloquent` vs `ActiveRecord`
- `Policies` Laravel vs `Pundit`

Le but est de commencer a creer une carte mentale entre les deux ecosystems.
