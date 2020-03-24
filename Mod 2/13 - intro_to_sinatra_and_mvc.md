# Sinatra and MVC

### Learning Goals

* [ ] Recognize MVC pattern 
* [ ] Sinatra framework 

--------------------------

### Hook




### Lecture Flow

1. MVC
    * an architecture pattern used for organizing web applications
    * not the only way, but a very popular way, especially for web applications
    * **Model**
        * data and logic
    * **View**
        * how the data is represented to the user (e.g., HTML, JSON)
    * **Controller**
        * accepts input from the interface, passes on requests to the model, and then calls the appropriate view to represent model data
        * middle man between View and Model

2. RESTful Routing
    * pull up Restular
    * talk about how REST allows us to be efficient with URLs/endpoints by doing different things when different HTTP Verbs are used

3. Sinatra
    1. create new app ` corneal new APP-NAME`
    1. use Corneal to make a scaffold

```bash
corneal -v              # Show Corneal version number
corneal help [COMMAND]  # Describe available commands or one specific command
corneal new APP-NAME    # Creates a new Sinatra application
corneal model NAME      # Generate a model
corneal controller NAME # Generate a controller
corneal scaffold NAME   # Generate a model with its associated views and controllers
```

  2. run application with shotgun - `shotgun`
  3. walk through `application_controller.rb`
  4. demo routes 
    - show how changing the verb or route breaks things
  5. move to views
    - talk about ERB interpolation characters, difference between `<%= %>` and `<% %>`

> commit and push, get students to pull

  6. Think-Pair-Share, add a new route that displays "Hello World!"
  7. pull up Network tab of Dev tools with Sinatra app - Look what it's doing for us with just so little code!
  8. Add a model/database
    - `rake db:create_migration NAME=whatever`