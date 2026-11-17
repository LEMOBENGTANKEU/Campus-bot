# Architecture du Projet CampusBot

## Vue d'ensemble

CampusBot est organisé selon une architecture client-serveur avec une séparation claire entre le backend (API Django REST Framework) et le frontend (application React Native).

```
Campus-bot/
├── backend/              # API Django REST Framework
├── frontend/             # Application React Native
├── docs/                 # Documentation technique
├── .github/              # Configuration CI/CD
├── nginx/                # Configuration Nginx
├── docker-compose.yml    # Orchestration Docker
└── README.md            # Documentation du projet
```

---

## Structure du Backend

```
backend/
├── campusbot/            # Configuration du projet Django
│   ├── __init__.py
│   ├── settings.py      # Configuration globale
│   ├── urls.py          # Routage principal
│   ├── wsgi.py          # Interface WSGI
│   ├── asgi.py          # Interface ASGI
│   └── celery.py        # Configuration Celery
├── apps/                # Applications Django modulaires
│   ├── authentication/  # Gestion de l'authentification
│   ├── faq/             # Gestion des FAQ
│   ├── conversations/   # Historique des conversations
│   ├── rag/             # Système RAG (IA)
│   └── documents/      # Gestion des documents
├── core/                # Modules partagés (utils, constants)
├── scripts/             # Scripts de maintenance
├── tests/               # Tests unitaires et d'intégration
├── static/              # Fichiers statiques
├── media/               # Fichiers uploadés
├── manage.py            # Script de gestion Django
├── requirements.txt     # Dépendances Python
└── Dockerfile           # Configuration Docker
```

### Détail des Applications Django

#### `apps/authentication/`
Gestion de l'authentification et des utilisateurs.
- **models.py** : Modèle User personnalisé avec rôles (student/admin)
- **serializers.py** : Sérialiseurs pour inscription, connexion, profil
- **views.py** : Endpoints API pour auth (login, register, logout, profile)
- **urls.py** : Routes de l'API d'authentification
- **admin.py** : Interface admin Django pour les utilisateurs

#### `apps/faq/`
Gestion des questions fréquentes et catégories.
- **models.py** : Modèles Category et FAQ
- **serializers.py** : Sérialiseurs pour CRUD FAQ
- **views.py** : Endpoints API avec filtres et recherche
- **urls.py** : Routes pour FAQ et catégories
- **admin.py** : Interface admin pour gérer les FAQ

#### `apps/conversations/`
Historique des conversations utilisateurs.
- **models.py** : Modèles Conversation et Message
- **serializers.py** : Sérialiseurs pour conversations et messages
- **views.py** : Endpoints API pour CRUD conversations
- **urls.py** : Routes pour conversations et messages
- **admin.py** : Interface admin pour les conversations

#### `apps/rag/`
Système RAG (Retrieval-Augmented Generation).
- **models.py** : Modèle Embedding pour vecteurs
- **services.py** : Service RAG avec LangChain et Gemini
- **serializers.py** : Sérialiseurs pour requêtes et réponses
- **views.py** : Endpoint API pour le chatbot
- **urls.py** : Routes pour le système RAG
- **admin.py** : Interface admin pour les embeddings

#### `apps/documents/`
Gestion de la base de connaissances.
- **models.py** : Modèles Document et DocumentChunk
- **serializers.py** : Sérialiseurs pour documents
- **views.py** : Endpoints API pour CRUD documents
- **urls.py** : Routes pour documents et traitement
- **tasks.py** : Tâches Celery pour traitement asynchrone
- **admin.py** : Interface admin pour les documents

---

## Structure du Frontend

```
frontend/
├── src/
│   ├── screens/         # Écrans de l'application
│   │   ├── auth/       # Écrans d'authentification
│   │   │   ├── LoginScreen.js
│   │   │   └── RegisterScreen.js
│   │   ├── admin/      # Écrans admin
│   │   │   ├── AdminDashboardScreen.js
│   │   │   └── FAQManagementScreen.js
│   │   ├── HomeScreen.js
│   │   ├── ChatScreen.js
│   │   ├── HistoryScreen.js
│   │   └── ProfileScreen.js
│   ├── components/      # Composants réutilisables
│   ├── navigation/     # Configuration navigation
│   │   └── AppNavigator.js
│   ├── services/        # Services API
│   │   └── api.js
│   ├── store/          # Redux store
│   │   ├── store.js
│   │   └── slices/     # Redux slices
│   │       ├── authSlice.js
│   │       └── conversationSlice.js
│   ├── contexts/       # React Context providers
│   ├── utils/          # Fonctions utilitaires
│   │   └── helpers.js
│   ├── constants/       # Constantes de l'app
│   │   └── index.js
│   ├── assets/         # Images, fonts, etc.
│   ├── App.js          # Composant racine
│   └── index.js        # Point d'entrée
├── android/            # Configuration Android
├── ios/                # Configuration iOS
├── package.json        # Dépendances Node
├── app.json           # Configuration React Native
├── babel.config.js    # Configuration Babel
└── metro.config.js    # Configuration Metro bundler
```

