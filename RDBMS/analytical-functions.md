Analytical functions in SQL are used to perform calculations across a set of rows related to the current row. These functions operate on a "window" of rows defined by an OVER clause. Analytical functions are powerful tools for performing complex calculations, rankings, and aggregations within specific groups of data. Here are some commonly used analytical functions with in-depth explanations and examples:

### 1. **ROW_NUMBER():**
   - **Purpose:**
     - Assigns a unique integer to each row within a partition based on the specified order.
   - **Example:**
     ```sql
     SELECT employee_id, salary, ROW_NUMBER() OVER (ORDER BY salary DESC) AS salary_rank
     FROM employees;
     ```
     This assigns a rank to each employee based on their salary in descending order.

### 2. **RANK():**
   - **Purpose:**
     - Assigns a rank to each row within a partition based on the specified order. Ties receive the same rank, and the next rank is skipped.
   - **Example:**
     ```sql
     SELECT employee_id, salary, RANK() OVER (ORDER BY salary DESC) AS salary_rank
     FROM employees;
     ```
     Similar to ROW_NUMBER(), but handles ties differently.

### 3. **DENSE_RANK():**
   - **Purpose:**
     - Assigns a rank to each row within a partition based on the specified order. Ties receive the same rank, and the next rank is not skipped.
   - **Example:**
     ```sql
     SELECT employee_id, salary, DENSE_RANK() OVER (ORDER BY salary DESC) AS salary_rank
     FROM employees;
     ```
     Similar to RANK(), but without skipped ranks for ties.

### 4. **LEAD() and LAG():**
   - **Purpose:**
     - LEAD() retrieves data from the next row within the partition, while LAG() retrieves data from the previous row.
   - **Example:**
     ```sql
     SELECT employee_id, salary, LEAD(salary) OVER (ORDER BY salary) AS next_salary
     FROM employees;
     ```
     Retrieves the salary of the next employee in ascending order.

### 5. **FIRST_VALUE() and LAST_VALUE():**
   - **Purpose:**
     - FIRST_VALUE() returns the value of a specified expression for the first row in the window, while LAST_VALUE() returns the value for the last row.
   - **Example:**
     ```sql
     SELECT employee_id, salary, FIRST_VALUE(salary) OVER (ORDER BY salary) AS first_salary
     FROM employees;
     ```
     Retrieves the salary of the employee with the lowest salary.

### 6. **SUM() OVER():**
   - **Purpose:**
     - Calculates the sum of a specified column over a window of rows.
   - **Example:**
     ```sql
     SELECT order_id, order_date, total_amount,
            SUM(total_amount) OVER (ORDER BY order_date) AS cumulative_sum
     FROM orders;
     ```
     Computes the cumulative sum of total_amount over the ordered rows.

### 7. **AVG() OVER():**
   - **Purpose:**
     - Calculates the average of a specified column over a window of rows.
   - **Example:**
     ```sql
     SELECT department, employee_id, salary,
            AVG(salary) OVER (PARTITION BY department) AS avg_salary_by_dept
     FROM employees;
     ```
     Computes the average salary within each department.

### 8. **NTILE():**
   - **Purpose:**
     - Divides the result set into a specified number of roughly equal parts, assigning a bucket number to each row.
   - **Example:**
     ```sql
     SELECT employee_id, salary, NTILE(4) OVER (ORDER BY salary) AS salary_quartile
     FROM employees;
     ```
     Divides employees into four quartiles based on their salary.

### 9. **PERCENT_RANK():**
   - **Purpose:**
     - Calculates the relative rank of each row within a partition in percentage terms.
   - **Example:**
     ```sql
     SELECT employee_id, salary, PERCENT_RANK() OVER (ORDER BY salary) AS percent_rank
     FROM employees;
     ```
     Assigns a percentage rank to each employee based on their salary.

### 10. **CUME_DIST():**
   - **Purpose:**
     - Calculates the cumulative distribution of a value within a partition.
   - **Example:**
     ```sql
     SELECT employee_id, salary, CUME_DIST() OVER (ORDER BY salary) AS cumulative_distribution
     FROM employees;
     ```
     Computes the cumulative distribution of employees based on their salary.

Analytical functions provide powerful capabilities for performing advanced calculations and analysis within SQL queries. These functions are particularly useful when dealing with ordered data or when partitioning the data into distinct groups. Understanding their application and syntax is essential for writing sophisticated SQL queries.
