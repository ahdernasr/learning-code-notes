# Control Structures
### If statements

```rust
/*
Logical Operators:
- And: &&
- Or: ||
- Equal: ==
- Negation: !=
*/

let some_number: i32 = 40;
if some_number < 50 {
	println!("Number is smaller than 50")
} else if some_number > 50 {
	println!("Number is bigger than 50");
} else {
	println!("Number is equal to 50");
};

//let if 

let value: i32 = if true {
	1
} else {
	2
};

```

### Match statements

```rust
/*

match value {

	possible_value => {statements to execute},
	possible_value => {statements to execute},

	_ => {default execution of some statements}

}

*/

match some_number {

	1 => println("The number is 1")
	2|3 => println("The number is 2 or 3")
	4..=10 => println("The number is between 4 and 100")
	_ => println("The number is greater than 100")

}

//let match is also used, same syntax as above for if

```

### While and Simple Loops

```rust
loop {
	println!("This is an infinite loop")
}

while action != true {
	println!("This is a while loop")
}
```

### For Loops

```rust
let mut some_vec: Vec<i32> = vec![45,30,85,90,41,39]

for i: i32 in 0..=5 {
	println!("{}", some_vec[i]);
}
//45 30 85 90 41 39

for i: i32 in some_vec {
	println!("{}", i);
}
//45 30 85 90 41 39
//However, ownership of some_vec is lost here, to avoid:

for i: &i32 in some_vec.iter() {
	println!("{}", i)
}
//or
for i: &i32 in &some_vec {
	println!("{}", i)
}
//45 30 85 90 41 39
//Ownership remains in both

for i: &mut i32 in some_vec.iter_mut() {
	*i += 5; //pointer
	println!("{}", i)
}
//50 35 90 95 46 44
// 'i' can be used to update values in some_vec now without passing ownership

```

### Break and Continue

```rust
/*
	Break: for stopping a loop
	Continue: for skipping the current iteration
*/

loop {
	if action {
		break; //breaks out of loop
	}
}

```