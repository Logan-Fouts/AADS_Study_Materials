# Chapter 8 (The Disjoint Set Class)
## 8.1 Equivalence Relations
- **Efficient Data Structure for Equivalence Problem**: Describes a simple, yet fast data structure for solving equivalence, notable for its easy implementation and efficient operation, utilizing just a simple array for constant average time per operation.

- **Running Time Analysis**: The analysis of the running time for this fast implementation is challenging, indicating the data structure's unique theoretical interest due to the unusual form of its worst-case scenario.

- **Equivalence Relations Explained**: An equivalence relation is defined as a relation that satisfies three specific properties:
  - **Reflexive**: Every element is related to itself.
  - **Symmetric**: If one element is related to another, then the second is related to the first.
  - **Transitive**: If an element is related to a second, which in turn is related to a third, then the first element is related to the third.

- **Examples of Equivalence Relations**:
  - **Electrical Connectivity**: Described as an equivalence relation because if one component is electrically connected to another, the connection is mutual, and if a chain of connections exists, the start and end components are connected.
  - **Geographic Location**: Cities or towns within the same country are considered equivalent, showcasing another instance of an equivalence relation.
  - **Road Travel**: The relation between towns connected by two-way roads is an equivalence relation due to the ability to travel mutually between them.
## 8.2 The Dynamic Equivalence Problem
- The equivalence class of an element a ∈ S is the subset of S that contains all the elements that are related to a.
- **Dynamic Equivalence Problem**: Focuses on deciding if two elements are equivalent under a given relation, challenging due to usually implicit relation definitions.
- **Equivalence Relation**: Defined by reflexivity, symmetry, and transitivity, with examples provided to illustrate both equivalence and non-equivalence relations.
- **Equivalence Classes**: Describes how each element belongs to a subset containing all elements it's related to, forming a partition of the set, which simplifies checking for equivalence.
- **Disjoint Set Strategy**: Initially, each element forms its own set, representing no relations. The strategy involves two operations: `find` (determines the set containing an element) and `union` (merges sets containing two elements into one, maintaining disjointness).
- **Union-Find Algorithm**: Dynamic as sets change over time, must operate ==online==, providing immediate responses for `find` operations. Differentiates from ==offline== algorithms that process all operations before providing responses.
	- Example: Written test is offline, Speaking test is online (you must answer the current question before moving one)
- **Efficiency Strategies**: Discusses maintaining equivalence class names in an array for fast `find` operations, and optimizing `union` operations by linking smaller equivalence classes to larger ones, aiming for efficient overall performance.
- **Application and Performance**: Mentions the importance in graph theory and compilers, with a focus on achieving efficient `find` or `union` operations but not both simultaneously in constant worst-case time.
- There are two strategies to solve this problem. One ensures that the find instruction can be executed in constant worst-case time, and the other ensures that the union instruction can be executed in constant worst-case time. It has been shown that both cannot be done simultaneously in constant worst-case time.

