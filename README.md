# useContext en React

El hook useContext es utilizado en React para consumir valores de un contexto previamente creado. Es una forma simple y directa de acceder a datos compartidos entre componentes sin necesidad de pasar "props" a través de cada nivel del árbol de componentes.

## ¿Cuándo usar useContext?

useContext es útil cuando:

Quieres evitar el prop drilling, es decir, no quieres pasar datos manualmente a través de muchos componentes intermedios.
Tienes datos o configuraciones que son necesarios en múltiples componentes (por ejemplo, temas, información de autenticación, configuraciones globales).
Sintaxis básica de useContext
javascript
Copiar código
const valor = useContext(Contexto);
Contexto es el contexto que has creado usando createContext.
valor será el valor almacenado en ese contexto, que puede ser cualquier tipo de dato (un objeto, string, array, etc.).
Pasos para usar useContext
Crear el contexto usando createContext.
Proveer el contexto a los componentes que lo necesiten utilizando el componente Provider.
Consumir el contexto con useContext en los componentes que necesiten acceder a esos datos.
Ejemplo básico de useContext
Vamos a ver un ejemplo donde compartimos información de un usuario entre varios componentes usando useContext.

1. Crear el contexto
   Primero, creamos el contexto utilizando createContext.

```javascript
import React, { createContext, useContext } from "react";

// Crear el contexto para el usuario
const UsuarioContext = createContext();
```

2. Proveer el contexto
   En el componente principal, usamos el Provider del contexto para envolver los componentes hijos que necesitan acceder al valor del contexto. Proveemos el valor (en este caso, un objeto de usuario).

```javascript
function App() {
	const usuario = { nombre: "Juan", edad: 30 };

	return (
		<UsuarioContext.Provider value={usuario}>
			<ComponenteA />
		</UsuarioContext.Provider>
	);
}
```

3. Consumir el contexto con useContext
   Dentro de cualquier componente hijo, usamos el hook useContext para acceder al valor del contexto (en este caso, el objeto usuario).

```javascript
function ComponenteA() {
	return <ComponenteB />;
}

function ComponenteB() {
	return <ComponenteC />;
}

function ComponenteC() {
	// Consumimos el contexto del usuario usando useContext
	const usuario = useContext(UsuarioContext);

	return <p>Nombre del usuario: {usuario.nombre}</p>;
}
```

Resultado
El componente App provee el contexto UsuarioContext con un valor de { nombre: 'Juan', edad: 30 }.
ComponenteC consume ese valor usando useContext y muestra el nombre del usuario.
Ejemplo completo

```javascript
Copiar código
import React, { createContext, useContext } from 'react';

// 1. Crear el contexto
const UsuarioContext = createContext();

function App() {
const usuario = { nombre: 'Juan', edad: 30 };

return (
// 2. Proveer el contexto a los componentes hijos
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

return <p>Nombre del usuario: {usuario.nombre}, Edad: {usuario.edad}</p>;
}

export default App;
```

## Ventajas de useContext

Simplifica el código: Evita la necesidad de pasar props a través de múltiples componentes intermedios (evita el prop drilling).
Modularidad: Los datos y la lógica están centralizados en un solo contexto, lo que hace que el código sea más organizado.
Mejora la legibilidad: Es más claro y limpio en comparación con pasar muchas props.
Consideraciones al usar useContext
Aunque useContext es útil para compartir datos entre componentes, no está diseñado para manejar estados complejos. Para eso, es mejor usar herramientas como Redux o Zustand.
Re-renderizado: Si el valor del contexto cambia, todos los componentes que consumen ese contexto se volverán a renderizar. Esto puede afectar el rendimiento si no se gestiona correctamente.
Resumen
useContext es un hook que permite consumir valores de un contexto.
Ayuda a evitar el prop drilling, facilitando la comunicación entre componentes.
Se utiliza en combinación con createContext y Provider.
Es ideal para manejar datos globales o configuraciones compartidas, como temas, información de usuario, o preferencias.
