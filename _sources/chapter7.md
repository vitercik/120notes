# Transformations

```{contents}
:local:
```

Often, the random variable we want to analyze does not exactly follow one of the named distributions we’ve analyzed in this class, but is a closely related transformation of one of these RVs. In this section, we will learn how to analyze these transformations of RVs.

## Change of variables

We begin with a motivating example. Given a Normal RV $X \sim N(0, 1)$, suppose we define a new random variable $Y = e^X$. This transformation is often used to model the evolution of stock prices. In this section, we will develop tools to analyze the distribution of $Y$.

```{admonition} Change of variables for a continuous RV

Let $X$ be a continuous RV, and define $Y = g(X)$, where $g$ is a differentiable and increasing function. The probability density function (PDF) of $Y$ is given by:

\begin{equation*}
f_Y(y) = f_X(g^{-1}(y)) \cdot \frac{1}{g'(g^{-1}(y))}.
\end{equation*}

If $g$ is a decreasing function, the PDF of $Y$ is modified to account for the absolute value of the derivative:
\begin{equation*}
f_Y(y) = f_X(x) \cdot \left| \frac{1}{g'(g^{-1}(y))} \right|.
\end{equation*}
```

We now return to our motivating example.

```{admonition} Log-Normal PDF
:class: tip

This is Example 8.1.3 from {cite}`Blitzstein19:Introduction`.

For $X \sim N(0, 1)$, we determine the PDF of $Y = e^X$ step by step.

**Step 1: Identify the transformation $g$.** The transformation $g(x) = e^x$ is both differentiable and strictly increasing.
    
**Step 2: Compute the inverse of $g$.** The inverse function $g^{-1}(y)$ satisfies $g(g^{-1}(y)) = y$. For $g(x) = e^x$, the inverse is:
\begin{equation*}
g^{-1}(y) = \ln y.
\end{equation*}
    
**Step 3: Compute the derivative of $g$.** The derivative of $g(x) = e^x$ is:
\begin{equation*}
g'(x) = e^x.
\end{equation*}
    
**Step 4: Identify the PDF of $X$.** Since $X \sim N(0, 1)$, its PDF is the standard normal density function:
\begin{equation*}
f_X(x) = \varphi(x) = \frac{1}{\sqrt{2\pi}} e^{-x^2/2}.
\end{equation*}
    
**Step 5: Derive the PDF of $Y$.** Substituting into the formula for $f_Y(y)$, we have:
\begin{equation*}
f_Y(y) =
\begin{cases}
0, & \text{if } y \leq 0 \text{ (since $Y = e^X > 0$)}, \\
f_X(g^{-1}(y)) \cdot \frac{1}{g'(g^{-1}(y))}, & \text{if } y > 0.
\end{cases}
\end{equation*}

For $y > 0$, substituting $g^{-1}(y) = \ln y$ and $g'(\ln y) = e^{\ln y} = y$, we find:
\begin{equation*}
f_Y(y) = f_X(\ln y) \cdot \frac{1}{y} = \varphi(\ln y) \cdot \frac{1}{y}.
\end{equation*}

Explicitly:
\begin{equation*}
f_Y(y) = \frac{1}{\sqrt{2\pi}} e^{-(\ln y)^2 / 2} \cdot \frac{1}{y}, \quad y > 0.
\end{equation*}
```

## Convolutions

This section will provide tools for determining the distribution of the sum of two independent random variables. Let $T = X + Y$, where $X$ and $Y$ are independent. The process for deriving the distribution of $T$ depends on whether $X$ and $Y$ are discrete or continuous.

1. **For Discrete RVs**
    
    If $X$ and $Y$ are discrete, the probability mass function of $T$ is given by:
    \begin{equation*}
    \mathbb{P}[T = t] = \sum_x \mathbb{P}[X = x \text{ and } Y = t - x] = \sum_x \mathbb{P}[X = x] \mathbb{P}[Y = t - x].
    \end{equation*}
    
2. **For Continuous RVs**
    
    If $X$ and $Y$ are continuous, the probability density function (PDF) of $T$ is obtained through convolution:
    \begin{equation*}
    f_T(t) = \int_{-\infty}^\infty f_X(x) f_Y(t - x) \, dx.
    \end{equation*}
    

