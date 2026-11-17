# CAMPUSBOT
### Assistant universitaire intelligent basé sur une architecture RAG

**Projet académique — Groupe 5**

---

# 1. Présentation du projet

## 1.1. Contexte

Dans les établissements d'enseignement supérieur, les étudiants ont régulièrement besoin d'informations concernant leur parcours universitaire : inscriptions, emplois du temps, frais de scolarité, procédures administratives et autres questions relatives à la vie académique.

Ces informations ne sont pas toujours centralisées ou facilement accessibles. Les mêmes questions sont fréquemment posées aux services administratifs, ce qui entraîne une perte de temps pour les étudiants et le personnel.

CampusBot est conçu pour répondre à cette problématique.

## 1.2. Définition

**CampusBot est une application mobile d'assistance universitaire intelligente permettant aux étudiants d'obtenir des réponses à leurs questions à partir d'une base de connaissances universitaire.**

L'application utilise une interface conversationnelle et une architecture RAG (Retrieval-Augmented Generation) pour rechercher les informations pertinentes avant de générer une réponse.

CampusBot repose sur deux espaces principaux :

- **Espace Étudiant :** permet de poser des questions, consulter les réponses et retrouver les conversations précédentes.
- **Espace Administrateur :** permet de gérer les informations universitaires qui alimentent la base de connaissances.

## 1.3. Objectif général

Faciliter l'accès aux informations universitaires grâce à un assistant conversationnel capable de rechercher et de restituer des informations pertinentes, de manière rapide et structurée.

## 1.4. Objectifs spécifiques

- Centraliser les informations universitaires dans une base de connaissances.
- Permettre aux étudiants de poser des questions en langage naturel.
- Fournir des réponses contextualisées à partir des données disponibles.
- Réduire les recherches manuelles d'informations.
- Conserver l'historique des conversations.
- Permettre aux administrateurs de maintenir les informations à jour.
- Garantir une utilisation sécurisée de la plateforme.

---

# 2. Utilisateurs et rôles

CampusBot possède deux catégories principales d'utilisateurs.

## 2.1. Étudiant

L'étudiant est l'utilisateur principal de l'application.

Il peut :

- Créer un compte et se connecter.
- Accéder à son tableau de bord.
- Poser des questions au chatbot.
- Consulter les réponses fournies.
- Explorer les catégories de FAQ.
- Effectuer des recherches.
- Consulter son historique de conversations.
- Reprendre une ancienne conversation.
- Gérer les informations de son profil.

Exemples de questions :

- Comment effectuer mon inscription ?
- Quels sont les frais de scolarité ?
- Où puis-je consulter mon emploi du temps ?
- Quelles sont les pièces nécessaires pour constituer mon dossier ?

## 2.2. Administrateur

L'administrateur est responsable de la gestion des informations disponibles dans CampusBot.

Il peut :

- Accéder à son espace d'administration.
- Ajouter une question et sa réponse.
- Modifier une information existante.
- Supprimer une FAQ.
- Organiser les FAQ par catégories.
- Consulter les statistiques d'utilisation.
- Administrer la base de connaissances.

L'administrateur ne doit pas avoir besoin de modifier directement le code source pour mettre à jour les FAQ.

---

# 3. Fonctionnalités principales

## 3.1. Authentification

Le système doit permettre :

- L'inscription des utilisateurs.
- La connexion et la déconnexion.
- La gestion des rôles.
- La protection des routes selon les permissions.

Les utilisateurs étudiants ne doivent pas pouvoir accéder aux fonctionnalités réservées aux administrateurs.

## 3.2. Assistant conversationnel

Le chatbot constitue le cœur de CampusBot.

Il permet à l'étudiant de formuler une question en langage naturel et de recevoir une réponse issue de la base de connaissances.

L'interface doit proposer :

- Une zone de saisie.
- Un bouton d'envoi.
- L'affichage des messages.
- L'indication du chargement.
- La gestion des erreurs.
- L'affichage des sources utilisées lorsque cela est possible.

## 3.3. Gestion des FAQ

Les FAQ sont organisées par catégories afin de faciliter leur consultation.

Exemples de catégories :

- Inscriptions.
- Frais de scolarité.
- Emplois du temps.
- Examens.
- Documents administratifs.
- Vie universitaire.

