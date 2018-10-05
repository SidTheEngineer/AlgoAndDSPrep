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