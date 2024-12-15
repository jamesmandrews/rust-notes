# Rust Development

## Getting started

### Create new Project
To create a new project, use the command `cargo new {projectname}`, replacing `{projectname}` with the name of your project. This will create a directory in the current directory where you run this command.

If you want the current directory to be the project directory, you can run `cargo init`, and it will build the project in the current directory.

### Executing your project
To execute your project from the base of the project directory, use `cargo run`.

## Variables
Variables are named locations in memory used to store values used in data execution.

To create a variable in Rust, you need to use the `let` keyword.

Example:
```rust
let value = 9;
```

Rust is smart enough to infer the data type, so type declarations are not necessary. However, it is good practice to define the variable types explicitly:

```rust
let value: i32 = 9;
```

Here, `i32` indicates an integer of 32-bit size. The Rust documentation has a list of available [data types](https://doc.rust-lang.org/book/ch03-02-data-types.html).

### Immutable and Mutable Variables
In Rust, variables are immutable by default. For example:
```rust
let value: i32 = 9;
value = 10; // This would result in a compile error.
```

To make a variable mutable, you must declare it with the `mut` keyword. The following example would compile and execute without error:
```rust
let mut value: i32 = 9;
value = 10;
```

Variables are immutable by default for several reasons:
- **Optimization and Performance:** Immutable variables can be stored in read-only memory, making them faster to access.
- **Code Clarity:** Immutable variables guarantee that their value will not change, making the code easier to reason about.

### Variable Shadowing
If you need to redefine a previously defined immutable variable, you can do so with the `let` keyword. This is called shadowing:
```rust
let value: i32 = 9;
let value: i32 = 10;
```

Shadowing allows changing the data type as well:
```rust
let value: i32 = 9;
let value: bool = true;
```

## Data Types

Rust is a statically typed language, meaning the compiler knows the data type of all variables at compile time.

### Scalar Types
- Integers (e.g., `i32`, `u32`)
- Floating-point numbers (e.g., `f32`, `f64`)
- Booleans (`bool`)
- Characters (`char`)

### Compound Types
- Tuples
- Arrays

### Integer Types
| Length | Signed | Unsigned | Range                 |
|--------|--------|----------|-----------------------|
| 8-bit  | i8     | u8       | −128 to 127, 0 to 255  |
| 16-bit | i16    | u16      | −32,768 to 32,767, 0 to 65,535 |
| 32-bit | i32    | u32      | −2,147,483,648 to 2,147,483,647, 0 to 4,294,967,295 |
| 64-bit | i64    | u64      | Larger ranges         |

### Float Types
Floating-point numbers have two sizes: `f32` (32-bit) and `f64` (64-bit). They do not differentiate between signed and unsigned.

### Tuples
Tuples can store multiple values of different data types:
```rust
let my_values = ("Alice", 30, 5.4);
```

Accessing tuple values uses dot notation with an index:
```rust
println!("{}", my_values.0); // Alice
println!("{}", my_values.1); // 30
println!("{}", my_values.2); // 5.4
```

### Arrays
Arrays store multiple values of the same data type. Once an array is declared, its size is fixed:
```rust
let my_numbers = [1, 2, 3, 4, 5];
```

## Constants
Constants are variables that will never change. They are conventionally defined in uppercase letters:
```rust
const PI: f64 = 3.14;
```

## Strings

### String Slices (`&str`)
String slices are immutable views into string data:
```rust
let greeting: &str = "Hello, world!";
```

### Owned Strings (`String`)
The `String` type is mutable and heap-allocated:
```rust
let mut name = String::from("Zenva");
name.push_str(" Academy");
```

## Flow Control

### If Statements
```rust
if my_value == 0 {
    // logic
}
```

### If/Else Statements
```rust
if my_value == 0 {
    // logic
} else if my_value == 1 {
    // logic
} else {
    // logic
}
```

### For Loops
```rust
let numbers = [1, 2, 3, 4, 5, 6];
for num in numbers {
    println!("{}", num);
}
```

### While Loops
```rust
while some_value > 10 {
    // logic
}
```

### Loop Statements
Loops run until a `break` statement is encountered:
```rust
let mut index = 1;
loop {
    index += 1;
    if index == 10 {
        break;
    }
}
```

## Functions

Functions encapsulate code for reuse. For example:
```rust
fn add_integers(a: i64, b: i64) -> i64 {
    a + b
}
```

## Ownership

### Key Principles
- **Ownership:** Each value has one owner.
- **Move:** Ownership transfers when assigning or passing a value.
- **Borrowing:** Use references to avoid ownership transfer.

### Example
```rust
let s1 = String::from("hello");
let s2 = s1; // Ownership transferred
// println!("{}", s1); // Error: s1 is no longer valid
```

Borrowing example:
```rust
fn calculate_length(s: &str) -> usize {
    s.len()
}
```

## Structs

### Defining a Struct
```rust
struct User {
    name: String,
    email: String,
    active: bool,
    login_count: i64,
}

fn main() {
    let user = User {
        name: String::from("Alice"),
        email: String::from("alice@example.com"),
        active: true,
        login_count: 1,
    };

    println!("name: {}, email: {}", user.name, user.email);
}
```

### Struct Methods
```rust
impl User {
    fn print_info(&self) {
        println!("name: {}, email: {}", self.name, self.email);
    }
}
```

## Hash Maps

### Creating and Accessing
```rust
use std::collections::HashMap;

let mut population = HashMap::new();
population.insert("Tokyo", 37_000_000);
println!("Population: {:?}", population.get("Tokyo"));
```

### Iterating Over HashMap
```rust
for (city, pop) in &population {
    println!("City: {}, Population: {}", city, pop);
}
```

