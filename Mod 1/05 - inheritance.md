# Inheritance Lecture Notes

### Learning Goals

- [ ] Review how to inherit from a parent class.
- [ ] Review what `super` is doing.
- [ ] Review the look up chain.
- [ ] Investigate `self` in the child and parent classes.
- [ ] Review how to `extend` to add class methods.
- [ ] Review how to `include` to add instance methods.

--------------------------

### Key Concepts
* Super
* Superclass/parent class
* Modules
* DRY
* Lookup Chain
* `self` in different contexts

### Lecture Flow

1. RSpec and TDD
2. Tests are just ruby code - put `binding.pry`
3. Build out Cat, Dog, and Fish classes according to tests
4. Dry them out with Animal class
    * explore `self` in different contexts
5. Add `super` to cat initialize - `number_of_lives` attribute
    * [`super` in Ruby Docs][1]
    * call `super` with arguments and without
6. Add a `mammal` module with custom action - `walk`
    * `include` and `extend` module
    * call `super` from `Dog#walk`

[1]: https://ruby-doc.org/docs/keywords/1.9/Object.html#method-i-super