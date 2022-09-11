# SQL_Queries_Basic
-- CODING COURSE BY GIRAFFE ACADEMY 
-- BASICS OF SQL

SELECT * FROM student;

DROP TABLE student;

ALTER TABLE student ADD gpa DECIMAL(3, 2);

ALTER TABLE student DROP COLUMN gpa;

CREATE TABLE student (
      student_id INT PRIMARY KEY,
      name VARCHAR(20),
      major VARCHAR(20)
);

DESCRIBE student;

INSERT INTO student 
VALUES(1, 'Jack', 'Biology');

INSERT INTO student (student_id, name, major)
VAlUES(1, 'Jack', 'Biology'),
    (2, 'Kate', 'Sociology'),
    (3, 'Claire', 'English'),
    (4, 'Jack', 'Chemistry'),
    (5, 'Mike', 'Computer Science');

CREATE TABLE student (
      student_id INT,
      name VARCHAR(20) NOT NULL,
      major VARCHAR(20) UNIQUE,
      PRIMARY KEY(student_id) 
);

INSERT INTO student (student_id, name, major)
VAlUES(1, 'Jack', 'Biology'),
    (2, NULL, 'Sociology'),
    (3, 'Claire', 'English'),
    (4, 'Jack', 'Chemistry'),
    (5, 'Mike', 'Computer Science');

INSERT INTO student (student_id, name, major)
VAlUES(1, 'Jack', 'Biology'),
    (2, NULL, 'Sociology'),
    (3, 'Claire', 'English'),
    (4, 'Jack', 'Biology'),
    (5, 'Mike', 'Computer Science');

CREATE TABLE student (
      student_id INT,
      name VARCHAR(20) ,
      major VARCHAR(20) DEFAULT 'undecided',
      PRIMARY KEY(student_id) 
);

INSERT INTO student (student_id, name)
VALUES (1, 'Jack');

CREATE TABLE student (
    student_id INT AUTO_INCREMENT,
    name VARCHAR(20),
    major VARCHAR(10),
    PRIMARY KEY(student_id)
);

INSERT INTO student (name, major)
VALUES ('Jack', 'Sociology'),
       ('Kate', 'Biology');


CREATE TABLE student (
    student_id INT AUTO_INCREMENT,
    name VARCHAR(20),
    major VARCHAR(20),
    PRIMARY KEY(student_id)
);

INSERT INTO student (name, major)
VALUES ('Jack', 'Biology'),
       ('Kate', 'Sociology'),
       ('Claire', 'Chemistry'),
       ('Jack', 'Biology'),
       ('Mike', 'Computer Science');

UPDATE student
SET major = 'English'
WHERE student_id = '4';

UPDATE student
SET major = 'Chemistry'
WHERE name = 'Claire';

DELETE FROM student
WHERE student_id = '5';

DROP TABLE student;

-- CORPORATE EXCERCISE CREATING COMPANY DATABASE

CREATE TABLE Employee (
    employee_id INT PRIMARY KEY,
    first_name VARCHAR(10),
    last_name  VARCHAR(10),
    birth_date DATE,
    sex VARCHAR(1),
    salary INT,
    supervisor_id INT,
    branch_id INT
      );

CREATE TABLE Branch (
    branch_id INT PRIMARY KEY,
    branch_name VARCHAR(10),
    manager_id INT,
    manager_start_date DATE,
    FOREIGN KEY(manager_id) REFERENCES Employee(employee_id) ON DELETE SET NULL
);

CREATE TABLE Client (
    client_id INT PRIMARY KEY,
    client_name VARCHAR(20),
    branch_id INT,
    FOREIGN KEY (branch_id) REFERENCES Branch(branch_id) ON DELETE SET NULL
    );

CREATE TABLE Works_With(
    employee_id INT,
    client_id INT,
    total_sales INT,
    PRIMARY KEY (employee_id, client_id),
    FOREIGN KEY (employee_id) REFERENCES Employee(employee_id) ON DELETE CASCADE,
    FOREIGN KEY (client_id) REFERENCES Client(client_id) ON DELETE CASCADE
);

CREATE TABLE Branch_Supplier (
 branch_id INT,
 supplier_name VARCHAR(20),
 supply_type VARCHAR(20),
 FOREIGN KEY(branch_id) REFERENCES Branch(branch_id) ON DELETE CASCADE
);