Chaque FAQ contient au minimum :

- Une question.
- Une réponse.
- Une catégorie.
- Des informations de suivi permettant sa gestion.

## 3.4. Historique des conversations

L'étudiant doit pouvoir :

- Consulter ses anciennes conversations.
- Ouvrir une conversation.
- Retrouver les questions et réponses précédentes.

Les conversations doivent être associées au compte de leur propriétaire.

## 3.5. Tableau de bord administrateur

L'administrateur dispose d'un tableau de bord présentant notamment :

- Le nombre de FAQ enregistrées.
- Le nombre de catégories.
- Le nombre d'utilisateurs.
- Le nombre de conversations.

Ces statistiques doivent provenir des données réellement enregistrées dans le système.

---

# 4. Architecture technique

## 4.1. Technologies retenues

| Composant | Technologie | Responsabilité |
|---|---|---|
| Application mobile | React Native | Interface utilisateur |
| Backend | Django REST Framework | API et logique métier |
| Base de données | PostgreSQL | Stockage des données |
| Recherche vectorielle | pgvector | Recherche sémantique |
| Intelligence artificielle | Gemini Flash | Génération des réponses |
| Orchestration IA | LangChain | Organisation du processus RAG |
| Communication | API REST | Échange entre mobile et backend |
| Gestion du code | Git / GitHub | Collaboration et versionnement |

## 4.2. Architecture générale

CampusBot suit une architecture client-serveur.

```text
             UTILISATEUR
                  |
                  |
          APPLICATION MOBILE
             React Native
                  |
                  |
              API REST
                  |
                  |
       DJANGO REST FRAMEWORK
                  |
          +-------+-------+
          |               |
          |               |
     AUTHENTIFICATION   MODULE RAG
                          |
                    LangChain
                          |
                 RECHERCHE VECTORIELLE
                          |
                       pgvector
                          |
                      PostgreSQL
                          |
                  CONTEXTE RETENU
                          |
                    Gemini Flash
                          |
                  RÉPONSE GÉNÉRÉE
                          |
                   API REST
                          |
                  APPLICATION
```

## 4.3. Responsabilités des composants

**React Native**

Gère les interfaces, les interactions et la communication avec le backend.

**Django REST Framework**

Centralise la logique métier, l'authentification, les autorisations, les conversations et les opérations sur les données.

**PostgreSQL**

Stocke les utilisateurs, les FAQ, les catégories et les conversations.

**pgvector**

Permet de stocker et de rechercher des représentations vectorielles des informations universitaires.

**LangChain**

Organise les différentes étapes nécessaires au fonctionnement du système RAG.

**Gemini Flash**

Intervient dans la génération des réponses à partir du contexte documentaire récupéré.

---

# 5. Fonctionnement de l'intelligence artificielle

## 5.1. Principe du RAG

RAG signifie Retrieval-Augmented Generation.

Il s'agit d'une approche qui combine deux opérations :

1. La récupération d'informations pertinentes dans une base de connaissances.
2. La génération d'une réponse à partir des informations récupérées.

L'objectif est de limiter les réponses inventées en donnant au modèle des informations vérifiables sur lesquelles s'appuyer.

## 5.2. Traitement d'une question

Lorsqu'un étudiant pose une question, le processus suit les étapes suivantes :

**Étape 1 — Réception**

L'application transmet la question au backend Django.

**Étape 2 — Préparation**

Le backend prépare la question pour la recherche sémantique.

**Étape 3 — Recherche**

Le système recherche dans la base documentaire les informations les plus pertinentes grâce à pgvector.

**Étape 4 — Construction du contexte**

Les informations pertinentes sont regroupées pour constituer le contexte destiné au modèle.

**Étape 5 — Génération**

Gemini Flash reçoit la question et le contexte récupéré afin de produire une réponse.

**Étape 6 — Restitution**

Le backend renvoie la réponse à l'application mobile.

**Étape 7 — Historisation**

La question et la réponse sont enregistrées dans l'historique de conversation.

## 5.3. Gestion des réponses incorrectes ou introuvables

CampusBot doit respecter une règle fondamentale :

**Une information absente de la base de connaissances ne doit pas être présentée comme une information universitaire vérifiée.**

