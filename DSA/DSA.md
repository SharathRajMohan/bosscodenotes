# DSA Prep — 4 Week Schedule for ML/DS Interviews

> A pattern-based 4-week plan to go from frozen-on-LeetCode to confidently solving easy/medium DSA problems in ML/DS interviews. Edit this page as you go — check off tasks, log confidence, write notes.
> 

## How to use this plan

The goal is **pattern recognition**, not problem count. By the end of 4 weeks you should be able to look at a new problem and name the underlying pattern within 30 seconds. That recognition is what unblocks the freeze.

**Three rules that matter more than the schedule itself:**

1. **Explain it out loud.** After every problem (solved or not), close the editor and explain the solution in 30 seconds as if to a colleague. If you can't, you didn't learn it — go back.
2. **Re-solve before you move on.** Every session starts with one quick re-solve of a problem from 7–14 days ago. This is where retention lives. Most people skip this; it's the highest-ROI habit.
3. **15-minute rule.** If you're stuck on an easy for 15 minutes, look at the solution, understand it, close the tab, re-implement from scratch. Staring teaches you nothing. Studying a pattern teaches you everything. No shame for the first 50 problems — you're building inventory.

**Time budget:** 1 hour weekdays, 2 hours weekends. ~9 hours/week. ~36 hours over 4 weeks. That's enough for ~40–50 problems if you keep volume modest and quality high.

**Start date:** *fill in* → **End date:** *fill in (4 weeks out)*

---

## The 8 patterns (your whole curriculum)

These cover ~80% of what ML/DS interviews ask. In priority order:

1. **Hashmap / set counting** — count things, find duplicates, check membership
2. **Two pointers** — sorted arrays, palindromes, pair-finding
3. **Sliding window** — "longest/max in a contiguous subarray"
4. **Running min/max** — single-pass aggregates (this is where the Q2 stock problem lives)
5. **Basic recursion / backtracking** — generate all X, permutations, subsets
6. **Simple dynamic programming** — "how many ways" / "min cost" with overlapping subproblems
7. **BFS / DFS on grids or simple graphs** — number of islands, flood fill
8. **Binary search** — beyond the basic case (rotated arrays, first/last occurrence)

Weeks 1–2 build patterns 1–4 (the high-frequency ones). Week 3 adds patterns 5–8. Week 4 is consolidation, mixed sets, and timed practice.

---

# 🗓️ Week 1 — Hashmaps & Two Pointers

**Goal:** Build instinct for the two most common patterns. By Friday, when you see "count / find / check membership," your hand should reach for a dict/set automatically.

## Week 1 weekly target

- [ ]  5 hashmap problems (Mon–Wed)
- [ ]  5 two-pointer problems (Thu–Sat)
- [ ]  Sunday: re-solve any 3 from this week without hints
- [ ]  Write the **trigger phrases** for both patterns in your own words (see Patterns Cheat Sheet below)

## Day-by-day suggestions

### Monday — Hashmap intro (1h)

- [x]  LeetCode #1 — Two Sum
- [x]  LeetCode #217 — Contains Duplicate
- After both: write 2 sentences on what the two problems have in common.
    - We find that we can add previous values encountered in the iteration into a hasmap and recall them in future iterations.
    - We check first and then alter the state of the hashmap.

### Tuesday — Hashmap reps (1h)

- [x]  LeetCode #242 — Valid Anagram
- [x]  LeetCode #387 — First Unique Character in a String

### Wednesday — Hashmap stretch (1h)

- [x]  LeetCode #350 — Intersection of Two Arrays II
- [x]  **Pattern reflection (15 min):** Without looking at solutions, write down — when should I reach for a hashmap vs a set? When does a `Counter` help?
    - Hashmap: Is essentially a dictionary, it is used ideally when we need to note a key and a value. For instance, we want to note the count of a character or the index at which it's located in a list, in simple words when there is an association involved (key,value) relationship.
    - Set: When no association is involved, as in we just want to store a list with no duplicates and this is what we would be evaluating against, like contains duplicate scenarios.
    - Counter: these are like swiss knives that can reduce code responsible for handling character counts of a string or sequence. It's always good to know.

### Thursday — Two pointers intro (1h)

