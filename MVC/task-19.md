# Research Questions

# MVC, Security, and Database Concepts

## 1. In MVC: Which part communicates with the database? Why?

Only the **Model** should communicate directly with the database.

### Reason:
  - Ensures separation of concerns:
  - Model → handles data and database logic  
  - Controller → handles application logic  
  - View → handles presentation  
  - Makes the system easier to maintain, test, and debug  
  - Prevents mixing database code with user interface or control logic  

---

## 2. Why store sensitive information in a configuration file?

Sensitive data (e.g., database credentials) should not be hardcoded in main application files.

### Reasons:
- **Security:** Easier to protect and exclude from version control  
- **Maintainability:** Changes can be made in one place  
- **Flexibility:** Different environments (development, testing, production) can use different configurations  
- **Reduced risk:** Prevents accidental exposure when sharing code  

---

## 3. What is PDO in PHP? Why is it preferred over mysqli?

**PDO (PHP Data Objects)** is a database access layer that provides a consistent interface for interacting with databases.

### Advantages over mysqli:
- Supports multiple database systems (MySQL, PostgreSQL, SQLite, etc.)  
- Supports prepared statements  
- Provides consistent and clean syntax  
- Offers better error handling using exceptions  

---

## 4. How do Prepared Statements prevent SQL Injection?

Prepared statements separate SQL logic from user input.

### How they work:
1. The SQL query is defined with placeholders  
2. User input is bound to these placeholders  
3. The database treats input strictly as data, not executable code  

### Result:
- Prevents malicious input from altering the query structure  
- Protects against SQL Injection attacks  

---

## 5. Single row vs multiple rows (real-world examples)

### Single row:
- Fetching a user during login using email or ID  
- Retrieving a specific product by its ID  

```sql
SELECT * FROM users WHERE id = 5;
```
### Multiple rows:

 - Displaying a list of products in an online store
 - Showing all students in a course
 - Listing blog posts on a homepage

```sql
SELECT * FROM users WHERE id = 5;
```
