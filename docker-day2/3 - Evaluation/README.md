## 🎯 ÉVALUATION JOUR 2 (14h - 16h)

# Évaluation Docker - Application Multi-Conteneurs

## 📋 Description

Stack applicative complète composée de :
- **API Flask** : Application Python exposant des endpoints REST
- **PostgreSQL** : Base de données relationnelle
- **Nginx** : Reverse proxy et serveur web

## 🏗️ Architecture
```
┌─────────────┐
│   Client    │
└──────┬──────┘
       │ Port 8080
       ▼
┌─────────────┐
│    Nginx    │ (Reverse Proxy)
└──────┬──────┘
       │ Port 5000
       ▼
┌─────────────┐      ┌──────────────┐
│  Flask API  │◄────►│  PostgreSQL  │
└─────────────┘      └──────────────┘
     (app)              (database)
```

## 🚀 Démarrage rapide

### Prérequis
- Docker Desktop installé
- Docker Compose v2+

### Installation

1. **Cloner/Créer le projet**
```bash
cd evaluation-docker
```

2. **Configurer les variables d'environnement**
```bash
cp .env.example .env
# Éditer .env avec vos valeurs
```

3. **Builder et démarrer la stack**
```bash
docker-compose up -d --build
```

4. **Vérifier le statut**
```bash
docker-compose ps
```

### 🧪 Tests

#### Test de l'API via Nginx
```bash
# Page d'accueil
curl http://localhost:8080/

# Health check
curl http://localhost:8080/health

# Informations
curl http://localhost:8080/api/info

# Test de connexion DB
curl http://localhost:8080/api/db-test
```

#### Test direct de l'API (sans Nginx)
```bash
curl http://localhost:5000/
```

## 📂 Structure du projet
```
evaluation-docker/
├── app/
│   ├── app.py              # Code Flask
│   ├── requirements.txt    # Dépendances Python
│   └── Dockerfile          # Image de l'API
├── nginx/
│   └── nginx.conf          # Configuration Nginx
├── docker-compose.yml      # Orchestration
├── .env                    # Variables d'environnement
└── README.md              # Cette documentation
```

## 🔧 Commandes utiles
```bash
# Voir les logs
docker-compose logs -f

# Logs d'un service spécifique
docker-compose logs -f api

# Entrer dans un conteneur
docker-compose exec api /bin/bash
docker-compose exec database psql -U appuser -d myapp

# Redémarrer un service
docker-compose restart api

# Arrêter la stack
docker-compose stop

# Tout supprimer
docker-compose down -v
```

## 🛡️ Sécurité

- ✅ Utilisateur non-root dans le conteneur Flask
- ✅ Variables d'environnement pour les secrets
- ✅ Healthchecks sur tous les services
- ✅ Réseau isolé pour la communication inter-conteneurs

## 📊 Volumes

- `postgres_data` : Persistance des données PostgreSQL

## 🌐 Réseau

- `app_network` (172.20.0.0/16) : Réseau bridge personnalisé

## 🐛 Troubleshooting

### L'API ne se connecte pas à la DB
```bash
# Vérifier que la DB est prête
docker-compose logs database

# Tester la connexion
docker-compose exec database pg_isready
```

### Nginx retourne 502
```bash
# Vérifier que l'API répond
docker-compose exec api curl localhost:5000/health
```

## 👤 Auteur

Participant à la formation Docker - Jour 2

## 📝 Licence

Projet d'évaluation - Formation Docker 2024
```

---

## 🎓 Grille d'évaluation détaillée

### Dockerfile Flask (25 points)

| Critère | Points | Description |
|---------|--------|-------------|
| FROM correct | 3 | Image Python appropriée |
| WORKDIR | 2 | Répertoire de travail défini |
| COPY requirements | 3 | Optimisation du cache |
| RUN pip install | 3 | Installation des dépendances |
| COPY code | 2 | Copie du code source |
| EXPOSE | 2 | Port exposé |
| ENV | 2 | Variables d'environnement |
| CMD/ENTRYPOINT | 5 | Commande de démarrage |
| Bonus sécurité | 3 | USER non-root, healthcheck |

### Docker Compose (40 points)

| Critère | Points | Description |
|---------|--------|-------------|
| Structure YAML | 5 | Syntaxe correcte |
| Service database | 8 | Config complète PostgreSQL |
| Service api | 10 | Build, env, depends_on |
| Service web | 8 | Nginx avec volumes |
| Networks | 4 | Réseau personnalisé |
| Volumes | 3 | Persistance données |
| Healthchecks | 2 | Au moins 1 service |

### Stack opérationnelle (25 points)

| Critère | Points | Description |
|---------|--------|-------------|
| Build réussi | 5 | Pas d'erreurs |
| Tous services UP | 10 | docker-compose ps |
| API accessible | 5 | Endpoints répondent |
| DB connectée | 5 | /api/db-test OK |

### Documentation (10 points)

| Critère | Points | Description |
|---------|--------|-------------|
| README complet | 5 | Structure, commandes |
| Architecture claire | 3 | Schéma ou description |
| Instructions tests | 2 | Comment vérifier |

---

## 💾 Fichiers à télécharger pour les participants

Créez une archive ZIP contenant :
```
formation-docker-jour2.zip
├── exercices/
│   ├── 01-nodejs/
│   │   ├── app.js
│   │   └── package.json
│   └── 02-wordpress/
│       └── .env.example
└── evaluation/
    ├── app/
    │   ├── app.py
    │   └── requirements.txt
    └── nginx/
        └── nginx.conf