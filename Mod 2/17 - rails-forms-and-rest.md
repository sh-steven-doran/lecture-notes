# Rails Forms and REST

### Learning Goals

* [ ] Discuss and Review Forms
* [ ] form_with, link_to, button_tag, submit_tag
* [ ] Strong params


--------------------------

### Hook

* `form_with`
* form helpers - `link_to`, `button_to`, `submit`
* strong params

### Lecture Flow

```
15m Create a new application
20m Build CRUD using REST
15m Mass Assignment
10m Refactor with before_action
===
60m Total
```

1. create new app (dogs and owners?)
2. create a form using `form_with`

```
<h1>Create a New Dog!!</h1>

<%= form_for @dog do |form| %>
  <%= form.label :name %>
  <%= form.text_field :name %>
  <%= form.label :breed %>
  <%= form.text_field :breed %>
  <%= form.submit %>
<% end %>
```

3. create a delete button on the show page
    * `<%= button_to 'Delete Dog', { action: "destroy", id: @dog.id }, method: :delete %>`

4. create a link to index that shows all dogs using `link_to`
    * `<%= link_to 'Home', dogs_path %>`