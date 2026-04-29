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

## 2. Sliding Window

Sliding window is a powerful problem-solving pattern where you use **two pointers** to define a “window” and slide them over a data structure, typically an array or a string to find subarrays or substrings that meet a certain requirement.

The power comes from **incremental updates**. When sliding from one position to the next:
- We **lose one** element (the one leaving the window on the left)
- We **gain one** element (the one entering the window on the right)
- Everything else stays the same

```
[1, 2, 3, 4, 5]
 ^     ^
 L     R

[1, 2, 3, 4, 5]
    ^     ^
    L     R

[1, 2, 3, 4, 5]
       ^     ^
       L     R
```

Brute force
```
Window [0, 2]: sum = nums[0] + nums[1] + nums[2]
Window [1, 3]: sum = nums[1] + nums[2] + nums[3]  // Recalculates nums[1], nums[2]
Window [2, 4]: sum = nums[2] + nums[3] + nums[4]  // Recalculates nums[2], nums[3]
```

Using sliding window
```
Window [0, 2]: sum = nums[0] + nums[1] + nums[2]
Window [1, 3]: sum = previous_sum - nums[0] + nums[3]  // O(1) update!
Window [2, 4]: sum = previous_sum - nums[1] + nums[4]  // O(1) update!
```

### Variable Size (Dynamic) Window

Instead of keeping the window size static, the window size changes throughout iteration by using two pointers, left and right, where **right expands** the window and **left contracts** it.

The general pattern is: expand until a condition is **violated**, then shrink until the condition is **restored**.

### When To Use

## 3. Fast & Slow Pointers

The fast and slow pointer (a.k.a. "tortoise and hare" a.k.a "Floyd's Algorithm") is a **two-pointer** technique where you move two pointers through a structure (often a linked list) at different speeds to reveal patterns you can’t see with a single pass.
- **Slow pointer** → moves 1 step at a time
- **Fast pointer** → moves 2 (or more) steps at a time

You can use this pattern to
- Detect cycles
- Find the start of a cycle
- Find the middle of a linked list

### Visualization

In this example, this pattern is used to find the start of a cycle

<img src="../assets/fast_and_slow_pointers.webp" alt="fast and slow pointers" height="400" />

Think of a race track:
- If there’s **no loop** → fast runs off the track (hits None)
- If there is a **loop** → fast eventually laps slow → collision

### Finding the Middle

```python
def find_middle(head):
    slow = head
    fast = head

    # Move until fast reaches the end
    while fast is not None and fast.next is not None:
        slow = slow.next          # move slow by 1
        fast = fast.next.next     # move fast by 2

    return slow  # slow is at the middle
```

### Cycle Detection

```python
def has_cycle(head) -> bool:
    slow = head
    fast = head

    while fast is not None and fast.next is not None:
        slow = slow.next
        fast = fast.next.next

        # If they meet, there's a cycle
        if slow is fast:
            return True

    # Fast reached the end, no cycle
    return False
```

### Finding Cycle Start

```python
def find_cycle_start(head):
    slow = head
    fast = head

    # Phase 1: detect cycle and find meeting point
    while fast is not None and fast.next is not None:
        slow = slow.next
        fast = fast.next.next

        if slow is fast:
            # Phase 2: find cycle start
            pointer = head
            while pointer is not slow:
                pointer = pointer.next
                slow = slow.next
            return slow  # cycle start

    return None  # no cycle
```

### Key Insights

The beauty of this pattern lies in how efficiently it solves these type of problems. It only uses O(n) time and O(1) space complexity, which means it's both fast and memory-efficient.

- For example, finding the start of a cycle, you could tranverse a linked list with a single pointer, hashing node values by saving them to a `Set`, and detecting if any encountered node is already in the set. This results in O(n) time AND space complexity

### When To Use

## 1. Bit Manipulation

### The 6 Bitwise Operators

#### 1. AND (`&`)

Returns `1` only if both bits are `1`.

```
  5 = 0101
& 3 = 0011
-----------
  1 = 0001
```

**Use case**: Check if a specific bit is set, clear bits, extract bits.

#### 2. OR (`|`)

Returns `1` if at least one bit is `1`.

```
  5 = 0101
| 3 = 0011
-----------
  7 = 0111
```

**Use case**: Set specific bits to 1.

#### 3. XOR (`^`)

Returns `1` if the bits are different.

```
  5 = 0101
^ 3 = 0011
-----------
  6 = 0110
```

**Use case**: Toggle bits, find unique elements, swap values.

**Key property**: `a ^ a = 0` and `a ^ 0 = a`

#### 4. NOT (`~`)

Flips all bits (`0` becomes `1`, `1` becomes `0`).

```
 ~5 = ~0101
-----------
    = 1010  (in a larger bit representation, this gives -6)
```

**Note**: In most languages, `~n = -(n + 1)` due to two's complement representation. Negative numbers are represented using two's complement: `-n = ~n + 1`

#### 5. Left Shift (`<<`)

Shifts bits to the left by specified positions. Each shift multiplies by 2.

```
5 << 1:
  0101 << 1
= 1010
= 10
```

**Formula**: `n << k = n × 2^k`

#### 6. Right Shift (`>>`)

Shifts bits to the right by specified positions. Each shift divides by 2 (integer division).

```
5 >> 1:
  0101 >> 1
= 0010
= 2
```

**Formula**: `n >> k = n / 2^k` (integer division)

