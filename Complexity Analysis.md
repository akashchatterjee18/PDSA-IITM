# Complexity Analysis

## 1. What Is Complexity?

Complexity analysis estimates how an algorithm's resource usage grows as the input size (n) increases.

- **Time complexity:** How the number of basic operations grows with input size.
- **Space complexity:** How the memory required by an algorithm grows with input size.
- **Input size ((n)):** The amount of data processed, such as the number of elements in a list.

Complexity is about growth rate, not the exact running time on one computer.

## 2. Asymptotic Notations

| Notation | Meaning | Typical use |
|---|---|---|
| (O(g(n))) — Big O | Asymptotic upper bound | Describes an upper limit on growth |
| (Omega(g(n))) — Big Omega | Asymptotic lower bound | Describes a lower limit on growth |
| (Theta(g(n))) — Big Theta | Tight asymptotic bound | Describes matching upper and lower growth |

For example, (3n^2 + 5n + 2 = Theta(n^2)), because the quadratic term dominates as (n) becomes large.

Big O is often used informally for worst-case complexity, but technically it describes an upper bound and does not itself mean “worst case”.

## 3. Common Complexity Classes

From generally more efficient growth to less efficient growth:

| Complexity | Name | Example |
|---|---|---|
| (O(1)) | Constant | Access an array element by index |
| (O(\log n)) | Logarithmic | Binary search in a sorted array |
| (O(n)) | Linear | Scan all elements once |
| (O(n\log n)) | Linearithmic | Typical efficient comparison sorts, such as merge sort |
| (O(n^2)) | Quadratic | Two nested loops over the same input |
| (O(n^3)) | Cubic | Three nested loops over the same input |
| (O(2^n)) | Exponential | Brute-force subset enumeration |
| (O(n!)) | Factorial | Brute-force enumeration of all permutations |

This ordering is about asymptotic growth for large (n). The actual performance of small inputs also depends on constants and implementation details.

## 4. Analysing Time Complexity

### A. Constant Time — (O(1))

The number of operations does not depend on (n).

```python
def first_element(items):
    return items[0]
```

Assuming index access is constant time, this takes (O(1)) time.

### B. Linear Time — (O(n))

One operation is performed for each element.

```python
def print_items(items):
    for item in items:
        print(item)
```

If the list has (n) elements, the loop runs (n) times. Time complexity: (O(n)).

### C. Quadratic Time — (O(n^2))

A nested loop may process every pair of elements.

```python
def print_pairs(items):
    for first in items:
        for second in items:
            print(first, second)
```

The inner loop runs (n) times for each of the (n) outer-loop iterations: (n \times n = n^2). Time complexity: (O(n^2)).

### D. Logarithmic Time — (O(\log n))

The input size is reduced by a constant factor at each step.

Binary search halves the search interval after each comparison. Its time complexity is (O(\log n)), provided the data is sorted and random access is available.

### E. Linearithmic Time — (O(n\log n))

Algorithms such as merge sort divide the input into smaller parts across about \(\log n\) levels and process a total of (O(n)) elements per level. Total time: (O(n\log n)).

## 5. Rules for Finding Time Complexity

1. **Drop constant factors:** (O(5n)) becomes (O(n)).
2. **Keep the fastest-growing term:** (O(n^2 + n + 10)) becomes (O(n^2)).
3. **Sequential sections:** Add their costs, then simplify. (O(n) + O(n^2) = O(n^2)).
4. **Nested loops:** Multiply iteration counts when they are independent. Two (n)-iteration loops nested together often give (O(n^2)).
5. **Halving or doubling:** Repeatedly halving (n) usually gives (O(\log n)) steps.
6. **Input-dependent loops:** Analyse the actual number of iterations; not every nested loop is quadratic.
7. **Conditionals:** Analyse the condition and the relevant branch. State whether you are discussing best, average, or worst case when it matters.
8. **Recursion:** Consider the number of recursive calls, the work per call, and the recursion depth.

## 6. Best, Average and Worst Case

- **Best case:** The minimum work for inputs of size (n).
- **Average case:** The expected work under a specified input distribution.
- **Worst case:** The maximum work for inputs of size (n).

Example: Linear search in a list:

| Case | Situation | Time |
|---|---|---|
| Best | Target is the first element | (O(1)) |
| Average | Target is around the middle, under a simple uniform-position assumption | (O(n)) |
| Worst | Target is last or absent | (O(n)) |

## 7. Space Complexity

Space complexity measures how memory usage grows with input size. Be clear about whether you are counting **total space** or **auxiliary space**.

- **Auxiliary space:** Extra memory used by the algorithm, excluding the input itself.
- A fixed number of variables typically uses (O(1)) auxiliary space.
- A new list containing (n) elements typically uses (O(n)) extra space.
- A recursive algorithm may use stack space proportional to its recursion depth.

Examples:

```python
def total(items):
    result = 0
    for item in items:
        result += item
    return result
```

This uses (O(1)) auxiliary space, excluding the input list.

```python
def doubled(items):
    result = []
    for item in items:
        result.append(item * 2)
    return result
```

This uses (O(n)) auxiliary space because the output list grows with the input.

## 8. Recursion and Complexity

For recursive algorithms, write a recurrence describing their running time.

Example: A function that reduces (n) by one at every call and does constant work per call:

[
T(n) = T(n-1) + O(1)
]

There are about (n) calls, so its time complexity is (O(n)). The recursion stack also uses (O(n)) space.

For binary search:

[
T(n) = T(n/2) + O(1)
]

The input is halved at each call, giving (O(\log n)) time. Its recursive stack depth is (O(\log n)).

For merge sort:

[
T(n) = 2T(n/2) + O(n)
]

This gives (O(n\log n)) time.

## 9. Quick Reference

| Code pattern | Typical time complexity |
|---|---|
| A fixed number of operations | (O(1)) |
| One loop through (n) items | (O(n)) |
| Two independent consecutive loops of size (n) | (O(n)) |
| Two nested loops of size (n) | (O(n^2)) |
| Loop that doubles an index until it reaches (n) | (O(\log n)) |
| Sorting using merge sort | (O(n\log n)) |
| Enumerating every subset of (n) items | (O(2^n)) |

These are common patterns, not universal rules. Always inspect the loop bounds, operations, data structures, and input assumptions.

## 10. Practice Questions

Try to determine the time complexity of each snippet.

**Q1**
```python
for i in range(n):
    print(i)
```

**Q2**
```python
for i in range(n):
    for j in range(n):
        print(i, j)
```

**Q3**
```python
i = n
while i > 1:
    i //= 2
```

**Q4**
```python
for i in range(n):
    for j in range(5):
        print(i, j)
```

### Answers

1. (O(n)) — one loop with (n) iterations.
2. (O(n^2)) — (n) iterations for each of (n) outer iterations.
3. (O(\log n)) — the value is halved each iteration.
4. (O(n)) — the inner loop runs a fixed five times, so the total work is proportional to (5n), which simplifies to (O(n)).

---

**Key idea:** Complexity analysis describes how resource usage scales as input size grows. Identify the input size, count the dominant work, simplify the growth rate, and state the assumptions.
