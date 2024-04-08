Fancy syntax for declaring custom object types (classes) 
```js
class ClassyMeme {
	// property declarations 
	fancy = true; 
	img;
	text; 

	// new instance constructor 
	constructor(img, text) {
		this.img = img; 
		this.text = text; 
	}

	// method 
	begPardon() {
		console.log('Do you have any Grey Poupon?);
	}
}

const fancyPooh = new ClassyMeme('fancyPooh.jpg', 'I am fancy');
fancyPooh.begPardon();
```

### Properties, Getters & Setters 
```js
class Meme {
	constructor(img, text) {
		this.img = img; 
		this.text = text; 
	}
	get imgType() {
		const [name, ext] = this.img.split('.');
		return ext;  
	} 
	set imgType(newExt) {
		const [name] = this.img.split('.');
		tihs.img = [name, newExt].join('.');
	}
}
```

```js
fancyPooh.img // 'fancyPooh.jpg'
fancyPooh.imgType // 'jpg'
fancyPooh.imgType = 'png'
fancyPooh.img // 'fancyPooh.png'
```

### Private properties/methods
```js
class Meme {
	#img; 
	constructor(img, text) {
		this.#img = img; 
		this.text = text; 
		this.#whisper();
	}
	get image() {
		return this.#img;
	}
	set image(newImage) {
		this.#img = newImage;
	}
	#whisper() {
		console.log('my secret img is', this.#img);
	}
	yell() {
		console.log('MY TEXT IS', this.text.toUpperCase());
	}
}
```

```js
const fancyPooh = new Meme('pooh.jpg', 'so fancy');
// my secret img is pooh.jpg

fancyPooh.img // undefined 
fancyPooh.#img // Error 

fancyPooh.image // 'pooh.jpg'
fancyPooh.image = 'otherPooh.jpg'

fancyPooh.#whisper() // Error 
fancyPooh.yell() // MY TEXT IS SO FANCY
```

### Class Inheritance 
```js
class GifMeme extends Meme {
	constructor(img, text) {
		if(!img.endsWith('.gif')) {
			throw new Error('Not a gif')
		}
		super(img, text)
	}
}

const failPooh = new GifMeme('pooh.jpg')
// Error: Not a gif 
const gitPooh = new GitMeme('pooh.gif')
// my secret img is pooh.gif 
gifPooh.image // pooh.gif
```