# propTypes

En esta lección, aprenderá a usar una característica importante de React llamada `propTypes`.

Los `propTypes` son útiles por dos razones. La primera razón es la _validación de props_.

La _validación_ puede garantizar que sus `props` estén haciendo lo que se supone que deben hacer. Si faltan `props`, o si están presentes pero no son lo que esperaba, se imprimirá una advertencia en la consola.

Esto es útil, pero la razón #2 es posiblemente más útil: _documentación_.

_Documentar_ los `props` hace que sea más fácil mirar un archivo y comprender rápidamente la clase de componente que contiene. Cuando tenga muchos archivos, y lo hará, esto puede ser un gran beneficio.

---

# Aplicar PropTypes

En el editor de código, eche un vistazo a la función de renderizado de `MessageDisplayer`.

Observe la expresión `this.props.message`. A partir de esta expresión, puede deducir que `MessageDisplayer` espera que se le pase un `prop` llamado `message`. En algún lugar, en algún momento, se espera que este código se ejecute:

```jsx
<MessageDisplayer message="something" />
```

Si un componente de clase espera un `prop`, ¡entonces puede darle a ese tipo de componente un `propType`!

El primer paso para hacer un `propType` es buscar una propiedad llamada `propTypes` en el objeto de instrucciones. Si no hay uno, ¡haga uno! Deberá declararlo después del cierre de la declaración de su componente, ya que será una propiedad estática.

Vea el ejemplo de una propiedad `propTypes` en las líneas 11-13. ¡Observe que el _valor_ de `propTypes` es un objeto, no una función!

El segundo paso es agregar una propiedad al objeto `propTypes`. Para cada `prop` que su componente de clase espera recibir, puede haber una propiedad en su objeto `propTypes`.

`MessageDisplayer` solo espera un `prop`: `message`. Por lo tanto, su objeto `propTypes` solo tiene una propiedad.

```jsx
// MessageDisplayer.js

import React from "react";

export class MessageDisplayer extends React.Component {
  render() {
    return <h1>{this.props.message}</h1>;
  }
}

// This propTypes object should have
// one property for each expected prop:
MessageDisplayer.propTypes = {
  message: React.PropTypes.string,
};
```

---

# Agregar propiedades a PropTypes

En el editor de código, mire la propiedad en el objeto `propTypes` de `MessageDisplayer`:

```jsx
message: React.PropTypes.string;
```

¿Cuáles son las propiedades en `propTypes` que se supone que son, exactamente?

El _nombre_ de cada propiedad en `propTypes` debe ser el nombre de un `prop` esperado. En nuestro caso, `MessageDisplayer` espera un `prop` llamado `message`, por lo que el _nombre_ de nuestra propiedad es `message`.

El _valor_ de cada propiedad en `propTypes` debe ajustarse a este patrón:

```jsx
React.PropTypes.expected - data - type - goes - here;
```

Dado que `message` presumiblemente será una cadena, elegimos `React.PropTypes.string`. Puede ver esto en la línea 12. ¡Observe la diferencia en mayúsculas entre el objeto `propTypes` y `React.PropTypes`!

Cada propiedad en el objeto `propTypes` se llama `propType`.

Seleccione el siguiente archivo en el editor de código, **Runner.js**. Encuentra el objeto `propTypes` de `Runner`.

¡`Runner` tiene seis `propTypes`! Mira a cada uno. Tenga en cuenta que `bool` y `func` se abrevian, pero todos los demás tipos de datos se escriben normalmente.

Si agrega `.isRequired` a un `propType`, recibirá una advertencia de la consola si ese `prop` no se envía.

Intente encontrar los seis `props` del objeto `propTypes` en la función de renderizado de `Runner`: `this.props.message`, `this.props.style`, etc.

```jsx
// Runner.js

import React from "react";

export class Runner extends React.Component {
  render() {
    let miles = this.props.miles;
    let km = this.props.milesToKM(miles);
    let races = this.props.races.map(function (race, i) {
      return <li key={race + i}>{race}</li>;
    });

    return (
      <div style={this.props.style}>
        <h1>{this.props.message}</h1>
        {this.props.isMetric && <h2>One Time I Ran {km} Kilometers!</h2>}
        {!this.props.isMetric && <h2>One Time I Ran {miles} Miles!</h2>}
        <h3>Races I've Run</h3>
        <ul id="races">{races}</ul>
      </div>
    );
  }
}

Runner.propTypes = {
  message: React.PropTypes.string.isRequired,
  style: React.PropTypes.object.isRequired,
  isMetric: React.PropTypes.bool.isRequired,
  miles: React.PropTypes.number.isRequired,
  milesToKM: React.PropTypes.func.isRequired,
  races: React.PropTypes.array.isRequired,
};
```

---

# PropTypes en componentes funcionales sin estado

¿Recuerdas los _componentes funcionales sin estado_? Puedes ver algunos conocidos en **Example.js**.

¿Cómo podría escribir `propTypes` para un componente funcional sin estado?

```jsx
// Manera usual:
class Example extends React.component {
}
Example.propTypes = {

};
...

// Forma componente funcional sin estado:
const Example = (props) => {
// ummm ??????
```

Resulta que el proceso es bastante similar. Para escribir `propTypes` para un componente funcional sin estado, defina un objeto `propTypes` como una propiedad _del propio componente funcional sin estado_. Así es como se ve:

```jsx
const Example = (props) => {
  return <h1>{props.message}</h1>;
};

Example.propTypes = {
  message: React.PropTypes.string.isRequired,
};
```

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

---

# 
