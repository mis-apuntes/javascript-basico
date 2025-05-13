# Funciones
Son bloques de código re-utilizables. 

## Crear una función

Se puede crear de dos manera:

```javascript
function nombreFuncion() {          // Tipo por construcción
    // ...
}

var nombreFuncion = function() {    // Tipo por expresión
    // ...
}
```
## Instrucción `return`

Las funciones pueden o no retornar un valor o una función.

+ función sin retorno

  ```javascript
  function nombreFuncion(a){
      // ...
  }
  ```

  > En realidad devuelve `undefined`

+ función con retorno

  ```javascript
  // Retornar un valor
  function nombreFuncion(a, b) {
      // ...
      var result = a + b; 
      return result;
  }
  
  // Retornar una función
  function nombreFuncion(a) {
      // ...
      return function () { /*...*/ } ;
  }
  ```

## Parámetros de una función

Los **parámetros** son valores que recibe una función y con los que la función trabajará.

```javascript
function nombreFuncion(param1, param2) {
    // ...
}
```
Los parámetros pueden ser:

- de cualquier tipo (Numéricos, booleanos, objetos, etc) o 
- funciones (denominada *callback*)

## Invocar una función

Para invocar, se debe escribir el nombre de la función seguido de `()`

```js
// Funciones sin parámetros
nombreFuncion();

// En caso de que requiera parámetros
nombreFunción("Hola", 1);

// Si la función devuelve un valor se puede asignar a una variable
var result = nombreFunción();
```

> **Notas**:
>
> - Si se pasa menos argumentos de los necesarios, los faltantes serán considerados `undefined`
>
> - Si se pasan más argumentos, los sobrantes se ignoran.
>
> ```javascript
> function multiplicar(a, b){
> 	console.log(a*b);
> }
> multiplicar();    //NaN
> multiplicar(2,3,4,5,1);   // 6
> ```

## Scope de una variable

El *scope* (o ámbito) es el contexto **generado por una función** y dentro del cual existen las variables que se hayan declarado dentro.

- Una variable es inaccesible desde fuera de su scope (Fuera de su ámbito, no existen.).

```javascript
var a = 10;     // scope es global

function mifn(){
    var b = 20  // scope local dentro la función mifn
    
    c = 30      // ¡scope glopal! (definido sin var)
    //(NO ES RECOMENDADO DEFINIR VARIABLES ASI)
    
    function subFn() {
        var str = "hola "; //scope local dentro subFn
        
        console.log(b)    // 20
    }
}
mifn();

console.log(c);  //30, existe acá!
console.log(b);  //error, no existe acà!
```

> **Notas**:
>
> - Es posible acceder a variables de *scopes* superiores pero no de inferiores.
> - _Solo las __funciones crean un scope__ en JavaScript_.
> - Toda variable declarada  __fuera de cualquier función__, es una __variable global__ y se añaden como atributo del **objeto global** `window`.
> - Crear una variable sin `var` la vuelve automáticamente en **variable global**. (NO es una buena practica). 

Ejemplo 2:
```javascript
function miFn2(){
    var arr = []
    var a = 7

    arr.push(function(){
        console.log(a)  //9
    })

    a = 8
    arr.push( (function(a){ 
        //la variable 'a' dentro la función es diferente a la variable global 'a'
        return function(){
                    console.log(a)  //8
                }
        })(a)	//ejecutando la función
        //al ejecutar la funcion se crea un contexto y toma el valor que tiene 'a' hasta ese momento
    ) 
    
    a = 9
    arr.push(function(){
        console.log(a)  //9
    })

    return arr
}

miFn2()[0]();	//9
miFn2()[1]();	//8
miFn2()[2]();	//9
```

## Funciones anónimas

Son funciones que no tienen nombre.
```javascript
function() {
    // ...
}
// como la invocamos?
```

La utilidad de las funciones anónimas, es:

- para encapsular variables.
- definir *callbacks*

### Encapsular variables

Las funciones anónimas nos ayudan a __"encapsular" variables__, para __prevenir__ que códigos de terceros que tengan (casualmente) definido variables con el mismo nombre colisionen.

```javascript
//libreria.js
//suponiendo que la 'libreria.js' contiene lo siguiente:
var str = "b" // 'str' scope global, se añadirá al obj 'window'
// ...


/*------------ Encapsulando las variables -----------*/
//miCodigo.js
(function() {
  var str = 10  //'str' scope local, NO se añadirá al obj 'window' 
  console.log(str)  //10
})()
```
- Como la función no tiene nombre, se la encierra entre `(function() {...})` y
  añadimos `()` al final para auto-ejecutar la función.

> **Nota**: es recomendable colocar nuestro código dentro de una **función anónima auto-ejecutada**.

### callbacks

Se pueden pasar _funciones anónimas_ como parámetro de otra función.

```javascript
function miFuncion(paramX, fn){ 
    //fn es una funcion que se recibe como argumento (callback)
    // ... 
    fn()    //ejecutamos la funciòn (callback)
}

//invocando a "miFuncion()" y enviamos una función anónima
miFuncion("hola", function(){   
    // cuerpo de la función anónima
})
```

## arguments

Cada función posee internamente un objeto llamado "arguments" (un *pseudo-array*) que contiene a los valores que se le han pasado a la función.

> `arguments` es una variable local del prototipo de una función (creada automáticamente por JS).

```javascript
function miFn(){
    console.log(arguments)
}
miFn()  //[]
miFn(1,"hola")  //[1, "hola"]

```

Ejemplo práctico:

```javascript
function sumar() {
    var total = 0 
    for(var i = 0; i < arguments.length; i++){
        total += arguments[i]
    }
    return total
}

sumar()          //0
sumar(2, 3)      //5
sumar(1, 4, 5)   //10
```

## Funciones de primera clase

Las funciones en *JavaScript* son objetos y por lo tanto es posible agregarles atributos.

```javascript
var miFn = function(){
    // cuerpo de la funcion
}

miFn.atributo = "Hola soy un atributo"

console.log(miFn.atributo)  // "Hola soy un atributo"
```
