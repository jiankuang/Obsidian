### Introduction
Closure is the most esoteric of JavaScript concepts. It can  
* Enables powerful pro-level functions like 'once' and 'memoize'
* Build iterators and generators, handle partial application  
* Module pattern: Preserve state for the life of an application without polluting the global namespace. 
* Asynchronous JavaScript: Callbacks and Promises rely on closure to persist state in an asynchronous environment.  

Functions get a new memory every run/invocation. 

Functions with memories 
* When our functions get called, we create a live store of data (local memory/variable environment/state) for that function's execution context. 
* When the function finishes executing, its local memory is deleted (except the returned value)
* But what if our functions could hold on to live data between executions? 
* This would let our function definitions have an associated cache/persistent memory 
* But it all starts with us **returning a function from another function**
### Returning Functions 
```js
function createFunction() {
	function multiplyBy2(num) {
		return num*2
	}
	return multiplyBy2
}

const generatedFunc = createFunction()
const result = generatedFunc(3) // 6
```
`generatedFunc` definition is stored in global memory, not in `createFunction` local memory.
In this case, `generatedFunc` has nothing to do with `createFunction` after `createFunction` is executed. 
![[Closure - Returning Functions.png]]
### Nested Function Scope 
Calling a function in the same function call as it was defined. 
```js
function outer() {
	let couter = 0;
	function incrementCounter() {
		counter++
	}
	incrementCounter()
}
outer()
```
Q: Where you define your functions or where you run your functions determines what data it has access to when you call it? 
![[Closure - Nested Function Scope.png]]
### Retaining Function Memory 
Calling a function outside of the function call in which it was defined. 
```js
function outer() {
	let counter = 0
	function incrementCounter() { counter++ }
	return incrementCounter
}

const myNewFunction = outer()
myNewFunction() // counter = 1
myNewFunction() // counter = 2
```
A: Where you define your functions determines what data it has access to when you call it.  
![[Closure - Retaining Function Memory.png]]
### Closure Technial definition
What can we call this "Backpack" ? 
- Closed over 'Variable Environment' (C.O.V.E.)
- Persistent Lexical Scope Referenced Data (P.L.S.R.D.)
- 'Backpack'
- 'Closure'
The 'backpack' (or 'closure') of live data is attached to `incrementCounter` (then to `myNewFunction`) through a hidden property known as `[[scope]]` which persists when the inner function is returned out. 
### Multiple Closure Instances 
```js
function outer() {
	let counter = 0
	function incrementCounter() { counter++ }
	return incrementCounter
}

const myNewFunction = outer()
myNewFunction() // counter = 1
myNewFunction() // counter = 2

const anotherFunction = outer()
anotherFunction() // counter = 1, this is a different counter 
anotherFunction() // counter = 2, in a different backpack (closure)
```
