# Components and Props
- Somo como funciones de JavaScript
- Aceptan entradas arbitrarias(props)
- Retornan elementos React que describen lo que debería aparecer en la pantalla

## Function and Class components
```javascript
/* Function components*/
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
/* Class components*/
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```
## Rendering a Component
Elementos React que representan etiquetas DOM
```javascript 
const element = <div />;
```
Elementos que representan componentes definidos por el usuario
```javascript
const element = <Welcome name="Sara" />;
```
React pasa atributos JSX e hijos a este componente como un solo objeto(props)
```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```
**_Nota: Siempre comience los nombres de los componentes con una letra mayúscula._**
## Composing Components
- Los componentes pueden hacer referencia a otros componentes en su salida
- Permite la abstracción de componentes para cualquier nivel de detalle
```javascript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```
## Extracting Components
**No tenga miedo de dividir los componentes en componentes más pequeños**
```javascript
/**
 * - Complicado de cambiar debido al anidamiento
 * - Dificil de reutilizar partes indivuales del mismo
 */
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```
```javascript
/**
 * - Avatar no necesita saber su contexto de uso
 * - Nombrar props desde el propio punto de vista del componente
 */
function Avatar(props) {
  return (
    <img className="Avatar"
      src={props.user.avatarUrl}
      alt={props.user.name}
    />
  );
}
```
```javascript
function UserInfo(props) {
  return (
    <div className="UserInfo">
      <Avatar user={props.user} />
      <div className="UserInfo-name">
        {props.user.name}
      </div>
    </div>
  );
}
```
**Simplify**
```javascript
function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={props.author} />
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```
- Si una parte de la UI se usa varias veces, se extrae
- Si es muy compleja por sí solo, se extrae

## Props are Read-Only
Nunca debe modificar sus propios props
### Funciones Puras
```javascript
function sum(a, b) {
  return a + b;
}
```
- No intentan cambiar sus entradas
- Siempre devuelven el mismo resultado para las mismas entradas
### Fuciones Impuras
```javascript
function withdraw(account, amount) {
  account.total -= amount;
}
```
- Cambia su propia entrada

### Regla Estricta
**Todos los componentes de React deben actuar como funciones puras con
respecto a sus props (propiedades).**
