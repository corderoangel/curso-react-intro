## React Portals

React Portals es una característica de React que permite renderizar componentes en un nodo del DOM fuera de la jerarquía DOM principal de la aplicación. Esto es útil cuando necesitas que un componente se muestre en una ubicación distinta en el árbol DOM, pero que mantenga la funcionalidad React (estado, eventos, etc.) asociada con su jerarquía original.

### ¿Cuándo usar React Portals?

Los portales son útiles en situaciones donde necesitas renderizar elementos fuera del flujo visual o estructural normal de tu aplicación, como:

-   **Modales:** Para evitar problemas de superposición o estilos de contenedores padres.
-   **Tooltips y popovers:** Para que se posicionen correctamente en relación al viewport, sin estar restringidos por el contenedor padre.
-   **Notificaciones o alertas globales:** Que deben aparecer por encima de todo el contenido.

### ¿Cómo funciona un Portal?

React Portals te permite especificar un nodo DOM distinto al nodo raíz de tu aplicación donde deseas renderizar el contenido. Esto se hace mediante la función ReactDOM.createPortal.

```javascript
ReactDOM.createPortal(
	children, // Los elementos que deseas renderizar
	domNode // El nodo DOM donde se debe renderizar
);
```

El método `createPortal` toma dos argumentos:

1. **children:** Los elementos React que quieres renderizar.
2. **domNode:** Un elemento DOM que existe fuera de la jerarquía DOM principal de tu aplicación, donde los elementos children se colocarán.

Ejemplo básico de React Portals
Imagina que estás creando un modal que debe aparecer sobre todo el contenido de la página. En lugar de renderizar el modal dentro del componente padre, puedes usar un portal para renderizarlo en el nodo DOM del documento (<div id="modal-root">).

1. Crear un nodo en el DOM para el portal
   En tu archivo HTML, agrega un elemento para contener el portal (por ejemplo, un `div` fuera del root principal):

```html
<body>
	<div id="root"></div>
	<div id="modal-root"></div>
</body>
```

2. Usar createPortal en React
   Crea un componente modal que use un portal para renderizarse en el nodo #modal-root.

```javascript
import React from "react";
import ReactDOM from "react-dom";

function Modal({ onClose }) {
	// Creamos un portal que se renderiza en #modal-root
	return ReactDOM.createPortal(
		<div className="modal">
			<div className="modal-content">
				<h2>Este es un modal</h2>
				<button onClick={onClose}>Cerrar</button>
			</div>
		</div>,
		document.getElementById("modal-root") // Renderizamos en #modal-root
	);
}

export default Modal;
```

3. Usar el modal en el componente principal

```javascript
import React, { useState } from "react";
import Modal from "./Modal";

function App() {
	const [isModalOpen, setIsModalOpen] = useState(false);

	return (
		<div>
			<h1>Aplicación principal</h1>
			<button onClick={() => setIsModalOpen(true)}>Abrir Modal</button>

			{isModalOpen && <Modal onClose={() => setIsModalOpen(false)} />}
		</div>
	);
}

export default App;
```

### Resultado

Cuando el usuario hace clic en "Abrir Modal", el modal se renderiza en el nodo `#modal-root` fuera del flujo normal de la aplicación React, pero aún sigue funcionando como parte de la misma jerarquía React, manteniendo el estado y eventos asociados.

### Ventajas de React Portals

-   **Control sobre el layout:** Puedes posicionar y estructurar el DOM de tus componentes sin estar limitado por el flujo normal del DOM en React.
-   **Interacción garantizada:** Aunque el contenido renderizado en el portal está fuera del árbol DOM principal, los eventos y el estado de React siguen funcionando como si estuviera dentro de la jerarquía React.
-   **Flexibilidad para elementos superpuestos:** Es especialmente útil para elementos que necesitan estar por encima de otros, como modales, tooltips o menús contextuales.

### Eventos y Portals

Aunque los elementos que renderizas con portales están fuera del árbol DOM principal, los eventos burbujean correctamente. Esto significa que si un elemento dentro del portal dispara un evento, seguirá burbujeando hacia los ancestros React como lo haría normalmente, incluso si esos ancestros no son parte del árbol DOM que contiene el portal.

### Ejemplo con un Tooltip

Otro caso común de uso de los portales es un tooltip que debe posicionarse sobre otros elementos en la página, sin estar restringido por el contenedor en el que fue creado.

```javascript
import React from "react";
import ReactDOM from "react-dom";

function Tooltip({ message, position }) {
	return ReactDOM.createPortal(
		<div style={{ position: "absolute", top: position.top, left: position.left }}>{message}</div>,
		document.body // El tooltip se renderiza en el cuerpo del documento
	);
}

export default Tooltip;
```

### Resumen

-   React Portals permite renderizar componentes en nodos DOM fuera de la jerarquía principal de React.
-   Utiliza ReactDOM.createPortal para especificar dónde se debe renderizar un componente.
-   Útil para elementos superpuestos como modales, tooltips, o notificaciones, sin afectar el flujo DOM principal.
-   Los eventos se manejan de la misma forma que en un componente normal, manteniendo la funcionalidad React completa.
