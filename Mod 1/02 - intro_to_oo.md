# Intro to OO Lecture Notes

### Learning Goals

* [ ] Define object in programming domain
* [ ] Explain the concept of sending messages
* [ ] Create a class and instantiate an instance of the class
* [ ] Explain the difference between a class and an instance
* [ ] Pass arguments to new by defining an initialize method in class
* [ ] Create instance methods
* [ ] Call methods on the implicit or explicit self
* [ ] Define attribute readers and writers using attr_ macros
* [ ] Get more practice with array compositions (each, map, select/filter)
* [ ] Explain the need for variable scope and why it's important to not utilize global variables

### Hook

* objects have identity, attributes, behavior 
* object can respond to messages
* classes are object factories - they provide the blueprint for instances


--------------------------

### Lecture Flow

1. Everything is an object
    * identity - `object.id`
    * attributes - `array.length`
    * behaviors - `array.concat`
2. Messages
    * different ways of calling methods
    * what happens when an object can't respond to a message
    * demonstrate `.methods`
    * messages are sent, it's up to the object how to respond/implement 
3. Custom objects

### Everything is an Object in Ruby

```ruby
# what is the data type of x?
# what is the value of x?
x = 3
puts x.class
puts x

# what happens when we run this code?
# what is split and where does it come from?
# how does x know what to do with split?
# what's happening when we run this code?
x = "hello how are you"
x.split
```

* we send _messages_ to objects that they respond to by doing some kind of work
* the exact work they do is defined on that object's _class_

```ruby
x = 3

# what does message name mean here?
message_name = :+

# what does send do?
# what does the argument to send specify?
# what other arguments does send take?
x.send(message_name, 1) === x + 1

# most operators in Ruby are just messages sent to objects
names = [ "Steven",  "Charlie",  "Dana" ]
names[0]
names.[](0)
names.send(:[], 0)

# objects complain when they don't know how to respond to messages
# objects complain when they don't know how to execute methods
names.respond_to_undefined_method

# check if an object responds to a message
names.responds_to? message_name
```

### What is an Object?

* _object = identity + state + behavior_
* _object = identity + attributes + actions_
* objects are instances of a class
* objects are copies of a class template
* objects have an identity
* objects can response to messages

```ruby
# we can instatiate a new object
the_crystal_gems = Array.new

# the_crystal_gems has an identity
the_crystal_gems.object_id

# the_crystal_gems has attributes
the_crystal_gems.length

# the_crystal_gems has behavior
the_crystal_gems.push('Garnet')

#the_crystal_gems is an instance of a class
the_crystal_gems.class
```

### Creating our own Objects

* why do we want to do this?
  * in general it allows us to define a bunch of attributes and behaviors for a type of object that all instances of that object will receive
  * more efficient, allows us to avoid having to write code over and over and over again

* create some kind of object as a hash

```ruby 
bank_account = {"user_id": 3, "balance": 100} 
```

* how do we make a bunch of these?

```ruby 
bank_account = {"user_id": 3, "balance": 100} 
bank_account = {"user_id": 5, "balane": 200} 
bank_account = {"user_id": 'a', "balance": 'yes'} 
```

* manually instatiating all these hashes is slow and error prone
* it's difficult to change any of the attributes
* __add binding.pry in different points to explore scope and self__

----

1. initialize with @user_id and @balance as instance variables. _You should discuss how scoping works and how instance variables live in the scope of the class. Demo this by accessing this variable in another method like `deposit`._
2. Create custom getters and setters for instance properties. Then show `attr_accessor` macro to add getters and setters to your instance variables, and `attr_reader` and `attr_writer` to be more specfic.
3. Add `@@all` as a class variable that lives outside each instance. This is an opportunity to hold on to all of the created instances of this class in memory in a place that is separate from each of the instances themselves. When adding new instances add `@@all << self` to `initialize`.
4. Adding a method that interacts with one of the instance methods. This showcases implicit `self`. This is a good chance to use defined getters and setters inside of other methods to understand how Ruby interprets variables / method calls more deeply.
5. What is `self` in each context? Use `binding.pry` to show that `self` is the class outside of any method, and use that intuition to write `BankAccount.all`. You can show that `BankAccount.new` is also a class method.


```ruby
class BankAccount
  attr_reader :user_id, :balance

  @@all = []

  def initialize(user_id, balance)
    @user_id = user_id
    @balance = balance

    @@all << self
  end

  def deposit(amount)
    @balance = @balance+amount
  end

  def widthdraw(amount)
    @balance = @balance-amount
  end

  def self.all
    @@all
  end
end
```

* Once you've got some fun objects to play with, you can do array operations on `BankAccount.all`! Have the students do some `map`, `select`, `find`, and `each` commands with you. 