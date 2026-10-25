# DSA Notes — Learn from Basics to Advanced
### Data Structures Using C (CSIT124) · Viva Edition

**Covers:** Modules I, II, III and V of your syllabus. **Leaves out:** Module IV (Trees) and Module VI (Graphs).

These notes are arranged in the order **DSA is actually learned**, not in syllabus-module order. Every chapter uses only ideas from the chapters before it, so you can start at Chapter 1 knowing nothing and read straight through. Each chapter begins with a small box saying **which syllabus module it belongs to** (examiners sometimes ask), **what it builds on**, and **why it comes at that point**.

> **How to study**
> 1. Read one chapter at a time, in order. Don't skip ahead. Later chapters assume the earlier ones.
> 2. For every topic, learn it as **Definition → Example → How it works → Complexity → Where it's used**. Answer viva questions in the same order.
> 3. Type out and run the C programs yourself. The **lab programs** from your syllabus are marked "(Lab Program N)".
> 4. At the end of each chapter, answer the **Check Yourself** questions out loud without looking.
> 5. On the last night, read only **Part A (Rapid-Fire Q&A)** and **Part B (Cheat Sheet)** at the end.

## The Learning Roadmap

```
STAGE 1 · FOUNDATIONS
   1 What Are Data Structures? ─► 2 C Toolkit (struct, pointers, malloc) ─► 3 Algorithms & Complexity
                                                │
STAGE 2 · THE FIRST DATA STRUCTURE              ▼
   4 Arrays ─► 5 Strings ─► 6 Sparse Matrices
                    │
STAGE 3 · WORKING ON ARRAYS                     ▼
   7 Searching ─► 8 Simple Sorting (bubble, selection, insertion, shell)
                    │
STAGE 4 · THINKING RECURSIVELY                  ▼
   9 Recursion & Tower of Hanoi ─► 10 Merge Sort & Quick Sort
                    │
STAGE 5 · DYNAMIC MEMORY                        ▼
   11 Linked Lists
                    │
STAGE 6 · RESTRICTED LISTS (built with arrays AND linked lists)
   12 Stacks ─► 13 Queues
                    │
STAGE 7 · ADVANCED                              ▼
   14 Hashing ─► 15 Heaps & Heap Sort ─► 16 Sorting Wrap-up
```

**Why this order?**
- You can't build a linked list without **structs, pointers and malloc**, so those come first.
- **Complexity** comes early because every later topic is judged by it ("this is O(n), that is O(log n)").
- **Arrays** are the simplest structure. Searching and the simple sorts only need arrays and loops.
- **Recursion** must come before **merge sort and quick sort**, because both are recursive.
- **Linked lists** come before **stacks and queues**, so you can build stacks and queues both ways (array and linked list) and compare them.
- **Hashing** and **heaps** combine ideas from everything before, so they come last.

---

## Table of Contents

