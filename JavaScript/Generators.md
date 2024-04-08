* Special functions declared with `function*` 
* Can pause execution with `yield` before a final stop with `return` 
* Qualify as both an `iterator` and an `iterable` 
* Make great values for `[Symbol.iterator]`

```js
function* dogerator() {
	yield 'so iterator'
	yield 'much generate'
	yield 'wow'
	return 
}
const meme = {
	[Symbol.iterator]: dogerator
}
for (let phrase of meme) {
	console.log(phrase)
}
```
