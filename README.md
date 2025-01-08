
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

On one hand, memory is limited and cannot be shared by multiple programs, so we hope that data structures can use space as efficiently as possible. The elements of an array are tightly packed without extra space for storing references (pointers) between linked list nodes, making them more space-efficient. However, arrays require allocating sufficient continuous memory space at once, which may lead to memory waste, and array expansion also requires additional time and space costs. In contrast, linked lists allocate and reclaim memory dynamically on a per-node basis, providing greater flexibility.

On the other hand, during program execution, as memory is repeatedly allocated and released, the degree of fragmentation of free memory becomes higher, leading to reduced memory utilization efficiency. Arrays, due to their continuous storage method, are relatively less likely to cause memory fragmentation. In contrast, the elements of a linked list are dispersedly stored, and frequent insertion and deletion operations make memory fragmentation more likely.

## Cache efficiency of data structures

Although caches are much smaller in space capacity than memory, they are much faster and play a crucial role in program execution speed. Since the cache's capacity is limited and can only store a small part of frequently accessed data, when the CPU tries to access data not in the cache, a cache miss occurs, forcing the CPU to load the needed data from slower memory.

Clearly, the fewer the cache misses, the higher the CPU's data read-write efficiency, and the better the program performance. The proportion of successful data retrieval from the cache by the CPU is called the cache hit rate, a metric often used to measure cache efficiency.

To achieve higher efficiency, caches adopt the following data loading mechanisms.

Cache lines: Caches don't store and load data byte by byte but in units of cache lines. Compared to byte-by-byte transfer, the transmission of cache lines is more efficient.
Prefetch mechanism: Processors try to predict data access patterns (such as sequential access, fixed stride jumping access, etc.) and load data into the cache according to specific patterns to improve the hit rate.
Spatial locality: If data is accessed, data nearby is likely to be accessed in the near future. Therefore, when loading certain data, the cache also loads nearby data to improve the hit rate.
Temporal locality: If data is accessed, it's likely to be accessed again in the near future. Caches use this principle to retain recently accessed data to improve the hit rate.
In fact, arrays and linked lists have different cache utilization efficiencies, mainly reflected in the following aspects.

Occupied space: Linked list elements occupy more space than array elements, resulting in less effective data volume in the cache.
Cache lines: Linked list data is scattered throughout memory, and since caches load "by line," the proportion of loading invalid data is higher.
Prefetch mechanism: The data access pattern of arrays is more "predictable" than that of linked lists, meaning the system is more likely to guess which data will be loaded next.
Spatial locality: Arrays are stored in concentrated memory spaces, so the data near the loaded data is more likely to be accessed next.

Overall, arrays have a higher cache hit rate and are generally more efficient in operation than linked lists. This makes data structures based on arrays more popular in solving algorithmic problems.

It should be noted that high cache efficiency does not mean that arrays are always better than linked lists. Which data structure to choose in actual applications should be based on specific requirements. For example, both arrays and linked lists can implement the "stack" data structure (which will be detailed in the next chapter), but they are suitable for different scenarios.

In algorithm problems, we tend to choose stacks based on arrays because they provide higher operational efficiency and random access capabilities, with the only cost being the need to pre-allocate a certain amount of memory space for the array.
If the data volume is very large, highly dynamic, and the expected size of the stack is difficult to estimate, then a stack based on a linked list is more appropriate. Linked lists can disperse a large amount of data in different parts of the memory and avoid the additional overhead of array expansion.

## Stack
A stack is a linear data structure that follows the principle of Last-In-First-Out (LIFO).

We can compare a stack to a pile of plates on a table. To access the bottom plate, one must first remove the plates on top. By replacing the plates with various types of elements (such as integers, characters, objects, etc.), we obtain the data structure known as a stack.

We refer to the top of the pile of elements as the "top of the stack" and the bottom as the "bottom of the stack." The operation of adding elements to the top of the stack is called "push," and the operation of removing the top element is called "pop."
Typically, we can directly use the stack class built into the programming language. However, some languages may not specifically provide a stack class. In these cases, we can use the language's "array" or "linked list" as a stack and ignore operations that are not related to stack logic in the program.

 # Common operations on stack

 The specific method names depend on the programming language used. Here, we use push(), pop(), and peek() as examples.

 # Implementing a stack

 To gain a deeper understanding of how a stack operates, let's try implementing a stack class ourselves.

