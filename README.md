# TASK- 7 CREATING VIEWS
# Using Database 'COMPANY' and two tables 'EMPLOYEES' and 'DEPARTMENTS' for creating 'VIEWS' by using MySQL Workbench.

CREATE DATABASE COMPANY;
USE COMPANY;

CREATE TABLE Employees(
employee_id INT PRIMARY KEY NOT NULL,
first_name VARCHAR(50),
last_name VARCHAR(50),
category VARCHAR(50),
department VARCHAR(50),
salary FLOAT DEFAULT 20000,
joining_date DATE
);

INSERT INTO Employees VALUES
(1, 'John', 'Smith', 'Full Time', 'Engineering', 80000, '2021-01-29'),
(2, 'Alice', 'Johnson', 'Part Time', 'HR', 30000.00, '2021-05-12'),
(3, 'Bob', 'Brown', 'Full Time', 'Finance', 90000, '2021-01-29'),
(4, 'Carol', 'White', 'Contract', 'IT', 75000, '2021-01-01'),
(5, 'David', 'Green', 'Full Time', 'Engineering', 85000, '2022-01-13'),
(6, 'Emma', 'Blue', 'Part Time', 'Finance', 32000, '2023-01-01'),
(7, 'Frank', 'Black', 'Full Time', 'HR', 60000, '2024-05-05'),
(8, 'Grace', 'Grey', 'Full Time', 'Marketing', 70000, '2021-01-22'),
(9, 'Henry', 'Red', 'Contract', 'Sales', 95000, '2021-01-08'),
(10, 'Ivy', 'Yellow', 'Full Time', 'Marketing', 28000, '2025-01-03');

SELECT * FROM Employees;

Employees table:

<img width="639" height="315" alt="image" src="https://github.com/user-attachments/assets/5f9d3f38-04bc-4783-8d81-b404c8807cf4" />

CREATE TABLE Departments(
    dept_id INT PRIMARY KEY NOT NULL,
    department varchar(50)
);

INSERT INTO Departments VALUES
(101, 'Engineering'),
(102, 'HR'),
(103, 'Finance'),
(104, 'Marketing'),
(105, 'Engineering'),
(106, 'Sales'),
(107, 'HR');

SELECT * FROM Departments;

Departments table:

<img width="238" height="239" alt="image" src="https://github.com/user-attachments/assets/81ec5dcc-78f8-401a-ae9a-37fcb2001dfc" />

# Creating View for Single Table 'EMPLOYEES':
CREATE VIEW EmployeesDetails AS
SELECT * FROM Employees;

SELECT * FROM EmployeesDetails;


<img width="633" height="294" alt="image" src="https://github.com/user-attachments/assets/a84b535b-0044-41fe-829a-8a18b51b75b7" />


CREATE VIEW EmpDetails AS
SELECT employee_id, first_name, last_name FROM Employees;

SELECT * FROM EmpDetails;

<img width="302" height="280" alt="image" src="https://github.com/user-attachments/assets/8797c256-1a23-46b5-8a26-0ab0186aed13" />

# Creating View for Single Table 'EMPLOYEES' by using ORDER BY clause:
CREATE VIEW OrderdEmployeeDetails AS
SELECT employee_id, first_name, last_name FROM Employees
ORDER BY first_name;

SELECT * FROM OrderedEmployeeDetails;

<img width="311" height="277" alt="image" src="https://github.com/user-attachments/assets/d415f90c-f7a9-48e0-8d0e-2495eb1ba0c8" />

# Creating View for Single Table 'EMPLOYEES' by using 'WHERE' clause:
CREATE VIEW EngineeringEmployees AS
SELECT employee_id, first_name, last_name FROM Employees
WHERE department = 'Engineering';

SELECT * FROM EngineeringEmployees;

<img width="314" height="113" alt="image" src="https://github.com/user-attachments/assets/fcc13ee0-44e6-484a-97bf-6f6d8f7d196f" />

# Creating View for Multiple Tables 'EMPLOYEES'and 'DEPARTMENTS':
CREATE VIEW department_id AS
SELECT employees.first_name, employees.salary, Departments.dept_id
FROM Employees, Departments
WHERE Employees.department = Departments.department;

SELECT * FROM department_id;


<img width="259" height="374" alt="image" src="https://github.com/user-attachments/assets/19b3dd06-67d2-4d53-ac52-77a68a1e7d26" />

# Create View with complex SELECT by using Table 'EMPLOYEES' only:
CREATE VIEW Highestsalary AS
SELECT *, 
SUM(salary) AS total_salary
FROM Employees
GROUP BY employee_id
HAVING SUM(salary) > 10000
ORDER BY total_salary DESC;

SELECT * FROM Highestsalary;


<img width="727" height="281" alt="image" src="https://github.com/user-attachments/assets/03473ae1-6612-4a54-ae5c-e87971670ba6" />

# Create View with complex SELECT by using both tables 'EMPLOYEES' and 'DEPARTMENTS':
CREATE VIEW ComplexQuery AS
SELECT employee_id, first_name, 
SUM(salary) AS total_salary,
COUNT(employee_id) AS total_employees,
AVG(salary) AS average_salary
FROM Employees
JOIN Departments
ON Employees.department = Departments.department
WHERE joining_date > '2021-01-01'
GROUP BY employee_id
HAVING SUM(salary) > 100000 
ORDER BY total_salary DESC;

SELECT * FROM ComplexQuery;


<img width="582" height="127" alt="image" src="https://github.com/user-attachments/assets/2b67780f-ae39-49b8-abc1-41de673c3829" />

# Use views for abstraction:
CREATE VIEW HighEarningEmployees AS
SELECT MAX(salary) as total_salary, employee_id, first_name, department FROM Employees
GROUP BY employee_id
ORDER BY MAX(salary) DESC
LIMIT 3;

SELECT * FROM HighEarningEmployees;

<img width="416" height="155" alt="image" src="https://github.com/user-attachments/assets/776e08b7-cdcc-4dae-b162-1ab32bb6ca55" />


# Use views for security View data:
CREATE VIEW secured_data AS
SELECT employee_id, first_name, last_name, department FROM Employees
ORDER BY first_name;

SELECT * FROM secured_data;

<img width="420" height="297" alt="image" src="https://github.com/user-attachments/assets/9c7b34b9-c2a8-46a1-bbb3-5e3ba96c2f82" />

# 'DELETING' a view table:
DROP VIEW EmpDetails;
