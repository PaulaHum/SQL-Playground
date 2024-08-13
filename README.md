# SQL Playground: Building a TV Show Review Database 📺🎉

## Project Description:
Welcome to the **SQL Playground!** 🎢 This project is your chance to dive into the world of SQL, and flex those database muscles 💪. Whether you're a newbie just starting out or a seasoned pro looking to brush up on your skills, this open-source project has got you covered.

We're building a TV Show Review Database in MySQL, where you can track your favorite series and see what others think about them. The database will include tables for **reviewers**, **series**, and **reviews**, all connected in a **Many-to-Many relationship**, making it the perfect playground to test your SQL queries. 😎

With this project, you'll get hands-on experience:

* Creating and managing databases 🛠️
* Crafting complex queries 🚀
* Experimenting with relationships between tables 💡
* Learning to create views to simplify your work 💻

All you need is MySQL (Terminal or Workbench, your choice!), a sense of adventure, and a love for good TV shows. Let's get started!

<h3>Project Steps:</h3>
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
<img width="265" alt="from reviews" src="https://github.com/user-attachments/assets/8d7d0bb4-8efc-4d9a-a2c0-3b69c5f2b104">


