## Normes ES6
----
La norme ES6 est une manière qui permet d'écrire du code JS selon une nouvelle norme. Elle diifère de la syntaxe classique de JS appelée ES5. Dans ce document on va essayer de voir quelques exemples afin de comprendre crtaines de ces différences.

### Déclarations:
* Les ; ne sont plus obligatoires.
* La concatenation de chaines de caractères peut se faire via ${variableAConcatainer}
* Les retours à la ligne se font directement sans '\n' grace au templates string.
* Variables: [const,let] variable = 10 (const ne change pas et let peut changer)
* Fonctions: const nomFonction = (args) => {
	corps
}

* Classe: class NomDeClasse {
	method1 = (args) =>{

	}
}

### Destructuring:
Permet d'accéder à des attributs d'objets json de manière plus rapide
ES5:
```Javascript
var test =  {
	name: 'eailyass',
	age: 25,
	details : {
		style: 'round',
		color: 'red',
	}
};
var name = test.name;
var color = test.details.color;
```
ES6:
```Javascript

const test =  {
	name: 'eailyass',
	age: 25,
	details : {
		style: 'round',
		color: 'red',
	}
};

const {name} = test;
const {color} = test; //Equivalent à const {details : {color}} = test; à éviter

```
### Arrow functions:
Les fonctions sont déclarées différement:
ES5:
```Javascript
var maFonction = function maFonction({val1,val2='default'}) {
  return {val1};
};
```
ES6:
```Javascript
const maFonction = () => 50;

```
Il est aussi possible de passer des arguments par défaut:
ES5:
```Javascript
var maFonction = function maFonction() {
  var number = arguments.length <= 0 || arguments[0] === undefined ? 42 : arguments[0];
  return number;
};
```
ES6:
```Javascript
const maFonction = (number=42) => number
console.log(maFonction(21)) // retourne 21
console.log(maFonction()) // retourne 42


```
### L'orienté objet:
ES6 a introduit l'orienté objet dans JS, chose qui a permis de créer des classes et faire des héritages de la manière suivante:
#### Classes et héritage:

ES6:
```Javascript
class Person {
	birthYear = 1992

	getAge = () => 2019-this.birthYear
}

const eailyass = new Person
console.log(eailyass.getAge()) // renvoit 27 
class User extends Person {
spec = 'react'
}
const eailyass_1 = new User
console.log(eailyass_1.getAge()) // renvoit 27 
```
#### Chargement de fichiers:
ES5:
```Javascript
var myFile = require('path/to/file');
```
ES6:
```Javascript
import file from 'path/to/file' // require reste valable

import _ from 'package'; // permet de charger les dépendances du projet 
```
#### Export de variables et valeurs:
Dans ES6 il est possible d'exporter juste des valeurs d'un fichier à un autre:

ES6 Fichier1:
```Javascript
 const test = 10;
 const test2 = 12;

 export { test1 , test2,}
```
ES6 Fichier2:
```Javascript
import {test1,test2} from 'path/to/Fichier1'
```
## Le Spread operator:
Sert à copier "cloner" une variable (équivalent de clone dans PHP). Il est invoqué par le mot-clé '...'.
ES6:
```Javascript
const obj1 = {
	nom : "eailyass",
	age: 25
}
const obj2 = {...obj1} // obj2 aura les mêmes valeurs que obj1

const tab1 = ['valer1','valeur2']
const tab2 = [...tab1]
```

## Les Boucles:
ES6 propose une syntaxr rapide de la boucle for

----
## Normes JSX:
`JSX` est un language qui permet d'écrire du pseudo-html dans des fichiers JS qui vont générer de l'html coté client par la suite. Il répond à certaines règles:
* En JSX il faut que tout le code soit enveloppée d'une seule balise. Il faut tjrs penser à créer une div qui regroupe le code.
* l'équivalent de l'attribut `class` dans html est `className` et celui de `for` est `htmlFor`
* Les props en JSX acceptent deux types de valeurs, des string et `les autres`. A noter que les autres peut être n'importe quelle valeur, à condition d'être enveloppé entre deux accolades. Quant aux valeurs booléennes, il est à noté que le simple fait de déclarer une prop sans lui affecter une valeur est équivalent à un `true` On retrouve une syntaxe telle que:
```javascript
<attributeName
	prop1="string"
	prop2= {autre}
	required 
{/*required est true*/} 
	/>
```

### Les conditions:
Les conditions et boucles n'éxistent pas dans JSX au vrai sens du terme. Elles sont illustrées sous forme d'opérateurs logiques `&&` `||` et opérateur trnaire `? :` ainsi pour executer un code selon une condition, on procède à la syntaxe suivante:
```javascript
{condition === true && ('code à éxecuter')}
```