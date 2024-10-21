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

## Linearity of Expectation

One of the fundamental properties of expectation is *linearity:* the expected value of a sum of random variables equals the sum of their individual expected values, regardless of whether these random variables are independent.

```{admonition} Linearity of expectation

1. **Sum of random variables**: The expectation of the sum of two random variables $X$ and $Y$ can be expressed as: $\mathbb{E}[X + Y] = \mathbb{E}[X] + \mathbb{E}[Y].$ Notably, this property holds even if $X$ and $Y$ are not independent.
2. **Scaling of random variables**: For a random variable $X$ and any constant $c \in \mathbb{R}$, the expectation scales linearly: $\mathbb{E}[cX] = c \mathbb{E}[X].$

```

These properties allow us to decompose complex random variables into simpler parts for easier computation.

For example, let $X \sim \text{Bin}(n, p)$ be a binomial RV. We know that $X = I_1 + I_2 + \cdots + I_n$, where each $I_j \sim \text{Bern}(p)$. Since $\mathbb{E}[I_j] = p$, we can conclude that $\mathbb{E}[X] =  \mathbb{E}[I_1 + I_2 + \cdots + I_n] = \mathbb{E}[I_1] + \cdots + \mathbb{E}[I_n] = np.$

As another example, suppose we have a bag with $w$ white marbles and $b$ black marbles. Let $X \sim \text{HGeom}(w, b, n)$ represent the number of white marbles when we draw $n$ marbles out of the bag randomly without replacement. Define the RV $I_j$ such that $I_j = 1$ if the $j$-th marble in the sample is white, and $I_j = 0$ otherwise. Then, the RV $X$ can be expressed as $X = I_1 + I_2 + \cdots + I_n.$ The RVs $I_1, \dots, I_n$ are not independent, but linearity of expectation still applies. For each indicator variable $I_j$,

```{math}
:label: hyp_exp
\mathbb{E}[I_j] = 1 \cdot \mathbb{P}[I_j = 1] + 0 \cdot \mathbb{P}[I_j = 0] = \mathbb{P}[\text{$j$-th marble is white}].
```

To calculate this probability, let’s start with the first marble. Since there are $w$ white marbles and $w+ b$ total marbles, $\mathbb{P}[1^{st} \text{ marble is white}] = \frac{w}{w+b}$. Next,

\begin{align*}
    \mathbb{P}[2^{nd} \text{ marble is white}] = \, &\mathbb{P}[2^{nd} \text{ marble is white} \mid 1^{st} \text{ marble is white}]\mathbb{P}[1^{st} \text{ marble is white}]\\
			+\, &\mathbb{P}[2^{nd} \text{ marble is white} \mid 1^{st} \text{ marble is black}]\mathbb{P}[1^{st} \text{ marble is black}].
\end{align*}

If we know the first marble is white, then there are $w-1$ white marbles out of the remaining $w+b-1$ marbles. Therefore, $\mathbb{P}[2^{nd} \text{ marble is white} \mid 1^{st} \text{ marble is white}] = \frac{w-1}{w+b-1}$. Meanwhile, $\mathbb{P}[2^{nd} \text{ marble is white} \mid 1^{st} \text{ marble is black}] = \frac{w}{w+b-1}$. Therefore,
\begin{equation*}
\mathbb{P}[2^{nd} \text{ marble is white}] = \frac{w-1}{w+b-1} \cdot \frac{w}{w+b} + \frac{w}{w+b-1}\left(1 - \frac{w}{w+b}\right) = \frac{w}{w+b}.
\end{equation*}
Returning to {eq}`hyp_exp`, we have that $\mathbb{E}[I_j] =  \mathbb{P}[j^{th} \text{ marble is white}] = \frac{w}{w+b}$. In other words, each marble we draw is equally likely to be white when considered in isolation (though not when conditioned on the previous draws), a phenomenon known as *symmetry*. In the end, we have that $\mathbb{E}[X] = \mathbb{E}[I_1 + \dots + I_n] = \mathbb{E}[I_1] + \cdots + \mathbb{E}[I_n] =  \frac{nw}{w+b}$.

We note that the events that the $1^{st}$ and $2^{nd}$ marbles are white are not independent: $\mathbb{P}[2^{nd} \text{ marble is white} \mid 1^{st} \text{ marble is white}] = \frac{w-1}{w+b-1} < \mathbb{P}[2^{nd} \text{ marble is white}]  = \frac{w}{w+b}$. This intuitively makes sense: once you know the first marble is white, there are fewer white marbles to choose from.

