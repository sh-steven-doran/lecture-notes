# Rails Review

### Learning Goals

* [ ] 


--------------------------

### Hook

* `before_action` filter - `find_thing`
* `f.check_box` - look at params
* validations - built-in and custom
* flash
* redirect does a new GET, statelessness, so data can be persisted across requests 
    * demonstrate looking at console 

### Lecture Flow

1. shared form partial for new and edit

```html
<%= form_for @person do |f| %>
  <%= f.label :name %>
  <%= f.text_field :name %><br>

  <%= f.fields_for :addresses do |addr| %>
    <%= addr.label :street %>
    <%= addr.text_field :street %><br>

    <%= addr.label :city %>
    <%= addr.text_field :city %><br>
  <% end %>

  <%= f.submit %>
<% end %>
```

---
```html
# users/edit.html.erb

<h2>Edit user</h2>
<%= render 'form' %>
```

---
```ruby
class PeopleController < ApplicationController
  def new
    @person = Person.new
    @person.addresses.build
  end

  def edit
    @person = Person.find(params[:id])
  end
  ...
```

2. custom routes
