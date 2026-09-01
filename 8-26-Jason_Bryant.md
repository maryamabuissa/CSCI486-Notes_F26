# Wed August 26th

For a graph traversal path if you wish to go backwards:
- For the problems we are going to do:
  - Traverse tree backwards until you reach the start

### What about repeated states?
- **Example:**
  - Grid search: number of nodes in a depth search tree of depth $d$ allowing repeated states
  - Four actions can be taken (one for each direction): $4^d$
  - You can go $d$ distance in $d$ steps
  - There are unique nodes in the search tree $\le 4d^2$
- **Solution:** Graph search

---

## Graph Search Pseudo Code

```text
function Best-First-Search(problem, f) returns a solution node or failure
    node <- Node(STATE=problem.INITIAL)
    frontier <- a priority queue ordered by f, with node as an element
    reached <- a lookup table, with one entry with key problem.INITIAL and value node

    while not is empty(frontier) do
        node <- POP(frontier)
        if problem.IS-GOAL(node.STATE) then return node
        for each child in EXPAND(problem, node) do
            s <- child.STATE
            if s is not in reached or child.PATH-COST < reached[s].PATH-COST then
                reached[s] <- child
                add child to frontier
    return failure
```

### Search Comparisons
Assess whether Breadth-First, Depth-First, or another graph search is best (e.g., for Four Queens, Depth-First is best).

- **Which is better? DFS vs. BFS**
  - **Depth-First Search (DFS):** Expands fewer nodes if lucky. Good space complexity.
  - **Breadth-First Search (BFS):** Always finds a solution eventually (i.e., is *complete*). Stores everything in memory.
- **Which finds the best solution (i.e., *optimal*)?**
  - **Breadth-First Search will always find the optimal solution** (for uniform step costs).
- **Runtime Complexity:**
  - Depth-First Search: 

---

## Big O Notation
*(Will be used for class)*

### Big O Examples
- $O(n)$: Linear time
- $O(n^2)$: Quadratic time# Wed August 26th

For a graph traversal path if you wish to go backwards:
- For the problems we are going to do:
  - Traverse tree backwards until you reach the start

### What about repeated states?
- **Example:**
  - Grid search: number of nodes in a depth search tree of depth $d$ allowing repeated states
  - Four actions can be taken (one for each direction): $4^d$
  - You can go $d$ distance in $d$ steps
  - There are unique nodes in the search tree $\le 4d^2$
- **Solution:** Graph search

---

## Graph Search Pseudo Code

```text
function Best-First-Search(problem, f) returns a solution node or failure
    node <- Node(STATE=problem.INITIAL)
    frontier <- a priority queue ordered by f, with node as an element
    reached <- a lookup table, with one entry with key problem.INITIAL and value node

    while not is empty(frontier) do
        node <- POP(frontier)
        if problem.IS-GOAL(node.STATE) then return node
        for each child in EXPAND(problem, node) do
            s <- child.STATE
            if s is not in reached or child.PATH-COST < reached[s].PATH-COST then
                reached[s] <- child
                add child to frontier
    return failure
```

### Search Comparisons
Assess whether Breadth-First, Depth-First, or another graph search is best (e.g., for Four Queens, Depth-First is best).

- **Which is better? DFS vs. BFS**
  - **Depth-First Search (DFS):** Expands fewer nodes if lucky. Good space complexity.
  - **Breadth-First Search (BFS):** Always finds a solution eventually (i.e., is *complete*). Stores everything in memory.
- **Which finds the best solution (i.e., *optimal*)?**
  - **Breadth-First Search will always find the optimal solution** (for uniform step costs).
- **Runtime Complexity:**
  - Depth-First Search: 

---

## Big O Notation
*(Will be used for class)*

### Big O Examples
- $O(n)$: Linear time
- $O(n^2)$: Quadratic time
