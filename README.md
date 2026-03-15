
# Projet MicroPilot

Ce dépôt Git permet de regrouper les ressources autour de la suite de vidéos [On développe une application de A à Z](https://www.youtube.com/watch?v=Y-V2_igRZBE&list=PLznEpxSFntoAawwp6X9Xuem7mZuhU0XMs&pp=sAgC) (MicroPilot).

## Présentation du projet
Le projet consiste en une suite de vidéos pour construire une application de gestion de micro-entreprise : gestion de contrats avec des périodes de prestation, suivi des factures et encaissement, suivi des comptes.

### Vidéo #01 - Maquettage Figma
Dans la première vidéo de la série, je vous présente le projet et le besoin. Puis on réalise les premiers écrans sur Figma : Page d'accueil, liste des contrats, détail d'un contrat, ...

Dans cette vidéo, je vous montre comment utiliser les layouts, créer des composants paramétrés, prototyper les interactions entre écrans.

Vidéo : https://www.youtube.com/watch?v=sxPAMq30KAA

### Vidéo #02 - Hébergement Proxmox
Dans la seconde vidéo, je vous montre comment monter un hébergement chez soi. 

On installe Proxmox sur un mini PC, on le configure, je vous présente les Community Scripts, on crée un nom de domaine avec Cloudflare, on installe un conteneur Nginx Proxy Manager et on configure un tunnel Cloudflared chiffré de bout en bout.

Vidéo : https://www.youtube.com/watch?v=VLDoywg4ZQw

### Vidéo #03 - Serveur d'identité Authentik
Dans cette troisième vidéo, je vous parle des bénéfices d'un serveur d'identité, des solutions qui existent, de l'installation de la solution Authentik, de sa configuration, et de sa personnalisation.

Vidéo : à venir

### Vidéo #04 - Base de données
Dans la quatrième vidéo de la série, on va concevoir la base de données en réalisant un modèle conceptuel de données (MCD) avec explications sur les concepts clés.

On va ensuite installer SQL Server 2025 sous forme de conteneur et créer la base de données associée.

Vidéo : à venir

### Vidéo #05 - Création de l'API
C'est dans cette cinquiète vidéo qu'on va créer l'API REST avec ASP.NET Web API et .NET 10. On va voir comment générer la documentation, gérer l'authentification, et développer les premiers contrôleurs et tests unitaires.

Vidéo : à venir

### Vidéo #06 - Création de l'application
Dans cette dernière vidéo du plan principal, on va créer l'application Blazor Web Assembly (wasm) avec .NET 10, en sollicitant une authentification auprès de notre serveur d'identité.

On verra comment organiser notre code, découper en composants, et on réalisera ensemble les premières fonctionnalités de l'application.

Vidéo : à venir

### Vidéos bonus
Une fois le plan principal réalisé, on pourra tenter d'explorer des axes d'amélioration :
- Intégration de CI/CD (Hébergement d'un Gitlab ?)
- Analyse des PDF de contrats par IA pour les créer automatiquement dans l'application
- ...