> [!Disjoint Set Time Complexity]
> - ***Needs clarification:***
> 	- For quick find a sequence of N − 1 unions (the maximum, since then everything is in one set) would take Θ($N^2$) time.
> 	- If we also keep track of the size of each equivalence class, and when performing unions we change the name of the smaller equivalence class to the larger, then the total time spent for N − 1 merges is O(N log N).
> 	- Organizing elements into linked lists based on their equivalence class. This method improves update times by avoiding full array searches but doesn't inherently reduce asymptotic running time. The breakthrough comes with tracking the size of each equivalence class and preferring to merge smaller classes into larger ones during union operations. This strategy ensures that an element's class can change at most log⁡ N times, leading to a total time of O(N log⁡ N) for N−1 merges. The approach balances the cost of find and union operations, aiming for an overall running time slightly over O(M+N) for M finds and N−1 unions.
## 8.3 Basic Data Structure
- The problem requires that `find` operations on any two elements return the same result if they are in the same set, without needing to return a specific name.
- Utilizes trees to represent sets, where all elements in a tree share the same root, simplifying set identification to checking root names.
- Initially, each set is a single-element tree, forming a forest with implicit representation in an array where each element points to its parent, and root elements point to themselves with a special marker (e.g., -1).
- Union operations merge two sets by linking the roots of their trees, aiming for constant time execution by adjusting parent pointers.
- The `find` operation's time complexity depends on the tree's depth, with potential for deep trees making `find` slow in the worst case.
- Discusses strategies to ensure efficient union operations without causing excessive `find` operation slowdowns, considering various models for analyzing average-case scenarios and their implications on the likelihood of merging larger trees.
## 8.4 Smart Union Algorithms
- **Union-By-Size Improvement**: Prioritizes merging smaller trees into larger ones to maintain shallower tree depths, enhancing efficiency.
- **Depth Limitation**: Ensures the maximum depth of any node does not exceed log N, enhancing find operation efficiency to O(log N).
- **Implementation Details**: Utilizes an array to track tree sizes, storing the negative size at each root, simplifying union operations without additional space requirements.
- **Union-By-Height Alternative**: Similar to union-by-size but tracks tree height instead, ensuring all trees have a maximum depth of O(log N) with straightforward implementation.
## 8.5 Path Compression
- **Path Compression Introduction**: Highlights path compression as an enhancement for the find operation in the union/find algorithm, independent of union strategies.
- **Operational Mechanism**: During find(x), path compression changes every node on the path from x to the root to directly point to the root, optimizing future accesses.
- **Compatibility with Union-By-Size**: Path compression works well with union-by-size, potentially speeding up operations by reducing tree depth and improving access times.
- **Union-By-Height and Path Compression**: Notes a compatibility issue with union-by-height due to path compression altering tree heights, leading to a preference for union-by-rank as an efficient alternative.
## 8.7 An Application
- **Maze Generation Example**: Illustrates maze creation using the union/find structure, where cells are initially separated by walls.
- **Algorithm Overview**: Begins with a fully walled maze except for entrance/exit, then randomly removes walls between unconnected cells until all cells are interconnected, ensuring one large connected maze.
- **Union/Find Application**: Utilizes union/find to track connected cells, ensuring walls are only removed to connect disjoint sets, preventing unnecessary wall removal between already connected cells.
- **Process Visualization**: Demonstrates through a 5x5 maze example, initially placing each cell in its own set, then progressively merging sets as walls are removed to connect cells.
- **Algorithm Conclusion**: Completes when all cells are reachable from any other, marked by all cells being in a single set, generating a complex maze with multiple paths.
- **Efficiency and Running Time**: The running time is influenced by union/find operations, with the number of find operations roughly between 2N to 4N for N cells, leading to an efficient O(N log* N) running time for maze generation.
## Summary
- Exercises 355 Summary We have seen a very simple data structure to maintain disjoint sets. When the union operation is performed, it does not matter, as far as correctness is concerned, which set retains its name. A valuable lesson that should be learned here is that it can be very important to consider the alternatives when a particular step is not totally specified. The union step is flexible; by taking advantage of this, we are able to get a much more efficient algorithm. Path compression is one of the earliest forms of self-adjustment, which we have seen elsewhere (splay trees, skew heaps). Its use is extremely interesting, especially from a theoretical point of view, because it was one of the first examples of a simple algorithm with a not-so-simple worst-case analysis.
# Chapter 2 (Algorithm Analysis)
- **Definition of an Algorithm:**
	- A set of clearly defined, simple instructions to solve a problem.
	- It must be correct and the resource requirements (time, space) should be reasonable.
	- Algorithms needing excessive resources, like a year or hundreds of gigabytes of memory, are impractical.
## 2.2 (Model)
- ![[Pasted image 20240227193557.png]]
- ![[Pasted image 20240227193754.png]]
	- These are just describing the bounds for each notation. Big Oh, Omega, Theta, and little-o
	- The idea of these definitions is to establish a relative order among functions. Given two functions, there are usually points where one function is smaller than the other function, so it does not make sense to claim, for instance, $f(N) < g(N)$. Thus, we compare their relative rates of growth.
	- When we say that T(N) = O(f(N)), we are guaranteeing that the function T(N) grows at a rate no faster than f(N); thus f(N) is an upper bound on T(N). Since this implies that $f(N) = Ω(T(N))$, we say that T(N) is a lower bound on f(N). 
	- As an example, $N^3$ grows faster than $N^2$ , so we can say that $N^2 = O(N^3 )$ $or $N^3 = Ω(N^2)$
