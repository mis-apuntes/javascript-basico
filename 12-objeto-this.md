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
            console.log(this)   //this es 'direccion' 
        }
    },
    nuevaDir: function(){
        return function(){
            //ATENCIÓN !!!
            console.log(this)   //this es 'window' ¿rompe this?
        } 
    }    
}
```

> Tomar en cuenta el ámbito de ejecución,
>
> - En un contexto global, `this` hace referencia al objeto global `window`.
>
> - `this` dentro de un *event handler*.
>
>   ```javascript
>   var boton = document.getElementById("boton");
>   
>   boton.addEventListener('click',function(){
>     alert(this.textContent);  // this referencia al elemento HTML (boton)
>   });
>   ```
>
> - `this` dentro de un *constructor*.
>
>   ```js
>   function Persona(nombrePersona, edadPersona){
>     this.nombre = nombrePersona; 
>     this.edad = edadPersona;
>     //this se refiere al objeto instanciado.
>   }
>   
>   var miAmigo = new Persona("Luis", 30);
>   console.log(miAmigo.nombre)  // "Luis"
>   ```

Si se usa `"use stric"`, `this` devuelve `undefined`.

```javascript
(function test(){
  "use strict";
  console.log(this);    //undefined
})();
```

## 