# Intro to Events
 
## Learning Goals

- [ ] Use events to allow user interaction with the page
- [ ] Identify important attributes on the event object and their uses
- [ ] Identify commonly used events
- [ ] Synthesize knowledge of DOM manipulation and events to allow user interaction to change DOM
- [ ] *Bonus* Explain event propagation and identify how this can be used

## Hook


## Lecture Flow

1. talk about events
    * what is an event, event types
    * What we're concerned about
        1. what node an event happened to
        2. what type of event occurred
        3. what code should be execute
2. impelemnt a generic event on some image
    * talk about callbacks
    * explore the event object 
        * `node.addEventListener(event){ console.log('clicking', event) }`
    * Think-Pair-Share
        * write the code that on click will change the image of that image
3. add the ability to increase votes
    * Think-Pair-Share
        * write the logic to increase the score of the first button
4. add the listener to all the up vote buttons
    * add class to buttons
5. final challenge
    * iterate through array of movies, add them to the DOM, make sure they up vote buttons work

--
        
```javascript
upVoteButton.addEventListener("click", function(e){
    let parentLi = e.target.pardentNode
    let span = parentLi.querySelector('span')
    span.innerText = parseInt(span.innerText) + 1
})
```
---
```javascript
let buttons = document.querySelectorAll('.up-vote')
let buttonsArray = Array.from(buttons)

buttonsArray.forEach(function(button) {
    button.addEventListener("click", function(e){
        let parentLi = e.target.pardentNode
        let span = parentLi.querySelector('span')
        span.innerText = parseInt(span.innerText) + 1
    })
})
```
---
```javascript
function createLi(movie) {
  let li = document.createElement('li')

  li.innerHTML = `
    <h3>${movie.title}</h3>
    <img alt=""
        src="${movie.imageUrl}g" />
    <h4>Year: </h4>
    <p>${movie.year}5</p>
    <h4>Score: <span>0</span> </h4>
    <button>Up Vote</button>
    <button>Down Vote</button>
  `

  li.className = 'movie'

  return li
}

movies.forEach(function(movie){
  let li = createLi(movie)
  ul.append(li)
})
```
