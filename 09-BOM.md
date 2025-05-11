# BOM (Browser Object Model)

El BOM es el modelo de objetos del navegador. Son objetos que modelan cosas como el historial, pantalla, etc (información sobre el navegador).

A traves de las propiedades y métodos del objeto global `window` se pueden acceder a informacion sobre el navegador y sus componentes.

    window -----|------ document -----|---- forms
                |                     |
                |					  |---- images
                |                     |
    KEY         |------ history       |---- links
                |                     |
                |------ location      |  ...
     Object     |
                |------ navigator
     Array      |
                |------ screen

- `window` : representa la ventana o **pestaña actual del navegador**.
- `document`: representa la página web actual (**DOM**).
- `history`: representa páginas en el **historial** del navegador.
- `location`: representa la **URL** de la página **actual**.
- `navigator`: representa **información sobre el navegador**.
- `screen`: representa la información de la **pantalla del dispositivo**.

## window 

Window es el objeto global. 

__Propiedades:__

- `.innerWidth`   -> devuelve al ancho del viewport

- `.innerHeight`  -> devuelve el alto del viewport

- `.outerWidth`   -> devuelve el ancho del navegador

- `.outerHeight`  -> devuelve el alto del navegador

- `.screenX`  posicion X de la ventana respecto al borde izquierdo de la pantalla

- `.screenY` posicion Y de la ventana respecto al borde superior de la pantalla

  La posición X=0 y Y=0 es la parte superior izquierda de la pantalla.

- `.pageXOffset`  -> indica la cantidad de scroll que se hizo en el eje X

- `.pageYOffset`  -> indica la cantidad de scroll que se hizo en el eje Y

Métodos
- `.alert('string')`  -> muestra un mensaje
- `.prompt('string')` -> pide información al usuario y la devuelve
- `.confirm('string')` -> hace una consulta al usuario y devuelve un boolean
- `.open('url')` -> abre una nueva ventana
- `.close()`     -> cierra una ventana
- `.moveTo(x, y)`    -> mover la ventana
- `.resizeTo(w, h)`  -> redimensiona la ventana
- `.scrollTo(x,y)`  -> mueve el scroll a las coordenadas indicadas
- `.scrollBy(x,y)`  -> mueve el scroll a partir de su posicion actual
- `.print()`       -> imprimir los contenidos de la página actual

> alert(), prompt() y confirm(), __No es recomendado su uso__, porque bloquea la ejecución de JS hasta que se cierre la ventana emergente. 

Ejemplo:
```javascript
var boton = document.getElementById('boton');

boton.addEventListener('click',function(){
    window.open('http://escuela.digital');
    // 
});
```
> Para acceder a las propiedades y métodos del objeto `window`, se puede omitir el nombre del objeto y llamar directamente a sus propiedades y métodos. p.e. `innerWith, innerHeight, alert(), open(), etc.`

## Navigator

Contiene información sobre el navegador

No hay estándares definidos sobre la informacion que devuelve cada navegador, sin embargo, todos los principales navegadores lo admiten.

El siguiente código se puede usar para obtener información básica sobre el navegador
```javascript
navigator.userAgent, // Get the User-agent
navigator.cookieEnabled, // Checks whether cookies are enabled in browser
navigator.appName, // Get the Name of Browser
navigator.language, // Get the Language of Browser
navigator.appVersion, // Get the Version of Browser
navigator.platform // Get the platform for which browser is compiled
```

Dentro del objeto navigator está el objeto geolocation que permite la geolocalización.

```javascript
var geolocation = navigator.geolocation;
```

Tambien se puede usar para obtener información el dispositivo movil

```javascript
// Obtener el nivel actual de la batería
navigator.getBattery().then(function(battery) {
    // Battery level is between 0 and 1, so we multiply it by 100 to get in percents
    console.log("Battery level: " + battery.level * 100 + "%");
});

// Vibrar el dispositivo durante 100 ms:
navigator.vibrate(100);
```

Ejemplo: Comprobar que se está usando el navegador Chrome

```javascript
if(window.chrome !== undefined){
    alert("Estas usando Chrome")
}
```
> No hay una manera única de saber que navegador está usando el usuario. Pero se puede usar la siguiente sugerencia [How to detect Safari, Chrome, IE, Firefox and Opera browser?](https://stackoverflow.com/questions/9847580/how-to-detect-safari-chrome-ie-firefox-and-opera-browser)

## Location
Location da información sobre la URL. Ejemplo; 

`https://developer.mozilla.org/es/docs/Learn/JavaScript#prerrequisitos`

Propiedades:

- `.href`   -> url completa p.e. `https://developer.mozilla.org/es/docs/Learn/JavaScript#prerrequisitos`
- `.hash`   -> devuelve la parte con #. p.e. `#prerrequisitos`
- `.host`   -> devuelve la info del host. p.e. `developer.mozilla.org`
- `.hostname` -> 
- `.protocol` -> devuelve el protocolo (http, https), p.e. `https:`
- `.port`     -> devuelve el puerto, p.e. ?????
- `.origin` -> devuelve el **dominio** (sin path). p.e. `https://developer.mozilla.org`
- `.pathname` -> el path (sin el dominio p.e.` /es/docs/Learn/JavaScript`)

Métodos:

- `assign('url')`  -> redirecciona hacia la URL
- `replace('url')` -> redirecciona sin meter la página al historial

Ejemplo: Redirigir con href
```javascript
var navigate = document.getElementById('navigate');
navigate.addEventListener('click',function(){
    location.href ="www.google.com";
});
```

## HISTORY

Contiene el historial de la pestaña activa

Métodos:
- `back()`     -> Retroceder
- `forward()`  -> Avanzar
- `go(<numero>)` -> Moverse en el historial, numeros positivos avanza hacia adelante y con negativos hacia atras.

> Por seguridad no se puede acceder a las URL del historial

# Funciones de tiempo
Existen dos métodos del objeto `window` para controlar la ejecución del código según el tiempo:

## setTimeout
Ejecutará el codigo despues de un cierto tiempo. 

Sintaxis: `setTimeout(fn, delay)`, 
- `fn`: una función que contiene el código que se ejecutará
- `delay`: es el tiempo en ms

```javascript
setTimeout(function(){
    console.log("Se imprimirá despues de 1 segundo")
}, 1000)    //segundo parametro se envia en miliseg.
```
## setInterval
Ejecutará el código ciclicamente en un intervalo de tiempo

Sintaxis: `setInterval(fn, interval)`
- `fn`: función que contiene el código que se ejecutará
- `interval` el intervalo de tiempo en ms.

```javascript
setInterval(function(){
    console.log("Se imprimirá cada 2 segundo")
}, 2000)
```

Para detenr el intervalo, `clearInterval()`. 
```javascript
var btn = document.getElementById('btn');

var intervalo = setInterval(function(){
        console.log("Se imprimirá cada 2 segundo")
    }, 2000)

btn.addEventListener("click", function(e){
    clearInterval(intervalo)    //para detener el intervalo
})
```

EJERCICIO: RELOJ
```javascript
var reloj = document.getElementById('reloj');

var getHour = function(){
    var fecha = new Date();
    var horas = fecha.getHours();
    var minutos = fecha.getMinutes();
    var segundos = fecha.getSeconds();
    if(segundos < 10){
        segundos = '0' + segundos;
    }
    reloj.textContent = horas + ':' + minutos + ':' + segundos;
};
setInterval(getHour,1000);
```