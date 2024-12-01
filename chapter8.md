# Conditional expectation

```{contents}
:local:
```

*Conditional expectation* provides a way to compute the expected value of a RV given additional information about the occurrence of a specific event or the value of another variable. It refines the notion of expectation by incorporating this new information, enabling more precise predictions and insights into the behavior of RVs under specific conditions.

For example, while $\mathbb{E}[\text{final exam grade}]$ would tell us, for a randomly chosen person the class, what we should expect their final exam grade to be, 
\begin{align*}
&\mathbb{E}[\text{final exam grade} \mid \text{used ChatGPT on the homework}] \text{ and}&\\
&\mathbb{E}[\text{final exam grade} \mid \text{didn't use ChatGPT on the homework}]
\end{align*}
would tell us what we could expect a student's final exam score to be based on whether they used ChatGPT on the homework 😉. Of course, we can anticipate that the former will be significantly lower than the latter.

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

### Properties of conditional expectation

1. **Dropping Independence**: If $ X $ and $ Y $ are independent, the conditional expectation $ \mathbb{E}[Y \mid X] $ simplifies to the unconditional expectation $ \mathbb{E}[Y] $. In other words, knowing $ X $ provides no additional information about $ Y $, so $ \mathbb{E}[Y \mid X] = \mathbb{E}[Y] $.
2. **Linearity**: Conditional expectation is linear, meaning that for two random variables $ Y_1 $ and $ Y_2 $,
$\mathbb{E}[Y_1 + Y_2 \mid X] = \mathbb{E}[Y_1 \mid X] + \mathbb{E}[Y_2 \mid X].$
3. **Adam's Law (Law of Iterated Expectations)**: The overall expectation of $ Y $ can be computed by taking the expectation of its conditional expectation:
$\mathbb{E}[\mathbb{E}[Y \mid X]] = \mathbb{E}[Y].$

```{admonition} Example: Time until first goal in soccer
:class: tip

Suppose a soccer team that takes shots following a Poisson process with a rate of $ \lambda $ shots per minute. Each shot results in a goal with a probability $ p $. Let $ Y $ represent the number of minutes until the first goal. The task is to determine $ \mathbb{E}[Y] $, the expected time until the first goal.

Hint: Let $ N $ be the number of shots taken until the first goal (including the shot that scores). Using Adam’s law ($ \mathbb{E}[Y] = \mathbb{E}[\mathbb{E}[Y \mid N]] $), we compute $ \mathbb{E}[Y] $ step by step.


**Step 1: Compute $ g(n) = \mathbb{E}[Y \mid N = n] $.** Given $ N = n $, the time $ Y $ until the first goal follows a Gamma distribution with shape parameter $ n $ and rate parameter $ \lambda $. The expected value of a Gamma random variable is given by the formula $ \frac{n}{\lambda} $. Therefore:
\begin{equation*}
g(n) = \mathbb{E}[Y \mid N = n] = \frac{n}{\lambda}.
\end{equation*}

**Step 2: Plug in $ N $.** Replacing $ n $ with $ N $, the conditional expectation becomes:
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

## Conditional variance

Conditional variance helps us understand the variability of a RV $Y$ within specific contexts or subgroups defined by another RV $X$. This is valuable because it allows us to distinguish between variability due to inherent randomness within groups as well as differences across groups.

```{admonition} Conditional variance
The **conditional variance** of $ Y $ given $ X $, denoted as $\text{Var}(Y \mid X)$, is defined as $\text{Var}(Y \mid X) = \mathbb{E}[Y^2 \mid X] - \mathbb{E}[Y \mid X]^2.$
```

**Eve's Law** connects the total variance of $ Y $ to both the conditional variance of $ Y $ given $ X $ and the variance of the conditional expectation of $ Y $. It is stated as:
\begin{equation*}
\text{Var}(Y) = \mathbb{E}[\text{Var}(Y \mid X)] + \text{Var}(\mathbb{E}[Y \mid X]).
\end{equation*}
Here, the first term, $\mathbb{E}[\text{Var}(Y \mid X)]$, captures the average variability within groups defined by $ X $, while the second term, $\text{Var}(\mathbb{E}[Y \mid X])$, measures the variability of group means.

Eve’s law is easier to work with if we define the following functions:
- $ h(x) = \text{Var}(Y \mid X = x) $: The variance of $ Y $ for a specific value of $ X = x $.
- $ h(X) = \text{Var}(Y \mid X) $: The conditional variance of $ Y $ given $ X $, varying across values of $ X $.
Using $ h(X) $ and $ g(X) = \mathbb{E}[Y \mid X] $, Eve's Law can also be rewritten as $\text{Var}(Y) = \mathbb{E}[h(X)] + \text{Var}(g(X)).$

We illustrate the intuition behind Eve’s law with an example involving Olympic gymnastics teams, where:
- $ X $ represents the country.
- $ Y $ represents the height of gymnasts.

There are two sources of variation in the height $ Y $:
1. **Within-group variation**: $\mathbb{E}[\text{Var}(Y \mid X)] = \mathbb{E}[h(X)]$
    - Within each country, people have different heights. The average variation in height within each country, $\mathbb{E}[\text{Var}(Y \mid X)]$, is the *within-group variation*.
2. **Between-group variation**: $\text{Var}(\mathbb{E}[Y \mid X]) = \text{Var}(g(X))$
    - Across countries, the average height is different. This variation in the average heights across countries, $\text{Var}(\mathbb{E}[Y \mid X])$, is the *between-group* variation.
In this context, Eve's Law explains how the total variance in gymnast heights combines the within-group and between-group components.

## Adam and Eve examples

```{admonition} Example: Revenue of a store
:class: tip

This is Example 9.6.1 from {cite}`Blitzstein19:Introduction`.

Consider a store where the number of customers $ N $ visiting on a given day is random. The key details are:
-  $ N $, the number of customers, has a mean of $ \mathbb{E}[N] = 1000 $ and a variance of $ \text{Var}(N) = 100 $.
-  Each customer spends a random amount $ Y_j $, where:
  - $ Y_1, Y_2, \dots $ are independent and identically distributed.
  - The spending per customer has a mean of $ \mathbb{E}[Y_j] = 5 $ and a variance of $ \text{Var}(Y_j) = 3 $.
- The total revenue $ Y $ for the day is the sum of the spending by all customers:
    \begin{equation*}
    Y = \sum_{j=1}^N Y_j.
    \end{equation*}

**Question:** What is $\mathbb{E}[Y]$?

**Step 1: Define the goal.** The total revenue $ Y $ depends on the random number of customers $ N $. Using the Adam’s law, we can express $ \mathbb{E}[Y] $ as $\mathbb{E}[Y] = \mathbb{E}[\mathbb{E}[Y \mid N]] = \mathbb{E}[g(N)],$ where $ g(N) = \mathbb{E}[Y \mid N] $ is the expected total revenue given $ N $ customers.

**Step 2: Compute $ g(n) $.** When the number of customers is fixed at $ N = n $, the total revenue is:
\begin{equation*}
g(n) = \mathbb{E}[Y \mid N = n] = \mathbb{E}\left[\sum_{j=1}^n Y_j \mid N = n\right].
\end{equation*}
Since the $ Y_j $'s are independent and identically distributed:
\begin{equation*}
g(n) = \mathbb{E}[Y_1] + \mathbb{E}[Y_2] + \cdots + \mathbb{E}[Y_n] = n \cdot \mathbb{E}[Y_j].
\end{equation*}
Substituting $ \mathbb{E}[Y_j] = 5 $, we have that $g(n) = 5n.$

**Step 3: Plug in $N$.** Replacing $ n $ with the random variable $ N $, the conditional expectation becomes $g(N) = \mathbb{E}[Y \mid N] = 5N.$

**Step 4: Apply Adam's Law.** Using Adam’s law, we compute $ \mathbb{E}[Y] $:
\begin{equation*}
\mathbb{E}[Y] = \mathbb{E}[\mathbb{E}[Y \mid N]] = \mathbb{E}[g(N)] = \mathbb{E}[5N].
\end{equation*}
Since $ 5 $ is a constant, we can factor it out: $\mathbb{E}[Y] = 5 \cdot \mathbb{E}[N].$
Finally, substituting $ \mathbb{E}[N] = 1000 $, we have that $\mathbb{E}[Y] = 5 \cdot 1000 = 5000.$

---

**Question**: What is $\text{Var}(Y)$?

**Step 1: Define the goal.** Using Eve's Law, we decompose $ \text{Var}(Y) $ into two components:
\begin{equation*}
\text{Var}(Y) = \mathbb{E}[h(N)] + \text{Var}(g(N)),
\end{equation*}
where $ h(N) = \text{Var}(Y \mid N) $ is the conditional variance of $ Y $ given $ N $, and $ g(N) = \mathbb{E}[Y \mid N] $ is the expected total revenue given $ N $.

**Step 2: Compute $ h(n) = \text{Var}(Y \mid N = n) $.** When the number of customers is fixed at $ N = n $, the total revenue is:
\begin{equation*}
\text{Var}(Y \mid N = n) = \text{Var}\left(\sum_{j=1}^n Y_j \mid N = n\right).
\end{equation*}
Since the spending amounts $ Y_j $ are independent:
\begin{equation*}
\text{Var}(Y \mid N = n) = \text{Var}\left(\sum_{j=1}^n Y_j\right) = \sum_{j=1}^n \text{Var}(Y_j).
\end{equation*}
Substituting $ \text{Var}(Y_j) = 3 $, we have that $\text{Var}(Y \mid N = n) = 3n.$

**Step 3: Plug in $ N $.** Replacing $ n $ with the random variable $ N $, the conditional variance becomes:
\begin{equation*}
h(N) = \text{Var}(Y \mid N) = 3N.
\end{equation*}

**Step 4: Apply Eve's Law.** Using Eve's Law, we compute the total variance:
\begin{equation*}
\text{Var}(Y) = \mathbb{E}[h(N)] + \text{Var}(g(N)).
\end{equation*}
Substituting $ h(N) = 3N $ and $ g(N) = 5N $, we have:
\begin{equation*}
\text{Var}(Y) = \mathbb{E}[3N] + \text{Var}(5N).
\end{equation*}
Simplifying further:
\begin{equation*}
\text{Var}(Y) = 3 \cdot \mathbb{E}[N] + 25 \cdot \text{Var}(N).
\end{equation*}
Substitute the values $ \mathbb{E}[N] = 1000 $ and $ \text{Var}(N) = 100 $:
\begin{equation*}
\text{Var}(Y) = 3 \cdot 1000 + 25 \cdot 100 = 3000 + 2500 = 5500.
\end{equation*}
```

```{admonition} Example: Grand Slam career
:class: tip

Alice is a tennis player who will participate in $ N $ Grand Slam tournaments over her career. The number of tournaments she plays, $ N $, follows a geometric distribution:
\begin{equation*}
N \sim \text{Geom}\left(\frac{1}{350}\right).
\end{equation*}
For each tournament, Alice has a probability of $ \frac{1}{15} $ of winning, independent of all other tournaments. Let $ T $ represent the total number of Grand Slams she wins during her career.

**Question:** What is the expected number of Grand Slam titles Alice will win, $ \mathbb{E}[T] $?

**Step 1: Define the goal.** We can compute $ \mathbb{E}[T] $ using the law of total expectation:
\begin{equation*}
\mathbb{E}[T] = \mathbb{E}[\mathbb{E}[T \mid N]] = \mathbb{E}[g(N)],
\end{equation*}
where $ g(N) = \mathbb{E}[T \mid N] $ is the expected number of titles given that she plays $ N $ tournaments.

**Step 2: Compute $ g(n) $.** When Alice plays exactly $ N = n $ tournaments, the number of titles she wins, $ T $, follows a $\text{Bin}\left(n, \frac{1}{15}\right)$ distribution. For a binomial random variable, the expected value is:
\begin{equation*}
\mathbb{E}[T \mid N = n] = n \cdot \frac{1}{15}.
\end{equation*}
Thus, $ g(n) = \frac{n}{15} $.

**Step 3: Plug in $N$.** Substituting the random variable $ N $ into $ g(n) $, we find:
\begin{equation*}
g(N) = \mathbb{E}[T \mid N] = \frac{N}{15}.
\end{equation*}

**Step 4: Apply Adam’s Law.** Using Adam’s law:
\begin{equation*}
\mathbb{E}[T] = \mathbb{E}[\mathbb{E}[T \mid N]] = \mathbb{E}[g(N)] = \mathbb{E}\left[\frac{N}{15}\right].
\end{equation*}
Factoring out $ \frac{1}{15} $:
\begin{equation*}
\mathbb{E}[T] = \frac{1}{15} \mathbb{E}[N].
\end{equation*}

For a geometric random variable $ N $ with success probability $ p = \frac{1}{350} $, the expected value is:
\begin{equation*}
\mathbb{E}[N] = \frac{1 - p}{p} = \frac{1 - \frac{1}{350}}{\frac{1}{350}} = 349.
\end{equation*}
Substituting this into the equation for $ \mathbb{E}[T] $:
\begin{equation*}
\mathbb{E}[T] = \frac{1}{15} \cdot 349 = 23.27.
\end{equation*}

---

**Question:** What is $ \text{Var}(T) $?

**Step 1: Define the goal.** Using Eve's Law, we express the variance of $ T $ as:
\begin{equation*}
\text{Var}(T) = \mathbb{E}[h(N)] + \text{Var}(g(N)),
\end{equation*}
where $ h(N) = \text{Var}(T \mid N) $ is the conditional variance of $ T $ given $ N $, and $ g(N) = \mathbb{E}[T \mid N] $ is the expected number of wins given $ N $.

**Step 2: Compute $ h(n) $.** When the number of tournaments is fixed at $ N = n $, the number of titles won, $ T $, follows the $\text{Bin}\left(n, \frac{1}{15}\right)$ distribution. The variance of a $\text{Bin}(n,p)$ random variable is $n \cdot p \cdot (1 - p).$ Substituting $ p = \frac{1}{15} $, we find:
\begin{equation*}
h(n) = \text{Var}(T \mid N = n) = n \cdot \frac{1}{15} \cdot \left(1 - \frac{1}{15}\right) = \frac{14n}{225}.
\end{equation*}

**Step 3: Plug in $N$.** Substituting $ N $ as the random variable, the conditional variance becomes:
\begin{equation*}
h(N) = \text{Var}(T \mid N) = \frac{14N}{225}.
\end{equation*}

**Step 4: Apply Eve's Law.** Using Eve's Law, we compute:
\begin{equation*}
\text{Var}(T) = \mathbb{E}[h(N)] + \text{Var}(g(N)).
\end{equation*}
Substituting $ h(N) = \frac{14N}{225} $ and $ g(N) = \frac{N}{15} $, we have:
\begin{equation*}
\text{Var}(T) = \mathbb{E}\left[\frac{14N}{225}\right] + \text{Var}\left(\frac{N}{15}\right).
\end{equation*}
For $ N \sim \text{Geom}(\frac{1}{350}) $, we know $ \mathbb{E}[N] = \frac{1 - \frac{1}{350}}{\frac{1}{350}} = 349 $. Substituting:
\begin{equation*}
\mathbb{E}[h(N)] = \frac{14}{225} \cdot \mathbb{E}[N] = \frac{14}{225} \cdot 349.
\end{equation*}

Moreover, 
\begin{equation*}
\text{Var}(N) = \frac{1 - \frac{1}{350}}{\left(\frac{1}{350}\right)^2} = 121,801.
\end{equation*}
Substituting:
\begin{equation*}
\text{Var}\left(\frac{N}{15}\right) = \frac{1}{15^2} \cdot \text{Var}(N) = \frac{1}{15^2} \cdot 121801 = \frac{121801}{225}.
\end{equation*}

Combining the two terms:
\begin{equation*}
\text{Var}(T) = \frac{14}{225} \cdot 349 + \frac{121801}{225} \approx 564.
\end{equation*}
```
```{admonition} Example: Clustering sampling
:class: tip

This is Example 9.6.2 from {cite}`Blitzstein19:Introduction`.

*Cluster sampling* is a method used in polling, such as for a presidential election, to gather insights about the population. In this process, a random state is first selected as the cluster for the poll. From the chosen state, a random sample of $ n $ individuals are selected, with replacement in this example. Each individual in the sample is asked about their political affiliation: say, Democrat or Republican.

Let $ X $ represent the number of Democrats in the sample. If the proportion of Democrats in the chosen state is denoted by $ q $, then $ X $ follows a binomial distribution, $ X \sim \text{Bin}(n, q) $. However, since the true proportion of Democrats, $ q $, is unknown, it is modeled as a random variable. In this example, $ q $ is assumed to follow a uniform distribution on $[0, 1]$, i.e., $ Q \sim \text{Unif}(0, 1) $.

**Question:** What is $\mathbb{E}[X]$?

**Step 1: Define the goal.** To compute $ \mathbb{E}[X] $, we use the law of total expectation:
\begin{equation*}
\mathbb{E}[X] = \mathbb{E}[\mathbb{E}[X \mid Q]] = \mathbb{E}[g(Q)],
\end{equation*}
where $ g(Q) = \mathbb{E}[X \mid Q] $ is the expected value of $ X $ given $ Q $.

**Step 2: Compute $ g(q) $.** When the fraction of Democrats in the chosen state is $ Q = q $, $ X $ follows a binomial distribution. The expected value of a binomial random variable is:
\begin{equation*}
g(q) = \mathbb{E}[X \mid Q = q] = nq.
\end{equation*}

**Step 3: Plug in $Q$.** Substituting $ Q $ as the random variable, we find:
\begin{equation*}
g(Q) = \mathbb{E}[X \mid Q] = nQ.
\end{equation*}

**Step 4: Apply Adam's Law.** Using Adam’s law:
\begin{equation*}
\mathbb{E}[X] = \mathbb{E}[\mathbb{E}[X \mid Q]] = \mathbb{E}[g(Q)] = \mathbb{E}[nQ].
\end{equation*}
Factoring out $ n $, we have that $\mathbb{E}[X] = n \mathbb{E}[Q].$ Since $ Q \sim \text{Unif}(0, 1) $, the expected value of $ Q $ is $\mathbb{E}[Q] = \frac{1}{2}.$ Thus:
\begin{equation*}
\mathbb{E}[X] = n \cdot \frac{1}{2} = \frac{n}{2}.
\end{equation*}

---

**Question:** What is $\text{Var}(X)$?

**Step 1: Define the goal.** To compute $ \text{Var}(X) $, we use Eve's Law:
\begin{equation*}
\text{Var}(X) = \mathbb{E}[h(Q)] + \text{Var}(g(Q)),
\end{equation*}
where $ h(Q) = \text{Var}(X \mid Q) $ is the conditional variance of $ X $ given $ Q $, and $ g(Q) = \mathbb{E}[X \mid Q] $.

**Step 2: Compute $ h(q) $.** When $ Q = q $, $ X$ is a binomial random variable, and the variance of a binomial random variable is:
\begin{equation*}
h(q) = \text{Var}(X \mid Q = q) = nq(1 - q).
\end{equation*}

**Step 3: Plug in $Q$.** Substituting $ Q $ as the random variable, we have:
\begin{equation*}
h(Q) = \text{Var}(X \mid Q) = nQ(1 - Q).
\end{equation*}

**Step 4: Apply Eve's Law.** Using Eve's Law:
\begin{equation*}
\text{Var}(X) = \mathbb{E}[h(Q)] + \text{Var}(g(Q)).
\end{equation*}
Substituting $ h(Q) = nQ(1 - Q) $ and $ g(Q) = nQ $:
\begin{equation*}
\text{Var}(X) = \mathbb{E}\left[nQ(1 - Q)\right] + \text{Var}(nQ).
\end{equation*}
Factoring out constants:
\begin{equation*}
\text{Var}(X) = n\left(\mathbb{E}[Q] - \mathbb{E}[Q^2]\right) + n^2\text{Var}(Q).
\end{equation*}
For $ Q \sim \text{Unif}(0, 1) $:
\begin{equation*}
\mathbb{E}[Q] = \frac{1}{2}, \quad \text{Var}(Q) = \frac{1}{12}.
\end{equation*}
From the relationship $ \text{Var}(Q) = \mathbb{E}[Q^2] - \mathbb{E}[Q]^2 $:
\begin{equation*}
\frac{1}{12} = \mathbb{E}[Q^2] - \left(\frac{1}{2}\right)^2.
\end{equation*}
Solving for $ \mathbb{E}[Q^2] $:
\begin{equation*}
\mathbb{E}[Q^2] = \frac{1}{3}.
\end{equation*}

Adding the two components:
\begin{equation*}
\text{Var}(X) = \frac{n}{6} + \frac{n^2}{12}.
\end{equation*}
```