# Continuous random variables

```{contents}
:local:
```

Up to this point, we have focused on discrete random variables, which have values that can be written down as a list. In this chapter, we will explore *continuous random variables*, which can assume any real value within a given interval—potentially extending infinitely, from $-\infty$ to $\infty$.

## Probability density functions

To build intuition, recall that for a discrete RV $X$ with PMF $f_X(x) = \mathbb{P}[X = x]$, we can calculate the probability it falls within some interval by summing up its PMF in this interval. For example, if $X \sim \text{Bin}(4, 0.5)$, for example, then $\mathbb{P}[1 \leq X \leq 3] = \mathbb{P}[X = 1] + \mathbb{P}[X = 2] + \mathbb{P}[X = 3] = f_X(1) + f_X(2) + f_X(3).$

A continuous RV has a *probability density function (PDF)* that’s defined similarly. In particular, we say that the RV $X$ has PDF $f_X(x)$ if $\mathbb{P}[a \leq X \leq b] = \int_a^b f_X(x) \, dx$. The only difference here is that instead of summing up the PMF over the discrete values, we are taking the integral over a continuous range (this intuitively makes sense since, as we learn in calculus class, an integral is a continuous version of a summation). The PDF of a continuous RV is illustrated in the following figure.
```{figure} images/pdf.png
---
name: pdf
width: 225px
align: center
---

This is Figure 5.2 from {cite}`Blitzstein19:Introduction`. It illustrates the PDF of a continuous RV $X$. To calculuate $\mathbb{P}[-2 \leq X \leq 2]$, we compute the integral of the function between $-2$ and $2$, which is the shaded region.
```
To be a valid PDF, it must be the case that $f_X(x) \geq 0$ and $\int_{-\infty}^\infty f_X(x) \, dx = 1$.

It immediately follows that a continuous RV’s cumulative distribution function (CDF) is defined as $F_X(x) = \mathbb{P}[X \leq x] = \int_{-\infty}^x f_X(t) \, dt$. Remembering the fundamental theorem of calculus, it follows that if we know a RV’s CDF, we can figure out its PDF by taking the derivative: $f_X(x) = F'_X(x)$. The CDF also allows us to easily compute the probability $X$ falls within an interval: $\mathbb{P}[a < X < b] = \int_a^b f_X(x) \, dx = F_X(b) - F_X(a)$.

It’s important to understand the differences between a discrete RV’s PMF and a continuous RV’s PDF. If we evaluate the PDF of a continuous RV $X$ at some number, say 3, it’s important to remember that $f_X(3) \not= \mathbb{P}[X=3]$ because, by definition, $\mathbb{P}[X = 3] = \int_3^3 f_X(x) \, dx = 0$. However, it is the case that the probability $X$ is in some tiny interval $(3, 3 + \epsilon)$ is *approximately* $f_X(3)\epsilon$:

\begin{equation*}\mathbb{P}\left[3 < X < 3 + \epsilon \right] = \int_{3}^{3 + \epsilon} f_X(x) \, dx \approx f_X(3)\epsilon.

\end{equation*}

Building on the intuition that an integral is just a continuous version of a sum, we define the expected value of a continuous RV in exactly the way you would expect:
\begin{equation*}

\mathbb{E}[X] = \int_{-\infty}^{\infty} x f_X(x) \, dx.

\end{equation*}

Similarly, even the law of the unconscious statistician (LOTUS) carries over directly:
\begin{equation*}

\mathbb{E}[g(X)] = \int_{-\infty}^{\infty} g(x) f_X(x) \, dx.

\end{equation*}

In the following table, we summarize the continuous analog of the concepts we learned for discrete RVs.

| **Discrete**                                        | **Continuous**                                                  |
|-----------------------------------------------------|------------------------------------------------------------------|
| $ X $ takes on values from a list $ x_1, x_2, \dots $ | $ X $ can be anything between $ -\infty $ and $ \infty $  |
| PMF $ f_X(x) = \mathbb{P}[X = x] $                        | PDF $ f_X(x) $ (but $ \mathbb{P}[X = x] = 0 $)                       |
| CDF $ F_X(x) = \mathbb{P}[X \leq x] = \sum_{x_i \leq x} f_X(x_i) $ | CDF $ F_X(x) = \mathbb{P}[X \leq x] = \int_{-\infty}^x f_X(t) \, dt $ |
| Expectation $ \mathbb{E}[X] = \sum x f_X(x) $             | $ \mathbb{E}[X] = \int_{-\infty}^{\infty} x f_X(x) \, dx $             |
| LOTUS $ \mathbb{E}[g(X)] = \sum g(x) f_X(x) $             | $ \mathbb{E}[g(X)] = \int_{-\infty}^{\infty} g(x) f_X(x) \, dx $       |

## Uniform

For a given interval $(a, b)$, a uniform random variable represents a "completely random" point somewhere between $ a $ and $ b $. In a uniform distribution, the probability of selecting a point within any sub-interval is proportional to the length of that interval.

