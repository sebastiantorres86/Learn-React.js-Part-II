# Componentes hijos actualizan el estado de sus padres

En la última lección, pasó información de un componente primario con estado a un componente secundario sin estado.

En esta lección, se expandirá en ese patrón. El componente secundario sin estado actualizará el estado del componente primario.

Así es como funciona eso:

1. El component de clase principal define un método que llama a `this.setState()`.
   Por ejemplo, mire en **Step1.js** el método `.handleClick()`.

```jsx
import React from "react";
import ReactDOM from "react-dom";
import { ChildClass } from "./ChildClass";

class ParentClass extends React.Component {
  constructor(props) {
    super(props);

    this.state = { totalClicks: 0 };
  }

  handleClick() {
    const total = this.state.totalClicks;

    // calling handleClick will
    // result in a state change:
    this.setState({ totalClicks: total + 1 });
  }
}
```

2. El componente padre vincula el método recién definido a la instancia actual del componente en su constructor. Esto garantiza que cuando pasemos el método al componente secundario, aún actualizará el componente primario.
   Por ejemplo, mire en **Step2.js** al final del método `constructor()`.

```jsx
import React from "react";
import ReactDOM from "react-dom";
import { ChildClass } from "./ChildClass";

class ParentClass extends React.Component {
  constructor(props) {
    super(props);

    this.state = { totalClicks: 0 };

    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    const total = this.state.totalClicks;

    // calling handleClick will
    // result in a state change:
    this.setState({ totalClicks: total + 1 });
  }

  // The stateful component class passes down
  // handleClick to a stateless component class:
  render() {
    return <ChildClass onClick={this.handleClick} />;
  }
}
```

3. Una vez que el _padre_ ha definido un método que actualiza su estado y está vinculado a él, el padre pasa ese método al _hijo_.
   Mire en **Step2.js**, el `prop` en la línea 28.

4.El _hijo_ recibe la función transmitida y la usa como un controlador de eventos.
Mira en **Step3.js**. Cuando un usuario hace clic en el `<button></button>`, se activará un evento de clic. Esto hará que se llame a la función transmitida, que actualizará el estado del padre.

```jsx
import React from "react";
import ReactDOM from "react-dom";

export class ChildClass extends React.Component {
  render() {
    return (
      // The stateless component class uses
      // the passed-down handleClick function,
      // accessed here as this.props.onClick,
      // as an event handler:
      <button onClick={this.props.onClick}>Click Me!</button>
    );
  }
}
```

Haga clic en los tres archivos en orden e intente seguir su cronología. ¡Cuando esté listo, haga clic en Siguiente y crearemos un ejemplo!

---

# Definir un controlador de eventos

Para que un componente secundario actualice el `state` de su elemento primario, el primer paso es algo que ha visto antes: debe definir un método de cambio de estado en el elemento primario.

---

# Pase el controlador de eventos

En el último ejercicio, definió una función en `Parent` que puede cambiar el estado de `Parent`.

`Parent` debe pasar esta función a `Child` para que `Child` pueda usarla en un detector de eventos en el menú desplegable.

---

# Reciva el controlador de eventos

¡Acaba de pasar una función a `Child` que puede cambiar el estado de `Parent`!

---

# Enlace automático

¡Buen trabajo! _Los componentes sin estado que actualizan el estado de sus padres_ es un patrón de React que verá cada vez más. Aprender a reconocerlo te ayudará a comprender cómo se organizan las aplicaciones React.

