# REACT - Una biblioteca de JavaAcript para contruir UI's
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
#### Import to the project
**Link & Route - Componenets**
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
- Hace enlaces que utilicen el historial del navegador sin refrescar la página
*/
```
**useLocation - Custom Hook**
```javascript
import {useLocation} from 'wuoter'
/* useLocation retorna -> ['/', f] */
/* function: f (to, replace) - Para navegar de forma programática, sin links */
export default function Home() {
const [path, pushLocation] = useLocation()
	/**
	 * handleSubmit. Atrapa un evento submit
	 * pushLocation. navega a una ruta específica cuando se de el evento submit
	 */
	const handleSubmit = evt => {
		evt.preventDefault()
		// navegar a otra ruta
		pushLocation(`/search/${keyword}`)
	}
}
```

## Custom Hook
- Los Hooks simplifican nuestros componentes
- Los Hooks nos permiten crear nuestros propios Hooks
- Extracción de lógica para ser utilizada en múltiples componentes
```javascript
/*------- Custom hook ---------*/
/* Hooks integrados */
import {useEffect, useState} from 'react'
/* Función que realiza una petición a un API para traerse los gifs */
import getGifs from '../services/getGifs'
/**
 * useGifs (Custom Hook) - Obtener una arreglo de gifs en base a una keyword
 * Se utiliza destructuración en los parámetros, para usar párametros nombrados
 * @return (object) - Contain a state and a arreglo de gifs
 */
export default function useGifs ({keyword} = {keyword: null}) {
	const [loading, set Loading] = useState(false)
	const [gifs, setGifs] = useState([])

	const keywordtoUse = keyword || localStorage.getItem("lastKeyword") || "random"

	useEffect(function () {
		setLoading(true)
		getGifs({keyword}) /* async */
			.then(gifs => {
				setGifs(gifs)
				setLoading(false)
				if (keyword) localStorage.setItem('lastKeyword', keyword)
			})
	}, [keyword])

	return {loading, gifs}
}
```

## Context
Es un objeto mágico que puede ser utilizado desde cualquier componente
```javascript
import React from 'react'

const Context = React.createContext(
	/* Objeto inicial que se provee en caso de que no se defina un proveedor */
	{
		name: 'Esto es sin provider',
		suscribeteAlCanal: true
	}
)

export default Context
```
### Proveedor
Delimita el rango donde puede ser utilizado el objeto proveido
```javascript
/* Proveer un value */
	return (
		<StatictContext.Provider value={
			{
				name: 'Esto es con provider',
				suscribeteAlCanal: true
			}
		}>
			<!-- Inicia rango -->
			<section>
			.  
			.
			.
			</section>
			<!-- termina rango -->
		</StatictContext.Provider> 
	)
```
### Consumidor
Define desde donde se utliza el objeto mágico
```javascript
/* Consumiento del contexto */
import React , {useContext} from 'react'
import StatictContext from '../../context/StatictContext'

export default function Detail({params}) {
	const context = useContext(StaticContext)
	return <h1>Gif con id {params.id}</h1>
}
```
