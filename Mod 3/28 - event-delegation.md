# Event Delegation
 
## Learning Goals

- [ ] Describe event bubbling/propogation
- [ ] Implement event delegation on a parent node
- [ ] Use control flow to differentiate behavior on the same event listener
- [ ] Understand why event delegation is effective
- [ ] Add datasets to elements 
- [ ] Access HTML elements using datasets

## Hook

* delegation is more efficient
* allows a single listener cover a number of nodes
* forms in js

## Lecture Flow

* fix bug from yesterday's lecture
* talk about `preventDefault`
* finish adding movies to project *with* listeners
    * add 0 score to movies object 
* remove movies from HTML

--
### Event Propogation

* add listener to ul for clicks on different nodes
* talk about datasets
    * `data-purpose="upVote"` 
    * `node.dataset.datasetName = 'some string'`
    * access using `console.dir(element)` 
* What are some benefits to event delegation over individual listeners?

```javascript
ul.addEventListener("click", function (e) {
    if (e.target.dataset.purpose === "upVote") {
        let parentLi = e.target.parentNode
        let span = parentLi.querySelector("span")
        span.innerText = parseInt(span.innerText) + 1
    } else if (e.target.innerText === "X") {
        let parentLi = e.target.parentNode
        parentLi.remove()
    }
})
```

* Think-Pair-Share
    * implement delete button - `&times;`

### Activity

* mini project
    *  Add a "Add Movie" button underneath the `h1` that displays a form for adding a new movie (i.e., title, imageUrl, and year)
*  On form submit, the form should disappear and the button should be there again
    *  use documentation to find methods to do what you need
    * `insertAdjacentElement`
    *  `replaceChild`
    *  accessing form elements
        * `console.dir(formThing)`
        * inputs are 0-indexed `e.target[0].value`
        * if provide a `name` attribute, inputs can be accessed using dot-notation - `e.target.title.value`
    
```javascript
let formButton = document.createElement("button")
formButton.innerText = "Add Movie"
let welcome = document.querySelector("img")
welcome.insertAdjacentElement("afterend", formButton)

formButton.addEventListener("click", function () {
    let newForm = document.createElement("form")
    newForm.innerHTML = `
        <input type="text" name="title"/>
        <input type="text" name="year"/>
        <input type="text" name="imageUrl"/>
        <input type="submit" value="submit" />
    `
    
    document.body.replaceChild(newForm, formButton)

    newForm.addEventListener("submit", function (e) {
        e.preventDefault()
        let title = e.target.title.value
        let year = e.target.year.value
        let image = e.target.imageUrl.value

        let newMovie = { title: title, year: year, imageUrl: imageUrl, score: 0 }

        ul.append(appendLi(newMovie))
        
        newForm.reset()

        document.body.replaceChild(formButton, newForm)
    })
})
```
--
```html
< form >
    <label>Movie Name:</label> <input type="text" placeholder="movie title"/>
    <input type="text" />
    <input type="number" />
    <input type="submit" value="submit" />
</form >
```