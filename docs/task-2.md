# Documentation

## 1- Database Tables and Indexes

- creating notes and users table 
- enforcing unique emails for users
- linking notes to users using the **Foreign Key** `user_id` 
- test cascade deletes "if we deleted some user his notes will be deleted as well"

## 2- Render the Notes and Note Page

- **adding routes**

    we added in `router.php` routes for `note, notes and note-create` 

     so now the array in the router.php becomes

     ```php
     <?php
      
     return [
         '/'             => 'controllers/index.php',
         '/about'        => 'controllers/about.php',
         '/contact'      => 'controllers/contact.php',
         '/notes'        => 'controllers/notes.php',
         '/note'         => 'controllers/note.php',
         '/note/create'  => 'controllers/note-create.php',
     ];
     
     ```
- We added new **controllers** and **views** to handle and display the new routes.     

>In the end, we were able to display all the notes written by a user and generate a separate page for each note based on its ID.

## 3- Introduction to Authorization 

The goal is to ensure users cannot access `notes` that do not belong to them.

```php
<?php
//                                    controllers/note.php
$config = require 'config.php';

$db = new Database($config['database']);


$heading = "Note";
$currentUserId=1;



$note = $db->query("SELECT * FROM notes where  id = :id ", ['id' => $_GET['id']])->fetch();

if(!$note){   //If the id does not match any record in the database -> display the 404 "not found page"
    
    abort();
}

if($note['user_id']!==$currentUserId){ //If the note does not belong to the current user -> display 403 "forbidden"
    abort(Response::FORBIDDEN);

    // Response class holds constants for HTTP status codes (404, 403)
}

require "views/note.view.php";

```
We're handling too many responsibilities in `note.php`. I can refactor that.

## 4- Programming is Rewriting

so we added these functions to `Database.php`

```php
// Retrieve all notes belonging to a specific user
    public function get()
    {
        return $this->statement->fetchall();
    }

// Retrieve one specific note belonging to the user
    public function find()
    {
        return $this->statement ->fetch();
    }
    
// Validate existence during fetch; avoids an extra conditional

    public function findOrFail()
    {
        $result = $this ->find();

        if(!$result){
            abort();
        }

        return $result;
    }


``` 
Add this function to `functions.php`

```php
// Authorize that this note is accessible by the current user
function authorize($condition,$status=Response::FORBIDDEN){
    if(! $condition){
        abort($status);
    }
}
```

## 5-Note taking and validation stuff

The goal is to get a note from the user..Here’s what we added to make it happen.

- A form was added in `note-create.view.php` to allow users to create a note.

- the note must be valid to the database so 

```php
//Validator.php

<?php

class Validator
{
    public static function string($value, $min = 1, $max = INF)  // this is a pure class 
    {
        $value = trim($value);

        return strlen($value) >= $min && strlen($value) <= $max;
    }



    public static function email($value)
    {

        return filter_var($value, FILTER_VALIDATE_EMAIL);
    }
}


```
```php
// controllers/note-create.php
if ($_SERVER['REQUEST_METHOD'] === "POST") {

    $errors = [];


    if (! Validator::string($_POST['body'],1,1000)) {

        $errors['body'] = 'The body is invalid';
    }

    
    if (empty($errors)) {
        $db->query("INSERT INTO `notes` (body,user_id) VALUES (:body, :user_id) ", 
        [
            'body' => $_POST['body'],    
            'user_id' => 1
        ]);
    }
}


```
