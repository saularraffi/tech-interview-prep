# DSA Patterns

Data Structures
- Array
- Linked List
- Stack
- Queue
- Heap
- Tree
- Trie
- Graph
- Hash Table
- Set
- Map

## 1. Prefix Sum

At its core, prefix sum is about **precomputing cumulative information** so you can answer range queries in O(1) instead of O(n).

Let's say you have array [0, 1, 2, 3, 4, 5]

You want to be able to compute a range sum (ex. sum of numbers from index 1 to index 3 -> `sum(1,3) = 1 + 2 + 3 = 6`). 

```
sum(0,5) = p[0] + p[1] + p[2] + p[3] + p[4] = 0 + 1 + 2 + 3 + 4 = 10
sum(1,4) = p[1] + p[2] + p[3] + p[4] = 1 + 2 + 3 + 4 = 10
sum(2,4) = p[2] + p[3] + p[4] = 2 + 3 + 4 = 9
sum(left, right) = p[left] + ... + p[right]
```

See how we keep recomputing the same things. The sum from index 0 up until index `right` is always the same. Therefore, we can create an array of precomputed sums, where the sum at each index `right` is `sum(0, right)`.

```
a = [0, 1, 2, 3, 4, 5]
p = [0, 1, 3, 6, 10, 15]
```

We now can determine the sum from 0 to any variable right idex `right`. But, we can also compute from any variable left index `left` by discarding the left adjacent sum:

```
sum(2,4) = p[right] - p[left - 1] = p[4] - p[1] = 10 - 1 = 9
```

### Build Prefix Sum

```python
def build_prefix_sum(nums):
    prefix = [0] * len(nums)
    prefix[0] = nums[0]

    for i in range(1, len(nums)):
        prefix[i] = prefix[i - 1] + nums[i]

    return prefix
```

### Query Range Sum

```python
def range_sum(prefix, left, right):
    if left == 0:
        return prefix[right]
    return prefix[right] - prefix[left - 1]
```

### Key Insights

Prefix sum is not just about sums - it’s about **transforming problems into cumulative relationships**

Edge case: When left = 0, there is no `prefix[left - 1]`. In this case, `sum(0, right) = prefix[right]`.

### When To Use

Prefix sum is the right tool when you see these patterns:

1. **Multiple range sum queries on a static array**: If the array does not change and you need to answer many range sum queries, preprocessing with prefix sum is almost always the right approach.
2. **Counting subarrays with a specific sum**: Problems like "find subarrays that sum to k" become tractable with prefix sums combined with a hash map.
3. **Finding equilibrium points or balance conditions**: When you need to compare sums of left and right portions of an array.
4. **2D grid problems involving rectangular sums**: Prefix sums extend naturally to 2D for calculating sums of any rectangular region.

| Problem Type                 | Examples                                                                 |
|------------------------------|--------------------------------------------------------------------------|
| Range sum queries            | Range Sum Query - Immutable, Range Sum Query 2D                          |
| Subarray sum equals target   | Subarray Sum Equals K, Continuous Subarray Sum                           |
| Subarray divisibility        | Subarray Sums Divisible by K                                             |
| Product-based queries        | Product of Array Except Self (uses prefix products)                      |
| Equilibrium problems         | Find Pivot Index, Partition Array Into Three Parts                       |
| Grid problems                | Matrix Block Sum, Maximal Square                                         |

## 2. Sliding Window
## 3. Fast & Slow Pointers
## 4. In-place Linked List Reversal
## 5. Monotonic Stack
## 6. Top K Elements
## 7. Overlapping Intervals / Merge Intervals
## 8. Modified Binary Search
## 9. Binary Search
## 10. Binary Tree Traversal
## 11. Depth-First Search (DFS)
## 12. Breadth-First Search (BFS)
## 13. Matrix Traversal
## 14. Backtracking
## 15. Dynamic Programming
## 16. Greedy Algorithms
## 17. Topological Sort
## 18. Trie (Prefix Tree)
## 19. Cyclic Sort
## 20. Two Heaps
## 21. Subsets
## 22. Bitwise XOR
## 23. K-way Merge
## 24. 0/1 Knapsack