# Intro to ActiveRecord Lecture Notes

### Learning Goals

* [ ] Define Object Relational Mapper (ORM)
* [ ] Describe how gems work and the value of shared code
* [ ] Implement ActiveRecord in their projects
* [ ] Practice creating migrations for updating the database structure
* [ ] Explain how rake works and how to run rake tasks
* [ ] Distinguish between and define "model", "class", and "table"
* [ ] Practice with ActiveRecord::Base instance and class methods
* [ ] Perform persistent CRUD actions on one model using ActiveRecord

--------------------------

### Hook

* relationships are macros that define an assortment of class and instance methods for us
* if something has a foreign key, then it "belongs to" the other thing


### Lecture Flow

1. Review file structure
    * review new files and directories - migrate, db, models
2. Go over migrations 
    * make cows
    * in console demo that we have no way for assigning cows to aliens
    * add `alien_id` to `cows` table, run migration
3. Set up one-to-many for aliens --> cows
    * macros are methods that define other methods for us 
    * gives us bunch of class and instance methods
    * add some cows to aliens
        * set the `alien_id` manually
        * use `alien.cows.create`
        * use `<<` 
    * show how to access the alien from the cow
        * `cow.alien` vs `alien.cows`
3. Set up `has_many_through`
    * create migration for join etc.
    * change relationships
    * create powers and heros and demonstrate that as associations are made, join records are also made