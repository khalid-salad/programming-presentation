## Correctness
* Code needs to be correct <!-- .element class="fragment" -->
* If code is incorrect, then it doesn't matter <!-- .element class="fragment" -->
  * how performant it is <!-- .element class="fragment" -->
  * how readable it is <!-- .element class="fragment" -->
----
For example 
```python
def bool_sat(formula):
    return True
```
<!-- .element class="fragment" -->
* $\mathcal{O}(1)$ solution to an NP-Complete problem <!-- .element class="fragment" -->
* but, obviously not a correct solution <!-- .element class="fragment" -->
----
* What is considered "correct" is context dependent, e.g. software that
  * controls a commercial plane <!-- .element class="fragment" -->
    * must be provably (mathematically) correct <!-- .element class="fragment" -->
  * launches League of Legends <!-- .element class="fragment" -->
    * 80% test coverage may be sufficient <!-- .element class="fragment" --> 
----
* You should always test your code
* This is the easiest way to catch bugs! <!-- .element class="fragment" -->
* For example <!-- .element class="fragment" -->
```python
def is_prime(n):
    if n in {0, 1}:
        return False
    else:
        for i in range(2, int(n ** 0.5)):
            if n % i == 0:
                return False
        return True
```
<!-- .element class="fragment" -->
* What is wrong with this code? <!-- .element class="fragment" -->
* May not be immediately obvious <!-- .element class="fragment" -->
  * So let's test it <!-- .element class="fragment" -->

```python
for i in range(2, 11):
    print(i, is_prime(i))
```
<!-- .element class="fragment" -->
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
|------|---------------|----------|
| $2$  | `True`        | ✓        |
| $3$  | `True`        | ✓        |
| $4$  | `True`        | ✗        |
| $5$  | `True`        | ✓        |
| $6$  | `True`        | ✗        |
| $7$  | `True`        | ✓        |
| $8$  | `True`        | ✗        |
| $9$  | `True`        | ✗        |
| $10$ | `False`       | ✓        |
</div><!-- .element class="fragment" -->


<div class="col", style="font-size:25px">

* Incorrect for composite values $4$, $6$, $8$, and $9$ <!-- .element class="fragment" -->
* For these values $\lfloor\sqrt{n}\rfloor = 2$ <!-- .element class="fragment" -->
* Off-by-one error — add 1 to the range: <!-- .element class="fragment" -->
  * `int(n ** 0.5) + 1`
</div>
</div>