| # | Chapter | Syllabus module | Lab programs |
|---|---|---|---|
| 1 | [What Are Data Structures?](#chapter-1--what-are-data-structures) | I | – |
| 2 | [The C Toolkit: Structures, Pointers & Dynamic Memory](#chapter-2--the-c-toolkit-structures-pointers--dynamic-memory) | I | – |
| 3 | [Algorithms & Complexity](#chapter-3--algorithms--complexity) | I | – |
| 4 | [Arrays](#chapter-4--arrays) | I | 8, 9, 10 |
| 5 | [Strings](#chapter-5--strings) | I | – |
| 6 | [Sparse Matrices](#chapter-6--sparse-matrices) | I | – |
| 7 | [Searching](#chapter-7--searching) | V | 1, 2 |
| 8 | [Simple Sorting: Bubble, Selection, Insertion & Shell](#chapter-8--simple-sorting-bubble-selection-insertion--shell) | V | 3, 4, 5 |
| 9 | [Recursion & Tower of Hanoi](#chapter-9--recursion--tower-of-hanoi) | II | – |
| 10 | [Divide & Conquer Sorting: Merge Sort & Quick Sort](#chapter-10--divide--conquer-sorting-merge-sort--quick-sort) | V | 6, 7 |
| 11 | [Linked Lists](#chapter-11--linked-lists) | III | 14, 17, 18, 19 |
| 12 | [Stacks](#chapter-12--stacks) | II + III | 11, 15 |
| 13 | [Queues](#chapter-13--queues) | II + III | 12, 13, 16 |
| 14 | [Hashing](#chapter-14--hashing) | V | – |
| 15 | [Heaps & Heap Sort](#chapter-15--heaps--heap-sort) | V | 23 |
| 16 | [Sorting Wrap-up: Keys, External Sorting & Choosing a Sort](#chapter-16--sorting-wrap-up-keys-external-sorting--choosing-a-sort) | V | – |
| A | [Rapid-Fire Viva Q&A](#a-rapid-fire-viva-qa) | All | – |
| B | [Last-Night Cheat Sheet](#b-last-night-cheat-sheet) | All | – |

---

# Chapter 1 — What Are Data Structures?

> **Syllabus:** Module I · **Builds on:** nothing, start here · **Why first:** you need the basic vocabulary (data structure, linear, non-linear, ADT) before anything else.

## 1.1 What is a Data Structure?

- **Data** = raw facts (e.g., 25, "Rahul", 9.8).
- **Information** = processed/meaningful data.
- **Data Structure** = a particular way of **storing and organizing data in memory** so that it can be **used efficiently** (accessed, inserted, deleted, searched, sorted).

> **Viva one-liner:** "A data structure is a way of organizing data in memory so that operations on it can be performed efficiently."

**Why do we need data structures?**
- To handle large amounts of data efficiently.
- To make searching and sorting faster.
- To use memory properly.
- Choosing the right data structure makes an algorithm faster. Example: searching in a sorted array takes `O(log n)` with binary search vs `O(n)` with linear search.

**Data Structure + Algorithm = Program** (Niklaus Wirth's famous statement)

## 1.2 Types / Classification of Data Structures

```
                     Data Structures
                    /               \
             Primitive           Non-Primitive
         (int, float, char,      /           \
          double, pointer)    Linear        Non-Linear
                              |               |
                   Array, Stack, Queue,    Tree, Graph
                   Linked List
```

| Classification | Meaning | Examples |
|---|---|---|
| **Primitive** | Basic types built into the language, operated on directly by machine instructions | `int`, `char`, `float`, `double`, pointer |
| **Non-Primitive** | Built using primitive types | Array, List, Stack, Queue, Tree, Graph |
| **Linear** | Elements arranged in a sequence; each element has one predecessor and one successor | Array, Stack, Queue, Linked List |
| **Non-Linear** | Elements arranged in a hierarchy or network; one element can connect to many | Tree, Graph |
| **Static** | Size fixed at compile time | Array |
| **Dynamic** | Size can grow/shrink at run time | Linked List |
| **Homogeneous** | All elements of the same type | Array |
| **Heterogeneous** | Elements of different types | Structure (`struct`) |

### Operations on Data Structures

1. **Traversing** – visiting each element exactly once.
2. **Searching** – finding the location of an element.
3. **Insertion** – adding a new element.
4. **Deletion** – removing an element.
5. **Sorting** – arranging elements in order.
6. **Merging** – combining two lists into one.

### Abstract Data Type (ADT)

An **ADT** describes **what** operations a data type supports, **not how** they are implemented.
Example: *Stack ADT* = a collection with operations `push`, `pop`, `peek`, `isEmpty`. It can be implemented using an array **or** a linked list. The user doesn't care which.

> **Viva:** "ADT is the logical view (what), data structure is the physical implementation (how)."

> ### Check Yourself — Chapter 1
> 1. **What is a data structure?** A way of organizing data in memory so it can be used efficiently.
> 2. **Primitive vs non-primitive?** Built-in basic types (int, char, float, pointer) vs types built from them (array, list, stack, tree).
> 3. **Linear vs non-linear?** Linear = elements in a sequence (array, stack, queue, list). Non-linear = hierarchy or network (tree, graph).
> 4. **Static vs dynamic?** Size fixed at compile time (array) vs size changes at run time (linked list).
> 5. **Name the basic operations on a data structure.** Traversing, searching, insertion, deletion, sorting, merging.
> 6. **What is an ADT?** A specification of *what* operations a type supports, without saying *how* they are implemented. Example: the Stack ADT.

---

# Chapter 2 — The C Toolkit: Structures, Pointers & Dynamic Memory

> **Syllabus:** Module I ("use of pointers in data structures") · **Builds on:** Chapter 1 · **Why now:** in C, every data structure is built from structures and pointers. Linked lists are impossible without them.

## 2.1 Structures in C

A **structure (`struct`)** groups variables of **different types** under one name. It is C's way of building a **heterogeneous** data type.

```c
struct student {
    int roll;
    char name[20];
    float marks;
};

struct student s1 = {1, "Asha", 88.5};
printf("%d %s %.1f", s1.roll, s1.name, s1.marks);   // dot (.) accesses members
s1.marks = 91.0;
```

- **`typedef`** gives a shorter name: `typedef struct student Student;` → `Student s2;`
- **Array of structures:** `struct student cls[60];` → `cls[i].roll`
- **Self-referential structure:** a struct can't contain *itself*, but it can contain a **pointer to its own type**. This is the building block of linked lists (Chapter 11):
  ```c
  struct node {
      int data;
      struct node *next;    // pointer to another node of the same type
  };
  ```
- `sizeof(struct)` can be **more** than the sum of its members because of **padding** (alignment).

**Structure vs Union:** In a structure, every member has its own memory, so the size is about the sum of the members. In a **union**, all members **share the same memory**, so the size equals the largest member and only one member can be used at a time.

## 2.2 Pointers

A **pointer** is a variable that stores the **memory address** of another variable.

```c
int x = 10;
int *p;      // p is a pointer to int
p = &x;      // & = "address of" operator
printf("%d", *p);   // * = "value at address" (dereference) → prints 10
*p = 20;            // changes x to 20
```

| Term | Meaning |
|---|---|
| `&x` | Address of x |
| `*p` | Value stored at the address held in p |
| **NULL pointer** | A pointer that points to nothing (`p = NULL;`). Used to mark the end of a linked list. |
| **Dangling pointer** | A pointer that points to memory that has already been freed |
| **Void pointer** (`void *`) | A generic pointer that can hold the address of any type (`malloc` returns `void *`) |
| **Wild pointer** | An uninitialized pointer (contains a garbage address) |
| **Memory leak** | Memory allocated with `malloc` but never freed and no longer reachable |

**Pointer arithmetic:** if `p` points to `a[0]`, then `p + 1` points to `a[1]`. `p + 1` moves by `sizeof(int)` bytes, not by 1 byte. Also, `a[i]` is the same as `*(a + i)`.

**Pointer to structure:**
```c
struct student { int roll; char name[20]; };
struct student s, *ptr = &s;
ptr->roll = 5;      // same as (*ptr).roll = 5;
```

## 2.3 Dynamic Memory Allocation (in `<stdlib.h>`)

| Function | Purpose | Example |
|---|---|---|
| `malloc(size)` | Allocates one block of `size` bytes; contents are **garbage** | `p = (int*) malloc(n * sizeof(int));` |
| `calloc(n, size)` | Allocates `n` blocks, each of `size` bytes, **initialized to 0** | `p = (int*) calloc(n, sizeof(int));` |
| `realloc(p, newsize)` | Changes the size of previously allocated memory | `p = realloc(p, 2*n*sizeof(int));` |
| `free(p)` | Releases the memory | `free(p);` |

`malloc` and `calloc` return `NULL` if memory is not available.

**Why pointers are important in data structures:**
1. **Dynamic memory allocation:** create nodes at run time (linked lists).
2. **Linking elements:** each node of a linked list stores a pointer to the next node.
3. **Passing arrays/large structures to functions** efficiently (pass the address, not a copy).
4. **Building non-linear structures** like trees and graphs.

> ### Check Yourself — Chapter 2
> 1. **What is a structure?** A user-defined type that groups variables of different types under one name.
> 2. **What is a self-referential structure?** A structure containing a pointer to its own type, e.g., `struct node *next`.
> 3. **What is a pointer?** A variable that stores the address of another variable.
> 4. **What do `&` and `*` do?** `&x` gives the address of x. `*p` gives the value at the address in p.
> 5. **What is the `->` operator?** It accesses a structure member through a pointer: `p->roll` is the same as `(*p).roll`.
> 6. **NULL, dangling, void and wild pointers?** Points to nothing / points to freed memory / generic pointer to any type / uninitialized pointer.
> 7. **malloc vs calloc?** malloc(size) gives one block with garbage values. calloc(n, size) gives n blocks initialized to 0.
> 8. **What does malloc return when memory isn't available?** NULL.
> 9. **What is a memory leak?** Memory that was allocated but never freed and is no longer reachable.
> 10. **Why are pointers important in data structures?** Dynamic allocation, linking nodes, and passing large data efficiently.

---

# Chapter 3 — Algorithms & Complexity

> **Syllabus:** Module I · **Builds on:** Chapter 1 · **Why now:** from here on, every data structure and algorithm is judged by how much time and memory it needs.

## 3.1 Algorithm

An **algorithm** is a finite, step-by-step set of well-defined instructions to solve a problem.

**Characteristics of an algorithm** (remember **"IODEF"**):
| Property | Meaning |
|---|---|
| **I**nput | Zero or more inputs |
| **O**utput | At least one output |
| **D**efiniteness | Every step is clear and unambiguous |
| **E**ffectiveness | Every step is basic enough to be carried out (by pen and paper) |
| **F**initeness | Must terminate after a finite number of steps |

**Algorithm vs Program:** An algorithm is language-independent (written in English/pseudocode) and must terminate. A program is written in a programming language and may run forever (e.g., an OS).

### Algorithm Design Approaches

| Approach | Idea | Example |
|---|---|---|
| **Divide and Conquer** | Break the problem into sub-problems, solve each, combine | Merge Sort, Quick Sort, Binary Search |
| **Greedy** | Pick the best choice at each step | Coin change, Prim's/Kruskal's |
| **Dynamic Programming** | Solve overlapping sub-problems once and store their results | Fibonacci with memoization |
| **Backtracking** | Try options, undo when stuck | N-Queens, Sudoku |
| **Brute Force** | Try all possibilities | Linear search |

**Top-down design:** break a big problem into smaller modules (functions). **Bottom-up design:** build small modules first, then combine them.

## 3.2 Complexity of Algorithms

**Complexity** measures how much **time** and **memory** an algorithm needs as a function of input size `n`.

- **Time Complexity** – the number of basic operations (steps) executed, expressed as a function of `n`. It does **not** mean seconds, because seconds depend on the machine.
- **Space Complexity** – the amount of memory needed = fixed part (code, constants, simple variables) + variable part (dynamic memory, recursion stack).

### Best, Average, Worst Case

Example: Linear search in an array of `n` elements:
- **Best case:** element found at first position → 1 comparison → `O(1)`
- **Worst case:** element at last position or not present → `n` comparisons → `O(n)`
- **Average case:** about `n/2` comparisons → `O(n)`

### Asymptotic Notations (how running time grows for large `n`)

| Notation | Name | Meaning | Bound |
|---|---|---|---|
| **O (Big-Oh)** | Upper bound | `f(n) = O(g(n))` if there exist constants `c > 0`, `n0` such that `f(n) ≤ c·g(n)` for all `n ≥ n0` | **Worst case** |
| **Ω (Omega)** | Lower bound | `f(n) ≥ c·g(n)` for all `n ≥ n0` | **Best case** |
| **Θ (Theta)** | Tight bound | `c1·g(n) ≤ f(n) ≤ c2·g(n)` for all `n ≥ n0` | **Exact growth** (both upper and lower) |

**Example:** `f(n) = 3n + 2`. Then `3n + 2 ≤ 4n` for all `n ≥ 2`, so `f(n) = O(n)` with `c = 4`, `n0 = 2`.

**Rules for finding Big-O:**
1. Drop constants: `O(5n)` → `O(n)`
2. Keep only the highest-order term: `O(n² + 3n + 7)` → `O(n²)`

**Common growth rates (slowest → fastest growing):**
```
O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(n³) < O(2ⁿ) < O(n!)
constant  log    linear  linearithmic quadratic cubic exponential factorial
```

**Finding complexity from code:**
```c
x = x + 1;                       // O(1)

for (i = 0; i < n; i++)          // O(n)
    sum += a[i];

for (i = 0; i < n; i++)          // O(n²) – nested loops
    for (j = 0; j < n; j++)
        c++;

for (i = 1; i < n; i = i * 2)    // O(log n) – i doubles each time
    c++;
```

## 3.3 Time–Space Trade-off

Often we can **save time by using more memory** or **save memory by spending more time**. We cannot always minimize both.

**Examples:**
- **Hashing** uses extra memory (the hash table) to get `O(1)` search time.
- **Merge sort** uses `O(n)` extra space; heap sort uses `O(1)` extra space but is usually slower in practice.
- **Lookup tables / memoization:** store precomputed results (more space) to avoid recomputation (less time).
- **Compressed files** save space but need time to decompress.

> **Viva:** "Time-space trade-off means reducing time by using more space or vice versa. Example: hashing gives O(1) search but uses extra memory."

> ### Check Yourself — Chapter 3
> 1. **What is an algorithm? Give its properties.** A finite sequence of clear steps. Input, Output, Definiteness, Finiteness, Effectiveness.
> 2. **Algorithm vs program?** An algorithm is language-independent and must terminate. A program is written in a language and may run forever.
> 3. **What is time complexity?** The number of basic steps as a function of input size n. It is not measured in seconds.
> 4. **What is space complexity?** The memory needed: a fixed part plus a variable part (dynamic memory, recursion stack).
> 5. **Big-O vs Omega vs Theta?** Upper bound (worst case) / lower bound (best case) / tight bound.
> 6. **Arrange in order of growth:** O(1) < O(log n) < O(n) < O(n log n) < O(n²) < O(2ⁿ) < O(n!).
> 7. **Complexity of a loop where i doubles each time?** O(log n).
> 8. **What is time-space trade-off?** Using more memory to save time, or the reverse. Example: hashing.

---

# Chapter 4 — Arrays

> **Syllabus:** Module I · **Builds on:** Chapters 2 and 3 · **Why now:** the array is the simplest data structure, and strings, searching, sorting, stacks, queues and hashing all use it.

## 4.1 What is an Array?

An **array** is a **finite, ordered collection of homogeneous (same type) elements** stored in **contiguous (consecutive) memory locations**, accessed by an **index**.

```c
int a[5] = {10, 20, 30, 40, 50};
//  index:   0   1   2   3   4
```

**Properties:**
- Fixed size (static), decided at compile time.
- Same data type for all elements.
- Contiguous memory.
- Random access in `O(1)` time using the index.
- In C the index starts at 0. The array name is a constant pointer to the first element (`a == &a[0]`).

**Terms:** `LB` = lower bound (smallest index), `UB` = upper bound (largest index).
**Length (number of elements)** = `UB − LB + 1`

**Advantages:** fast random access, simple, cache-friendly.
**Disadvantages:** fixed size (wastes memory or runs out), insertion and deletion are costly (`O(n)`) because elements must be shifted.

## 4.2 Representation of Linear (1-D) Arrays in Memory

The computer stores only the **base address** (address of the first element). Every other address is calculated:

> **LOC(A[k]) = Base(A) + w × (k − LB)**
> where `w` = size of each element in bytes.

**Example:** `int A[10]`, Base = 1000, w = 4 bytes, LB = 0. Address of `A[6]` = 1000 + 4 × (6 − 0) = **1024**.

Because this is a single formula, **any element is accessed in O(1) time (random access).**

## 4.3 Traversing a Linear Array

Visiting each element once (e.g., to print it or add it to a sum).
```
Algorithm TRAVERSE(A, LB, UB)
1. Set K = LB
2. Repeat while K <= UB:
       Process A[K]
       K = K + 1
3. Exit
```
```c
for (i = 0; i < n; i++)
    printf("%d ", a[i]);
```
Complexity: `O(n)`.

## 4.4 Insertion in an Array (Lab Program 8: insert at k-th position)

To insert at position `k`, **shift elements from the end towards the right** to make space, then insert.

```c
#include <stdio.h>
int main() {
    int a[100], n, i, pos, item;
    printf("Enter number of elements: ");
    scanf("%d", &n);
    printf("Enter elements: ");
    for (i = 0; i < n; i++) scanf("%d", &a[i]);

    printf("Enter element and position (1 to %d): ", n + 1);
    scanf("%d %d", &item, &pos);

    if (pos < 1 || pos > n + 1) { printf("Invalid position\n"); return 0; }

    for (i = n - 1; i >= pos - 1; i--)   // shift right, starting from the last element
        a[i + 1] = a[i];
    a[pos - 1] = item;                   // position is 1-based, index is 0-based
    n++;

    printf("Array after insertion: ");
    for (i = 0; i < n; i++) printf("%d ", a[i]);
    return 0;
}
```
**Why shift from the end?** If we shifted from the front, each element would overwrite the next one before it was moved.
Complexity: worst case `O(n)` (insert at the beginning), best case `O(1)` (insert at the end).

## 4.5 Deletion from an Array (Lab Program 9: delete from a sorted array)

Find the element, then **shift all following elements one position left**.

```c
#include <stdio.h>
int main() {
    int a[100], n, i, item, pos = -1;
    printf("Enter number of elements: ");
    scanf("%d", &n);
    printf("Enter sorted elements: ");
    for (i = 0; i < n; i++) scanf("%d", &a[i]);

    printf("Enter element to delete: ");
    scanf("%d", &item);

    /* array is sorted, so use binary search to find it (explained in Chapter 7) */
    int low = 0, high = n - 1, mid;
    while (low <= high) {
        mid = (low + high) / 2;
        if (a[mid] == item) { pos = mid; break; }
        else if (a[mid] < item) low = mid + 1;
        else high = mid - 1;
    }

    if (pos == -1) { printf("Element not found\n"); return 0; }

    for (i = pos; i < n - 1; i++)    // shift left
        a[i] = a[i + 1];
    n--;

    printf("Array after deletion: ");
    for (i = 0; i < n; i++) printf("%d ", a[i]);
    return 0;
}
```
Complexity: `O(n)` for shifting (the search is `O(log n)`).

## 4.6 Merging Two Sorted Arrays (Lab Program 10)

Compare the front elements of both arrays and copy the smaller one. When one array runs out, copy the rest of the other.

```c
#include <stdio.h>
int main() {
    int a[50], b[50], c[100], m, n, i, j, k;
    printf("Size of first sorted array: ");  scanf("%d", &m);
    for (i = 0; i < m; i++) scanf("%d", &a[i]);
    printf("Size of second sorted array: "); scanf("%d", &n);
    for (j = 0; j < n; j++) scanf("%d", &b[j]);

    i = j = k = 0;
    while (i < m && j < n) {
        if (a[i] <= b[j]) c[k++] = a[i++];
        else              c[k++] = b[j++];
    }
    while (i < m) c[k++] = a[i++];   // leftover from a
    while (j < n) c[k++] = b[j++];   // leftover from b

    printf("Merged array: ");
    for (k = 0; k < m + n; k++) printf("%d ", c[k]);
    return 0;
}
```
Complexity: `O(m + n)`.

## 4.7 Two-Dimensional Arrays

A 2-D array is an array of arrays, i.e., a **matrix** with rows and columns.
```c
int a[3][4];    // 3 rows, 4 columns = 12 elements
```
Memory is linear (1-D), so a 2-D array must be "flattened" in one of two ways:

**Row-Major Order** (used by **C**): store row 0 completely, then row 1, and so on.
**Column-Major Order** (used by **FORTRAN, MATLAB**): store column 0 completely, then column 1, and so on.

For an array `A[M][N]` (M rows, N columns), with lower bounds `LB1` (rows) and `LB2` (columns):

> **Row-major:**    LOC(A[i][j]) = Base + w × [ N × (i − LB1) + (j − LB2) ]
> **Column-major:** LOC(A[i][j]) = Base + w × [ M × (j − LB2) + (i − LB1) ]

**Example:** `int A[3][4]`, Base = 1000, w = 4, LB = 0. Find `A[1][2]`.
- Row-major: 1000 + 4 × (4×1 + 2) = 1000 + 24 = **1024**
- Column-major: 1000 + 4 × (3×2 + 1) = 1000 + 28 = **1028**

> **Memory trick:** Row-major → multiply the **row index** by the **number of columns**. Column-major → multiply the **column index** by the **number of rows**.

## 4.8 Multidimensional Arrays

An array with more than two dimensions, e.g., `int a[2][3][4];` (2 blocks × 3 rows × 4 columns = 24 elements).
Row-major address (0-based) for `A[d1][d2][d3]`:
> LOC(A[i][j][k]) = Base + w × [ (i × d2 + j) × d3 + k ]

Total elements = product of all dimensions.

## 4.9 Arrays as Function Parameters

- When you pass an array to a function, **only the base address is passed** (not a copy of the whole array).
- So any change made inside the function **changes the original array** (it acts like call by reference).
- `void f(int a[], int n)` is exactly the same as `void f(int *a, int n)`.
- The size must be passed separately, because inside the function `sizeof(a)` gives the size of a pointer, not of the array.
- For 2-D arrays, the **column size must be specified**: `void f(int a[][4], int rows)`. The compiler needs the column count to calculate row-major addresses.

```c
void display(int a[], int n) {
    for (int i = 0; i < n; i++) printf("%d ", a[i]);
}
void doubleAll(int *a, int n) {
    for (int i = 0; i < n; i++) a[i] *= 2;   // changes the original array
}
```

## 4.10 Implementing a 1-D Array / Functions Associated with Arrays

Static array: `int a[100];` (the size must be a constant).
Dynamic 1-D array (size decided at run time):
```c
int *a, n;
scanf("%d", &n);
a = (int *) malloc(n * sizeof(int));
if (a == NULL) { printf("Memory not available"); exit(1); }
for (int i = 0; i < n; i++) scanf("%d", &a[i]);
/* ... use a[i] like a normal array ... */
free(a);
```
Common array functions: `read()`, `display()`, `insert()`, `delete()`, `search()`, `sort()`, `merge()`, `reverse()`, `findMax()`.

> ### Check Yourself — Chapter 4
> 1. **What is an array?** A fixed-size collection of same-type elements in contiguous memory, accessed by index.
> 2. **Why does indexing start at 0 in C?** The index is the offset from the base address: `a[i] = *(a + i)`.
> 3. **Address formula for a 1-D array?** `Base + w(k − LB)`.
> 4. **Row-major vs column-major?** Stored row by row (C) vs column by column (FORTRAN).
> 5. **Why is insertion or deletion in an array costly?** Elements must be shifted: O(n).
> 6. **Why do we shift from the end when inserting?** So no element is overwritten before it has been moved.
> 7. **What is passed when you pass an array to a function?** Only the base address, so changes inside the function affect the original array.
> 8. **Why must the column size be given for a 2-D array parameter?** The compiler needs it to calculate row-major addresses.
> 9. **Complexity of merging two sorted arrays?** O(m + n).

---

# Chapter 5 — Strings

> **Syllabus:** Module I · **Builds on:** Chapter 4 · **Why now:** in C, a string is just a character array.

## 5.1 Character Strings in C

A **string** in C is a **character array terminated by the null character `'\0'`**.
```c
char s[] = "HELLO";    // occupies 6 bytes: H E L L O \0
char s2[10] = {'H','I','\0'};
```
- `'\0'` marks the end of the string (ASCII value 0).
- `"A"` is a string (2 bytes: `'A'` and `'\0'`); `'A'` is a single character (1 byte).

**Input/Output:**
- `scanf("%s", s);` stops reading at a space.
- `gets(s);` reads spaces too but is **unsafe** (no bounds check; removed from the C11 standard).
- `fgets(s, sizeof(s), stdin);` is the safe way to read a line with spaces.
- `puts(s);` / `printf("%s", s);` print a string.

## 5.2 String Operations (`<string.h>`)

| Function | Work | Example / Result |
|---|---|---|
| `strlen(s)` | Length (without `'\0'`) | `strlen("HELLO")` → 5 |
| `strcpy(d, s)` | Copy s into d | d = "HELLO" |
| `strncpy(d, s, n)` | Copy first n chars | |
| `strcat(d, s)` | Append s to the end of d | "Hi" + "There" → "HiThere" |
| `strcmp(s1, s2)` | Compare | returns **0** if equal, **< 0** if s1 < s2, **> 0** if s1 > s2 |
| `strrev(s)` | Reverse (non-standard, works in Turbo C) | "abc" → "cba" |
| `strupr(s)` / `strlwr(s)` | Upper/lower case (non-standard) | |
| `strchr(s, c)` | Pointer to first occurrence of character c | |
| `strstr(s1, s2)` | Pointer to first occurrence of substring s2 in s1 | |

**Writing them yourself (common viva question):**
```c
int myStrlen(char s[]) {
    int i = 0;
    while (s[i] != '\0') i++;
    return i;
}

void myStrrev(char s[]) {
    int i = 0, j = myStrlen(s) - 1;
    char t;
    while (i < j) { t = s[i]; s[i] = s[j]; s[j] = t; i++; j--; }
}

int isPalindrome(char s[]) {
    int i = 0, j = myStrlen(s) - 1;
    while (i < j)
        if (s[i++] != s[j--]) return 0;
    return 1;
}
```

> ### Check Yourself — Chapter 5
> 1. **How is a string stored in C?** As a char array ending with `'\0'`.
> 2. **What is `'\0'`?** The null character (ASCII 0). It marks the end of a string.
> 3. **`"A"` vs `'A'`?** A string of 2 bytes (`'A'` and `'\0'`) vs a single character of 1 byte.
> 4. **What does strcmp return?** 0 if equal, negative if the first is smaller, positive if the first is larger.
> 5. **strlen vs sizeof?** strlen counts characters before `'\0'`. sizeof gives the total bytes of the array.
> 6. **Why is gets() unsafe?** It has no size limit, so it can overflow the buffer. Use fgets().

---

# Chapter 6 — Sparse Matrices

> **Syllabus:** Module I · **Builds on:** Chapter 4 (2-D arrays) · **Why now:** your first example of choosing a smarter representation to save memory.

## 6.1 What is a Sparse Matrix?

A **sparse matrix** is a matrix in which **most elements are zero**. (A rough rule: more than half the elements are 0.)
A matrix with mostly non-zero elements is called a **dense matrix**.

**Problem:** Storing all the zeros wastes memory and processing time.
**Solution:** Store **only the non-zero elements**.

**Sparsity** = (number of zero elements) / (total elements)

## 6.2 Representation 1: Triplet (3-tuple / Array) Representation

Each non-zero element is stored as a row of **(row, column, value)**. The first row (header) stores **(total rows, total columns, number of non-zero elements)**.

Example 4×5 matrix (the first row of the triplet table is the header: rows, cols, non-zero count):
```
0 0 3 0 4
0 0 5 7 0
0 0 0 0 0
0 2 6 0 0
```
| Row | Col | Value |
|---|---|---|
| **4** | **5** | **6** |
| 0 | 2 | 3 |
| 0 | 4 | 4 |
| 1 | 2 | 5 |
| 1 | 3 | 7 |
| 3 | 1 | 2 |
| 3 | 2 | 6 |

Memory: normal storage = 4×5 = 20 values; triplet = 7×3 = 21 values here. The saving becomes large for big matrices (e.g., a 1000×1000 matrix with 50 non-zeros: 1,000,000 vs 153 values).

```c
/* Convert a matrix to triplet form */
int sp[50][3], k = 1;
for (i = 0; i < r; i++)
    for (j = 0; j < c; j++)
        if (a[i][j] != 0) {
            sp[k][0] = i; sp[k][1] = j; sp[k][2] = a[i][j];
            k++;
        }
sp[0][0] = r; sp[0][1] = c; sp[0][2] = k - 1;   // header row
```

## 6.3 Representation 2: Linked List Representation

Each non-zero element is a node: `| row | col | value | next |` (linked lists are explained in Chapter 11). This is useful when the number of non-zero elements keeps changing.

**Special sparse matrices:** lower triangular, upper triangular, diagonal, and tridiagonal matrices.

**Applications:** image processing, graph adjacency matrices of sparse graphs, scientific computing, recommender systems.

> ### Check Yourself — Chapter 6
> 1. **What is a sparse matrix?** A matrix in which most elements are zero.
> 2. **Why not store it normally?** The zeros waste memory and processing time.
> 3. **What is triplet representation?** Each non-zero element is stored as (row, column, value). The first row stores (rows, columns, count of non-zeros).
> 4. **Other representation?** A linked list with nodes (row, col, value, next).
> 5. **Applications?** Image processing, scientific computing, adjacency matrices of sparse graphs.

---

# Chapter 7 — Searching

> **Syllabus:** Module V · **Builds on:** Chapters 3 and 4 · **Why now:** the first real algorithms on arrays, and the first time you see O(n) vs O(log n) in practice.

## 7.1 What is Searching?

**Searching** = finding the location of a given element (the **key**) in a collection. It is **successful** if the key is found, **unsuccessful** otherwise.

## 7.2 Linear (Sequential) Search (Lab Program 1)

Compare the key with **each element one by one** from the start until it is found or the list ends.
- Works on **unsorted and sorted** data.
- Works on arrays **and** linked lists.

```
Algorithm LINEAR_SEARCH(A, N, KEY)
1. Repeat for i = 0 to N−1:
       If A[i] = KEY then return i
2. Return −1  (not found)
```
```c
#include <stdio.h>
int main() {
    int a[100], n, key, i, found = 0;
    printf("Enter n: "); scanf("%d", &n);
    printf("Enter elements: ");
    for (i = 0; i < n; i++) scanf("%d", &a[i]);
    printf("Enter element to search: "); scanf("%d", &key);

    for (i = 0; i < n; i++) {
        if (a[i] == key) {
            printf("%d found at position %d (index %d)\n", key, i + 1, i);
            found = 1;
            break;
        }
    }
    if (!found) printf("%d not found\n", key);
    return 0;
}
```
**Complexity:** Best O(1) (first element), Average O(n), Worst O(n). Space O(1).

## 7.3 Binary Search (Lab Program 2)

**Precondition: the array must be SORTED.**
**Idea (divide and conquer):** Compare the key with the **middle** element:
- If they are equal → found.
- If key < middle → search the **left half**.
- If key > middle → search the **right half**.

Each step **halves** the search space.

```
Algorithm BINARY_SEARCH(A, N, KEY)
1. low = 0, high = N − 1
2. While low <= high:
       mid = (low + high) / 2
       If A[mid] = KEY → return mid
       Else if KEY < A[mid] → high = mid − 1
       Else → low = mid + 1
3. Return −1
```
```c
#include <stdio.h>
int main() {
    int a[100], n, key, low, high, mid, i;
    printf("Enter n: "); scanf("%d", &n);
    printf("Enter elements in sorted order: ");
    for (i = 0; i < n; i++) scanf("%d", &a[i]);
    printf("Enter element to search: "); scanf("%d", &key);

    low = 0; high = n - 1;
    while (low <= high) {
        mid = low + (high - low) / 2;    // avoids integer overflow of (low + high)
        if (a[mid] == key) {
            printf("%d found at position %d\n", key, mid + 1);
            return 0;
        }
        else if (key < a[mid]) high = mid - 1;
        else low = mid + 1;
    }
    printf("%d not found\n", key);
    return 0;
}
```
**Recursive version** (come back to this after Chapter 9, Recursion):
```c
int binSearch(int a[], int low, int high, int key) {
    if (low > high) return -1;
    int mid = (low + high) / 2;
    if (a[mid] == key) return mid;
    if (key < a[mid]) return binSearch(a, low, mid - 1, key);
    return binSearch(a, mid + 1, high, key);
}
```
**Example:** `A = [10, 20, 30, 40, 50, 60, 70]`, key = 60
- low = 0, high = 6, mid = 3 → A[3] = 40 < 60 → low = 4
- low = 4, high = 6, mid = 5 → A[5] = 60 → **found at index 5** (2 comparisons)

**Complexity:** Best O(1), Average/Worst **O(log₂ n)**. For n = 1,000,000 it needs only about 20 comparisons!

## 7.4 Linear vs Binary Search

| Linear Search | Binary Search |
|---|---|
| Works on unsorted data | Needs **sorted** data |
| O(n) | O(log n) |
| Sequential access is enough (works on linked lists) | Needs random access (arrays) |
| Simple | A bit more complex |
| Good for small or unsorted data | Good for large sorted data |

> ### Check Yourself — Chapter 7
> 1. **Linear vs binary search?** O(n) on any data vs O(log n) on sorted data only.
> 2. **Precondition for binary search?** The data must be sorted and allow random access (an array).
> 3. **Why `mid = low + (high − low)/2`?** It avoids integer overflow of `low + high`.
> 4. **Best case of each?** O(1): the key is the first element (linear) or the middle element (binary).
> 5. **Can binary search be used on a linked list?** Not efficiently, because reaching the middle takes O(n).
> 6. **Maximum comparisons in binary search for n = 1024?** 11 (⌊log₂ n⌋ + 1).

---

# Chapter 8 — Simple Sorting: Bubble, Selection, Insertion & Shell

> **Syllabus:** Module V · **Builds on:** Chapters 4 and 7 · **Why now:** binary search needs sorted data. These sorts use only loops and swaps, with no recursion needed.

## 8.1 Sorting – Basics

**Sorting** = arranging data in a particular order (ascending or descending).

| Term | Meaning |
|---|---|
| **Internal sorting** | All data fits in **main memory (RAM)** while sorting (bubble, quick, merge, heap...) |
| **External sorting** | Data is too large for RAM and is kept on **disk**; sorted in parts (external merge sort) |
| **Stable sort** | **Equal keys keep their original relative order.** (Bubble, Insertion, Merge are stable.) |
| **In-place sort** | Needs only O(1) extra memory (Bubble, Selection, Insertion, Heap, Quick*) |
| **Comparison sort** | Sorts by comparing elements. The lower bound for comparison sorts is Ω(n log n). |
| **Pass** | One complete iteration over the (remaining) list |

**Stability example:** records (Amit, 70), (Ravi, 60), (Neha, 70) sorted by marks. A stable sort keeps Amit before Neha.

## 8.2 Bubble Sort (Lab Program 3)

**Idea:** Repeatedly compare **adjacent** elements and **swap** them if they are in the wrong order. After each pass, the **largest remaining element "bubbles up" to its correct position at the end**.

**Example:** `[5, 1, 4, 2, 8]`
- Pass 1: (5,1) swap → [1,5,4,2,8]; (5,4) swap → [1,4,5,2,8]; (5,2) swap → [1,4,2,5,8]; (5,8) no swap → **[1,4,2,5,8]** (8 is in place)
- Pass 2: [1,4,2,5,8] → (4,2) swap → **[1,2,4,5,8]**
- Pass 3: no swaps → stop (optimized version).

```c
#include <stdio.h>
int main() {
    int a[100], n, i, j, temp, swapped;
    printf("Enter n: "); scanf("%d", &n);
    for (i = 0; i < n; i++) scanf("%d", &a[i]);

    for (i = 0; i < n - 1; i++) {              // n−1 passes
        swapped = 0;
        for (j = 0; j < n - 1 - i; j++) {      // last i elements are already sorted
            if (a[j] > a[j + 1]) {
                temp = a[j]; a[j] = a[j + 1]; a[j + 1] = temp;
                swapped = 1;
            }
        }
        if (swapped == 0) break;               // no swap → array already sorted
    }

    printf("Sorted: ");
    for (i = 0; i < n; i++) printf("%d ", a[i]);
    return 0;
}
```
- **Passes:** at most n−1. **Comparisons (worst):** n(n−1)/2.
- **Best O(n)** (already sorted, with the `swapped` flag), **Average/Worst O(n²)**, Space O(1), **Stable: Yes**, In-place: Yes.

## 8.3 Selection Sort (Lab Program 4)

**Idea:** In each pass, **find the minimum element** in the unsorted part and **swap it with the first element of the unsorted part**.

**Example:** `[64, 25, 12, 22, 11]`
- Pass 1: min = 11 → swap with 64 → [**11**, 25, 12, 22, 64]
- Pass 2: min = 12 → swap with 25 → [11, **12**, 25, 22, 64]
- Pass 3: min = 22 → swap with 25 → [11, 12, **22**, 25, 64]
- Pass 4: min = 25 → already in place → [11, 12, 22, **25**, 64]

```c
#include <stdio.h>
int main() {
    int a[100], n, i, j, min, temp;
    printf("Enter n: "); scanf("%d", &n);
    for (i = 0; i < n; i++) scanf("%d", &a[i]);

    for (i = 0; i < n - 1; i++) {
        min = i;
        for (j = i + 1; j < n; j++)
            if (a[j] < a[min]) min = j;
        if (min != i) { temp = a[i]; a[i] = a[min]; a[min] = temp; }
    }

    printf("Sorted: ");
    for (i = 0; i < n; i++) printf("%d ", a[i]);
    return 0;
}
```
- **O(n²) in all cases** (it always scans the whole unsorted part), Space O(1), **Not stable**, In-place.
- **Plus point:** the **minimum number of swaps** (at most n−1). Good when writing to memory is costly.

## 8.4 Insertion Sort (Lab Program 5)

**Idea:** Like sorting playing cards in your hand. Take one element at a time and **insert it into its correct position in the already-sorted left part** by shifting larger elements to the right.

**Example:** `[12, 11, 13, 5, 6]`
- i=1: key = 11 → shift 12 → [11, 12, 13, 5, 6]
- i=2: key = 13 → no shift → [11, 12, 13, 5, 6]
- i=3: key = 5 → shift 13, 12, 11 → [5, 11, 12, 13, 6]
- i=4: key = 6 → shift 13, 12, 11 → [5, 6, 11, 12, 13]

```c
#include <stdio.h>
int main() {
    int a[100], n, i, j, key;
    printf("Enter n: "); scanf("%d", &n);
    for (i = 0; i < n; i++) scanf("%d", &a[i]);

    for (i = 1; i < n; i++) {
        key = a[i];
        j = i - 1;
        while (j >= 0 && a[j] > key) {   // shift larger elements right
            a[j + 1] = a[j];
            j--;
        }
        a[j + 1] = key;                  // insert at the correct place
    }

    printf("Sorted: ");
    for (i = 0; i < n; i++) printf("%d ", a[i]);
    return 0;
}
```
- **Best O(n)** (already sorted), **Average/Worst O(n²)** (reverse sorted), Space O(1), **Stable: Yes**, In-place.
- **Best for small or nearly-sorted data.** It is also **online** (it can sort data as it arrives).

## 8.5 Shell Sort

**Developed by Donald Shell (1959).** It is an **improved insertion sort**.
**Problem with insertion sort:** an element moves only one position at a time, which is slow if it is far from its correct place.
**Idea:** First sort elements that are **far apart (gap)**, then reduce the gap step by step. When gap = 1 it becomes a normal insertion sort, but by then the array is **nearly sorted**, so it is fast.

**Common gap sequence:** n/2, n/4, ..., 1

**Example:** `[35, 33, 42, 10, 14, 19, 27, 44]`, n = 8
- gap = 4: compare (35,14), (33,19), (42,27), (10,44) → swap where needed → `[14, 19, 27, 10, 35, 33, 42, 44]`
- gap = 2: insertion sort on elements 2 apart → `[14, 10, 27, 19, 35, 33, 42, 44]`
- gap = 1: normal insertion sort → `[10, 14, 19, 27, 33, 35, 42, 44]`

```c
void shellSort(int a[], int n) {
    for (int gap = n / 2; gap > 0; gap /= 2) {
        for (int i = gap; i < n; i++) {        // gapped insertion sort
            int temp = a[i], j;
            for (j = i; j >= gap && a[j - gap] > temp; j -= gap)
                a[j] = a[j - gap];
            a[j] = temp;
        }
    }
}
```
- Complexity depends on the gap sequence. Worst case with n/2 gaps is **O(n²)**; with better sequences it is about **O(n^1.5)** or **O(n log² n)**. Best case O(n log n).
- Space O(1). **Not stable.** In-place.
- Also called the **diminishing increment sort**.

> ### Check Yourself — Chapter 8
> 1. **What is a stable sort? Examples?** Equal keys keep their original order. Bubble, insertion and merge sort.
> 2. **What is an in-place sort?** It needs only O(1) extra memory.
> 3. **Internal vs external sorting?** Data fits in RAM vs data stays on disk.
> 4. **Best case of bubble sort?** O(n), using the "swapped" flag on already-sorted data.
> 5. **Which sort makes the fewest swaps?** Selection sort (at most n − 1).
> 6. **Which sort is best for nearly sorted data?** Insertion sort.
> 7. **Number of comparisons in selection sort?** Always n(n − 1)/2.
> 8. **What is shell sort?** Insertion sort on elements a gap apart, with the gap shrinking to 1 (diminishing increment sort).

---

# Chapter 9 — Recursion & Tower of Hanoi

> **Syllabus:** Module II ("application of stacks: recursion", Tower of Hanoi) · **Builds on:** Chapters 2 and 3 · **Why now:** merge sort and quick sort (next chapter) are recursive, so you must understand recursion first.

## 9.1 Recursion

**Recursion** is when a **function calls itself**, directly or indirectly, to solve a smaller instance of the same problem.

Every recursive function has two parts:
1. **Base case** – the condition where the function stops calling itself. **Without it you get infinite recursion and a stack overflow.**
2. **Recursive case** – the function calls itself with a smaller input.

```c
int fact(int n) {
    if (n == 0 || n == 1) return 1;   // base case
    return n * fact(n - 1);           // recursive case
}

int fib(int n) {
    if (n <= 1) return n;             // fib(0)=0, fib(1)=1
    return fib(n - 1) + fib(n - 2);
}
```

**How the computer runs recursion:** it uses a *stack*, which works like a pile of plates: the last plate put on is the first one taken off (Chapter 12 explains stacks fully). Each function call pushes an **activation record (stack frame)** onto the system stack. It holds the parameters, local variables, and the return address. When the function returns, its frame is popped.

`fact(3)` → push fact(3) → push fact(2) → push fact(1) → returns 1 → pop → 2×1 = 2 → pop → 3×2 = **6**

**Types of recursion:**
- **Direct:** A calls A.
- **Indirect:** A calls B, B calls A.
- **Tail recursion:** the recursive call is the **last** statement (it can be converted into a loop easily).

**Recursion vs Iteration:**
| Recursion | Iteration |
|---|---|
| Function calls itself | Uses loops |
| Uses the stack (extra memory) | No extra stack |
| Slower (function call overhead) | Faster |
| Code is short and elegant | Code can be longer |
| Risk of stack overflow | Risk of infinite loop |

Any recursive program can be converted to iteration using an explicit stack.

## 9.2 Tower of Hanoi

**Problem:** There are 3 pegs (Source **A**, Auxiliary **B**, Destination **C**) and `n` disks of different sizes on A, with the largest at the bottom. Move all disks to C following these rules:
1. Move only **one disk at a time**.
2. Only the **top disk** of a peg can be moved.
3. **A larger disk can never be placed on a smaller disk.**

**Recursive solution:**
1. Move the top `n−1` disks from A to B (using C).
2. Move the largest (n-th) disk from A to C.
3. Move the `n−1` disks from B to C (using A).

```c
#include <stdio.h>
void toh(int n, char src, char aux, char dst) {
    if (n == 1) {
        printf("Move disk 1 from %c to %c\n", src, dst);
        return;
    }
    toh(n - 1, src, dst, aux);                           // step 1
    printf("Move disk %d from %c to %c\n", n, src, dst); // step 2
    toh(n - 1, aux, src, dst);                           // step 3
}
int main() {
    int n;
    printf("Enter number of disks: ");
    scanf("%d", &n);
    toh(n, 'A', 'B', 'C');
    return 0;
}
```

**Output for n = 3 (7 moves):**
```
1. Disk 1: A → C      5. Disk 1: B → A
2. Disk 2: A → B      6. Disk 2: B → C
3. Disk 1: C → B      7. Disk 1: A → C
4. Disk 3: A → C
```
> **Minimum number of moves = 2ⁿ − 1** (n = 3 → 7, n = 4 → 15, n = 64 → about 1.8 × 10¹⁹).
> **Time complexity = O(2ⁿ)** (exponential). Recurrence: `T(n) = 2T(n−1) + 1`.

> ### Check Yourself — Chapter 9
> 1. **What is recursion?** A function calling itself to solve a smaller version of the same problem.
> 2. **What is a base case? What happens without it?** The stopping condition. Without it: infinite recursion and a stack overflow.
> 3. **Direct vs indirect recursion?** A calls A vs A calls B and B calls A.
> 4. **What is tail recursion?** The recursive call is the last statement, so it is easy to turn into a loop.
> 5. **Recursion vs iteration?** Recursion is shorter but uses stack memory and is slower. Iteration uses loops with no call overhead.
> 6. **Tower of Hanoi: moves for n disks?** 2ⁿ − 1 (7 moves for 3 disks).
> 7. **Complexity of Tower of Hanoi?** O(2ⁿ). Recurrence: T(n) = 2T(n − 1) + 1.

---

# Chapter 10 — Divide & Conquer Sorting: Merge Sort & Quick Sort

> **Syllabus:** Module V · **Builds on:** Chapter 4 (merging two sorted arrays), Chapter 8, Chapter 9 · **Why now:** these are the fast O(n log n) sorts, built with recursion (divide and conquer).

## 10.1 Merge Sort (Lab Program 7)

**Idea (divide and conquer):**
1. **Divide** the array into two halves.
2. **Recursively sort** both halves.
3. **Merge** the two sorted halves into one sorted array.

```
            [38, 27, 43, 3, 9, 82, 10]
              /                    \
      [38, 27, 43, 3]         [9, 82, 10]
       /         \             /       \
   [38, 27]   [43, 3]      [9, 82]    [10]
    /    \     /   \        /   \       |
  [38]  [27] [43]  [3]    [9]  [82]   [10]
    \    /     \   /        \   /       |
   [27, 38]   [3, 43]      [9, 82]    [10]
       \         /             \       /
     [3, 27, 38, 43]         [9, 10, 82]
              \                    /
         [3, 9, 10, 27, 38, 43, 82]
```

```c
#include <stdio.h>

void merge(int a[], int low, int mid, int high) {
    int temp[100], i = low, j = mid + 1, k = 0;
    while (i <= mid && j <= high) {
        if (a[i] <= a[j]) temp[k++] = a[i++];   // <= keeps it stable
        else              temp[k++] = a[j++];
    }
    while (i <= mid)  temp[k++] = a[i++];
    while (j <= high) temp[k++] = a[j++];
    for (i = low, k = 0; i <= high; i++, k++)   // copy back
        a[i] = temp[k];
}

void mergeSort(int a[], int low, int high) {
    if (low < high) {
        int mid = (low + high) / 2;
        mergeSort(a, low, mid);
        mergeSort(a, mid + 1, high);
        merge(a, low, mid, high);
    }
}

int main() {
    int a[100], n, i;
    printf("Enter n: "); scanf("%d", &n);
    for (i = 0; i < n; i++) scanf("%d", &a[i]);
    mergeSort(a, 0, n - 1);
    printf("Sorted: ");
    for (i = 0; i < n; i++) printf("%d ", a[i]);
    return 0;
}
```
- **O(n log n) in ALL cases** (best, average, worst). Recurrence: `T(n) = 2T(n/2) + n`.
- **Space O(n)** (extra temp array), so **not in-place**. **Stable: Yes.**
- **Best for linked lists and external sorting** (large files on disk).

## 10.2 Quick Sort / Partition Exchange Sort (Lab Program 6)

> **Quick sort is also called "Partition Exchange Sort"** (both names are in your syllabus; they are the **same algorithm**). It was developed by **C.A.R. Hoare**.

**Idea (divide and conquer):**
1. **Choose a pivot** element (first, last, middle, or random).
2. **Partition:** rearrange the array so that elements **smaller than the pivot go to its left** and **larger elements go to its right**. The pivot is now at its **final sorted position**.
3. **Recursively** quick sort the left and right parts.

**Partition (Lomuto scheme, pivot = last element):**
```c
#include <stdio.h>

void swap(int *x, int *y) { int t = *x; *x = *y; *y = t; }

int partition(int a[], int low, int high) {
    int pivot = a[high];
    int i = low - 1;                  // boundary of the "smaller than pivot" region
    for (int j = low; j < high; j++) {
        if (a[j] < pivot) {
            i++;
            swap(&a[i], &a[j]);
        }
    }
    swap(&a[i + 1], &a[high]);        // put the pivot in its correct place
    return i + 1;
}

void quickSort(int a[], int low, int high) {
    if (low < high) {
        int p = partition(a, low, high);
        quickSort(a, low, p - 1);     // left of pivot
        quickSort(a, p + 1, high);    // right of pivot
    }
}

int main() {
    int a[100], n, i;
    printf("Enter n: "); scanf("%d", &n);
    for (i = 0; i < n; i++) scanf("%d", &a[i]);
    quickSort(a, 0, n - 1);
    printf("Sorted: ");
    for (i = 0; i < n; i++) printf("%d ", a[i]);
    return 0;
}
```

**Example:** `[10, 80, 30, 90, 40, 50, 70]`, pivot = 70
→ after partition: `[10, 30, 40, 50, 70, 90, 80]`. 70 is at its final place. Now sort `[10,30,40,50]` and `[90,80]` recursively.

**Complexity:**
- **Best/Average: O(n log n)** – the pivot divides the array into roughly equal halves.
- **Worst: O(n²)** – the pivot is always the smallest or largest element (e.g., an **already sorted array with the first/last element as pivot**).
- Space: O(log n) for the recursion stack. **Not stable.** In-place.
- **Avoid the worst case** by choosing a random pivot or the median-of-three.

**Why is quick sort usually the fastest in practice?** It is in-place, cache-friendly, and has small constant factors.

## 10.3 Quick Sort vs Merge Sort

| Quick Sort | Merge Sort |
|---|---|
| Worst O(n²) | Always O(n log n) |
| In-place (O(log n) stack) | Needs O(n) extra space |
| Not stable | Stable |
| The work is done in **partitioning** (before recursion) | The work is done in **merging** (after recursion) |
| Usually faster on arrays | Better for linked lists and external sorting |

> ### Check Yourself — Chapter 10
> 1. **What is divide and conquer?** Split the problem, solve the parts recursively, then combine the results.
> 2. **Complexity of merge sort?** O(n log n) in all cases. Extra space O(n).
> 3. **What is partition exchange sort?** Another name for quick sort.
> 4. **What is a pivot?** The element around which the array is partitioned. After partitioning, it is in its final position.
> 5. **Worst case of quick sort? When?** O(n²), when the pivot is always the smallest or largest element (e.g., sorted input with the first or last element as pivot).
> 6. **How do you avoid the worst case?** Use a random pivot or the median of three.
> 7. **Which of the two is stable?** Merge sort. Quick sort is not.
> 8. **Which sort is used for linked lists and external sorting?** Merge sort.

---

# Chapter 11 — Linked Lists

> **Syllabus:** Module III · **Builds on:** Chapter 2 (struct, pointers, malloc), Chapter 4 (the limits of arrays) · **Why now:** your first dynamic data structure, which grows and shrinks at run time.

## 11.1 Why Linked Lists?

Problems with arrays:
1. **Fixed size.** You must know the size in advance, which wastes memory or runs out.
2. **Costly insertion/deletion.** Elements must be shifted, O(n).
3. **Needs contiguous memory.** A large block may not be available even when enough total memory is free.

A **linked list** solves these problems.

## 11.2 What is a Linked List?

A **linked list** is a **linear collection of data elements called nodes**, where the order is given by **pointers (links)**, not by physical position in memory.
Each **node** has two parts:
1. **INFO / DATA** – the actual value
2. **LINK / NEXT** – the address of the next node

```
 START/HEAD
    |
    v
 +----+----+    +----+----+    +----+------+
 | 10 |  --+--->| 20 |  --+--->| 30 | NULL |
 +----+----+    +----+----+    +----+------+
  data next
```
- **START (HEAD)** pointer holds the address of the first node.
- The **last node's link is NULL**, which marks the end of the list.
- If `START == NULL`, the list is **empty**.

**Node in C (a self-referential structure: a structure that contains a pointer to its own type):**
```c
struct node {
    int data;
    struct node *next;
};
```

**Creating a node:**
```c
struct node *newnode = (struct node *) malloc(sizeof(struct node));
newnode->data = 10;
newnode->next = NULL;
```

### Array vs Linked List

| Array | Linked List |
|---|---|
| Fixed size (static) | Dynamic size (grows/shrinks at run time) |
| Contiguous memory | Nodes scattered anywhere in memory |
| Random access, O(1) | Sequential access only, O(n) |
| Insertion/deletion O(n) (shifting) | Insertion/deletion O(1) once the position is known (just change links) |
| No extra memory per element | Extra memory for the pointer in every node |
| Memory may be wasted if not full | Memory allocated only as needed |
| Binary search possible | Binary search not efficient (no random access) |
| Cache friendly | Not cache friendly |

### Types of Linked Lists

1. **Singly linked list** – each node points to the next one only.
2. **Doubly linked list** – each node points to both the next and the previous node.
3. **Circular linked list** – the last node points back to the first node.
4. **Doubly circular linked list** – doubly linked, and the last and first nodes are connected both ways.
5. **Header linked list** – has a special header node at the beginning, which can store information such as the count of nodes.

## 11.3 Representation of a Linked List in Memory

Without pointers (or in a textbook like Lipschutz), a linked list is represented using **two parallel arrays**:
- `INFO[k]` – data of node k
- `LINK[k]` – index of the next node
- `START` – index of the first node
- `NULL` – represented by 0 or −1

Example (list: A → B → C, with START = 3):
| Index | INFO | LINK |
|---|---|---|
| 1 | B | 4 |
| 2 | – | – |
| 3 | A | 1 |
| 4 | C | 0 (NULL) |

Traversal: START = 3 → INFO[3] = A → LINK[3] = 1 → B → LINK[1] = 4 → C → LINK[4] = 0 → stop.

**AVAIL list (free storage list):** the free (unused) nodes are kept in a separate linked list called **AVAIL**. When a new node is needed, it is taken from AVAIL. When a node is deleted, it is returned to AVAIL.
- **Overflow:** inserting when `AVAIL == NULL` (no free memory).
- **Underflow:** deleting when `START == NULL` (empty list).

## 11.4 Operations on a Singly Linked List


### Traversing

```
1. PTR = START
2. Repeat while PTR != NULL:
       Process PTR->data
       PTR = PTR->next
3. Exit
```
```c
void display(struct node *head) {
    struct node *ptr = head;
    while (ptr != NULL) {
        printf("%d -> ", ptr->data);
        ptr = ptr->next;
    }
    printf("NULL\n");
}
```
**Why not move `head` itself?** Because we would lose the address of the first node. Always use a temporary pointer.

### Searching (Linear only)

```c
struct node* search(struct node *head, int key) {
    struct node *ptr = head;
    int pos = 1;
    while (ptr != NULL) {
        if (ptr->data == key) { printf("Found at position %d\n", pos); return ptr; }
        ptr = ptr->next;
        pos++;
    }
    printf("Not found\n");
    return NULL;
}
```
Complexity O(n). **Binary search isn't efficient on a linked list** because reaching the middle element takes O(n) time.

### Insertion

**(a) At the beginning – O(1)**
```
newnode->next = head;
head = newnode;
```
**(b) At the end – O(n)** (traverse to the last node)
```
ptr = head; while (ptr->next != NULL) ptr = ptr->next;
ptr->next = newnode;
```
**(c) After a given position/node – O(n)**
```
newnode->next = ptr->next;   // step 1: connect new node to the next node FIRST
ptr->next = newnode;         // step 2: then connect the previous node to the new node
```
> **Order matters!** If you do step 2 first, you lose the address of the rest of the list.

### Deletion

**(a) From the beginning:** `temp = head; head = head->next; free(temp);`
**(b) From the end:** go to the second-last node, `free` its next, set its next to NULL.
**(c) By value:** keep a pointer `prev` to the node before the target: `prev->next = target->next; free(target);`

Always `free()` the deleted node, otherwise there is a **memory leak**.

### Complete Singly Linked List Program (Lab Program 14)

```c
#include <stdio.h>
#include <stdlib.h>

struct node {
    int data;
    struct node *next;
};
struct node *head = NULL;

struct node* createNode(int x) {
    struct node *n = (struct node *) malloc(sizeof(struct node));
    if (n == NULL) { printf("Memory overflow\n"); exit(1); }
    n->data = x;
    n->next = NULL;
    return n;
}

void insertBegin(int x) {
    struct node *n = createNode(x);
    n->next = head;
    head = n;
}

void insertEnd(int x) {
    struct node *n = createNode(x), *ptr = head;
    if (head == NULL) { head = n; return; }
    while (ptr->next != NULL) ptr = ptr->next;
    ptr->next = n;
}

void insertAtPos(int x, int pos) {           // pos is 1-based
    if (pos == 1) { insertBegin(x); return; }
    struct node *ptr = head;
    for (int i = 1; i < pos - 1 && ptr != NULL; i++) ptr = ptr->next;
    if (ptr == NULL) { printf("Invalid position\n"); return; }
    struct node *n = createNode(x);
    n->next = ptr->next;
    ptr->next = n;
}

void deleteBegin() {
    if (head == NULL) { printf("Underflow: list empty\n"); return; }
    struct node *temp = head;
    head = head->next;
    printf("Deleted %d\n", temp->data);
    free(temp);
}

void deleteEnd() {
    if (head == NULL) { printf("Underflow: list empty\n"); return; }
    if (head->next == NULL) {                // only one node
        printf("Deleted %d\n", head->data);
        free(head); head = NULL; return;
    }
    struct node *ptr = head;
    while (ptr->next->next != NULL) ptr = ptr->next;   // second-last node
    printf("Deleted %d\n", ptr->next->data);
    free(ptr->next);
    ptr->next = NULL;
}

void deleteValue(int key) {
    struct node *ptr = head, *prev = NULL;
    while (ptr != NULL && ptr->data != key) { prev = ptr; ptr = ptr->next; }
    if (ptr == NULL) { printf("%d not found\n", key); return; }
    if (prev == NULL) head = ptr->next;      // deleting the first node
    else prev->next = ptr->next;
    free(ptr);
    printf("Deleted %d\n", key);
}

void search(int key) {
    struct node *ptr = head;
    int pos = 1;
    while (ptr != NULL) {
        if (ptr->data == key) { printf("%d found at position %d\n", key, pos); return; }
        ptr = ptr->next; pos++;
    }
    printf("%d not found\n", key);
}

void display() {
    struct node *ptr = head;
    if (head == NULL) { printf("List is empty\n"); return; }
    while (ptr != NULL) { printf("%d -> ", ptr->data); ptr = ptr->next; }
    printf("NULL\n");
}

int main() {
    int ch, x, pos;
    while (1) {
        printf("\n1.Insert Begin 2.Insert End 3.Insert at Pos 4.Delete Begin\n"
               "5.Delete End 6.Delete Value 7.Search 8.Display 9.Exit\nChoice: ");
        scanf("%d", &ch);
        switch (ch) {
            case 1: printf("Value: "); scanf("%d", &x); insertBegin(x); break;
            case 2: printf("Value: "); scanf("%d", &x); insertEnd(x); break;
            case 3: printf("Value and position: "); scanf("%d %d", &x, &pos); insertAtPos(x, pos); break;
            case 4: deleteBegin(); break;
            case 5: deleteEnd(); break;
            case 6: printf("Value: "); scanf("%d", &x); deleteValue(x); break;
            case 7: printf("Value: "); scanf("%d", &x); search(x); break;
            case 8: display(); break;
            case 9: return 0;
        }
    }
}
```
"Creation" of a list = calling `insertEnd()` repeatedly for n values.

### Count Occurrences of an Item (Lab Program 17)

```c
int countItem(struct node *head, int item) {
    int count = 0;
    struct node *ptr = head;
    while (ptr != NULL) {
        if (ptr->data == item) count++;
        ptr = ptr->next;
    }
    return count;
}
```

### Increment Every Node's Data by 10 (Lab Program 18)

```c
void incrementBy10(struct node *head) {
    struct node *ptr = head;
    while (ptr != NULL) {
        ptr->data += 10;
        ptr = ptr->next;
    }
}
/* in main: display(); incrementBy10(head); display();  → shows before and after */
```

### Other Common Viva Programs on Linked Lists

**Count nodes:** traverse and increment a counter.
**Reverse a singly linked list (very common question):**
```c
void reverse() {
    struct node *prev = NULL, *curr = head, *next = NULL;
    while (curr != NULL) {
        next = curr->next;   // save next
        curr->next = prev;   // reverse the link
        prev = curr;         // move prev forward
        curr = next;         // move curr forward
    }
    head = prev;
}
```
**Find the middle node:** use two pointers, slow (moves 1 step) and fast (moves 2 steps). When fast reaches the end, slow is at the middle.

## 11.5 Garbage Collection and Compaction

When nodes are deleted, their memory must be returned so it can be reused.

**Garbage** = memory that is allocated but no longer reachable or used by the program.

**Garbage Collection:** the process of **automatically finding unused memory blocks and returning them to the free storage list (AVAIL list)**.
- It usually happens when memory is nearly exhausted, or when the CPU is idle.
- It works in **two phases:**
  1. **Marking phase:** go through all reachable nodes (from all pointers in use) and **mark** them.
  2. **Collection (sweep) phase:** scan the whole memory, and **unmarked nodes are added to the AVAIL list**.
- Languages like Java and Python have automatic garbage collection. **C does not.** In C the programmer must call `free()` manually.

**Compaction:** After many allocations and deallocations, free memory is broken into small scattered pieces (**fragmentation**). A large request may fail even if the total free memory is enough.
**Compaction moves all used blocks to one end of memory** so that all free memory becomes **one large contiguous block**. Pointers must be updated after moving.

> **Viva:** "Garbage collection reclaims unused memory and adds it to the free list. Compaction rearranges used memory to remove fragmentation and make free memory contiguous."

## 11.6 Doubly Linked List (DLL)

Each node has **three parts**: a pointer to the **previous** node, the **data**, and a pointer to the **next** node.

```
 NULL <-- [prev | 10 | next] <--> [prev | 20 | next] <--> [prev | 30 | next] --> NULL
           ^ head
```
```c
struct dnode {
    struct dnode *prev;
    int data;
    struct dnode *next;
};
```

**Advantages over a singly linked list:**
- Can be traversed in **both directions** (forward and backward).
- Deleting a given node is easier, because you can get to the previous node directly.
- Inserting before a given node is easy.

**Disadvantages:**
- Extra memory for the `prev` pointer in each node.
- More pointer updates on insertion/deletion (more chances of bugs).

**Applications:** browser forward/back, music player next/previous, undo/redo, LRU cache.

### Doubly Linked List Program (Lab Program 19)

```c
#include <stdio.h>
#include <stdlib.h>

struct dnode { struct dnode *prev; int data; struct dnode *next; };
struct dnode *head = NULL;

struct dnode* createNode(int x) {
    struct dnode *n = (struct dnode *) malloc(sizeof(struct dnode));
    n->data = x; n->prev = n->next = NULL;
    return n;
}

void insertBegin(int x) {
    struct dnode *n = createNode(x);
    if (head != NULL) { n->next = head; head->prev = n; }
    head = n;
}

void insertEnd(int x) {
    struct dnode *n = createNode(x), *ptr = head;
    if (head == NULL) { head = n; return; }
    while (ptr->next != NULL) ptr = ptr->next;
    ptr->next = n;
    n->prev = ptr;
}

void insertAfter(int key, int x) {              // insert x after the node containing key
    struct dnode *ptr = head;
    while (ptr != NULL && ptr->data != key) ptr = ptr->next;
    if (ptr == NULL) { printf("%d not found\n", key); return; }
    struct dnode *n = createNode(x);
    n->next = ptr->next;
    n->prev = ptr;
    if (ptr->next != NULL) ptr->next->prev = n;
    ptr->next = n;
}

void deleteValue(int key) {
    struct dnode *ptr = head;
    while (ptr != NULL && ptr->data != key) ptr = ptr->next;
    if (ptr == NULL) { printf("%d not found\n", key); return; }
    if (ptr->prev != NULL) ptr->prev->next = ptr->next;
    else head = ptr->next;                      // deleting the first node
    if (ptr->next != NULL) ptr->next->prev = ptr->prev;
    free(ptr);
    printf("Deleted %d\n", key);
}

void search(int key) {
    struct dnode *ptr = head; int pos = 1;
    while (ptr != NULL) {
        if (ptr->data == key) { printf("Found at position %d\n", pos); return; }
        ptr = ptr->next; pos++;
    }
    printf("Not found\n");
}

void displayForward() {
    struct dnode *ptr = head;
    printf("Forward: ");
    while (ptr != NULL) { printf("%d <-> ", ptr->data); ptr = ptr->next; }
    printf("NULL\n");
}

void displayBackward() {
    struct dnode *ptr = head;
    if (ptr == NULL) { printf("List empty\n"); return; }
    while (ptr->next != NULL) ptr = ptr->next;   // go to the last node
    printf("Backward: ");
    while (ptr != NULL) { printf("%d <-> ", ptr->data); ptr = ptr->prev; }
    printf("NULL\n");
}

int main() {
    int ch, x, key;
    while (1) {
        printf("\n1.Insert Begin 2.Insert End 3.Insert After 4.Delete\n"
               "5.Search 6.Display Fwd 7.Display Back 8.Exit\nChoice: ");
        scanf("%d", &ch);
        switch (ch) {
            case 1: scanf("%d", &x); insertBegin(x); break;
            case 2: scanf("%d", &x); insertEnd(x); break;
            case 3: printf("After which value, new value: "); scanf("%d %d", &key, &x); insertAfter(key, x); break;
            case 4: scanf("%d", &x); deleteValue(x); break;
            case 5: scanf("%d", &x); search(x); break;
            case 6: displayForward(); break;
            case 7: displayBackward(); break;
            case 8: return 0;
        }
    }
}
```

## 11.7 Circular Linked List (CLL)

In a **circular linked list**, the **last node points back to the first node** instead of NULL. There is no NULL anywhere in the list.

```
  head
   |
   v
 [10| ]--> [20| ]--> [30| ]--+
   ^                         |
   +-------------------------+
```

- **Singly circular:** `last->next = head`
- **Doubly circular:** `last->next = head` and `head->prev = last`

**Traversal must stop when we come back to `head`** (not at NULL), so use a `do-while` loop:
```c
void display() {
    if (head == NULL) { printf("Empty\n"); return; }
    struct node *ptr = head;
    do {
        printf("%d -> ", ptr->data);
        ptr = ptr->next;
    } while (ptr != head);
    printf("(back to head)\n");
}
```

**Insert at the end:**
```c
void insertEnd(int x) {
    struct node *n = createNode(x);
    if (head == NULL) { head = n; n->next = head; return; }
    struct node *ptr = head;
    while (ptr->next != head) ptr = ptr->next;   // find the last node
    ptr->next = n;
    n->next = head;
}
```
**Insert at the beginning:** insert as at the end, then set `head = n`. (Or keep a `last` pointer: then both insertions are O(1).)

**Delete from the beginning:**
```c
void deleteBegin() {
    if (head == NULL) return;
    if (head->next == head) { free(head); head = NULL; return; }  // one node
    struct node *last = head, *temp = head;
    while (last->next != head) last = last->next;
    head = head->next;
    last->next = head;
    free(temp);
}
```

> **Tip:** Many implementations keep a pointer to the **last** node instead of the head, since `last->next` is the head. Then insertion at both the beginning and the end is O(1).

**Advantages:** any node can be the starting point, and the list can be traversed repeatedly in a cycle. Good for round-robin scheduling.
**Disadvantage:** there is a risk of an **infinite loop** if the stopping condition is wrong.
**Applications:** round-robin CPU scheduling, multiplayer games (turns), circular buffers, repeating a music playlist.

## 11.8 Generalized List

A **generalized list** is a finite sequence of elements where **each element is either an atom (single value) or another list (sub-list)**.

Example: `L = (a, (b, c), d)`
- Length = 3 (elements: `a`, `(b, c)`, `d`)
- `(b, c)` is a sub-list.

Other examples: `( )` is an empty list; `(a, (b, (c, d)))` is a nested list.

**Node structure** (uses a tag/flag):
```
| tag | data / sublist pointer | next |
```
- `tag = 0` → the node holds an **atom (data)**
- `tag = 1` → the node holds a **pointer to a sub-list**

```c
struct gnode {
    int tag;                    // 0 = atom, 1 = sublist
    union {
        char data;
        struct gnode *sublist;
    } u;
    struct gnode *next;
};
```
**Applications:** representing **multivariable polynomials**, LISP programming lists, nested data structures (like JSON).

## 11.9 Application: Polynomial Representation Using a Linked List

A polynomial like `5x³ + 4x² + 2` is stored as a linked list where each node represents one term:
```
| coeff | exp | next |
```
```
[5|3| ]-->[4|2| ]-->[2|0|NULL]
```
Terms are stored in **decreasing order of exponent**.
**Why a linked list instead of an array?** An array would need a slot for every exponent (e.g., `x¹⁰⁰⁰ + 1` would need 1001 slots, mostly zeros). A linked list stores only the non-zero terms.

```c
struct poly {
    int coeff;
    int exp;
    struct poly *next;
};
```

### Polynomial Addition Algorithm

Let `p1` and `p2` point to the two polynomials:
1. If `p1->exp == p2->exp` → add the coefficients, create a node with the sum, and move both pointers.
2. If `p1->exp > p2->exp` → copy the p1 term, move p1.
3. If `p1->exp < p2->exp` → copy the p2 term, move p2.
4. When one list ends, copy the remaining terms of the other.

```c
struct poly* newTerm(int c, int e) {
    struct poly *t = (struct poly *) malloc(sizeof(struct poly));
    t->coeff = c; t->exp = e; t->next = NULL;
    return t;
}

struct poly* addPoly(struct poly *p1, struct poly *p2) {
    struct poly *result = NULL, *tail = NULL, *t;
    while (p1 != NULL || p2 != NULL) {
        if (p2 == NULL || (p1 != NULL && p1->exp > p2->exp)) {
            t = newTerm(p1->coeff, p1->exp); p1 = p1->next;
        } else if (p1 == NULL || p2->exp > p1->exp) {
            t = newTerm(p2->coeff, p2->exp); p2 = p2->next;
        } else {                                   // equal exponents
            t = newTerm(p1->coeff + p2->coeff, p1->exp);
            p1 = p1->next; p2 = p2->next;
        }
        if (result == NULL) result = tail = t;
        else { tail->next = t; tail = t; }
    }
    return result;
}
```
**Example:** `(5x³ + 4x² + 2) + (3x² + 2x + 1)` = **`5x³ + 7x² + 2x + 3`**

**Polynomial multiplication:** multiply each term of p1 by each term of p2 (multiply coefficients, **add exponents**), then combine terms with equal exponents.

> ### Check Yourself — Chapter 11
> 1. **What is a linked list?** A linear collection of nodes, each holding data and a pointer to the next node.
> 2. **Array vs linked list?** Static vs dynamic, contiguous vs scattered, random vs sequential access, costly vs cheap insertion and deletion.
> 3. **What does the last node contain? How do you know the list is empty?** NULL in its next field. The list is empty when `head == NULL`.
> 4. **Why use a temp pointer for traversal?** So the address held in head isn't lost.
> 5. **What is the AVAIL list?** The list of free nodes from which new nodes are taken.
> 6. **Overflow and underflow in a linked list?** No free memory when inserting / deleting from an empty list.
> 7. **Garbage collection vs compaction?** Reclaiming unused nodes into the free list (mark and sweep) vs moving used blocks together to remove fragmentation.
> 8. **Advantage of a doubly linked list?** Two-way traversal, and a given node is easy to delete.
> 9. **How do you stop traversing a circular list?** Stop when the pointer comes back to head (use do-while).
> 10. **What is a generalized list?** A list whose elements can be atoms or sub-lists, e.g., (a, (b, c), d).
> 11. **How is a polynomial stored?** As nodes of (coefficient, exponent, next) in decreasing order of exponent.
> 12. **How do you reverse a linked list?** Use three pointers (prev, curr, next) and reverse each link.

---

# Chapter 12 — Stacks

> **Syllabus:** Module II (+ "stack implementation using linked list" from Module III) · **Builds on:** Chapters 4, 9 and 11 · **Why now:** a stack is a list with a restriction. You can now build it with an array *and* with a linked list, and see how recursion really works inside the computer.

## 12.1 What is a Stack?

A **stack** is a **linear data structure** in which insertion and deletion happen at **only one end**, called the **TOP**.
It follows **LIFO – Last In, First Out** (equivalently, FILO – First In, Last Out).

**Real-life examples:** a pile of plates, a stack of books, the browser back button, undo (Ctrl+Z).

```
      |  30  |  ← TOP (last pushed, first popped)
      |  20  |
      |  10  |
      +------+
```

### Stack Operations

| Operation | Work |
|---|---|
| `push(x)` | Insert x on top |
| `pop()` | Remove and return the top element |
| `peek()` / `top()` | Return the top element without removing it |
| `isEmpty()` | True if `top == -1` |
| `isFull()` | True if `top == MAX − 1` |

- **Overflow:** trying to **push** onto a **full** stack.
- **Underflow:** trying to **pop** from an **empty** stack.

All stack operations take **O(1)** time.

## 12.2 Array Representation of Stack (Lab Program 11)

We use an array `stack[MAX]` and an integer `top`, initially `-1`.

**PUSH algorithm:**
```
1. If TOP = MAX − 1 then print "Overflow" and exit
2. TOP = TOP + 1
3. STACK[TOP] = ITEM
```
**POP algorithm:**
```
1. If TOP = −1 then print "Underflow" and exit
2. ITEM = STACK[TOP]
3. TOP = TOP − 1
```

```c
#include <stdio.h>
#define MAX 5

int stack[MAX], top = -1;

void push(int x) {
    if (top == MAX - 1) {
        printf("Stack Overflow! Cannot push %d\n", x);
        return;
    }
    stack[++top] = x;
    printf("%d pushed\n", x);
}

int pop() {
    if (top == -1) {
        printf("Stack Underflow! Stack is empty\n");
        return -1;
    }
    return stack[top--];
}

int peek() {
    if (top == -1) { printf("Stack is empty\n"); return -1; }
    return stack[top];
}

void display() {
    if (top == -1) { printf("Stack is empty\n"); return; }
    printf("Stack (top to bottom): ");
    for (int i = top; i >= 0; i--) printf("%d ", stack[i]);
    printf("\n");
}

int main() {
    int ch, x;
    while (1) {
        printf("\n1.Push 2.Pop 3.Peek 4.Display 5.Exit\nEnter choice: ");
        scanf("%d", &ch);
        switch (ch) {
            case 1: printf("Enter value: "); scanf("%d", &x); push(x); break;
            case 2: x = pop(); if (x != -1) printf("Popped: %d\n", x); break;
            case 3: x = peek(); if (x != -1) printf("Top: %d\n", x); break;
            case 4: display(); break;
            case 5: return 0;
            default: printf("Invalid choice\n");
        }
    }
}
```
**Drawback of array stack:** fixed size. A linked-list stack (next section) has no fixed size limit.

## 12.3 Stack Using a Linked List (Lab Program 15)

**Idea:** `top` is the head of the list. **Push = insert at the beginning, Pop = delete from the beginning.** Both are O(1).
**There is no overflow** (unless the computer runs out of memory). Underflow happens when `top == NULL`.

```c
#include <stdio.h>
#include <stdlib.h>
struct node { int data; struct node *next; };
struct node *top = NULL;

void push(int x) {
    struct node *n = (struct node *) malloc(sizeof(struct node));
    if (n == NULL) { printf("Stack Overflow (no memory)\n"); return; }
    n->data = x;
    n->next = top;     // new node points to the old top
    top = n;           // new node becomes top
    printf("%d pushed\n", x);
}

void pop() {
    if (top == NULL) { printf("Stack Underflow\n"); return; }
    struct node *temp = top;
    printf("%d popped\n", top->data);
    top = top->next;
    free(temp);
}

void display() {
    struct node *ptr = top;
    if (top == NULL) { printf("Stack empty\n"); return; }
    printf("Stack (top to bottom): ");
    while (ptr != NULL) { printf("%d ", ptr->data); ptr = ptr->next; }
    printf("\n");
}

int main() {
    int ch, x;
    while (1) {
        printf("\n1.Push 2.Pop 3.Display 4.Exit\nChoice: ");
        scanf("%d", &ch);
        switch (ch) {
            case 1: printf("Value: "); scanf("%d", &x); push(x); break;
            case 2: pop(); break;
            case 3: display(); break;
            case 4: return 0;
        }
    }
}
```

## 12.4 Applications of Stack

1. **Expression conversion** (infix → postfix/prefix)
2. **Expression evaluation** (postfix/prefix)
3. **Recursion / function calls** (the system call stack)
4. **Balanced parentheses checking** `{[()]}`
5. **Undo/Redo** in editors
6. **Browser back button**
7. **Reversing** a string or list
8. **Tower of Hanoi**
9. **Backtracking** (maze solving, DFS)

## 12.5 How Recursion Uses a Stack

Now that you know stacks, go back to Chapter 9: **recursion is run by the computer using a stack** (the **call stack**).
- Every function call **pushes** an **activation record (stack frame)** containing the parameters, local variables and return address.
- When the function returns, its frame is **popped** and control goes back to the caller.

Trace of `fact(3)`:
```
call fact(3)  →  [fact(3)]
call fact(2)  →  [fact(3), fact(2)]
call fact(1)  →  [fact(3), fact(2), fact(1)]   ← base case reached, returns 1
pop fact(1)   →  fact(2) computes 2 * 1 = 2
pop fact(2)   →  fact(3) computes 3 * 2 = 6
pop fact(3)   →  answer 6
```
- **Stack overflow** happens when there are too many frames (for example, a missing base case).
- Any recursive function can be rewritten as a loop by using **your own stack** instead of the call stack.

## 12.6 Polish Notation (Expressions)

| Notation | Operator position | Example of `A + B` | Other name |
|---|---|---|---|
| **Infix** | Between operands | `A + B` | Normal notation |
| **Prefix** | Before operands | `+ A B` | **Polish notation** |
| **Postfix** | After operands | `A B +` | **Reverse Polish Notation (RPN)** |

Named after the Polish mathematician **Jan Łukasiewicz**.

**Why convert to postfix/prefix?**
- Infix needs **brackets, precedence, and associativity rules**, which are hard for a computer to evaluate directly.
- Postfix/prefix need **no brackets**, and the order of operations is fixed by position.
- A postfix expression can be evaluated in **one left-to-right scan using a stack**. That is why **compilers** convert infix to postfix (the "compilation of polish expressions").

### Operator Precedence and Associativity

| Operator | Precedence | Associativity |
|---|---|---|
| `^` (exponent) | Highest (3) | **Right to left** |
| `*`  `/`  `%` | 2 | Left to right |
| `+`  `-` | Lowest (1) | Left to right |

## 12.7 Infix → Postfix (using a stack)

**Algorithm:** Scan the infix expression **left to right**:
1. **Operand** → add it directly to the output.
2. **`(`** → push it on the stack.
3. **`)`** → pop and output until `(` is found; discard both brackets.
4. **Operator** → while the stack top is an operator with **higher or equal precedence** (for `^`, only *higher*, because it is right-associative), pop it to the output. Then push the current operator.
5. At the end, pop all remaining operators to the output.

**Example:** `A * (B + C) / D - E`

| Symbol | Stack | Postfix output |
|---|---|---|
| A | | A |
| * | * | A |
| ( | * ( | A |
| B | * ( | A B |
| + | * ( + | A B |
| C | * ( + | A B C |
| ) | * | A B C + |
| / | / | A B C + * ← `*` popped (equal precedence) |
| D | / | A B C + * D |
| - | - | A B C + * D / ← `/` popped (higher) |
| E | - | A B C + * D / E |
| end | | **A B C + * D / E -** |

**Another quick one:** `A + B * C - D / E` → **`A B C * + D E / -`**

## 12.8 Infix → Prefix

**Method (Reverse – Convert – Reverse):**
1. **Reverse** the infix expression.
2. **Swap** `(` with `)` and vice versa.
3. Convert to **postfix**, with one change: for **equal precedence, do not pop** (pop only operators of *strictly higher* precedence; for `^` pop equal too).
4. **Reverse** the result → prefix.

**Example:** `A * (B + C) / D - E`
1. Reverse: `E - D / ) C + B ( * A`
2. Swap brackets: `E - D / ( C + B ) * A`
3. Postfix of this (pop only strictly higher): `E D C B + A * / -`
4. Reverse: **`- / * A + B C D E`**

**Check (bracketing method):** `((A * (B + C)) / D) - E` → move each operator before its brackets → `- / * A + B C D E` ✔

> **Shortcut for viva (manual method):** fully bracket the expression according to precedence. For postfix, move each operator to replace its **closing** bracket. For prefix, move it to replace its **opening** bracket. Then remove all brackets.

## 12.9 Evaluation of a Postfix Expression

**Algorithm:** Scan **left to right**:
1. Operand → **push**.
2. Operator → **pop two** (first pop = `op2`, second pop = `op1`), compute `op1 operator op2`, **push** the result.
3. At the end, the stack holds the answer.

**Example:** `5 6 2 + * 12 4 / -`

| Symbol | Action | Stack |
|---|---|---|
| 5 | push | 5 |
| 6 | push | 5 6 |
| 2 | push | 5 6 2 |
| + | 6 + 2 = 8 | 5 8 |
| * | 5 * 8 = 40 | 40 |
| 12 | push | 40 12 |
| 4 | push | 40 12 4 |
| / | 12 / 4 = 3 | 40 3 |
| - | 40 − 3 = 37 | **37** |

```c
/* Evaluates single-digit postfix, e.g. "562+*84/-" */
#include <stdio.h>
#include <ctype.h>
int st[50], top = -1;
void push(int x) { st[++top] = x; }
int pop() { return st[top--]; }

int evalPostfix(char *e) {
    for (int i = 0; e[i] != '\0'; i++) {
        if (isdigit(e[i])) push(e[i] - '0');
        else {
            int b = pop(), a = pop();      // b = op2, a = op1
            switch (e[i]) {
                case '+': push(a + b); break;
                case '-': push(a - b); break;
                case '*': push(a * b); break;
                case '/': push(a / b); break;
            }
        }
    }
    return pop();
}
```

## 12.10 Evaluation of a Prefix Expression

Same as postfix, but scan **right to left**, and the **first pop is `op1`**, the second is `op2`.
**Example:** `- * + 2 3 4 5` → scan from the right: push 5, 4, 3, 2 → `+`: 2 + 3 = 5 → `*`: 5 × 4 = 20 → `-`: 20 − 5 = **15**. (Infix: `(2 + 3) * 4 − 5`.)

## 12.11 Converting Back ("vice versa")

**Postfix → Infix:** Scan left to right. Push operands. On an operator, pop `op2` then `op1` and push the string `(op1 operator op2)`.
Example: `A B + C *` → push A, B → `+` gives `(A+B)` → push C → `*` gives **`((A+B)*C)`**

**Prefix → Infix:** Scan right to left. Push operands. On an operator, pop `op1` then `op2` and push `(op1 operator op2)`.
Example: `* + A B C` → push C, B, A → `+` gives `(A+B)` → `*` gives **`((A+B)*C)`**

**Prefix → Postfix:** Scan right to left. On an operator, pop `op1`, `op2` and push `op1 op2 operator`.
**Postfix → Prefix:** Scan left to right. On an operator, pop `op2`, `op1` and push `operator op1 op2`.

> ### Check Yourself — Chapter 12
> 1. **What is a stack? What principle does it follow?** A linear structure with insertion and deletion at one end (the top). LIFO.
> 2. **Overflow and underflow?** Pushing onto a full stack / popping from an empty stack.
> 3. **Why is top initialized to −1?** −1 means empty, and the first push goes to index 0.
> 4. **Stack using a linked list: where do push and pop happen?** At the head (head = top). Both are O(1), and there is no overflow.
> 5. **Applications of a stack?** Recursion, expression conversion and evaluation, bracket matching, undo, the browser back button.
> 6. **What is Polish notation?** Prefix (operator before operands). Reverse Polish notation is postfix.
> 7. **Why do computers prefer postfix?** It needs no brackets or precedence rules and can be evaluated in one scan with a stack.
> 8. **Convert `(A+B)*C` to postfix and prefix.** `AB+C*` and `*+ABC`.
> 9. **Which data structure does recursion use?** A stack (the call stack of activation records).
> 10. **How do you check balanced brackets?** Push each opening bracket. On a closing bracket, pop and match it. At the end, the stack must be empty.

---

# Chapter 13 — Queues

> **Syllabus:** Module II (+ "queue implementation using linked list" from Module III) · **Builds on:** Chapters 11 and 12 · **Why now:** the queue is the "sister" of the stack, so it's easiest to learn right after it.

## 13.1 What is a Queue?

A **queue** is a **linear data structure** in which **insertion happens at one end (REAR)** and **deletion happens at the other end (FRONT)**.
It follows **FIFO – First In, First Out**.

**Real-life examples:** a ticket counter line, a printer job queue, CPU scheduling, keyboard buffer, call center waiting.

```
 FRONT →  10 | 20 | 30 | 40  ← REAR
 (delete here)           (insert here)
```

### Queue Operations

| Operation | Work |
|---|---|
| `enqueue(x)` / insert | Add at REAR |
| `dequeue()` / delete | Remove from FRONT |
| `peek()` / `front()` | See the front element |
| `isEmpty()` | `front == -1` (or `front > rear`) |
| `isFull()` | `rear == MAX − 1` (linear queue) |

### Representation of a Queue

1. **Array representation** (below)
2. **Linked list representation** (covered below)

## 13.2 Linear Queue Using an Array (Lab Program 12)

```c
#include <stdio.h>
#define MAX 5
int queue[MAX], front = -1, rear = -1;

void insert(int x) {
    if (rear == MAX - 1) { printf("Queue Overflow\n"); return; }
    if (front == -1) front = 0;          // first element
    queue[++rear] = x;
    printf("%d inserted\n", x);
}

void delete() {
    if (front == -1 || front > rear) { printf("Queue Underflow\n"); return; }
    printf("%d deleted\n", queue[front++]);
    if (front > rear) front = rear = -1; // queue became empty, reset
}

void display() {
    if (front == -1) { printf("Queue is empty\n"); return; }
    printf("Queue: ");
    for (int i = front; i <= rear; i++) printf("%d ", queue[i]);
    printf("\n");
}

int main() {
    int ch, x;
    while (1) {
        printf("\n1.Insert 2.Delete 3.Display 4.Exit\nChoice: ");
        scanf("%d", &ch);
        switch (ch) {
            case 1: printf("Value: "); scanf("%d", &x); insert(x); break;
            case 2: delete(); break;
            case 3: display(); break;
            case 4: return 0;
        }
    }
}
```

**Drawback of a linear queue:** After some deletions, empty spaces at the **front cannot be reused**. Once `rear` reaches `MAX−1`, the queue says "Overflow" even if the front is empty.
Example: MAX = 5. Insert 5 elements, delete 3 → 3 slots are free, but `rear == 4`, so insertion is still refused.
**Solution → Circular Queue.**

## 13.3 Circular Queue

In a **circular queue**, the last position is connected back to the first position, forming a circle. When `rear` reaches the end, it **wraps around** to index 0 if that space is free.

**Key formulas (use `% MAX` to wrap):**
- Next rear: `rear = (rear + 1) % MAX`
- Next front: `front = (front + 1) % MAX`
- **Full condition:** `(rear + 1) % MAX == front`
- **Empty condition:** `front == -1`

### Circular Queue Using an Array (Lab Program 13)

```c
#include <stdio.h>
#define MAX 5
int cq[MAX], front = -1, rear = -1;

void insert(int x) {
    if ((rear + 1) % MAX == front) { printf("Circular Queue Overflow\n"); return; }
    if (front == -1) front = rear = 0;       // first element
    else rear = (rear + 1) % MAX;            // wrap around
    cq[rear] = x;
    printf("%d inserted\n", x);
}

void delete() {
    if (front == -1) { printf("Circular Queue Underflow\n"); return; }
    printf("%d deleted\n", cq[front]);
    if (front == rear) front = rear = -1;    // only one element was there
    else front = (front + 1) % MAX;
}

void display() {
    if (front == -1) { printf("Queue is empty\n"); return; }
    printf("Queue: ");
    int i = front;
    while (1) {
        printf("%d ", cq[i]);
        if (i == rear) break;
        i = (i + 1) % MAX;
    }
    printf("\n");
}

int main() {
    int ch, x;
    while (1) {
        printf("\n1.Insert 2.Delete 3.Display 4.Exit\nChoice: ");
        scanf("%d", &ch);
        switch (ch) {
            case 1: printf("Value: "); scanf("%d", &x); insert(x); break;
            case 2: delete(); break;
            case 3: display(); break;
            case 4: return 0;
        }
    }
}
```
**Advantage:** better memory utilization, since freed spaces are reused.
**Uses:** CPU round-robin scheduling, traffic light systems, memory buffers (keyboard buffer, streaming).

## 13.4 Queue Using a Linked List (Lab Program 16)

**Idea:** Keep two pointers, `front` (first node) and `rear` (last node).
**Insert at the rear, delete from the front.** Both are O(1).

```c
#include <stdio.h>
#include <stdlib.h>
struct node { int data; struct node *next; };
struct node *front = NULL, *rear = NULL;

void insert(int x) {
    struct node *n = (struct node *) malloc(sizeof(struct node));
    n->data = x; n->next = NULL;
    if (rear == NULL) front = rear = n;     // empty queue
    else { rear->next = n; rear = n; }
    printf("%d inserted\n", x);
}

void delete() {
    if (front == NULL) { printf("Queue Underflow\n"); return; }
    struct node *temp = front;
    printf("%d deleted\n", front->data);
    front = front->next;
    if (front == NULL) rear = NULL;         // queue became empty
    free(temp);
}

void display() {
    struct node *ptr = front;
    if (front == NULL) { printf("Queue empty\n"); return; }
    printf("Queue: ");
    while (ptr != NULL) { printf("%d ", ptr->data); ptr = ptr->next; }
    printf("\n");
}

int main() {
    int ch, x;
    while (1) {
        printf("\n1.Insert 2.Delete 3.Display 4.Exit\nChoice: ");
        scanf("%d", &ch);
        switch (ch) {
            case 1: printf("Value: "); scanf("%d", &x); insert(x); break;
            case 2: delete(); break;
            case 3: display(); break;
            case 4: return 0;
        }
    }
}
```
> **Important:** When the last node is deleted, set `rear = NULL` too. Otherwise `rear` becomes a dangling pointer.

## 13.5 Priority Queue

A **priority queue** is a queue in which **each element has a priority**, and the element with the **highest priority is deleted first**, regardless of insertion order.
**Rules:**
1. A higher-priority element is processed before a lower-priority one.
2. Elements with the **same priority** are processed in **FIFO** order.

**Types:**
- **Ascending priority queue:** the smallest value (highest priority) is removed first.
- **Descending priority queue:** the largest value is removed first.

**Implementations:**
| Method | Insert | Delete |
|---|---|---|
| Unsorted array/list | O(1) | O(n) (search for highest) |
| Sorted array/list | O(n) (find position) | O(1) |
| Multiple queues (one queue per priority level) | O(1) | O(number of priorities) |
| **Heap** (best, see Chapter 15) | O(log n) | O(log n) |

**Applications:** CPU scheduling by priority, Dijkstra's shortest path, Huffman coding, emergency room triage, OS interrupt handling.

## 13.6 Deque (Double-Ended Queue)

A **deque** (pronounced "deck") is a linear list in which **insertion and deletion can happen at both ends** (front and rear).
Operations: `insertFront`, `insertRear`, `deleteFront`, `deleteRear`.

**Types:**
1. **Input-restricted deque:** insertion at **only one end** (rear), deletion at **both** ends.
2. **Output-restricted deque:** deletion at **only one end** (front), insertion at **both** ends.

> A deque can work as **both a stack and a queue**. Use only one end → stack. Insert at one end, delete at the other → queue.

**Applications:** browser history, undo/redo with a limit, sliding window problems, palindrome checking, work-stealing job schedulers.

## 13.7 Stack vs Queue

| Stack | Queue |
|---|---|
| LIFO | FIFO |
| One end (TOP) | Two ends (FRONT, REAR) |
| push / pop | enqueue / dequeue |
| One pointer: `top` | Two pointers: `front`, `rear` |
| Used in recursion, expression evaluation, undo | Used in scheduling, buffering, BFS |
| Example: pile of plates | Example: ticket line |

> ### Check Yourself — Chapter 13
> 1. **What is a queue? What principle does it follow?** Insert at the rear, delete at the front. FIFO.
> 2. **Drawback of a linear array queue?** Space freed at the front can't be reused.
> 3. **Full condition of a circular queue?** `(rear + 1) % MAX == front`.
> 4. **Why use `% MAX`?** To wrap the index back to 0 after the last position.
> 5. **Queue using a linked list: which pointers?** front (for deletion) and rear (for insertion). When the queue becomes empty, set rear = NULL too.
> 6. **What is a priority queue? Best implementation?** Elements are removed by priority. A heap.
> 7. **What is a deque? Types?** Insertion and deletion at both ends. Input-restricted and output-restricted.
> 8. **How many stacks are needed to build a queue?** Two.
> 9. **Stack vs queue?** LIFO with one end vs FIFO with two ends.

---

# Chapter 14 — Hashing

> **Syllabus:** Module V · **Builds on:** Chapter 7 (searching), Chapter 11 (linked lists, used for chaining) · **Why now:** hashing is the fastest way to search (O(1) on average) and uses arrays and linked lists together.

## 14.1 What is Hashing?

**Problem:** Linear search is O(n), and binary search is O(log n) but needs sorted data. Can we search in **O(1)**?
**Hashing** is a technique to **store and retrieve data in constant time O(1) on average**, by calculating the location of a key directly from the key itself.

- **Hash table:** an array where the data is stored. Its positions are called **buckets/slots**.
- **Hash function h(k):** converts a key `k` into an index in the hash table (0 to m−1).
- **Collision:** when **two different keys get the same index**, i.e., `h(k1) = h(k2)`.
- **Load factor α = n / m** (n = number of keys stored, m = table size). A smaller α means fewer collisions.

## 14.2 Hash Functions

**Properties of a good hash function:**
1. Easy and fast to compute.
2. Distributes keys **uniformly** across the table.
3. Minimizes collisions.
4. Always gives the same index for the same key (deterministic).

| Method | Formula / Working | Example (m = 100 unless stated) |
|---|---|---|
| **Division method** (most common) | `h(k) = k mod m`. Choose m as a **prime** not close to a power of 2 | m = 97: h(1234) = 1234 % 97 = **70** |
| **Mid-square method** | Square the key and take the **middle digits** | k = 3205 → k² = 10272025 → middle 2 digits = **72** |
| **Folding method** | Split the key into parts and **add** them (ignore the final carry) | k = 12345678 → 12 + 34 + 56 + 78 = 180 → ignore carry → **80** |
| **Multiplication method** | `h(k) = floor(m × (k × A mod 1))`, with 0 < A < 1 (Knuth suggests A ≈ 0.618) | |
| **Digit extraction** | Use selected digits of the key | |

## 14.3 Collision Resolution Techniques

Two main categories:

```
        Collision Resolution
         /               \
 Open Hashing           Closed Hashing
 (Separate Chaining)    (Open Addressing)
                        /       |        \
                   Linear   Quadratic   Double
                   Probing  Probing     Hashing
```
> Note the confusing names: **open hashing = chaining**, **closed hashing = open addressing**.

**Example used below:** table size m = 10, h(k) = k mod 10. Insert keys **23, 43, 13, 27**.

#### (A) Separate Chaining (Open Hashing)
Each table slot holds a **linked list** of all the keys that hash to that slot.
```
0: NULL
...
3: 23 -> 43 -> 13 -> NULL
...
7: 27 -> NULL
```
- **Advantages:** simple, the table never becomes full, deletion is easy, and α can be greater than 1.
- **Disadvantages:** extra memory for pointers; a long chain makes search slow (worst case O(n)).

#### (B) Open Addressing (Closed Hashing)
All keys are stored **in the table itself**. On a collision, we **probe** (search) for another empty slot. α must be ≤ 1.

**1. Linear Probing:** check the next slots one by one.
> `h(k, i) = (h(k) + i) mod m`, for i = 0, 1, 2, ...

Insert 23, 43, 13, 27:
- 23 → 3
- 43 → 3 is taken → 4
- 13 → 3 taken, 4 taken → 5
- 27 → 7

| Index | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 |
|---|---|---|---|---|---|---|---|---|---|---|
| Key | | | | 23 | 43 | 13 | | 27 | | |

**Problem: Primary clustering.** Occupied slots form long continuous blocks, so searching and inserting become slow.

**2. Quadratic Probing:** jump by squares to spread keys out.
> `h(k, i) = (h(k) + i²) mod m`, for i = 0, 1, 2, ... → checks h, h+1, h+4, h+9, ...

Insert 23, 43, 13: 23 → 3; 43 → 3 taken → 3+1 = 4; 13 → 3 taken → 4 taken → 3+4 = **7**.
- Removes primary clustering, but causes **secondary clustering** (keys with the same hash follow the same probe sequence).
- It may not find an empty slot even when one exists, unless m is prime and α < 0.5.

**3. Double Hashing:** use a **second hash function** to decide the step size.
> `h(k, i) = (h1(k) + i × h2(k)) mod m`, commonly `h2(k) = R − (k mod R)`, where R is a prime < m. h2(k) must never be 0.

- **Best open addressing method.** It removes both primary and secondary clustering.

**Deletion in open addressing:** you can't simply empty the slot, because that would break the probe chain for other keys. Mark it as **"DELETED" (a tombstone)** instead.

**Rehashing:** when the load factor becomes too high (e.g., α > 0.7), create a **bigger table (about double, prime size)** and reinsert all keys using the new hash function.

## 14.4 Chaining vs Open Addressing

| Separate Chaining | Open Addressing |
|---|---|
| Keys stored in linked lists outside the table | Keys stored inside the table |
| Table never gets full | Table can get full |
| α can be > 1 | α ≤ 1 |
| Extra memory for pointers | No pointers |
| Easy deletion | Deletion needs "deleted" markers |
| Less sensitive to the hash function | Suffers from clustering |

**Applications of hashing:** symbol tables in compilers, database indexing, caches, password storage (cryptographic hashes), dictionaries/sets (Python `dict`, Java `HashMap`), spell checkers.

**Complexity:** search/insert/delete are **O(1) on average**, and **O(n) in the worst case** (all keys collide).

> ### Check Yourself — Chapter 14
> 1. **What is hashing?** Computing a storage index from the key itself, for O(1) average access.
> 2. **Properties of a good hash function?** Fast to compute, spreads keys uniformly, and causes few collisions.
> 3. **What is a collision?** Two different keys getting the same index.
> 4. **Collision resolution techniques?** Chaining; open addressing (linear probing, quadratic probing, double hashing).
> 5. **What is primary clustering?** Long runs of filled slots in linear probing.
> 6. **What is the load factor?** α = n/m (keys stored ÷ table size).
> 7. **Why choose a prime table size?** It spreads keys more evenly with the division method.
> 8. **What is rehashing?** Building a bigger table and reinserting all keys when α gets too high.
> 9. **Open hashing vs closed hashing?** Open hashing = chaining (outside the table). Closed hashing = open addressing (inside the table).

---

# Chapter 15 — Heaps & Heap Sort

> **Syllabus:** Module V (heap sort) · **Builds on:** Chapter 8, Chapter 13 (priority queue) · **Why now:** a heap is stored in an array but behaves like a tree. It gives an in-place O(n log n) sort and is the best way to build a priority queue.

## 15.1 Heap Sort (Lab Program 23)

> A heap is a kind of tree. Trees are Module IV, which isn't part of your viva, so this chapter teaches **only the heap knowledge you need for heap sort**.

**What is a heap?** A **complete binary tree** (all levels filled except possibly the last, which is filled left to right) that satisfies the **heap property**:
- **Max-heap:** every parent ≥ its children → the **largest element is at the root**.
- **Min-heap:** every parent ≤ its children → the smallest element is at the root.

**A heap is stored in an array** (no pointers needed). For the node at index `i` (0-based):
- **Left child = 2i + 1**
- **Right child = 2i + 2**
- **Parent = (i − 1) / 2**

```
Array: [90, 15, 10, 7, 12, 2]        Tree view:
index:   0   1   2  3   4  5               90
                                          /   \
                                        15     10
                                       /  \    /
                                      7   12  2
```

**Heap Sort algorithm (ascending, using a max-heap):**
1. **Build a max-heap** from the array (call heapify on every non-leaf node, from index n/2 − 1 down to 0).
2. **Swap the root (the maximum) with the last element.** The largest element is now at its final place.
3. Reduce the heap size by 1 and **heapify the root** again.
4. Repeat steps 2–3 until the heap size is 1.

**Heapify(i):** if a child is larger than node i, swap node i with its **largest child**, then continue heapifying down from that child.

```c
#include <stdio.h>

void swap(int *x, int *y) { int t = *x; *x = *y; *y = t; }

void heapify(int a[], int n, int i) {
    int largest = i, l = 2 * i + 1, r = 2 * i + 2;
    if (l < n && a[l] > a[largest]) largest = l;
    if (r < n && a[r] > a[largest]) largest = r;
    if (largest != i) {
        swap(&a[i], &a[largest]);
        heapify(a, n, largest);            // fix the affected subtree
    }
}

void heapSort(int a[], int n) {
    for (int i = n / 2 - 1; i >= 0; i--)   // 1. build max-heap
        heapify(a, n, i);
    for (int i = n - 1; i > 0; i--) {      // 2. extract max one by one
        swap(&a[0], &a[i]);                //    move current max to the end
        heapify(a, i, 0);                  //    restore heap on the reduced array
    }
}

int main() {
    int a[100], n, i;
    printf("Enter n: "); scanf("%d", &n);
    for (i = 0; i < n; i++) scanf("%d", &a[i]);
    heapSort(a, n);
    printf("Sorted: ");
    for (i = 0; i < n; i++) printf("%d ", a[i]);
    return 0;
}
```
- **O(n log n) in all cases.** Building the heap takes O(n); each of the n extractions takes O(log n).
- **Space O(1)** (in-place). **Not stable.**
- **Advantage:** guaranteed O(n log n) with no extra memory. **Disadvantage:** slower than quick sort in practice (poor cache use).
- A heap is also the best way to implement a **priority queue** (Chapter 13).

> ### Check Yourself — Chapter 15
> 1. **What is a heap?** A complete binary tree in which every parent is ≥ its children (max-heap) or ≤ its children (min-heap).
> 2. **Where is the largest element in a max-heap?** At the root (index 0).
> 3. **Children and parent of index i?** Left child 2i + 1, right child 2i + 2, parent (i − 1)/2 (0-based).
> 4. **Steps of heap sort?** Build a max-heap, swap the root with the last element, shrink the heap, heapify, and repeat.
> 5. **Complexity of heap sort?** O(n log n) in all cases, with O(1) extra space.
> 6. **Is heap sort stable?** No.
> 7. **Why is a heap the best priority queue?** Both insert and delete-max are O(log n).

---

# Chapter 16 — Sorting Wrap-up: Keys, External Sorting & Choosing a Sort

> **Syllabus:** Module V · **Builds on:** all the sorting chapters · **Why last:** real-world sorting means records with several fields and files too big for memory.

## 16.1 Sorting on Different Keys

Real data is usually **records** (structures) with many fields, e.g., a student with `roll`, `name`, `marks`. We can sort these records on **any field**, and that field is called the **key**.
- **Primary key:** the main field to sort on (e.g., marks).
- **Secondary key:** used to break ties when primary keys are equal (e.g., name).

**Method 1 – compare both keys together:**
```c
struct student { int roll; char name[20]; int marks; };

/* sort by marks (descending); if marks are equal, by name (ascending) */
int compare(struct student a, struct student b) {
    if (a.marks != b.marks) return b.marks - a.marks;   // primary key
    return strcmp(a.name, b.name);                      // secondary key
}

void sortStudents(struct student s[], int n) {
    struct student temp;
    for (int i = 0; i < n - 1; i++)                     // bubble sort on records
        for (int j = 0; j < n - 1 - i; j++)
            if (compare(s[j], s[j + 1]) > 0) {
                temp = s[j]; s[j] = s[j + 1]; s[j + 1] = temp;   // swap whole records
            }
}
```
**Method 2 – use a stable sort twice:** first sort by the **secondary** key, then do a **stable** sort by the **primary** key. Records with equal primary keys stay in secondary-key order. (Radix sort uses this idea, sorting digit by digit.)

**Tip:** when records are large, sort an **array of pointers/indices** instead of moving whole records, which saves time.

## 16.2 External Sorting

**External sorting** is used when the **data is too large to fit into main memory (RAM)** and must be kept on **secondary storage (disk/tape)**. Example: sorting a 10 GB file with 1 GB of RAM.

**Most common method: External Merge Sort**
1. **Run creation phase:** read as much data as fits in RAM (e.g., 1 GB), sort it using an internal sort (like quick sort), and write it back to disk as a **sorted run**. Repeat → 10 sorted runs.
2. **Merge phase:** merge the sorted runs together (**k-way merge**). Read a small part of each run into memory, repeatedly output the smallest element, and write the final sorted file.

**Goal:** minimize the number of **disk reads/writes (I/O)**, because disk access is much slower than RAM.
**Variants:** balanced two-way merge, multi-way (k-way) merge, polyphase merge.

| Internal Sorting | External Sorting |
|---|---|
| Data fits in RAM | Data is on disk |
| Speed depends on comparisons | Speed depends on disk I/O |
| Bubble, Quick, Heap... | External merge sort |

## 16.3 Which Sort Should I Use?

| Situation | Best choice | Why |
|---|---|---|
| Very small array, or nearly sorted | **Insertion sort** | O(n) on nearly sorted data, very low overhead |
| General-purpose sorting of arrays | **Quick sort** (random/median pivot) | Fastest on average, in-place |
| Guaranteed O(n log n) and stable | **Merge sort** | Always O(n log n), keeps equal keys in order |
| Guaranteed O(n log n) with no extra memory | **Heap sort** | O(n log n) and O(1) space |
| Writing to memory is expensive | **Selection sort** | At most n − 1 swaps |
| Sorting a linked list | **Merge sort** | Needs no random access |
| Medium-size array, simple code | **Shell sort** | Much faster than insertion sort, still easy |
| Data bigger than RAM | **External merge sort** | Works run by run from disk |
| Sorting records by two keys | Any **stable** sort, used twice | Stability keeps the secondary order |

**The sorting journey you just finished:** simple O(n²) sorts (Chapter 8) → shell sort, a faster insertion sort (Chapter 8) → divide and conquer, O(n log n) (Chapter 10) → heap sort, O(n log n) in-place (Chapter 15) → real-world records and files (this chapter).

> ### Check Yourself — Chapter 16
> 1. **What is sorting on different keys?** Sorting records on a chosen field (key), with a secondary key to break ties.
> 2. **How do you sort by two keys using a stable sort?** Sort by the secondary key first, then stable-sort by the primary key.
> 3. **What is external sorting?** Sorting data too large for RAM, kept on disk.
> 4. **Phases of external merge sort?** Create sorted runs that fit in memory, then do a k-way merge of the runs.
> 5. **What does external sorting try to minimize?** Disk reads and writes (I/O).
> 6. **Which sorting algorithm is the best?** It depends: quick sort on average, merge sort for stability and guarantees, insertion sort for small or nearly sorted data, heap sort for O(1) space.

---

# A. Rapid-Fire Viva Q&A

These are extra and tricky questions examiners like to ask. They are not repeated from the chapter boxes.

**Basics, Pointers, Arrays, Complexity**
1. **Is an array a primitive data structure?** No. It is non-primitive (linear), built from primitive types.
2. **What is the difference between data type and data structure?** A data type says what kind of value a variable holds (int, char). A data structure is an organized collection of data with operations on it.
3. **What is the size of a pointer?** It does not depend on the type it points to. It depends on the system: usually 4 bytes on 32-bit and 8 bytes on 64-bit systems.
4. **What does `a[i]` mean internally?** `*(a + i)`, i.e., the value at the address base + i × size.
5. **Can we change an array's size after declaring it?** Not for static arrays. For dynamic arrays we use `realloc`.
6. **What happens if you access `a[10]` in `int a[10]`?** Undefined behavior. C does no bounds checking.
7. **What is the difference between `char s[]` and `char *s`?** `char s[] = "hi"` is a modifiable array. `char *s = "hi"` points to a string literal that must not be modified.
8. **What is `'\0'`?** The null character (ASCII 0) that ends a string.
9. **Why is `gets()` dangerous?** It doesn't check the buffer size, which can cause a buffer overflow. Use `fgets()`.
10. **Which is better: O(n log n) or O(n²)?** O(n log n). It grows much more slowly.
11. **What is the complexity of accessing an array element?** O(1).
12. **What is the space complexity of a recursive factorial?** O(n), because of the recursion stack.

**Stacks and Queues**
13. **Real-life use of a stack in a computer?** Function call management, undo, back button, compilers (parsing expressions, matching brackets).
14. **How do you check balanced parentheses?** Push every opening bracket. On a closing bracket, pop and check that it matches. At the end, the stack must be empty.
15. **What is a stack overflow in recursion?** Too many nested calls (usually a missing base case) fill up the call stack.
16. **Postfix of `A + B * C`?** `A B C * +`.
17. **Prefix of `A + B * C`?** `+ A * B C`.
18. **Postfix of `(A + B) * (C − D)`?** `A B + C D − *`.
19. **Prefix of `(A + B) * (C − D)`?** `* + A B − C D`.
20. **Evaluate `2 3 4 * +`.** 3 × 4 = 12, 2 + 12 = **14**.
21. **Why is `^` treated differently in conversion?** It is right-associative: `A^B^C = A^(B^C)`.
22. **Initial values of front and rear?** -1 and -1.
23. **How many elements can a circular queue of size N hold with the `(rear+1)%N == front` full check?** N (using the front = -1 empty marker, as in these notes). In the version that starts with front = rear = 0, only N−1 can be used.
24. **What is the difference between a circular queue and a circular linked list?** A circular queue is a queue ADT (FIFO) implemented in a circular way. A circular linked list is a list structure whose last node points to the first.
25. **Which DS is used for CPU scheduling?** A queue (round robin uses a circular queue; priority scheduling uses a priority queue).
26. **Which DS is used for the printer spooler?** A queue.

**Linked Lists**
27. **What is the time to insert at the beginning of a linked list vs an array?** O(1) vs O(n).
28. **What is the time to access the k-th element of a linked list?** O(k), i.e., O(n).
29. **What does `malloc` return if memory isn't available?** NULL.
30. **What is a header node?** An extra dummy node at the start, which can store metadata like the count. It simplifies insertion and deletion at the beginning.
31. **How do you detect a loop in a linked list?** Floyd's cycle detection: a slow pointer (1 step) and a fast pointer (2 steps). If they meet, there is a loop.
32. **How do you find the middle of a linked list in one pass?** Slow and fast pointers. When fast reaches the end, slow is at the middle.
33. **How many pointers change when inserting in the middle of a singly linked list?** Two (`new->next` and `prev->next`).
34. **How do you delete a node in a DLL?** `ptr->prev->next = ptr->next; ptr->next->prev = ptr->prev; free(ptr);` (check for NULL at the ends).
35. **Why is a linked list good for polynomials?** It stores only the non-zero terms, and it is easy to insert new terms.
36. **What do we do with exponents when multiplying polynomials?** Add the exponents and multiply the coefficients.
37. **Which is better for stack implementation: array or linked list?** A linked list, because its size is dynamic and it has no overflow. An array is simpler and slightly faster.

**Searching, Sorting, Hashing**
38. **Which searching is used in a telephone directory/dictionary?** Binary search (or interpolation search), because the data is sorted.
39. **Maximum comparisons in binary search for n = 1024?** log₂1024 + 1 = 11.
40. **Which sorting algorithm is fastest?** No single one is best. Quick sort is usually fastest on average, merge sort guarantees O(n log n) and is stable, and insertion sort is best for small or nearly sorted arrays.
41. **Which sorting algorithm does C's `qsort()` library function use?** Usually a version of quick sort (it depends on the implementation).
42. **Name the divide-and-conquer sorts.** Quick sort and merge sort.
43. **How many passes does bubble sort need for n elements?** At most n − 1.
44. **What is the number of comparisons in selection sort?** Always n(n−1)/2.
45. **Is heap sort stable?** No.
46. **What is the best case of quick sort?** O(n log n), when the pivot divides the array into equal halves.
47. **What is the lower bound for comparison-based sorting?** Ω(n log n).
48. **Can a hash table give O(1) search always?** No. That is the average case. The worst case is O(n) when many keys collide.
49. **What is a perfect hash function?** One that gives no collisions for a given set of keys.
50. **Which collision method needs the table to be at least as big as the number of keys?** Open addressing (α ≤ 1).

**Lab-related (be ready to explain your code)**
51. **Why do you take `top = -1` in a stack program?** -1 means empty, and the first push goes to index 0.
52. **Why do you use `% MAX` in a circular queue?** To wrap the index back to 0 after the last position.
53. **Why do you `free()` a node after deletion?** To return the memory and avoid a memory leak.
54. **Why do you use `struct node *` in a function parameter?** To pass the address of the list so the function can access the nodes.
55. **What happens if you forget `n->next = NULL` when creating a node?** `next` holds a garbage address, and traversal will crash or loop forever.

---

# B. Last-Night Cheat Sheet

### Complexity Table (memorize this)
| Algorithm | Best | Average | Worst | Extra Space | Stable? | In-place? |
|---|---|---|---|---|---|---|
| Linear Search | O(1) | O(n) | O(n) | O(1) | – | – |
| Binary Search | O(1) | O(log n) | O(log n) | O(1) | – | – |
| Bubble Sort | O(n) | O(n²) | O(n²) | O(1) | Yes | Yes |
| Selection Sort | O(n²) | O(n²) | O(n²) | O(1) | No | Yes |
| Insertion Sort | O(n) | O(n²) | O(n²) | O(1) | Yes | Yes |
| Shell Sort | O(n log n) | ~O(n^1.25 to n^1.5) | O(n²) | O(1) | No | Yes |
| Quick Sort | O(n log n) | O(n log n) | O(n²) | O(log n) | No | Yes |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) | Yes | No |
| Heap Sort | O(n log n) | O(n log n) | O(n log n) | O(1) | No | Yes |
| Hash Search | O(1) | O(1) | O(n) | O(n) table | – | – |

### Data Structure Operations
| Structure | Access | Search | Insert | Delete |
|---|---|---|---|---|
| Array | O(1) | O(n) / O(log n) if sorted | O(n) | O(n) |
| Stack | O(n) | O(n) | O(1) push | O(1) pop |
| Queue | O(n) | O(n) | O(1) enqueue | O(1) dequeue |
| Singly Linked List | O(n) | O(n) | O(1) at head | O(1) at head |
| Doubly Linked List | O(n) | O(n) | O(1) at known node | O(1) at known node |
| Hash Table | – | O(1) avg | O(1) avg | O(1) avg |

### Formulas
- **1-D address:** `LOC(A[k]) = Base + w(k − LB)`
- **2-D row-major:** `Base + w[N(i − LB1) + (j − LB2)]` (N = number of columns)
- **2-D column-major:** `Base + w[M(j − LB2) + (i − LB1)]` (M = number of rows)
- **Number of elements:** `UB − LB + 1`
- **Tower of Hanoi moves:** `2ⁿ − 1`
- **Circular queue next index:** `(i + 1) % MAX`; **full:** `(rear + 1) % MAX == front`
- **Heap (0-based):** left `2i+1`, right `2i+2`, parent `(i−1)/2`
- **Bubble/selection comparisons:** `n(n−1)/2`
- **Binary search max comparisons:** `⌊log₂ n⌋ + 1`
- **Load factor:** `α = n / m`
- **Linear probing:** `(h(k) + i) mod m` | **Quadratic:** `(h(k) + i²) mod m` | **Double:** `(h1(k) + i·h2(k)) mod m`

### One-Line Definitions
| Term | Definition |
|---|---|
| Data structure | A way to organize data for efficient access and modification |
| Algorithm | A finite sequence of clear steps to solve a problem |
| Stack | LIFO list, insert/delete at the top |
| Queue | FIFO list, insert at rear, delete at front |
| Circular queue | Queue where the rear wraps to the front to reuse space |
| Priority queue | Removal is based on priority, not arrival order |
| Deque | Insert/delete at both ends |
| Linked list | Nodes connected by pointers |
| Sparse matrix | Matrix with mostly zeros |
| Recursion | A function calling itself, with a base case |
| Hashing | Mapping keys to table indices for O(1) access |
| Collision | Two keys mapping to the same index |
| Stable sort | Keeps the relative order of equal keys |
| Garbage collection | Reclaiming unused memory into the free list |
| Compaction | Moving used blocks together to remove fragmentation |

### Infix → Postfix/Prefix Quick Practice (cover the answers and try)
| Infix | Postfix | Prefix |
|---|---|---|
| `A + B * C` | `A B C * +` | `+ A * B C` |
| `(A + B) * C` | `A B + C *` | `* + A B C` |
| `A * B + C / D` | `A B * C D / +` | `+ * A B / C D` |
| `(A + B) * (C − D)` | `A B + C D − *` | `* + A B − C D` |
| `A + B − C` | `A B + C −` | `− + A B C` |
| `A ^ B ^ C` | `A B C ^ ^` | `^ A ^ B C` |
| `A * (B + C) / D − E` | `A B C + * D / E −` | `− / * A + B C D E` |

---

## Viva Tips
1. **Answer in a structure:** definition → small example → complexity → one application. Example: *"A queue is a linear data structure that follows FIFO. Insertion is at the rear and deletion at the front, like a ticket line. Both operations are O(1). It is used in CPU scheduling."*
2. **Draw if allowed.** A quick sketch of a linked list, a stack, or a circular queue impresses examiners.
3. **Know your lab programs.** Be able to explain overflow/underflow checks, `top = -1`, `% MAX`, `malloc`/`free`, and the order of pointer changes in insertion.
4. **If you don't know, don't bluff.** Say what you do know about the related concept. Examiners give partial credit for honest, related answers.
5. **Most-asked topics:** stack vs queue, infix→postfix conversion, circular queue, array vs linked list, linked list insertion/deletion, binary search, quick sort vs merge sort, stable sorting, hashing and collisions, time complexity.

**All the best for Monday! 🎯**
