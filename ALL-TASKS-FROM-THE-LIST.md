# sqlbolt-exercises-for-mate-academy
### Lesson 2. Task 2 
- #### Find the movies released in the years between 2000 and 2010
```sql
SELECT Title 
  FROM movies 
    Where year >= 2000 AND year <=2010
```
### Lesson 3. Task 4
- #### Find all the WALL-* movies
```sql
SELECT * 
  FROM movies 
    Where Title LIKE "%WALL%"
```
### Lesson 4. Task 1
- #### List all directors of Pixar movies (alphabetically), without duplicates
```sql
SELECT DISTINCT Director 
  FROM movies
    ORDER BY Director
```
### Lesson 5. Task 3
- #### List all the cities west of Chicago, ordered from west to east
```sql
SELECT *
  FROM north_american_cities
    Where Longitude < -87.629798
      ORDER BY Longitude
```
### Lesson 5. Task 4
- #### List the two largest cities in Mexico (by population)
```sql
SELECT *
  FROM north_american_cities
    Where Country = "Mexico"
      ORDER BY Population DESC
        LIMIT 2
```
### Lesson 5. Task 5
- #### List the third and fourth largest cities (by population) in the United States and their population
```sql
SELECT *
  FROM north_american_cities
    Where Country = "United States"
      ORDER BY Population DESC 
        LIMIT 2 OFFSET 2
```
### Lesson 6. Task 2
- #### Show the sales numbers for each movie that did better internationally rather than domestically
```sql
SELECT title,international_sales, domestic_sales
  FROM movies
    INNER JOIN boxoffice
      ON movies.id = boxoffice.movie_id
        WHERE international_sales > domestic_sales
```
### Lesson 6. Task 3
- #### List all the movies by their ratings in descending order
```sql
SELECT title, rating
  FROM movies
    INNER JOIN boxoffice
      ON movies.id = boxoffice.movie_id
        ORDER BY rating DESC
```
### Lesson 7. Task 3
- #### List all buildings and the distinct employee roles in each building (including empty buildings)
```sql
SELECT DISTINCT building_name, role
  FROM buildings
    LEFT JOIN employees
      ON building_name = employees.building;
```
### Lesson 8. Task 1
- #### Find the name and role of all employees who have not been assigned to a building
```sql
SELECT *
  FROM employees
    LEFT JOIN buildings
      ON employees.building = buildings.building_name
        WHERE building IS NULL;
```
### Lesson 8. Task 2
- #### Find the names of the buildings that hold no employees
```sql
SELECT building_name
  FROM buildings
  LEFT JOIN employees
    ON employees.building = buildings.building_name
      WHERE building IS NULL;
```
### Lesson 9. Task 2
- #### List all movies and their ratings in percent
```sql
SELECT title,
  rating * 10 AS percent
    FROM boxoffice
      LEFT JOIN movies
        ON movies.id = boxoffice.movie_id;
```
### Lesson 9. Task 3
- #### List all movies that were released on even number years
```sql
SELECT title
  FROM movies
    WHERE year % 2 = 0;
```
### Lesson 10. Task 2
- #### For each role, find the average number of years employed by employees in that role
```sql
SELECT Role, AVG(Years_employed)
  FROM employees
    GROUP BY Role;
```
### Lesson 11. Task 2
- #### Find the number of Employees of each role in the studio
```sql 
SELECT Role,COUNT()
  FROM employees
    GROUP BY Role;
```
### Lesson 11. Task 3.
- #### Find the total number of years employed by all Engineers
```sql
SELECT role, SUM(years_employed) 
  FROM employees 
    WHERE role = "Engineer";
```
### Lesson 12. Task 2
- #### Find the total domestic and international sales that can be attributed to each director
```sql
SELECT Director,SUM(domestic_sales) + SUM(international_sales)
  FROM movies
    INNER JOIN boxoffice 
      ON movies.Id = boxoffice.movie_id
        GROUP BY Director
```
### Lesson 13. Task 1
- #### Add the studio’s new production, Toy Story 4 to the list of movies (you can use any director)
```sql
INSERT INTO movies (title, director, year, length_minutes) 
  VALUES ('Toy Story 4', 'John Lasseter', 2019, 123);
```
### Lesson 14. Task 3
- #### Both the title and director for Toy Story 8 is incorrect! The title should be “Toy Story 3” and it was directed by Lee Unkrich
```sql
UPDATE movies
  SET Title = "Toy Story 3", 
    Director = "Lee Unkrich"
      WHERE Title = "Toy Story 8";
```
### Lesson 15. Task 2
- #### Andrew Stanton has also left the studio, so please remove all movies directed by him.
```sql
DELETE FROM movies
  WHERE Director = "Andrew Stanton";
```
### Lesson 16. Task 1
- #### Create a new table named Database with the following columns:
1. ##### Name A string (text) describing the name of the database
2. ##### Version A number (floating point) of the latest version of this database
3. ##### Download_count An integer count of the number of times this database was downloaded
```sql 
CREATE TABLE Database (
    Name TEXT,
      Version DOUBLE,
        Download_count INTEGER
);
```
### Lesson 17. Task 2
- #### Add another column named Language with a TEXT data type to store the language that the movie was released in. Ensure that the default for this language is 
- #### English.
```sql
ALTER TABLE movies 
  ADD Language TEXT DEFAULT "English"; 
```
### Lesson 18. Task 2
- #### And drop the BoxOffice table as well
```sql
DROP TABLE IF EXISTS boxoffice;
```
