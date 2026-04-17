# Research

## 1. Class vs.Obgect

The easiest way to understand this is through the *"Blueprint Analogy"*

- **Class**: This is the blueprint or template . It defines what properties (data) and methods (behavior) an item will have , but it doesn't "exist" as a physical thing yet.

- **Object**: This is the actual instance built from the blueprint.

## 2.`$this` vs. `self::`

The difference depends on whether you are talking to a specific **instance** or the **class itself**.

- `$this`: Refers to the current object instance. You use it to access non-static properties and methods. Used for data that changes per object .

`ex`: 
```php
$this->name; //the name of this specific user
```

- `self::` : Refers to the class itself. You use it to access static properties, constants, or static methods. Used for data that is shared across all objects 

`ex`: 
```php
self::MIN_PASSWORD_LENGTH; //A rule that applies to the entire class, not just one user
```

## 3.Access Modifiers (Encapsulation)

These define the "visibility" of your code.

|Modifier|Visibility|
|----|----|
|`public`|Can be accessed from anywhere (inside or outside the class).|
|`protected`|Can only be accessed within the class itself or by "child" classes (inheritance).|
|`private`|Can only be accessed within the specific class where it was created|

## 4.Typed Properties

In older PHP versions, we didn't have to say what kind of data a property held. Typed Properties (introduced in PHP 7.4) allow you to explicitly declare the type.

- **Without Type**: `public $age;` (Could accidentally be assigned a string like "apple").

- **With Type**: `public int $age;` (PHP will throw an error if you try to put anything other than an integer here).

## 5.Constructor Methods

The `__construct()` method is a special function that runs automatically the moment you create a new object (using the `new` keyword)

### Why it’s useful to pass arguments:

Instead of creating an object and then manually setting all its data line-by-line, you can "inject" the necessary data right at the start.

`ex`:
```php
class User {
    public string $name;

    // The constructor sets the name immediately
    public function __construct($name) {
        $this->name = $name;
    }
}

// Creating the object and setting the data in one step
$user = new User("Shams");
```
This ensures that an object is never in an "incomplete" state; it has all the data it needs to function from the second it is born :)