If we denote this random variable as $ X \sim \text{Unif}(a, b) $, then its probability density function (PDF) $ f_X(x) $ is defined as:
\begin{equation*}
f_X(x) =
\begin{cases}
c & \text{if } a \leq x \leq b \\
0 & \text{else}
\end{cases}
\end{equation*}
To determine the value of $ c $, we use the fact that the total area under the PDF over the interval $(a, b)$ must be equal to 1. This means:
\begin{equation*}
1 = \int_{-\infty}^{\infty} f_X(x) \, dx = \int_{-\infty}^a 0 \, dx + \int_a^b c \, dx + \int_b^{\infty} 0 \, dx = 0 + c(b - a) + 0.
\end{equation*}
Solving for $ c $ gives:
\begin{equation*}
c = \frac{1}{b - a}.
\end{equation*}

Thus, for a uniform random variable $ X $ over $(a, b)$, the PDF is $ f_X(x) = \frac{1}{b - a} $ for $ a \leq x \leq b $ and 0 otherwise. For example, if $ X \sim \text{Unif}(0, 1) $, then the PDF is:
\begin{equation*}
f_X(x) =
\begin{cases}
1 & \text{if } 0 \leq x \leq 1 \\
0 & \text{else}
\end{cases}
\end{equation*}

Meanwhile, if $ X \sim \text{Unif}\left(\frac{1}{2}, 1\right) $, then the PDF is:
\begin{equation*}
f_X(x) =
\begin{cases}
\frac{1}{1 - \frac{1}{2}} = 2 & \text{if } \frac{1}{2} \leq x \leq 1 \\
0 & \text{else}
\end{cases}
\end{equation*}

The CDF of a continuous uniform random variable $ X $ over an interval $(a, b)$ is defined  as follows:
1. **When $ x < a $**: Since $ x $ is less than the lower bound $ a $, the probability $ \mathbb{P}[X \leq x] $ is zero. Mathematically, $\mathbb{P}[X \leq x] = \int_{-\infty}^x 0 \, dt = 0.$
2. **When $ a \leq x \leq b $**: In this case, $ x $ falls within the interval $(a, b)$, so we calculate $ \mathbb{P}[X \leq x] $ by integrating $ f_X(t) $ from $ a $ to $ x $: $\mathbb{P}[X \leq x] = \int_a^x f_X(t) \, dt = \int_a^x \frac{1}{b - a} \, dt = \frac{x - a}{b - a}.$
3. **When $ x > b $**: Here, $ x $ is greater than the upper bound $ b $, meaning $ X $ is certainly less than or equal to $ x $, so $ \mathbb{P}[X \leq x] = 1 $.

To summarize, the CDF $ F_X(x) = \mathbb{P}[X \leq x] $ for a uniform random variable $ X \sim \text{Unif}(a, b) $ is:
\begin{equation*}
F_X(x) = \begin{cases}
0 & \text{if } x < a \\
\frac{x - a}{b - a} & \text{if } a \leq x \leq b \\
1 & \text{if } x > b.
\end{cases}
\end{equation*}

For example, if $ X \sim \text{Unif}(0, 1) $, the CDF becomes:
\begin{equation*}
F_X(x) = \begin{cases}
0 & \text{if } x < 0 \\
x & \text{if } 0 \leq x \leq 1 \\
1 & \text{if } x > 1.
\end{cases}
\end{equation*}

The following figure illustrates the PDF and CDF of the $\text{Unif}(0, 1) $ distribution.
```{figure} images/uniform.png
---
name: uniform
width: 475px
align: center
---

This is Figure 5.6 from {cite}`Blitzstein19:Introduction`. It illustrates the PDF and CDF of the $\text{Unif}(0, 1) $ distribution.
```

### Expectation of $ X $

The expectation of $ X $ is given by:
\begin{equation*}
\mathbb{E}[X] = \int_{-\infty}^{\infty} x f_X(x) \, dx = \int_a^b \frac{x}{b - a} \, dx.
\end{equation*}
Evaluating this integral, we find:
\begin{equation*}
\mathbb{E}[X] = \left. \frac{x^2}{2(b - a)} \right|_a^b = \frac{b^2 - a^2}{2(b - a)} = \frac{a + b}{2}.
\end{equation*}
For a uniform random variable $ X \sim \text{Unif}(0, 1) $, this yields $ \mathbb{E}[X] = \frac{0 + 1}{2} = \frac{1}{2} $.

### Variance of $ X $

The variance of $ X $ is $ \text{Var}(X) = \mathbb{E}[X^2] - \mathbb{E}[X]^2 $. First, we calculate $ \mathbb{E}[X^2] $ using LOTUS:
\begin{equation*}
\mathbb{E}[X^2] = \int_a^b x^2 f_X(x) \, dx = \left. \frac{x^3}{3(b - a)} \right|_a^b = \frac{b^3 - a^3}{3(b - a)}.
\end{equation*}
Then, the variance becomes:
\begin{equation*}
\text{Var}(X) = \frac{b^3 - a^3}{3(b - a)} - \left(\frac{a + b}{2}\right)^2 = \frac{(b - a)^2}{12}.
\end{equation*}