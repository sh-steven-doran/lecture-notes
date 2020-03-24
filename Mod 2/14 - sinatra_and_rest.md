# Sinatra and MVC

### Learning Goals

* [ ] Recognize MVC pattern 
* [ ] Sinatra framework 

--------------------------

### Hook




### Lecture Flow

1. MVC Review

2. RESTful Routing Review
    * pull up Restular
    * connect verbs to CRUD and to Index, New, Show, Edit

3. Sinatra
  1. use Corneal to make a scaffold
  2. run application with shotgon
  3. walk through `application_controller.rb`
  4. demo routes 
        - show how changing the verb or route breaks things
  5. move to views
        - talk about ERB interpolation characters, difference between `<%= %>` and `<% %>`

> commit and push, get students to pull

  6. Think-Pair-Share, add a new routes other endpoints
  8. Add a model/database

  
```html
    <form action="/donuts" method="post">
        <label>Donut Name: </label><input type="text" name="name">
        <input type="submit">
    </form>
    
    <input type="hidden" name="_method" value="DELETE">
```

```ruby
# config.ru

#...

use Rack::MethodOverride

run ApplicationController
use CostumesController

#...
```