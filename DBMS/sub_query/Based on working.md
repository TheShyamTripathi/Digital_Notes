## Based on working
Subqueries can also be classified based on their **working** or **execution behavior**, which includes how and when they are executed relative to the outer query. Based on this, subqueries are classified as:

### 1. **Non-Correlated Subquery**

A **non-correlated subquery** is an independent subquery that can be executed separately from the outer query. The subquery is evaluated only once, and its result is passed to the outer query. This type of subquery does not reference any columns from the outer query and can be executed in isolation.

#### Example:
```sql
SELECT name
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
- The subquery `(SELECT AVG(salary) FROM employees)` calculates the average salary, and the outer query retrieves all employees with a salary greater than this value.
- **Execution:** The subquery is executed first and then passed to the outer query.

#### Working Process:
1. The subquery runs independently and returns a result.
2. The outer query uses this result to filter or calculate.

---

### 2. **Correlated Subquery**

A **correlated subquery** is dependent on the outer query. For each row processed by the outer query, the subquery is executed. In other words, the subquery is evaluated multiple times—once for each row processed by the outer query. The correlated subquery references columns from the outer query, creating a dependency between the two.

#### Example:
```sql
SELECT e1.name, e1.salary
FROM employees e1
WHERE e1.salary > (SELECT AVG(e2.salary) FROM employees e2 WHERE e1.department_id = e2.department_id);
```
- In this case, the subquery depends on the outer query. For each employee (`e1`), the subquery calculates the average salary for that employee's department (`e1.department_id = e2.department_id`).
- **Execution:** The subquery is executed for each row processed by the outer query.

#### Working Process:
1. The outer query begins to process each row.
2. For each row, the subquery is executed using values from the current row.
3. The result of the subquery is used by the outer query for that particular row.

---

### 3. **Inline View Subquery**

An **inline view subquery** (also called a derived table) is a subquery used in the `FROM` clause of the main query. The result of the subquery is treated as a temporary table or view, which is then used by the outer query. Inline view subqueries allow for complex queries to be simplified and modularized.

#### Example:
```sql
SELECT emp.name, emp.salary
FROM (SELECT name, salary FROM employees WHERE department_id = 10) AS emp
WHERE emp.salary > 50000;
```
- The subquery `(SELECT name, salary FROM employees WHERE department_id = 10)` acts as a temporary table (`emp`), and the outer query filters employees with a salary greater than 50,000.
- **Execution:** The subquery is executed first and its result is treated as a table for the outer query.

#### Working Process:
1. The subquery is executed first as a derived table.
2. The result of the subquery is used by the outer query as if it were a table.

---

### 4. **Nested Subquery**

A **nested subquery** is when a subquery is placed inside another subquery. These subqueries are evaluated in a bottom-up approach, meaning the innermost subquery is executed first, and its result is passed to the next level of subquery or the outer query.

#### Example:
```sql
SELECT name
FROM employees
WHERE salary = (SELECT MAX(salary) FROM employees WHERE department_id = (SELECT department_id FROM departments WHERE name = 'HR'));
```
- In this query, there are two levels of subqueries:
  - The innermost subquery `(SELECT department_id FROM departments WHERE name = 'HR')` returns the `department_id` for the 'HR' department.
  - The second subquery `(SELECT MAX(salary) FROM employees WHERE department_id = ...)` finds the highest salary in that department.
  - The outer query returns the employee with that salary.
- **Execution:** The innermost subquery is executed first, then the second subquery, and finally the outer query.

#### Working Process:
1. The innermost subquery is executed first and passes its result to the next level.
2. The next subquery uses that result and passes its own result to the next query or outer query.
3. The outer query finally processes the result.

---

### 5. **Exists and Not Exists Subquery**

An **Exists subquery** checks for the existence of rows returned by the subquery. It returns `TRUE` if the subquery returns one or more rows, and `FALSE` otherwise. This type of subquery is typically used to check whether a certain condition is met.

#### Example:
```sql
SELECT name
FROM employees e
WHERE EXISTS (SELECT 1 FROM departments d WHERE e.department_id = d.department_id AND d.name = 'Sales');
```
- The subquery checks whether there is any department named 'Sales' that matches the employee's department. If so, the outer query returns the names of those employees.
- **Execution:** The subquery is evaluated for each row in the outer query, but it returns `TRUE` as soon as it finds a matching row.

#### Working Process:
1. For each row in the outer query, the subquery is executed.
2. The subquery checks for the existence of any rows matching the condition.
3. If the subquery finds a match, it returns `TRUE` and the outer query processes that row.

---

### 6. **Not Exists Subquery**

A **Not Exists subquery** is similar to `Exists`, but it returns `TRUE` if the subquery does not return any rows. It is typically used to filter out rows based on the absence of certain records.

#### Example:
```sql
SELECT name
FROM employees e
WHERE NOT EXISTS (SELECT 1 FROM departments d WHERE e.department_id = d.department_id AND d.name = 'HR');
```
- The subquery checks if the employee is not in the 'HR' department. If no matching rows are found, the outer query includes that employee.
- **Execution:** The subquery is executed for each row, and it returns `TRUE` if no rows are found.

---

### Summary of Subquery Types Based on Working:

| Type                        | Description                                                                               | Execution Behavior |
|-----------------------------|-------------------------------------------------------------------------------------------|--------------------|
| **Non-Correlated Subquery**  | Independent of the outer query and can be executed separately                             | Executed once      |
| **Correlated Subquery**      | Dependent on the outer query, executed for each row processed by the outer query           | Executed for each row |
| **Inline View Subquery**     | Subquery in the `FROM` clause, treated as a temporary table                               | Executed once      |
| **Nested Subquery**          | A subquery within another subquery, executed in a bottom-up manner                        | Innermost first    |
| **Exists Subquery**          | Returns `TRUE` if the subquery returns one or more rows                                   | Executed for each row |
| **Not Exists Subquery**      | Returns `TRUE` if the subquery returns no rows                                            | Executed for each row |

---

### Advantages of Subqueries Based on Working:

1. **Simplification**: Subqueries, especially non-correlated and inline views, simplify complex queries by breaking them down into smaller, modular pieces.
2. **Flexibility**: Correlated subqueries allow for flexible row-by-row comparisons, which can be hard to achieve with simple joins.
3. **Reusability**: Nested subqueries and inline views allow for the reusability of results within the main query.

### Disadvantages of Subqueries Based on Working:

1. **Performance Issues**: Correlated subqueries can lead to performance issues, especially with large datasets, as they are executed repeatedly for each row in the outer query.
2. **Complexity**: Nested and correlated subqueries can make the SQL code harder to understand, debug, and maintain.
3. **Execution Overhead**: Exists and Not Exists subqueries can sometimes be slower compared to using joins in certain scenarios, especially if the subquery returns many rows.

Would you like to explore the performance aspects or alternatives to subqueries (like joins) next?