A stack follows the principle of Last-In-First-Out, which means we can only add or remove elements at the top of the stack. However, both arrays and linked lists allow adding and removing elements at any position, therefore a stack can be seen as a restricted array or linked list. In other words, we can "shield" certain irrelevant operations of an array or linked list, aligning their external behavior with the characteristics of a stack.

Implementation based on a linked list

When implementing a stack using a linked list, we can consider the head node of the list as the top of the stack and the tail node as the bottom of the stack.
we simply insert elements at the head of the linked list. This method of node insertion is known as "head insertion." For the pop operation, we just need to remove the head node from the list.

Below is an example code for implementing a stack based on a linked list:

```ruby
     class LinkedListStack:
    """Stack class based on linked list"""

    def __init__(self):
        """Constructor"""
        self._peek: ListNode | None = None
        self._size: int = 0

    def size(self) -> int:
        """Get the length of the stack"""
        return self._size

    def is_empty(self) -> bool:
        """Determine if the stack is empty"""
        return self._size == 0

    def push(self, val: int):
        """Push"""
        node = ListNode(val)
        node.next = self._peek
        self._peek = node
        self._size += 1

    def pop(self) -> int:
        """Pop"""
        num = self.peek()
        self._peek = self._peek.next
        self._size -= 1
        return num

    def peek(self) -> int:
        """Access stack top element"""
        if self.is_empty():
            raise IndexError("Stack is empty")
        return self._peek.val

    def to_list(self) -> list[int]:
        """Convert to a list for printing"""
        arr = []
        node = self._peek
        while node:
            arr.append(node.val)
            node = node.next
        arr.reverse()
        return arr
      
```

Implementation based on an array

When implementing a stack using an array, we can consider the end of the array as the top of the stack. push and pop operations correspond to adding and removing elements at the end of the array, respectively, both with a time complexity of O(1).

Since the elements to be pushed onto the stack may continuously increase, we can use a dynamic array, thus avoiding the need to handle array expansion ourselves. Here is an example code:

```ruby
   class ArrayStack:
    """Stack class based on array"""

    def __init__(self):
        """Constructor"""
        self._stack: list[int] = []

    def size(self) -> int:
        """Get the length of the stack"""
        return len(self._stack)

    def is_empty(self) -> bool:
        """Determine if the stack is empty"""
        return self.size() == 0

    def push(self, item: int):
        """Push"""
        self._stack.append(item)

    def pop(self) -> int:
        """Pop"""
        if self.is_empty():
            raise IndexError("Stack is empty")
        return self._stack.pop()

    def peek(self) -> int:
        """Access stack top element"""
        if self.is_empty():
            raise IndexError("Stack is empty")
        return self._stack[-1]

    def to_list(self) -> list[int]:
        """Return array for printing"""
        return self._stack
      
```

# Comparison of the two implementations

Supported Operations

Both implementations support all the operations defined in a stack. The array implementation additionally supports random access, but this is beyond the scope of a stack definition and is generally not used.

# Time Efficiency

In the array-based implementation, both push and pop operations occur in pre-allocated contiguous memory, which has good cache locality and therefore higher efficiency. However, if the push operation exceeds the array capacity, it triggers a resizing mechanism, making the time complexity of that push operation.

In the linked list implementation, list expansion is very flexible, and there is no efficiency decrease issue as in array expansion. However, the push operation requires initializing a node object and modifying pointers, so its efficiency is relatively lower. If the elements being pushed are already node objects, then the initialization step can be skipped, improving efficiency.

Thus, when the elements for push and pop operations are basic data types like int or double, we can draw the following conclusions:

The array-based stack implementation's efficiency decreases during expansion, but since expansion is a low-frequency operation, its average efficiency is higher.
The linked list-based stack implementation provides more stable efficiency performance.

# Space Efficiency

When initializing a list, the system allocates an "initial capacity," which might exceed the actual need; moreover, the expansion mechanism usually increases capacity by a specific factor (like doubling), which may also exceed the actual need. Therefore, the array-based stack might waste some space.

However, since linked list nodes require extra space for storing pointers, the space occupied by linked list nodes is relatively larger.

In summary, we cannot simply determine which implementation is more memory-efficient. It requires analysis based on specific circumstances.



# Typical applications of stack

