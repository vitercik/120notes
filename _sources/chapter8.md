# Conditional expectation

```{contents}
:local:
```

*Conditional expectation* provides a way to compute the expected value of a RV given additional information about the occurrence of a specific event or the value of another variable. It refines the notion of expectation by incorporating this new information, enabling more precise predictions and insights into the behavior of RVs under specific conditions.

## Conditional expectation given an event

We begin with the definition of conditional expectation given an event.

```{admonition} Conditional expectation given an event

1. **Discrete Random Variable:** Let $ A $ be an event and $ Y $ a discrete random variable. The conditional expectation of $ Y $ given $ A $ is expressed as:

\begin{equation*}
\mathbb{E}[Y \mid A] = \sum_y y \mathbb{P}[Y = y \mid A] = \sum_y y \cdot \frac{\mathbb{P}[A \mid Y = y] \mathbb{P}[Y = y]}{\mathbb{P}[A]},
\end{equation*}
where the summation is taken over all possible values of $ Y $.

2. **Continuous Random Variable:** If $ A $ is an event and $ Y $ is a continuous random variable, then we replace the PMF $\mathbb{P}[Y = y]$ with the PDF $f_Y(y)$ and take an integral rather than a sum:

\begin{equation*}
\mathbb{E}[Y \mid A] = \int_{-\infty}^\infty y \cdot \frac{\mathbb{P}[A \mid Y = y] f_Y(y)}{\mathbb{P}[A]} \, dy.
\end{equation*}
```

Building off of this definition, the **Law of Total Expectation** is a natural extension of the Law of Total Probability.

```{admonition} Law of total expectation

If $ A_1, A_2, \dots, A_n $ partition the set of all possible outcomes, then:
\begin{equation*}
\mathbb{E}[Y] = \sum_{i=1}^n \mathbb{E}[Y \mid A_i] \mathbb{P}[A_i].
\end{equation*}
```


```{list-table} A tennis player is in a best-of-three match. The random variable $ Y $ represents the number of sets won. This table summarizes the joint PMF of the player's performance in the events he did or did not sleep well.
:header-rows: 1
:name: tennis

* - 
  - **$ Y = 0 $**
  - **$ Y = 1 $**
  - **$ Y = 2 $**
* - **Didn't sleep well**
  - $ 0.15 $
  - $ 0.30 $
  - $ 0.10 $
* - **Slept well**
  - $ 0.05 $
  - $ 0.20 $
  - $ 0.20 $
```

```{admonition} Example: Tennis match
:class: tip

Suppose a tennis player is in a best-of-three match. The random variable $ Y $ represents the number of sets won. The player's performance is influenced by whether they slept well the night before. The probabilities of winning 0, 1, or 2 sets under different sleep conditions are summarized in {numref}`tennis`.

**Question:** What is the expected number of sets won $\mathbb{E}[Y] $ given that the player slept well?

Let $ A $ represent the event of sleeping well. First, we compute $ \mathbb{P}[A] $, the probability of sleeping well:
\begin{equation*}
\mathbb{P}[A] = 0.05 + 0.20 + 0.20 = 0.45.
\end{equation*}

Next, we calculate the conditional probabilities of winning 0, 1, or 2 sets given $ A $:

\begin{align*}
\mathbb{P}[Y = 0 \mid A] &= \frac{\mathbb{P}[Y = 0 \text{ and } A]}{\mathbb{P}[A]} = \frac{0.05}{0.45},
\mathbb{P}[Y = 1 \mid A] &= \frac{\mathbb{P}[Y = 1 \text{ and } A]}{\mathbb{P}[A]} = \frac{0.20}{0.45},
\mathbb{P}[Y = 2 \mid A] &= \frac{\mathbb{P}[Y = 2 \text{ and } A]}{\mathbb{P}[A]} = \frac{0.20}{0.45}.
\end{align*}

Finally, we compute the conditional expectation $ \mathbb{E}[Y \mid A] $ using these probabilities:
\begin{equation*}
\mathbb{E}[Y \mid A] = 0 \cdot \mathbb{P}[Y = 0 \mid A] + 1 \cdot \mathbb{P}[Y = 1 \mid A] + 2 \cdot \mathbb{P}[Y = 2 \mid A].
\end{equation*}
Substituting the values:
\begin{equation*}
\mathbb{E}[Y \mid A] = 0 \cdot \frac{0.05}{0.45} + 1 \cdot \frac{0.20}{0.45} + 2 \cdot \frac{0.20}{0.45} = \frac{0.60}{0.45} = 1.333.
\end{equation*}
Thus, the expected number of sets won, given that the player slept well, is approximately 1.33.
```

