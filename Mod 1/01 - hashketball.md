# Hashketball Lecture Notes

### Learning Goals

* [ ] Distinguish between data types in Ruby
* [ ] Show how to look up documentation for data types in Ruby
* [ ] Demonstrate the use of common Array methods
  * [ ] `#each`
  * [ ] `#map`
  * [ ] `#select`
  * [ ] `#find`
* [ ] Differentiate array methods by their respective return values
* [ ] Define the Single Responsibility Principle
* [ ] Employ test-driven development best practices in their labs
  * [ ] `rspec --fail-fast` handle one error at a time
  * [ ] Red, Green, Refactor
  * [ ] Make it work (shameless green), make it right, make it fast

--------------------------

### Hook

* demonstrate a developer's thought process
* work on array methods
* talk about tests

### Lecture Flow

* Just a review of the Hashketball Lab

1. Lecture 101
    * shouldn't be first introduction to topic
    * no code along

2. Explore file structure
3. TDD and RSpec
    * Red-Green-Refactor

4. Pseudocode and defining the problem
    * write pseudocode for `num_points_scored`
    
5. review `.map` - a method for creating a new array from an enumerable
6. write a `get_all_players` helper method using map - student activity
7. use `.find` to solve shoe_size test

### Defining the Problem

* what are the steps we need to do to solve the problem

```ruby
def num_points_scored(player_name)
  # get a list of all the players
  # find the player whose name matches the argument 'player_name'
  # return that player's points
end
```

* what's the optimal data structure we could use here - `[{}, {}, {}...]` with each has representing a player
* so how can we get there?

### Digression on .map

* let's write a method called `double_all` 
* write it with `.each` and then with `.map`
* demo in console

```ruby
# sandwich pattern
def double_all(array)
  doubles = []

  array.each do |num|
    doubles << num * 2
  end

  doubles
end
```

```ruby
def double_all(array)
  array.map { |num| num * 2 }
end
```

* `.map` returns an array with elements corresponding to each element in the original array

```ruby
# what will this return?
arr.map do |num|
  7
end
```

* `.map` iterates - there are lots of methods that iterate over an Enumerable

### Student Exercise

* write a method that takes an array of instructor hashes and returns an array of names (strings)
* think, pair, share

```ruby
# Define a method called get_names that takes an array of instructors and returns just their names
instructors = [ {name: 'Steven', hometown: 'Red Deer'}, 
                {name: 'Dana', hometown: 'Long Island'}, 
                {name: 'Charlie', hometwon: 'Prague'} ]

def get_names(instructors)
  instructors.map do |instructor|
    instructor[:name]
  end
end
```

### Apply to `get_all_players` method

* walk through each step - What parts of the hash do we need? How do we eliminate the keys?
* what do we get at each point?

```ruby
def get_all_player
  players = game_hash.values.map do |team|
    team[:players]
  end

  players.flatten
end
```

### `.select` and `.find` digression

* loop over an array of numbers, get the even values
* what would be returned here?

```ruby
[1,2,3,4].select { |n| 3 }
```

* how to get just one value?

```ruby
[1,2,3,4].select { |n| n == 4 }
# => [4]
```

### Build out `find_player` and `shoe_size` methods

* use `.find` to get a single player from the `all_players` array by name

### Single Responsibility Principle

* a single method should do just one thing