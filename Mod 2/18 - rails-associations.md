# Rails Associations

### Learning Goals

* [ ] Refresher on has_many and belongs_to
* [ ] Use Rails form helper methods that create an associated object
* [ ] Implement `dependent: :destroy` in order to destroy associated objects to normalize database


--------------------------

### Hook

* ActiveRecord associations review
* `collection_select` in Rails form
* `dependent_destroy`
* foreign key constraints - referential integrity

### Lecture Flow

1. create new rails 1-to-many app
    * `rails g resource Farmer name`
    * `rails g resource Cow name spots:integer farmer:references`
2. review the files made - controller, routes, migration, model
3. set up associations and migrate
4. play with cows and farmers in console - talk about foreign keys and referential integrity
5. seed some farmers
6. create new form and create and new routes
7. implement a select the hard way, then use collection select
    * look at params, strong params
8. validations
9. `dependent_destroy` in Farmer


* <https://apidock.com/rails/ActionView/Helpers/FormBuilder/collection_select>

### Cow Controller

```ruby
class CowsController < ApplicationController

  def new
    @cow = Cow.new(spots: rand(0..25))
  end

  def create
    @cow = Cow.new(cow_params)
    if @cow.save
      redirect_to cow_path(@cow)
    else
      redirect_to new_cow_path
    end
  end

  private
  
  def cow_params
    params.require(:cow).permit(:name, :spots, :farmer_id)
  end

end
```
--
### DIY `collection_select`

```html
<!-- DIY f.collection_select -->
<select name="cow[farmer_id]">
<% Farmer.all.each do |farmer| %>
  <option value="<%= farmer.id %>">
    <%= farmer.name %>
  </option>
<% end %>
</select>
```
--
### Cow Form
```ruby
# collection_select
# First arg is method we want to call on @post (:famer_id),
# Second The collection we want to use to populate the dropdown(Farmer.all),
# Third The value we want in our params: Farmer#id,
# Fourth What do we want to display in the tag itself? Farmer#name
```

```html
<h1>Create a Cow</h1>

<%= form_with model: @cow do |f| %>
  <%= f.label :name %>
  <%= f.text_field :name %>
  <br>
  <%= f.label :spots %>
  <%= f.number_field :spots %>
  <br>
  <%= f.collection_select :farmer_id, Farmer.all, :id, :name %>
  <br>
  <%= f.submit %>
<% end %>
```
--
### Errors

```html
<% if @cow.errors.any? %>
  <ul>
    <% @cow.errors.full_messages do |message| %>
    <li><%= message %></li>
    <% end %>
  </ul>
<% end %>
```
--
### Validations

```ruby
class Cow < ApplicationRecord
  belongs_to :farmer
  #belongs_to farmer will also validate the presence and validity of our farmer;
  # the farmer has to exist for this cow to be associated with it

  validates :name, { presence: true, uniqueness: true }
  # validates :name, uniqueness: { case_sensitive: false }
  validates :spots, numericality: { less_than_or_equal_to: 50 }
end
```