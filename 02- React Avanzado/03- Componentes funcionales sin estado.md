# Componentes funcionales sin estado

En el editor de código, eche un vistazo a `GuineaPigs` de la última lección.

Observe que su objeto de instrucciones solo tiene una propiedad: `render()`.

Cuando separa un componente contenedor de un componente de presentación, el componente de _presentación_ siempre terminará así: una función `render()` y ninguna otra propiedad.

Si tiene una clase de componente con nada más que una función de representación, puede reescribir esa clase de componente de una manera muy diferente. ¡En lugar de utilizar `React.Component`, puede escribirlo como una función de JavaScript!

Un componente de clase escrita como una función se llama _componente funcional sin estado_. Los componentes funcionales sin estado tienen algunas ventajas sobre las clases de componentes típicas. Cubriremos esas ventajas en esta lección.

Haga clic en **Example.js** para ver un componente funcional sin estado en acción.

```jsx
// Example.js
// A component class written in the usual way:
export class MyComponentClass extends React.Component {
  render() {
    return <h1>Hello world</h1>;
  }
}

// The same component class, written as a stateless functional component:
export const MyComponentClass = () => {
  return <h1>Hello world</h1>;
};

// Works the same either way:
ReactDOM.render(<MyComponentClass />, document.getElementById("app"));
```

---

# Componentes funcionales sin estado y props

Los componentes funcionales sin estado generalmente tienen `props` que se les pasan.

Para acceder a estos `props`, proporcione un _parámetro_ a su componente funcional sin estado. Este parámetro será automáticamente igual al objeto de `props` del componente.

Es costumbre nombrar los `props` de este parámetro. Lea **Example.js** para ver cómo funciona.

Los componentes funcionales sin estado no solo son más concisos, sino que también influirán sutilmente en su manera positiva de pensar sobre los componentes. ¡Destacan el hecho de que los componentes son básicamente funciones! Un componente toma dos entradas opcionales, `props` y `state`, y genera HTML y/u otros componentes.

¡Verás muchos componentes funcionales sin estado en el próximo curso de React!

```jsx
// Example.js
// Normal way to display a prop:
export class MyComponentClass extends React.Component {
  render() {
    return <h1>{this.props.title}</h1>;
  }
}

// Stateless functional component way to display a prop:
export const MyComponentClass = (props) => {
  return <h1>{props.title}</h1>;
};

// Normal way to display a prop using a variable:
export class MyComponentClass extends React.component {
  render() {
    let title = this.props.title;
    return <h1>{title}</h1>;
  }
}

// Stateless functional component way to display a prop using a variable:
export const MyComponentClass = (props) => {
  let title = props.title;
  return <h1>{title}</h1>;
};
```
