# Intro to ORMs Lecture Notes

### Learning Goals

* [ ] Follow code that is organized into different files
* [ ] Define Object Relational Mapper (ORM)
* [ ] Explain how the `sqlite` gem works as a driver or wrapper around SQL
* [ ] Implement HEREDOCs to be saved in variables to be executed by SQL driver
* [ ] Perform persistent CRUD actions on a model
* [ ] Distinguish between ORM and SQL
* [ ] Demonstrate that ORMs are the pattern connecting scripting languages and databases
* [ ] Explain to a peer all the things that happen when we call `Tweet.all` (your answer should include when SQL is fired & when Ruby objects are created)

--------------------------

### Hook


### Lecture Flow

1. SQL Review
    * build 1-to-many tables for books and authors; do SQL activities
    * build many-to-many tables for books and authors; do SQL activities
2. CRUD - SQL and Ruby comparison
    * write example commands in each language to do CRUD actions
3. ORM
    * define ORM
    * _a pattern that maps database rows into Ruby objects and vice-versa_
    * _Ruby classes are represented in the DB as tables_
    * _attributes of classes are represented as columns_
    * _relationships between different classes are managed through foreign keys_
    * why is it helpful?
        * single language
        * abstractions, metaprogramming
        * allows for us to swap out our DB framework
4. __TAKE BREAK__
5. Twitter Application
    * walk through application
        * `environment.rb`
        * `run.rb`
        * `TweetApp.rb`
        * `bundler`
        * `sqlite` gem
    * show how current app works - no persistence
    * build new `Tweet.all` function that pulls from the database
        * manually add a tweet to the database
        
```ruby
def self.all
    # @@all
    sql = <<-SQL
      SELECT *
      FROM tweets;
    SQL
    
    results = DB[:conn].execute(sql)
    
    # how do we turn this array of hashes into an array of Tweets
    
    results.map do |row|
      Tweet.new(row["message"], row["username"])
    end
end
```
6. Twitter con't
    * make new `Tweet#save` function
    * mention SQL sanitization

```ruby
def save
    # @@all << self
    # self

    username = self.username
    message = self.message

    #what SQL would we want to implement to save Tweet instances to the database
    
    # HEREDOC 
    sql = <<-SQL
      INSERT INTO tweets (username, message)
      VALUES (?, ?);
    SQL
    

    DB[:conn].execute(sql, username, message)
end    
```
7. Twitter con't
    * how would we write the other CRUD actions - Update and Delete

## Domain Modeling and SQL Review

Draw out what your schema (structure of your tables and columns) would be for the following domains. Consider what tables are needed, what columns belong on which tables, and where the foreign keys belong.

1. Books and Authors where each book has a single author. Books should have a title and authors should have a name

### Books
| id  | title                | page_count | author_id |
| --- | ------------------- | ---------- | --------- |
| 1   | The Wheel of Time    | 1000       | 1         |
| 2   | The Knife Something  | 1000       | 1         |
| 3   | Ender's Game         | 263        | 2         |
| 4   | The Name of the Wind | 500        | 3         |



### Authors
id | name  
--- | ---            
1  | Robert Jordan     
2  | Orseon Scott Card 
3  | Patrick Rothfuss
4  | Stephen King


Q: Write the SQL to find all books written by a certain author given the author's id.

```sql
SELECT * 
FROM books
WHERE author_id = 1;
```

Q: Write the SQL to find all books written by a certain author given the author's name.

```sql
SELECT *
FROM books
JOIN authors
ON books.author_id = authors.id
WHERE authors.name = "Orseon Scott Card";
```

2. Books and Authors where each book can have one or multiple authors. Books should have a title and authors should have a name

### Authors
id | name   
--- | ---           
1  | Robert Jordan     
2  | Orseon Scott Card 
3  | Patrick Rothfuss
4  | Stephen King
5  | Terry Pratchet
6  | Neil Gaiman

### Books
id | title                | page_count 
--- | --- | ---
1  | The Wheel of Time    | 1000       
2  | The Knife Something  | 1000       
3  | Ender's Game         | 263        
4  | The Name of the Wind | 500        
5  | Good Omens           | 300        


### Book_authors
id | author_id | book_id
--- | --- | ---
1  | 1         | 1
2  | 5         | 5
3  | 6         | 5
4  | 2         | 3
5  | 3         | 4
6  | 1         | 2



Q: Write the SQL to find all books written by a certain author given their name
author = Robert Jordan

```sql
SELECT * 
FROM books
JOIN book_authors
ON books.id = book_authors.book_id
JOIN authors
ON book_authors.author_id = authors.id
WHERE authors.name = "Robert Jordan";
```


3. After completing the questions above, is there a rule you can determine about which table the foreign key belongs on given two associated tables?

    - child table => we want the foreign key to be on the belongs_to table (e.g., the books table)

# CRUD REVIEW
What are the four ways we can interact with data?

* Create  
SQL: `INSERT INTO books (title, page_count) VALUES ("Harry Potter", 399)`    
Ruby: `Book.new("Harry Potter", 399)`


* Read  
SQL: `SELECT * FROM books;`   
Ruby: `Book.all`


* Update  
SQL: `UPDATE books SET page_count = 300 WHERE title = "Harry Potter";`   
Ruby: `harry_potter.page_count = 300`


* Destroy  
SQL: `DELETE FROM books WHERE title = "Harry Potter";`   
Ruby: `harry_potter.delete`



## Lecture Notes

### What does an ORM do?
* provides a Ruby interface to our database 
* it connects our Ruby models/attributes/instances to tables/columns/rows in the database
* it translates data from database into Ruby objects

### How does it help us?
* scripting with Ruby
* more concise to call "Tweet.all" than to write out entire SQL query
* puts everything in a single language
* only have to work with a single language
* extensibility and maintainability
* swap out ORMs, keep your Ruby code



```ruby
class Tweet
  attr_accessor :message, :username
  attr_reader :id

  # @@all = []

  def self.all
    # @@all
    sql = <<-SQL
      SELECT *
      FROM tweets;
    SQL

    results = DB[:conn].execute(sql)

    # how do we turn this array of hashes into an array of Tweets

    results.map do |row|
      # Tweet.new({"message" => row["message"], "username" => row["username"]})
      Tweet.new(row) # why would this also work?
    end
  end

  def initialize(message, username)
    @message = pmessage
    @username = username

    @id = props["id"] # why might we want to add the id attribute?
  end

  def save
    # @@all << self
    # self

    username = self.username
    message = self.message

    #what SQL would we want to implement to save Tweet instances to the database
    
    # HEREDOC 
    sql = <<-SQL
      INSERT INTO tweets (username, message)
      VALUES (?, ?);
    SQL
    

    DB[:conn].execute(sql, username, message)
  end
  
  def update
    # what SQL could we implement to change the message of a tweet
  end

  def delete
    # what SQL could we implement to delete a row from the tweets table
  end
end
```