# Generate Permutations

## Summary

This section explains an algorithm to generate all distinct permutations of an array. A permutation refers to a possible arrangement of elements in a set, and this algorithm ensures that all permutations are generated in sorted order.

---

## Problem Statement

Given an array of distinct integers, generate all possible permutations of the array such that:

1. Each permutation is a unique arrangement of elements from the input array.
2. The permutations are returned in sorted order.

This problem has wide-ranging applications in mathematics, combinatorics, and computer science. Generating permutations is essential for solving problems involving arrangements, ordering, and optimization.

### Visual Representation

For example, given the input array `[1, 2, 3]`, the possible permutations are:

```
[1, 2, 3], [1, 3, 2], [2, 1, 3], [2, 3, 1], [3, 1, 2], [3, 2, 1]
```

These permutations represent all possible arrangements of the input elements.

---

## Approach

The solution uses a backtracking algorithm to systematically explore all possible arrangements of the input array. At each step, the algorithm swaps elements to generate new permutations and recursively explores these arrangements.

### Steps

1. **Initialization**:

   - Define an empty array `P` to store all permutations.
   - Use a helper function `permute` to recursively generate permutations.

2. **Recursive Backtracking**:

   - If the current index (`low`) is equal to the last index (`high`), add the current arrangement to `P`.
   - Otherwise, for each index `i` from `low` to `high`:
     - Swap the element at index `low` with the element at index `i`.
     - Recursively call `permute` with the next index (`low + 1`).
     - Backtrack by swapping the elements back to their original positions.

3. **Return Result**:

   - After all recursive calls, return `P`, which contains all generated permutations.

### Pseudocode

```plaintext
function permutations(arr):
    initialize P as []

    function permute(arr, low, high):
        if low == high:
            add copy of arr to P
            return
        for i from low to high:
            swap(arr[low], arr[i])
            permute(arr, low + 1, high)
            swap(arr[low], arr[i])  // backtrack

    permute(arr, 0, arr.length - 1)
    return P
```

---

## Time Complexity

- **Worst Case**: `O(n * n!)`
  - There are `n!` permutations, and each permutation takes `O(n)` time to generate due to copying the array.

## Space Complexity

- **Worst Case**: `O(n)`
  - The recursion stack depth grows up to `n` levels for an array of size `n`.

---

## Applications

- Solving problems involving arrangements or orderings.
- Generating all possible test cases for a given input set.
- Solving optimization problems in machine learning and artificial intelligence.
- Exploring solution spaces in decision-making problems.

---

## Example Walkthrough

### Input

```javascript
permutations([1, 2, 3]);
```

### Process

1. Start with `[1, 2, 3]`.
2. Swap elements to generate new arrangements and recursively explore these arrangements:
   - Swap `1` with `1`: `[1, 2, 3]`.
   - Recursively generate permutations of `[2, 3]`.
     - Swap `2` with `2`: `[1, 2, 3]`.
     - Swap `2` with `3`: `[1, 3, 2]`.
   - Backtrack and swap `1` with `2`: `[2, 1, 3]`.
     - Recursively generate permutations of `[1, 3]`.
   - Continue exploring all paths.

### Output

```javascript
[
  [1, 2, 3],
  [1, 3, 2],
  [2, 1, 3],
  [2, 3, 1],
  [3, 1, 2],
  [3, 2, 1],
];
```

---

## Edge Cases

- **Empty Array**: Returns an empty array (`[]`).
- **Single Element**: Returns the array itself (`[[element]]`).
- **Duplicate Elements**: If duplicates are present, the function must be modified to handle them (not covered in this implementation).

---

## Limitations

- This implementation does not handle duplicate elements in the input array. A mechanism to ensure uniqueness is needed for arrays with duplicates.
- Performance may degrade for very large arrays, as the number of permutations grows factorially.

---

## Mathematical Insight

The total number of permutations of an array of size `n` is given by `n!` (factorial of `n`), which represents all possible arrangements of `n` distinct elements.

---

## Additional Notes

This backtracking algorithm ensures all permutations are explored efficiently without unnecessary computations. The recursive nature of the algorithm simplifies the implementation but requires careful handling of swaps and backtracking.

---

## Example Decision Tree

For the input `[1, 2, 3]`, the algorithm explores the following paths:

1. Start with `[1, 2, 3]`.
2. Swap `1` with `1`, then recursively permute `[2, 3]`.
3. Swap `2` with `2`, then recursively permute `[3]`.
4. Swap `3` with `3`, then backtrack and explore other paths by swapping.
5. Continue exploring paths by swapping elements at different indices.

This process generates all permutations systematically.
