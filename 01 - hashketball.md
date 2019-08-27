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

```text
Lecture Plan

 2m  Talk about lectures
 3m  Working with the spec and intro TDD
 3m  Build the game hash
10m  Define the problem
 5m  Digression on `map`
10m  Student Exercise
 5m  Apply to `get_players`
10m  Digression with `select` and `find`
10m  Single Responsibility Priniciple (SRP) and putting it together
===
 1h  Total 
```

### Lecture 101

* labs are generally deployed before the associated lecture
* students do better if it’s not the first time seeing the material
* feel free but I wouldn’t recommend code-along
* stop and ask questions whenever you need to
* correct me as I type

* just a review of the Hashketball lab
* explore file structure and what we’ve been given


### TDD and RSpec

* I always start a project - or lab - by looking at the tests and running RSpec
* use —fail-fast
* red, green, refactor
* shameless green - write the smallest amount of code needed to pass test
* tests are just Ruby code - puts something
* run specific file or line
* walk through a spec file
* feedback loop of reading tests/errors and then making changes to code

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