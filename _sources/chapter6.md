# Joint distributions

```{contents}
:local:
```

Until now, whenever we have analyzed multiple random variables in a single problem, we have assumed they were independent—that is, information about one random variable gave us no insight into the others. While independence is a useful assumption for simplifying calculations, most random variables are not independent. In this chapter, we will develop tools to jointly analyze *dependent* random variables.

## Joint, marginal, and conditional

### Discrete

Let $ X $ and $ Y $ be two discrete random variables.

```{admonition} Joint cumulative distribution function (CDF)
The *joint CDF* of $ X $ and $ Y $, denoted $ F_{X,Y}(x,y) $, is defined as the probability that $ X \leq x $ and $ Y \leq y $, or $ F_{X,Y}(x,y) = \mathbb{P}[X \leq x, Y \leq y] $.
```

```{figure} images/joint_PMF.png
---
name: joint_pmf
width: 400px
align: center
---

This is Figure 7.1 from {cite}`Blitzstein19:Introduction`. It illustrates the joint PMF of two RVs $X$ and $Y$.
```

```{admonition} Joint probability mass function (PMF)
The *joint PMF* of $ X $ and $ Y $, denoted $ f_{X,Y}(x,y) $, is the probability that $ X = x $ and $ Y = y $, or $ f_{X,Y}(x,y) = \mathbb{P}[X = x, Y = y] $. See {numref}`Figure {number} <joint_pmf>` for an illustration.
```
```{figure} images/marginal_PMF.png
---
name: marginal_pmf
width: 375px
align: center
---

This is Figure 7.2 from {cite}`Blitzstein19:Introduction`. It is a bird's-eye view of the PMF in {numref}`Figure {number} <joint_pmf>`. As {cite}`Blitzstein19:Introduction` states, the marginal PMF $f_X(x)$ is obtained by summing over the joint PMF in the $y$-direction.
```

```{admonition} Marginal PMF
We obtain the *marginal PMF* of $ X $, $ f_X(x) = \mathbb{P}[X = x] $, via the law of total probability: we sum over the joint probabilities over all possible values of $ Y $, so 
\begin{equation*}
f_X(x) = \mathbb{P}[X = x] = \sum_y \mathbb{P}[X = x, Y = y] = \sum_y f_{X,Y}(x,y).
\end{equation*}
The marginal PMF of $Y$, $f_Y(y)$, is defined symmetrically. See {numref}`Figure {number} <marginal_pmf>` for an illustration.
```

```{figure} images/conditional_PMF.png
---
name: conditional_pmf
width: 600px
align: center
---

This is Figure 7.3 from {cite}`Blitzstein19:Introduction`. To obtain the conditional PMF $\mathbb{P}[Y = y \mid X = x]$, we renormalize the slice of the joint PMF that corresponds to the event that $X = x$.
```

```{admonition} Conditional PMF
The *conditional PMF* of $ Y $ given $ X = x $, $ \mathbb{P}[Y = y \mid X = x] $, represents the probability that $ Y = y $ given that $ X = x $. It is calculated using the definition of conditional probability 
\begin{equation*}
\mathbb{P}[Y = y \mid X = x] = \frac{\mathbb{P}[X = x, Y = y]}{\mathbb{P}[X = x]},
\end{equation*}
assuming $ \mathbb{P}[X = x] > 0.$ The conditional PMF of $X$ given $Y = y$ is defined symmetrically. See {numref}`Figure {number} <conditional_pmf>` for an illustration.
```


```{list-table} Joint PMF of $ X $ and $ Y $ for the following basketball free throw example.
:header-rows: 1
:name: free_throw

* - 
  - **$ Y = 1 $**
  - **$ Y = 0 $**
* - **$ X = 1 $**
  - $ f_{X,Y}(1,1) = \mathbb{P}[X = 1, Y = 1] = \frac{5}{100} $
  - $ f_{X,Y}(1,0) = \frac{20}{100} $
* - **$ X = 0 $**
  - $ f_{X,Y}(0,1) = \frac{3}{100} $
  - $ f_{X,Y}(0,0) = \frac{72}{100} $
``` 

