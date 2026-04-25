# Research

## 1. MVC Pattern
**MVC** stands for **Model, View, Controller**

- **Model**  
  Handles data and business logic.  
  It interacts with the database (e.g., SQL).

- **View**  
  Responsible for the user interface (UI).  
  Displays data using HTML/CSS.

- **Controller**  
  Acts as a middle layer.  
  It receives user input, communicates with the Model, and returns data to the View.

---

## 2. Routing
A **Router** is responsible for directing incoming requests to the correct part of the application.

It works like a **traffic cop**:
- `/home` → Home Controller  
- `/profile` → Profile Controller  

It reads the URL and decides which code should run.

---

## 3. Front Controller

A **Front Controller** means using a single entry point (usually `index.php`) for all requests

Instead of:
- `about.php`
- `contact.php`
- `profile.php`

You use:
- `index.php`

All requests go through this file, which then decides what to do using routing.

**Advantages:**
- Centralized control  
- Easier security handling  
- Cleaner project structure  

--- 
## 4. Clean URLs
Clean URLs look like:

``` 
example.com/users/profile 
```
instead of:

```
example.com/index.php?page=users&action=profile
```
**Why use them?**
- More readable  
- Better for SEO  
- Easier to remember  
- More professional  

---

## 5. Separation of Concerns
This principle means each part of the application should have a specific responsibility.

### Bad practice:

Putting SQL queries inside HTML files.


```html
<div>
  <?php
    $result = mysqli_query(...);
  ?>
</div>

```
### Problems:

- Hard to read and maintain
- Difficult to debug
- Security risks

### Good practice:

- Model → handles database (SQL)
- View → handles display (HTML)
- Controller → connects them