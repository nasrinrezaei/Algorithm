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
     
