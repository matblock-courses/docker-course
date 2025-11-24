Exercice 2 : Déploiement d'une application WordPress avec Docker Compose
================================================================
Ce projet utilise Docker Compose pour déployer une application WordPress avec une base de données MySQL. Il inclut également la configuration d'un volume pour la persistance des données.

1 - Créer docker-compose.yml

2 - Définir une stack WordPress + MySQL avec services, réseaux et volumes

3 - Gérer la persistance

4 - Configurer les volumes pour sauvegarder les données MySQL

5 - Démarrer la stack

```bash
Lancer docker-compose up -d pour déployer tous les services
```

6 - Vérifier la communication entre les conteneurs

```bash
Tester les connexions entre conteneurs sur le réseau interne


# Démarrer la stack complète
docker-compose up -d

# Voir l'état des services
docker-compose ps

# Voir les logs
docker-compose logs -f

# Logs d'un service spécifique
docker-compose logs wordpress

# Exécuter une commande dans un conteneur
docker-compose exec database mysql -u root -p

# Arrêter la stack
docker-compose stop

# Arrêter et supprimer les conteneurs (garde les volumes)
docker-compose down

# Tout supprimer y compris les volumes
docker-compose down -v

# Rebuilder les images si nécessaire
docker-compose build --no-cache
```

---