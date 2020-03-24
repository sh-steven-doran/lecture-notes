# Intro to Rails - Forms, Params, Routes

### Learning Goals

* [ ] Create a new Rails application
* [ ] Describe similarities between Sinatra routing & Rails routing
* [ ] Generate a controller
* [ ] Create actions/methods for a RESTful controller
* [ ] Create views
* [ ] Generate a model
* [ ] Create routes

--------------------------

### Hook

* MVC
* routing
* form_for
* strong params

### Lecture Flow

1. What is Rails?
    * MVC web application framework written in Ruby
    * created in 2003 by David Heinermeier Hansen
    * 3 principles:
        * Ruby Programming Language
        * Model-View-Controller Architecture
        * Programmer Happiness
    * convention over configuration
        * software design pattern that tries to eliminate the number of decisions a developer has to make
        * relies on conventional patterns
        * developer only needs to specify and code out the non-standard parts of a program
        
2. Installing Rails
    * `gem install rails`
    * `brew install yarn`

3. Routing
    * difference between Sinatra and Rails
    * focus on Routing DSL
    
4. Forms
    * form_for

5. Strong Params

5. Make petstore application or something
    * let the errors drive us - just go to `/pets`
    * let's build out some RESTful paths for pets
    * making a controller
        * `rails g controller pets index show`
        * `rails g scaffold_controller pets`
        * `rails g scaffold Pet name:string animal:string`
    * routing
        * in Sinatra `get '/pets do...` 
    * migrations
    * models
    * form_for
    * strong params