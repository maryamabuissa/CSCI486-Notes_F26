# 9/21/2026 — MDP notes

## Review

- Search returns a plan / actions.
- MDP returns a **policy**: what action to take in each state.
- Once we have a policy, the agent can act like a reflex agent: see state → choose action.

Gridworld: start at bottom left, blocked square in the middle, goal and death states on the right.

Movement isn’t guaranteed:
- 80% intended direction
- 10% to either side

So the shortest path isn’t always the safest.

## Horizon

**Finite horizon:** only care about the next N steps. After the cutoff, rewards don’t count.

- Low N → might rush toward the goal if it can reach it.
- N = 100 → has time to take a longer, safer route.
- Best action can change depending on how many steps are left.

## Rewards

R(s) = x for **non-terminal** states — basically the reward for staying in the game. Goal/death rewards are separate.

- **Slightly positive:** might go in circles to keep collecting rewards.
- **Very positive:** even more reason to stay alive and keep collecting.
- **Slightly negative:** wants to finish, but might still go around to avoid death.
- **Very negative, like -1000:** might choose death just to end the game quickly. Every extra step costs too much.
- **x = 0:** no cost for taking extra steps, but goal/death rewards still matter.

Exact behavior depends on the terminal rewards, horizon, and discount factor.

## Discounted rewards

Want rewards sooner to count more than rewards later:

$$
U([s_0,s_1,\ldots]) = R(s_0) + \gamma R(s_1) + \gamma^2 R(s_2) + \cdots
$$

**Gamma = discount factor.** Board uses 0 < γ ≤ 1.

- Low γ, like 0.01 → mostly cares about short-term rewards.
- High γ, like 0.99 → cares more about long-term rewards too.
- γ = 1 → no discounting. Fine for finite tasks, but infinite reward sums can be a problem.

High γ doesn’t mean it stops caring — it cares less about how long it waits.

Even when x = 0, discounting makes getting a positive goal reward sooner better.

## Expected utility

How do we know where we’ll be 1000 steps from now? We don’t know exactly. Average over the possible paths using their probabilities.

$$
U^\pi(s) = \mathbb{E}\left[\sum_{t=0}^{\infty}\gamma^t R(s_t)\right]
$$

- s = starting state
- π = policy
- E = expected value over possible state sequences

Depends on the **policy** and **start state**, not just the most likely path.

## Best policy + Bellman equation

Choose the policy with the highest expected utility:

$$
\pi_s^* = \arg\max_\pi U^\pi(s)
$$

Once we know the best state values, choose the action with the best expected next-state value:

$$
\pi^*(s) = \arg\max_{a\in A(s)}\sum_{s'}P(s'\mid s,a)U^*(s')
$$

Bellman equation:

$$
U^*(s) = R(s) + \gamma\max_{a\in A(s)}\sum_{s'}P(s'\mid s,a)U^*(s')
$$

Basically: **value now = reward now + discounted best expected future value.**

P(s' | s, a) = chance of reaching s' from s after action a. U* = best possible utility. Argmax gives the choice; max gives its value.
