# Javascript

Es un lenguaje de programación creado por __Netscape__, creado para añadir interactividad a las páginas web.

> Java no es javascript, java (o c++) es un lenguaje de propósito general.

Javascript es un __lenguaje interpretado__ (no compilado, osea que no genera ningún fichero (objeto o exe). Y es el navegador que interpreta el código.

> **Nota**: *JavaScript* es una implementación del estándar *ECMAScript*.

## Insertar JavaScript en HTML
Los archivos *JavaScript* por sí solos no pueden ejecutarse directamente desde el navegador; Es necesario incrustarlos en un documento HTML.

- **Opción 1**: (no recomendada) en el mismo documento
  
    ```html
    <!DOCTYPE html>
    <html>
        ...
        <script>
            // código javascript
        </script>
        ...
    </html>
    ```
- **Opción 2** (recomendada) hacer referencia a un archivo `.js` externo.
  
    ```html
    <!DOCTYPE html>
    <html>
        ...
        <body>
            ...
            <script src="path/del/archivo.js"></script> 
        <body>
    </html>
    ```
    
    Colocar el código JS al final del `<body>` _es una buena práctica_.
    
    También se pueden consumir código JS de terceros desde internet, cambiando el valor de `src` por una *URL*.

## Uso `console.log`

Es un método de registro, se utiliza __para fines de depuración__.

```javascript
/* cualquier valor*/
console.log("Hello, World!");

/* multiple valores */
console.log("Hello", "World");  //Hello World

/* objetos */
console.log({nombre: "Carlos Ramos"});

/* funciones */
console.log(function(){return "Hola"});

/*elementos HTML */
console.log(document.body)
```

Tambien existen otras variantes:

`console.error(<valor>)` imprime en rojo  
`console.info(<valor>)` imprime en gris  
`console.warn(<valor>)` imprime en amarillo

## Declarar variables
```javascript
var n1;         // sin valor (undefined)
var n2 = 'hola' // con valor (string)

// se puede omitir 'var' No recomiendado.
```

- Javascript es "__Case Sensitive__"
- Por convención las variables __comienzan con minúscula__.

## Tipos de datos

Tipos primitivos:
+ __String__: cero o mas caracteres encerrados entre comillas (') o (").

+ __Number__: incluye enteros, decimales, negativos, etc.

+ __Boolean__: dos valores true y false.
    > **Nota**: existen **falsy values** y **truthy values**, estos son valores que __se comportan__ como *false* y *true* respectivamente. 
    >
    > + __Falsy values__: `NaN`, `0`, `""`, `Null` y `Undefined`. 
    > + todo lo demás son __Truthy values__.
    
+ __Null__: no tiene valor .

+ __Undefined__: no definido.

    > Cuando declaramos una variable `var n;` es del tipo __undefined__.

Tipos compuestos
+ **Arrays**
+ **Object**

### String
Se denotan por comillas dobles o comillas simples, pero no ambas a la vez.
```javascript
var a = "nombre";
var b = 'apellido';
```
> Un string NO es un arreglo de caractares.

#### Caracteres de escape
Los más usados son:

* `\n` salto de línea
* `\t` tabulador


### Number
número entero, decimal, positivo o negativo.

```js
var numNatural= 1234;
var numEntero = -479;
var numDecimal = 3.141592;
var numDecimal2 = -0.123;
```

#### Base de numeración
Por defecto, el sistema de numeración es el decimal.
+ __Base Hexadecimal__ (base 16): anteponemos el prefijo `0X.`
+ __Base Octal__ (base 8): anteponemos un cero `0`.
```javascript
var n1 = 57; // número en base 10
var n2 = 012345; //base 8, porque empieza por 0
var n3 = 0xFF32; //base 16, porque empieza por 0x
```
#### Valores especiales para variables numéricas
+ __NaN__: no es un número. p.e. `1 * "hola"`.
+ __Infinity__: infinito, por ejemplo `3/0.`

### Null
Cuando una variable no contiene ningún valor.
```javascript
n = 'hola'
n = null; //libera memoria
```

### Verificar el tipo de dato de una variable

```js
var n = "hola";
typeof(n);
```

## Conversión entre tipos de datos

### Conversión implicita
```javascript
var a = "75";
var b = 25;
var res = a + b; // concatena: 7525
var res2 = a * b; // conversion implícita: 75*25 = 1875
```

> La conversión implícita se aplica cuando existe una __operación aritmética que no es la suma__. por ejemplo: `1 + "2"` retorna `"12"` (concatena)

### Conversión explícita
+ `parseFloat(cadena)` convierte en num. decimal, si es posible.

+ `parseInt(cadena, numero)` convierte a entero, el segundo argumento permite escoger la base (entre 2 y 36).

+ `(<num>).toString(argumento)` convierte *num* a string, si se pasa un número como argumento, cambia de base.
    ```javascript
    var n = 13;
    n.toString();     // retorna "13"
    n.toString(16);   // retorna ”d”
    n.toString(2);    // retorna “1101”
    ```

## Operadores

### Operadores lógicos y relacionales

    >, <, <=, >=
    ==  (igualdad de valor)
    !=  (diferente de valor)
    === (igualdad de tipo y valor)
    !== (diferente de tipo y valor)
    &&  (y)
    ||  (o)
    !   (No)

### Operadores aritméticos

    +   (para valores strings los concantena)
    -
    *
    /
    %   (Modulo) devuelve el resto de una division

### Contadores

- `a = a+1` es equivalente a escribir `a++`  
- `a = a-1` es equivalente a escribir `a--`  
- `num = num+2` es equivalente a escribir `num += 2`  
- `num = num*2` es equivalente a escribir `num *= 2`  
- `num = num/2` es equivalente a escribir `num /= 2`

> **Nota**: `++a` es un preincremento (incrementa antes de retornar el valor).

### Operador para evaluar si una variable fue definida

```javascript
var a   //undefined

var r = a || 10
console.log(r)  // 10

a = 5
r = a || 10
console.log(r)  //4
```

# Estructuras de programación

## Estructura "if-else"

    if(condición){
        sentencia;
    } else {
        sentencia;
    }

### If else if

    if(condicion1){
        sentencia;
    }else if (condicion2){
        sentencia;
    } else {
        sentencia;
    }

### Operador ternario

    var res = if (condicion) ? <valor(evaluado-a-True)> : <valor(evaluado-a-False)> 

## Estructura "while"

    while(condición){
        sentencia;
    }

## Estructura "do while"

    do {
        sentencia;
    } while(condición)

> Se ejecutará al memos una vez el bloque `do`.

## Estructura "for"
    for(i=i; i<10; i++){
        sentencia;
    }

### Ciclo "for in"
Se usa para recorrer los _indices de arrays_ o _propiedades_ de un objeto.

```javascript
var miObj = {
    nombre: "Carlos",
    apellido: "Ramos"
}

// Iterar propiedades de un objeto
for(prop in miObj) {
    console.log(prop)   //nombre apellido
}

// Iterar un array
for(idx in [1,2,"hola",false]){
    console.log(idx)    //0 1 2 3
}
```

### Ciclo "for of" FALTA

### Ciclo "for each"

Es un método de lista que permite iterar sus elementos. Enviar como argumento una función.

```javascript
    [1,2,"hola",false].forEach(
        function(item) {
         console.log(item)   //1 2 "hola" false
        }
    );
```

## 

## Sentencias "break" y "continue"

    for(...){
        if(condicion)
            break;      //detiene el loop (ciclo for)
        if(otracondicion)
            continue;   //salta al siguiente número del ciclo, es decir,
           				//ya no ejecuta las sentencias de abajo.
            
        sentencias;  //no ejecutarán estas sentencias si ejecutó 'continue'.
    }

## Estructura "switch-case"

La estructura `switch` recibe como parámetro un valor que será comparado con cada caso, 

    switch(opcion){
        case <valor-1>:
            sentencias;
            break;
        case <valor-2>:
            sentencias;
            break;
        default:
            sentencias;
    }

> **Nota**: Se recomienda añadir la instrucción `break` en cada caso, para que termine las comparaciones siguientes.

## Estructura "do-while"

    do{
        sentencias;
    } while(condicion);

# Arrays
Un *array* es un conjunto de elementos colocados de forma adyacente en la memoria de manera que nos podemos referir a ellos con un solo nombre común.

Los *arrays* en *JavaScript* **son dinámicos** (tamaño variable) y **pueden contener valores de cualquier tipo**.

El indice de un *array* comienza en `0` , es decir, el primer elemento esta en la poción `0`, el seguno en `1`, así sucesivamente.

```javascript
// Definir un array
var miArray = new Array();
var arr = [] 	//otra forma de definir

// Asignar valores a un array
miArray[0] = "texto";            //string
miArray[1] = 100;                //number
miArray[2] = {nombre: "Carlos"}; // object
miArray[3] = function() {/* instrucciones*/};   //function 

//Acceder a un elemento de un array
var item = miArray[i] //donde i es el indice y empieza por 0, 1, ...`

```

En *JavaScript* las *arrays* siempre son  __(1 dimensión) y dinámicas__, pero se puede simular matrices multidimensionales. 

## Simular matriz multidimensional

*JavaScript* no soporta directamente matrices (*arrays* de dos o más dimensiones).

```javascript
var Matriz2D=new Array(5);
for(i=0;i<=4;i++)
{
    Matriz2D[i]=new Array(5);
}
```

Para acceder a sus elementos:

```js
Matriz2D[0][0] // primer elemento de la matriz.
```

## Funciones de arrays

```javascript
var arr = [5,4,3,2,1]

// Obtener el tamaño de un array
var len = arr.length //5

var arrReverse = arr.reverse()  //[1,2,3,4,5]

var joinArr = arr.join()    //"1,2,3,4,5"
var joinArr = arr.join("|") //"1|2|3|4|5"

var splitArr = joinArr.split("|")   //[1,2,3,4,5]

arr.push(6)      //[1,2,3,4,5,6]
arr.unshift(0)   //[0,1,2,3,4,5,6]

var ultimoElem = arr.pop()   //6 y arr: [0,1,2,3,4,5]
var primerElem = arr.shift() //0 y arr: [1,2,3,4,5]

// lastIndexOf() busca un elemento y devuelve su posición.
var miArr = [1,2,3,2,5]
pos = miArr.lastIndexOf(2)  // 3 porque la busca empieza de atras.

// slice() devulve una copia de una parte del array.
// arr.slice(<pos-ini>, <pos-fin>); <pos-fin> es no incluido.
var miArr = [1,2,3,4,5];
miArr.slice(1, 3)     //retorna: [2,3]
miArr.slice(1, 4)     //retorna: [2,3,4]
miArr.slice(1, 10)    //retorna: [2,3,4,5]
miArr     // [1,2,3,4,5] No se modifica el original

// 'splice()' Extrae y añade/reemplaza (opcional)
// arr.splice(<pos>, <cantEliminar> [, <valReemplazo-1>, ...])
var miArr = [0,1,2,3,4,5];
miArr.splice(2, 3)            //retorna: [2,3,4] y miArr: [0,1,5]
var miArr = [0,1,2,3,4,5];
miArr.splice(3, 1, "tres")    //retorna: [3] y miArr: [0,1,2,"tres",4,5]
var miArr = [0,1,2,3,4,5];
miArr.splice(1, 0, true, -1)  //retorna: [] y miArr: [0,true,-1,1,2,3, 4, 5]

// fill() cambia elementos por un valor específico.
// fill(<valor>,<pos-ini>,<pos-fin>) (pos-fin es no incluido)
var arr = [1,2,3,4,5];
arr.fill(7, 3);		// retorna: [1,2,3,7,7] y arr [1,2,4,7,7]
var arr = [1,2,3,4,5];
arr.fill(7, 1, 3);	// retorna: [1,7,7,7,5] y arr [1,7,7,7,5]

```
## Funciones avanzadas de arrays
```javascript
// Recorrer un array
arr.forEach(function(item) {
    console.log(item)   //1 2 "hola", false
})

// La funcion "map" retorna un array modificado
var arrDoble = arr.map(function(elem) {
    return elem * 2 
})  //[10.8.6.4.2]
```

# Manejo de errores

La forma normal

```javascript
try {
    //Alguna instrucción sensible a dar error
    //por ejm lectura de entradas, archivos, tipos de datas
} catch(err) {
    //Si ocurre algun error se ejecutará este bloque.
    console.log(err)
} finally {
    // Este bloque es opcional.
    //Las instrucciones de este bloque siempre se ejecutará
}
```

Lanzar errores de forma intensionada.

```javascript
try {
    // ...
    if(hayErrores){
        //Lanzando el error
        throw new Error("Mensaje sobre el error.")
    }
} catch(err) {
    console.log(err.message()) // ("Mensaje sobre el error."
}
```

Lanzar errores personalizados

```javascript
try {
    // ...
    if(hayErrores){
        //Lanzando el error
        throw "Este es el mensaje de error" //enviando un string
    }
} catch(err) {
    console.log(err) // ("Este es el mensaje de error"
}

// Tambien se puede enviar un objeto o funcion
try {
    // ...
    if(hayErrores){
        //Lanzando el error
        throw {
            tipo: 1,
            mensaje: "mensaje de error"
        }
    }
} catch(err) {
    console.log(err.tipo) // 1
    console.log(err.mensaje) // "mensaje de error""
}
```

