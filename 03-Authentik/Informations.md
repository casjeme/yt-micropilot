# Vidéo #03 - Serveur d'identité Authentik

Ces ressources sont en lien avec la vidéo de la série de vidéos [On développe une application de A à Z](https://www.youtube.com/watch?v=Y-V2_igRZBE&list=PLznEpxSFntoAawwp6X9Xuem7mZuhU0XMs&pp=sAgC) (MicroPilot) : [Authentik : le serveur d'identité SSO open source](https://www.youtube.com/watch?v=VLDoywg4ZQw).

## Liens utiles
- [Authentik](https://goauthentik.io/) : site officiel
- [Community Scripts Generator - Docker](https://community-scripts.org/generator?script=docker) : générateur du script Docker pour le personnaliser
- [Installation Authentik](https://docs.goauthentik.io/install-config/install/docker-compose/) : documentation officielle pour l'installation

## Création du conteneur LXC Docker
Rendez-vous sur [le générateur community-script.org](https://community-scripts.org/generator?script=docker) pour créer un script personnalisé d'installation du conteneur LXC Docker. Pour rappel sur la config recommandée : 
- CPU : 2 Coeurs
- RAM : 4 à 6 Go
- Disque : 16 à 20Go

Ou copiez directement la ligne de commande suivante et collez-là dans le Shell Proxmox :
```bash
# Conteneur (2 CPU Cores, 4Go de RAM, 20Go de disque, conteneur LXC nommé "authentik")
mode=generated var_cpu="2" var_ram="4096" var_disk="20" var_hostname="authentik" bash -c "$(curl -fsSL https://raw.githubusercontent.com/community-scripts/ProxmoxVE/main/ct/docker.sh)"
```
Puis rendez-vous sur le conteneur, dans la Console, et vérifiez la présence de Docker et Docker Compose avec les commandes
```bash
docker --version
docker compose version
```
## Installation Authentik
Une fois Docker disponible, créez un dossier /opt/authentik :
```bash
mkdir -p /opt/authentik
cd /opt/authentik
```
Puis téléchargez le fichier docker-compose.yml officiel :
```bash
wget https://goauthentik.io/docker-compose.yml
```
Générez les secrets nécessaires dans un fichier `.env` :
```bash
# Génération du mot de passe PostgreSQL
echo "PG_PASS=$(openssl rand -base64 36 | tr -d '\n')" >> .env
# Génération de la clé secrète Authentik
echo "AUTHENTIK_SECRET_KEY=$(openssl rand -base64 60 | tr -d '\n')" >> .env
```
Vous pouvez ouvrir le fichier `.env` pour constater la bonne prise en compte :
```bash
nano .env
```
Le contenu du fichier peut contenir les paramètres suivants :
```env
# Secrets (générés automatiquement)
PG_PASS=<votre_mot_de_passe_généré>
AUTHENTIK_SECRET_KEY=<votre_clé_secrète_générée>

# Ports (optionnel — à personnaliser si besoin)
# COMPOSE_PORT_HTTP=9000
# COMPOSE_PORT_HTTPS=9443

# Email (recommandé pour les notifications admin)
# AUTHENTIK_EMAIL__HOST=smtp.example.com
# AUTHENTIK_EMAIL__PORT=587
# AUTHENTIK_EMAIL__USERNAME=notifications@example.com
# AUTHENTIK_EMAIL__PASSWORD=motdepasse_smtp
# AUTHENTIK_EMAIL__USE_TLS=true
# AUTHENTIK_EMAIL__FROM=authentik@example.com
```
Comme d'habitude faites `Ctrl + O` pour enregistrer le fichier puis `Enter`, et `Ctrl + X` pour quitter.

Enfin, faites-monter le docker-compose avec :
```bash
docker compose pull
docker compose up -d
```
Vous pouvez alors vous rendre sur `https://(votre-ip):9443/if/flow/initial-setup/` (attention, le `/` à la fin est important, sinon vous aurez une erreur 404).