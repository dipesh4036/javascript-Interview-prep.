*1) Understanding the Double Exclamation (!!) in JavaScript:*

!! does just one thing: whatever you write after it will be converted into its truthy or falsy state. For example, if we write !!-1, it will give us true.

    !!-1 gives true
    !![1, 2, 3] gives true
    !!{name: "harsh"} gives true
    !!"Hello Sheryians" gives true
    !!0 gives false
    !!null gives false
That means if you write !! in front of anything, it will give you either true or false depending on its truthy or falsy nature.

*this keyword-*
```javascript
            // Global context
            console.log(this); // Output: Window

            // Function context
            function myFunction() {
                console.log(this);
            }
            myFunction(); // Output: Window

            // Method context
            const myObject = {
                myMethod: function() {
                    console.log(this);
                }
            };
            myObject.myMethod(); // Output: myObject

            // Function inside method (ES5)
            const myObjectES5 = {
                myMethod: function() {
                    function innerFunction() {
                        console.log(this);
                    }
                    innerFunction(); // Output: Window
                }
            };
            myObjectES5.myMethod();

            // Function inside method (ES6)
            const myObjectES6 = {
                myMethod: function() {
                    const innerFunction = () => {
                        console.log(this);
                    };
                    innerFunction(); // Output: myObjectES6
                }
            };
            myObjectES6.myMethod();

            // Constructor function
            function Person(name) {
                this.name = name;
                console.log(this);
            }
            const person1 = new Person('Alice'); // Output: Person { name: 'Alice' }

            // Event listener
            const myElement = document.getElementById('myElement');
            myElement.addEventListener('click', function() {
                console.log(this);
            }); // Output: myElement
```

``` javascript
    // all in one example of this keyword
    let user = {
        username: "XYZ",
        price : "123",
        welcomemessage : function(){
            console.log(`${this.username},welcome to website`);
            console.log(this);
        }
    }
    user.welcomemessage()
    user.username = "ABC";
    user.welcomemessage()
```

*3)Understanding call, apply, and bind-*
To change a function's this value to some object of our choice, we can use call, apply, and bind.
```javascript
// usign "call"
function abcd() {
    console.log(this);
}

var obj = { name: "xyz" };

// Using `call` to change `this` inside the function from `window` to `obj`
abcd.call(obj); // `this` = { name: "xyz" }

// other example: where interview this example is very good use this example to explain.
function setUsername(username) {
    this.username = username;
    console.log("called");
}
function createUser(username,email,password) {
    setUsername.call(this,username);
    this.email = email;
    this.password = password;
}
let result = new createUser("xyz", "xyz@example.com",123)
console.log(result);

```



using "apply"
```javascript
function abcd() {
    console.log(this);
}

var obj = { name: "xyz" };

// Using `apply` to change `this` inside the function from `window` to `obj`
abcd.apply(obj); // `this` = { name: "xyz" }


```

// using bind :-bind is very similar to call, just that it doesn't call the function straightaway but returns the function to call it later whenever we want.
```javascript
function abcd() {
    console.log(this);
}

var obj = { name: "xyz" };

// Using `bind` to change `this` inside the function from `window` to `obj`
var newFunc = abcd.bind(obj);

// `newFunc` variable now contains a function which we can run in the future:
newFunc(); // `this` = { name: "xyz" }

```
*4) Understanding Pure Functions-*

A pure function is any function which has these two features:
    It should always return the same output for the same input.
    It will never change/update the value of a global variable.
```javascript
    Pure Function:
    function calc(val) {
    return val + 2;
}
    // Always returns the same answer if you pass the same value for the "val" argument,
    // hence this function is a pure function.

    // Impure Function:
    let someVal = 0;

    function calc(x) {
        someVal++;
    }

    // Changes a value of a global variable called someVal.
```
*5)  Understanding Lambda Functions-*
Lambda functions are the easy and shorter way to create functions in JavaScript.
```javascript
    // Older Way to Create Functions:
    function calc(val) {
    return val + 2;

    // Lambda Functions:
    // You put `()` and then an arrow `=>` followed by opening `{}`, and that's a lambda function.
    // Save it in a variable.
    var abcd = () => { };
}
```
Lambda functions, also known as arrow functions, provide a concise syntax for defining functions in JavaScript. They are especially handy for writing short, one-line functions or function expressions. In the example, abcd is a lambda function assigned to a variable.

*6) Understanding Currying-*
In currying, we create a function that returns another function. The returning function uses arguments of the parent function too. So, upon running the parent function, we get a new function, which, upon running, does some work with both of the arguments.

