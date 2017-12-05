# 1332 Final Exam

## Content
### First part of Exam
* All Multiple Choice
* Test 1, 2, 3

### Second Part of Exam
* Graph Algorithms (coding)
* String Searching (coding)
* Diagram LCS
* Floyd-Warshaw (maybe diagram)
* Dynamic Programming
    * Fibonacci
* Huffman Coding

## Material
### Test 1
  * Arrays
    * Arrays are data structures built into Java
    * Once you define their size they cannot be resized
    * Insertion is O(n) because you have to move everything back
      * From back, it's O(1). (Best case)
    * Deletion is O(n) because you have to move everything forward
      * From back, it's O(1). (Best case)
    * Search is O(1) because you just use the index
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
    * Big O
      * Get: O(n) have to iterate through the list  
      * Search: O(n) same reason for get
      * Add (to end): O(1) (all)
      * Add (at index): O(n) (all)
      * Add (to begining): O(1) (all)
      * Delete (from end): O(n) (singly) / O(1) (doubly)
      * Delete (at index): O(n) (all)
      * Delete (from beginning): O(1) (all)
    * Circular
      * Can either be singularly or doubly linked.
      * Based on the linking, adding and removing is the same.
      
 * Stacks
    * ADT that follows LIFO (last-in-first-out).
    * Can only access data at the top of the stack.
    * Array-Backed:
      * Add to the back and remove from the back of the array.
      * Variable keeps track of the index of the top element as well as the size.
      ```java
      Object[] arr;
      int size;
      
      public void push(Object o) {
         if (arr.length == size) {
            resize(); //or throw an exception (implementation defined)
         }
         arr[size] = o;
         size++;
      }
      
      public Object pop() {
         size--;
         Object item = arr[size];
         arr[size] = null;
         return item;
      }
      ```
### Second Part
   * Graphs:
      * A subgraph of a graph is a graph where all its vertices and edges are a subset of the original graph's edges and vertices.
      * A spanning subgraph of a graph is a graph which has all the vertices of the original graph, but its edges are still a subset of the original graph's edges.
      * A connected graph has a path between every pair of vertices.
      * **Forest:** An undirected graph with no cycles.
      * **Tree:** A forest, but all the vertices are connected.
      * Depth First Search:
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
