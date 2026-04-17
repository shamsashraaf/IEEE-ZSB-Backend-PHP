# Security 


## 1. Code Architecture and Refactoring

### Modularization with Functions

The first step in securing a codebase is moving away from ***"spaghetti code"*** where database logic is mixed with HTML.

- **Separation of Concerns:** Connection logic and query execution should be moved into a dedicated file (e.g., `functions.php`).

- **Database Wrappers:** Creating a `connect()` function and a `db_read()` function allows you to update connection credentials or query logic in one place rather than on every page.

### Transitioning to Object-Oriented Programming (OOP)

Moving to a class-based structure enhances security through abstraction and inheritance.

 - **Class Abstraction:** Create a `Database` class for core connections and specific classes (e.g., `User`, `Posts`) for table-specific logic.

- **Inheritance:** By having the `User` class `extend` the `Database` class, it inherits database access without rewriting the connection code.

-  **Access Modifiers:** Use `private` for internal methods like `connect()` so they cannot be triggered from outside the class, and `public` for methods intended for use in the application.

-----

## 2. Authentication and Authorization

### Secure Login Messaging

A common security flaw is "User Enumeration," where specific error messages reveal whether an account exists.

- **Generic Errors:** Never specify which part of the login failed. Instead of "Wrong Password" or "Wrong Email," use a unified message: **"Wrong email or password."**

- **Session Management:** Centralize `session_start()` at the entry point of the application (e.g., `index.php`) to ensure session data is available across all pages consistently.

### Principle of Least Privilege (Access Control)

Users should only have the minimum level of access required to perform their tasks.
- **Role-Based Access Control (RBAC):** Implement a "rank" or "level" column in the database (e.g., Admin, Editor, User).

- **Access Verification Function:** Use a centralized `access()` function that checks the current user's rank against the required rank for a specific page or action.

- **Hierarchy Mapping:** Ensure that higher ranks (Admin) automatically inherit the permissions of lower ranks (Editor/User) by using "allowed" arrays in the logic.

----

## 3. Mitigating SQL Injection

SQL Injection occurs when user input is treated as part of the SQL command.

### POST Injection (Forms)

- **Input Sanitization:** Use `addslashes()` to escape single quotes, preventing users from "breaking out" of the SQL string.

- **Server-Side Validation:** Use PHP’s `filter_var()` with `FILTER_VALIDATE_EMAIL` to ensure the input matches the expected format before it ever touches a database query.

### GET Injection (URLs)

- **URL Manipulation:** Attackers can append `UNION SELECT` or `ORDER BY` statements to URL parameters (e.g., `post.php?id=4`).

- **Type Casting:** If a parameter is expected to be an integer (like an ID), explicitly cast it using `(int)$_GET['id']`. This strips all malicious text and reduces the value to a safe number.

### The Gold Standard: Prepared Statements (PDO)

The most effective defense against SQLi is separating the query structure from the data.

- **PDO (PHP Data Objects):** Using PDO allows for a unified interface for multiple database types and supports native prepared statements.

- **Placeholders:** Instead of inserting variables directly into the query, use named placeholders (e.g., `:id`).

* **Data Binding:** Send the user data as a separate array during execution. The database engine treats this data strictly as a literal value, making it impossible to execute as code.

-----

## 4. Preventing Cross-Site Scripting (XSS)

XSS occurs when malicious scripts **(JavaScript/PHP)** are injected into the database and then rendered in another user's browser.

- **Impact:** Attackers can use `document.cookie` to steal session IDs and hijack user accounts.

- **Output Cleaning:** Every piece of data retrieved from a database or URL must be "cleaned" before being printed to HTML.

- **Escaping HTML:** Use `htmlspecialchars()` to convert characters like `<` and `>` into their HTML entity equivalents (`&lt;` and `&gt;`). This prevents the browser from interpreting the text as a script tag.

- **Consistency:** Wrap this in a global `clean()` function so you can easily update your sanitization strategy across the entire site.

