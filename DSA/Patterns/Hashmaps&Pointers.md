# Week 1 Recall Notes — Hashmap/Set & Two Pointers

## Hashmap / Set

**Trigger phrases:** "count occurrences," "find duplicates," "check membership," "have I seen this before?"

**Core rule of thumb:**
- Hashmap (dict) → when you need an **association** (key → value), e.g. value → index (Two Sum), char → count.
- Set → when you only need **membership**, no associated value (Contains Duplicate).
- `Counter` → standard-library shorthand for counting; totally fine to use in interviews.

**The one rule that prevents self-matches:** *check before you insert.* Look up the complement/value in the map first — only after confirming it's not (yet) a false match do you add the current element in.

**Consume-from-map pattern:** when a problem needs you to "use up" a count once matched (Valid Anagram, Intersection of Two Arrays II), decrement on match rather than just checking existence — otherwise you allow more matches than the actual shared count permits.

**Bugs caught this week:**
- Off-by-one in "pop when count reaches X" — decrementing to `0` means "fully used," not `1`.
- Trust the loop over manual special-casing — `range(len(x))` already handles empty/length-1 inputs correctly; extra `if` branches for those cases are often dead code.

---

## Two Pointers

Three distinct shapes seen this week — naming which one applies is the fast way to unblock the freeze:

**1. Converging (both ends → middle)** — *Valid Palindrome*
- `left=0`, `right=len-1`, move inward, stop when `left >= right`.
- Inner `while` loops (not `if`) needed when a pointer might need to skip *multiple* invalid characters in a row. Always guard inner skip-loops with `left < right` so one side can't skip past the other or go out of bounds.
- Bounds-check must come **before** the index-access check in a combined condition (`left < right and nums[left] == nums[left+1]`) — Python's short-circuit `and` only protects you if the safe check is first.

**2. Same-direction, different speeds, no write-back** — *Is Subsequence*
- One pointer (`t`) always advances; the other (`s`) advances only on a match.
- Both pointers need their own bounds check in the loop condition — not just the "outer" one — or you risk indexing past the shorter sequence once it's fully matched.

**3. Read/write, same-direction, overwriting a prefix** — *Remove Duplicates, Move Zeroes*
- `write` = index of the last confirmed "kept" value (a prefix marker, not literally "the end").
- `read` scans forward unconditionally; `write` only advances (and gets written to) when `read` finds something that should be kept.
- "In place" often means *overwrite a prefix + return a length*, not literally shrink the array.
- Some variants need a **second pass** after the main loop to finish the job (e.g. padding zeros in Move Zeroes) — moving values forward doesn't automatically clean up the leftover tail.

**Sorted-array bonus (3Sum):**
- Sorting + fixed outer index `i` + converging two-pointer on the remainder = classic "reduce N-sum to two-pointer" trick.
- When the sum is off-target, move **only one** pointer (the one that fixes the direction) — not both unconditionally.
- Dedupe at **three** levels: outer `i` (skip if same as previous, guard `i != 0` first), and both `left`/`right` after a match (skip forward/backward past repeats before making the final `left+=1, right-=1` move).

---

## General habits reinforced this week
- **Trace before you trust.** Most bugs were found by hand-tracing a small, deliberately chosen test case — not by staring at the code.
- **Input type is part of the spec.** "List of characters" vs "string" determined whether in-place mutation was even legal (Reverse String).
- **Explain it out loud.** If you can't narrate the "why" in ~30 seconds, the pattern hasn't fully landed yet.