ALTER TABLE Employee
ADD FOREIGN KEY(supervisor_id)
REFERENCES Employee(employee_id)
ON DELETE SET NULL ;

ALTER TABLE Employee
ADD FOREIGN KEY (branch_id)
REFERENCES Branch(branch_id)
ON DELETE SET NULL ;

-- Employee
INSERT INTO Employee (employee_id, first_name, last_name, birth_date, sex, salary, supervisor_id, branch_id)
VALUES (100, 'David', 'Wallace', '1967-11-17', 'M', 250000, NULL, NULL),
       (101, 'Jan', 'Levinson', '1961-05-11', 'F', 110000, 100, NULL),
       (102, 'Michael', 'Scott', '1964-03-15', 'M', 75000, 100, NULL),
       (103, 'Angela', 'Martin', '1971-06-25', 'F', 63000, 102, NULL),
       (104, 'Kelly', 'Kapoor', '1980-02-05', 'F', 55000, 102, NULL),
       (105, 'Stanley', 'Hudson', '1958-02-19', 'M', 69000, 102, NULL),
       (106, 'Josh', 'Porter', '1969-09-05', 'M', 78000, 100, NULL),
       (107, 'Andy', 'Bernard', '1973-07-22', 'M', 65000, 106, NULL),
       (108, 'Jim', 'Halpert', '1978-10-01', 'M', 71000, 106, NULL);
       
-- Branch
INSERT INTO Branch
VALUES (1, 'Corporate', 100, '2006-02-09'),
       (2, 'Scranton', 102, '1992-04-06'),
       (3, 'Stamford', 106, '1998-02-13');

-- Corporate Branch
UPDATE Employee
SET branch_id = 1
WHERE employee_id <= 101;

-- Scranton Branch 
UPDATE Employee
SET branch_id = 2
WHERE employee_id BETWEEN 102 AND 105;

-- Stamford Branch 
UPDATE Employee
SET branch_id = 3
WHERE employee_id >= 106;

-- Branch Supllier
INSERT INTO Branch_Supplier 
VALUES(2, 'Hammer Mill', 'Paper'),
      (2, 'Uni-Ball', 'Writing Utensils'),
      (3, 'Patriot Paper', 'Paper'),
      (2, 'J.T. Forms & Labels', 'Custom Forms'),
      (3, 'Uni-Ball', 'Writing Utensils'),
      (3, 'Hammer Mill', 'Paper'),
      (3, 'Stamford Lables', 'Custom Forms');

-- Client
INSERT INTO Client
VALUES(400, 'Dunmore Highschool', 2),
      (401, 'Lackwana Country', 2),
      (402, 'FedEx', 3),
      (403, 'John Daly Law, LLC', 3),
      (404, 'Scranton Whitepages', 2),
      (405, 'Times Newspaper', 3),
      (406, 'FedEx', 2);

-- Works_With
INSERT INTO Works_With
VALUES(105, 400, 55000),
      (102, 401, 267000),
      (108, 402, 22500),
      (107, 403, 5000),
      (108, 403, 12000),
      (105, 404, 33000),
      (107, 405, 26000),
      (102, 406, 15000),
      (105, 406, 130000);
      
DROP TABLE Employee, Branch, Client, Works_With, Branch_Supplier;

SELECT * FROM Employee;

SELECT * FROM Branch;

SELECT * FROM Branch_Supplier;

SELECT * FROM Client;

SELECT * FROM Works_With;

SELECT DISTINCT sex FROM Employee;

SELECT * FROM Employee ORDER BY salary;

SELECT * FROM Employee LIMIT 5;

SELECT COUNT(employee_id)
FROM Employee;

SELECT COUNT (employee_id)
FROM Employee
WHERE sex = 'F' AND birth_date >= '1971-01-01';

SELECT AVG (salary)
FROM Employee
WHERE sex = 'M';

SELECT SUM(salary)
FROM Employee;

SELECT COUNT(sex), sex
FROM Employee
GROUP BY sex;

SELECT SUM(total_sales), employee_id
FROM Works_With
GROUP BY employee_id;

SELECT *
FROM Client
WHERE client_name LIKE '%LLC%';

SELECT *
FROM Branch_Supplier
WHERE supplier_name LIKE '%Label%';

