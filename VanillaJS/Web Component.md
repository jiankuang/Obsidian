![[WebComponent.png]]
A modular, reusable building block for web development that encapsulates a set of related functionality and user interface elements. 
In short, your own custom HTML tag element. 
* Compatible with every browser 
* It's actually a set of standards: 
	* Custom Elements 
	* HTML Templates 
	* Shadow DOM 
	* Declarative Shadow DOM (new)
* It's similar to the idea of components on most of the libraries for JavaScript 
* We have freedom of choice on how to define them and use them 
### Custom Element 
A way to define new, reusable HTML elements with custom behavior and functionality using JavaScript. 
We can define our own HTML tags using the custom Elements API 
```js
class MyElement extends HTMLElement {
	constructor() {           // Set up initial state, event listeners, etc. 
		super()
		this.dataset.language
	}
	// Custome Elements Lifecycle
	connectedCallback() {}    // The element is added to the document 
	disconnectedCallback() {} // The element is removed from the document 
	adoptedCallback() {}      // The element has been moved to a new document 

	attributeChangedCallback(name, oldValue, newValue) {}
}

customElements.define("my-element", MyElement)
```

```html
<body>
	<!-- We can define our own custom attributes using the `data-*` spec. -->
	<my-element data-language="en"> 
		<!-- Custom Elements with Slots -->
		<!-- The slot is the content that we can define as the component's children. With templates we can have more than one slot. -->
		<div>
			<h2>Slot of My Element</h2>
		</div>
	</my-element>
</body>

<script>
document.createElement("my-element")
</script>
```

**WARNING**
The HTML tag we define must contain a hyphen (-) to assure future compatibility
#### Where to define HTML for a Custom Element
There are several alternatives
* Use DOM APIs (createElement)
* Use a `<template>` in the main HTML
* Use an external HTML file loaded with fetch (it can be prefetched)
	* Using `innerHTML` 
	* Using `DOMparser` (Here is a link to MDN's [documentation on DOMParser](https://developer.mozilla.org/en-US/docs/Web/API/DOMParser))
#### Where to define CSS for a Custom Element
There are several alternatives 
* Use CSSOM APIs
* Add a `<script>` to a `<template>`
* Add a `<link>` in the `<template>`
* Use an external CSS file loaded with fetch (it can be prefetched) and injected in the Shadow DOM as a `<style>`
### HTML Templates
#### Template Element
Fragments of markup that can be cloned and inserted into the document at runtime, with reusable HTML content that can be rendered and modified dynamically. 
It allow us to define HTML content that is not going to be parsed by the browser and it's going to be available for usage only if we clone it. 
```html
<template id="template1">
	<style>
		/* this declaration also changes h1s outside of the custom element */
		h1 {color: red;}
	</style>
	<header>
		<h1>This is a template</h1>
		<p>This content is not rendered initially</p>
	</header>
</template>
```
#### Template Element Cloning 
We clone the template and we append it as a child; typically in `conntectedCallback` method of the Custom Element.
```js
connectedCallback() {
	const template = document.getElementById("template1")
	const content = template.content.cloneNode(true)
	this.appendChild(content)
}
```
### Shadow DOM 
A private, isolated DOM tree within a web component that is separate from the main document's DOM tree. 
* Allows more control over styling and encapsulation of functionality of a Custom Element. 
* By default, CSS declared in the main DOM won't be applied to the Shadow DOM. 
* CSS declared in the Shadow DOM applies only on there. 
* There are new pseudo-classes and pseudo-element to allow communication between DOMs in stylesheets. 
* It can be opened or closed defining visibility from the outer DOM. 
We have to create a Shadow DOM manually in our Custom Element, typically in the constructor and we save it. 
```js
class MyElement extends HTMLElement {
	constructor() {
		super()
		this.root = this.attachShadow({mode: "open"})
	}
	connectedCallback() {
		this.root.appendChild(...)
	}
}
```
#### Declarative Shadow DOM 
A way to define Shadow DOM directly in HTML markup using a new set of attributes and tags. 
**Warning**: Browser compatibility (the feature just arrived to Safari) 


