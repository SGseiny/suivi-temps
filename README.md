# Suivi des temps par projet/phase

Application web de saisie et de consultation des temps passés par projet et par phase, réalisée dans le cadre d'un exercice technique d'entrée en alternance.

## 1. Compréhension du besoin

Le besoin exprimé se résume à 4 fonctionnalités :
1. Authentification d'un utilisateur (identifiant + mot de passe)
2. Saisie du temps passé sur une phase d'un projet donné, pour une semaine choisie
3. Sauvegarde persistante de cette saisie
4. Consultation des temps déjà saisis par l'utilisateur connecté

Contraintes imposées : pas de base de données obligatoire, deux comptes et la liste des projets/phases codés en dur, accessible depuis un navigateur, sans contrainte de design poussé.

## 2. Choix méthodologiques et techniques

| Choix | Justification |
|---|---|
| HTML/CSS/JavaScript natif (aucun framework) | Exercice court (quelques heures), pas besoin d'un build tool ni d'une stack lourde pour 4 fonctionnalités. Réduit aussi la dépendance à des bibliothèques externes pour un hébergement statique simple. |
| Authentification codée en dur (`USERS`) | Conforme à la consigne ; dans une vraie mise en production, ce mécanisme serait remplacé par une authentification serveur avec mots de passe hashés (jamais en clair côté client). |
| Projets/phases codés en dur (`PROJECTS`) | Conforme à la consigne ; structure en objet JS facilement éditable pour ajouter un projet ou une phase sans toucher au reste du code. |
| Persistance via `localStorage` | Remplace la base de données par un mécanisme de sauvegarde fichier-like, propre au navigateur du poste utilisé. Choix assumé : permet un hébergement 100% statique (GitHub Pages) sans backend, conformément à l'esprit "sauvegarde dans un fichier quelconque" de la consigne. |
| Un fichier HTML unique | Facilite le déploiement statique et la lecture du code dans le cadre de cet exercice ; sur un projet réel de plus grande taille, le code serait scindé (composants, modules JS séparés). |

## 3. Limites connues (assumées, par souci de transparence)

- Les données sont stockées **par navigateur**, pas sur un serveur central : si le recruteur teste depuis deux navigateurs différents, les saisies ne sont pas partagées entre les deux.
- L'authentification n'est pas sécurisée (mots de passe visibles dans le code source) : acceptable uniquement dans le cadre de cet exercice de démonstration, jamais en production.
- Pas de gestion multi-appareil ni de synchronisation : hors périmètre de l'exercice demandé.

## 4. Utilisation

Comptes de test :
- `asali` / `alt2026`
- `jdupont` / `alt2026`

1. Se connecter avec l'un des deux comptes
2. Choisir une semaine, un projet, une phase, saisir le nombre d'heures, valider
3. Les saisies apparaissent immédiatement dans le tableau du bas, avec le total d'heures
4. Possibilité de supprimer une ligne saisie par erreur

## 5. Lancer le projet en local

Aucune dépendance ni installation nécessaire :
1. Cloner le repo
2. Ouvrir `index.html` directement dans un navigateur (double-clic, ou clic droit > "Ouvrir avec")

## 6. Déploiement

Hébergé en statique via GitHub Pages : Settings > Pages > branche `main` > dossier `/root`.

## 7. Pistes d'évolution si le projet devait grossir

- Remplacer `localStorage` par un vrai backend (API REST + base de données) pour une persistance partagée entre utilisateurs et appareils
- Authentification sécurisée côté serveur (hash des mots de passe, sessions/JWT)
- Export des temps saisis en CSV/Excel pour reporting
- Vue "manager" consolidant les temps de plusieurs collaborateurs par projet