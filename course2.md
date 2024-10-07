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