- ![[Pasted image 20240227194423.png]]
# Chapter 3 (Lists, Stacks, Queues)
## Abstract Data Types (ADTs)
- Defines a set of operations without specifying their implementation.
- Lists, sets, and graphs can be viewed as ADTs.
- Key operations for a set ADT might include add, remove, and contains.

## Lists
- **Introduction to Lists**: Conceptual foundation of linear arrangements of elements.
- **Implementations**: 
  - **Array-based lists**: Fixed-size and dynamic resizing strategies, advantages, and limitations.
  - **Linked lists**: Singly linked lists, doubly linked lists, and circular linked lists with their operations (insertion, deletion, traversal).
- **Java Collections Framework (JCF)**: Overview of the List interface and its implementations in Java (`ArrayList`, `LinkedList`).
- **Applications**: Use cases in software development, such as managing ordered collections of objects.

## Stacks
- **Concept and Properties**: LIFO (Last-In-First-Out) principle for element access.
- **Implementations**:
  - **Array-based stacks**: Managing stack operations with arrays, handling capacity issues.
  - **Linked-list stacks**: Using nodes for flexible stack management without size limitations.
- **Key Operations**: `push()`, `pop()`, `peek()`, and utility methods like `isEmpty()`.
- **Applications**: Expression evaluation, backtracking algorithms, function call management in programming languages.

## Queues
- **Concept and Properties**: FIFO (First-In-First-Out) principle for element processing.
- **Implementations**:
  - **Array-based queues**: Circular queue design to efficiently use array space.
  - **Linked-list queues**: Nodes to flexibly manage queue elements.
- **Key Operations**: `enqueue()`, `dequeue()`, `front()`, and `isEmpty()`.
- **Specialized Queues**:
  - **Priority Queues**: Managing elements based on priority rather than insertion order.
  - **Dequeues (Double-Ended Queues)**: Allowing insertion and deletion at both ends.
- **Applications**: Scheduling, buffering, and resource management in computing systems.
# Chapter 5 (Hashing)
- **Hash Table ADT**: Unlike the search tree ADT discussed in Chapter 4 that supports various operations, the hash table ADT limits the set of operations that can be performed on elements.
- **Hashing Technique**: Hashing is an implementation technique for hash tables, aiming for constant average time complexity for insertions, deletions, and searches.
- **Limited Operations**: Hash tables do not efficiently support operations that require element ordering, such as finding the minimum or maximum elements or printing all elements in sorted order.
## 5.1 General Idea
- **Hash Table Structure**: The ideal hash table is simply an array with a fixed size, containing items. Each item includes a key (used for searching) and possibly other data fields.
- **Key Role**: The key is a part of the item used for search operations. For example, an item might be an employee record where the employee's ID number is the key, and the record contains other information like the employee's name.
- **Hash Function**: Each key is mapped to a number within the 0 to `TableSize - 1` range by a hash function. The hash function should ideally be easy to compute and distribute keys uniformly across the hash table to avoid collisions.
- **Core Idea of Hashing**: The fundamental concept involves mapping keys to array indices using a hash function.
- **Primary Challenges**:
  - **Choosing a Hash Function**: Selecting a function that minimizes collisions and is computationally efficient.
  - **Collision Handling**: Determining a strategy to address the issue when multiple keys hash to the same value.
  - **Table Size Determination**: Deciding on the size of the hash table, balancing space efficiency with the need to minimize collisions.
