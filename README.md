# 1. Librerías de Iconos en React

Las librerías de iconos ofrecen una amplia gama de iconos que se pueden integrar fácilmente en tus componentes. Algunas de las más populares son:

## 1.1 Font Awesome

Font Awesome es una de las bibliotecas de iconos más utilizadas. Ofrece una gran cantidad de iconos gratuitos y premium que puedes incluir fácilmente en tus proyectos de React.

Pasos para usar Font Awesome en React:
Instala la librería de React Font Awesome usando npm:

```bash
npm install @fortawesome/react-fontawesome @fortawesome/free-solid-svg-icons
```

Importa el icono que quieres usar y el componente FontAwesomeIcon:

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

## 1.2 React Icons

Otra opción popular es la librería React Icons, que reúne varios paquetes de iconos como Font Awesome, Material Icons, Feather, entre otros.

Pasos para usar React Icons:
Instala la librería usando npm:

```bash
npm install react-icons
```

Importa el icono que quieres usar:

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

# 2. Usar SVG en React

Los SVGs son gráficos vectoriales escalables que puedes usar para renderizar iconos de alta calidad sin perder resolución. React permite integrar SVGs de dos maneras principales: como archivos o directamente en el JSX como código.

## 2.1. SVG como componente de React

Puedes importar un archivo SVG directamente como un componente React, lo que facilita su uso y personalización.

Primero, coloca el archivo SVG en tu proyecto.

Luego, importa el archivo SVG y úsalo como un componente:

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

## 2.2. SVG en JSX

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

En este ejemplo:

El código del SVG está directamente en el JSX, y puedes personalizar atributos como fill, width, y height para cambiar el color y tamaño del icono.
Ventajas de SVGs en React
Escalabilidad: Los SVGs son gráficos vectoriales, lo que significa que se escalan perfectamente sin perder calidad.
Personalización: Puedes cambiar fácilmente los atributos de un SVG (como el color y el tamaño) directamente en el JSX.
Ligereza: Los archivos SVG suelen ser muy livianos, lo que mejora el rendimiento de tu aplicación.
¿Cuándo usar Librerías de Iconos o SVGs?
Librerías de Iconos: Útiles cuando necesitas un conjunto grande de iconos rápidamente y no quieres preocuparte por diseñar o personalizar cada uno.
SVGs: Ideales para iconos personalizados o únicos que necesitan un alto grado de personalización o escalabilidad.
Ejemplo combinado
Aquí tienes un ejemplo donde uso tanto React Icons como un SVG personalizado:

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

Conclusión
Librerías de iconos como Font Awesome o React Icons te permiten agregar iconos de manera rápida y sencilla.
SVGs ofrecen mayor personalización y escalabilidad, y pueden integrarse directamente como componentes o como código JSX.
