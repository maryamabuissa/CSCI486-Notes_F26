# Lecture Notes: Probabilistic Inference & Bayes Nets

> **Class Intro:** Start of class talking about last week and mid-semester reflection/feedback.

## Inference / Probabilistic Inference

* **Definition:** Calculate a probability that may be hard to calculate.
* **Application:** Answers questions like what is the probability a ghost is in $(1,2)$ with a noise (distance) of two.

### Fire, Robbery, Alarm Example

If you have a Bayes Net like the fire, robbery, alarm example:

* Last week we wanted the probability of fire given John and Mary called.
* We rewrite: alpha times the sum over alarm, robbery of the probability $P(F,r,a,j,m)$

$$
\alpha \sum_{a,r} P(F,r,a,j,m)
$$

* Simplify using the chain rule: alpha sum of $a,r$ $P(F) P(r \mid F) P(a \mid r,f) P(j \mid a) P(m \mid a)$

$$
\alpha \sum_{a,r} P(F) P(r \mid F) P(a \mid r,f) P(j \mid a) P(m \mid a)
$$

* *Note:* John and Mary only care about alarm, not fire or robbery.
* This is **inference by enumeration / direct inference**.

## Bayes Nets

* Provide a systematic way to represent a joint distribution (think back to table of all possible values) through simple conditional distributions like the above.
* This allows us to do the simplification.
* **Key Takeaway:** The reason we do Bayes Nets is to get to the simplification part.

## How to Make a Bayes Net

### Two Relationship Types a Variable Might Have

1. **Causal relationship**
   * Fire causes alarm (i.e., they are not independent).
2. **Diagnostic relationship**
   * *Question:* Does Mary calling cause the alarm?
   * *Answer:* No, but they are not independent. We say Mary has a **diagnostic relationship** to the alarm.

## Example of Creating a Bayes Net

### Steps

1. Choose an order of nodes.
2. For each node $x$, add the minimal set of parents such that the probability of $x$ given everything so far is the probability of $x$ given the parents. In other words, the parents explain the child.

### Example 1: Order `F, R, A, J, M`

* **Add node for Fire:** has no parents yet.
* **Add node for Robbery:** independent, needs no parents.
* **Add node Alarm:** it depends on both fire and robbery and neither can be removed, so add both to its parent set.
* **Add node for John:** smallest number of parents is just the alarm.
* **Add node for Mary:** same for Mary.

### Board Work for Another Order

* `M, J, R, F, A`
* `M, J, A, R, F`

> **Summary:** All this to say that the first nodes should be the ones that influence the most other nodes. This makes smaller nets and is called **causal order**.
