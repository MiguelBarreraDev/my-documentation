# this
- Una propiedad de un contexto de ejecución
- Palabra clave
- Tiene diferencias entre el modo estricto y el modo no estricto
- En la mayoría de casos, el valor de **this** está determinado por cómo se llama
	a una función (enlace en tiempo de ejecución)
- ES5 introdujo el **bind()** método para establecer el valor de **this** independientmente
	de como se llame
- ES2015 introdujo las **arrow functions** que no tienen sus propios enlaces a **this** o **super()**
```javascript
/* Simple definition of an arrow function */
const function_name = (params) => {
	// instructions...
}
```

## Contexto Global
- Fuera de cualquier función
- **This** se refiere al objeto global
- In the browser, the **window** object is also the global object
```javascript
/**
 * Siempre puede obtener fácilmente el objeto global utlizando la
 * propiedad 'globalThis'
 *
 * In the browser:
 */
console.log(globalThis) // window
this === window // true
this.text = "tell me Daddy"
console.log(window.text) // "tell me Daddy"
```

## Contexto de Función
- Dentro de una función, el valor **this** depende de como se llame a la función
```javascript
/**
 * Example:
 * El código no está en modo estricto.
 * El valor de 'this' no está establecido por la llamada.
 * 
 * 'this' se establecerá de forma predeterminada en el objeto global
 */
function f1() {
	return this
}
// In a browser
f1() === window // true
```
- En modo estricto sino se establece el valor de **this** en un contexto de ejecución,
	permanece como undefined
- Para establecer **this** al llamar a una función, use **call()** o **apply**
```javascript
var obj = {a: 'Custom'}
var a = 'Global'

function whatsThis() {
	return this.a
}

/**
 * No se establece el valor de 'this'.
 * No está en modo estricto.
 * No usa let o const para definir variables
 * Hace referencia al objeto global(window) in browser
 *
 * @return 'Global'
 */
whatsThis()
/**
 * Se establece el valor de 'this' al llamar a las funciones
 *
 * @return 'Custom' 
 */
whatsThis.call(obj)
whatsThis.apply(obj)
```
- Los metodos **call()** y **apply()** aceptan más de un parametro
	- El primer parametro es el objeto que será usado para estbalecer el valor de **this**
	- El resto son usados como argumentos de la función
```javascript
function add(c, d) {
	return this.a + this.b + c + d
}

let o = {a: 1, b: 3}
// Todos menos el primero are used as the arguments
add.call(o, 5, 7) // 16
// Members of the array are used as the arguments
add.apply(o, [10, 20]) // 34
```
- En modo no estricto, si el valor pasado como 'this' a call o apply no es un objeto,
	se intentará convertirlo en un objeto
	- Valores null y undefined -> Objeto global
	- Primitivos -> Se convierten en objeto usando el constructor relacionado
## Contexto de Clase
- Dentro de un **constructor** de clase, **this** es un objeto regular
- Todos los métodos no estáticos de agregan al prototipo de this
- Los métodos estáticos son propiedades de la clase misma
```javascript
class Animal {
	constructor() {
		// Obteniendo el prototipo del objeto regular
		const proto = Object.getPrototypeOf(this)
		// Imprimiendo los nombres de las propiedades del prototipo
		console.log(Object.getOwnPropertyNames(proto))
	}
	toSleep() {}
	makeNoise() {}
	static getOwner() {}
}

new Animal() // ['constructor', 'toSleep', 'makeNoise']
```
### Clases derivadas
- Los contructores derivados no tienen **this** vinculación inicial
- La llamada **super()** crea un this enlace dentro del constructor
- Hacer referencia a **this** antes de llamar a **super()** generará un error
```javascript
class Base {
	constructor() {
		this.name = "Pepito"
	}
}
// Referencia a 'this' despues de llamar al método 'super()'
// :)
class DerivedClass1 extends Base()
{
	cosntructor() {
		super()
		this.lastname = "De ti"
		console.log(this)
	}
}
// Referencia a 'this' antes de llamar al método 'super()'
// :(
class DerivedClass2 extends Base()
{
	cosntructor() {
		this.lastname = "De ti"
		super()
		console.log(this)
	}
}

new DerivedClass1() // {name: 'Pepito', lastname: 'De ti'}
new DerivedClass2() // ReferenceError
```
- En general las clases derivadas no deben regresar antes de llamar a **super()**
- Pueden Regresar si devuelven un **Object** o no tienen constructor
```javascript
class Base {}
/* Derived classes */
class Good extends Base {}
class AlsoGood extends Base {
	constructor() {
		return {a: 5}
	}
}
class Bad extends Base {
	constructor() {}
}

new Good() // Permitido - No hay constructor
new AlsoGood() // Permitido - Retorna un objeto 
new Bad() // Error - Tiene constructor pero no llama antes a super() 
```
