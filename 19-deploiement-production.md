# 19 - Deploiement Production

## Objectif

Preparer une API Rails pour un environnement de production fiable.

## Base de donnees production

PostgreSQL reste le choix naturel. Pense:

- sauvegardes
- pool de connexions
- index
- monitoring

## Puma

Puma sert les requetes applicatives. Il faut regler:

- nombre de workers
- nombre de threads
- timeout

## Nginx

Souvent place devant Puma pour:

- reverse proxy
- compression
- gestion TLS
- headers

## Docker

Docker simplifie la reproductibilite mais n'est pas obligatoire. Il devient utile si:

- tu veux uniformiser les environnements
- tu deploies sur une plateforme conteneurisee

## Render et Railway

Tres bons choix pour aller vite sur des projets modernes avec peu d'ops manuelles.

## VPS

Plus de controle, plus de responsabilite:

- securite
- updates
- monitoring
- logs

## Variables d'environnement

Tu dois externaliser:

- secrets
- URLs externes
- credentials base
- config Redis/S3/mail

## Logs

Surveille:

- erreurs applicatives
- temps de reponse
- jobs echoues
- SQL lent

## Securite production

- HTTPS partout
- credentials proteges
- CSP et headers si necessaire
- gems a jour
- acces admin restreint

## Ce que tu dois retenir

Un deploiement reussi n'est pas juste un `deploy`. C'est un systeme stable: base, app server, secrets, logs, jobs et supervision.
