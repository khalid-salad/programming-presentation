---
title: Programming Tips
theme: moon
---
# Programming Tips
---
## Table of Contents
<style>
.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container">

<div class="col">

* Introduction <!-- .element class="fragment" -->
  * Correctness <!-- .element class="fragment" -->
  * Readability <!-- .element class="fragment" -->
  * Performance <!-- .element class="fragment" -->
</div>

<div class="col">

* Problem Solving <!-- .element class="fragment" -->
  * Subroutines <!-- .element class="fragment" -->
  * Debugging <!-- .element class="fragment" -->
  * Example <!-- .element class="fragment" -->
</div>
---

## Introduction
### Things to Consider <!-- .element class="fragment" -->
Good code depends on <!-- .element class="fragment" -->
* Correctness <!-- .element class="fragment" -->
* Readability <!-- .element class="fragment" -->
* Performance <!-- .element class="fragment" -->
---
## Correctness
* Code needs to be correct <!-- .element class="fragment" -->
* If code is incorrect, then it doesn't matter <!-- .element class="fragment" -->
  * how performant it is <!-- .element class="fragment" -->
  * how readable it is <!-- .element class="fragment" -->
----

### For example 
```python
def bool_sat(formula):
    return True
```
<!-- .element class="fragment" -->
* $\mathcal{O}(1)$ solution to an NP-Complete problem <!-- .element class="fragment" -->
* but, obviously not a correct solution <!-- .element class="fragment" -->
----

## What does "correct" mean?
* Depends on context, e.g. consider software that <!-- .element class="fragment" -->
  * controls a commercial plane <!-- .element class="fragment" -->
    * must be provably (mathematically) correct <!-- .element class="fragment" -->
  * launches League of Legends <!-- .element class="fragment" -->
    * 80% test coverage is sufficient <!-- .element class="fragment" --> 
----
<style>
.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

### Testing
<div class="container">

<div class="col">

* You should always test your code <!-- .element class="fragment" -->
* This is the easiest way to catch bugs! <!-- .element class="fragment" -->
* For example <!-- .element class="fragment" -->

```python
def is_prime(n):
  if n in {0, 1}:
    return False
  else:
    sqrtn = int(n ** 0.5)
    for i in range(2, sqrtn):
      if n % i == 0:
        return False
    return True
```
<!-- .element class="fragment" -->
</div>

<div class="col">

* What is wrong with this code? <!-- .element class="fragment" -->
* May not be immediately obvious <!-- .element class="fragment" -->
  * So let's test it <!-- .element class="fragment" -->

```python
for i in range(2, 11):
  print(i, is_prime(i))
```
<!-- .element class="fragment" -->
</div>
----
<style>
.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container">

<div class="col">

| $i$  | `is_prime(i)` | Correct? |
| ---- | ------------- | -------- |
| $2$  | `True`        | ✓        |
| $3$  | `True`        | ✓        |
| $4$  | `True`        | ✗        |
| $5$  | `True`        | ✓        |
| $6$  | `True`        | ✗        |
| $7$  | `True`        | ✓        |
| $8$  | `True`        | ✗        |
| $9$  | `True`        | ✗        |
| $10$ | `False`       | ✓        |
</div>


<div class="col", style="font-size:25px">

* Incorrect for composite values $4$, $6$, $8$, and $9$ <!-- .element class="fragment" -->
* For these values $\lfloor\sqrt{n}\rfloor = 2$ <!-- .element class="fragment" -->
* Off-by-one error — add 1 to the range: <!-- .element class="fragment" -->
  * `int(n ** 0.5) + 1`
</div>
</div>
----

## Edge Cases
* <!-- .element class="fragment" --> Be sure to test for <font color="red">edge cases</font> 
  * boundary or degenerate cases <!-- .element class="fragment" -->
    * <!-- .element class="fragment" --> sorting an <font color="red">empty list</font> 
    * <!-- .element class="fragment" --> binary search returning <font color="red">first</font> or <font color="red">last</font> index 
    * <!-- .element class="fragment" --> checking if 0 or 1 is <font color="red">prime</font>
    * <!-- .element class="fragment" --> traversing a graph with <font color="red">no edges</font>
