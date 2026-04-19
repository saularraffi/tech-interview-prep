# Data Structures & Algorithms Notes

## > Methodology

1. Understand the scenario and what the question is asking of you
2. Write down details of the question (unique information gives you hints to optimal solutions)
3. Determine any assumptions you may be making and ask the interviewer any clarifying questions
4. Illustrate the problem and start with a generic example with no special cases and of sufficient size (most provided examples are too small, by about 50%)
5. Start with the brute force approach. Come up with the algorithm (without actually implementing) and complexity.
6. Optimize your algorithm
   - Can I try to solve this problem **`intuitively`** and see what I come up with?
   - Can I find an optimal solution based on **`details/constraints`** given by the question?
   - Am I doing **`repetative work`** that can be avoided?
   - Are there **`data structures`** that are better to use than others? (array/string, stack, queue, hash table, tree, etc.)
   - What is the **`base case`**? Can I work up from there? (Dynamic programming)
   - Can I perform any **`precomputation`** on the input? Will sorting help me?
   - Can I **`manipulate the input`** to help me? (ex. changing values in an input array)
   - Can I implement **`two-pointer / multi-pointer traversal`**? Will the pointers move out-to-in or in-to-out?
   - Should I use **`recursion or iteration`**? Can I implement a decision tree (recursive)?
   - Can I implement **`BFS or DFS`**?
   - Are there **`time vs. space tradeoffs`** that can be made to make one or the other more efficient?
   - Can I **`simplify the input`** temporarily to make it easier to solve the problem?
   - Is there a **`different parameter for success`** I can look for?
7. Walk through the steps of your algorithm and make sure it works, conceptually
8. Implement the algorithm
9. Test your code
   1. Look through the code to make sure the code looks fine
   2. Walk through the code with an example input
   3. Focus on "hot spots" (parts of code that often cayse problem)
      - Base cases in recursive code
      - Integer division
      - Null nodes in binary trees
      - The start and end of iteration through a linked list
   4. Test edge cases

## > Recursive Algorithm Methodology

