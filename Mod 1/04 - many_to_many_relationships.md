# Many-To-Many Lecture Notes

### Learning Goals

* [ ] Implement both sides of a many to many relationship
* [ ] Practice keeping groups of data related to classes on the class as a class variable
* [ ] Demonstrate single source of truth by not storing collections of objects on other objects
* [ ] Demonstrate single source of truth by not storing one object in multiple collections

--------------------------


### Lecture Flow

1. Review Tweets and User
    * diagram ERD
    * pull up code - Where was the Source of Truth for tweets? 
    * what did we pass into `Tweet#initialize`? - a `User` object
    * `Tweet.new('hey there', user)` - remember the tweet belongs to a user
    * the tweet kept track of its user
    * in pseudocode, how did a user access their tweets? - search through all the tweets for those that where user was self
    * what data type does `Tweet.user` return?
    * how can a tweet find out the name of the user who made it?
    * questions

2.  The world isn't a simple as a bunch of one-to-many relationships
    * aquarium -< exhibits -< fish
    * `Exhibit.new('coral reefs', aquarium) # <- we expect aquarium to be AN INSTANCE OF the AQUARIUM class`
    * `Fish.new('nemo', exhibit) # <- we expect exhibit to be AN INSTANCE OF the EXHIBIT class`

3. More complex relationships - let's create a domain model for a hospital
    * doctor and patient classes
    * what is their relationship? - doctor >---< patient
    * __Question: We know Models are classes that store data. Where in this domain could I store the data about what time the patient is scheduled to meet the doctor? What is the realtionship between these two models?__
    * Single Responsibility Principle
    * A doctor has many appointments / appointment belongs to doctor (we already know how to model this)
    * A patient has many appointments / appointment belongs to patient (we already know how to model this)
    * A doctor has many patients through appointments
    * A patient has many doctors through appointments
    * __When we create an Appointment instance, what are the dependencies?__

4. Add `Like` to Twitter
    * create class
    * create initializer - what dependencies?
    
### Deliverables

* Create a _User_ class. The class should have these methods:
  * [x] `User#initialize` which takes a username
  * [x] `User#username` reader method
  * [x] `User#tweets` that returns an array of Tweet instances
  * [x] `User#post_tweet` that takes a message, creates a new tweet, and adds it to the user's tweet collection  
  * [ ] `User.print_tweets` that prints the message of each tweet to the screen in a _pretty_ way (be creative)
  * [ ] `User#like_tweet` that accepts as a tweet instance as a parameter
  * [ ] `User#liked_tweets` that returns a collection of all the tweets this user has liked - __STUDENT ACTIVITY__
<br>  

* Create a _Tweet_ class. The class should have these methods:
	* [x] `Tweet#initialize` which takes a message and a user
	* [x] `Tweet#message` that returns a string
	* [x] `Tweet#user` that returns an instance of the user class
	* [x] `Tweet.all` that returns all the Tweets created.
	* [x] `Tweet#username` that returns the username of the tweet's user
	* [ ] `Tweet#likers` that returns a collection of all the Users who have liked this tweet

----


```ruby
class Like

  attr_accessor :user, :tweet

  @@all = []

  def self.all
    @@all
  end

  def initialize(user, tweet)
    @user = user
    @tweet = tweet
    @@all << self
  end


end
```
