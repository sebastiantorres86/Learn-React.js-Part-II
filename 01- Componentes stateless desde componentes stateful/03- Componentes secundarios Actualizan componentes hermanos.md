# Componentes secundarios Actualizan componentes hermanos

Patrones dentro de patrones dentro de patrones!

En la lección 1, aprendió su primer patrón de programación React: un componente primario _con estado_ pasa un `prop` a un componente secundario _sin estado_.

En la lección 2, aprendió que el patrón de la lección 1 es en realidad parte de un patrón más grande: un componente primario con estado pasa un _controlador de eventos_ a un componente secundario sin estado. El componente hijo luego usa ese _controlador de eventos_ para actualizar el `state` de su padre.

En esta lección, ampliaremos el patrón por última vez. Un componente hijo actualiza el estado de su padre y el padre pasa ese estado a un componente hermano.

---

# Un hermano para mostrar, otro para cambiar

Una de las primeras cosas que aprendió sobre los componentes es que solo deberían tener un trabajo.

En la última lección, `Child` tenía dos trabajos:

1- `Child` mostró un nombre.

2- `Child` ofreció una forma de _cambiar_ ese nombre.

Debe dividir `Child` en dos: un componente para mostrar el nombre y un componente diferente para permitir que un usuario _cambie_ el nombre.

En el editor de código, seleccione **Child.js**. Tenga en cuenta que estas líneas se han
desvanecido:

```jsx
// Child.js
import React from "react";

export class Child extends React.Component {
  constructor(props) {
    super(props);

    this.handleChange = this.handleChange.bind(this);
  }

  handleChange(e) {
    const name = e.target.value;
    this.props.onChange(name);
  }

  render() {
    return (
      <div>
        <select id="great-names" onChange={this.handleChange}>
          <option value="Frarthur">Frarthur</option>
          <option value="Gromulus">Gromulus</option>
          <option value="Thinkpiece">Thinkpiece</option>
        </select>
      </div>
    );
  }
}
```

```jsx
<h1>Hey, my name is {this.props.name}!</h1>
```

La nueva versión de `Child` muestra un menú desplegable para _cambiar_ el nombre, y _eso es todo_.

Seleccione **Sibling.js** en el editor de código.

Lea la declaración `return` de la función de renderizado.

¡_Aquí_ se muestra el nombre! O al menos se mostrará, una vez que haya realizado una pequeña edición.

```jsx
import React from "react";

export class Sibling extends React.Component {
  render() {
    return (
      <div>
        <h1>Hey, my name is Frarthur!</h1>
        <h2>Don't you think Frarthur is the prettiest name ever?</h2>
        <h2>Sure am glad that my parents picked Frarthur!</h2>
      </div>
    );
  }
}
```

Esto nos lleva al nuevo concepto esencial para esta lección: tendrá información de _visualización_ de un componente sin estado, y un componente sin estado diferente ofrecerá la capacidad de _cambiar_ esa información.

---

# Pase los props correctos a los hermanos correctos

Mire **Parent.js** en el editor de código.

Tres cosas han cambiado en este archivo desde la última lección:

1. Se ha requerido `Sibling` en la línea 4.
2. Se ha agregado una instancia `<Sibling />` a la función de representación en la línea 27.
3. `<Sibling />` y `<Child />` se han incluido en un `<div></div>`, ya que las expresiones JSX deben tener solo un elemento externo.

```jsx
// Parent.js
import React from "react";
import ReactDOM from "react-dom";
import { Child } from "./Child";
import { Sibling } from "./Sibling";

class Parent extends React.Component {
  constructor(props) {
    super(props);

    this.state = { name: "Frarthur" };

    this.changeName = this.changeName.bind(this);
  }

  changeName(newName) {
    this.setState({
      name: newName,
    });
  }

  render() {
    return (
      <div>
        <Child name={this.state.name} onChange={this.changeName} />
        <Sibling />
      </div>
    );
  }
}

ReactDOM.render(<Parent />, document.getElementById("app"));
```

---

# Mostrar información en un componente hermano

¡Estás en el último paso!

Has pasado el nombre a `<Sibling />` como `prop`. Ahora `<Sibling />` tiene que _mostrar_ ese `prop`.

---

# Resumen de Componentes sin estado heredan de componentes con estado

¡Acaba de ejecutar su primer patrón de programación React completo!

Revisemos. Siga cada paso en el editor de código:

- Un componente de clase _con estado_ define una función que llama a `this.setState`. (**Parent.js**, líneas 15-19)

- El componente con estado pasa esa función a un componente sin estado. (**Parent.js**, línea 24)

- Ese componente de clase _sin estado_ define una función que llama a la función transmitida y que puede tomar un _objeto de evento_ como argumento. (**Child.js**, líneas 10-13)

-El componente de clase _sin estado_ utiliza esta nueva función como controlador de eventos. (**Child.js**, línea 20)

- Cuando se detecta un evento, el estado del padre se actualiza. (Un usuario selecciona un nuevo elemento del menú desplegable)

- El componente de clase con estado pasa su estado, distinto de la capacidad de _cambiar_ su estado, a un componente sin estado diferente. (**Parent.js**, línea 25)

- Ese componente de clase sin estado recibe el estado y lo muestra. (**Sibling.js**, líneas 5-10)

- Se representa una instancia del componente de clase con estado. Un componente secundario sin estado muestra el `state` y otro componente secundario sin estado muestra una forma de _cambiar_ el `state`. (Parent.js, líneas 23-26)

¡Este patrón ocurre en React todo el tiempo! Cuanto más lo vea, más se hará evidente su elegancia.

¡Conocer este patrón es tu primer paso para entender cómo las aplicaciones React se ajustan juntas! Tendrás más práctica para usarlo a lo largo de este curso, así como en el curso después de este.
