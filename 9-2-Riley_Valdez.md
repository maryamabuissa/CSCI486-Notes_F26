# Recall from Monday 8-31

- A* Algorithm searches "towards" the goal
- Uses a Heuristic: estimate of remaining cost to nearest goal
- Admissible: h(n) less than or equal to h*(n) where h*(n) is the actual cost to nearest goal 
- Admissibility -> tree A* optimal

# Today:

Goals for heuristic need to be non-negative, and goals have the value of 0

A-B A-C B-C C-G where G is goal
 1   3   1   6

 Heuristic values: h(a) = 8, h(b) = 7, h(c) = 0.

 - Recall that A* algorithm, that the frontier is a priority queue ordered by f, where f is f(n) = g(n) + h(n)
 - where g(n) is weight of edge and where h(n) is cost of heuristic

 - In this example, the returned cost would be from A->C->G, due to the weight of the heuristic of c, being 0
 - In order to make it optimal follow the psuedocode of:
-     if s is not in reached or child.Path-Cost < reached[s].Path-Cost then
       reached[s] <- Child

- Note: A* Dijkstra's w/cost c(n,a,n') + h(n) - h(n')

# New Terms:
- Consistency: h(n) is less than or equal to c(n, a, n') + h(n')
-      n is a node, where a is an action, and n' is the node we are traveling too
- Rephrased: h(n) - h(n') is less than or equal to c(n, a, n') + h(n')
-      The amount h drops in one step, can not be more than the cost of that step
## Example metaphor:
-   Time to get to Denver, h? ~ 20 hours
-   Time to drive to GJT, c? = 10 min
-   time to fly to DEN from GJT, h? ~45 min
-     Traveling 10 min to airport will cut > 19 hours off of my trip
      which seems inconsistent
## Exercise:
**Consistency -> admissibility**
### Summary:
- admissible -> Tree A* optimal
- consistent -> Graph A* optimal

### A good tool to use:

qiao.github.io/PathFinding.js/visual  


# So far:
1. Phrase problem as state space search
2. Used Human thinky ability to come up w/ heurisitc
3. put our intelligence in A*
4. Speedy and optimal search

<img width="165" height="165" alt="RigbyCat" src="https://github.com/user-attachments/assets/a9fab57b-fd56-46a7-ab33-c030e67977f2" />
