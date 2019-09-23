# Hashes and the Internet Lecture Notes

### Learning Goals

* [ ] Recognize the parts of the request-response lifecycle
    * [ ] Define client and describe setting up the request
    * [ ] Define server and describe how the response is formatted
    * [ ] Identify HTML as a response type
    * [ ] Identify and define JSON
* [ ] Define Application Programming Interface (API)
    * [ ] Explain the uses of an API on the internet
* [ ] Practice making requests to an API and parsing and examining the result
* [ ] Practice writing a command line application (CLI)

--------------------------

### Hook

* what is the request-response lifecycle?
* what is an API?
* what is JSON
* how to make a request to an API

### Lecture Flow

1. clients make requests to a URL with an HTTP verb
    * the most used verb is GET but there are others and there are conventions that guide their use
2. servers respond with a response code and a body
    * if the client is a browser the response is usually HTML
    * but a server can respond with other things as well
    * go to Reddit - this is serving HTML, CSS, and Javascript that the browser interprets and renders into the site we see
    * open dev tools


![Request-Response Cycle](https://miro.medium.com/max/1146/1*bx2bWzqeKCBndthiLGMK5g.png)

3. but if we request JSON we get something totally different
    * what is JSON - kind of like hash
    * a language agnostic data object
    * it's a convention of the web for passing data between servers and clients
4. Ruby gems for working with the Internet
5. REST Client
    * open new ruby file
    * what is an API - application programming interface
    * make url `"https://www.googleapis.com/books/v1/volumes?q=ruby+programming"`
    * look at the response, it's class
    * look at the documentation for Rest Client to see what we can do
    * `JSON.parse` the respone - what do we get
    * let's write an application that queries the Google Books API and the prints the results to the page
    * how can we make an application that accepts use input?
    * refactoring


```ruby
require 'pry'
require 'rest-client'
require 'json'


# write an application that takes in some user input
def welcome
  puts "Welcome to the BookSearcher"
  puts "Please enter a term:"
end

def get_user_input
  gets.chomp
end


# make a request to the google books api using term

def fetch_books(term)
  response = RestClient.get("https://www.googleapis.com/books/v1/volumes?q=#{term}")

  JSON.parse(response.body)
end


def get_title(book)
  book["volumeInfo"]["title"]
end

def get_author(book)
  if  book["volumeInfo"]["authors"]
   book["volumeInfo"]["authors"].join(" and ")
  else
   "No authors found"
  end
end

def get_description(book)
  if book["volumeInfo"]["description"]
    book["volumeInfo"]["description"][0..140] + "..."
  else
    "No description available"
  end
end

def print_book(title, authors, description)
  puts "*" * 30
  puts "Title: #{title}"
  puts "Authors: #{authors}"
  puts "Description: #{description}"
end


def run
  welcome
  search_term = get_user_input

  fetch_books(search_term)["items"].each do |book|
    title = get_title(book)
    authors = get_author(book)
    description = get_description(book)

    print_book(title, authors, description)
  end
end

# and display a list of books, including title, author and description, that are found
run
```

