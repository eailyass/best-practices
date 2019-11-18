# Global cheatsheet


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
	créer entité: make:entity
	créer migration: make:migration
	montre ce qui va changer dans la bdd: doctrine:migrations:migrate --write-sql
	effectuer la migration: doctrine:migrations:migrate
	
