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
