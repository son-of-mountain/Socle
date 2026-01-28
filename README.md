![Moi](tp.png "This is a sample image.")
# Socle Applicatif - Gestion Universitaire

Ce projet est une application web complète de gestion universitaire, composée de :
- **Frontend** : Vue.js 3 + Vite (Interface utilisateur) ([lien github : https://github.com/melhansali/SocleApplicatif](https://github.com/son-of-mountain/SocleFrontend))
- **Backend** : Spring Boot (API REST) (lien github : https://github.com/son-of-mountain/Socle)
- **Base de Données** : Oracle XE 11g

## 🚀 Démarrage Rapide (Livrable)

Le projet est configuré pour être lancé en **une seule commande** via Docker Compose.

### Prérequis
- Docker Desktop (ou Docker Engine + Docker Compose) installé.

### Lancer l'application

1. Ouvrez un terminal à la racine du projet.
2. Exécutez la commande suivante :

```bash
docker compose up --build
```

Cette commande va :
- Construire les images du Backend et du Frontend.
- Démarrer la base de données Oracle.
- Initialiser la base de données (Schéma + Données sauvegardées).
- Lancer les serveurs d'application.

> **Note** : Le premier démarrage de la base de données Oracle peut prendre quelques minutes. Attendez que le service `backend` démarre complètement.

### Accès à l'application

Une fois les services démarrés :

- **Application Web (Frontend)** : [http://localhost](http://localhost)
- **API Backend (Swagger/Info)** : [http://localhost:8080](http://localhost:8080)
- **Base de Données** : Port `1521`
  - User: `dosi`
  - Password: `dosi`

---

## 💾 Sauvegarde des Données (Optionnel)

Si vous ajoutez des données via l'application et souhaitez les conserver pour une future démonstration (ou pour la livraison), utilisez le script fourni :

```bash
# Sauvegarde l'état actuel de la base de données
./save_db_data.sh
```

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
