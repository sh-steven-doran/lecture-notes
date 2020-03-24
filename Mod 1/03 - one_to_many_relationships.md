# One-To-Many Lecture Notes

### Learning Goals

* [ ] Implement one object to many objects relationship
* [ ] One object has many objects
* [ ] One object belongs to another object
* [ ] Practice passing custom objects as arguments to methods
* [ ] Demonstrate single source of truth
* [ ] Infer type of method (class or instance) through naming conventions

--------------------------

### Terms

* __Model__ - a class whose primary responsibility is to store data and define behaviors
* __Domain__ - the part of the real world we are trying to reproduce in our code, the subject matter of the problem (the domain of Learn is online education)
* __Domain Model__ - the representation of our domain in our models/classes to represent concrete or abstract conecpts (e.g., students, classes, assignments etc.)
* __Relationship__ - how one model/class/thing relates to others in the domain
	* _one\_to\_many_ - a relationship where a single model contains or keeps track of other models (e.g., an author has many books, a musician has many albums, an album has many songs etc.)

### Lecture Flow

1. Show breeder deliverables and build out Dog class using class/instance methods and attributes
    * explore `self` in different states
    * remove `self` - too much?
2. Introduce key concepts for the lecture
    * Model
    * Domain
    * Domain Model
    * One-to-Many
3. Show how to draw a one-to-many in erd
    * come up with different domain examples
4. Build out `User` and `Tweet` as per deliverables 
    * show how to access app through a single point of entry
    * when writing `User#post_tweet` add it manually then extract a private method
    * __be sure to break at the correct place to talk about *Single Source of Truth*__ --->> right after Tweets can be instantiated and they are being saved as an instance variable on the User




### Single Source of Truth

* Demonstrate why we want single source of truth...
    1. first just save the tweets in the user class, don't create a `@@all` class variable in `Tweet`
    2. show how we can get a user's tweets this way
    3. then add the `@@all` and shovel method in `Tweet#initialize`, also add `Tweet.all` method
    4. Create a user and have that user post a few tweets.
    5. Remove a tweet from Tweet.all.
    6. Call user.tweets to see it's still there.
    7. From here rewrite the `User#post_tweets` and `User#tweets` methods 
    8. comment out the `@tweets` variable in `User#initialize`

	
### Deliverables

* __Explain the difference between # and . notation__

* Create a _User_ class. The class should have these methods:
  * [ ] `User#initialize` which takes a username
  * [ ] `User#username` reader method
  * [ ] `User#tweets` that returns an array of Tweet instances
  * [ ] `User#post_tweet` that takes a message, creates a new tweet, and adds it to the user's tweet collection  
  * [ ] `User.print_tweets` that prints the message of each tweet to the screen in a _pretty_ way (be creative)
<br>  

* Create a _Tweet_ class. The class should have these methods:
	* [ ] `Tweet#initialize` which takes a message and a user
	* [ ] `Tweet#message` that returns a string
	* [ ] `Tweet#user` that returns an instance of the user class
	* [ ] `Tweet.all` that returns all the Tweets created.
	* [ ] `Tweet#username` that returns the username of the tweet's user

```ruby
class User
  attr_reader :username, :tweets

  def initialize(usernmae)
    @username = username
    @tweets = [] # this is the idea that we will remove later
  end

  def post_tweet(message)
    # create a new tweet
    tweet = Tweet.new(message, self)
    # add that tweet to this users collection of tweets
    add_tweet(tweet)
  end
  
  # once we build out the Tweet class to
  # keep track of its user we can rewrite
  # these methods this way
  
  # def post_tweet(message)
  #   Tweet.new(self, message)
  # end
  
  # def tweets
  #   Tweet.all.select do |tweet|
  #     tweet.user == self
  #   end
  # end

  private

  def add_tweet(tweet)
    self.tweets << tweet
  end
end

class Tweet
  attr_reader :message, :user

  @@all = []

  def initialize(message, user)
    @message = message
    @user = user

    @@all << self
  end

  def self.all
    @@all
  end
end
```



