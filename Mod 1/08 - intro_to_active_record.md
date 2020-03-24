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

* migrations allow us to build and change our database
* rake tasks just execute small bit of code, scripts
* ActiveRecord is an ORM that gives us all the functionality we've been building out manually

### Lecture Flow

1. File structure
    * Gemfile
    * `lib` folder holds models and app code
    * `db` directory holds migrations and seeds.rb file
    * `config` holds environment file
    * `require 'bundler'` and `Bundler.require` load all of the gems in our Gemfile
    * `ActiveRecord::Base.establish_connection` sets up our database with options hash
    * `require_all` loads all of our application code

2. Rake
    * allows us to define _tasks_ which are just little bits of ruby code to be executed
    * define them in our `Rakefile`
    * can view them using `rake -T`
    * some are coming from `sinatra/activerecord/rake` library, some we defined

3. Migrations and Database structure
    * what's our domain going to be? - be creative - 1-to-many
    * `rake db:create_migration` - look at tasks available in `rake -T`
    * look at migrations - what's this sequence number mean?
    * write a migration using `change`
    * conventions - plural vs singular
    * run migration, demo `rake db:migrate:status`
    * look at `schema.rb` - match version to migration number
    * `schema.rb` is the **authoritative representation of the database structure**
    * demonstrate rolling back
    * write a migration to add a column

4. Connecting models to AR
    * __MAJOR KEY__ 🔑 convention is to have the model class name singular and the sql table plural
    * create a class that inherits from `ActiveRecord::Base`
    * play around with creating and stuff in console
    * pull up DB in browser and show that the records are being made
        * `new`
        * `save`
        * `create`
        * `update`
        * `find`
        * `find_by`
        * `delete`
    * map these to CRUD
    * what type of object comes back from `Model.all`?

5. Methods from ActiveRecord
    * `Model.new` - creates a new instance in local memory without persistence
    * `Model#save` - inserts or updates instance in db
    * `Model.create` - Model.new + Model\#save
    * `Model.all` - all instances
    * `Model.first` - instance with the lowest ID in the db
    * `Model.find` - also find by id
    * `Model.find_by(attribute: value)` - can find by one attribute-value pair or multiple