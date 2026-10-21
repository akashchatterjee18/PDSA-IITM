# Lists and Arrays

## Sequences

Two basic ways of storing a sequence of values are:

-   List
-   Array

## Lists

-   Flexible length (can vary).
-   Easy to modify.
-   Values are scattered in memory.

## Arrays

-   Fixed length.
-   Allocate a continuous block of memory.
-   Supports random access.

## Linked Lists

Typically, a sequence of nodes.

-   Each node contains a value and points to the next node in the
    sequence (linked list).

<img width="2172" height="724" alt="image" src="https://github.com/user-attachments/assets/8ec684be-66ff-471f-a159-e2b36bb21d35" />


-   `head` points to the first node.
-   `tail` refers to the last node.
-   The last node points to `None`.

This link makes it easy to modify the list.

### Inserting a Value

Insert a value `x` between nodes `vᵢ₋₁` and `vᵢ`:

<img width="2172" height="724" alt="image" src="https://github.com/user-attachments/assets/884cb7b3-022a-4ee9-916d-0acf1e2522f9" />


-   Insertion/deletion is easy via local "plumbing".
-   Need to follow links to access `A[i]`, which takes `O(i)` time.

## Arrays

-   Fixed size, declared in advance.
-   Allocate a continuous block of memory.
    -   `n` times the storage for a single value.

| Index    | Value  |
|----------|--------|
| `A[0]`   | `v₀`   |
| `A[1]`   | `v₁`   |
| `A[2]`   | `v₂`   |
| `…`      | `…`    |
| `A[i]`   | `vᵢ`   |
| `…`      | `…`    |
| `A[n-1]` | `vₙ₋₁` |

### Random Access

To access `A[i]`:

-   Compute the offset to `A[i]` from `A[0]`.

-   Accessing `A[i]` takes constant time, independent of `i`.

-   Inserting and deleting elements is expensive.

    -   Expanding and contracting requires moving `O(n)` elements in the
        worst case.

## Operations

### Exchange `A[i]` and `A[j]`

-   **List:** `O(n)` for lists.
-   **Array:** Constant time for arrays.

### Delete `A[i]` or Insert `v` After `A[i]`

-   **List:** Constant time for a list if we are already at `A[i]`.
-   **Array:** `O(n)` for arrays.

Need to keep the implementation in mind when analysing data structures.

## Implementing Lists in Python

### Python Class Node

A list is a sequence of nodes.

-   `self.value` is the stored value.
-   `self.next` is the next node.

Empty list? ---> `self.value` is `None`.

``` python
class Node:
    def __init__(self, v=None):
        self.value = v
        self.next = None

    def isempty(self):
        if self.value == None:
            return True
        else:
            return False
```

### Creating Lists

``` python
l1 = Node()    # Empty list
l2 = Node(5)   # Singleton list

l1.isempty()   # True
l2.isempty()   # False
```

## Appending to a List

### Recursive Implementation

Add `v` to the end of the list.

-   If the list is empty, update `l.value` from `None` to `v`.
-   If the last value is reached (`l.next` is `None`), `l.next` is
    `None`; point `next` at a new node with value `v`.
-   Otherwise, recursively append to the rest of the list.

``` python
def append(self, v):
    if self.isempty():
        self.value = v
    elif self.next == None:
        self.next = Node(v)
    else:
        self.next.append(v)
    return
```

### Iterative Implementation

-   If empty, replace `l.value` by `v`.
-   Loop through `l` until the end of the list.
-   Add `v` at the end.

``` python
def appendi(self, v):
    if self.isempty():
        self.value = v
        return

    temp = self
    while temp.next != None:
        temp = temp.next

    temp.next = Node(v)
    return
```

## Insert at the Start of the List

-   Want to insert `v` at the head.
-   Create a new node with `v`.
-   Cannot change where the head points, so this doesn't work directly.

So, we will exchange the values `v₀` and `v`, then make the new node
point to `head.next`, and then make `head.next` point to the new node.

``` python
def insert(self, v):
    if self.isempty():
        self.value = v
        return

    newnode = Node(v)

    (self.value, newnode.value) = (newnode.value, self.value)
    (self.next, newnode.next) = (newnode, self.next)

    return
```

## Delete a Value `v`

-   Remove the first occurrence of `v`.
-   Scan the list for the first `v` --- look ahead at the next node.
-   If the next node's value is `v`, bypass it.
-   Cannot bypass the first node in the list:
    -   Instead, copy the second node's value to the head and bypass the
        second node.

### Recursive Implementation

``` python
def delete(self, v):
    if self.isempty():
        return

    if self.value == v:
        self.value = None
        if self.next != None:
            self.value = self.next.value
            self.next = self.next.next
        return

    else:
        if self.next != None:
            self.next.delete(v)
            if self.next.value == None:
                self.next = None
        return
```

### Iterative Implementation

``` python
def deletei(self, v):
    if self.isempty():
        return

    if self.value == v:
        if self.next is None:
            self.value = None
        else:
            self.value = self.next.value
            self.next = self.next.next
        return

    temp = self
    while temp.next is not None:
        if temp.next.value == v:
            temp.next = temp.next.next
            return
        temp = temp.next

    return
```
