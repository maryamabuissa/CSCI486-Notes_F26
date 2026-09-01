Recall: an Agent is a mapping from a list of percepts to an action

Ex. The Roomba can tell whether the room is dirty or clean,and which room the Roomba is in.

Recall: Rationality is taking the action expected to maximize the sum performance measure given the percepts and preexisting knowledge.

AGENTS

Ex. 1  
Legally distinct roomba problem

Agent: Vroomba

Percepts: what room its in, cleanliness of both rooms  
.  
Goal: clean both rooms.

Actions: L, R, Suck.

\[A, 0, 1\] → suck  
\[A, 0, 0\] → suck or R			THESE ACTIONS MAKE THIS A RATIONAL AGENT.  
\[B, 0, 1\] → L  
\[B, 1, 1\] → Anything. 

Ex. 2   
4 queens

Agent: Thing placing the queens

Percepts: 4 x 4 chess board, 0 \- 4 Queens.

Action: Place a queen.

Goal: queens cannot attack each other.

Ex. 3   
8 puzzle

Agent: Thing Moving the Tiles

Percept: Location of Tiles.

Action:Slide a tile Up, Down, Left, Or Right, into an empty space.

Goal: In the fewest steps 

Assuming the board is randomly arranged this is the end state.

\----------------------------------------------------------------------------------------------------------------------------  
State space graph

State space: set of states

(INSERT PACMAN STATES HERE

Successor function: succ: (state, action) → (resulting state, cost)

(INSERT PACMAN NEXT STATE HERE)

Initial State  
Goal test: goal (state) → boolean

Ex 1\.  
 Legally distinct roomba problem

State space: cleanliness of both rooms, which room the Vroomba is in.

Initial state: rooms A and B dirty, Room A starting position.

Actions: L, R, Suck.

Successor function: L/R moves if possible, suck cleans room the Vroomba is in.

Goal test: both rooms are clean.

State space graph: every state is a node, directed edges from successor function.

\[INSERT STATE SPACE GRAPH\]

You can use graph search to solve the problem

Ex. 2

4 Queens

To be continued (Try to fill out the above sections for 4 queens at home)

8 Queens

State space: board and position of queens

Initial state: empty

Actions: place a queen on empty space

Successor function: placing a queen, puts a queen there.

Goal test: no queens can attack eachother

By adjusting the actions we can reduce the \# of states on the state space graph

Ex. Actions: place a queen on an empty SAFE SPACE reduced from \!64 to significantly less.

