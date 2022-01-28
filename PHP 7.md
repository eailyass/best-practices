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

### Final

Empêche les classes filles de surcharger une méthode, "final" de la calsse mère.

Si la classe elle-même est définie comme finale, elle ne pourra pas être étendue.

### Variables et fonctions statiques

Une variable statique a une portée locale mais elle garde toujours la dernière valeur assignée. Par exemple
```php
function test()
{
    $a = 0;
    echo $a;
    $a++;
}


function test()
{
    static $a = 0;
    echo $a;
    $a++;
}
```
dans le premier cas $a est initilisée à 0 à chaque appel de la fonction, mais dans le second cas, elle est initialisée à 0 juste la première fois.

Une fonction statique sert à être appelée sans instancier la classe mère. du coup la variable __$this__ ne peut être utilisée.

**Il n'existe pas de classes statiques**
## Constantes magiques:
----
## Méthodes magiques:
Les méthodes magiques sont des méthodes PHP qui servent quand elles existent dans un objet à se lancer après que tel ou tel événement survient.


### \_\_construct() et \_\_destruct():
Appelées respectivement lors de la création et la destruction d'une instance.

### \_\_call(), \_\_callStatic():
La première appelée quand on tente d'appeler une méthode dont on a pas droit d'appeler (privée ou n'éxiste pas). La seconde fait la même chose mais pour les méthodes statiques.  **\_\_callStatic() doit obligatirement être statique**
### \_\_get(), \_\_set()
La première est appelée lorsque l'on essaye d'accéder à un attribut qui n'existe pas ou auquel on n'a pas accès. La seconde lorsque l'on essaye d'assigner une valeur à un attribut auquel on n'a pas accès ou qui n'existe pas.
### \_\_isset(), \_\_unset()
*********
### \_\_sleep(), \_\_wakeup()
********
### \_\_toString()
Appelée lorsque l'objet est amené à être converti en chaîne de caractères. Cette méthode doit retourner la chaîne de caractères souhaitée.
### \_\_invoke()
Appelée dés qu'on veut utiliser un objet comme une fonction. Elle est appelée au lieu de l'érreur fatale qui va être générée.
### \_\_set_state()
Elle est Appelée lorsque vous appelez la fonction __var_export__ en passant votre objet à exporter en paramètre. var_export a pour rôle d'exporter la variable passée en paramètre sous forme de code PHP (chaîne de caractères). Si vous ne spécifiez pas de méthode \_\_set_state dans votre classe, une erreur fatale sera levée.
### \_\_clone()
Appelée lors du clonage d'un objet, via le __mot-clé__ clone.

```php
$nouvelObj = clone $ancienObj;
```
Elle permet de changer le comportement de __clone__ (modifier des attributs du nouvel objet, incrémenter un compteur...)

__Le clonage permet de faire une copie exacte d'un objet vers un nouvel objet sans garder de liens entre les deux.__

### \_\_debugInfo()
Permet de changer le comportement de var_dump() sur l'objet en question et donne la possibilité de selectionner les informations à retourner dans var_dump()

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
### Abstraction des classes:
- Les classes définies comme abstraites ne peuvent pas être instanciées
- Toute classe contenant au moins une méthode abstraite doit elle-aussi être abstraite. 
- Les méthodes définies comme abstraites déclarent simplement la signature de la méthode - elles ne peuvent définir son implémentation.
- Lors de l'héritage d'une classe abstraite, toutes les méthodes marquées comme abstraites dans la déclaration de la classe parente doivent être définies par l'enfant ; de plus, ces méthodes doivent être définies avec la même visibilité, ou une visibilité moins restreinte. 

```php
abstract class AbstractClass 
{
    // Force les classes filles à définir cette méthode
    abstract protected function getValue();
    abstract protected function prefixValue($prefix);

    // méthode commune
    public function printOut() {
        print $this->getValue() . "\n";
   }
}

class ConcreteClass1 extends AbstractClass 
{
     protected function getValue() {
       return "ConcreteClass1";
     }

     public function prefixValue($prefix) {
       return "{$prefix}ConcreteClass1";
    }
}
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
```php

trait A {
    public function smallTalk() {
        echo 'a';
    }
    public function bigTalk() {
        echo 'A';
    }
}

trait B {
    public function smallTalk() {
        echo 'b';
    }
    public function bigTalk() {
        echo 'B';
    }
}

class Talker {
    use A, B {
        B::smallTalk insteadof A;
        A::bigTalk insteadof B;
    }
}

```

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

