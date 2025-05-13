# DOM (Document Object Model)

El DOM es una API para acceder y manipular los elementos de los documentos HTMl y XML. 

Por otro lado el DOM se puede entender como la **representación jerárquica** (forma de árbol) **de componentes** (nodos) que representan **el documento HTML**. 

Existen varios tipos de nodos:

1. __Elemento__  -> se corresponde con una etiqueta HTML.
2. __Texto__     -> Es el texto dentro de un elemento.
3. __Atributos__ -> Los atributos de los elementos.

El componente de nivel superior (raíz) es `document`.
```html
<a href="www.google.com" id="link"> ir a <strong>Google</strong></a>
```

```javascript
var a = document.getElementById("link");

// Ver los nodos hijos de <a>
console.log(a.childNodes);  //[object NodeList] (2)
							//[#text,<strong/>]

//accediendo al atributo
console.log(a.href)		// www.google.com
```
## Acceder a propiedades del document

```javascript
var css = document.styleSheets;
var title = document.title;
var scripts = document.scripts;
var charset = document.charset;
var url = document.URL;
var domain = document.domain;
```

Acceder a __elementos HTML__  a traves de propiedades de `document`
```javascript
var head    = document.head;
var body    = document.body;
var html    = document.documentElement;
var images  = document.images;
var links   = document.links;
var forms   = document.forms;

// Las propiedades anteriores devuelven un array, se puede acceder mediante un indice o el "id" definido de la etiqueta.

links[0]       // devuelve el primer elemento del array (indice 0) 
links.primero  // devuelve el elemento que tiene el id="primero"
```


> **Importante**: Para manipular los elementos del DOM, el _código JavaScript debe ejecutarse después de que el elemento se haya creado_.

## Acceder a elementos

Hay dos formas:

1. __getElements__: obtiene elementos mediante el tag, id o clase.
    ```javascript
    var p = document.getElementById('parrafo'); //retorna un solo elemento (objeto)
    
    var links = document.getElementsByTagName('a'); // retorna un array
    var parrafos = document.getElementsByClassName('parrafo'); // retorna un array
    ```
2. __querySelector__: obtiene elementos por selectores de css, se puede usar cualquier selector válido de css.
    ```javascript
    var parrafos = document.querySelectorAll('article > p'); // retorna un array
    
    var parrafo = document.querySelector('#parrafo'); // retorna un elemento (objeto)
    ```

## Acceder a los atributos
- Acceder a todos sus atributos: `.attributes` devuelve un objeto con todos los atributos (NO ES MUY UTILIZADO).
    ```javascript
    console.log(parrafo.attributes);    // objeto con todos los atributos
    ```

- Acceder mediante el método `.getAttributes(<atributo>)` devuelve el valor del atributo buscado
    ```javascript
    link.getAttributes('id')    // retorna un string con el id
    link.getAttributes('href')  // retorna un string con el enlace
    ```
- Acceder mediante sus propiedades (los atributos son propiedades del elemento)
    ```javascript
    console.log(link.id)      // retorna un string con el id
    console.log(link.href)    // retorna un string con el enlace
    console.log(link.className) // retorna las clases del elemento
    
    console.log(input.require) // retorna un boolean 
    ```
    Con esta notación también se pueden __setear valores__.
    ```javascript
    link.href = "www.google.com.bo"     // nuevo valor definido.
    ```
>  Los atributos __require, controls, etc. son atributos booleanos__, si se intenta acceder mediante `.getAttributes()`, retornará `""` (string vacio). En su lugar utilizar la notación punto (accediendo como propiedad)



## Acceder a los nodos texto
Existen 2 tipos: 
- `.textContent`, obtiene todo el texto dentro el elemento incluyendo el texto de los hijos. 
- `.value`  (para los elementos tipo input, button, textarea, etc)

la misma notación sirve para *setear* un valor.

```html
<a href="www.google.com" id="link"> ir a <strong>Google</strong></a>

<input type="text" id="username" value="anonimo">
```

