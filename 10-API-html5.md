# Canvas (lienzo)
Permite dibujar sobre un área.

> Los elementos dibujados no forman parte del DOM.

```html
<canvas id="lienzo" width="500" height="300"> </canvas> 
```
```javascript
// Obtener el elemento
var canvas = document.getElementById('lienzo');

// Obtener las dimensiones
var w = canvas.width;
var h = canvas.height;

// Obtener el contexto
var c = canvas.getContext('2d');
// Sobre el contexto se dibujará usando métodos y propiedades
c.strokeStyle = "red";
```
Para dibujar con canvas se realiza a través de métodos y propiedades.

PROPIEDADES

    .strokeStyle  -> define el color de la linea
    .lineWidth    -> el ancho de la linea
    .fillStyle    -> color de relleno

MÉTODOS

    .stroke()     -> dibuja una linea
    .fill()       -> dibuja un relleno
    .beginPath()  -> comienza una ruta
    .closePath()  -> cerrar una ruta
    .moveTo()     -> para moverse a un punto

FORMAS

    .lineTo()     -> define una linea que culmina en el punto determinado
    .rect()       -> dibuja un rectangulo,
                     requiere x,y,w,h
    .arc()        -> dibuja arcos de circulo
                     Parametros:
                        cx (centro x)
                        cy (centro y)
                        r  (radio)
                        startAngle (angulo de inicio)
                        endAngle (angulo de final)
                        sentido (boolean)
    
                                270 (3PI/2)
                        180(PI)               0
                                  90(PI/2)

TEXTO

    .strokeText()
    .fillText()
      parametros: "texto",x,y

```javascript
// for(var i = 0; i < 30; i++){
//   c.moveTo(0, i * 10);
//   c.lineTo(w,i *10);
// }
// c.strokeStyle = "red";
// c.stroke();

// c.rect(50,50,200,100);
// c.fillStyle = "red";
// c.strokeStyle = "green";
// c.lineWidth = 10;
// c.stroke();
// c.fill();

// c.font = "bold 40px Arial";
// c.lineWidth = 2;
// c.fillText("Hola Mundo",50,200);
// c.strokeText("Adiós mundo",50,250);

c.arc(w/2, h/2, 120,0, Math.PI * 2);
c.fillStyle = "red";
c.fill();
```
<!--BUSCAR UN EJERCICIO INTERESANTE-->

# Audio y video

EVENTOS

    'play'  (cuando se reproduce)
    'pause' (cuando se pausa)
    'ended' (cuando termina el video)

MÉTODOS

    play()
    pause()
    load()

PROPIEDADES

    currentTime   -> tiempo actual de reproduccion
    duration      -> la duracion total del video
    volume        -> nivel de volumen (0 a 1)

```html
<video src="mi-video.mp4" id="video" controls> </video>
```

```javascript
var video = document.getElementById('video');

video.addEventListener('play', function(){
  console.log("se esta reproduciendo el video");
});
video.addEventListener('pause', function(){
  console.log("se ha pausado el video");
});
video.addEventListener('ended', function(){
  console.log("el video ha terminado");
});
```
<!--BUSCAR UN EJERCICIO INTERESANTE-->

# Geolocalización

Se usa el objeto `gelocation` que es una propiedad del objeto `navigator`,
tiene tres métodos relevantes:

    .getCurrentPosition() -> detecta la posicion actual
    .watchPosition()      -> detecta la posicion actual y va actualizandola en el tiempo.
    .clearWatch()         -> detiene watchPosition

El método `navigator.geolocation.getCurrenPosition(exito,error)` recibe dos *callbacks*:

- exito, si se logra determinar la posición (requerido)
- error, si no se logra determinar la posición (opcional)

El *callback* "exito" recibe un parámetro (objeto de la clase Position) que almacena los datos de la geolocalización.

Ejemplo
```javascript
var miUbicacion = navigator.geolocation;
miUbicacion.getCurrentPosition(function(p){
  console.log(p.coords.latitude);
  console.log(p.coords.longitude);
});
```

 Para comprobar si el navegador es compatible con la API de geolocalización:

```js
if(navigator.geolocation){
    // Horray! Support!
} else {
    // No support...
}
```

# Almacenamiento web

## LocalStorage
El objeto localStorage proporciona un almacenamiento del tipo valor-clave persistente (pero no permanente) de cadenas.

Los valores almacenados persisten indefinidamente a menos que el usuario borre los datos guardados o configure un límite de caducidad.

El límite del almacenamiento varia y depende del navegador (aprox. 2MB a 10MB)

```javascript
// Guardar un dato
localStorage.setItem('name', 'John Smith');

// Obtener un dato
var data = localStorage.getItem('name'); // "John Smith"

// Eliminar un dato
localStorage.removeItem('name');

// Borrar todo el almacenamiento
localStorage.clear();

// Obtener el número de elementos guardados
localStorage.length;
```

### Guardar datos estructurados (JSON)
```javascript
var players = [{name: "Tyler", score: 22}, {name: "Ryan", score: 41}];

localStorage.setItem('players', JSON.stringify(players));

console.log(JSON.parse(localStorage.getItem('players')));
// [ Object { name: "Tyler", score: 22 }, Object { name: "Ryan", score: 41 } ]
```
### Evento "storage"
Siempre que se establezca un valor en localStorage, se enviará un evento de `storage` en todas las demás `windows` desde el mismo origen. 

Esto se puede usar para sincronizar el estado entre diferentes páginas sin recargar o comunicarse con un servidor.

Primera ventana
```javascript
var input = document.getElementById("myInput");

input.value = localStorage.getItem('user-value');

input.addEventListener("input", function(event) {
    localStorage.setItem('user-value', input.value);
});
```

Segunda ventana
```javascript
var output = document.getElementById('p');

output.textContent = localStorage.getItem('user-value');

window.addEventListener('storage', function(event) {
    if (event.key === 'user-value') {
        output.textContent = event.newValue;
    }
});
```
> El evento no se activa ni se puede capturar en Chrome, Edge y Safari si el dominio se modificó mediante un script.

## SessionStorage
El objeto `sessionStorage` implementa la misma interfaz que `localStorage`.  Pero tiene dos diferencias:
- Los datos de `sessionStorage` se almacenan por separado para cada ventana
- Los datos solo persisten durante el tiempo que están abiertas las ventanas.

```javascript
// Guardar datos en sessionStorage
sessionStorage.setItem('key', 'value');

// Obtener datos guardados de sessionStorage
var data = sessionStorage.getItem('key');

// Eliminar datos guardados de sessionStorage
sessionStorage.removeItem('key')
```

## Alternativa simple de manejo del almacenamiento
`localStorage` y `sessionStorage` son objetos por tanto se pueden guardar datos agregandoles atributos.

```javascript
// Set
localStorage.greet = "Hi!"; // localStorage.setItem("greet", "Hi!");

// Get
localStorage.greet; // localStorage.getItem("greet");

// Remove item
delete localStorage.greet; // localStorage.removeItem("greet");

// Clear storage
localStorage.clear();
```