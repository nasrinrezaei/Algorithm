# Algorithm
## Algorithm efficiency assessment

Complexity analysis reflects the relationship between the time and space resources required for algorithm execution and the size of the input data. It describes the trend of growth in the time and space required by the algorithm as the size of the input data increases
This definition might sound complex, but we can break it down into three key points to understand it better.

. "Time and space resources" correspond to time complexity and space complexity, respectively.

."As the size of input data increases" means that complexity reflects the relationship between algorithm efficiency and the volume of input data.

."The trend of growth in time and space" indicates that complexity analysis focuses not on the specific values of runtime or space occupied but on the "rate" at which time or space grows.

Complexity analysis overcomes the disadvantages of actual testing methods, reflected in the following aspects:

. It is independent of the testing environment and applicable to all operating platforms.

. It can reflect algorithm efficiency under different data volumes, especially in the performance of algorithms with large data volumes.

###  Iteration

Iteration is a control structure for repeatedly performing a task. In iteration, a program repeats a block of code as long as a certain condition is met until this condition is no longer satisfied.

1. For loops

      The for loop is one of the most common forms of iteration, and it's particularly suitable when the number of iterations is known in advance.
      
      ```ruby
      def for_loop(n: int) -> int:
          """for loop"""
          res = 0
          # Loop sum 1, 2, ..., n-1, n
          for i in range(1, n + 1):
              res += i
          return res
      ```
      
      The number of operations in this summation function is proportional to the size of the input data 
      , or in other words, it has a linear relationship. This "linear relationship" is what time complexity describes.

2. While loops

      Similar to for loops, while loops are another approach for implementing iteration. In a while loop, the program checks a condition at the beginning of each iteration; if the condition is true, the execution continues, otherwise, the loop ends.
      
      ```ruby
      def while_loop(n: int) -> int:
          """while loop"""
          res = 0
          i = 1  # Initialize condition variable
          # Loop sum 1, 2, ..., n-1, n
          while i <= n:
              res += i
              i += 1  # Update condition variable
          return res
      ```
      
      while loops provide more flexibility than for loops, especially since they allow for custom initialization and modification of the condition variable at each step.
      
      Overall, for loops are more concise, while while loops are more flexible. Both can implement iterative structures. Which one to use should be determined based on the specific requirements of the problem.

3. Nested loops

      We can nest one loop structure within another. Below is an example using for loops:
      
      ```ruby
      def nested_for_loop(n: int) -> str:
          """Double for loop"""
          res = ""
          # Loop i = 1, 2, ..., n-1, n
          for i in range(1, n + 1):
              # Loop j = 1, 2, ..., n-1, n
              for j in range(1, n + 1):
                  res += f"({i}, {j}), "
          return res
      ```
      
      In such cases, the number of operations of the function is proportional to 
      , meaning the algorithm's runtime and the size of the input data 
       has a 'quadratic relationship.'
    
    We can further increase the complexity by adding more nested loops, each level of nesting effectively "increasing the dimension," which raises the time complexity to "cubic," "quartic," and so on.

### Recursion

Recursion is an algorithmic strategy where a function solves a problem by calling itself. It primarily involves two phases:

1. Calling: This is where the program repeatedly calls itself, often with progressively smaller or simpler arguments, moving towards the "termination condition."

2. Returning: Upon triggering the "termination condition," the program begins to return from the deepest recursive function, aggregating the results of each layer.

From an implementation perspective, recursive code mainly includes three elements.

1. Termination Condition: Determines when to switch from "calling" to "returning."
2. Recursive Call: Corresponds to "calling," where the function calls itself, usually with smaller or more simplified parameters.
3. Return Result: Corresponds to "returning," where the result of the current recursion level is returned to the previous layer.

```ruby
def recur(n: int) -> int:
    """Recursion"""
    # Termination condition
    if n == 1:
        return 1
    # Recursive: recursive call
    res = recur(n - 1)
    # Return: return result
    return n + res
```

