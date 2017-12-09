# 1332 Final Exam

## Content
### First part of Exam
* All Multiple Choice
* Test 1, 2, 3

### Second Part of Exam
* Graph Algorithms (coding)
  * DFS
  * BFS
  * Kruskals - Minimum Spanning Tree
  * Djikstra
  * Prims - Minimum Spanning Tree
* String Searching (coding)
* Diagram LCS
* Floyd-Warshaw (maybe diagram)
* Dynamic Programming
    * Fibonacci

## First Part
### Test 1
  * **Arrays**
    * Arrays are data structures built into Java
    * Once you define their size they cannot be resized
    * Insertion is **O(n)** because you have to move everything back
      * From back, it's O(1). (Best case)
    * Deletion is **O(n)** because you have to move everything forward
      * From back, it's **O(1)**. (Best case)
    * Search is **O(1)** because you just use the index
    * Generic Arrays
    ```java
    T[] arr = (T[]) new Object[n];
    ```
  * **ArrayLists**
    * ArrayLists is a data structure backed by an Array
    * ArrayList size can be increased if the arraylsit fills up
    * inherits AbstractList and implements List interface
    * ArrayList cannot be used for primitive types
    * Same Big O as Arrays
    * Contains is O(n) (have to iterate through since you are not providing an index)
    * Get (at an index) is O(1)

  * **LinkedList**
    * LinkedList is a list of connected nodes
    * Each node contains references to other nodes as well as the data it holds
    * Singular, Doubly, and Circular LinkedList
      * Singular Node
      ```java
      class Node<T> {
          T data;
          Node<T> next;
        }
      ```
      * Double Node
      ```java
      class Node<T> {
          T data;
          Node<T> prev;
          Node<T> next;
        }
      ```
    * **Big O**
      * Get: O(n) have to iterate through the list  
      * Search: O(n) same reason for get
      * Add (to end): O(1) (all)
      * Add (at index): O(n) (all)
      * Add (to begining): O(1) (all)
      * Delete (from end): O(n) (singly) / O(1) (doubly)
      * Delete (at index): O(n) (all)
      * Delete (from beginning): O(1) (all)
    * Circular
      * any node can be a starting point
      * tail -> next = head
      * useful for implementations of queue because you don't need to maintain a reference to head and tail
      * Can be implemented as a Singular or Doubly linked List
      * Inherits the Big O of both types depending on which type it is

  * **Stacks**
    * Stacks are LIFO, think about a stack of plates
    * They can be backed by ArrayLists or LinkedLists
    * When backed by an array, new elements should be added to the back of the array and removed from the back
    * When backed by a singly linked list new elements should be added to the front and removed from the front
    * **Big O:**
      * Add: O(1) (stack.push())
      * Remove: O(1) (stack.pop())
      * Peek (first element): O(1)
      * Access / Search: O(n)
  * **Queue**
    * Queues are FIFO, think about a line of people
    * They can be backed by Arrays (ArrayLists) or LinkedList
    * When backed by an array you dequeue from the front and enqueue to the back
      * this means you need to keep a reference to the front and the back
      * whenever you remove from the front you need to increment front and mod with the length of the backing array (Queue is circular in this nature)
      * Whenever you add you have to also increment back
        * if back is greater than the length of the backing array then you must set back to (front + size) % backingArray.length
        * if size == backingArray.length, then resize()
      * resizing is O(n)
      ```java
      private T[] resize() {
          int newLength = backingArray.length * 2;
          T[] newArrayList = (T[]) new Object[newLength];
          for (int i = 0; i < backingArray.length; i++) {
            newArrayList[i] = backingArray[(front + i)
            % backingArray.length];
          }
          front = 0;
          back = size;
          return newArrayList;
        }
      ```
    * When backed by a singly linked list you want to add to the back and remove from the front
    * When backed by a doubly linked list you want to add to the back and remove from the front
    * **Big O:**
      * Enqueue: O(1) (insert)
      * Dequeue: O(1) (poll)
      * Peek: O(1)
      * Access / Search : O(n)

  * **Trees**
    * Trees are data structures that contains of nodes which have their own subtrees
    * It is a Graph
    * It is a recursive data structure
    * Each node contains references to other nodes
    * The node that is not referenced to by any other nodes is called the root node
    * Nodes that have contain no sub-trees are leaf Nodes
    * Types of trees: Binary Search Tree, AVL Tree (auto balancing), 2-4 Tree

  * **Binary Search Tree**
    * Each node contains as much 2 sub-nodes
    * All nodes to the right of a node contains data less than the current node
    * All nodes to the left of a node contains data greater than the current node
    * Traversals
      * In Order (recursive) -> left node, current node, right node
      * Post Order (recursive) -> left, right, current
      * Pre Order (recursive) -> current, left, right
      * Level Order (iterative)
        * use a queue data structure to store visited nodes and to poll
        * Other 3 traversal were DFS
        * Store root node in Queue
        * While queue is not empty
          * poll the Queue (and store the data in a list)
          * add the left and right node to the queue (if they are not null)
        * return the list
      * Removing
        * Predecessor Method (replace node with largest node smaller than it)
        * Successor Method (replace node with smallest node larger than it)
      * **Big O**
        * Searching: O(log n), Worst - O(n)
        * Adding: O(log n), Worst - O(n)
        * Removing: O(log n), Worst - O(n)

      ![Image](https://upload.wikimedia.org/wikipedia/commons/thumb/d/da/Binary_search_tree.svg/1200px-Binary_search_tree.svg.png)

  * **Recursion**
    * Base Case
    * Approach to Base Case
    * Recursive Case

  * **Generics**
    * Generics are just a placeholder for objects

### Test 2
  * **AVLs**
    * Rotations
      * Right Rotation
        * When the balance factor is greater than 1, left subtree is more than one higher than the right subtree
        ![Image](http://occcwiki.org/images/e/ef/SingleRightRotation.png)
      * Left Rotation
        * When the balance factor is less than -1, right subtree is more than one higher than the left subtree
        ![Image](http://occcwiki.org/images/f/f4/SingleLeftRotation.png)
      * Left-Right Rotation
        * When the balance factor is less than -1, but the height of that node is > 0
        ![Image](http://occcwiki.org/images/a/a3/DoubleRightRotation.png)
      * Right-Left Rotation
        * When the balance factor is greater than 1, but the height of that node is < 0
        ![Image](http://occcwiki.org/images/f/f7/DoubleLeftRotation.png)
    * Height
      * In an AVL tree each node has a height field where you store the height of the node
      * Every time you add or remove a node you have to update the height of the node
    ```python
    def height(node):
        if node is None:
          return -1
        else:
          return node.height
    def update_height(node):
        node.height = max(height(node.left),
        height(node.right)) + 1
    ```
    * Balance Factor
      * height(node.left) - height(node.right)
    * **Big O**
      * Adding: O(log n)
      * Removing: O(log n)
      * Search: O(log n)
      * Balancing: O(1)
  * **Heaps (min and max)**
    * Specialized Tree
    ![Image](http://interactivepython.org/runestone/static/pythonds/_images/heapOrder.png)
    * 2 properties
      * Completeness (filed left to right)
      * Order (everything below a node is less/greater than it)
    * Heaps are usually stored as Arrays
      * Root of heap is A[i]
      * Parent A[floor(i/2)]
      * Left Child A[2i]
      * Right Child A[2i + 1]
    * Add
      * add new element to last index in heap
      * keep checking if it is bigger/smaller than its parent, if it is then switch the parent with it
      * keep doing this until its smaller/bigger than its parent
    * Remove
      * same as add but reverse
      * remove first element and replace it with last element in heap
      * keep checking if its children are bigger/smaller than it
      * if they are then switch the biggest/smallest children with it
      * keep doing this until you are at end of index or both children are smaller/bigger than it
    * Heapify (one node)
      * Makes one node adhere to heap properties
      * O(log n) algorithm
    * Build Heap
      * Heapify for all nodes
      * O(n * log n) algorithm
    * **Big O**
      * Adding: O(log n)
      * Removing: O(log n)
      * Get (only can get top element, cant access/search for others): O(1)
  * **Priority Queues**
    * Queue that is ordered by some comparator
    * Usually implemented with a heap
    * However it is an abstract data type and can be implement with a wide array of data structures
    * **Big O**
      * Adding: O(log n)
      * Delete: O(log n)
      * Search: O(n)
  * **Hash Maps**
    * Hash Maps are data structures that store key value pairs
    * It is usually backed by an array (could also be an arraylist)
    * The key is hashed and this hash value is modded with the length of the array which is used as the index to place the element in
    * If an element is already in that index, external chaining or probing is utilized to deal with collisions
    * Hash Maps usually have a load factor which is equal to the (number of elements) / (length of backing table)
    * Once the load factor threshold is met the table must be resized and all keys need to be rehashed and put back into the resized table
      * this is accomplished by saving the current table in a temp variable
      * then resize the original table to size * 2 + 1
      * for every element in the temp table add it to the new table
    * When removing a value from the HashMap you do the same thing as add, except you dont add any data and just returned the removed data and set the current ```table[index].setRemoved(true);```
      * this is done because in HashMap search, get, and remove whenever you hit a null value know that the value is not in the hash map or cannot be removed from the hashmap
    * Adding to hashmap also takes into account removed values
      * whenever you are probing and you come across a removed value, save that value
      * keep probing until you find the key
      * if you don't find the key then put the key,value pair into the removed index that you saved earlier
      * This is done because we want the key,value pair to be closest to the ideal index as possible
    * External Chaining
      * LinkedList
        * Add: O(1) (adding to head)
        * Removing: O(n) (removed pair could be anywhere in the linkedlist)
        * Search: O(n) (same as remove)
      * BST
        * Add: O(log n) / O(n)
        * Remove: O(log n) / O(n)
        * Search O(log n) / O(n)
      * AVL
        * Add: O(log n)
        * Remove: O(log n)
        * Search: O(log n)
    * Probing
      * Linear - keep adding one to the index until you find the key or an empty spot
      * Quadratic - index + 1, index + 2^2, index + 3^2, index + 4^2 ...
        * this does not check every index so there are more empty slots and sometimes a Key,Value pair cannot be added in
        * this means that sometimes the array is resized independent of the load factor
        * if you probe n times, where n is the size of the array, then you have to resize the array
    * **Big O Average/Worst**
      * Adding: amortized O(1) (may have to resize the table if the load factor is reached) / O(n)
      * Removing: amortized O(1) / O(n)
      * Search: amortized O(1) / O(n)

  * **SkipLists**
    * Weird ass data structures
    * Really no real-word use cases
    ![Image](https://i.imgur.com/nNjOtfa.png)
    * At both ends of the levels, you need a reference to -(infinity) and +(infinity)
    * Adding
      * Usually done by a predetermined coin flip method
      * For example, if you have a order of HHHTTHT
        * Add 50 - promote 3 levels (3 heads at first, stop when you get to a tails)
        * Add 20 - dont promote (after first tail is another tail so you cannot promote)
        * Add 10 - promote one level (stop at last tail)
    * Search
      * Start at the top level
      * If the node to the right of negative infinity is greater than the value you are looking for then the node is not on that level so go down to the next level
      * If the node to the right of negative infinity is less than the value you are looking for then go to that node
        * keep doing this for a level until you get to a node that is not smaller than the value you are looking for
      * Then drop down to the level before
    * **Big O**
      * Add: O(log n) / O(n)
      * Remove: O(log n) / O(n)
      * Search: O(log n) (better than linked lists) / O(n)
      * Space: O(n log n)

### Test 3
  * Test 3 contained sorting, graphs, and string searching; however, graphs and string searching are more revelant in the second part of the final so we will only be discussing sorting here
  * **Bubble Sort**
    * Simplest sorting algorithm
    * Stable and in-place
    * At the end of each iteration it is guaranteed that at least the last element is sorted
    ```python
    def bubbleSort(alist):
        for passnum in range(len(alist)-1,0,-1):
            for i in range(passnum):
                if alist[i]>alist[i+1]:
                    temp = alist[i]
                    alist[i] = alist[i+1]
                    alist[i+1] = temp
    ```
    * Save the last place you swapped at so you dont compare that again, makes bubble sort little bit more efficient
    * **Big O**
      * Best: O(n)
      * Worst: O(n^2)
      * Average: O(n^2)
  * **Cocktail Sort**
    * same as bubble, but in each outer iteration you sort forward and then backwards
    * meaning for each iteration you have one for loop that moves the largest element all the way back
    * and then another for loop that starts from the book and moves the smallest element to the front
  * **Selection Sort**
    * Find the minimum element in the list and switch it with the element in the front
    * unstable (if the first and last element are the same you will move the last element all the way to the front) and in-place
    ```python
      def selectionSort(alist):
          for fillslot in range(len(alist)-1,0,-1):
              positionOfMin=0
              for location in range(1,fillslot+1):
                  if alist[location]< alist[positionOfMin]:
                    positionOfMin = location

              temp = alist[fillslot]
              alist[fillslot] = alist[positionOfMin]
              alist[positionOfMin] = temp
    ```
    * Selection sort can also be implemented in a way that moves the maximum element to the back
    * **Big O**
      * All Cases: O(n^2)
  * **Insertion Sort**
    * stable and in-place
    * start at the first index and for each subsequent index in the array you put it in the correct spot
      * for example if your array is [4, 5, 1, 3]
      * [4]
      * [4, 5] -> [4, 5] (already in order)
      * [4, 5, 1] -> [4, 1, 5] -> [1, 4, 5]
      * [1, 4, 5, 3] -> [1, 4, 3, 5] -> [1, 3, 4, 5]
    ```python
    def insertionSort(alist):
        for index in range(1,len(alist)):
          currentvalue = alist[index]
          position = index

          while position>0 and alist[position-1]>currentvalue:
            alist[position]=alist[position-1]
            position = position-1

          alist[position]=currentvalue
    ```
    * **Big O**
      * Best: O(n)
      * Average: O(n^2)
      * Worst: O(n^2)
  * **Merge Sort**
    * Divide and Conquer algorithm
    * Keep breaking up the array into smaller arrays
    * Once each element is in its own array, build up and sort each subarray and merge them
    * stable, but out of place (have to make new arrays)
    * recursive in nature
    * MergeSort(arr[], l,  r)  
        * If r > l
          1. Find the middle point to divide the array into two halves:  
               middle m = (l+r)/2
          2. Call mergeSort for first half: Call mergeSort(arr, l, m)
          3. Call mergeSort for second half: Call mergeSort(arr, m+1, r)
          4. Merge the two halves sorted in step 2 and 3: Call merge(arr, l, m, r
   * Breaking up the array
     ```python
     def mergeSort(arr,l,r):
      if l < r:
          # Same as (l+r)/2, but avoids overflow for
          # large l and h
          m = (l+(r-1))/2
          # Sort first and second halves
          mergeSort(arr, l, m)
          mergeSort(arr, m+1, r)
          merge(arr, l, m, r)
     ```
   * Merging the arrays
      ```python
      # Merges two subarrays of arr[].
      # First subarray is arr[l..m]
      # Second subarray is arr[m+1..r]
      def merge(arr, l, m, r):
          n1 = m - l + 1
          n2 = r- m
          # create temp arrays
          L = [0] * (n1)
          R = [0] * (n2)
          # Copy data to temp arrays L[] and R[]
          for i in range(0 , n1):
              L[i] = arr[l + i]
          for j in range(0 , n2):
              R[j] = arr[m + 1 + j]
          # Merge the temp arrays back into arr[l..r]
          i = 0     # Initial index of first subarray
          j = 0     # Initial index of second subarray
          k = l     # Initial index of merged subarray
          while i < n1 and j < n2 :
              if L[i] <= R[j]:
                  arr[k] = L[i]
                  i += 1
              else:
                  arr[k] = R[j]
                  j += 1
              k += 1
          # Copy the remaining elements of L[], if there
          # are any
          while i < n1:
              arr[k] = L[i]
              i += 1
              k += 1
          # Copy the remaining elements of R[], if there
          # are any
          while j < n2:
              arr[k] = R[j]
              j += 1
              k += 1
      ```
    * **Big O**
      * All Cases: O(n log n)
  * **Quick Sort**
    * unstable and inplace
    * divide and conquer
    * the pivot index is chosen at random
    * Method
      * swap the pivot value with the first value of the array
      * have a left pointer that points to the second item in the array
      * have a right pointer that points to the last item
      * increment left index as long as the left index <= right index and arr[leftindex] < pivot
      * decrement the right index as long as right index >= left index and arr[rightindex] > pivot
      * then swap the pivot value with arr[rightindex]
      * that subarray is sorted, so call
        * quicksort(low, rightindex, arr)
        * quicksort(rightindex + 1, high, arr)
    * **Big O**
      * Best and Average: O(n log n)
      * Worst: O(n^2)
  * **Radix Sort**
    * Can only be used to sort integers
    * not a comparison sort
    * two variations, LSD (least significant digit) and MSD (most significant digit)
    * Place numbers in buckets based on digit
      * start with ones digit and move up to tens, and so on
    * These buckets are an array of Queues
    * The number of iterations is equal to the number of digits in the largest number
    * At the end of one iteration you pop off all numbers in the array of queues and add back to the original array that was passed
    * Do this K number of times
    * **Big O**
      * All Cases: O(kn)
      * K is number of digits in largest number


## Second Part
### Graphs
  * **Subgraph:** A subgraph of a graph is a graph where all its vertices and edges are a subset of the original graph's edges and vertices.
  * **Spanning Subgraph:** A spanning subgraph of a graph is a graph which has all the vertices of the original graph, but its edges are still a subset of the original graph's edges.
  * A connected graph has a path between every pair of vertices.
  * **Forest:** An undirected graph with no cycles.
  * **Tree:** A forest, but all the vertices are connected.
  * **Spanning Tree:** A spanning tree of a connected graph is a spanning subgraph that is a tree. This spanning tree is not unique unless the original graph is a tree.
  * **Spanning Forest:** A spanning forest is a spanning subgraph that is a forest.
  * **Depth First Search:**
     * Efficiency is O(n + m), where n is number of vertices, and m is number of edges.
<<<<<<< HEAD
     ```java
      public void dfs(List<Vertex<T>> list, Vertex vertex, Graph graph, Stack<Vertex<T>> visited) {
         ArrayList<Vertex<T>> list = new ArrayList();
         Stack<Vertex<T>> visited = new Stack<>();
         list.add(vertex);
         visited.add(vertex);
         List edges = graph.adjList().get(vertex);
         for (Edge edge : edges) {
            Vertex end = edge.V;
            if (!visited.contains(end)) {
              if (!(edge.getV().equals(vertex))) {
                dfs(list, end, graph, visited);
              }
            }
         }
      }
     ```
     * DFS(list, vertex, graph) visits all the vertices and edges in the connected component of vertex.
     * **All** the edges and vertices visited by DFS(list, vertex, graph form a spanning tree of the connected component of vertex.
=======
       ```java
       public void dfs(List<Vertex<T>> list, Vertex vertex, Graph graph, Stack<Vertex<T>> visited) {
          ArrayList<Vertex<T>> list = new ArrayList();
          Stack<Vertex<T>> visited = new Stack<>();
          list.add(vertex);
          visited.add(vertex);
          List edges = graph.adjList().get(vertex);
          for (Edge edge : edges) {
             Vertex end = edge.V;
             if (!visited.contains(end)) {
               if (!(edge.getV().equals(vertex)) {
                   dfs(list, end, graph, visited);
               }
             }
          }
       }
       ```
>>>>>>> e3c190860d26de45392b9a868e0068a73ff8a499
     * **Diagraming**:
        * Start at Vertex
        * Add it to list and to set
        * For all the vertices adjacent to it
          * check if we have visited it
          * if we have not, then call dfs on that vertex
          * if we have then do nothing, and check the next vertex incident to it
        * If all vertices incident to it are visited, keep going back one vertex from that vertex until you find a vertex that has another incident vertex that we have not visited yet
        * Call dfs on that vertex, and repeat steps
        * You are done when all vertices have been visited

  * **Breadth First Search:**
     * Efficiency is O(n + m), where n is number of vertices, and m is number of edges.
        ```java
        public void bfs(Vertex<T> start, Graph<T> graph) {
            Queue<Vertex<T>> queue = new LinkedList<>();
            HashSet<Vertex<T>> visited = new HashSet<>();
            List<Vertex<T>> list = new ArrayList<>();
            queue.add(start);
            visited.add(start);
            list.add(start);
            while(!queue.isEmpty() && visited.size() < graph.getAdjList().size()) {
                Vertex<T> removed = queue.remove();
                for (Edge<T> item: graph.getAdjList().get(removed)) {
                    if (!visited.contains(item.getV())) {
                        visited.add(item.getV());
                        list.add(item.getV());
                        queue.add(item.getV());
                    }
                }
            }
        }
        ```
    * **Djikstras**

    * **Kruskals**

    * **Prims**

### String Searching
    * KMP
    * Boyer-Moore
    * Rabin-Karp
        String searching:
        n = text length, m = pattern length
        KMP: best = O(m), avg,worst = O(m + n)
        Boyer Moore: best = O(m), avg = O(m + n), worst = O(mn) (when first char is always mismatched)
        Rabin Karp: best = O(m), avg = O(m + n), worst = O(mn) (poor hash, pattern/text hash are equal)

### Dynamic Programming
    * Floyd-Warshall
    * LCS (Diagram)
