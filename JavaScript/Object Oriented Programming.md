Object Oriented Programming 
```js
const config = { paradigm: "imperative" };
const program = new Program(config);
program.run = (args) => {
	console.log(`programming ${paradigm}ly`);
}
const output = program.run();
```