Symfony best practices:
====

## Installation:
* Use composer and Symfony flex
* Symfony flex used to automated some tasks used in symfony


## Configuration:
* .env
    - Contient les informations d'environnement qui ne sont pas liées à l'application (base de donnée...)
    - déclaration de la Bdd: DATABASE_URL="mysql://username:pwd@127.0.0.1:3306/db_name"

* services.yml:

		Les configurations liées à l'application
		Si une valeur reste toujours constante, vaut mieux la déclarer en tant que "const" dans une classe que la déclarer dans le fichier services.
		les services sont automatiquement déclarés (symfony 3.3) sauf dans le cas ou il faut ajouter certains parametres ==> all controllers are services by default
		si l'objet necessite des variables pour la construction, elles ne doivent plus être déclarées dans le dossier services.yml comme arguments, mais peuvent directement être déclrées dans le constructeur et "type-hinted", l'autowiring s'occupe du reste.


## Services: (avant symfoy "3.3")
* service container
  * il suffit de créer un objet ds le dossier services pr qu'il soit accessible.
  * si l'objet necessite des variables pour la construction, elles doivent être déclarées dans le fichier services.yml

## Controllers (version 4):
* symfony suit la règle de "thin controllers" "fat models" ===> les controleurs doivent contenir le juste nécessaire
* le suffixe "action" n'est plus recommandé
* Les routes sont déclarées en tant qu'annotations (déclarer type:annotation dans le fichier config/routes.yml)

## Templates (version 4):

* Dossier /templates
* tous les fichiers twig sont desormais centralisés dans ce même dossier pour simplifier la tache 
* lowercase snake_cased names pour les fichiers twig
* Les extensions twig sont des classes php qui étendent la classe Twig\Extension\AbstractExtension et qui sont déclarées dans le dossier /src/Twig  ils servent à ajouter de nouveaux filtres et fonctionnalités à twig

## security symfony:
 	security.yaml => use bcrypt instead of sha-512
 	use @security annotation
 	providers: 
 	firewalls:

## Translation:
 app/config/config.yml
  translator: { fallbacks: ['%locale%'] }
  app/config/parameters.yml
  	parameters:
    locale:     en

## Components:
1. install: composer require symfony/extName
	2. validator component
    3. LDAP component
	4. Console component:
	 	Create a command under symfony:
	 		- Create class in "command" directory under bundle.
	 		- name with Command suffix.
	 		- use configure() function then execute() function
	5. Security component
	6. HTTPFoundation component:
	 		- Request
	 		- Response
	 		- Cache management

## Controllers:
	Thin controller fat model
	use paramconverter 

## Service container:
	$container->get('service_id')
	Lazy loading
## Doctrine:
	Lazy loading	
### Fixtures
créer des fixtures make:fixtures
executer fixtures doctrine:fixtures:load
créer des fixtures sans purger la bdd --append
créer des fixtures pour une classe bien définie --group=NomDeLaFixture 


# API:
## Serializer:
* JMSSerialiser
* Resonse::HTTP_NOT_FOUND
* LexikJWTAUthentificator

## FOSRESTBundle:

### Gestion des routes:

#### annotations:
```
	@Rest\post(
	path= "routePath",
	name= "routeName",
	requirements: {}
	)
	@Rest\get...
```
#### Serialisation:
```
- activer le body_converter
- ajouter la config:
	format_listener:
	    rules:
	        - { path: '^/', priorities: ['json'], fallback_format: 'json' }  (permet de définir les paths et le format à utiliser)

	fos_rest:
	    view:
	        view_response_listener: true	(permet de récupérer l'objet retourné et le sérialiser puis envoyer un status code)

- Ajouter l'annotation @View (
	statusCode = 201,
    serializerGroups = {"POST_CREATE"}
	)
```

#### Négociation de contenu:
   permet au client de demander le format de données, la lanqgue et le charset de sa requête...

#### Déserialisation:
- par paramConverter ou bien par formulaire
  - Cas de paramConverter:

```
-Activer le paramConverter et le bodyConverter:
	sensio_framework_extra:
	request: { converters: true }

fos_rest:
    body_converter:
        enabled: true  (permet la converstion de JSON à un objet)
- Ajouter l'annotation @paramConverter
@ParamConverter("article", converter="fos_rest.request_body")
```
  - Cas de formulaire:
				
créer forms<br>
Traitement des requêtes GET et POST:
- QueryParam pour les GET
- RequestParam pour les POST




Symfony 4.1
		Monolog
		Surcouche - startekit: tout api hérite d'une classe
		Standardisation
		Doctrine : DQL - 
		Integration continue : junkins automatiser le build et les tests.
		hebergement aws 
		docker 
		securité: se focaliser sur le back office. API.







Mission principale:
TBD

Salaire Brut: 
	3400 mensuel * 12,12
	

Congé:
24 jours
Avantages sociaux et en nature:

	Tickets restaurant: 10,86 ticket restau. = 2400e annuel
	Pass navigo : 100%
	Forfait telephone: 20 euros/ mois
	Mutuelle 100%
	Prime de cooptation: 1500e Brute