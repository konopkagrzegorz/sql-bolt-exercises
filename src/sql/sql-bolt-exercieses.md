## Exercise 1

1. Find the title of each film<br>
``SELECT title FROM movies;``<br>
---
2. Find the director of each film<br>
``SELECT director FROM movies;``<br>
---
3. Find the title and director of each film<br>
``SELECT title,director FROM movies;``<br>
---
4. Find the title and year of each film<br>
``SELECT title,year FROM movies;``<br>
---
5. Find all the information about each film<br>
``SELECT * FROM movies;``<br>
---
## Exercise 2

1. Find the movie with a row id of 6<br>
``SELECT * FROM movies WHERE movies.Id = 6;``<br>
---
2. Find the movies released in the years between 2000 and 2010<br>
``SELECT * FROM movies WHERE Year >= 2000 AND Year <=2010;``<br>
---
3. Find the movies not released in the years between 2000 and 2010<br>
``SELECT * FROM movies WHERE Year NOT BETWEEN 2000 AND 2010;``<br>
---
4. Find the first 5 Pixar movies and their release year<br>
``SELECT * FROM movies LIMIT 5;``<br>
   
## Exercise 3

1. Find all the Toy Story movies<br>
``SELECT * FROM movies WHERE Title LIKE "Toy Story%";``<br>
---
2. Find all the movies directed by John Lasseter<br>
``SELECT * FROM movies WHERE director = "John Lasseter";``<br>
---
3. Find all the movies (and director) not directed by John Lasseter<br>
``SELECT * FROM movies WHERE director != "John Lasseter";``<br>
---
4. Find all the WALL-* movies<br>
``SELECT * FROM movies WHERE title LIKE "WALL-_";;``<br>
---

## Exercise 4

1. List all directors of Pixar movies (alphabetically), without duplicates<br>
   ``SELECT DISTINCT director FROM movies ORDER BY director;``<br>
---
2. List the last four Pixar movies released (ordered from most recent to least)<br>
   ``SELECT title FROM movies ORDER BY year DESC LIMIT 4;``<br>
---
3. List the first five Pixar movies sorted alphabetically<br>
   ``SELECT * FROM movies ORDER BY title ASC LIMIT 5;``<br>
---
4. List the next five Pixar movies sorted alphabetically<br>
   ``SELECT * FROM movies ORDER BY title ASC LIMIT 5 OFFSET 5;``<br>
---
   