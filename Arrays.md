## Prefix Sum Array

Using a prefix sum array is a way we can quickly (O(n)) calculate sum queries on some static array. Essentially, we can create some new array that represents the sum of the values up to some particular point from the original array (a "range sum") in O(n) time. Below is an example:

```Java
int[] originalArray = new int[]{ 1, 2, 3, 4, 5, 6, 7 };

int sumArray = new int[originalArray.length;]
sumArray[0] = originalArray[0];

for (int i = 1; i < originalArray.length; i++) {
    sumArray[i] += sumArray[i - 1] + nums[i];
}

// sumArray = [1, 3, 6, 10, 15, 21, 28]
```
