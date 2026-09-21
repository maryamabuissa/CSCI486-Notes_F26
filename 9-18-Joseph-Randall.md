# Friday September 18th

## From Last Class
1. informed search/pruning: "domain knowledge"
	-lookup tables for common situations
	-approximate evaluation (estimate the value of non-terminal nodes - "deep enough")
	-ex: # of captured pieces in chess

## Informed Search vs Heuristic
1. heuristic: approximate distance to goal?
2. evaluation: how good is the board?

- forward pruning: ignore bad moves
	heuristic (no provable guarantees)
	sort actions, prune worst
	evaluate likely outcomes, prune worst

- meta reasoning:
	ex: Do we want to gamble?
	A: 0.8 probability for $4k vs 0.2 for $0 (Expected Value: (0.8)(4,000) + (0.2)(0) = $3.2k)
	B: 1.0 probability for $3k vs 0 for $0 (Epected Value: (1)(3,000) + (0)(0) = $3k)

	C: 0.2 probability for $4k vs 0.8 for $0 (Expected Value: (0.2)(4,000) + (0.8)(0) = $800)
	D: 0.25 probability for $3k vs 0.75 for $0 (Expected Value: (0.25)(3,000) + (0.75)(0) = $750)

- Uncertainty in outcome of actions
	Rewards at each step
	(Warning: Math)

## Markov Decision Processes
1. Markov
	- stochastic (random)
	- probabilities only depend on current state

2. Decision
	- agent has choices at every step

3. Processes
	- happens over time


## Policy
1. Policy-Mapping: state -> action

2. Probability
	- P(A): Probability of A
	- P(A|B): Probability of A given B
		P(2|even) = (1/3)

3. MDPs
	- S: set of states (some terminal)
	- actions(S): actions available in state S
	- P(s'|s,a): transition model
	- R(s): reward function

4. Evaluate Policy (Calculating Expected Value)
	- We want maximum expected value.
	- Number of steps? We don't want a simple guarantee of goal state if it runs on for too long.
		Optimal policy if R(s) = 0.2 for non-terminal s
	- horizon: infinite
		finite if there's a point N after which rewards cease to matter.
		R(s) = 0 for non-terminal s
		N = 3 (After 3 steps we don't care)
		what if N=100?