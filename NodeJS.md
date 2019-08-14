module.exports.say=

debug filename.js

## Initialiser un projet

Permet de créer le fichier package.json dans le dossier en cours qui va permettre de gérer les dépendances par la suite.
```bash
npm init
```


## appeler un module

var fs = require("fs");
## installer package

npm install connect

## si on dispose d'un fichier package.json

npm install // installe ts les dependencies de package.json
On peut créer le fichier package.json à partir de la commande "npm init"



## Modules:

	http : envoyer/recevoir des requêtes http
	url : l'url client
	querystring : renvoyer un tableau de paramètres issues de l'url (les paramètres GET)
	events : gérer les événements

	### créer un module:
		simple fichier .js à inclure en chemin relatif : require('./monModule') ou bien mettre dans le sous-dossier node_modules et l'appler require('monModule').
		Pour utiliser les fonctions au sein des modules créés il faut les exporter via la commande exports: exports.nomMethode

	### ExpressJS
	module implémentant des fonctionnalités de base pour notre serveur (gestion de routes)


## Evenements:
	Ecouter des événements:
		Objet.on('eventName', function(params){})
	Emettre des événements:
		# créer l'objet
		var EventEmitter = require(events).EventEmitter
		var event = new EventEmitter();
		event.emit("nomDeLevent", paramètre 1, [paramètre 2],...);
		# Ecouter l'event
		Objet.on('nomDeLevent', function(params){})



## Gulp:

	### Fonctions de base:
		gulp.task('nomDeLaTache', function () {
		  return gulp.src(ici-ma-source)
		    /* ici les plugins Gulp à exécuter */
		    .pipe(gulp.dest(ici-ma-destination));
		});

		gulp.task('watch', function)
		
	### modules les plus utilisés pour CSS
		less : consolider les fichiers .less dans le même css
		csscomb : réordonner les priorités
		cssbeautify : linter et indenter
		csso : minifier le code css
