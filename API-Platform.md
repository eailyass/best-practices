# API Platform
Après création des entités et des relations entre elles, on installe API Platform via la commande:
composer req api-platform/core  Ou composer req api-platform/api-pack

## 1. Gérer une entité via API Platform 

- Ajouter l'annotation @ApiRessource() au début de l'entité, puis toutes nos routes sont générées de manière automatique.
- ou bien lors de la création de l'entité: php bin/console make:entity --api-resource
- Les opérations de CRUD sont automatiquement gérées et on distingue entre deux opérations: les collections et les items où:
  * Collections contient: Get de tous les éléments + Post pour créer un nouvel élément.
  * Items contient: les opérations RUD sur un élément.
- Il est possible de gérer manuellement chaque opération via les annotations @collectionOperations et itemsOperations.
  * @ApiRessource(
  collectionOperations={"get"},
  itemsOperations={"put","delete",..} )
- Ces deux annotations sont complétement séparées.
- Ces annotations permettent aussi de surcharger les routes par défaut itemsOperations={"get"={"methode"="GET", "path"="/our/customized/path", "requirements" = ""...}}

### Interface de description:
C'est une interface incluse dans api-platform qui nous permet d'explorer notre api. Elle respecte les normes OpenAPI et permet d'effectuer des taches crud sur notre bdd.

 - Si on a besoin d'y effectuer une requête post, il suffit d'envoyer notre objet json dans le champ dédié.
 - Si notre objet Foo comporte une relation avec un objet Bar, il faut spécifier `l'IRI` de ce dernier dans le json:
  ```json
    {
      "attribut1":"valeurString",
      "attribut2":"valeurString",
      "attribut3":204,
      "attribut-relation":"/api/Bars/<id>",
    }
  ```

## 2. Opérations sur les ressources:
### a. Appliquer un tri par défaut:
Ajouter l'annotation attributes->Order dans @ApiRessource(
attributes= {
	"order" = {
	"champ1" : "Asc/Desc", "champ2" : "Asc/Desc"..
	}
})

### b. Gestion des filtres:
#### 1. SearchFilter:
Ajouter l'annotation @ApiFilter(
	SearchFilter::class,
	properties={
	"attribut1":""
	"attribut2":""
	})
#### 2. RangeFilter:
Ajouter l'annotation @ApiFilter(
	RangeFilter::class,
	properties={
	"attribut1":""
	"attribut2":""
	})
Appeler la méthode via le GET : path/to/resource?attribut1[gt|lt|between...]=valeur
#### 3. OrderFilter:
Similaire à [l'annotation order ci-dessus.](#a-appliquer-un-tri-par-défaut) mais fait partie de l'annotation @ApiFilter

## 3. La gestion de l'authentification JWT:
- JWT = Json web token. C'est un token envoyé à chaque transaction par l'utilisateur. Il se compose des éléments suivants sous format JSON:
  * Header: contient l'algorithme de cryptage "HS256" + le type "JWT"
  * Payload: contient le username "name", et peut contenir d'autres informations comme le timestamp de création "iat" et celui d'expiration "exp" 
  * Signature: le token généré.
- Cette gestion est faite via le LexikJWTAuthentificationBundle. Besoin d'un secret_key, public_key, passphrase et token_ttl(nbr de secondes de validité du token). Ils sont déclarés dans le fichier de config yml et initialisés dans le fichier .env. Ces clés sont de type pem, générées par la commande suivante:
  * Clé privée: "openssl genrsa -out /chemin/vers/cle-prive.pem -aes256 4096" puis taper la passphrase
  * Clé publique: "openssl rsa -pubout -in /chemin/vers/cle-prive.pem -out /chemin/vers/cle-publique.pem -aes256 4096" puis taper la passphrase
  * modifier la passphrase dans le fichier .env
- Il faut par la suite configurer le fichier security.yml, modifier le providers et le firewall:
   firewall:
      api:
         pattern: ^/pattern/to/api
         statless:true
         json_login:
            check_path: /path/check (penser à créer cette route dans le dossier routes) \
            success_handler: lexik_jwt_authentication.hadnler.authentication_success\
            failure_handler: lexik_jwt_authentication.hadnler.authentication_failure\
         guard:\
            authenticators:\
            - lexik_jwt_authentication.jwt_token_authenticator