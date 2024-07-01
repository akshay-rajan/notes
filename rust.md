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
## Compound Data Types in Rust

#### Tuples
- **Definition**: Tuples are fixed-size collections of values of different types.
- **Syntax**:
  ```rust
  let tup: (i32, f64, u8) = (500, 6.4, 1);
  ```
- **Accessing Elements**:
  - Destructuring:
    ```rust
    let (x, y, z) = tup;
    println!("The value of y is: {}", y);
    ```
  - Using dot notation:
    ```rust
    let x = tup.0;
    let y = tup.1;
    let z = tup.2;
    ```

#### Structs
- **Definition**: Structs are custom data types that group related values.
- **Types of Structs**:
  - **Classic C-like Struct**:
    ```rust
    struct User {
        username: String,
        email: String,
        sign_in_count: u64,
        active: bool,
    }

    let user1 = User {
        username: String::from("someusername123"),
        email: String::from("someone@example.com"),
        sign_in_count: 1,
        active: true,
    };
    ```
  - **Tuple Structs**:
    ```rust
    struct Color(i32, i32, i32);

    let black = Color(0, 0, 0);
    ```
  - **Unit-like Structs** (without fields, useful for traits):
    ```rust
    struct AlwaysEqual;
    ```

- **Accessing Struct Fields**:
  ```rust
  let user_email = user1.email;
  ```

- **Struct Update Syntax**:
  ```rust
  let user2 = User {
      email: String::from("another@example.com"),
      ..user1
  };
  ```

#### Enums
- **Definition**: Enums allow the definition of a type by enumerating its possible variants.
- **Syntax**:
  ```rust
  enum Message {
      Quit,
      Move { x: i32, y: i32 },
      Write(String),
      ChangeColor(i32, i32, i32),
  }

  let msg1 = Message::Quit;
  let msg2 = Message::Move { x: 10, y: 20 };
  let msg3 = Message::Write(String::from("hello"));
  let msg4 = Message::ChangeColor(255, 0, 0);
  ```

- **Using Enums with `match`**:
  ```rust
  match msg1 {
      Message::Quit => println!("Quit variant"),
      Message::Move { x, y } => println!("Move to ({}, {})", x, y),
      Message::Write(text) => println!("Text message: {}", text),
      Message::ChangeColor(r, g, b) => println!("Change color to ({}, {}, {})", r, g, b),
  }
  ```

#### Option Type
- **Definition**: Represents a value that can be either something or nothing.
- **Variants**: `Some(T)` and `None`.
- **Usage**:
  ```rust
  let some_number = Some(5);
  let some_string = Some("a string");

  let absent_number: Option<i32> = None;
  ```

- **Handling `Option` with `match`**:
  ```rust
  let x: Option<i32> = Some(5);
  match x {
      Some(value) => println!("Value: {}", value),
      None => println!("No value"),
  }
  ```

#### Result Type
- **Definition**: Represents either success (`Ok`) or failure (`Err`).
- **Variants**: `Ok(T)` and `Err(E)`.
- **Usage**:
  ```rust
  fn divide(numerator: f64, denominator: f64) -> Result<f64, String> {
      if denominator == 0.0 {
          Err(String::from("Cannot divide by zero"))
      } else {
          Ok(numerator / denominator)
      }
  }

  let result = divide(4.0, 2.0);
  match result {
      Ok(value) => println!("Result: {}", value),
      Err(err) => println!("Error: {}", err),
  }
  ```

## Error Handling in Rust

#### Introduction to Error Handling
- Rust distinguishes between recoverable and unrecoverable errors.
- **Recoverable Errors**: Represented by the `Result` type.
- **Unrecoverable Errors**: Represented by the `panic!` macro.

#### The `Result` Type
- **Definition**: Used for functions that can return an error.
- **Variants**:
  - `Ok(T)` for successful results.
  - `Err(E)` for errors.

```rust
fn divide(numerator: f64, denominator: f64) -> Result<f64, String> {
    if denominator == 0.0 {
        Err(String::from("Cannot divide by zero"))
    } else {
        Ok(numerator / denominator)
    }
}
```

- **Using `Result`**:
  - Match Expressions:
    ```rust
    match divide(4.0, 2.0) {
        Ok(value) => println!("Result: {}", value),
        Err(err) => println!("Error: {}", err),
    }
    ```
  - Methods on `Result`:
    - `unwrap()`: Returns the value if `Ok` or panics if `Err`.
      ```rust
      let result = divide(4.0, 2.0).unwrap();
      ```
    - `expect(msg)`: Similar to `unwrap()` but with a custom error message.
      ```rust
      let result = divide(4.0, 0.0).expect("Division failed");
      ```

#### The `Option` Type
- **Definition**: Used for values that may be absent.
- **Variants**:
  - `Some(T)` for present values.
  - `None` for absent values.

```rust
let some_number = Some(5);
let absent_number: Option<i32> = None;
```

- **Using `Option`**:
  - Match Expressions:
    ```rust
    match some_number {
        Some(value) => println!("Value: {}", value),
        None => println!("No value"),
    }
    ```
  - Methods on `Option`:
    - `unwrap()`: Returns the value if `Some` or panics if `None`.
      ```rust
      let number = some_number.unwrap();
      ```
    - `expect(msg)`: Similar to `unwrap()` but with a custom error message.
      ```rust
      let number = absent_number.expect("No value found");
      ```

#### The `panic!` Macro
- **Definition**: Used for unrecoverable errors that require the program to stop execution.
- **Usage**:
  ```rust
  panic!("Something went wrong!");
  ```

- **Backtraces**: When a panic occurs, Rust prints a backtrace to help locate the source of the error. Enable backtraces by setting the `RUST_BACKTRACE` environment variable.
  ```sh
  export RUST_BACKTRACE=1
  ```

#### Error Propagation
- **Using `?` Operator**: Simplifies error propagation in functions that return `Result`.
  ```rust
  fn read_username_from_file() -> Result<String, io::Error> {
      let mut file = File::open("hello.txt")?;
      let mut username = String::new();
      file.read_to_string(&mut username)?;
      Ok(username)
  }
  ```

- **Example with `?` Operator**:
  ```rust
  use std::fs::File;
  use std::io::{self, Read};

  fn read_username_from_file() -> Result<String, io::Error> {
      let mut f = File::open("hello.txt")?;
      let mut s = String::new();
      f.read_to_string(&mut s)?;
      Ok(s)
  }
  ```

