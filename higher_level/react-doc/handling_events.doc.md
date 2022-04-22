# Handling Events
- Los eventos de reacción se nombran usando camelCase
- Con JSX, se pasa una función como controlador de enventos
```javascript
<button onClick={activateLasers}>
  Activate Lasers
</button>
```
- Debes llamar explicitamente a **preventDefault** para evitar el comportamiento
  predeterminado
```javascript
function Form() {
  /**
   * @param () e - Evento sintético 
   */
  function handleSubmit(e) {
    e.preventDefault();
    console.log("You clicked submit.")
  }

  return (
    <form onSubmit={habdleSubmit}>
      <button type="submit">Submit</button>
    </form>
  )
}
```
- En class components comunmente un controlador de eventos es un método
- En javascript los métodos de clase no están vinculados de forma predeterminada
```javascript
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    /* This binding is necessary to make `this` work in the callback */
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(prevState => ({
      isToggleOn: !prevState.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}
```
