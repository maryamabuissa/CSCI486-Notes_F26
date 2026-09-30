## Adversarial Search Recap
*   Search involves two players: one "max" and one "min".
*   Each player attempts to get their best possible score while ensuring the other player does not achieve their best outcome.
*   Alpha-Beta pruning pseudo code from previous class time.

## Complex Game Playing Formats
Standard algorithms do not natively know how to handle the following formats:
*   Infinite game trees
*   More than 2 players
*   Games with subjective goal states
*   Randomness
*   Non-zero-sum games

### Focus Solutions
*   **More than 2 players:** Add a level for each player and record utilities separately.
*   **Non-zero-sum games:** Keep track of utilities separately for each player, making sure that each player maximizes their own utility.

## Randomness & Stochastic Games
*   Chance gets its own turn in the game tree.
*   Chance does not have any utility of its own because it is based purely on random chance (average case).
*   Probability ranges from 0 to 1.
*   **Probability Examples:**
    *   D6 (six-sided die): Rolling a 1 with probability (wp) 1/6, rolling a 2 wp 1/6.
    *   Loaded coin: Heads (H) wp 60%, Tails (T) wp 40%.
<img width="4000" height="1848" alt="image" src="https://github.com/user-attachments/assets/5d48cbac-a6ba-419e-827e-6779122ee22f" />

## Expectimax Search
*   **Expected value:** Calculated as the sum of the probability of a number occurring multiplied by the number itself.
*   <img width="4000" height="1848" alt="image" src="https://github.com/user-attachments/assets/af859108-4387-4d27-9d13-30090ab3ad2c" />
*   <img width="4000" height="1848" alt="image" src="https://github.com/user-attachments/assets/d563962d-6560-4cca-82dd-9ba51b2bb6cd" />

*   **Pruning limitation:** You cannot prune these trees because all chance values have an effect on the final outcome.

## Informed Search & Pruning using Domain Knowledge
*   Use lookup tables for common situations.
*   Use approximate evaluation to estimate the value of non-terminal nodes by searching *deep enough*.
