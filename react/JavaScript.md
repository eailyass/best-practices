## Le DOM:
Tout DOM commence par l'élément ``document``.
### Chercher des éléments depuis document:

#### Quelques Méthodes simples pour selectionner des élémpents:

```javascript
document.getElementById('#id')
document.getElementByClassNamme("class")
document.getElementByTagName("tag") // selectionner par une balise
```

#### La méthode querySelector:
Elle sert à faire des requêtes plus complexes avec les signes suivants: 
* '#' : pour un ID
* '.' : pour un une classe
* '>' : pour les enfants directs 
Elle retourne la première valeur trouvée.  

Pour retourner un tableau d'éléments il faut utiliser la méthode ``querySelectorAll``

### Chercer depuis un élément:
* element.children : retourne liste des enfants
* element.parentElement : retourne le parent
* element.nextElementSibling : retourne l'élément suivant du même niveau
* element.previousElementSibling : retourne l'élément précédent du même niveau

### Modifier le contenu d'un élément:
* element.innerHTML = 'code html' : remplace le contenu de l'élément par le code html.
* element.textContent = 'text' : remplace le contenu de l'élément par du texte.
* element.classList.[add(),remove(),replace()] : ajouter/supprimer/remplacer une classe.
* element.classList.contains("className") : retourne true si l'élément contient la claase.
* element.style.cssAttribute = 'valeur CSS' : modifie le style de l'élément.
* element.[setAttribute("nom","valeur"), getAttribute("nom"), removeAttribute("nom")] : manipuler les attributs d'un élément.
* document.createElement("balise") : créer un élément dans le document.
* element.[appendChild(elt),removeChild(elt),replaceChild(newElt,oldElt)] : manipuler un element fils.

### Les événements:
* __AddEventListener('event', function())__ : S'applique sur un élément, document, window mais aussi sur tout objet prenant en charge les évènements (comme XMLHttpRequest).
* __preventDefault()__ permet d'annuler le comportement par défaut de l'élément.
* Les événements se propagent dans le DOM du fils en parent, (un click dans sur une div se propage sur les différentes balises parentes). Il est possible d'utiliser __stopPropagation()__ pour éviter ce comportement.