### Common Techniques

#### Bit Masking

- `1 << k` creates a number with only the k-th bit set and `n & (1 << k)` isolates that bit (so, if that bit was set, the entire binary has one bit, otherwise it has no bits)

Example:

```
n      = 101101
mask   = 000100   (1 << 2)
------------------------
n & mask = 000100   ← isolates that bit
```

## 2. Greedy Algorithms

Greedy algorithms are a class of algorithms that make locally optimal choices at each step with the hope of finding a global optimum solution.

<img src="../assets/greedy_algorithm.png" alt="greedy algorithms" width="1000" height="180" />

The key characteristics of greedy algorithms:

1. **Makes one choice at a time**: At each step, select the option that looks best right now
2. **Never reconsiders**: Once a choice is made, it is final
3. **Builds solution incrementally**: Each choice extends the partial solution
4. **Local optimization**: Each step is locally optimal, not necessarily globally optimal

Important: when choosing a greedy algorith, you have to choose the right **greedy criteria** - how you're selecting the most optimal choice at every step

Here's how it works:
1. Identify the decision being made - greedy problems usually ask you to repeatedly make a local choice. So, ask yourself, "At each step, what am I choosing?"
2. Determinine the minimum state needed - greedy usually does not need full history. Track only what affects the next choice.
3. Consider all the options available at that specific moment.
4. Choose the option that seems best at that moment (local choice), regardless of future consequences. This is the "greedy" part - you take the best option available now, even if it might not be the best in the long run.
5. Move to the new state based on your chosen option. This becomes your new starting point for the next iteration.
6. Repeat steps 3-5 until you reach the goal state or no further progress is possible.

Advice: start off by sorting the input around the **greedy criteria** choice - most greedy problems become clear after sorting.

### Common Mistakes

#### Mistake 1: Assuming Greedy Works Without Proof

Just because a problem looks like it should be greedy does not mean it is. Always verify with counterexamples.

Before committing to greedy in an interview, think: "Can I construct a case where the greedy choice leads to a suboptimal solution?"

#### Mistake 2: Wrong Greedy Criterion

Choosing the wrong sorting or selection criterion leads to incorrect results.

#### Mistake 3: Greedy for Counting Problems

If the problem asks "how many ways" or "count all solutions," greedy usually does not apply. These typically need DP or backtracking.

### When To Use

## 3. Binary Search

Why O(log n)? With each comparison, binary search eliminates half the remaining elements. If you start with n elements:

- After 1 comparison: n/2 elements remain
- After 2 comparisons: n/4 elements remain
- After k comparisons: n/2^k elements remain
- We stop when only 1 element remains: n/2^k = 1, which gives k = log₂(n).

### When To Use

## 4. Cyclic Sort

The `cycle sort` algorithm is an in-place sorting algorithm. This means that no external data structure (such as a `list` or `heap`) is required to perform the `cycle sort` operation.

The underlying assumption for the `cycle sort` algorithm is that an unsorted list is similar to a graph, where nodes are connected with edges. We can assume that a relationship between nodes `A` and `B` exists if, in order to sort the array, the element present at node `A` should be at the index of node `B` when rotated.

**This is the big idea:**

Given an element `a`, we can find the index at which it will occur in the sorted list by simply counting the number of elements in the entire list that are smaller than `a`.

Take this array for example - [40, 10, 30, 20]

At index 2, we have the value 30. We need to ask, how many numbers are smaller than 30? They are values 10 and 20, therefore, 2 values are smaller than 30. Therefore, the value 30 belongs at index 2.

When values are constrained to a fixed range, like `1 to n`, then the indexing can be simplified to:

```
correct index = value - range_start

if range is 1 to n, then

correct index = value - 1
```

### Complexity

Time: O(n)
Space: O(1)

### Code Template

```python
i = 0

while i < len(nums):
    correct = nums[i] - 1

    if nums[i] != nums[correct]:
        nums[i], nums[correct] = nums[correct], nums[i]
    else:
        i += 1
```

### Example

```
nums = [8, 3, 5, 2, 4, 6, 1, 7]
fixed range: 1-8
```

Step 1:

```python
i = 0
nums[i] = 8
correct index = 7

[7, 3, 5, 2, 4, 6, 1, 8]
```

Step 2:

```python
i = 0
nums[i] = 7
correct index = 6

[1, 3, 5, 2, 4, 6, 7, 8]
```

Step 3:

```python
i = 1
nums[i] = 3
correct index = 2

[1, 5, 3, 2, 4, 6, 7, 8]
```

Step 4:

```python
i = 1
nums[i] = 5
correct index = 4

[1, 4, 3, 2, 5, 6, 7, 8]
```

Step 5:

```python
i = 1
nums[i] = 4
correct index = 3

[1, 2, 3, 4, 5, 6, 7, 8]
```

### When To Use

## 5. Intervals (Overlapping / Merge)
## 6. Monotonic Stack
## 7. Top K Elements
## 8. Two Heaps
## 9. K-way Merge
## 10. Binary Tree Traversal
## 11. Matrix Traversal
## 12. Depth-First Search (DFS)
## 13. Breadth-First Search (BFS)
## 14. Topological Sort
## 15. In-place Linked List Reversal
## 16. Subsets
## 17. Backtracking
## 18. Trie (Prefix Tree)
## 19. Dynamic Programming
## 20. 0/1 Knapsack