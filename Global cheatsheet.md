# Global cheatsheet


## MySQL:
	login command: mysql -u username -p
	know variables (port, host, charset...): show variables  (after login)


## Doctrine:
	Generate database : doctrine:create:database
	créer entité: make:entity
	créer migration: make:migration
	montre ce qui va changer dans la bdd: doctrine:migrations:migrate --write-sql
	effectuer la migration: doctrine:migrations:migrate
	