```{admonition} Swim race
:class: tip

Suppose a swimmer swims two laps. Let $X$ represent the time taken to complete the first lap and $Y$ the time for the second lap. Assume both times are independent and follow an exponential distribution with rate parameter $\lambda$, i.e., $X, Y \sim \text{Expo}(\lambda)$. The PDF of $X$ and $Y$ is:
\begin{equation*}
f_X(x) = f_Y(y) =
\begin{cases}
\lambda e^{-\lambda x}, & \text{if } x > 0, \\
0, & \text{otherwise.}
\end{cases}
\end{equation*}

Now, let $T = X + Y$ represent the total time to complete both laps. We aim to find the PDF of $T$.

**Step 1: Set up the convolution.** For $t > 0$, the PDF of $T$ is given by:
\begin{equation*}
f_T(t) = \int_{-\infty}^\infty f_X(x) f_Y(t - x) \, dx.
\end{equation*}

Since $f_X(x) = 0$ for $x < 0$ and $f_Y(t - x) = 0$ for $t - x < 0$ (i.e., $x > t$), the product $f_X(x)f_Y(t - x)$ is nonzero only when $0 \leq x \leq t$. Thus, the integral simplifies to:
\begin{equation*}
f_T(t) = \int_0^t f_X(x) f_Y(t - x) \, dx.
\end{equation*}
    
**Step 2: Substitute the PDFs of $X$ and $Y$.** Substituting $f_X(x) = \lambda e^{-\lambda x}$ and $f_Y(t - x) = \lambda e^{-\lambda (t - x)}$, we get:
\begin{equation*}
f_T(t) = \int_0^t \lambda e^{-\lambda x} \cdot \lambda e^{-\lambda (t - x)} \, dx.
\end{equation*}
Combining terms, we find:
\begin{equation*}
f_T(t) = \lambda^2 e^{-\lambda t} \int_0^t e^{-\lambda x + \lambda x} \, dx = \lambda^2 e^{-\lambda t} \int_0^t 1 \, dx.
\end{equation*}
    
**Step 3: Evaluate the integral.** The integral of 1 over $[0, t]$ is simply $t$, so:
\begin{equation*}
f_T(t) = \lambda^2 t e^{-\lambda t}.
\end{equation*}
    

Thus, the total time $T = X + Y$ follows a distribution with PDF:
\begin{equation*}
f_T(t) = \lambda^2 t e^{-\lambda t}, \quad t > 0.
\end{equation*}
```

## Gamma

We will begin this section with a review of Poisson processes in the context of the 2014 FIFA World Cup. During the World Cup, the average number of soccer goals scored per 90-minute game was approximately 2.7. Let $X_{90}$ represent the total number of goals scored in a game, with $\mathbb{E}[X_{90}] = 2.7$. The sequence of goals over continuous time can be modeled as a **Poisson process** with a rate parameter $\lambda$. In a Poisson process with rate $\lambda$, the random variable $X_t$, representing the number of goals scored in an interval of $t$ minutes, follows a Poisson distribution:
\begin{equation*}
X_t \sim \text{Pois}(\lambda t), \quad \mathbb{P}[X_t = k] = \frac{e^{-\lambda t}(\lambda t)^k}{k!}.
\end{equation*}
Given that the expected number of goals in a 90-minute game is $\mathbb{E}[X_{90}] = 2.7$, and using the property $\mathbb{E}[X_t] = \lambda t$, we have:
\begin{equation*}
2.7 = \lambda \cdot 90 \implies \lambda = 0.03.
\end{equation*}
Thus, the rate of goals is $\lambda = 0.03$ goals per minute.

Here are a few example questions we might ask about this Poisson process:

1. **What is the probability of exactly 4 goals before halftime?** The interval from the start of the game to halftime (45 minutes) is modeled by $X_{45} \sim \text{Pois}(\lambda t = 0.03 \cdot 45 = 1.35)$. The probability of exactly 4 goals is:

\begin{equation*}
\mathbb{P}[X_{45} = 4] = \frac{e^{-\lambda t} (\lambda t)^4}{4!} = \frac{e^{-1.35}(1.35)^4}{4!} \approx 0.03.
\end{equation*}
    
2. **What is the probability the first goal is scored within the first 10 minutes?** Let $T_1$ represent the time until the first goal. In a Poisson process, $T_1$ follows an exponential distribution with rate $\lambda = 0.03$, i.e., $T_1 \sim \text{Expo}(\lambda)$. The cumulative distribution function (CDF) of $T_1$ is:

