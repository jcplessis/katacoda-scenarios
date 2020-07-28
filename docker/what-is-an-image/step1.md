Une image docker c'est un fichier _tar_ qui contient des fichiers _tar_.
Chaque _tar_ correspond à une couche, une fois tous les _tar_ extrait à un même endroit on obtien le filesystem de notre container.

Commençons par télécharger une image :

`docker pull redis:3.2.11-alpine`{{execute}}

Exportons la :

`docker save redis:3.2.11-alpine > redis.tar`{{execute}}

Puis extrayons la :

`tar -xvf redis.tar`{{execute}}

On voit maintenant le contenu avec les layers et les metadata :

`ll`{{execute}}

`cat repositories`{{execute}}

`cat manifest.json`{{execute}}

On peut en extraire une couche pour retrouver notre filesystem :

`tar -xvf da2a73e79c2ccb87834d7ce3e43d274a750177fe6527ea3f8492d08d3bb0123c/layer.tar`{{execute}}