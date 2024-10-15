# Expectation

```{contents}
:local:
```

## Definition of expectation

While the full distribution of a RV provides a complete description of its behavior, it can be cumbersome to work with since it involves many probabilities. Instead, it is often more practical to summarize a distribution with just a few key numbers that describe the "average" value of the RV and how much it varies or spreads.

One important summary is the *expected value*.

```{admonition} Expected value

For a RV $ X $ that takes distinct values $ x_1, x_2, \dots $, the expected value, denoted $ \mathbb{E}[X] $, is given by:
\begin{equation*}
\mathbb{E}[X] = \sum_{i = 1}^{\infty} x_i \mathbb{P}[X = x_i].
\end{equation*}
This formula gives a weighted average of the possible values of $ X $, where the weights are the probabilities associated with each value.

```

For example, let $ X \sim \text{Bern}(p) $ be a Bernoulli random variable that takes the value 1 with probability $ p $ and 0 with probability $ 1 - p $. The expected value of $ X $ is $\mathbb{E}[X] = 0 \cdot \mathbb{P}[X = 0] + 1 \cdot \mathbb{P}[X = 1] = 1 \cdot p = p.$
This means that the expected value of a Bernoulli random variable is simply $ p $, the probability of success.

Below, we illustrate the $\text{Bern}(p)$ PMF for several choices of $p$, together with the expected value.

```{figure} images/bern25.png
---
name: bern25
width: 225px
align: center
---

PMF of the $\text{Bern}(0.5)$ distribution, with the expected value marked by a star.
```

```{figure} images/bern50.png
---
name: bern50
width: 225px
align: center
---

PMF of the $\text{Bern}(0.5)$ distribution, with the expected value marked by a star.
```

```{figure} images/bern75.png
---
name: bern75
width: 225px
align: center
---

PMF of the $\text{Bern}(0.75)$ distribution, with the expected value marked by a star.
```


As another example, let $X$ be the number of touchdown passes thrown by the Packers quarterback in a game between the Bears and the Packers, with its PMF as follows:


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

Then $\mathbb{E}[X] = 0 \cdot 0.1 + 1 \cdot 0.25 + 2 \cdot 0.25 + 3 \cdot 0.25 + 4 \cdot 0.1 + 5 \cdot 0.05 = 2.15$.

We illustrate the PMF and expected value of this random variable below.

```{figure} images/football_exp.png
---
name: football_exp
width: 300px
align: center
---

Illustration of the PMF and expected number of touchdown passes thrown by the Packers quarterback.
```

```{admonition} Example: Investment returns.
:class: tip

Suppose an investment has a 50% chance of gaining 20% and a 50% chance of losing 10%. To calculate the expected return, we multiply the probability of each outcome by the corresponding return and sum the results, so the expected return is $0.5 \cdot 0.2 + 0.5 \cdot (-0.1) = 0.05.$
In other words, the expected return of this investment is 5%.

Meanwhile, suppose the investment has a 50% chance of gaining 200% and a 50% chance of losing 190%. The expected return is $0.5 \cdot 2.0 + 0.5 \cdot (-1.9) = 0.05.$ Even though the potential gains and losses are much larger in this case, the expected return is still 5% (however, the *variance* is different, a topic we will return to later in this chapter).
```