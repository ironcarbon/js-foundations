# js-foundation

# JS Engine
* JS is single threaded language which uses callback queue.
*  Computer can only understand ones and zeros. Computer does not know what is JS file so V8 engine understands JS, it reads our code and then it runs this code.
*  Thanks to the JS Engine which was found by Brendan Eich(SpiderMonkey for Firefox), we are able to run the code on a browser, previously could only read HTML and CSS.

* JS File        ->         JS Engine        ->          Computer

*  JS Engine understand the JS file and tell the computer what to do(translator)

![JS ENGINE](images/js-engine-1.png)


# Inside the JS Engine:

* JS engine can be built by anybody but it is a lot of work. V8 engine which was built by Google is the fastest and is written in C++ which is low level programming language.
* If everybody creates its own JS, it would be a total chaos which is why ECMAScript was created. It defines the standard of JS engines and how it should work. ECMAScript is a governing body of a JS that essentially decides how the language should be standardized.
* Once we understand JS engine principles and why it’s built the way, we will able to write OPTIMIZED CODE.

# Interpreters and Compilers

* There are 2 ways to run JS using an interpreter or a compiler.

* In programming, there are generally 2 ways of translating to machine language or something that our computers can understand. It applies to most programming languages like JS, Python, Java, C++. They all use some of these concepts.

Interpreter: Translation happens LINE BY LINE on the fly.

Compiler: DOES NOT TRANSLATE ON THE FLY.  Compilers work a head of time to create a translation of what code we have written and compiles down to usually a language that can be understood by machines.
* It basically takes the WHOLE CODE and try to understand what code does. Then, it takes the program in JS or ay type of language and WRITE A NEW PROGRAM IN A NEW LANGUAGE that computer can understand.

![JS Engine 2](images/interpreter-compiler-1.png)

![JS Engine 3](images/interpreter-compiler-2.png)

![JS Engine 4](images/interpreter-compiler-3.png)
* Interpreters start translating their first line and runs the code for us. An interpreter is a natural fit for something like JS. JS originally was created for the browser.
* Compiler takes little bit longer to start up because it has to go to compilation step at the beginning. Go through our code, understand it and spit it out into another language. Compiler does not need to repeat the translation for each pass through so the edits that compilers do are called OPTIMIZATION


* BABEL is a JS compiler that makes your modern JS code and returns browser compatible JS(older JS)
* TYPESCRIPT is a superset of a JS that compiles down to JS.
* Both of these do what compilers do: TAKE ONE LANGUAGE AND CONVERT INTO A DIFFERENT ONE!


WRITING OPTIMIZED CODE/ EFFICIENT CODE:
* We want to write code in a way that helps compiler make the optimization.
* Paramater restructuring is best way to not use arguments in the function which might deoptimized code!
* For in loop could be problematic for iterating objects so USE Object.keys()
* delete keyword in JS could be problematic.
* eval()
* With 

Hidden classes
Inline caching  is done by compiler



# Optimization takeaways
1. Always instantiate your object properties in the same order so that hidden classes, and subsequently optimized code, can be shared.
2. Adding properties to an object after instantiation will force a hidden class change and slow down any methods that were optimized for the previous hidden class. Instead, assign all of an object’s properties in its constructor.
3. Code that executes the same method repeatedly will run faster than code that executes many different methods only once (due to inline caching).


# WebAssembly
WebAssembly have the standard binary executable format.
WebAssembly is a way to take code in any programming language and run it within a web browser.
- It runs really really fast on the browser instead of going through the entire JS engine process. Might be game changer in the future.

# Call Stack and Memory Heap
* JS Engine basically reads our code and executes it.
* Call Stack is a region in memory which operates in FIRST IN LAST OUT mode.
* Call stacks stores functions and variables as your code executes at each entry state of the stack also called stack frame which allows us to know where we are in the code and it runs in FIRST IN LAST OUT mode.
* We use memory heap to actually point to different variables and objects that we store so that we know where to look.
* Call Stack stores only functions which are pushed into it.
Variables are stored in memory heap directly.


