

# CMPS 2200 Assignment 1

**Name:** Sofia Bareiro


In this assignment, you will learn more about asymptotic notation, parallelism, functional languages, and algorithmic cost models. As in the recitation, some of your answer will go here and some will go in `main.py`. You are welcome to edit this `assignment-01.md` file directly, or print and fill in by hand. If you do the latter, please scan to a file `assignment-01.pdf` and push to your github repository. 
  
  

1. (2 pts ea) **Asymptotic notation** (12 pts)

  - 1a. Is $2^{n+1} \in O(2^n)$? Why or why not?
  - **The statement is true because 2^n+1 is equal to 2*2^n. In Big-O notation we're concerned with how functions grow as n becomes larger. Since both of them grow at the same rate, then 2^n+1 is just a constant multiple of 2^n.**

    
  - 1b. Is $2^{2^n} \in O(2^n)$? Why or why not?
  - **The statement is false because the left side grows faster than 2^n.**
    
  
  - 1c. Is $n^{1.01} \in O(\mathrm{log}^2 n)$?
  - **This is false because n^1.01 grows faster than long^2(n).A polynomial function like n^1.01 grow much faster than log functions for large n.**
  

  - 1d. Is $n^{1.01} \in \Omega(\mathrm{log}^2 n)$?
  - **This is true because n^1.01 grows faster than log^2(n), and therefore provides a lower bound. Since n^1.01 grows much faster than log^2(n), we can say that n^1.01 provides a lower bound to log^2 n as n grows larger.**


  - 1e. Is $\sqrt{n} \in O((\mathrm{log} n)^3)$?
  - **This is false because sqrt(n) grows much faster than (logn)^3, as sqrt(n) is a polynomial function and (logn)^3 is a log function. Since polynomial functions grow faster than log functions for large n, the left side cannot be bounded to the right side.**


  - 1f. Is $\sqrt{n} \in \Omega((\mathrm{log} n)^3)$?
  - **This is true because omega denotes a lower bound. Since the left side grows faster than the right side, we can say that the left side provides a lower bound to the right side.**


2. **SPARC to Python** (12 pts)

Consider the following SPARC code of the Fibonacci sequence, which is the series of numbers where each number is the sum of the two preceding numbers. For example, 0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610 ... 
$$
\begin{array}{l}
\mathit{foo}~x =   \\
~~~~\texttt{if}{}~~x \le 1~~\texttt{then}{}\\
~~~~~~~~x\\   
~~~~\texttt{else}\\
~~~~~~~~\texttt{let}{}~~(ra, rb) = (\mathit{foo}~(x-1))~~,~~(\mathit{foo}~(x-2))~~\texttt{in}{}\\  
~~~~~~~~~~~~ra + rb\\  
~~~~~~~~\texttt{end}{}.\\
\end{array}
$$ 

  - 2a. (6 pts) Translate this to Python code -- fill in the `def foo` method in `main.py`  

  - 2b. (6 pts) What does this function do, in your own words?
- The function foo(x) calculates the x-th Fibonacci number. It does so by recursively calling itself to compute the sum of the two preceding Fibonacci numbers, until it reaches the base case of x=0 or x=1.
  

3. **Parallelism and recursion** (26 pts)

Consider the following function:  

```python
def longest_run(myarray, key)
   """
    Input:
      `myarray`: a list of ints
      `key`: an int
    Return:
      the longest continuous sequence of `key` in `myarray`
   """
```
E.g., `longest_run([2,12,12,8,12,12,12,0,12,1], 12) == 3`  
 
  - 3a. (7 pts) First, implement an iterative, sequential version of `longest_run` in `main.py`.  

  - 3b. (4 pts) What is the Work and Span of this implementation?
- The work is the total number of operations performed. Since we are iterating through the array once, the work is porportional to the size of the array, which is O(n), where n is the length of the array.
- The span is the longest chain of dependent operations. Since this function only uses a single loop and no nested operations, there are no parallel dependencies. The span is constant, or O(1). 


  - 3c. (7 pts) Next, implement a `longest_run_recursive`, a recursive, divide and conquer implementation. This is analogous to our implementation of `sum_list_recursive`. To do so, you will need to think about how to combine partial solutions from each recursive call. Make use of the provided class `Result`.   

  - 3d. (4 pts) What is the Work and Span of this sequential algorithm?
- Work is O(n), where n is the size of the input list. Span is O(logn), since the recursive function fivides the input list in half at each step.  


  - 3e. (4 pts) Assume that we parallelize in a similar way we did with `sum_list_recursive`. That is, each recursive call spawns a new thread. What is the Work and Span of this algorithm?
- Work is still O(n), because each element is processed once in the recursive calls. Span is O(logn). 

