# Actualización de métodos de ciclo de vida

Hay dos categorías que aún no hemos discutido: _actualización_ y _desmontaje_ de los métodos del ciclo de vida. Esta lección cubre ambos.

¿Qué es la _actualización_?

La primera vez que se renderiza una instancia de componente, no se actualiza. Un componente se actualiza cada vez que se renderiza, comenzando con el segundo renderizado.

Existen cinco métodos de actualización del ciclo de vida:

- componentWillReceiveProps
- shouldComponentUpdate
- componentWillUpdate
- render
- componentDidUpdate

Cada vez que se _actualiza_ una instancia de componente, llama automáticamente a los cinco métodos, en orden.

---

# componentWillReceiveProps

El primer método de actualización del ciclo de vida se llama `componentWillReceiveProps`.

Cuando se _actualiza_ una instancia de componente, se llama a `componentWillReceiveProps` antes de que comience el renderizado.

Como era de esperar, solo se llama a `componentWillReceiveProps` si el componente recibirá `props`:

```jsx
// se llamará a componentWillReceiveProps aquí:
ReactDOM.render(<Example prop="myVal" />, document.getElementById("app"));

// componentWillReceiveProps NO será llamado aquí:
ReactDOM.render(<Example />, document.getElementById("app"));
```

Busque en el editor de código un ejemplo de `componentWillReceiveProps`. Léelo y trata de descubrir cómo funciona.

`componentWillReceiveProps` automáticamente pasa un argumento: un objeto llamado `nextProps`. `nextProps` es una vista previa del próximo objeto de props `que el componente está a punto de recibir.

En la línea 6, `nextProps.text` se evaluará como `"Hello world"`.

```jsx
// Example.js

import React from "react";

export class Example extends React.Component {
  componentWillReceiveProps(nextProps) {
    alert(
      "Check out the new props.text that " +
        "I'm about to get:  " +
        nextProps.text
    );
  }

  render() {
    return <h1>{this.props.text}</h1>;
  }
}

// The first render won't trigger
// componentWillReceiveProps:
ReactDOM.render(<Example text="Hello world" />, document.getElementById("app"));

// After the first render,
// subsequent renders will trigger
// componentWillReceiveProps:
setTimeout(() => {
  ReactDOM.render(
    <Example text="Hello world" />,
    document.getElementById("app")
  );
}, 1000);
```

---

# shouldComponentUpdate

El segundo método de actualización del ciclo de vida se llama `shouldComponentUpdate`.

Cuando se actualiza un componente, `shouldComponentUpdate` recibe una llamada después de `componentWillReceiveProps`, pero aún antes de que comience el renderizado.

Mira **Example.js** en el editor de código. Léelo y trata de descubrir cómo `shouldComponentUpdate` funciona.

`shouldComponentUpdate` debería devolver `true` o `false`.

Si `shouldComponentUpdate` devuelve `true`, entonces no sucede nada notable. Pero si `shouldComponentUpdate` devuelve `false`, ¡entonces el componente no se actualizará! No se llamará a ninguno de los métodos restantes del ciclo de vida para ese período de actualización, incluido `render`.

La mejor manera de usar `shouldComponentUpdate` es hacer que devuelva `false` _solo bajo ciertas condiciones_. Si se cumplen esas condiciones, su componente no se actualizará.

`shouldComponentUpdate` recibe automáticamente dos argumentos: `nextProps` y `nextState`. Es típico comparar `nextProps` y `nextState` con el actual `this.props` y `this.state`, y usar los resultados para decidir qué hacer. Vea cómo **Example.js** hace esto en las líneas 10-19.

```jsx
// Example.js

import React from "react";

export class Example extends React.Component {
  constructor(props) {
    super(props);

    this.state = { subtext: "Put me in an <h2> please." };
  }

  shouldComponentUpdate(nextProps, nextState) {
    if (
      this.props.text == nextProps.text &&
      this.state.subtext == nextState.subtext
    ) {
      alert("Props and state haven't changed, so I'm not gonna update!");
      return false;
    } else {
      alert("Okay fine I will update.");
      return true;
    }
  }

