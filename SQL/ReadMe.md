# Problems to revisit for SQL Revision

## Basic Joins

### Confirmation Rate

```js
# Write your MySQL query statement below
SELECT s.user_id,
ROUND(AVG(if(c.action="confirmed",1,0)),2) AS confirmation_rate
FROM Signups AS s
LEFT JOIN Confirmations AS c
ON
s.user_id=c.user_id
GROUP BY (s.user_id);
```

Look at `ROUND(AVG(if(c.action="confirmed",1,0)),2)`. It is similar to if action==confirmed -> ADD 1 else ADD 0 divided by total actions of User that's why we do `GROUP BY (s.user_id)`.


### Managers with Atleast 5 direct reports

```js
# Write your MySQL query statement below
SELECT e.name FROM Employee AS e
JOIN Employee ON
e.id=Employee.managerId
GROUP BY e.id
HAVING COUNT(e.id)>=5;
```

The GROUP BY clause in SQL collapses rows with identical values into single summary rows

### Students and Examinations

This question uses concept of CROSS JOIN (1*n) mapping a response with every row. So, every table containing n rows, each of that row would be mapped with every one of other rows of another table

```js
# Write your MySQL query statement below
SELECT s.student_id,s.student_name,sub.subject_name,COUNT(e.student_id) AS attended_exams FROM Students AS s
CROSS JOIN Subjects AS sub
LEFT JOIN Examinations AS e
ON s.student_id=e.student_id
AND sub.subject_name=e.subject_name
GROUP BY s.student_id,sub.subject_name,s.student_name
ORDER BY s.student_id, sub.subject_name
```
Solve this question again while revising

### Average Time Process per machine

```js
# Write your MySQL query statement below
SELECT a.machine_id,ROUND(AVG(b.timestamp-a.timestamp),3) AS processing_time FROM Activity a
JOIN Activity b
ON a.machine_id=b.machine_id
AND a.process_id=b.process_id
AND a.activity_type='start'
AND b.activity_type='end'
GROUP BY a.machine_id;
```

SOlve this question again too
### Rising Temperature
```js
# Write your MySQL query statement below
SELECT w1.id FROM Weather w1, Weather w2
WHERE DATEDIFF(w1.recordDate,w2.recordDate)=1 AND w1.temperature>w2.temperature
```
Since, we need to compare every row with each other we used implicit CROSS JOIN like `SELECT w1.id FROM Weather w1, Weather w2`

## Subqueries

### Department Top Three Salaries

This question uses Correlated Subqueries which is processed **Outside In** , i.e the outer query is processed first because some data of the outer query is processed in the inner subquery

```js
# Write your MySQL query statement below
SELECT d.name AS Department, e.name AS Employee,e.salary AS Salary FROM Employee e
JOIN Department d
ON e.departmentId=d.id
WHERE
3>(SELECT COUNT(DISTINCT(e2.salary)) FROM employee e2

WHERE
e2.departmentId=e.departmentId
AND 
e2.salary>e.salary)

```
It works like For-each loop, i.e every row from the outer query is iterated to check if the salary in the outer query is largest or not (if it comes in top-three or not)

THE simple subquery is processed **inside out**
like 
```js
SELECT * FROM Employee e
WHERE e.salary > (SELECT AVG(salary) FROM EMPLOYEE)
```

### Movie Rating

```js
# Write your MySQL query statement below
(SELECT u.name AS results FROM Users u
JOIN MovieRating m
ON
u.user_id=m.user_id
GROUP BY u.user_id
ORDER BY COUNT(movie_id) DESC,u.name
LIMIT 1)
UNION ALL
(SELECT m1.title AS results FROM Movies m1
JOIN MovieRating m2
ON m1.movie_id=m2.movie_id
AND m2.created_at>="2020-02-01" AND m2.created_at<="2020-02-29"
GROUP BY m1.movie_id
ORDER BY AVG(m2.rating) DESC,m1.title
LIMIT 1)


```

- Important Rule:
1. When you use **UNION**, **SQL** expects **ORDER BY** and **LIMIT** to either apply to the entire combined result (placed at the very end of everything) OR to individual queries <u>**(which must be wrapped in parentheses)**. Because your first query isn't in parentheses, the SQL parser crashes when it suddenly hits the **UNION** keyword.</u>

2. <u>Standard **UNION** removes duplicate rows.</u> If the top user and the top movie happen to have the exact same name (e.g., a user named "Daniel" and a movie named "Daniel"), standard UNION would delete one.<u> **UNION ALL** keeps both.</u>


## Advanced Select And Joins

**IMPORTANT RULE**  
If a column is in your SELECT statement and it doesn't have an aggregator (like SUM or COUNT) wrapped around it, it MUST be listed in the GROUP BY clause.  
For example:

```js
// THIS WILL CAUSE AN ERROR
SELECT department, name 
FROM Employee 
GROUP BY department;
```
In the above code, if we aggregate every row by Department, then the SQL doesn't know which name to pur first because there are many names in the department, multiple employees.  

So, we have two Choices:

```js
-- THIS WILL CAUSE AN ERROR
SELECT department, name 
FROM Employee 
GROUP BY department,name;
```
It will display all the name in the given department 

OR

```js
SELECT department, COUNT(name)
FROM Employee 
GROUP BY department;
```
It will have certainty what to display in the row i.e number of employees in that particular department