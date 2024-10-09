# Efectos en React: useEffect

El hook useEffect en React es utilizado para manejar efectos secundarios en componentes funcionales. Los efectos secundarios incluyen cualquier interacción con el mundo externo o cualquier cosa que no esté directamente relacionada con el renderizado del componente, como:

Llamadas a APIs.
Suscripciones a eventos.
Manipulación directa del DOM.
Temporizadores o intervalos.
Limpieza de efectos anteriores cuando un componente se desmonta.
El hook useEffect es un reemplazo para los métodos del ciclo de vida en los componentes de clase, como componentDidMount, componentDidUpdate, y componentWillUnmount.

Sintaxis básica

```javascript
useEffect(() => {
	// Código del efecto
}, [dependencias]);
```

## Parámetros de useEffect

Función de efecto: Se ejecuta después de que el componente ha sido renderizado. Dentro de esta función puedes colocar lógica que realice cualquier efecto secundario.
Array de dependencias (opcional): Especifica qué valores deben cambiar para que el efecto se vuelva a ejecutar. Si no se especifica, el efecto se ejecuta en cada renderizado.
Ejemplos comunes de useEffect

1. Ejecución en cada renderizado
   Si no proporcionas un array de dependencias, el efecto se ejecutará después de cada renderizado del componente.

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

2. Ejecución solo una vez (equivalente a componentDidMount)
   Si proporcionas un array de dependencias vacío ([]), el efecto se ejecuta solo una vez, cuando el componente se monta.

```javascript
useEffect(() => {
	console.log("Este efecto solo se ejecuta una vez cuando el componente se monta.");
}, []);
```

Esto es útil para operaciones como llamadas a APIs o suscripciones que solo necesitan ocurrir una vez.

3. Ejecución cuando cambian las dependencias
   Puedes especificar dependencias en el array para ejecutar el efecto solo cuando ciertos valores cambian.

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

En este ejemplo, el efecto que establece el intervalo se ejecuta una vez cuando el componente se monta. El efecto de limpieza (clearInterval) se ejecuta cuando el componente se desmonta.

4. Limpieza de efectos (equivalente a componentWillUnmount)
   Cuando un componente se desmonta, puedes realizar tareas de limpieza (como cancelar suscripciones, detener temporizadores o eliminar escuchadores de eventos) devolviendo una función desde el useEffect.

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

5. Múltiples efectos en un componente
   Puedes tener más de un useEffect en un mismo componente para manejar diferentes efectos.

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

Ejemplo completo con useEffect
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

## Resumen

useEffect es el hook para manejar efectos secundarios como actualizaciones del DOM, llamadas a APIs, suscripciones, y más.
Se ejecuta después del renderizado del componente.
Puedes controlar cuándo se ejecuta usando un array de dependencias.
El useEffect también puede manejar la limpieza de efectos al desmontar o actualizar el componente.