Although iteration and recursion can achieve the same results from a computational standpoint, they represent two entirely different paradigms of thinking and problem-solving.

  . Iteration: Solves problems "from the bottom up." It starts with the most basic steps, and then repeatedly adds or accumulates these steps until the task is complete.

  . Recursion: Solves problems "from the top down." It breaks down the original problem into smaller sub-problems, each of which has the same form as the original problem. These sub-problems are then further decomposed into even smaller sub-problems, stopping at the base case whose solution is known.

  1. Call stack

     Every time a recursive function calls itself, the system allocates memory for the newly initiated function to store local variables, the return address, and other relevant information. This leads to two primary outcomes.

     . The function's context data is stored in a memory area called "stack frame space" and is only released after the function returns. Therefore, recursion generally consumes more memory space than iteration.

     . Recursive calls introduce additional overhead. Hence, recursion is usually less time-efficient than loops.

     In practice, the depth of recursion allowed by programming languages is usually limited, and excessively deep recursion can lead to stack overflow errors.

  2. Tail recursion

     Interestingly, if a function performs its recursive call as the very last step before returning, it can be optimized by the compiler or interpreter to be as space-efficient as iteration. This scenario is known as tail recursion.

     . Regular recursion: In standard recursion, when the function returns to the previous level, it continues to execute more code, requiring the system to save the context of the previous call.

     . Tail recursion: Here, the recursive call is the final operation before the function returns. This means that upon returning to the previous level, no further actions are needed, so the system does not need to save the context of the previous level.

       ```ruby
              def tail_recur(n, res):
          """Tail recursion"""
          # Termination condition
          if n == 0:
              return res
          # Tail recursive call
          return tail_recur(n - 1, res + n)
        ```

     . Regular recursion: The summation operation occurs during the "returning" phase, requiring another summation after each layer returns.

     . Tail recursion: The summation operation occurs during the "calling" phase, and the "returning" phase only involves returning through each layer.

     > [!TIP]
     > Note that many compilers or interpreters do not support tail recursion optimization. For example, Python does not support tail recursion optimization by default, so even if the function is in the form of tail recursion, it may still encounter stack overflow issues.

  3.  Recursion tree

      When dealing with algorithms related to "divide and conquer", recursion often offers a more intuitive approach and more readable code than iteration. Take the "Fibonacci sequence" as an example.

        ```ruby
            def fib(n: int) -> int:
            """Fibonacci sequence: Recursion"""
            # Termination condition f(1) = 0, f(2) = 1
            if n == 1 or n == 2:
                return n - 1
            # Recursive call f(n) = f(n-1) + f(n-2)
            res = fib(n - 1) + fib(n - 2)
            # Return result f(n)
            return res
        ```
       Observing the above code, we see that it recursively calls two functions within itself, meaning that one call generates two branching calls.

      undamentally, recursion embodies the paradigm of "breaking down a problem into smaller sub-problems." This divide-and-conquer strategy is crucial.

        . From an algorithmic perspective, many important strategies like searching, sorting, backtracking, divide-and-conquer, and dynamic programming directly or indirectly use this way of thinking.

        . From a data structure perspective, recursion is naturally suited for dealing with linked lists, trees, and graphs, as they are well suited for analysis using the divide-and-conquer approach.

## Time complexity

The runtime can intuitively assess the efficiency of an algorithm. How can we accurately estimate the runtime of a piece of an algorithm?

1. Determining the Running Platform: This includes hardware configuration, programming language, system environment, etc., all of which can affect the efficiency of code execution.
2. Evaluating the Run Time for Various Computational Operations: For instance, an addition operation + might take 1 ns, a multiplication operation * might take 10 ns, a print operation print() might take 5 ns, etc.
3. Counting All the Computational Operations in the Code: Summing the execution times of all these operations gives the total run time.

For example, consider the following code with an input size of n:
```ruby
 # Under an operating platform
 def algorithm(n: int):
 a = 2      # 1 ns
 a = a + 1  # 1 ns
 a = a * 2  # 10 ns
 # Cycle n times
for _ in range(n):  # 1 ns
print(0)        # 5 ns
```
Using the above method, the run time of the algorithm can be calculated as (6n+12)ns:

However, in practice, counting the run time of an algorithm is neither practical nor reasonable. First, we don't want to tie the estimated time to the running platform, as algorithms need to run on various platforms. Second, it's challenging to know the run time for each type of operation, making the estimation process difficult.

### Assessing time growth trend

Time complexity analysis does not count the algorithm's run time, but rather the growth trend of the run time as the data volume increases.

Let's understand this concept of "time growth trend" with an example. Assume the input data size is 
n, and consider three algorithms A, B, and C:

```ruby
# Time complexity of algorithm A: constant order
def algorithm_A(n: int):
    print(0)
# Time complexity of algorithm B: linear order
def algorithm_B(n: int):
    for _ in range(n):
        print(0)
# Time complexity of algorithm C: constant order
def algorithm_C(n: int):
    for _ in range(1000000):
        print(0)
```

. Algorithm A has just one print operation, and its run time does not grow with n. Its time complexity is considered "constant order."

. Algorithm B involves a print operation looping n times, and its run time grows linearly with n. Its time complexity is "linear order."

. Algorithm C has a print operation looping 1,000,000 times. Although it takes a long time, it is independent of the input data size n. Therefore, the time complexity of C is the same as A, which is "constant order."

 > [!TIP]
     > For example, although algorithms A and C have the same time complexity, their actual run times can be quite different. Similarly, even though algorithm B has a higher time complexity than C, it is clearly superior when the input data size n is small. In these cases, it's difficult to judge the efficiency of algorithms based solely on time complexity. Nonetheless, despite these issues, complexity analysis remains the most effective and commonly used method for evaluating algorithm efficiency.

1. Constant order O(1):

   Constant order means the number of operations is independent of the input data size n. In the following function, although the number of operations size might be large, the time 
   complexity remains O(1) as it's unrelated to n:

   ```ruby
   def constant(n: int) -> int:
   """Constant complexity"""
   count = 0
   size = 100000
   for _ in range(size):
   count += 1
   return count
   ```

2. Linear order O(n)

   Linear order indicates the number of operations grows linearly with the input data size n. Linear order commonly appears in single-loop structures:

   
   ```ruby
   def linear(n: int) -> int:
         """Linear complexity"""
         count = 0
         for _ in range(n):
               count += 1
                return count
   ```
3. Quadratic order O(n*n)

   Quadratic order means the number of operations grows quadratically with the input data size n. Quadratic order typically appears in nested loops, where both the outer and inner loops 
   have a time complexity of O(n), resulting in an overall complexity of O(n*n)

      
   ```ruby
   def quadratic(n: int) -> int:
    """Quadratic complexity"""
    count = 0
    # Loop count is squared in relation to the data size n
    for i in range(n):
        for j in range(n):
            count += 1
    return count
   ```
