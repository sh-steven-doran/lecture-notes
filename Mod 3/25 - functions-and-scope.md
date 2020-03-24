# Functions and Scope

## Learning Goals

* [ ] Explain variable scoping in JS
* [ ] Explain difference between `var`, `let`, and `const`, and explain hoisting
* [ ] Distinguish between a function and its invocation
* [ ] Write functions in the correct syntax
* [ ] Explain the differences and similarities between methods in Ruby and functions in JS
* [ ] Explain what it means for functions to be first-class citizens


--------------------------

## Hook

1. how to get JS into your HTML
2. how scope works in JS - global, function, block, lexical scoping
3. how hoisting works
4. variables - difference between `let`, `var`, and `const`
5. first class functions

### 1. How to do JS

* `<script>` tag directly in html, linked js file `<script src="...">` 

### 2. Lexical Scoping

> Lexical Scope means that in a nested group of functions, the inner functions have access to the variables and other resources of their parent scope. This means that the child functions are lexically bound to the execution context of their parents. Lexical scope is sometimes also referred to as Static Scope.

* demo variable scoping in Ruby:

```ruby
def some_method
    puts "#{some_variable}"
end

some_method # error
```
* how to get this to work?
    * declare variable within method 
    * pass it  in
* scope in Ruby is determine by the *type* of variable

* in JS:

```javascript
function someMethod(){
    console.log(someVariable)
}

someMethod() // error
```
> * Nested functions have access to variables declared in their outer scope. 
> * scope in JavaScript is determined by *where* variables are defined in our code. There can also be a variety of scopes in our code, ranging from very local to global

* how to get this to work?
    * declare variable within function
    * move variable outside of function in both Ruby and JS
    * demonstrate global, function, and block scoping in JS (maybe compare it to Ruby?)

### 3. Type of Scope

1. Global
    *  a variable declared in the global scope; outside a function, outside a block, outside an object. These variables are globally accessible meaning they can be read anywhere in your code.

```javascript
var name = 'my global name'
``` 

2. Function
    * variables are confined to the functions in which they were declared. These variables are not accessible in the global scope. They can only be accessed within the function or any scope that is 'lower' on the scope chain, or more local (more on that later)

```javascript
function fnScope(){
  let name = 'a local name'
}

name  // =>  error
```    


3. Block
    * much like a function, variables defined within a block are only accessible within that block or in more local scopes

```javascript
if (true){
  let name = 'a block variable'
}

name // => error
```

### 4. Hoisting

> While JavaScript is being compiled, functions declared with the function keyword and variables declared with the var keyword are "hoisted" to the top of whatever scope they are in. Declarations are not phyisically moved to the top of whatever scope they're in. Instead, they are processed first (allocated memory) then assigned a value.

```ruby
puts not_hoisted # attempt to invoke the variable before it is declared

not_hoisted = "Ruby does not hoist anything!"

# => undefined local variable or method `not_hoisted` for main:Object (NameError)
```
*  variables declared with the var keyword are "hoisted" to the top of whatever scope they are in
*  their declaration gets hoisted but their definition does not - so the engine knows there's a variable named dog but has no idea what that variable's value is

```javascript
console.log(dog)

var dog = 'penny' // undefined
```

```javascript
var dog; //declare dog but do not assign it (value will be undefined)

console.log(dog) // undefined

dog = 'penny' //assign a value to dog
```

```javascript
num = 6
console.log(num) // 6
var num
```

```javascript
console.log(dog)

let dog = 'penny' // ReferenceError
```

* functions declared with the function keyword are also hoisted

```javascript
bark() // 'woof'

function bark() {
  console.log('woof')
}
```

```javascript
bark() // ReferenceError

let bark = function() {
  console.log('woof')
} 
```
 
* The engine doesn't actually move your variables. The variable and function declarations are put into memory during the compile phase, but stay exactly where you typed them in your code.

### 4. Var, Let, and Const

* variables can be declared without any of these keywords, they become global and this is a very very bad idea
* `var` is the older way of declaring variables
    * is hoisted
    * allows v and redefinition
    * not as strict with regard to block scope
* `let` is newer
    * is not hoisted
    * allows reassignment but not redeclaration
* `const` also newer
    * is not hoisted
    * does not allow reassignment or redeclaration
    * objects declared with `const` are not immutable, properties can be added
* never use `var`, use `const` unless you plan to reassign, most people generally use `let`

### 5. First Class Functions

* In JS functions are first class objecs:
    * functions can have properties
    * functions can be passed as argument to other functions
    * functions can be returned by another function
    * functions can be assigned to a variable
* Not so much in Ruby
    * demonstrate how you can't assign a method to a variable in Ruby, just its return
    
```ruby
def some_method
    "I am a method"
end

some_variable = some_method

some_variable # "I am a method"

# the return of the method is stored in the hash
some_hash = { method: some_method }

some_hash[:method] # "I am a method"
```


* Assigning functions to variables in JS

```javascript
function multiplier(num1, num2){
    return num1 * num2
}

let someVar = multiplier

someVar // ƒ ...

someVar(2, 2) // 4

let someObj = { func: multiplier }

// the function is now just a property of the object
someObj.func // ƒ...

someObj.func(2, 2) // 4
```

* Callbacks - function that can be passed into other functions

```javascript
function double(x){
    console.log(x * 2)
    return x * 2
}

let array = [1,2,3,4,5]

array.forEach(function(n){
    double(n)
})

array.forEach(double)
```

* functions that return functions (higher order functions)

```javascript
function multiplier(x){
    return function(y){
        return x * y
    }
}

multiplier(2)(5) // 10
```

* closures
    * "a closure is when a function is able to remember and access its lexical scope even when that function is executing outside its lexical scope."

```javascript
function multiplier(x){
    return function(y){
        return x * y
    }
}

let doubler = multiplier(2)

doubler // ƒ...

doubler(5) // 10 => how does doubler remember that 2 was passed into multiplier?

let tripler = multiplier(3)

tripler(5) // 15
```

--

```javascript
function closure() {
  var cheese = 'cheddar'

  return function() {
    return `I like to eat ${cheese}`
  }
}

closure() //function

closure()() // "I like to eat cheddar"

console.log(cheese) //Uncaught ReferenceError: cheese is not defined
```

