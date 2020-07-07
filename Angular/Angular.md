# Angular

## Demarrer un nouveau projet:

- Installer nodejs
- Installer npm
- Installer angular cli via npm
- Créer un projet: ng new "project-name"
- Lancer le serveur `ng serve --open`

## Anatomie d'un projet angular:

installer un package => utiliser npm (fichier ajouté dans package.json)
définir le lien vers le fichier de style (css, bootstrap...) dans angular.json
fichier app.module.ts ?
le dossier src contient nos fichiers de dev

### app.module.ts:
C'est le fichier qui permet de déclarer la configuration de notre projet, surtout via le décorateur @ngModule. Ce décorateur est une fonction qui prend en paramètre un objet ou on déclare principalement les éléments suivants:
* imports: les modules angular utilisés dans notre projet
* declarations: les components créés par les dev
* boostrap: le component racine de notre projet (par défaut: AppComponent)

### main.ts:
Le fichier responsable sur le paramétrage du démarrage de notre app. Il permet de:
* Determiner l'environnement (prod, dev...)
* Instancier le module `platformBrowserDynamic`  par le component racine `AppComponent`

### Component et son anatomie:

chaque component se compose de 3 fichiers principaux html, css et ts 
- Pour genérer son propre component, executer la commande `ng generate component <component_name>`.
Le fichier principal est ``componentName.component.ts``, il contient les éléments suivants:
 * ``export class ComponentName`` : export permet aux autres components d'utiliseer celui-ci
 * ``@Component()`` : un decorateur sous forme de fonction qui accepte un objet, ou on mentionne:
 	`
 	selector: 'le-selecteur' // le nom que va porter la directive de ce component dans les html du projet
 	template|templateUrl: 'code html | lien vers html'
 	styles|styleUrls : ['code css']|['lien1 vers css, lien2...']
 	`


## Data binding:

### property binding => [] - (mettre une propriété html entre crochets) : [propriété] = "variable TS"
string interpolation/ one-way-binding : {{ variable typescript }}

### evenement binding:
 (event)= "function" <--> TS function 

### two way binding:
appelé aussi "banana in a box", permet d'effectuer un binding dans les deux sens et a pour effet de modifier un élément du DOM en meme temps qu'en saisie. ``[(propriété)]``




décorateur


## Les directives:

### Structurelles:
	* \*ngIf: Appliquer une condition sur un élément. ``<balise-html *ngIf="expression_logique; [else #reference] "></balise-html> ``
	L'expression logique peut être n'importe quelle expression JS ie variable, booleen, fonction...
		* Elvis opérateur: un shorthand de *ngIf qui consiste à ajouter un '?' devant unvariable pour ne pas l'afficher si elle est undefined.
	* \*ngFor : appliquer une boucle for sur un élément. ``<ng-element *ngFor=" let element of Array; [facultatifs]"></ng-element> ``
	peut accepter des paramètres facultatifs comme:
		* index: l'index de l'élement en cours, qui s'incrémente à chaque itération.
		* first: boolean qui est true lors du premier élément.
		* last: boolean qui est true lors du dernier élément.
		* odd:
		* even: 
### par attribut:
	*[ngStyle]: permet d'appliquer un style de manière conditionnelle aussi, accepte un objet ou une fonction.
	*[ngClass]: Principalement pour le styling conditionnel ``<balise-html [ngClass]="'classe1 classe2' ou un array ['classe1', 'classe2',...] ou un objet {'classe1':true, 'classe2':false,...} ou une fonction qui retourne les classes à mettre (recommandé) 'classeAppliquer()'"></balise-html> ``
	*[ngSwitch]: permet d'afficher/masquer des elements du DOM selon une condition `` <balise-html [ngSwitch]="variable">
		<balise-html *ngSwitchCase="valeur1"> valeur </balise-html>
		<balise-html *ngSwitchCase="valeur2"> valeur </balise-html>
		<balise-html *ngSwitchCase="valeur3"> valeur </balise-html>
		<balise-html *ngSwitchDefault > valeur </balise-html>
	</balise-html>


