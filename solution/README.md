# Solution 

```js
// Bucket sort is a distribution sort. It works by distributing elements into 'buckets' and then sorting these buckets individually.
// After sorting, the buckets are combined to form the sorted array.
// This implementation uses insertion sort to sort the elements within each bucket.

// Bucket sort is very fast because it distributes elements into buckets strategically based on their values.
// This, however, means it uses more memory for the sake of speed.

function bucketSort(array, bucketSize) {
  if (array.length === 0) {
    return array;
  }

  // Step 1: Determine the minimum and maximum values in the array
  let minValue = array[0];
  let maxValue = array[0];
  for (let i = 1; i < array.length; i++) {
    if (array[i] < minValue) {
      minValue = array[i];
    } else if (array[i] > maxValue) {
      maxValue = array[i];
    }
  }

  // Step 2: Initialize buckets
  // Default bucket size can be adjusted
  bucketSize = bucketSize || 5;
  let bucketCount = Math.floor((maxValue - minValue) / bucketSize) + 1;
  let buckets = new Array(bucketCount).fill(null).map(() => []);

  // Step 3: Distribute input array values into buckets
  for (let i = 0; i < array.length; i++) {
    let bucketIndex = Math.floor((array[i] - minValue) / bucketSize);
    buckets[bucketIndex].push(array[i]);
  }

  // Step 4: Sort each bucket and place back into the array
  array.length = 0;
  for (let i = 0; i < buckets.length; i++) {
    insertionSort(buckets[i]);  // Use insertion sort to sort individual buckets
    array.push(...buckets[i]);  // Concatenate sorted buckets back into the array
  }

  return array;
}

// Helper function: Insertion Sort
function insertionSort(array) {
  for (let i = 1; i < array.length; i++) {
    let currentValue = array[i];
    let j;
    for (j = i - 1; j >= 0 && array[j] > currentValue; j--) {
      array[j + 1] = array[j];
    }
    array[j + 1] = currentValue;
  }
  return array;
}

module.exports = bucketSort;
```