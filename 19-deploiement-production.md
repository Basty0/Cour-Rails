# 19 - Déploiement en production

## Objectif

Préparer une API Rails pour un environnement de production fiable, stable et surveillable.

## Base de données en production

PostgreSQL reste le choix naturel.

Il faut penser à :

- la sauvegarde
- le pool de connexions
- les index
- le monitoring

## Puma

Puma sert les requêtes applicatives.

Il faut réfléchir à :

- la mémoire disponible
- le nombre de workers
- le nombre de threads
- les timeouts

## Nginx

Nginx est souvent placé devant Puma pour :

- le reverse proxy
- la compression
- la gestion TLS
- certains headers HTTP

## Docker

Docker améliore la reproductibilité, mais n'est pas obligatoire.

Il devient très utile si :

- tu veux uniformiser les environnements
- tu déploies dans une plateforme conteneurisée

## Render et Railway

Ce sont de très bons choix pour aller vite avec peu d'opérations manuelles.

## VPS

Le VPS donne plus de contrôle, mais aussi plus de responsabilités :

- sécurité
- mises à jour
- monitoring
- logs

## Variables d'environnement

Tu dois externaliser :

- les secrets
- les URLs externes
- les identifiants de base
- la configuration Redis, S3 ou mail

## Logs

Surveille :

- les erreurs applicatives
- les temps de réponse
- les jobs échoués
- les requêtes SQL lentes

## Sécurité en production

- HTTPS partout
- secrets protégés
- gems à jour
- accès admin restreint
- configuration propre des en-têtes si nécessaire

## Ce que tu dois retenir

Un bon déploiement ne consiste pas seulement à rendre l'application accessible. Il faut aussi penser fiabilité, sécurité, observabilité et maintenance.
