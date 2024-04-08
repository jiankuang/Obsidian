Functional Programming, declarative, focus on "what"
```js
(function program({paradigm}) {
	return function run(args) {
		return `do stuff ${paradigm}ly`
	}
})({paradigm: "declarative"})()
```
### IIFE
Immediately Invoked Function Expression
```js
// Function Expression 
function bling(line) {
	console.log('one thing')
}
// Invoked function
bling('hotline')

// IIFE
(function bling(line) {
	console.log('one thing')
})()
```

