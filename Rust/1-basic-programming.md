# Basic Programming Concepts
### Program Outputs and Comments

```rust
print!(
	"This is going to be 
	printed on multiple
	lines"
);

println!("This is going to be printed on one line").

println!("{} {}", "Ahmed", "Nasr");
//Ahmed Nasr, printing out variables into the print statement

println!("{:?}", (1, 2, 3, 4));
//(1, 2, 3, 4)
```

### Variables and Scalar Data Types

```rust
let mut x: f32 = 15:0;
//mut -> variable data type
//:f32 -> 32bit floating point number

/* 
Scalar Types:
- Integers
	-> Signed types: can store postitive or negative values:
			i8, i16, i32, i64
	-> Unsigned types: can only store postitive values
			u8, u16, u32, u64
- Floats 
	-> f32, f64
- Boolean
	-> bool
- Characters
	-> single letters, digits, emojis, unicode scalars
*/

println!("The max number in i8 = {}", std::i8::MAX);
//127 (8 bits allocated)

```

### Shadowing and Constants

```rust
//Initialise multiple variables in the same statement
let (first_number: i32, second_number: f64) = (250, 480.22);

//Underscores instead of commas
let largenumber: i32 = 1_000_000;

//Change types of sum of two numbers
let n3: i32 = n1 + n2 as f64

/* 
Shadowing 
-> Concept of using or updating a variable with the same name

Shadowing variable's mutability also takes hold
*/

//Constants are not changed, cannot be changed to mut
const MAX_SALARY:u32 = 100_000;

```

### Compound data types: strings

```rust
// Fixed length strings: &str
let some_string: &str = "Fixed length str";

//Growable strings (String)
let mut growable_string: String = String::from("Growable str")
 
//Add character
growable_string.push('s')

//Pop last character
growable_string.pop()

//Add string to string
growable_string.push_str('string to be pushed')

/* 
Other functions:
- .is_empty()
- .len()
- .capacity
- .contains()
- .trim()
*/

//Non string to string
let num_str: String = number.to_string()
//Note that this can replace String::from
```

### Tuples and Arrays

```rust
/*
Tuples
-> Fixed length
-> Collection of values of different/same types
*/

let my_infromation: (&str, i32) = ("Salary", 40_000);
//accessed my my_information.i where i is the index

//destructuring
let (salary: &str, salary_value: i32) = my_information;

/* 
Arrays
-> Elements of the same types
-> Number of elements must be known at compile time
*/ 

let mut number_array: [i32;5] = [4,5,6,7,8];
number_array[4] = 5;

//array with the same values
let same_value_array: [i32; 10] = [0; 10];
let char_array: [char; 5] = ['a'; 5]

//subset array
let mut number_array_1: [i32;5] = [4,5,6,8,9]
let subset_array: &[i32] = &number_array_1[0...3]
//0th element to 3rd element NOT included
let subset_array: &[i32] = &number_array_1[0...=3]
//0th element to 3rd element INCLUDED

/* 
Common functions on arrays:
- array.len()
- array.get(index) returns the Value, or 'None'
*/
```

### Compound Data Type: Vectors

```rust
/* 
Vectors
- Collection of data of the same type
- Can be resized (key advantage on arrays)
*/

let mut number_vec: Vec<i32> = vec![4,5,6,7,8,9,10]
number_vec[i]
number_vec[4] = 5

let vec_with_same_elements: Vec<i32> = vec![0;10]

/* 
Common functions on vecttors:
- vector.len()
- vector.get(index) returns the Value, or 'None'
- vector.push(value)
- vector.remove(index)
- vector.contains(&value)
*/
```

### Functions and Inputs

```rust
/* Functions */

fn function(parameter: parameter_type) {

}

fn function_with_inputs_outputs(num1: i32, num2: i32) -> i32 {
	num1 * num2
}

fn function_with_multiple_outputs(num1: i32, num2: i32) -> (i32, i32, i32) -> {
	(num1*num2, num1+num2, num1-num2)
}

let result: (multiplication: i32, addition: i32, subtraction: i32)
	= function_with_inputs_multiple_outputs(10, 8)

/* Code blocks */

let full_name: String {
	let first_name: &str = "Ahmed";
	let last_name: &str = "Nasr";
	format!("{} {}", first_name, last_name)
	//No semicolon behind the last statement,
	//Meaning it is the return statement value
}

/* Taking inputs */ 

let mut n: String = String::new()
std::io::stdin()
	.read_line(&mut n)
	.expect("failed to read input");

let n: f64 = n.trim().parse().expect("invalid input")
```