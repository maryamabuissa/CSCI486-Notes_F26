# CSCI 486 10/23 - Bayes Nets, Markov Models, Filtering

- **Robbery**: $P(R) = 0.001$
- **Fire**: $P(F) = 0.002$

```
Robbery    Fire
   \        /
    v      v
     Alarm
   /      \
  v       v
John     Mary
```

| R | F | P(A)  |
|---|---|-------|
| T | T | 0.95  |
| T | F | 0.25  |
| F | T | 0.94  |
| F | F | 0.001 |

| A | P(J) |
|---|------|
| T | 0.9  |
| F | 0.05 |

| A | P(M) |
|---|------|
| T | 0.7  |
| F | 0.01 |

$P(M \mid j)$

|           |           |
|-----------|-----------|
| R = T     | R = F     |
| F = T     | F = T     |
| A = F     | A = T     |
| J = T     | J = T     |
| M = T     | M = T     |
| w * 0.05  | w = 0.9   |
| w = 0.05  |           |

---

**Inference Summary from 10/21:**

- Exact inference - enumeration
- approximate inference - sampling

## Markov Models: Factoring Time Into Inferencing**

**Ex)** Your friend is hiking in the mountains. You want to know if it is raining where they are. You can only measure the height of the river.

- $E_1, E_2, \ldots,$ Evidence
- $X_1$ - is it raining at t = 1?
- $X_2$
- $X_3$
- .
- .
- .

has a transition model: $P(X_t \mid X_{t-1})$ <- only the most recent timestep

Assume stationarity: transition probabilities don't change

**Markov Assumption:** 

$$P(X_t \mid X_{0:t-1}) = P(X_t \mid X_{t-1})$$

**Markov Sensor Assumption:**

$$P(E_t \mid X_{0:t}, E_{0:t-1}) = P(E_t \mid X_t)$$

- Evidence only relates to current state of the world

---

**Joint Distribution**:

$$P(X_0, X_1, \ldots, X_t) = P(X_0)\,P(X_1 \mid X_0)\,P(X_2 \mid X_{0:1}) \ldots$$

$$= P(X_0) \prod_{i=1..t} P(X_i \mid X_{i-1}$$

Like a Bayes Net but goes on forever

Each Evidence X pair is a Bayes Net B,

$$B_1 \rightarrow B_2 \rightarrow B_3 \rightarrow \ldots$$

**Inference Tasks:**

- Filtering: $P(X_t \mid e_{1:t})$
- Prediction: $P(X_{t+k} \mid e_{t:1})$
- Smoothing: $P(X_k \mid e_{1:t})$, $0 \le k < t$
- Most Likely Explaination: $\underset{X_{1:t}}{\operatorname{argmax}}\,\big(P(x_{1:t} \mid e_{1:t})\big)$

**Idea of Filtering:** Maintain and update the model at every timestep


