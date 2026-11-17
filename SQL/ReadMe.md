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

### Restaurant Growth
```js
# Write your MySQL query statement below
WITH DailySum AS (
    SELECT
    visited_on,
    SUM(amount) AS daily_amount
    FROM Customer
    GROUP BY visited_on
)
SELECT d1.visited_on AS visited_on, SUM(d2.daily_amount) AS amount, ROUND(SUM(d2.daily_amount)/7,2) AS average_amount FROM DailySum d1
JOIN DailySum d2
ON d2.visited_on<=d1.visited_on # d1 is the current date
AND DATEDIFF(d1.visited_on,d2.visited_on)<7
GROUP BY d1.visited_on
HAVING COUNT(d2.visited_on)>=7




```
- In this question we save a random view of the table so that we can get the query we wanted `WITH DailySum AS (
    SELECT
    visited_on,
    SUM(amount) AS daily_amount
    FROM Customer
    GROUP BY visited_on
)`  
Revisit Again

### Friend Request II

```js
# Write your MySQL query statement below
WITH total_friends AS 
(
    SELECT requester_id AS id
    FROM RequestAccepted
    UNION ALL
    SELECT accepter_id AS id
    FROM RequestAccepted
)

SELECT id, COUNT(id) AS num 
FROM total_friends
GROUP BY id
ORDER BY num DESC
LIMIT 1
```
- Same concept we use `WITH table_name AS (running_our_query)`

### Investments in 2k16
```js
SELECT ROUND(SUM(tiv_2016),2) AS tiv_2016
FROM Insurance
WHERE tiv_2015 IN 
(
    SELECT tiv_2015
    FROM Insurance
    GROUP BY tiv_2015
    HAVING COUNT(tiv_2015)>1
)
AND (lat,lon) IN
(
    SELECT lat,lon
    FROM Insurance
    GROUP BY lat,lon
    HAVING COUNT(*)=1
)
```

## Basic Aggregate Functions

### Average Selling Price
- Usage OF **IFNULL**:
  `IFNULL(ROUND(SUM(t1.price*t2.units)/SUM(t2.units),2),0) AS average_price`
- If product is not sold, it will equate to Zero
```js
# Write your MySQL query statement below
SELECT t1.product_id,
IFNULL(ROUND(SUM(t1.price*t2.units)/SUM(t2.units),2),0) AS average_price
 FROM Prices t1
LEFT JOIN UnitsSold t2
ON
t1.product_id=t2.product_id
AND
(t2.purchase_date>=t1.start_date AND t2.purchase_date<=t1.end_date)
GROUP BY t1.product_id
```

### Percentage of Users Attended a Contest
- USage of Select Statement in Aggregation
```js
# Write your MySQL query statement below
SELECT contest_id,((COUNT(user_id)/(SELECT COUNT(*) FROM Users))*100) AS percentage
FROM Register
GROUP BY contest_id
ORDER BY percentage DESC,contest_id ASC
```
### Monthly Transactions I
- Two ways to formate Month:
1. `DATE_FORMAT(date,'%Y-%m')`: 'Y' means 1999 and 'y' means 99. 'M' means 'February' and 'm' means '02'
2. `SUBSTR(date,1,7)`: Substring from `1 to 7`. Includes `1999-02`

```js
SELECT 
    DATE_FORMAT(trans_date, '%Y-%m') AS month,
    country,
    COUNT(*) AS trans_count,
    SUM(IF(state = 'approved', 1, 0)) AS approved_count,
    SUM(amount) AS trans_total_amount,
    SUM(IF(state = 'approved', amount, 0)) AS approved_total_amount
FROM Transactions
GROUP BY 
    DATE_FORMAT(trans_date, '%Y-%m'), 
    country;
```

### Immediate Food Delivery ||

```js
# Write your MySQL query statement below
SELECT ROUND(AVG(IF(order_date=customer_pref_delivery_date,1,0))*100,2) AS immediate_percentage FROM Delivery
WHERE (customer_id,order_date) IN
(
    SELECT customer_id,MIN(order_date)
FROM Delivery
GROUP BY
customer_id
)


```

