Document Object Model 
### HTML Elements 
```js
document
document.getElementById('my-id')
document.querySelectorAll('#my-id')
document.documentElement // HTML of the whole document (page)
```
### Attributes 
```js
element.getAttribute("name")
element.setAttribute("name", "toggle")
```
#### Attribute presence vs. value 
```js
btn.getAttribute("disabled") // ""
btn.setAttribute("disabled", "false")
btn.hasAttribute("disabled") // true
btn.deleteAttribute("disabled")
```
### Event Handlers
```js
element.addEventListener('click', (e) => {
	console.log('you clicked on: ', e.target)
})
```
### window 
It's better to wait for the `DOMContentLoaded` event for DOM manipulation 
```js
window.addEventListener("DOMContentLoaded", () => {
	let nav = document.querySelector("nav")
	console.log(nav)
})
```
`load` event waits for everything in the page to be loaded. That means style sheets are loaded and parsed, images are loaded, web fonts are loaded, videos are loaded. 