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

## Ownership

Rust has a concept of variable ownership.  What this means is that when a variable is passed to a function or macro it becomes the owner, once taken by a function or macro it no longer exists in the calling function.


```
fn addIntegers(a: i64. b: i64) -> i32 {
    let sum = a + b;
    sum
}


fn main  {
  let added = addIntegers(1,2); // adds 2 integers together.
  println!("{}", added); // variable passed to println! macro prints to screen
  let added2 = addIntegers(added, 5); // fails because added was passed to println! and no longer exists.
}
```




