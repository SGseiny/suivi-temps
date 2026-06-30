# Suivi des temps

Petite application web pour saisir et consulter le temps passé par projet et par phase, semaine par semaine.

## Fonctionnalités

- Connexion avec identifiant / mot de passe
- Saisie du temps sur une phase d'un projet, pour une semaine donnée
- Sauvegarde automatique des saisies
- Consultation de l'historique avec total d'heures, filtre par projet
- Export CSV / Excel / JSON
- Suppression d'une saisie

## Techno

HTML / CSS / JS, sans framework. Les données sont stockées dans le `localStorage` du navigateur (pas de base de données, comme demandé dans le sujet).

## Comptes de test

- pbellugue / admin
- mwitman / admin

Les comptes et la liste des projets/phases sont codés en dur dans le fichier (`USERS` et `PROJECTS`), comme demandé.

## Remarques

- Les mots de passe sont hachés (SHA-256) plutôt que stockés en clair dans le code, mais ça reste un mécanisme côté navigateur donc pas une vraie sécurité production.
- Les données sont propres à chaque navigateur (pas de partage entre plusieurs postes), puisqu'il n'y a pas de backend.

## Lancer le projet

Cloner le repo et ouvrir `index.html` dans un navigateur, rien d'autre à installer.

## Suivi des étapes

Le détail des étapes de réalisation est dans `CHANGELOG.md`.