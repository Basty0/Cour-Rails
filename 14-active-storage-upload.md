# 14 - Active Storage et upload de fichiers

## Objectif

Gérer des fichiers dans Rails proprement, avec stockage local ou cloud, sans négliger la validation, la sécurité et la performance.

## Active Storage

Active Storage est la solution native de Rails pour attacher des fichiers à des modèles.

## Exemple

```ruby
class User < ApplicationRecord
  has_one_attached :avatar
end
```

### Explication

Ici, un utilisateur peut avoir un avatar attaché.

Rails gère alors :

- le lien entre le modèle et le fichier
- le stockage
- les métadonnées associées

## Upload d'image

Depuis un contrôleur API, tu peux recevoir un fichier dans les paramètres et l'attacher au modèle.

### Règle

Un upload ne doit jamais être pensé comme "je reçois juste un fichier". Il faut aussi penser :

- validation
- poids
- type
- sécurité
- stratégie de stockage

## Validations de fichiers

Rails ne couvre pas tout nativement pour les validations métier de fichier. On ajoute souvent :

- type MIME autorisé
- taille maximale
- présence si nécessaire

## Stockage cloud

Options courantes :

- local en développement
- Amazon S3 en production
- parfois Cloudinary selon les besoins

## S3

Configuration typique :

- bucket
- région
- credentials
- service déclaré dans `storage.yml`

## Optimisation d'image

Selon le besoin :

- variantes
- redimensionnement
- compression

### Règle

Si le traitement devient coûteux, il vaut mieux le déplacer dans un background job.

## Bonnes pratiques

- stocker l'URL ou la référence, pas le binaire dans le JSON
- sécuriser les accès
- limiter la taille des uploads
- traiter les transformations lourdes en asynchrone

## Comparaison avec Laravel

- c'est proche de la logique `Storage` + upload Laravel
- Rails te donne un flux plus centralisé via Active Storage

## Ce que tu dois retenir

Un upload bien conçu demande plus qu'un simple attachement de fichier. Il faut penser validation, stockage, diffusion, sécurité et coût de traitement.