Back and forward in browsers, undo and redo in software. Every time we open a new webpage, the browser pushes the previous page onto the stack, allowing us to go back to the previous page through the back operation, which is essentially a pop operation. To support both back and forward, two stacks are needed to work together.

Memory management in programs. Each time a function is called, the system adds a stack frame at the top of the stack to record the function's context information. In recursive functions, the downward recursion phase keeps pushing onto the stack, while the upward backtracking phase keeps popping from the stack.


## Queue

A queue is a linear data structure that follows the First-In-First-Out (FIFO) rule. As the name suggests, a queue simulates the phenomenon of lining up, where newcomers join the queue at the rear, and the person at the front leaves the queue first.

We call the front of the queue the "head" and the back the "tail." The operation of adding elements to the rear of the queue is termed "enqueue," and the operation of removing elements from the front is termed "dequeue."

We can directly use the ready-made queue classes in programming languages:

```ruby
	/* Initialize the queue */
	// JavaScript does not have a built-in queue, so Array can be used as a queue
	const queue = [];
	
	/* Enqueue elements */
	queue.push(1);
	queue.push(3);
	queue.push(2);
	queue.push(5);
	queue.push(4);
	
	/* Access the first element */
	const peek = queue[0];
	
	/* Dequeue an element */
	// Since the underlying structure is an array, shift() method has a time complexity of O(n)
	const pop = queue.shift();
	
	/* Get the length of the queue */
	const size = queue.length;
	
	/* Check if the queue is empty */
	const empty = queue.length === 0;
	      
```

## Implementing a queue

To implement a queue, we need a data structure that allows adding elements at one end and removing them at the other. Both linked lists and arrays meet this requirement.

1. Implementation based on a linked list

   We can consider the "head node" and "tail node" of a linked list as the "front" and "rear" of the queue, respectively. It is stipulated that nodes can only be 
   added at the rear and removed at the front.

```ruby
	class LinkedListQueue:
    """Queue class based on linked list"""

    def __init__(self):
        """Constructor"""
        self._front: ListNode | None = None  # Head node front
        self._rear: ListNode | None = None  # Tail node rear
        self._size: int = 0

    def size(self) -> int:
        """Get the length of the queue"""
        return self._size

    def is_empty(self) -> bool:
        """Determine if the queue is empty"""
        return self._size == 0

    def push(self, num: int):
        """Enqueue"""
        # Add num behind the tail node
        node = ListNode(num)
        # If the queue is empty, make the head and tail nodes both point to that node
        if self._front is None:
            self._front = node
            self._rear = node
        # If the queue is not empty, add that node behind the tail node
        else:
            self._rear.next = node
            self._rear = node
        self._size += 1

    def pop(self) -> int:
        """Dequeue"""
        num = self.peek()
        # Remove head node
        self._front = self._front.next
        self._size -= 1
        return num

    def peek(self) -> int:
        """Access front element"""
        if self.is_empty():
            raise IndexError("Queue is empty")
        return self._front.val

    def to_list(self) -> list[int]:
        """Convert to a list for printing"""
        queue = []
        temp = self._front
        while temp:
            queue.append(temp.val)
            temp = temp.next
        return queue

	      
```

2. Implementation based on an array

    similar to implementing a queue with an array, we can also use a circular array to implement a double-ended queue.
   
