# 🧑‍💻 Mastering OOP: Python vs Java vs JavaScript/TypeScript

Object-Oriented Programming (OOP) is a fundamental paradigm that makes code **modular, reusable, and maintainable**. Whether you are coding in **Python, Java, or JavaScript/TypeScript**, the core **4 pillars of OOP** remain the same:

* **Encapsulation**
* **Abstraction**
* **Inheritance**
* **Polymorphism**

In this blog, we’ll explore all four with **examples in Python, Java, and JS/TS**, along with insights into **compile-time overloading**, **static methods**, and the classic **abstract class vs interface** question.

---

## 🔹 1. Encapsulation

Encapsulation means **binding data and methods together** inside a class, restricting direct access to internal details.

**Python Example**

```python
class Account:
    def __init__(self, balance):
        self.__balance = balance  # private attribute

    def deposit(self, amount):
        self.__balance += amount

    def get_balance(self):
        return self.__balance
```

**Java Example**

```java
class Account {
    private double balance;

    public Account(double balance) {
        this.balance = balance;
    }

    public void deposit(double amount) {
        balance += amount;
    }

    public double getBalance() {
        return balance;
    }
}
```

**TypeScript Example**

```ts
class Account {
    private balance: number;

    constructor(balance: number) {
        this.balance = balance;
    }

    deposit(amount: number) {
        this.balance += amount;
    }

    getBalance(): number {
        return this.balance;
    }
}
```

---

## 🔹 2. Abstraction

Abstraction hides **implementation details** and exposes only the **essential features**.

**Python Example**

```python
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass

class Circle(Shape):
    def __init__(self, r):
        self.r = r

    def area(self):
        return 3.14 * self.r * self.r
```

**Java Example**

```java
abstract class Shape {
    abstract double area();
}

class Circle extends Shape {
    double r;
    Circle(double r) { this.r = r; }
    double area() { return 3.14 * r * r; }
}
```

**TypeScript Example**

```ts
abstract class Shape {
    abstract area(): number;
}

class Circle extends Shape {
    constructor(private r: number) { super(); }
    area(): number { return 3.14 * this.r * this.r; }
}
```

---

## 🔹 3. Inheritance

Inheritance lets one class **reuse properties/methods of another**.

**Python Example**

```python
class Animal:
    def sound(self):
        print("Some sound")

class Dog(Animal):
    def sound(self):
        print("Bark")
```

**Java Example**

```java
class Animal {
    void sound() { System.out.println("Some sound"); }
}

class Dog extends Animal {
    void sound() { System.out.println("Bark"); }
}
```

**TypeScript Example**

```ts
class Animal {
    sound() { console.log("Some sound"); }
}

class Dog extends Animal {
    sound() { console.log("Bark"); }
}
```

---

## 🔹 4. Polymorphism

Polymorphism means **many forms**—the same method name behaves differently based on the object.

**Python Example**

```python
class Animal:
    def speak(self): print("Animal sound")

class Dog(Animal):
    def speak(self): print("Bark")

class Cat(Animal):
    def speak(self): print("Meow")

for a in [Dog(), Cat()]:
    a.speak()
```

**Java Example**

```java
class Animal {
    void speak() { System.out.println("Animal sound"); }
}

class Dog extends Animal {
    void speak() { System.out.println("Bark"); }
}

class Cat extends Animal {
    void speak() { System.out.println("Meow"); }
}

public class Main {
    public static void main(String[] args) {
        Animal a1 = new Dog();
        Animal a2 = new Cat();
        a1.speak();  // Bark
        a2.speak();  // Meow
    }
}
```

**TypeScript Example**

```ts
class Animal {
    speak() { console.log("Animal sound"); }
}

class Dog extends Animal {
    speak() { console.log("Bark"); }
}

class Cat extends Animal {
    speak() { console.log("Meow"); }
}

let animals: Animal[] = [new Dog(), new Cat()];
animals.forEach(a => a.speak());
```

---

## 🔹 Compile-Time Overloading

**Method Overloading** → Same method name, different parameter lists.

* ✅ **Java supports it** (compile-time decision).
* ❌ **Python/JS don’t** (last method wins, but can mimic using `*args`, default params, or function overloading utilities).

**Java Example**

