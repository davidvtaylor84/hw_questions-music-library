**Q1** - How has our Album class changed to represent moving from a one table design to a **ONE artist has MANY albums** relationship with two tables?
The album class now takes in an artist. Within this library, we can have a singular artist with many albums, but not vice versa. The artist class does not take in an album.
---

**Q2** - What does it mean for our `albums` table (specifically the `artist_name` column?)
In our Albums table, the artist_name references information stored in a separate table, the Artists table.
---

**Q3** - In a typical OO design we can imagine that an instance of the Artist class has a collection (perhaps a `list`) of Album instances. But here our models reflect the modelling in the database. So we cannot just evaluate `artist.albums`. How do we, in this application, get the list of `albums` for a particular artist?
We have to find the artist by ID and use that as the Value in the run_sql function. We put the result of this in a For Loop to find instances in which artist and the album details appear, and then return these albums(?).
---

**Q4** - In SQL terms when we denote an `album` as belonging to an `artist` we set the Foreign Key `artist_id`. But our Album class has an instance of an `Artist`. 

(a) This means when we write an instance of `Album` to the database we have to do what? (hint: line 9-10 `album_repository`)
We have to reference the artist by way of the artist id in the separate artist model/class.

(b) What is the 'opposite' thing we have to do when we get an `artist_id` back from the database in order to set the `artist` property on an `Album` instance? (hint: line 33-34 `album_repository`)
We have to create an artist variable that references its position in the database and use that in the artist field in the album class.

---
**Q5** - When we create an new instance of an Album we must already have created  ____________________ ? 
A reference in the table to the artist's ID in the album model(?)
---
**Q6** - With the following code -

```python
album_1 = Album("Roll With It", artist_1, "Rock")
album_repository.save(album_1)
album_1.genre = "Pop"
album_repository.update(album_1)
```
(a) The 4th line requires that the album_repository's `save` method has updated `album_1` with *something* from the database. What? 
The artist ID(?)

(b) What is the SQL command that means the database gives us that *something* when we `save` an album?
"INSERT INTO albums (title, artist_id, genre) VALUES (%s, %s, %s) RETURNING *"
---
**Q7** - In terms of Python types when we get data back from the database using `psycopg`'s `fetchall` method we get something equivalent to a _______ of _______.
an instance of a class
---
**Q8** - Our respositories take this data structure and if we have many rows (as in `select_all`) we _______ through it. We change each _______ into an ________
we Cursor through it(?). 

---
**Q9** - Even if we only have one row as a result (as in `select`) we still get back the same Python type. So to get access to the one row we care about we do what?


---
**Q10** - Sometimes our SQL queries are dynamic and we set up placeholders to insert `values` into. We do this using  ___________
answer: %s
---
**Q11** - The number of placeholders should be the same as the number of __________
Variables we are looking for according to the Class structure.
---
**Q12** - Why is it necessary to split this into two variables? (the placeholder `sql` string and a `values` list). Why do we not just create the SQL string like this?

```python
sql = "SELECT * FROM albums where id = " + id
```
The SQL speaks to the database whilst the values are mapped from the Python classes(?). These are separate operations brought together in this function.









