# Intro to the Dom
 
## Learning Goals

- [ ] Draw DOM tree by looking at HTML
- [ ] Explain what a DOM node is and what its most important attributes are
- [ ] Use the Chrome Dev tools to explore the DOM tree and its attributes
- [ ] Use JS to select DOM nodes
- [ ] Use JS to add, remove, and edit DOM nodes

## Hook

* introduce DOM
* diagram DOM
* DOM CRUD actions

## Lecture Flow

### 1. DOM
* DOM Tree - representation of the HTML document as a tree
    * show DOM in console
    * JavaScript allows us to traverse and manipulate the DOM
    * nodes - parent, children, siblings
* diagramming the DOM Tree
    * find example online
    * diagramming group exercise

### 2. DOM CRUD

* the node you call these methods on determines the scope of the query
* introduce `#` and `.` syntax

#### READ:
- get `#image-container` from the page and change its background color
- save DOM element to variable - `console.dir(var)`, it's an object
- demo each of the following: 
    - `node.getElementById`
    - `node.getElementsByTagName`
    - `node.getElementsByClassName`
    - `node.querySelector`
    - `node.querySelectorAll`

* **5 min to write down what each of the read methods will return**

-- 
- `node.getElementById`
  - an element that is a child of the chosen `node` that has the id given as an argument
- `node.getElementsByTagName`
  - all elements that are children of the chosen `node` who's `tagName` matches the argument
- `node.getElementsByClassName`
  - all elements that are children of the chosen `node` who's `className` matches the argument
- `node.querySelector`
  - the first element that is a child of the chosen `node` that matches the argument
- `node.querySelectorAll`
  - the all elements that are children of the chosen `node` that matches the argument
  - We can also combine selectors for more specificity:
    - We need a space between `#parent .child`
    - We can chain selectors `div.image.highlighted`
    - We can search for siblings with `~`
     
---

#### DELETE:

* get the `ul` child node of image container
* save it to variable
* remove it
* then add it back to the div
* remove `ul` with `remove()`


--
- `node.removeChild(childNode)`
  - remove the child passed into the argument from the `node` that the method is being called on 
- `node.remove()`

---

#### UDATE:

* replace movie image with something else
* how to get image?
* `image.src = "image.url"`

--
- We can change/add any attribute of a `node`. Example: `body.style.backgroundColor = red`
  - this will either update the `style.backgroudColor` if one already exists, or add a `style.backgroundColor` if one does not exist
- `innerText`/`textContent`
- `innerHTML`
    
---

#### CREATE:
  
* add a whole new movie to DOM
* `innerText` vs `innerHTML` - the former just puts a string, the latter recognizes the string as HTML and treats it as such
* 

```javascript
let ul = document.getElementsByTagName("ul")[0]
function appendLi() {
    let li = document.createElement("li")
    let h3 = document.createElement("h3")
    h3.innerText = "The Goonies"


    li.innerHTML = `
    <h3>The Goonies</h3>
                    <img alt=""
                        src="https://images-na.ssl-images-amazon.com/images/I/515DYf99zfL.jpg" />
                    <h4>Year: </h4>
                    <p>1985</p>
                    <h4>Score: <span>0</span> </h4>
                    <button>Up Vote</button>
                    <button>Down Vote</button>
    `
    li.className = "movie"

    return li
}
ul.append(appendLi())
```
  
--
- `document.createElement`
- `document.body.appendChild(element)`

---