For instance, in bubble sort, the outer loop runs  n-1 For instance, in bubble sort, the outer loop runs n-1, n-2,..., 2, 1 times, averaging n/2 times, resulting in a time complexity of O((n-1)n/2) = O(n*n) 
      
   ```ruby
 def bubble_sort(nums: list[int]) -> int:
    """Quadratic complexity (bubble sort)"""
    count = 0  # Counter
    # Outer loop: unsorted range is [0, i]
    for i in range(len(nums) - 1, 0, -1):
        # Inner loop: swap the largest element in the unsorted range [0, i] to the right end of the range
        for j in range(i):
            if nums[j] > nums[j + 1]:
                # Swap nums[j] and nums[j + 1]
                tmp: int = nums[j]
                nums[j] = nums[j + 1]
                nums[j + 1] = tmp
                count += 3  # Element swap includes 3 individual operations
    return count
   ```
4. Exponential order O(2^n)

   Biological "cell division" is a classic example of exponential order growth: starting with one cell, it becomes two after one division, four after two divisions, and so on, resulting 
   in  2^n cells after n divisions.

      ```ruby
      def exponential(n: int) -> int:
          """Exponential complexity (loop implementation)"""
          count = 0
          base = 1
          # Cells split into two every round, forming the sequence 1, 2, 4, 8, ..., 2^(n-1)
          for _ in range(n):
              for _ in range(base):
                  count += 1
              base *= 2
          # count = 1 + 2 + 4 + 8 + .. + 2^(n-1) = 2^n - 1
          return count
   ```
   In practice, exponential order often appears in recursive functions. For example, in the code below, it recursively splits into two halves, stopping after n
 divisions:

      ```ruby
      def exp_recur(n: int) -> int:
          """Exponential complexity (recursive implementation)"""
          if n == 1:
              return 1
          return exp_recur(n - 1) + exp_recur(n - 1) + 1
   ```

   Exponential order growth is extremely rapid and is commonly seen in exhaustive search methods (brute force, backtracking, etc.). For large-scale problems, exponential order is unacceptable, often requiring dynamic programming or greedy algorithms as solutions.

   5.  Logarithmic order O(logn)
  
      In contrast to exponential order, logarithmic order reflects situations where "the size is halved each round." Given an input data size n, since the size is halved each round, the number of iterations is logn, the inverse function of n^2.

         ```ruby
            def logarithmic(n: int) -> int:
          """Logarithmic complexity (loop implementation)"""
          count = 0
          while n > 1:
              n = n / 2
              count += 1
          return count
    ```
Like exponential order, logarithmic order also frequently appears in recursive functions. The code below forms a recursive tree of height logn

         ```ruby
                 def log_recur(n: int) -> int:
                """Logarithmic complexity (recursive implementation)"""
                if n <= 1:
                    return 0
                return log_recur(n / 2) + 1
    ```

    Logarithmic order is typical in algorithms based on the divide-and-conquer strategy, embodying the "split into many" and "simplify complex problems" approach. It's slow-growing and is the most ideal time complexity after constant order.

6.  Linear-logarithmic order O(n logn)
   Linear-logarithmic order often appears in nested loops, with the complexities of the two loops being O(logn) and O(n) respectively. The related code is as follows:

        ```ruby
             def linear_log_recur(n: int) -> int:
                """Linear logarithmic complexity"""
                if n <= 1:
                    return 1
                count: int = linear_log_recur(n // 2) + linear_log_recur(n // 2)
                for _ in range(n):
                    count += 1
                return count
    ```

    Mainstream sorting algorithms typically have a time complexity of O(n logn), such as quicksort, mergesort, and heapsort.

7. Factorial order O(n!)
   Factorial order corresponds to the mathematical problem of "full permutation.

        ```ruby
             def factorial_recur(n: int) -> int:
          """Factorial complexity (recursive implementation)"""
          if n == 0:
              return 1
          count = 0
          # From 1 split into n
          for _ in range(n):
              count += factorial_recur(n - 1)
          return count
    ```

    Note that factorial order grows even faster than exponential order; it's unacceptable for larger n values.

## Space complexity

Space complexity is used to measure the growth trend of the memory space occupied by an algorithm as the amount of data increases. This concept is very similar to time complexity, except that "running time" is replaced with "occupied memory space".

# Space related to algorithms

The memory space used by an algorithm during its execution mainly includes the following types.

. Input space: Used to store the input data of the algorithm.
. Temporary space: Used to store variables, objects, function contexts, and other data during the algorithm's execution.
. Output space: Used to store the output data of the algorithm.

Generally, the scope of space complexity statistics includes both "Temporary Space" and "Output Space".

Temporary space can be further divided into three parts
. Temporary data: Used to save various constants, variables, objects, etc., during the algorithm's execution.
. Stack frame space: Used to save the context data of the called function. The system creates a stack frame at the top of the stack each time a function is called, and the stack frame space is released after the function returns.
. Instruction space: Used to store compiled program instructions, which are usually negligible in actual statistics.

# Calculation method

The method for calculating space complexity is roughly similar to that of time complexity, with the only change being the shift of the statistical object from "number of operations" to "size of used space".

However, unlike time complexity, we usually only focus on the worst-case space complexity. This is because memory space is a hard requirement, and we must ensure that there is enough memory space reserved under all input data.

Consider the following code, the term "worst-case" in worst-case space complexity has two meanings.

1. Based on the worst input data: When  n<10, the space complexity is O(1); but when n>10 the initialized array nums occupies O(n) space, thus the worst-case space complexity is O(n).
2. Based on the peak memory used during the algorithm's execution: For example, before executing the last line, the program occupies O(1) space; when initializing the array nums , the program occupies O(n) space, hence the worst-case space complexity is O(n).

          ```ruby
             def algorithm(n: int):
          a = 0               # O(1)
          b = [0] * 10000     # O(1)
          if n > 10:
              nums = [0] * n  # O(n)
          ```