```{admonition} Example: Basketball free throws
:class: tip

Suppose we want to analyze the likelihood of a player making two consecutive free throws in a game. Let $ X $ be an indicator variable representing whether a player makes the first free throw (1 if they make it, 0 if they miss), and $ Y $ is an indicator variable representing whether they make the second free throw.

The joint PMF of $X$ and $Y$ is given in {numref}`free_throw`.

The marginal PMF of $X$ is $f_X(0) = \mathbb{P}[X = 0] = f_{X,Y}(0,0) + f_{X,Y}(0,1) = \frac{25}{100}$ and $f_X(1) = \mathbb{P}[X = 1] = f_{X,Y}(1,0) + f_{X,Y}(1,1) = \frac{75}{100}$. Similarly, the marginal PMF of $Y$ is $f_Y(0) = f_{X,Y}(0,0) + f_{X,Y}(1,0) = \frac{8}{100}$ and $f_Y(1) = f_{X,Y}(0,1) + f_{X,Y}(1,1) = \frac{92}{100}$.

Finally, the conditional PMF of $X$ given $Y = 0$, for example, is $\mathbb{P}[X = 0 \mid Y = 0] = \frac{f_{X,Y}(0,0)}{f_Y(0)} = \frac{5/100}{8/100} = \frac{5}{8}$ and $\mathbb{P}[X = 1 \mid Y = 0] = 1- \frac{5}{8} = \frac{3}{8}.$
```

```{admonition} Independence
Two random variables $ X $ and $ Y $ are said to be independent if their joint cumulative distribution function (CDF) $ F_{X,Y}(x,y) $ can be expressed as the product of their individual CDFs, $ F_X(x) $ and $ F_Y(y) $, for all values of $ x $ and $ y $. In other words, $ X $ and $ Y $ are independent if $ F_{X,Y}(x,y) = F_X(x)F_Y(y) $ holds for all possible pairs of values.

An equivalent condition for independence is that the joint probability mass function (PMF) $ f_{X,Y}(x,y) $ can be factored as the product of the marginal PMFs of $ X $ and $ Y $, i.e., $ f_{X,Y}(x,y) = f_X(x)f_Y(y) $.
```

```{list-table} Joint PMF for the following coin flip example
:header-rows: 1
:name: joint_pmf_coin

* - 
  - **$ Y = 0 $**
  - **$ Y = 1 $**
* - **$ X = 0 $**
  - $ f_{X,Y}(0,0) = \mathbb{P}[X = 0, Y= 0] = 0 $
  - $ f_{X,Y}(0,1) =\mathbb{P}[X = 0, Y = 1] = \mathbb{P}[X = 0] = \frac{1}{4} $
* - **$ X = 1 $**
  - $ f_{X,Y}(1,0) =\mathbb{P}[X = 1, Y= 0] = \mathbb{P}[X = 1] = \frac{1}{2} $
  - $ f_{X,Y}(1,1) =0 $
* - **$ X = 2 $**
  - $ f_{X,Y}(2,0) =0 $
  - $ f_{X,Y}(2,1) =\frac{1}{4} $
```

