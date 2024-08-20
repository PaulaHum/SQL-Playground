# 🛝 SQL Playground: Building a TV Show Review Database 📺
![Gif Banner](https://github.com/user-attachments/assets/a7258f3b-ded9-48bc-aca0-e7d782916de8)


## Description:
Welcome to the **SQL Playground!** 🎢 This project is your chance to dive into the world of SQL, and flex those database muscles 💪. Whether you're a newbie just starting out or a seasoned pro looking to brush up on your skills, this open-source project has got you covered.

We're building a TV Show Review Database in MySQL, where you can track your favorite series and see what others think about them. The database will include tables for **reviewers**, **series**, and **reviews**, all connected in a **Many-to-Many relationship**, making it the perfect playground to test your SQL queries. 😎

With this project, you'll get hands-on experience:

* Creating and managing databases 🛠️
* Crafting complex queries 🚀
* Experimenting with relationships between tables 💡
* Learning to create views to simplify your work 💻

All you need is MySQL (Terminal or Workbench, your choice!), a sense of adventure, and a love for good TV shows. Let's get started!

## Project Steps: 
1. Set up a brand new Database using Terminal and if you wish, a MySQL Workbench
```
CREATE DATABASE tv_database;
```

2. Choose the newly created database
```
USE tv_database;
```

3. Let’s create 3 Tables and set Many to Many relationships between all of them
   
*  Table `reviewers` 
```
CREATE TABLE reviewers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL
);
```

* Table `series`
```
CREATE TABLE series (
    id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(100),
    released_year YEAR,
    genre VARCHAR(100)
);
```
* Table `reviews`
```
CREATE TABLE reviews (
    id INT PRIMARY KEY AUTO_INCREMENT,
    rating DECIMAL(2 , 1 ),
    series_id INT,
    reviewer_id INT,
    FOREIGN KEY (series_id) REFERENCES series (id),
    FOREIGN KEY (reviewer_id) REFERENCES reviewers (id)
);
```
4. Update tables with the following data:
   
* Insert data into the `series` table:
```
INSERT INTO series (title, released_year, genre) VALUES
     ('Twin Peaks', 1990, 'Drama'),
     ('The Mire', 2018, 'Drama'),
     ('True Detective', 2014, 'Drama'),
     ('Bojack Horseman', 2014, 'Animation'),
     ('Breaking Bad', 2008, 'Drama'),
     ('The Wire', 2002, 'Drama'),
     ('Fargo', 2014, 'Drama'),
     ('Modern Family', 2009, 'Comedy'),
     ('The Office', 2005, 'Comedy'),
     ('Futurama', 1999, 'Drama'),
     ('Graczyks', 1999, 'Comedy'),
     ('Honeymooners', 1998, 'Comedy'),
     ('Seinfeld', 1989, 'Comedy'),
     ('Stranger Things', 2016, 'Drama');
```
   <img width="362" alt="Bob's Burgers" src="https://github.com/user-attachments/assets/3e208d99-b705-4f11-9bc2-77d4172d40e6">

* Insert data into the `reviewers` table:
```
INSERT INTO reviewers (first_name, last_name) VALUES
     ('Krzysztof', 'Rutkowski'),
     ('Jaroslaw', 'Jakimowicz'),
     ('Kim', 'Kardashian'),
     ('Piotr', 'Jarzyna'),
     ('Colt', 'Steele'),
     ('Kanye', 'West'),
     ('Napoleon', 'Bonaparte')
```
<img width="203" alt="mysql SELECT  FROM reviewers;" src="https://github.com/user-attachments/assets/a3d0201f-345e-4311-adfe-c18a95c47b33">

* Insert data into the `reviews` table:
```
INSERT INTO reviews(series_id, reviewer_id, rating) VALUES
     (1,1,8.0),(1,2,7.5),(1,3,8.5),(1,4,7.7),(1,5,8.9),
     (2,1,8.1),(2,4,6.0),(2,3,8.0),(2,6,8.4),(2,5,9.9),
     (3,1,7.0),(3,6,7.5),(3,4,8.0),(3,3,7.1),(3,5,8.0),
     (4,1,7.5),(4,3,7.8),(4,4,8.3),(4,2,7.6),(4,5,8.5),
     (5,1,9.5),(5,3,9.0),(5,4,9.1),(5,2,9.3),(5,5,9.9),
     (6,2,6.5),(6,3,7.8),(6,4,8.8),(6,2,8.4),(6,5,9.1),
     (7,2,9.1),(7,5,9.7),
     (8,4,8.5),(8,2,7.8),(8,6,8.8),(8,5,9.3),
     (9,2,5.5),(9,3,6.8),(9,4,5.8),(9,6,4.3),(9,5,4.5),
     (10,5,9.9),
     (13,3,8.0),(13,4,7.2),
     (14,2,8.5),(14,3,8.9),(14,4,8.9);
```
<img width="265" alt="from reviews" src="https://github.com/user-attachments/assets/3da813ee-45dd-4e19-a8c7-ec87410465b9">

5. Let’s try writing some queries using our three tables
   
* Select Title and Rating from `series` and `reviews` tables
```
SELECT 
   title, rating
FROM
    series
        JOIN
    reviews ON series.id = reviews.series_id;
```
* Select Title and Rating (rounded up to 2 digits after coma) from `series` and `reviews` tables. Rating should appear as `avg_rating`.  Let’s group it by the Title and order by the avg_rating
```
SELECT 
    title, ROUND(AVG(rating), 2) AS avg_rating
FROM
    series
        JOIN
    reviews ON series.id = reviews.series_id
GROUP BY title
ORDER BY avg_rating;
```
* Show all titles which are unrated (have no rating/haven’t been reviewed)
```
SELECT 
    title AS unreviewed_series
FROM
    series
        LEFT JOIN
    reviews ON series.id = reviews.series_id
WHERE
    rating IS NULL;
```
_We may also do it other way around…_

```
SELECT 
    title AS unreviewed_series
FROM
    reviews
        RIGHT JOIN
    series ON series.id = reviews.series_id
WHERE
    rating IS NULL;
```
* Pull the data from all three tables: Title, Rating, and combination of first and last name of the reviewer
```
SELECT 
    title,
    rating,
    CONCAT(first_name, ' ', last_name) AS reviewer
FROM
    reviews
        INNER JOIN
    series ON reviews.series_id = series.id
        INNER JOIN
    reviewers ON reviews.reviewer_id = reviewers.id;
```
  <img width="526" alt="rating reviewer" src="https://github.com/user-attachments/assets/e49a9ead-360d-45be-8acc-1d4242a92c29">

* Let’s create a new view. By using this “virtual table” we will be able to simplify our queries moving forward

-- INSTEAD OF TYPING THIS QUERY ALL THE TIME...
```
SELECT
    title, released_year, genre, rating, first_name, last_name
FROM
    reviews
	JOIN
    series ON series.id = reviews.series_id
	JOIN
    reviewers ON reviewers.id = reviews.reviewer_id;
```

-- WE CAN CREATE A VIEW:

```
CREATE VIEW full_reviews AS
    SELECT
        title, released_year, genre, rating, first_name, last_name
    FROM
        reviews
            JOIN
        series ON series.id = reviews.series_id
            JOIN
        reviewers ON reviewers.id = reviews.reviewer_id;
```

-- NOW WE CAN TREAT THAT VIEW AS A VIRTUAL TABLE
```
SELECT * FROM full_reviews;
```
* you can find a new virtual table created - full_reviews

<img width="175" alt="(mysql SHOW TABLES;" src="https://github.com/user-attachments/assets/39407aea-03e7-48f2-8bbd-98eb75d94026">

7. Using the new view - full_reviews, select all titles with more than 1 review. Carry out two aggregate functions on rating field - Average rating and Count of rating
```
SELECT
   title, AVG(rating), COUNT(rating) AS review_count
FROM
   full_reviews
GROUP BY title
HAVING COUNT(rating) > 1;
```
8. Select title and average rating of each title, group it by title. At the end add the overall average using ROLL UP
```
SELECT
   title, AVG(rating)
FROM
   full_reviews
GROUP BY title WITH ROLLUP;
```
##
🎉 **And that's it!** You're all set to explore and practice SQL with this fun TV Show Review Database. Happy querying!

 
   







