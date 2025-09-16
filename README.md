# 🌍 Gaia

---

## 📖 Description

Docker Compose prête à l'emploi pour déployer [Gitea](https://gitea.io/) et [Jenkins](https://www.jenkins.io/) dans un environnement local, offrant une alternative à GitHub pour la gestion de dépôts Git et l'automatisation CI/CD. Ce projet permet de créer un système local de gestion de code source et de documentation (README) avec des pipelines d'intégration et de déploiement continus (CI/CD).

---

## ✨ Fonctionnalités

- **Gitea** : Serveur Git léger pour gérer les dépôts, wikis, et documentation (similaire à GitHub).
- **Jenkins** : Automatisation CI/CD pour construire, tester et déployer vos projets.
- **Configuration pré-intégrée** : Gitea et Jenkins fonctionnent ensemble dans un réseau Docker.
- **Données persistantes** : Volumes pour les données de Gitea, Jenkins, et la base de données.
- **Prêt pour la production** : Supporte HTTPS et les sauvegardes pour un usage professionnel.

---

## 🛠 Prérequis

- [Docker](https://docs.docker.com/get-docker/) (version 20.10+)
- [Docker Compose](https://docs.docker.com/compose/install/) (version 1.29+ ou Docker Compose V2)
- Des connaissances de base sur Docker, Git, et les pipelines CI/CD

---

## 📦 Installation

1. **Cloner le dépôt** :
   ```bash
   git clone https://github.com/BangSkyline/Gaia.git
   cd Gaia
   ```
   
2. **Démarrer les services** :
   Lancez la commande suivante pour télécharger les images et démarrer les conteneurs :
   ```bash
   docker compose up -d
   ```

3. **Configurer Gitea** :
   - Accédez à Gitea via `http://localhost:3000` (ou le port configuré).
   - Suivez l'assistant d'installation :
     - Hôte de la base de données : `db` (nom interne du conteneur).
     - Nom de la base de données : `gitea`.
     - Utilisateur/Mot de passe : Comme défini dans `.env`.
   - Connectez-vous avec les identifiants administrateur définis dans `.env`.

4. **Configurer Jenkins** :
   - Accédez à Jenkins via `http://localhost:8080` (ou le port configuré).
   - Récupérez le mot de passe initial dans les logs : `docker compose logs jenkins`.
   - Suivez l'assistant d'installation pour configurer Jenkins et installer les plugins recommandés.
   - Connectez-vous avec `admin` et le mot de passe défini dans `JENKINS_ADMIN_PASSWORD`.

---

## 🚀 Utilisation

- **Accéder à Gitea** : Naviguez vers `http://<ip-du-conteneur>:85` pour gérer vos dépôts, wikis, et README.
- **Accéder à Jenkins** : Naviguez vers `http://<ip-du-conteneur>:8080` pour configurer vos pipelines CI/CD.
- **Intégration Gitea-Jenkins** :
   - Configurez des webhooks dans Gitea pour déclencher des builds Jenkins.
   - Installez le plugin Jenkins [Gitea Plugin](https://plugins.jenkins.io/gitea/) pour une intégration native.

---

## 🔍 Aperçu des services

| Service | Image | Rôle | Ports |
|---------|-------|------|-------|
| gitea   | gitea/gitea:1.21 | Serveur Git et interface web | 85:80 |
| jenkins | jenkins/jenkins:2.426-lts | Serveur CI/CD | 8080:80 |
| db      | Postegre| Base de données PostegreSQl | 5432 (interne) |

---

[![GitHub Repo stars](https://img.shields.io/github/stars/BangSkyline/Gaia?style=social)](https://github.com/BangSkyline/Gaia)
[![Docker Compose](https://img.shields.io/badge/Docker%20Compose-1.29%2B-blue)](https://docs.docker.com/compose/)
[![Gitea](https://img.shields.io/badge/Gitea-1.21%2B-green)](https://gitea.io/)
[![Jenkins](https://img.shields.io/badge/Jenkins-2.426%2B-orange)](https://www.jenkins.io/)

---

*Si ce projet vous est utile, mettez une étoile au dépôt !*
