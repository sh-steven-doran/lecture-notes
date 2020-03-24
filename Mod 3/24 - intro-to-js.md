# Intro to JavaScript

## Learning Goals

- [ ] Briefly explain the history of JS
- [ ] Understand the role of JS in web development
- [ ] Explain the relationship between HTML and JS
- [ ] Use script tags to load JS into an HTML page
- [ ] Explain the basic data types and data structures in JS
- [ ] Explain the difference between pass-by-value and pass-by-reference


--------------------------

## Hook

1. Welcome to Mod 3
2. JS - where it comes from and what it does
3. Why JS - what it provides us over something like Rails
4. Datatypes
5. Pass by reference vs pass by value

## Lecture Flow

### 1. Welcome to Mod 3

* more independence
    * don't run to instructors at the first sign of a problem
    * read the error, try to figure it out
    * utilize debugging skills - break points, console.logs
    * ask the internet
    * ask a classmate
    * if none of that works come to an instructor but be ready to explain the steps you've taken and why they didn't help
* take charge of your learning
    * I'm not going to hassle you to finish your labs but your success in the program will be directly correlated to the amount of labs you complete
    * be on time to lecture - you're grown ups, we won't be chasing you down but we will take note when you're late, it's a sign of immaturity and disrespect
    * I will do my best to adhere to the schedule as it is in the calendar and will also try to give you as much notice as possible when things have to change
    * if you come across something that is confusing, seek other resources to help you educate yourself about the topic before coming to an instructor - this is the job you've signed up for, there will rarely be anyone around to guide you through problems you're having
    * share resources with your classmates and your instructors - we're all still learning and lots of the best stuff I've found has come from students

### 2. History of JS

* don't want to spend a bunch of time reviewing history - look that up yourselves
    * focus on 'Just Enough JavaScript' - try to avoid rabbit holes
    * I don't know how engines work but I know how to drive
* JS engines interpret JS code (e.g., browsers)
    * All JavaScript engines implement a specification of the language provided by ECMAScript
    * different engines vary in their implementation of the standard and that's why you will see differences in performance and why one browser will support certain language features while others do not
* different versions of ES, important to understand legacy versions
    
### 3. Why JS

* JS has fewer conventions than ruby
    * less opinionated, there are fewer "right" ways to solve problems
    * labs might use different conventions based on who wrote them
* JavaScript gives us 3 primary abilities:
    1. The ability to make requests
    2. The ability to control what the user sees on the page (DOM)
    3. The ability to capture user 
* Request-Response Cycle
    * compare Rails page loading vs JS SPA apps, ajax etc - doesn't require a full page reload
        * efficiency
        * flexibility 
        * only sends request when we need info from our server - doesn't get the same info over and over and over
    * Coffee Dad twitter - if it were a straight up Rails app how would we get more tweets as we scroll down?
        * how does it appear to be working?
  
    
### 4. JavaScript Data Types Overview

There are seven data types in JavaScript:

  1. Symbol
    - new primitive, unique identifier
    - we won't use them
  2. Undefined
    - create `var coffee` in console, compare with Ruby
    - like a word in a book I don't know the definition of
    - the thing exists, it just hasn't been defined yet
    - error if I just type the name `coffee` without declaring it
  3. Null
    - purposely making it empty
  4. Boolean
    - do falsey checks on different data types
  5. Number
    - no real difference between floats and integers
    - NaN - `8 * 'some string'`, `NaN === NaN //false`
    - 0
  6. String
    - interpolation
    - ""
  7. Object  
    - hashes, arrays, function - all objects
    - collection of data
    - can retain behavior
    - can be assigned properties
    - Object vs. object literals
    - functions
        - functions are objects that can be executed
        - definition vs invocation (`renderTweet` vs. `renderTweet()`
        - functions always return undefined unless explicitly returning otherwise
        - experssion vs. declaration (`function renderTweet(){...}` vs `let renderTweet = function(){...}`)
        - anonymous functions (`function(){...}`)
    - pass by reference vs pass by value 


    
### 5. Pass by Value vs Pass by Reference

* primitives are pass by value
    * this is like photocopying a piece of paper and passing copies around
    * if one person writes something on their paper it doesn't change the version everyone else has

```javascript
var number = 1

var copyOfNumber = number

copyOfNumber = 2

copyOfNumber // 2
number // 1
```
    
* non-primitives are pass by reference  
    * like giving an address, providing a reference
    * not copying the whole campus and passing copies out
    * if everyone gets the address they each have a reference to a thing - if the thing changes it changes for everyone
    * some methods will produce new copies of objects - `slice` etc.
    * `Array.from(array)` will create a brand new object
    * `Object.assign`
    * `[...array]`

```javascript
var array = [1,2,3]

var copyOfArray = array

copyOfArray.push(9)

copyOfArray // [1,2,3,9]
array // [1,2,3,9]
```