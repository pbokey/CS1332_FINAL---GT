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
  * Arrays
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
  * ArrayLists
    * ArrayLists is a data structure backed by an Array
    * ArrayList size can be increased if the arraylsit fills up
    * inherits AbstractList and implements List interface
    * ArrayList cannot be used for primitive types
    * Same Big O as Arrays
    * Contains is O(n) (have to iterate through since you are not providing an index)
    * Get (at an index) is O(1)

  * LinkedList
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

  * Stacks
    * Stacks are LIFO, think about a stack of plates
    * They can be backed by ArrayLists or LinkedLists
    * When backed by an array, new elements should be added to the back of the array and removed from the back
    * When backed by a singly linked list new elements should be added to the front and removed from the front
    * **Big O:**
      * Add: O(1) (stack.push())
      * Remove: O(1) (stack.pop())
      * Peek (first element): O(1)
      * Access / Search: O(n)
  * Queue
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
              newArrayList[i] = backingArray[(front + i) % backingArray.length];
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

  * Trees
    * Trees are data structures that contains of nodes which have their own subtrees
    * It is a Graph
    * It is a recursive data structure
    * Each node contains references to other nodes
    * The node that is not referenced to by any other nodes is called the root node
    * Nodes that have contain no sub-trees are leaf Nodes
    * Types of trees: Binary Search Tree, AVL Tree (auto balancing), 2-4 Tree

  * Binary Search Tree
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

  * Recursion
    * Base Case
    * Approach to Base Case
    * Recursive Case

  * Generics
    * Generics are just a placeholder for objects

### Test 2
  * AVLs
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
          node.height = max(height(node.left), height(node.right)) + 1
      ```
    * Balance Factor
      * height(node.left) - height(node.right)
    * **Big O**
      * Adding: O(log n)
      * Removing: O(log n)
      * Search: O(log n)
      * Balancing: O(1)
  * Heaps (min and max)
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

    * Heapify (one node)
      * Makes one node adhere to heap properties
      * O(log n) algorithm
    * Build Heap
      * Heapify for all nodes
      * O(n * log n) algorithm
  * Priority Queues
  * Hash Maps
    * External Chaining
      * LinkedList
      * BST
      * AVL
    * Probing
      * Linear
      * Quadratic
  * SkipLists

### Test 3

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
     ```java
     public void dfs(List list, Vertex vertex, Graph graph) {
        list = new ArrayList();
        list.add(vertex);
        List edges = graph.adjList().get(vertex);
        for (Edge edge : edges) {
           Vertex end = edge.V;
           if (!list.contains(end)) {
              dfs(list, end, graph);
           }
        }
     }
     ```
     * ```DFS(list, vertex, graph``` visits all the vertices and edges in the connected component of ```vertex```.
     * All the edges and vertices visited by ```DFS(list, vertex, graph``` form a spanning tree of the connected component of ```vertex```.
