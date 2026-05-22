# 00 - Introduction

## Objectif

Comprendre ce qu'est Rails, pourquoi il reste très fort pour construire une API backend moderne, et comment un développeur Laravel doit ajuster sa manière de penser.

## Ruby en une phrase

Ruby est un langage orienté objet, très expressif, conçu pour être agréable à lire et rapide à écrire.

## Rails en une phrase

Rails est un framework qui fournit une structure forte, des conventions stables et une excellente productivité pour créer des applications web et des API.

## Philosophie Rails

Rails repose sur quelques idées simples :

- optimiser le temps développeur
- éviter de refaire les mêmes décisions sur chaque projet
- privilégier une structure standard
- rendre le code lisible et cohérent
- permettre d'aller vite sans sacrifier la maintenabilité

## Pourquoi c'est important

Un développeur Laravel qui arrive sur Rails fait souvent une erreur classique : il cherche immédiatement les équivalents exacts de Laravel. Ce réflexe aide un peu au début, mais il devient vite un frein.

La bonne approche est la suivante :

- comprendre ce que Rails veut faire
- comprendre pourquoi Rails le fait de cette manière
- adopter les conventions avant de vouloir les contourner

## Convention Over Configuration

Rails applique fortement le principe "Convention Over Configuration".

Cela veut dire qu'au lieu de te demander de tout configurer manuellement, Rails suppose des règles par défaut.

Exemples :

- un modèle `User` pointe naturellement vers la table `users`
- un contrôleur `UsersController` correspond à une ressource `users`
- les fichiers placés dans `app/models`, `app/controllers` ou `app/jobs` ont déjà une signification précise

## Règle pratique

Quand une convention Rails existe, commence par la respecter.

Tu personnalises seulement si :

- la règle par défaut ne couvre pas ton besoin
- tu comprends exactement ce que tu modifies
- tu peux justifier ce changement à long terme

## Laravel vs Rails

Laravel et Rails visent tous les deux une bonne expérience développeur, mais leur style diffère :

- Laravel expose souvent plus d'outils explicites
- Rails pousse plus fort vers une manière de faire standard
- Laravel est plus familier si tu viens du monde PHP
- Rails devient extrêmement rapide quand tu acceptes le "Rails Way"

## Ce que Rails fait souvent mieux

- cohésion globale du framework
- conventions d'architecture très fortes
- intégration naturelle entre ORM, jobs, mailers, realtime et storage
- rapidité pour lancer un produit métier ou un SaaS

## Ce que Laravel fait souvent mieux

- prise en main plus douce pour un développeur PHP
- documentation très pédagogique
- écosystème très riche autour de l'admin, du frontend hybride et de la DX
- adoption plus simple dans une équipe déjà centrée sur PHP

## Comment penser "Rails Way"

Pour bien apprendre Rails :

- n'essaie pas de reprogrammer Laravel en Ruby
- accepte la convention avant la personnalisation
- laisse les noms, les dossiers et les patterns Rails travailler pour toi
- garde les contrôleurs fins et les responsabilités bien séparées
- ajoute des abstractions seulement quand le code en a réellement besoin

## Ce que tu dois retenir

Rails n'est pas seulement une boîte à outils. C'est une façon structurée de construire une application. Plus tu respectes cette structure, plus tu avances vite et proprement.

## Exercice

Note les équivalents suivants :

- `routes/api.php` vs `config/routes.rb`
- `app/Models` vs `app/models`
- `Eloquent` vs `ActiveRecord`
- `Policies` Laravel vs `Pundit`

Le but est de commencer à construire une vraie carte mentale entre les deux écosystèmes.
