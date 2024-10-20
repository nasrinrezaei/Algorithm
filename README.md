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