Lorsque le système ne trouve pas suffisamment d'informations pertinentes :

- Il doit signaler qu'il ne dispose pas d'une réponse fiable.
- Il ne doit pas inventer de dates, de montants ou de procédures.
- Il peut orienter l'étudiant vers le service compétent lorsque les informations de contact sont disponibles.

## 5.4. Gestion de la base de connaissances

La qualité des réponses dépend directement de la qualité des informations enregistrées.

Le processus d'alimentation comprend :

1. La collecte des documents et informations universitaires.
2. L'extraction du contenu pertinent.
3. Le nettoyage et la structuration des informations.
4. Le découpage des documents en unités exploitables.
5. La génération des embeddings.
6. L'enregistrement des vecteurs dans PostgreSQL avec pgvector.

Une mise à jour de la base documentaire doit entraîner la mise à jour des données utilisées par le moteur de recherche.

---

# 6. Organisation des données

Les principales entités de la base de données sont les suivantes.

| Entité | Description |
|---|---|
| User | Informations des utilisateurs |
| Role | Rôle de chaque utilisateur |
| Category | Catégories des FAQ |
| FAQ | Questions et réponses |
| Document | Documents alimentant la base de connaissances |
| DocumentChunk | Fragments de documents utilisés pour la recherche |
| Embedding | Représentations vectorielles des fragments |
| Conversation | Conversations des étudiants |
| Message | Messages échangés avec le chatbot |

Les relations doivent garantir la cohérence des données.

Exemples :

- Un utilisateur peut posséder plusieurs conversations.
- Une conversation contient plusieurs messages.
- Une catégorie peut regrouper plusieurs FAQ.
- Un document peut être découpé en plusieurs fragments.
- Chaque fragment peut posséder une représentation vectorielle.

---

# 7. Sécurité et contrôle d'accès

La sécurité doit être prise en compte dès la conception.

Les exigences principales sont :

- Authentification des utilisateurs.
- Gestion des rôles et permissions.
- Protection des endpoints de l'API.
- Validation des données reçues.
- Protection des informations personnelles.
- Séparation des conversations entre utilisateurs.
- Protection des clés API et secrets.
- Mise en place de quotas pour limiter les abus du chatbot.

Les opérations administratives doivent être accessibles uniquement aux utilisateurs disposant des permissions nécessaires.

---

# 8. Organisation fonctionnelle du projet

Le projet est organisé autour de cinq grands modules.

| Module | Responsabilité |
|---|---|
| Interface mobile | Écrans et interactions utilisateur |
| Backend et API | Logique métier et communication |
| Intelligence artificielle | Recherche et génération des réponses |
| Base de données | Stockage et gestion des informations |
| Sécurité et tests | Protection et validation du système |

Ces modules doivent être développés de manière coordonnée.

Aucune partie ne doit être conçue indépendamment des contrats d'interface et des structures de données communes.

---

# 9. Organisation de l'équipe

Le groupe est constitué de six membres.

## Équipe Frontend

**NJIMONGBA FOCHIVE MAMA ABDOURAHIM**

**GUILIBEB A MOUKON DURELLE**

Responsabilités :

- Développement de l'application React Native.
- Conception des interfaces.
- Navigation entre les écrans.
- Intégration des API.
- Gestion des états de l'application.
- Tests des interactions utilisateur.

## Équipe Backend

**LEMOBENG TANKEU WILLY AUREL**

**DJOUKOUO KENGNE ANGE RAYANNE**

**NDOUNDA MICHEL**

**TALEGHANG TALEGHANG BAURELE EKUMENE**

Responsabilités :

- Développement de l'API Django REST Framework.
- Gestion de l'authentification.
- Implémentation des fonctionnalités métier.
- Développement du système RAG.
- Intégration de Gemini Flash et LangChain.
- Gestion des conversations.
- Sécurité et contrôle des accès.

## Responsabilité Base de données

**DJOUKOUO KENGNE ANGE RAYANNE**

Responsabilités complémentaires :

- Conception du modèle relationnel.
- Mise en place de PostgreSQL.
- Intégration de pgvector.
- Gestion des migrations.
- Organisation de la base documentaire.
- Optimisation des recherches.

La responsabilité de la base de données est transversale et nécessite une collaboration avec les membres du backend.

---

