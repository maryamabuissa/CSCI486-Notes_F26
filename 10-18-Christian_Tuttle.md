

P(a | b) = P(a,b) / P(b)

### Bayes' Rule

P(a,b) = P(a | b) × P(b) = P(b | a) × P(a)

P(a | b) = [P(b | a) × P(a)] / P(b)

- Want: P(cause | effect)

## Chain Rule

P(X₁, X₂, ..., Xₙ) = ∏ P(Xᵢ | X₁, ..., Xᵢ₋₁)

Examples:

P(a,b) = P(a) × P(b | a)

P(a,b,c) = P(a) × P(b | a) × P(c | b,a)

## Setting: Reasoning Under Uncertainty (Stochastic)

- Part 1: No randomness
- Part 2: Stochastic actions
- Part 3: Stochastic percepts

### This Week
- Interpreting Bayes nets

### Today
- Inference with Bayes nets
- Creating Bayes nets

### Next Up
- Fast and approximate inference
- Adding the brains in

### Goal

Infer reality from diagnostic percepts.

Example: Probability of a ghost in (1,2) if we heard distance 3.

---

# Joint Distribution for Dependent Random Variables

| T | W | P |
|---|---|---|
| Hot | Sun | 0.5 |
| Cold | Sun | 0.3 |
| Hot | Rain | 0.1 |
| Cold | Rain | 0.1 |

P(Sun) = 0.8

- Inference by enumeration

P(Cold | Rain) = 0.5

### Size of Joint Distribution

For n variables that have d values:

dⁿ → giant!

## Conditional Distribution

### P(W | Hot)

| W | P |
|---|---|
| Sun | 5/6 |
| Rain | 1/6 |

### P(W | Cold)

| W | P |
|---|---|
| Sun | 3/4 |
| Rain | 1/4 |

- Same distribution!

## Probabilistic Inference

Compute desired probabilities from known probabilities.

### Bayesian Network

```text
      Robbery       Fire
         \          /
          \        /
            Alarm
            /   \
           /     \
         John    Mary
```

P(J | R,F,A,M)

---

# Conditional Independence

John and robbery/fire are conditionally independent given alarm.

P(J | R,F,A,M) = P(J | A)

### Joint Probability

P(r, ¬f, a, ¬j, ¬m)

Using the chain rule:

P(r, ¬f, a, ¬j, ¬m) = P(r) × P(¬f | r) × P(a | r, ¬f) × P(¬j | a,r,¬f) × P(¬m | ¬j,a,r,¬f)

Using conditional independence:

P(r, ¬f, a, ¬j, ¬m) = P(r) × P(¬f) × P(a | r, ¬f) × P(¬j | a) × P(¬m | a)

## Inference with Bayesian Networks

P(F | j,m) = P(F,j,m) / P(j,m)

P(F | j,m) = α × P(F,j,m)

Marginalize over r and a:

P(F | j,m) = α × ∑(r,a) P(F,r,a,j,m)

Factorize:

P(F | j,m) = α × ∑(r,a) [P(F) × P(r) × P(a | F,r) × P(j | a) × P(m | a)]

Move independent terms outside the summation:

P(F | j,m) = α × P(F) × ∑(r) P(r) × ∑(a) [P(a | F,r) × P(j | a) × P(m | a)]
