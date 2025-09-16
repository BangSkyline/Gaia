# 🌍 Gaia

[![GitHub Repo stars](https://img.shields.io/github/stars/BangSkyline/Gaia?style=social)](https://github.com/BangSkyline/Gaia)
[![Docker Compose](https://img.shields.io/badge/Docker%20Compose-1.29%2B-blue)](https://docs.docker.com/compose/)
[![Gitea](https://img.shields.io/badge/Gitea-1.21%2B-green)](https://gitea.io/)
[![Jenkins](https://img.shields.io/badge/Jenkins-2.426%2B-orange)](https://www.jenkins.io/)

---

## 📖 Description

**Gaia** est une configuration Docker Compose prête à l'emploi pour déployer [Gitea](https://gitea.io/) et [Jenkins](https://www.jenkins.io/) dans un environnement local, offrant une alternative à GitHub pour la gestion de dépôts Git et l'automatisation CI/CD. Ce projet permet de créer un système local de gestion de code source et de documentation (README) avec des pipelines d'intégration et de déploiement continus (CI/CD).

Gaia est idéal pour les développeurs souhaitant héberger leurs propres dépôts Git et automatiser leurs workflows dans un environnement autohébergé, avec une configuration simple et rapide.

---

## ✨ Fonctionnalités

- **Gitea** : Serveur Git léger pour gérer les dépôts, wikis, et documentation (similaire à GitHub).
- **Jenkins** : Automatisation CI/CD pour construire, tester et déployer vos projets.
- **Configuration pré-intégrée** : Gitea et Jenkins fonctionnent ensemble dans un réseau Docker.
- **Données persistantes** : Volumes pour les données de Gitea, Jenkins, et la base de données.
- **Personnalisation facile** : Variables d'environnement via `.env` pour les ports, mots de passe, etc.
- **Prêt pour la production** : Supporte HTTPS et les sauvegardes pour un usage professionnel.

---

## 🛠 Prérequis

Avant de commencer, assurez-vous d'avoir installé :

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

2. **Copier le fichier d'environnement** :
   Copiez le fichier d'exemple et personnalisez-le selon vos besoins (par exemple, ports, mots de passe) :
   ```bash
   cp .env.example .env
   ```

   Modifiez `.env` avec vos valeurs préférées :
   - `GITEA_ADMIN_USER` et `GITEA_ADMIN_PASSWORD` : Identifiants pour l'administrateur Gitea.
   - `JENKINS_ADMIN_PASSWORD` : Mot de passe initial pour Jenkins.
   - `DB_ROOT_PASSWORD` : Mot de passe root pour la base de données.
   - `HTTP_PORT_GITEA` : Port pour Gitea (par défaut : 3000).
   - `HTTP_PORT_JENKINS` : Port pour Jenkins (par défaut : 8080).

3. **Démarrer les services** :
   Lancez la commande suivante pour télécharger les images et démarrer les conteneurs :
   ```bash
   docker compose up -d
   ```

4. **Configurer Gitea** :
   - Accédez à Gitea via `http://localhost:3000` (ou le port configuré).
   - Suivez l'assistant d'installation :
     - Hôte de la base de données : `db` (nom interne du conteneur).
     - Nom de la base de données : `gitea`.
     - Utilisateur/Mot de passe : Comme défini dans `.env`.
   - Connectez-vous avec les identifiants administrateur définis dans `.env`.

5. **Configurer Jenkins** :
   - Accédez à Jenkins via `http://localhost:8080` (ou le port configuré).
   - Récupérez le mot de passe initial dans les logs : `docker compose logs jenkins`.
   - Suivez l'assistant d'installation pour configurer Jenkins et installer les plugins recommandés.
   - Connectez-vous avec `admin` et le mot de passe défini dans `JENKINS_ADMIN_PASSWORD`.

6. **Vérifier la configuration** :
   Vérifiez l'état des services :
   ```bash
   docker compose ps
   ```
   Consultez les logs pour dépanner :
   ```bash
   docker compose logs -f
   ```

---

## 🚀 Utilisation

- **Accéder à Gitea** : Naviguez vers `http://localhost:3000` pour gérer vos dépôts, wikis, et README.
- **Accéder à Jenkins** : Naviguez vers `http://localhost:8080` pour configurer vos pipelines CI/CD.
- **Intégration Gitea-Jenkins** :
   - Configurez des webhooks dans Gitea pour déclencher des builds Jenkins.
   - Installez le plugin Jenkins [Gitea Plugin](https://plugins.jenkins.io/gitea/) pour une intégration native.
- **Arrêter les services** : `docker compose down`
- **Mise à jour** : Téléchargez les dernières images avec `docker compose pull` et redémarrez avec `docker compose up -d`.

### ⚙️ Configuration personnalisée

- **HTTPS Support** : Ajoutez un reverse proxy (comme Traefik ou Nginx) pour activer SSL. Montez vos certificats dans le volume approprié.
- **Sauvegarde** :
   - Gitea : Sauvegardez les données avec `docker compose exec gitea gitea dump`.
   - Jenkins : Sauvegardez le dossier `~/.jenkins` dans le volume `jenkins_home`.
   - Base de données : `docker compose exec db mysqldump -u root -p gitea > backup.sql`.
- **Pipelines CI/CD** : Configurez Jenkins pour cloner les dépôts Gitea et exécuter des builds automatisés.

---

## 📂 Structure du projet

```
Gaia/
├── docker-compose.yml      # Fichier Compose principal définissant les services
├── .env.example            # Exemple de variables d'environnement
├── gitea/                  # Volume pour les données Gitea
├── jenkins/                # Volume pour les données Jenkins
└── README.md               # Ce fichier
```

---

## 🔍 Aperçu des services

| Service | Image | Rôle | Ports |
|---------|-------|------|-------|
| gitea   | gitea/gitea:1.21 | Serveur Git et interface web | 3000:3000 |
| jenkins | jenkins/jenkins:2.426-lts | Serveur CI/CD | 8080:8080 |
| db      | mariadb:10.11 | Base de données MariaDB | 3306 (interne) |

---

## 🛠 Dépannage

- **Problèmes de connexion à la base de données** : Vérifiez que le service `db` est sain (`docker compose logs db`). Redémarrez si nécessaire.
- **Jenkins ne démarre pas** : Vérifiez le mot de passe initial dans les logs (`docker compose logs jenkins`) et assurez-vous que le port 8080 est libre.
- **Gitea inaccessible** : Vérifiez le port `HTTP_PORT_GITEA` dans `.env` et les logs (`docker compose logs gitea`).
- **Intégration Gitea-Jenkins** : Assurez-vous que le webhook Gitea pointe vers `http://jenkins:8080/gitea-webhook/`.
- **Documentation** :
   - [Gitea](https://docs.gitea.io/)
   - [Jenkins](https://www.jenkins.io/doc/)
   - [Jenkins Gitea Plugin](https://plugins.jenkins.io/gitea/)

Si vous rencontrez des problèmes, ouvrez une issue sur le [dépôt GitHub](https://github.com/BangSkyline/Gaia/issues).

---

## 🤝 Contribution

Les contributions sont les bienvenues ! Veuillez suivre ces étapes :

1. Forkez le dépôt.
2. Créez une branche pour votre fonctionnalité (`git checkout -b feature/NouvelleFonctionnalité`).
3. Validez vos modifications (`git commit -m 'Ajout de NouvelleFonctionnalité'`).
4. Poussez vers la branche (`git push origin feature/NouvelleFonctionnalité`).
5. Ouvrez une Pull Request.

Pour des modifications majeures, ouvrez d'abord une issue pour en discuter.

---

## 📜 Licence

Ce projet est sous licence MIT - voir le fichier [LICENSE](LICENSE) pour plus de détails (à ajouter si absent).

---

## 🙏 Remerciements

- [Gitea](https://gitea.io/) pour une alternative légère à GitHub.
- [Jenkins](https://www.jenkins.io/) pour son puissant système CI/CD.
- Équipes Docker et Docker Compose pour les outils de conteneurisation.
- Communautés Gitea, Jenkins, et MariaDB pour leurs images Docker officielles.

---

*Construit avec ❤️ pour une gestion de code et CI/CD autohébergée. Si ce projet vous est utile, mettez une étoile au dépôt !*