# Intro to TDD

### Learning Goals

* [ ] Explain the need for testing in general
* [ ] Install RSpec in a project
* [ ] Define Test-Driven development
* [ ] Describe what a testing framework is and what the RSpec framework does
* [ ] Write tests for a basic function while considering entire problem space
* [ ] Describe the difference between failing, passing, and pending test cases
* [ ] Define assertions and matchers in the context of test cases
* [ ] Use output from a testing framework to guide their development

--------------------------

### Hook

* testing can drive the development of the code you need to write
* shameless green
* Red-Green-Refactor


### Lecture Flow

1. install RSpec gem
2. initialize RSpec in the project, go over the files it created
    * show directory structure using `tree`
3. create `spec/palindrome_spec.rb`
    * walk through set up
4. four stages of testing
    1. setup
    2. execercise
    3. expectation
    4. teardown 
5. shameless greeen
    * write the least amount of code possible to get test to pass
6. Red-Green-Refactor
7. add `--format documentation` and `--color` to `.rspec` file
8. extract test object using `let`
9. edge cases
    * numbers
    * capitalization
    * spaces
    * weird characters
    * empty strings

### Code

```ruby
class Palindrome

  def self.run(word)
    word.reverse == word
  end
end
```
----
```ruby
require 'spec_helper'
require_relative '../lib/palindrome'

RSpec.describe Palindrome do
  describe '.run' do
    it 'returns true when given a palidrome' do
      result = Palindrome.run("poop")
      expect(result).to be true
    end

    it 'returns false when given a word that is not a palindrome' do
      result = Palindrome.run("poopy")
      expect(result).to be false
    end
  end
end
```

