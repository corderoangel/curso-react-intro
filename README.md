# INTRODUCCIÓN A REACT

## Índice

1. [Componentes](#componentes)
2. [Props](#props)
3. [Estilos CSS](#estilos-css)
4. [Eventos](#eventos)
5. [Estado](#estado)

## Componentes

Un componente en React es una pieza reutilizable e independiente de código que encapsula una parte de la interfaz de usuario (UI) y la lógica asociada. Piensa en los componentes como los bloques de construcción que conforman una aplicación de React. Pueden ser tan simples como un botón o tan complejos como una página completa.

### Tipos de componentes

**Componentes funcionales:** Son funciones de JavaScript que devuelven el HTML (o JSX, que es una extensión de la sintaxis de JavaScript) que se renderizará en la página. Estos componentes pueden recibir props (propiedades) para personalizar su contenido o comportamiento.

```jsx
function MiComponente() {
	return <h1>¡Hola, soy un componente funcional!</h1>;
}
```

**Componentes de clase (menos comunes en versiones recientes de React):** Son clases de JavaScript que extienden de React.Component. Antes de React 16.8, los componentes de clase eran necesarios para manejar el estado y el ciclo de vida de un componente, pero ahora las funciones pueden hacer lo mismo usando hooks.

```jsx
class MiComponente extends React.Component {
	render() {
		return <h1>¡Hola, soy un componente de clase!</h1>;
	}
}
```

### Características clave de los componentes:

-   **Reutilizables:** Puedes usar un mismo componente en varias partes de tu aplicación, lo que permite mantener tu código más limpio y organizado.

-   **Modulares:** Dividen la UI en pequeñas piezas que se pueden gestionar de manera individual.

-   **Declarativos:** En lugar de manipular el DOM directamente, describes qué quieres que se muestre y React se encarga de actualizar la interfaz cuando los datos cambian.

-   **Reciben datos a través de props:** Los componentes pueden recibir datos de sus componentes padres mediante las props.

```jsx
function Saludo(props) {
	return <h1>¡Hola, {props.nombre}!</h1>;
}

// Usar el componente en otro lugar
<Saludo nombre="Juan" />;
//En este ejemplo, el componente Saludo recibe una prop llamada nombre y la usa para personalizar el saludo.
```

### 1.3 JSX (JavaScript + XML)

En React, el código que parece HTML en realidad es JSX, que te permite escribir estructuras de UI en un archivo JavaScript y luego ser traducido a JavaScript por React.

## Props

En React, los componentes se comunican principalmente a través de props. Esta es la forma en que los componentes padres pueden enviar datos a sus componentes hijos. Las props son el equivalente de los atributos HTML en los componentes de React.

### ¿Qué son las props?

-   Las props (abreviatura de "properties") son datos que los componentes padres envían a los componentes hijos.

-   Los componentes no pueden modificar sus propias props; simplemente las reciben como argumentos.

-   Son inmutables, lo que significa que una vez que un componente hijo las recibe, no puede cambiarlas directamente.

-   Los componentes funcionales reciben las props como un argumento de la función.

-   Los componentes de clase acceden a las props usando this.props.

-   Enviar props desde el componente padre al hijo

-   Cuando usas un componente, puedes pasarle props de la misma manera que pasarías atributos a una etiqueta HTML.

```jsx
function ComponentePadre() {
	return <ComponenteHijo mensaje="¡Hola desde el padre!" />;
}

function ComponenteHijo(props) {
	return <h1>{props.mensaje}</h1>;
}
```

En este ejemplo:

-   El `ComponentePadre` le pasa una prop mensaje al `ComponenteHijo`.

-   El `ComponenteHijo` accede a esa prop a través del objeto `props` y la muestra en un elemento `<h1>`.

### Props como atributos

Puedes pensar en las props como los atributos de las etiquetas HTML. Sin embargo, con React, puedes pasar cualquier tipo de dato a través de las props, no solo cadenas de texto.

```jsx
function ComponenteHijo(props) {
	return (
		<div>
			<h1>{props.titulo}</h1>

			<p>Edad: {props.edad}</p>

			<p>Es desarrollador: {props.esDesarrollador ? "Sí" : "No"}</p>
		</div>
	);
}

function ComponentePadre() {
	return <ComponenteHijo titulo="Perfil de Usuario" edad={25} esDesarrollador={true} />;
}
```

-   Aquí el ComponenteHijo recibe varios tipos de props: un string (titulo), un número (edad) y un booleano (esDesarrollador).

### Resumen

-   Props son la manera en que los componentes se comunican entre sí. El padre le pasa datos al hijo.

-   **Inmutabilidad:** Los componentes hijos no pueden cambiar las props que reciben.

-   Las props son similares a los atributos HTML, pero más poderosas porque pueden ser de cualquier tipo de dato (números, objetos, funciones, etc.).

**Ejemplo avanzado:** pasamos una función como prop

Además de datos estáticos, también puedes pasar funciones como props, lo que permite que los componentes hijos comuniquen eventos de vuelta al padre:

```jsx
function ComponentePadre() {
	const manejarClick = () => {
		alert("¡El botón fue clicado desde el hijo!");
	};

	return <ComponenteHijo onClick={manejarClick} />;
}

function ComponenteHijo(props) {
	return <button onClick={props.onClick}>Clic aquí</button>;
}
```

En este ejemplo, el ComponentePadre le pasa una función manejarClick al ComponenteHijo a través de la prop onClick. El ComponenteHijo ejecuta esa función cuando el botón es clicado, generando una interacción entre los dos.

## Estilos CSS

En React, tienes varias formas de aplicar estilos CSS a tus componentes. Aquí te explico las principales técnicas:

### 1. CSS tradicional (Archivos .css)

Puedes usar CSS como lo harías en cualquier proyecto web tradicional. Creas un archivo .css, defines tus clases y luego las aplicas a los elementos en los componentes React usando el atributo className (en lugar de class como en HTML estándar).

### Pasos:

1. Crea un archivo CSS (estilos.css):

```css
.mi-componente {
	color: blue;
	font-size: 20px;
}
```

2. Importa el archivo CSS en tu componente React:

```jsx
import "./estilos.css";

function MiComponente() {
	return <h1 className="mi-componente">¡Hola, mundo!</h1>;
}
```

### Notas:

-   **Importar archivos CSS:** Cada archivo de CSS que importes se aplicará a nivel global en tu aplicación.
-   **className vs class:** En JSX, se usa `className` en lugar de `class` porque `class` es una palabra reservada en JavaScript.

### 2. Estilos en línea

Puedes aplicar estilos directamente a los elementos usando el atributo style. Los estilos en línea se pasan como un objeto de JavaScript, donde las propiedades CSS se escriben en camelCase en lugar de la notación con guiones.

### Ejemplo:

```jsx
function MiComponente() {
	const estilos = {
		color: "red",
		backgroundColor: "yellow",
		fontSize: "24px",
	};

	return <h1 style={estilos}>¡Hola, con estilos en línea!</h1>;
}
```

### Notas:

Las propiedades CSS se escriben en camelCase (por ejemplo, backgroundColor en lugar de background-color).
Los valores numéricos como fontSize deben ser seguidos de una cadena que especifique la unidad (px, %, etc.), a menos que sea un número sin unidades.

### 3. CSS Modules (Módulos CSS)

Los CSS Modules son una forma de crear estilos locales y evitar conflictos de nombres entre clases. Con CSS Modules, cada clase o ID se convierte en un nombre único, lo que garantiza que los estilos se apliquen solo a un componente específico.

### Pasos:

1. Crea un archivo CSS con extensión .module.css (estilos.module.css):

```css
.miComponente {
	color: green;
	font-size: 18px;
}
```

2. Importa y aplica el módulo CSS en tu componente:

```jsx
import styles from "./estilos.module.css";

function MiComponente() {
	return <h1 className={styles.miComponente}>¡Hola con CSS Modules!</h1>;
}
```

### Ventajas:

Estilos locales: Las clases de CSS Modules son únicas y se aplican solo a los componentes donde se importan, evitando colisiones con otros estilos.

### 4. Styled Components (CSS en JS)

Otra opción muy popular es usar librerías como **Styled Components**, que permite escribir CSS directamente dentro de tu archivo JavaScript, creando componentes estilizados. Estos estilos se aplican de manera dinámica y permiten usar todas las capacidades de JavaScript dentro de los estilos.

### Instalación:

```bash
npm install styled-components
```

### Ejemplo:

```jsx
import styled from "styled-components";

const Titulo = styled.h1`
	color: purple;
	font-size: 22px;
	background-color: lightgray;
`;

function MiComponente() {
	return <Titulo>¡Hola con Styled Components!</Titulo>;
}
```

### Ventajas:

-   **Estilos dinámicos:** Puedes utilizar props y lógica de JavaScript dentro de tus estilos, lo que ofrece una flexibilidad enorme.
-   **Encapsulamiento total:** Los estilos aplicados a los componentes son únicos y no afectan otros componentes.

### 5. Frameworks y Librerías de CSS

Puedes usar frameworks CSS como Bootstrap, TailwindCSS, o librerías de componentes como Material-UI dentro de tus proyectos React. Estas herramientas ya vienen con clases predefinidas que puedes usar directamente en tus componentes.

### Ejemplo con Bootstrap:

**Instala Bootstrap:**

```bash
npm install bootstrap
```

**Importa Bootstrap en tu archivo principal (index.js o App.js):**

```jsx
import "bootstrap/dist/css/bootstrap.min.css";
```

```jsx
function MiComponente() {
	return <button className="btn btn-primary">Botón con Bootstrap</button>;
}
```

### Resumen de opciones para estilos en React

-   **CSS tradicional:** Clases globales, se comporta como CSS estándar.
-   **Estilos en línea:** Definidos directamente en el JSX, ideales para estilos dinámicos simples.
-   **CSS Modules:** Estilos locales y encapsulados, ideales para evitar colisiones de estilos.
-   **Styled Components:** CSS dentro de JS, ideal para componentes dinámicos y estilizados.
-   **Frameworks CSS:** Como Bootstrap o Tailwind para estilos rápidos y estandarizados.

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

## Estado

El estado es uno de los conceptos más importantes en React. Representa los datos que un componente necesita para renderizarse y actualizarse de forma dinámica. En otras palabras, el estado contiene información que puede cambiar con el tiempo y que afecta a cómo se muestra el componente.

A diferencia de las props (que son datos que un componente recibe desde su componente padre), el estado es interno y local al componente. Cada componente puede gestionar su propio estado y modificarlo cuando sea necesario.

### Características del Estado:

-   **Privado y local:** El estado es específico de un componente. A diferencia de las props, no puede ser accedido o modificado directamente por otros componentes.
-   **Dinamismo:** El estado permite a los componentes de React ser dinámicos, ya que cuando el estado cambia, React vuelve a renderizar el componente automáticamente.
-   **Controlado por el componente:** El componente gestiona su propio estado a través de funciones que permiten actualizarlo.

### Uso del Estado con useState

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

-   **useState(0):** Define el estado inicial (contador) con un valor de 0. El hook `useState` devuelve un arreglo con dos elementos:

-   **contador:** El valor actual del estado.

-   **setContador:** Una función que se usa para actualizar el estado.

-   **incrementar:** Es la función que se ejecuta cuando el botón es clicado. Llama a setContador para aumentar el valor del estado en 1.

Cuando el estado cambia con setContador, React vuelve a renderizar el componente para reflejar el nuevo valor del contador.

### Ciclo de vida del Estado

Cuando un componente se renderiza por primera vez, React establece el estado inicial. Luego, cuando el estado se actualiza (por ejemplo, al hacer clic en un botón), React:

-   Detecta que el estado ha cambiado.
-   Vuelve a renderizar el componente, aplicando los cambios necesarios en la interfaz.

### ¿Cuándo usar el Estado?

El estado es útil en situaciones donde un componente necesita:

-   **Gestionar entradas del usuario:** Como en un campo de texto donde se captura lo que el usuario escribe.
-   **Controlar interacciones:** Como un botón de "Me gusta" que cambia de estado al hacer clic.
-   **Mostrar o esconder elementos:** Como en un menú desplegable.
-   **Actualizar información dinámicamente:** Como en un contador o una lista que se actualiza a partir de datos.

**Ejemplo completo:** Controlar entradas de usuario

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

### En este ejemplo:

-   El estado `nombre` se actualiza cada vez que el usuario escribe algo en el campo de texto.
-   El valor del `input` se controla usando el estado, haciendo que React actualice dinámicamente el contenido del párrafo que muestra el nombre.

### Resumen del Estado en React

-   El estado es un mecanismo para almacenar datos locales dentro de un componente.
-   Se gestiona a través de hooks como useState en componentes funcionales.
-   Cuando el estado cambia, React vuelve a renderizar el componente automáticamente.
-   El estado es ideal para manejar cambios dinámicos en la interfaz de usuario, como interacciones o datos que deben cambiar a lo largo del tiempo.