```{admonition} Example: Tossing a coin
:class: tip

This is Example 9.1.9 from {cite}`Blitzstein19:Introduction`.

Suppose we toss a fair coin repeatedly. Define $ W_{HT} $ as the number of flips required to observe the pattern "HT" for the first time. For example, in the sequence $ \text{TTHHT} $, $ W_{HT} = 5 $.

**Question:** What is $ \mathbb{E}[W_{HT}] $?

We break $ W_{HT} $ into two components:
    - $ W_1 $: The number of flips until the first heads (H).
    - $ W_2 $: The additional number of flips required to observe the first tails (T) after the first heads.
Since $ W_1, W_2 \sim \text{FS}(\frac{1}{2}) $), we compute:
\begin{equation*}
\mathbb{E}[W_{HT}] = \mathbb{E}[W_1 + W_2] = \mathbb{E}[W_1] + \mathbb{E}[W_2] = 2 + 2 = 4.
\end{equation*}

---

Next, define $ W_{HH} $ as the number of flips required to observe the pattern "HH" for the first time. For example, in the sequence $ \text{TTTHTHH} $, $ W_{HH} = 7 $.

**Question:** What is $ \mathbb{E}[W_{HH}] $?

**Step 1: Define the goal.** Using the law of total expectation, we will compute $ \mathbb{E}[W_{HH}] $ based on the outcomes of the first tosses:

\begin{align*}
\mathbb{E}[W_{HH}] &= \mathbb{E}[W_{HH} \mid \text{1st two tosses are (H, H)}] \cdot \mathbb{P}[\text{1st two tosses are (H, H)}]\\
&+\mathbb{E}[W_{HH} \mid \text{1st two tosses are (H, T)}] \cdot \mathbb{P}[\text{1st two tosses are (H, T)}]\\
&+\mathbb{E}[W_{HH} \mid \text{1st toss is T}] \cdot \mathbb{P}[\text{1st toss is T}].
\end{align*}

**Step 2: Compute individual probabilities.**
- If the first two tosses are (H, H), then $ \mathbb{E}[W_{HH} \mid \text{1st tosses are (H, H)}] = 2 $.
- If the first two tosses are (H, T), then $ \mathbb{E}[W_{HH} \mid \text{1st tosses are (H, T)}] = 2 + \mathbb{E}[W_{HH}] $ (due to the memoryless property of the coin tosses).
- If the first toss is T, then $ \mathbb{E}[W_{HH} \mid \text{1st toss is T}] = 1 + \mathbb{E}[W_{HH}] $.

**Step 3: Solve for $ \mathbb{E}[W_{HH}] $.**
Substitute the values into the expectation formula:
\begin{equation*}
\mathbb{E}[W_{HH}] = 2 \cdot \frac{1}{4} + (2 + \mathbb{E}[W_{HH}]) \cdot \frac{1}{4} + (1 + \mathbb{E}[W_{HH}]) \cdot \frac{1}{2}.
\end{equation*}

Solving for $ \mathbb{E}[W_{HH}] $, we get that $\mathbb{E}[W_{HH}] = 6.$
```

## Conditional expectation given a random variable

