---
slug: dynamic_programming
title: Implementing a 2D Dynamic Programming Solution
date: April 11, 2021
author: Pranav Ramesh
author_title: Technepreneur & blogger
author_url: https://github.com/pr28416
author_image_url: https://media-exp1.licdn.com/dms/image/C4D03AQE8US7zv3uUhQ/profile-displayphoto-shrink_400_400/0/1619024957277?e=1626912000&v=beta&t=cDgil4bLuNR5N8cVLnZHlmfiHcZ_ad0HKC2KsPbONfM
tags: [dynamic programming]
---

**Dynamic programming** is a quick, intuitive method of solving many problems. It is meant to solve a bigger problem by solving smaller "subproblems" and using the solutions of the subproblems to solve the bigger problems in turn. The key advantage of this is that once the solutions of the subproblems are calculated, they do not have to be recalculated, saving execution time.

One common dynamic programming approach is **memoization**, which essentially means to "remember" a previous subproblem's solution. While this may seem synonymous to dynamic programming, memoization is mostly only applicable for **one-dimensional problems**, or problems that only provide one input.

For instance, take the Fibonacci numbers. The `n`th fibonacci number is `f(n)`, where `f(n) = f(n-1) + f(n-2)`. A memoized approach would be to remember previous fibonacci numbers and use them to calculate the next. However, we can see that with this particular problem, only a single input, `n`, is given for us to attempt to find `f(n)`.

A **two-dimensional program** is one where two inputs, `n` and `k`, are given to produce `f(n, k)`, where the function `f` is our algorithm. One way to combat a two-dimensional program using dynamic programming would be to use the top-down approach, where smaller subproblems are solved using smaller inputs of `n` and `k`. The solutions for smaller inputs of `n` and `k` are solved, and gradually as `n` and `k` get bigger, it is much easier to calculate their solutions because previous subproblems have already been solved.

The best way to approach a two-dimensional program using top-down dynamic programming is to set up a table/grid, where one axis is `n` and the other is `k`​. When you code this, you will make a 2D array of these dimensions.

Let's say we are given the following problem:

* *Given two dimensions, n and k, find the number of distinct paths from one corner to the opposite (e.g. top-left to bottom-right)​*

While this problem can easily be solved using `nCr(n, k)`, we will take a dynamic programming approach.
​
We can begin by creating our 2d array, calling it `dp`. The row axis will be values for `n`, and the column axis will be values for `k​`.

```python title="Creating dp array"
def solution(N, K):
    # Create 2d DP array
    dp = [[0 for i in range(K+1)] for j in range(N+1)]
```

You would first establish one or more base cases, just like with recursion (although in this case we will use an iterative approach to traverse the 2D array). For instance, we can claim that whenever `n = 0` or `k = 0`, the values in those rows/columns will be 1, because there is only one way to travel from:

* A point to itself (`n = 0`, `k = 0`)
* A point to the opposite on the same line (`n = 0`, `k ≠ 0` or `n ≠ 0`, `k = 0`)

|n, k	|k = 0	|k = 1	|k = 2	|k = 3	|k = 4	|k = 5|
|---|---|---|---|---|---|---|
|n = 0|	1|	1|	1|	1|	1|	1|
|n = 1|	1|	0|	0|	0|	0|	0|
|n = 2|	1|	0|	0|	0|	0|	0|
|n = 3|	1|	0|	0|	0|	0|	0|
|n = 4|	1|	0|	0|	0|	0|	0|
|n = 5|	1|	0|	0|	0|	0|	0|
|n = 6|	1|	0|	0|	0|	0|	0|

```python title="Implementing base cases" {5-8}
def solution(N, K):
    # Create 2d DP array
    dp = [[0 for i in range(K+1)] for j in range(N+1)]
    
    # Base cases
    for i in range(max(N+1, K+1)):
        if i <= N: dp[i][0] = 1
        if i <= K: dp[0][i] = 1
```

Next, we must establish how we will solve the subproblems. Let's propose that a particular cell's solution is the sum of the cell directly to the left and directly above. `f(i, j) = f(i-1, j) + f(i, j-1)`. Therefore, we can write a nested loop to iterate through every cell of our `dp` array, and for every cell, we will equate it to its left cell and cell above it.

Note that when we traverse, we start at row/column 1 for each because we don't need to resolve our base cases.

```python title="Solving subproblems" {10-13}
def solution(N, K):
    # Create 2d DP array
    dp = [[0 for i in range(K+1)] for j in range(N+1)]
    
    # Base cases
    for i in range(max(N+1, K+1)):
        if i <= N: dp[i][0] = 1
        if i <= K: dp[0][i] = 1
        
    # Solving subproblems
    for n in range(1, N+1):
        for k in range(1, K+1):
            dp[n][k] = dp[n-1][k] + dp[n][k-1]
```

The final step is to return the bottom-right corner, because the dimensions for that corner, `(n, k)`, solve our overall problem.

|n, k	|k = 0	|k = 1	|k = 2	|k = 3	|k = 4	|k = 5|
|---|---|---|---|---|---|---|
|n = 0|	1|	1|1 	|1	|1      |1|
|n = 1|	1|	2|3 	|4	|5  	|6|
|n = 2|	1|	3|6 	|10	|15 	|21|
|n = 3|	1|	4|10    |20	|35	    |56|
|n = 4|	1|	5|15    |35	|70 	|126|
|n = 5|	1|	6|21    |56	|126	|252|
|n = 6|	1|	7|28    |84	|210	|462|

```python title="Return solved problem" {15-16}
def solution(N, K):
    # Create 2d DP array
    dp = [[0 for i in range(K+1)] for j in range(N+1)]
    
    # Base cases
    for i in range(max(N+1, K+1)):
        if i <= N: dp[i][0] = 1
        if i <= K: dp[0][i] = 1
        
    # Solving subproblems
    for n in range(1, N+1):
        for k in range(1, K+1):
            dp[n][k] = dp[n-1][k] + dp[n][k-1]
    
    # Return solved problem
    return dp[N][K]
```