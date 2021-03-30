# Booktown!

## clone repo and checkout into your own branch!

- Step 0. Take a look at the Schema file, click this link and draw an ERB. https://app.dbdesigner.net/designer/schema/new
  - you can submit a screenshot with your branch.
- Step 1. You should create a database then connect to it.
- Step 2. Once you've connected to the database, run the schema file from psql
- Step 3. Once you've run the schema file, run the seeds file (also from psql) to populate our database!

Tackle the questions below and record the queries for each problem in the solutions file.

1. get all books by mark lutz

 Programming Python
 Learning Python
(2 rows)

SELECT books.title FROM books JOIN authors ON books.authorId=authors.id WHERE authors.name ILIKE '%mark%';

2. get all books in the childrens books subject

SELECT books.title FROM books JOIN subjects ON subjects.id=books.subjectId WHERE subjects.name ILIKE '%children%';

 Franklin in the Dark
 Goodnight Moon
(2 rows)

3. get all subjects that a given author has written on
SELECT subjects.name
FROM subjects JOIN books ON subjects.id=books.subjectId
JOIN authors ON books.authorId=authors.id
WHERE authors.name ILIKE '%may%';

 Drama
(1 row)

4. get all authors that have written books on a given subject

SELECT authors.name
FROM subjects
JOIN books
ON subjects.id=books.subjectId
JOIN authors ON books.authorId=authors.id
WHERE subjects.name ILIKE '%hor%';

 King    Stephen
(1 row)

5. get all books by Hogarth Burne
SELECT books.title
FROM subjects JOIN books ON subjects.id=books.subjectId
JOIN authors ON books.authorId=authors.id
WHERE authors.name ILIKE '%bianco%';

 The Velveteen Rabbit
(1 row)

6. get the author of Little Women
SELECT authors.name
FROM subjects JOIN books ON subjects.id=books.subjectId
JOIN authors ON books.authorId=authors.id
WHERE books.title = 'Little Women';


 Alcott  Louisa May
(1 row)

7. Add yourself as a new author
INSERT INTO authors (name) VALUES ('Nat');

8. Add a new book by yourself and to any subject of your choosing
INSERT INTO books (title, authorId, subjectId) VALUES ('Nat's Diary', (SELECT id FROM authors WHERE name = 'Nat'), 9);

9. Now find that book authored by yourself and change it's author to King Stephen

UPDATE books SET authorId= (SELECT id FROM authors WHERE name = 'Lil Stephhh') WHERE title = 'Nat's Diary';

10. Get the subject of the 2001 Space Oddyssey
SELECT subjects.name FROM books JOIN subjects ON (books.subjectId = subjects.id) WHERE books.title = '2001: A Space Odyssey';

 Science Fiction
(1 row)

11. Get any book that starts has Science in it's subject
SELECT books.title FROM books JOIN subjects ON (books.subjectId = subjects.id) WHERE subjects.name ILIKE '%science%';

 Dune
 2001: A Space Odyssey
(2 rows)