Normal Function:
```javascript
function add(val, val2) {
    return val + val2;
}

```
Currying Example:
``` javascript
function add(val) {
    return function(val2) {
        return val + val2;
    }
}

var fnc2 = add(2);
var ans = fnc2(5);

// On function call where we receive another function,
// this gets the answer 7 in variable ans.
```
In the currying example, the add function takes one argument val and returns another function. When we call add(2), it returns a function that takes another argument. This returned function (fnc2) then adds 2 to any value passed to it. In the end, ans holds the value 7, which is the result of adding 2 and 5.

*7) Understanding Temporal Dead Zone (TDZ)-*
In JavaScript, we got new ways to create variables and constants with the help of let and const, and they brought a new concept into the picture known as Temporal Dead Zone (TDZ).

In this concept, if you try using a variable created with let or const before declaring it, it will result in an error, more specifically a ReferenceError.
``` javascript
console.log(a); // ReferenceError: Cannot access 'a' before initialization
let a = 12;
```
Note: In the previous days when we used to create variables with the var keyword, there was no such error because var doesn't support TDZ, and we used to get undefined as the answer if we ever asked for a value of a variable before declaring it.

*8) Understanding Closures-*
Every time we have a function that returns another function, it creates something called closures.

In closures, there's a parent function which might contain some data/variables which can be accessed/used by the child function present inside it. The parent function always returns the child function in closures.

``` javascript
function parent(a) {
    var someVal = a + 2;
    return function(b) {
        someVal++;
        // This returning function can access or change parent's variable someVal's value.
    }
}
```
In this example, the parent function takes an argument a. Inside the parent function, there's a variable someVal which holds the value of a + 2. The parent function returns another function which can access and modify the someVal variable. This returned function is a closure, and it retains access to the variables of its parent function even after the parent function has finished executing.

*9) Understanding Synchronous and Asynchronous Code Execution-*
In synchronous code execution, code is executed line by line. The first line executes first, then the second line, and so on. This method of code execution is called synchronous code execution.

However, JavaScript also supports something called asynchronous code execution. In asynchronous code execution, some code, which is asynchronous, will move to the side stack for execution and will run after all the synchronous code is finished.

Let me explain: Imagine we have two types of code, sync and async. The first, second, and third lines are sync, and the fourth and fifth lines are async code. Now, how will they get executed?

The first, second, and third lines will move to the main stack (main stack gets executed first), and the fourth and fifth lines will move to the side stack. Code on the side stack will wait until the main stack is empty. Then, side stack code will move to the main stack for execution.

*10) Understanding Lexical Environment-*
Think of a lexical environment like a little bubble where your code lives. It holds all the things your code needs, like variables and functions, and keeps them organized. When your code runs, it looks inside its own bubble to find what it needs.
``` javascript
// Inside the lexical environment bubble:
var a = 12;
var b = 24;

function abcd() {
    console.log("hey");
}

// Other variables, functions, and stuff
```
In this lexical environment, we have defined variables a and b, a function abcd(), and potentially other variables, functions, and code. Each of these elements exists within the lexical environment and can be accessed or used by other parts of the code within the same lexical scope.

*11) Understanding Execution Context-*
Each time a function is called, a new execution context is created. It helps manage the scope of variables, keeps track of the call stack, and ensures proper execution of the code. It's the environment in which your code operates and performs its tasks.

It's like a stage for code to run.

You call a function →
Execution context gets created →
It contains lexical environment of the code, which means variables, functions, and other things related to it to execute that function.
Few more things:

Execution context
Lexical environment

*12) An IIFE (Immediately Invoked Function Expression)-*
IIFE is a JavaScript function that is executed immediately after it is defined. It's a way to create a function expression and then immediately execute it.

``` javascript
(function() {
  console.log("IIFE executed!");
})();

```

*Lexical scoping and Closure-*:

// lexical scope:  same as scope concept above
``` javascript
function outer(){
    let name = "XYZ";
    function inner(){
        console.log(name);
    }
    function innertwo(){
        console.log(name);
    }
    inner();
    innertwo();
}
outer();

```

Closure:Closure. Sorting things out can definitely bring clarity and peace. Thorn, on the other hand, seems to represent a challenge or obstacle. Maybe there's something prickly in your path that needs addressing before you can fully attain closure?


``` javascript
    function outer(){
    let name = "XYZ";
    function inner(){
        console.log(name);
    }
    return inner;
}
let result = outer()
result()
```