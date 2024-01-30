# SQL Analytic Functions: A Comprehensive Guide with Detailed Examples

## Introduction

SQL analytic functions are powerful tools for performing complex calculations, rankings, and aggregations within specific groups of data. This comprehensive guide aims to provide a detailed exploration of SQL analytic functions, their syntax, and various scenarios in which they can be applied.

### 1. SQL Analytic Functions vs Aggregate Functions

Before diving into interview questions, it's crucial to understand the distinction between analytic functions and aggregate functions.

**Aggregate functions** return a single result for each group of rows, such as the average salary of all employees:
```sql
-- Aggregate Function: Average Salary of all employees
SELECT AVG(Salary) AS AVG_SAL FROM EMPLOYEES;
```

On the other hand, **analytic functions** calculate an aggregate value over a group of rows and return a result for each row of the group, as demonstrated in the following example:
```sql
-- Analytic Function: Average Salary of all employees department-wise
SELECT Department_Id, AVG(Salary) AS AVG_SAL FROM EMPLOYEES GROUP BY Department_Id ORDER BY Department_Id;
```

### 2. Analytic Functions Syntax

Analytic functions have a specific syntax that may vary for each function. The basic syntax is as follows:

```sql
Analytic_Function([ arguments ]) OVER ([partition_clause ] [ order_by_clause [ windowing_clause ] ])
```

- **Arguments:** The column on which the aggregation is done.
- **Partition Clause:** Defines the group of rows upon which the aggregation needs to be done.
- **Order By Clause:** Orders the rows within the partition.
- **Windowing Clause:** Provides further control over the window within which an analytic function can apply.

The Windowing Clause in SQL analytic functions provides a way to define the window, or subset of rows, within which the analytic function operates. It further refines how the function's calculations are applied to the specified rows. The Windowing Clause is optional, and its usage depends on the specific requirements of the analytic function.

The basic syntax of the Windowing Clause looks like this:

```sql
OVER (
    [PARTITION BY partition_expression, ... ]
    [ORDER BY sort_expression [ASC | DESC], ... ]
    window_frame_clause
)
```

Let's break down each part of the Windowing Clause:

1. **PARTITION BY clause:**
   - It divides the result set into partitions or groups based on the specified column(s).
   - The analytic function is applied independently within each partition.
   - If this clause is omitted, the function is applied to the entire result set as a single group.

   Example:
   ```sql
   OVER (PARTITION BY Department_Id ORDER BY Salary)
   ```
   In this case, the result set is partitioned by the `Department_Id` column, and the analytic function is applied separately to each department.

2. **ORDER BY clause:**
   - It determines the order of rows within each partition.
   - The analytic function is applied in this order.
   - If this clause is omitted, the function operates on an unordered set of rows.

   Example:
   ```sql
   OVER (ORDER BY Hire_date DESC)
   ```
   This orders the rows based on the `Hire_date` column in descending order, affecting how the analytic function processes the data.

3. **window_frame_clause:**
   - It specifies the range or window of rows to include in the calculation.
   - It includes options like `ROWS`, `RANGE`, and `GROUPS` to define the window.
   - If this clause is omitted, the default window is the entire partition.

   Examples:
   - `ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING`: Specifies a window that includes the current row and its neighboring rows.
   - `RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW`: Includes all rows from the beginning of the partition to the current row.

Here's an example using the `SUM` analytic function with the Windowing Clause:

```sql
SELECT
  Employee_Id,
  First_Name,
  Department_Id,
  Salary,
  SUM(Salary) OVER (PARTITION BY Department_Id ORDER BY Salary) AS Cumulative_Salary
FROM EMPLOYEES;
```

In this query, the `SUM` function calculates the cumulative salary within each department, and the Windowing Clause ensures that the summation is performed in the specified order and within each department's partition.

### 3. Examples of SQL Analytic Functions

Let's explore various scenarios using SQL analytic functions with detailed explanations:

#### 3.1 Calculate Total Sum of Salary Department-wise

