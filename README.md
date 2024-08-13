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

 ```CREATE DATABASE tv_database;```

2. Choose the newly created database

```USE tv_database;```

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
