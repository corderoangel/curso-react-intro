# INTRODUCCIÓN A REACT

## Índice

1. [Qué es un componente](#qué-es-un-componente)
2. [Tipos de componentes](#tipos-de-componentes)
    - [Componentes funcionales](#componentes-funcionales)
    - [Componentes de clase](#componentes-de-clase)
3. [Características clave de los componentes](#características-clave-de-los-componentes)
    - [Reutilizables](#reutilizables)
    - [Modulares](#modulares)
    - [Declarativos](#declarativos)
    - [Reciben datos a través de props](#reciben-datos-a-través-de-props)
4. [JSX (JavaScript + XML)](#jsx-javascript--xml)
5. [Comunicación entre componentes en React: Props y atributos](#comunicación-entre-componentes-en-react-props-y-atributos)
6. [¿Qué son las props?](#qué-son-las-props)
7. [Props como atributos](#props-como-atributos)
8. [Resumen](#resumen)

## Qué es un componente

Un componente en React es una pieza reutilizable e independiente de código que encapsula una parte de la interfaz de usuario (UI) y la lógica asociada. Piensa en los componentes como los bloques de construcción que conforman una aplicación de React. Pueden ser tan simples como un botón o tan complejos como una página completa.

## Tipos de componentes

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

## Características clave de los componentes:

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

## JSX (JavaScript + XML)

En React, el código que parece HTML en realidad es JSX, que te permite escribir estructuras de UI en un archivo JavaScript y luego ser traducido a JavaScript por React.

## Comunicación entre componentes en React: Props y atributos

En React, los componentes se comunican principalmente a través de props. Esta es la forma en que los componentes padres pueden enviar datos a sus componentes hijos. Las props son el equivalente de los atributos HTML en los componentes de React.

## ¿Qué son las props?

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

## Props como atributos

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

## Resumen

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
