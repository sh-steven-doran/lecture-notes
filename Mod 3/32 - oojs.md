
# OOJS

## Learning Goals

- [ ] describe the difference betwee `__proto__` and `prototype`
- [ ] create a JavaScript class to wrap properties and functions
- [ ] create instance and class methods using `static`

## Lecture Hook

* use classes to create code that is modular and resusable
* encapsulate related logic

## Lecture Flow

### 1. Demonstrate Object Creation in JS

* creating objects repeatedly is inefficient

```javascript
let jaws = {
    title: 'Jaws', 
    year: 1975,
    imageUrl: 'jawsposter.com',
    prettyPrint: function(){
        return `${this.title} - ${this.year}`
    },  
    score: 8
}

let matrix = {
    title: 'The Matrix',
    year: 1999,
    imageUrl: "matrixposter.com",
    prettyPrint: function() {
        return `${this.title} - ${this.year}`
    },
    score: 3
}

// inefficient, not DRY, prone to error, not easy to replicate    
``` 

* in Ruby - making an object allows us to easily duplicate behavior and attributes

```ruby
class Movie
    attr_accessor :title, :year, :image_url, :score
    
    def initialize(title, year, image_url, score)
        @title = title
        @year = year
        @image_url = image_url
        @score = score
    end
    
    def pretty_print
        "#{@title} - #{@year}"
    end
end

matrix = Movie.new('The Matrix', 1999, "matrixposter.com", 9)
matrix.score # 9
matrix.pretty_print # "The Matrix - 1999"
```

> Classes are in fact "special functions", and just as you can define function expressions and function declarations, the class syntax has two components: class expressions and class declarations.

* `class` is mostly syntactic sugar around regular JS code - it makes JS look more like a traditional OO language like Ruby
* `class` is a keyword that acts as a special function - can do class declarations and expressions
* `constructor` function is parallel to `initialize` in Ruby
* `static` functions are like class methods
* regular functions are like instance methods

```javascript
// lots of syntactical sugar

class Movie {
    constructor(title, year, imageUrl, score){
        this.title = title
        this.year = year
        this.imageUrl = imageUrl
        this.score = score
    }
    
    prettyPrint() {
        return `${this.title} - ${this.year}`
    }
}

let matrix = new Movie("The Matrix", 1999, "matrixposter.com", 9)
matrix.score // 9
matrix.prettyPrint // "The Matrix - 1999"

```

* turn movie into its own class in application
* to make a "class" method in JS use `static`



### 2. Prototypical Inheritance

* in Ruby we can call `#class` to see something's "blue print" and `.ancestors` to get a sense of its inheritance chain

```ruby
class Animal
end

class Mammal < Animal
end

class Dog < Mammal
end

Dog.ancestors

# [Dog,
#  Mammal,
#  Animal,
#  Object,
#  JSON::Ext::Generator::GeneratorMethods::Object,
#  PP::ObjectMixin,
#  Kernel,
#  BasicObject]
```

* JS `__proto__` vs `prototype`
    * prototype is the blueprint, the "class"
    * proto is an object that pulls in all the functions and properties that every instance of the class should have
    * instance gets `__proto__`, class has `prototype`
    * `prototype` is the blueprint the class provides to all instances to pass own properties and metbods

```javascript
matrix.__proto__ === Movie.prototype

// true
```

### 3. Refactoring

* create Movie class

```javascript
// Movie.js

class Movie {
  constructor(obj){
    this.id = obj.id
    this.title = obj.title
    this.year = obj.year
    this.imageUrl = obj.imageUrl
    this.score = obj.score
  }
  
  prettyPrint() {
    return `${this.title} - ${this.year}`
  }

  createLi() {
    let li = document.createElement('li')
    // console.log('rendering movie', movie.title)
  
    li.innerHTML = `
      <h3>${this.title}</h3>
      <img alt="" src="${this.imageUrl}" />
      <h4>Year: </h4>
      <p>${this.year}</p>
      <h4>Score: <span>${this.score}</span> </h4>
      <button class="up-vote">Up Vote</button>
      <button data-purpose='down'>Down Vote</button>
      <button data-purpose="delete">&times;</button>
    `
  
    li.className = 'movie'
    li.dataset.beef = 'stuff'
    return li
  }

  render(el) {
    let li = this.createLi()
    el.append(li)
  }
}
```

* create an Adapter class to abstract out API connection

```javascript
// Adapter.js

class Adapter {
  static baseUrl = "http://localhost:3000/api/v1/movies"

  static getMovies() {
    return fetch(this.baseUrl).then(response => response.json())
  }

  static addMovie(obj) {
    let options = {
      method: "POST", 
      headers: {
        "content-type": "application/json",
        accept: "application/json"
      },
      body: JSON.stringify(obj)
    }

    return fetch(this.baseUrl, options).then(response => response.json())
  }
}

// how to save likes and delete candy using adapter?

```