In recursive functions, stack frame space must be taken into count. Consider the following code:

     ```ruby
           def function() -> int:
    # Perform certain operations
    return 0

      def loop(n: int):
          """Loop O(1)"""
          for _ in range(n):
              function()
      
      def recur(n: int):
          """Recursion O(n)"""
          if n == 1:
              return
          return recur(n - 1)
          ```
The time complexity of both loop() and recur() functions is 
, but their space complexities differ.

. The loop() function calls function() n times in a loop, where each iteration's function() returns and releases its stack frame space, so the space complexity remains O(1).
. The recursive function recur() will have n instances of unreturned recur() existing simultaneously during its execution, thus occupying  O(n) stack frame space.

# Common types

1. Constant order O(1):
   Constant order is common in constants, variables, objects that are independent of the size of input data n.
   Note that memory occupied by initializing variables or calling functions in a loop, which is released upon entering the next cycle, does not accumulate over space, thus the space complexity remains O(1) :

          ```ruby
          def function() -> int:
          """Function"""
          # Perform some operations
          return 0
      
            def constant(n: int):
                """Constant complexity"""
                # Constants, variables, objects occupy O(1) space
                a = 0
                nums = [0] * 10000
                node = ListNode(0)
                # Variables in a loop occupy O(1) space
                for _ in range(n):
                    c = 0
                # Functions in a loop occupy O(1) space
                for _ in range(n):
                    function()
                ```
   2. Linear order O(n)
      Linear order is common in arrays, linked lists, stacks, queues, etc., where the number of elements is proportional to n:

          ```ruby
              def linear(n: int):
          """Linear complexity"""
          # A list of length n occupies O(n) space
          nums = [0] * n
          # A hash table of length n occupies O(n) space
          hmap = dict[int, str]()
          for i in range(n):
              hmap[i] = str(i)
                ```
      This function's recursive depth is n, meaning there are n instances of unreturned linear_recur() function, using O(n) size of stack frame space:
               ```ruby
        def linear_recur(n: int):
          """Linear complexity (recursive implementation)"""
          print("Recursive n =", n)
          if n == 1:
              return
          linear_recur(n - 1)
                ```
      3. Quadratic order O(n^2)
     
         Quadratic order is common in matrices and graphs, where the number of elements is quadratic to n:

             ```ruby
              /* Quadratic complexity */
                  void quadratic(int n) {
                      // A two-dimensional list occupies O(n^2) space
                      vector<vector<int>> numMatrix;
                      for (int i = 0; i < n; i++) {
                          vector<int> tmp;
                          for (int j = 0; j < n; j++) {
                              tmp.push_back(0);
                          }
                          numMatrix.push_back(tmp);
                      }
                  }
             ```
         the recursive depth of this function is n, and in each recursive call, an array is initialized with lengths n,n-1,n-2,...,2,1 averaging n/2 thus overall occupying O(n^2)  space:

             ```ruby
             def quadratic_recur(n: int) -> int:
                """Quadratic complexity (recursive implementation)"""
                if n <= 0:
                    return 0
                # Array nums length = n, n-1, ..., 2, 1
                nums = [0] * n
                return quadratic_recur(n - 1)
             ```

         4.  Exponential order O(2^n)
        
         Exponential order is common in binary trees. A "full binary tree" with n levels has 2^n-1 nodes, occupying O(2^n) space:

             ```ruby
             def build_tree(n: int) -> TreeNode | None:
                """Exponential complexity (building a full binary tree)"""
                if n == 0:
                    return None
                root = TreeNode(0)
                root.left = build_tree(n - 1)
                root.right = build_tree(n - 1)
                return root
                         ```
         5. Logarithmic order O(logn):

            Logarithmic order is common in divide-and-conquer algorithms. For example, in merge sort, an array of length n is recursively divided in half each round, forming a recursion tree of height logn, using O(logn) stack frame space.

## Balancing time and space

Ideally, we aim for both time complexity and space complexity to be optimal. However, in practice, optimizing both simultaneously is often difficult.
Lowering time complexity usually comes at the cost of increased space complexity, and vice versa. The approach of sacrificing memory space to improve algorithm speed is known as "space-time tradeoff"; the reverse is known as "time-space tradeoff".
The choice depends on which aspect we value more. In most cases, time is more precious than space, so "space-time tradeoff" is often the more common strategy. Of course, controlling space complexity is also very important when dealing with large volumes of data.

## Classification of data structures
Common data structures include arrays, linked lists, stacks, queues, hash tables, trees, heaps, and graphs. They can be classified into "logical structure" and "physical structure".

# Logical structure: linear and non-linear

The logical structures reveal the logical relationships between data elements. In arrays and linked lists, data are arranged in a specific sequence, demonstrating the linear relationship between data; while in trees, data are arranged hierarchically from the top down, showing the derived relationship between "ancestors" and "descendants"; and graphs are composed of nodes and edges, reflecting the intricate network relationship.

logical structures can be divided into two major categories: "linear" and "non-linear". Linear structures are more intuitive, indicating data is arranged linearly in logical relationships; non-linear structures, conversely, are arranged non-linearly.

. Linear data structures: Arrays, Linked Lists, Stacks, Queues, Hash Tables.
. Non-linear data structures: Trees, Heaps, Graphs, Hash Tables.

