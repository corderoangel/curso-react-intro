# Comunicación entre componentes en React: Props y atributos

En React, los componentes se comunican principalmente a través de props. Esta es la forma en que los componentes padres pueden enviar datos a sus componentes hijos. Las props son el equivalente de los atributos HTML en los componentes de React.

## ¿Qué son las props?

Las props (abreviatura de "properties") son datos que los componentes padres envían a los componentes hijos. Los componentes no pueden modificar sus propias props; simplemente las reciben como argumentos.

Son inmutables, lo que significa que una vez que un componente hijo las recibe, no puede cambiarlas directamente.

Los componentes funcionales reciben las props como un argumento de la función.

Los componentes de clase acceden a las props usando this.props.

Enviar props desde el componente padre al hijo

Cuando usas un componente, puedes pasarle props de la misma manera que pasarías atributos a una etiqueta HTML.

```jsx
function ComponentePadre() {
	return <ComponenteHijo mensaje="¡Hola desde el padre!" />;
}

function ComponenteHijo(props) {
	return <h1>{props.mensaje}</h1>;
}
```

En este ejemplo:

El ComponentePadre le pasa una prop mensaje al ComponenteHijo.

El ComponenteHijo accede a esa prop a través del objeto props y la muestra en un elemento <h1>.

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

Aquí el ComponenteHijo recibe varios tipos de props: un string (titulo), un número (edad) y un booleano (esDesarrollador).

## Resumen

Props son la manera en que los componentes se comunican entre sí. El padre le pasa datos al hijo.

Inmutabilidad: Los componentes hijos no pueden cambiar las props que reciben.

Las props son similares a los atributos HTML, pero más poderosas porque pueden ser de cualquier tipo de dato (números, objetos, funciones, etc.).

Ejemplo avanzado: pasamos una función como prop

Además de datos estáticos, también puedes pasar funciones como props, lo que permite que los componentes hijos comuniquen eventos de vuelta al padre:

```jsx

Copiar código

function ComponentePadre() {

const manejarClick = () => {

alert('¡El botón fue clicado desde el hijo!');

};

return <ComponenteHijo onClick={manejarClick} />;

}

function ComponenteHijo(props) {

return <button onClick={props.onClick}>Clic aquí</button>;

}
```

En este ejemplo, el ComponentePadre le pasa una función manejarClick al ComponenteHijo a través de la prop onClick. El ComponenteHijo ejecuta esa función cuando el botón es clicado, generando una interacción entre los dos.
