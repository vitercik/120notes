# Conditional probability

```{contents}
:local:
```

When faced with new information, it is often necessary to adjust our beliefs or probabilities accordingly. This is where the concept of **conditional probability** comes into play. Conditional probability allows us to quantify the likelihood of an event $ A $, given that another event $ B $ has already occurred. It is defined mathematically as:

\begin{equation*}
\mathbb{P}[A \mid B] = \frac{\mathbb{P}[A \cap B]}{\mathbb{P}[B]} \quad \text{for} \quad \mathbb{P}[B] > 0.
\end{equation*}

In essence, this formula narrows the probability of $ A $ by focusing only on the outcomes in which $ B $ happens, as the following discussions illustrate.

**Finite sample space: Visualizing outcomes.** (This is Intuition 2.2.3 from {cite}`Blitzstein19:Introduction`.) The leftmost panel of {numref}`Figure {number} <pebble>` illustrates a finite sample space where each possible outcome is represented as a pebble.
```{figure} images/pebble.png
---
name: pebble
width: 600px
align: center
---

Visualization of $\mathbb{P}[A \mid B]$. This is Figure 2.1 from {cite}`Blitzstein19:Introduction`.
```
It also illustrates two events $A$ and $B$, which are sets of outcomes, i.e., sets of pebbles. Suppose we know that event $B$ occurred, which means we can disregard all outcomes in $B^c$, as in the middle panel of {numref}`Figure {number} <pebble>`. To compute $\mathbb{P}[A \mid B]$ (the probability $A$ occurs given that $B$ occurred), we normalize the probabilities of the remaining outcomes to maintain a total probability of 1, as in the rightmost panel of {numref}`Figure {number} <pebble>`. This normalization explains the denominator of $\mathbb{P}[A \mid B] = \frac{\mathbb{P}[A \cap B]}{\mathbb{P}[B]}$. If all outcomes are equally likely, then $\mathbb{P}[A \mid B] = \frac{1}{4}$.

**Rolling a die.**
Imagine rolling a die repeatedly, as in the following figure.

```{figure} images/frequentist.png
---
name: frequentist
width: 350px
align: center
---

Rolling a die. Rolls where the number is at least 4 are circled and rolls where the number is odd are underlined.
```

Suppose $ B $ is the event that the outcome is greater than or equal to 4 (marked by a circle in {numref}`Figure {number} <frequentist>`), and $ A $ is the event that the outcome is odd (underlined). By observing the rolls where $ B $ occurs, we can estimate the probability that $ A $ also occurs. In the example above, the fraction of times $ A $ occurs when $ B $ happens is $\frac{2}{6}$. This is a (frequentist) intuition that helps explain why $\mathbb{P}[A \mid B] = \frac{1}{3}$.

```{admonition} Example: Bears vs. Packers.
:class: tip

This example is from {cite}`Severini20:Analytic`.

We can generalize the coin-flipping example to more practical “experiments”, such as football games where the Bears play the Packers at home. For intuition, as in the coin-flipping example, we can interpret the probability of an event as the long-run relative frequency of the event happening over a long sequence of games. Let $ A $ be the event that the Bears win. If, over this long sequence of games, $A$ occurs about 25% of the time, we can interpret this as meaning that $ \mathbb{P}[A] = 0.25 $. Let $B$ be the event that the Bears' quarterback throws four interceptions during the at-home game. Suppose that, in our long sequence of games *in which the Bears’ quarterback throws an interception* (i.e., $B$ occurs), the Bears win about 5% of the time. This would mean that the conditional probability of the Bears winning, given that their quarterback throws four interceptions, drops to $ \mathbb{P}[A \mid B] = 0.05 $: the interceptions negatively affect their chances of winning.
```

```{admonition} Tossing coins.
:class: tip

Suppose we toss a coin twice. We will explore conditional probability through two scenarios:
**Question:** What is the probability that both flips land on heads, given that the first flip lands on heads?

The sample space is $ S = \{(H,H), (H,T), (T,H), (T,T)\} $. The event that both flips land on heads is $ A = \{(H,H)\} $, and the event that the first flip lands on heads is $ B = \{(H,H), (H,T)\} $. Therefore, $\mathbb{P}[B] = \frac{1}{2}$ and $\mathbb{P}[A \cap B] = \frac{|\{HH\}|}{|S|} = \frac{1}{4}$. Therefore,
   \begin{equation*}
   \mathbb{P}[A \mid B] = \frac{\mathbb{P}[A \cap B]}{\mathbb{P}[B]} = \frac{1/4}{1/2} = \frac{1}{2}.
   \end{equation*}

**Question:** What is the probability that both flips land on heads, given that at least one flip lands on heads?

The event that at least one flip lands on heads is $ C = \{(H,H), (H,T), (T,H)\} $. The conditional probability is:
   \begin{equation*}
   \mathbb{P}[A \mid C] = \frac{\mathbb{P}[A \cap C]}{\mathbb{P}[C]} = \frac{1/4}{3/4} = \frac{1}{3}.
   \end{equation*}
```

It is important to keep in mind that conditional probabilities still obey the basic rules of probability. For example, $ \mathbb{P}[A \mid B] = 1 - \mathbb{P}[A^c \mid B] $. This means that if the probability of the Bears winning after their quarterback throws four interceptions is $ 0.05 $, the probability of them *not* winning given the same information is $ 0.95 $.