```javascript
var a = document.getElementById("link");
var i = document.getElementById("username")

// como get
console.log(a.textContent)  // "Ir a Google"
console.log(i.value)        // "anonimo"

// como set
a.textContent = "Enlace hacia Google";
i.value = "";
```

## Crear elementos
Sintaxis `document.createElement('<element>`)`

```javascript
// Crear un <div>
var div = document.createElement('div');
div.textContent = "Texto dentro del div";
div.id = "myDiv";

// Crear un <a>
var link = document.createElement('a');
link.textContent = "Ir a Google";
link.href = "www.google.com";
link.target = "_blank";
```
## Insertar elementos dentro de otro
```javascript
document.body.appendChild(div);
div.appendChild(link);
```
> El elemento hijo se insertará al final del padre

## Insertar un elemento antes de otro
```javascript
padre.insertBefore(hijoNuevo, hijoSiguiente);

//Ejemplo
// <div id="padre"> <p id="hijo1"></p> <p id="hijo2"></p> </div>
padre.insertBefore(link, hijo2); // insertará el link entre el hijo1 e hijo2.
```

## Eliminar elementos
```javascript
// Hay dos formas
padre.removeChild(hijo);    // Elimina al hijo

elemento.remove();  // Se elimina el mismo
```

## Modificar elementos

### innerHTML 
Es una propiedad que contiene el HTML interno del elemento. Sirve como get y set.

```html
<div id="padre"> 
    <p id="hijo1">parrafo 1</p> 
    <p id="hijo2">parrafo 2</p>
</div>

```

```javascript
// como get
console.log(padre.innerHTML);  
    // <p id="hijo1">parrafo 1</p> 
    // <p id="hijo2">parrafo 2</p>

// como set
hijo2.innerHTML = '<a href="www.google.com"> ir a Google </a>'; //reemplaza/añade el html definido.
console.log(padre.innerHTML);  
    // <p id="hijo1">parrafo 1</p> 
    // <p id="hijo2"><a href="www.google.com"> ir a Google </a></p>

```

### Modificar atributos
Se usan:
- `.getAttributes('<atributo>')` 
- `.setAttributes('<atributo>', '<valor>')` 
- `.removeAttributes('<atributo>')` 

```javascript
// <p id="parr"> parrafo 1</p>

p.setAttributes('id', 'parrafo')

// <p id="parrafo"> parrafo 1</p>

p.removeAttribute('id');

// <p> parrafo 1</p>
```

### Modificar clases
- `.className`  (devuelve un string con las clases)
- `.classList` (devuelve un array con las clases), y tiene tres métodos:
    - `.add('clase')`      -> añade la clase
    - `.remove('clase')`   -> quita la clase
    - `.toggle('clase')`   -> añade la clase (si no la tenia) y se la quita (si es que la tenia).

```html
<p class="clase1 clase2 clase3" id="parrafo">
```
```javascript
console.log(parrafo.className)  // "clase1 clase2 clase3"
console.log(parrafo.classList)  // [clase1, clase2, clase3]

parrafo.classList.add("clase4")
```

## Modificar css
se usa la propiedad style seguida de la propiedad a modificar.

```javascript
parrafo.style //es un objeto con todos los estilos definidos con JS (NO recupera los estilos definios en el CSS)

// como set
parrafo.style.background = "red";

// como get
console.log(parrafo.style.background);
```
> Estos estilos se añaden (en el HTML) en tiempo de ejecución, **Evitar en lo posible**.

## Traversing
Moverse a través del DOM

Propiedades

- `.parentNode`       -> el nodo padre
- `.children`         -> todos los elementos (tags) hijos 
- `.childNodes`       -> todos los nodos hijos (incluyendo los nodo texto)
- `.firstChild`       -> el primer nodo hijo
- `.firsElementChild` -> el primer elemento hijo
- `.lastChild`        -> el ultimo nodo hijo
- `.lastElementChild` -> el ultimo elemento hijo
- `.nextSibling`      -> va al siguiente nodo hermano
- `.previousSibling`  -> va al anterior nodo hermano
- `.nextElementSibling` -> va al siguiente elemento hermano
- `.previousElementSibling` -> va al anterior elemento hermano