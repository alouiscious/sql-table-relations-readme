[21:28:45] (master) sql-table-relations-readme
// ♥ sqlite3 pets_database.db
SQLite version 3.24.0 2018-06-04 14:10:15
Enter ".help" for usage hints.
sqlite> CREATE TABLE cats (id INTEGE              R sqlite> CREATE TABLE cats (id INTEGER PRIMARY KEY, name TEXT, ageINT, breed TEXT);
sqlite> INSERT INTO cats (name, age, breed) VALUES ("Maru", 3, "Scottish Fold");
Error: table cats has no column named age
sqlite> .schema
CREATE TABLE cats (id INTEGERER PRIMARY KEY, name TEXT, ageINT, breed TEXT);
sqlite> DROP TABLE cats
   ...> ;
sqlite> CREATE TABLE cats (
   ...> id INTEGER PRIMARY KEY,                           ...> name TEXT,
   ...> age INTEGER,
   ...> breed TEXT);
sqlite> .schema
CREATE TABLE cats (
id INTEGER PRIMARY KEY,
name TEXT,
age INTEGER,
breed TEXT);
sqlite> INSERT INTO cats (name, age, breed)
   ...> VALUES ("Maru", 3, "Scottish Fold");
sqlite> INSERT INTO cats (name, age, breed)
   ...> VALUES ("Hana", 1, "Tabby");
sqlite> CREATE TABLE owners (id INTEGER PRIMARY KEY, name TEXT);
sqlite> ALTER TABLE cats ADD COLUMN owner_id INT;
sqlite> .schema cats
CREATE TABLE cats (
id INTEGER PRIMARY KEY,
name TEXT,
age INTEGER,
breed TEXT, owner_id INT);
sqlite> .schema owners
CREATE TABLE owners (id INTEGER PRIMARY KEY, name TEXT);
sqlite> INSERT INTO owners (name) VALUES ("mugumogu");
sqlite> SELECT * FROM owners;
1|mugumogu
sqlite> UPDATE cats SET owner_id = 1 WHERE name = "Maru"
   ...> ;
sqlite> UPDATE cats SET owner_id = 1 WHERE name = "Hana";
sqlite> SELECT * FROM cats WHERE owner_id = 1;
1|Maru|3|Scottish Fold|1
2|Hana|1|Tabby|1
sqlite> DROP TABLE owners
   ...> ;
sqlite> DROP TABLE cats;
sqlite> CREATE TABLE cats (
   ...> id INTEGER PRIMARY KEY,
   ...> name TEXT,
   ...> age INTEGER,
   ...> breed TEXT,
   ...> owner_id INTEGER);
sqlite> CREATE TABLE owners (id INTEGER PRIMARY KEY, name TEXT);
sqlite> INSERT INTO owners (name) VALUES ("mugumogu");
sqlite> INSERT INTO owners (name) VALUES ("Sophie");
sqlite> INSERT INTO cats (name, age, breed, owner_id) VALUES ("Maru", 3, "Scottish Fold", 1);
sqlite> INSERT INTO cats (name, age, breed, owner_id) VALUES ("Hana", 3, "Tabby", 1);
sqlite> INSERT INTO cats (name, age, breed, owner_id) VALUES ("Nona", 4, "Tortoiseshell", 2);
sqlite> INSERT INTO cats (name, age, breed) VALUES ("Lil' Bub", 2, "perma-kitten");
sqlite> .schema cats
CREATE TABLE cats (
id INTEGER PRIMARY KEY,
name TEXT,
age INTEGER,
breed TEXT,
owner_id INTEGER);
sqlite> SELECT * FROM cats;
1|Maru|3|Scottish Fold|1
2|Hana|3|Tabby|1
3|Nona|4|Tortoiseshell|2
4|Lil' Bub|2|perma-kitten|
sqlite> SELECT * FROM owners;
1|mugumogu
2|Sophie
sqlite> .headers on
sqlite> .mode column
sqlite> SELECT * FROM owners;
id          name      
----------  ----------
1           mugumogu  
2           Sophie    
sqlite> SELECT * FROM cats;
id          name        age         breed          owner_id  
----------  ----------  ----------  -------------  ----------
1           Maru        3           Scottish Fold  1         
2           Hana        3           Tabby          1         
3           Nona        4           Tortoiseshell  2         
4           Lil' Bub    2           perma-kitten             
sqlite> SELECT * FROM cats WHERE owner_id = 2;
id          name        age         breed          owner_id  
----------  ----------  ----------  -------------  ----------
3           Nona        4           Tortoiseshell  2         
sqlite> SELECT Cats.name, Cats.breed, Owners.name FROM Cats INNER JOIN Owners ON Cats.owner_id = Owners.id;
name        breed          name      
----------  -------------  ----------
Maru        Scottish Fold  mugumogu  
Hana        Tabby          mugumogu  
Nona        Tortoiseshell  Sophie    
sqlite> SELECT Cats.name, Cats.breed, Owners.name AS "owner_name" FROM Cats INNE
name        breed          owner_name
----------  -------------  ----------
Maru        Scottish Fold  mugumogu  
Hana        Tabby          mugumogu  
Nona        Tortoiseshell  Sophie    
sqlite> SELECT Cats.name AS "cat_name", Cats.breed, Owners.name AS "owner_name" FROM Cats INNER JOIN Owners ON Cats.owner_id = Owners.id;
cat_name    breed          owner_name
----------  -------------  ----------
Maru        Scottish Fold  mugumogu  
Hana        Tabby          mugumogu  
Nona        Tortoiseshell  Sophie    
sqlite> SELECT Cats.name AS "cat_name". Cats.breed, Owners.name AS owner_name FROM Cats LEFT OUTER JOIN Owners ON Cats.owner_id = Owners_id;
Error: near ".": syntax error
sqlite> SELECT Cats.name AS "cat_name", Cats.breed, Owners.name AS owner_name FROM Cats LEFT OUTER JOIN Owners ON Cats.owner_id = Owners_id;
Error: no such column: Owners_id
sqlite> SELECT Cats.name AS "cat_name", Cats.breed, Owners.name AS owner_name FROM Cats LEFT OUTER JOIN Owners ON Cats.owner_id = Owners.id;
cat_name    breed          owner_name
----------  -------------  ----------
Maru        Scottish Fold  mugumogu  
Hana        Tabby          mugumogu  
Nona        Tortoiseshell  Sophie    
Lil' Bub    perma-kitten             
sqlite> INSERT INTO owner (name) VALUES ("Penny");
Error: no such table: owner
sqlite> INSERT INTO owners (name) VALUES ("Penny");
sqlite> 