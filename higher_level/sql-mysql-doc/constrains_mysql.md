# MySQL Constrains
Limit the data that can be inserted into tables
### NOT NULL
No permite valores Nulos
```mysql
-- Creat table
CREATE TABLE users
(
	id INT,
	username VARCHAR(256) NOT NULL,
	City VARCHAR(55)
);
-- Insert record
INSERT INTO users VALUES (1, NULL, 'Lima')
-> Error: column username cannot be null
```

### UNIQUE
Ensures that all data are unique in a column
```mysql
-- Creat table
CREATE TABLE users
(
	id INT,
	username VARCHAR(256) NOT NULL UNIQUE,
	City VARCHAR(55)
);
-- Insert record
INSERT INTO users VALUES (1, 'PapiHaru', 'Lima')
-> Query OK
-- Insert record
INSERT INTO users VALUES (10, 'PapiHaru', 'Buenos Aires')
-> Error: Duplicate entry 'PapiHaru' for key 'username'
```

### PRIMARY KEY
- Cannot be NULL
- This constraint automatically has a UNIQUE constraint defined
- Use then to refer to table rows
- Become foreign keys in other tables
```mysql
-- Creat table
CREATE TABLE users
(
	id INT PRIMARY KEY,
	username VARCHAR(256) NOT NULL UNIQUE,
	City VARCHAR(55)
);

```
### FOREIGN KEY
- A foreign key in one table points to a primary key in aother table
```mysql
-- Create table referenced
CREATE TABLE users
(
	id INT PRIMARY KEY,
	username VARCHAR(256) NOT NULL UNIQUE,
	City VARCHAR(55)
);
-- Create table of reference
CREATE TABLE Contacts
(
	contactId INT PRIMARY KEY,
	firstname VARCHAR(256) NOT NULL,
	userId INT,
	address VARCHAR(256),
	FOREIGN KEY (userId) REFERENCES users(id)
);
```
### ENUM
Is a string object a value chosen a list of permitted values
```mysql
-- Create table
CREATE TABLE users
(
	id INT PRIMARY KEY,
	username VARCHAR(256) NOT NULL UNIQUE,
	beauty ENUM('High'. 'Average', 'Low'),
	City VARCHAR(55)
);
-- Insert record
INSERT INTO users VALUES (1, 'ElPepe', 'Average', NULL)
-> Query OK
-- Insert record
INSERT INTO users VALUES (5, 'Haru', 'SinDescripción', 'Arequipa')
-> Campo 'beauty' se completa con un empty string
```
### SET
A SET can have zero or more values, chosen from a list of permitted values
```mysql
-- Create table
CREATE TABLE users
(
	id INT PRIMARY KEY,
	username VARCHAR(256) NOT NULL UNIQUE,
	beauty ENUM('High'. 'Average', 'Low'),
	city VARCHAR(55),
	certificates SET('A1', 'A2', 'B1', 'C1')
);
-- Insert record
INSERT INTO users VALUES (1, 'Grillo', 'High', NULL, 'A1,B1');
-> Query OK
-- Insert record
INSERT INTO users VALUES (1, 'Grillo', 'High', NULL, 'A1,C1,P1');
-> Solo son insertados los certificados permitidos en el SET constraint
```
