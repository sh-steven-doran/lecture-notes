# Rails Validations

### Learning Goals

* [ ] 


--------------------------

### Hook

* `before_action` filter - `find_thing`
* `f.check_box` - look at params
* validations - built-in and custom
* flash
* redirect does a new GET, statelessness, so data can be persisted across requests 
    * demonstrate looking at console 

### Lecture Flow

1. create new Rails app - 1-to-many
    * use resources to set up relational integrity
    * set up `dependent_destroy`
    * seed some parent data
    * make new, show, and create endpoints
    * make views
2. add some validations 
    * demo in console
3. walk through the case where record doesn't save because of validations
    * if using `form_with` be sure to set `local: true`
    * talk about redirect vs render - watch console behavior, 
    * render errors on the page