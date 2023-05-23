# Ownership
### Primitive and Non-primitive types

```rust
/* 
Main Rules:
- Each value in Rust has a variable thats called its owner
- There can only be one owner at a time
- When the owner goes out of scope, the value will be dropped

Copy is made when there is a seperate memory location
Move is when there is a change of ownership

Primitive types copy, while Non-primitive types move
Primitives: integers, floats, chars...
Non-primitives: strings, vectors, arrays...

OWNERSHIP DOES NOT APPLY FOR PRIMITIVE TYPES
*/

let vec_1: Vec<i32> = vec![5,6,7,8,9]
let vec_2: Vec<i32> = vec_1.clone(); //Copy of vec1 to vec2
let vec_3: &Vec<i32> = &vec_1 //Referes to the value in vec_1
```

### Ownership and References in Functions

```rust
/*

When a primitive type (in the heap) is passed through a function
It's value is COPIED to the new variable inside the function
It is not moved

*/

fn stack_function(mut stack_num: i32) {
	stack_num = 56
	println!("Var: {}", stack_num)
}

let var: i32  = 32;
stack_function(var);
//value of var is copied to stack_num
//so now there is two different places in the stack for var and stack_num

/*

When a non-primitive type (in the stack) is passed through a function
It's value is MOVED to the new variable, and its ownership is DROPPED
It's value will be dropped
When the function runs and finishes, the value of the function
is dropped too.

*/

fn heap_functin(var: Vec<i32>) {
	println("Var: {:?}", var)
}

let mut heap_vec: Vec<i32> = vec![4,5,6]
heap_function(heap_vec)
//heap_vec ownership is lost, var has new ownership

//if you want to keep the value of heap_vec, call the function
//with a reference to a vector instead
fn heap_functin(var: &Vec<i32>) {
	println("Var: {:?}", var)
}
heap_function(&heap_vec)
//If you were to update the value insdie the function now
//The change would appear everywhere
```

### Mutable and Immutable References

```rust
/*

References Rules:
- One mutable reference in a scope
- Many immutable references
- Mutable and immutable can not coexist
- Scope of a reference
- Data should not change when immutable references are in scope

*/

let mut heap_num: Vec<i32> = vec![4,5,6];

let ref1: &mut Vec<i32> = &mut heap_num;
let ref2: &mut Vec<i32> = &mut heap_num;
//Not allowed

let ref1: &mut Vec<i32> = &heap_num;
let ref2: &mut Vec<i32> = &heap_num;
//Allowed

let ref1: &Vec<i32> = &heap_num;
let ref2: &mut Vec<i32> = &heap_num;
//Not allowed, in the same scope
//Scope of a reference:
//From the point it is instantiated, to the last point it is used

```