* <!-- .element class="fragment" --> Depending on the context, you may also need to test for <font color=red>invalid inputs</font>
---
## Readability
* <!-- .element class="fragment" --> Usually the most important thing after correctness 
* <!-- .element class="fragment" --> Code will be <font color="red">read</font> far more often than it is <font color="red">written</font>
* <!-- .element class="fragment" --> <font color=red>Maintenance</font> of code is often the highest expense
----
## Syntax
* <!-- .element class="fragment" --> Follow a set of best-practices for your language. For example
  * <!-- .element class="fragment" --> In Python, there is PEP 8
  * <!-- .element class="fragment" --> IN C, there is the Linux Kernel Style
* <!-- .element class="fragment" --> The style chosen is less important than that you <font color=red>follow a consistent style</font>
----
## For Example
<div class="container">

<div class="col">

<fieldset style="border: 2px groove">
      <legend style="border: 2px groove;margin-left: 3em; padding:10px "><font color=white>ugly</font></legend>

```python[]
c=(a+b)**0.5
L=[1,2,7]
```

</div>


</fieldset>


<div class="col">

<fieldset style="border: 2px groove">
      <legend style="border: 2px groove;margin-left: 3em; padding:10px "><font color=white>readable</font></legend>

```python[]
c = (a + b) ** 0.5
L = [1, 2, 7]
```

</div>

</fieldset>

</div>

* <!-- .element class="fragment" --> The easiest way to be consistent is to use a formatter
  * <!-- .element class="fragment" --> A formatter automatically formats your code
    * Black, yapf, autopep, etc. for Python
    * clang-format for C/C++


Note: notice that, while the _semantics_ of both sets of code are the same, the code on the left is
more cluttered and difficult to read.
----
## Structure
* <!-- .element class="fragment" --> Syntactic readability (style) is not enough
* <!-- .element class="fragment" --> Code should be written for readability
* <!-- .element class="fragment" --> <font color=red>Modular</font> and <font color=red>structured</font> code is easier to
  * <!-- .element class="fragment" --> read
  * <!-- .element class="fragment" --> write
  * <!-- .element class="fragment" --> debug
----
## Example Problem
* Consider the following problem
<fieldset style="border: 2px groove; padding:10px">
      <legend style="border: 2px groove;margin-left: -3em; padding:10px "><font color=white>Problem</font></legend>
Find the largest product of two $3$-digit numbers that is a palindrome. 
</fieldset> <!-- .element class="fragment" -->

<!-- .element class="fragment" -->
<fieldset style="border: 2px groove; padding:10px">
      <legend style="border: 2px groove;margin-left: -3em; padding:10px "><font color=white>Brute Force Solution</font></legend>
Iterate through all $10^6$ pairs of products and check if they are palindromic while keeping track of max.
</fieldset>

<!-- .element class="fragment" -->
----
## Bad Structure

<div class="container">

<div class="col">

```python[|1|2|3-8|9-10|1]
for a, b in pairs:
  prod = a * b
  is_palindrome = True
  n = len(str(prod))
  for i in range(n):
    if s[i] != s[n - i - 1]:
      is_palindrome = False
      break
  if not is_palindrome:
    continue
  else:
    if prod > biggest:
      biggest = prod
```

</div>

<div class="col">

* <!-- .element class="fragment" --> Code is hard to follow
* <!-- .element class="fragment" --> Unnecessarily complex — <code>is_palindrome</code> is essentially a sentinel value
* <!-- .element class="fragment" --> code is <font color=red>imperative</font>, not <font color=red>declarative</font>

</div>

</div>
----

## Better Structure
<div class="container">

<div class="col">

