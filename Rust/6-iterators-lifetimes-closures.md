# Iterators, Lifetimes, and Closures

### Lifetimes

A lifetime is a construct the compiler uses to ensure all borrows are valid. 
It explains the scope in which a reference is valid.


```rust 

//dangling reference example

let int integer = 10;
let additional_int: &i32 = some_fn(integer);

fn some_fn(i: i32) -> &32i {
    &i
}

//this does not work because the function is providing a reference to a value that's lifetime is finished after the function runs
//this is why understanding lifetimes is important

```

### Closures

Rust's closures are anonymous functions you can save in a variable or pass as arguments to other functions. They also capture the environment around them

```rust

{

    //closure captures this
    let x:i32= 9;
    let y:i32= 10;

    let closure: || -> () = |num: i32| -> i32 {
        x+y+num
    }

    //Different syntaxes:
    let closure1: |u32| -> u32 = |x: u32| -> u32 { x + 1};
    let closure1 = |x| { x + 1}; //type is inferred
    let close3 = |x| x + 1; //one line so no curly brackets needed, type is inferred

}

```

### Iterators

An iterator is responsible for the logic of iterating over each item and determining when the sequence has finished

```rust

let some_vec: Vec<i32> = vec![1,2,3,4,5,6,7];
let mut iter: Iter<i32> = some_vec.iter()

> iter
// Iter([1,2,3,4,5,6,7])

> iter.next()
//Some(1)
> iter.next()
//Some(2)

//if there is nothing left in the vector, it returns the None variant

//methods for iterators:
//any function: returns true is any of the values pass a certain condition and false if none of them do
let a: Vec<i32> = vec![1,2,3,4,5,6,7];
let mut check: bool = a.iter().any(|&x: i32| x > 0)
> check
//Some(True)

//all function: returns true if all the values satisfy the given condition
let mut check: bool = a.iter().all(|&x: i32| x > 3)
> check
//Some(False)

//find function: will search for ONE element that satisfies the condition, returns None if none of the elements pass
let mut check: bool = a.iter().find(|&&x: i32| x > 3)
> check
//Some(4)

//position function: will return the poisition for ONE element that satisfies the condition, returns None if none of the elements pass
let mut check: bool = a.iter().position(|&x: i32| x > 3)
> check
//Some(3)

//max: will return the biggest value, min: will return the smallest value
let mut check: bool = a.iter().max()
> check

//Iterates through the vector from back to front
let mut iter: Iterator<Item = &i32> = a.iter().rev()
//Some(7)

```

2 More advanced functions for iterators are collect and filter.

```rust

let a: Vec<i32> = vec![0,1,2,3,4,5,6,7];
let some_values: Iterator<&i32> = a.iter().filter(|&x| *x >= 5); //returns new iterator that iterators through the vector filtered y the condition
let collected_values: some_values.collect::<Vec<&u32>> //Collects the iterator into a new vector, note this is a vector of references

//Collects the iterator into a new vector, but it is no longer in references
let some_values: Iterator<&i32> = a.into_iter().filter(|&x| x >= 5)some_values.collect::<Vec<u32>> 
//Vector a is no longer owner of its vector

let mut mapped_values = a.iter().map(|x| 2* *x).collect::<Vec<u32>>();
>mapped_values
//0,2,4,6,8,10,12,14

```