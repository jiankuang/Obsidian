### CommonJS Modules
Original Node module system, still around 
```js
const cowsay = require('cowsay');

module.exports = {
	mooove: () => cowsay.say({text: 'Get going'})
};
```
### ES Modules
ECMAScript Modules: The new(ish) hotness, supported by browsers too 
```js
import { say } from 'cowsay'

export const mooove = () => say({text: 'Get going'})
```
#### Using ES Modules 
in the browser
```html
<script type="module">
	// import away
</script>
```
in Node 
* Option 1: `.mjs` extension 
* Option 2: `"type": "module"` in `package.json`