```python
def is_palindrome(num):
  n = len(str(num))
  for i in range(n):
    if s[i] != s[n - i - 1]:
      return False
  return True

biggest = 0
for a, b in pairs:
  prod = a * b
  if is_palindrome(prod):
    biggest = max(biggest, prod)
```

</div>

<div class="col">

* <!-- .element class="fragment" --> Code is much easier to follow
* <!-- .element class="fragment" --> Function <code>is_palindrome</code> clearly conveys intent
* <!-- .element class="fragment" --> code is <font color=red>declarative</font>

</div>

</div>
----

## Good Structure

```python
def is_palindrome(num):
  n = len(str(num))
  for i in range(n):
    if s[i] != s[n - i - 1]:
      return False
  return True

def main():
  biggest = 0
  for a, b in product(range(100, 1000), repeat=2):
    prod = a * b
    if is_palindrome(prod):
      biggest = max(biggest, prod)
  print(biggest)
```

* <!-- .element class="fragment" --> Basically the same code
* <!-- .element class="fragment" --> <code>main</code> describes what the code is doing <font color=red>overall</font>

----

## Comments
* <!-- .element class="fragment" --> Code should be commented
* <!-- .element class="fragment" --> but not <font color=red>over commented</font>

<fieldset style="border: 2px groove">
      <legend style="border: 2px groove;margin-left: -4em; padding:10px "><font color=white>Bad Comment</font></legend>

```python[]
def i_sqrt(n):
  i = 0
  while i ** 2 < n:
    i += 1  # increment i
  return i
```

</fieldset>

<!-- .element class="fragment" --> 

* <!-- .element class="fragment" --> it is clear that <code>i += 1</code> increments <code>i</code>
* <!-- .element class="fragment" --> comment is superfluous and <font color=red>distracting</font>

----
## Good Comments
* <!-- .element class="fragment" --> As a rule of thumb
  * <!-- .element class="fragment" --> good <font color=red>code</font> describes <font color=red>what</font> and <font color=red>how</font>
  * <!-- .element class="fragment" --> good <font color=red>comments</font> describe <font color=red>why</font>
----
## Good Comment Example

<fieldset style="border: 1px groove">
      <legend style="border: 1px groove;margin-left: -4em; padding:3px "><font color=white>Good Comment</font></legend>

```python[|3]
def is_prime(n):
  ...
  # we need only check for odd factors up to sqrt(n)
  for i in range(3, int(n ** 0.5) + 1), 2):
    if n % i == 0:
      return False
  return True
```

</fieldset>

<!-- .element class="fragment" fragment-id=1--> 


* <!-- .element class="fragment" fragment-id=2--> this comment explains why the code is iterating through $3$, $5$, $\dots$, $\lfloor\sqrt{n}\rfloor$
* <!-- .element class="fragment" --> without this comment, the reader would have to determine for themself why it only checks odd numbers up to $\lfloor\sqrt{n}\rfloor$

----
## Good Code
* <!-- .element class="fragment" --> If your code is well-written, it will improve readability
* <!-- .element class="fragment" --> Not just in terms of structure, but things like variable and function names
----
## Good Code
* <!-- .element class="fragment" --> Well-written code often makes many comments <font color=red>unecessary</font>
* <!-- .element class="fragment" --> Often expressed as
> Good Code is its Own Best Documentation
<!-- .element class="fragment" -->
* <!-- .element class="fragment" --> Not an excuse to avoid comments

----
## Bad Naming
```python[|6|]
def qs(a):
  if len(a) <= 1:
    return a
  else:
    x, z, y = [], [], a[0]
    for p in a:
      if p < y:
        x.append(p)
      else:
        z.append(p)
    return qs(x) + qs(z)
```
<!-- .element class="fragment" -->
* <!-- .element class="fragment" --> These names convey almost <font color=red>nothing</font> about the meaning of the code