- [x]  LeetCode #125 — Valid Palindrome
    - [x]  Valid Palindrome check function with string cleaning and eval performed inside the loop and not as a separate process.
- [x]  LeetCode #344 — Reverse String
- [x]  Additional: Check if a string is a Subsequence of another string. || (dual-pointer bounds-checking lesson)
- Important note: whenever you index into two different sequences inside one loop, both pointers need bounds-checking in the loop condition — not just one
- I've now seen **two distinct two-pointer sub-patterns**: converging from both ends (Palindrome), and same-direction-different-speed (Is Subsequence). I can now recognize *which* two-pointer shape a new problem needs within seconds.

### Friday — Two pointers reps (1h)

- [x]  LeetCode #26 — Remove Duplicates from Sorted Array
- Important point:  The problem doesn't actually require you to shrink the array or "clean up" the tail — it only requires that the first k slots contain the correct unique values in order. Whatever garbage sits after index k-1 is irrelevant and ignored by whoever calls your function.
Why design the problem this way? Because in many languages (C++, Java), arrays have a fixed size — you can't literally shrink one in place; you can only overwrite values within it. So "remove in place" really means "rearrange so the answer occupies a prefix, and report how long that prefix is" — the caller is expected to just look at nums[0:k] and ignore the rest. It's a common convention in in-place array problems, and worth remembering: "in place" often means "overwrite a prefix + return a length," not "physically shrink."
- [x]  LeetCode #283 — Move Zeroes
- [x]  Additional:

```python
'''
Given an integer array nums, return all the unique triplets 
[nums[i], nums[j], nums[k]] such that i != j != k and nums[i] + nums[j] + nums[k] == 0.
Example: nums = [-1,0,1,2,-1,-4] → [[-1,-1,2],[-1,0,1]]
(Note: the answer must not contain duplicate triplets, and order within a triplet or between triplets doesn't matter.)
nums[left]+nums[right] == -nums[i]
'''
```

- Important notes:
    - **whenever you combine a bounds-check with an index-access check in the same condition, the bounds-check goes first**, so short-circuit evaluation protects you.

### Saturday — Two pointers stretch (2h)

- [x]  LeetCode #167 — Two Sum II (Input Array Is Sorted)
- [x]  LeetCode #11 — Container With Most Water *(this one is the payoff — savor the pattern click)*
- [x]  **End-of-day:** explain Container With Most Water out loud in under 60 seconds. Record yourself on phone if helpful.

### Sunday — Review (2h)

- [x]  Re-solve 3 problems from earlier in the week without hints, time yourself
- [x]  Update confidence ratings in the tracker below
- [x]  Write Week 1 reflection in the reflections section

---
[Hashmap and Pointers](Patterns/Hashmaps&Pointers.md)
---

# 🗓️ Week 2 — Sliding Window & Running Min/Max

**Goal:** Internalize "one pass through the array, maintain some state." Many ML interview Qs hide in this family.

## Week 2 weekly target

- [x]  4 sliding window problems (Mon–Wed)
- [x]  4 running min/max problems (Thu–Sat) — this is where the stock-buy/sell problem lives, the one you froze on
- [x]  Sunday: re-solve 3 problems from Weeks 1 and 2 mixed

## Day-by-day suggestions

### Monday — Sliding window intro (1h)

- [x]  LeetCode #643 — Maximum Average Subarray I *(fixed-size window — the easiest entry point)*

<aside>
💡

To directly answer your question about the pattern in general, here's the clean mental model, using this exact problem:

**The picture:** think of the window as a physical frame of width `k` sliding across the array, one step at a time. At any moment, `window_sum` represents *exactly* what's currently inside the frame — nothing more.

```
nums:   [1, 12, -5, -6, 50, 3]
         ↑________________↑
window: [1, 12, -5, -6]        sum=2      ← starting position
             ↑________________↑
window:     [12, -5, -6, 50]   sum=51     ← slid right by 1
                 ↑________________↑
window:         [-5, -6, 50, 3] sum=42    ← slid right by 1 again
```

