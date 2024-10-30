# Databases

Stores all data for a web app.  

-  Accessed via the application server (API)  
- Data is often structured (tables, columns, rows)  
- Stores: user info, login credentials, etc...  

Types of databases:  
- Spreadsheets (csv): Google sheets, excel.  
  - Useful for humans, not useful for programs.  
- Relational databases (sql): MySQL, postgreSQL  
  - Structured data with fixed schema.  
  - Commonly used, pretty scalable.  
- Non-relational databases (no sql): MongoDB
  - Semi-structured data with flexible schema.  
  
Structure of SQL:  
- Organized in columns (ie: ID, Name, Address), and rows (1, 2, 3...)  

### SQL  

Allows us to write scripts to access and manipulate our database.  

- `SELECT * FROM users;` Retrieve information for all users.  

> `*` represents 'all'  

- `SELECT * FROM users WHERE user_id = 1;` Retrieve from specific user.  

- `UPDATE users SET email = 'test@gmail.com' WHERE user_id = 1;` Update information.  

- `DELETE FROM users ...` etc...

#### MySQL  

A database management system, that uses SQL.  

Setup: Once a connection is created...  