----
## Good Naming
```python[|6|]
def quicksort(array):
  if len(array) <= 1:
    return array
  else:
    left, right, pivot = [], [], array[0]
    for ele in array:
      if ele < pivot:
        left.append(ele)
      else:
        right.append(ele)
    return quicksort(left) + quicksort(right)
```
<!-- .element class="fragment" -->

* <!-- .element class="fragment" --> These names convey
  * <!-- .element class="fragment" --> function is quicksort
  * <!-- .element class="fragment" --> input is an array
  * <!-- .element class="fragment" --> left and right are partitions around pivot = array[0]
  * <!-- .element class="fragment" --> ele iterates through values of array

----
## Side by Side

<div class="container">


<div class="col">


```python
def qs(a):
  if len(a) <= 1:
    return a
  else:
    x, z, y = [], [], a[0]
    for p in a:
      if p < y:
        x.append(p)
      else:
        z.append(p)
    return qs(x) + qs(z)
```

</div>


<div class="col">


```python
def quicksort(array):
  if len(array) <= 1:
    return array
  else:
    left, right, pivot = [], [], array[0]
    for ele in array:
      if ele < pivot:
        left.append(ele)
      else:
        right.append(ele)
    return quicksort(left) + quicksort(right)
```

</div>

</div>

----
## Miscellaneous
* <!-- .element class="fragment" --> Impractical to create exhaustive list of best practices
  * <!-- .element class="fragment" --> and some practices are debateable
* <!-- .element class="fragment" --> Good idea to look at resources like
  * <!-- .element class="fragment" --> The Little Book of Python Anti-Patterns
  * <!-- .element class="fragment" --> The C++ Core Guidelines
* <!-- .element class="fragment" --> And to use a <font color=red>linter</font> — a static analysis tool to flag bugs, style errors, etc., like
  * <!-- .element class="fragment" --> flake8 for Python
  * <!-- .element class="fragment" --> clang-tidy for C++

---
## Performance
* <!-- .element class="fragment" --> Highly case-by-case
  * <!-- .element class="fragment" --> specific use case may allow for less performant code
    * <!-- .element class="fragment" --> e.g. a one-time scientific calculation
  * <!-- .element class="fragment" --> or may require more performant code
    * <!-- .element class="fragment" --> e.g. real-time financial analysis

----

## Performance
* <!-- .element class="fragment" --> Usually comes down to correct choice of algorithm and data structure
  * <!-- .element class="fragment" --> e.g. if checking existence of an element, an array gives $\mathcal{O}(n)$ but a hash table gives $\mathcal{O}(1)$
    * <!-- .element class="fragment" --> which might make the difference between $\mathcal{O}(n^2)$ and $\mathcal{O}(n)$ overall
* <!-- .element class="fragment" --> While it does depend on use case, it is <font color=red>usually</font> still best to focus on readability over performance
  * <!-- .element class="fragment" --> it is easier to make slow code fast than to make confusing code understandable

---
## Problem Solving

---

## Subroutines
* <!-- .element class="fragment" --> Break up your code into smaller functions
  * <!-- .element class="fragment" --> easier to code small, individual parts
  * <!-- .element class="fragment" --> easier to make changes and diagnose bugs
* <!-- .element class="fragment" --> Any task that is <font color=red>repeated</font> should go in a subroutine

----

## Debugging
* <!-- .element class="fragment" --> Use a debugger when encountering issues
  * <!-- .element class="fragment" --> will allow you to proceed through a program step-by-step
  * <!-- .element class="fragment" --> will help catch a variety of (but not all) bugs

----

## Example Problem

<fieldset style="border: 2px groove; padding:10px">
      <legend style="border: 2px groove;margin-left: -3em; padding:10px "><font color=white>Problem</font></legend>
Given an array of integers $\texttt{nums}$ and a positive integer $k$, find whether it is possible to divide $\texttt{nums}$ into sets of $k$ consecutive
numbers. 
</fieldset> <!-- .element class="fragment" -->

----

