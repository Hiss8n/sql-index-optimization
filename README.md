# SQL Script Documentation

## Overview
This project contains a MySQL script named `answer.sql` that performs administrative database changes. It removes an index from the `customers` table and configures a user named `bob` with limited database access.

## File Purpose
The script is designed to:
- remove the `IdxPhone` index from the `customers` table
- create a local MySQL user named `bob`
- grant insert privileges to the `salesDB` database
- update the user's password

## SQL Statements

### 1. Remove the index
```sql
ALTER TABLE customers
DROP INDEX IdxPhone;
```
This statement deletes the `IdxPhone` index from the `customers` table. This may be required if the index is no longer used or if the table structure is being redesigned.

### 2. Create the user
```sql
CREATE USER 'bob'@'localhost' IDENTIFIED BY 'S$cu3r3!';
```
This creates a MySQL user named `bob` who can connect only from the local machine (`localhost`). The initial password is `S$cu3r3!`.

### 3. Grant permissions
```sql
GRANT INSERT ON salesDB.* TO 'bob'@'localhost';
```
This grants the user permission to insert records into all tables in the `salesDB` database. The privilege is limited to `INSERT`, so the user does not have full administrative rights.

### 4. Change the user password
```sql
ALTER USER 'bob'@'localhost' IDENTIFIED BY 'P$55!23';
```
This resets the password for the `bob` account to `P$55!23`.

## Notes
- The script assumes the database `salesDB` exists.
- The `IdxPhone` index must exist before it is dropped; otherwise, the statement will fail.
- Using hardcoded passwords in SQL files is not recommended for production environments.
- These commands should normally be executed by a database administrator with the proper privileges.

## Result
After executing the script:
- the `customers` table no longer has the `IdxPhone` index
- a local database user named `bob` exists
- `bob` can insert records into `salesDB`
- the password for `bob` is updated