```java
class MathUtils {
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
    int add(int a, int b, int c) { return a + b + c; }
}
```

**Python Workaround**

```python
class MathUtils:
    def add(self, *args):
        return sum(args)

m = MathUtils()
print(m.add(2, 3))      # 5
print(m.add(2, 3, 4))   # 9
```

**TypeScript Example**

```ts
class MathUtils {
    add(a: number, b: number): number;
    add(a: number, b: number, c: number): number;
    add(a: number, b: number, c?: number): number {
        return c !== undefined ? a + b + c : a + b;
    }
}

const m = new MathUtils();
console.log(m.add(2, 3));     // 5
console.log(m.add(2, 3, 4));  // 9
```

---

## 🔹 Static Methods

A **static method** belongs to the class, not to objects. Useful for **utilities and helpers**.

**Python Example**

```python
class MathUtils:
    @staticmethod
    def square(x): return x * x

print(MathUtils.square(5))  # 25
```

**Java Example**

```java
class MathUtils {
    public static int square(int x) {
        return x * x;
    }
}

System.out.println(MathUtils.square(5)); // 25
```

**TypeScript Example**

```ts
class MathUtils {
    static square(x: number): number {
        return x * x;
    }
}

console.log(MathUtils.square(5)); // 25
```

---

## 🔹 Abstract Class vs Interface

Both are used for **abstraction**, but differ in purpose and flexibility.

### Abstract Class

* Cannot be instantiated.
* Can have **abstract + concrete methods**.
* Can hold **fields, constructors, and state**.
* Use when classes share **common state/behavior**.

### Interface

* Defines a **contract** (only methods/properties).
* A class can **implement multiple interfaces** (supports multiple inheritance).
* Use when you need to define **roles/capabilities**.

**Java Example**

```java
abstract class Animal {
    String name;
    Animal(String name) { this.name = name; }
    
    abstract void sound();
    void eat() { System.out.println(name + " eats food."); }
}

interface Pet {
    void play();
}

class Dog extends Animal implements Pet {
    Dog(String name) { super(name); }

    void sound() { System.out.println("Bark"); }
    public void play() { System.out.println("Dog plays fetch."); }
}
```

**TypeScript Example**

```ts
abstract class Animal {
    constructor(public name: string) {}
    abstract sound(): void;
    eat() { console.log(`${this.name} eats food.`); }
}

interface Pet {
    play(): void;
}

class Dog extends Animal implements Pet {
    sound() { console.log("Bark"); }
    play() { console.log("Dog plays fetch."); }
}
```

**Python Example**

```python
from abc import ABC, abstractmethod

class Animal(ABC):
    def __init__(self, name):
        self.name = name

    @abstractmethod
    def sound(self): pass

    def eat(self):
        print(f"{self.name} eats food.")

class Pet(ABC):
    @abstractmethod
    def play(self): pass

class Dog(Animal, Pet):
    def sound(self):
        print("Bark")

    def play(self):
        print("Dog plays fetch.")
```

---

## 🔹 Abstract Class vs Interface (Comparison)

| Feature                  | Abstract Class                              | Interface                                   |
| ------------------------ | ------------------------------------------- | ------------------------------------------- |
| **Purpose**              | Base class with shared **state + behavior** | Contract defining **capabilities**          |
| **Implementation**       | Can have **abstract + concrete methods**    | Only abstract methods (Java < 8)            |
| **Fields/Variables**     | Allowed (instance + static)                 | Only constants (in Java)                    |
| **Multiple Inheritance** | ❌ Only one abstract class (Java)            | ✅ Multiple interfaces allowed               |
| **When to use**          | When classes share **common code/state**    | When classes need to **guarantee behavior** |

---

## ✅ Final Thoughts

* **Encapsulation** → Data hiding
* **Abstraction** → Hiding implementation, showing interface
* **Inheritance** → Reuse through hierarchy
* **Polymorphism** → Same method, different behavior
* **Compile-Time Overloading** → Only in statically typed languages like Java, TS
* **Static Methods** → Belong to class, not object
* **Abstract vs Interface** → Base behavior vs role/capability

👉 Mastering these concepts in **Python, Java, and JavaScript/TypeScript** makes you interview-ready and improves your cross-language coding skills.