## Where to Start
* <!-- .element class="fragment" --> Look at examples
  1) <!-- .element class="fragment" --> $\texttt{nums} = [1, 2, 3, 3, 4, 4, 5, 6]$, $k = 4$
     * <!-- .element class="fragment" --> Solution: $[1, 2, 3, 4], [3, 4, 5, 6]$
  2) <!-- .element class="fragment" --> $\texttt{nums} = [3, 2, 1, 2, 3, 4, 3, 4, 5, 9, 10, 11]$, $k = 3$
     * <!-- .element class="fragment" --> Solution: $[1, 2, 3], [2, 3, 4], [3, 4, 5], [9, 10, 11]$

----

## Where to Start
* <!-- .element class="fragment" --> Hopefully notice a pattern:
  * <!-- .element class="fragment" --> if $x = \min(A)$, then $x, x + 1, \dots, x + k - 1$ form a subarray
  * <!-- .element class="fragment" --> naturally lends itself to a recursive solution
    * <!-- .element class="fragment" --> remove $x, x + 1, \dots, x + k - 1$, then repeat
    * <!-- .element class="fragment" --> if run out of elements before removing all $k$, then no solution 

----

## Writing a solution
* <!-- .element class="fragment" --> Two observations
  1) <!-- .element class="fragment" --> we are removing the $k$ smallest elements
  2) <!-- .element class="fragment" --> if we know some element $x$, we know the next element is $x + 1$
* <!-- .element class="fragment" --> 1. suggests the use of a heap
* <!-- .element class="fragment" --> 2. suggests the use of a dictionary (associative array)
* <!-- .element class="fragment" --> both solutions are valid

----

## Heap Solution
* <!-- .element class="fragment" --> Heap <code>pop</code> removes the smallest element
* <!-- .element class="fragment" --> Need to account for removing the $k$ smallest <font color=red>distinct</font> elements
* <!-- .element class="fragment" --> Thus, set up <code>(value, count)</code> pairs

----

## Heap Solution
* <!-- .element class="fragment" --> Then <code>pop</code>, say smallest value is $(x, c)$
  * <!-- .element class="fragment" --> effectively removing $c$ copies of $x$
  * <!-- .element class="fragment" --> then, remove $c$ copies of $x + 1, \dots, x + k - 1$, if possible
    * <!-- .element class="fragment" --> if not possible, return <code>False</code>
  * <!-- .element class="fragment" --> after popping, need to return remaining elements to heap
  * <!-- .element class="fragment" --> keep track of remaining elements in array

----

## Python Implementation

```python
popped = []  # store popped heap values
prev, min_count = heappop(heap)
for i in range(k - 1):
  if not heap:  # ran out of elements
    return False
  else:
      value, count = heappop(heap)
      if value != prev + 1:  # not consecutive
        return False
      else:
        count -= min_count
        prev = value
        if count > 0:
          popped.append((value, count))
for val in popped:
    heappush(heap, val)
```

----

## Dictionary Solution
* <!-- .element class="fragment" --> Dictionary holds the count for each element
* <!-- .element class="fragment" --> if $x$ is the minimum and $D[x] = \texttt{count}$
  * <!-- .element class="fragment" --> must have $D[x + i] \geq \texttt{count}$ for $i \in [1, 2, \dots, k - 1]$
  * <!-- .element class="fragment" --> i.e., must have $D[x + 1] \geq \texttt{count}$, $D[x + 2] \geq \texttt{count}$, and so on
  * <!-- .element class="fragment" --> else return <code>False</code>
* <!-- .element class="fragment" --> Decrease $D[x + i]$ by $\texttt{count}$
* <!-- .element class="fragment" --> Remove entry if it becomes 0

----

## Python Implementation

```python
while counts:  # dictionary to store counts
  x = min(counts)
  min_count = counts[x]
  del counts[x]  # remove smallest
  for i in range(1, k):
      if counts[x + i] < min_count:
        return False
      else:
        counts[x + i] -= min_count
        if counts[x + i] == 0:
          del counts[x + i]
```

---

# Thank you!