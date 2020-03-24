# Sinatra Forms and Associated Objects
### Learning Goals

* [ ] Describe how the params hash is built
* [ ] Describe how to nest hashes inside of the params hash
* [ ] Describe how to nest arrays inside of the params hash
* [ ] Describe how mass-assignment works in relation to hashes
* [ ] Demonstrate how to use params hash to mass-assign and create related objects

--------------------------

### Hook

* RESTful routing
* forms
* params, mass assignment
* select
* associations


### Lecture Flow

1. create RESTful CRUD app for a domain
    * start at "Create", mass assignment, error in saving  
2. Change the welcome page to show links to relevant end point
3. add some 1-to-many relationship (designer?)
    * seed data `seeds.rb`
        * put a `.destroy_all` at the top
    * edit "New" to include designer
    * demo with a select dropdown for designer
4. seed data `seeds.rb`
    * put a `.destroy_all` at the top

     
---
### Helper Code Snippets
     
```ruby
# New
get '/donuts/new' do
  @donut = Donut.new
  @designers = Designer.all
  
  erb :'donuts/new'
end
```

--

```ruby
# Create
post '/donuts' do
  donut = Donut.create(params)
  redirect_to "/donuts/#{donut.id}"
end
```

--


```html
<section>
  <form action="/donuts" method="POST">
    <label>
      Flavor
      <input type="text" name="flavor" value="<%= @donut.flavor %>">
    </label>

    <label>
      Price
      <input type="number" name="snippet" value="<%= @donut.price %>">
    </label>

    <label>
      Designer
      <select name="designer_id">
        <% @designers.each do |designer| %>
          <option value="<%= designer.id %>"><%= designer.name %></option>
        <% end  %>
      </select>
    </label>

    <input type="submit">
  </form>
</section>

```