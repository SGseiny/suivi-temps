# Suivi des temps par projet/phase

Application web permettant à un utilisateur authentifié de saisir et consulter le temps passé sur différentes phases de différents projets, semaine par semaine.

## Fonctionnalités

- Authentification par identifiant et mot de passe
- Saisie du temps passé pour une semaine, un projet et une phase donnés
- Sauvegarde automatique des saisies
- Consultation de l'historique des temps saisis, avec total d'heures
- Filtrage de l'historique par projet
- Export de l'historique (filtré) en CSV, Excel et JSON
- Suppression d'une saisie

## Stack technique

HTML / CSS / JavaScript natif, sans framework ni dépendance externe. Le stockage des données s'appuie sur le `localStorage` du navigateur, ce qui permet un déploiement entièrement statique (aucun serveur applicatif ni base de données requis).

## Choix de conception

**Pas de framework.** Le périmètre fonctionnel (authentification simple, formulaire, tableau) ne justifie pas l'ajout d'une couche de build ou d'une librairie front. Un seul fichier HTML autoporté simplifie le déploiement et la lecture du code.

**Comptes et référentiels en dur.** Les identifiants utilisateurs ainsi que la liste des projets et de leurs phases sont définis directement dans le code (`USERS` et `PROJECTS`). C'est un choix volontaire pour un périmètre limité ; une montée en charge nécessiterait de déporter ces données vers un backend avec gestion des utilisateurs et des référentiels projets dynamiques.

**Mots de passe hachés (SHA-256).** Les mots de passe ne sont jamais stockés en clair dans le code source : seule leur empreinte SHA-256 y figure, calculée et comparée côté navigateur via l'API Web Crypto. Cela évite l'exposition directe du mot de passe en clair, sans toutefois constituer une sécurité de niveau production (un hash sans salage reste vulnérable à une attaque par dictionnaire). Une vraie protection nécessiterait une authentification côté serveur avec salage, hash robuste (bcrypt/argon2) et gestion de session.

**Export multi-format.** L'historique des temps saisis peut être exporté en CSV, Excel (.xls) et JSON directement depuis l'interface, pour faciliter la réutilisation des données dans un outil de reporting externe.

**Stockage local.** `localStorage` joue le rôle de couche de persistance légère, propre à chaque navigateur. C'est suffisant pour une démonstration ou un usage individuel, mais ne permet pas de partager les données entre plusieurs postes ou utilisateurs simultanés.

## Limites connues

- Les données sont propres au navigateur utilisé ; pas de synchronisation multi-appareils.
- L'authentification n'est pas sécurisée au sens production (pas de hash des mots de passe, pas de session serveur) : adaptée à une démonstration, pas à un usage réel avec données sensibles.
- Pas de gestion multi-utilisateurs centralisée (chaque utilisateur ne voit que ses propres saisies, stockées localement).

## Comptes de test

| Identifiant | Mot de passe |
|---|---|
| pbellugue | admin |
| mwitman | admin |

## Utilisation

1. Cloner le repository
2. Ouvrir `index.html` dans un navigateur (aucune installation requise)
3. Se connecter avec l'un des comptes ci-dessus
4. Sélectionner une semaine, un projet et une phase, saisir le nombre d'heures, valider
5. Consulter l'historique des saisies dans le tableau en bas de page

## Déploiement

Le projet est hébergé en statique via GitHub Pages, branche `main`, dossier racine.

## Évolutions possibles

- Backend avec base de données pour une persistance partagée entre utilisateurs et appareils
- Authentification sécurisée (hash des mots de passe, gestion de sessions)
- Export des temps saisis (CSV, Excel)
- Vue consolidée multi-utilisateurs pour un rôle manager/chef de projet