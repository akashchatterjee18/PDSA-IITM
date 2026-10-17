# Complexity Analysis

> Consolidated notes from the lecture notebook: algorithmic efficiency, growth rates, asymptotic notation, iterative analysis, and recurrences.

## What Is Complexity?

Complexity analysis studies how an algorithm's resource usage grows with input size.

- **Time complexity:** Number of basic operations performed.
- **Space complexity:** Memory used by the algorithm.
- **Input size:** Depends on the problem: list length, number of graph vertices/edges, number of points, or number of bits representing an integer.

Actual runtime depends on hardware, language, implementation, and other factors. Complexity analysis compares growth rates rather than relying only on seconds.

## Measuring Running Time

- Analyse the algorithm independently of the underlying hardware.
- Count basic operations such as comparisons, assignments, arithmetic operations, and data accesses.
- Different inputs of the same size can require different amounts of work, so distinguish best, average, and worst cases.
- The worst case gives an upper performance guarantee across valid inputs of size n.

For example, searching an unsorted list may stop early if a target is near the beginning. If the target is absent, every element must be checked.

### Input-size examples

- List: n = length of the list.
- Graph: often described using vertices V and edges E.
- Positive integer N: its binary input length is floor(log₂ N) + 1, not N itself.

## Common Growth Rates

From slower growth to faster growth for large n:

| Complexity | Name | Typical example |
|---|---|---|
| O(1) | Constant | Access an array element by index |
| O(log n) | Logarithmic | Binary search |
| O(n) | Linear | Scan a list |
| O(n log n) | Linearithmic | Merge sort |
| O(n²) | Quadratic | Compare all pairs |
| O(n³) | Cubic | Three nested loops over size-n dimensions |
| O(2ⁿ) | Exponential | Enumerate all subsets |
| O(n!) | Factorial | Enumerate all permutations |

Constants and implementation details can still matter for small inputs.

### Example growth table

The entries below show the approximate number of steps for common growth functions. Values such as 2ⁿ and n! become enormous very quickly, so scientific notation is used.

| Input n | log₂ n | n | n log₂ n | n² | n³ | 2ⁿ (approx.) | n! (approx.) |
|---:|---:|---:|---:|---:|---:|---:|---:|
| 10 | 3.32 | 10 | 33 | 10² | 10³ | 10³ | 10⁶ |
| 10² | 6.64 | 10² | 664 | 10⁴ | 10⁶ | 10³⁰ | 10¹⁵⁸ |
| 10³ | 9.97 | 10³ | ≈ 10⁴ | 10⁶ | 10⁹ | 10³⁰¹ | 10²⁵⁶⁸ |
| 10⁴ | 13.29 | 10⁴ | ≈ 1.3 × 10⁵ | 10⁸ | 10¹² | 10³⁰¹⁰ | 10³⁵⁶⁶⁰ |
| 10⁵ | 16.61 | 10⁵ | ≈ 1.7 × 10⁶ | 10¹⁰ | 10¹⁵ | 10³⁰¹⁰³ | 10⁴⁵⁶⁵⁷⁴ |
| 10⁶ | 19.93 | 10⁶ | ≈ 2.0 × 10⁷ | 10¹² | 10¹⁸ | 10³⁰¹⁰³⁰ | 10⁵⁵⁶⁵⁷⁰⁹ |

*The 2ⁿ and n! columns are order-of-magnitude approximations, not exact values. The factorial estimates use Stirling's approximation.*

<img width="621" height="428" alt="image" src="https://github.com/user-attachments/assets/b17b55e8-9208-40cd-be35-7220fcb74ffd" />

**How to read the table:**

- log₂ n grows very slowly. It is the number of times n can be halved before reaching about 1.
- n grows proportionally to the input size.
- n log₂ n grows faster than linear but much more slowly than quadratic.
- n² and n³ become costly for large inputs.
- 2ⁿ and n! explode even for relatively small inputs, making exhaustive algorithms impractical very quickly.

Quadratic and cubic algorithms become impractical quickly as n grows.

## Real-World Motivation: Matching Aadhaar Records and SIM Records

Suppose there are 10⁹ Aadhaar records and 10⁹ SIM records, and we want to identify matching records. This is a simplified algorithm-analysis illustration, not a model of an actual identity system.

### Naive approach: compare every pair

The number of pairs is approximately:

$$
10^9 \times 10^9 = 10^{18}
$$

At 10⁷ basic operations per second:

$$
\frac{10^{18}}{10^7}=10^{11}\text{ seconds}
$$

That is approximately **3,170 years**, using about 31.6 million seconds per year.

### Better approach: sort/index and search

If one collection is sorted or indexed, each lookup can take about log₂ n comparisons rather than checking all n records.

$$
\log_2(10^9)\approx30
$$

For 10⁹ lookups, this is approximately:

$$
10^9\times30=3\times10^{10}\text{ comparisons}
$$

