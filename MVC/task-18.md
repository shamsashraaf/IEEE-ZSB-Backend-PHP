# Research 

## 1. The Controller's Job

### When the user clicks the button:

1. The request goes to the Controller (through routing).
2. The Controller:
   -  Figures out what the user wants (view profile).
   -  Calls the Model to get data (e.g., user info from database).
   - Processes or prepares that data if needed.
3. Then it sends the data to the View.
4. Finally, the View generates the HTML page and returns it to the user.

----
## 2. Static HTML vs Dynamic PHP view

|Static HTML|Dynamic PHP view|
|:---|:---|
|Fixed content| Changes based on data|
|Same for every user |Dofferent per user|
|No logic|Contains PHP code|

`Ex`:

- **static html**

```html
<h1>welcome, shams</h1>

```

- **Dynamic PHP** :

```php
<h1> welcome, <?php echo $username; ?> </h1>

```

---
## 3. How Controller passes data to View

The Controller sends data as variables

`Ex`:

- **Controller**:

   ```php
   $userName = "Shams";
   include "view.php";
   ```
- **View (view.php)**:   

  ```php
  <h1>Hello, <?php echo $userName; ?></h1>
  ```
- **in frameworks** :
  
  ```php
  return view('profile', ['name' => $userName]);
  ```
---

## 4. Templating (Headers & Footers):
Instead of repeating code, we reuse parts.

`Ex`:

`header.php`
`footer.php`

- In your View:
  ```php
  include 'header.php';
  
  echo "<h1>Profile Page</h1>";
  
  include 'footer.php';
  ```
**So**:

   - Navigation bar = written once
   - Footer = written once
   - Reused everywhere  

*MVC* helps organize this cleanly.

---

## 5. Logic in Views: 

### Why NOT put heavy logic in Views?

- Makes code messy
- Hard to debug
- Breaks MVC principle
- Hard to reuse

**View should only**:
 -  Display data
 - Simple conditions (like if empty)