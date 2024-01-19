# docker-apache-starter_kit

Kit de démarrage pour vos projets web statiques

## Contexte 

Le répertoire `mon-projet` contient la base pour créer un projet web statique

## Utilisation

Dans le cadre de la formation, vous allez travailler sur des exercices et projets web.

La 1ère partie est consacrée au web "statique" (HTML, CSS et JS client). Pour exécuter vos pages web dans un environnement "http", vous allez créer un container "docker" contenant le serveur web "Apache".

## Prérequis

1. Posséder un compte sur [Docker HUB](https://hub.docker.com).
2. Avoir "[Docker Desktop](https://www.docker.com/products/docker-desktop/)" installé sur votre ordinateur.

## Étapes de construction d'un projet web statique

1. Créer un dossier pour votre projet
2. Dans ce dossier: 
    1. Créer un fichier `README.md` qui contiendra un descriptif du projet.
    2. Créer un fichier `docker-compose.yml` qui contiendra la configuration du conteneur exécutant le serveur web Apache.
    3. Créer 1 sous-dossier "www" qui contiendra les pages web du projet. Dans ce dossier, créer un fichier `index.html` qui sera le point d'entrée de votre projet.

    Votre arborescence ressemble alors à celle présente dans le dossier `mon-projet` de ce dépôt.

## docker.compose.yml

Le fichier docker-compose décrit et configure les composants nécessaires au conteneur.

```yml
name: monprojet-serveur-web
services:
  apache: 
    image: httpd 
    container_name: monprojet-apache
    restart: always 
    volumes: 
      - './www:/usr/local/apache2/htdocs'
    ports: 
      - '3000:80'
```
## Démarrer le conteneur : 

Ouvrir un terminal et se positionner dans le répertoire qui contient le docker-compose.yml.

Taper la commande : `docker compose up` pour démarrer le conteneur.

## Explications du docker-compose.yml

`name: mon-projet-serveur-web` : C'est le nom de votre conteneur.

`services: ` : déclare une section qu icontiendra les applicatifs de votre conteneur.

`apache` : déclaration d'un 1er service nommé apache. Vous pouvez choisir le nom qui vous convient.

`image: httpd` : l'image utilisée par le service apache. Si elle n'est pas disponible sur votre PC, Docker la téléchargera automatiquement au 1er démarrage du conteneur depuis le docker hub.

`container_name: monprojet-apache` : C'est le nom du conteneur du service apache. Il aparaitra comme "sous-conteneur" de votre conteneur principal (ici nommé monprojet-serveur-web).

`restart: always` : permet au conteneur de redémarrer automatiquement 

```yml
volumes: 
      - './www:/usr/local/apache2/htdocs'
```
Déclare les volumes du conteneur. Dans cet exemple, fait le lien entre le répertoire local `./www` et le répertoire de travail du serveur web `/usr/local/apache2/htdocs`. Du point de vue du conteneur, c'est comme si le contenu de votre dossier local `./www` était situé dans le répertoire du conteneur `/usr/local/apache2/htdocs`.

```yml
ports: 
      - '3000:80'
```
Expose le port 3000 et le lie au port 80 du conteneur.

Le port 3000 est le port utilisé pour accéder au site web.
Le port 80 est le port utilisé par le conteneur.

Vous accédez à l'application via [http://localhost:3000](http://localhost:3000).

