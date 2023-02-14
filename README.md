# js-interview-prep

## How JavaScript Works?
JavaScript is a Synchronous, Single-threaded language (Can execute one command at a time in particular order).Everything in JS happens inside execution context. We can assume execution context as a place which contains two components. Memory and Code.
Memory is a place where all the variables and functions are stored as key value pairs. It is also called as Variable Environment.
Code component is place where code is executed one line at a time. Also called as Thread of execution.

![execution_context](https://user-images.githubusercontent.com/88746202/218819067-fd45594a-7231-4e7c-b4f4-6b9fd0377c15.png)

## How JavaScript code is executed?
When we run a JS program, A Global Execution Context is created. It is created in two phases.
  - Memory Creation phase
  - Code Execution phase 
Cosidering the block code,

![image](https://user-images.githubusercontent.com/88746202/218807089-513cc8b5-f0fc-4085-b7e3-0ba73a48e7e8.png)

In the first phase, memory is allocated to variables and functions. When JS encouters first varible on line 2, memory is allocated for variable `input`.
Memory space is reserved for `input` and a special value `undefined` is stored as value.
Moving forward, memory space is allocated for function `double` and stores the entire code of the function in the memory space.
Memory space is allocated for `double3` and `doubleInput` and `undefined` as value respectively. 

In phase second phase, JS runs through the whole code line by line again and executes the code now. When it encounters `input = 2`, the value `undefined` will be replaced by `2`. Moving forward to line 3 function, there is nothing to do. So it moves forward. JS encounters function invocation. 
Whenever JS encounters a function invocation a new execution context is created in two phases. 

    In phase 1, memory is allocated to variables and funtions, 
    Memory is allocted to input and result
    
    In phase 2, code is executed and the value `undefined` will be replaced by `2` and `4` after making the calculation
    When a return keyword is encountered, it states that return the control of the program to the place where the function was invoked. 
    `double3` will be replaced with  `result` which is 6 and the execution context is deleted
    
Control moves to line 8 and as soon as JS encounters function  invocation, the whole process repeats.
As the whole program finishes execution, Global execution context gets deleted.

## Call Stack 

A Stack data structure, which maintains the order of execution of Execution context. Whenever JS code runs, call stack is populated with Global execution Context. When function invocation is made, new Execution context is created and pushed into the stack. When the function finishes it's execution it is popped off from the stack.

## Hoisting in JavaScript
Hoisting is a phenomenon in JS where we can access variables and functions even before initializing with out getting any error.

![image](https://user-images.githubusercontent.com/88746202/218827532-e16f0707-9889-444b-8083-32efd6e0422e.png)
![image](https://user-images.githubusercontent.com/88746202/218827472-8091cf4e-7740-4927-a1d2-c60239766e35.png)
![image](https://user-images.githubusercontent.com/88746202/218827256-70b55e32-ff4d-4295-91f4-ce15bcb8db89.png)

When we try to access variables or functions which doesn't have memory space allocated, we will get reference error. 

![image](https://user-images.githubusercontent.com/88746202/218827084-82797da6-cd30-4b5e-bd62-4d6d986f64cd.png)

When helloWorld is an arrow function, it behaves just like another variables. `helloWorld` will be given undefined in memory creation phase

#### Does let & const declarations are hoisted? 
Yes, they get hoisted but in a different way compared to variables declared with var keyword. These declaraions will be in the temporal dead zone. 

![image](https://user-images.githubusercontent.com/88746202/218829642-ee9ae0e7-b4c0-456b-b78e-1d3843e3e249.png)
![image](https://user-images.githubusercontent.com/88746202/218829899-d174a119-db8e-4658-b091-0136c747fc27.png)

![temporaldeadzone](https://user-images.githubusercontent.com/88746202/218831028-ecbb1639-153a-4eb9-8ada-8352c8190291.png)

Variables declared with `var` keyword is allocated memory and attacted to `Global` object where as for `let` and `const` variables, memory is allocated and attached to diferent Object `Script` which is a seperate memory space. And this space can not be used/accessed before initializing the variables. 

**Temporal Dead Zone** is a phase when let & const variables are hosited till the time these variables are initialized with values. When we try to access variables which are in temporal dead zone, we will get `ReferenceError`
