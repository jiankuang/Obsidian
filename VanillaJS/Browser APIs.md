### Media 
#### getUserMedia 
```js
const avStream = await navigator.mediaDevices.getUserMedia({
	audio: true, 
	video: true
})

const video = document.querySelector('video')
video.srcObject = avStream
await video.play()
```