```{admonition} Example: Coin flips
:class: tip

Suppose a fair coin is flipped twice. Let the random variable $ X $ represent the number of heads obtained in the two flips. Define another random variable, $ Y $, such that $ Y = 1 $ if both tosses landed the same way (either both heads or both tails), and $ Y = 0 $ otherwise.

**Question 1:** What is the joint probability mass function (PMF) of $ X $ and $ Y $?

The joint PMF of $ X $ and $ Y $ is given in {numref}`joint_pmf_coin`.

**Question 2:** What is the marginal PMF of $ X $?

The marginal PMF of $ X $, representing the probability distribution of the number of heads, is calculated as follows:

- $ f_X(0) = \mathbb{P}[X = 0] = \mathbb{P}[X = 0, Y = 0] + \mathbb{P}[X = 0, Y = 1] = \frac{1}{4} $
- $ f_X(1) = \mathbb{P}[X = 1, Y = 0] + \mathbb{P}[X = 1, Y = 1] = \frac{1}{2} $
- $ f_X(2) = \frac{1}{4} $

**Question 3:** What is the marginal PMF of $ Y $?

The marginal PMF of $ Y $, representing the probability of the tosses landing the same way or not, is calculated as follows:

- $ f_Y(0) = \mathbb{P}[Y = 0] = \mathbb{P}[X = 0, Y = 0] + \mathbb{P}[X = 1, Y = 0] + \mathbb{P}[X = 2, Y = 0] = \frac{1}{2} $
- $ f_Y(1) = \frac{1}{2} $

**Question 4:** Are $ X $ and $ Y $ independent?

No, $ X $ and $ Y $ are not independent. For example, the joint probability $ f_{X,Y}(0,0) = 0 $ does not equal the product of the marginals $ f_X(0)f_Y(0) = \frac{1}{4} \cdot \frac{1}{2} = \frac{1}{8} $.
```

### Continuous

Next, let $X$ and $Y$ be two continuous RVs. In this case, the definition of the joint CDF remains the same:

```{admonition} Joint cumulative distribution function (CDF)
The *joint CDF* of $ X $ and $ Y $, denoted $ F_{X,Y}(x,y) $, represents the probability that $ X \leq x $ and $ Y \leq y $, or $ F_{X,Y}(x,y) = \mathbb{P}[X \leq x, Y \leq y] $.
```

Recall that in the case of a single continuous RV, we obtain the PDF by taking the derivative of the CDF. The same holds true when working with joint continuous RVs, except we must take the derivate in terms of $x$ and $y$.

```{admonition} Joint probability density function (PDF)
The *joint PDF* of $ X $ and $ Y $, denoted $ f_{X,Y}(x,y) $, is obtained by taking the second partial derivative of the joint CDF with respect to both $ x $ and $ y $. In other words, $ f_{X,Y}(x,y) = \frac{\partial^2}{\partial x \partial y}F_{X,Y}(x,y) $.
```
```{admonition} Marginal PMF
The marginal PDF of $ X $, denoted $ f_X(x) $, is obtained by integrating the joint PDF over all values of $ Y $. This is expressed as $ f_X(x) = \int_{-\infty}^{\infty} f_{X,Y}(x,y) \, dy $.
```

```{admonition} Example: Uniform distribution over a square
:class: tip

Suppose $ (X, Y) $ is a completely random point chosen uniformly from within the square region $ \{(x,y): x, y \in [0,1]\} $ in the plane. This means that any point within the square is equally likely to be chosen.

The joint probability density function (PDF) of $ X $ and $ Y $, $ f_{X,Y}(x,y) $, is defined as follows:

\begin{equation*}f_{X,Y}(x,y) = \begin{cases}1 &\text{if }(x,y) \in [0,1] \times [0,1]\\ 0 &\text{else.}\end{cases}\end{equation*}

To find the marginal PDF of $ X $, denoted $ f_X(x) $, we integrate $ f_{X,Y}(x,y) $ over all possible values of $ y $:

\begin{equation*}
f_X(x) = \int_{-\infty}^{\infty} f_{X,Y}(x,y) \, dy = \int_{-\infty}^0 0 \, dy + \int_0^1 1 \, dy + \int_1^{\infty} 0 \, dy = y \Big|_{0}^1 = 1.
\end{equation*}

This result implies that $ X $ follows a uniform distribution on the interval $ [0,1] $, or $ X \sim \text{Unif}(0,1) $.

Since the joint PDF $ f_{X,Y}(x,y) $ can be factored as the product of the marginal PDFs of $ X $ and $ Y $ for all $ x, y \in [0,1] \times [0,1] $, i.e., $ f_{X,Y}(x,y) = 1 = f_X(x) f_Y(y) $, we conclude that $ X $ and $ Y $ are independent.

```