### Détail des Dossiers Frontend

#### `src/screens/`
Contient tous les écrans de l'application.
- **auth/** : Login et inscription
- **admin/** : Dashboard et gestion admin
- **HomeScreen.js** : Page d'accueil avec catégories
- **ChatScreen.js** : Interface de chat avec le bot
- **HistoryScreen.js** : Historique des conversations
- **ProfileScreen.js** : Profil utilisateur

#### `src/components/`
Composants UI réutilisables (boutons, inputs, cards, etc.).

#### `src/navigation/`
Configuration de la navigation (React Navigation).
- Stack Navigator pour auth
- Tab Navigator pour navigation principale

#### `src/services/`
Services pour communiquer avec l'API backend.
- **api.js** : Configuration Axios et endpoints API

#### `src/store/`
Gestion d'état avec Redux Toolkit.
- **store.js** : Configuration du store
- **slices/** : Slices pour auth et conversations

#### `src/contexts/`
React Context providers pour état global.

#### `src/utils/`
Fonctions utilitaires (formatage, validation, etc.).

#### `src/constants/`
Constantes de l'application (couleurs, tailles, screens).

#### `src/assets/`
Ressources statiques (images, icônes, fonts).

---

## Structure de la Documentation

```
docs/
├── api/                # Documentation API
│   ├── authentication.md
│   ├── faq.md
│   ├── conversations.md
│   ├── rag.md
│   └── documents.md
├── database/           # Documentation base de données
│   ├── schema.md
│   ├── migrations.md
│   └── relationships.md
└── deployment/         # Documentation déploiement
    ├── docker.md
    ├── production.md
    └── monitoring.md
```

---

## Configuration CI/CD

### `.github/workflows/backend-ci.yml`
Pipeline CI/CD pour le backend Django :
- Tests unitaires avec PostgreSQL
- Linting avec Flake8
- Build Docker image
- Déploiement automatique sur main

### `.github/workflows/frontend-ci.yml`
Pipeline CI/CD pour le frontend React Native :
- Tests unitaires
- Linting ESLint
- Build Android APK
- Build iOS (sur macOS)

---

## Configuration Docker

### `docker-compose.yml`
Orchestration des services :
- **postgres** : Base de données PostgreSQL avec pgvector
- **redis** : Broker pour Celery
- **backend** : API Django REST Framework
- **celery** : Worker Celery pour tâches asynchrones
- **celery-beat** : Scheduler Celery pour tâches planifiées
- **nginx** : Reverse proxy et serveur de fichiers statiques

### `nginx/nginx.conf`
Configuration Nginx :
- Reverse proxy vers backend
- Service des fichiers statiques
- Service des fichiers media
- Gestion des uploads

---

## Variables d'Environnement

### `.env.example`
Template des variables d'environnement requises :
- Configuration Django (SECRET_KEY, DEBUG, ALLOWED_HOSTS)
- Configuration base de données
- Configuration Redis
- Configuration RAG (GEMINI_API_KEY, modèles)
- Configuration CORS

---

## Flux de Données

```
React Native App
       ↓
    API REST
       ↓
Django REST Framework
       ↓
┌──────┴──────┐
│             │
PostgreSQL  LangChain + Gemini
(pgvectors)    (RAG)
```

1. L'utilisateur envoie une question depuis l'app mobile
2. L'app envoie la requête à l'API Django
3. Django authentifie l'utilisateur
4. Le service RAG recherche les chunks pertinents dans PostgreSQL
5. LangChain envoie le contexte à Gemini Flash
6. Gemini génère la réponse
7. Django renvoie la réponse à l'app mobile
8. La conversation est sauvegardée en base de données

---

## Sécurité

- Authentification par token (Django REST Framework Token Authentication)
- Séparation des rôles (student/admin)
- Protection des endpoints admin
- Validation des données
- Variables d'environnement pour secrets
- HTTPS en production (Nginx)