## Création d'un objet
## Lifecycle hooks:
Sont des interfaces, décrites dans angular/core, qui donnent accès à des moments clés du cycle de vie d'un component et de ses enfants, depuis sa création, pendant ses changements, puis lors de sa destruction. On distingue trois interfaces principales (y en a d'autres) 
### onInit:
Permet d'executer du code dés l'initialisation du component en implémentant la méthode ``ngOnInit()``
### onChanges:
Permet d'executer du code dés le changement du component dans le DOM en implémentant la méthode ``ngOnChanges()``
### onDestroy:
Permet d'executer du code dés la destruction du component et avant sa suppression du DOM en implémentant la méthode ``ngOnInit()``
## Decorateurs:
Sont précédés par @ et sont propores à Angulatr, donc éxistent dans les fichiers .ts. Ils existent pas mal de décorateurs dans le core d'angular dont on peut citer:
### @
### @Input
Permet aux données de traverser le component parent vers les enfants.
### @Output
Permet de créer des events pour passer les données depuis le component vers l'exterieur (un component parent)
###Event emitter

## Services
- Utilisés pour encapsuler une logique utilisée d'une manière transversale dans l'appli (peut être utilisé par n'importe quel component qui l'injecte)
- Le service le plus utilisé est celui qui permet de communiquer avec le backend.

### Injections
L'injecteur est un outil permettant d'enregistrer nos services. Il suffit d'importer le décorateur Injectable dans notre service et l'utiliser avant la declaration de notre classe service comme suit:
`import {Injectable} from 'angular/core';
@Injectable()
export class serviceName{}`
### Enregistrement et initialisation
Ensuite, il ne faut pas oublier de l'enregistrer dans ``AppModule`` au sein du décorateur ``NgModule({ providers: 'serviceName'})``

Finalement, il faut l'injecter dans le constructeur de la classe où on veut l'utiliser. 
 * AppModule:
 * AppComponent:
 * Component:

## HTTP et les observables:
### Observables:

	RxJs= Reactive Extensions Library
	* of(...items) : retourne des observables depuis les arguments fournis
	* from(iterable): pour convertir un tableau en observable

## Le routage:
Se déclarent dans app.module.ts ou dans un fichier séparé de routing
Constante de type Routes dont les éléments sont de la forme suivante:
{path: "route", component|redirectTo: ComponentName|'routeName'} avec params {path: "route/:param", component: ComponentName}
 <router-outlet></router-outlet>
 routerLink="route-Name" (remplace href)
 routerLinkActive= "active" : permet d'ajouter une classe css lorsque la route est active. Il peut être combiné avec `[routerLinkActiveOptions]="{exact:true}"` pour dire que ça ne peut s'activer que si le path de la route est exactement celui dans la barre de navigation.
 ActivatedRoute 
 this.route.snapshot.params['paramNam'] === snapshot: en temps réél de la route, params: paramètres de la route 
 this.router.navigate()
### Les guards:
Permet de créer des restrictions d'accès sur les routes.
Est sous forme de service
import CanActivate
@Injectable : decorateur au dessus du nom de la classe car le service est injectable
canActivate(): décrit la logique d'authentification
Ajouter à 

## Les Formulaires:
Il y a deux approches pour les forms, **les reactive forms** et **les template-driven forms**
### Les reactive forms:


## Communications HTTP:

Pour faire des communications http il faut importer le `HttpClientModule` depuis `@angular/common/http` dans `AppModule` puis injecter le service `HttpClient` dans le component ou service qui va effectuer la communication.

* get(): permet de faire des requetes http pour récuperer des données.
* post(), put(), patch() : permet d'envoyer les données au serveur.
* delete() : permet de supprimer une ressource sur le serveur.


#ref