# Sliding Window — Recall Notes (Week 2, Mon–Tue)

## Trigger phrases
"Longest/shortest/max **substring** or **subarray**," "contiguous," "no repeating characters within a range," "at most K distinct." The sharpest test: *does this problem care about a contiguous range, or just about finding elements anywhere?* Contiguous range → sliding window. Anywhere in the structure → hashmap or two-pointer.

## The two flavors

### 1. Fixed-size window (width `k` never changes)
- Compute the state of the **first** window directly (one real computation).
- Slide one step at a time: **remove the outgoing element** (`nums[i-k]` / `s[left]`), **add the incoming element** (`nums[i]` / `s[right]`) — always exactly one in, one out, in lockstep.
- Skeleton:
```python
state = <compute from first k elements>
best = <init from state>
for i in range(k, len(nums)):
    state = update(state, remove=nums[i-k], add=nums[i])
    best = compare(best, state)
```
- Loop bound gotcha: make sure the **last** valid window (where the right edge reaches exactly `len(nums)`) isn't cut off — `right <= len(nums)` vs `right < len(nums)` is an easy off-by-one.

### 2. Variable-size window (width grows/shrinks based on validity)
- `right` advances every step, **unconditionally**. `left` only advances **when the window becomes invalid** — and may need to advance **multiple times in a row** (hence a `while`, not an `if`, for shrinking — same reasoning as the palindrome skip-loops).
- Skeleton:
```python
left = 0
state = <empty>
best = 0
for right in range(len(s)):
    <add s[right] into state>
    while <window is invalid>:
        <remove s[left] from state>
        left += 1
    best = update(best, right - left + 1)
```
- **Efficiency trick:** since the window was valid *before* adding `s[right]`, the only thing that could have broken it is `s[right]` itself. So the invalidity check only needs to look at **that one entry's count** (`state[s[right]] > 1`), not scan the whole state every step.

## Choosing the window's "state" tool
- **Running sum** — when the property is additive (max average, max sum).
- **`Counter` (not a plain `set`!)** — when you need to track "how many of X are currently in the window," because you'll need to **partially remove** elements as the window shrinks/slides. A `set` only knows "present or not" — it can't tell you a duplicate is still in the window after one copy leaves, and iterating+deleting from a live dict/Counter mid-loop throws `RuntimeError` unless you snapshot the keys first (`for k in list(d.keys())`).
- `Counter` behaves like a dict but defaults missing keys to `0` — `c[x] += 1` never raises `KeyError`, even on a brand-new key.

## Key distinctions from other patterns
| Pattern | Shape |
|---|---|
| Hashmap/Set | One global pass, no window — "have I seen this anywhere?" |
| Two Pointers | Two pointers move independently (often converging), usually over sorted data or comparing two full sequences — not about a contiguous range. |
| Sliding Window | One window `[left, right]`, `right` leads, `left` trails to keep the window valid — always about a **contiguous** stretch. |

**Overlap to remember:** sliding window is the *shape of the loop*; hashmap/Counter is often the *tool* tracking what's inside the window. "Sliding window vs. hashmap" is usually a false choice — many problems are both at once.