# Rust Cheat Sheet

This cheat sheet provides a quick reference for Rust programming, covering syntax, data types, control flow, functions, structs, enums, error handling, and more.

## Table of Contents

1. [Basics](#1-basics)
   - [Comments](#comments)
   - [Variables](#variables)
   - [Data Types](#data-types)
2. [Control Flow](#2-control-flow)
3. [Functions](#3-functions)
4. [Structs](#4-structs)
5. [Enums](#5-enums)
6. [Traits](#6-traits)
7. [Error Handling](#7-error-handling)
8. [Modules](#8-modules)
9. [Crates and Packages](#9-crates-and-packages)
10. [Common Collections](#10-common-collections)
11. [Ownership and Borrowing](#11-ownership-and-borrowing)
12. [Concurrency](#12-concurrency)

## 1. Basics

### Comments
```rust
// Single-line comment

/* 
   Multi-line comment 
*/
```

### Variables
Immutable by default:
```rust
let x = 5;
```
Mutable:
```rust
let mut y = 10;
y += 5; // y is now 15
```

### Data Types
Scalar Types:

* Integers: i32, u32, i64, u64, etc.
* Floating-point: f32, f64
* Boolean: bool
* Character: char

Compound Types:

* Tuple:
```rust
let tup: (i32, f64, char) = (500, 6.4, 'z');
```
* Array:
```rust
let arr: [i32; 5] = [1, 2, 3, 4, 5]; // Fixed size array
```

## 2. Control Flow

### Conditional Statements
```rust
if condition {
    // code
} else if another_condition {
    // code
} else {
    // code
}
```

### Loops
Loop:
```rust
loop {
    // code
    if some_condition {
        break; // Exit loop
    }
}
```
While Loop:
```rust
while condition {
    // code
}
```
For Loop:
```rust
for i in 0..5 { // 0 to 4
    // code
}

// For iterating over an array
for item in arr.iter() {
    println!("{}", item);
}
```

## 3. Functions

### Function Definition
```rust
fn function_name(parameters: Type) -> ReturnType {
    // code
    return value; // Optional return statement
}
```

### Example Function
```rust
fn add(x: i32, y: i32) -> i32 {
    x + y // No need for 'return'
}
```

### Calling a Function
```rust
let result = add(5, 10);
println!("Result: {}", result);
```

## 4. Structs

### Struct Definition
```rust
struct Person {
    name: String,
    age: u32,
}
```

### Struct Instantiation
```rust
let person = Person {
    name: String::from("Alice"),
    age: 30,
};
```

### Accessing Struct Fields
```rust
println!("Name: {}, Age: {}", person.name, person.age);
```

## 5. Enums

### Enum Definition
```rust
enum Direction {
    Up,
    Down,
    Left,
    Right,
}
```

### Using Enums
```rust
let dir = Direction::Up;
match dir {
    Direction::Up => println!("Moving up!"),
    Direction::Down => println!("Moving down!"),
    _ => println!("Moving sideways!"),
}
```

## 6. Traits

### Defining a Trait
```rust
trait Speak {
    fn speak(&self);
}
```

### Implementing a Trait
```rust
struct Dog;

impl Speak for Dog {
    fn speak(&self) {
        println!("Woof!");
    }
}
```

### Using Traits
```rust
let dog = Dog;
dog.speak(); // Outputs: Woof!
```

## 7. Error Handling

### Result Type
```rust
fn divide(dividend: f64, divisor: f64) -> Result<f64, String> {
    if divisor == 0.0 {
        Err(String::from("Cannot divide by zero!"))
    } else {
        Ok(dividend / divisor)
    }
}
```

### Using Result
```rust
match divide(10.0, 0.0) {
    Ok(result) => println!("Result: {}", result),
    Err(e) => println!("Error: {}", e),
}
```

### Panic
```rust
// This will panic if the condition is false
assert!(1 == 2, "1 is not equal to 2");
```

## 8. Modules

### Defining a Module
```rust
mod my_module {
    pub fn my_function() {
        // code
    }
}
```

### Using a Module
```rust
use my_module::my_function;

fn main() {
    my_function();
}
```

## 9. Crates and Packages

### Adding Dependencies
In Cargo.toml:
```toml
[dependencies]
serde = "1.0"
```

### Using Crates
```rust
use serde::{Serialize, Deserialize}; // Example usage of the serde crate
```

## 10. Common Collections

### Vector
```rust
let mut vec = vec![1, 2, 3];
vec.push(4);
vec.pop(); // Removes last element
```

### HashMap
```rust
use std::collections::HashMap;

let mut scores = HashMap::new();
scores.insert(String::from("Blue"), 10);
scores.insert(String::from("Yellow"), 50);
```

### HashSet
```rust
use std::collections::HashSet;

let mut set = HashSet::new();
set.insert(1);
set.insert(2);
```

### String
```rust
let mut s = String::from("Hello");
s.push_str(", world!"); // Appends a string
```

## 11. Ownership and Borrowing

### Ownership
Each value in Rust has a single owner.
When the owner goes out of scope, the value is dropped.

### Borrowing
Immutable Borrowing:
```rust
let s1 = String::from("Hello");
let s2 = &s1; // s2 borrows s1
println!("{}", s2);
```
Mutable Borrowing:
```rust
let mut s1 = String::from("Hello");
let s2 = &mut s1; // Mutable borrow
s2.push_str(", world!");
println!("{}", s2);
```

### Slices
Reference to a contiguous sequence of elements:
```rust
let s = String::from("Hello, world!");
let hello = &s[0..5]; // Slice of the first 5 characters
```

## 12. Concurrency

### Threads
```rust
use std::thread;

let handle = thread::spawn(|| {
    // code that runs in a separate thread
});

handle.join().unwrap(); // Wait for the thread to finish
```

### Message Passing
Using channels for communication between threads:
```rust
use std::sync::mpsc;

let (tx, rx) = mpsc::channel();

thread::spawn(move || {
    tx.send("Hello from thread!").unwrap();
});

let message = rx.recv().unwrap();
println!("{}", message);
```
