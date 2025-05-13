# Funcion constructor

JavaScript no tenia clases, por lo que la POO se conseguia a través de constructores y prototipos. Pero ES6 ya incorpora clases.

En JS existen constructores nativos del lenguaje.
```javascript
var fecha = new Date();

var num = new Number(10);  // NO RECOMENDADO HACER USO DE ESTOS CONSTRUCTORES PARA TIPOS PRIMITIVOS,

// En ves de constructores definir mediante su valor
var num = 10; 
```

Definiendo una clase con la función constructor.

```javascript
//Definimos una función que simulará la "Clase"
function Persona(nom, ape){
    this.nombre = nom
    this.apellido = ape
    this.presentarse = function(){
        return "Me llamo " + this.nombre
    }
}

var p1 = new Persona("Carlos", "Ramos")
p1.presentarse();   //"Me llamo Carlos"

var p2 = new Persona("Luis", "Quispe")
p2.apellido     //"Quispe"
```
> Por convención la primera letra de la clase empieza en mayúscula

## Propiedades públicas y privadas
Las __propiedades públicas__ son accesibles y modificables desde las instancias.

En cambio las __propiedades privadas__ no se puede acceder a su valor desde afuera, para accederlos es a través de sus métodos.

```javascript
function Pais(nombre, capital){
    this.nombre = nombre;   // prop. publica
    this.capital = capital; // prop. publica
    
    var idioma = "Español"  // prop. privada
    this.getIdioma = function(){
        return idioma
    };
    this.setIdioma = function(val){
        idioma = val;
    }
}

var bolivia = new Pais("Bolivia", "La Paz");
// Acceder/Modificar a propiedades publicas
bolivia.capital = "Sucre"

// Acceder/Modificar a propiedades privadas
console.log(bolivia.getIdioma()); //"Español"

bolivia.setIdioma("Quechua");
console.log(bolivia.getIdioma()); //"Quchua"
```

## Métodos públicos y privados
Los **métodos públicos** son funciones que se pueden **acceder desde las instancias**.

Los **métodos privados** solo pueden ser invocados desde funciones públicas del mismo objeto.

```javascript
function Persona(nom, ap){
  this.nombre = nom;
  this.apellido = ap;
    
  this.saludar = function(){    // método público
    return "Buenos días, me llamo " + nombreCompleto(); 
  };
    
  var _this = this;
  function nombreCompleto(){    // método privado
      return _this.nombre+ " "+ _this.apellido;
  }
}

var p1 = new Persona("Carlos", "Ramos");
p1.saludar();
```

## Propiedades de clase ("Atributos estáticos")
Son propiedades que perteneces a la clase. No son accesibles ni modificables desde las instancias. 
```javascript
function Prestamo() {
    //Definimos la clase Prestamo ...
}

// Definiendo una propiedad de clase/atributo estático
Prestamo.interes = 0.12;

var p = new Prestamo();
console.log(p.interes) // undefined! 
// la instancia "p" no puede acceder al valor de la propiedad "interes".

console.log(Prestamo.interes)    //0.12
```

## Métodos de clase ("métodos estáticos")
Son funciones que no pueden ser accedidos desde las instancias. Solo se puede acceder desde la clase.
```javascript
function Calculo(){
	//Definimos la clase Calculo ...
}

//definiendo el método de clase
Calculo.piesAMetros = function(pies){
  return pies * 0.3048;
};

Calculo.piesAMetros(10)
```

## Herencia
```javascript
// Clase padre 
function Mascota(nombre,color){
    this.nombre = nombre;
    this.color = color;
}
// Clase hija (hereda de la clase Mascota)
function Perro(nombre,color,raza,edad){
    Mascota.call(this,nombre,color);
    this.raza = raza;
    this.edad = edad;
}

//instanciar objetos
var duque = new Perro("duque","negro", "doberman",5);
var neron = new Perro("neron","marron","pastor aleman",4);
```