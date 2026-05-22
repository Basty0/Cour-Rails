# 17 - Architecture Enterprise Rails

## Objectif

Faire evoluer une petite API Rails vers une application large sans la transformer en chaos.

## Probleme classique

Au debut, Rails est tres simple. Ensuite arrivent:

- gros controllers
- models trop intelligents
- logique dupliquee
- queries complexes partout

## Briques utiles

### Services

Pour les use cases metier.

### Queries

Pour isoler des lectures complexes:

- `PostsQuery.new(user: current_user).visible`

### Concerns

Utiles avec moderation. Un concern qui masque du code confus n'est pas une victoire.

### Forms

Pratique pour la validation de payloads complexes ou multi-models.

### Interactors

Option utile si ton equipe aime modeler les use cases comme des commandes explicites.

### Validators

Quand les validations de domaine depassent le simple model.

## Organisation grande application

Une structure frequente:

- `app/services`
- `app/queries`
- `app/policies`
- `app/serializers`
- `app/forms`

## Clean architecture Rails

Il ne faut pas sur-architecturer trop tot. Le bon seuil:

- quand les cas metier se repetent
- quand plusieurs controllers reutilisent les memes operations
- quand les tests deviennent fragiles

## Regles pragmatiques

- une abstraction doit supprimer une douleur reelle
- preferer des noms metier
- garder les dependances explicites
- tester les use cases importants en isolation

## Comparaison Laravel

Les memes enjeux existent avec Actions, DTO, Repositories, Services et Domains. Rails n'evite pas la dette de structure. Il la repousse seulement mieux au demarrage.

## Ce que tu dois retenir

Une architecture enterprise Rails reussie reste idiomatique Rails. Elle n'essaie pas de nier le framework, elle organise la complexite autour de lui.
