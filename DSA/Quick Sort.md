```js
function quickSort(nums) {
	// base case, arrays of length 0 or 1 are sorted already
	if (nums.length <= 1) return nums;
	
	// last number is the pivot
	const pivot = nums[nums.length - 1];
	const left = [];
	const right = [];
	
	// sort all smaller numbers than the pivot into left
	// and all bigger numbers into right
	for (let i = 0; i < nums.length - 1; i++) {
		if (nums[i] < pivot) {
			left.push(nums[i]);
		} else {
			right.push(nums[i]);
		}
	}

	// call quick sort on left and right
	// concat all into one big array with pivot in the middle
	return [...quickSort(left), pivot, ...quickSort(right)];
}
```