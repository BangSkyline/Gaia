# Image officielle Jenkins LTS
FROM jenkins/jenkins:lts

# Définir des variables d'environnement
ENV JAVA_OPTS="-Djenkins.install.runSetupWizard=false"

# Optionnel : installer des outils ou plugins de base
# Exemple : git, curl, jq (utile dans les pipelines)
USER root
RUN apt-get update && apt-get install -y git curl jq && rm -rf /var/lib/apt/lists/*

# Revenir à l'utilisateur jenkins pour la sécurité
USER jenkins

# Exposer les ports (déjà exposés dans l'image de base, mais explicite)
EXPOSE 84 50000
