# BFS / DFS on Grids — Recall Notes (Week 3, Thu–Fri)

## Trigger phrases
"Number of islands," "connected regions," "flood fill," "shortest path in a grid/maze" — anything involving a 2D grid where cells connect to their neighbors (usually 4-directionally: up/down/left/right, not diagonal — always confirm this from the problem statement).

## The core traversal skeleton (same for every grid problem)
1. **Visit a cell.**
2. **Mark it as visited** — critical, since grids have cycles/revisits. Without this, infinite loops or double-counting.
3. **Recurse/enqueue into each valid neighbor** — valid = still in bounds, and not already visited/doesn't match the required condition.

**The "sink" trick:** instead of a separate `visited` set, just mutate the grid cell itself the moment you visit it (e.g. `"1"` → `"0"` for islands, `old_color` → `new_color` for flood fill). Simpler than tracking a parallel data structure, works because you're not asked to preserve the original grid.

## DFS (Depth-First Search)
- Goes as deep as possible down one path before backtracking. Naturally implemented with **recursion**.
- Base case: out-of-bounds OR doesn't match the target condition → `return`.
- Bounds check for a 2D grid: `0 <= r < len(grid)` (rows) AND `0 <= c < len(grid[0])` (columns) — easy to mix up which dimension goes with which index.
- Recurse into all 4 neighbors: `(r+1,c), (r-1,c), (r,c+1), (r,c-1)`.
- **Design tip:** a DFS helper can `return True`/`False` (e.g. "did I just discover a new island?") — the outer loop can use that return value directly to drive counting, instead of a separate check before calling it.

## BFS (Breadth-First Search)
- Explores all immediate neighbors first, then their neighbors — "ripples outward" in rings. Implemented with a **queue** (`collections.deque` — O(1) pops from the front, unlike a list's `.pop(0)` which is O(n)).
- **Mark visited immediately when adding to the queue, not when popping it.** If you wait until pop-time to mark a cell visited, the same cell can be added to the queue multiple times (via different paths) before any instance is processed — causing redundant work or incorrect behavior.
- Skeleton:
```python
queue = deque([(r, c)])
grid[r][c] = <mark visited>
while queue:
    cur_r, cur_c = queue.popleft()
    for nr, nc in [(cur_r+1,cur_c), (cur_r-1,cur_c), (cur_r,cur_c+1), (cur_r,cur_c-1)]:
        if <in bounds> and <still unvisited/matches condition>:
            grid[nr][nc] = <mark visited>   # mark on add
            queue.append((nr, nc))
```
- Since BFS doesn't naturally return a boolean the way a DFS helper can, the outer loop needs an explicit check (`if grid[r][c] == "1":`) *before* calling BFS, rather than relying on a return value.

## When to use which
- **For connectivity / counting connected regions** (islands, flood fill): order of exploration doesn't matter — both DFS and BFS visit the identical *set* of cells and arrive at the same answer. DFS is usually preferred here purely for simplicity (no queue/import needed, recursion handles the frontier implicitly).
- **For shortest path / fewest steps:** BFS is the only one of the two that guarantees correctness. Its ring-by-ring order means the *first* time BFS reaches any cell, it did so via the shortest possible path — DFS gives no such guarantee, since it might stumble onto a long path to a cell long before trying the direct short one.
- One-line rule: *DFS and BFS visit the same reachable cells either way — pick DFS for simplicity when only connectivity matters, pick BFS specifically when you need shortest-path guarantees, since its ring-by-ring order is what makes that guarantee true.*

## Edge case worth remembering: flood-fill-style "recolor" traps
When a fill/recolor operation's "new value" could equal the "old value" (e.g. Flood Fill's `newColor == originalColor`), guard against it explicitly **before** starting the traversal:
```python
if new_value == old_value:
    return grid  # no-op, avoid ever starting the recursion
```
Without this guard: filling a cell to a value identical to what it already was means the cell never stops "looking like" the original target — so the normal "already visited" check (comparing against the original value) can never trigger, and traversal can revisit cells forever (infinite recursion / infinite loop).

## General bugs to watch for (recurring across both problems)
- Confusing which grid dimension (`len(grid)` vs `len(grid[0])`) bounds which index (`r` vs `c`).
- Comparing grid contents against the wrong type (e.g. checking `== 0` when the grid stores the string `"0"`).
- Inverted conditions in the base case (checking "is this the new/wrong value" instead of "is this the old/target value" — easy to flip which one should trigger a `return`).