## Gestion de la config de base:
* git config --global -l => liste la config
* git config --global user.name "username" => définir l'utilisateur.
* git config --global core.editor code|subl... => définir l'éditeur de texte par défaut.

### Gestion des accès sur linux:
* git config --global credential.helper.store puis git pull => enregistrer l'id et mdp
* si les eaccès changent, la communication avec le serveur va échouer et git va redemander les nouveaux accès

## Gestion des repos:
* git remote -v ==> permet de voir les liens de repos distants.

### Modification d'un repo distant:
Dans le cas ou le serveur distant est migré par exemple!
git remote set-url "nom distant (origin)" "nouveau lien (le même utilisé dans git clone)"

## Commandes de logs:

* git log ==> tous les commits
* git log --oneline ==> les commits sur 1 seule ligne
* git log -n ==> les n derniers commits
* git log -p filename ==> les commits sur un seul fichier

## Commande checkout:
Permet un retour sur un commit pour visualiser:

* git checkout "commitId" ==> retour dans le commit en question pour visualiser. aucune modif n'est prise en charge dans le master head
* git checkout "commitId" "fileName" ==> Modifier un fichier dans un commit particulier avec prise en charge dans le master head *permet aussi de récupérer un fichier récemment supprimé* 

## Commande revert:
Permet d'annuler un commit:

* git revert "commitId" ==> annuler le commit en question
* git revert "commitId" "fileName" ==> annuler le commit dans un fichier particulier

## Commande reset:

Permet de supprimer les commits. Ou encore de forcer le "head" à se mettre sur un commit spécifique
  - git reset "commitId" [--mixed] ==> supprimer les commits après le "commitId", garde les modifs sur les fichiers sans les stagger.
  - git reset "commitId" --soft ==> supprimer les commits après le "commitId" mais garde les changements apportés aux fichiers un nouveau commit permet de persister
  - git reset "commitId" --hard ==> supprimer les commits après le "commitId" et efface les modifications sur tous les fichers modifiés après les commitId
  - git reset --hard "branch_name" ==> force la branche à adopter le même historique de commits que "branch_name" est utile si on veut absolument faire ressembler notre branche à "branche_name" (mieux qu'un pull --force)

## Commande rebase:
Permet d'intègrer les modifications de la branche mère dans celles d'une branche `feature` sans écraser les commit de cette dernière. C'est une sorte de mixage entre les modifications des deux branches.
  - git checkout `feature`  git rebase `master` => se positionner sur la branche et faire un rebase sur la branche principale.
  - S'il y a des confilts il faut les traiter manuellement puis faire git rebase --continue

## Commande restore:

 permet d'annuler les modifications sur un fichier

 - git restore "fichier" => annule les modification sur un fichier (eq à git checkout "fichier")
- git restore --staged "path" => pour désindexer un path ajouté à l'index avec un git add (annule l'effet du git add sur un path)

## Gestion des branches:

- git branch "branch_name" ==> permet de créer une nouvelle branche.
- git checkout "branch_name" ==> permet de fixer le pointeur sur la branche créer pour travailler dessus.
- git push origin "branch_name" ==> effectuer un push sur notre branche

### Merger la branche avec la master:
- git checkout master ==> se positionner sur la branche master.
- git merge "branch_name" ==> fusionner la branche dev dans le master.
- git push origin master => pusher les modifications du merge vers le serveur.

## Gestion des conflits:
- Une fois deux développeurs travaillent en local sur le même fichier en même temps (même branche ou branches différents) - un conflit est créé lors du pull, il faut le régler manuellement dans le fichier.

### La commande blame
- git blame "fileName.ext" ==> Des fois, on a besoin de savoir qui a modifié un fichier, on peut passer par cette commande qui nous liste toutes les modifs avec le nom d'utilisateur à côté

## Gestion d'un nouveau projet:
Un projet est géré selon plusieurs cas de figure

##Modifier un commit:

### Modifier le dernier commit:
- git commit --amend: Si on a fait un commit puis on s'est souvenu qu'il fallait modifier le message et/ou les fichiers qu'on a "commit". Un éditeur s'ouvre avec le message du commit qu'on peut modifier, et si on a "add" de nouveaux fichier ils seront ajoutés au commit.
