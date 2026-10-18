# Merge Sort

## 1. Why Do We Need a Better Sorting Algorithm?

Both **Selection Sort** and **Insertion Sort** take quadratic time in
the worst case:

$$
O(n^2)
$$

For sufficiently large inputs (for example, around (n \> 10{,}000),
depending on the machine and implementation), quadratic-time sorting can
become impractical.

Therefore, we look for an algorithm that performs better than (O(n\^2)).

------------------------------------------------------------------------

## 2. Strategy 3: Divide and Conquer

The strategy is:

1.  Divide the list into two halves.
2.  Sort the left half and the right half separately.
3.  Combine the two sorted halves to obtain one fully sorted list.

This is the basic idea behind **Merge Sort**.

### Divide-and-conquer pattern

-   **Divide:** Break the problem into smaller parts.
-   **Conquer:** Solve each part separately, usually recursively.
-   **Combine:** Combine the solutions efficiently.

------------------------------------------------------------------------

## 3. Merging Two Sorted Lists

Suppose `A` and `B` are already sorted lists. The goal is to combine
them into one sorted list `C`.

### Procedure

1.  Compare the first unprocessed element of `A` with the first
    unprocessed element of `B`.
2.  Move the smaller element into `C`.
3.  Advance the position in the list from which the element was taken.
4.  Repeat until one list has no elements left.
5.  Append all remaining elements from the other list to `C`.

If `A` is empty, append the remaining elements of `B` to `C`. If `B` is
empty, append the remaining elements of `A` to `C`.

### Example

Let the two sorted lists be:

``` text
A = [32, 74, 89]
B = [21, 55, 64]
```

Merge them by repeatedly taking the smaller front element:

-   Compare `32` and `21` → take `21`.
-   Compare `32` and `55` → take `32`.
-   Compare `74` and `55` → take `55`.
-   Compare `74` and `64` → take `64`.
-   `B` is now exhausted, so append the remaining elements of `A`:
    `74, 89`.

The result is:

``` text
C = [21, 32, 55, 64, 74, 89]
```

### Python implementation: merging two sorted lists

``` python
def merge(A, B):
    (m, n) = (len(A), len(B))
    (C, i, j, k) = ([], 0, 0, 0)

    while k < m + n:
        if i == m:
            C.extend(B[j:])
            k = k + (n - j)

        elif j == n:
            C.extend(A[i:])
            k = k + (m - i)

        elif A[i] < B[j]:
            C.append(A[i])
            (i, k) = (i + 1, k + 1)

        else:
            C.append(B[j])
            (j, k) = (j + 1, k + 1)

    return C
```

### Meaning of the variables

-   `A`, `B`: the two sorted input lists.
-   `m`, `n`: lengths of `A` and `B`.
-   `C`: the output list.
-   `i`: index of the next unprocessed element of `A`.
-   `j`: index of the next unprocessed element of `B`.
-   `k`: number of elements already placed in `C`.

The loop continues while `k < m + n`, because the output must contain
all `m + n` elements.

**Important cases:**

-   If `i == m`, all elements of `A` have been processed. Append
    `B[j:]`.
-   If `j == n`, all elements of `B` have been processed. Append
    `A[i:]`.
-   Otherwise, compare `A[i]` and `B[j]`, and append the smaller one.

The expression `A[i] < B[j]` means that when the values are equal, the
element from `B` is chosen first. The output remains sorted, but this
implementation is not stable when equal keys occur in both lists.

------------------------------------------------------------------------

## 4. Merge Sort Algorithm

Let `n` be the length of list `A`.

1.  If `n <= 1`, return `A`: a list containing zero or one element is
    already sorted.
2.  Split the list into two halves:
    -   Left half: `A[:n//2]`
    -   Right half: `A[n//2:]`
3.  Recursively sort each half.
4.  Merge the two sorted halves.
5.  Return the merged list.

### Python implementation

``` python
def mergesort(A):
    n = len(A)

    if n <= 1:
        return A

    L = mergesort(A[:n//2])
    R = mergesort(A[n//2:])

    B = merge(L, R)
    return B
```

The slices `A[:n//2]` and `A[n//2:]` divide the list into two parts. For
odd-length lists, the two halves may differ in length by one.

The recursive calls continue until each sublist contains at most one
element. The sorted sublists are then merged as the recursion returns.

------------------------------------------------------------------------

## 5. Example: Sorting a List

Consider the input:

``` text
A = [43, 32, 22, 78, 63, 57, 91, 13]
```

### Step 1: Divide into two halves

``` text
[43, 32, 22, 78]       [63, 57, 91, 13]
```

### Step 2: Divide again

``` text
[43, 32] [22, 78]      [63, 57] [91, 13]
```

