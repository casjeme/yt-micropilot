# Vidéo #02 - Hébergement Proxmox
Ces ressources sont en lien avec la vidéo de la série de vidéos [On développe une application de A à Z](https://www.youtube.com/watch?v=Y-V2_igRZBE&list=PLznEpxSFntoAawwp6X9Xuem7mZuhU0XMs&pp=sAgC) (MicroPilot) : [Hébergement à la maison avec Proxmox](https://www.youtube.com/watch?v=VLDoywg4ZQw).

## Liens utiles
- [Proxmox VE](https://www.proxmox.com/en/downloads/proxmox-virtual-environment/iso) : téléchargement de l'iso d'installation
- [Rufus](https://rufus.ie/fr/) : création du média d'installation USB
- [Community Scripts](https://community-scripts.org/) : scripts d'administration de Proxmox
- [Cloudflare](https://www.cloudflare.com/fr-fr/) : création du nom de domaine
- [Certificat intermédiaire Cloudflare](https://developers.cloudflare.com/ssl/static/origin_ca_rsa_root.pem) : fichier à télécharger pour "Intermediate Certificate" lors de la création d'un certificat sur Nginx Proxy Manager.

## Installation de Cloudflared
Tapez les commandes suivantes pour télécharger et installer le package Cloudflared :
```bash
# Télécharger et installer le paquet
curl -L --output cloudflared.deb https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64.deb
dpkg -i cloudflared.deb

# Vérifier l'installation
cloudflared --version
```
Puis connectez-vous avec la commande :
```bash
cloudflared tunnel login
```
Pour créer le tunnel :
```bash
cloudflared tunnel create npm-tunnel
```
Pour créer le fichier de configuration :
```bash
mkdir -p /etc/cloudflared
nano /etc/cloudflared/config.yml
```
Contenu du fichier de configuration :
```yaml
tunnel: <TUNNEL-ID>
credentials-file: /root/.cloudflared/<TUNNEL-ID>.json

ingress:
  - hostname: "*.exemple.fr"
    service: https://localhost:443
    originRequest:
      noTLSVerify: false
      originServerName: www.exemple.fr
  - service: http_status:404
```
Pour créer l'entrée DNS sur Cloudflare :
```bash
cloudflared tunnel route dns npm-tunnel "*.exemple.fr"
```
Pour installer et activer le service Cloudflared :
```bash
cloudflared --config /etc/cloudflared/config.yml service install
systemctl enable cloudflared
systemctl start cloudflared
```