```ruby
class ArrayDeque:
    """Double-ended queue class based on circular array"""

    def __init__(self, capacity: int):
        """Constructor"""
        self._nums: list[int] = [0] * capacity
        self._front: int = 0
        self._size: int = 0

    def capacity(self) -> int:
        """Get the capacity of the double-ended queue"""
        return len(self._nums)

    def size(self) -> int:
        """Get the length of the double-ended queue"""
        return self._size

    def is_empty(self) -> bool:
        """Determine if the double-ended queue is empty"""
        return self._size == 0

    def index(self, i: int) -> int:
        """Calculate circular array index"""
        # Implement circular array by modulo operation
        # When i exceeds the tail of the array, return to the head
        # When i exceeds the head of the array, return to the tail
        return (i + self.capacity()) % self.capacity()

    def push_first(self, num: int):
        """Front enqueue"""
        if self._size == self.capacity():
            print("Double-ended queue is full")
            return
        # Move the front pointer one position to the left
        # Implement front crossing the head of the array to return to the tail by modulo operation
        self._front = self.index(self._front - 1)
        # Add num to the front
        self._nums[self._front] = num
        self._size += 1

    def push_last(self, num: int):
        """Rear enqueue"""
        if self._size == self.capacity():
            print("Double-ended queue is full")
            return
        # Calculate rear pointer, pointing to rear index + 1
        rear = self.index(self._front + self._size)
        # Add num to the rear
        self._nums[rear] = num
        self._size += 1

    def pop_first(self) -> int:
        """Front dequeue"""
        num = self.peek_first()
        # Move front pointer one position backward
        self._front = self.index(self._front + 1)
        self._size -= 1
        return num

    def pop_last(self) -> int:
        """Rear dequeue"""
        num = self.peek_last()
        self._size -= 1
        return num

    def peek_first(self) -> int:
        """Access front element"""
        if self.is_empty():
            raise IndexError("Double-ended queue is empty")
        return self._nums[self._front]

    def peek_last(self) -> int:
        """Access rear element"""
        if self.is_empty():
            raise IndexError("Double-ended queue is empty")
        # Calculate rear element index
        last = self.index(self._front + self._size - 1)
        return self._nums[last]

    def to_array(self) -> list[int]:
        """Return array for printing"""
        # Only convert elements within valid length range
        res = []
        for i in range(self._size):
            res.append(self._nums[self.index(self._front + i)])
        return res

	      
```

##  Hash table

A hash table, also known as a hash map, is a data structure that establishes a mapping between keys and values, enabling efficient element retrieval. Specifically, when we input a key into the hash table, we can retrieve the corresponding value in O(1) time complexity.

In addition to hash tables, arrays and linked lists can also be used to implement query functionality, but the time complexity is different. Their efficiency is compared in Table 6-1:

. Inserting an element: Simply append the element to the tail of the array (or linked list). The time complexity of this operation is O(1)

. Searching for an element: As the array (or linked list) is unsorted, searching for an element requires traversing through all of the elements. The time complexity of this operation is O(n).

.Deleting an element: To remove an element, we first need to locate it. Then, we delete it from the array (or linked list). The time complexity of this operation is O(n).

As observed, the time complexity for operations (insertion, deletion, searching, and modification) in a hash table is O(1), which is highly efficient.

### Common operations of hash table

Common operations of a hash table include: initialization, querying, adding key-value pairs, and deleting key-value pairs. Here is an example code:

```ruby

/* Initialize hash table */
const map = new Map();
/* Add operation */
// Add key-value pair (key, value) to the hash table
map.set(12836, 'Xiao Ha');
map.set(15937, 'Xiao Luo');
map.set(16750, 'Xiao Suan');
map.set(13276, 'Xiao Fa');
map.set(10583, 'Xiao Ya');

/* Query operation */
// Input key into hash table, get value
let name = map.get(15937);

/* Delete operation */
// Delete key-value pair (key, value) from hash table
map.delete(10583);
	      
```

There are three common ways to traverse a hash table: traversing key-value pairs, traversing keys, and traversing values. Here is an example code:

```ruby
/* Traverse hash table */
console.info('\nTraverse key-value pairs Key->Value');
for (const [k, v] of map.entries()) {
    console.info(k + ' -> ' + v);
}
console.info('\nTraverse keys only Key');
for (const k of map.keys()) {
    console.info(k);
}
console.info('\nTraverse values only Value');
for (const v of map.values()) {
    console.info(v);
}

```
### Simple implementation of a hash table

First, let's consider the simplest case: implementing a hash table using only one array. In the hash table, each empty slot in the array is called a bucket, and each bucket can store a key-value pair. Therefore, the query operation involves finding the bucket corresponding to the key and retrieving the value from it.

So, how do we locate the corresponding bucket based on the key? This is achieved through a hash function. The role of the hash function is to map a larger input space to a smaller output space. In a hash table, the input space consists of all the keys, and the output space consists of all the buckets (array indices). In other words, given a key, we can use the hash function to determine the storage location of the corresponding key-value pair in the array.

With a given key, the calculation of the hash function consists of two steps:

1. Calculate the hash value by using a certain hash algorithm hash().
2. Take the modulus of the hash value with the bucket count (array length) capacity to obtain the array index corresponding to the key.

index = hash(key) % capacity

