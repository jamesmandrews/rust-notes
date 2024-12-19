# Rust Development

## Getting Started

### Create a New Project
To create a new project, use the command `cargo new {projectname}`, replacing `{projectname}` with the name of your project. This will create a directory in the directory you ran this command from.

If you want the current directory to be the project directory, you can run `cargo init`, and it will build the project in the current directory.

### Executing Your Project
To execute your project from the base of the project directory, use `cargo run`.

## Variables
Variables are named locations in memory used to store values during program execution.

To create a variable in Rust, you need to use the `let` keyword.

Example:
```rust
let value = 9;
```

Rust is smart enough to infer the data type, so type declarations are not necessary. However, it is good practice to define the variable types explicitly.

```rust
let value: i32 = 9;
```

`i32` denotes a 32-bit integer type. The Rust documentation provides a list of available [data types](https://doc.rust-lang.org/book/ch03-02-data-types.html).

### Immutable and Mutable Variables
In Rust, variables are immutable by default. If you try to reassign a value to an immutable variable, you will get a compile error.

```rust
let value: i32 = 9;
value = 10; // Compile error
```

To make a variable mutable, you must declare it with the `mut` keyword. The example below compiles and executes without error:

```rust
let mut value: i32 = 9;
value = 10;
```

#### Why Are Variables Immutable by Default?
- **Optimization and Performance**: Immutable variables can be placed in read-only memory, which makes them faster to access.
- **Code Clarity**: Once defined, an immutable variable never changes, ensuring consistent behavior throughout the code.

### Variable Shadowing
If you need to redefine a previously defined immutable variable, you can do so using the `let` keyword. This is called shadowing. Shadowing allows you to reuse the same variable name while changing its value or type.

```rust
let value: i32 = 9;
let value: i32 = 10;
```

In the example above, `value` is shadowed with a new integer value. You can also change its data type:

```rust
let value: i32 = 9;
let value: bool = true;
```

While shadowing is useful, overusing it can make the code harder to read.

## Data Types

Rust is a statically typed language, meaning the compiler knows the data type of all variables at compile time.

### Scalar Types
- **Integer**: Fixed-width signed (`i8`, `i16`, `i32`, `i64`, `i128`) and unsigned (`u8`, `u16`, `u32`, `u64`, `u128`) types.
- **Floating-Point**: `f32` and `f64` types for single and double precision.
- **Boolean**: Represented by `bool` (`true` or `false`).
- **Character**: Represented by `char` and can store any Unicode scalar value.

### Compound Types
- **Tuples**: A collection of values of different types.
- **Arrays**: A collection of values of the same type, with a fixed length.

Refer to the provided table and examples for details.

### Integer Types Table
| Length | Signed | Unsigned | Range                        |
|--------|--------|----------|-----------------------------|
| 8-bit  | `i8`   | `u8`     | -128 to 127 or 0 to 255     |
| 16-bit | `i16`  | `u16`    | -32,768 to 32,767 or 0 to 65,535 |
| 32-bit | `i32`  | `u32`    | -2,147,483,648 to 2,147,483,647 or 0 to 4,294,967,295 |
| 64-bit | `i64`  | `u64`    | ...                         |
| 128-bit| `i128` | `u128`   | ...                         |

### Constants
Constants are variables that never change and are declared using the `const` keyword. Constants must have an explicit type.

```rust
const PI: f64 = 3.141592;
```

### Strings
Rust provides two main types of strings:
1. **String Slices (`&str`)**: Immutable references to string data.
2. **Owned Strings (`String`)**: Mutable, heap-allocated strings.

Use `&str` for static strings and `String` when you need ownership or mutability.

### Ownership
Ownership is a core concept in Rust that ensures memory safety without a garbage collector.
#### Rules:
1. Each value in Rust has a variable that is its owner.
2. There can only be one owner at a time.
3. When the owner goes out of scope, the value is dropped.

For example:
```rust
let s1 = String::from("hello");
let s2 = s1; // Ownership is moved to s2
```

To enable borrowing instead of transferring ownership, use references (`&`) or mutable references (`&mut`).

```rust
let s = String::from("hello");
let len = calculate_length(&s);

fn calculate_length(s: &String) -> usize {
    s.len()
}
```

### Advanced Data Structures

#### Vectors
A `Vec<T>` (vector) is a resizable array that can grow or shrink as needed. Vectors are heap-allocated and store elements of a specific type `<T>`.

To declare a vector:
```rust
let mut numbers: Vec<i32> = Vec::new(); 
numbers.push(10);
numbers.push(20);
numbers.push(30);

println!("{:?}", numbers);
```

Alternatively, use the vector macro for concise syntax:
```rust
let numbers = vec![1, 2, 3, 4, 5];
println!("{:?}", numbers);
```

**Key Operations**:
- **Push**: Add elements to the end using `push()`.
- **Pop**: Remove the last element using `pop()`.
- **Accessing Elements**: Use indices or the `get()` method for safe access.
- **Iteration**: Iterate using `for` loops with borrowing or mutable borrowing.

#### HashMaps
A `HashMap<K, V>` is a collection of key-value pairs where keys are unique and map to specific values.

Creating and inserting values:
```rust
use std::collections::HashMap;

let mut population = HashMap::new();
population.insert("Tokyo", 37_000_000);
population.insert("London", 17_000_000);
population.insert("Dubai", 7_000_000);

println!("Population: {:?}", population);
```

Accessing values:
```rust
if let Some(&value) = population.get("Tokyo") {
    println!("Population of Tokyo: {}", value);
}
```

Updating values:
```rust
population.insert("Tokyo", 39_000_000); // Overwrites the value
```

Removing values:
```rust
population.remove("Tokyo");
```

#### Stacks
A stack is a "Last In, First Out" (LIFO) data structure. Example:
```rust
struct Stack {
    items: Vec<i32>,
}

impl Stack {
    fn new() -> Self {
        Stack { items: Vec::new() }
    }

    fn push(&mut self, value: i32) {
        self.items.push(value);
    }

    fn pop(&mut self) -> Option<i32> {
        self.items.pop()
    }

    fn peek(&self) -> Option<&i32> {
        self.items.last()
    }
}

fn main() {
    let mut stack = Stack::new();
    stack.push(1);
    stack.push(2);
    stack.push(3);

    println!("Top element: {:?}", stack.peek());
    stack.pop();
    println!("Top element after pop: {:?}", stack.peek());
}
```

#### Queues
A queue is a "First In, First Out" (FIFO) data structure. Example:
```rust
use std::collections::VecDeque;

struct Queue {
    items: VecDeque<i32>,
}

impl Queue {
    fn new() -> Self {
        Queue { items: VecDeque::new() }
    }

    fn enqueue(&mut self, value: i32) {
        self.items.push_back(value);
    }

    fn dequeue(&mut self) -> Option<i32> {
        self.items.pop_front()
    }

    fn peek(&self) -> Option<&i32> {
        self.items.front()
    }
}

fn main() {
    let mut queue = Queue::new();
    queue.enqueue(1);
    queue.enqueue(2);
    queue.enqueue(3);

    println!("Front element: {:?}", queue.peek());
    queue.dequeue();
    println!("Front element after dequeue: {:?}", queue.peek());
}
```

#### Performance Tips
- Preallocate capacity for vectors and hash maps using `Vec::with_capacity()` or `HashMap::with_capacity()` to avoid frequent reallocations.
- Use appropriate types for keys in hash maps (e.g., `String`, `i32`) to ensure efficient hashing.
