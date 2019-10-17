# Astuces Ubuntu:
-----
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
### 
