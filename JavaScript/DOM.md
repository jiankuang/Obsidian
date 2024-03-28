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
