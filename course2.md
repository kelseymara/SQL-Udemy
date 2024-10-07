# Overview
These notes are from this Udemy Course: https://adp-gptlearning.udemy.com/course/the-complete-sql-bootcamp/learn/lecture/18192138#overview

## Aggregation Functions
```SQL
SELECT MIN(replacement_cost) FROM film; // returns lowest replacement cost
SELECT MAX(replacement_cost) FROM film; // returns highest replacement cost
SELECT MAX(replacement_cost), MIN(replacement_cost) FROM film; // returns both
SELECT COUNT(*) FROM film; // returns how many rows
SELECT AVG(replacement_cost) FROM film; // returns average replacement cost
SELECT ROUND(AVG(replacement_cost),2); // rounds average replacement cost to 2 decimal places
SELECT SUM(replacement_cost); // returns sum of replacement cost
```

## GROUP BY
- choose a **categorical** column to GROUP BY
- categorical columns are non-continuous
- **the GROUP BY clause must appear right after a FROM or WHERE statement**
```SQL
SELECT category_col, AGG(data_col) // AGG is placeholder for Aggregate Function
FROM table
GROUP BY category_col;

SELECT category_col, AGG(data_col) // AGG is placeholder for Aggregate Function
FROM table
WHERE category_col!='A' // you can filter before group by
GROUP BY category_col;
```
- in the SELECT statement, columns **must either have an aggergate function or be in the GROUP BY call** (look at code above)
- where statements should not refer to the aggregation result, later on we will learn to use HAVING to filter on those results
You can group by multiple columns:
```SQL
SELECT company, division, SUM(sales)
FROM finance_table
GROUP BY company, division;
```
If you want to sort results based on the aggregate, make sure to reference the entire function:
```SQL
SELECT company, SUM(sales)
FROM finance_table
GROUP BY company
ORDER BY SUM(sales)
LIMIT 5;
```
## GROUP BY (part 2)
```SQL
SELECT DATE(payment_date) FROM payment; // formats the date into a more readable and takes out timestamp

SELECT DATE(payment_date) FROM payment
GROUP BY DATE(payment_date); // want to group the dates to see which ones have same date
```
## GROUP BY - Challenge
- We have 2 staff members, with staff IDs 1 and 2. We want to give a bonus to the staff member that handled the most payments (most in terms of number of payments processed, not total dollar amount).
- How many payments did each staff member handle and who gets the bonus?
```SQL
SELECT staff_id, COUNT(amount)
FROM payment,
GROUP BY staff_id;
```
- Corporate HQ is conducting a study on the relationship between replacement cost and a movie MPAA rating (e.g. PG, R, etc...)
- What is the average replacement cost per MPAA rating? note: you many need to expand the AVG column to view correct results
```SQL
SELECT rating, ROUND(AVG(replacement_cost),2)
FROM film
GROUP BY rating;
```
- We are running a promotion to reward our top 5 customers with coupons
- What are the customer ids of the top 5 customers by total spend?
```SQL
SELECT customer_id, SUM(amount)
FROM payment
ORDER BY SUM(amount) DESC
LIMIT 5;
```

## HAVING
- The HAVING clause allows us to filter **after** an aggregation has already taken place
```SQL


```