Non-linear data structures can be further divided into tree structures and network structures.
. Tree structures: Trees, Heaps, Hash Tables, where elements have a one-to-many relationship.
. Network structures: Graphs, where elements have a many-to-many relationships.

# Physical structure: contiguous and dispersed

During the execution of an algorithm, the data being processed is stored in memory. We can think of memory as a vast Excel spreadsheet, with each cell capable of storing a certain amount of data.

The system accesses the data at the target location by means of a memory address. The computer assigns a unique identifier to each cell in the table according to specific rules, ensuring that each memory space has a unique memory address. With these addresses, the program can access the data stored in memory.

> [!TIP]
     > It's worth noting that comparing memory to an Excel spreadsheet is a simplified analogy. The actual working mechanism of memory is more complex, involving concepts like address space, memory management, cache mechanisms, virtual memory, and physical memory.

Memory is a shared resource for all programs. When a block of memory is occupied by one program, it cannot be simultaneously used by other programs. Therefore, considering memory resources is crucial in designing data structures and algorithms. For instance, the algorithm's peak memory usage should not exceed the remaining free memory of the system; if there is a lack of contiguous memory blocks, then the data structure chosen must be able to be stored in non-contiguous memory blocks.

The physical structure reflects the way data is stored in computer memory and it can be divided into contiguous space storage (arrays) and non-contiguous space storage (linked lists). The two types of physical structures exhibit complementary characteristics in terms of time efficiency and space efficiency.

It is worth noting that all data structures are implemented based on arrays, linked lists, or a combination of both. For example, stacks and queues can be implemented using either arrays or linked lists; while implementations of hash tables may involve both arrays and linked lists.

. Array-based implementations: Stacks, Queues, Hash Tables, Trees, Heaps, Graphs, Matrices, Tensors.
. Linked-list-based implementations: Stacks, Queues, Hash Tables, Trees, Heaps, Graphs, etc.

Data structures implemented based on arrays are also called “Static Data Structures,” meaning their length cannot be changed after initialization. Conversely, those based on linked lists are called “Dynamic Data Structures,” which can still adjust their size during program execution

## Basic data types¶

When discussing data in computers, various forms like text, images, videos, voice and 3D models comes to mind. Despite their different organizational forms, they are all composed of various basic data types.

Basic data types are those that the CPU can directly operate on and are directly used in algorithms, mainly including the following.

. Integer types: byte, short, int, long.
. Integer types: byte, short, int, long.
. Character type: char, used to represent letters, punctuation, and even emojis in various languages.
. Boolean type: bool, used to represent "yes" or "no" decisions.

Basic data types are stored in computers in binary form. One binary digit is 1 bit. In most modern operating systems, 1 byte consists of 8 bits.

The range of values for basic data types depends on the size of the space they occupy. Below, we take Java as an example.
. The integer type byte occupies 1 byte = 8 bits and can represent 2^8 numbers.
. The integer type int occupies 4 bytes = 32 bits and can represen 2^32 numbers.

Every programming language has its own data type definitions, which might differ in space occupied, value ranges, and default values.
  . n Python, the integer type int can be of any size, limited only by available memory; the floating-point float is double precision 64-bit; there is no char type, as a single character is actually a string str of length 1.
  . C and C++ do not specify the size of basic data types, it varies with implementation and platform. The above table follows the LP64 data model, used for Unix 64-bit operating systems including Linux and macOS.

  So, what is the connection between basic data types and data structures? We know that data structures are ways to organize and store data in computers. The focus here is on "structure" rather than "data".
  If we want to represent "a row of numbers", we naturally think of using an array. This is because the linear structure of an array can represent the adjacency and the ordering of the numbers, but whether the stored content is an integer int, a decimal float, or a character char, is irrelevant to the "data structure".
  In other words, basic data types provide the "content type" of data, while data structures provide the "way of organizing" data.

  ## Array
  
  An array is a linear data structure that operates as a lineup of similar items, stored together in a computer's memory in contiguous spaces. It's like a sequence that maintains organized storage. Each item in this lineup has its unique 'spot' known as an index.

  ### Common operations on arrays

  1. Initializing arrays¶

      Arrays can be initialized in two ways depending on the needs: either without initial values or with specified initial values. When initial values are not specified, most programming 
      languages will set the array elements to 0:

       ```ruby
            # Initialize array
            arr: list[int] = [0] * 5  # [ 0, 0, 0, 0, 0 ]
            nums: list[int] = [1, 3, 2, 5, 4]
       ```

     2.  Accessing elements
    
        Elements in an array are stored in contiguous memory spaces, making it simpler to compute each element's memory address.
        array indexing conventionally begins at 0 While this might appear counterintuitive, considering counting usually starts at 1 within the address calculation formula, an index is 
        essentially an offset from the memory address. For the first element's address, this offset is 0, validating its index as 0. Accessing elements in an array is highly efficient, 
        allowing us to randomly access any element in O(1) time.

     3. Inserting elements
    
        Array elements are tightly packed in memory, with no space available to accommodate additional data between them. Inserting an element in the middle of an array requires shifting 
        all subsequent elements back by one position to create room for the new element.
        It's important to note that due to the fixed length of an array, inserting an element will unavoidably result in the loss of the last element in the array. Solutions to address 
        this issue will be explored in the "List" chapter.

     4. Deleting elements
    
        To delete an element at index i, all elements following index i must be moved forward by one position. Please note that after deletion, the former last element becomes 
        "meaningless," hence requiring no specific modification.

     In summary, the insertion and deletion operations in arrays present the following disadvantages:

     . High time complexity: Both insertion and deletion in an array have an average time complexity of O(n), where n is the length of the array.
     . Loss of elements: Due to the fixed length of arrays, elements that exceed the array's capacity are lost during insertion.
     . Waste of memory: Initializing a longer array and utilizing only the front part results in "meaningless" end elements during insertion, leading to some wasted memory space.

   5. Traversing arrays

      In most programming languages, we can traverse an array either by using indices or by directly iterating over each element:

         ```ruby
           /* Traverse array */
            void traverse(int *nums, int size) {
                int count = 0;
                // Traverse array by index
                for (int i = 0; i < size; i++) {
                    count += nums[i];
                }
            }
       ```

