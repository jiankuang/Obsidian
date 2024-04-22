![[Stack.png]]

### Use Cases
* JavaScript engines have a call stack 
* When you hit 'undo' in your text editor or 'back' in your browser, you are using a stack
### Implementation
#### Using Array (Object)
```js
class Stack {
	constructor() {
		this._storage = {};
		this._length = 0;
	}
	push(value) {
		// TODO: add typechecking and check arguments 
		this._storage[this._length] = value;
		this._length++;
	}
	pop() {
		if (this._length) { 
			const lastVal = this._storage[this._length-1];
			delete this._storage[this._length-1]; 
			this._length--;
			return lastVal;
		}
	}
	peek() {
		if (this._length) { 
			return this._storage[this._length-1];
		}
	}
}
```
#### Using Linked List 
![[Stack - Using Linked List.png]]
```ts
type Node<T> = {
	value: T, 
	prev: Node<t>,
}
export default class Stack<T> {
	public length: number
	private head?: Node<T>

	constructor() {
		this.head = undefined
		this.length = 
	}
	push(item: T): void {
		const node = {value: item} as Node<T>

		this.length++
		if(!this.head) {
			this.head = node
			return
		}
		node.prev = this.head 
		this.head = node 
	}
	pop(): T | undefined {
		this.length = Math.max(0, this.length-1)
		if(this.length === 0) {
			const head = this.head
			this.head = undefined
			return head?.value 
		}

		const head = this.head as Node<T>
		this.head = head.prev
		return head.value
	}
	peek(): T | undefined {
		return this.head?.value
	}
}
```