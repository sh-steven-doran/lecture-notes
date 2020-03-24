# Rails Auth

### Learning Goals

* [ ] 


--------------------------

### Hook

* =

### Lecture Flow

1. Set up our app for a user
    * `rails g resource User username password_digest`
    * `rails db:migrate`
    * `resources :users, only: [:new, :create, :show]`

```ruby
class User < ApplicationRecord
  has_secure_password
  validates :username, uniqueness: { case_sensitive: false }
end
```
--
```html
<h1>Sign Up</h1>

<%= form_for @user do |f| %>
  <%= f.label :username %>
  <%= f.text_field :username %>
  <%= f.label :password %>
  <%= f.password_field :password %>
  <%= f.label :password_confirmation %>
  <%= f.password_field :password_confirmation %>
  <%= f.submit %>
<% end %>
```
--
```ruby
def create
  @user = User.new(user_params)

  if @user.save
    flash.notice = 'User created successfully.'
    redirect_to user_path(@user)
  else
    flash[:errors] = @user.errors.full_messages
    redirect_to new_user_path
  end
end
```
2. `bcrypt` stuff
    * adds salt and then hashes - one way

```ruby
# in rails console
> salted_pw = BCrypt::Password.create('P@ssw0rd')
  => "$2a$10$YQvJPemUzm8IdCCaHxiOOes6HMEHda/.Hl60cUoYb4X4fncgT8ubG"

> salted_pw.class
  => BCrypt::Password

> salted_pw == 'P@ssw0rd'
  => true
```
--
```ruby
# in rails console
> sample_digest = User.last.password_digest
  => "$2a$10$SJiIJnmQJ/A4z4fFG5EuE.aOoCjacFuQMVpVzQnhPSJKYLFCoqmWy"

> sample_digest.class
  => String

> sample_digest == 'P@ssword'
 => false

> bcrypt_sample_digest = BCrypt::Password.new(sample_digest)
  => "$2a$10$dw4sYcbLXc8XRX6YGc7ve.ot6LbYevMbSpFQZUaa8tm5NI8cxBPwa"

> bcrypt_sample_digest.class
  => BCrypt::Password

> bcrypt_sample_digest == 'P@ssw0rd'
  => true
```
--

3. Add sessions stuff

```ruby
get "signup", to: "users#new", as: "signup" # remove new from user resources
get "login", to: "sessions#new", as: "login"
post "sessions", to: "sessions#create", as: "sessions"
```
--
```ruby
class SessionsController < ApplicationController
  def new
  end
  
  def create
    @user = User.find_by(username: params[:username])
    if @user && @user.authenticate(params[:password])
      session[:user_id] = @user.id
      redirect_to user_path(@user)
    else
      redirect_to login_path
    end
  end
end
```
--
```html
<h1>Log In</h1>

<%= form_tag sessions_path do %>
  <%= label_tag "Username" %>
  <%= text_field_tag :username %>
  <%= label_tag "Password" %>
  <%= password_field_tag :password %>
  <%= submit_tag "Sign In" %>
<% end %>
```
--
```ruby
# add current user session to user#create

def create
  @user = User.new(user_params)

  if @user.save
    flash.notice = 'User created successfully.'
    session[:user_id] = @user.id
    redirect_to user_path(@user)
  else
    flash[:errors] = @user.errors.full_messages
    redirect_to new_user_path
  end
end
```
4. On dogs index just show the users dogs if logged in

```ruby
# dogs_controller

def index
  if session[:user_id]
    @user = User.find(session[:user_id])
    @dogs = @dogs
  else
    @dogs = Dog.all # or force a login
  end
end
```

5. Refactor so don't have to repeat that logic all the time, add logic to `ApplicationController`

```ruby
def current_user
  if session[:user_id]
    @user = User.find_by(id: session[:user_id])
  end
end

def logged_in?
  !!current_user
end
```
---
```ruby
# dogs_controller

def index
  if logged_in?
    @dogs = current_user.dogs
  else
    @dogs = Dog.all # or force a login
  end
end
```

6. add logic to redirect to log in page unless already logged in

```ruby
# application_controller.rb

def authorized
  redirect_to login_path unless logged_in?
end
```
--
```ruby
# in any controllers that need it

before_action :authorized
skip_before_action :authorized, only: [:new, :create] # or whatever onlys you need
```

7. logging out

```ruby
# routes

delete "sessions", to: "sessions#destroy"
```
--
```ruby
# sessions_controller

def destroy
  session.delete(:user_id) # or session[:user_id] = nil
end
```
--
```ruby
# application.html.erb

<% if logged_in? %>
  <%= link_to "Logout", sessions_path, method: :delete %>
<% else %>
  <%= link_to "Login", login_path %>
<% end %>
```