\begin{equation*}
F_{T_1}(t) = \mathbb{P}[T_1 \leq t] =
\begin{cases}
0, & \text{if } t \leq 0, \\
1 - e^{-\lambda t}, & \text{if } t > 0.
\end{cases}
\end{equation*}
Substituting $t = 10$ and $\lambda = 0.03$:
\begin{equation*}
F_{T_1}(10) = 1 - e^{-0.03 \cdot 10} = 1 - e^{-0.3} \approx 0.26.
\end{equation*}
Thus, there is approximately a 26% chance the first goal is scored within the first 10 minutes.

Next, let $T_5$ represent the time until the 5th goal is scored in a soccer game. In the remainder of this section, our goal will be to determine the PDF of $T_5$. Doing so will rely on the ***Gamma function,*** defined as:
\begin{equation*}
\Gamma(a) = \int_0^{\infty} e^{-x}x^{a-1} \, dx, \quad a > 0.
\end{equation*}
Key properties of the Gamma function include:
- $\Gamma(a + 1) = a \Gamma(a)$,
- $\Gamma(n) = (n-1)!$ for positive integers $n$.

```{admonition} Gamma distribution

A random variable $Y$ is said to have a **Gamma distribution** with shape parameter $a > 0$ and rate parameter $\lambda > 0$ if its probability density function (PDF) is:
\begin{equation*}
f_Y(y) = \frac{\lambda e^{-\lambda y}(\lambda y)^{a-1}}{\Gamma(a)}, \quad y > 0.
\end{equation*}
This is written as $Y \sim \text{Gamma}(a, \lambda)$.
```

Let's return back to the World Cup example, where we aim to find the PDF of $T_5$, the time until the 5th goal is scored in a soccer game. Let $X_t$ denote the number of goals scored within the first $t$ minutes of the game. The time $T_5 \leq t$ if and only if at least 5 goals are scored by time $t$, i.e., $X_t \geq 5$. The cumulative distribution function (CDF) of $T_5$ is:
\begin{equation*}
F_{T_5}(t) = \mathbb{P}[T_5 \leq t] = \mathbb{P}[X_t \geq 5] = \sum_{k=5}^\infty \mathbb{P}[X_t = k],
\end{equation*}
where $X_t \sim \text{Pois}(\lambda t)$ and $\mathbb{P}[X_t = k] = \frac{e^{-\lambda t}(\lambda t)^k}{k!}$.

To find the PDF of $T_5$, we differentiate the CDF:
\begin{equation*}
f_{T_5}(t) = \frac{d}{dt}F_{T_5}(t).
\end{equation*}
Differentiating term by term:
\begin{equation*}
f_{T_5}(t) = \frac{\lambda e^{-\lambda t}(\lambda t)^4}{4!} = \frac{\lambda e^{-\lambda t}(\lambda t)^4}{\Gamma(5)}.
\end{equation*}

Thus, $T_5 \sim \text{Gamma}(5, \lambda)$, meaning the time until the 5th goal follows a Gamma distribution with shape parameter $5$ and rate parameter $\lambda$.
For example, to find the probability of scoring 5 goals in the first 45 minutes, we compute:
\begin{equation*}
\mathbb{P}[T_5 \leq 45] = \int_0^{45} f_{T_5}(t) \, dt = \int_0^{45} \frac{\lambda e^{-\lambda t}(\lambda t)^4}{\Gamma(5)} \, dt.
\end{equation*}
Substituting $\lambda = 0.03$:
\begin{equation*}
\mathbb{P}[T_5 \leq 45] = \frac{1}{\Gamma(5)} \int_0^{45} 0.03 \cdot e^{-0.03 t}(0.03 t)^4 \, dt.
\end{equation*}
Evaluating this integral gives approximately $0.01$, meaning there is about a 1% chance of scoring 5 goals within 45 minutes.

Generalizing beyond this example, the Gamma distribution has a close relationship with the Poisson process, summarized as follows.

```{admonition} Connection between the Gamma and Exponential distributions
If $Y_1, Y_2, \dots, Y_j \sim \text{Expo}(\lambda)$ are independent, then their sum $Y_1 + Y_2 + \cdots + Y_j$ follows a Gamma distribution:
\begin{equation*}
Y_1 + Y_2 + \cdots + Y_j \sim \text{Gamma}(j, \lambda).
\end{equation*}
```

To summarize, for a Poisson process with rate $\lambda$:

1. The number of arrivals in an interval of length $t$ follows the $\text{Pois}(\lambda t)$ distribution,
2. The time between consecutive arrivals follows the $\text{Expo}(\lambda)$ distribution,
3. The time of the $j^{\text{th}}$ arrival follows the $\text{Gamma}(j, \lambda)$ distribution.