[YouTube - 5 Simple Steps for Solving Any Recursive Problem](https://www.youtube.com/watch?v=ngCos392W4w)

1. What's the simplest possible input?
2. Play around with examples and visualize
3. Relate hard cases to simpler cases
4. Generalize the pattern
5. Write code by combining recursive pattern with the base case(s)

## > Dynamic Programming Methodology

### Recursion

1. Determine your base case(s)
2. Determine how to get to the base case
3. Determine how the solution for n (whatever your current input is) can leverage the solution for n - 1 (whatever the reduced input is)
   - Visualize the problem as a tree
4. Make the solution efficient --> leverage memoization

### Tabulation

1. Visualize the problem as a table
2. Size the table based on the input(s) (may not necessarily be n, could be n + 1 for ex.)
3. Initialize the table with default values
   - Based on what the return value of the function will be
4. Seed the trivial answer into the table --> this is your base case
5. Iterate through the table, filling further positions in the table based on the current position

## > Questions To Ask Interviewer

- Does the input data structure contain any of the following?
  - Negative numbers?
  - Floating points?
  - Nulls?
  - Elements of different same data type?
- Is the input data structure valid?
  - If the input is a BST, is it guaranteed to be a valid BST?
  - If the input is a linked list, is it guaranteed to be a valid linked list?
  - Same with graph
- Can the input data structure be empty or null?
- Are there any duplicate elements in the input data structure?
- Is the input data structure sorted? in ascending or descending order?
- Can I manipulate the input data structure
- If the input is a tree, is it a Binary Tree or BST? is it a balanced tree?
  - If I'm given a tree and a node, is the node guaranteed to be in the tree?
- If linked list, is it a singly or doubly linked list?
- If graph, are there any loops? any self-loops?
- Should I optimize for space or time?
- How big is the size of the input? how big is the range of values?

## > Python Specific

### Strings and Arrays

- `array[i], array[j] = array[j], array[y]` --> swaps two values in array
- `elem1, elem2 = array[0], array[1]` --> in general you can assign 2 values at the same time
  - `val1, val2 = dict[key1], dict[key2]` --> works for dictionaries too
  - `x, y = 1, 2` --> even with just numbers
- `list(string)` --> turns string into array of chars and returns the array
  - `list(dict)` --> turns a dictionary into an array of keys and returns the array
  - `list(dict.values())` --> turns a dictionary into an array of the values and returns the array
- `"".join(array)` --> turn array of characters into string
- `str.split(del)` --> split string str by delimiter del into an array
- Dictionaries are ordered in python
- `list.reverse()` --> reverse an array, doesn't work on string
- `list[::-1]` --> reverse an array or string
- `string[start:end]` --> get substring from index start (inclusive) to index end (exclusive)
  - Also works for arrays
  - `array[:x]` --> from beginning to x (exclusive)
  - `array[x:]` --> from x (inclusive) to end
- `f"My name is {saular} and I am {25} years old"` --> this is an f string and it does the same things as the **.format()** method

### Hash Tables

- Sets are used to store multiple items in a single variable, ex. myset = {"apple", "banana", "cherry"}
- `set.add(x)` --> add an element to a set
- `mySet = set()` --> initialize empty set. If you try to do mySet = {}, then you initialize a dictionary
- `del dict[key]` --> delete a key from dictionary
- `dict.get(key, default)` --> returns the value of the key, if key does not exist then return default
- `set1.union(set2)` --> combines set1 and set2 and returns resulting set (duplicates are removed)
- `dict1.update(dict2)` --> combines dict1 and dict2 and assings resulting dict to dict1 (duplicates are removed)
- `mySet = {1,2,3} ... mySet.add(3)` --> attempting to add a value that is already in a set will not add it to the set
- `arrayToSet = set(array)` --> converts array to set and returns the result

### Iteration

- `for key, value in dict.items():` --> iterate over dictionary
- `for i in range(x, -1, -1)` --> iterate x times in reverse order
- `for i in reversed(array)` --> iterate over array in reverse
- `[0 for col in range(n)]` --> create an array of zeros with length n
- `[[0 for col in range(n)] for row in range(m)]` --> create an n by m sized matrix of zeros
- `for idx, val in enumerate(array)` --> allows you to loop over array and get both the value and the index, so now you can use this all the time rather than having to choose between the two types of for loops
- `for _ in range(x)` --> for when you don't need to access the variable in the for loop
- `array.copy()` --> returns a shallow copy of the array
  - `array[:]` --> returns the same thing, since the copy method may not work based on the python version

### Sorting

- `sorted(array, key=lambda x: x[0])` --> sort array by the first element of each sub array
- `sorted(array)` --> does the same thing as the sort() method but this returns the sorted array
  - `sorted(string)` --> takes in a string, splits up into array of characters, and sorts and returns the array of characters
- `array.sort(reverse=True)` sort an array in reverse order

### Math Operations

- `%` --> get remainder (ex. 10%3 = 1)
- If you take the modulo of a negative number, let's say -4%3, you get the number of 3's it takes to make -4 positive -> 2
- `//` --> round down division operator --> 5 / 3 = 2.5, but 5 // 3 = 2 --> eliminates need to cast to int
- `num**x` --> number to the power of x
- `num % biggerNum = num` --> ex. 8 % 10 = 8

### Heaps

- `heapq.heapify(array)` --> convert array into heap array
- `heapq.heappush(heap, element)` --> add element to heap
- `heapq.heappop(heap)` --> remove root of heap and return it

### Other

- `Ord(char)` --> returns the Unicode value of the character char
- The sort method on arrays has time complexity O(nlog(n))
- `x is not None` --> check if x is not null (can't do x not None)
- `if x is not None and ...` --> so if x is None, then the second part of the if statement won't execute. This is only the casing when ANDing
- in an if statement with an 'and' operator, both conditions execute. It's not that if the first is false, then the second won't execute
- `float("inf") and float("-inf")` --> infinity and negative infinity
- Only arrays, dictionaries, and sets are mutable in python
- When you pass a mutable datatype as an argument to python function, you can change its state within the function. If you pass an immutable datatype as an argument to a python function, you cannot change its state
  - If you pass in an object, you can change its object properties, but you cannot assign the object itself to a new instance
- `if type(x) is list` --> check if element is a list; can work with other data types
- `if x := 5 > 3` --> assign variable within conditional and use it
  - `if x := 5 and x > 3` --> this, however, is invalid because x in the second statement is not defined yet, you must tread **x := 5** as a variable

## > General Notes

**Remember - you are not developing your skill to code, you are developing your skill to find the simplest and most optimal solution**

- When determining the worst-case space complexity of an algorithm, you consider the maximum space that needed to be used throughout the algorithm. So, if 5 units of space are used on average but at a given point, n units of space are used, where n is the largest amount of space needed throughout the algorithm, then the space complexity is O(n).
- In most languages, concatenating to a string is O(n) operation, where n is the length of the string, whereas appending to a list is an O(1) operation. This is because when concatenating to a string, python iterated through the string and adds the element(s) to the end of it --> O(n) complexity
- A problem that gives you a sorted array is a good indication that the problem can be solved in linear time or at least with a time complexity that is better than the brute force approach
- Look into tail recursion
- When deleting from linked list, assign the node to be deleted to a variable and after the previous node points to the appropriate node, set the node to be deleted to None
- When going through a while loop with 2 pointers on the array, consider where you may be able to implement a nested while loop that keeps moving one of the pointers
- Depth of a tree is the length of its longest branch (number of edges)
- Remember that if you are implementing a recursive algorithm, depending on how it is implemented, you can return a value at the end (will execute once all func calls are over)
- When analyzing the complexity of an algorithm, if there are two separate loops and they are looping over sets of different lengths, then take both into account --> ex. algorithm loops over array1 (length n) then separately over array2 (length m), therefore time complexity is O(n + m)
- When analyzing the complexity of recursive tree-related algorithms, remember to consider the height of the tree.
- When implementing a recursive algorithm and there is information you need to store throughout the traversals, consider creating a class that holds the information you need and passing that object between function calls and then at the end, returning the desired attribute of the returning object. You can implement it the same exact way you would if you were using a dictionary.
- Breadth First Search --> use queue; Depth First Search --> use stack
  - Common theme for array based problems --> see what the result is up until that point, make a determination, continue
- 3-color depth first search --> to learn more, check out the **Cycle in Graph** problem
- The join operation to turn an array of strings into one string (ex. "".join(array)) has a time complexity of O(n)
- When you're planning on solving a problem recursively, at least know the benefits that an iterative solution would have offered --> easier to debug and no avoiding using up space on the call stack
- When implementing two pointer traversal, it's easier to move pointers from out to in rather than from in to out
- When you have multiple conditionals in an if statement, grouping statments into parentheses does matter
  - The statement `if False and False or True` is true, but the statement `if False and (False or True)` is false
    - This is because the first statement is interpreted as `if (False and True) or True` --> `if False or True`
- There are 3 basic ways to represent a graph in memory (objects and pointers, matrix, and adjacency list) --> familiarize yourself with each representation and its pros & cons
- In general, a graph traveral algorithm will have a time complexity of **O(V + E)**, where `V` is the number of verticies and `E` is the number of edges
  - This is because some graphs have more verticies than edges (like when some nodes have no edges to/from other nodes) and some graphs have more edges than verticies
- You likely may be given a dynamic programming problem during the Google on-site interview (based off of what that guy from AlgoExpert mock interview said)
- Two ways to think about dynamic programming problem or tell if a problem is based on dynamic programming
  - If you can think of the problem playing out like a tree
  - If the answer to the current input can be computed by leveraging the answer to one step down from that input
    - Ex. fibonacci calculation --> fib of 5 depends on fib of 4 and 4
- Many dynamic programming problem solutions share a similar vibe with the fibonacci implementation
  - And because of this, many can also leverage memoize (hash table)

## > LeetCode Problems To Come Back To

### these are problems that had valuable lessons, not necessarily problems that were just hard

39. Combination Sum
40. Number of Provinces (popular in Amazon)

## > Code Notes

- When performing a recursive algorithm to generate some BST, this is valid

  ```python
  def generateTree(self, bst, array):
      # BASE CASE(S)
      # SOME CODE

      # bst initially passed in as None
      bst = TreeNode(...) # TreeNode is the BST class with val, left, and right properties
      bst.left = self.generateTree(bst.left, ...)
      bst.right = self.generateTree(bst.right, ...)

      return bst

  ```

  - Because you first call the func with `bst` as `None`, then you set `bst` to be a node, then you call the function on its left child and right child. In those function calls, `bst` is `None` again, and when they return, they return those trees to `bst.left` and `bst.right`, respecively.

- Consider using an enum for more readable code

  ```python
  HOME_TEAM_WON = 1
  AWAY_TEAM_WON = 2
  GAME_IS_TIE = 3

  # SOME CODE

  if result == HOME_TEAM_WON:
      # SOME CODE
  elif result == AWAY_TEAM_WON:
      # SOME CODE
  else:
      # SOME CODE
  ```

- Binary search implemented

  ```python
  def binary_search(arr, target):
      start = 0
      end = len(arr) - 1

      # remember <= and NOT <
      while start <= end:
          mid = (end + start) // 2
          if arr[mid] < target:
              start = mid + 1 # remember set to mid + 1, not mid

          elif arr[mid] > target:
              end = mid - 1 # remember set to mid - 1, not mid

          else:
              return mid

      return -1
  ```

- Reverse an array in place

  ```python
  def reverseArrayInPlace(array):
      start = 0
      end = len(array) - 1
      while start < end:
          array[start], array[end] = array[end], array[start]
          start += 1
          end -= 1
  ```

- Notice how the caching system is implemented in the `nth fibonacci` recursive algorithm

  ```python
  def getNthFib(n, cache={1: 0, 2: 1}):
      if n in cache:
          return cache[n]
      else:
          # 0 1 1 2 3 5 8
          # when n = 3 --> cache[2] = fib(2) + fib(1) = 1 + 0 = 1
          # when n = 5 --> cached[5] = fib(4) + fib(3) = 2 + 1 = 3
          cache[n] = getNthFib(n - 1, cache) + getNthFib(n - 2, cache)
          return cache[n]
  ```

- Setting up a for loop with reverse indexing

  ```python
  s = 'hello'

  for i in reversed(range(len(s))):
      print('i={} char={}'.format(i, s[i]))

  # this is the same as
  for i in reversed([0,1,2,3,4]):
      ...

  # and same as
  for i in [4,3,2,1,0]:
      ...

  # output
  # i=4 char=o
  # i=3 char=l
  # i=2 char=l
  # i=1 char=e
  # i=0 char=h
  ```

- Example of using a class to manage data during a recursive algorithm

  ```python
  class TreeInfo:
      def __init__(self, nodeCount=0):
          self.nodeCount = nodeCount

  def getNodeCount(root):
      treeInfo = TreeInfo()
      getNodeCountHelper(root, treeInfo)
      return treeInfo.nodeCount

  def getNodeCountHelper(root, treeInfo):
      if root is None:
          return

      getNodeCountHelper(root.left, treeInfo)
      # working with TreeInfo
      treeInfo.nodeCount += 1 # <---
      getNodeCountHelper(root.right, treeInfo)
  ```

- Another example of using a class to manage data during a recursive algorithm
  - This is from the `Height Balanced Binary Tree` problem from AlgoExpert, in which you must return true if the input tree is balanced and false if it is not

  ```python
  class TreeInfo:
      def __init__(self, height, isBalanced):
          self.height = height
          self.isBalanced = isBalanced

  def heightBalancedBinaryTree(tree):
      return heightBalancedBinaryTreeHelper(tree).isBalanced

  def heightBalancedBinaryTreeHelper(tree):
      if tree is None:
          return TreeInfo(0, True)

      leftSubtreeInfo = heightBalancedBinaryTreeHelper(tree.left)
      rightSubtreeInfo = heightBalancedBinaryTreeHelper(tree.right)

      # notice multi-line conditional --> better readability
      isBalanced = (
          leftSubtreeInfo.isBalanced and
          rightSubtreeInfo.isBalanced and
          abs(leftSubtreeInfo.height - rightSubtreeInfo.height) <= 1
      )
      height = max(leftSubtreeInfo.height, rightSubtreeInfo.height) + 1

      return TreeInfo(height, isBalanced)
  ```

- A problem that has 2 scenarios --> ex. checking if array is monotonic (non-increasing or non-decreasing)

  ```python
  def isMonotonic(array):
      isNonDecreasing = True
      isNonIncreasing = True
      # you don't need to know whether to check fo non-increasing or non-decreasing
      # just attempt to disprove non-increasing and non-decreasing
      for i in range(1, len(array)):
          if array[i] < array[i - 1]:
              isNonDecreasing = False
          if array[i] < array[i - 1]:
              isNonIncreasing = False

      # if both disproven --> return False
      # if either were not disproven --> return True
      return isNonDecreasing or isNonIncreasing
  ```

- Creating a BST from an array without a helper function (for this example, assuming the array is sorted in ascending order)

  ```python
  def createTree(array):
      if len(array) == 0:
          return None

      mid = (len(array) - 1) // 2
      currentValue = array[mid]

      leftSubtree = createTree(array[:mid])
      rightSubtree = createTree(array[mid+1:])

      return TreeNode(currentValue, leftSubtree, rightSubtree)
  ```

- When a problem involves doing something to each level of a binary tree, consider an **iterative** algorithm using a **queue**
  - example, inverting a binary tree

  ```python
  def invertBinaryTree(tree):
      queue = [tree]
      # while queue is not empty
      while len(queue):
          current = queue.pop(0)
          if current is None:
              continue
          swapLeftAndRight(current)
          # queue allows for breadth first swapping
          # we don't move onto the next level until current level fully swapped
          queue.append(current.left)
          queue.append(current.right)

  def swapLeftAndRight(tree):
      tree.left, tree.right = tree.right, tree.left
  ```

- When passing an array to a recursive function, if you want the array to be exclusive to each call (rather than other function calls being able to manipulate the same array), then you must pass a **copy** of the array --> because remember, arrays are mutable and when you pass an array to a function, you are just passing a reference to that array, so the new function context is still working with the same array reference as the previous function context
  - This algorithm returns an array of all paths of a tree from its root to each of its lead nodes

  ```python
  # input
  #           2
  #         /   \
  #        1     3

  def getAllTreePaths(root):
      finalPaths = []
      getAllTreePathsHelper(root, [], finalPaths)
      return finalPaths

  def getAllTreePathsHelper(root, runningPath, finalPaths):
      if root is None:
          return

      runningPath.append(root.val)

      if root.left is None and root.right is None:
          finalPaths.append(runningPath)

      # see here that we are passing runningPath[:] to each function call, which passes a copy of runningPath
      getAllTreePathsHelper(root.left, runningPath[:], finalPaths)
      getAllTreePathsHelper(root.right, runningPath[:], finalPaths)

  # output
  # [[2, 1], [2, 3]]
  ```

  - This is what the output would be if the runningPath array itself, rather than a copy of it, was passed to each function call

  ```python
  # input
  #           2
  #         /   \
  #        1     3

  def getAllTreePaths(root):
      ...

  def getAllTreePathsHelper(root, runningPath, finalPaths):
      ...

      getAllTreePathsHelper(root.left, runningPath, finalPaths)
      getAllTreePathsHelper(root.right, runningPath, finalPaths)

  # output
  # [[2, 1, 3], [2, 1, 3]]
  ```

  - You can see that, because the same array was being manipulated throughout the function calls, the output subarrays are all the same
  - However, the last algorithm (with copying) is not space efficient, as a new array is being created with each function call. Instead of copying the array into each function call, you can just use the same array reference throughout and just pop off the last element before returning from the array

  ```python
  def getAllTreePaths(root):
      ...

  def getAllTreePathsHelper(root, runningPath, finalPaths):
      if root is None:
          return

      runningPath.append(root.val)

      if root.left is None and root.right is None:
          # we still need to append a copy of the array, otherwise all arrays in finalPath will be referencing the same array --> runningPath.pop() at the end of each function call will affect each array in finalPaths
          finalPaths.append(runningPath[:])

      getAllTreePathsHelper(root.left, runningPath, finalPaths)
      getAllTreePathsHelper(root.right, runningPath, finalPaths)

      # once we are done with this node, pop it from the running path so that we can start exploring the parent's right branch
      runningPath.pop()
  ```

- You can embed a function definition within another function definition
  - This algorithm returns a unique list of all duplicate values within a Binary Tree

  ```python
  def getDuplicateValues(root):
      values = set()
      duplicates = set()

      # nested function definition
      def findDuplicates(root):
          if root is None:
              return
          if root.val in values and root.val not in duplicates:
              duplicates.add(root.val)

          values.add(root.val)

          findDuplicates(root.left)
          findDuplicates(root.right)

      # call the function here
      findDuplicates(root)
      return list(duplicates)
  ```

  - Benefits of this
    - More readability --> you know that the nested function is only called by the parent function and its implementation can be abstracted from the overall implementation
    - You can use local variables within the parent function inside the nested function without passing them as arguments

- Example of an iterative approach to depth first search algorithm using stack (in this example, performing in-order traversal on a Binary Tree)

  ```python
  def inOrderTraversal(root):
      stack = []
      current = root

      while True:
          # keep pushing to stack while left child exists
          if current is not None:
              stack.append(current)
              current = current.left
          # after left is traversed, push right child to stack
          elif stack: # notice how we don't need to say 'elif len(stack) > 0'
              current = stack.pop()
              print(current.val)
              current = current.right
          else:
              break
  ```

- Example of using a stack for DFS on a graph

  ```python
  def dfs(node):
      stack = [node]

      while len(stack):
          node = stack.pop()
          print(node.val)
          # we reverse so that the last child pushed onto the stack is the node's leftmost child
          for child in reversed(node.children):
              stack.append(child)
  ```

- Sometimes you can use an array instead of a hash table (ex. when keeping track of visited elements in an array) because both will have a constant lookup time
  - This algorithm check to see if an array completes one full cycle, treating each element in the array as the next index to check (not sure if this algorithm is implemented 100% correctly)

  ```python
  # input --> [4, 3, 1, 0, 2]
  # this contains one full cycle
  # [>4, 3, 1, 0, 2]
  # [4, 3, 1, 0, >2]
  # [4, 3, >1, 0, 2]
  # [4, >3, 1, 0, 2]
  # [4, 3, 1, >0, 2]
  # [>4, 3, 1, 0, 2]

  def completesOneFullCycle(array):
      idx = 0
      # every time an element is visited, that position is marked in positionsVisited
      positionsVisited = [False for _ in range(len(array))]
      for i in range((len(array))):
          nextIdx = array[idx]
          if positionsVisited[nextIdx] == True:
              return False
          idx = array[idx]
          positionsVisited[idx] = True

      return idx == 0
  ```

- Heap class implementation

  ```python
  class MinHeap:
      def __init__(self, array):
          self.heap = self.buildHeap(array)

      # ===================== Core Functions =====================

      # O(n) time | O(1) space
      def buildHeap(self, array):
          for idx in reversed(range(len(array))):
              if not self.hasChildren(idx, array):
                  continue
              self.siftDown(idx, array)
          return array

      # O(log(n)) time | O(1) space
      def siftDown(self, currentIdx, heap):
          while self.hasChildren(currentIdx, heap):
              leftChildIdx = self.getLeftChildIdx(currentIdx, heap)
              rightChildIdx = self.getRightChildIdx(currentIdx, heap)
              smallerChildIdx = self.getSmallerChildIdx(currentIdx, heap)

              if heap[currentIdx] <= heap[smallerChildIdx]:
                  break

              self.swap(currentIdx, smallerChildIdx, heap)
              currentIdx = smallerChildIdx

      # O(log(n)) time | O(1) space
      def siftUp(self, currentIdx, heap):
          parentIdx = self.getParentIdx(currentIdx)

          while parentIdx != -1 and heap[currentIdx] < heap[parentIdx]:
              self.swap(currentIdx, parentIdx, heap)
              currentIdx = parentIdx
              parentIdx = self.getParentIdx(currentIdx)

      # O(1) time | O(1) space
      def peek(self):
          return self.heap[0]

      # O(log(n)) time | O(1) space
      def remove(self):
          lastIdx = len(self.heap) - 1
          self.swap(0, lastIdx, self.heap)
          removed = self.heap.pop()
          self.siftDown(0, self.heap)
          return removed

      # O(log(n)) time | O(1) space
      def insert(self, value):
          self.heap.append(value)
          lastIdx = len(self.heap) - 1
          self.siftUp(lastIdx, self.heap)

      # ===================== Helper Functions =====================

      def swap(self, i, j, heap):
          heap[i], heap[j] = heap[j], heap[i]

      def getParentIdx(self, idx):
          if idx == 0:
              return -1
          return (idx - 1) // 2

      def getLeftChildIdx(self, idx, heap):
          leftChildIdx = (idx * 2) + 1
          if leftChildIdx > len(heap) - 1:
              return -1
          return leftChildIdx

      def getRightChildIdx(self, idx, heap):
          rightChildIdx = (idx * 2) + 2
          if rightChildIdx > len(heap) - 1:
              return -1
          return rightChildIdx

      def hasChildren(self, idx, heap):
          leftChild = self.getLeftChildIdx(idx, heap)
          return leftChild != -1

      def getSmallerChildIdx(self, idx, heap):
          leftChildIdx = self.getLeftChildIdx(idx, heap)
          rightChildIdx = self.getRightChildIdx(idx, heap)
          if leftChildIdx == -1:
              return -1
          if rightChildIdx == -1:
              return leftChildIdx
          return leftChildIdx if heap[leftChildIdx] <= heap[rightChildIdx] else rightChildIdx
  ```

- Using a heap to find the kth largest element in an array

  ```python
  import heapq

  def findKthLargest(nums, k):
      # convert nums array into a heap array
      heapq.heapify(nums)

      # keep popping root element until kth largest is the root element
      while len(nums) > k:
          heapq.heappop(nums)

      return nums[0]
  ```

  - Whereas sorting the array then returning array[-1*k] would run in O(nlog(n)) time, this algorithm runs in O(n) time
    - Heapifying an array takes O(n) time
    - Removing the root of a heap takes O(log(n)) time

- Instead of writing an if statement for updating a variable depending on which value is bigger, use the max() function instead

  ```python
  array = [4, 5, 1, 8, 9, 0]
  maxNum = float('-inf')

  for num in array:
      # instead of this
      maxNum = num if num > maxNum else maxNum

      # just do this
      maxNum = max(num, maxNum)
  ```

- When talking about complexity, realize that there is a difference between O(n + m) and O(max(n, m)). For instance, when traversing a array1 then traversing array2 --> this is O(n + m), whereas traversing both arrays at the same time with 2 pointers and going until the end of the longest one --> this is O(max(n, m))

  ```python
  array1 = [1,2,3]
  array2 = [1,2,3,4,5]

  # this takes n operations
  for num in array1:
      ...

  # this takes m operations
  for num in array2:
      ...

  # we have to go through 3 elements in array1 then 5 elements in array2
  # so, we do n operations and then m operations, so n + m operations in total

  ptr1 = 0
  ptr2 = 0

  # this will either take n operations or m operations, depending on which is larger
  while ptr1 < len(array1) or ptr2 < len(array2):
      ...

  # if array1 has 3 elements and array2 has 5 elements, then the loop will run 5 times
  # so there will be max(n, m) operations
  ```

- Adding an array to another array

  ```python
  array1 = [...]
  array2 = [...]

  # you could just add array2 to array1, but this will create a new array --> not spacially optimal
  array1 += array2

  # you could loop through array2 and add elements from array1 one by one
  for num in array2:
      array1.append(num)

  # but you can just use the extend method to do the same thing as above but in one line
  array1.extend(array2)
  ```

- When traversing linked list or tree or anything with a next/child node, you can check if next is None like this

  ```python
  def printList(head):
      current = head

      # this is the wordy way
      while current is not None:
          print(current.val)

      # this is the concise way
      while current:
          print(current.val)
  ```

- Here is a Suffix Trie Class that will construct a suffix trie from a string and also allow allow you to check if a string is in the trie

  ```python
  class SuffixTrie:
      def __init__(self, string):
          # each node is a hash table where keys are mapped to other nodes (other hash tables)
          self.root = {}
          self.endSymbol = "*"
          self.populateSuffixTrieFrom(string)

      def addStringToTrie(self, string):
          current = self.root
          for char in string:
              # if char is not in the current node's hash table, add it and set to empty hash table (like None in a tree)
              if char not in current:
                  current[char] = {}
              # whether char is in node or not, traverse down the tree
              current = current[char]
          # once string is inserted fully, end it with the end symbol
          current[self.endSymbol] = True

      def populateSuffixTrieFrom(self, string):
          # for each substring, add to trie
          for idx, _ in enumerate(string):
              substring = string[idx:len(string)]
              self.addStringToTrie(substring)

      def contains(self, string):
          current = self.root
          for char in string:
              if char in current:
                  current = current[char]
              else:
                  return False
          # if all the characters were tracked down the trie, but no end symbol in current node, then the string is not in the trie (the string is a substring but not a full match)
          return self.endSymbol in current
  ```

## AlgoExpert Solutions Explained

### Three Number Sum

- sort the input array
- iterate through array with for loop
- in each iteration, perform two pointer traversal where leftPtr moves from i+1 to end and rightPtr moves from end to left
- if array[i] + array[leftPtr] + array[rightPtr] == target sum --> add the triplet to result
  - if sum < target sum --> move leftPtr to the right
  - if sum > target sum --> move rightPtr to the left
- once leftPtr goes past rightPtr, continue to the next iteration in the for loop and reset pointers
- return the list of triplets

### Smallest Difference

- sort both arrays
- perform two pointer traversal, one pointer for each array
- if difference between array1[ptr1] and array2[ptr2] < smallestDiff --> update smallestDiff
- move the pointer that points to the smaller element to the right
  - this is because the arrays are sorted, the pointer pointing to the smallest value needs to be updated so that the difference between the two values decreases
- return the smallest difference at the end

### Move Element To End

- perform two pointer traversal with startPtr and endPtr
- inside outer while loop, while array[endPtr] == valueToMove --> move endPtr left
- next, if array[startPtr] == valueToMove --> swap array[startPtr] and array[endPtr]
- move startPtr right and continue outer loop until startPtr < endPtr
- return array

### Monotonic Array

- keep track of two booleans --> isNonDecreasing and isNonIncreasing
- iterate through input array
  - if current element is smaller then next element --> isNonIncreasing = False
  - if current element is larger than next element --> isNonDecreasing = False
- after loop, return isNonIncreasing or isNonDecreasing
  - if array is not non-increasing and not non-decreasing, then array is not monotonic
  - if either non-increasing or non-decreasing, then array is monotonic

### Spiral Traverse

- overview: traverse the matrix perimeter by perimeter
- 4 pointers --> start of row, end of row, start of column, and end of column
  - first traverse top of box, from left to right
  - then traverse right side of box, from top to bottom
  - then traverse bottom of box, from right to left
  - then traverse left of box, from bottom to top
- move the 4 pointers inward and do it again until start of row passes end of row or until start of column goes past end of column

### Longest Peak

- overview: treat each element as a potential peak and calculate left length and right length
- iterate through array
- check if left element and right element are < current element
  - if so, then current element is a peak
  - else, current element is not peak --> continue to next iteration
- if peak found, set leftIdx left of current and rightIdx right of current
- move leftIdx to the left until out of bounds or until next element is greater
- move rightIdx to the right until out of bounds or until next element is greater
- peak length is distance between leftIdx and rightIdx
  - update longest peak length if need be
- set the next index in the iteration to rightIdx
- return longest peak

### Array Of Products

- Method #1
  - build leftProducts array, which will contain running products from left to right
    - running product for leftProducts[i] = array[i-1] _ array[i-2] _ ... \* array[0]
  - build rightProducts array, which will contain running products from right to left
    - running product for rightProducts[i] = array[i+1] _ array[i+2] _ ... \* array[lastIdx]
  - build final products array where products[i] = leftProducts[i] \* rightProducts[i]
  - return products array

- Method #2
  - build products array, which will contain running products from left to right (same as last method)
  - iterate through input array in reverse, keep track of running product, and set products[i] = array[i] \* runningProduct
  - example:
    - input array - [5 1 4 2]
    - products array after first iteration - [1 5 5 20]
    - products array during second iteration - [1 5 5 20] -> [1 5 10 20] -> [1 40 10 20] -> [8 40 10 20]
  - return products array

### First Duplicate Value

- Method #1
  - initialize hash table
  - iterate through array
  - if element is in hash table --> return element
  - else, add element to hash table

- Method #2
  - iterate through array
  - get absolute value of current element
  - if array[absVal - 1] is negative --> return absVal
  - else, set array[absVal - 1] to be negative
  - after loop, return -1 because there are no duplicates

### Merge Overlapping Intervals

- sort intervals by first element of each interval
- add first interval to result
- iterate through intervals
  - if next interval in array overlaps with last interval in result, set end of last interval in result to max(end of last interval, end of current interval)
  - else, add interval to result
- return result containing non-overlapping intervals

### Validate BST

- recursive algorithm that traverses all the nodes and checks if the node value is < minVal and >= maxVal
  - if not, return False
- check left tree, passing current node val as maxVal
- check right tree, passing current node val as minVal
- is left is valid and right is valid, return True
  - else, return False

### BST Traversal

- in-order traversal
  - traverse left
  - record current node
  - traverse right
- pre-order traversal
  - record current node
  - traverse left
  - traverse right
- post-order traversal
  - traverse left
  - traverse right
  - record current node

### Min Height BST

- recursive algorithm that calculates middle element of array
  - if middle element < current node in tree --> set middle element as left child
  - if middle element >= current node in tree --> set middle element as right child
- set current node to the newly added node
- call the recursive function one on left half of array and once on right half of array

### Find Kth Largest Value In BST

- Method #1
  - perform in-order traversal and build the array of values
  - return array[-1 * k]

- Method #2
  - perform reverse in-order traversal
    - traverse right
    - check current
    - traverse left
  - keep track of number of nodes visited and the latest visited node
  - once number of nodes visited >= k --> return latest visited node

### Reconstruct BST

### Invert Binary Tree

- Method #1
  - add root to queue
  - loop over queue until empty
  - dequeue node and swap its left and right child
  - add children to queue

- Method #2
  - recursive function
  - swap current node's left and right children
  - call on left child then right child

### Binary Tree Diameter

- recursive algorithm
- calculate diameter of current node --> max of these two pieces of info...
  - left subtree height + right subtree height
  - max between left diameter and right diameter
- at the end of each function call, return height and diameter of current node

### Find Successor

- Method #1
  - build in-order traversal array of nodes from the input tree
  - return the node that comes after the target node in the array
  - if target node is the last node --> return None

- Method #2
  - if the target node has a right child --> return the left most child of the node's right child
  - else, return the right most parent

### Height Balanced Binary Tree

- recursive algorithm
- calculate height of current node
- determine if current node is balanced --> this is true if...
  - left subtree is balanced
  - right subtree is balanced
  - difference between left subtree height and right subtree height is <= 1
- at the end of each function call, return height and isBalanced for each node

### Max Subset Sum No Adjacent

### Number Of Ways To Make Change

### Min Number Of Coins For Change

### Levenshtein Distance

### Number Of Ways To Traverse Graph

### Kadane's Algorithm

### Single Cycle Check

- loop n times, where n is the length of the array
- calculate next index --> current index + value at current index
  - mod next index with length of array, because it could be out of bounds
  - next index will either be positive or negative, but both will work because array[-1] will reference last element
- during the loop, if number of elements visited > 0 and current index is 0 --> return False
  - without this, there can be loop in graph that goes through index 0 and if it lands on 0 at the end, then we will return True at the end and that's not right
- after loop, if curren index is 0 --> return True
  - othewise, return False

### Breadth-first Search

- add root node to queue
- dequeue node from queue, add node's children to queue, continue

### River Sizes

- initialize a matrix of 0's
- iterate through matrix, marking each position as visited
- if you come across a 1 and that position in the visited matrix is False --> perform DFS
  - count up the number of connected 1's
- return array of river counts

### Youngest Common Ancestor

- get the depth of descendant1 and descendant2 in the graph
- d1 is a pointer to descendant1 and d2 is a pointer to descendant2
- whichever descendant is deeper in the graph, move respective pointer to parent until both pointers have same depth
- then, move both pointers up until they land on the same parent --> return that parent node

### Remove Islands

- initialize a matrix of 0's to denote which elements have been visited
- iterate through matrix
- if element is on the border and is a 1 --> perform DFS on it and mark all its corresponding positions in the visited matrix to True
- at this point, the visited matrix contains all the islands that touch the border
- afterwards, loop through matrix again and change any 1 to a 0 if it's corresponding position in the visited matrix is False (so if it is not part of a border island)

### Cycle In Graph

- Method #1
  - keep track of nodes that have been visited as well as nodes in the current traversal stack
    - both with arrays for easy indexing
  - loop through the nodes and for each node, perform DFS
  - at the start of each DFS traversal, mark the current node as visited in the visited array and mark it in the traversal stack
    - if a node that we visit is already in the traversal stack --> a cycle exists --> return True
    - at the end of the DFS function, unmark the current node in the traversal stack

- Method #2
  - use 3-color DFS
    - WHITE - node has node been visited
    - BLACK - node has been visited, but not in stack
    - GREY - node is in stack
  - instead of using 2 arrays, one for visited notes and one for nodes in stack --> use one array of colors

### Minimum Passes Of Matrix

### Task Assignment

### Valid Starting City

### Remove Kth Node From End

- perform 2 pointer traversal --> move ptrRight all the way to the end and only strat moving ptrLeft after k nodes have been seen
- at the end of the traversal, ptrRight should be pointing to None at the end of the list and ptrLeft should be pointing to the node that needs to be deleted (meanwhile, keep track of the node before ptrLeft)
- set node before ptrLeft to point to node after ptrLeft
- if ptrLeft is pointing to head, then just move head to the right

### Sum Of Linked List

- traverse both lists at the same time
- sum up the two current node values and the carry value (either 1 or 0)
  - if either node is None --> use the value 0
- set the carry = sum // 10 --> will result in 1 if sum > 9, otherwise, it will set to 0
- after the loop, once traversal reaches end of both lists, check if carry is 1
  - if so, add one more node to the resulting list with value of 1
  - if you use this as the while loop condition `while nodeOne or nodeTwo or carry != 0` --> then after traversal ends for both lists, it will check the carry value and if it is 1, then it will do the above task

### Permutations

### Powerset

### Phone Number Mnemonics

### Staircase Traversal

### Search In Sorted Matrix

- start looking at the top right corner of the matrix
- if target is less than current element --> move left
- if target is greater than current element --> move down
- if targe == current element --> return coordinate
- once row or col is out of bounds, exit loop and return [-1, -1]

### Three Number Sort

- Method #1
  - overview: variation of bucket sort
  - iterate over array and keep count of how many times each value appears
  - iterate over array again and insert first element x times, second element y times, and third element z times, where x, y, and z are how many times first, second, and third elements appear, respectively

- Method #2
  - iterate through the array from left to right, moving all first elements to the left by swapping
  - iterate through the array again, this time from right to left, moving all the third elements to the right by swapper
  - naturally, the second elements will all result in the middle of the array

- Method #3
  - use 3 pointer traversal --> firstPtr, secondPtr, thirdPtr
    - firstPtr will be initialized to first element, secondPtr to second element, and thirdPtr to last element
  - if element at secondPtr == first expected element --> swap elements at firstPtr and secondPtr, then shift both pointerts to the right
  - if element at secondPtr == third expected element --> swap elements at secondPtr and thirdPtr, then shift secondPtr right and thirdPtr left
  - once secondPtr goes past thirdPtr, stop the loop

### Balanced Brackets

- create string of opening and closing brackets
- create dictionary with keys as closing brackets and values as opening brackets
- initialize empty stack
- iterate through input string
  - if char is opening bracket, push to stack
  - otherwise, if char is closing bracket...
    - if stack is empty, that means no opening bracket came before --> return false
    - if top of stack is corresponding opening bracket --> pop
    - if top of stack is not corresponding opening bracket --> return false

### Sunset Views

- if direction is East, iterate through buildings from left to right
- if direction is West, iterate through buildings from right to left
- keep track of running max height
- if current building is larger than running max height --> add to result array
- return result array after loop

### Sort Stack

- the intuition is to pop an element off stack, sort the remainder of stack, insert element in correct position (by popping element off stac, until correct position found, then pushing elment and then pushing rest of elements)
- the main recursive function is going to pop element from stack, then call itself again
  - keep doing this until stack empty
- going back up the call stack, for each element, insert into correct position in stack
- insert method is another recursive function
  - keep popping elements off until stack empty or current element is greater than or equal to top of stack --> push onto stack
  - going back up call stack, for each element, push back onto stack

### Next Greater Element

- initialize results array of -1's
- initialize empty stack
- iterate over the input array twice (range of double the length of input array)
  - using mod to keep track of index
- if stack empty, push index of current element onto stack
- if current element <= element at index that's on top of stack --> push current index onto stack
  - otherwise, pop index off stack and set value at that index in results array to the current element
  - keep doing this until stack empty or current element <= element at index that's on top of stack

### Longest Palindromic Substring

- palindrome center can either be single char or in between two chars
- iterate through string and treat each character as a potential palindrome center
  - use two pointer traversal to compare left and right chars, keep moving outward while left and right match and keep count
- after each char check, also check if between current char and last char is a center --> another two pointer traversal

### Group Anagrams

- initialize a hash table (going to act as buckets for anagrams)
- iterate through the array of strings
- for each string, sort the string and check if the sorted string is a currently a key in the hash table
  - if so, append the original string to the list (each key maps to a list of strings)
  - otherwise, create a new key as the sorted string and map it to an array with one element, the original word
- after that loop, convert the values in the hash table to a list and return
  - `list(anagrams.values())`

### Valid IP Adress

### Reverse Words in String

- initialize array to hold words and spaces
- iterate through string and keep track of the running word
- any time a space is encountered, append running word (if there is one) to array and append space to array, then restart running word
  - those adjecent individual spaces will be joined in the end and will become clusters of spaces
- after iteration, reverse list and join everything into one string and return

### Minimum Characters For Words

- initialize hash table of overall max characters needed
- for each word in list, create hash table of characters and counts
- after analyzing each word, go through hash table for that word and for each character...
  - if character is in max hash table, set its count to max between current max count and character count in current word
  - otherwise, add character to max hash table and set count to 1
- after iterating through words list, create result array, appending each character from max hash table n times, where n is the number of times that character is required
- return result array