6. Finding elements

   Locating a specific element within an array involves iterating through the array, checking each element to determine if it matches the desired value.
   Because arrays are linear data structures, this operation is commonly referred to as "linear search."
   ```ruby
         /* Search for a specified element in the array */
      int find(int *nums, int size, int target) {
          for (int i = 0; i < size; i++) {
              if (nums[i] == target)
                  return i;
          }
          return -1;
      }
   ```

   ## Advantages and limitations of arrays

   Arrays are stored in contiguous memory spaces and consist of elements of the same type. This approach provides substantial prior information that systems can leverage to optimize the efficiency of data structure operations.

. High space efficiency: Arrays allocate a contiguous block of memory for data, eliminating the need for additional structural overhead.
. Support for random access: Arrays allow O(1) time access to any element.
. Cache locality: When accessing array elements, the computer not only loads them but also caches the surrounding data, utilizing high-speed cache to enchance subsequent operation speeds.

However, continuous space storage is a double-edged sword, with the following limitations:

. Low efficiency in insertion and deletion: As arrays accumulate many elements, inserting or deleting elements requires shifting a large number of elements.
. Fixed length: The length of an array is fixed after initialization. Expanding an array requires copying all data to a new array, incurring significant costs.
. Space wastage: If the allocated array size exceeds the what is necessary, the extra space is wasted.

Typical applications of arrays

Arrays are fundamental and widely used data structures. They find frequent application in various algorithms and serve in the implementation of complex data structures.
. Random access: Arrays are ideal for storing data when random sampling is required. By generating a random sequence based on indices, we can achieve random sampling efficiently.
. Sorting and searching: Arrays are the most commonly used data structure for sorting and searching algorithms. Techniques like quick sort, merge sort, binary search, etc., are primarily operate on arrays.
. Lookup tables: Arrays serve as efficient lookup tables for quick element or relationship retrieval. For instance, mapping characters to ASCII codes becomes seamless by using the ASCII code values as indices and storing corresponding elements in the array.
. Machine learning: Within the domain of neural networks, arrays play a pivotal role in executing crucial linear algebra operations involving vectors, matrices, and tensors. Arrays serve as the primary and most extensively used data structure in neural network programming.
. Data structure implementation: Arrays serve as the building blocks for implementing various data structures like stacks, queues, hash tables, heaps, graphs, etc. For instance, the adjacency matrix representation of a graph is essentially a two-dimensional array.


## Linked list

Memory space is a shared resource among all programs. In a complex system environment, available memory can be dispersed throughout the memory space. We understand that the memory allocated for an array must be continuous. However, for very large arrays, finding a sufficiently large contiguous memory space might be challenging. This is where the flexible advantage of linked lists becomes evident.

A linked list is a linear data structure in which each element is a node object, and the nodes are interconnected through "references". These references hold the memory addresses of subsequent nodes, enabling navigation from one node to the next.

we see that the basic building block of a linked list is the node object. Each node comprises two key components: the node's "value" and a "reference" to the next node.

. The first node in a linked list is the "head node", and the final one is the "tail node".
. The tail node points to "null", designated as null in Java, nullptr in C++, and None in Python.
. In languages that support pointers, like C, C++, Go, and Rust, this "reference" is typically implemented as a "pointer".
The design of linked lists allows for their nodes to be distributed across memory locations without requiring contiguous memory addresses.

As the code below illustrates, a ListNode in a linked list, besides holding a value, must also maintain an additional reference (or pointer). Therefore, a linked list occupies more memory space than an array when storing the same quantity of data.

  ```ruby
         /* Search for a specified element in the array */
      iclass ListNode:
    """Linked list node class"""
    def __init__(self, val: int):
        self.val: int = val               # Node value
        self.next: ListNode | None = None # Reference to the next node
   ```

Common operations on linked lists:

1. Initializing a linked list
   Constructing a linked list is a two-step process: first, initializing each node object, and second, forming the reference links between the nodes. After initialization, we can traverse 
   all nodes sequentially from the head node by following the next reference.
   ```ruby
        # Initialize linked list: 1 -> 3 -> 2 -> 5 -> 4
      # Initialize each node
      n0 = ListNode(1)
      n1 = ListNode(3)
      n2 = ListNode(2)
      n3 = ListNode(5)
      n4 = ListNode(4)
      # Build references between nodes
      n0.next = n1
      n1.next = n2
      n2.next = n3
      n3.next = n4
   ```

   The array as a whole is a variable, for instance, the array nums  includes elements like nums[0], nums[1], and so on, whereas a linked list is made up of several distinct node objects. We typically refer to a linked list by its head node, for example, the linked list in the previous code snippet is referred to as n0.

2. Inserting nodes¶
Inserting a node into a linked list is very easy. let's assume we aim to insert a new node P between two adjacent nodes n0 and n1. This can be achieved by simply modifying two node references (pointers), with a time complexity of O(1).
By comparison, inserting an element into an array has a time complexity of O(n), which becomes less efficient when dealing with large data volumes.
```ruby
     def insert(n0: ListNode, P: ListNode):
    """Insert node P after node n0 in the linked list"""
    n1 = n0.next
    P.next = n1
    n0.next = P
   ```
