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
require 'json'
require 'rest-client'

# take in input
puts "Welcom to our fancy book searcher thing. What term would you like to search:"
user_input = gets.chomp

formatted_input = user_input.tr(' ', '+')

url = "https://www.googleapis.com/books/v1/volumes?q=#{formatted_input}"

response = RestClient.get(url)
response_hash = JSON.parse(response)

books = response_hash["items"].map do |item|
  item["volumeInfo"]
end

# iterate over each book item
# print title, authors, and page count for each book

books.each do |book|
  puts book["title"]
  puts book["authors"]
  puts book["pageCount"]
  puts "*" * 15
end

binding.pry
```

