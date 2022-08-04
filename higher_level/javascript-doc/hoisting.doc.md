# Hoisting

Question0: ¿Funciona?
```javascript
console.log(a) // undefined
var a = 'hello'
```
Answer: Sí funciona, debido al hoisting.
*Details*
- En el proceso de compilación e identificación se buscan variables y funciones
- _Lexical Enviroment_ guarda variables y funciones en memoria


Question1: ¿Funciona?
```javascript
noSeSiFunciona()

function noSeSiFunciona () {
  console.log('Hello, funciona')
}
```
Answer: Sí funciona, debido al hoisting.
*Details*
- Como en el anterior ejemplo, _Lexical Enviroment_ guarda variables y funciones en memoria


Question2: ¿Funciona?
```javascript
noSeSiFunciona()

var noSeSiFunciona = function () {
  console.log('Hello, funciona')
}
```
Answer: No funciona, debido a que "Sí no es una declaración, no hay hoisting"

## Concepto
| Sí no es una decaración, no es hoisting y nos va a tirar un error.
*¿Qué podemos hostear?*
- CLASS
- FUNCTION
- CONST
- LET
- VAR

### Hositing de var (Se inicializa)
```javascript
console.log(a) // undefined
var a = 'hello'
```
*¿Cómo funciona esto?*
```javascript
// Son identificadas las variables y funciones
console.log(a)
// Se crea una referencia a las variables identificadas y son inicializadas en undefined
lexicalEnvironment = {
  a: undefined
}
// Pueden encontrarse nuevas asignaciones para una referencia durante la ejecución
var a = 2
// Es actualizada la referencia con el nuevo valor encontrado
lexicalEnvironment = {
  a: 2
}
```
### Hoisting de let/const (No se inicializan)
```javascript
console.log(a)
let a = 'hello'
// Reference Error: a is not defined
// or
// Cannont access 'a' before initialization
```
*¿Cómo funciona esto?*
```javascript
// Son identificadas las variables y funciones
// Temporal Dead Zone - start
console.log(a)
// No se inicializan las variables identificadas
lexicalEnvironment = {
  a: uninitialized
}
// En tiempo de ejecución son inicializada en undefined
// Temporal Dead Zone - end
lexicalEnvironment = {
  a: undefined
}
// Pueden encontrarse nuevas asignaciones para una referencia durante la ejecución
var a = 2
// Es actualizada la referencia con el nuevo valor encontrado
lexicalEnvironment = {
  a: 2
}
```
