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
  - `cargo build`: Builds the project.
  - `cargo run`: Builds and runs the project.

The *hello_world/src/main.rs* is our source file.
*hello_world/Cargo.toml* is the package management file for the project, where we will list our dependencies.

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
  let arr: [i32; 3] = [0, 1, 2, 3];
  let first = arr[0];
  println!("Array: {:?}", arr);
  let slice = &arr[1..3]; // Slicing, [1, 2], size unknown
  println!("Length of slice: {}", slice.len());
  ```

- **Strings**
  ```rust
  let mut string: String = String::from("Hello, ");
  string.push("world!");
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
  for i in 0..6 {
    print!("{}", i);
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

- **Implementing a Struct**
  ```rust
  struct Weapon {
    name: String,
    damage: i32,
    rounds: i32
  }
  impl Weapon {
    fn details(&self) {
      println!("Name: {}", self.name);
    }
  }
  let ak = Weapon {
    name: String::from("AK 47"),
    damage: 137,
    capacity: 150
  };
  ak.details();
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

## Working with Collections in Rust

#### Overview
Rust provides powerful and flexible collection types in its standard library. The most commonly used collections are vectors, strings, hash maps, and slices.

#### Vectors
- **Definition**: A growable array type, `Vec<T>`.
- **Creating Vectors**:
  ```rust
  let v: Vec<i32> = Vec::new();
  let v = vec![1, 2, 3];
  ```
- **Updating Vectors**:
  ```rust
  let mut v = Vec::new();
  v.push(5);
  v.push(6);
  v.push(7);
  ```
- **Reading Elements**:
  - Using Index:
    ```rust
    let third = &v[2];
    ```
  - Using `get` Method:
    ```rust
    match v.get(2) {
        Some(third) => println!("The third element is {}", third),
        None => println!("There is no third element."),
    }
    ```
- **Iterating Over Vectors**:
  ```rust
  let v = vec![100, 32, 57];
  for i in &v {
      println!("{}", i);
  }

  let mut v = vec![100, 32, 57];
  for i in &mut v {
      *i += 50;
  }
  ```

#### Strings
- **Definition**: A collection of `char` values representing a sequence of UTF-8 encoded characters.
- **Creating Strings**:
  ```rust
  let s = String::new();
  let s = "initial contents".to_string();
  let s = String::from("initial contents");
  ```
- **Updating Strings**:
  ```rust
  let mut s = String::from("foo");
  s.push_str("bar");
  s.push('!');
  ```
- **Concatenation**:
  ```rust
  let s1 = String::from("Hello, ");
  let s2 = String::from("world!");
  let s3 = s1 + &s2; // s1 is moved here and can no longer be used
  ```
- **String Slices**:
  ```rust
  let hello = "helloworld";
  let s = &hello[0..5]; // s will be "hello"
  ```

#### Hash Maps
- **Definition**: A collection of key-value pairs. Keys are unique.
- **Creating Hash Maps**:
  ```rust
  use std::collections::HashMap;

  let mut scores = HashMap::new();
  scores.insert(String::from("Blue"), 10);
  scores.insert(String::from("Yellow"), 50);
  ```
- **Accessing Values**:
  ```rust
  let team_name = String::from("Blue");
  let score = scores.get(&team_name);
  ```
- **Iterating Over Hash Maps**:
  ```rust
  for (key, value) in &scores {
      println!("{}: {}", key, value);
  }
  ```
- **Updating Values**:
  - Overwriting:
    ```rust
    scores.insert(String::from("Blue"), 25);
    ```
  - Only Inserting If the Key Has No Value:
    ```rust
    scores.entry(String::from("Yellow")).or_insert(50);
    scores.entry(String::from("Blue")).or_insert(50);
    ```
  - Updating Based on the Old Value:
    ```rust
    let text = "hello world wonderful world";
    let mut map = HashMap::new();

    for word in text.split_whitespace() {
        let count = map.entry(word).or_insert(0);
        *count += 1;
    }
    ```

#### Slices
- **Definition**: References to a contiguous sequence of elements in a collection.
- **String Slices**:
  ```rust
  let s = String::from("hello world");
  let hello = &s[0..5];
  let world = &s[6..11];
  ```
- **Array Slices**:
  ```rust
  let a = [1, 2, 3, 4, 5];
  let slice = &a[1..3]; // [2, 3]
  ```

## Generics, Traits, and Lifetimes

#### Generics
- **Definition**: Generics allow for the definition of functions, structs, enums, and methods with types that are specified later.
- **Syntax**:
  ```rust
  fn largest<T: PartialOrd>(list: &[T]) -> &T {
      let mut largest = &list[0];
      for item in list {
          if item > largest {
              largest = item;
          }
      }
      largest
  }
  ```
  - `T`: A placeholder for any type that implements the `PartialOrd` trait.

#### Traits
- **Definition**: Traits are Rust's way of defining shared behavior. Rust does not support inheritance, but it supports interfaces through Traits.
- **Syntax**:
  ```rust
  pub trait Summary {
      fn summarize(&self) -> String;
  }
  ```
- **Implementing Traits**:
  ```rust
  pub struct Article {
      pub headline: String,
      pub location: String,
      pub author: String,
      pub content: String,
  }

  impl Summary for Article {
      fn summarize(&self) -> String {
          format!(
            "{}, by {} ({})", self.headline, self.author, self.location
          )
      }
  }
  ```
- **Trait Bounds**: Ensure that a generic type has certain behavior.
  ```rust
  fn notify<T: Summary>(item: &T) {
      println!("Breaking news! {}", item.summarize());
  }
  ```

#### Lifetimes
- **Definition**: Lifetimes are a way of specifying how long references should be valid.
- **Syntax**: Lifetime annotations use an apostrophe (`'`) followed by a name.
  ```rust
  fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
      if x.len() > y.len() {
          x
      } else {
          y
      }
  }
  ```
  - `'a`: A lifetime parameter that ensures the returned reference is valid as long as both input references are valid.

#### Lifetime Elision
- **Elision Rules**: The compiler can infer lifetimes in some cases.
  1. Each parameter with a reference gets its own lifetime.
  2. If there is exactly one input lifetime, that lifetime is assigned to all output lifetimes.
  3. If there are multiple input lifetimes, but one of them is `&self` or `&mut self`, the lifetime of `self` is assigned to all output lifetimes.

```rust
fn first_word(s: &str) -> &str {
    let bytes = s.as_bytes();
    for (i, &item) in bytes.iter().enumerate() {
        if item == b' ' {
            return &s[0..i];
        }
    }
    &s[..]
}
```

#### Combining Generics, Traits, and Lifetimes
- **Example**:
  ```rust
  use std::fmt::Display;

  fn longest_with_an_announcement<'a, T>(
      x: &'a str,
      y: &'a str,
      ann: T,
  ) -> &'a str
  where
      T: Display,
  {
      println!("Announcement! {}", ann);
      if x.len() > y.len() {
          x
      } else {
          y
      }
  }
  ```

## Concurrency in Rust

#### Introduction to Concurrency
- Concurrency allows multiple computations to happen at the same time.
- Rust's concurrency model ensures memory safety without needing a garbage collector.

#### Threads
- **Definition**: Threads allow multiple parts of a program to run simultaneously.
- **Creating Threads**:
  ```rust
  use std::thread;
  use std::time::Duration;

  let handle = thread::spawn(|| {
      for i in 1..10 {
          println!("hi number {} from the spawned thread!", i);
          thread::sleep(Duration::from_millis(1));
      }
  });

  for i in 1..5 {
      println!("hi number {} from the main thread!", i);
      thread::sleep(Duration::from_millis(1));
  }

  handle.join().unwrap();
  ```

#### Message Passing
- **Definition**: Threads communicate by sending messages to each other.
- **Using Channels**:
  ```rust
  use std::sync::mpsc;
  use std::thread;

  let (tx, rx) = mpsc::channel();

  thread::spawn(move || {
      let val = String::from("hi");
      tx.send(val).unwrap();
  });

  let received = rx.recv().unwrap();
  println!("Got: {}", received);
  ```

#### Shared State Concurrency
- **Definition**: Threads share memory to communicate.
- **Using `Mutex`**:
  ```rust
  use std::sync::{Arc, Mutex};
  use std::thread;

  let counter = Arc::new(Mutex::new(0));
  let mut handles = vec![];

  for _ in 0..10 {
      let counter = Arc::clone(&counter);
      let handle = thread::spawn(move || {
          let mut num = counter.lock().unwrap();
          *num += 1;
      });
      handles.push(handle);
  }

  for handle in handles {
      handle.join().unwrap();
  }

  println!("Result: {}", *counter.lock().unwrap());
  ```

#### Atomics and Lock-free Programming
- **Definition**: Low-level concurrency primitives for fine-grained control.
- **Using `Atomic` Types**:
  ```rust
  use std::sync::atomic::{AtomicUsize, Ordering};
  use std::thread;

  let counter = AtomicUsize::new(0);
  let handles: Vec<_> = (0..10).map(|_| {
      thread::spawn(|| {
          for _ in 0..1000 {
              counter.fetch_add(1, Ordering::SeqCst);
          }
      })
  }).collect();

  for handle in handles {
      handle.join().unwrap();
  }

  println!("Result: {}", counter.load(Ordering::SeqCst));
  ```

#### `Send` and `Sync` Traits
- **`Send` Trait**: Types that can be transferred across thread boundaries.
- **`Sync` Trait**: Types that can be referenced from multiple threads.

