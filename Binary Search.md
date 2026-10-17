# Searching in a List

## Search Problem

**Problem:** Given a value \(v\) and a list \(L\), determine whether \(v\) is present in \(L\).

### Naive Search (Linear Search)

The naive approach scans the list element by element until the target is found or the list ends.

**Algorithm:**

1. Start from the first element.
2. Compare each element \(x\) with the target \(v\).
3. If \(x=v\), return `True`.
4. If the entire list is scanned without finding \(v\), return `False`.

**Python implementation:**

```python
def naive_search(v, L):
    for x in L:
        if v == x:
            return True
    return False
```

**Example:**

```python
naive_search(5, [2, 4, 5, 8, 10])
# True

naive_search(7, [2, 4, 5, 8, 10])
# False
```

### Complexity Analysis

Let \(n\) be the length of the list.

| Case | Number of comparisons | Time complexity |
|---|---|---|
| Best case | 1 | \(O(1)\) |
| Average case | Proportional to \(n\) | \(O(n)\) |
| Worst case | \(n\) | \(O(n)\) |

- **Best case:** The target is the first element.
- **Worst case:** The target is absent or appears at the last position.
- **Auxiliary space complexity:** \(O(1)\), because the algorithm uses a constant amount of extra space.

---

## Searching in a Sorted List

If a list is sorted in ascending order, we can use **Binary Search** to find an element more efficiently.

### Binary Search: Basic Idea

Instead of checking every element, binary search repeatedly divides the search interval into two halves.

**Algorithm:**

1. If the list is empty, return `False`.
2. Find the middle index.
3. Compare the target \(v\) with the middle element.
4. If they are equal, return `True`.
5. If \(v\) is smaller, search the left half.
6. Otherwise, search the right half.
7. Repeat until the target is found or the search interval becomes empty.

**Important:** Binary search requires the list to be sorted.

### Recursive Implementation

```python
def binary_search(v, L):
    if L == []:
        return False

    m = len(L) // 2

    if v == L[m]:
        return True

    if v < L[m]:
        return binary_search(v, L[:m])

    return binary_search(v, L[m + 1:])
```


### Complexity Analysis

Let \(n\) be the length of the list.

At each recursive call, the search interval is approximately halved.

| Case | Time complexity |
|---|---|
| Best case | \(O(1)\) |
| Average case | \(O(log n)\) |
| Worst case | \(O(log n)\) |

The number of halvings required to reduce a list of length \(n\) to a constant-sized interval is proportional to \(log n\).

- **Auxiliary space complexity:** \(O(log n)\) for the recursive call stack.
- **Additional allocation:** List slicing creates temporary lists. An iterative implementation avoids recursive calls and repeated slicing.

---

## Alternative Calculation: Binary Search Using Recurrence Relations

We can derive the time complexity of binary search mathematically using a recurrence relation.

Let \(T(n)\) represent the time required to search a list of length \(n\).

### Base Case

When the list is empty, the algorithm immediately returns `False`.

$$
T(0)=1
$$

Here, the constant \(1\) represents constant work.

### Recursive Case

For a non-empty list, binary search performs constant work to inspect the middle element and then searches at most half the list.

$$
T(n)=T\left(\left\lfloor\frac{n}{2}\right\rfloor\right)+1
$$

For simplicity, assume \(n\) is a power of two.

### Expanding the Recurrence

Starting with:

$$
T(n)=T\left(\frac{n}{2}\right)+1
$$

Substitute the recurrence repeatedly:

$$
T(n)=T\left(\frac{n}{4}\right)+2
$$

$$
T(n)=T\left(\frac{n}{8}\right)+3
$$

$$
T(n)=T\left(\frac{n}{2^k}\right)+k
$$

We stop when the remaining problem size becomes \(1\):

$$
\frac{n}{2^k}=1
$$

Therefore,

$$
2^k=n
$$

Taking logarithms to base \(2\):

$$
k=\log_2 n
$$

Substituting this value into the recurrence:

$$
T(n)=T(1)+\log_2 n
$$

Since \(T(1)\) is constant,

$$
T(n)=O(\log n)
$$

Thus, the time complexity of binary search is:

$$
\boxed{O(\log n)}
$$

### Intuition

Every step reduces the search space by approximately half.

| Search steps | Remaining elements |
|---:|---:|
| 0 | \(n\) |
| 1 | \(n/2\) |
| 2 | \(n/4\) |
| 3 | \(n/8\) |
| \(k\) | \(n/2^k\) |

This is why binary search is much faster than linear search for large, sorted lists.

---

## Linear Search vs Binary Search

| Property | Linear Search | Binary Search |
|---|---|---|
| Requires sorted list | No | Yes |
| Search strategy | Examine elements sequentially | Repeatedly halve the search interval |
| Best-case time | \(O(1)\) | \(O(1)\) |
| Worst-case time | \(O(n)\) | \(O(\log n)\) |
| Recursive implementation required | No | No |
| Suitable for unsorted lists | Yes | No |

**Key takeaway:** Use linear search when the list is unsorted or small. Use binary search when the list is sorted and efficient searching is important.
