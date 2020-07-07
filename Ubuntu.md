# Astuces Ubuntu:
-----

## Anatomie et gestion de fichiers:
### Anatomie ubuntu:
### Gestion des fichiers:

**Recherche**:
* find <'chemin de recherche'> -name <nom> -type d(pour directory)/f(pour file)

## Gestion de la mémoire:

**Afficher l'état de mémoire**: free -m

### Ajouter de la mémoire swap:
swap est une zone d'un disque dur faisant partie de la mémoire virtuelle. Il est conseillé que la taille du swap soit entre x1 et x2 fois la taille de sa RAM. Dans Ubuntu, swap se trouve généralement sous une forme de partition de disque dur – on parle alors de partition d'échange. Il peut aussi se présenter sous forme de fichier – on parle alors de fichier d'échange. Ce mode est le plus conseillé.

**Créer un fichier swap**: sudo fallocate -l (taille du fichier) (nom du fichier)

**Attribuer les droits nécessaies**: sudo chmod 600 (nom du fichier)

**Définir le fichier créé en tant qu'espace swap**: sudo mkswap (nom du fichier)

**Activer le fichier swap**: sudo swapon (nom du fichier)

**Rendre le fichier disponible au démarange en ajoutant cette ligne au fichier fstab**: (chemin du fichier) none swap sw 0 0 

## Gestion du stockage:

**Afficher les différentes partitions**: sudo fdisk -l [Lister les partitions] /dev/sda [modifier la partition] Comme on peut utiliser df -h
**Formater une partition**: sudo mkfs [type de file system ex: ext4] [nom de la partition /dev/sdXX]

### Etendre/Créer une partition:
Pour étendre ou créer un partition il faut télécharger une iso de l'outil "gparted" puis booter via cette iso. Un outil graphique permet d'effectuer le nécessaire.

Par la suite on boot normalement puis il on retrouve l'espace étendu si on utilise la commande fdisk -l. Cependant, la partie étendue a été ajoutée de manière physique mais il faut l'ajouter de manière logique. Pour cela il est nécessaire de passer par les commandes suivantes:

**Afficher le path du volume logique**: sudo lvdisplay  (récupérer la donnée path)

**Etendre le volume logique**: sudo lvextend -L +20G path/du/LV (ajoute 20 Go au LV)

**Redimentionner le volume**: sudo resize2fs path/du/LV

## Manipuler SSH:
### Se connecter via SSH:
### Transfert de fichiers via SSH:
## Manipuler tar et gzip:

## Gestion des utilisateurs:

**Afficher les utilisateurs:** users

**ajouter des utilisateurs:** sudo adduser 'username'

**ajouter un utilisateur à un groupe:** sudo adduser 'username' 'groupname' (permet d'ajouter un user au group root pour des droits sudo)

**Modifier un mot de passe**: sudo passwd 'username'

**Supprimer un utilisateur:** sudo deluser 'username'

## Gestion des packets:

Les packets servent pour assurer la mise à jour du système. Ils sont régulièrement téléchargés et mis à jour depuis les serveurs ubuntu. L'installation de ses packets se fait via `apt` ou `apt-get` et même avec `dpkg`.
Les liens vers les packets sont enregistrés dans le fichier `sources.list` qui se trouve dans le dossier `/etc/apt/`

### La gestion par apt / apt-get:
apt ou apt-get est le gestionnaire de packets sur ubuntu il permet plusieurs fonctionnalités, les deux commandes sont quasi similaires avec quelques différences comme la prise en charge des regex avec apt-get. C'est à dire `apt-get install php*` permet d'installer tous les packets qui commencent par php tandis que avec apt ça ne fonctionne pas.

* apt-get update : permet de mettre à jour le chache des sources.

* apt-get upgrade: permet de mettre à jour toutes les applications du système.

* apt-get install/remove <nom_de_packet>: permet d'installer/supprimer un packet spécifique.

* apt-get -y install <nom_de_packet>: permet de répondre automatiquement par 'oui' sur toutes les interaction pouvant intervenir lors de l'installation (utile pour automatiser les install sans intervention de l'user).

#### apt-mark:

Cette commande permet de gérer les packets à mettre à jour ou non de manière manuelle. Si on veut qu'un packet ne se mette pas a jour lors du `apt-upgrade` on utilise cette commande:
* apt-mark hold <nom_du_packet> : ignorer la maj de ce packet.
* apt-mark showhold : afficher tous les packets dont la maj est ignorée.

## La commande curl:
C'est à la fois une bibliothèque et une cli, qui permet de créer des requêtes en plusieurs protocoles dont http et ftp. La commande de base est `curl www.example.com`
**Télécharger un fichier:** `curl www.example.com/path-to-file`
**Télécharger et changer le nom:** `curl -o <fileName1> www.example.com/path-to-file`