## Geometric and negative binomial

```{admonition} Geometric distribution

The geometric distribution arises from a sequence of independent Bernoulli trials, where each trial results in a success with probability $ p $ and a failure with probability $ q = 1 - p $. In this context, let the random variable $ X $ represent the number of failures that occur before the first success. We say that $ X $ follows a *geometric distribution with parameter $ p $*, denoted as $ X \sim \text{Geom}(p) $.

The probability mass function $ p_X(k) $ of a geometric random variable is $\mathbb{P}[X = k] = p_X(k) = q^k p$ for $k = 0, 1, 2, \dots$. This expression reflects the probability of having $ k $ consecutive failures (each occurring with probability $ q $) followed by a single success (occurring with probability $ p $). For example, if we observe the sequence "FFFFFS," where five failures are followed by one success, the probability of this specific sequence occurring is given by $ q^5 p $.

```

The expectation $ \mathbb{E}[X] $ for a geometric random variable can be derived by summing over all possible values of $ k $:

\begin{equation*}
\mathbb{E}[X] = \sum_{k = 0}^{\infty} k \cdot \mathbb{P}[X = k] = p \sum_{k = 0}^{\infty} k q^k = \frac{1 - p}{p}.
\end{equation*}

The following distribution is closely related to the geometric distribution.

```{admonition} First success distribution

Suppose we perform a sequence of independent Bernoulli trials, where each trial results in a success with probability $ p $ and a failure with probability $ q = 1 - p $. Let $ Y $ be the total number of trials required to achieve the first successful outcome, *including the successful trial itself*. Then $Y$ follows the *first success distribution with parameter $p$*, denoted $ Y \sim \text{FS}(p) $.
```

The key relationship between $ Y $ and the geometric distribution is that $ Y $ counts the total number of trials, while the geometric random variable $ X $ only counts the number of failures before the first success. Mathematically, $Y = X+1$, where $ X \sim \text{Geom}(p) $. Since $ Y $ simply adds one successful trial to the count of failures, the expected value of $ Y $ can be derived using the linearity of expectation:

\begin{equation*}
\mathbb{E}[Y] = \mathbb{E}[X + 1] = \mathbb{E}[X] + 1 = \frac{1 - p}{p} + 1 = \frac{1}{p}.
\end{equation*}

In other words, on average, the number of trials required to achieve the first success (including the successful trial itself) is $ \frac{1}{p} $.

```{admonition} Example
:class: tip

Imagine a couple who decides to continue having children until they have at least one boy and one girl. Each child is either a boy or a girl, and each outcome is independent with an equal probability of 50%. The couple never has twins, so each child is born individually.

**Question:** What is the expected number of children they’ll have?

For example, if the sequence of births is G-G-G-B, they would have four children in total. If the sequence is **B-B-G**, they would have three children in total.

1. **Step 1: Define the Random Variables**
    
    Let $ X $ denote the number of children needed, starting from the second child, to get a gender different from the firstborn. Essentially, $ X $ is the number of additional children required after the first child to achieve a child of the opposite gender. For example, if the birth order is G-G-G-B, then $X = 3$ and if the birth order is B-B-G, then $X = 2$.
    
2. **Step 2: Define the Goal**
    
    The goal is to compute the expected number of children the couple will have, which can be expressed as $\mathbb{E}[\# \text{children}] = \mathbb{E}[1 + X] = 1 + \mathbb{E}[X]$. Here, the "1" represents the firstborn, and $ X $ represents the additional children needed.
    
3. **Step 3: Identify the Distribution of $ X $**
    
    Notice that $ X $ represents the number of children until the couple has a child of the opposite gender from the firstborn. This is equivalent to the distribution $ \text{FS}(\frac{1}{2}) $, which describes the number of trials until the first success, given a success probability of $ \frac{1}{2} $. The expected value of $ X $ is $\mathbb{E}[X] = \frac{1}{\frac{1}{2}} = 2$.
    
4. **Step 4: Calculate the Final Answer**
    
    The total expected number of children the couple will have is: $\mathbb{E}[\# \text{children}] = 1 + \mathbb{E}[X] = 1 + 2 = 3.$
    

```

