# Formularios de reacción

La última lección de esta unidad es sobre formularios.

Piense en cómo funcionan los formularios en un entorno típico sin React. Un usuario escribe algunos datos en los campos de entrada de un formulario y el servidor no lo sabe. El servidor permanece sin pistas hasta que el usuario presiona el botón "enviar", que envía todos los datos del formulario al servidor simultáneamente.

En React, como en muchos otros entornos JavaScript, esta no es la mejor manera de hacer las cosas.

El problema es el período de tiempo durante el cual un formulario piensa que un usuario ha escrito una cosa, pero el servidor piensa que el usuario ha escrito una cosa diferente. ¿Qué sucede si, durante ese tiempo, una _tercera_ parte del sitio web necesita saber qué ha escrito un usuario? Podría pedir el formulario o el servidor y obtener dos respuestas diferentes. En una aplicación JavaScript compleja con muchas partes móviles e interdependientes, este tipo de conflicto puede generar problemas fácilmente.

En un formulario React, desea que el servidor sepa sobre cada nuevo carácter o eliminación, _tan pronto como suceda_. De esa manera, su pantalla siempre estará sincronizada con el resto de su aplicación.

---

# Entrada onChange

Un formulario tradicional no actualiza el servidor hasta que un usuario presiona "enviar". Pero desea actualizar el servidor _cada vez que un usuario ingresa o elimina cualquier carácter_.

---

# Escribir un controlador de eventos de entrada

En este ejercicio, definirá una función que se llama cada vez que un usuario ingresa o elimina cualquier carácter.

Esta función será un _controlador de eventos_. Escuchará los eventos de `change`. Puede ver un ejemplo de un controlador de eventos que escucha eventos de cambio en **Example.js**.

```jsx
// Example.js
import React from "react";

export class Example extends React.Component {
  constructor(props) {
    super(props);

    this.state = { userInput: "" };

    this.handleChange = this.handleChange.bind(this);
  }

  handleChange(e) {
    this.setState({
      userInput: e.target.value,
    });
  }

  render() {
    return <input onChange={this.handleChange} type="text" />;
  }
}
```

---

# Establecer el estado inicial de la entrada

¡Bien! Cada vez que alguien escribe o elimina en `<input />`, el método `.handleUserInput()` actualizará `this.state.userInput` con el texto de `<input />`.

Como está usando `this.setState`, ¡eso significa que `Input` necesita un estado inicial! ¿Cuál debería ser el _valor_ inicial de `this.state`?

Bueno, `this.state.userInput` se mostrará en `<input />`. ¿Cuál debería ser el texto inicial en `<input />` cuando un usuario visita la página por primera vez?

¡El texto inicial debe estar en blanco! De lo contrario, parecería que alguien ya ha escrito algo.

---

# Actualizar el valor de una entrada

Cuando un usuario escribe o elimina en `<input />`, eso activará un evento de _cambio_, que llamará a `handleUserInput`. ¡Eso es bueno!

`handleUserInput` establecerá `this.state.userInput` igual a cualquier texto que esté actualmente en el campo de entrada. ¡Eso también es bueno!

Solo hay un problema: puede configurar `this.state.userInput` a lo que desee, pero a `<input />` no le importará. Debe de alguna manera hacer que el texto de `<input />` responda a `this.state.userInput`.

¡Suficientemente fácil! Puede controlar el texto de una `<input />` configurando su atributo `value`.

---

# Controlado vs no controlado

Hay dos términos que probablemente aparecerán cuando hable sobre formularios React: _componente controlado_ y c*omponente no controlado*. Al igual que el enlace automático, los _componentes controlados_ frente a los _no controlados_ es un tema con el que debería estar familiarizado, pero no es necesario que comprenda profundamente en este momento.

Un _componente no controlado_ es un componente que mantiene su propio estado interno. Un _componente controlado_ es un componente que no mantiene ningún estado interno. Como un componente controlado no tiene estado, debe ser _controlado_ por alguien más.

Piense en un elemento `<input type='text' />` típico. Aparece en pantalla como un cuadro de texto. Si necesita saber qué texto está actualmente en el cuadro, puede preguntar al `<input />`, posiblemente con algún código como este:

```jsx
let input = document.querySelector('input [type = "text"]');

let typedText = input.value; // input.value será igual a cualquier texto que esté actualmente en el cuadro de texto.
```

Lo importante aquí es que `<input />` _realiza un seguimiento_ de su propio texto. Puede preguntarle cuál es su texto en cualquier momento, y podrá decírselo.

El hecho de que `<input />` realiza un seguimiento de la información lo convierte en un _componente no controlado_. Mantiene su propio estado interno, recordando datos sobre sí mismo.

Un _componente controlado_, por otro lado, no tiene memoria. Si le solicita información sobre sí mismo, tendrá que obtener esa información a través de `props`. La mayoría de los componentes React están _controlados_.

En React, cuando le das a `<input />` un atributo `value`, entonces sucede algo extraño: `<input />` SE CONVIERTE en controlado. Deja de usar su almacenamiento interno. Esta es una manera más "React" de hacer las cosas.

Puede encontrar más información sobre componentes controlados y no controlados en la [documentación de React Forms](https://reactjs.org/docs/forms.html).

---

# Resumen de formularios React

¡Buen trabajo! Acabas de escribir tu primer formulario React.

Tenga en cuenta que no utilizó un botón de envío. ¡Ni siquiera usaste un elemento `<form>`! Su "formulario" en realidad era solo un `<input />`.

Ese no siempre será el caso. En ocasiones, aún querrá un elemento `<form>` y un botón de envío, especialmente si necesita diferenciar entre un formulario terminado y un formulario en progreso. Pero en algunos casos, está bien tener un "formulario" que realmente sea solo un campo de entrada.

Esto se debe a que, a diferencia del paradigma de forma tradicional, en React reenvías tu formulario en cada cambio de carácter. Eso elimina la necesidad de "enviar" algo.

¡Eso marca el final de esta unidad! Has aprendido una amplia variedad de técnicas importantes: estilos en línea, separación de componentes de contenedor y presentación, componentes funcionales sin estado, proptypes y formularios. ¡Lo revisarás todo en el próximo curso! Solo falta una herramienta importante en su cinturón de herramientas: _métodos de ciclos de vida_. Cubriremos los de la unidad final de este curso.