At 10⁷ operations per second, this is about 3,000 seconds, or **50 minutes**, under the simplified assumption that lookup comparisons dominate and the data is already sorted/indexed. Sorting, disk I/O, data cleaning, and overhead can add significant time.

**Lesson:** a better algorithm can matter far more than simply using faster hardware.

## Real-World Motivation: Closest Pair of Points

Given n points on a screen, find the pair with the smallest distance.

### Naive algorithm

Compare every unique pair:

$$
\binom{n}{2}=\frac{n(n-1)}{2}
$$

Therefore, time complexity is Θ(n²).

For n = 100,000:

$$
\frac{100000\times99999}{2}\approx5\times10^9\text{ pairs}
$$

At a hypothetical 10⁷ operations per second, this is roughly 500 seconds (about 8.3 minutes) if each pair takes one operation. Actual distance calculations and language overhead may increase the time.

### More efficient algorithm

A standard divide-and-conquer closest-pair algorithm runs in O(n log n) time under its usual assumptions.

$$
n\log_2 n=100000\times\log_2(100000)\approx1.66\times10^6
$$

This is dramatically fewer operations than about 5 × 10⁹ pair comparisons.

A 4000 × 2000 image has 8 × 10⁶ pixel positions. Treating every pixel as a point would make a naive all-pairs algorithm especially expensive.

## Asymptotic Notation

Asymptotic notation describes growth as input size becomes large. It does not predict exact runtime.

### Big O — upper bound

$$
f(n)\in O(g(n))
$$

There must exist constants c > 0 and n₀ ≥ 0 such that:

$$
0\le f(n)\le c\,g(n)\quad\text{for all }n\ge n_0
$$

Eventually, f(n) is at most a constant multiple of g(n).

**Example:** Show that 100n + 5 ∈ O(n²).

For n ≥ 1, n ≤ n² and 1 ≤ n². Therefore:

$$
100n+5\le100n^2+5n^2=105n^2
$$

Choose c = 105 and n₀ = 1.

A tighter bound is also possible: for n ≥ 1, 100n + 5 ≤ 105n, so 100n + 5 ∈ O(n). The tight growth rate is Θ(n).

**Another example:** 100n² + 20n + 5 ∈ O(n²).

For n ≥ 1:

$$
100n^2+20n+5\le100n^2+20n^2+5n^2=125n^2
$$

Choose c = 125 and n₀ = 1.

### Big Omega — lower bound

$$
f(n)\in\Omega(g(n))
$$

There must exist constants c > 0 and n₀ ≥ 0 such that:

$$
0\le c\,g(n)\le f(n)\quad\text{for all }n\ge n_0
$$

**Example:**

$$
n^3\in\Omega(n^2)
$$

For n ≥ 1, n³ ≥ n². Choose c = 1 and n₀ = 1.

Lower bounds can also describe a limit that applies to every algorithm solving a problem. For example, comparison-based sorting requires Ω(n log n) comparisons in the worst case.

### Big Theta — tight bound

$$
f(n)\in\Theta(g(n))
$$

There must exist constants c₁, c₂ > 0 and n₀ ≥ 0 such that:

$$
c_1g(n)\le f(n)\le c_2g(n)\quad\text{for all }n\ge n_0
$$

This means f(n) has matching asymptotic upper and lower bounds.

**Example:**

$$
f(n)=\frac{n(n-1)}2=\frac{n^2}2-\frac n2
$$

For n ≥ 1:

$$
f(n)\le\frac{n^2}{2}
$$

Choose c₂ = 1/2. For n ≥ 2, n ≤ n²/2, so:

$$
f(n)=\frac{n^2}2-\frac n2\ge\frac{n^2}4
$$

Choose c₁ = 1/4 and n₀ = 2. Therefore:

$$
\frac{n^2}4\le f(n)\le\frac{n^2}2\quad(n\ge2)
$$

Hence f(n) ∈ Θ(n²).

### Important distinction

- **O:** upper bound.
- **Ω:** lower bound.
- **Θ:** tight bound.

Big O is often used to report worst-case complexity, but Big O does not itself mean worst case. The case (best, average, or worst) and the asymptotic bound are separate concepts.

### Higher-order functions cannot be bounded by lower-order ones

$$
n^3\notin O(n^2)
$$

No fixed constant c can make n³ ≤ cn² for all sufficiently large n, because this would require n ≤ c forever.

## Properties of Asymptotic Bounds

### Sum rule

If f₁(n) ∈ O(g₁(n)) and f₂(n) ∈ O(g₂(n)), then:

$$
f_1(n)+f_2(n)\in O(\max(g_1(n),g_2(n)))
$$

For sequential phases, add the running times and keep the dominant growth rate.

Example: phase A takes O(n), phase B takes O(n²):

$$
O(n)+O(n^2)=O(n^2)
$$

### Product rule

If an outer loop runs n times and an inner loop runs m times per outer iteration, the total work is often O(nm).