```{figure} images/circle.png
---
name: circle
width: 275px
align: center
---

This is Figure 7.6 from {cite}`Blitzstein19:Introduction`. For a fixed $x \in [-1,1]$, $(x,y)$ is in the unit circle centered at the origin if $x^2 + y^2 \leq 1$, or in other words, if $-\sqrt{1 - x^2} \leq y \leq \sqrt{1 - x^2}$.
```

```{admonition} Example: Uniform distribution over a circle
:class: tip

Suppose $ (X, Y) $ is a completely random point chosen uniformly from within a circle of radius 1, centered at the origin. This region can be described as $ \{(x, y) : x^2 + y^2 \leq 1\} $. Any point within this circle is equally likely to be chosen.

The joint probability density function (PDF) of $ X $ and $ Y $, denoted $ f_{X,Y}(x, y) $, is defined as follows:

\begin{equation*}f_{X,Y}(x,y) = \begin{cases} \frac{1}{\pi} & \text{if }x^2 + y^2\leq 1\\
0 &\text{else}\end{cases}\end{equation*}
(understanding why the PDF is $\frac{1}{\pi}$ inside the circle requires comfort with multi-variable integration, so you may take this as given—don’t worry if you don’t know how we arrived at $\frac{1}{\pi}$).

To find the marginal PDF of $ X $, denoted $ f_X(x) $, we integrate $ f_{X,Y}(x, y) $ over all possible values of $ y $:

\begin{equation*}
f_X(x) = \int_{-\infty}^{\infty} f_{X,Y}(x, y) \, dy.
\end{equation*}

We know that $f_{X,Y}(x, y) = \frac{1}{\pi}$ so long as $(x,y)$ is in the circle of radius 1, centered at the origin, or in other words, so long as $x^2 + y^2\leq 1$. Looking at {numref}`circle`, we can see that for a specific choice of $x \in [-1,1]$, $f_{X,Y}(x, y) = \frac{1}{\pi}$ so long as $-\sqrt{1 - x^2} \leq y \leq \sqrt{1 - x^2}$. Otherwise, $f_{X,Y}(x, y) = 0$. Therefore, for $x \in [-1,1]$,

\begin{equation*}
f_X(x) = \int_{-\infty}^{-\sqrt{1 - x^2}} 0 \, dy + \int_{-\sqrt{1 - x^2}}^{\sqrt{1 - x^2}} \frac{1}{\pi} \, dy + \int_{\sqrt{1 - x^2}}^{\infty} 0 \, dy = \left. \frac{y}{\pi} \right|_{-\sqrt{1 - x^2}}^{\sqrt{1 - x^2}} = \frac{2}{\pi} \sqrt{1 - x^2}.
\end{equation*}

For $x \not\in [-1,1]$, $f_X(x) = 0$.

This result shows that $ X $ does not follow a uniform distribution, as $ f_X(x) $ depends on $ x $ in a non-constant way.

Moreover, $ X $ and $ Y $ are not independent. For example, $ f_{X,Y}(0.9, 0.9) = 0 $, because the point $ (0.9, 0.9) $ lies outside the circle (as $ 0.9^2 + 0.9^2 > 1 $), even though both $ f_X(0.9) $ and $ f_Y(0.9) $ are non-zero. This demonstrates that the joint probability does not equal the product of the marginals, confirming that $ X $ and $ Y $ are dependent.
```

### Hybrid

