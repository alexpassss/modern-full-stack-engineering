### **Coding Tasks**

---

### **1. Array and String Manipulation**

**Task 1: Longest Substring Without Repeating Characters**

- **Problem**: Given a string `s`, find the length of the **longest substring** without repeating characters.

- **Input**:

  - `s = "abcabcbb"`

- **Output**:

  - `3` (The answer is "abc", with a length of 3)

- **Solution approach**:

  - Use the **sliding window technique** and a **hashmap** to track the characters and their positions.
  - For each character, slide the window to the right, and update the start of the window if a repeated character is found.

- **Expected time complexity**: **O(n)**

---

**Task 2: Trapping Rain Water**

- **Problem**: Given `n` non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it can trap after raining.

- **Input**:

  - `height = [0,1,0,2,1,0,1,3,2,1,2,1]`

- **Output**:

  - `6`

- **Solution approach**:
  - Use two pointers, one starting from the left and one from the right. Calculate trapped water by maintaining two variables, `left_max` and `right_max`, which store the maximum heights seen so far from both sides.
- **Expected time complexity**: **O(n)**

---

### **2. Dynamic Programming**

**Task 3: Longest Increasing Subsequence**

- **Problem**: Given an integer array `nums`, return the length of the **longest strictly increasing subsequence**.

- **Input**:

  - `nums = [10,9,2,5,3,7,101,18]`

- **Output**:

  - `4` (The LIS is `[2,3,7,101]`)

- **Solution approach**:

  - Use **dynamic programming** to keep track of the longest increasing subsequence up to each element. You can improve the time complexity to **O(n log n)** using a **binary search**.

- **Expected time complexity**: **O(n log n)**

---

**Task 4: Coin Change**

- **Problem**: Given an array `coins` representing coin denominations and an integer `amount`, return the fewest number of coins needed to make up the amount. If that amount cannot be made up, return `-1`.

- **Input**:

  - `coins = [1, 2, 5]`, `amount = 11`

- **Output**:

  - `3` (11 = 5 + 5 + 1)

- **Solution approach**:

  - Use **dynamic programming** to solve this problem by creating a table where each index represents the minimum number of coins needed to make up that amount. Update the table iteratively for each coin.

- **Expected time complexity**: **O(n \* amount)**

---

### **3. Graphs**

**Task 5: Word Ladder**

- **Problem**: Given two words, `beginWord` and `endWord`, and a dictionary of words, find the **length of the shortest transformation sequence** from `beginWord` to `endWord`, such that only one letter can be changed at a time and each transformed word must exist in the dictionary.

- **Input**:

  - `beginWord = "hit"`, `endWord = "cog"`, `wordList = ["hot","dot","dog","lot","log","cog"]`

- **Output**:

  - `5` (The shortest transformation is: "hit" -> "hot" -> "dot" -> "dog" -> "cog")

- **Solution approach**:

  - Use **BFS (Breadth-First Search)** to explore all possible word transformations level by level. For each word, change one letter at a time and check if the resulting word is in the dictionary.

- **Expected time complexity**: **O(N \* L^2)**, where `N` is the number of words in the dictionary and `L` is the length of each word.

---

**Task 6: Course Schedule II**

- **Problem**: There are a total of `n` courses you have to take, labeled from `0` to `n-1`. Some courses may have prerequisites. Return the ordering of courses you should take to finish all courses. If it’s impossible, return an empty array.

- **Input**:

  - `numCourses = 4`, `prerequisites = [[1,0],[2,0],[3,1],[3,2]]`

- **Output**:

  - `[0,1,2,3]` or `[0,2,1,3]`

- **Solution approach**:

  - Use **Topological Sorting** with **Kahn's algorithm** or **DFS** to detect cycles. Maintain an in-degree array to determine the order in which the courses should be taken.

- **Expected time complexity**: **O(V + E)**, where `V` is the number of courses and `E` is the number of prerequisites.

---

### **4. Backtracking**

**Task 7: N-Queens**

- **Problem**: The **N-Queens problem** involves placing `n` queens on an `n x n` chessboard so that no two queens can attack each other. Return all distinct solutions to the N-Queens puzzle.

- **Input**:

  - `n = 4`

- **Output**:

  - ```
    [[".Q..",
      "...Q",
      "Q...",
      "..Q."],
     ["..Q.",
      "Q...",
      "...Q",
      ".Q.."]]
    ```

- **Solution approach**:

  - Use **backtracking** to place queens one row at a time. For each queen, check if the current placement is valid (i.e., no other queen threatens it). If valid, place the queen and continue to the next row; otherwise, backtrack.

- **Expected time complexity**: **O(n!)**

---

**Task 8: Subsets II**

- **Problem**: Given a collection of integers that might contain duplicates, return all possible **subsets (the power set)**.

- **Input**:

  - `nums = [1,2,2]`

- **Output**:

  - `[[],[1],[1,2],[1,2,2],[2],[2,2]]`

- **Solution approach**:

  - Use **backtracking** to generate all subsets. Sort the array first and ensure that duplicates are handled by skipping over repeated elements during the subset generation.

- **Expected time complexity**: **O(2^n)**

---

### **5. System Design and Optimization**

**Task 9: Design a Cache (LRU Cache)**

- **Problem**: Design a data structure that follows the **Least Recently Used (LRU) Cache** principle. Implement the `LRUCache` class:

  - `LRUCache(int capacity)` initializes the cache with a positive size `capacity`.
  - `int get(int key)` returns the value of the `key` if it exists, otherwise returns `-1`.
  - `void put(int key, int value)` updates the value if the `key` exists, otherwise adds the key-value pair to the cache. If the cache reaches its capacity, it should invalidate the least recently used item.

- **Solution approach**:

  - Use a **hashmap** to store key-value pairs for `O(1)` access, and a **doubly linked list** to maintain the order of use. The doubly linked list allows for efficient addition and removal of nodes.

- **Expected time complexity**: **O(1)** for both `get` and `put` operations.

---

**Task 10: Median of Two Sorted Arrays**

- **Problem**: Given two sorted arrays `nums1` and `nums2` of size `m` and `n`, return the **median** of the two sorted arrays.

- **Input**:

  - `nums1 = [1,3]`, `nums2 = [2]`

- **Output**:

  - `2.0`

- **Solution approach**:

  - Use **binary search** to partition the arrays such that the left half of both arrays contains smaller elements and the right half contains larger elements. The median is the average of the two middle elements.

- **Expected time complexity**: **O(log(min(m, n)))**

---

### **6. Tree Problems**

**Task 11: Serialize and Deserialize Binary Tree**

- **Problem**: Design an algorithm to serialize and deserialize a binary tree. Serialization is the process of converting a tree into a string representation, and deserialization is the process of converting a string back into a tree.

- **Solution approach**:
  - Use **pre-order traversal** (or level-order) for serialization and store nulls explicitly for missing children. During deserialization, reconstruct the tree

by following the same traversal order.

- **Expected time complexity**: **O(n)** for both serialization and deserialization.

---

**Task 12: Lowest Common Ancestor of a Binary Tree**

- **Problem**: Given a binary tree, find the **lowest common ancestor (LCA)** of two given nodes.

- **Input**:

  - `root = [3,5,1,6,2,0,8,null,null,7,4]`, `p = 5`, `q = 1`

- **Output**:

  - `3` (The LCA of nodes 5 and 1 is 3)

- **Solution approach**:

  - Use a **recursive DFS approach**. Traverse the tree and return the node if it matches either `p` or `q`. If both children return non-null results, the current node is the LCA.

- **Expected time complexity**: **O(n)**