Three nested loops with iteration counts m, n, and p often give O(mnp).

### Ignore constants and lower-order terms

$$
O(5n)=O(n)
$$

$$
O(n^2+n+10)=O(n^2)
$$

The fastest-growing term dominates as n becomes large.

## Analysing Iterative Programs

### Example 1: Find the maximum element

~~~python
def max_element(L):
    maxval = L[0]
    for i in range(1, len(L)):
        if L[i] > maxval:
            maxval = L[i]
    return maxval
~~~

- Input size: n = len(L).
- The loop scans the remaining elements once.
- At most n − 1 comparisons occur.
- **Time:** Θ(n).
- **Auxiliary space:** Θ(1).
- Assumption: the list is non-empty.

### Example 2: Check whether a list contains duplicates

~~~python
def no_duplicates(L):
    for i in range(len(L)):
        for j in range(i + 1, len(L)):
            if L[i] == L[j]:
                return False
    return True
~~~

Each unordered pair is compared at most once. If no duplicates exist, the comparison count is:

$$
(n-1)+(n-2)+\cdots+2+1=\frac{n(n-1)}2
$$

- **Worst-case time:** Θ(n²).
- **Best-case time:** Θ(1) if a duplicate is found in the first comparison (for a list with at least two elements).
- **Auxiliary space:** Θ(1).

Early return can reduce work for some inputs but does not change the worst-case bound.

### Example 3: Matrix multiplication

Let A have dimensions m × n and B have dimensions n × p. Their product C = AB has dimensions m × p.

~~~python
def matrix_multiply(a, b):
    m, n, p = len(a), len(a[0]), len(b[0])
    c = [[0 for _ in range(p)] for _ in range(m)]

    for i in range(m):
        for j in range(p):
            for k in range(n):
                c[i][j] += a[i][k] * b[k][j]

    return c
~~~

- The loops iterate m, p, and n times.
- **Time:** Θ(mnp) for this standard algorithm.
- If all dimensions equal n, time becomes Θ(n³).
- The output matrix uses Θ(mp) space. Including the output, extra storage beyond the inputs is Θ(mp).

### Example 4: Number of bits in a positive integer

~~~python
def number_of_bits(n):
    count = 1
    while n > 1:
        count += 1
        n //= 2
    return count
~~~

For a positive integer n, the number of binary digits is:

$$
\lfloor\log_2 n\rfloor+1
$$

- Measured against the numeric value n, the loop takes Θ(log n) iterations.
- If input size is the number of binary digits b, the algorithm takes Θ(b) iterations.
- Assumption: n ≥ 1.

## Recursion and Recurrence Relations

Recursive algorithms call themselves on smaller inputs. Use a recurrence to describe their work.

### Example 1: Tower of Hanoi

Goal: move n disks from peg A to peg B using peg C as the auxiliary peg. Only one disk may move at a time, and a larger disk may never be placed on a smaller disk.

Recursive solution:

1. Move n − 1 disks from A to C, using B as auxiliary.
2. Move the largest disk from A to B.
3. Move n − 1 disks from C to B, using A as auxiliary.

Let M(n) be the minimum number of moves.

Base case:

$$
M(1)=1
$$

Recurrence:

$$
M(n)=M(n-1)+1+M(n-1)=2M(n-1)+1
$$

Expanding:

$$
\begin{aligned}
M(n)&=2M(n-1)+1\\
&=4M(n-2)+3\\
&=8M(n-3)+7\\
&=\cdots=2^n-1
\end{aligned}
$$

Thus:

$$
\boxed{M(n)=2^n-1}
$$

For five disks:

$$
M(5)=2^5-1=31\text{ moves}
$$

The number of moves is Θ(2ⁿ), so the algorithm grows exponentially.


## Quick Reference: Code Patterns

| Pattern | Typical time |
|---|---|
| Fixed number of operations | Θ(1) |
| One loop through n items | Θ(n) |
| Two consecutive loops, each of size n | Θ(n) |
| Two nested loops, each of size n | Θ(n²) |
| Three nested loops, each of size n | Θ(n³) |
| Repeatedly halve/double a value until a threshold | Θ(log n) iterations |
| Each of n items uses a logarithmic search | Θ(n log n) |
| Enumerate every subset | Θ(2ⁿ) subsets |
| Enumerate every permutation | Θ(n!) permutations |

These are common patterns, not universal rules. Inspect the actual loop bounds and operations.


## Key Takeaways

- Complexity describes how resource usage scales with input size.
- Count basic operations rather than depending solely on measured seconds.
- Consider input size, best/average/worst case, and memory usage.
- Big O is an upper bound, Big Omega a lower bound, and Big Theta a tight bound.
- For sequential phases, add costs; for nested loops, count combined iterations.
- A better algorithm can make an otherwise infeasible problem practical.
- For recursion, formulate a recurrence and solve it.