3. Deleting nodes
   Deleting a node from a linked list is also very easy, involving only the modification of a single node's reference (pointer).
   t's important to note that even though node P continues to point to n1 after being deleted, it becomes inaccessible during linked list traversal. This effectively means that P is no longer a part of the linked list.
   ```ruby
    def remove(n0: ListNode):
    """Remove the first node after node n0 in the linked list"""
    if not n0.next:
        return
    # n0 -> P -> n1
    P = n0.next
    n1 = P.next
    n0.next = n1
   ```

4. Accessing nodes
   Accessing nodes in a linked list is less efficient. As previously mentioned, any element in an array can be accessed in O(1) time. n contrast, with a linked list, the program involves 
   starting from the head node and sequentially traversing through the nodes until the desired node is found. In other words, to access the i-th node in a linked list, the program must 
   iterate through i-1 nodes, resulting in a time complexity of O(n).

      ```ruby
   def access(head: ListNode, index: int) -> ListNode | None:
    """Access the node at `index` in the linked list"""
    for _ in range(index):
        if not head:
            return None
        head = head.next
    return head
   ```

5. Finding nodes
   Traverse the linked list to locate a node whose value matches target, and then output the index of that node within the linked list. This procedure is also an example of linear search. 
    The corresponding code is provided below:

   ```ruby
         def find(head: ListNode, target: int) -> int:
    """Search for the first node with value target in the linked list"""
    index = 0
    while head:
        if head.val == target:
            return index
        head = head.next
        index += 1
    return -1
    ```

There are three common types of linked lists: 

. Singly linked list: This is the standard linked list described earlier. Nodes in a singly linked list include a value and a reference to the next node. The first node is known as the head node, and the last node, which points to null (None), is the tail node.

. Circular linked list: This is formed when the tail node of a singly linked list points back to the head node, creating a loop. In a circular linked list, any node can function as the head node.

. Doubly linked list: In contrast to a singly linked list, a doubly linked list maintains references in two directions. Each node contains references (pointer) to both its successor (the next node) and predecessor (the previous node). Although doubly linked lists offer more flexibility for traversing in either direction, they also consume more memory space.


   ```ruby
         def find(head: ListNode, target: int) -> int:
         /* Bidirectional linked list node class */
      class ListNode {
          constructor(val, next, prev) {
              this.val = val  ===  undefined ? 0 : val;        // Node value
              this.next = next  ===  undefined ? null : next;  // Reference to the successor node
              this.prev = prev  ===  undefined ? null : prev;  // Reference to the predecessor node
          }
      }
   ```
## Typical applications of linked lists

Singly linked lists are frequently utilized in implementing stacks, queues, hash tables, and graphs.

. Stacks and queues: In singly linked lists, if insertions and deletions occur at the same end, it behaves like a stack (last-in-first-out). Conversely, if insertions are at one end and deletions at the other, it functions like a queue (first-in-first-out).
. Hash tables: Linked lists are used in chaining, a popular method for resolving hash collisions. Here, all collided elements are grouped into a linked list.
.Graphs: Adjacency lists, a standard method for graph representation, associate each graph vertex with a linked list. This list contains elements that represent vertices connected to the corresponding vertex.

Doubly linked lists are ideal for scenarios requiring rapid access to preceding and succeeding elements.
. Advanced data structures: In structures like red-black trees and B-trees, accessing a node's parent is essential. This is achieved by incorporating a reference to the parent node in each node, akin to a doubly linked list.
. Browser history: In web browsers, doubly linked lists facilitate navigating the history of visited pages when users click forward or back.
. LRU algorithm: Doubly linked lists are apt for Least Recently Used (LRU) cache eviction algorithms, enabling swift identification of the least recently used data and facilitating fast node addition and removal.

Circular linked lists are ideal for applications that require periodic operations, such as resource scheduling in operating systems.

. Round-robin scheduling algorithm: In operating systems, the round-robin scheduling algorithm is a common CPU scheduling method, requiring cycling through a group of processes. Each process is assigned a time slice, and upon expiration, the CPU rotates to the next process. This cyclical operation can be efficiently realized using a circular linked list, allowing for a fair and time-shared system among all processes.

. Data buffers: Circular linked lists are also used in data buffers, like in audio and video players, where the data stream is divided into multiple buffer blocks arranged in a circular fashion for seamless playback.

## List

A list is an abstract data structure concept that represents an ordered collection of elements, supporting operations such as element access, modification, addition, deletion, and traversal, without requiring users to consider capacity limitations. Lists can be implemented based on linked lists or arrays.

. A linked list inherently serves as a list, supporting operations for adding, deleting, searching, and modifying elements, with the flexibility to dynamically adjust its size.
. Arrays also support these operations, but due to their immutable length, they can be considered as a list with a length limit.

When implementing lists using arrays, the immutability of length reduces the practicality of the list. This is because predicting the amount of data to be stored in advance is often challenging, making it difficult to choose an appropriate list length. If the length is too small, it may not meet the requirements; if too large, it may waste memory space.

To solve this problem, we can implement lists using a dynamic array. It inherits the advantages of arrays and can dynamically expand during program execution.

In fact, many programming languages' standard libraries implement lists using dynamic arrays, such as Python's list, Java's ArrayList, C++'s vector, and C#'s List. In the following discussion, we will consider "list" and "dynamic array" as synonymous concepts.