Afterward, we can use the index to access the corresponding bucket in the hash table and thereby retrieve the value.

Let's assume that the array length is capacity = 100, and the hash algorithm is defined as hash(key) = key. Therefore, the hash function can be expressed as key % 100

### Hash collision and resizing

Essentially, the role of the hash function is to map the entire input space of all keys to the output space of all array indices. However, the input space is often much larger than the output space. Therefore, theoretically, there will always be cases where "multiple inputs correspond to the same output".

In the example above, with the given hash function, when the last two digits of the input key are the same, the hash function produces the same output. For instance, when querying two students with student IDs 12836 and 20336, we find:

12836 % 100 = 36

It is easy to understand that as the capacity n of the hash table increases, the probability of multiple keys being assigned to the same bucket decreases, resulting in fewer collisions. Therefore, we can reduce hash collisions by resizing the hash table.

Similar to array expansion, resizing a hash table requires migrating all key-value pairs from the original hash table to the new one, which is time-consuming. Furthermore, since the capacity of the hash table changes, we need to recalculate the storage positions of all key-value pairs using the hash function, further increasing the computational overhead of the resizing process. Therefore, programming languages often allocate a sufficiently large capacity for the hash table to prevent frequent resizing.
20336 % 100 = 36


The load factor is an important concept in hash tables. It is defined as the ratio of the number of elements in the hash table to the number of buckets. It is used to measure the severity of hash collisions and often serves as a trigger for hash table resizing. For example, in Java, when the load factor exceeds 0.75, the system will resize the hash table to twice its original size.

### Hash collision

The previous section mentioned that, in most cases, the input space of a hash function is much larger than the output space, so theoretically, hash collisions are inevitable. For example, if the input space is all integers and the output space is the size of the array capacity, then multiple integers will inevitably be mapped to the same bucket index.

Hash collisions can lead to incorrect query results, severely impacting the usability of the hash table. To address this issue, whenever a hash collision occurs, we perform hash table resizing until the collision disappears. This approach is pretty simple, straightforward, and working well. However, it appears to be pretty inefficient as the table expansion involves a lot of data migration as well as recalculation of hash code, which are expansive. To improve efficiency, we can adopt the following strategies:

1. Improve the hash table data structure in a way that locating target element is still functioning well in the event of a hash collision.
2. Expansion is the last resort before it becomes necessary, when severe collisions are observed.

There are mainly two methods for improving the structure of hash tables: "Separate Chaining" and "Open Addressing".

### Separate chaining

In the original hash table, each bucket can store only one key-value pair. Separate chaining converts a single element into a linked list, treating key-value pairs as list nodes, storing all colliding key-value pairs in the same linked list. Figure 6-5 shows an example of a hash table with separate chaining.

The operations of a hash table implemented with separate chaining have changed as follows:

. Querying Elements: Input key, obtain the bucket index through the hash function, then access the head node of the linked list. Traverse the linked list and compare key to find the target key-value pair.

. Adding Elements: Access the head node of the linked list via the hash function, then append the node (key-value pair) to the list.

. Deleting Elements: Access the head of the linked list based on the result of the hash function, then traverse the linked list to find the target node and delete it.

Separate chaining has the following limitations:

. Increased Space Usage: The linked list contains node pointers, which consume more memory space than arrays.

. Reduced Query Efficiency: This is because linear traversal of the linked list is required to find the corresponding element.

The code below provides a simple implementation of a separate chaining hash table, with two things to note:

. Lists (dynamic arrays) are used instead of linked lists for simplicity. In this setup, the hash table (array) contains multiple buckets, each of which is a list.

. This implementation includes a hash table resizing method. When the load factor exceeds 2/3, we expand the hash table to twice its original size.

