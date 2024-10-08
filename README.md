# Hooks en React

Los hooks son una característica de React que permite usar el estado y otras funcionalidades de React sin necesidad de escribir componentes de clase. Introducidos en React 16.8, los hooks hacen que los componentes funcionales sean más potentes y flexibles, proporcionando una forma simple y directa de manejar la lógica del ciclo de vida, el estado y los efectos secundarios en los componentes.

¿Por qué usar hooks?
Antes de los hooks, React requería usar componentes de clase para manejar el estado y el ciclo de vida. Los hooks permiten manejar estos aspectos directamente en componentes funcionales, lo que simplifica el código y mejora la legibilidad.

Hooks más importantes

## 1. useState

El hook useState permite agregar y gestionar el estado local en un componente funcional. Cada vez que el estado cambia, el componente se vuelve a renderizar.

Sintaxis:

```javascript
const [estado, setEstado] = useState(valorInicial);
```

estado: El valor actual del estado.
setEstado: Función para actualizar el valor del estado.
valorInicial: El valor inicial del estado.
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

## 2. useEffect

useEffect es un hook que se utiliza para manejar efectos secundarios en los componentes, como llamadas a APIs, suscripciones, o cambios en el DOM. Es similar a los métodos del ciclo de vida como componentDidMount, componentDidUpdate, y componentWillUnmount en los componentes de clase.

Sintaxis:

```javascript
useEffect(() => {
	// Código a ejecutar
}, [dependencias]);
```

Dependencias: Si proporcionas un array de dependencias, el efecto solo se ejecutará cuando esas dependencias cambien. Si el array está vacío, el efecto solo se ejecuta una vez después del primer renderizado.
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

## 3. useContext

useContext permite acceder al contexto de React, una forma de compartir datos globales (como el tema, la autenticación o el idioma) entre componentes sin tener que pasar props manualmente a través de cada nivel de componentes.

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

## 4. useReducer

useReducer es una alternativa a useState cuando la lógica del estado es más compleja. Es útil para gestionar el estado en aplicaciones más grandes o cuando el estado tiene múltiples transiciones.

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

## 5. useRef

useRef crea una referencia mutable que puedes asociar a elementos del DOM. No provoca renderizados adicionales cuando cambia.

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

## 6. useMemo

useMemo memoriza el resultado de una función costosa y solo la recalcula cuando cambian las dependencias. Ayuda a mejorar el rendimiento evitando cálculos innecesarios.

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

## Otros hooks útiles

useCallback: Devuelve una función memorizada que solo se crea nuevamente si cambian las dependencias.
useImperativeHandle: Personaliza la instancia de un componente que se expone a los padres usando ref.
useLayoutEffect: Similar a useEffect, pero se dispara después de que todas las modificaciones del DOM se han hecho.

## Conclusión

Los hooks son una herramienta poderosa que permiten escribir componentes más simples y reutilizables. Hacen que la gestión del estado, los efectos secundarios, y otras funcionalidades avanzadas en React sean más accesibles en componentes funcionales.
