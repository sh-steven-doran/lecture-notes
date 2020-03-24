# Fetch and Async
 
## Learning Goals

- [ ] Implement Fetch functionality against an external datasource
- [ ] Set up an API backend using `json-server`
- [ ] Describe how to interact with an external datasource using RESTful conventions
- [ ] Understand asynchronous behavior in JavaScript
- [ ] Utilize Fetch and Promises to implement async API calls

## Hook


## Lecture Flow

### 1. Async

```javascript
function iAmSync(){
    for (i = 0; i < 10000000; i++) {
        let d = new Date()
    }
    console.log('done!')
}
```

```javascript
function iAmAsync(){
    setTimeout(function(){
    console.log('inside timeout')
    
}, 10000)
    console.log('outside timeout')
}
```

### 2. JSON Server

* `npm install -g json-server`
* `json-server --watch db.json`


```javascript
// json-server.json

{
    "port": 4000
}
```

```javascript
// db.json

{
  "movies":  [
    {
      "title": "Jaws",
      "imageUrl": "https://resizing.flixster.com/h8e7W7cVaQhuLdSvABDkJk6r5sc=/206x305/v1.bTsxMTE2NjE5OTtqOzE4MzU0OzEyMDA7ODAwOzEyMDA",
      "year": 1975,
      "score": 0
    },
    ...
  ]
}
```

### 3. Fetch

* `json-server -w test.json`
* `fetch("http://localhost:4000/posts")` - returns a promise

```javascript
fetch("http://localhost:4000/posts").then(function(response){ return response.json() })
```

```javascript
fetch("http://localhost:4000/posts")
.then(function(response){ return response.json() })
```

```javascript
fetch("http://localhost:4000/posts")
.then(function(response){ return response.json() })
.then(function(data){ console.log(data) })
```

* example with Pokemon API - [https://pokeapi.co/docs/](https://pokeapi.co/docs/)

```javascript
fetch("https://pokeapi.co/api/v2/berry/1/")
.then(response => response.json())
.then(console.log)
```

* **Think-Pair-Share** - write the code needed to make a request against our API to get a list of movies

```javascript
fetch("http://localhost:4000/movies")
.then(function(response){ return response.json() })
.then(function(data){ console.log(data) })
```

* change app code to get data from API

```javascript
function getMovies() {
  fetch("http://localhost:4000/movies")
  .then(function(response){ return response.json() })
  .then(function(movies){ 
    console.log(movies)
    movies.forEach(function(movie){
      let li = createLi(movie)
      ul.append(li)
    })
  })
}
```

* create a new movie using API

```javascript

function createMovie(movie) {
  fetch("http://localhost:4000/movies", {
    method: "POST",
    headers: {
      "content-type": "application/json",
      accepts: "application/json"
    },
    body: JSON.stringify(movie)
  })
  .then(function(response) { return response.json() })
  .then(function(movie){
    let li = createLi(movie)
    ul.append(li)
  })
}
```