UPDATE Branch_Supplier
SET supplier_name = 'Stamford Labels'
WHERE branch_id = 3 AND supply_type = 'Custom Forms';

SELECT *
FROM Employee
WHERE birth_date LIKE '%10%';

SELECT *
FROM Employee
WHERE birth_date LIKE '____-10%';

SELECT *
FROM Employee
WHERE birth_date LIKE '%02%';

SELECT *
FROM Client
WHERE client_name LIKE '%School%';

SELECT first_name FROM Employee
UNION
SELECT branch_name FROM Branch;

SELECT E.employee_id, E.first_name, E.last_name, B.branch_id, B.branch_name, E.salary
FROM Employee E
JOIN Branch B
ON E.employee_id = B.manager_id;

SELECT E.first_name, E.last_name, WW.total_sales, C.client_name
FROM Works_With WW
JOIN Employee E
USING (employee_id)
JOIN Client C
USING (client_id)
WHERE WW.total_sales > 30000;

SELECT E.first_name, E.last_name
FROM Employee E
WHERE E.employee_id IN (
    SELECT WW.employee_id
FROM Works_With WW
WHERE WW.total_sales > 30000);

SELECT C.client_name
FROM client C
WHERE branch_id IN(
SELECT B.branch_id
FROM Branch B
WHERE B.manager_id = 102);

-- CREATE TABLE Branch (
  --  branch_id INT PRIMARY KEY,
  --  branch_name VARCHAR(10),
  --  manager_id INT,
  --  manager_start_date DATE,
  --  FOREIGN KEY(manager_id) REFERENCES Employee(employee_id) ON DELETE SET NULL);

DELETE FROM Employee
WHERE employee_id = 102;

-- CREATE TABLE Branch_Supplier (
-- branch_id INT,
-- supplier_name VARCHAR(20),
-- supply_type VARCHAR(20),
-- FOREIGN KEY(branch_id) REFERENCES Branch(branch_id) ON DELETE CASCADE);

DELETE FROM Branch
WHERE branch_id = 2;

CREATE TABLE employee_trigger(
    message VARCHAR(100)
);

DELIMITER $$
CREATE 
TRIGGER New_Employee_trigger BEFORE INSERT
ON Employee
FOR EACH ROW BEGIN
INSERT INTO employee_trigger VALUES('Added New Employee');
END $$
DELIMITER ;

INSERT INTO Employee
VALUES (109, 'Oscar', 'Martinez', '1968-02-19', 'M', 69000, 106, 3);

SELECT * FROM employee_trigger;

DELIMITER $$
CREATE TRIGGER New_Employee_First_trigger 
BEFORE INSERT 
ON Employee 
FOR EACH ROW BEGIN
INSERT INTO employee_trigger VALUES (NEW.first_name);
END $$
DELIMITER ;

INSERT INTO Employee
VALUES (110, 'Kevin', 'Malone', '1978-05-28', 'M', 11000, 106, 3);

SELECT * FROM employee_trigger;

DELIMITER $$
CREATE TRIGGER sex_identifying_trigger 
BEFORE INSERT 
ON Employee 
FOR EACH ROW BEGIN
IF NEW.sex = 'M' THEN
INSERT INTO employee_trigger VALUES ('Added Male Employee');
ELSEIF NEW.sex = 'F' THEN
INSERT INTO employee_trigger VALUES ('Added Female Employee');
ELSE 
INSERT INTO employee_trigger VALUES ('Added Other Employee');
END IF;
END $$
DELIMITER ;

INSERT INTO Employee
VALUES (111, 'Pam', 'Beesly', '1988-07-08', 'F', 45000, 106, 3);

SELECT * FROM employee_trigger;

DELIMITER $$
CREATE TRIGGER sex_identifying_trigger 
BEFORE UPDATE;

DELIMITER $$
CREATE TRIGGER sex_identifying_trigger 
BEFORE DELETE;

DELIMITER $$
CREATE TRIGGER sex_identifying_trigger 
AFTER UPDATE;

DELIMITER $$
CREATE TRIGGER sex_identifying_trigger
AFTER DELETE;

DROP TRIGGER New_Employee_trigger;

DROP TRIGGER New_Employee_First_trigger;

DROP TRIGGER sex_identifying_trigger;
