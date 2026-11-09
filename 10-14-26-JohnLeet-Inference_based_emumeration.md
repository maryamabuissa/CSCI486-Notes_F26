# CSCI 486 — Probability, Conditional Probability & Bayesian Networks
**Class recap — October 14, 2026**

## What We Covered
We moved from counting possible outcomes to reasoning about uncertainty: **sample spaces → events → probability rules → conditional probability → independence → Bayesian networks**. These ideas help AI systems update beliefs when they receive new evidence.

## 1. Sample Spaces and Events
- **Sample space** $\Omega$: the set of all possible outcomes.
- **Event** $E \subseteq \Omega$: a subset of outcomes that satisfy a condition.
- **Probability** $P(E)$: the chance that an event occurs, between 0 and 1.

Example: roll two six-sided dice. An outcome is an **ordered pair** $(d_1,d_2)$, so there are $6\cdot6=36$ equally likely outcomes.

If $T=d_1+d_2$ is the sum, then:

$$P(T=2)=\frac{1}{36},\qquad P(T=7)=\frac{6}{36},\qquad P(T=8)=\frac{5}{36}.$$

**Why?** Count the ordered pairs that produce the desired sum, then divide by 36. For example, $T=7$ has $(1,6),(2,5),(3,4),(4,3),(5,2),(6,1)$.

### Basic probability rules
1. $0\le P(E)\le 1$.
2. $P(\Omega)=1$.
3. If $A$ and $B$ are **disjoint** (cannot both occur), $P(A\cup B)=P(A)+P(B)$.
4. In general, overlapping events require subtraction: 

$$\boxed{P(A\cup B)=P(A)+P(B)-P(A\cap B)}$$

5. Complement rule: $P(A^c)=1-P(A)$.

**Notation:** $A\cup B$ means *A or B*; $A\cap B$ means *A and B*.

## 2. Counting With Combinations
When order does **not** matter and repetition is allowed, the number of multisets of size $k$ selected from $n$ categories is:

$$\boxed{\binom{n+k-1}{k}}$$

For example, three rolls of a four-sided die in nondecreasing order ($X_1\le X_2\le X_3$) correspond to choosing a multiset of three values from $\{1,2,3,4\}$:

$$\binom{4+3-1}{3}=\binom63=20.$$

There are $4^3=64$ equally likely ordered sequences in total, so:

$$P(X_1\le X_2\le X_3)=\frac{20}{64}=\boxed{\frac5{16}}.$$

## 3. Conditional Probability
Conditional probability asks: **How likely is A, given that B has occurred?**

$$\boxed{P(A\mid B)=\frac{P(A\cap B)}{P(B)}}\qquad P(B)>0$$

The condition $B$ restricts the possible outcomes. It does **not** automatically mean $B$ causes $A$.

Rearranging gives the **product (chain) rule**:

$$\boxed{P(A\cap B)=P(A\mid B)P(B)}$$

For three events:

$$P(A\cap B\cap C)=P(A\mid B,C)P(B\mid C)P(C).$$

Here $P(A\mid B,C)$ means the probability of $A$ given **both** $B$ and $C$.

## 4. Independence vs. Conditional Dependence
Two events $A$ and $B$ are **independent** if learning that one happened does not change the probability of the other:

$$P(A\mid B)=P(A)\quad\text{(when }P(B)>0\text{)}.$$

Equivalently:

$$\boxed{P(A\cap B)=P(A)P(B)}.$$

**Important distinction:** Independent events *can* happen together. Disjoint events *cannot* happen together. Nonzero-probability disjoint events are therefore not independent.

Events may also be **conditionally independent** given a third variable $C$:

$$P(A,B\mid C)=P(A\mid C)P(B\mid C).$$

This means that once $C$ is known, learning about $A$ provides no additional information about $B$.

## 5. Bayesian Networks
A **Bayesian network** is a **directed acyclic graph (DAG)** representing a joint probability distribution.

- Each **node** is a random variable.
- An **arrow** represents a direct probabilistic dependency in the model.
- Each node has a **conditional probability distribution** given its parents.
- **Acyclic** means you cannot follow arrows and return to the starting node.

Example from the notes:

```text
            Alarm
           /     \
     John calls   Mary calls
```

If $A$ = alarm, $J$ = John calls, and $M$ = Mary calls, the graph represents the factorization:

$$\boxed{P(A,J,M)=P(A)P(J\mid A)P(M\mid A)}$$

The model assumes $J$ and $M$ are conditionally independent **given the alarm**. Their calls may still be correlated when the alarm state is unknown.

### Conditional probability tables
The handwritten example includes illustrative values resembling:

| Alarm state | $P(J=\mathrm{true}\mid A)$ | $P(M=\mathrm{true}\mid A)$ |
|---|---:|---:|
| True | 0.9 | 0.7 |
| False | 0.05 | 0.01 |

These are conditional probabilities, **not** the overall probabilities of John or Mary calling. For example, $P(J=\mathrm{true}\mid A=\mathrm{true})=0.9$ says John calls 90% of the time **when the alarm sounds**.

A separate fire variable appears in the notes with $P(F)=0.002$. If fire is modeled as a cause of the alarm, its arrow would point **into** the alarm node, and the alarm would need a conditional probability table such as $P(A\mid F)$ (or $P(A\mid B,F)$ if burglary $B$ is another cause). The complete probabilities cannot be calculated without that table.

## 6. Why Bayesian Networks Matter for AI
A full joint distribution for $n$ Boolean variables requires $2^n$ entries before normalization. A Bayesian network can represent the same distribution more compactly **when conditional independence assumptions hold**.

The general factorization is:

$$\boxed{P(X_1,\ldots,X_n)=\prod_{i=1}^{n}P(X_i\mid \mathrm{Parents}(X_i))}.$$

This allows an AI system to reason from evidence: *If Mary calls, does that make an alarm more likely? If an alarm is likely, how does that change the probability of a fire?* Answering those questions requires inference through the network.

## Main Takeaway
```text
Possible outcomes (Ω)
        ↓
Events (A, B, ...)
        ↓
Probabilities P(A)
        ↓
Evidence changes beliefs: P(A | B)
        ↓
Independence assumptions
        ↓
Bayesian network (DAG + probability tables)
        ↓
Inference about uncertain events
```

**Equations worth remembering:**

$$P(A\mid B)=\frac{P(A\cap B)}{P(B)}$$

$$P(A\cap B)=P(A\mid B)P(B)$$

$$P(A\cap B)=P(A)P(B)\quad\text{if independent}$$

$$P(X_1,\ldots,X_n)=\prod_iP(X_i\mid\mathrm{Parents}(X_i))$$