![Call Stack and Memory Heap 1](images/callstack-memoryheap-1.png)

![Call Stack and Memory Heap 2](images/callstack-memoryheap-2.png)


# Stack Overflow: 
Maximum stack size exceeded warning pops up instead of crashing the browser. 
1. Recursion
2. A lot of function is nested each other


# Garbage Collection: 
JS is a garbage collected language that means when js allocates memory like within a function we create an object and that object gets stored somewhere in memory heap automatically with JS when we finish calling the function and let’s say we don’t need that object anymore. It is going to clean it up for us.

JS automatically frees up the memory that we no longer use and will collect our garbage.

* In JS, garbage collector freeze memory on the heap and prevents memory leaks that is when the memory gets too big until it reaches maximum size. (Mark and Sweep Algorithm)

# Memory Leak: Memory is limited. Reasons of memory leak:
1. Global Variable: Do not use too many global variables.
2. Event Listeners: Adding event listeners and never remove them when you don’t need them.(Especially in single page applications)
3. setInterval(() => {
4. // referencing objects
5. }) 
6. —If we don’t stop setInterval, it will keep running

To write an efficient code, we have to be conscious to not have stack overflow or a memory leak and to manage that memory well.

# Single Threaded
* JS is a single threaded language which means that only one set of instructions is executed at a time. It does not do multiple things. Easy way to check that language is single threaded or not => Look how many call stack it has!
* One call stack allow us a run code one at a time. We can not run functions in parallel. Because of this js is SYNCHRONOUS that is wanted to time in order that it appears. Only one thing can happen at the time.

* alert(‘hi’) mimics the long running JS. The website is frozen in time until taking some sort of action.




## Types in JS

* In programming, there are 2 types of languages: dynamically and statically typed languages.

# JS Types
1. Numbers
2. Boolean
3. String
4. Undefined    ==> absence of definition. It is used as the default value when the JS engine initialize our variables.
5. Null     ==> absence of value
6. Symbol('hello')   => created with ES6, mostly use for object properties so that object property is unique.
7. {}

* typeof operator in JS tells us the type of the item.
typeof true
typeof null
typeof {}

* Arrays and Functions are OBJECT!
* We can add a property to a function just like we can do with an object with a dot notation.

function a(){
    return 'hello'
}

a.name = 'ipek'
console.log(a.name)

* In JS, there are primitive and non primitive types.

Primitive Type: It is a data that only represents a single value so that means primitive type directly contains the value of that type.

Built-in objects with come with JS. Primitive types can create a wrapper object around this primitive value.

true.toString()   // 'true'
* Primitive types are always primitives but to chain different methods, they can create a wrapper object.

* Arrays are objects in JS. typeof []  // object
- To test if that is array:
 Array.isArray([1,2,3])  //true
 Array.isArray({1,2,3})  //false

 # Pass By Reference vs Pass By Value
 * Primitive types are immutable. We can't really change them. In order to change them, we need to completely remove the primitive type.  =>Pass by value: copy the value and create that value somewhere else in memory.

 * Objects in JS are stored in memory and are passed by reference which means that we don't copy the values like we did with primitive types.

* Having an object helps saving space in memory. Not copying and cloning the object.

concat() method

* Each object gets passed by reference.

# Type Coercion
* In JS, type coercion happens when you use DOUBLE EQUAL. Double equal simply means compare two values and if they have different types try to coerce one into the same type.
* Three equals means compare two values but don't try to coerce the values.
* Type coercion does not happen just with the equals sign. You can also do an IF STATEMENT.
-0 === +0   //true
Object.is(-0,+0)  //false

* Prefer using three equals because type coercion in JS could be tricky.
* Always use the same types for operations.
* NaN === NaN returns always false because in this comparison, they are two different NaN objects which point to two different references in memory.

* Empty array is considered as false because length of the parameter is 0.
* The Object.is() method determines whether two values are the same value.



