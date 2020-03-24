Mod 3

# ES6 Syntax

## Learning Goals

- [ ] Use spread operators to copy arrays and objects
- [ ] Use spread operators to created modified copies of arrays and objects
- [ ] Use destructuring and object property shorthand to simplify code
- [ ] Use keys on an object dynamically


## Hook

## Lecture Flow

### 1. Spread Operator `...`
 
* pass by reference issues when working with objects
* spread operator allows us to copy objects and create new ones
* avoid mutating state - everything should be new
    
```javascript
// with arrays
    
const array = [1,2,3,4]
const b = array.slice() // copies the array
const c = [...array] // copies the array
// array ≠ b ≠ c
    
const d = [...array, 5, 6] // creates a new array with added elements
const e = [8, 9, ...array] // prepends elements to a new copied array
const f = [...array, ...array] // doubles the array
const g = [...array, 'beef', ...array] // doubles the array, adds an element
    
// with objects
    
const obj = {thing: 'stuff', huh: 'blah'}
const obj2 = {...obj} // copies object, obj ≠ obj2
const obj3 = {...obj, occupation: 'speech writer'} // adds keys
const obj4 = {...obj, huh: 'barf'} // overwrites key
    
const obj5 = {name: 'Sindy', huh: 'garp'}
const obj6 = {...obj, ...obj5} // merges & overwrites
    
const obj7 = {name: 'Sindy', age: 45, car: {model: "Mustang", color: 'red'}}
const obj8 = {...obj7} // copy but preserves reference to nested object
// obj7.car === obj8.car
// => clone me, tell me to go home, same reference
```

### 2. Destructuring

```javascript

const obj = {name: 'Sindy', age: 45, car: {model: "Mustang", color: 'red'}}

// Old way
// const name = obj.name
// const car = obj.car

const { name, car } = obj

`
<div>
    <h1>Hi, my name is ${ name }. I drive a ${ car.color } ${ car.model }.</h1>
</div>
`

const {name, car: { model, color } } = obj // give us name, model, and color variables, but not car


function someFunction({ name, car }(
    console.log(`Hi, my name is ${ name }. I drive a ${ car.color } ${ car.model }.`
)

someFunction(obj) 
```

### 3. Restructuring

```javascript
const potato = 'friend'
const pumpkin = 'scary'
const lettuce = 'tasty'

const oldWay = { potato: potato, pumpkin: pumpkin, lettuce: lettuce }
const restructured = { potato, pumpkin, lettuce }
```