# COMPONENTES

Un componente en React es una pieza reutilizable e independiente de código que encapsula una parte de la interfaz de usuario (UI) y la lógica asociada. Piensa en los componentes como los bloques de construcción que conforman una aplicación de React. Pueden ser tan simples como un botón o tan complejos como una página completa.

## Tipos de componentes:

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
