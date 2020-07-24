# ¿Qué es un método de ciclo de vida?

Los _métodos de ciclo de vida_ son métodos que se llaman en ciertos momentos de la vida de un componente.

Puede escribir un método de ciclo de vida que se llame justo antes de que un componente se procese por primera vez.

Puede escribir un método de ciclo de vida que se llame justo después de que se procese un componente, todas las veces, excepto por primera vez.

Puede adjuntar métodos de ciclo de vida a muchos momentos diferentes en la vida de un componente. ¡Esto tiene implicaciones poderosas!

---

# Métodos de montaje del ciclo de vida

Hay tres categorías de métodos de ciclo de vida: _montaje_ (_mounting_), _actualización_ (_updating_)y _desmontaje_ (_unmounting_). Esta lección trata sobre la primera categoría: _montar_ métodos de ciclo de vida.

Un componente se "monta" cuando se procesa por primera vez. Esto es cuando se llaman los métodos de _montaje del ciclo de vida_.

Existen tres _métodos de montaje del ciclo de vida_:

- componentWillMount
- render
- componentDidMount

Cuando se _monta_ un componente, llama automáticamente a estos tres métodos, en orden.

---

# componentWillMount

El primer método de ciclo de vida de _montaje_ se llama `componentWillMount`.

Cuando un componente se renderiza por primera vez, se llama a `componentWillMount` justo _antes_ del renderizado.

Mire **Example.js** y siga estos pasos:

1. En las líneas 14-17, `<Example />` se representa por primera vez. `<Example />` comienza el período de _montaje_.
2. `<Example />` llama al primer método de ciclo de vida de montaje, `componentWillMount`.
3. `componentWillMount` se ejecuta y aparece una alerta en la pantalla. (líneas 5-7)
4. Después de que `componentWillMount` haya finalizado, `<Example />` llama al segundo método de ciclo de vida de montaje: `render`.
5. `<h1>Hello world</h1>` aparece en la pantalla (líneas 9-11)
6. Dos segundos después, `<Example />` vuelve a aparecer (líneas 20-22). No se llama a `componentWillMount` porque los eventos de ciclo de vida de montaje solo se ejecutan la primera vez que se procesa un componente.

¡Puedes llamar a `this.setState` desde dentro de `componentWillMount`!

Mire **Example2.js** para ver un ejemplo de `this.setState` dentro de `componentWillMount`. Vea si puede seguir cómo `<Example2 />` representaría `<h1>hello world</h1>`.

```jsx
// Example.js
import React from "react";
import ReactDOM from "react-dom";

export class Example extends React.Component {
  componentWillMount() {
    alert("component is about to mount!");
  }

  render() {
    return <h1>Hello world</h1>;
  }
}

ReactDOM.render(<Example />, document.getElementById("app"));

setTimeout(() => {
  ReactDOM.render(<Example />, document.getElementById("app"));
}, 2000);
```

```jsx
// Example2.js
import React from "react";
import ReactDOM from "react-dom";

export class Example2 extends React.Component {
  constructor(props) {
    super(props);

    this.state = { text: "" };
  }

  componentWillMount() {
    this.setState({ text: "Hello world" });
  }

  render() {
    return <h1>{this.state.text}</h1>;
  }
}

ReactDOM.render(<Example2 />, document.getElementById("app"));
```

---

# render

¡`render` es un método de ciclo de vida!

No vamos a repasar `render` aquí, ya hemos hablado mucho sobre eso. Sin embargo, debe comprender cómo encaja `render` en el período de _montaje_. Cada vez que se monta un componente, se llama a `componentWillMount` primero, seguido de `render`, seguido de `componentDidMount`.

render` pertenece a dos categorías: montando métodos de ciclo de vida y _actualizar métodos de ciclo de vida_. Cubriremos los métodos de actualización del ciclo de vida en la próxima lección. Pero primero, ¡hay un método de ciclo de vida de montaje final!

---

# componentDidMount

El método de ciclo de vida de montaje final se llama `componentDidMount`.

Cuando un componente se renderiza por primera vez, se llama a `componentDidMount` justo después de que el HTML del `render` haya terminado de cargarse. Busque en el editor de código un ejemplo de `componentDidMount`.

¡`componentDidMount` se usa mucho!

Si su aplicación React usa AJAX para obtener datos iniciales de una API, entonces `componentDidMount` es el lugar para hacer esa llamada AJAX. En términos más generales, `componentDidMount` es un buen lugar para conectar una aplicación React a aplicaciones externas, como web APIs o frameworks JavaScript. `componentDidMount` también es el lugar para establecer temporizadores usando `setTimeout` o `setInterval`.

Si eso suena vago, no te preocupes. ¡Pondrá en práctica los métodos del ciclo de vida en el proyecto final de este curso! Sin mencionar en el mundo real...

```jsx
// Example.js
import React from "react";

export class Example extends React.Component {
  componentDidMount() {
    alert("component just finished mounting!");
  }

  render() {
    return <h1>Hello world</h1>;
  }
}
```

