# Rust Development

## Getting started

### Create new Project.
To create create a new project use the command `cargo run {projectname}`.  Replacing `{projectname}` with the name of your project.  This will create a directory in the directory you have run this command from.

If you want the directory your in to be the project directory you can run `cargo init` and it will build the project in the currect directory you are in.

### Executing your project.
To execute your project from the base of the project directory use `cargo run`.

## Variablles
Variables are named locations in mamory used to store values used in data execution.

To create a variable in Rust you need to use the `let` keyword.

Example
```
let value = 9
```

Rust is smart enough to know what the data type is so type declarations are not necesary. However it is good practice
to define the variable types as they are defined.

```
let value: i32 = 9;
```

`i32` being an `integer 32` type.  The Rust documentation has a list of available [data types](https://doc.rust-lang.org/book/ch03-02-data-types.html)

### Immutable and Mutable variables
In rust variables are immutable by default.  If yout take our example above, and tried to reassign `value` as we do below, you would get a compile error.  
```
let value: i32 = 9;
value = 10;
```

In order to make a variable mutable you must declare it as mutable with the `mut` keyword.  The example below would compile and execute without error.

```
let mut value: i32 = 9;
value = 10
```

Variables are immutible by default for a few reasons.
    * Optimization and Performance.  Immutable variables can be put in read-only memory which makes them faster to access.
    * Code clarity.  Once defined an immutable variable never changes and therefore it can be relied on to have the same value when reading code.

### Variable Shadowing
If you need to redefine a previously defined immutable variable you can do so with the let keyword.  This is called shadowing because the previous declaration shadows the new delcaration.  I however do not recommend doing this as it make the code less easy to read.

```
let value: i32 = 9;
let value: i32 = 10
```

In the example above shadowed the value with the same data type.  However using shadow not only can you change the value, but you can also redeclare the datatype as in the example below we shadow `value` which was an `i32` integer with a `bool` boolean value.

```
let value: i32 = 9;
let value: bool = true;
```

## Datatype

Rust is a statically typed language.  Meaning that the compiler knows the datatype of all variables at compile time.

* Scalar Types ( interger, float, boolean, and character)
* Compound types (tuples, arrays)

### Interger Types

| length | Signed | Unsigned | Range |
|:-:|:-:|:-:|-:|
| 8bit | i8 | u8 |-128 to 127 or 0 to 255 |
| 16bit | i16 | u16 |-32,768 to 32,767 or 0 to 65,535 |
| 32bit | i32 | u32 | |
| 64bit | i64 | u64 | |

### Float Types
Float types have a 32 bit and 64 bit type and do not differenciate between signed and unsigned.  `f32` and `f64`.

### Tuples
Are used to store multiple values.  They can be values of different data types

```
let my_values = ("alice", 30, 5.4);
```

Accessing tuple values uses a dot notation with an index.

```
let my_values = ("alice", 30, 5.4);
println!("{}", my_values.0); // alice
println!("{}", my_values.1); // 30
println!("{}", my_values.2); // 5.4
```

### Arrays
Are used to store multiple values, but they must be of the same data type.  Once an array is delclared its size is fixed.

```
let my_numbers = [1,2,3,4,5];
```

### Constants

Constants are variables that will never change.  While there is no rule stating they must be delcared this way, you will often find constants defined in all upper case characters

```
const PI: u32 = 3.14;
```

or

```
const pi: u32 = 3.14;
```

## Code comment.

Rust uses C like comment blocks `/* */` and `//` for commenting code.

## Strings

### Declaring Strings in Rust
In Rust, strings are more complex than simple variable types like integers or floats. Rust strings come in two main forms: &str (string slices) and String. The difference lies in their flexibility and ownership model.

### String Slices: &str
String slices, denoted as &str, are immutable views into a string data. They are often used for referencing string data in a memory-efficient way without owning the actual data. For example:

```
fn main() { 
  let greeting: &str = "Hello, world!"; 
  println!("{}", greeting); 
}
```

Here, greeting is a string slice referencing the static string literal “Hello, world!”. It is hardcoded into the program and is immutable.

### Using String Literals
Sometimes you might see simple declarations like:

```
let name = "John";
```

This works because name is implicitly assigned a &str type. In Rust, when you use double quotes around text, you are creating a string literal which is a &str by default. This allows you to utilize strings efficiently when you don’t need to modify them or own the data outright. This is a convenient way to deal with static string data.

### Owned Strings: String
The String type is a growable, mutable, heap-allocated data structure. This makes it more versatile compared to &str. Consider the following snippet:

```
fn main() { 
  let mut name = String::from("Zenva"); 
  name.push_str(" Academy"); 
  println!("{}", name); 
}
```

Here, we create a String using String::from() and then modify it using push_str() to add more text. Notice the mut keyword, indicating that we can mutate the variable.

### Choosing Between &str and String
The choice between &str and String largely depends on your specific requirements:

* Use &str when you have a string literal or when you do not need to own the data.
* Use String when you require a string that you can modify or if you need ownership of the data.


## Flow Control

### If Statements

If statments look like below.

```
if myValue == 0 {
    // some logic
}
```

```
if myValue == 0 && myOtherValue == 2 {
    // some other logic
}
```

### If/Else statements


```
if myValue == 0 {
    // some logic
}
else if myvalue == 1 {
    // some logic
}
else {
    // some logic
}
```

### If/Let statements

Allows us to set a variable as a value 

```
let somevalue = if someothervalue === true { "hi" } else { "bye" }
```

### For Loop.

```
let numbers = [1,2,3,4,5,6];
for num in numbers {
    // some logic
}
```

### While Loops

```
while somevalue > 10 {
    // some logic
}
```


### Loop Statement

Loops statements create a loop that will loop until a break statement is used to break out of it.

```
let mut index = 1;
loop {
    index+=1;

    if index == 10 {
        break;
    }
}
```

## Functions

Functions are a way of encapsulating code that performs a singular task, so that it can be reused instead of writing the code over and over again.  For example if you wanted a function to add 2 integers together.

```
fn addIntegers(a: i64. b: i64) -> i32 {
    let sum = a + b;
    return sum;
}

let added = addIntegers(1,2);
let added2 = addIntegers(2,2);
```

Unlike variables, when creating a function with parameters you must include the datatype in the declaration.  A function must also declare the return type, this is done using the arrow notation `-> i32` in the above example indicates that the function will return a 32 bit integer.

When returning the result you can return it like we do above, or you can just place the variable on the last line without a semicolon and it will be returned, like the example below.

```
fn addIntegers(a: i64. b: i64) -> i32 {
    let sum = a + b;
    sum
}

let added = addIntegers(1,2);
let add
```

### Ownership

#### Key Principles of Ownership
* Ownership: Each value in Rust has a single owner, which is the variable that holds it.
* Ownership Transfer (Move): When ownership is transferred, the previous owner can no longer use the value.
Scope and Lifespan: A value is dropped (deallocated) when its owner goes out of scope.

#### Rules of Ownership
* Each value has one owner: A value can only be owned by one variable at a time.
* Ownership transfer on assignment: When assigning or passing a value to another variable, ownership is transferred unless the type is a copy type.
* Automatic deallocation: When the owner of a value goes out of scope, Rust automatically frees the memory for the value.

#### Copy Types vs. Non-Copy Types

##### Copy Types:
Simple, fixed-size types that implement the Copy trait.
Instead of transferring ownership, they are copied on assignment or function calls.
**Examples**:
* Scalars: integers (i32, u64), floats (f32, f64), bool, char.
* Fixed-size collections: arrays (e.g., [i32; 3]), tuples (e.g., (i32, f64)) if all components are Copy.

##### Non-Copy Types:
Types that do not implement the Copy trait and rely on ownership transfer.
Typically, these manage heap memory or other resources.
**Examples**:
* String, Vec<T>, Box<T>, HashMap<K, V>.
* Custom types (e.g., structs) unless explicitly marked Copy and all fields are Copy.

###### Examples
###### Ownership Transfer (Move) for Non-Copy Types
```
let s1 = String::from("hello"); // String is a non-Copy type
let s2 = s1; // Ownership is transferred (moved) to s2
// println!("{}", s1); // Error: s1 is no longer valid
```

###### Copy Behavior
```
let x = 5; // i32 is a Copy type
let y = x; // x is copied into y
println!("x: {}, y: {}", x, y); // Both x and y are valid
```
###### Function Calls
* Non-Copy Type:
```
let s = String::from("hello");
takes_ownership(s); // Ownership of s is transferred to the function
// println!("{}", s); // Error: s is no longer valid

fn takes_ownership(s: String) {
    println!("{}", s);
}
```

* Copy Type:

```
let n = 42;
makes_copy(n); // n is copied into the function
println!("{}", n); // n is still valid

fn makes_copy(n: i32) {
    println!("{}", n);
}
```

##### Borrowing and References
Borrowing lets you use a value without taking ownership.
Two types:
* Immutable Borrow (&): Multiple borrows allowed.
* Mutable Borrow (&mut): Only one mutable borrow allowed at a time.
```
let s = String::from("hello");
let len = calculate_length(&s); // Borrow s with `&`
println!("Length: {}", len); // s is still valid

fn calculate_length(s: &String) -> usize {
    s.len() // Borrowed value is read-only
}
```

##### Summary of Ownership with Data Types
* Copy types: Scalars (e.g., integers, floats, booleans) and simple composite types (e.g., small arrays, tuples) are copied, not moved.
* Non-Copy types: Heap-allocated data (e.g., String, Vec<T>) and custom types follow the move semantics for ownership transfer.
* Rust’s ownership system ensures memory safety by managing moves, copies, and borrows at compile time.

### Slice Types
Are a type that allows us to access part of a collection or a string as a reference.

```
let message = String::from("Hello world");
let hello = &message[0..5];
```

In the above example we want to copy the word `Hello` into the variable `hello`.  To do this we treat the string as an array each letter is an index.  `H` being index 0 and `o` being index 4.  In our delcaration for variable hello we use `&message` to get a reference to the `message` variable, and then use `[0..5]` to get the positions for the word `Hello`.  The 2nd index value must be 1 greater than the last index you want to slice.

## Structs

### Defining a struct
Are custom data types that allow you to structure related data together as a single variable.  Below is an example of what a struct might look like for a `User` object with various attributes.

```
struct User {
    name: String,
    email: String,
    active: bool,
    login_count: i64
}

fun main() {

    let user = User {
        name: String::from("Alice),
        email: String::from("alice@example.com"),
        active: true,
        login_count: 1        
    };

    println!("name: {}, email: {}", user.name, user.email);
}

```

### Struct methods.
A method is a function that is associated with a struct, you define methods using the 'impl' keyword and the name of the struct it is associated with.  In this case our `User` struct

```
struct User {
    name: String,
    email: String,
    active: bool,
    login_count: i64
}

impl User {
    fn print_info(&self) {
        println!("name: {}, email: {}", self.name, self.email);
    }
}

fun main() {

    let user = User {
        name: String::from("Alice),
        email: String::from("alice@example.com"),
        active: true,
        login_count: 1        
    };

    user.print_info();
}

```

## Enum

In Rust, enums (short for enumerations) allow you to define a type by enumerating its possible variants. Each variant can optionally carry data of different types, making enums a versatile way to represent and work with structured data.

Key Features of Rust Enums:
Variants: Define a set of distinct, named alternatives for a type.
Data Association: Each variant can optionally include associated data, similar to a tuple or struct.
Pattern Matching: Enums work seamlessly with Rust's powerful match expressions, allowing exhaustive handling of all possible variants.
Example:
```
enum Message {
    Quit,                       // No associated data
    Move { x: i32, y: i32 },    // Struct-like associated data
    Write(String),              // Tuple-like associated data
    ChangeColor(i32, i32, i32), // Multiple values
}

fn process_message(msg: Message) {
    match msg {
        Message::Quit => println!("Quit message received."),
        Message::Move { x, y } => println!("Move to ({}, {}).", x, y),
        Message::Write(text) => println!("Message: {}", text),
        Message::ChangeColor(r, g, b) => println!("Change color to RGB({}, {}, {}).", r, g, b),
    }
}

fn main() {
    let msg = Message::Move { x: 10, y: 20 };
    process_message(msg);
}
```

Enums are ideal when a value can be one of several different kinds of data, and they are a core feature in Rust for modeling complex systems safely and expressively.

### Option Enum
The Option enum is used to represent a value that might or might not exist.

#### Variants:
* None: Represents the absence of a value.
* Some(T): Wraps a value of type T.
Example:
```
let value: Option<i32> = Some(5);
let no_value: Option<i32> = None;

if let Some(v) = value {
    println!("We have a value: {}", v);
} else {
    println!("No value present.");
}
```

### Result Enum
The Result enum is used for error handling, representing either success or failure.

#### Variants:
* Ok(T): Represents success and wraps a value of type T.
* Err(E): Represents an error and wraps an error value of type E.
Example:

```
fn divide(a: i32, b: i32) -> Result<i32, &'static str> {
    if b == 0 {
        Err("Division by zero!")
    } else {
        Ok(a / b)
    }
}

match divide(10, 2) {
    Ok(result) => println!("Result: {}", result),
    Err(err) => println!("Error: {}", err),
}
```

### Why Are They Special?
Option and Result are foundational in Rust because they eliminate null and unsafe error handling patterns.
They're part of the standard library and widely used for safe, idiomatic Rust programming.

## Crates and Modules.

### Crates

Crates are packages of code used to perform specific tasks.

Two kinds of crate.
  * Binary Crate: are an executable file and must have a main function.  All Rust projects that have a main function would be considered a binary crate. 
  * Library Crate:  Library crates do not have a main function and can not be executed on their own.

To install a Libray crate to your project use the command below.

```
cargo add {{packagename}}
```

When a package is added you should see it added to the `Cargo.toml` file

In order to use a package in our code you must declare it with a `use` statement

Below we tell our code to `use` the `rand::Rng` function from the `rand` package.

```
use rand::Rng

fn main() {
  let mut rng = rand::thread_rng();
  let random_number:u32 = rng.gen_range(0..1000);
  println!("Random: {}", random_number);
}
```

### Modules

Modules are localized library crates, allowing you to organize your code for resuability.

Let's say we have 2 functions for calculating numbers, we will want them in their own module called `calculation`.

Create a file called `caclulation.rs`.  We have 2 functions.  `add` and `subtract`.  To make them available to code outside the `calculation.rs` file you must use the `pub` keyword before the `fn` keyword

```
pub fn add (a:u32, b:u32) -> u32 {
  return a + b;
}

pub fn subtract (a:u32, b:u32) -> u32 {
  return a - b;
}
```

Then in our main.rs file we use the `mod` keyword to include it

```
mod calculation

fn main {
  let sum:u32 = calculation::add(1, 4)
  println!("Sum: {}", sum);
}
```

## Advanced Data Structures

### Vectors

A `Vec<T>` called a vector is one of the most commonly used data structures in Rust.  It is a resizable array that can hold elements of a specific type `<T>`.  To grow and shrink as needed and are heap allocated.

To declare a vector you use the following format.

```
let mut numbers: Vec<i32> = Vec::new(); 
numbers.push(10);
numbers.push(20);
numbers.push(30);


println!("{:?}", numbers);
```

You can also create a vector using a vector macro. This is more concise then the previous method.

```
let mut numbers2: vec![1,2,3,4,5]; 
println!("{:?}", numbers2);
```

#### Push and Pop

You use the `push` method to add an item to the end of the array, and the `pop` method to remove an item from the end of the array.

```
  let mut fruits = vec!["apple", "banana", "orange"]; 
  fruits.push("grape");

  let removed = fruits.pop();
  println!("{:?}, Removed: {:?}", fruits, removed);
```

#### Accessing and modifying elements

You can access elements using an index, just like a regular array.

```
  let numbers3: vec![100,200,300,400,500]; 
  let second = numbers3[1];
  println!("Second: {}", second); 
```

The above code will access the 2nd element of the array at index `1` and store it in a variable.

A safer way to access an element of a vector is using the `get()` method.  If the element doesn't exist it will return `None` enum and if it does the `Some` Enum

```
  let numbers3: vec![100,200,300,400,500];
  let index = 5
  match numbers3.get(index){
    Some(value) => println!("Value: {}", value);
    None => println!("No value at index: {}", value);
  }
```

Iterating through a vector

```
let animals = vec!["dog","cat","rabbit"]

// borrowing the vector with &
for animal in &animals {
    println("{}", animal);
}
```

You can also also borrow a mutable reference to modify the values

```
let numbers = vec![1,2,3,4,5];
for number in &mut numbers {
    number *= 2
}

println!("{:?}", numbers)

```

You need to be careful when using vecs, when a vec grows out of space it will typically double it's capacity copying the current data into the new memory allocation.  To avoid this you can allocate with capacity.

```
let mut vec = Vec::with_capaticy(10);

for i in 0..10 {
    vec.push(1);
}

println!("Vector: {:?}, Capacity: {}", vec, vec.capacity())

```

### Hash Maps

A hashmap is a collection of key value pairs. `Hashmap<K,V>`  Where `K` is the key type, and `V` is the value type.  The keys are unique and maps to specifically one value.  That value can be of any type.  `Array`, `Enum`, `Struct` etc...

Example on how to create and insert data into a hashmap
```
let mut population = Hashmap.new();
population.insert("Tokyo", "37000000);
population.insert("London", "17000000);
population.insert("Dubai", "7000000);

println!("Population: {:?}, population)

```

Example of accessing a value using a key.
```
let mut population = Hashmap.new();
population.insert("Tokyo", "37000000);
population.insert("London", "17000000);
population.insert("Dubai", "7000000);

match population.get("Tokyo){
  Some(&value) => println!("Population: {}", value);
  None => println!("No value at key index: {}", value);
}

```

To update a value just re-insert it into the hashmap.
```
let mut population = Hashmap.new();
population.insert("Tokyo", "37000000);
population.insert("London", "17000000);
population.insert("Dubai", "7000000);

match population.get("Tokyo){
  Some(&value) => println!("Population: {}", value);
  None => println!("No value at key index: {}", value);
}

population.insert("Tokyo", "57000000);

match population.get("Tokyo){
  Some(&value) => println!("Population: {}", value);
  None => println!("No value at key index: {}", value);
}

```

To remove a key value pair you can use the remove() function on the hashmap using the key you want to remove.

Example of accessing a value using a key.
```
let mut population = Hashmap.new();
population.insert("Tokyo", "37000000);
population.insert("London", "17000000);
population.insert("Dubai", "7000000);

match population.get("Tokyo){
  Some(&value) => println!("Population: {}", value);
  None => println!("No value at key index: {}", value);
}

population.remove("Tokyo");

match population.get("Tokyo){
  Some(&value) => println!("Population: {}", value);
  None => println!("No value at key index: {}", value);
}

```

#### Iterating over Hashmap.

Below you can use a for loop to iterate over the hashmap.

```
let mut population = Hashmap.new();
population.insert("Tokyo", "37000000);
population.insert("London", "17000000);
population.insert("Dubai", "7000000);

for (city, population) in &populations {
  println!("City: {:?}, city, Population: {:?}, population);
}
```

Below you can iterate over only the values.

```
let mut population = Hashmap.new();
population.insert("Tokyo", "37000000);
population.insert("London", "17000000);
population.insert("Dubai", "7000000);

for population in populations.values() {
  println!(Population: {:?}, population);
}
```

Using the `entry`/`insert` function to insert if a key entry doesn't exist.


```
let mut population = Hashmap.new();
population.insert("Tokyo", "37000000);
population.insert("London", "17000000);
population.insert("Dubai", "7000000);

population.entry("Seatle").insert(2000000);
population.entry("Dubai").insert(3000000);

for population in populations.values() {
  println!(Population: {:?}, population);
}
```


#### Hashmap performance
For better performance keys should be either String, i32, or usize since they are easier to hash.
You can also preallocate the capacity the same way as Vectors

```
let mut scores = HashMap::with_capacity(10);
for i in 0..5 {
  scores.insert(i, i*10);
}

println!("{?:}", scores);
println!("{}", scores.capacity());
```
### Stacks

A stack is a datastruckter that follows the "Last In First Out" principle.  It does this with the `push()` and `pop()` functions.  The `push()` puts an item on the stack, and `pop()` will take from the stack.


```
struct Stack {
  items: Vec<i32>
}

impl Stack {
  fn new() -> Self {
    Stack { items: Vec::new() }
  }

  fn push(&mut self, value: i32) {
    self.items.push(value);
  }

  fn pop(&mut self) {
    self.items.pop(value)
  }

  // Peaks at the top element without removing it.
  fn peek(&self) -> Option<&i32> {
    self.items.last()
  }
}

fn main() {
  let mut stack = Stack::new();
  stack.push(1);
  stack.push(2);
  stack.push(3);

  println!("{:?}", stack.peak());

  let popped = stack.pop();

  println!("{:?}", stack.peak());
}

```

### Queue Data Stricture (fifo)

A Queue data structure follows the first in first out principle.  It uses the `enqueue` and `dequeue` functions to manage the structure.

```
struct Queue {
  items: Vec<i32>
}

impl Queue {
  fn new() -> Self {
    Stack { items: Vec::new() }
  }

  fn enqueue(&mut self, value: i32) {
    self.items.push_back(value);
  }

  fn dequeue(&mut self) {
    self.items.pop_front();
  }

  // Peaks at the front element without removing it.
  fn peek(&self) -> Option<&i32> {
    self.items.front()
  }

}

fn main() {
  let mut queue = Queue::new();
  queue.enqueue(1);
  queue.enqueue(2);
  queue.enqueue(3);

  println!("{:?}", queue.peak());

  let popped = stack.dequeue();

  println!("{:?}", stack.peak());
}

```
