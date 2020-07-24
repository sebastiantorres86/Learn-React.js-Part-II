# Separe los componentes del contenedor de los componentes de presentación: explicación

En esta lección, aprenderá su segundo patrón de programación: separar los _componentes de presentación_ de los _componentes de muestra_.

Haz clic en Ejecutar. En el navegador, navegue a `https://localhost:8000`.

Estás viendo un componente renderizado `<GuineaPigs />`.

El trabajo de `<GuineaPigs />` es hacer un carrusel de fotos de conejillos de Indias. ¡Hace esto perfectamente bien! Y, sin embargo, tiene un problema: hace demasiadas cosas.

Podemos dividir `<GuineaPigs />` en componentes más pequeños, pero antes de hacerlo: ¿cómo _sabemos_ que GuineaPigs hace demasiadas cosas? ¿Cómo puede saber cuándo un componente tiene demasiadas responsabilidades?

_Separar los componentes del contenedor de los componentes de presentación_ ayuda a responder esa pregunta. Le muestra cuándo podría ser un buen momento para dividir un componente en componentes más pequeños. También le muestra _cómo_ realizar esa división.

---

# Separe los componentes del contenedor de los componentes de presentación: aplique

_Separar los componentes del contenedor de los componentes de presentación_ es un patrón de programación React popular.

Aquí está la idea básica detrás de esto: si un componente tiene que tener `state`, hacer cálculos basados en `props` o administrar cualquier otra lógica compleja, entonces ese componente no debería tener _además_ que representar JSX similar a HTML.

En lugar de representar JSX similar a HTML, el componente debería representar otro componente. Debería ser el trabajo de _ese_ componente renderizar JSX tipo HTML.

Seguir este patrón separa su _lógica de negocios_ de su _lógica de presentación_, lo cual es una [buena cosa](http://www.dictionary.com/browse/good-thing).