```ruby
class HashMapChaining:
    """Chained address hash table"""

    def __init__(self):
        """Constructor"""
        self.size = 0  # Number of key-value pairs
        self.capacity = 4  # Hash table capacity
        self.load_thres = 2.0 / 3.0  # Load factor threshold for triggering expansion
        self.extend_ratio = 2  # Expansion multiplier
        self.buckets = [[] for _ in range(self.capacity)]  # Bucket array

    def hash_func(self, key: int) -> int:
        """Hash function"""
        return key % self.capacity

    def load_factor(self) -> float:
        """Load factor"""
        return self.size / self.capacity

    def get(self, key: int) -> str | None:
        """Query operation"""
        index = self.hash_func(key)
        bucket = self.buckets[index]
        # Traverse the bucket, if the key is found, return the corresponding val
        for pair in bucket:
            if pair.key == key:
                return pair.val
        # If the key is not found, return None
        return None

    def put(self, key: int, val: str):
        """Add operation"""
        # When the load factor exceeds the threshold, perform expansion
        if self.load_factor() > self.load_thres:
            self.extend()
        index = self.hash_func(key)
        bucket = self.buckets[index]
        # Traverse the bucket, if the specified key is encountered, update the corresponding val and return
        for pair in bucket:
            if pair.key == key:
                pair.val = val
                return
        # If the key is not found, add the key-value pair to the end
        pair = Pair(key, val)
        bucket.append(pair)
        self.size += 1

    def remove(self, key: int):
        """Remove operation"""
        index = self.hash_func(key)
        bucket = self.buckets[index]
        # Traverse the bucket, remove the key-value pair from it
        for pair in bucket:
            if pair.key == key:
                bucket.remove(pair)
                self.size -= 1
                break

    def extend(self):
        """Extend hash table"""
        # Temporarily store the original hash table
        buckets = self.buckets
        # Initialize the extended new hash table
        self.capacity *= self.extend_ratio
        self.buckets = [[] for _ in range(self.capacity)]
        self.size = 0
        # Move key-value pairs from the original hash table to the new hash table
        for bucket in buckets:
            for pair in bucket:
                self.put(pair.key, pair.val)

    def print(self):
        """Print hash table"""
        for bucket in self.buckets:
            res = []
            for pair in bucket:
                res.append(str(pair.key) + " -> " + pair.val)
            print(res)

```

It's worth noting that when the linked list is very long, the query efficiency O(n) is poor. In this case, the list can be converted to an "AVL tree" or "Red-Black tree" to optimize the time complexity of the query operation to O(log n).

## Open addressing

Open addressing does not introduce additional data structures but instead handles hash collisions through "multiple probing". The probing methods mainly include linear probing, quadratic probing, and double hashing.
Let's use linear probing as an example to introduce the mechanism of open addressing hash tables.

1. Linear probing

Linear probing uses a fixed-step linear search for probing, differing from ordinary hash tables.

