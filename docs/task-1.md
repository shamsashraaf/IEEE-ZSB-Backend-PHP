# Documentation 

### PHP : 
  is a server-side programming language used mainly for building dynamic websites and web applications.

and this is your first `php` tag   

``` php 
//  print Hello world 
<?php echo "Hello World" ?>

// <?php ?> so the compiler know this is php 
// echo used to print output 

```

weird syntax ?!.. **let's get through it** 

---
## Variables 

To declare a variable we use `$` and then we give it a name

EX 

```php

<?php 
$greeting = "Hello World"; // "" or '' can be used with a string

echo $greeting; 

?>

```
Note : 
You can use `<?= $greeting ?>` instead of `<?php echo $greeting ?>`

 ---
## Concatination

We use `.` to concatenate two strings 

`Ex`
```php
<?php 
$name = "shams";

echo "hello " . $name; 

// we can also do this 
echo "hello $name";
?>
```
---
## Conditions
You can also make descions with `PHP`

Ex
```php
<?php 
$name = "Dark Matter";
$read = true ;            // you just met our first boolean

if($read){                //if read = true .. yep php understand that 
 $message = "You have read $name";
}else{                                     //if read = false
 $message = "You have NOT read $name";
}

echo $message;
?>
```
there is another short way called ( **Ternary shorthand** )
Ex
```php
echo $read? "You have read $name":"You have NOT read $name";
```
---
## Arrays

To declare and initialize an array in `PHP`, we create a variable (e.g., `$books`) and use `[]` to initialize it and to print it we use `foreach` statment and you can also use the famous zero-based index.

Ex
```php
<?php 
$books = [
        "Do Androids Dream of Electric Sheep",
        "The langoliers",
        "Hail Mary"
       ];

 foreach($books as $book ){
    echo $book;
 }  
 
 <?= $books[0] > // "Do Androids Dream of Electric Sheep"
 <?= $books[1] > // "The langoliers"
 <?= $books[2] > // "Hail Mary"
 
?>

```
You can store more than one list

Ex 
```php
<?php 
$books = [
    [
        "Do Androids Dream of Electric Sheep",
        "Philip k.Dick",
        "http://example.com",
    ],
    [
        "Progecgt Hail Mary",
        "Andy Weir",
        "http://example.com"
    ]
];

<?= $books[0][0];> // "Do Androids Dream of Electric Sheep"
<?= $books[0][1];> // "Philip k.Dick"
<?= $books[0][2];> // "http://example.com",


?>
```
### Associative Arrays

to link the list member with a `key` , we use that `key` to access them instead of using numbers

Ex 
```php
<?php 
$books = [
    [
       "name"        => "Do Androids Dream of Electric Sheep",
       "author"     => "Philip k.Dick",
       "purchaseUrl" => "http://example.com",
    ],
    [
        "name"        => "Progecgt Hail Mary",
        "author"      => "Andy Weir",
        "purchaseUrl" => "http://example.com"
    ]
];
    <?= $books[0]["name"]>; // "Do Androids Dream of Electric Sheep"
    <?= $books[1]["name"]>; // "Progecgt Hail Mary"

    foreach($books as $book){ //with foreach
    echo $book[name]; 
}
```
---
## Functions 

A function is declared with `function` key word ,we give it a name if it's a `named function ` , we can called it later using it's name

Ex 
```php
function filterByAuthor($books,$author){  
 $filterBooks = [];

 foreach ($books as $book) {
    if($book['author']===$author){
        $filterBooks[]=$book;
    }
 }
 return $filterBooks;
}

 <?php foreach (filterByAuthor($books,"Philip k.Dick") as $book) : ?> //itirate over the return of the "filterByAuthor" 
    <li>
        <a href="<?= $book['purchaseUrl'] ?>">
            <?= $book["name"];?> (<?= $book ['releaseYear'] ?>) - By <?= $book['author'] ?>
        </a>
    </li>
    
   <?php endforeach?>   

```

> there is a bit *HTML* here ..*PHP* can be written alongside *HTML* just be carful with tags to avoid syntax error 
### Anonymous Functions (lambda function)

you can assign a function to a variable instead of giving it a name 
and then you have an `anonymous function`

Ex
```php

$filterByAuthor = function ($books,$author){ // notice that we're using "$filterByAuthor" variable
 $filterBooks = [];

 foreach ($books as $book) {
    if($book['author']===$author){
        $filterBooks[]=$book;
    }
 }
 return $filterBooks;
}
?>
   <?php foreach ($filterByAuthor($books,"Philip k.Dick") as $book) : ?> // using the variable to call the function
    <li>
        <a href="<?= $book['purchaseUrl'] ?>">
            <?= $book["name"];?> (<?= $book ['releaseYear'] ?>) - By <?= $book['author'] ?>
        </a>
    </li>
    
   <?php endforeach?>

```
This example was very naive. **PHP** provides a predefined function like `array_filter`, which returns elements that satisfy a given condition *"in a callback function"*.

Ex
```php
<?php 
foreach(array_filter($books,
function($book){return $book['author']==='Philip k.Dick';})  as $book)
{
    <li>
        <a href="<?= $book['purchaseUrl'] ?>">
            <?= $book["name"];?> (<?= $book ['releaseYear'] ?>) - By <?= $book['author'] ?>
        </a>
    </li>

}

//This short, neat code does the same thing as the previous one
?>
```