```sql
-- Sample Data
CREATE TABLE EMPLOYEES (
    Employee_Id INT,
    First_Name VARCHAR(50),
    Department_Id INT,
    Salary INT
);

INSERT INTO EMPLOYEES VALUES
(100, 'John', 90, 24000),
(101, 'Jane', 90, 17000),
(102, 'Doe', 100, 17000);

-- Query
SELECT Employee_Id, First_Name, Department_Id, Salary, SUM(Salary) OVER(PARTITION BY Department_Id) AS SUM_SAL
FROM EMPLOYEES ORDER BY Employee_Id;
```

**Explanation:**
In this example, the `SUM(Salary) OVER(PARTITION BY Department_Id)` calculates the total sum of salaries within each department. The `PARTITION BY` clause divides the result set into partitions based on the `Department_Id`, and the `SUM(Salary)` is applied within each partition.

**Expected Output:**
```
Employee_Id | First_Name | Department_Id | Salary | SUM_SAL
--------------------------------------------------------
100         | John       | 90             | 24000  | 41000
101         | Jane       | 90             | 17000  | 41000
102         | Doe        | 100            | 17000  | 17000
```

#### 3.2 Calculate Cumulative Sum of Salary Department-wise

```sql
-- Query
SELECT Employee_Id, First_Name, Department_Id, Salary,
       SUM(Salary) OVER(PARTITION BY Department_Id ORDER BY Employee_Id) AS CUML_SAL
FROM EMPLOYEES ORDER BY Employee_Id;
```

**Explanation:**
The `SUM(Salary) OVER(PARTITION BY Department_Id ORDER BY Employee_Id)` calculates the cumulative sum of salaries within each department. The `PARTITION BY` clause ensures that the cumulative sum is reset for each department, and the `ORDER BY` clause defines the order in which the cumulative sum is calculated.

**Expected Output:**
```
Employee_Id | First_Name | Department_Id | Salary | CUML_SAL
--------------------------------------------------------
100         | John       | 90             | 24000  | 24000
101         | Jane       | 90             | 17000  | 41000
102         | Doe        | 100            | 17000  | 17000
```

#### 3.3 Calculate Cumulative Sum of the Organization

```sql
-- Query
SELECT Employee_Id, First_Name, Department_Id, Salary,
       SUM(Salary) OVER(ORDER BY Employee_Id) AS CUML_SAL
FROM EMPLOYEES ORDER BY Employee_Id;
```

**Explanation:**
Here, the `SUM(Salary) OVER(ORDER BY Employee_Id)` calculates the cumulative sum of salaries across the entire organization. The absence of the `PARTITION BY` clause means that the cumulative sum considers all rows in the result set.

**Expected Output:**
```
Employee_Id | First_Name | Department_Id | Salary | CUML_SAL
--------------------------------------------------------
100         | John       | 90             | 24000  | 24000
101         | Jane       | 90             | 17000  | 41000
102         | Doe        | 100            | 17000  | 58000
```

#### 3.4 Calculate Cumulative Average of Salary Department-wise

```sql
-- Query
SELECT Employee_Id, First_Name, Department_Id, Salary,
       AVG(Salary) OVER(PARTITION BY Department_Id ORDER BY Employee_Id) AS AVG_SAL
FROM EMPLOYEES ORDER BY Employee_Id;
```

**Explanation:**
In this example, the `AVG(Salary) OVER(PARTITION BY Department_Id ORDER BY Employee_Id)` calculates the cumulative average of salaries within each department. The `PARTITION BY` clause ensures that the average is computed separately for each department, and the `ORDER BY` clause defines the order of computation.

**Expected Output:**
```
Employee_Id | First_Name | Department_Id | Salary | AVG_SAL
--------------------------------------------------------
100         | John       | 90             | 24000  | 24000
101         | Jane       | 90             | 17000  | 20500
102         | Doe        | 100            | 17000  | 17000
```

#### 3.5 Calculate Average of Salary for Current and Previous Record Department-wise

