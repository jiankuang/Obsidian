![[Queue.png]]

### Use Cases
* JavaScript engines have message queue that executes your code at runtime. 
### Implementation 
#### Using Array (Object)
```js
class Queue {
	constructor() {
		this._storage = {};
		this._length = 0;
		this._headIndex = 0;
	}
	enqueue(value) {
		// TODO: argument validation 
		this._storage[this._headIndex + this._length] = value;
		this._length++;
	}
	dequeue() {
		if(this._length) {
			const firstVal = this._storage[this.headIndex];
			delete this._storage[this._headIndex];
			this._length--;
			this._headIndex++;
			return firstVal;
		}
	}
	peek() {
		if(this._length) {
			return this._storage[this._headIndex];
		}
	}
}
```
#### Using Linked List
![[Queue - Using Linked List.png]]
```ts
type Node<T> {
	value: T,
	next?: Node<T>,
}

export default class Queue<T> {
	public length: number 
	private head?: Node<T>
	private tail?: Node<T>

	constructor() {
		this.head = this.tail = undefined
		this.length = 0
	}
	enqueue(item: T): void {
		const node = {value: item} as Node<T>
		this.length++
		if (!this.tail) {
			this.tail = this.head = node
			return
		}
		this.tail.next = node
		this.tail = node 
	}
	deque(): T | undefined {
		if(!this.head) {
			return undefined 
		}
		this.length--
		const head = this.head
		this.head = this.head.next 
		head.next = undefined // free 
		if (this.length === 0) {
			this.tail = undefined
		}
		return head.value
	}
	peek(): T | undefined {
		return this.head?.value
	}
}
```
