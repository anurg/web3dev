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




### Advanced Typescript features

- Union and intersection types
- Keyof
- Typeof
- Conditional types
- Utility types
- Infer type
- Mapped types

