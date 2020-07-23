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

Recuerde que todos los archivos son invisibles para todos los demás, excepto lo que usted elige exponer a través de module.exports. Podría tener 100 archivos diferentes, todos con variables globales llamadas estilo, y no podría haber conflictos.