### Game Play Analysis IV

- Important Note:
1. Usage of `DATE_ADD(given_date, INTERVAL 1 DAY)`: It makes comparison with day after a given day.
```js
# Write your MySQL query statement below
SELECT ROUND(COUNT(player_id)/(SELECT COUNT(DISTINCT player_id) FROM Activity),2) AS fraction FROM Activity
WHERE 
(player_id,event_date) IN
(SELECT player_id,DATE_ADD(MIN(event_date),INTERVAL 1 DAY)
FROM Activity
GROUP BY player_id)
```

- `COUNT` AND `DISTINCT` : To count distinct products from the table having multiple products
`SELECT COUNT(DISTINCT product_id) FROM Products`

- Important nuance which you may miss it 

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

### Conditional use oF Cases
```js
SELECT *,
CASE
    WHEN (x+y>z) AND (x+z>y) AND (y+z>x) THEN 'Yes'
    ELSE 'No'
END
AS
triangle
FROM Triangle
```

### Cross Join (Q. Consecutive Numbers)

```js
# Write your MySQL query statement below
SELECT DISTINCT(l1.num) AS ConsecutiveNums
FROM
Logs l1,Logs l2,Logs l3
WHERE l1.id=l2.id-1
AND l2.id=l3.id-1
AND l1.num=l2.num
AND l2.num=l3.num
```

### Product Price at a Given Date

```js
# Write your MySQL query statement below
SELECT product_id, 10 AS price
FROM Products
GROUP BY product_id
HAVING MIN(change_date) > '2019-08-16'
UNION
SELECT product_id,new_price AS price
FROM Products
WHERE
(product_id,change_date)
IN
(SELECT product_id,MAX(change_date)
FROM Products
WHERE change_date <= '2019-08-16'
GROUP BY product_id)
```

### Last person to fit in Bus
- Important Concept: q1 current person, q2 every person before q1, Separate both this concerns and then solve it

```js
# Write your MySQL query statement below
SELECT q1.person_name FROM Queue q1
JOIN Queue q2
ON
q2.turn<=q1.turn # q1 is current person, q2 is all the person who boarded before them
GROUP BY q1.turn,q1.person_name
HAVING SUM(q2.weight)<=1000
ORDER BY q1.turn DESC
LIMIT 1
```

## Advanced Regex/Clause

### Fix Names in Table
- Usage of `CONCAT`
```js
# Write your MySQL query statement below
SELECT user_id,
CONCAT(UPPER(SUBSTRING(name,1,1)),LOWER(SUBSTRING(name,2))) AS name
FROM Users
ORDER BY user_id
```
### Delete records with duplicate email ID(preserving email in smaller Id)
- Usage of `DELETE`

```js
# Write your MySQL query statement below
DELETE p1 FROM Person p1,Person p2
WHERE p1.email=p2.email AND p1.id>p2.id
```

- SECOND HIGHEST SALARY
- `<>` Means **Not Equal to**
```js
SELECT id,MAX(salary) FROM Table
WHERE salary <>(SELECT MAX(salary) FROM Table)
```

### Group Sold Products By the Date
1. `CONCAT`: Joins fields in the single rows
1. `GROUP_CONCAT`: Joins multiple rows
```js
# Write your MySQL query statement below
SELECT sell_date,
COUNT(DISTINCT product) AS num_sold,
GROUP_CONCAT(DISTINCT product ORDER BY product ASC,',') AS products
 FROM
Activities a1
GROUP BY sell_date
ORDER BY sell_date

```

### Find Users with Valid Emails(MUST REVISE QUESTION FOR REGEXP SUMS UP EVERYTHING)

```js
# Write your MySQL query statement below
SELECT * FROM Users
WHERE REGEXP_LIKE(mail,'^[a-zA-Z][a-zA-Z0-9_.-]*@leetcode\\.com$','c')
```

**OR**
```js
SELECT * 
FROM Users
WHERE mail REGEXP '^[a-zA-Z][a-zA-Z0-9_.-]*@leetcode\\.com$'
  AND mail LIKE BINARY '%@leetcode.com';
  // To make case-sensitive comparison
```