```{admonition} Example: Injury recovery time
:class: tip

Suppose an athlete has sustained an injury, but it is unclear whether the injury is minor or major.

- If the injury is minor, the time it takes to heal follows an exponential distribution with rate $ \lambda_0 $ (so the expected healing time is $ \frac{1}{\lambda_0} $).
- If the injury is major, the healing time follows an exponential distribution with rate $ \lambda_1 $ (with expected healing time $ \frac{1}{\lambda_1} $).
- We assume that $ \lambda_0 > \lambda_1 $, meaning that minor injuries generally heal faster than major ones.

The injury is major with probability $ p_1 $ and as minor with probability $ p_0 = 1 - p_1 $. Let $ I $ be an indicator random variable, where $ I = 1 $ if the injury is major and $ I = 0 $ if it is minor. Let $ T $ represent the time it takes for the injury to heal.

**Question:** What is the marginal cumulative distribution function (CDF) of $ T $?

The marginal CDF of $ T $, denoted $ F_T(t) $, can be computed as follows:

\begin{equation*}
F_T(t) = \mathbb{P}[T \leq t] = \mathbb{P}[T \leq t \mid I = 0] \cdot \mathbb{P}[I = 0] + \mathbb{P}[T \leq t \mid I = 1] \cdot \mathbb{P}[I = 1].
\end{equation*}

Substituting the expressions for each conditional probability, we get:

\begin{equation*}
F_T(t) = \left(1 - e^{-\lambda_0 t}\right)p_0 + \left(1 - e^{-\lambda_1 t}\right)p_1 = 1 - p_0 e^{-\lambda_0 t} - p_1 e^{-\lambda_1 t}.
\end{equation*}

**Question:** What is the marginal probability density function (PDF) of $ T $?

The marginal PDF of $ T $, denoted $ f_T(t) $, is the derivative of $ F_T(t) $ with respect to $ t $:

\begin{equation*}
f_T(t) = \frac{d}{dt} F_T(t) = p_0 \lambda_0 e^{-\lambda_0 t} + p_1 \lambda_1 e^{-\lambda_1 t}.
\end{equation*}
```

## 2D LOTUS

The law of the unconscious statistician extends naturally to joint random variables. We will only state it here for discrete RVs (the definition for continuous RVs involves multi-variable integration, which we do not assume knowledge of in this class).

```{admonition} 2D Law of the unconscious statistician (LOTUS)


Let $ g: \mathbb{R}^2 \to \mathbb{R} $ be a function. When $ X $ and $ Y $ are discrete random variables, the expected value of $ g(X, Y) $, denoted $ \mathbb{E}[g(X, Y)] $, is calculated as

\begin{equation*}
\mathbb{E}[g(X, Y)] = \sum_x \sum_y g(x, y) \cdot \mathbb{P}[X = x, Y = y].
\end{equation*}
```

```{list-table} Joint PMF of $ X $ and $ Y $ for shots and goals in soccer
:header-rows: 1
:name: soccer

* - 
  - **$ X = 1 $**
  - **$ X = 2 $**
* - **$ Y = 0 $**
  - $ \frac{3}{10} $
  - $ \frac{2}{10} $
* - **$ Y = 1 $**
  - $ \frac{1}{10} $
  - $ \frac{3}{10} $
* - **$ Y = 2 $**
  - $ 0 $
  - $ \frac{1}{10} $
```

```{admonition} Example: Shots per goal in soccer
:class: tip

In the first 15 minutes of a soccer match, a team will make between 1 and 2 shots on goal. Let $ X $ represent the number of shots taken and $ Y $ represent the number of goals scored. The joint probability distribution of $ X $ and $ Y $ is given by {numref}`soccer`.

**Question:** What is the expected number of goals per shot?

To find this, we calculate $ \mathbb{E}\left[\frac{Y}{X}\right] $ as follows:

\begin{equation*}
\mathbb{E}\left[\frac{Y}{X}\right] = \frac{0}{1} \cdot \frac{3}{10} + \frac{1}{1} \cdot \frac{1}{10} + \frac{0}{2} \cdot \frac{2}{10} + \frac{1}{2} \cdot \frac{3}{10} + \frac{2}{2} \cdot \frac{1}{10} = \frac{7}{20}.
\end{equation*}

Thus, the expected number of goals per shot is $ \frac{7}{20} $.
```