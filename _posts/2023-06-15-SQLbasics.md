---
title: '[Database SQL Basics]'
date: 2023-06-15 13:20:00 +0000
categories: [Database, SQL]
math: true
---

# Create Schema
```
CREATE SCHEMA 'schema_name' DEFAULT CHARATER SET utf8mb4
```
We can give schema name after CREATE SCHEMA function 
```
DEFAULT settings for utf-8 encoding
SELECT * FROM SCHEMATA;
```

# Create table and define variable types
```
CREATE Table 'schema_name'.'table_name'(
	'id' INT,
	'name' VARCHAR(45),
	'age' INT,
	PRIMARY KEY('id')
);
```
'schema_name'.'table_name' means that which schema the database should creaate the table

PRIMARY KEY('id') define 'id' column as primary key

*Note* that we don't need to use capital letters and we don't need ' ' to specify table and column names

## Display the columns 
```
SHOW FULL COLUMNS FROM 'schema_name'.'table_name';
```

## SELECT, INSERT, UPDATE and DELETE
```
SELECT 'id', 'name' FROM 'schema_name'.'table_name'; # specify the column names
SELECT * FROM 'schema_name'.'table_name'; all columns
```

**Sort the data (order by)**
```
select * from 'schema_name'.'table_name' order by age; # acsending order
# order by ascending
select * from 'schema_name'.'table_name' order by age ASC;
# order by descending
select * from 'schema_name'.'table_name' order by age DESC;
# muptile column
select * from 'schema_name'.'table_name' order by name DESC, age ASC;
```

**Obtain unique information (select distinct)** 
```
SELECT DISTINCT 'name' FROM 'schema_name'.'table_name';
```

**Pagination (limit/offset)**
```
select * from 'schema_name'.'table_name' limit 3 offset 1;

Result
id	name	age	height
2	  May	30	140
3 	Tim	25	170
4	  Jay	60	185
```
`limit` is to indicate how many rows will be presented and `offset` skip a specific number of results. 

**Group by**
```
select * from 'schema_name'.'table_name' group by age;

Result
age
10
20
30
```

**Aggregation function (count/sum/avg/min/sum)**
### how to count the number of distinct values (count(*))? 
```
select count(*) as frequency, name from 'schema_name'.'table_name' group by name;
```

**Use group by to extract duplicated rows and count**
```
select name from 'schema_name'.'table_name' group by name having count(*) >1;


Data:
name
mike
mike
kate

Result:
name
mike
```

```
# to find the single values
select nums from 'schema_name'.'table_name' group by num having count(*) = 1;
```
group by 1 means group by the first column. 

### find the min and max values `(min/max)`
```
# find the min value
select min(age) as min_age from 'schema_name'.'table_name';
# find the max value
select max(age) as max_age from 'schema_name'.'table_name';
```

### how to find the average value from the columns `avg`?
```
select avg(age) as mean_age from 'schema_name'.'table_name';
```

### how to find the sum value from the columns `sum`? 
```
select sum(age) as sum_age from 'schema_name'.'table_name';
```

**How to find the total sum of age greater than 50?**
```
select sum(age > 50) as sum_age50 from 'schema_name'.'table_name';
```

**How to find cumulative sum?**
```
select sum (age) over (id) as cum_age from 'schema_name'.'table_name';
```

### combine two columns and create a new column `concat`
```
select concat('id', '-', 'date') as new_column from 'schema_name'.'table_name';
# condition for the concat function
select concat('id', '-', 'date') as new_column from 'schema_name'.'table_name' having new_column like '%a%;
```

**Insert the data by rows**
```
INSERT INTO 'schema_name'.'table_name' ('id', 'name', 'age') VALUES (1, 'John', 50);

INSERT INTO 'schema_name'.'table_name' ('id', 'name', 'age') VALUES (1, 'John', 50), (2, 'James', 45);
```

# WHERE: Filter using condition statement 
```
SELECT * FROM 'schema_name'.'table_name' WHERE 'id' = 1;
```

WHERE uses other arithmatic signs such as, `=`, `>`, `<`, `!=`

WHERE name IS NULL # finds the name that contains null value 

IS NULL/ NOT IS NULL

**Filter by the character length (length)**
```
# To find the rows where the length of the email address is larger than 10, we can use: 
SELECT * FROM 'schema_name'.'table_name' WHERE length(email) > 10;
```
**Select the odd numbered IDs**
```
SELECT id FROM 'schema_name'.'table_name' WHERE (id % 2 =1 );
```

**Important: some database contains null and we want filter NULL (ifnull)**

```
SELECT * FROM 'schema_name'.'table_name' WHERE IFNULL('age', 0) > 50;
```

It implies that if it's null then convert null value into 0 and use the condition

**Multiple Conditions**
```
SELECT * FROM 'schema_name'.'table_name' WHERE 'age' > 20 AND 'height' < 6;
```
Note that `and` and `or` can be used 

**Using the conditions create the column**

For example, if the patients are male and age greater than 50, create column name called binary 0 or 1
```
SELECT GENDER, AGE FROM PATIENTS 
CASE WHEN GENDER = 'M' and AGE > 50 THEN 1 
ELSE 0 
END AS Binary
```

**Range Conditions**

```
#returns the specific id values
SELECT * FROM 'schema_name'.'table_name' WHERE 'id' IN (1,3); 
```
``IN`` and ``NOT IN`` can be used

```
#returns within a specific range
SELECT * FROM 'schema_name'.'table_name' WHERE 'id' BETWEEN 1 AND 5;
```

**Note that BETWEEN can be applied to dates**
```
SELECT * FROM 'schema_name'.'table_name' WHERE visit between start_date and end_date;
```

**To extract the year and month from the dataset**
```
select date_format(date, '%Y-%m) as month from 'schema_name'.'table_name' WHERE visit ;
```

```
# find the pattern
SELECT * FROM 'schema_name'.'table_name' WHERE name LIKE '%a%'
```

`%` matches zero, one or multiple characters

`_` matches only one character

## Update the value
```
UPDATE 'schema_name'.'table_name' SET 'name' = 'Andy', 'age' = 18 WHERE 'id' = 2;
```

## Remove the rows 
```
DELETE FROM 'schema_name'.'table_name' WHERE 'id' = 1;
```

## If-else statement more example 
*case when (condition) then (result) else (result) end;*

How to convert all gender from male to female?
```
select employee_id set sex = case sex when 'f' then 'm' else 'f' end;
```

```
select employee_id,
case when employee_id % 2 = 1 and name not like 'M%' then salary
else 0
end as bonus
from employees 
order by employee_id;
```
```
select employee_id , salary * ( employee_id%2 ) * ( name not like 'M%') as bonus from employees
order by employee_id;
```