Conditional expectation, given a random variable, is an important concept in probability. The notation $ \mathbb{E}[Y \mid X] $ represents the expectation of $ Y $ conditioned on $ X $. The goal in this section is to understand what this expression means and how it functions. As a first step, it is helpful to first understand $ \mathbb{E}[Y \mid X = x] $. Here, $ X = x $ represents the event that $X$ equals $x$. The expectation $ \mathbb{E}[Y \mid X = x] $ is the conditional expectation of $ Y $ given this event and can be determined using the conditional probability distribution of $ Y $ given $ X = x $. For a discrete random variable $ Y $, the conditional expectation $ \mathbb{E}[Y \mid X = x] $ is, by definition,

\begin{equation*}
\mathbb{E}[Y \mid X = x] = \sum_y y \cdot \mathbb{P}[Y = y \mid X = x].
\end{equation*}

For instance, if $ X $ is also discrete, this can be expressed using the joint and marginal probabilities:

\begin{equation*}
\mathbb{E}[Y \mid X = x] = \sum_y y \cdot \frac{\mathbb{P}[Y = y, X = x]}{\mathbb{P}[X = x]}.
\end{equation*}

Similarly, if $ X $ and $ Y $ are continuous random variables, the conditional expectation is given by:

\begin{equation*}
\mathbb{E}[Y \mid X = x] = \int_{-\infty}^\infty y \cdot \frac{f_{X,Y}(x, y)}{f_X(x)} \, dy,
\end{equation*}

where $ f_{X,Y}(x, y) $ is the joint probability density function of $ X $ and $ Y $, and $ f_X(x) $ is the marginal density of $ X $.

We will use the notation $ g(x) = \mathbb{E}[Y \mid X = x] $ to represent the conditional expectation of $ Y $ given $ X = x $. Intuitively, it provides the best prediction for the value of $ Y $, assuming that the value of $ X $ is known.

For example, let $ X $ represent a person's age and $ Y $ represent their maximum heart rate. The general rule of thumb is that a person’s maximum heart rate is 220 minus their age. Of course, this is just a rough estimate; some people’s maximum heart rate will be higher or lower. In other words, 220 minus age is our best guess for a person’s maximum heart rate. We can express this rule of thumb in terms of conditional expectation: for a 21-year-old, for example,

\begin{equation*}
\mathbb{E}[Y \mid X = 21] = \mathbb{E}[\text{maximum heart rate} \mid \text{21 years old}] = 199.
\end{equation*}

More generally,

\begin{equation*}
\mathbb{E}[Y \mid X = x] = \mathbb{E}[\text{maximum heart rate} \mid x \text{ years old}] = 220 - x = g(x).
\end{equation*}

We are now ready to define $\mathbb{E}[Y \mid X]$.

```{admonition} Example: Conditional expectation given a random variable

The *conditional expectation of $ Y $ given $ X $*, denoted $ \mathbb{E}[Y \mid X] $, is defined as the random variable $ g(X) $.
```

For example, if $ g(x) = x^2 $, then $ g(X) = X^2 $, meaning the conditional expectation is expressed as a function of $ X $. Importantly, $ \mathbb{E}[Y \mid X] $ is a function of the random variable $ X $, not of $ Y $.

To illustrate, we return to the case where $ X $ represents a person's age and $ Y $ represents their maximum heart rate:

\begin{equation*}
\mathbb{E}[Y \mid X] = \mathbb{E}[\text{maximum heart rate} \mid X \text{ years old}] = 220 - X = g(X).
\end{equation*}

