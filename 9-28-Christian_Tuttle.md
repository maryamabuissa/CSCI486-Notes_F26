# Policy Iteration 

  

## Policy Iteration 

  

- Variables: Gamma ($\gamma$), speed, reward 

- We can solve a linear system of equations in time $O(n^2)$. 

- Run simplified value iteration. 

- On code: `U <- policy-evaluation(pi, U, mdp)` 

- The code after that is expensive. 

- Do less frequently, but make it have more effect. 

  

### Summary 

- Policy iteration does more work per iteration but can converge faster in practice. 

  

# Example: New Game 

  

## Game Setup 

  

- 6-sided die. 

- States: Values of 1, 2, 3, 4, 5, and 6. 

  

## Actions 

  

- Roll: Reward = -1. 

- Stop: Reward = number on the dice. 

  

## Results 

  

If you fill out the table, you find that it is best to: 

  

- Roll on 1 and 2. 

- Stop on all other numbers. 

  

### Summary 

- MDPs allow us to model the world and figure out the best policy (offline planning). 

- They also allow us to start learning. 
