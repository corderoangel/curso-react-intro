# INTRODUCCIÓN A REACT

## Índice

1. [Componentes](#componentes)
2. [Props](#props)
3. [Estilos CSS en React](#estilos-css-en-react)
    1. [CSS tradicional (Archivos .css)](#1-css-tradicional-archivos-css)
        - [Pasos](#pasos)
        - [Notas](#notas)
    2. [Estilos en línea](#2-estilos-en-línea)
        - [Ejemplo](#ejemplo)
        - [Notas](#notas-1)
    3. [CSS Modules (Módulos CSS)](#3-css-modules-módulos-css)
        - [Pasos](#pasos-1)
        - [Ventajas](#ventajas)
    4. [Styled Components (CSS en JS)](#4-styled-components-css-en-js)
        - [Instalación](#instalación)
        - [Ejemplo](#ejemplo-1)
        - [Ventajas](#ventajas-1)
    5. [Frameworks y Librerías de CSS](#5-frameworks-y-librerías-de-css)
        - [Ejemplo con Bootstrap](#ejemplo-con-bootstrap)
4. [Resumen de opciones para estilos en React](#resumen-de-opciones-para-estilos-en-react)

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

## Estilos CSS en React

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
