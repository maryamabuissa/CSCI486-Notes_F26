# CSCI 486 — Reinforcement Learning & Q-Learning

**Class notes — October 7, 2026**

## What We Covered Today

Today we moved from **Markov Decision Processes (MDPs)** into **reinforcement learning (RL)**.

The major difference is that an RL agent can **learn from experience** instead of already knowing everything about the environment.

```text
current state s
      ↓
take action a
      ↓
receive reward r
      ↓
arrive in next state s'
      ↓
update what we know
```

The basic learning loop is:

$$
(s,a,r,s') \longrightarrow \text{update our estimate}
\longrightarrow \text{better future decisions}
$$

---

## 1. From MDPs to Reinforcement Learning

With an MDP, we describe the world using:

- states $s$
- actions $a$
- transition probabilities $P(s' \mid s,a)$
- rewards $R$
- utilities $U(s)$
- a policy $\pi(s)$
- a discount factor $\gamma$

In **reinforcement learning**, the agent may not know the transition model or reward structure ahead of time. Instead, it learns by interacting with the environment and observing what happens.

> **Notation note:** The lecture sometimes writes a reward as $R(s)$, while the Q-learning pseudocode uses the observed reward $r$. Here, $r$ means the reward actually observed from a transition.

---

## 2. Active Reinforcement Learning

In **active RL**, the agent must choose actions while it is still learning. This creates an exploration/exploitation tradeoff.

### Exploitation

Choose the action that currently looks best.

### Exploration

Try an action that may not currently look best so the agent can learn more about it.

The agent needs a balance between the two.

> **Important:** $\gamma$ is the **discount factor**, not the exploration parameter. It controls how much future reward matters.

The pseudocode shown in class used an exploration function involving both a Q-value and a visit count:

$$
a=\arg\max_{a'}f\left(Q(s',a'),N_{sa}(s',a')\right)
$$

Conceptually:

- $Q(s',a')$ asks: **How good does this action currently look?**
- $N_{sa}(s',a')$ asks: **How thoroughly have I tried it?**

---

## 3. Utility vs. Q-Values

A utility describes the value of a **state**:

$$
\boxed{U(s)}
$$

> **How good is it to be in state $s$?**

A Q-value describes the value of a **state-action pair**:

$$
\boxed{Q(s,a)}
$$

> **How good is it to take action $a$ while in state $s$?**

For optimal Q-values:

$$
\boxed{
U^*(s)=\max_a Q^*(s,a)
}
$$

The optimal policy chooses the action that gives that value:

$$
\boxed{
\pi^*(s)=\arg\max_a Q^*(s,a)
}
$$

The important distinction is:

```text
max     → returns the best VALUE
argmax  → returns the ACTION producing that value
```

For example, if:

$$
Q(s,N)=4,\quad Q(s,S)=1,\quad Q(s,E)=8,\quad Q(s,W)=3,
$$

then:

$$
\max_aQ(s,a)=8
$$

while:

$$
\arg\max_aQ(s,a)=E.
$$

---

## 4. Learning by Correcting an Estimate

The update equations from class follow one basic idea:

$$
\boxed{
\text{new estimate}
=
\text{old estimate}
+
\text{correction}
}
$$

For a state utility, a temporal-difference style update is:

$$
U(s)\leftarrow
U(s)+
\alpha\left[r+\gamma U(s')-U(s)\right]
$$

The expression:

$$
r+\gamma U(s')-U(s)
$$

is the **temporal-difference (TD) error**: the difference between the new target and the old prediction.

So:

```text
positive error → outcome looks better than predicted
negative error → outcome looks worse than predicted
zero error     → prediction already matches the target
```

The learning rate $\alpha$ controls how strongly the estimate changes.

---

## 5. Q-Learning

Q-learning applies the same correction idea to **state-action values**.

The main equation from class was:

$$
\boxed{
Q(s,a)
\leftarrow
Q(s,a)
+
\alpha
\left[
r+\gamma\max_{a'}Q(s',a')-Q(s,a)
\right]
}
$$

The pieces are:

| Symbol | Meaning |
|---|---|
| $s$ | state we were in |
| $a$ | action we took |
| $r$ | reward we received |
| $s'$ | state we arrived in |
| $a'$ | possible action from $s'$ |
| $\alpha$ | learning rate |
| $\gamma$ | discount factor |
| $Q(s,a)$ | current estimate of the state-action pair |

The easiest way to read the equation is:

### Build the new target

$$
\boxed{
\text{target}
=
r+\gamma\max_{a'}Q(s',a')
}
$$

This means:

> Take the reward we just received and add the discounted value of the best action we currently think is available from the next state.

### Compare it with the old prediction

$$
\boxed{
\delta
=
r+\gamma\max_{a'}Q(s',a')-Q(s,a)
}
$$

### Correct the old Q-value

$$
\boxed{
Q(s,a)\leftarrow Q(s,a)+\alpha\delta
}
$$

So Q-learning is essentially asking:

> **After seeing what happened, was this action better or worse than I previously thought?**

Q-learning is **model-free** because it can learn from observed transitions $(s,a,r,s')$ without explicitly maintaining the transition probabilities $P(s'\mid s,a)$.

---

## 6. Approximate Q-Learning

We also introduced **approximate Q-learning**.

Regular Q-learning can conceptually store a separate value for every state-action pair:

$$
Q(s,a)
$$

That becomes difficult when there are enormous numbers of possible states, such as in Pacman.

Instead of memorizing every exact situation, approximate Q-learning represents a state-action pair using **features**.

Examples from class included:

- number of nearby ghosts
- amount of nearby food

Each feature has a learned weight describing how important it is.

The approximate Q-value is:

$$
\boxed{
Q(s,a)=\sum_i w_i f_i(s,a)
}
$$

where:

- $f_i(s,a)$ = feature $i$ of the state-action pair
- $w_i$ = learned importance of that feature

For example, experience may cause:

```text
nearby ghosts → negative weight
nearby food   → positive weight
```

The weights are updated using the same Q-learning TD error:

$$
\boxed{
w_i\leftarrow w_i+\alpha\delta f_i(s,a)
}
$$

where:

$$
\delta=
r+\gamma\max_{a'}Q(s',a')-Q(s,a).
$$

The major advantage is **generalization**: instead of memorizing every exact situation, the agent learns which features tend to predict good or bad outcomes.

---

## 7. Main Takeaway

The conceptual thread from today's lecture was:

```text
MDP
 ↓
Reinforcement Learning
 ↓
experience: (s, a, r, s')
 ↓
Q(s,a): how good was this action from this state?
 ↓
compare what happened with what we predicted
 ↓
update Q(s,a)
 ↓
repeat and improve
```

When the state space becomes too large to memorize:

```text
individual Q(s,a) entries
          ↓
describe state-action pairs with features
          ↓
Approximate Q-Learning
          ↓
learn which features predict good/bad outcomes
```

### Equations Worth Recognizing

**Q-learning:**

$$
\boxed{
Q(s,a)
\leftarrow
Q(s,a)
+
\alpha
\left[
r+\gamma\max_{a'}Q(s',a')-Q(s,a)
\right]
}
$$

**Approximate Q-value:**

$$
\boxed{
Q(s,a)=\sum_iw_if_i(s,a)
}
$$

**Approximate Q-learning weight update:**

$$
\boxed{
w_i\leftarrow w_i+\alpha\delta f_i(s,a)
}
$$

The common idea behind all of them is:

$$
\boxed{
\text{prediction}
\rightarrow
\text{experience}
\rightarrow
\text{error}
\rightarrow
\text{correction}
}
$$
