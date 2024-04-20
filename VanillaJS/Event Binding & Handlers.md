### Events 
Each DOM element has a list of possible events we can listen to 
* Basic: `load`, `click`, `dblclick`
* Value: `change`, typically with form elements 
* Keyboard Events: `keyup`, `keydown`, `keypress` 
* Mouse Events: `mouseover`, `mouseout`, etc. 
* Pointer and Touch Events
* Scroll, Focus and more APIs 
Some specific objects have special events: 
* `DOMContentLoaded` , `popstate` in `window`
Here's a link to check out [MDN's Event reference](https://developer.mozilla.org/en-US/docs/Web/Events)
```js
element.addEventListener('click', (e) => {
	console.log('you clicked on: ', e.target)
})
```
#### `window` object specific events 
##### `DOMContentLoaded`
It's better to wait for the `DOMContentLoaded` event for DOM manipulation 
```js
window.addEventListener("DOMContentLoaded", () => {
	let nav = document.querySelector("nav")
	console.log(nav)
})
```
`load` event waits for everything in the page to be loaded. That means style sheets are loaded and parsed, images are loaded, web fonts are loaded, videos are loaded. 
##### `popstate`
`popstate` won't be fired if the user clicks on an external link or changes the URL manually
### Advanced Event Handling 
```js
function eventHander(event) {}
const options = {
	once: true, // eventHandler will be fired only once 
	passive: true
}
element.addEventListener("load", eventHandler, options)
element.removeEventListener("load", eventHandler)
```
#### Dispatching Custom Events 
We can reuse the same system for our own custom events and messages 
```js
const event = new Event("mycustomname")
element.dispatchEvent(event)
```
