# Rack and the Internet

### Learning Goals

* [ ] High level understanding of the Internet vs the World Wide Web
* [ ] Discuss HTTP Verbs and when to use different ones
* [ ] Understand how conventional user of HTTP Verbs corresponds to CRUD actions
* [ ] Be able to describe Rack
* [ ] Recognize MVC pattern 

--------------------------

### Hook

* we're going to talk a little bit about the "How It Works" of the internet, but try not to get bogged down in it - focus on "How To Do It" part 


### Lecture Flow

1. What is the Internet
    * DARPA
    * a way of exchanging data in "packets" over a distributed network
    * data doesn't flow linearly
    * infrastructure - cables, wires, wifi

2. What is the World Wide Web
    * a system that sits on top of the Internet
    * primarily a network of HTML documents with unique addresses accessed via a client of some sort using HTTP requests and responses
    * other protocols exist on the Internet - SMTP for email, FTP and Bittorrent for transferring files, etc.

3. IP addresses
    * unique numerical identifier for networked devices

4. Domain Name System (DNS)
    * a distributed lookup system that associated human-readable website names with the IP address of that service

5. Request-Respones Cycle
    * clients send requests, servers send responses
    * Request is a piece of data formatted with instructions for where and how the request should be made as well as information about the client sending the request
    * it can send data in a body but this is optional and depends on the method being used
    * Response is a piece of data formatted with the response from the server indicating the status of the request, information about the response, and a body (this is where the HTML is)
    * Response Codes

6. HTTP Verbs
    * conventions for formatting HTTP requests
    * e.g., for GET, parameters come in the URL string itself, for POST, parameters/data are put into the body of the request
    * other conventions - specific HTTP verbs are used to execute particular types of actions on the server
    * HTTP Verbs and CRUD
        * convention, agreement between server and client
        * As developers, we will design our apps to accepts particular types of requests at specific endpoints to carry out certain actions and to raise the correct errors when something else happens
        * The platforms we use (e.g., Sinatra, Rails etc.) do a lot of this for us 

7. Rack
    * not going to spend a lot of time demoing this since it isn't something you'll ever do and it's covered in the labs
    * it's a gem and an architecture
    * it's middleware, software that sits between the webserver and our application
    * it's an architecture because it defines a simple interface and any application that implements this interface can be run in Rack
    * Sinatra and Rails are Rack apps because they implement the interface designed by Rack, Rack then takes care of the communication between the webserver and our application 
        * this allows us to easily switch webservers without having to change any of our application code
        * it also means we can change our application platform (e.g., from Sinatra to Rails) and not have to reconfigure out webserver
    * you could use Rack alone to implement a static web application
    * **static vs. dyanamic web apps**