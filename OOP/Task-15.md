# Research

## 1. Inheritance

The main benefit of **Inheritance** is **code reusability**. It allows you to define a general class once and then create specialized versions of it without rewriting the common code. This creates a natural hierarchy and makes the codebase easier to maintain.

* **Parent Class (Base):** `Vehicle` (has attributes like `fuel` and `speed`).
* **Child Class (Derived):** `ElectricCar` (inherits `fuel` and `speed` but adds `batteryLevel`).

```cpp
class Vehicle {
public:
    int speed;
    void move() { /* shared logic */ }
};

class ElectricCar : public Vehicle {
public:
    int batteryLevel;
    // move() is inherited automatically!
};
```



----

## 2. The `final` Keyword

In C++ and similar languages, the `final` keyword acts as a "dead end" for specific parts of your code.

- **Before a Class:** It prevents any other class from inheriting from it.
- **Before a Method:** It prevents a child class from overriding that specific method.

### Why would a developer want to use this?

1.  **Design Integrity:** You want to ensure the logic in that class or method remains exactly as you wrote it.

2.  **Optimization:** It allows the compiler to perform "devirtualization," which can slightly improve performance because it knows exactly which function to call at compile-time.

----

## 3. Overriding Methods

To **override** a method means to provide a new, specific implementation in a child class for a method that already exists in the parent class. This allows the child to behave differently while keeping the same interface.

 ### How can you call the original parent method from inside the overridden one ?

using the **scope resolution operator** (`::`)

`ex` :

```cpp
void Dog::makeSound() {
    Animal::makeSound(); // Calls the parent version
    cout << "Bark!";     // Adds new behavior
}
```

----

## 4. Abstract Class vs. Interface
While both act as blueprints, they serve different architectural purposes:

| Feature | Abstract Class | Interface (Pure Virtual Class) |
| --- | --- | --- |
| **Purpose** | Defines what an object **is**. | Defines what an object **can do**. |
| **Implementation** | Can have both implemented and unimplemented methods. | Generally contains only method signatures (pure virtual). |
| **Variables** | Can have member variables (state). | Usually does not have variables. |

### Can a class implement multiple interfaces?

**Yes.** This is one of the primary reasons to use interfaces. While many languages *(like Java or C#)* forbid inheriting from multiple classes to avoid the "Diamond Problem," they allow implementing as many interfaces as needed.

---

## 5. Polymorphism
In simple terms, **Polymorphism** means "many forms." It is the ability of different objects to respond to the same function call in their own unique way.

`Example:`

Imagine a base class `Shape` with a method `draw()`.
- When you call `draw()` on a `Circle` object, it renders a curve.
- When you call `draw()` on a `Square` object, it renders four straight lines.

The programmer just calls `shape->draw()`, and the program "knows" which version to run based on the actual type of the object at runtime.