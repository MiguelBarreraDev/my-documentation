## Conceptos de JavaScript Moderno
- Definimos variables con declaraciones **let y const**
- Usamos la palabra **class** para definir las clases en JavaScript
- Usamos a veces **=>** para deifinir funciones (arrow functions)
https://gist.github.com/gaearon/683e676101005de0add59e8bb345340c

## Introdución JSX
```javascript
const element = <h1>Hello, world</h1>;
```
- No es , ni HTML
- Es una extensión de sintaxis de JavaScript
### Why ?
- React acepta el hecho de que la lógica de renderizado está inherentemente
	ligada con la lógica de la interfaz de usuario
- No separa el marcado y la lógica
- Separa las preocupaciones con unidades acopladas llamadas **componentes**
### Incrustar expresiones en JSX
- Puede poner cualquier expresión de JavaScript válida dentro de las llaves
```javascript
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>; /* Expresiones */

ReactDOM.render(
  element,
  document.getElementById('root')
);
```
- JSX también es una expresión
- Después de la compilación, las expresiones JSX se convierten en llamadas de función
	JavaScript regulares
```javascript
function getGreeting(user) {
if (user) {
	return <h1>Hello, {formatName(user)}!</h1>;
}
	return <h1>Hello, Stranger.</h1>;
}
```
### Expecificación de atributos con JSX
Literales
```javascript
const element = <a href="https://www.reactjs.org"> link </a>;
```
Expresiones
```javascript
const element = <img src={user.avatarUrl}></img>;
```
**_Advertencia_**
React DOM usa camelCase -> la convención de nomenclatura de propiedades
en lugar de los nombres de atributos HTML
```javascript
/* Examples: Conversiones */
class -> className
tabindex -> tabIndex
```
### Specifying Children with JSX
```javaScript
const element = <img src={user.avatarUrl} />;
```
```javaScript
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```
### JSX previene los ataques de inyección
```javascript
const title = response.potentiallyMaliciousInput;
/* This is safe: */
const element = <h1>{title}</h1>;
```
- Todo se convierte en una cadena antes de ser renderizado.
- Ayuda a prevenir ataques XXS (cross-site-scripting)
### JSX representa objetos
Babel compila **JSX** hasta las **React.createElement()** llamadas
```javascript
/************************************/
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
/* Estos dos ejemplos son idénticos */
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
/************************************/
/* React.createElement crea un objeto como este(~) */
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!'
  }
};
```

## What is a Element?
```javascript
const element = <h1>Hello, world</h1>;
```
- Los elementos son los componentes básicos más pequeños de las aplicaciones React
- Un elemento describe lo que desea ver en la pantalla
- React Dom se encarga de actualizar el DOM para que coincida con los elementos React
### Rendering an Element into the DOM
- Los elementos son de lo que están 'hechos' los componentes
- Para representar un elemento React en un nodo DOM raíz, pase ambos a ReactDOM.render()
```javascript
const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```
### Updating the Rendered Element
- React elements are inmutable
- An element is like a single frame in a movie: it respresents the UI at certain point in time
- Only way to update the UI is to create a new element
```javascript
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(element, document.getElementById('root'));
}
- In practice, most React apps only call ReactDOM.render() once.

setInterval(tick, 1000);
```
### React Only Updates What’s Necessary
ReactDOM compara elementos y subelementos con el anterior, y aplica actualizaciones
necesarias para llevar el DOM al estado deseado
