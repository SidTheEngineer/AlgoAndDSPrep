## Backtracking

#### Example Problems
[Combination Sum](https://leetcode.com/problems/combination-sum/description/)

#### How to indentify

We know we're probably looking at a backtracking problem when we need to construct a **set/list/combination** of all "ways" to construct some solution. Examples of this include generating the power set of a set, permutations of some string, etc. Take a look at the overall pattern for a lot of backtracking problems with the (roughly) solution code to Combination Sum below:

```Java

public List<List<Integer>> combinationSum(int[] candidates, int target) {
    ArrayList<ArrayList<Integer>> solutionSet = new ArrayList<>();
    helper(new ArrayList<Integer>(), solutionSet, Arrays.asList(candidates), 0, target);
    return solutionSet;
}

public void helper(List<Integer> currentSolution, List<List<Integer>> solutionSet, List<Integer> input, int index, int target) {
    if (target < 0) {
        return;
    }
    if (target == 0) {
        solutionSet.add(currentSolution);
        return;
    }
    for (int i = index; i < input.length; i++) {
        currentSolution.add(input[i]);
        recurse(currentSolution, solutionSet, input, index, target - input[i]);
    }
}

```

## Dynamic Programming

#### Example Problems
 - [House Robber](https://leetcode.com/problems/house-robber/description/)
 - [Minimum Path Distance]()

#### How to identify
We know we're probably looking at a problem that lends itself to an optimal dynamic programming solution when the probelm can be divided into overlapping subproblems that can be solved independently. There are two uses for dynamic programming:

1. Finding an optimal solution: We need to find a solution that is as large or as small as possible.
2. Counting the number of solutions: We need to calculate the total number of possible solutions.

Take a look at the (rough) solution to the House Robber problem below. Because we know that we can make two choices at each step towards our solution, we'll need a 2D array where one index of the array represents not choosing and the other choosing:

```Java
public int rob(int[] houses) {
    int[][] dp = new int[houses.length + 1][2];
    for (int i = 1; i <= houses.length; i++) {

        // Not choosing is going to be the max of previously not choosing and previously choosing
        dp[i][0] = Math.max(dp[i - 1][0], dp[i - 1][1]);

        // Choosing is going to be the sum of the current house we're choosing and previously not choosing
        dp[i][1] = nums[i - 1] + dp[i - 1][0];
    }

    return Math.max(dp[houses.length][0], dp[houses.length][1]);
}
```

Additionally, the minimum path distance problem lends itself to a dynamic programming solution as well. We know that we have to take some "steps" to a solution, and these overlapping steps starting with the first is how we will get there. The first "step" we need to take in our algorithm exists at `grid[0][0]`

```Java
public int minPathSum(int[][] grid) {
    for (int y = 0; y < grid.length; y++) {
        for (int x = 0; x < grid[0].length; x++) {
            // Here is the first step (this is essentially doing grid[y][x] = grid[y][x])
            if (x == 0 && y == 0) continue;
            if (x == 0) {
                grid[y][x] = grid[y-1][x] + grid[y][x];
            } else if (y == 0) {
                grid[y][x] = grid[y][x-1] + grid[y][x];
            } else {
                grid[y][x] = Math.min(grid[y-1][x], grid[y][x-1]) + grid[y][x];
            }
        }
    }
    
    return grid[grid.length-1][grid[0].length - 1];
}
```

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