```{admonition} Example
:class: tip

This is a classic problem called the coupon collector problem. Imagine that there are $ n $ different types of toys that you are trying to collect. Each time you acquire a toy, it is equally likely to be any one of the $ n $ types, regardless of the toys you have collected so far. The goal is to determine the expected number of toys you need to collect in order to have at least one of each type.

**Question:** What is the expected number of toys needed to complete the set?

1. **Step 1: Define the Random Variables**
    
    Let $ N $ denote the total number of toys needed to collect all $ n $ different types. This can be expressed as the sum of individual random variables $ N_1, N_2, \ldots, N_n $, where:
    
    - $ N_1 $ is the number of toys needed to collect the first type that you haven’t seen before. Clearly, $ N_1 = 1 $ because the first toy you collect will always be a new type.
    - $ N_2 $ is the number of additional toys needed to collect a second type that you haven’t seen before.
    - $ N_j $ is the number of additional toys needed to collect the $ j $-th type that you haven’t seen before.
    
    Thus, $N = N_1 + N_2 + \cdots + N_n.$
    
2. **Step 2: Identify the Distribution of $ N_j $**
    
    Each $ N_j $ follows the first success distribution, where the probability of success depends on how many types are yet to be collected.
    
    - $ N_2 \sim \text{FS}\left(\frac{n-1}{n}\right) $, as you are looking for a toy of a new type among the $ n $ available types, given that you’ve already collected one type.
    - More generally, $ N_j $ follows $ \text{FS}\left(\frac{n-j+1}{n}\right) $ because you are searching for a new type of toy among the remaining $ n - (j - 1) $ types.
3. **Step 3: Compute the Final Answer**
    
    The expected total number of toys $ N $ is given by the sum of the expected values of each $ N_j $. Therefore,
\begin{equation*}
    \mathbb{E}[N] = \mathbb{E}[N_1] + \mathbb{E}[N_2] + \cdots + \mathbb{E}[N_n] = 1 + \frac{n}{n-1} + \frac{n}{n-2} + \cdots + n \approx n \log n.
\end{equation*}
    
```
    

```{admonition} Example
:class: tip

The **St. Petersburg paradox** is a classic problem in probability theory and economics. The setup of this paradox involves a game where a fair coin is flipped repeatedly until it lands on heads for the first time. The game has the following structure:

- If the game ends in one round (i.e., you get heads on the first flip), you win \$2.
- If the game ends in two rounds (i.e., the first heads occurs on the second flip), you win \$4.
- More generally, if the game ends in $ i $ rounds, you win \$$ 2^i $.

Let $ X $ denote the total winnings from the game. By definition, the winnings are given by $ X = 2^N $, where $ N $ is the number of rounds needed to get the first heads. The expected value of $ X $ can be calculated as follows:

\begin{align*}
\mathbb{E}[X] &= \sum_{i = 1}^{\infty} 2^i \cdot \mathbb{P}[X = 2^i] = \sum_{i = 1}^{\infty} 2^i \cdot \mathbb{P}[2^N = 2^i]\\
&= \sum_{i = 1}^{\infty} 2^i \cdot \mathbb{P}[N = i] =  2 \cdot \frac{1}{2} + 4 \cdot \frac{1}{4} + 8 \cdot \frac{1}{8} + \cdots = \infty.
\end{align*}

This result is counterintuitive because it suggests that a rational person should be willing to pay any amount to play this game, despite the unrealistic nature of achieving such high winnings. In fact, since $N \sim \text{FS}\left(\frac{1}{2}\right)$, so the expected number of rounds of the game is $\mathbb{E}[N] = 2$.

It’s important to note that $ \infty = \mathbb{E}[X] = \mathbb{E}\left[2^N\right] \not=  2^{\mathbb{E}[N]} = 4$.

To make the game more realistic, suppose you impose a bound of 40 rounds. In this case, the maximum potential winnings are \$$ 2^{40} $, which is approximately one trillion dollars. However, the expected value of $ X $ when limiting the number of rounds to 40 can be calculated as $\mathbb{E}[X] = \sum_{n = 1}^{40} \frac{1}{2^n} \cdot 2^n = 40.$ By capping the game at 40 rounds, the expected winnings become finite and are equal to 40 dollars.

```

We will introduce one more distribution that is closely related to the geometric distribution.

