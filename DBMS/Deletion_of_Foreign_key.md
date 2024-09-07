The error you're encountering suggests that the `Flight_No` column cannot be dropped because it's part of a foreign key constraint (`fk_flight`). To resolve this issue, you need to:

1. **Find the Correct Foreign Key Constraint Name**: Ensure that you have the correct name of the foreign key constraint associated with the `Flight_No` column. 

2. **Drop the Foreign Key Constraint**: Remove the foreign key constraint before attempting to drop the column.

Here's a step-by-step approach:

### 1. Identify the Foreign Key Constraint

Run this query to find out the foreign key constraints associated with `booking_info`:

```sql
SELECT CONSTRAINT_NAME
FROM information_schema.KEY_COLUMN_USAGE
WHERE TABLE_NAME = 'booking_info'
  AND COLUMN_NAME = 'Flight_No'
  AND REFERENCED_TABLE_NAME IS NOT NULL;
```

### 2. Drop the Foreign Key Constraint

Assuming you find the foreign key constraint name (let's say it's `fk_flight`), use the following command to drop it:

```sql
ALTER TABLE booking_info
DROP FOREIGN KEY fk_flight;
```

### 3. Drop the Column

After removing the foreign key constraint, you can now drop the `Flight_No` column:

```sql
ALTER TABLE booking_info
DROP COLUMN Flight_No;
```

### Example Workflow

1. **Find Foreign Key Constraint Name**:

   ```sql
   SELECT CONSTRAINT_NAME
   FROM information_schema.KEY_COLUMN_USAGE
   WHERE TABLE_NAME = 'booking_info'
     AND COLUMN_NAME = 'Flight_No'
     AND REFERENCED_TABLE_NAME IS NOT NULL;
   ```

2. **Drop the Foreign Key Constraint**:

   ```sql
   ALTER TABLE booking_info
   DROP FOREIGN KEY fk_flight;  -- Replace with the actual constraint name
   ```

3. **Drop the Column**:

   ```sql
   ALTER TABLE booking_info
   DROP COLUMN Flight_No;
   ```

By following these steps, you should be able to drop the column after removing the foreign key constraint. If you need further help with the exact names or queries, let me know!
