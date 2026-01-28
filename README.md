![Moi](tp.png "This is a sample image.")
# Socle Applicatif - Gestion Universitaire
Ce projet est une application web complète de gestion universitaire, composée de :

- **Frontend** : Vue.js 3 + Vite (interface utilisateur)  [GitHub - SocleFrontend](https://github.com/melhansali/SocleFrontend)

- **Backend** : Spring Boot (API REST  [GitHub - SocleBackend](https://github.com/melhansali/SocleBackend)

- **Base de données** : Oracle XE 11g


## 🚀 Démarrage Rapide (Livrable)

### Lancer l'application

1. Ouvrez un terminal à la racine du projet.
2. Exécutez la commande suivante :

```bash
docker compose up --build
```
### Accès à l'application

Une fois les services démarrés :

- **Application Web (Frontend)** : [http://localhost](http://localhost)
- **API Backend (Swagger/Info)** : [http://localhost:8080](http://localhost:8080)
- **Base de Données** : Port `1521`
  - User: `dosi`
  - Password: `dosi`

---

Le projet est configuré pour être lancé en **une seule commande** via Docker Compose.

### Prérequis
- Docker Desktop (ou Docker Engine + Docker Compose) installé.


Cette commande va :
- Construire les images du Backend et du Frontend.
- Démarrer la base de données Oracle.
- Initialiser la base de données (Schéma + Données sauvegardées).
- Lancer les serveurs d'application.

> **Note** : Le premier démarrage de la base de données Oracle peut prendre quelques minutes. Attendez que le service `backend` démarre complètement.

## 💾 Sauvegarde des Données (Optionnel)

Cela génère un fichier `backend/database/data.dmp`. Ce fichier sera automatiquement chargé au prochain redémarrage (`docker compose up`), garantissant que vos données sont persistantes même après suppression des conteneurs.

## 🛠 Architecture Technique

### 1. Frontend (Dossier `frontend`)
- **Framework** : Vue.js 3
- **Serveur** : Nginx (dans le conteneur Docker)
- **Proxy** : Les appels API `/api` sont redirigés automatiquement vers le backend.

### 2. Backend (Dossier `backend`)
- **Framework** : Spring Boot
- **Port** : 8080
- **Connexion DB** : JDBC vers le service `db`.

### 3. Base de Données (Service `db`)
- **Image** : `gvenzl/oracle-xe:11-slim`
- **Initialisation** : Scripts SQL et DMP dans `backend/database`.

## ❓ Dépannage

- **Le Frontend ne charge pas les données ?**
  Vérifiez que le Backend est bien démarré (logs : `Started Application`).
- **Erreur de connexion DB ?**
  La base Oracle peut être lente à démarrer. Docker Compose attend qu'elle soit "Healthy", mais l'initialisation des tables peut prendre du temps.

---
*Projet réalisé pour le Socle Applicatif.*
