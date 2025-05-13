# ECMAScript 6

ECMAScript 6 es la nueva versión del lenguaje estándar ECMAScript que esta terminada desde Junio de 2015.

## Variables y constantes

Las variables siguen existiendo
```javascript
var numero = 5;
```

Variables de bloque (block-scope), su usa `let`
```javascript
for(let i=0; i<10; i++) {
    console.log(i); // 0, 1, 2, ... , 9
}
console.log(i)  // Undefined
```

Las constantes se declara con `const`, matinenen su valor durante la ejecución.
```javascript
const year = 2020;
// ...
year = 2021;    // Error no se permite cambiar el valor
```

## Parámetros

### Valores por defecto
```javascript
function saludar(nombre="anónimo") {
    console.log("Hola " + nombre);
}

saludar();  // "Hola anónimo"
```

### Parámetros spread
Permiten pasar arrays que se cotejen con los parámetros de una función.
```javascript
function sumar(a,b,c){
  return a + b + c;
}

var miArray = [4,5,6];
// se deben poner tres puntos delante del array
var resSuma = sumar(...miArray);
console.log(resSuma);
```

### Parámetros rest
Consiste en pasar un número indeterminado de parámetros.
```javascript
function sumar(...elementos){
  var suma = 0;
  for(let i= 0; i <elementos.length; i++){
    suma += elementos[i];
  }
  return suma;
}

console.log(sumar(1,2,3,4));
```

## Arrow functions (funciones de flecha)
Es una __nueva sintaxis__ para __funciones anónimas__

- __Los parámetros__ se pasan entre paréntesis.
    ```javascript
    var miFuncion = (param1, param1) => {
            console.log("Funcion con parámetros: "+param1+" y "+param2);
        };
    ```
- Si es __un solo parámetro__, se omite los parentesis. 
    ```javascript
    var miFuncion = param1 => {
            console.log("Función con un parámetro: "+param1);
        };
    ```
- Si la función __no recibe parámetros__ se escriben los paréntesis vacios `()`
    ```javascript
    var miFuncion = () => {
            console.log("Función sin parámetros");
        };
    ```
- Si la función __retorna un valor y__ solo tiene __una linea de código__, se omite `return` y las llaves `{ }` 
    ```javascript
    var suma = (a,b) => a + b;
    ```
- Si la función retorna un valor y tiene multiples lineas de código, se usa `return`
    ```javascript
    var texto = () => {
        var text = "";
        // ... 
        return text;
    }
    ```
- Si la función devuelve un objeto directamente, se indica entre paréntesis después de la flecha.
    ```javascript
    var estudiante = (nombre,apellido) => ({
        nombre: nombre,
        apellido: apellido
    });
    var est1 = estudiante("Andre", "Soto");
    ```
### Lexical this
Dentro las funciones de flecha, `this` se refiere a su contexto (sin importar si está dentro de otra función)

```javascript
function Persona(){
  this.edad = 0;
  setInterval(() => {this.edad++},2000);    //this se refiere a Persona
  this.getEdad = () => this.edad;
}
```

## Desestructuración
Permite extraer valores de objetos y arrays y almacenarlos en variables en una sola línea de código.
```javascript
var dias = ["lunes","martes","miercoles"];
var amigo = {
  nombre: "Jorge",
  edad: "40",
  pais: "España"
};

var [dia1,dia2,dia3] = dias;
var {nombre,edad,pais} = amigo;

console.log(dia2);  //"martes"
console.log(nombre);  //"Jorge"
```
## Interpolación
Utilizar las variables dentro de cadenas.
```javascript
var nombre = "Carlos";
var pais = "Bolivia";

// forma antigua
var saludar1 = "hola " + nombre + ", bienvenido a " + pais;

// con interpolacion
var saludar2 = `hola ${nombre}, bienvenido a ${pais}`;
```

## For of
Para recorrer arrays

```javascript
var meses = ["enero","febrero","marzo","abril"];

for(let mes of meses){
  console.log(mes);
}
```

## POO
Definir __clases__

```javascript
class Persona {
    constructor(nombre,apellido,edad,pais,sexo,casado){
        this.nombre = nombre;
        this.apellido = apellido;
        this.pais= pais;
    }
    saludar(){
        return  `Hola, me llamo ${this.nombre} ${this.apellido} y vivo en ${this.pais}.`;
    }
}

var yo = new Persona("Carlos", "Felipe", "Bolivia");
```

Hacer __herencia__

```javascript
class Empleado extends Persona {
  constructor(nombre, apellido, pais, cargo, empresa){
    super(nombre, apellido, pais);
    this.cargo = cargo;
    this.empresa = empresa;
  }
  describirTrabajo(){
    return `Trabajo como ${this.cargo} en ${this.empresa}.`;
  }
}

var secretaria = new Empleado("Sandra","Canales","Colombia","secretaria","Facebook");
```