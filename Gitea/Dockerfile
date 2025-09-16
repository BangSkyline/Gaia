# Image officielle Gitea
FROM gitea/gitea:1.22

# Définir les variables d'environnement
ENV USER_UID=1000
ENV USER_GID=1000

# Configuration Gitea via variables (format INI en double underscore)
ENV GITEA__database__DB_TYPE=postgres
ENV GITEA__database__HOST=gitea-db:5432
ENV GITEA__database__NAME=gitea
ENV GITEA__database__USER=gitea
ENV GITEA__database__PASSWD=gitea_pass
ENV GITEA__server__DOMAIN=localhost:
ENV GITEA__server__HTTP_PORT=3000
ENV GITEA__server__ROOT_URL=http://192.168.95.65/

# Exposer le port HTTP (Gitea)
EXPOSE 3000
