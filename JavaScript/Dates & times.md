```js
const today = new Date();
console.log(today.toDateString());
// "Sun Apr 07 2024"
console.log(today.toLocaleDateString());
// "4/7/2024"
console.log(Date.now());
// 1712512483569
```
### console.time
```js
console.time('stopwatch');
runAround();
console.timeLog('stopwatch');
// stopwatch: 17293ms 
```
### Timeouts
```js
console.log('prints immediately')
setTimeout(() => console.log('print >1 second later'), 1000)
console.log('prints immediately?')
```
### Intervals
```js
const traveling = setInterval(() => {
	console.log('Are you there yet?')
}, 1000)
```