## 2 Pillars: Closures and Prototypal Inheritance
# Functions
* Functions in JS are also object. 
When we invoke a function, we get 2 parameters automatically. 'this' + 'arguments' (array like object)
* Because of the 'arguments' object, we can't technically have any parameters defined for a function.?
* When we define our functions and the compiler looks at our code lexically. It determines what variables are available for us in our variable environment.

# Higher Order Functions
* Simply a function that can take function as an argument or function returns another function.
Why useful?


# Closures

* Closures are also called lexical scoping(staticlly scoped). Lexical means where it is written, scoping is what variable we have access to.

* Functions returns functions  => closure

# PROTOTYPE

# 4
![Prototype 1](images/prototype2.png)
![Prototype 2](images/prototype1.png)
![Prototype 3](images/prototype3.png)
![Prototype 4](images/prototype4.png)


## FUNCTIONAL PROGRAMMING
![Perfect Function](images/perfect-function.png)


## OOP VS FP
* Inheritance is a superclass that is extended to smaller pieces that add or overwrite things. Base class must be very general so that don;t overload the subclasses. It can easily get out of hand.

* In composition, it is about smaller pieces that are combined to create something bigger. And if we need to add something later on, we can add another puzzle by composing things together.

 ## ASYNCHRONOUS

Async functions are functions that we can execute later.

When JS engine sees something that is asynchronous, it send it over the web API.

JS is a single threaded language that can be non-blocking. Single threaded means it has only one call stack and it can only do one thing at a time. In call stack, first in last out. Whatever is at the top the call stack gets run first then below that below until the call stack is empty.
In order to not block the single thread, it can be asynchronous with callback functions.

(Other languages are multi-thread)Deadlocks could be a problem with them.

Synchronous code is executed line by line.

What is the program?
1. It has to allocate memory otherwise we would not be able to have variables.
2. It also has to parse and execute scripts which means read and run commands.

JS engine consist of two parts memory heap and call stack.
In memory heap where memory allocation happens.
In call stack where the code is read and executed. It tells where you are in the program.

Memory Leak; we have a limited memory and memory leak happens when we have unused memory which fill up the memory heap. That's why global variables are bad.

Stack Overflow is when stack is overflowing. Call stack is getting bigger and does not have enough space anymore. Recursion might cause a stack overflow.

Synchronous code is predictable. We know what happens first then what happens next. But it can get slow.

In order to run JS, it needs more than JS ENGINE. It needs JS RUN TIME ENVIRONMENT which is part of the browser.(included in browsers)

JS run time environment have extra things on top of the engine which are WEB API, CALLBACK QUEUE and EVENT LOOP.

onClick, onLoad, onDone Event listeners have callback functions. When the event happens, function start to work.
 
 

## SUMMARY

* Memory heap gets cleaned up by garbage collection.

* Variables can not be overwritten fully. When you defined variable, it has already gotten undefined in global execution context but functions are different. Functions are fully hoisted.



# hoisting

* Any variable declaration are assigned a default value of undefined during the creation phase of execution context and this term is hoisting.

* Function Execution Context: It is created whenever function is invoked.

# scope

* Where variables are accessible.
& Current execution context.
* If JS engine can't find a variable in local(like function's execution context), it will look to the nearest parent execution context for the variable. That lookup process will continue all the way up, until the engine reaches the global execution context. In that case, if the global execution context does not have the variable, then it will throw a ReferenceError, because that variable does not exist anywhere up the scope chain or the execution context chain.

# closure scope


# this
* 'this' is the object that function is property of
*  Methods are functions that are inside of objects so the property methods can be accessed with dot notation.
* Whatever to the left of the dot which is the object that the function is a property of.

2 main benefits of using 'this'
 1. gives methods access to their object
 2. execute same code for multiple objects


 * this ==> It matters HOW THE FUNCTION WAS CALLED not where it is written like lexical scope.

* Everything in JS is actually lexical scoped how you write, it determines what we have available except THIS keyword

* 'this' keyword is DYNAMICALLY SCOPED so HOW THE FUNCTION WAS CALLED is the matter!

*
    How we can solve this?

    Arrow functions are LEXICALLY bound so they have lexical behaviour.