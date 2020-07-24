# Técnicas avanzadas de React

En esta unidad, aprenderá una variedad de técnicas útiles que se espera que los programadores de React conozcan.

Aprenderá cómo hacer un _componente funcional sin estado_, cómo hacer un _propType_, cómo escribir un formulario y cómo usar estilos.

También se le presentará su segundo patrón de programación: dividir componentes en _componentes de presentación_ y _componentes de contenedor_.

---

# Estilos en línea

Hay muchas formas diferentes de usar estilos en React. Esta lección se centra en uno de ellos: _estilos en línea_.

Un estilo en línea es un estilo que se escribe como un _atributo_, como este:

```jsx
<h1 style={{ color: "red" }}>Hola mundo</h1>
```

Observe las llaves dobles. ¿Para qué son esos?

Las llaves _exteriores_ inyectan JavaScript en JSX. Dicen que "todo lo que hay entre nosotros debe leerse como JavaScript, no como JSX".

Las llaves _internas_ crean un objeto JavaScript literal. Hacen de este un objeto JavaScript válido:

```jsx
{
  color: "red";
}
```

Si inyecta un literal de objeto en JSX, y su inyección completa es _solo_ ese literal de objeto, entonces terminará con llaves dobles. No hay nada inusual en cómo funcionan, pero se ven divertidos y pueden ser confusos.

---

# Hacer una variable de objeto de estilo

¡Eso es todo lo que necesitas para aplicar estilos básicos en React! Simple y directo.

Un problema con este enfoque es que se vuelve desagradable si desea usar más que unos pocos estilos. Una alternativa que a menudo es más agradable es almacenar un objeto de estilo en una _variable_ y luego inyectar esa variable en JSX.

Busque en el editor de código un ejemplo. El objeto de estilo se _define_ en las líneas 3-6 y luego se _inyecta_ en la línea 11.

Si no está acostumbrado a usar módulos, entonces este código puede haberlo hecho contraerse incontrolablemente:

```jsx
const style = {
  color: "darkcyan",
  background: "mintcream",
};
```

¡Definir una variable llamada `style` en el ámbito de nivel superior sería una idea extremadamente mala en muchos entornos JavaScript! En React, sin embargo, está totalmente bien.

Recuerde que todos los archivos son invisibles para todos los demás, excepto lo que usted elige exponer a través de `module.exports`. Podría tener 100 archivos diferentes, todos con variables globales llamadas `style`, y no podría haber conflictos.

---

# Sintaxis de nombres de estilo

En JavaScript normal, los _nombres de estilo_ se escriben en minúsculas con guiones:

```javascript
const styles = {
  "margin-top": "20px",
  "background-color": "green",
};
```

En React, esos mismos nombres se escriben en camelCase:

```jsx
const styles = {
  marginTop: "20px",
  backgroundColor: "green",
};
```

Esto tiene un efecto cero en los _valores_ de propiedad de estilo, solo en los _nombres_ de propiedad de estilo.

---

# Sintaxis de valor de estilo

En el último ejercicio, aprendió cómo los _nombres_ de estilo son ligeramente diferentes en React que en JavaScript normal.

En este ejercicio, aprenderá cómo los _valores_ de estilo son ligeramente diferentes en React que en JavaScript normal.

En JS regular, los _valores_ de estilo son casi siempre cadenas. Incluso si un valor de estilo es numérico, generalmente debe escribirlo como una cadena para poder especificar una unidad. Por ejemplo, debe escribir `"450px"` o "20%".

En React, si escribe un valor de estilo como un _número_, se asume la unidad `"px"`.

¡Que conveniente! Si desea un tamaño de fuente de 30px, puede escribir:

```jsx
{
  fontSize: 30;
}
```

Si desea usar unidades que no sean "px", puede usar una cadena:

```jsx
{
  fontSize: "2em";
}
```

Especificar "px" con una cadena seguirá funcionando, aunque es redundante.

Algunos estilos específicos no completarán automáticamente el "px" por usted. Estos son estilos en los que no es probable que uses "px" de todos modos, por lo que realmente no tienes que preocuparte por eso. [Aquí hay una lista de estilos que no asumen "px"](https://facebook.github.io/react/tips/style-props-value-px.html).

---

# Compartir estilos en múltiples componentes

¿Qué sucede si desea reutilizar estilos para varios componentes diferentes?

Una forma de hacer que los estilos sean _reutilizables_ es mantenerlos en un archivo JavaScript separado. Este archivo debe _exportar_ los estilos que desea reutilizar, a través de `export`. Luego puede `import` sus estilos a cualquier componente que los desee.

En el editor de código, avance y retroceda entre **facebookStyles.js** y **FacebookColorThief.js** para ver un archivo de estilos en acción.

```jsx
// facebook color palette

const blue = "rgb(139, 157, 195)";
const darkBlue = "rgb(059, 089, 152)";
const lightBlue = "rgb(223, 227, 238)";
const grey = "rgb(247, 247, 247)";
const white = "rgb(255, 255, 255)";

const colorStyles = {
  blue: blue,
  darkBlue: darkBlue,
  lightBlue: lightBlue,
  grey: grey,
  white: white,
};
```

```jsx
// FacebookColorThief.js

import React from "react";
import ReactDOM from "react-dom";
import { colorStyles } from "./facebookStyles";

let divStyle = {
  backgroundColor: styles.darkBlue,
  color: styles.white,
};

export class Wow extends React.Component {
  render() {
    return <div style={divStyle}>Wow, I stole these colors from Facebook!</div>;
  }
}

ReactDOM.render(<Wow />, document.getElementById("app"));
```
