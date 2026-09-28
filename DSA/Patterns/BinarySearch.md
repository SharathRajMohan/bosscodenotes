# Binary Search: Recall Notes (Week 3, Sat)
 
## Trigger phrases
"Sorted array," "O(log n)," "find first/last occurrence," "smallest value that is at least X," "where would this be inserted." More generally, any search space where you can tell, from one probe at the middle, that the answer is definitely to the left or definitely to the right.
 
## Core idea
Check the middle, throw away the half that can't contain the answer, repeat. Each step halves the search space, so O(n) becomes O(log n). Space is O(1) in the iterative version.
 
## The textbook template (#704)
```python
def search(nums, target):
    left, right = 0, len(nums) - 1
    while left <= right:
        mid = (left + right) // 2
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```
 
## The off-by-one rules (why each detail is what it is)
- **`left <= right`, not `left < right`:** `left == right` means exactly one candidate is still unchecked. With `<` you would skip it and wrongly return -1 on inputs like `[1]`, target `1`. Read `left <= right` as "the search space still contains at least one element."
- **`left = mid + 1` and `right = mid - 1`, not `mid`:** you have already checked `mid` and ruled it out. Setting `left = mid` can leave the range unchanged (for example `left=0, right=1` gives `mid=0` forever), which is an infinite loop.
- **`right = len(nums) - 1`:** both ends are inclusive indices, so the last valid index is `len - 1`. This pairs with `left <= right`.
- **Interview footnote:** `(left + right) // 2` is safe in Python because integers do not overflow. In Java or C++ write `left + (right - left) // 2`.
## The big upgrade: a match is not always the end (#34)
For variants beyond the textbook case, a match records a **candidate** and keeps narrowing toward the side you care about.
 
- **First occurrence:** on a match, set `first = mid` and go **left** with `right = mid - 1`.
- **Last occurrence:** on a match, set `last = mid` and go **right** with `left = mid + 1`.
- A later iteration overwrites the candidate if a better one exists. If none exists, the candidate is already correct.
```python
def searchRange(nums, target):
    left, right = 0, len(nums) - 1
    first = -1
    while left <= right:
        mid = (left + right) // 2
        if nums[mid] == target:
            first = mid
            right = mid - 1          # keep looking left
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    if first == -1:                   # guard: target absent
        return [-1, -1]
    last = -1
    left, right = first, len(nums) - 1
    while left <= right:
        mid = (left + right) // 2
        if nums[mid] == target:
            last = mid
            left = mid + 1           # keep looking right
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return [first, last]
```
The two passes differ by one line. If you want to avoid the duplicated loop, write one helper with a flag for "search left" vs "search right".
 
## Why not "find any match, then walk outward"?
It works, but with a million copies of the target the walk is O(n), which breaks the O(log n) requirement. Let binary search find the edge directly.
 
## Traps to remember
- **Negative-index wraparound:** `nums[-1]` does not raise an error in Python, it silently reads the last element. Guard any `nums[mid - 1]` access with `mid > 0`, and never start a search with `left = -1`. This is the same bounds-check-first habit as 3Sum.
- **Empty array and absent target:** if the first pass finds nothing, return early. Otherwise the second pass starts from `first = -1` and can index `nums[-1]` or crash on an empty list.
- **Values are contiguous, positions are not adjacent:** all copies of the target form one block, but first and last are only next to each other when there are exactly two copies. You want the left edge and the right edge of that block.
## Bonus insight: what `left` means when the target is missing
When the loop ends without a match, `left` sits at the index where the target would have to be inserted to keep the array sorted. That is the basis of "search insert position" and "smallest value that is at least X" problems.
 
## Habits reinforced
- Trace the loop by hand with `left`, `right` and `mid` written out at every step, especially for the not-found case.
- Test edge cases before running: empty array, single element, target absent, target at either end, many duplicates.
 