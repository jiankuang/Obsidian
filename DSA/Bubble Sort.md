

Runtime: O(n^2)

```ts
function bubble_sort(arr: number[]): void {
	for (let i=arr.length; i>0; i--) {
		let swrapped = false // we can break the outer loop when there is no swrap
		for (let j=0; j<i; j++) {
			if (arr[j]>arr[j+1]) {
				const temp = arr[j+1]
				arr[j+1] = arr[j]
				arr[j] = temp
				swrapped = true
			}
		}
		if (swrapped === false) break
	}
}
```