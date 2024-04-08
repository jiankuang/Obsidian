`.map()` only works on Array and its descendants 
but 
`for ... of` works on any iterable object 
### What makes an object "iterable" ? 
An iterable object has an `@@iterator` method, i.e.:
* the object has a `[Symbol.iterator]` property
* the value of that property is a function which returns an `iterator` object 
### What makes an object an "iterator" ? 
* Has a `.next()` method 
* `.next()` returns an object of shape `{ done, value }`
### [[Generators]]
Qualify as both an `iterator` and an `iterable`
