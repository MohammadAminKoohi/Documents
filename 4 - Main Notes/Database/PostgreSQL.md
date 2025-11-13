
2024-08-18 15:13

Status: 

Tags: #Database #Backend

# PostgreSQL

**SQL**: Structured Query Language

## Database Operations

- **Create Database**:
  ```sql
  CREATE DATABASE <NAME>;
  ```

- **Drop Database**:
  ```sql
  DROP DATABASE <NAME>;
  ```

## Table Operations

- **Create Table**:
  ```sql
  CREATE TABLE <NAME> (
      column_name data_type constraints,
      ...
  );
  ```

- **Drop Table**:
  ```sql
  DROP TABLE <NAME>;
  ```

- **Alter Table**:
  - **Add a column**:
    ```sql
    ALTER TABLE <TABLE_NAME> ADD COLUMN column_name data_type;
    ```

  - **Alter column type**:
    ```sql
    ALTER TABLE <TABLE_NAME> ALTER COLUMN column_name TYPE new_data_type;
    ```

- **Rename Table**:
  ```sql
  ALTER TABLE <old_name> RENAME TO <new_name>;
  ```

- **Rename Column**:
  ```sql
  ALTER TABLE <TABLE_NAME> RENAME COLUMN <old_column_name> TO <new_column_name>;
  ```

## Data Manipulation

- **Insert Data**:
  ```sql
  INSERT INTO <TABLE_NAME> (
      column1, column2
  ) VALUES (
      value1, value2
  );
  ```

- **Update Data**:
  ```sql
  UPDATE <TABLE_NAME> 
  SET column1 = value1, column2 = value2
  WHERE condition;
  ```

- **Delete Data**:
  ```sql
  DELETE FROM <TABLE_NAME> 
  WHERE condition;
  ```

## Data Querying

- **Select Data**:
  ```sql
  SELECT column1, column2
  FROM <TABLE_NAME>
  WHERE condition
  ORDER BY column1 ASC|DESC
  LIMIT number;
  ```

- **Select All Columns**:
  ```sql
  SELECT * FROM <TABLE_NAME>;
  ```

- **Select Distinct**:
  ```sql
  SELECT DISTINCT column1 FROM <TABLE_NAME>;
  ```

- **Select with Joins**:
  - **Inner Join**:
    ```sql
    SELECT column1, column2
    FROM <TABLE1>
    INNER JOIN <TABLE2> ON <TABLE1>.common_column = <TABLE2>.common_column;
    ```

  - **Left Join**:
    ```sql
    SELECT column1, column2
    FROM <TABLE1>
    LEFT JOIN <TABLE2> ON <TABLE1>.common_column = <TABLE2>.common_column;
    ```

  - **Right Join**:
    ```sql
    SELECT column1, column2
    FROM <TABLE1>
    RIGHT JOIN <TABLE2> ON <TABLE1>.common_column = <TABLE2>.common_column;
    ```

  - **Full Outer Join**:
    ```sql
    SELECT column1, column2
    FROM <TABLE1>
    FULL OUTER JOIN <TABLE2> ON <TABLE1>.common_column = <TABLE2>.common_column;
    ```

- **Aggregate Functions**:
  - **Count**:
    ```sql
    SELECT COUNT(column_name) FROM <TABLE_NAME>;
    ```

  - **Sum**:
    ```sql
    SELECT SUM(column_name) FROM <TABLE_NAME>;
    ```

  - **Average**:
    ```sql
    SELECT AVG(column_name) FROM <TABLE_NAME>;
    ```

  - **Min**:
    ```sql
    SELECT MIN(column_name) FROM <TABLE_NAME>;
    ```

  - **Max**:
    ```sql
    SELECT MAX(column_name) FROM <TABLE_NAME>;
    ```

- **Group By**:
  ```sql
  SELECT column1, COUNT(*)
  FROM <TABLE_NAME>
  GROUP BY column1;
  ```

- **Having**:
  ```sql
  SELECT column1, COUNT(*)
  FROM <TABLE_NAME>
  GROUP BY column1
  HAVING COUNT(*) > number;
  ```

- **Order By**:
  ```sql
  SELECT column1, column2
  FROM <TABLE_NAME>
  ORDER BY column1 ASC|DESC;
  ```

- **Limit**:
  ```sql
  SELECT column1, column2
  FROM <TABLE_NAME>
  LIMIT number;
  ```

## Database Management

- **Connect to Database**:
  ```bash
  \c <database>
  ```

- **Show Databases**:
  ```bash
  \l
  ```

- **Show Tables**:
  ```bash
  \dt
  ```

- **Show Table Schema**:
  ```bash
  \d <TABLE_NAME>
  ```

- **Execute SQL File**:
  ```bash
  \i <PATH>
  ```

- **List All Tables and Views**:
  ```bash
  \d
  ```

### LIMIT and OFFSET

- **Limit**:
  - Restricts the number of rows returned by a query.
  ```sql
  SELECT column1, column2
  FROM <TABLE_NAME>
  LIMIT number_of_rows;
  ```

- **Offset**:
  - Skips a specified number of rows before beginning to return rows.
  - Often used together with `LIMIT` for pagination.
  ```sql
  SELECT column1, column2
  FROM <TABLE_NAME>
  LIMIT number_of_rows OFFSET offset_value;
  ```

- **Example**:
  - Retrieve 10 rows starting from the 6th row in the result set.
  ```sql
  SELECT * FROM employees
  LIMIT 10 OFFSET 5;
  ```

### BETWEEN

- **Between**:
  - Filters the result set to include only rows where a column's value falls within a specified range.
  - The range is inclusive, meaning the boundary values are included.
  ```sql
  SELECT column1, column2
  FROM <TABLE_NAME>
  WHERE column_name BETWEEN value1 AND value2;
  ```

- **Example**:
  - Find employees whose salaries are between 40,000 and 60,000.
  ```sql
  SELECT * FROM employees
  WHERE salary BETWEEN 40000 AND 60000;
  ```

### LIKE

- **Like**:
  - Used to search for a specified pattern in a column.
  - `%` represents any sequence of characters (including none).
  - `_` represents any single character.
  ```sql
  SELECT column1, column2
  FROM <TABLE_NAME>
  WHERE column_name LIKE 'pattern';
  ```

- **Example**:
  - Find all employees whose names start with 'A'.
  ```sql
  SELECT * FROM employees
  WHERE name LIKE 'A%';
  ```

- **Example**:
  - Find all employees whose names have 'n' as the second character.
  ```sql
  SELECT * FROM employees
  WHERE name LIKE '_n%';
  ```

## Indexes and Constraints

- **Create Index**:
  ```sql
  CREATE INDEX index_name ON <TABLE_NAME> (column_name);
  ```

- **Drop Index**:
  ```sql
  DROP INDEX index_name;
  ```

## Views and Functions

- **Create View**:
  ```sql
  CREATE VIEW view_name AS
  SELECT column1, column2
  FROM <TABLE_NAME>
  WHERE condition;
  ```

- **Drop View**:
  ```sql
  DROP VIEW view_name;
  ```

- **Create Function**:
  ```sql
  CREATE FUNCTION function_name (parameters)
  RETURNS return_type AS $$
  BEGIN
      -- Function body
  END;
  $$ LANGUAGE plpgsql;
  ```

## Backup and Restore

- **Backup Database**:
  ```bash
  pg_dump -U username -d database_name -f backup_file.sql
  ```

- **Restore Database**:
  ```bash
  psql -U username -d database_name -f backup_file.sql
  ```

## Additional Resources

- [PostgreSQL Data Types](https://www.postgresql.org/docs/current/datatype.html)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
