# Search Algorithms

## Intro to Linear Search
- Given an array, the simplest way to search for a value is to look at every element in the array and check if it's the value we want
- javascript methods: **includes, indexOf, find, findIndex** are linear searches

```javascript
const linearSearch = (arr, val) => {
    for (let i = 0; i < arr.length; i++){
        if (arr[i] === val) return i;
    }
    return -1;
}
```

### Linear Search Big O
- Best case: O(1) 
- Average case: O(n)
- Worst case: O(n)

## Intro to Binary Search
- Much faster than Linear via Divide and conquer
- Rather than eliminating one element at a time, you can eliminate half of the remaining elements at a time
- However, only works on sorted array 

```javascript
// Psuedo
function binarySearch(arr, elem)
	variable start
	variable end
	variable middle
	
	while arr[middle] !== elem and start <= end
		if elem greater than arr[middle]
			start = middle + 1
		elem less than arr[middle] (else)
			end = middle - 1
		RESET middle
	
	if arr[middle] === elem then return middle

	return -1 // means not found
```

```javascript
function binarySearch(arr, elem){
  let start = 0;
  let end = arr.length - 1;
  let middle = Math.floor((start + end)/2);

  while (arr[middle] !== elem && start <= end){
    if(elem < arr[middle]){
      end = middle - 1;
    } else {
      start = middle + 1;
    }
    middle = Math.floor((start + end)/2);
  }

  if (arr[middle] === elem){
    return middle;
  }
  return -1;
}
```
## Binary Search Big O
- Best case: O(1) 
- Average case: O(log n)
- Worst case: O(log n)