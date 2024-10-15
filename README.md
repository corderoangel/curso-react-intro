## Eventos

En React, los eventos funcionan de manera similar a los eventos en HTML, pero con algunas diferencias clave en cuanto a la sintaxis y la gestión. React utiliza una versión sintética de los eventos llamada SyntheticEvent, que unifica el manejo de eventos para todos los navegadores.

A continuación, te explico dos de los eventos más comunes en React: onClick y onChange.

### onClick: Manejo de eventos de clic

El evento onClick se activa cuando un usuario hace clic en un elemento. En React, lo puedes manejar como un atributo del elemento JSX y asignarle una función que se ejecutará cuando ocurra el clic.

Ejemplo básico de onClick:

```jsx
function MiComponente() {
	const manejarClick = () => {
		alert("¡Has hecho clic en el botón!");
	};

	return <button onClick={manejarClick}>Clic aquí</button>;
}
```

**En este ejemplo:**

-   `onClick` es un atributo del botón.
-   `manejarClick` es una función que se ejecutará cuando se haga clic en el botón.
-   La función muestra una alerta cuando el botón es clicado.

**Ejemplo con parámetros:**
Si quieres pasar parámetros a la función que maneja el evento `onClick`, debes envolver la función dentro de una función anónima, ya que no puedes llamarla directamente (esto ejecutaría la función en lugar de esperar al clic).

```jsx
function MiComponente() {
	const manejarClick = (nombre) => {
		alert(`¡Hola, ${nombre}!`);
	};

	return <button onClick={() => manejarClick("Juan")}>Clic aquí</button>;
}
```

### onChange: Manejo de cambios en campos de formulario

El evento onChange se usa principalmente en formularios, para capturar cambios en elementos de entrada como `<input>`, `<select>`, `<textarea>`, etc. Se activa cada vez que el valor de un campo cambia, lo que permite manejar la actualización del estado del componente en tiempo real.

```jsx
import { useState } from "react";

function MiComponente() {
	const [valor, setValor] = useState("");

	const manejarCambio = (event) => {
		setValor(event.target.value);
	};

	return (
		<div>
			<input type="text" value={valor} onChange={manejarCambio} />
			<p>Valor actual: {valor}</p>
		</div>
	);
}
```

**En este ejemplo:**

-   `onChange` es el evento aplicado al campo de entrada (`<input>`).
-   `manejarCambio` es la función que se ejecuta cada vez que el usuario escribe en el campo.
-   `event.target.value` obtiene el valor actual del campo de entrada y lo guarda en el estado con setValor.

**Explicación:**  
Se utiliza el hook useState para manejar el estado del valor del campo de entrada.
Cada vez que el usuario escribe algo en el input, el evento onChange captura el valor y actualiza el estado.
El valor actualizado del estado se muestra dinámicamente debajo del input.

**Resumen de Sintaxis de Eventos**

-   Eventos en React utilizan camelCase (por ejemplo, onClick, onChange).
-   Las funciones manejadoras de eventos suelen estar definidas dentro del componente y se pasan como referencias (por ejemplo, `onClick={manejarClick}`).
-   Para pasar parámetros a las funciones manejadoras, se usa una función anónima (por ejemplo, onClick={() => manejarClick(parametro)}).

**Otros eventos comunes**

-   **onSubmit:** Se dispara cuando se envía un formulario.
-   **onMouseEnter y onMouseLeave:** Se activan cuando el ratón entra o sale de un elemento.
-   **onKeyDown, onKeyUp, onKeyPress:** Capturan eventos de teclado.

**Ejemplo combinado: onClick y onChange**

```jsx
import { useState } from "react";

function Formulario() {
	const [nombre, setNombre] = useState("");

	const manejarCambio = (event) => {
		setNombre(event.target.value);
	};

	const manejarClick = () => {
		alert(`Nombre ingresado: ${nombre}`);
	};

	return (
		<div>
			<input type="text" value={nombre} onChange={manejarCambio} placeholder="Escribe tu nombre" />
			<button onClick={manejarClick}>Mostrar Nombre</button>
		</div>
	);
}
```

**En este ejemplo:**

-   **onChange** captura el valor del campo de texto y actualiza el estado nombre.
-   **onClick** muestra una alerta con el valor actual del estado cuando se hace clic en el botón.

### Conclusión

Los eventos como onClick y onChange permiten interactuar con los usuarios en React. Puedes asignar funciones manejadoras a los eventos para capturar acciones y actualizar el estado de los componentes, lo que facilita crear interfaces dinámicas y reactivas.
