# Combinatorial Analysis (Counting)

*Probability course, lecture 2 (Discrete Probability, Section 3)*

---

## Table of Contents

- [0. Why counting matters](#0-why-counting-matters)
- [1. The multiplication rule](#1-the-multiplication-rule)
- [2. Number of subsets](#2-number-of-subsets)
- [3. Permutations](#3-permutations)
- [4. Choosing k out of n without repetition](#4-choosing-k-out-of-n-without-repetition)
  - [4.1 Ordered selection](#41-ordered-selection)
  - [4.2 Unordered selection and binomial coefficients](#42-unordered-selection-and-binomial-coefficients)
- [5. Partitions and the multinomial coefficient](#5-partitions-and-the-multinomial-coefficient)
- [6. Choosing with repetition](#6-choosing-with-repetition)
  - [6.1 Ordered selection with repetition](#61-ordered-selection-with-repetition)
  - [6.2 Unordered selection with repetition: stars and bars](#62-unordered-selection-with-repetition-stars-and-bars)
- [7. The big decision table](#7-the-big-decision-table)
- [8. The link with probability](#8-the-link-with-probability)
- [9. Worked examples](#9-worked-examples)
- [10. Method checklist for any counting exercise](#10-method-checklist-for-any-counting-exercise)
- [11. Common mistakes](#11-common-mistakes)
- [12. Practice problems](#12-practice-problems)

---

## 0. Why counting matters

With equally likely outcomes on a finite sample space $\Omega$:

$$P(A) = \frac{|A|}{|\Omega|}$$

So every such probability problem becomes two counting problems: count $|\Omega|$ and count $|A|$. The whole lecture is a toolbox for counting quickly and correctly.

The most important habit: **before using any formula, decide what the objects are, whether order matters, and whether repetition is allowed.** Most mistakes come from skipping this.

[Back to top](#table-of-contents)

---

## 1. The multiplication rule

**Statement.** Take finite sets $\Omega_1, \dots, \Omega_N$ with $|\Omega_k| = n_k$. If you choose one element from $\Omega_1$ ($n_1$ options), then one from $\Omega_2$ ($n_2$ options), and so on up to $\Omega_N$, the total number of sequences is

$$|\Omega_1 \times \Omega_2 \times \dots \times \Omega_N| = n_1 n_2 \cdots n_N$$

**Why it works.** For each of the $n_1$ first choices there are $n_2$ second choices, so there are $n_1 n_2$ pairs. For each pair there are $n_3$ third choices, and so on. It is a tree: multiply the branching numbers.

**Key subtlety.** The *number* of options at step 2 may depend on step 1, but it must be the *same number* whatever you chose at step 1. This is exactly what happens with $n, n-1, n-2, \dots$ in permutations: the set changes, the count does not.

**Examples.**

- **Restaurant.** 6 starters, 7 main courses, 5 desserts: $6 \times 7 \times 5 = 210$ three-course meals.
- **Three dice.** An even number, then a 6, then a number smaller than 4: $3 \times 1 \times 4 = 12$ outcomes.
- **PIN codes.** 4 digits: $10^4$. With all digits distinct: $10 \cdot 9 \cdot 8 \cdot 7$.

**Companion rules you will constantly need.**

- **Addition rule.** If a task splits into disjoint cases, add the counts of the cases.
- **Complement rule.** $|A| = |\Omega| - |A^c|$. Use it whenever the phrase "at least one" appears.
- **Handle constraints first.** If one position has a restriction, fill it first, then fill the rest.

[Back to top](#table-of-contents)

---

## 2. Number of subsets

A set with $n$ elements has $2^n$ subsets.

**Proof (bijection).** Encode each subset $A$ of $\Omega = \{\omega_1, \dots, \omega_n\}$ by a string of $n$ bits: the $i$-th bit is $1$ if $\omega_i \in A$ and $0$ otherwise. For $n = 4$:

- $\{\omega_1\} \mapsto 1000$
- $\{\omega_1, \omega_3, \omega_4\} \mapsto 1011$
- $\emptyset \mapsto 0000$

This is a bijection between subsets and binary strings of length $n$. Each bit has 2 choices, so by the multiplication rule there are $2^n$ strings, hence $2^n$ subsets.

**Consequences (all the same number).**

- $|\mathcal{F}| = 2^n$, where $\mathcal{F}$ is the $\sigma$-algebra of all events on $\Omega$.
- The number of functions from an $n$-element set to $\{0,1\}$ is $2^n$.
- More generally, the number of functions from a $k$-element set to an $n$-element set is $n^k$.

[Back to top](#table-of-contents)

---

## 3. Permutations

A **permutation** of $n$ distinct objects is an ordering of them, i.e. a bijection from $\{1, \dots, n\}$ to itself.

Choose the image of 1 ($n$ ways), then of 2 ($n-1$ ways), and so on down to the image of $n$ (1 way). By the multiplication rule:

$$n! = n(n-1)(n-2)\cdots 1, \qquad 0! = 1$$

**Examples.**

- 4 books on a shelf: $4! = 24$ arrangements.
- A standard deck of cards: $52!$ orderings (roughly $8 \times 10^{67}$).

**Variations you must know.**

1. **Objects that must stay together.** Glue them into one block, permute the blocks, then permute inside the block.
   *Example: 5 people in a row with A and B adjacent.* The block AB counts as one object, so $4!$ arrangements, times $2!$ orders inside the block, gives $48$.
2. **Objects that must not be adjacent.** Either count everything and subtract the "adjacent" arrangements (complement), or place the other objects first and insert the special ones into the gaps.
3. **Identical objects (anagrams).** If $n$ objects contain groups of $n_1, n_2, \dots, n_k$ identical ones, the number of distinguishable orderings is
   $$\frac{n!}{n_1!\, n_2! \cdots n_k!}$$
   *Example: MISSISSIPPI* has 11 letters (1 M, 4 I, 4 S, 2 P), so there are $\dfrac{11!}{1!\,4!\,4!\,2!} = 34650$ distinct words.
   Reason: $n!$ counts as if all objects were different, so each real arrangement is counted $n_1! \cdots n_k!$ times.
4. **Circular arrangements** (rotations considered the same): $(n-1)!$.

[Back to top](#table-of-contents)

---

## 4. Choosing k out of n without repetition

### 4.1 Ordered selection

Choose $k$ elements from $n$ **keeping track of order**. There are $n$ choices for the first element, $n-1$ for the second, and so on, ending with $n-k+1$ choices for the $k$-th:

$$n(n-1)\cdots(n-k+1) = \frac{n!}{(n-k)!} \tag{3.1}$$

**Second proof.** Take a permutation of all $n$ elements ($n!$ choices) and keep only the first $k$. Each ordered $k$-tuple appears in exactly $(n-k)!$ permutations (the ways of ordering the leftover elements), so divide by $(n-k)!$ and obtain (3.1) again.

**Typical use.** A podium (gold, silver, bronze) among 10 runners: $10 \cdot 9 \cdot 8 = 720$. The roles are distinguishable, so order matters.

### 4.2 Unordered selection and binomial coefficients

To choose $k$ elements **without order**, first choose them with order and then forget the order. Any given set of $k$ elements can be ordered in $k!$ ways, so

$$\binom{n}{k} = \frac{n!}{k!\,(n-k)!}$$

**Typical use.** A committee of 3 chosen among 10 people: $\binom{10}{3} = 120$. Everybody has the same role, so order does not matter.

**Properties (very useful in exercises).**

- **Symmetry:** $\binom{n}{k} = \binom{n}{n-k}$. Choosing who is in is the same as choosing who is out.
- **Edge values:** $\binom{n}{0} = \binom{n}{n} = 1$ and $\binom{n}{1} = n$.
- **Pascal's rule:** $\binom{n}{k} = \binom{n-1}{k-1} + \binom{n-1}{k}$. Focus on one particular element: either it is chosen (pick $k-1$ more from the rest) or it is not (pick all $k$ from the rest).
- **Sum:** $\displaystyle\sum_{k=0}^{n} \binom{n}{k} = 2^n$. This counts all subsets by size and agrees with Section 2.
- **Binomial theorem:** $(a+b)^n = \displaystyle\sum_{k=0}^{n} \binom{n}{k} a^k b^{n-k}$.

**Quick test for "order or not?"** Ask whether swapping two chosen elements gives a different outcome. If yes, order matters.

[Back to top](#table-of-contents)

---

## 5. Partitions and the multinomial coefficient

Let $n_1 + n_2 + \dots + n_k = n$. The number of ways to partition $n$ elements into $k$ subsets of cardinalities $n_1, \dots, n_k$ is

$$\binom{n}{n_1\ n_2\ \cdots\ n_k} = \frac{n!}{n_1!\, n_2! \cdots n_k!}$$

**Derivation.** Choose group 1: $\binom{n}{n_1}$ ways. Then group 2 from what remains: $\binom{n-n_1}{n_2}$ ways. And so on. Multiply, and everything telescopes to $\dfrac{n!}{n_1! \cdots n_k!}$.

**Example (box of balls).** For a box with $n$ balls there are:

- $\dfrac{n!}{(n-k)!}$ ordered ways to pick $k$ balls,
- $\dbinom{n}{k}$ unordered ways to pick $k$ balls,
- $\dbinom{n}{n_1\ n_2\ n_3}$ ways to subdivide the balls into 3 groups of $n_1$, $n_2$, $n_3$ balls each.

**Warning: labelled versus unlabelled groups.** The formula treats the groups as distinguishable (group 1 is "the group of size $n_1$", and so on).

- If the groups have **different sizes**, they are automatically distinguishable: the formula is correct as it stands.
- If some groups have the **same size and are interchangeable**, divide by the number of ways of shuffling those groups.
  *Example: split 6 people into 3 unlabelled pairs.* Labelled version: $\dfrac{6!}{2!\,2!\,2!} = 90$. Divide by $3! = 6$ to get $15$.

Note that the anagram formula of Section 3 and the multinomial coefficient are the same formula: each position receives a "label" telling which group it belongs to.

[Back to top](#table-of-contents)

---

## 6. Choosing with repetition

Now each element may be picked several times (for instance, each ball is put back in the box after being drawn).

### 6.1 Ordered selection with repetition

There are $n$ choices for the first element, $n$ for the second, and so on:

$$n^k = n \times n \times \dots \times n$$

**Typical use.** 3 draws with replacement from an urn of 10 balls: $10^3$. Words of length $k$ over an alphabet of $n$ letters: $n^k$.

### 6.2 Unordered selection with repetition: stars and bars

Suppose we choose $k$ elements from $n$, allowing repetitions but discarding the order. Note that naively dividing $n^k$ by $k!$ does **not** give the right answer, because of repetitions.

Instead, label the elements $1, 2, \dots, n$ and, for each element, draw a $\ast$ each time it is picked:

```
 1     2    3   ...   n
 **    *        ...  ***
```

There are $k$ stars and $n-1$ vertical bars. Now delete the numbers:

$$\ast\ast \mid \ast \mid \mid \dots \mid \ast\ast\ast$$

This diagram uniquely identifies an unordered selection of $k$ (possibly repeated) elements. So we only have to count such diagrams. There are $n+k-1$ positions, and a diagram is fixed by choosing which $k$ positions hold the stars:

$$\binom{n+k-1}{k}$$

This is the **stars and bars** argument.

**Equivalent formulation (very common in exercises).** The number of non-negative integer solutions of

$$x_1 + x_2 + \dots + x_n = k$$

is $\dbinom{n+k-1}{k}$. Here $x_i$ is "how many times element $i$ was picked".

**Variants.**

- If every $x_i$ must be **at least 1** (positive solutions), first give one unit to each variable, leaving $k-n$ to distribute: $\dbinom{k-1}{n-1}$.
- If $x_i \ge m_i$ for each $i$, subtract all the minimums from $k$ first, then apply the basic formula.

**Why not $n^k / k!$?** With repeats, different unordered outcomes correspond to different numbers of ordered ones. The multiset $\{a,a,b\}$ comes from 3 orderings, whereas $\{a,b,c\}$ comes from 6.

**Example (box of balls with replacement).** There are:

- $n^k$ ordered ways to pick $k$ balls,
- $\dbinom{n+k-1}{k}$ unordered ways to pick $k$ balls.

[Back to top](#table-of-contents)

---

## 7. The big decision table

| | Order matters | Order does not matter |
|---|---|---|
| **No repetition** | $\dfrac{n!}{(n-k)!}$ | $\dbinom{n}{k}$ |
| **Repetition allowed** | $n^k$ | $\dbinom{n+k-1}{k}$ |

Additional formulas:

- Permutations of $n$ elements: $n!$ (the case $k = n$ of the top-left cell).
- Partition of $n$ elements into $k$ subsets of sizes $n_1, \dots, n_k$: $\dfrac{n!}{n_1! \cdots n_k!}$.

[Back to top](#table-of-contents)

---

## 8. The link with probability

The four counts above are counts of *outcomes*, but the formula $P(A) = |A|/|\Omega|$ needs the outcomes to be **equally likely**.

- **Ordered draws with replacement.** All $n^k$ sequences are equally likely. Good.
- **Unordered draws with replacement.** The $\binom{n+k-1}{k}$ multisets are **not** equally likely (the multiset $\{a,a,b\}$ is less likely than $\{a,b,c\}$ in a physical experiment). Dividing by $\binom{n+k-1}{k}$ gives wrong probabilities. In such problems, model $\Omega$ as ordered sequences ($n^k$ of them) and count the favourable sequences.
- **Unordered draws without replacement.** All $\binom{n}{k}$ subsets are equally likely, and it is equally valid to model with ordered draws. Just be **consistent between numerator and denominator**: count both with order or both without.

**Golden rule:** use the same model for $|A|$ and $|\Omega|$.

[Back to top](#table-of-contents)

---

## 9. Worked examples

**A. Birthday problem.** Probability that among $k$ people at least two share a birthday (365 equally likely days).

- $\Omega$ = all sequences of birthdays: $|\Omega| = 365^k$ (ordered, with repetition).
- "At least one match" is awkward, so use the complement. No match: $365 \cdot 364 \cdots (365-k+1)$ (ordered, no repetition).
- $P(\text{match}) = 1 - \dfrac{365 \cdot 364 \cdots (365-k+1)}{365^k}$. For $k = 23$ this already exceeds $1/2$.

**B. Lottery.** Pick 6 numbers out of 49.

- Order is irrelevant: $|\Omega| = \binom{49}{6} = 13\,983\,816$, so the probability of matching all 6 is $1/13\,983\,816$.
- Exactly 3 correct: choose which 3 of the 6 winning numbers you hold, and 3 losing numbers from the 43 others: $\dfrac{\binom{6}{3}\binom{43}{3}}{\binom{49}{6}}$.
  Pattern: **(choose from the good group) $\times$ (choose from the bad group)**, divided by the total. This is the hypergeometric structure and appears constantly.

**C. Poker hand: exactly one pair** (5 cards from 52, order irrelevant, $|\Omega| = \binom{52}{5}$). Use the multiplication rule in stages:

1. Rank of the pair: $13$.
2. Two suits for that rank: $\binom{4}{2}$.
3. Three other distinct ranks: $\binom{12}{3}$.
4. A suit for each of these three cards: $4^3$.

Count $= 13 \cdot \binom{4}{2} \cdot \binom{12}{3} \cdot 4^3 = 1\,098\,240$.

**D. Distributing identical objects.** 10 identical sweets to 4 children, any number each: non-negative solutions of $x_1 + \dots + x_4 = 10$, so $\binom{13}{3} = 286$. If each child must get at least one: $\binom{9}{3} = 84$.

**E. Two dice.** $|\Omega| = 36$ (ordered pairs, all equally likely). Do not use "unordered pairs" (21 of them): the outcome $\{3,4\}$ is twice as likely as $\{3,3\}$.

[Back to top](#table-of-contents)

---

## 10. Method checklist for any counting exercise

1. **Define $\Omega$** and check that the outcomes are equally likely.
2. **Identify the objects** and ask: are they distinguishable? Is there an order? Is there repetition?
3. **Build the outcome step by step** (multiplication rule). Picture the tree.
4. **Constraints:** place the most restricted objects first.
5. **Cases:** split into disjoint cases and add.
6. **"At least", "not all", "none":** try the complement.
7. **Overcounting check:** if a formula counts each real outcome $m$ times, divide by $m$. This is the origin of every $k!$ and $n_i!$ in the lecture.
8. **Sanity check:** try a tiny case (for example $n = 3$, $k = 2$) and list the outcomes by hand.

[Back to top](#table-of-contents)

---

## 11. Common mistakes

- Using $\binom{n}{k}$ when order matters, or $\frac{n!}{(n-k)!}$ when it does not.
- Applying stars and bars to a physical random experiment and treating the multisets as equally likely.
- Dividing by $k!$ when there are repetitions (Section 6.2).
- Forgetting to divide by $m!$ for $m$ interchangeable groups of the same size (Section 5).
- Mixing ordered counting in the numerator with unordered counting in the denominator.
- Treating "adjacent" objects as a single block and forgetting the internal order of the block.
- Forgetting that $0! = 1$ and $\binom{n}{0} = 1$.

[Back to top](#table-of-contents)

---

## 12. Practice problems

Each problem comes with the method to use, but no solution.

1. How many 5-letter words (any letters) can be formed from a 26-letter alphabet? How many with all letters distinct? *(Ordered, first with then without repetition.)*
2. In how many ways can 8 people sit in a row if two of them refuse to sit next to each other? *(Complement: total minus the glued arrangements.)*
3. A committee of 4 is chosen from 7 men and 5 women. What is the probability that it contains exactly 2 women? *(Good group times bad group, over $\binom{12}{4}$.)*
4. How many distinct arrangements of the letters of "STATISTICS" are there? *(Anagram formula.)*
5. How many non-negative integer solutions does $x_1 + x_2 + x_3 + x_4 = 12$ have? And if each $x_i \ge 2$? *(Stars and bars, subtract the minimums first.)*
6. What is the probability that a 5-card poker hand contains no aces? *(Same model in numerator and denominator.)*
7. Prove combinatorially that $\binom{n}{k} = \binom{n-1}{k-1} + \binom{n-1}{k}$ and that $\sum_{k} \binom{n}{k} = 2^n$. *(Focus on one element; classify subsets by size.)*

[Back to top](#table-of-contents)
