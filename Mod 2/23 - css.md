# CSS

### Learning Goals

* [ ] Discuss what CSS does and why it's important
* [ ] Cover the basics of HTML
* [ ] Differentiate between inline, internal, and external stylesheets
* [ ] Demonstrate the anatomy of a declaration block
* [ ] Understand how to use class, id, and element selectors, and selector order of importance
* [ ] Demonstrate the use of the box model, positioning, flex box, CSS grid in page layout
* [ ] Introduce CSS Frameworks like Bootstrap, Semantic UI, Materialize


--------------------------



### Lecture Flow

1. What is CSS? Why does it cascade?
2. Inline, internal, and external stylesheets
3. Selector specificity
4. Box model
    * give something a background color then play around with margin, padding, and border
5. Positioning
    * relative, absolute, fixed
    * default is static
    * difference between block and inline elements
    * Relative
        * moves an element from its default position
        * can set `top` and `bottom` attributes 
        * will move it relative to where it should be in the normal flow of the document
    * Absolute
        * can set `top` and `bottom` 
        * will remove from normal document flow and position it with respect to the document
    * Fixed
        * similar to absolute, but relative to window so will stay in the same place during scroll  
6. Text
7. CDNs


### Code

#### Stylsheets and Selectors

```html
Inline styles:
<h1 style="color: PaleVioletRed">

Internal Stylesheets:
<style>
 div {
   background: lavendar;
 }
</style>

External Stylesheets:
<link rel="stylesheet" href="styles.css">
```

```css
//Element Selectors:
body {
    text-align: center;
}

//Class Selectors:
.header {
    height: 400px;
    background-image: url("./images/header_img.jpg");
    background-size: cover;
}

//ID Selectors:
#page-title {
    color: white;
    font-size: 150px;
    font-family: sans-serif;
}

//Chaining/Multiple selectors:
button {
    font-size: 20px;
    padding: 10px;
}

button a {
    text-decoration: none;
}
```
#### The Box Model
```css
  .intro {
     padding: 30px;
     border: 4px solid black;
     margin: 50px;
   }
```

#### Layouts - Floats & Clear
```css
   .article-body {
      width: 300px;
      float: left;
   }

   .grand-canyon-image {
      float: left;
   }

   .park-info {
      clear: both;
   }
```