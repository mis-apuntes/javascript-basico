## Los tipos de datos en JS son objetos

```javascript
//Definido de manera literal (RECOMENDADO)
var cadena = "Yo soy un string literal"; 
var numero = 10; 

//definido por constructor (NO RECOMENDADO)
var cadena2 = new String("yo soy otro string"); 
var numero2 = new Number(20);

typeof cadena       //string
typeof cadena2      //object

// ambas variables se pueden usar como objetos
cadena.toUpperCase()
cadena2.toUpperCase()
```

## typeof e instanceof

Para saber el tipo dato de una variable o un valor, ejecutar `typeof <valor>`, retorna un string indicando el tipo.

Ejemplos

```javascript
console.log(typeof 1)       //number
console.log(typeof "uno")   //string
console.log(typeof {})      //object
console.log(typeof function(){})   //function
```

Para saber si una variable o valor es de un tipo específico, se usa `<valor> instanceof <Clase>`

```javascript
function Persona(){
    this.nombre = "Carlos"
}

var p = new Persona();
var str = "Carlos"

console.log(p instanceof Persona)   //true   
console.log(str instanceof Persona)   //false   
```

## Valores por referencia

Al momento de definir una variable (del tipo __objeto o array__) a partir de otra ya definida anteriormente, el valor es pasado por referencia, es decir, que **no se crea una copia** de los valores sino se crea un apuntador a la misma dirección de memoria (de la variable original).

>Los cambios que se realicen en cualquiera de las variables afectarán a todas las que tienen la misma referencia.

```javascript
var objOriginal = {
    nombre : "Carlos";
}

var objCopia = objOriginal;
console.log(objCopia); //{nombre : "Carlos"}

// Si se hace un cambio en la variable 'objCopia', 
// afectará tambien a la variable 'objOriginal'
objCopia.nombre = "Luis";

console.log(objOriginal); //{nombre : "Luis"}
```

## El objeto `this`

`this` hace referencia al objeto padre inmediato.

```javascript
this //objeto global 'window'

var miObj = {
    nombre: "Carlos",
    apellido: "Ramos",
    saludar: function(){
        return "Me llamo "+ this.nombre; //this es 'miObj'
    },
    direccion: {
        zona: "Temporal",
        imprimir: function(){
            console.log(this.zona)   //this es 'direccion' 
        }
    },
    nuevaDir: function(){
        return function(){
            //ATENCIÓN !!!
            console.log(this)   //this es 'window' ¿rompe this?
        } 
    }    
}

miObj.saludar();
miObj.direccion.imprimir();
miObj.nuevaDir()();
```

Dependiendo el ámbito de ejecución, `this` cambia,

- En un contexto global, `this` hace referencia al objeto global `window`.

- `this` dentro de un *event handler*.

  ```javascript
  var boton = document.getElementById("boton");
  
  boton.addEventListener('click',function(){
    alert(this.textContent);  // this referencia al elemento HTML (boton)
  });
  ```

- `this` dentro de un *constructor*.

  ```js
  function Persona(nombrePersona, edadPersona){
    this.nombre = nombrePersona; 
    this.edad = edadPersona;
    //this se refiere al objeto instanciado.
  }
  
  var miAmigo = new Persona("Luis", 30);
  console.log(miAmigo.nombre)  // "Luis"
  ```

- Si se usa `"use stric"`, `this` devuelve `undefined`.

    ```javascript
    (function test(){
      "use strict";
      console.log(this);    //undefined
    })();
    ```

## Hoisting

El interprete de JS **eleva las declaraciones con `var`** al inicio de su scope pero **no eleva su definición**.

```js
// Por ejemplo
console.log(x); // undefined
var x = 5;

// Es como ejecutar --------------
var x:
console.log(x); // undefined
x = 5;
// -------------------------------

// Ojo! En el caso de let o const no aplica
console.log(a) // ReferenceError
let a = 10;
```

En el caso de las funciones declaradas con `function`  también se elevan al inicio del *scope*.

```js
// Se puede invocar a la función antes de estar definida.
saludar("Carlos")   // "Hola Carlos"

function saludar(nombre) {
    console.log("hola " + nombre)
}
```

Pero si la función está define con `var` solo su declaración se eleva pero no su definición.

```js
console.log(despedirse) //Undefined
despedirse("Luis")  //Error!

var despedirse = function(nombre) {
    console.log("Adios " + nombre)
}
```

## Prototype

El prototype es el __objeto base__ del cual todos los demás objetos __heredan sus propiedades y métodos__.

```javascript
// Al crear variables "primitivas" en JS, estos heredan las prop y metodos de su prototipo (osea son objetos).
var a = 10;         // hereda de Number.prototype
a.toString();   // "10"

var b = "Hola";     // hereda de String.prototupe
b.toUpperCase();// "HOLA"

// Todo en JS tiene un prototipo y se puede acceder mediante el nombre de la clase
Number.prototype
String.prototype
Boolean.prototype
Object.prototype
Function.prototype
Array.prototype
// Etc.
```

Se pueden añadir nuevas propiedades y/o métodos a los prototipo

```javascript
Number.prototype.esPositivo = function(){
    return this > 0
}

a.esPositivo(); //true
```

> Recomendación: __evitar__ hacer uso sobre las clases predefinidas de javascript (el ejemplo anterior solo con fines didacticos)

### Mejorar el rendimiento de objetos

<!--Un poco contradictorio con lo que dice arriba, buscar mas información sobre prototype-->

Uno de los objetivos de utilizar prototipos, es para mejorar el rendimiento de los objetos,

```javascript
funtion Persona(nombre){
    this.nombre = nombre
    //imprimirInfo = function(){ console.log(nombre)} 
    // Esto no es muy eficiente cuando se tiene muchos objetos, 
    // porque por cada objeto, la función se repite en todos
    // ellos (y esto hace que se ocupe mayor espacio).
}

// Para mejorar se debe crear una funcion en el prototipo.
Persona.prototype.imprimirInfo = function(){
    console.log(nombre)
}

var p1 = new Persona("Carlos")
p1.imprimirInfo()   //"Carlos"

var p1 = new Persona("Felip")
p1.imprimirInfo()   //"Felipe"
```

### Funciones especiales bind(), call() y apply()

__*Todas las funciones*__ tiene estas tres funciones en su prototype `Function.prototype.bind()`  
`Function.prototype.call()`  
`Function.prototype.apply()`

```javascript
var car1 = {
    color: "verde",
    marca: "mazda",
    imprimir: function(){console.log(this.marca+" - "+this.color)}
}

function logCar(arg1) {
    this.imprimir()
    console.log("===== "+arg1+" ======")
}

//bind(): devuelve la misma función
logCar.bind(car1)("abc")
// call(): se pasa los argumentos separados por coma
logCar.call(car1, "123")
// apply(): se pasa los argumentos en un array 
logCar.apply(car1, ["asd"])
```

Ejemplo de uso; _"Funciones prestadas"_

```javascript
var car2 = {
    color: "rojo",
    marca: "toyota"
}

car1.imprimir.call(car2)
```