### Step 3: Divide into single-element lists

``` text
[43] [32] [22] [78]    [63] [57] [91] [13]
```

A single-element list is already sorted.

### Step 4: Merge adjacent single-element lists

``` text
[32, 43] [22, 78]      [57, 63] [13, 91]
```

### Step 5: Merge the sorted pairs

``` text
[22, 32, 43, 78]       [13, 57, 63, 91]
```

### Step 6: Merge the two sorted halves

``` text
[13, 22, 32, 43, 57, 63, 78, 91]
```

The final list is sorted in ascending order.

### Recursion pattern

The question "How do we sort `A[:n//2]` and `A[n//2:]`?" is answered by
**recursion**: apply the same Merge Sort strategy to each half.

------------------------------------------------------------------------

## 6. Analysis of the `merge` Function

Suppose:

-   `A` has length (m).
-   `B` has length (n).
-   The output list `C` has (m+n) elements.

During each iteration of the main loop, at least one element is added to
`C`. Once either input list is exhausted, the remaining elements of the
other list are appended.

Therefore, the total number of elements processed is proportional to
(m+n).

The time complexity of merging is:

$$
T_{\text{merge}}(m,n) = O(m+n)
$$

Since

$$
m+n \leq 2\max(m,n),
$$

we can also express the bound as:

$$
O(\max(m,n))
$$

When both input lists have approximately the same length, this is linear
in their common length.

**Space complexity:** The function creates a new output list containing
(m+n) elements, so the auxiliary space required for the output is
(O(m+n)).

------------------------------------------------------------------------

## 7. Analysis of the `mergesort` Function

Let (T(n)) denote the time taken by Merge Sort for an input of size (n).

For simplicity, assume that (n) is a power of two. The base case is a
list of one element:

$$
T(1)=1
$$

For an input of size (n):

-   Two recursive calls sort two halves, each of size (n/2).
-   Merging the two sorted halves takes linear time, proportional to
    (n).

Hence, the recurrence is:

$$
T(n)=2T\left(\frac{n}{2}\right)+n
$$

### Expanding the recurrence

Start with:

$$
T(n)=2T\left(\frac{n}{2}\right)+n
$$

Expand (T(n/2)):

$$
T\left(\frac{n}{2}\right)
=2T\left(\frac{n}{4}\right)+\frac{n}{2}
$$

Substitute this into the original recurrence:

$$
T(n)=2\left[2T\left(\frac{n}{4}\right)+\frac{n}{2}\right]+n
$$

Simplifying:

$$
T(n)=4T\left(\frac{n}{4}\right)+2n
$$

Expand once more:

$$
T(n)=8T\left(\frac{n}{8}\right)+3n
$$

After (k) expansions, the general form is:

$$
T(n)=2^kT\left(\frac{n}{2^k}\right)+kn
$$

### Finding the number of levels

The recursion reaches the base case when the subproblem size becomes
(1):

$$
\frac{n}{2^k}=1
$$

Therefore,

$$
2^k=n
$$

Taking logarithms to base (2):

$$
k=\log_2 n
$$

Substitute (k=`\log`{=tex}\_2 n) into the expanded recurrence:

$$
T(n)=2^{\log_2 n}T(1)+n\log_2 n
$$

Using (2\^{`\log`{=tex}\_2 n}=n) and (T(1)=1):

$$
T(n)=n+n\log_2 n
$$

Thus,

$$
T(n)=n(\log_2 n+1)
$$

The dominant term is (n`\log `{=tex}n), so the time complexity is:

$$
\boxed{T(n)=O(n\log n)}
$$

More precisely, Merge Sort has time complexity
(`\Theta`{=tex}(n`\log `{=tex}n)) in the best, average, and worst cases
when merging is linear.

------------------------------------------------------------------------

## 8. Key Takeaways

-   Selection Sort and Insertion Sort have (O(n\^2)) worst-case time
    complexity.

-   Merge Sort uses the **divide-and-conquer** strategy.

-   Merge Sort recursively divides a list into smaller halves and merges
    the sorted halves.

-   Merging lists of lengths (m) and (n) takes (O(m+n)) time.

-   Merge Sort satisfies the recurrence:

    $$
    T(n)=2T\left(\frac{n}{2}\right)+n
    $$

-   Its time complexity is:

    $$
    \boxed{\Theta(n\log n)}
    $$

-   The usual list-based implementation uses (O(n)) auxiliary space for
    merging, in addition to the recursion stack.

-   Merge Sort is stable when equal elements from the left list are
    selected before equal elements from the right list. In the code
    above, the comparison uses `<`, so equal elements from `B` are
    selected first; using `<=` instead would preserve stability for
    ordinary ascending sorting.
