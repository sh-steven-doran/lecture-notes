# SQL Review Lecture Notes

### Learning Goals

* [ ] Explain persistence and the need for using SQL
* [ ] Define SQL
* [ ] Explain the difference between SQLite3 and SQL
* [ ] Explore provided data through SQLite Browser
* [ ] Define CRUD
* [ ] Perform CRUD actions on a single table
* [ ] Perform CRUD actions across related tables

--------------------------

### Hook

- databases allow us to persist data
- SQL allows us to ask questions about our data
- CRUD are the core actions we can do with data
- this afternoon we'll see how to write some Ruby code that allows us to talk to our database

### Lecture Flow

__Intro__
I'm not super awesome at SQL but there's a good reason and you'll begin to see why tomorrow. __BUT__ - being awesome at SQL is a really great skill to have and having a team member who is really strong at SQL can be really clinch at times so if you're interested in this stuff I encourage you to keep at it.

1. What is persistence? How have we been persisting data so far in the apps we've been making?
    * why do we need persistence?
    * why is the current way we've been persisting data not awesome?
2. What can we do with data? - CRUD
    * Instagram example
3. What is a database? What have we been doing in our apps instead of using a database?
    * a bunch of tables
    * relational vs others
    * RDBMS
    * SQLite3 - a type of RDBMS
4. Introduce chinook.rb - have them pull the code
    * explore the data, install DB Browser Lite
    * talk about Primary Keys, Foreign Keys - how do these map to the way we were storing data?
5. SQL
    * what is SQL?
    * what's the difference between SQL and SQLite?
    * write some SQL queries - __THINK PAIR SHARE__
    * associate SQL exercises with CRUD actions

### What can I do with data?

CREATE


READ

* read
* evaluate
* admire

UPDATE

* update
* manipulate
* aggregate
* transform

DELETE / DESTROY

* delete

CRUD 

* Instagram
    * CREATE - posting a new picture
        * INSERT / CREATE
    * READ - scrolling through my feed
        * SELECT
    * UPDATE - tagging somebody after the fact, editing a comment
        * UPDATE / ALTER
    * DELETE - throwing that pic in the garbage
        * DELETE


### Challenges

1. Write the SQL to return all of the rows in the artists table?

READ

```sql
SELECT * 
FROM artists;
```

2. Write the SQL to select the artist with the name "Black Sabbath"

READ

```sql
SELECT artists.name FROM artists WHERE name = "Black Sabbath";

SELECT * FROM artists WHERE name LIKE "%black%";
```

3. Write the SQL to create a table named 'fans' with an autoincrementing ID that's a primary key and a name field of type text

CREATE

```sql
CREATE TABLE fans (
    id INTEGER PRIMARY KEY,
    name TEXT
);
```

4. Write the SQL to alter the fans table to have a artist_id column type integer?

UPDATE

```sql
ALTER TABLE fans
ADD COLUMN artist_id INTEGER;
```

5. Write the SQL to add yourself as a fan of the Black Eyed Peas? ArtistId **169**

CREATE

```sql
INSERT INTO fans (name, artist_id)
VALUES ("Dan", 169);
```

6. How would you update your name in the fans table to be your new name?

```sql
UPDATE fans
SET name = "New Steven"
WHERE name = "Dan";
```

7. Write the SQL to return fans that are not fans of the black eyed peas.

READ

```sql
SELECT * FROM fans
WHERE artist_id != 169;
```

```sql
SELECT * 
FROM fans
WHERE artist_id IS NOT 169;
```

7. Write the SQL to change a fan's artist.

UPDATE

```sql
 UPDATE fans 
 SET artist_id = 6 
 WHERE id = 1;
```

8. Write the SQL to display an artists name next to their album title

```sql
SELECT albums.title, artists.name
FROM albums
JOIN artists
ON artists.id = albums.artist_id;
```

9. Write the SQL to display artist name, album name and number of tracks on that album

```sql
SELECT artists.name, albums.title, count(*) track_count
FROM artists
JOIN albums ON artists.id = albums.artist_id
JOIN tracks ON albums.id = tracks.album_id
GROUP by tracks.album_id
ORDER BY artists.name;
```

10. Write the SQL to return the name of all of the artists in the 'Pop' Genre

```sql
SELECT artists.name
FROM artists
JOIN albums ON artists.id = albums.artist_id
JOIN tracks ON albums.id = tracks.album_id
JOIN genres ON genres.id = tracks.genre_id
WHERE genres.name = "Pop"
GROUP BY artists.name;
```



### BONUS (very hard)

11. I want to return the names of the artists and their number of rock tracks
    who play Rock music
    and have move than 30 tracks
    in order of the number of rock tracks that they have
    from greatest to least


