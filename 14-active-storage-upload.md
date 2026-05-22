# 14 - Active Storage Upload

## Objectif

Gerer des fichiers dans Rails proprement, avec stockage local ou cloud.

## Active Storage

Active Storage est la solution native Rails pour attacher des fichiers a des models.

## Exemple

```ruby
class User < ApplicationRecord
  has_one_attached :avatar
end
```

## Upload image

Depuis un controller API, tu peux recevoir un fichier dans les params et l'attacher au model.

## Validations fichiers

Rails ne couvre pas tout nativement sur les validations metier de fichier. On ajoute souvent:

- type MIME
- taille maximale
- presence si necessaire

## Stockage cloud

Options courantes:

- local en developpement
- Amazon S3 en production
- parfois Cloudinary selon les besoins

## S3

Configuration typique:

- bucket
- region
- credentials
- service declare dans `storage.yml`

## Optimisation image

Selon le besoin:

- variantes
- redimensionnement
- compression

Pour une API, pense aussi a ne pas renvoyer les fichiers bruts dans les payloads principaux.

## Bonnes pratiques

- stocker l'URL ou la reference, pas le binaire dans le JSON
- securiser les acces
- limiter la taille des uploads
- traiter les transformations en background job si lourd

## Comparaison Laravel

- proche de la logique `Storage` + uploads Laravel
- Rails te donne un flux plus centralise via Active Storage

## Ce que tu dois retenir

Un upload n'est pas juste "recevoir un fichier". Il faut penser validation, stockage, URL, securite et cout de traitement.