**The reason incremental update works:** when the frame slides one step right, it **loses exactly one element on the left edge** (the one that's no longer inside the frame) and **gains exactly one element on the right edge** (the new one now inside). Everything in the *middle* of the frame stays exactly the same — so there's no need to recompute it. That's the entire efficiency gain: you're not recomputing `k` elements each time, just swapping 2.

**The general skeleton for ANY fixed-size sliding window problem:**

```python
window_state = <compute from first k elements>
best = <initialize from window_state>
for i in range(k, len(nums)):
    window_state = update(window_state, remove=nums[i-k], add=nums[i])
    best = compare(best, window_state)
```

Here `i` plays the role of your `right` — the incoming element's index. `i-k` is always the outgoing element — the one that just fell outside the left edge of a width-`k` window.

This "add the new, remove the old, compare" rhythm is the entire pattern — you'll see the *exact* same skeleton in tomorrow's problems, just with the "state" being something other than a simple sum (e.g., a count of distinct characters).

**Monday's first problem done.** Ready for **#1876 — Substrings of Size Three with Distinct Characters**, the second fixed-window problem for today?

</aside>

- [x]  LeetCode #1876 — Substrings of Size Three with Distinct Characters

### Tuesday — Variable-size window (1h)

- [x]  LeetCode #3 — Longest Substring Without Repeating Characters *(combines sliding window + hashmap — note the synergy)*

### Wednesday — Window stretch (1h)

- [x]  LeetCode #209 — Minimum Size Subarray Sum
- [x]  **Reflection:** When does the window grow vs shrink? Write your own rule.
    - [x]  Grow (`right`) to chase validity. Shrink (`left`) to minimize once valid — keep shrinking while still valid, stop the moment it breaks.

### Thursday — Running min/max intro (1h)

- [x]  **LeetCode #121 — Best Time to Buy and Sell Stock** ← *this is Q2 from your real interview*
- [x]  After solving: write a 3-sentence explanation of why the one-pass O(n) works.
    
    My explanation:
    
    - We utilize state variables to keep track of the most lowest price day come across so far.
    - Since, we know the lowest possible buy day using the state variable, all we need to focus on is to check if the current iteration yields a profit or a loss. In situations of a profit we update max_profit, provided the new profit is greater than the old profit. And in situations of a loss, we update the min_price state to hold the new lowest possible buy day.
    - At the end of the loop we simply return the maximum profit state variable.

### Friday — Running aggregate reps (1h)

- [x]  LeetCode #53 — Maximum Subarray (Kadane's algorithm)
- [x]  LeetCode #485 — Max Consecutive Ones

### Saturday — Stretch (2h)

- [x]  LeetCode #122 — Best Time to Buy and Sell Stock II *(notice how a tiny problem-statement change flips the strategy)*
- [ ]  LeetCode #918 — Maximum Sum Circular Subarray *(harder — only attempt if Sat feels strong; otherwise save for Week 4)*

### Sunday — Mixed review (2h)

- [ ]  Re-solve 1 hashmap + 1 two-pointer + 1 sliding window problem from earlier weeks
- [ ]  Update tracker, write Week 2 reflection

---

[Sliding Window Notes](Patterns\SlidingWindow.md)

---


# 🗓️ Week 3 — Recursion, DP, BFS/DFS, Binary Search

**Goal:** Cover the remaining 4 patterns lightly. Don't try to master DP in a week — just learn to *recognize* it.

## Week 3 weekly target

- [ ]  2 recursion/backtracking problems
- [ ]  2 simple DP problems
- [ ]  2 BFS/DFS problems
- [ ]  2 binary search problems
- [ ]  Sunday: mixed review across all 8 patterns

## Day-by-day suggestions

### Monday — Recursion (1h)

- [x]  LeetCode #344 review (already done — but solve it recursively this time)
- [x]  LeetCode #509 — Fibonacci Number (recursive, then memoized — feel the speedup)

### Tuesday — Backtracking taste (1h)

- [x]  LeetCode #78 — Subsets *(the canonical backtracking warm-up)*

### Wednesday — Simple DP (1h)

- [x]  LeetCode #70 — Climbing Stairs
- [x]  LeetCode #198 — House Robber
- [x]  **Reflection:** What's the difference between recursion + memoization and bottom-up DP? Write it.

### Thursday — BFS/DFS on grids (1h)

- [x]  LeetCode #200 — Number of Islands *(the canonical grid DFS)*

### Friday — More graph traversal (1h)

- [ ]  LeetCode #733 — Flood Fill
- [ ]  **Reflection:** When BFS vs DFS? Write the difference in 2 sentences.

### Saturday — Binary search (2h)

- [ ]  LeetCode #704 — Binary Search *(the textbook case — make sure you nail the off-by-one)*
- [ ]  LeetCode #34 — Find First and Last Position of Element in Sorted Array *(this is where binary search gets interesting)*

### Sunday — Big review (2h)

- [ ]  Re-solve 4 problems, one from each Week-1–2 pattern
- [ ]  Update tracker, write Week 3 reflection

---
[Recursion, DP and Back Tracking notes](Patterns\RecursionDPnBackTracking.md) \
[BFS and DFS notes](Patterns\BFSDFS.md)

---

# 🗓️ Week 4 — Consolidation, Mixed Sets & Timed Practice

**Goal:** Simulate interview conditions. By the end of this week, you should be solving an easy in ~15 min and a medium in ~30 min.

## Week 4 weekly target

- [ ]  3 timed easy problems from random patterns (no hints, 15 min limit each)
- [ ]  3 timed medium problems (30 min limit each)
- [ ]  One full mock: 60 min, 2 problems (1 easy + 1 medium), pick patterns blind
- [ ]  Final reflection + decide what to keep practicing post-plan

## Day-by-day suggestions

### Monday — Timed easies (1h)

- [ ]  Pick 3 unseen easies across hashmap / two-pointer / sliding-window. 15 min each.
- [ ]  If you don't finish in 15 min — note the pattern, move on.

### Tuesday — First timed medium (1h)

- [ ]  LeetCode #560 — Subarray Sum Equals K *(hashmap + prefix sum — beautiful combo)*
- [ ]  30 min hard cap. If stuck at 20 min, peek at a hint.

### Wednesday — Second timed medium (1h)

- [ ]  LeetCode #438 — Find All Anagrams in a String *(sliding window + hashmap)*

### Thursday — Third timed medium (1h)

- [ ]  LeetCode #424 — Longest Repeating Character Replacement

### Friday — Light day, re-solve favorites (1h)

- [ ]  Pick 2 problems you found beautiful from the past 4 weeks. Re-solve. This is consolidation.

### Saturday — **Mock interview** (2h)

- [ ]  60 min: 1 random easy + 1 random medium, talking out loud the whole time (record yourself)
- [ ]  30 min: review the recording — where did you ramble? Where did you freeze? Where did you forget to talk?
- [ ]  30 min: post-mortem write-up in reflections

### Sunday — Final reflection (2h)

- [ ]  Re-solve the stock problem (#121) one more time, talking out loud the whole way through. Notice how different this feels from day 1.
- [ ]  Fill out the **Final Reflection** section below: which patterns feel solid, which still feel shaky, what to do next.

---

# 📋 Patterns Cheat Sheet

*Fill these in **in your own words** as you finish each pattern. Don't copy from solutions — write what makes the pattern click for you. This is the artifact that survives the 4 weeks.*

## 1. Hashmap / Set

**Trigger phrases:** *e.g., "count occurrences", "find duplicates", "check membership", "have I seen this before?"*

**My rule of thumb:** 

**Template code:** 

```
# fill in
```

## 2. Two Pointers

**Trigger phrases:** 

**My rule of thumb:** 

## 3. Sliding Window

**Trigger phrases:** 

**My rule of thumb:** 

## 4. Running Min/Max (single-pass aggregate)

**Trigger phrases:** 

**My rule of thumb:** 

## 5. Recursion / Backtracking

**Trigger phrases:** 

**My rule of thumb:** 

## 6. Dynamic Programming

**Trigger phrases:** 

**My rule of thumb:** 

## 7. BFS / DFS

**Trigger phrases:** 

**My rule of thumb:** 

## 8. Binary Search

**Trigger phrases:** 

**My rule of thumb:** 

---

# 📊 Progress Tracker

Log every problem here. Confidence is 1–5: **1** = couldn't solve, looked at solution; **3** = solved with hints / took >15 min; **5** = solved cleanly under time, explained it out loud.

| Week | Date | Problem | Pattern | Time spent | Solved without hints? | Confidence (1–5) | Notes |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1 |  | Two Sum (#1) | Hashmap |  |  |  |  |
| 1 |  | Contains Duplicate (#217) | Hashmap |  |  |  |  |
| 1 |  | Valid Anagram (#242) | Hashmap |  |  |  |  |
| 1 |  | First Unique Character (#387) | Hashmap |  |  |  |  |
| 1 |  | Intersection of Two Arrays II (#350) | Hashmap |  |  |  |  |
| 1 |  | Valid Palindrome (#125) | Two pointers |  |  |  |  |
| 1 |  | Reverse String (#344) | Two pointers |  |  |  |  |
| 1 |  | Remove Duplicates Sorted Array (#26) | Two pointers |  |  |  |  |
| 1 |  | Move Zeroes (#283) | Two pointers |  |  |  |  |
| 1 |  | Two Sum II (#167) | Two pointers |  |  |  |  |
| 1 |  | Container With Most Water (#11) | Two pointers |  |  |  |  |
| 2 |  | Max Avg Subarray I (#643) | Sliding window |  |  |  |  |
| 2 |  | Substrings Size 3 Distinct (#1876) | Sliding window |  |  |  |  |
| 2 |  | Longest Substring No Repeat (#3) | Sliding window |  |  |  |  |
| 2 |  | Min Size Subarray Sum (#209) | Sliding window |  |  |  |  |
| 2 |  | Best Time Buy/Sell Stock (#121) | Running min/max |  |  |  |  |
| 2 |  | Maximum Subarray (#53) | Running min/max |  |  |  |  |
| 2 |  | Max Consecutive Ones (#485) | Running min/max |  |  |  |  |
| 2 |  | Best Time Buy/Sell II (#122) | Running min/max |  |  |  |  |
| 3 |  | Fibonacci (#509) | Recursion |  |  |  |  |
| 3 |  | Subsets (#78) | Backtracking |  |  |  |  |
| 3 |  | Climbing Stairs (#70) | DP |  |  |  |  |
| 3 |  | House Robber (#198) | DP |  |  |  |  |
| 3 |  | Number of Islands (#200) | DFS/BFS |  |  |  |  |
| 3 |  | Flood Fill (#733) | DFS/BFS |  |  |  |  |
| 3 |  | Binary Search (#704) | Binary search |  |  |  |  |
| 3 |  | First & Last Position (#34) | Binary search |  |  |  |  |
| 4 |  | Subarray Sum Equals K (#560) | Hashmap + prefix |  |  |  |  |
| 4 |  | Find All Anagrams (#438) | Sliding window + hashmap |  |  |  |  |
| 4 |  | Longest Repeating Char Replace (#424) | Sliding window |  |  |  |  |

---

# 🔁 Spaced-Repetition Review Log

List problems by **date last reviewed** so you can spot what's gone stale. Anything older than 14 days = re-solve before adding new problems.

| Problem | Pattern | First solved | Last reviewed | # of reviews | Next review due |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |

---

# 📝 Weekly Reflections

## Week 1

- **What clicked:**
- **What didn't:**
- **Patterns I now reach for without thinking:**
- **Adjustments for next week:**

## Week 2

- **What clicked:**
- **What didn't:**
- **Patterns I now reach for without thinking:**
- **Adjustments for next week:**

## Week 3

- **What clicked:**
- **What didn't:**
- **Patterns I now reach for without thinking:**
- **Adjustments for next week:**

## Week 4 — Final Reflection

- **Patterns I can confidently identify in <30 sec:**
- **Patterns still shaky:**
- **Where did I freeze in the mock?**
- **Biggest unlock of the 4 weeks:**
- **Plan for weeks 5–8 (if continuing):**

---

# 🚧 What NOT to do (anti-patterns I'll avoid)

- ❌ Doing "Blind 75" linearly — mixes patterns and breaks the repetition effect
- ❌ Watching YouTube solutions before attempting — passive learning, near-zero retention
- ❌ Grinding mediums while easies still feel hard — pattern recognition is built at the easy level
- ❌ Measuring progress by problem count — measure by: can I name the pattern in 30 sec?
- ❌ Skipping the explain-out-loud step
- ❌ Skipping the re-solve / spaced repetition — this is where almost everyone leaks progress
