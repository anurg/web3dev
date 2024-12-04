### Typescript Notes

 ### Types of languages
### Strongly typed languages
    1.Examples - Java, C++, C, Rust
    2. Benefits - 
    - Lesser runtime errors
    - Stricter - codebase
    - Easy to catch errors at compile time

### Loosely typed languages
    1. Examples - Python, Javascript, Perl, php
    2. Benefits
        - Easy to write code
        - Fast to bootstrap
        - Low learning curve

People realised that javascript is a very power language, but lacks types. Typescript was introduced as a new language to add types on top of javascript.

### What is typescript?
TypeScript is a programming language developed and maintained by Microsoft. 
It is a strict syntactical superset of JavaScript and adds optional static typing to the language.

### Where/How does typescript code run?
    - Typescript code never runs in your browser. Your browser can only understand javascript. 
    - Javascript is the runtime language (the thing that actually runs in your browser/nodejs runtime)
    - Typescript is something that compiles down to javascript
    - When typescript is compiled down to javascript, you get type checking (similar to C++). If there is an error, the conversion to Javascript fails. 

### Typescript compiler
tsc is the official typescript compiler that you can use to convert Typescript code into Javascript
There are many other famous compilers/transpilers for converting Typescript to Javascript. Some famous ones are - 
- esbuild
- swc

### Bootstrap a simple Typescript App
- Step 1 - Install tsc/typescript globally
```
    npm install -g typescript
```

- Step 2 - Initialize an empty Node.js project with typescript
```
    mkdir node-app
    cd node-app
    npm init -y
    npx tsc --init
```
These commands should initialize two files in your project
    ```
    package.json
    tsconfig.json
    ```

- Step 3- Create a a.ts file
```
const x: number = 1;
console.log(x);
```
- Step 4 - Compile the ts file to js file
```
tsc -b
```
Step 5 - Explore the newly generated index.js file

### Typescript provides you some basic types
number, string, boolean, null, undefined.
 
### The tsconfig file
The tsconfig file has a bunch of options that you can change to change the compilation process.
Some of these include-

- 1. target
The target option in a tsconfig.json file specifies the ECMAScript target version to which the TypeScript compiler will compile the TypeScript code.
To try it out, try compiling the following code for target being ES5 and es2020
```
const greet = (name: string) => `Hello, ${name}!`;
```
- Output for ES5
```
"use strict";
var greet = function (name) { return "Hello, ".concat(name, "!"); };
```
- Output for ES2020
```
"use strict";
const greet = (name) => `Hello, ${name}!`;
```
- 2. rootDir
Where should the compiler look for .ts files. Good practise is for this to be the src folder
- 3. outDir
Where should the compiler look for spit out the .js files.
- 4. noImplicitAny
Try enabling it and see the compilation errors on the following code - 
```
const greet = (name) => `Hello, ${name}!`;
```
Then try disabling it
- 5. removeComments
Weather or not to include comments in the final js file


```
"target": "es2016", 
"rootDir": "./src",   
"outDir": "./dist", 
"removeComments": true, 
"noImplicitAny": true,  /* Enable error reporting for expressions and declarations with an implied 'any' type. */
```

### Sample Typescript Code
```
// Function in typescript
function greet(name:string):string {
    return `Hello ${name}`
}
console.log(greet("Anurag"))

// Function with return
function sum(a:number,b:number):number {
    return a+b
}
console.log(sum(2,5))
```
### Type inference

```
function isLegal(age: number) {
    if (age > 18) {
        return true;
    } else {
        return false
    }
}

console.log(isLegal(2));
```
### Function Calling another Function
```
function delayedCall(fn: () => void) {
    setTimeout(fn, 1000);
}

delayedCall(function() {
    console.log("hi there");
})
```

### Typescript Interfaces
How can you assign types to objects? For example, a user object that looks like this - 
```
const user = {
	firstName: "harkirat",
	lastName: "singh",
	email: "email@gmail.com".
	age: 21,
}
```
To assign a type to the user object, you can use interfaces
```
interface User {
	firstName: string;
	lastName: string;
	email: string;
	age: number;
}
```
### Assignment #1 - Create a function isLegal that returns true or false if a user is above 18. It takes a user as an input.
```
interface User {
    name:string;
    email:string;
    age:number
}
function isLegal(user:User):boolean {
    return user.age>18
}
```
### TODO Assignment #2 - Create a React component that takes todos as an input and renders them

