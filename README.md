## ¿Qué es React Context?

React Context es una característica que permite compartir datos entre varios componentes en una aplicación de React, sin necesidad de pasar "props" de un componente a otro en cada nivel del árbol de componentes. Es ideal cuando ciertos datos o estados necesitan ser accesibles en muchos niveles de la jerarquía de componentes, como:

-   El tema (modo oscuro o claro).
-   Datos de usuario autenticado.
-   Preferencias globales.
-   Idioma de la aplicación.

### Problema que soluciona React Context

Imagina que tienes un árbol de componentes con varias capas y deseas pasar una misma prop desde un componente superior hasta uno en niveles muy inferiores. Esto genera lo que se llama "prop drilling", donde tienes que pasar datos a través de múltiples componentes, aunque muchos de ellos no usen esos datos.

Ejemplo de prop drilling:

```javascript
function App() {
	const usuario = { nombre: "Juan" };

	return <ComponenteA usuario={usuario} />;
}

function ComponenteA({ usuario }) {
	return <ComponenteB usuario={usuario} />;
}

function ComponenteB({ usuario }) {
	return <ComponenteC usuario={usuario} />;
}

function ComponenteC({ usuario }) {
	return <p>Nombre del usuario: {usuario.nombre}</p>;
}
```

En este caso, el prop `usuario` debe pasar por `ComponenteA` y `ComponenteB` aunque no lo necesiten, solo para llegar a `ComponenteC`. React Context soluciona este problema permitiendo que los datos sean accesibles directamente en el componente que los necesita, sin tener que pasarlos manualmente por cada nivel.

### Cómo funciona React Context

React Context se utiliza en tres pasos principales:

-   Crear el Contexto.
-   Proveer el Contexto.
-   Consumir el Contexto.

1. **Crear el Contexto:** primero, se crea el contexto utilizando el método `createContext` de React.

```javascript
import React, { createContext } from "react";

// Crear un contexto
const UsuarioContext = createContext();
```

El contexto se puede inicializar con un valor predeterminado opcional que estará disponible para los componentes que lo consuman si no se ha proporcionado ningún valor.

2. **Proveer el Contexto:** el contexto debe ser "proveído" a los componentes que lo necesiten, usando el componente Provider que React Context proporciona. El Provider envuelve los componentes que necesitan acceso al contexto y les pasa los valores.

```javascript
function App() {
	const usuario = { nombre: "Juan" };

	return (
		<UsuarioContext.Provider value={usuario}>
			<ComponenteA />
		</UsuarioContext.Provider>
	);
}
```

Aquí, el componente `App` envuelve a `ComponenteA` dentro del `UsuarioContext.Provider`, pasando el objeto usuario como valor del contexto. Cualquier componente dentro de este árbol (incluyendo `ComponenteA`, sus hijos, y sus descendientes) podrá acceder al valor proporcionado por el contexto.

3. **Consumir el Contexto:** los componentes que necesitan acceder al valor del contexto pueden consumirlo usando el hook `useContext` o el componente de renderizado `Consumer`.

Uso con useContext (más común):

```javascript
import { useContext } from "react";
import { UsuarioContext } from "./App"; // Importamos el contexto

function ComponenteC() {
	const usuario = useContext(UsuarioContext); // Accedemos al valor del contexto
	return <p>Nombre del usuario: {usuario.nombre}</p>;
}
```

En este ejemplo, `ComponenteC` obtiene el valor usuario directamente desde el contexto, sin necesidad de recibir `props` de los componentes superiores.

### Uso con Consumer (menos común):

También puedes consumir el contexto usando el patrón Consumer, aunque con hooks (useContext), esto es menos frecuente en componentes funcionales.

```javascript
function ComponenteC() {
	return <UsuarioContext.Consumer>{(usuario) => <p>Nombre del usuario: {usuario.nombre}</p>}</UsuarioContext.Consumer>;
}
```

Ejemplo completo con useContext

```javascript
import React, { createContext, useContext } from "react";

// 1. Crear el contexto
const UsuarioContext = createContext();

function App() {
	const usuario = { nombre: "Juan" };

	return (
		// 2. Proveer el contexto
		<UsuarioContext.Provider value={usuario}>
			<ComponenteA />
		</UsuarioContext.Provider>
	);
}

function ComponenteA() {
	return <ComponenteB />;
}

function ComponenteB() {
	return <ComponenteC />;
}

function ComponenteC() {
	// 3. Consumir el contexto con useContext
	const usuario = useContext(UsuarioContext);
	return <p>Nombre del usuario: {usuario.nombre}</p>;
}

export default App;
```

### ¿Cuándo usar React Context?

-   Cuando tienes datos que necesitas compartir entre varios componentes en diferentes niveles de la jerarquía.
-   Para evitar el `prop drilling` (pasar datos manualmente a través de muchos componentes intermedios).
-   Al manejar datos globales que no cambian muy frecuentemente, como el tema, autenticación de usuario, o configuraciones globales.

### Alternativas a React Context

Aunque React Context es una herramienta poderosa, no es adecuada para todas las situaciones. Si tienes datos que cambian frecuentemente o una aplicación muy grande, podrías considerar usar una biblioteca de administración de estado como `Redux` o `Zustand`.

### Resumen

-   React Context permite compartir datos entre componentes sin necesidad de pasar props por cada nivel.
-   `createContext` crea el contexto, `Provider` lo proporciona, y `useContext` lo consume.
-   Es útil para evitar prop drilling y manejar datos globales como temas, autenticación, y preferencias.
