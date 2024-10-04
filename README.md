# ¿Qué es el Estado en React?

El estado es uno de los conceptos más importantes en React. Representa los datos que un componente necesita para renderizarse y actualizarse de forma dinámica. En otras palabras, el estado contiene información que puede cambiar con el tiempo y que afecta a cómo se muestra el componente.

A diferencia de las props (que son datos que un componente recibe desde su componente padre), el estado es interno y local al componente. Cada componente puede gestionar su propio estado y modificarlo cuando sea necesario.

## Características del Estado:

Privado y local: El estado es específico de un componente. A diferencia de las props, no puede ser accedido o modificado directamente por otros componentes.
Dinamismo: El estado permite a los componentes de React ser dinámicos, ya que cuando el estado cambia, React vuelve a renderizar el componente automáticamente.
Controlado por el componente: El componente gestiona su propio estado a través de funciones que permiten actualizarlo.
Uso del Estado con useState
En componentes funcionales, el estado se gestiona utilizando el hook useState. Este hook permite añadir y gestionar el estado dentro de un componente funcional.

Ejemplo básico con useState:

```jsx
import { useState } from "react";

function Contador() {
	// Definir el estado inicial
	const [contador, setContador] = useState(0);

	// Función para incrementar el contador
	const incrementar = () => {
		setContador(contador + 1); // Actualizar el estado
	};

	return (
		<div>
			<p>Has hecho clic {contador} veces</p>
			<button onClick={incrementar}>Incrementar</button>
		</div>
	);
}
```

### Explicación:

useState(0): Define el estado inicial (contador) con un valor de 0. El hook useState devuelve un arreglo con dos elementos:

contador: El valor actual del estado.
setContador: Una función que se usa para actualizar el estado.
incrementar: Es la función que se ejecuta cuando el botón es clicado. Llama a setContador para aumentar el valor del estado en 1.

Cuando el estado cambia con setContador, React vuelve a renderizar el componente para reflejar el nuevo valor del contador.

## Ciclo de vida del Estado

Cuando un componente se renderiza por primera vez, React establece el estado inicial. Luego, cuando el estado se actualiza (por ejemplo, al hacer clic en un botón), React:

Detecta que el estado ha cambiado.
Vuelve a renderizar el componente, aplicando los cambios necesarios en la interfaz.

## ¿Cuándo usar el Estado?

El estado es útil en situaciones donde un componente necesita:

Gestionar entradas del usuario: Como en un campo de texto donde se captura lo que el usuario escribe.
Controlar interacciones: Como un botón de "Me gusta" que cambia de estado al hacer clic.
Mostrar o esconder elementos: Como en un menú desplegable.
Actualizar información dinámicamente: Como en un contador o una lista que se actualiza a partir de datos.
Ejemplo completo: Controlar entradas de usuario
Aquí tienes un ejemplo de cómo el estado se utiliza para controlar un campo de texto:

```jsx
import { useState } from "react";

function FormularioNombre() {
	// Estado para almacenar el valor del input
	const [nombre, setNombre] = useState("");

	// Función que actualiza el estado cuando el usuario escribe
	const manejarCambio = (event) => {
		setNombre(event.target.value);
	};

	return (
		<div>
			<input type="text" value={nombre} onChange={manejarCambio} placeholder="Escribe tu nombre" />
			<p>Nombre: {nombre}</p>
		</div>
	);
}
```

## En este ejemplo:

El estado nombre se actualiza cada vez que el usuario escribe algo en el campo de texto.
El valor del input se controla usando el estado, haciendo que React actualice dinámicamente el contenido del párrafo que muestra el nombre.
Resumen del Estado en React
El estado es un mecanismo para almacenar datos locales dentro de un componente.
Se gestiona a través de hooks como useState en componentes funcionales.
Cuando el estado cambia, React vuelve a renderizar el componente automáticamente.
El estado es ideal para manejar cambios dinámicos en la interfaz de usuario, como interacciones o datos que deben cambiar a lo largo del tiempo.
