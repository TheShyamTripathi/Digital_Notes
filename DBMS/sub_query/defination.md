### What is a Subquery?
A **subquery** (also called an inner query or nested query) is a query within another SQL query. The result of the subquery is used by the main (or outer) query. It helps in breaking down complex queries into smaller, more manageable parts, making it easier to understand and maintain.

### Syntax:
```sql
SELECT column_name
FROM table_name
WHERE column_name OPERATOR (SELECT column_name FROM another_table WHERE condition);
```

### Example of Subquery:
```sql
SELECT name 
FROM employees 
WHERE salary > (SELECT AVG(salary) FROM employees);
```
In this example, the subquery calculates the average salary from the `employees` table, and the main query retrieves the names of employees whose salary is greater than the average.

---

### Types of Subqueries

1. **Single Row Subquery:**
   - Returns only one row as a result.
   
   **Example:**
   ```sql
   SELECT name 
   FROM employees 
   WHERE salary = (SELECT MAX(salary) FROM employees);
   ```
   The subquery returns the highest salary, and the outer query selects the employee(s) with that salary.

2. **Multiple Row Subquery:**
   - Returns more than one row.

   **Example:**
   ```sql
   SELECT name 
   FROM employees 
   WHERE department_id IN (SELECT department_id FROM departments WHERE location = 'New York');
   ```
   Here, the subquery returns all `department_id`s located in New York, and the outer query fetches employee names who belong to those departments.

3. **Correlated Subquery:**
   - The subquery refers to a column from the outer query, making it dependent on the outer query for each row processed.

   **Example:**
   ```sql
   SELECT e1.name, e1.salary 
   FROM employees e1
   WHERE e1.salary > (SELECT AVG(e2.salary) FROM employees e2 WHERE e1.department_id = e2.department_id);
   ```
   This subquery compares the salary of an employee to the average salary within the same department.

4. **Nested Subquery:**
   - Subqueries can be nested within each other.
   
   **Example:**
   ```sql
   SELECT name 
   FROM employees 
   WHERE salary = (SELECT MAX(salary) FROM employees WHERE department_id = (SELECT department_id FROM departments WHERE name = 'HR'));
   ```
   This query finds the employee with the highest salary in the 'HR' department.

5. **Exists Subquery:**
   - Used to check for the existence of rows in a subquery result.
   
   **Example:**
   ```sql
   SELECT name 
   FROM employees e 
   WHERE EXISTS (SELECT 1 FROM departments d WHERE e.department_id = d.department_id AND d.name = 'Sales');
   ```
   This checks if there is any employee in the 'Sales' department and returns the names.

---

### Advantages of Subqueries:

1. **Simplicity:** Subqueries can simplify complex queries by breaking them down into smaller parts.
2. **Modularity:** Queries become easier to maintain and update when split into subqueries.
3. **Reusability:** The result of a subquery can be reused in the outer query without needing to execute the logic multiple times.
4. **Isolation:** Each subquery runs independently, which can reduce the complexity of large queries.

### Disadvantages of Subqueries:

1. **Performance Issues:** Subqueries can sometimes be slower than joins, especially with large datasets, as the subquery may run multiple times for each row in the outer query.
2. **Limited Flexibility:** Subqueries are less flexible than joins when it comes to returning large datasets or complex conditions.
3. **Not Supported Everywhere:** Some database systems have limitations on the use of subqueries in certain cases (e.g., older versions of MySQL didn’t support certain subqueries).
4. **Complexity in Debugging:** Nested subqueries can become hard to debug when the query logic becomes too deep or complicated.

Would you like help with more examples or optimizing subqueries for better performance?