## 5.2 Hash Function
- **Integer Keys Hashing**: If keys are integers, a simple modulo operation (`Key mod TableSize`) is commonly used as the hash function. This can be effective unless the keys have patterns that conflict with the table size.
- **Table Size and Prime Numbers**: To prevent clustering and uneven distribution, especially in cases where keys might form patterns (like all ending in zero), it's recommended to use a prime number for `TableSize`.
- **String Keys Hashing**: For string keys, hash functions must be more carefully designed. A basic approach might involve summing the ASCII values of the characters. However, this method may not distribute keys evenly, particularly for large tables.
- **Overflow in Hashing**: When computing hash values, overflow is permissible and can be accounted for to ensure the final hash value is positive and within the required range.
- **Efficiency vs. Distribution**: When keys are long, hashing every character can be computationally expensive. A common compromise is to hash a subset of characters to save time, even if it means a slight reduction in distribution evenness.
- **Collision Resolution**: When two elements hash to the same value (collision), it must be resolved. The text discusses two primary methods: separate chaining and open addressing, and hints at other advanced techniques.
- **Separate Chaining and Open Addressing**: These are basic strategies for handling collisions. Separate chaining uses a linked list to manage collisions at each hash table index, while open addressing finds the next available slot in the table for the colliding item.
- **Practical Hash Function Design**: The hash function might be tailored to the key's structure, such as using parts of a street address, city, and ZIP code for more complex keys like full addresses. Some may choose to hash characters at odd positions for efficiency at the expense of perfect distribution.
## 5.3 Separate Chaining
- **Separate Chaining Overview**: The strategy known as separate chaining resolves hash collisions by maintaining a list of all elements that hash to the same value.
- **List Implementation**: Standard library list implementations, such as doubly linked lists, are used, but for space efficiency, simpler list structures may be preferable.
- **Search and Insert Operations**: Searching involves hashing the key to identify the correct list to traverse. Insertions check for the element's presence; if not found, the element is inserted at the front of the list for convenience and because new elements might be accessed again soon.
- **Handling Duplicates**: If duplicates are expected, a separate field is kept to account for the number of occurrences, avoiding the insertion of the same element multiple times.
- **Load Factor and Search Cost**: The load factor (λ) is the ratio of elements to table size. For separate chaining, keeping λ around 1 is typical, meaning the table size is close to the number of elements expected. The cost of searching depends on λ, with unsuccessful searches averaging λ nodes to examine and successful ones examining about 1 + (λ/2) nodes.
- **Table Expansion and Prime Size**: When the load factor exceeds 1, a `rehash` function is called to expand the table, discussed in a later section. It is also recommended to use a prime number for the table size to maintain good key distribution.
## 5.4 Hashing Tables Without Linked Lists
- **Linked List Disadvantages**: Separate chaining uses linked lists, which may slow down the algorithm due to the overhead of allocating new list nodes. It also adds the complexity of managing an additional data structure.
- **Alternative to Linked Lists**: As an alternative to using linked lists for collision resolution, probing hash tables try sequential cells until an empty one is found, following a defined sequence.
- **Probing Sequence**: The probing sequence is determined by a set of functions h0(x), h1(x), h2(x), ..., where hi(x) is calculated as `(hash(x) + f(i)) mod TableSize` and f(0) = 0. The function f represents the collision resolution strategy.
- **Table Size and Load Factor**: Probing hash tables require a larger table size compared to separate chaining hash tables to minimize collisions. The load factor, denoted by λ, is generally recommended to be kept below 0.5 for these tables, which do not use separate chaining.
- **Probing Hash Tables**: These tables utilize probing strategies for collision resolution and hence are termed probing hash tables. They are efficient in space utilization since all data is stored within the table itself, but require careful management to avoid excessive collisions. 
### 5.4.1 Linear Probing
- **Linear Probing**: Separate chaining's alternative, linear probing, uses a linear function for collision resolution where sequential cells (with wraparound) are tried to find an empty spot. 
- **Function \( f(i) \)**: For linear probing, \( f(i) \) is typically \( i \), indicating that the cells \( h_0(x), h_1(x), h_2(x), ... \) are probed in order. 
- **Primary Clustering**: A phenomenon where occupied cells form blocks, making any new key hashing into the cluster require multiple attempts to resolve the collision, thus increasing it.
- **Probe Expectations**: 
	- **Insertions and Unsuccessful Searches**: Approximately $\frac{1}{2} \left(1 + \frac{1}{(1 - \lambda)^2}\right)$ probes are needed.
	- **Successful Searches**: Roughly $\frac{1}{2} \left(1 + \frac{1}{(1 - \lambda)}\right)$ probes are needed. This suggests that, on average, successful searches should be quicker than unsuccessful ones.
