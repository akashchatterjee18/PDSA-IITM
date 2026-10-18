# Sorting Algorithms

## Sorting a List

Sorting a list makes many other computations easier, such as:

-   Binary search
-   Median finding
-   Checking for duplicates
-   Building a frequency table of values

## How Do We Sort a List?

### Problem

I am the TA for a course. The instructor has a pile of evaluated exam
papers in random order. My task is to arrange the papers in descending
order of marks.

## Selection Sort

### Strategy 1: Selecting the Minimum Repeatedly

1.  Scan the entire pile and find the paper with the minimum marks.
2.  Move this paper to a new pile.
3.  Repeat the process with the remaining papers.
4.  Eventually, the new pile is sorted in descending order.

This strategy is called **Selection Sort**.

### Selection Sort: Main Idea

-   Select the next element in sorted order.
-   Append it to the final sorted list.
-   To avoid using a second list, swap the minimum element into the
    first position, the second minimum into the second position, and so
    on.
-   Eventually, the list is rearranged in place in ascending order.

> **Note:** The paper-pile example describes descending order, while the
> code below sorts in ascending order.

### Python Code

``` python
def SelectionSort(L):
    n = len(L)

    if n < 1:
        return L

    for i in range(n):
        minpos = i

        for j in range(i + 1, n):
            if L[j] < L[minpos]:
                minpos = j

        L[i], L[minpos] = L[minpos], L[i]

    return L
```

### Analysis of Selection Sort

#### Correctness

Correctness follows from the loop invariant: at the beginning of each
outer-loop iteration, the prefix `L[:i]` contains the `i` smallest
elements in sorted order. The algorithm selects the minimum element from
the remaining suffix and places it at position `i`.

#### Efficiency

-   The outer loop iterates `n` times.
-   The inner loop searches the remaining suffix for the minimum
    element.
-   The number of comparisons is:

$$
T(n) = (n-1) + (n-2) + \cdots + 1 + 0
$$

Equivalently,

$$
T(n) = 0 + 1 + 2 + \cdots + (n-1)
$$

Using the arithmetic-series formula,

$$
T(n) = \frac{n(n-1)}{2} = \frac{n^2-n}{2}
$$

Therefore,

$$
T(n) \in O(n^2)
$$

Selection Sort uses (O(1)) auxiliary space when implemented in place.

## Insertion Sort

### Strategy 2: Inserting Each Paper into Its Correct Position

1.  Move the first paper to a new pile.
2.  Take the second paper:
    -   If its marks are lower than the first paper's, place it below.
    -   If its marks are higher, place it above.
3.  Take the third paper and insert it into the correct position among
    the first two papers.
4.  Repeat this process for all the remaining papers.

This process is called **Insertion Sort**.

### Insertion Sort: Main Idea

-   Start by building a sorted list.
-   Pick the next element and insert it into the correct position in the
    sorted portion.

#### Iterative formulation

-   Assume `L[:i]` is sorted.
-   Insert `L[i]` into `L[:i]` so that `L[:i+1]` becomes sorted.

#### Recursive formulation

-   Recursively sort `L[:-1]`.
-   Insert `L[-1]` into its correct position in the sorted list.

### Iterative Insertion Sort: Python Code

``` python
def InsertionSort(L):
    n = len(L)

    if n < 1:
        return L

    for i in range(n):
        j = i

        while j > 0 and L[j] < L[j - 1]:
            L[j], L[j - 1] = L[j - 1], L[j]
            j = j - 1

    return L
```

The iterative version updates the original list in place.

### Recursive Insertion Sort and Recursive Sorting Function: Python Code

``` python
def Insert(L, v):
    n = len(L)

    if n < 1:
        return [v]

    if v >= L[-1]:
        return L + [v]
    else:
        return Insert(L[:-1], v) + [L[-1]]

def ISort(L):
    n = len(L)

    if n < 1:
        return L

    L = Insert(ISort(L[:-1]), L[-1])
    return L
```

### Difference Between the Iterative and Recursive Versions

-   The **iterative Insertion Sort** updates the original list.
-   The **recursive version** returns a new sorted list.

## Analysis of Iterative Insertion Sort

### Correctness

Correctness follows from the loop invariant:

-   Before each iteration, `L[:i]` is sorted.
-   The algorithm moves `L[i]` left until it reaches its correct
    position.
-   Consequently, `L[:i+1]` is sorted.

### Efficiency

-   The outer loop runs `n` times.
-   In iteration `i`, the inner loop may perform up to `i` steps to
    insert `L[i]` into `L[:i]`.

In the worst case, the total number of steps is:

$$
T(n) = 0 + 1 + 2 + \cdots + (n-1)
$$

Therefore,

$$
T(n) = \frac{n(n-1)}{2}
$$

Hence,

$$
T(n) \in O(n^2)
$$

The worst-case time complexity of iterative Insertion Sort is (O(n\^2)).
Its best-case time complexity is (O(n)), when the list is already
sorted.

## Analysing the Recursive Functions

Let:

-   (TI(n)) be the time taken by `Insert` for a list of size `n`.
-   (TS(n)) be the time taken by `ISort` for a list of size `n`.

### Time Complexity of `Insert`

Base case:

$$
TI(0) = 1
$$

In each recursive call, `Insert` removes the last element from the list
and performs a constant amount of additional work.

$$
TI(n) = TI(n-1) + 1
$$

Expanding the recurrence,

$$
TI(n) = TI(n-2) + 1 + 1
$$

Continuing,

$$
TI(n) = TI(0) + n
$$

Thus, the time complexity is linear:

$$
TI(n) \in O(n)
$$

### Time Complexity of `ISort`

Base case:

$$
TS(0) = 1
$$

Each call to `ISort` recursively sorts a list of size `n-1`, then calls
`Insert` on a list of size `n-1`.

$$
TS(n) = TS(n-1) + TI(n-1)
$$

Since $T_I(n) \in O(n)$, expanding the recurrence gives:

$$
TS(n) = 1 + 2 + \cdots + (n-1) + \text{constant work}
$$

Using the arithmetic-series formula,

$$
TS(n) \approx \frac{n(n-1)}{2}
$$

Therefore,

$$
TS(n) \in O(n^2)
$$
