# More Data Types

## Structures, Traits, Generics, Enums

### Structs Basics

Groups items of different types into a single types.
Structus are essentially a collection of different or the same data types.

```rust

//Each field is assigned a type
struct Person {
    citizienship: String,
    name: String,
    age: i32,
    gender char,
    salary: i32
}

//Creating an implementation of the structure
//Contains the functions we can have for each struct
impl Person {
    // self indicates the current instance of the struct
    fn compute_taxes(&self) -> f32 {
        (self.salary as f32 /3.) * 0.5
    } // this would return ( 150_000 / 3 ) * 0.5

    //handmade constructor with default values
    fn new() -> Self {
        Person {
            name: String::from("Ahmed Nasr"),
            citizenship: String::From("Egypt"),
            age: 19,
            gender: 'M',
            salary: 150_000,
        }
    }
}

//Creating an instance of the structure
let person: Person = Person{
    name: String::from("Ahmed Nasr"),
    citizenship: String::From("Egypt"),
    age: 19,
    gender: 'M',
    salary: 150_000,
};

person1.compute_taxes()
Person::compute_taxes(&person1)
// these would return ( 150_000 / 3 ) * 0.5

Person::new()
// this would create the default instantiation


//Using values from other structures:
let person3: person = Person {
    age:50,
    name: String::from("Mohammed")
    ..person1
}
//This person has its own age and name but all the other properties come from person1

```

This helps avoiding repeating code, since methods and variables can be recycled as many times as we need.

Tuple structures are very similar to struct but they do not have a name associated with individual fields like normal structs do

```rust 

//tuple struct
struct Numbers(i32,i32)
let some_nums: Mumbers = Numbers(32, 16);

```

### Traits and Default Implementation

Traits are an abstract definition of shared behavior among different structures.

``` Rust 

//2 Seperate Structs, Person and Student
struct Person {
	citizenship: String, 
	name: String, 
	age: u8,
	gender: char,
	salary: i32,
}

struct Student {
	name_std: String,
	age: u8,
	sex: char, 
	country: String
}


trait GeneralInfo {
    //Code inside the functions here is not necessary, but if it was implemented it would be the default implementation which would be ran if the implementation was run on a function where the function is not defined

    //The functions in a trait may also use eachother

	fn info(&self) -> (&str, u8, char);
	fn country_info(&self) -> str;
}

impl GeneralInfo for Person {
	fn info(&self) -> (&str, u8, char) {
		(&self.name, self.age, self.gender)
	}

	fn country_info(&self) -> &str {
		&self.citizenship
	}
}

impl GeneralInfo for Student {
	fn info(&self) -> (&str, u8, char) {
		(&self.name_std, self.age, self.sex)
	}

	fn country_info(&self) -> &str {
		&self.country
	}
}

let person1: Person = Person{}
let student1: Student = Student{}

person1.info()
student.info()
//returns info on person1 and student1

```

### Enums

Enumerators are types that represent data that is one of several possible variants.

```rust

enum Direction {
    Up,
    Down, 
    Left, 
    Right
}

imp Direction {
    fn is_up(&self) -> bool {
        if let Color::up = self {
            return true;
        }
        return false;
    }
}

fn main() {
    let player_direction:Direction = Direction::Up;

    match player_direction {
        Direction::Up ==> println!("Heading Up")
        Direction::Down ==> println!("Heading Down")
        Direction::Right ==> println!("Heading Right")
        Direction::Left ==> println!("Heading Left")
    }
}


```

### Generics 

Generics are a facility to write code for multiple contexts with different types

```rust

//Returns self, no matter what type T is 
fn return_self<T> (x:T) -> T {
    x
}

//std:ops:Mul<Output = T> + Copy is used to restrict the generic to only types that have the multiplication trait and the copy trait
fn square<T: std::ops:Mul<Output = T> + Copy> (x: T) -> T {
    x*x
}

//for longer lists:
fn square<T> (x: T) -> T 
where T:  std::ops:Mul<Output = T> + Copy + std::ops::Add
{
    x+x;
    x*x
}

square(5)
square(5.5)
//both work

```

Generics can also be implemented with structs

```rust

struct Point<T, U> {
    x: T,
    y: U,
}

//Implementation
imp<T, U> Point<T, U> 
where T: std::fmt::Debug, U: std::fmt::Debug
{
    fn printing(&self) -> (<T>, <U>) {
        (self.x, self.y)
    }
}

let p1: Point<i32, i32> = Point {x: 5, y:5}
let p2: Point<f64, f64> = Point {x: 5.0, y:5.0}
let p3: Point<i32, f64> = Point {x: 5, y:5.0}
//All work


```

### Option and Result Enums

Option enum is an enum with 2 variants:
- None
- Some(T)

```rust 

let mut disease: Option<String> = None;
disease = Some(String::from("Diabetes"))

match disease {
    Some(disease_name: String) => "handle"
    None => "handle"
}

disease.unwrap()
///the value of disease goes from Some("Diabetes") to just "Diabetes
//This works for all data types.

```

Result enum is an enum with 2 variants:
- Ok(T)
- Err(E)

```rust

fn division(divident: f64, divisor: f64) ->         Result<f64, String> {
    if divisor == 0.0 {
        Err(String::from("Error: Divison by zero")       
    } else {
        Ok(divident / divisor)
    }
}

division(64.0, 8.0)
//returns Ok(8)
division(2.0, 0.0)
//returns Err(Error: Division by zero)

//Another use with vectors
let some_vec: Vec<i32> = vec![5,5,2,1,5,9]
let result1: Result<&i32, &str> = match some_vec.get(index: 5) {
    Some(a: &i32) => Ok(a)
    None => Err("The value does not exist")
}

```

### Hash Maps

A HashMap is a data structure that allows us to store data in key-value pairs.
- Each value is associated with a corresponding key.
- Keys are unique, whereas values can duplicate.
- Values can be accessed using their corresponding keys.

```Rust

use std:collections::HashMap;

let mut person:HasMap<&str, i32> = HshMap::new()
//k: Key, v: Value
person.insert(k: "Ahmed", v: 18)
person.insert(k: "Mo", v: 21)

//overwrite previous value
person.insert(k: "Ahmed", v: 19)

person.get("Ahmed")
//Returns Option with Some(v) which is 19 here

person.contains_key("Amin")
//false

//looping hashmaps:
for (name, age) in &person {
    ...
}
//Order is random on each run

```

HashMap use case: counting quantity of elements in a vector:

```rust

let some_vec: Vec<i32> = vec![5,5,8,8,1,0,1,5,5,5,5];
let mut freq_vec::HashMap<i32, u32> = HasMap::new();

for i: &i32 in &some_vec {
    let freq: &mut u32 = freq_vec.entry(key: *i).or_insert(default: 0);
    *freq += 1
}

//returns {1: 2, 8:2, 5:6, 0: 1}

```