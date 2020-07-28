# Processus

Pour commencer lançons un container _redis_ :

`docker run -d --name=db redis:alpine`{{execute}}

Ce container lance un process qui s'appelle _redis-server_. Du point de vue de l'hôte ce processus est visible.

`ps aux | grep redis-server`{{execute}}

On peut aussi demander à docker quels sont les process lancés par un container : 

`docker top db`{{execute}}

On pourrait chercher quel est le processus parent de ce processus et on verrait probablement qu'il s'agit de _docker-containerd_.

On peut aussi regarder en détail toute l'arborescense des processus enfants de _dockerd_ pour voir les containers :

`pstree -c -p -A $(pgrep dockerd)`{{execute}}

# Répertoires

On peut aller dans le répertoire /proc, et rechercher les fichiers de configuration de notre processus _redis_.

`DBPID=$(pgrep redis-server)
echo Redis is $DBPID
ls /proc/$DBPID`{{execute}}

On y trouverait par exemple ses variable d'environnement :
`cat /proc/$DBPID/environ`{{execute}}

Qu'on peut comparer à ce que le container voit réellement :
`docker exec -it db env`{{execute}}