### Implementing interfaces
Interfaces have another special property. You can implement interfaces as a class.
Let’s say you have an personinterface - 
```
interface Person {
    name: string;
    age: number;
    greet(phrase: string): void;
}
```
You can create a class which implements this interface.
```
class Employee implements Person {
    name: string;
    age: number;

    constructor(n: string, a: number) {
        this.name = n;
        this.age = a;
    }

    greet(phrase: string) {
        console.log(`${phrase} ${this.name}`);
    }
}
```
### types
Very similar to interfaces , types let you aggregate data together.But they let you do a few other things.
```
type User = {
	firstName: string;
	lastName: string;
	age: number
}
```
- 1. Unions
Let’s say you want to print the id of a user, which can be a number or a string.
You can not do this using interfaces
```
type StringOrNumber = string | number;
function Id(id:StringOrNumber) {
    console.log( `Id: ${id}`)
}
Id(25)
Id("Hello")
```
- 2. Intersection
What if you want to create a type that has every property of multiple types/ interfaces
You can not do this using interfaces
```
type Employee= {
    name:string;
    startDate:Date;
}
type Manager = {
    name:string;
    department:string;
}

type TeamLead = Employee & Manager;
const teamLead:TeamLead = {
    name:"Anurag",
    startDate:new Date(),
    department:"IT"
}s
```
### Arrays in TS
If you want to access arrays in typescript, it’s as simple as adding a [] annotation next to the type.
- Example 1: Given an array of positive integers as input, return the maximum value in the array
```
function maxValue(arr:number[]):number {
    let max = 0;
    for (let i=0;i<arr.length;i++) {
        if (arr[i]> max) {
            max = arr[i]
        }
    }
    return max
}

console.log(maxValue([1,2,3,4,5,4,3,2,4,5,6,7]))
```

- Example 2: Given a list of users, filter out the users that are legal (greater than 18 years of age)
```
interface User {
    name:string;
    age:number;
}
function fileteredUsers(users:User[]):User[] {
   return users.filter(u=>u.age>=18)
}

const users: User[] = [
    {
        name:"Anurag",
        age:50
    },
    {
        name:"Harry",
        age:17
    }
]

console.log(fileteredUsers(users))
```
### Enums

Enums (short for enumerations) in TypeScript are a feature that allows you to define a set of named constants.
The concept behind an enumeration is to create a human-readable way to represent a set of constant values, which might otherwise be represented as numbers or strings.

```
enum Direction {
    Up,
    Down,
    Left,
    Right
}

function doSomething(keyPressed: Direction) {
	// do something.
}

doSomething(Direction.Up)
console.log(Direction.Up)
```
The final value stored at runtime is still a number (0, 1, 2, 3). 

### How to change values?
```
enum Direction {
    Up = 1,
    Down, // becomes 2 by default
    Left, // becomes 3
    Right // becomes 4
}

function doSomething(keyPressed: Direction) {
	// do something.
}

doSomething(Direction.Down)
console.log(Direction.Down)
```

### Can also be strings
```
enum Direction {
    Up = "UP",
    Down = "Down",
    Left = "Left",
    Right = 'Right'
}

function doSomething(keyPressed: Direction) {
	// do something.
}

doSomething(Direction.Down)
console.log(Direction.Down)
```
### Common usecase in express
```
enum ResponseStatus {
    Success = 200,
    NotFound = 404,
    Error = 500
}

app.get("/', (req, res) => {
    if (!req.query.userId) {
			res.status(ResponseStatus.Error).json({})
    }
    // and so on...
		res.status(ResponseStatus.Success).json({});
})
```
### Generics
- 1. Problem Statement
Let’s say you have a function that needs to return the first element of an array. Array can be of type either string or integer.
How would you solve this problem?

```
function getFirstElement(arr:(string|number)[]) {
    return arr[0];
}

console.log(getFirstElement([1,2,3]))
```
What is the problem in this approach?
User can send different types of values in inputs, without any type errors
```
console.log(getFirstElement([1,2,`3`]))
```

Typescript isn’t able to infer the right type of the return type
```
const el = getFirstElement(["harkiratSingh", "ramanSingh"]);
console.log(el.toLowerCase())
```
Typescript shows error
```
Property 'toLowerCase' does not exist on type 'string | number'.
  Property 'toLowerCase' does not exist on type 'number'.ts(2339)
any
```

### Solution - Generics
Generics enable you to create components that work with any data type while still providing compile-time type safety.
```
function Identity<T>(arg:T):T {
    return arg
}

console.log(Identity<string>("Hello"))
console.log(Identity<number>(35))
```
- Solution to original problem
```
function getFirstElement<T>(arr:T[]):T {
    return arr[0];
}

console.log(getFirstElement<number>([1,2,"3"])) //This line will give error
const el = getFirstElement<string>(["harkiratSingh", "ramanSingh"]);
console.log(el.toLowerCase())  //Now TS is able to infer type
```
### Exporting and Importing Modules

TypeScript follows the ES6 module system, using import and export statements to share code between different files. 

### 1. Constant exports
- math.ts
```
export function add(x: number, y: number): number {
    return x + y;
}

export function subtract(x: number, y: number): number {
    return x - y;
}
```
- main.ts
```
import { add, subtract } from "./math"

add(1, 2)
```
### 2. Default exports
```
export default class Calculator {
    add(x: number, y: number): number {
        return x + y;
    }
}
```
- calculator.ts 
 ```
import Calculator from './Calculator';

const calc = new Calculator();
console.log(calc.add(10, 5));
```

https://angularexperts.io/blog/advanced-typescript?ref=dailydev 
### Advanced Typescript features

- Union and intersection types
- Keyof
- Typeof
- Conditional types
- Utility types
- Infer type
- Mapped types

