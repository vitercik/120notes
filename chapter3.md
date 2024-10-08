# Random variables and their distributions

```{contents}
:local:
```

## Random variables

When performing an experiment, we are often more interested in specific properties of the outcomes rather than the outcomes themselves. For example, if we toss a coin three times, instead of focusing on each individual result (e.g., heads or tails for each toss), we may be more interested in the total number of head we observed.

This is where **random variables** come into play. A random variable, denoted as $ X $, is a variable that takes on different values based on the outcome of a random experiment. More formally, given an experiment with a sample space $ S $, a random variable is a function that maps each outcome $s \in S $ to a real number in $ \mathbb{R} $. The value assigned to each outcome, $ X(s) $, depends on the random result of the experiment, represented by a probability function $ \mathbb{P} $.

To make this concrete, let’s return to the example of tossing a coin three times. The sample space $ S $ for this experiment consists of all possible sequences of heads (H) and tails (T):

\begin{equation*}
S = \{HHH, HHT, HTH, HTT, THH, THT, TTH, TTT\}
\end{equation*}

Now, define the random variable $ X $ as the number of heads observed in the sequence. For each outcome in the sample space, the random variable assigns a corresponding value:

- $ X(HHH) = 3 $ (three heads)
- $ X(HHT) = X(HTH) = X(THH) = 2 $ (two heads)
- $ X(HTT) = X(THT) = X(TTH) = 1 $ (one head)
- $ X(TTT) = 0 $ (no heads)

In this way, the random variable simplifies the experiment's outcomes, focusing on the specific feature we care about—in this case, the number of heads—while preserving the underlying randomness of the experiment.

We’ll now provide the formal definition of a *discrete* random variable. (We will discuss *continuous* random variables later in the quarter.)

```{admonition} Discrete random variable
A discrete **random variable** (RV) is a type of random variable that can take on either a finite or an infinite list of distinct values, such as $ x_1, x_2, x_3, \dots $. For a discrete random variable, the sum of the probabilities that $ X $ takes each of these values must equal 1. In other words:

\begin{equation*}
\mathbb{P}[X = x_1 \text{ or } X = x_2 \text{ or } X = x_3 \text{ or } \dots ] = 1.
\end{equation*}

The expression $ \mathbb{P}[X = x] $ is shorthand for the probability that the random variable $ X $ takes the value $ x $, which refers to the probability of the event $\{s \in S \text{ such that } X(s) = x\}$ where the outcome of the experiment $ s \in S $ results in $ X(s) = x $.
```

## Distributions and probability mass functions

The **probability mass function (PMF)** of a discrete random variable is a function that assigns probabilities to each possible value of the random variable. The PMF is denoted by $ p_X(x) = \mathbb{P}[X = x] $, which gives the probability that $ X $ takes the value $ x $.

```{admonition} Example: Tossing coins.
:class: tip

Suppose we toss a coin three times, and let $ X $ represent the number of heads. The possible values of $ X $ are 0, 1, 2, and 3, and the PMF would look as follows:

- $ p_X(0) = \mathbb{P}[X = 0] = \mathbb{P}[\{TTT\}] = \frac{1}{8} $
- $ p_X(1) = \mathbb{P}[X = 1] = \mathbb{P}[\{HTT, THT, TTH\}] = \frac{3}{8} $
- $ p_X(2) = \mathbb{P}[X = 2] = \frac{3}{8} $
- $ p_X(3) = \mathbb{P}[X = 3] = \mathbb{P}[\{HHH\}] = \frac{1}{8} $

See {numref}`Figure {number} <coin_pmf>` for an illustration.
```

```{figure} images/coin_pmf.png
---
name: coin_pmf
width: 250px
align: center
---

PMF of the number of times a coin lands heads when tossed three times.
```

```{admonition} Example: Touchdown passes.
:class: tip

As another example, if our experiment is a game between the Bears and Packers, $X$ might be the number of touchdowns passes thrown by the Packers quarterback. Its PMF may look something like {numref}`touchdown`, as illustrated in {numref}`football_pmf`.

```

```{list-table} PMF of the number of touchdown passes thrown by Packers quarterback.
:header-rows: 1
:name: touchdown

* - $x$
  - $ p_X(x) = \mathbb{P}[X = x] $
* - 0
  - 0.10
* - 1
  - 0.25
* - 2
  - 0.25
* - 3
  - 0.25
* - 4
  - 0.10
* - 5
  - 0.05
```

```{figure} images/football_pmf.png
---
name: football_pmf
width: 250px
align: center
---

Illustration of the PMF of the number of touchdown passes thrown by the Packers quarterback.
```