  render() {
    return (
      <div>
        <h1>{this.props.text}</h1>
        <h2>{this.state.subtext}</h2>
      </div>
    );
  }
}
```

---

# componentWillUpdate

El tercer método de actualización del ciclo de vida es `componentWillUpdate`.

Se llama a `componentWillUpdate` entre `shouldComponentUpdate` y `render`.

`componentWillUpdate` recibe dos argumentos: `nextProps` y `nextState`. Lea **Example.js** en el editor de código para verlo en acción.

¡No puede llamar a `this.setState` desde el cuerpo de `componentWillUpdate`! Lo que plantea la pregunta, ¿por qué lo usarías?

El objetivo principal de `componentWillUpdate` es interactuar con cosas fuera de la arquitectura React. Si necesita realizar una configuración que no sea React antes de que se procese un componente, como verificar el tamaño de la ventana o interactuar con una API, entonces `componentWillUpdate` es un buen lugar para hacerlo.

Si eso suena abstracto, ¡está bien! Todos los métodos del ciclo de vida pueden parecer un poco teóricos, hasta que los haya utilizado en escenarios de la vida real. Harás más de eso en el próximo curso.

```jsx
// Example.js

import React from "react";

export class Example extends React.Component {
  componentWillUpdate(nextProps, nextState) {
    alert("Component is about to update!  Any second now!");
  }

  render() {
    return <h1>Hello world</h1>;
  }
}
```

---

# componentDidUpdate

El último método de ciclo de vida actualizado es `componentDidUpdate`.

Cuando se actualiza una instancia de componente, se llama a `componentDidUpdate` _después_ de que el HTML renderizado haya terminado de cargarse.

Mire **Ejemplo.js** para un ejemplo de `componentDidUpdate`.

`componentDidUpdate` automáticamente pasa dos argumentos: `prevProps` y `prevState`. `prevProps` y `prevState` son referencias a los `props` y el `state` del componente antes de que comenzara el período de actualización actual. Puede compararlos con los `props` y el `state` actual.

`componentDidUpdate` se usa generalmente para interactuar con cosas fuera del entorno React, como el navegador o las API. Es similar a `componentWillUpdate` de esa manera, excepto que se llama después del renderizado en lugar de antes.

```jsx
// Example.js

import React from "react";

export class Example extends React.component {
  componentDidUpdate(prevProps, prevState) {
    alert("Component is done rendering!");
  }

  render() {
    return <h1>Hello world</h1>;
  }
}
```

---

# componentWillUnmount

El período de _desmontaje_ de un componente se produce cuando el componente se _elimina_ del DOM. Esto podría suceder si el DOM se vuelve a procesar sin el componente, o si el usuario navega a un sitio web diferente o cierra su navegador web.

`componentWillUnmount` es el único método de desmontaje del ciclo de vida.

Se llama a `componentWillUnmount` justo antes de eliminar un componente del DOM. Si un componente inicia algún método que requiera limpieza, entonces `componentWillUnmount` es donde debe colocar esa limpieza.

Puede ver un ejemplo en **Example.js**, como de costumbre.

```jsx
// Example.js
import React from "react";

export class Example extends React.Component {
  componentWillUnmount() {
    alert("Goodbye world");
  }

  render() {
    return <h1>Hello world</h1>;
  }
}
```

---

# Resumen de métodos de ciclo de vida

¡Felicitaciones por haber llegado al final de nuestros cursos introductorios de React! En este punto, ha adquirido todas las herramientas que necesita para programar en React!

Sin embargo, todavía no has terminado con este curso. Es posible que se pregunte cómo crear una aplicación React en su propia computadora. Hemos creado un artículo para guiarlo a través de este proceso. ¡[Haz clic](https://www.codecademy.com/articles/how-to-create-a-react-app) para comenzar!
