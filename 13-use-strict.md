# Use strict

<!--Complementar con la definición y añadir ejemplos si es necesario-->

```js
'use strinct'
```

**No se recomienda usar en un scope global**, porque eso implicaría que todo el código *javascript* de la aplicación (librerías importadas, códigos de terceros, etc.) estén acorde a esta sintaxis, sino es así provocará error.

La forma recomendada de usar es dentro de las funciones:

+ Si queremos envolver nuestro código sin que afecte código de terceros, creamos una función anónima auto-ejecutada.

  ```javascript
  (function() {
      'use strict'
      // sentencias ...
  })()
  ```

+ También podemos colocar en funciones específicas

  ```javascript
  function getNombre(){
      'use strict'    //esto solo afectará a este ámbito
      var nombre = "Carlos"
      return nombre
  }
  
  variable2 = "hola mundo"
  ```