# 10. Limites du projet

CampusBot est un assistant d'information universitaire.

Il ne doit pas être confondu avec un système complet de gestion universitaire.

Les fonctionnalités suivantes ne constituent pas le cœur du projet :

- Gestion effective des inscriptions.
- Paiement des frais de scolarité.
- Gestion des notes.
- Modification des emplois du temps.
- Réseau social étudiant.
- Messagerie entre étudiants.
- Gestion administrative complète des établissements.

CampusBot doit fournir des informations sur ces sujets lorsque celles-ci sont disponibles dans sa base de connaissances, mais ne doit pas nécessairement réaliser les opérations administratives correspondantes.

---

# 11. Livrables attendus

Le projet doit aboutir aux livrables suivants :

1. Maquettes et prototype interactif de l'application.
2. Application mobile React Native.
3. Backend Django REST Framework.
4. Base de données PostgreSQL.
5. Système de recherche vectorielle pgvector.
6. Système RAG intégré avec LangChain et Gemini Flash.
7. Système d'authentification et de gestion des rôles.
8. Base de connaissances universitaire.
9. Historique des conversations.
10. Tests fonctionnels et techniques.
11. Documentation technique et utilisateur.
12. Procédure de déploiement.

---

# 12. Méthode de collaboration

Pour garantir la cohérence du projet, tous les membres doivent respecter les règles suivantes.

## 12.1. Git et GitHub

- Chaque membre travaille sur une branche dédiée.
- Les modifications doivent être régulièrement synchronisées.
- Les commits doivent avoir des messages explicites.
- Les changements importants doivent être vérifiés avant leur fusion dans la branche principale.

## 12.2. Communication entre frontend et backend

Les deux équipes doivent s'accorder sur :

- Les endpoints de l'API.
- Les formats des requêtes.
- Les formats des réponses JSON.
- Les mécanismes d'authentification.
- La gestion des erreurs.
- Les structures des données.

Le frontend ne doit pas inventer ses propres formats de données indépendamment du backend.

## 12.3. Qualité du code

Chaque membre doit :

- Respecter l'organisation du projet.
- Écrire du code lisible et maintenable.
- Documenter les parties complexes.
- Tester les fonctionnalités développées.
- Éviter les duplications inutiles.
- Ne pas intégrer une fonctionnalité sans comprendre son fonctionnement.

---

# 13. Principes fondamentaux de CampusBot

Toutes les décisions techniques et fonctionnelles doivent respecter les principes suivants :

**1. Fiabilité**

Les réponses doivent s'appuyer sur des informations disponibles et vérifiables.

**2. Simplicité**

L'application doit être facile à utiliser, même pour un étudiant peu expérimenté avec les outils numériques.

**3. Cohérence**

Les interfaces, les API et les données doivent respecter une architecture commune.

**4. Sécurité**

Les comptes, les conversations et les informations doivent être protégés.

**5. Maintenabilité**

L'application doit pouvoir évoluer sans nécessiter une reconstruction complète.

**6. Utilité**

Chaque fonctionnalité développée doit contribuer directement à l'objectif principal : faciliter l'accès à l'information universitaire.

---

# 14. Critères de réussite

CampusBot sera considéré comme fonctionnel lorsque :

- Un étudiant pourra créer un compte et se connecter.
- Il pourra poser une question depuis l'application mobile.
- Le backend pourra traiter cette question.
- Le système RAG pourra rechercher des informations pertinentes.
- Le chatbot pourra produire une réponse contextualisée.
- L'étudiant pourra consulter ses anciennes conversations.
- L'administrateur pourra gérer les FAQ.
- Les modifications de la base de connaissances seront prises en compte.
- Les permissions seront correctement appliquées.
- Les principaux scénarios auront été testés.

---

# Conclusion

CampusBot est un projet logiciel combinant développement mobile, développement backend, gestion de données et intelligence artificielle.

Sa valeur ne réside pas uniquement dans la présence d'un chatbot, mais dans sa capacité à fournir aux étudiants des informations universitaires pertinentes à partir d'une base de connaissances contrôlée.

Chaque membre de l'équipe contribue à la réalisation d'un même produit. La cohérence entre les interfaces, le backend, la base de données et le moteur RAG est donc une condition essentielle de réussite.