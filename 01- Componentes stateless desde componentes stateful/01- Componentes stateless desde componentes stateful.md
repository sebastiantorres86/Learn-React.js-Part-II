# Los componentes sin estado se heredan de los componentes con estado

¡Aprendamos nuestro primer _patrón de programación_!

En esta lección, veremos una versión simple de un patrón de programación. Las siguientes lecciones se ampliarán sobre esa lección y, al final, tendremos un patrón de programación en toda su complejidad.

Nuestro patrón de programación utiliza dos componentes React: un componente _con estado_ y un componente _sin estado_. "Con estado" describe cualquier componente que tenga una propiedad `state`; "Sin estado" describe cualquier componente que no lo hace.

En nuestro patrón, un componente _con estado_ pasa su `state` a un componente _sin estado_.

---

# Construir una componente de clase con estado

Hagamos que un componente _con estado_ pase su estado a un componente _sin estado_.

Para que esto suceda, necesita dos componente de clase: una clase _con estado_ y una clase _sin estado_.

---

# Construir una clase de componentes sin estado

¡Excelente! Acaba de crear un componente de clase _con estado_ llamada Parent.

Ahora, hagamos nuestro componente de clase _sin estado_.

---

# Pase el estado de un componente

Se supone que un `<Parent />` pasa su estado a un `<Child />`.

Antes de que un `<Parent />` pueda pasar algo a un `<Child />`, debe `import` `Child` en **Parent.js**.

---

# No actualizar props

¡Buen trabajo! Acaba de pasar información de un componente _con estado_ a un componente _sin estado_. Harás mucho de eso.

Aprendiste anteriormente que un componente puede _cambiar_ su estado llamando a `this.setState()`. Quizás te hayas estado preguntando: ¿cómo _cambia_ un componente sus props?

La respuesta: ¡no lo hacen!

Un componente nunca debe actualizar `this.props`. Mire **Bad.js** para ver un ejemplo de lo que no debe hacer.

Esto es potencialmente confuso. `props` y `state` almacenan información _dinámica_. La información dinámica puede cambiar, por definición. Si un componente no puede cambiar sus `props`, ¿para qué sirven los `props`?

**Un componente React debe usar `props` para almacenar información que se puede cambiar, pero que solo puede ser cambiado po un componente _diferente_.**

**Un componente React debe usar el `state` para almacenar información que el componente en sí mismo puede cambiar.**

Si eso es un poco confuso, ¡no te preocupes! Las siguientes dos lecciones serán ejemplos.

```jsx
import React from "react";

class Bad extends React.Component {
  render() {
    this.props.message = "yo"; // NOOOOOOOOOOOOOO!!!
    return <h1>{this.props.message}</h1>;
  }
}
```

