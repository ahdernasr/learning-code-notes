# Stack implementation

### Implementing Stack

A Stack is a data structure where the last element in is always the last element out.

2 methods:
- Push: Add an element to the the top of the stack
- Pop: Remove an element from the top of the stack

```rust 

//Stack implemention with vectors of int32 values

fn new_stack(maxsize: usize) -> Vec<u32> {
    // Creates a vector with stated max capacity
    let vec: Vec<u32> = Vec::with_capacity(maxsize);
}

fn pop(stack: &mut Vec<u32>) -> Option<u32>) {
    //Removes the last value from the stack and sets it to popped_val
    let popped_val: Option<u32> = stack.pop();
    println!("The poped value is {:?}", popped_val);
    //return the popped value
    popped_val
}

fn push(stack: &mut Vec<u32>, item: u32, maxsize: usize) {
    //if the stack is already at maxsize no value will be added
    if stack.len() == maxsize {
        println!("Cannot add more");
    } else {
        //add to stack and print it
        stack.push(item);
        println("Stack: {:?}", stack);
    }
}

fn size(stack: &Vec<u32>) -> usize {
    //Return size of stack
    stack.len();
}

fn main() {
    const MAX_SIZE = 8;
    //intialising and playing with the stack
    let mut stack: Vec<u32> = new_stack(maxsize: 8 as usize);
    push(&mut stack, item, size_Stack as usize);
    pop(&mut stack)
}


```

### String Reversal Using Stacks

Assume the stack implement above exists with its push, pop, and size methods.
However, the stack now takes chars instead of u32.

```rust
fn main() {
    let input_string: String = String::from("Welcome to rust");
    //Create the stack with its parameters
    let size_stack: uszie = input_string.len();
    let mut stack: Vec<char> = new_stack(maxsize: size_stack);
    //Initialise the reversed string as empty
    let mut rev_string: String = String::new();

    //For each character in the input string, push to the stack
    for i: char in input_string.chars() {
        push(&mut stack, item: i, maxsize: size_stack)
    }

    //For each element in the stack, push to the reversed string
    for i: usize in 0..size(&stack) {
        rev_string.push(ch: pop(&mut stack).unwrap());
    }

    //rev_string now holds the reversed string


}
```