# Herramientas de desarrollor de Chrome

## Pestaña "Source"

Contiene los archivos html css js de la página.

### Breakpoint
Se puede Colocar breakpoints haciendo click sobre el número de linea en el que se desea detener la ejecución del código.

### Watch
La pestaña "Watch" es para evaluar una expresion, colocar el nombre de una variable que haya sido definia en el código JS. 
Mientras avanza la ejecución del código, se irá actualizando el valor de la variable observada. 

### DOM Breakpoints
Escucha los cambios de elementos del dom.

1. ir a la pestaña "Elements" 
2. click derecho (sobre el elemento (tag) que se quiere observar) > Break on ... > (hay tres opciones)
    1. subtree modificafion (ver cualquier modificacion de los nodos hijos y/o nietos)
    2. Attributes modification ()
    3. Node removal (ver si se eleminia el elemento) 

### Snippets (panel izquierdo)
 
Para crear codigos de prueba,


### XHR Breakpoints
para ajax

BUSCAR COMO SE USA Y EJEMPLOS 


### Event listener Breakpoints
Par escuchar un evento
BUSCAR COMO SE USA Y EJEMPLOS 

## Pestaña "Network"
Contiene todo los recursos y archivos que se carga en la página. y tiempo de demora en carga

## Psstaña "Console"
Consola de JS
ver console.table(array2D ) 


# jQuery
Se seleccionan elementos del DOM con `$('')`

Se pasa como parámetro cualquier __selector CSS válido__.
Esta seleccion devuelve un objeto jQuery y los métodos de jQuery devuelven un objeto jQuery lo que permite encadenar métodos fácilmente.

var button = $('button').css({
  background: "red",
  "font-size": "20px",
  border: "none"
});


# NODE JS

Es la implementación de JavaScript en el servidor.

## Aplicaciones isomÃģrficas
Se denominan a las apps que tienen JS en el backend y el frontend.

## npm -> Node package manager

    npm install <modulo> -g          (instala globalmente el modulo, osea en la máquina)
    npm install <modulo> --save      (instala como dependencia del proyecto)
    npm install <modulo> --save-dev  (instala como dependencia de desarrollo)

> Aunque tu proyecto no sea con Node, Node te puede ayudar en la etapa de desarrollo p.e. minificar css y js y otras cosas.

### Para comenzar un proyecto
Ejecutar el comando:

    npm init
   
Esto crea un archivo package.json con toda la información del proyecto y sus dependencias.

En caso de clonar un proyecto, se debe ejecutar:

    npm install

Este comando lee el package.json e instala las dependencias definidas.

Ejemplo:
Instalar un servidor http.

Ejecutar: 

    npm install http --save-dev

Crear un archivo app.js y escribir:
```javascript
// Ejemplo de conexion
var http = require('http');
var server = http.createServer(function(req,res){
  res.write('<h1>Hola mundo desde Node JS</h1>');
  res.end();
}).listen(3000,function(){
  console.log('Servidor corriendo en el puerto 3000');
});
```

> Si quieres trabajar más rapido usa Express


# Gulp
Sistema de automatización de tareas.

    npm install -g gulp          (1 sola vez)

    npm install --save-dev gulp  (para cada proyecto)
    
    crear un gulpfile.js         (en la raiz del proyecto)

Métodos de GULP

    .task('nombreTarea',*['tareas previas'], function);
    .src('path')
    .dest('path')
    .watch('path', ['nombreTarea']) //cada vez que hay cambios en el 'path' se ejecutan las tareas.
    
    // Además
    .pipe()  -> encadena un proceso (stream) con el siguiente

Para cada tarea se usa un plugin (o modulo de node). Cada uno tiene su propia documentacion.

Ejemplo: 
```javascript
var gulp = require('gulp');
var concat = require('gulp-concat');

gulp.task('unir',function(){
  gulp.src('./js/*.js')
    .pipe(concat('final.js'))
    .pipe(gulp.dest('./js/'));
});

gulp.task('default',function(){ //
  gulp.watch('./js/*.js',['unir']);
});

// para ejecutar las tareas, ir a la consola y escribir: gulp,
// como se difinio la tarea "default" no es necesario enviar el nombre
// de la tarea como parámetro del comando gulp.
```

# Otros
Angular

React

Yeoman

Ionic Framework 

electron js