- **Formulas under Ideal Conditions**: Assuming no clustering and independence between probes, the expected probes for an unsuccessful search is $\frac{1}{1 - \lambda}$. For a successful search, it's the same as during insertion.
- **Performance Issues**: Clustering can severely affect performance in practice, not just theoretically. For instance, if \( \lambda = 0.75 \), linear probing might expect 8.5 probes per insertion. At \( \lambda = 0.9 \), the expected probes rise to 50, which is not practical.
- **Probing Efficiency**: Linear probing is effective when the table is less than half full ( \( \lambda = 0.5 \) ), needing an average of 2.5 probes for insertion and 1.5 for a successful search. However, the strategy becomes less efficient as the table fills beyond this point.
### 5.4.2 Quadratic Probing
- **Quadratic Probing Advantage**: This method resolves the primary clustering issue found in linear probing by using a quadratic function for collision resolution, generally \( f(i) = i^2 \).
- **Collision Resolution with Quadratic Probing**: The quadratic function attempts cells at a distance of \( i^2 \) from the initial collision, leading to a spread-out pattern of probes that avoids clustering.
- **Limitations of Full Tables**: Quadratic probing does not guarantee finding an empty cell once the table exceeds half full, particularly if the table size is not prime.
- **Guarantee of Insertion**: A theorem states that if the table size is prime and at least half empty, an insertion can always be performed using quadratic probing.
- **Importance of Prime Table Size**: Having a prime table size ensures that the sequence of probes covers a significant portion of the table, preventing early repeat probes that can happen with non-prime table sizes.
- **Standard Deletion Issues**: Deletion in probing hash tables isn't straightforward because removing an item might disrupt the probe sequence. Lazy deletion, marking entries as deleted without actually removing them, is often used instead.
- **Table Fullness and Rehashing**: When the load factor exceeds 0.5, meaning the table is more than half full, rehashing is triggered to expand the table and redistribute the elements.
- **Secondary Clustering**: Although quadratic probing solves primary clustering, secondary clustering can still occur when multiple keys hash to the same starting index.
- **Eliminating Secondary Clustering**: This can be avoided by computing an additional hash function, although this increases the computational complexity of the hash function.
### 5.4.3 Double Hashing
- **Double Hashing Overview**: Double hashing is a collision resolution method designed to overcome linear probing's primary clustering problem by using a secondary hash function.
- **Collision Function for Double Hashing**: The secondary hash function is typically $f(i) = i * {hash_2}(x)$, where the next cell to probe is determined by the distance ${hash_2}(x), 2{hash_2}(x)$, etc.
- **Requirements for hash2**: The secondary hash function must never evaluate to zero, and all table cells should be reachable. A common function is ${hash_2}(x) = R - (x \mod R)$, with R being a prime number less than the table size.
- **Prime Table Size Importance**: Using a prime number for table size ensures that all cells can be probed, which is not guaranteed if the table size is not prime.
- **Guarantee of Insertion with Prime Size**: If the table size is prime and the table is at least half empty, double hashing guarantees that a new element can always be inserted.
- **Rehashing When Full**: If the number of elements exceeds half the table size, the table is rehashed to a larger size to maintain efficiency.
- **Secondary Clustering in Double Hashing**: Although double hashing avoids primary clustering, elements that hash to the same initial position can still probe the same alternative cells, known as secondary clustering.
- **Double Hashing Efficiency**: Simulations suggest that double hashing has a similar number of expected probes to a random collision resolution strategy, making it theoretically attractive.
- **Comparison with Quadratic Probing**: Quadratic probing is likely simpler and faster in practice, especially for complex keys such as strings where hash functions are costly to compute, since it does not require a secondary hash function.
## 5.5 Rehashing
- **Open Addressing and Full Tables**: When using open addressing with quadratic resolution, operations can become inefficient and insertions may fail if the hash table becomes too full, especially after numerous deletions and insertions.
- **Rehashing Solution**: To address this issue, rehashing involves creating a new table approximately twice the size of the original, utilizing a new hash function. This process involves re-computing hash values for each non-deleted element and inserting them into the new table.
- **New Table Creation**: The new table, selected to be of size 17 (a prime number for better distribution), uses a revised hash function \( h(x) = x \mod 17 \). All active elements from the old table are then rehashed and inserted into this new table.
- **Interactive Systems Impact**: In interactive systems, the user triggering a rehash might experience noticeable slowdowns, as the process can momentarily affect performance.
- **Rehashing Strategies with Quadratic Probing**:
	- **Early Rehashing**: Some implementations rehash when the table is half full to prevent performance degradation.
	- **Rehashing on Failure**: Others wait to rehash only when an insertion actually fails.
	- **Load Factor-Based Rehashing**: A balanced approach involves rehashing when the table reaches a predefined load factor, helping maintain good performance without frequent rehashing.