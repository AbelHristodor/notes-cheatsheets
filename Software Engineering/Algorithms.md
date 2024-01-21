---
created: 2024-01-11T15:32
updated: 2024-01-21T15:08
tags:
  - engineering
  - interview-questions
---
1. **Sorting Algorithms:**
   - **Bubble Sort**: A simple comparison-based algorithm that repeatedly steps through the list, compares adjacent elements, and swaps them if they are in the wrong order. The pass through the list is repeated until no swaps are needed. Its worst-case time complexity is O(n^2).
   - **Insertion Sort**: Builds the final sorted array one item at a time. It is much less efficient on large lists than more advanced algorithms such as quicksort. Its worst-case time complexity is O(n^2).
   - **Merge Sort**: A divide and conquer algorithm that divides the unsorted list into n sublists, each containing one element (a list of one element is considered sorted), then repeatedly merges sublists to produce a new sorted sublist until there is only one sublist remaining. This will be the sorted list. The time complexity is O(n log n).
   - **Quick Sort**: Also a divide and conquer algorithm, which works by selecting a 'pivot' element from the array and partitioning the other elements into two sub-arrays, according to whether they are less than or greater than the pivot. The sub-arrays are then sorted recursively. The average time complexity is O(n log n), but the worst case is O(n^2).

2. **Search Algorithms:**
   - **Linear Search**: The simplest search algorithm that checks every element in the list until the desired element is found or the list ends. Its time complexity is O(n).
   - **Binary Search**: An efficient algorithm that finds the position of a target value within a sorted array. It compares the target value to the middle element of the array; if they are not equal, the half in which the target cannot lie is eliminated and the search continues on the remaining half until the value is found. The time complexity is O(log n).

3. **Graph Algorithms:**
   - **Depth-First Search (DFS)**: An algorithm for traversing or searching tree or graph data structures. It starts at the root node and explores as far as possible along each branch before backtracking. Its time complexity is O(V+E), where V is the number of vertices and E is the number of edges.
   - **Breadth-First Search (BFS)**: Another algorithm for traversing or searching tree or graph data structures. It starts at the root node and explores all neighbor nodes at the present depth prior to moving on to nodes at the next depth level. Its time complexity is also O(V+E).

4. **Dynamic Programming:**
   - **Fibonacci Sequence**: The Fibonacci sequence can be computed using dynamic programming to store previously calculated values, reducing the exponential complexity of the recursive approach to O(n).
   - **Knapsack Problem**: This algorithm determines the most efficient way to pack items into a container given weight constraints. The complexity of the dynamic programming approach is O(nW), where n is the number of items and W is the capacity of the knapsack.

5. **Hashing Algorithm:**
   - **Hash table operations**: Involves computing an index using a hash function and then using this index to place or retrieve the data within a table structure. The average-case complexity for insert, delete, and search operations is O(1), assuming a good hash function and enough table size.

6. **String Matching Algorithms:**
   - **KMP (Knuth-Morris-Pratt)**: A string-matching algorithm that seeks occurrences of a "word" W within a main "text string" S by employing the observation that when a mismatch occurs, the word itself embodies sufficient information to determine where the next match could begin, thus bypassing re-examination of previously matched characters. Its time complexity is O(n+m), where n is the length of the text string and m is the length of the word.
