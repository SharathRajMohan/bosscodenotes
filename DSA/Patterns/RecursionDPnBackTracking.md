# Recursion, Backtracking & DP — Recall Notes (Week 3, Mon–Wed)

## Recursion — the basics
**Trigger phrases:** "generate all X," "how many ways," self-similar structure ("problem on n depends on problem on n-1").

Every recursive function needs:
- **Base case** — smallest version of the problem, answered directly, no further calls.
- **Recursive case** — reduce to a smaller version of the *same* problem, combine its result.

**The recursive leap of faith:** don't trace the whole call stack in your head. Trust that "if I already had the correct answer to the smaller subproblem, here's how I'd use it" — reason about one layer at a time.

**Common bug:** accidentally using `if/elif` where the recurrence actually needs **both** branches summed (e.g. `ways(n) = ways(n-1) + ways(n-2)` needs both calls added, not a choice between them — an `if/elif` silently throws one branch away).

---

## Recursion + Memoization (Top-Down DP)
**Direction:** starts at the big problem (`n`), recurses **down** toward the base case — same call direction as plain recursion, just with a cache added so repeated subproblems aren't recomputed.

**Why plain recursion can be exponential:** overlapping subproblems get recomputed from scratch every time they're needed (e.g. naive Fibonacci recomputes `fib(2)` many times over) — O(2ⁿ).

**Template:**
```python
def solve(n, memo):
    if n in memo:
        return memo[n]
    if <base case>:
        return <base value>
    result = <combine solve(smaller_n, memo) calls>
    memo[n] = result
    return result
```
- Pass `memo` explicitly as a parameter (a dict) through every recursive call — don't use a mutable default argument (`def f(n, memo={})`), it persists incorrectly across separate top-level calls.
- Check the cache **first**, before doing any other work.
- Store into the cache **right before returning**, so every computed value benefits future calls.
- Collapses O(2ⁿ) → O(n): each unique subproblem computed exactly once.

---

## Bottom-Up DP (Iterative)
**Direction:** starts **at** the base case(s), builds **upward** to `n` in a simple loop — no recursion, no call stack at all.

**Template (when only the previous 1-2 values are needed):**
```python
prev2 = <base value for n=0>
prev1 = <base value for n=1>
for i in range(2, n+1):
    current = <same recurrence as the top-down version, using prev1/prev2>
    prev2 = prev1
    prev1 = current
return prev1
```
- Same recurrence relation as top-down — just computed left-to-right instead of top-down.
- Often more space-efficient: two running variables instead of an O(n) memo dict/array, when only the last couple of values are ever needed.
- Generally preferred once the recursive structure is understood — avoids recursion overhead, easier to reason about for space optimization.

**Recognizing the same recurrence in disguise:** Climbing Stairs (`ways(n) = ways(n-1) + ways(n-2)`) is structurally identical to Fibonacci, just different base-case labels. House Robber uses the same *shape* (`best(i)` depends on `i-1` and `i-2`) but a different combining rule: `best(i) = max(nums[i] + best(i-2), best(i-1))` — "rob it" vs. "skip it," not addition.

**Three DP variants at a glance:**
| Variant | Direction | Recursion? |
|---|---|---|
| Plain recursion | top-down | yes, no caching |
| Recursion + memoization | top-down | yes, with caching |
| Bottom-up | starts at base case, builds up | no |

---

## Backtracking
A flavor of recursion used to **explore all possible choices**: make a choice → recurse to explore everything downstream of it → **undo** the choice before trying the next alternative, so exploration always returns to a clean slate.

**Template:**
```python
def backtrack(state):
    if <base case>:
        record a COPY of the current state (not a reference!)
        return
    for <each choice available>:
        make the choice (mutate state)
        backtrack(next state)
        undo the choice (mutate state back)
```

**Key mechanics (from Subsets):**
- One **shared, mutated** list (`current`) is reused throughout the whole recursion — it grows and shrinks like a stack as you go deeper and come back up.
- `.append()` before recursing = make the choice. `.pop()` right after the recursive call returns = undo it, so the sibling branch starts clean.
- **Snapshot on save:** when recording a result, append a **copy** (`current[:]` or `list(current)`), never `current` itself — otherwise later mutations to the shared list retroactively corrupt already-saved results.
- No duplicate-checking needed when every choice sequence is inherently distinct (e.g. include/exclude for each element) — different choice paths can never produce the same output.
- Choice count multiplies at each level: `2` choices × `2` choices × `2` choices = `2ⁿ` total outcomes for n binary decisions (Subsets). A `for` loop over multiple choices (rather than a fixed include/exclude pair) generalizes this to permutations, combinations, etc.