Why Functions? DRY (Don't repeat yourself)
### Higher Order Functions 
Any function that takes in a function or passes out a function
```js
function copyArrayAndManipulate(array, instructions) {
	const output = []
	for (let i=0; i<array.length; i++) {
		output.push(instructions(array[i]))
	}
	return output
}

function multiplyBy2(input) { return input * 2 }
const result = copyArrayAndManipulate([1, 2, 3], multiplyBy2)
```
In this case, 
`copyArrayAndManipulate` is our Higher Order Function 
`multiplyBy2` is our Callback function 
![[Functions - Higher Order Function.png]]
We have actually built our own version of `map` function. 
### Arrow Functions
Introduced in ES6 