```{admonition} Example: Breaking a stick
:class: tip

This is Example 9.2.4 from {cite}`Blitzstein19:Introduction`.


Suppose a stick of length 1 is broken at a random point $ X $, where $ X \sim \text{Uniform}(0, 1) $. Then, another breakpoint $ Y $ is chosen randomly from a uniform distribution over the interval $ (0, x) $. The goal is to compute $ \mathbb{E}[Y \mid X] $, the conditional expectation of $ Y $ given $ X $.

**Step 1: Determine $ g(x) $.** Given $ X = x $, the random variable $ Y $ is uniformly distributed over $ (0, x) $. For a uniform distribution, the expectation is simply the midpoint of the interval. Thus:
\begin{equation*}
g(x) = \mathbb{E}[Y \mid X = x] = \frac{x}{2}.
\end{equation*}

**Step 2: Express $ \mathbb{E}[Y \mid X] $ as a function of $ X $.**
By substituting $ X $ into the expression for $ g(x) $, we get:
\begin{equation*}
\mathbb{E}[Y \mid X] = g(X) = \frac{X}{2}.
\end{equation*}
```

### Properties of Conditional Expectation

1. **Dropping Independence**: If $ X $ and $ Y $ are independent, the conditional expectation $ \mathbb{E}[Y \mid X] $ simplifies to the unconditional expectation $ \mathbb{E}[Y] $. In other words, knowing $ X $ provides no additional information about $ Y $, so $ \mathbb{E}[Y \mid X] = \mathbb{E}[Y] $.
2. **Linearity**: Conditional expectation is linear, meaning that for two random variables $ Y_1 $ and $ Y_2 $,
$\mathbb{E}[Y_1 + Y_2 \mid X] = \mathbb{E}[Y_1 \mid X] + \mathbb{E}[Y_2 \mid X].$
3. **Adam's Law (Law of Iterated Expectations)**: The overall expectation of $ Y $ can be computed by taking the expectation of its conditional expectation:
$\mathbb{E}[\mathbb{E}[Y \mid X]] = \mathbb{E}[Y].$

```{admonition} Example: Time until first goal in soccer
:class: tip

Consider a soccer team that takes shots following a Poisson process with a rate of $ \lambda $ shots per minute. Each shot results in a goal with a probability $ p $. Let $ Y $ represent the number of minutes until the first goal. The task is to determine $ \mathbb{E}[Y] $, the expected time until the first goal.

Hint: Let $ N $ be the number of shots taken until the first goal (including the shot that scores). Using Adam’s law ($ \mathbb{E}[Y] = \mathbb{E}[\mathbb{E}[Y \mid N]] $), we compute $ \mathbb{E}[Y] $ step by step.


**Step 1: Compute $ g(n) = \mathbb{E}[Y \mid N = n] $.** Given $ N = n $, the time $ Y $ until the first goal follows a Gamma distribution with shape parameter $ n $ and rate parameter $ \lambda $. The expected value of a Gamma random variable is given by the formula $ \frac{n}{\lambda} $. Therefore:
\begin{equation*}
g(n) = \mathbb{E}[Y \mid N = n] = \frac{n}{\lambda}.
\end{equation*}

**Step 2: Compute $ \mathbb{E}[Y \mid N] $ as a function of $ N $.** Replacing $ n $ with $ N $, the conditional expectation becomes:
\begin{equation*}
g(N) = \mathbb{E}[Y \mid N] = \frac{N}{\lambda}.
\end{equation*}

**Step 3: Use Adam's law $ \mathbb{E}[Y] $.**
Using Adam's law ($ \mathbb{E}[Y] = \mathbb{E}[\mathbb{E}[Y \mid N]] $), we substitute $ g(N) $:
\begin{equation*}
\mathbb{E}[Y] = \mathbb{E}[g(N)] = \mathbb{E}\left[\frac{N}{\lambda}\right] = \frac{1}{\lambda} \mathbb{E}[N].
\end{equation*}

**Step 4: Compute $ \mathbb{E}[N] $.** The random variable $ N $, the number of shots until the first goal, follows a first success distribution with success probability $ p $. Therefore, the expected number of trials until the first success is $ \mathbb{E}[N] = \frac{1}{p} $.

Substituting $ \mathbb{E}[N] $ into the expression for $ \mathbb{E}[Y] $, we find:
\begin{equation*}
\mathbb{E}[Y] = \frac{1}{\lambda} \cdot \frac{1}{p} = \frac{1}{\lambda p}.
\end{equation*}
```