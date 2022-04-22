# State and Lifecycle
- **Código a perfeccionar**
```javascript
function Clock(props) {
  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {props.date.toLocaleTimeString()}.</h2>
    </div>
  );
}

function tick() {
  ReactDOM.render(
    <Clock date={new Date()} />,
    document.getElementById('root')
  );
}
/* ReactDOM.render() es llamado en cada intervalo*/
setInterval(tick, 1000);
```
## Iniciamos
- Estos conceptos nos permitirán renderizar componentes sin la necesidad de
llamar a ReactDOM.render() cada vez
- Permitirán que los componentes sean realmente reutlizables y encapsulados

## State
- Similar a props, pero es privado y está completamente controlado por el
  componente
- **Convert to class componente**
```javascript
/**
 * Clase ES6 que hereda de React.Component
 * render: método heredado
 * this: Hace referencia al componente (Clock)
 */
class Clock extends React.Component {
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
/**
 * Se llamará al método render cada vez que haya una actualización
 */
```
## Adding local state
- Agregar un constructor de clase que asigne el estado inicial
- Los componentes de clase siempre deben llamar al constructor base con props

## Adición de métodos de ciclo de vida
En aplicaciones con muchos componentes, es muy importante liberar recursos
tomados por los componentes cuando se destruyen (Dejar de ser parte del arbol de nodos)
- **Montaje (método)**
Cuando se renderiza un componente por primera vez en el DOM
- **Desmontar (método)**
Cuando se elimina un componente del DOM

### Resultado
- Agregamos un método tick() que será llamada cada segundo y actualizará el estado
```javascript
class Clock extends React.Component {
  /**
   * Método contructor
   * Los componentes de clase siempre deben llamar al constructor base con props
   * Lugar donde se inicializan estados del componente
   */
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
  /**
   * Método integrado de montaje
   * Se ejecuta cuando se renderiza por primera vez el componente
   */
  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }
  /**
   * Método integrado de desmontaje
   * Se ejecuta cuando se remueve el componente del arbol de nodos del DOM
   */
  componentWillUnmount() {
    clearInterval(this.timerID);
  }
  /**
   * Actualiza el estado del componente
   * Usa this.State (método heredado) para actualizar
   */
  tick() {
    this.setState({
      date: new Date()
    });
  }
  /**
   * Renderiza el componente en el DOM
   */
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);
```
