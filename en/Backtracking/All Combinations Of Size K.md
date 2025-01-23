# All Combinations Of Size K

## Summary

This document explains an algorithm to generate all possible combinations of size `k` from a range `[1, n]`. The algorithm uses a backtracking approach to explore combinations systematically. It is efficient and handles edge cases such as `k = 0` or `n < k` gracefully.

---

## Problem Statement

The problem is to generate all possible combinations of size `k` from a range of integers `[1, n]`. A combination is defined as a subset of numbers selected from the range `[1, n]` such that:

1. Each combination contains exactly `k` unique integers.
2. The integers in each combination are sorted in ascending order.
3. The combinations themselves are output in lexicographical order.

The task requires implementing an efficient algorithm to systematically explore all possible combinations and return them in the required order. The algorithm must handle edge cases like:

- When `k = 0`, where the only valid combination is an empty set.
- When `n < k`, where it is impossible to generate combinations, resulting in an empty output.

This problem is fundamental in combinatorics and has applications in various fields like mathematics, software testing, and algorithmic problem-solving.

### Visual Representation

For example, if `n = 4` and `k = 2`, the possible combinations are:

```
1, 2   1, 3   1, 4   2, 3   2, 4   3, 4
```

These combinations are generated systematically in lexicographical order.

---

## Approach

The solution uses a backtracking algorithm to generate combinations. At each step, it decides whether to include or exclude the current number in the combination being formed. The process ensures all possible combinations of size `k` are explored systematically.

### Steps

1. **Initialization**:

   - `currentCombination`: An array to track the current combination being constructed.
   - `allCombinations`: An array to store all valid combinations.
   - `currentValue`: Tracks the current number being considered, starting at `1`.

2. **Recursive Backtracking**:

   - Include the `currentValue` in the combination and recursively build further combinations.
   - Exclude the `currentValue` and explore other possibilities.

3. **Base Cases**:

   - If the `currentCombination` reaches size `k`, add it to `allCombinations`.
   - If `currentValue` exceeds `n`, stop further recursion.

4. **Return Result**:
   - After recursion completes, return `allCombinations` containing all valid combinations.

### Pseudocode

```plaintext
function generateCombinations(n, k):
    initialize allCombinations as []
    initialize currentCombination as []

    function backtrack(currentValue):
        if currentCombination.length == k:
            add currentCombination.copy() to allCombinations
            return
        if currentValue > n:
            return

        // Include the current value
        currentCombination.append(currentValue)
        backtrack(currentValue + 1)
        currentCombination.pop()

        // Exclude the current value
        backtrack(currentValue + 1)

    backtrack(1)
    return allCombinations
```

---

## Time Complexity

- **Worst Case**: `O(k * C(n, k))`
  - `C(n, k)` is the number of combinations (binomial coefficient), and each combination requires copying an array of size `k`.

## Space Complexity

- **Worst Case**: `O(k)`
  - The `currentCombination` array grows up to size `k`.

---

## Applications

- Generating lottery combinations.
- Selecting team members from a pool of candidates.
- Forming unique subsets of items for combinatorial testing.
- Solving combinatorial problems in mathematics.
- Creating test cases for software testing.
- Enumerating subsets for machine learning or optimization problems.

---

## Example Walkthrough

### Input

```javascript
generateCombinations(4, 2);
```

### Process

1. Start with `currentValue = 1`.
2. Explore all combinations of size `2` by including or excluding numbers in the range `[1, 4]`.
3. Backtrack after reaching valid combinations to explore other possibilities.

### Detailed Steps

- Start with an empty combination `[]`.
- Add `1` → `[1]`, then add `2` → `[1, 2]` (valid combination).
- Backtrack, replace `2` with `3` → `[1, 3]` (valid combination).
- Backtrack, replace `3` with `4` → `[1, 4]` (valid combination).
- Backtrack fully, start with `2` → `[2]`, add `3` → `[2, 3]`.
- Backtrack, replace `3` with `4` → `[2, 4]`.
- Backtrack fully, start with `3` → `[3]`, add `4` → `[3, 4]`.

### Output

```javascript
[
  [1, 2],
  [1, 3],
  [1, 4],
  [2, 3],
  [2, 4],
  [3, 4],
];
```

---

## Edge Cases

- `n < k`: Returns an empty array (`[]`).
  - Explanation: It is impossible to form a combination when there are fewer elements than required.
- `k = 0`: Returns an array with an empty combination (`[[]]`).
  - Explanation: An empty combination is the only valid combination when no elements are required.

---

## Limitations

- Performance may degrade for very large values of `n` and `k`, as the number of combinations grows exponentially.
- Memory usage increases with larger values of `k` since `currentCombination` can grow up to size `k`.

---

## Mathematical Insight

The number of combinations is given by the binomial coefficient `C(n, k)`, which represents the number of ways to choose `k` items from a set of `n` items:

```
C(n, k) = n! / (k! * (n - k)!)
```

This explains the growth in time complexity as `n` and `k` increase.

---

## Additional Notes

The backtracking approach ensures all combinations are explored efficiently without unnecessary computations. The use of recursion allows the algorithm to dynamically build combinations and backtrack when needed.

---

## Example Decision Tree

For `n = 4` and `k = 2`, the algorithm explores the following paths:

1. Include `1`, then include `2` → `[1, 2]`.
2. Backtrack, include `3` → `[1, 3]`.
3. Backtrack, include `4` → `[1, 4]`.
4. Backtrack fully, include `2`, then `3` → `[2, 3]`.
5. Backtrack, include `4` → `[2, 4]`.
6. Backtrack fully, include `3`, then `4` → `[3, 4]`.

This process ensures all combinations are generated systematically.
