# Database


## MySQL:
	login command: mysql -u username -p
	know variables (port, host, charset...): show variables  (after login)

	exporter le résultat d'une requête vers un CSV:
	
```sql
	SELECT ......

	INTO OUTFILE '/var/lib/mysql-files/fileName.csv'
	FIELDS TERMINATED BY ';'
	ENCLOSED BY '"'
	LINES TERMINATED BY '\n';
```
``Le dossier d'export du fichier doit être exactement celui dans l'exemple sinon on obtient une érreur '--secure-file-priv'``



## Doctrine:
	Generate database : doctrine:create:database
	Créer entité: make:entity
	Créer migration: make:migration
	Montre ce qui va changer dans la bdd: doctrine:migrations:migrate --write-sql
	Effectuer la migration: doctrine:migrations:migrate
	Annuler une migration (le fichier Version1254586558 par expl): doctrine:migration:execute --down 1254586558

## Postgres:

### Commandes de base:

psql -d 'database_name' -U 'username' -W : Se connecter à une bdd.

	Rattacher une sequence à l'ID d'une table
```sql
		alter table ....
		alter column id set default nextval('...._id_seq');
```