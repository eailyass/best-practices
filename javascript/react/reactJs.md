## Notions React:
----
React est une _bibliothèque JS_ développée par Facebook, qui permet de générer des applications web à base de JS suivant la norme `ES6`, du `CSS` en plus de la génération du `HTML` via la norme `JSX`
### Prérequis:
* Avant tout démarrage il est nécessaire d'installer npm et react-install
* Initialiser un projet avec `npm init` qui permet de génerer un fichier package.json qui gère les dépendances du projet.
* Créer un projet via la commande create-react-app [nom_du_projet]

### Structure d'un projet:
#### Dossier public:
Contient in fichier index.html avec une balise principale. L'application est en général de type SPA (single page app), donc on garde notre page index.html et c'est le js qui va venir changer le contenu de cette page.

#### Dossier node_modules:
C'est le dossier ou on trouve tous les modules installés par npm.

#### Dossier src:
Contient la logique de l'application, avec deux fichiers principaux en plus du css qui accompagne:
* index.js à partir duqeul on va viser notre public/index.html
* app.js qui est un component react.

Ce dossier peut contenir tous ce qui va nous aider à organiser la logique de l'application comme:

* components: dossier qui rassemble les composants développés
* styles: regroupe tous le fichier des styles (index.css...)
* containers: des composantes qui contiennet d'autre composantes (le fichier app.js par expl)
* helper: librairie personnelle de fonctions developpées.

#### Principe général:
Un projet est constitué de plusieurs composants (fichier js avec du JSX éventuellement + fichier css pour le style). Plusieurs composants peuvent être regroupés dans un container, et le tout est appelé dans un fichier central (app.js) selon différentes règles.

### Les spécificités react:

#### Un composant:
C'est un fichier js qui importe forcément la biblio react via `import React from 'react'` et eventuellement un fichier de style. Et déclare une fonction qui retourne du `JSX` et se termine par un `export default nomDeFonction`. Il esxiste en deux type, stateless et statefull.
##### Composant stateless:
Implémente et retourne une méthode et importe `React`
##### Composant stateful:
Implémente une classe qui étend la classe `Component` et qui retourne du JSX via la méthode `render()` et importe `React` et `Component` de la biblio `react`
##### Principe des props:
Pour garantir la réutilisabilité du component la fonction accepte des variables qu'in appelle `props` selon la syntaxe suivante:
```javascript
const functionName = props => (
	<div>
		<div className="nom de la classe">
			props.propriete_1
		<``/div>
		<div className="nom de la classe">
			props.propriete_2
		<``/div>
	<``/div>
	);
```
Après on importe le composant dans le fichier central et on spécifie pour chaque props le valeur à attribuer.

#### Un container:
C'est un fichier js qui a la même structure d'un composant avec une propriété `children`.
```javascript
const functionName = props => (
	<div>
		{props.children}
	<``/div>
	);
```
#### Le lifecycle d'un composant:
Un composant a un lifecycle de plusieurs étapes qu'on peut appeler pour executer des étapes avanat ou après l'import du composant.

#### Principe des données descendantes:
Dans react on trouve la notion de composant parent et composants fils. En effet, tout composant qui emet la fonction `render` est un parent des composants invoqués par cette même fonction. Ainsi deux régles émanent de cette notion:
* Une `prop` est toujours passée par un composant parent vers un enfant.
* Toute prop passée est en lecture seule.

#### Les propTypes:
Le fait que nos composants disposent de props, implique que lors de l'appel de ces composants, les props doivent être définis ou à la rigeur aient une valeur par défaut. Cette valeur par défaut est renseignée par la propriété `defaultProps` de la manière suivante:
```javascript
function MyCoolComponent({ name, required, value }) {
  // …
}

MyCoolComponent.defaultProps = {
  name: "test",
  required: false,
}
```
Cette façon de faire a quelques inconvénients comme dans le cas où on ne définit pas les valeurs par défaut de toutes les variables. Chose qui emet une érreur dans le cas d'ommission d'une valeur. Pour cela une deuxième alternative se présente, à savoir les propTypes. Elles sont gérées par l'import du module `prop-types`, et permettent de définir le type de chaque prop ainsi que si elle est `required` ou pas...
Sa mise en oeuve peut se faire de la manière suivante:
```javascript
import PropTypes from 'prop-types'

// La fonction Card ici…

Card.propTypes = {
  card: PropTypes.string.isRequired,
  feedback: PropTypes.oneOf([
    'hidden',
    'justMatched',
    'justMismatched',
    'visible',
  ]).isRequired,
  onClick: PropTypes.func.isRequired,
}
```

### Spécificités des classes:
Une classe est utilisée lorsqu'on doit déclaer des fonctions métier. Elle contient plusieurs spécificités dont on cite:
#### La notion `this`:
En général, faire appel à `this` dans une classe signifie qu'on est en train de viser l'instance même dont on est à l'interieur.
##### Binding explicite:
##### Binding par fonction fléchée:
##### Binding par decorator:
### La notion de l'état local:




Routes : app.js

Les states remontent, les props redescendent.

## Rducer /reducers
## 
## Thunk