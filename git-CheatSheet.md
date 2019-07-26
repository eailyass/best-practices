## Commandes de logs:

git log ==> tous les commits
git log --oneline ==> les commits sur 1 seule ligne
git log -n ==> les n derniers commits
git log -p filename ==> les commits sur un seul fichier

## Commande checkout:

git checkout "commitId" ==> retour dans le commit en question pour visualiser. aucune modif n'est prise en charge dans le master head
git checkout "commitId" "fileName" ==> Modifier un fichier dans un commit particulier avec prise en charge dans le master head

## Commande revert:

git revert "commitId" ==> annuler le commit en question
git revert "commitId" "fileName" ==> annuler le commit dans un fichier particulier