```sql
-- Query
SELECT Employee_Id, First_Name, Department_Id, Salary,
       AVG(Salary) OVER(PARTITION BY Department_Id ORDER BY Employee_Id ROWS 1 PRECEDING) AS AVG_SAL
FROM EMPLOYEES ORDER BY Employee_Id;
```

**Explanation:**
Here, the `AVG(Salary) OVER(PARTITION BY Department_Id ORDER BY Employee_Id ROWS 1 PRECEDING)` calculates the average salary for the current and previous records within each department. The `ROWS 1 PRECEDING` clause specifies the window size for the average calculation.

**Expected Output:**
```
Employee_Id | First_Name | Department_Id | Salary | AVG_SAL
--------------------------------------------------------
100         | John       | 90             | 24000  | 24000
101         | Jane       | 90             | 17000  | 20500
102         | Doe        | 100            | 17000  | 17000
```

### 4. Using LAG and LEAD Analytic

 Functions

The `LAG` and `LEAD` functions are useful for accessing the value of a specific row before or after the current row, respectively.

#### 4.1 Display Next Hire Date for Employees

```sql
-- Query
SELECT Employee_Id, First_Name, Department_Id, Hire_date,
       LEAD(Hire_date) OVER(ORDER BY Hire_date) AS NEXT_HIREDATE
FROM EMPLOYEES ORDER BY Hire_date;
```

**Explanation:**
The `LEAD(Hire_date) OVER(ORDER BY Hire_date)` function retrieves the hire date of the next employee based on the order of hire date. This is useful for identifying the next hire date for each employee.

**Expected Output:**
```
Employee_Id | First_Name | Department_Id | Hire_date | NEXT_HIREDATE
-------------------------------------------------------------------
100         | John       | 90             | 2022-01-01 | 2022-02-01
101         | Jane       | 90             | 2022-02-01 | NULL
102         | Doe        | 100            | 2022-03-01 | NULL
```

### 5. RANK and DENSE_RANK

#### 5.1 RANK Example
```sql
-- Query
SELECT Employee_Id, First_Name, Department_Id, Salary,
       RANK() OVER(PARTITION BY Department_Id ORDER BY Salary) AS SAL_RANK
FROM EMPLOYEES;

-- Expected Output
/*
Employee_Id | First_Name | Department_Id | Salary | SAL_RANK
--------------------------------------------------------
100         | John       | 90             | 24000  | 2
101         | Jane       | 90             | 17000  | 1
102         | Doe        | 100            | 17000  | 1
*/
```

**Explanation:**
The `RANK() OVER(PARTITION BY Department_Id ORDER BY Salary)` function assigns a rank to each employee based on their salary within their respective departments. In case of ties (equal salaries), employees receive the same rank, and the next rank is skipped.

#### 5.2 DENSE_RANK Example
```sql
-- Query
SELECT Employee_Id, First_Name, Department_Id, Salary,
       DENSE_RANK() OVER(PARTITION BY Department_Id ORDER BY Salary) AS SAL_RANK
FROM EMPLOYEES;

-- Expected Output
/*
Employee_Id | First_Name | Department_Id | Salary | SAL_RANK
--------------------------------------------------------
100         | John       | 90             | 24000  | 2
101         | Jane       | 90             | 17000  | 1
102         | Doe        | 100            | 17000  | 1
*/
```

**Explanation:**
The `DENSE_RANK() OVER(PARTITION BY Department_Id ORDER BY Salary)` function also assigns ranks based on salary within departments, but it does not skip ranks in case of ties. It ensures a continuous sequence of ranks without gaps.

### 6. Finding Employees with MAX and MIN Salary

#### 6.1 Find Employee with MAX Salary Department-wise
```sql
-- Query
SELECT * FROM (
    SELECT Employee_Id, First_Name, Department_Id, Salary,
           RANK() OVER(PARTITION BY Department_Id ORDER BY Salary DESC) AS SAL_RANK
    FROM EMPLOYEES
) WHERE SAL_RANK = 1;

-- Expected Output
/*
Employee_Id | First_Name | Department_Id | Salary | SAL_RANK
--------------------------------------------------------
100         | John       | 90             | 24000  | 1
102         | Doe        | 100            | 17000  | 1
*/
```

