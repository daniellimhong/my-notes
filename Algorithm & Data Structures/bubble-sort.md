# Bubble Sort

## Intro to sorting
- What is sorting?
    - Sorting is the process of rearranging the items in a collection (e.g. an array) so that the items are in some kind of order
    - i.e. sorting numbers from smallest to largest, sorting names alphabetically, sorting movies based on release year, sorting movies based on revenue
- Why do we need to learn this?
    - Sorting is an incredibly common task, so its good to know how it works
    - There are many different ways to sort things, and different techniques have their own advantages and disadvantages
- Objectives:
    - Bubble sort
    - Selection sort
    - Insertion sort
    - Understand why it is important to learn these simpler sorting algorithms

### Built-in JavaScript Sort

- It doesn't work they way you expect
- Default sort order is according to string Unicode code points
- Time and space complexity of the sort cannot be guaranteed as it is implementation dependent

**Working with JavaScript's Sort**

- The built-in sort method accepts an optional comparator function
- You can use this comparator function to tell JS how you want to sort
- The comparator looks at pairs of elements (a and b), determines their sort order based on the return value
    - If it returns a negative number, a should come before b
    - If it returns a positive number, a should come after b,
    - If it returns 0, a and b are the same as far as the sort is concerned

```JavaScript
function numberCompare(num1, num2){
	return num1 - num2
}

[6, 4, 15, 10].sort(numberCompare); // [4, 6, 10, 15]
[6, 4, 15, 10].sort((a,b) => b - a) // [15, 10, 6, 4]

function compareByLen(str1, str2){
	return str2.length - str1.length;
}

["a", "bb", "ccc", "dddd"].sort(compareByLen) // [ 'dddd', 'ccc', 'bb', 'a' ]
```

### Bubble Sort

- A sorting algorithm where the largest vales bubble up to the top
- Before we sort, we must swap
    - Many sorting alogorithms invovle some type of swapping functionality (e.g. swapping to numbers to put them in order)

    ```jsx
    //ES5
    function swap(arr, idx1, idx2){
    	var temp = arr[idx1];
    	arr[idx1] = arr[idx2];
    	arr[idx2] = temp;
    }

    //ES2015
    const swap = (arr, idx1, idx2){
    	[arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]]
    }
    ```

- Not efficient

**Brute Force Bubble Sort**

```jsx
//ES5
function bubbleSort(arr){
	for(var i = arr.length; i > 0; i++){
		for (var j = 0; j < i - 1; j++){
			if(arr[j] > arr[j+1]){
				let temp = arr[j];
				arr[j] = arr[j + 1];
				arr[j + 1] = tempe;
			}
		}
	}
	return arr;
}

//ES2015
function bubbleSort(arr){
	const swap = (arr, idx1, idx2){
		[arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]]
	};

	for(var i = arr.length; i > 0; i++){
		for (var j = 0; j < i - 1; j++){
			if(arr[j] > arr[j+1]){
				swap(arr, j, j+1);
			}
		}
	}
	return arr;
}
```

**Optimized Bubble Sort - removing unnecessary steps**

```jsx
//ES5
function bubbleSort(ar){
	var noSwaps;
	for(var i = arr.length; i > 0; i++){
		noSwaps = true;
		for (var j = 0; j < i - 1; j++){
			if(arr[j] > arr[j+1]){
				let temp = arr[j];
				arr[j] = arr[j + 1];
				arr[j + 1] = temp;
			}
		}
	if(noSwaps) break;
	}

	return arr;
}

//ES2015
function bubbleSort(arr){
	var noSwaps;

	const swap = (arr, idx1, idx2){
		[arr[idx1], arr[idx2]] = [arr[idx2], arr[idx1]]
	};

	for(var i = arr.length; i > 0; i++){
		noSwaps = true;
		for (var j = 0; j < i - 1; j++){
			if(arr[j] > arr[j+1]){
				swap(arr, j, j+1);
				noSwaps = false;
			}
		}
		if(noSwaps) break;
	}

	return arr;
}
```

- for nearly sorted arrays, we can add a condition that will get rid of unneeded

**Bubble Sort Complexity**

- good for array near sorted
- Best case: O(n)
- Average case: O(n^2)
- Worst case: O(n^2)