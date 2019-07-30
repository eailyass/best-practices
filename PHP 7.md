# PHP et l'orienté objet
---
## Les classes
### Les constantes de classes
On peut déclarer une constante au sein d'une classe via le mot clé __const__ ou __define__. La constante est déclarée une seule fois pour la classe et pas pour chaque instance de la classe.

### Les classes anonymes:

Une classe anonyme est une classe sans nom. Alors ça change pas le fonctionnement de la classe en elle même, ni même sa syntaxe, à part bien évidement qu’on ne met pas le nom. Elle est déclarée par le mot clé _new class() {}_ sert généralement dans les tests et surtout pour manipuler les mocks.

### Fonctions anonymes:

Des fonctions sans nom déclarés de la manière suivante:
```php
 function($param1,...){

}
```
Elles servent en général comme fonctions de callback.
Il éxiste aussi des fonctions anonymes statiques:

```php
static function($param1,...){

}
```
Elles servent à découpler la fonction de la classe qui l'abrite.

### Autoloading:

Il est inclus par défaut depuis PHP 5.4 via la fonction __spl_autoload_register()__ 

```php
spl_autoload_register(function ($className) {
    include 'classes/' . $className . '.class.php';
}); 
```

### Constructeur/destructeur:

Le constructeur est déclaré par la méthode __\_\_construct()__ ou le même nom de la classe mais cette dernière méthode est dépréciée dés php 5.3.3

Le destructeur les appelé par la méthode __\_\_destruct()__ et permet de ne plus faire référence à un objet.

### Visibilité des variables et méthodes:
* Pour les variables/constantes: 

Le code suivant fait l'affaire:

```php

class MyClass
{
    public $public = 'Public';
    protected $protected = 'Protected';
    private $private = 'Private';

    function printHello()
    {
        echo $this->public;
        echo $this->protected;
        echo $this->private;
    }
}

$obj = new MyClass();
echo $obj->public; // Fonctionne
echo $obj->protected; // Erreur fatale
echo $obj->private; // Erreur fatale
$obj->printHello(); // Affiche Public, Protected et Private

```
### L'opérateur de résolution de portée:
fournit un moyen d'accéder aux membres static ou constant, ainsi qu'aux propriétés ou méthodes surchargées d'une classe.
L'appel peut se faire de deux endroits:
1. En dehors de la classe:
```php
class MyClass {
    const CONST_VALUE = 'Une valeur constante';
}

$classname = 'MyClass';
echo $classname::CONST_VALUE;
```

2. A l'intérieur de la classe via les mots clés _self_, _parent_ ou _static_

### Les interfaces

permettent de créer du code qui spécifie quelles méthodes une classe doit implémenter, sans avoir à définir comment ces méthodes fonctionneront.

### Les Traits

Un trait tente de réduire certaines limites de l'héritage simple.
Un trait est semblable à une classe, mais il ne sert qu'à grouper des fonctionnalités d'une manière intéressante. Il n'est pas possible d'instancier un Trait en lui-même. Il permet l'utilisation de méthodes de classe sans besoin d'héritage.
* Précédence:
  * Une méthode héritée depuis une classe mère est écrasée par une méthode issue d'un Trait.
  * Les méthodes de la classe courante écrasent les méthodes issues d'un Trait.
  * ceci veut dire ClasseMere::maMethode() < Trait::maMethode() < ClassFille::maMethode().

Le Trait est invoqué dans une classe via le mot clé _use_
```php

trait monTrait {
 public function maFonction(){
 	//
 }
}
class maClasse {
use monTrait;
//
}

```

Si deux Traits insèrent une méthode avec le même nom, une erreur fatale est levée si le conflit n'est pas explicitement résolu.

Pour résoudre un conflit de nommage entre des Traits utilisés dans la même classe, il faut utiliser l'opérateur insteadof pour choisir une des méthodes en conflit.

## Déclarations de types des arguments et de types de retour:
### Déclaration de type d'arguments:
	function maFonction([int,float,string,array,classe..] $maVariable){
		//fonction
	}
### Déclaration de type de retour:
Il est déclaré avant l'ouverture de l'accolade du corps de la fonction
	
	function maFonction($maVariable):[int,float,string,array,classe..] {
		//fonction
	}
Il est possible que les valeurs de retour soient marquées comme nullable en préfixant le nom du type avec un point d'interrogation (?)
<pre><code>
	function maFonction($maVariable): <b>?</b> [int,float,string,array,classe..] {
		//fonction
	}
</pre></code>

### Géstion des constantes:
En PHP 5.6 on déclare des constantes de la manière suivnate:
	
```php
	const MA_CONSTANTE = vleur; // peut même être un array
```
En PHP 7 on peut utiliser défine:
```php
	define("MA_CONSTANTE",vleur); // peut même être un array
```
A l'inverse pour "define", déclarer une fonction via "const" doit se faire au début du context et les constantes sont sensibles à la casse.

## Propriétés des classes:

