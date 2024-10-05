# Conditional probability

```{contents}
:local:
```

## Definition and intuition

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

```{admonition} Example: Tossing coins.
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

## Bayes’ rule and the law of total probability

In this section, we will cover two famous tools for calculating conditional probabilities: Bayes’ rule and the law of total probability.

```{admonition} Bayes' rule.
Bayes’ rule tells us that

\begin{equation*}

\mathbb{P}[A \mid B] = \frac{\mathbb{P}[B \mid A] \mathbb{P}[A]}{\mathbb{P}[B]}.

\end{equation*}
```

This fact follows simply from the observation that

1. $\mathbb{P}[A \mid B] = \frac{\mathbb{P}[A \cap B]}{\mathbb{P}[B]}$, which means that $\mathbb{P}[A \cap B] = \mathbb{P}[A \mid B]\mathbb{P}[B]$.
2. Moreover, $\mathbb{P}[B \mid A] = \frac{\mathbb{P}[A \cap B]}{\mathbb{P}[A]}$, which means that $\mathbb{P}[A \cap B] = \mathbb{P}[B \mid B]\mathbb{P}[A]$.

As a result, $\mathbb{P}[A \mid B]\mathbb{P}[B] = \mathbb{P}[B \mid B]\mathbb{P}[A]$, and Bayes’ rule follows immediately.

To apply Bayes’ rule it will often be useful to use the *law of total probability*.

```{figure} images/LOTP.png
---
name: LOTP
width: 400px
align: center
---

Visualization of the law of total probability. This is Figure 2.3 from {cite}`Blitzstein19:Introduction`.
```

```{admonition} Law of total probability (LOTP).
Suppose $A_1, \dots, A_n$ *partition* sample space $S$, which means that they're disjoint their union is $S$, as in {numref}`Figure {number} <LOTP>`. The law of total probability tells us that

\begin{equation*}

\mathbb{P}[B] = \sum_{i = 1}^n \mathbb{P}[B \cap A_i] = \sum_{i = 1}^n \mathbb{P}[B \mid A_i] \mathbb{P}[A_i].

\end{equation*}
```

```{admonition} Example: The importance of scoring first.
:class: tip

This example is from {cite}`Severini20:Analytic`.

Using data from the English Premier League, we can calculate the probability that the home team wins by considering different scenarios regarding which team scores first. In particular, we can use LOTP to derive the following formula:

\begin{align*}
&\mathbb{P}[\text{home team wins}]\\
=\, &\mathbb{P}[\text{home team wins} \mid \text{home team scores first}] \cdot \mathbb{P}[\text{home team scores first}]\\
+\, &\mathbb{P}[\text{home team wins} \mid \text{visitor scores first}] \cdot \mathbb{P}[\text{visitor scores first}]\\
+\, &\mathbb{P}[\text{home team wins} \mid \text{neither team scores first}] \cdot \mathbb{P}[\text{neither team scores first}].
\end{align*}

From the EPL data, we have the following values:

- $\mathbb{P}[\text{home team wins} \mid \text{home team scores first}] = 0.718$
- $\mathbb{P}[\text{home team scores first}] = 0.534$
- $\mathbb{P}[\text{home team wins} \mid \text{visitor scores first}] = 0.178$
- $\mathbb{P}[\text{visitor scores first}] = 0.39$
- $\mathbb{P}[\text{home team wins} \mid \text{neither team scores first}] = 0$
- $\mathbb{P}[\text{neither team scores first}] = 0.076$

Using these values, the total probability of the home team winning is: $0.718 \cdot 0.534 + 0.178 \cdot 0.39 + 0 \cdot 0.076 = 0.453$.
```

We’ll now work through an example that combines Bayes’ rule and LOTP. Suppose we have a population of 10 sick and 90 healthy people, as in the following figure.
```{figure} images/sick1.png
---
name: sick1
width: 250px
align: center
---

10 sick and 90 healthy people.
```

If we chose a random person from this pool, 

\begin{equation*}
\mathbb{P}[\text{random person is sick}] = \frac{\text{(# sick)}}{\text{# total people}} = \frac{10}{100}.
\end{equation*}

Now, suppose that we test this population. Of the 10 sick people, suppose that 9 test positive, and of the 90 healthy people, another 9 test positive, as in the following figure.
```{figure} images/sick2.png
---
name: sick2
width: 280px
align: center
---

Results of a test.
```

If we chose a random sick person from this pool, the probability they test positive is:

\begin{align*}
\mathbb{P}[\text{random person tests positive} \mid \text{they’re sick}] &= \frac{\text{(# people who are sick and test positive)}}{\text{(# sick people)}}\\
&= \frac{9}{10}.
\end{align*}

Meanwhile, suppose we chose a random person from this pool who tested positive, as highlighted in the following figure.
```{figure} images/sick3.png
---
name: sick3
width: 280px
align: center
---

Highlighting the people who tested positive, both sick and healthy.
```

The probability they’re actually sick is equal to

\begin{align*}
\mathbb{P}[\text{random person is sick} \mid \text{they test positive}] &= \frac{\text{(# people who are sick and test positive)}}{\text{(# people who test positive)}}\\
&= \frac{9}{18} = \frac{1}{2}.
\end{align*}

In other words, even if you tested positive, you only have a 50-50 chance of being sick! This surprising fact is called the “false positive paradox.”

Another way to express this probability is via Bayes’ rule:

\begin{align*}

\mathbb{P}[\text{random person is sick} \mid \text{they test positive}] &= \frac{\mathbb{P}[\text{positive} \mid \text{sick}]\mathbb{P}[\text{sick}]}{\mathbb{P}[\text{positive}]}\\
&= \frac{\frac{9}{10} \cdot \frac{1}{10}}{\frac{18}{100}} = \frac{1}{2}.

\end{align*}

To get an intuition for the false positive paradox, we will expand out the denominator of this equation using the LOTP:

\begin{align*} &\mathbb{P}[\text{random person is sick} \mid \text{they test positive}]\\
=\, &\frac{\mathbb{P}[\text{positive} \mid \text{sick}]\mathbb{P}[\text{sick}]}{\mathbb{P}[\text{positive} \mid \text{sick}]\mathbb{P}[\text{sick}] + \mathbb{P}[\text{positive} \mid \text{healthy}]\mathbb{P}[\text{healthy}]}.

\end{align*}

We can see that as $\mathbb{P}[\text{healthy}]$ gets larger and larger, the $\mathbb{P}[\text{random person is sick} \mid \text{they test positive}]$ will get smaller and smaller. Intuitively, once a significant fraction of the population is healthy, a relatively large number will test positive compared to the true positives, and $\mathbb{P}[\text{random person is sick} \mid \text{they test positive}]$ will be driven to a small number.

We'll finish this section with a few more examples.

```{admonition} Example
:class: tip

This example is from {cite}`Ross18:First`.

Imagine you're going away for the weekend and ask your roommate to water your plant. If your roommate forgets to water the plant, there's a 90% chance it will be dead by the time you return. If your roommate remembers to water the plant, there's only a 10% chance it will die. You're fairly confident that your roommate will remember to water it, estimating the likelihood at 85%.

**Question 1:** What is the probability that your plant will still be alive when you return?

**Step 1: Define the events.** Let's define the events:

- $ R $: Your roommate waters the plant.
- $ D $: The plant is dead.

**Step 2: Define the goal.** To answer the question, we want to calculate $ \mathbb{P}[D^c] $, the probability that the plant is *not* dead, using the Law of Total Probability:

\begin{equation*}
\mathbb{P}[D^c] = \mathbb{P}[D^c \mid R] \cdot \mathbb{P}[R] + \mathbb{P}[D^c \mid R^c] \cdot \mathbb{P}[R^c]
\end{equation*}

**Step 3: Compute the individual probabilities.** We are given the following information:

- $ \mathbb{P}[D \mid R^c] = 0.9 $, so $ \mathbb{P}[D^c \mid R^c] = 0.1 $.
- $ \mathbb{P}[D \mid R] = 0.1 $, so $ \mathbb{P}[D^c \mid R] = 0.9 $.
- $ \mathbb{P}[R] = 0.85 $, meaning your confidence in your roommate remembering is 85%.

**Step 4: Plug in to get the final answer.** Now we can calculate the probability that the plant is alive:

\begin{equation*}
\mathbb{P}[D^c] = 0.9 \cdot 0.85 + 0.1 \cdot 0.15 = 0.78.
\end{equation*}

---

**Question 2:** You return home to find your plant is dead. What is the probability that your roommate forgot to water it?

In other words, we want to calculate $ \mathbb{P}[R^c \mid D] $, the probability that your roommate forgot, given that the plant is dead.

Using Bayes' Rule:

\begin{equation*}
\mathbb{P}[R^c \mid D] = \frac{\mathbb{P}[D \mid R^c] \cdot \mathbb{P}[R^c]}{\mathbb{P}[D]} = \frac{\mathbb{P}[D \mid R^c] \cdot \mathbb{P}[R^c]}{1 - \mathbb{P}[D^c]}
\end{equation*}

From the previous information, we know:

- $ \mathbb{P}[D \mid R^c] = 0.9 $
- $ \mathbb{P}[R^c] = 0.15 $ (since $ \mathbb{P}[R] = 0.85 $)
- $ \mathbb{P}[D^c] = 0.78 $, so $ \mathbb{P}[D] = 1 - 0.78 = 0.22 $

Now, plugging in the values:

\begin{equation*}
\mathbb{P}[R^c \mid D] = \frac{0.9 \cdot 0.15}{0.22} \approx 0.61.
\end{equation*}
```

```{admonition} Example
:class: tip

This example is from {cite}`Harchol23:Introduction`.

Imagine a bomb detector system where the alarm lights up with high accuracy if a bomb is present. Specifically, if a bomb is there, the alarm goes off with a probability of 0.99. However, the system isn't perfect, and if no bomb is present, the alarm still (incorrectly) lights up with a probability of 0.05. Additionally, suppose that the likelihood of a bomb being present in any given situation is 0.1.

**Question:** Given that the alarm has gone off, what is the probability that there is actually a bomb?

**Step 1: Define the events.**

- $ A $: The alarm goes off.
- $ B $: A bomb is present.

**Step 2: Define the goal.** To answer the question, we need to calculate $ \mathbb{P}[B \mid A] $, the probability that a bomb is present given that the alarm has gone off. We can use Bayes' Rule for this calculation:

\begin{equation*}
\mathbb{P}[B \mid A] = \frac{\mathbb{P}[A \mid B] \cdot \mathbb{P}[B]}{\mathbb{P}[A]}
\end{equation*}

**Step 3: Compute the individual probabilities.** From the given information, we know:

- $ \mathbb{P}[A \mid B] = 0.99 $ (the probability that the alarm goes off if a bomb is present).
- $ \mathbb{P}[A \mid B^c] = 0.05 $ (the probability that the alarm goes off when there is no bomb).
- $ \mathbb{P}[B] = 0.1 $ (the probability that a bomb is present).
- $ \mathbb{P}[B^c] = 0.9 $ (the probability that there is no bomb).

**Step 4: Plug in to get the final answer.** Now, we can calculate the desired probability:

\begin{equation*}
\mathbb{P}[B \mid A] = \frac{\mathbb{P}[A \mid B] \cdot \mathbb{P}[B]}{\mathbb{P}[A \mid B] \cdot \mathbb{P}[B] + \mathbb{P}[A \mid B^c] \cdot \mathbb{P}[B^c]}.
\end{equation*}

Substituting the known values:

\begin{equation*}
\mathbb{P}[B \mid A] = \frac{0.99 \cdot 0.1}{0.99 \cdot 0.1 + 0.05 \cdot 0.9} = \frac{0.099}{0.099 + 0.045} = \frac{0.099}{0.144} \approx 0.6875.
\end{equation*}
```