```{admonition} Negative binomial distribution

Suppose we perform a sequence of independent Bernoulli trials, where each trial results in a success with probability $ p $. Let $X$ be the number of failures before $r^{th}$ success. Then we say that $X$ follows the *negative binomial distribution with parameters $(r,p)$, denoted $X \sim \text{NBin}(r,p)$.

```
To determine the PMF of $X$, we will start with an example, where $X \sim \text{NBin}(5, p)$, which is the number of failures before the fifth success. Under the following sequences (with 1 representing success and 0 representing failure), there are three failures before the fifth success: 11010011, or 11010101, or ... Indeed, to represent three failures before the fifth success, the last digit in these sequences **must** be a 1, and must be preceded by three 0s (the three failures) and four 1s (the four other successes), arranged in any order. There are ${3 + 4 \choose 3}$ different sequences of this form: imagine drawing seven fill-in-the-blank slots, three of which we must fill in with 0s, and the rest with 1s. Each sequence has a probability of $p^5(1-p)^3$ (for the five success and the three failures). Therefore 

\begin{equation*}

\mathbb{P}[X = 3] = {3 + 4 \choose 3}p^5(1-p)^3.

\end{equation*}
By the exact same logic, for $X \sim \text{NBin}(r,p)$,

\begin{equation*}

\mathbb{P}[X = n] = {n + r-1 \choose n}p^r(1-p)^n

\end{equation*}

 for $n = 0, 1, 2, \dots$.
To calculate the expectation of $X$, we can write it as $X = X_1 + \cdots + X_r$ where $X_1$ is the number of failures until the $1^{st}$ success, $X_2$ is the number of failures between $1^{st}$ and second $2^{nd}$ successes, and so on. We can see that $X_i \sim \text{Geom}(p)$, so by linearity of expectation, $\mathbb{E}[X] = r \cdot \frac{1-p}{p}$.

```{admonition} Example
:class: tip

This season, suppose Arsenal wins each soccer game independently with a probability of 0.7. 

**1. Number of Games Before a Win.** Let $ X $ be the number of games Arsenal plays before winning their first game. Since each game is independent and has a fixed probability of success (a win) of 0.7, $X \sim \text{Geom}(0.7).$

**2. Number of Losses Before Winning Five Games.** Next, let $ Y $ represent the number of games Arsenal loses before achieving five wins. Then $Y \sim \text{NBin}(5, 0.7).$

```

## Indicator random variables and the fundamental bridge

An indicator random variable is a simple variable that indicates whether a specific event has occurred or not.

```{admonition} Indicator random variable

Given an event $A$, define the RV $ I_A $ is as follows:

\begin{equation*}
I_A =
\begin{cases}
1 & \text{if event } A \text{ occurs} \\
0 & \text{otherwise}.
\end{cases}
\end{equation*}

```

The fundamental relationship between the probability and expectation of an indicator RV is captured by the following formula:

\begin{equation*}
\mathbb{E}[I_A] = 1 \cdot \mathbb{P}[I_A = 1] + 0 \cdot \mathbb{P}[I_A = 0] = \mathbb{P}[I_A = 1] = \mathbb{P}[A].
\end{equation*}

This equation shows that the expected value of an indicator random variable $ I_A $ is equal to the probability of the event $ A $.

```{admonition} Example
:class: tip

Suppose a university is deciding whether to test all 100 people in a dormitory for COVID-19. Before conducting individual tests, they will test the sewage. If the sewage sample tests positive, they will test all 100 people in the dorm. Let’s model this situation using indicator random variables:

- Each person in the dorm is independently negative with a probability of 0.9.
- Let $ X $ represent the total number of tests conducted, including the sewage test.
- Let $ A $ denote the event that the sewage test is positive, with indicator RV $I_A$.

The total number of tests $ X $ is $X = 1 + 100 \cdot I_A$. Here, the "1" represents the initial sewage test, and the term $ 100 \cdot I_A $ represents the additional 100 individual tests if the sewage test is positive. To find the expected number of tests $ \mathbb{E}[X] $, we first need to determine $ \mathbb{E}[I_A] $. The probability of $ A $, which is the probability that at least one person in the dorm has COVID-19, is given by $\mathbb{P}[A] = 1 - \mathbb{P}[\text{no one has COVID}] = 1 - 0.9^{100}.$ Therefore, the expected value of $ I_A $ is $\mathbb{E}[I_A] = \mathbb{P}[A] = 1 - 0.9^{100}$.

Now, we can calculate the expected number of tests:

\begin{equation*}
\mathbb{E}[X] = \mathbb{E}[1 + 100 \cdot I_A] = 1 + 100 \mathbb{E}[I_A] = 1 + 100(1 - 0.9^{100}).
\end{equation*}

```