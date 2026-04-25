# Research

## 1. Traits

### How do "Traits" solve inhertiance problem ?

**PHP** doesn't allow a class to extend multiple classes *(no multiple inheritance)*. Traits allow you to reuse sets of methods across different classes without *inheritance*.

`ex`:
```php
trait Logger {
    public function log($message) {
        echo "Log: $message";
    }
}

trait Timestamp {
    public function getTimestamp() {
        return date('Y-m-d H:i:s');
    }
}

class User {
    use Logger, Timestamp;  // Using multiple traits
}

$user = new User();
$user->log("User created");  // Works
echo $user->getTimestamp();   // Works

```
----
### When to use them ?
  - When multiple classes share common functionality that doesn't fit in a parent class .
  - To avoid deep or rigid inheritance hierarchies.
  - When you need to compose behavior from multiple sources.

## 2. Namespaces

### What is a Namespace ?  
A namespace is a container that groups related classes, functions, and constants, preventing naming conflicts.

### How it prevents naming collisions ?  
Without namespace , you cannot have two classes named `User` 

`ex` :

```php
// File: ProjectA/Models/User.php
namespace ProjectA\Models;
class User { }

// File: ProjectB/Models/User.php  
namespace ProjectB\Models;
class User { }

// Using both
use ProjectA\Models\User as UserA;
use ProjectB\Models\User as UserB;

$user1 = new UserA();
$user2 = new UserB();  // No conflict!

```
Namespaces create virtual directories/containers, so `ProjectA\Models\User` and `ProjectB\Models\User` are treated as completely different classes.

----
## 3. Autoloading

### What is Autoloading ?

Autoloading is a mechanism that automatically loads class files when a class is first used (instantiated or referenced)

### How it saves time:

#### Before autoloading:

```php
require_once 'classes/User.php';
require_once 'classes/Product.php';
require_once 'classes/Order.php';
require_once 'classes/Payment.php';
// ... dozens or hundreds of requires

$user = new User();  // already loaded
$product = new Product();  // already loaded

```
#### With autoloading :

```php
spl_autoload_register(function ($className) {
    include 'classes/' . $className . '.php';
});

$user = new User();      // automatically loads User.php
$product = new Product(); // automatically loads Product.php
// no manual requires needed!
```

- no need to write/maintain long lists of `require` statements
- files load only when needed (lazy loading) - improves performance
- Easier code organizarion and refactoring 
- PSR-4 autoloading (Composer) is the modern standard

----

## 4. Magic Methods (`__get` and `__set`)

### What they are used for ?

- `__get($name)` - Triggered when reading an inaccessible or non-existent property
- `__set($name, $value)` - Triggered when writing to an inaccessible or non-existent property

### When they are triggered:

- Creating flexible objects with dynamic properties
- Implementing "magic" getters/setters for private/protected properties
- Creating data containers or DTOs
- Lazy loading of properties

----
## 5. Static Methods and Properties

### What does "static" mean?

Static methods and properties belong to the **class itself** , not to instances (objects) of the class. They are shared across all instances.

```php
class Counter {
    public static $count = 0;
    private static $instance = null;
    
    public static function increment() {
        self::$count++;
    }
    
    public static function getCount() {
        return self::$count;
    }
}

// Access without creating an object:
Counter::increment();
Counter::increment();
echo Counter::getCount();  // Output: 2

// Static property is shared:
$c1 = new Counter();
$c2 = new Counter();
// Both see the same static::$count value
```
### Do you need `new` keyword?  
**NO**. Static methods/properties are accessed using `ClassName::method()` without creating an object.

### When to use static:

- Utility/helper functions (`Math::calculate()`)
- Singleton pattern (`Database::getInstance()`)
- Factory methods (`User::createFromArray()`)
- Constants and class-level counters