**Explanation:**
The inner query uses `RANK()` to assign ranks based on descending salary within each department. The outer query then selects rows where the rank is 1, indicating the employee with the highest salary in each department.

#### 6.2 Find Employee with MIN Salary Department-wise
```sql
-- Query
SELECT * FROM (
    SELECT Employee_Id, First_Name, Department_Id, Salary,
           RANK() OVER(PARTITION BY Department_Id ORDER BY Salary) AS SAL_RANK
    FROM EMPLOYEES
) WHERE SAL_RANK = 1;

-- Expected Output
/*
Employee_Id | First_Name | Department_Id | Salary | SAL_RANK
--------------------------------------------------------
101         | Jane       | 90             | 17000  | 1
102         | Doe        | 100            | 17000  | 1
*/
```

**Explanation:**
Similar to the previous example, the inner query uses `RANK()` to assign ranks based on ascending salary within each department. The outer query then selects rows where the rank is 1, indicating the employee with the lowest salary in each department.

### 7. Difference between Employee Salary and Max Salary in the Department

```sql
-- Query
SELECT Employee_Id, First_Name, Department_Id, Salary,
       MAX(Salary) OVER(PARTITION BY Department_Id) AS MAX_SAL,
       (MAX(Salary) OVER(PARTITION BY Department_Id) - Salary) AS SAL_DIFF
FROM EMPLOYEES ORDER BY Employee_Id;

-- Expected Output
/*
Employee_Id | First_Name | Department_Id | Salary | MAX_SAL | SAL_DIFF
---------------------------------------------------------------------
100         | John       | 90             | 24000  | 24000   | 0
101         | Jane       | 90             | 17000  | 24000   | 7000
102         | Doe        | 100            | 17000  | 17000   | 0
*/
```

**Explanation:**
This query calculates the difference between each employee's salary and the maximum salary in their respective departments. The `MAX(Salary) OVER(PARTITION BY Department_Id)` ensures that the maximum salary is applied to all rows within the same department.

**Expected Output:**
```
Employee_Id | First_Name | Department_Id | Salary | MAX_SAL | SAL_DIFF
---------------------------------------------------------------------
100         | John       | 90             | 24000  | 24000   | 0
101         | Jane       | 90             | 17000  | 24000   | 7000
102         | Doe        | 100            | 17000  | 17000   | 0
```

### 8. Finding Employee with MAX Salary without RANK or DENSE_RANK

```sql
-- Query
SELECT * FROM (
    SELECT Employee_Id, First_Name, Department_Id, Salary,
           MAX(Salary) OVER(PARTITION BY Department_Id) AS MAX_SAL,
           (MAX(Salary) OVER(PARTITION BY Department_Id) - Salary) AS SAL_DIFF
    FROM EMPLOYEES
) WHERE SAL_DIFF = 0;

-- Expected Output
/*
Employee_Id | First_Name | Department_Id | Salary | MAX_SAL | SAL_DIFF
---------------------------------------------------------------------
100         | John       | 90             | 24000  | 24000   | 0
102         | Doe        | 100            | 17000  | 17000   | 0
*/
```

**Explanation:**
This query finds employees whose salary is equal to the maximum salary in their respective departments. The `SAL_DIFF = 0` condition ensures that only rows with no salary difference (i.e., equal salaries

) are selected.

**Expected Output:**
```
Employee_Id | First_Name | Department_Id | Salary | MAX_SAL | SAL_DIFF
---------------------------------------------------------------------
100         | John       | 90             | 24000  | 24000   | 0
102         | Doe        | 100            | 17000  | 17000   | 0
```

## Conclusion

SQL analytic functions provide a powerful way to perform advanced calculations and aggregations within specific groups of data. By understanding their syntax and various use cases, you can enhance your ability to analyze and extract valuable insights from your database. Whether you're working with large datasets or conducting analytical queries, incorporating analytic functions into your SQL toolkit can significantly improve your efficiency and the depth of your analysis.
