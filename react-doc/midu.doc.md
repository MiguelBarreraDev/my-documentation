# REACT - Una biblioteca de javascript para contruir UI's
- Declarativa: No imperativa, ejemplo de comprar sushi
- Basada en componentes: Reutilizar código
- Una de las bibliotecas más usadas(npm)

## Use React - dependencias
- react -> totalmente agnóstica al uso, es el core de la aplicación
- react-dom -> Posee el código para que react funcione en el navegador

## Conceptos
- jsx -> Parecido a html pero es javascript
- Props -> Propiedades que posee nuestros componentes
- Fragment -> Renderizar multiples elementos secundarios sin agregar nodos adicionales
```javascript
return (
	<React.Fragment> /* No se agrega en el DOM */
		<button>Incrementar</button> /* elemento secundario */
		<button>Decrementar</button> /* elemento secundario */
	</React.Fragment>
)
```
## Hooks
Permite dotar de cierta funcionalidad a los componentes
### useState
Cada que se modifica el estado se renderiza el componente
```javascript
/* Use states in React */
import {useState} from 'react'
const [state, function] = useState(State_initial)
```
### useEffect
Permite ejecutar una función cada vez que se renderice nuestro componente
```javascript

import {useEffect} from 'react'
/**
 * useEffect(function, dependencias)
 * firstParameter: Lo que se ejecuta cuando se renderiza el componente
 * secondParameter: información que si cambia, se ejecuta el efecto
 */
useEffect(function () {
	console.log('efecto ejecutado')
}, [])
/* Su mal uso puede causar bucles infinitos */
```
## Routes
### wuoter
Install with npm
```javascript
/**
 * npm: Administrador de paquetes
 * - Instala las dependencias secuencialmente
 */
npm install wuoter
```
Install with yarn
```javascript
/**  
 * yarn: Administrador de paquetes de facebook
 * - Instala las dependencias en paralelo
 */
yarn add wuoter
```
Import to the project
```javascript
import { Link, Route } from 'wuoter'

export default function App() {
	return (
		<>
			<Link to='/gif/colombia'></Link>
			<Link to='/gif/ecuador'></Link>
			<a src='/gif/peru'></a>
			<Route
				component={listOfGifs}
				path="/gif/:keyword"
			/>
		</>
	)
}
/*
A la hora de declarar rutas
<a></a>
- Renderiza toda la pagina
<Link></Link>
- Renderiza solo el componente
- Hace enlaces que utilicen el history del navegador sin refersacr al página
*/
```
