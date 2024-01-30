Relational Database Management System (RDBMS) is a type of database management system that organizes data into tables with rows and columns, where each row represents a record and each column represents an attribute. In RDBMS, SQL (Structured Query Language) is commonly used for managing and manipulating data. Aggregate functions, GROUP BY, and HAVING are essential SQL concepts for working with data in a relational database.

### Aggregate Functions:
Aggregate functions operate on sets of values and return a single value based on the operation applied to the set. Here are some common aggregate functions:

1. **COUNT:**
   - Counts the number of rows in a result set.

   ```sql
   SELECT COUNT(*) FROM employees;
   ```

2. **SUM:**
   - Calculates the sum of values in a numeric column.

   ```sql
   SELECT SUM(salary) FROM employees;
   ```

3. **AVG:**
   - Computes the average of values in a numeric column.

   ```sql
   SELECT AVG(salary) FROM employees;
   ```

4. **MIN:**
   - Finds the minimum value in a column.

   ```sql
   SELECT MIN(salary) FROM employees;
   ```

5. **MAX:**
   - Retrieves the maximum value in a column.

   ```sql
   SELECT MAX(salary) FROM employees;
   ```

### GROUP BY Clause:
The GROUP BY clause is used to group rows returned by a SELECT statement based on the values in one or more columns. It is often used in conjunction with aggregate functions to perform calculations on each group of rows.

```sql
SELECT column1, aggregate_function(column2)
FROM table
GROUP BY column1;
```

**Example:**
Suppose we have an "orders" table with columns (order_id, customer_id, product_id, quantity, and order_date). We want to calculate the total quantity of products ordered by each customer.

```sql
SELECT customer_id, SUM(quantity) AS total_quantity
FROM orders
GROUP BY customer_id;
```

### HAVING Clause:
The HAVING clause is used in combination with the GROUP BY clause to filter the results of a query based on aggregated values. It is similar to the WHERE clause but is applied after the GROUP BY operation.

```sql
SELECT column1, aggregate_function(column2)
FROM table
GROUP BY column1
HAVING condition;
```

**Example:**
Building on the previous example, suppose we want to find customers who have ordered more than 50 units in total.

```sql
SELECT customer_id, SUM(quantity) AS total_quantity
FROM orders
GROUP BY customer_id
HAVING SUM(quantity) > 50;
```

In this example, the HAVING clause filters the results to include only those customers whose total ordered quantity is greater than 50.

To summarize:
- **Aggregate functions** perform calculations on sets of values.
- The **GROUP BY clause** groups rows based on specified columns.
- The **HAVING clause** filters results after grouping based on aggregate function conditions.
