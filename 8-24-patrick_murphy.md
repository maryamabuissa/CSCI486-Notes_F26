# 8-24-26 AI Notes

## Agent

**Agent:** map from percepts to actions

**Reflex agent.** Uses conditions, action rules to make actions.

- If I meet a condition, I do an action.

**Planning agent:** makes + executes a series of actions based on environment

- Based on what it sees, it makes a plan.

**Learning agent:** updates rules based on experience

- Based on what it experiences and learns, it updates its plan and action.

## Rationality

**Rationality:** taking action expected to maximize performance (performance is based on the goal).

### 4 categories

#### Act rationally

#### Think like a human

- Not talked in a class.

#### Think rationally

#### Act rationally

- This is the main focus.

## Graph search

**Algorithms**

- BFS
- DFS
- `A*`

In project 1 you will use all 3 of these algorithms.

**Plan:** construct state space graph, enumerate paths, take the best one

- Graph of every state the agent can be in
  - Two states are connected when an action connects them.

**Issues?**

- Too many paths to enumerate
- Way too much
- Repeat states

**Explicit graph representation:** `(V, E)`

- Too big

**Implicit graph representation** (This is what we'll use in class)

- Start node
- Successor func
- Can construct graph as we search

## Tree search returns a solution, or failure

```text
1. initialize the frontier using the initial state of problem
2. loop do
3.     if the frontier is empty then return failure
4.     choose a leaf node and remove it from the frontier
5.     if the node contains a goal state then return the corresponding solution
6.     expand the chosen node, adding the resulting nodes to the frontier
```

## Example of state graph

- (`R` = Roomba, `E` = empty, `D` = dirty, `C` = clean)
- Not a goal state (both rooms dirty)

```text
Move Left              Base state                Right
_________    <- L      _________      R ->      _________
| R | E |              | R | E |                | E | R |
| D | D |              | D | D |                | D | D |
---------              ---------                ---------
                           |
                         Suck
                           v
                       _________
                       | R | E |
                       | C | D |
                       ---------
```


**Things to notice**
- Some paths lead to nothing
  - Like if Roomba is left, and goes left, it's just the same state.
  - If the Roomba starts left, moves right, then moves left, etc... it repeats indefinitely.

**State:** status of the world

**Node:** state, parent, most recent action, and a path cost.

**Frontier:** set of nodes that are at the edge of what's been explored

**Expand:** get children from the successor function

**Data structure for the frontier?**

- queue (FIFO) -> BFS
- stack (LIFO) -> DFS
- Priority queue (a queue where you have weights in it)
