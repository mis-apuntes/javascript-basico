# Eventos
Es todo lo que ocurre en la aplicación/pagina web.

Por ejemplo:

- Que el usuario haga clic
- Que el usuario reproduzca un video
- Que el usuario haga scroll
- Que la página cargue completamente

Estos eventos son capturados por el navegador y con JavaScript podemos ejecutar funciones en el momento que ocurran.

Todo evento está asociado a un elemento HTML. sin embargo también podrían asociarse al objeto global `window`.

Sintaxis: 

```
<elementoHtml>.addEventListener(<tipoEvento>, <callBack>);
```

+ `<elementoHtml>`: es un objeto que debe hacer referencia a una etiqueta html.

+ `<tipoEvento>`: es un string que indica el tipo de evento que va a escuchar. p.e. *click*, *keypress*, etc. (ver [Tipos de eventos](#tipos-eventos))

+ `<callBack>`: es la función que se ejecutará si se activa el evento.

Ejemplo 1: Botón que da la hora

```javascript
(function(){
	var btnTime = document.getElementById('btnTime');
    var tagMostrar = document.getElementById('showTime');

    btnTime.addEventListener('click', function(){
    	var hoy = new Date();
        tagMostrar.textContent = hoy.getHours() +':'+ hoy.getMinutes() +':'+ hoy.getSeconds();
    });
})();
```

Ejemplo 2: Obtener el tamaño de la ventana (evento asociado al objeto global)
```javascript
(function(){
  addEventListener('resize', function(){
      var w = window.innerWidth,
      h = window.innerHeight;
      console.log('La ventana mide ' + w + ' x ' + h);
  });
})();
```

## Objeto "event" 

El objeto event tiene información sobre el evento.

```javascript
var boton = documento.getElementById("btn");

boton.addEventListener("click", function(event) {
    console.log("Evento disparado")
    console.log(event)  // 'event' es un objeto que tiene informacion extra sobre el evento
    console.log(event.x) //posicion 'x' de donde se hizo click
    console.log(event.y) //posicion 'y' de donde se hizo click
    
    console.log(e.target) // elemento sobre el cual se hizo click
    console.log(e.which)  // 1: clic izq, 3: clic der
    // ...
})
```
> Por convención se suele llamar "e" o "event".

### Método `preventDefault()`
Es un método del objeto "event", que evita que se tengan comportamientos predeterminados de ciertos eventos:
- En formularios evita que se haga 'Submit'.
- En enlaces evita que se redireccione. 
- Cuando se pulsan las 'teclas flecha' evita el scroll.
- Etc.

```javascript
linkExt.addEventListener("click", function(e){
    // ...
    e.preventDefaul()  // evita comportamiento por defecto del link.
})
```

### Método `stopPropagation()`
Cuando un evento se activa, también se activan los eventos de sus ancestros (propagación de evento). Para detener la propagación, se utiliza `.stopPropagation()` del objeto "event" 

```javascript
/* html
<div id="container"> 
	<button id="button">pulsar</button> 
</div>
*/

var container = document.getElementById('container');
var boton = document.getElementById('button');

boton.addEventListener('click', function(e){
    console.log("Hiciste click en el boton");
    e.stopPropagation();
});

container.addEventListener('click', function(){
    console.log("Hiciste click en el container");
});
```
## Tipos de eventos

<a id="tipos-eventos"></a>

### Relacionados con el mouse:

| Evento      | Descripción                                                  |
| ----------- | ------------------------------------------------------------ |
| click       | cuando se pulsa el boton izq                                 |
| dblclick    | Cuando se hace doble click                                   |
| mouseenter  | Cuando entra en el area del elemento                         |
| mouseleave  | Cuando sale del área del elemento                            |
| mousemove   | Cuando se mueve el cursor dentro un elemento.                |
| mousedown   | Cuando se pulsa el boton del raton (ocurre antes de soltar)  |
| mouseup     | El boton del raton se libera. (ocurre luego de soltar)       |
| contextmenu | click derecho=?                                              |
| moseover    | The event occurs when the pointer is moved onto an element, or onto **one of its children** |
| mouseout    | The event occurs when a user moves the mouse pointer out of an element, or **out of one of its children** |

> [Mouseover and mouseenter example](https://www.w3schools.com/jquery/tryit.asp?filename=tryjquery_event_mouseenter_mouseover#:~:text=mouseenter%20and%20mouseover.-,The%20mouseover%20event%20triggers%20when%20the%20mouse%20pointer%20enters%20the,moved%20over%20the%20div%20element.)

EJERCICIO: Lienzo de dibujo
```javascript
var dibujar = function(e){
    var punto = document.createElement('div');
    punto.classList.add('punto');
    punto.style.left = (e.pageX - 10) + 'px';
    punto.style.top = (e.pageY - 10) + 'px';
    punto.style.background = 'tomato';
    document.body.appendChild(punto);
};
addEventListener('mousedown', function(){
    addEventListener('mousemove', dibujar);
    addEventListener('mouseup', function(){
        removeEventListener('mousemove', dibujar);
    });
});
```

### Relacionados con el teclado

+ keydown
+ keyup
+ keypress  (cuando se pulsa una **tecla que imprime un caracter)**

EJERCICIO: Atajos de teclado
```javascript
addEventListener('keydown', function(e){
    // console.log(e.which);
    if(e.ctrlKey === true && e.altKey === true && e.which === 89){
      alert("Bienvenido al juego");
    }
});
```

### Relacionados con formularios

| Evento | Descripción |
| ---------------  | --------------- |
| focus | El campo se activa (es en foco)|
| blur     |  El elemento pierde el foco|
| select   | El usr selecciona el texto de un elemento input o textarea|
| change |  Ocurre cuando cambia el valor de un `<select>` , `<input>` o `<textarea>` (ocurre luego de perder el foco)  |
| submit | cuando se envia el formulario, se asocia a un tag `<form>`. |
| reset   |  Borra todos los inputs. |
| input | El evento ocurre cuando el *value* de un `<input>` o `<textarea>` cambia. (ocurre inmediatamente el usuario escribe/borra una letra) |

```javascript
// Ejercicio 1: detectar la opcion seleccionada
(function(){
  'use strict';
  var pais = document.getElementById('pais');
  pais.addEventListener('change', function(){
    console.log('Tu país es ' + this.value);
  });
})();

// Ejercicio 2: detectar si un checkbox o radio button se selecciona
(function(){
  'use strict';
  var check = document.getElementById('check');
  check.addEventListener('change', function(e){
    if(e.target.checked){
      alert("Gracias por suscribirte a nuestro newsletter");
    } else {
      alert("Lamentamos tu decision =(");
    }
  });
})();
```