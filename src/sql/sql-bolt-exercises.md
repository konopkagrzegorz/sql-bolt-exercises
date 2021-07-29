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

## Review 1 (Exercise 5)

1. List all the Canadian cities and their populations<br>
   ``SELECT city,population FROM north_american_cities WHERE country = "Canada";``<br>
---
2. Order all the cities in the United States by their latitude from north to south<br>
   ``SELECT * FROM north_american_cities WHERE country = "United States" ORDER BY Latitude DESC;``<br>
---
3. List all the cities west of Chicago, ordered from west to east<br>
   ``SELECT * FROM north_american_cities WHERE longitude < -87.629798 ORDER BY longitude;``<br>
---
4. List the two largest cities in Mexico (by population)<br>
   ``SELECT * FROM north_american_cities WHERE country = "Mexico" ORDER BY population DESC LIMIT 2;``<br>
---
5. List the third and fourth largest cities (by population) in the United States and their population<br>
   ``SELECT * FROM north_american_cities WHERE country = "United States" ORDER BY population DESC LIMIT 2 OFFSET 2;``<br>
---
## Exercise 6

1. Find the domestic and international sales for each movie<br>
   ``SELECT Movies.title, Boxoffice.domestic_sales, Boxoffice.international_sales FROM Boxoffice INNER JOIN movies ON Boxoffice.Movie_id = Movies.Id;``<br>
---
2. Show the sales numbers for each movie that did better internationally rather than domestically<br>
   ``SELECT Movies.title, Boxoffice.domestic_sales, Boxoffice.international_sales FROM Boxoffice INNER JOIN movies ON Boxoffice.Movie_id = Movies.Id WHERE domestic_sales < international_sales;``<br>
---
3. List all the movies by their ratings in descending order<br>
   ``SELECT title FROM movies INNER JOIN boxoffice ON Boxoffice.Movie_id = Movies.Id ORDER BY rating DESC;``<br>
---

## Exercise 7

1. Find the list of all buildings that have employees<br>
   ``SELECT DISTINCT building FROM employees;``<br>
---
2. Find the list of all buildings and their capacity<br>
   ``SELECT building_name,capacity FROM buildings;``<br>
---
3. List all buildings and the distinct employee roles in each building (including empty buildings)<br>
   ``SELECT DISTINCT building_name, employees.role FROM buildings LEFT JOIN employees ON buildings.building_name = employees.building;``<br>
---

## Exercise 8

1. Find the name and role of all employees who have not been assigned to a building<br>
   ``SELECT name, role FROM employees WHERE building IS NULL;``<br>
---
2. Find the names of the buildings that hold no employees<br>
   ``SELECT building_name FROM buildings LEFT JOIN employees ON buildings.building_name = employees.building WHERE employees.building IS NULL;``<br>
---

## Exercise 9

1. List all movies and their combined sales in millions of dollars<br>
   ``SELECT title, (domestic_sales + international_sales)/1000000 AS sales FROM movies INNER JOIN boxoffice ON movies.id = boxoffice.movie_id;``<br>
---
2. List all movies and their ratings in percent<br>
   ``SELECT title, rating*10 AS ratings_precent FROM movies INNER JOIN boxoffice ON movies.id = boxoffice.movie_id;``<br>
---
3. List all movies that were released on even number years<br>
   ``SELECT * FROM movies INNER JOIN boxoffice ON movies.id = boxoffice.movie_id WHERE movies.year % 2 = 0;``<br>
---

## Exercise 10

1. Find the longest time that an employee has been at the studio<br>
   ``SELECT MAX(years_employed) FROM employees;``<br>
---
2. For each role, find the average number of years employed by employees in that role<br>
   ``SELECT role, AVG(years_employed) FROM employees GROUP BY role;``<br>
---
3. Find the total number of employee years worked in each building<br>
   ``SELECT building,SUM(years_employed) FROM employees GROUP BY building;``<br>
---

## Exercise 11

1. Find the number of Artists in the studio (without a HAVING clause)<br>
   ``SELECT COUNT(*) FROM employees WHERE ROLE = "Artist";``<br>
---
2. Find the number of Employees of each role in the studio<br>
   ``SELECT role,COUNT(*) AS number FROM employees GROUP BY role;``<br>
---
3. Find the total number of years employed by all Engineers<br>
   ``SELECT role, SUM(years_employed) AS number FROM employees GROUP BY role HAVING role = "Engineer";``<br>
---

## Exercise 12

1. Find the number of movies each director has directed<br>
   ``SELECT director,COUNT(*) AS number FROM movies GROUP BY director;``<br>
---
2. Find the total domestic and international sales that can be attributed to each director<br>
   ``SELECT role,COUNT(*) AS number FROM employees GROUP BY role;``<br>
---

## Exercise 13

1. Add the studio's new production, Toy Story 4 to the list of movies (you can use any director)<br>
   ``INSERT INTO movies(title,director,year,length_minutes) VALUES("Toy Story 4", "John Lasseter", 2020, 90);``<br>
---
2. Toy Story 4 has been released to critical acclaim!<br>It had a rating of 8.7, and made 340 million domestically and 270 million internationally.<br>Add the record to the BoxOffice table.<br>
   ``INSERT INTO boxoffice (movie_id,rating,domestic_sales,international_sales) VALUES (15,8.7,340000000,270000000);``<br>
---

## Exercise 14

1. The director for A Bug's Life is incorrect, it was actually directed by John Lasseter<br>
   ``UPDATE movies SET director = "John Lasseter" WHERE title = "A Bug's Life";``<br>
---
2. The year that Toy Story 2 was released is incorrect, it was actually released in 1999<br>
   ``UPDATE movies SET year = 1999 WHERE title = "Toy Story 2";``<br>
---
3. Both the title and director for Toy Story 8 is incorrect! The title should be "Toy Story 3" and it was directed by Lee Unkrich<br>
   ``UPDATE movies SET director = "Lee Unkrich", title = "Toy Story 3" WHERE title = "Toy Story 8";``<br>
---

## Exercise 15

1. This database is getting too big, lets remove all movies that were released before 2005.<br>
   ``DELETE FROM movies WHERE year < 2005;``<br>
---
2. Andrew Stanton has also left the studio, so please remove all movies directed by him.<br>
   ``DELETE FROM movies WHERE director = "Andrew Stanton";``<br>
---

## Exercise 16

1. Create a new table named Database with the following columns:
   * Name A string (text) describing the name of the database
   * Version A number (floating point) of the latest version of this database
   * Download_count An integer count of the number of times this database was downloaded<br>
   
This table has no constraints.<br>
   ``DCREATE table Database(id INTEGER PRIMMARY KEY, Name TEXT, Version DOUBLE, Download_count INTEGER);``<br>
---

## Exercise 17

1. Add a column named Aspect_ratio with a FLOAT data type to store the aspect-ratio each movie was released in.<br>
   ``ALTER TABLE movies ADD column aspect_ratio FLOAT;``<br>
---
2. Add another column named Language with a TEXT data type to store the language that the movie was released in. Ensure that the default for this language is English.<br>
   ``ALTER TABLE movies ADD column Language TEXT default "English";``<br>
---

## Exercise 18

1. We've sadly reached the end of our lessons, lets clean up by removing the Movies table<br>
   ``DROP TABLE movies;``<br>
---
2. And drop the BoxOffice table as well<br>
   ``DROP TABLE BoxOffice;``<br>
---