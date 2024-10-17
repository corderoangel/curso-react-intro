# INTRODUCCIÓN A REACT

## Índice

1. [Componentes](#componentes)
2. [Props](#props)
3. [Estilos CSS](#estilos-css)
4. [Eventos](#eventos)
5. [Estado](#estado)
6. [Iconos](#iconos)
7. [Local storage](#localstorage)
8. [Hooks](#hooks)
9. [Carpetas](#carpetas)
10. [Efectos](#efectos-useeffect)

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

## Iconos

Las librerías de iconos ofrecen una amplia gama de iconos que se pueden integrar fácilmente en tus componentes. Algunas de las más populares son:

### Font Awesome

Font Awesome es una de las bibliotecas de iconos más utilizadas. Ofrece una gran cantidad de iconos gratuitos y premium que puedes incluir fácilmente en tus proyectos de React.

**Pasos para usar Font Awesome en React:**

1. Instala la librería de React Font Awesome usando npm:

```bash
npm install @fortawesome/react-fontawesome @fortawesome/free-solid-svg-icons
```

2. Importa el icono que quieres usar y el componente FontAwesomeIcon:

```jsx
import { FontAwesomeIcon } from "@fortawesome/react-fontawesome";
import { faCoffee } from "@fortawesome/free-solid-svg-icons";

function MiComponente() {
	return (
		<div>
			<h1>
				Disfruta tu café <FontAwesomeIcon icon={faCoffee} />
			</h1>
		</div>
	);
}
```

En este ejemplo, el icono del café (faCoffee) se renderiza dentro de un h1.

### React Icons

Otra opción popular es la librería React Icons, que reúne varios paquetes de iconos como Font Awesome, Material Icons, Feather, entre otros.

**Pasos para usar React Icons:**

1. Instala la librería usando npm:

```bash
npm install react-icons
```

2. Importa el icono que quieres usar:

```jsx
import { FaBeer } from "react-icons/fa"; // Importa el icono desde el paquete Font Awesome

function MiComponente() {
	return (
		<div>
			<h1>
				¡Vamos a tomar una cerveza! <FaBeer />
			</h1>
		</div>
	);
}
```

Con React Icons, puedes combinar diferentes colecciones de iconos en una sola aplicación sin necesidad de instalar cada paquete por separado.

### Usar SVG en React

Los SVGs son gráficos vectoriales escalables que puedes usar para renderizar iconos de alta calidad sin perder resolución. React permite integrar SVGs de dos maneras principales: como archivos o directamente en el JSX como código.

#### SVG como componente de React

Puedes importar un archivo SVG directamente como un componente React, lo que facilita su uso y personalización.

-   Primero, coloca el archivo SVG en tu proyecto.

-   Luego, importa el archivo SVG y úsalo como un componente:

```jsx
import React from "react";
import { ReactComponent as Logo } from "./logo.svg"; // Importa el SVG como un componente

function MiComponente() {
	return (
		<div>
			<h1>Mi Aplicación</h1>
			<Logo /> {/_ Renderiza el SVG como un componente _/}
		</div>
	);
}
```

### SVG en JSX

Otra forma de usar SVGs es incluir directamente el código SVG dentro del JSX del componente. Esto te permite personalizar el SVG más fácilmente, como cambiar el color, tamaño, etc.

```jsx
function IconoPersonalizado() {
	return (
		<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="100" height="100" fill="blue">
			<path d="M12 2L2 22h20L12 2zm0 3.84L18.66 20H5.34L12 5.84zM12 9c-.552 0-1 .448-1 1s.448 1 1 1 1-.448 1-1-.448-1-1-1zm0 4c-.552 0-1 .448-1 1v4h2v-4c0-.552-.448-1-1-1z" />
		</svg>
	);
}

function MiComponente() {
	return (
		<div>
			<h1>Icono SVG personalizado</h1>
			<IconoPersonalizado />
		</div>
	);
}
```

**En este ejemplo:**

El código del SVG está directamente en el JSX, y puedes personalizar atributos como `fill`, `width`, y `height` para cambiar el color y tamaño del icono.

### Ventajas de SVGs en React

-   **Escalabilidad:** Los SVGs son gráficos vectoriales, lo que significa que se escalan perfectamente sin perder calidad.
-   **Personalización:** Puedes cambiar fácilmente los atributos de un SVG (como el color y el tamaño) directamente en el JSX.
-   **Ligereza:** Los archivos SVG suelen ser muy livianos, lo que mejora el rendimiento de tu aplicación.

### ¿Cuándo usar Librerías de Iconos o SVGs?

-   **Librerías de Iconos:** Útiles cuando necesitas un conjunto grande de iconos rápidamente y no quieres preocuparte por diseñar o personalizar cada uno.
-   **SVGs:** Ideales para iconos personalizados o únicos que necesitan un alto grado de personalización o escalabilidad.

**Ejemplo combinado**
Aquí tienes un ejemplo donde uso tanto `React Icons` como un `SVG` personalizado:

```jsx
import { FaReact } from "react-icons/fa"; // React Icons

function MiComponente() {
	return (
		<div>
			<h1>Iconos en React</h1>
			<h2>React Icon:</h2>
			<FaReact size="50" color="blue" /> {/_ Usando React Icons _/}
			<h2>SVG personalizado:</h2>
			<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="50" height="50" fill="red">
				<path d="M12 2L2 22h20L12 2zm0 3.84L18.66 20H5.34L12 5.84zM12 9c-.552 0-1 .448-1 1s.448 1 1 1 1-.448 1-1-.448-1-1-1zm0 4c-.552 0-1 .448-1 1v4h2v-4c0-.552-.448-1-1-1z" />
			</svg>
		</div>
	);
}
```

En este ejemplo, usamos React Icons para mostrar el logo de React y un SVG personalizado que hemos integrado directamente en el JSX.

### Conclusión

-   Librerías de iconos como Font Awesome o React Icons te permiten agregar iconos de manera rápida y sencilla.
-   SVGs ofrecen mayor personalización y escalabilidad, y pueden integrarse directamente como componentes o como código JSX.

## LocalStorage

LocalStorage es una API de almacenamiento del lado del cliente que permite guardar datos de manera
persistente en el navegador del usuario. Los datos almacenados en el LocalStorage no tienen fecha de
expiración, lo que significa que permanecerán allí incluso si el usuario cierra el navegador o reinicia
su computadora, hasta que se eliminen manualmente o mediante código.

A continuación te explico cómo funciona y cómo puedes utilizarlo en tus proyectos.

### Características de LocalStorage:

-   **Persistencia:** Los datos almacenados no se eliminan cuando se cierra el navegador, a diferencia de
    `SessionStorage`, que se borra cuando la sesión del navegador finaliza.

-   **Almacenamiento basado en clave-valor:** Almacena pares de claves y valores, donde ambas deben ser
    cadenas de texto.

-   **Capacidad:** Los navegadores típicamente ofrecen entre 5 y 10 MB de almacenamiento por origen.

-   **Alcance:** Los datos se almacenan por dominio, por lo que solo las páginas del mismo dominio pueden
    acceder a los datos almacenados.

### Métodos principales de LocalStorage

El objeto localStorage proporciona los siguientes métodos para manipular los datos:

-   **setItem(key, value):** Almacena un valor con una clave específica.
-   **getItem(key):** Recupera el valor almacenado de una clave.
-   **removeItem(key):** Elimina el valor almacenado de una clave específica.
-   **clear():** Elimina todos los datos almacenados en el LocalStorage.
-   **length:** Devuelve el número de pares clave-valor almacenados.
-   **key(index):** Devuelve la clave en la posición especificada por el índice.

**Ejemplos de uso**

1. Guardar datos en el LocalStorage:

```javascript
// Guardar un valor en LocalStorage
localStorage.setItem("nombre", "Juan");

// Guardar un valor numérico (debe ser convertido a string)
localStorage.setItem("edad", 25);
```

En este ejemplo, se guardan dos valores:

Una cadena de texto con la clave "nombre" y el valor "Juan".
Un número con la clave "edad" y el valor 25. El número se convierte automáticamente a una cadena de texto.

2. Recuperar datos del LocalStorage:

```javascript
// Recuperar los datos almacenados
const nombre = localStorage.getItem("nombre");
const edad = localStorage.getItem("edad");

console.log(nombre); // "Juan"
console.log(edad); // "25" (aunque se guardó como número, LocalStorage lo devuelve como string)
```

3. Eliminar datos específicos del LocalStorage:

```javascript
// Eliminar un valor específico
localStorage.removeItem("nombre");

// Intentar recuperar el valor eliminado
console.log(localStorage.getItem("nombre")); // null
```

4. Limpiar todo el LocalStorage:

```javascript
// Eliminar todos los elementos del LocalStorage
localStorage.clear();
```

5. Recorrer todas las claves almacenadas:

```javascript
for (let i = 0; i < localStorage.length; i++) {
	const clave = localStorage.key(i);
	const valor = localStorage.getItem(clave);
	console.log(`Clave: ${clave}, Valor: ${valor}`);
}
```

Este código itera sobre todas las claves almacenadas en LocalStorage y muestra tanto la clave como el valor
asociado.

### Almacenar objetos en LocalStorage

LocalStorage solo acepta valores en formato de cadena de texto (string). Si deseas almacenar objetos,
primero debes convertirlos a JSON usando `JSON.stringify()`, y cuando los recuperes, deberás convertirlos
nuevamente a un objeto usando `JSON.parse()`.

Ejemplo de almacenar y recuperar un objeto:

```javascript
// Crear un objeto
const usuario = {
	nombre: "Juan",
	edad: 30,
	pais: "España",
};

// Convertir el objeto a JSON y almacenarlo
localStorage.setItem("usuario", JSON.stringify(usuario));

// Recuperar el objeto almacenado y convertirlo de nuevo a objeto JavaScript
const usuarioRecuperado = JSON.parse(localStorage.getItem("usuario"));

console.log(usuarioRecuperado); // {nombre: "Juan", edad: 30, pais: "España"}
```

### Usos comunes de LocalStorage

-   **Persistir preferencias de usuario:** Puedes almacenar configuraciones como el tema (oscuro/claro),
    idioma, preferencias de diseño, etc.

-   **Carrito de compras:** Es útil para guardar el contenido de un carrito de compras en una tienda en línea,
    permitiendo al usuario recuperar los productos seleccionados al regresar.

-   **Datos de formularios:** Almacenar temporalmente la información que el usuario ha ingresado en un
    formulario para prevenir la pérdida de datos si la página se recarga.

-   **Autenticación básica:** Guardar tokens de autenticación para gestionar sesiones en aplicaciones sin
    servidores de autenticación avanzados (aunque es recomendable usar cookies o SessionStorage para tokens).

### Limitaciones de LocalStorage

-   **Seguridad:** Los datos en LocalStorage no están cifrados, lo que significa que pueden ser accesibles
    por scripts maliciosos si tu sitio web sufre un ataque XSS. Nunca guardes información sensible (como
    contraseñas o tokens de acceso sin cifrar) en LocalStorage.

-   **Sincronización:** LocalStorage es síncrono, lo que significa que cada operación de lectura o escritura
    puede bloquear la ejecución del código mientras se procesa. Esto podría generar problemas de rendimiento si
    se realizan muchas operaciones consecutivas.

-   **Espacio limitado:** Aunque la mayoría de los navegadores permiten entre 5 y 10 MB de almacenamiento,
    esta cantidad puede no ser suficiente para aplicaciones con grandes volúmenes de datos.

### Conclusión

LocalStorage es una herramienta poderosa y fácil de usar para almacenar datos persistentes en el navegador
del usuario. Aunque tiene ciertas limitaciones, es una opción ideal para guardar datos no sensibles y de
bajo tamaño, como configuraciones, temas o preferencias de usuario.

## Hooks

Los hooks son una característica de React que permite usar el estado y otras funcionalidades de React sin
necesidad de escribir componentes de clase. Introducidos en React 16.8, los hooks hacen que los componentes
funcionales sean más potentes y flexibles, proporcionando una forma simple y directa de manejar la lógica
del ciclo de vida, el estado y los efectos secundarios en los componentes.

### ¿Por qué usar hooks?

Antes de los hooks, React requería usar componentes de clase para manejar el estado y el ciclo de vida.
Los hooks permiten manejar estos aspectos directamente en componentes funcionales, lo que simplifica el
código y mejora la legibilidad.

#### Hooks más importantes

1. useState

El hook useState permite agregar y gestionar el estado local en un componente funcional. Cada vez que el
estado cambia, el componente se vuelve a renderizar.

Sintaxis:

```javascript
const [estado, setEstado] = useState(valorInicial);
```

-   **estado:** El valor actual del estado.
-   **setEstado:** Función para actualizar el valor del estado.
-   **valorInicial:** El valor inicial del estado.

Ejemplo:

```javascript
import { useState } from "react";

function Contador() {
	const [contador, setContador] = useState(0);

	return (
		<div>
			<p>Has hecho clic {contador} veces</p>
			<button onClick={() => setContador(contador + 1)}>Incrementar</button>
		</div>
	);
}
```

2. useEffect

useEffect es un hook que se utiliza para manejar efectos secundarios en los componentes, como llamadas
a APIs, suscripciones, o cambios en el DOM. Es similar a los métodos del ciclo de vida como
`componentDidMount`, `componentDidUpdate`, y `componentWillUnmount` en los componentes de clase.

**Sintaxis:**

```javascript
useEffect(() => {
	// Código a ejecutar
}, [dependencias]);
```

**Dependencias:** Si proporcionas un array de dependencias, el efecto solo se ejecutará cuando esas
dependencias cambien. Si el array está vacío, el efecto solo se ejecuta una vez después del primer
renderizado.

Ejemplo:

```javascript
import { useState, useEffect } from "react";

function Reloj() {
	const [hora, setHora] = useState(new Date());

	useEffect(() => {
		const intervalId = setInterval(() => {
			setHora(new Date());
		}, 1000);

		return () => clearInterval(intervalId); // Limpieza del intervalo al desmontar
	}, []);

	return <h2>{hora.toLocaleTimeString()}</h2>;
}
```

3. useContext

useContext permite acceder al contexto de React, una forma de compartir datos globales (como el tema,
la autenticación o el idioma) entre componentes sin tener que pasar props manualmente a través de cada
nivel de componentes.

Sintaxis:

```javascript
const valor = useContext(Contexto);
```

Ejemplo:

```javascript
import { useContext } from "react";
import { TemaContexto } from "./TemaContexto";

function Boton() {
	const tema = useContext(TemaContexto);

	return <button style={{ background: tema.color }}>Botón</button>;
}
```

4. useReducer

`useReducer` es una alternativa a useState cuando la lógica del estado es más compleja. Es útil para
gestionar el estado en aplicaciones más grandes o cuando el estado tiene múltiples transiciones.

Sintaxis:

```javascript
const [estado, dispatch] = useReducer(reducer, estadoInicial);
```

reducer: Una función que toma el estado actual y una acción, y devuelve un nuevo estado.
estadoInicial: El estado inicial para el reducer.
Ejemplo:

```javascript
import { useReducer } from "react";

function reducer(estado, accion) {
	switch (accion.type) {
		case "incrementar":
			return { contador: estado.contador + 1 };
		case "decrementar":
			return { contador: estado.contador - 1 };
		default:
			return estado;
	}
}

function Contador() {
	const [estado, dispatch] = useReducer(reducer, { contador: 0 });

	return (
		<div>
			<p>{estado.contador}</p>
			<button onClick={() => dispatch({ type: "incrementar" })}>Incrementar</button>
			<button onClick={() => dispatch({ type: "decrementar" })}>Decrementar</button>
		</div>
	);
}
```

5. useRef

`useRef` crea una referencia mutable que puedes asociar a elementos del DOM. No provoca renderizados
adicionales cuando cambia.

Sintaxis:

```javascript
const ref = useRef(valorInicial);
```

Ejemplo:

```javascript
import { useRef } from "react";

function EntradaEnfocar() {
	const inputRef = useRef(null);

	const enfocarInput = () => {
		inputRef.current.focus();
	};

	return (
		<div>
			<input ref={inputRef} />
			<button onClick={enfocarInput}>Enfocar input</button>
		</div>
	);
}
```

6. useMemo

`useMemo` memoriza el resultado de una función costosa y solo la recalcula cuando cambian las dependencias.
Ayuda a mejorar el rendimiento evitando cálculos innecesarios.

Sintaxis:

```javascript
const valorMemorizado = useMemo(() => calcularValor(), [dependencias]);
```

Ejemplo:

```javascript
import { useMemo } from "react";

function Lista({ elementos }) {
	const listaOrdenada = useMemo(() => {
		return elementos.sort();
	}, [elementos]);

	return (
		<ul>
			{listaOrdenada.map((el) => (
				<li key={el}>{el}</li>
			))}
		</ul>
	);
}
```

### Otros hooks útiles

**useCallback:** Devuelve una función memorizada que solo se crea nuevamente si cambian las dependencias.
**useImperativeHandle:** Personaliza la instancia de un componente que se expone a los padres usando ref.
**useLayoutEffect:** Similar a useEffect, pero se dispara después de que todas las modificaciones del DOM
se han hecho.

### Conclusión

Los hooks son una herramienta poderosa que permiten escribir componentes más simples y reutilizables.
Hacen que la gestión del estado, los efectos secundarios, y otras funcionalidades avanzadas en React
sean más accesibles en componentes funcionales.

## Carpetas

En un proyecto típico de React, la organización de carpetas varía según las preferencias del equipo y la escala del proyecto, pero hay algunas estructuras comunes que muchos desarrolladores utilizan para mantener el código organizado y fácil de mantener. A continuación te presento una estructura de carpetas recomendada y ampliamente utilizada:

1. Estructura Base

```bash
/src
│
├── /assets
│   ├── /images      # Imágenes o gráficos utilizados en la aplicación
│   ├── /fonts       # Tipografías personalizadas
│   ├── /styles      # Estilos CSS globales o archivos SCSS
│
├── /components
│   ├── /Button      # Componente reutilizable con su CSS y tests
│   │   ├── Button.js
│   │   ├── Button.css
│   │   └── Button.test.js
│   └── /Header
│       ├── Header.js
│       ├── Header.css
│       └── Header.test.js
│
├── /hooks           # Hooks personalizados (custom hooks)
│   └── useAuth.js
│
├── /context         # Context API para estados globales
│   └── AuthContext.js
│
├── /pages           # Páginas o vistas principales de la aplicación
│   ├── Home.js
│   ├── About.js
│   └── Contact.js
│
├── /services        # Servicios o funciones que realizan peticiones a APIs
│   ├── apiService.js
│   └── authService.js
│
├── /store           # Manejo del estado global con Redux o cualquier otra librería de estado
│   ├── actions.js
│   ├── reducers.js
│   └── store.js
│
├── /utils           # Utilidades y funciones auxiliares (helpers)
│   └── formatDate.js
│
├── App.js           # Componente raíz de la aplicación
├── index.js         # Punto de entrada principal
└── reportWebVitals.js # Archivo de performance (puede o no usarse)
```

### Descripción de las carpetas:

-   **/assets:** Aquí se almacenan los recursos estáticos como imágenes, fuentes y estilos globales.

-   **/components:** Se guardan los componentes reutilizables de la aplicación, organizados en carpetas donde cada componente tiene sus archivos de lógica (JS o JSX), estilos (CSS o SCSS), y pruebas (test.js).

-   **/hooks:** Hooks personalizados para reutilizar la lógica que involucra estados o efectos complejos.

-   **/context:** Aquí se almacenan los contextos creados con la Context API para manejar estados globales o temas que necesiten compartirse en toda la aplicación.

-   **/pages:** Las páginas o vistas principales, que pueden estar asociadas a rutas específicas.

-   **/services:** Se colocan los servicios que hacen peticiones a APIs o manejan la lógica relacionada con datos externos.

-   **/store:** Si utilizas una librería de manejo de estado como Redux, aquí se alojan los archivos de acciones (actions), reductores (reducers) y la configuración del store.

-   **/utils:** Funciones auxiliares o de utilidad que no encajan en otras categorías, como formateadores de fechas, validaciones, etc.

2. Organización por feature o módulo

En proyectos más grandes, algunos equipos optan por una estructura basada en features (funcionalidades), agrupando componentes, servicios, y hooks relacionados en una carpeta por módulo. Por ejemplo:

```bash
Copiar código
/src
├── /features
│ ├── /auth
│ │ ├── components
│ │ ├── services
│ │ ├── hooks
│ │ └── AuthContext.js
│ └── /dashboard
│ ├── components
│ ├── services
│ ├── hooks
│ └── Dashboard.js
```

### Consideraciones Finales

-   **Escalabilidad:** La organización modular o por feature ayuda a mantener proyectos grandes bien organizados.
-   **Reutilización:** Mantener componentes, hooks y servicios bien estructurados en sus carpetas facilita su reutilización.
-   **Pruebas:** Es recomendable que los archivos de pruebas se ubiquen junto a los componentes que prueban, para mantener la cohesión del código.

Este enfoque es flexible y puedes adaptarlo según las necesidades específicas de tu proyecto.

## Efectos (useEffect)

El hook `useEffect` en React es utilizado para manejar efectos secundarios en componentes funcionales. Los efectos secundarios incluyen cualquier interacción con el mundo externo o cualquier cosa que no esté directamente relacionada con el renderizado del componente, como:

-   Llamadas a APIs.
-   Suscripciones a eventos.
-   Manipulación directa del DOM.
-   Temporizadores o intervalos.
-   Limpieza de efectos anteriores cuando un componente se desmonta.
-   El hook `useEffect` es un reemplazo para los métodos del ciclo de vida en los componentes de clase, como `componentDidMount`, `componentDidUpdate`, y `componentWillUnmount`.

Sintaxis básica

```javascript
useEffect(() => {
	// Código del efecto
}, [dependencias]);
```

### Parámetros de useEffect

-   **Función de efecto:** Se ejecuta después de que el componente ha sido renderizado. Dentro de esta función puedes colocar lógica que realice cualquier efecto secundario.

-   **Array de dependencias (opcional):** Especifica qué valores deben cambiar para que el efecto se vuelva a ejecutar. Si no se especifica, el efecto se ejecuta en cada renderizado.

Ejemplos comunes de useEffect:

1. **Ejecución en cada renderizado:** si no proporcionas un array de dependencias, el efecto se ejecutará después de cada renderizado del componente.

```javascript
import { useState, useEffect } from "react";

function Contador() {
	const [contador, setContador] = useState(0);

	useEffect(() => {
		console.log("El componente ha sido renderizado o actualizado.");
	});

	return (
		<div>
			<p>Contador: {contador}</p>
			<button onClick={() => setContador(contador + 1)}>Incrementar</button>
		</div>
	);
}
```

En este ejemplo, el useEffect se ejecuta cada vez que el componente se renderiza, incluso cuando el estado del contador cambia.

2. **Ejecución solo una vez (equivalente a componentDidMount)**: si proporcionas un array de dependencias vacío ([]), el efecto se ejecuta solo una vez, cuando el componente se monta.

```javascript
useEffect(() => {
	console.log("Este efecto solo se ejecuta una vez cuando el componente se monta.");
}, []);
```

Esto es útil para operaciones como llamadas a APIs o suscripciones que solo necesitan ocurrir una vez.

3. **Ejecución cuando cambian las dependencias**: Puedes especificar dependencias en el array para ejecutar el efecto solo cuando ciertos valores cambian.

```javascript
import { useState, useEffect } from "react";

function Reloj() {
	const [segundos, setSegundos] = useState(0);

	useEffect(() => {
		const intervalId = setInterval(() => {
			setSegundos((s) => s + 1);
		}, 1000);

		// Limpieza del intervalo cuando el componente se desmonta
		return () => clearInterval(intervalId);
	}, []);

	return <p>Segundos: {segundos}</p>;
}
```

En este ejemplo, el efecto que establece el intervalo se ejecuta una vez cuando el componente se monta. El efecto de limpieza `(clearInterval)` se ejecuta cuando el componente se desmonta.

4. **Limpieza de efectos (equivalente a componentWillUnmount)**: Cuando un componente se desmonta, puedes realizar tareas de limpieza (como cancelar suscripciones, detener temporizadores o eliminar escuchadores de eventos) devolviendo una función desde el useEffect.

```javascript
useEffect(() => {
	// Suscribirse a algún evento o recurso externo
	const suscripcion = suscribirseAEvento();

	// Limpieza cuando el componente se desmonta
	return () => {
		desuscribirseDeEvento(suscripcion);
	};
}, []);
```

Esta función de limpieza se ejecuta cuando el componente se desmonta o cuando cambian las dependencias, previniendo fugas de memoria y manteniendo el comportamiento del componente predecible.

5. **Múltiples efectos en un componente**: Puedes tener más de un `useEffect` en un mismo componente para manejar diferentes efectos.

```javascript
useEffect(() => {
	// Efecto 1
	console.log("Se ejecuta al montar");
}, []);

useEffect(() => {
	// Efecto 2
	console.log("Se ejecuta en cada renderizado");
});
```

Cada uno tiene su propio comportamiento dependiendo de las dependencias que especifiques.

**Ejemplo completo con useEffect**
Este ejemplo ilustra cómo usar useEffect para manejar un temporizador y una limpieza al desmontar el componente.

```javascript
import { useState, useEffect } from "react";

function Temporizador() {
	const [segundos, setSegundos] = useState(0);

	useEffect(() => {
		const intervalId = setInterval(() => {
			setSegundos((prev) => prev + 1);
		}, 1000);

		// Limpieza del intervalo cuando el componente se desmonta
		return () => clearInterval(intervalId);
	}, []); // El efecto solo se ejecuta una vez, al montar el componente

	return <div>Han pasado {segundos} segundos.</div>;
}
```

Aquí, el temporizador se incrementa cada segundo y cuando el componente se desmonta, el intervalo se limpia para evitar comportamientos inesperados.

### Resumen

-   useEffect es el hook para manejar efectos secundarios como actualizaciones del DOM, llamadas a APIs, suscripciones, y más.
-   Se ejecuta después del renderizado del componente.
-   Puedes controlar cuándo se ejecuta usando un array de dependencias.
-   El `useEffect` también puede manejar la limpieza de efectos al desmontar o actualizar el componente.
