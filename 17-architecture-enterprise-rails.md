# 17 - Architecture Rails pour projet plus large

## Objectif

Faire évoluer une petite API Rails vers une application plus grande sans la transformer en chaos technique.

## Problème classique

Au début, Rails est très simple. Puis arrivent :

- des contrôleurs trop gros
- des modèles trop intelligents
- de la logique dupliquée
- des requêtes complexes un peu partout

## Pourquoi l'architecture devient importante

Une petite application peut survivre avec quelques raccourcis.

Une grande application, non.

Quand l'équipe grandit et que le domaine métier se complexifie, il faut mieux structurer le code.

## Briques utiles

### Services

Ils portent les use cases métier.

### Queries

Ils isolent des lectures complexes.

Exemple :

- `PostsQuery.new(user: current_user).visible`

### Concerns

Ils servent à partager un comportement commun.

### Règle sur les concerns

Un concern peut être utile, mais il peut aussi masquer du code confus. Il ne faut donc pas l'utiliser comme cache-misère architectural.

### Forms

Ils peuvent aider à valider des payloads complexes ou à coordonner plusieurs objets.

### Interactors

Certaines équipes aiment représenter les use cases sous forme de commandes explicites.

### Validators

Ils deviennent utiles quand les validations dépassent le simple modèle ActiveRecord.

## Organisation d'une grande application

Une structure fréquente :

- `app/services`
- `app/queries`
- `app/policies`
- `app/serializers`
- `app/forms`

## Règles pragmatiques

- une abstraction doit supprimer une vraie douleur
- le nom doit exprimer une intention métier
- les dépendances doivent rester explicites
- les use cases importants doivent être faciles à tester

## Quand ajouter des couches

Ajoute une nouvelle couche quand :

- la logique se répète
- plusieurs contrôleurs réutilisent les mêmes opérations
- les tests deviennent fragiles
- le code perd en lisibilité

## Comparaison avec Laravel

Les mêmes enjeux existent avec les Actions, DTO, Services ou couches Domain dans Laravel.

Rails ne supprime pas la nécessité d'une bonne architecture. Il te donne simplement un démarrage plus cohérent.

## Ce que tu dois retenir

Une architecture Rails mature doit rester idiomatique Rails. Le but n'est pas d'empiler des patterns, mais d'organiser la complexité de manière claire et progressive.