.Inserting Elements: Calculate the bucket index using the hash function. If the bucket already contains an element, linearly traverse forward from the conflict position (usually with a step size of 1 until an empty bucket is found, then insert the element.

. Searching for Elements: If a hash collision is encountered, use the same step size to linearly traverse forward until the corresponding element is found and return value; if an empty bucket is encountered, it means the target element is not in the hash table, so return None.

However, linear probing is prone to create "clustering". Specifically, the longer the continuously occupied positions in the array, the greater the probability of hash collisions occurring in these continuous positions, further promoting the growth of clustering at that position, forming a vicious cycle, and ultimately leading to degraded efficiency of insertion, deletion, query, and update operations.

It's important to note that we cannot directly delete elements in an open addressing hash table. Deleting an element creates an empty bucket None in the array. When searching for elements, if linear probing encounters this empty bucket, it will return, making the elements below this bucket inaccessible. The program may incorrectly assume these elements do not exist.

To solve this problem, we can adopt the lazy deletion mechanism: instead of directly removing elements from the hash table, use a constant TOMBSTONE to mark the bucket. In this mechanism, both None and TOMBSTONE represent empty buckets and can hold key-value pairs. However, when linear probing encounters TOMBSTONE, it should continue traversing since there may still be key-value pairs below it.

However, lazy deletion may accelerate the performance degradation of the hash table. Every deletion operation produces a delete mark, and as TOMBSTONE increases, the search time will also increase because linear probing may need to skip multiple TOMBSTONE to find the target element.


To address this, consider recording the index of the first encountered TOMBSTONE during linear probing and swapping the positions of the searched target element with that TOMBSTONE. The benefit of doing this is that each time an element is queried or added, the element will be moved to a bucket closer to its ideal position (the starting point of probing), thereby optimizing query efficiency.

The code below implements an open addressing (linear probing) hash table with lazy deletion. To make better use of the hash table space, we treat the hash table as a "circular array,". When going beyond the end of the array, we return to the beginning and continue traversing.


```ruby
class HashMapOpenAddressing:
    """Open addressing hash table"""

    def __init__(self):
        """Constructor"""
        self.size = 0  # Number of key-value pairs
        self.capacity = 4  # Hash table capacity
        self.load_thres = 2.0 / 3.0  # Load factor threshold for triggering expansion
        self.extend_ratio = 2  # Expansion multiplier
        self.buckets: list[Pair | None] = [None] * self.capacity  # Bucket array
        self.TOMBSTONE = Pair(-1, "-1")  # Removal mark

    def hash_func(self, key: int) -> int:
        """Hash function"""
        return key % self.capacity

    def load_factor(self) -> float:
        """Load factor"""
        return self.size / self.capacity

    def find_bucket(self, key: int) -> int:
        """Search for the bucket index corresponding to key"""
        index = self.hash_func(key)
        first_tombstone = -1
        # Linear probing, break when encountering an empty bucket
        while self.buckets[index] is not None:
            # If the key is encountered, return the corresponding bucket index
            if self.buckets[index].key == key:
                # If a removal mark was encountered earlier, move the key-value pair to that index
                if first_tombstone != -1:
                    self.buckets[first_tombstone] = self.buckets[index]
                    self.buckets[index] = self.TOMBSTONE
                    return first_tombstone  # Return the moved bucket index
                return index  # Return bucket index
            # Record the first encountered removal mark
            if first_tombstone == -1 and self.buckets[index] is self.TOMBSTONE:
                first_tombstone = index
            # Calculate the bucket index, return to the head if exceeding the tail
            index = (index + 1) % self.capacity
        # If the key does not exist, return the index of the insertion point
        return index if first_tombstone == -1 else first_tombstone

    def get(self, key: int) -> str:
        """Query operation"""
        # Search for the bucket index corresponding to key
        index = self.find_bucket(key)
        # If the key-value pair is found, return the corresponding val
        if self.buckets[index] not in [None, self.TOMBSTONE]:
            return self.buckets[index].val
        # If the key-value pair does not exist, return None
        return None

    def put(self, key: int, val: str):
        """Add operation"""
        # When the load factor exceeds the threshold, perform expansion
        if self.load_factor() > self.load_thres:
            self.extend()
        # Search for the bucket index corresponding to key
        index = self.find_bucket(key)
        # If the key-value pair is found, overwrite val and return
        if self.buckets[index] not in [None, self.TOMBSTONE]:
            self.buckets[index].val = val
            return
        # If the key-value pair does not exist, add the key-value pair
        self.buckets[index] = Pair(key, val)
        self.size += 1

    def remove(self, key: int):
        """Remove operation"""
        # Search for the bucket index corresponding to key
        index = self.find_bucket(key)
        # If the key-value pair is found, cover it with a removal mark
        if self.buckets[index] not in [None, self.TOMBSTONE]:
            self.buckets[index] = self.TOMBSTONE
            self.size -= 1

    def extend(self):
        """Extend hash table"""
        # Temporarily store the original hash table
        buckets_tmp = self.buckets
        # Initialize the extended new hash table
        self.capacity *= self.extend_ratio
        self.buckets = [None] * self.capacity
        self.size = 0
        # Move key-value pairs from the original hash table to the new hash table
        for pair in buckets_tmp:
            if pair not in [None, self.TOMBSTONE]:
                self.put(pair.key, pair.val)

    def print(self):
        """Print hash table"""
        for pair in self.buckets:
            if pair is None:
                print("None")
            elif pair is self.TOMBSTONE:
                print("TOMBSTONE")
            else:
                print(pair.key, "->", pair.val)

```

### Quadratic probing is similar to linear probing and is one of the common strategies of open addressing. When a collision occurs, quadratic probing does not simply skip a fixed number of steps but skips a number of steps equal to the "square of the number of probes", i.e., 1,4,9,.... steps

Quadratic probing has the following advantages:

Quadratic probing attempts to alleviate the clustering effect of linear probing by skipping the distance of the square of the number of probes.


Quadratic probing skips larger distances to find empty positions, which helps to distribute data more evenly.

However, quadratic probing is not perfect:

Clustering still exists, i.e., some positions are more likely to be occupied than others.

Due to the growth of squares, quadratic probing may not probe the entire hash table, meaning that even if there are empty buckets in the hash table, quadratic probing may not be able to access them.

