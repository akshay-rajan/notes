# Rust

Rust is a systems programming language that runs blazingly fast, prevents segfaults, and guarantees thread safety.

#### Overview of Rust
- **History and Purpose**: Developed by Mozilla, Rust is designed for performance, safety, and concurrency.
- **Features**: Memory safety without garbage collection, zero-cost abstractions, and concurrency support.

#### Installing Rust
- **Rustup**: The recommended tool for managing Rust versions and associated tools.
  ```sh
  curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
  ```

#### Setting Up the Development Environment
- **IDE Setup**: Install Visual Studio Code and the Rust extension for enhanced development experience.
  - Visual Studio Code
  - Rust Extension

#### Creating and Running a Rust Project
- **Cargo**: Rust’s build system and package manager.
  ```sh
  cargo new hello_world
  cd hello_world
  cargo run
  ```
  - `cargo new`: Creates a new Rust project.
  - `cargo run`: Builds and runs the project.

## Basic Syntax and Core Concepts in Rust

#### Variables and Mutability
- **Immutable Variables**: By default, variables are immutable.
  ```rust
  let x = 5;
  println!("The value of x is: {}", x);
  ```
- **Mutable Variables**: Use `mut` to make a variable mutable.
  ```rust
  let mut y = 10;
  y = 20;
  println!("The value of y is: {}", y);
  ```

#### Data Types
- **Scalar Types**: Include integers, floating-point numbers, Booleans, and characters.
  - Integers: `i8`, `u8`, `i16`, `u16`, `i32`, `u32`, `i64`, `u64`, `i128`, `u128`, `isize`, `usize`.
  - Floating-point: `f32`, `f64`.
  - Boolean: `bool` (true or false).
  - Character: `char` (Unicode scalar values).
  ```rust
  let a: i32 = 10;
  let b: f64 = 3.14;
  let c: bool = true;
  let d: char = 'A';
  ```

- **Compound Types**: Include tuples and arrays.
  - Tuples: Fixed size, can contain multiple types.
  ```rust
  let tup: (i32, f64, u8) = (500, 6.4, 1);
  let (x, y, z) = tup;
  ```
  - Arrays: Fixed size, same type.
  ```rust
  let arr: [i32; 3] = [1, 2, 3];
  let first = arr[0];
  ```

#### Functions
- **Defining Functions**: Use the `fn` keyword.
  ```rust
  fn main() {
      println!("Hello, world!");
  }
  ```

- **Parameters and Return Values**: Functions can take parameters and return values.
  ```rust
  fn add(a: i32, b: i32) -> i32 {
      a + b
  }
  let result = add(5, 3);
  ```

#### Control Flow
- **If Statements**: Conditional branching.
  ```rust
  let number = 5;
  if number < 10 {
      println!("Condition was true");
  } else {
      println!("Condition was false");
  }
  ```

- **Loops**: Repeating code.
  - `loop`: Infinite loop until explicitly broken.
  ```rust
  loop {
      println!("Loop forever!");
      break;
  }
  ```
  - `while`: Loop with a condition.
  ```rust
  let mut n = 3;
  while n != 0 {
      println!("{}!", n);
      n -= 1;
  }
  ```
  - `for`: Loop through a collection.
  ```rust
  let arr = [10, 20, 30];
  for element in arr {
      println!("The value is: {}", element);
  }
  ```

- **Match Statements**: Powerful pattern matching.
  ```rust
  let number = 7;
  match number {
      1 => println!("One"),
      2 => println!("Two"),
      3 => println!("Three"),
      4..=6 => println!("Between four and six"),
      _ => println!("Other"),
  }
  ```

## Ownership, Borrowing, and Lifetimes in Rust

#### Ownership
- **Concept**: Ownership is Rust’s system for managing memory.
- **Rules**:
  1. Each value in Rust has a single owner.
  2. When the owner goes out of scope, the value is dropped.
  3. Ownership can be transferred (moved) to another variable.

```rust
let s1 = String::from("hello");
let s2 = s1; // s1 is moved to s2, s1 is no longer valid
```

#### Borrowing
- **References**: Allow access to data without taking ownership.
- **Rules**:
  1. You can have either one mutable reference or any number of immutable references.
  2. References must always be valid.

```rust
let s = String::from("hello");

// Immutable reference
let r1 = &s;
let r2 = &s;
println!("{} and {}", r1, r2); // r1 and r2 can both be used

// Mutable reference
let mut s = String::from("hello");
let r3 = &mut s;
r3.push_str(", world");
println!("{}", r3);
```

#### Lifetimes
- **Purpose**: Ensure that references are valid for as long as they are used.
- **Syntax**: Lifetimes are annotated using `'a`.

##### Lifetime Annotations
- **Basic Usage**:
  - Lifetimes are indicated using a single quote followed by a name, like `'a`.
  - Typically used in function signatures to relate the lifetimes of input and output references.

```rust
fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```

- **Explanation**:
  - The function `longest` takes two string slices with the same lifetime `'a`.
  - The returned string slice will have the same lifetime `'a`.

#### Borrow Checker
- **Functionality**: Ensures references do not outlive the data they point to, preventing dangling references and memory safety issues.

```rust
fn main() {
    let r;
    {
        let x = 5;
        r = &x; // Error: `x` does not live long enough
    }
    println!("r: {}", r);
}
```
