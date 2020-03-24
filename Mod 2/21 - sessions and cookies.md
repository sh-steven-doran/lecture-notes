# Sessions and Cookies

### Learning Goals

- [ ] Describe the stateless nature of HTTP
- [ ] Understand the difference between `flash` and `session`
  - [ ] Decide when to use what
- [ ] Use sessions to make HTTP stateful
  - [ ] Add and remove information from the `session`
- [ ] Understand how cookies enable sessions to work
  - [ ] Use cookies to store data on the browser
  - [ ] Cookies are key-value pairs with some extra info


--------------------------

### Hook

* cookies allow us to implement state in HTTP
* difference between flash and session
* 

### Lecture Flow

1. Talk about cookies, how they provide state
2. Demonstrate New Yorker and Ebay
3. Create cart:
    1. create route - `post "/cart", to: "cart#add_to_cart"`
    2. add path to button - `<td><%= button_to "Add to cart", { action: "add_to_cart", controller: "cart", id: book.id }%></td>`
    3. create cart controller with `add_to_cart` action
    4. add logic to view cart items on `books#index`
    5. add remove from cart button
    6. add clear cart button
4. Add article limit:
    1. add counter logic to `books#show`
    2. add view logic to show page
     
--
```ruby
class CartController < ApplicationController
  def add_to_cart
    session[:cart] ||= []
    session[:cart] << params[:id]

    redirect_to books_path
  end

  def clear_cart
    session[:cart] = []

    redirect_to books_path
  end

  def remove_from_cart
    session[:cart] = session[:cart].select{|id| id != params[:id]}

    redirect_to books_path
  end
end
```
--
```ruby
Rails.application.routes.draw do
  resources :books

  post "/cart", to: "cart#add_to_cart"
  delete "/clear_cart", to: "cart#clear_cart"
  delete "/cart", to: "cart#remove_from_cart"
end
```
--
```ruby
# BooksController

...

  def index
    session[:cart] ||= []

    @cart_books = session[:cart].map do |id|
      Book.find(id)
    end

    @books = Book.all
  end

  def show
    session[:views] ||= 0
    session[:views] += 1

    @book = Book.find(params[:id])
  end
  
  ...
```