# Probability and counting

```{contents}
:local:
```

## Sets

In probability, the primary goal is to determine how likely a specific **set** of outcomes is, given a particular experiment. In this section, we'll focus on understanding the concept of *sets*, which form the foundation of probability theory.

```{warning}
This first section will admittedly be a bit dry, but bear with me! For the rest of the class, it's necessary that we're all completely comfortable with these definitions and notations.
```

A *set* is a collection of objects or elements. For example, the set $\{1, 3, 5, 7\}$ contains four numbers, while the outcomes from flipping a coin twice form the set $\{HH, HT, TH, TT\}$ (where $H$ stands for Heads and $T$ stands for Tails). There’s also the empty set, denoted $∅$, which contains no elements.

**Subsets.** If every element in the set $A$ is also in the set $B$, then $A$ is called a *subset* of $B$, represented as $A \subseteq B$. For example, $\{HH, HT\} \subseteq \{HH, HT, TH, TT\}$.

**Elements of sets.** When we use the notation $a \in A$, it means that $a$ is an element of set $A$. Meanwhile, the notation $a \notin A$ means that $a$ is not an element of $A$.   For example, $1 \in \{1, 3, 5, 7\}$, but $2 \notin \{1, 3, 5, 7\}$.

**Unions and intersections.** Key operations involving sets include the *union* and *intersection*. The *union* of two sets, denoted $A \cup B$, is the set of elements that are in either $A$ or $B$, or both. See {numref}`Figure {number} <union>` for an illustration.
```{figure} images/union.png
---
name: union
width: 200px
align: center
---

Union $A\cup B$
```
The *intersection*, $A \cap B$, contains the elements that are in both sets, as in {numref}`Figure {number} <intersection>`.
```{figure} images/intersection.png
---
name: intersection
width: 200px
align: center
---

Intersection $A \cap B$
```

If two sets share no elements, they are called *disjoint*, meaning $A \cap B = \emptyset$, as in {numref}`Figure {number} <disjoint>`.
```{figure} images/disjoint.png
---
name: disjoint
width: 200px
align: center
---

Disjoint sets
```

**Complements.** Often, we work with sets that are part of a larger set, called a *sample space*. The *complement* of a set $A$, denoted $A^c$, consists of elements in the sample space that are not in $A$, as illustrated in {numref}`Figure {number} <complement>`.
```{figure} images/complement.png
---
name: complement
width: 200px
align: center
---

Complement $A^c$
```

**Cardinality.** The final definition we'll cover in this section is the *cardinality* of a set, which is the number of elements in the set, denoted $|A|$.   For example, if $A = \{1, 3, 5, 7\}$, then $|A| = 4$.

## Sample spaces and events

The *sample space* of an experiment, typically denoted as $S$, is the set of all possible outcomes of that experiment. For instance, if our experiment involves flipping two coins, the sample space is $\{HH, HT, TH, TT\}$. An *event* is a subset of the sample space. For example, the event that exactly one coin lands Heads is represented by the subset $\{HT, TH\}$.

```{admonition} Example: Deck of cards
:class: tip
This is Example 1.2.3 by {cite}`Blitzstein19:Introduction`.

Suppose we have a standard deck of 52 cards, and our experiment is drawing a single card. In this case, the sample space $S$ is the set of all 52 cards. We can define many events based on this experiment. For example:

- Let $A$ be the event that the card drawn is an ace. In other words,  
  $A = \{\text{Ace of Diamonds, Ace of Clubs, Ace of Hearts, Ace of Spades}\}$, and $|A| = 4$.
- Let $B$ be the event that the card drawn has a black suit (i.e., clubs or spades).
- Let $C$ be the event that the card drawn is a diamond.
- Let $D$ be the event that the card drawn is a heart.

We can also define intersections and unions of events. For example:

- $A \cap D$ is the event that the card is the Ace of Hearts.
- $A \cap B$ is the event that the card is either the Ace of Spades or the Ace of Clubs.
- $A \cup C \cup D$ is the event that the card is either red (i.e., it is a diamond or heart) or an ace.
- Finally, $(A \cup B)^c = A^c \cap B^c$ is the event that the card is a red non-ace.
```

```{admonition} Example: Soccer
:class: tip
Suppose our experiment is a soccer match where Arsenal plays Liverpool. In this case, the sample space $S = \{\text{Arsenal wins, Liverpool wins, draw}\}$ is the set of possible outcomes. We could define the event $A$ to capture the scenario where Arsenal doesn't win, i.e., $A = \{\text{Liverpool wins, draw}\}$.
```

```{admonition} Example: Stocks
:class: tip
We can also view a stock's performance over time as an experiment. For example, suppose we track its price over the course of a month. A simple example of a sample space for this experiment would be $S = \{\text{price goes up, price goes down, price stays the same}\}$. We could define the event $A$ to capture the scenario where the stock price doesn't go up, i.e., $A = \{\text{price goes down, price stays the same}\}$.
```

## A naive definition of probability

As described at the beginning, the primary goal in probability is to determine how likely a specific set of outcomes is, given a particular experiment. Given an event $A$ (such as Arsenal not winning a match or a stock price not rising), our goal will be to determine how likely that event is to occur. We will refer to this likelihood as the *probability of the event $A$*.

In this class, we will begin with a very basic, naive method for calculating the probability of the event $A$, which we will denote as $\mathbb{P}_{\text{naive}}[A]$. This method is only to build intuition. In the next class, with this intuition, we will be ready to move on to the actual, non-naive definition of probability.

The first method you might try to calculate the likelihood of an event $A$ is to count the number of outcomes where that event happens---which we will call the number of "favorable" outcomes---and divide it by the total number of possible outcomes. Since $A$ is a set of outcomes, we know that the number of favorable outcomes is $|A|$ and the number of possible outcomes is the size of the sample space $|S|$. In other words,  
\begin{equation*}
\mathbb{P}_{\text{naive}}[A] = \frac{\# \text{favorable outcomes}}{\# \text{possible outcomes}} = \frac{|A|}{|S|}.
\end{equation*}

For example, suppose we flip two coins, and $A = \{HT, TH\}$ is the event that exactly one Head appears. Then  
\begin{equation*}
\mathbb{P}_{\text{naive}}[A] = \frac{|A|}{|S|} = \frac{2}{4}.
\end{equation*}
Intuitively, this makes sense!

Similarly, suppose we pick a card from a standard deck. Let $A$ be the event that we draw the Ace of Spades or the Ace of Clubs. Then  
\begin{equation*}
\mathbb{P}_{\text{naive}}[A] = \frac{|A|}{|S|} = \frac{2}{52}.
\end{equation*}

Remember that the complement of $A$, denoted $A^c$, consists of the elements in the sample space that are not in $A$. Therefore, the probability that event $A$ does not happen is $\mathbb{P}_{\text{naive}}[A^c]$, which we can calculate as:  
\begin{equation*}
\mathbb{P}_{\text{naive}}[A^c] = \frac{|A^c|}{|S|} = \frac{|S| - |A|}{|S|} = 1 - \mathbb{P}_{\text{naive}}[A].
\end{equation*}

This naive approach to probability assumes that all outcomes are equally likely and that the number of possible outcomes is finite. However, in many cases, such as predicting the outcome of a soccer match, not all outcomes are equally likely (e.g., Arsenal winning versus Liverpool winning). Therefore, we will require a more sophisticated approach to calculating probabilities, which we will introduce in the next section.