Common list operations

1. Initializing a list
   We typically use two initialization methods: "without initial values" and "with initial values".
      ```ruby
            /* Initialize list */
      // Without initial values
      const nums1 = [];
      // With initial values
      const nums = [1, 3, 2, 5, 4];
      ```
 2. Accessing elements¶
    Lists are essentially arrays, thus they can access and update elements in O(1) time, which is very efficient.

    ```ruby
         # Access elements
      num: int = nums[1]  # Access the element at index 1
      
      # Update elements
      nums[1] = 0    # Update the element at index 1 to 0
    ```
3. Inserting and removing elements
   Compared to arrays, lists offer more flexibility in adding and removing elements. While adding elements to the end of a list is an O(1) operation, the efficiency of inserting and 
   removing elements elsewhere in the list remains the same as in arrays, with a time complexity of O(n).

   ```ruby
        # Clear list
      nums.clear()
      
      # Append elements at the end
      nums.append(1)
      nums.append(3)
      nums.append(2)
      nums.append(5)
      nums.append(4)
      
      # Insert element in the middle
      nums.insert(3, 6)  # Insert number 6 at index 3
      
      # Remove elements
      nums.pop(3)        # Remove the element at index 3
    ```
4. Iterating the list
   Similar to arrays, lists can be iterated either by using indices or by directly iterating through each element.
    ```ruby
       # Iterate through the list by index
      count = 0
      for i in range(len(nums)):
          count += nums[i]
      
      # Iterate directly through list elements
      for num in nums:
          count += num
      
    ```

5. Concatenating lists
   Given a new list nums1, we can append it to the end of the original list.
     ```ruby
      # Concatenate two lists
      nums1: list[int] = [6, 8, 7, 10, 9]
      nums += nums1  # Concatenate nums1 to the end of nums
      
    ```
6.  Sorting the list
   Once the list is sorted, we can employ algorithms commonly used in array-related algorithm problems, such as "binary search" and "two-pointer" algorithms.

## List implementation

Many programming languages come with built-in lists, including Java, C++, Python, etc. Their implementations tend to be intricate, featuring carefully considered settings for various parameters, like initial capacity and expansion factors. Readers who are curious can delve into the source code for further learning.
To enhance our understanding of how lists work, we will attempt to implement a simplified version of a list, focusing on three crucial design aspects:
. Initial capacity: Choose a reasonable initial capacity for the array. In this example, we choose 10 as the initial capacity.

. Size recording: Declare a variable size to record the current number of elements in the list, updating in real-time with element insertion and deletion. With this variable, we can locate the end of the list and determine whether expansion is needed.

. Expansion mechanism: If the list reaches full capacity upon an element insertion, an expansion process is required. This involves creating a larger array based on the expansion factor, and then transferring all elements from the current array to the new one. In this example, we stipulate that the array size should double with each expansion.

## Memory and cache

In the first two sections of this chapter, we explored arrays and linked lists, two fundamental and important data structures, representing "continuous storage" and "dispersed storage" respectively.

In fact, the physical structure largely determines the efficiency of a program's use of memory and cache, which in turn affects the overall performance of the algorithm.

# Computer storage devices

There are three types of storage devices in computers: hard disk, random-access memory (RAM), and cache memory. The following table shows their different roles and performance characteristics in computer systems.

	Hard Disk	Memory	Cache
Usage	Long-term storage of data, including OS, programs, files, etc.	Temporary storage of currently running programs and data being processed	Stores frequently accessed data and instructions, reducing the number of CPU accesses to memory
Volatility	Data is not lost after power off	Data is lost after power off	Data is lost after power off
Capacity	Larger, TB level	Smaller, GB level	Very small, MB level
Speed	Slower, several hundred to thousands MB/s	Faster, several tens of GB/s	Very fast, several tens to hundreds of GB/s
Price	Cheaper, several cents to yuan / GB	More expensive, tens to hundreds of yuan / GB	Very expensive, priced with CPU

We can imagine the computer storage system as a pyramid structure shown in Figure 4-9. The storage devices closer to the top of the pyramid are faster, have smaller capacity, and are more costly. This multi-level design is not accidental, but the result of careful consideration by computer scientists and engineers.
. Hard disks are difficult to replace with memory. Firstly, data in memory is lost after power off, making it unsuitable for long-term data storage; secondly, the cost of memory is dozens of times that of hard disks, making it difficult to popularize in the consumer market.
. It is difficult for caches to have both large capacity and high speed. As the capacity of L1, L2, L3 caches gradually increases, their physical size becomes larger, increasing the physical distance from the CPU core, leading to increased data transfer time and higher element access latency. Under current technology, a multi-level cache structure is the best balance between capacity, speed, and cost.

> [!TIP]
     > The storage hierarchy of computers reflects a delicate balance between speed, capacity, and cost. In fact, this kind of trade-off is common in all industrial fields, requiring us to find the best balance between different advantages and limitations.

Overall, hard disks are used for long-term storage of large amounts of data, memory is used for temporary storage of data being processed during program execution, and cache is used to store frequently accessed data and instructions to improve program execution efficiency. Together, they ensure the efficient operation of computer systems.

during program execution, data is read from the hard disk into memory for CPU computation. The cache can be considered a part of the CPU, smartly loading data from memory to provide fast data access to the CPU, significantly enhancing program execution efficiency and reducing reliance on slower memory.

# Memory efficiency of data structures¶

In terms of memory space utilization, arrays and linked lists have their advantages and limitations.
