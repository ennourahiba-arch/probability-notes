# Probability: Introduction and Discrete Probability

> Lecture notes, expanded with explanations and worked examples.
> Formulas use GitHub-compatible LaTeX (`$...$` and `$$...$$`).

## Contents

1. [Motivating example: the Monty Hall problem](#1-motivating-example-the-monty-hall-problem)
2. [The sample space](#2-the-sample-space)
3. [Events and the family F](#3-events-and-the-family-f)
4. [Countable vs. uncountable sets](#4-countable-vs-uncountable-sets)
5. [Probability measure and probability space](#5-probability-measure-and-probability-space)
6. [Structure of F (Remark 1.8)](#6-structure-of-f-remark-18)
7. [Example: rolling a die, unions and "or"](#7-example-rolling-a-die-unions-and-or)
8. [Preview: an uncountable sample space](#8-preview-an-uncountable-sample-space)
9. [Equally likely outcomes](#9-equally-likely-outcomes)
10. [Worked examples: die and cards](#10-worked-examples-die-and-cards)

---

## 1. Motivating example: the Monty Hall problem

**Setup** (from a TV game show)

- There are 3 doors. Behind one is a Ferrari; the other two are empty (in the classic version, goats).
- You pick a door.
- The host, who **knows** where the car is, opens one of the *other* doors, always an empty one.
- He then asks: do you want to **stay** or **switch**?

**Answer:** switching wins with probability $\tfrac23$, staying wins with probability $\tfrac13$.

**Why (case analysis)**

| Your first pick | Probability | Host's action | If you switch |
|---|---|---|---|
| The car | $\tfrac13$ | opens one of the 2 empty doors | you **lose** |
| An empty door | $\tfrac23$ | forced to open the *other* empty door | you **win** |

- Your first pick is right with probability $\tfrac13$.
- If your first pick was right and you switch, you lose.
- If your first pick was wrong and you switch, you **win**.
- So switching wins exactly when your first pick was wrong, which happens with probability $\tfrac23$.

Opening a door does not change the $\tfrac13$, because the host never opens your door and never reveals the car. The remaining $\tfrac23$ is concentrated on the one other closed door.

**Intuition with 100 doors.** You pick one door (probability $\tfrac1{100}$). The host opens 98 empty doors, leaving yours and one other. Your door is still $\tfrac1{100}$, so the other door holds the car with probability $\tfrac{99}{100}$.

**Key point.** The host's action is **not random**: he knows where the car is and must avoid it. That is why his opening a door carries information. If he opened a door at random and it happened to be empty, switching would be $50/50$. New information changes probabilities, but how it changes depends on *how the information was produced*. This is the idea behind **conditional probability**.

---

## 2. The sample space

**Definition.** The **sample space** $\Omega$ is the set of all possible outcomes of a random experiment. Each element $\omega \in \Omega$ is an **outcome** (or sample point).

A good sample space is:

- **Exhaustive:** every possible result of the experiment is in $\Omega$.
- **Mutually exclusive:** exactly one outcome occurs each time the experiment is run.

**Discrete** means $\Omega$ is finite or countably infinite (its elements can be listed, even if the list never ends).

**Examples**

| Experiment | Sample space $\Omega$ | Size |
|---|---|---|
| Toss a coin | $\{H, T\}$ | 2 |
| Roll a die | $\{1,2,3,4,5,6\}$ | 6 |
| Toss a coin twice | $\{HH, HT, TH, TT\}$ | 4 |
| Toss a coin until the first head | $\{H, TH, TTH, TTTH, \dots\}$ | countably infinite |
| Monty Hall: door hiding the car | $\{\text{door }1, \text{door }2, \text{door }3\}$ | 3 |

**Remarks**

- The sample space depends on what you choose to record. For two coin tosses, recording only the *number of heads* gives $\Omega = \{0,1,2\}$, but then the outcomes are **not** equally likely (1 head is twice as likely as 0 heads). Recording the full sequence is usually safer.
- Order matters when recording sequences: $HT$ and $TH$ are different outcomes.

---

## 3. Events and the family F

An **event** is a subset $A \subseteq \Omega$, that is, a collection of outcomes. The event $A$ **occurs** if the outcome $\omega$ that actually happens lies in $A$.

$\mathcal{F}$ denotes the family of events. In the discrete case it is the set of **all subsets** of $\Omega$ (the *power set*):

$$\mathcal{F} = \{A : A \subseteq \Omega\} = 2^{\Omega}.$$

Note: $\mathcal{F}$ is the collection of events (the *domain* of the probability function). It is $P$, defined below, that assigns probabilities to events.

**Example 1: coin.** $\Omega = \{H,T\}$, so

$$\mathcal{F} = \{\emptyset,\ \{H\},\ \{T\},\ \{H,T\}\}, \qquad 2^2 = 4 \text{ events}.$$

**Example 2: die.** $\Omega = \{1,\dots,6\}$, so $\mathcal{F}$ has $2^6 = 64$ events. For instance:

- "even number" $= \{2,4,6\}$
- "at least 5" $= \{5,6\}$
- the impossible event $\emptyset$ and the certain event $\Omega$

In general, if $\Omega$ has $n$ elements, then $\mathcal{F}$ has $2^n$ elements.

**Dictionary: logic words and set operations**

| In words | Set operation |
|---|---|
| $A$ **or** $B$ | $A \cup B$ |
| $A$ **and** $B$ | $A \cap B$ |
| **not** $A$ | $A^c$ |

---

## 4. Countable vs. uncountable sets

A set is **countable** if its elements can be listed in a row, $x_1, x_2, x_3, \dots$, so that every element appears at some position. Equivalently, it is finite or in bijection with $\mathbb{N}$.

| Type | Meaning | Examples |
|---|---|---|
| **Finite** | Has $n$ elements for some $n \in \mathbb{N}$ | $\{H,T\}$, $\{1,\dots,6\}$ |
| **Countably infinite** | Infinite, but can be listed as $x_1, x_2, x_3, \dots$ | $\mathbb{N}$, $\mathbb{Z}$, $\mathbb{Q}$ |
| **Uncountable** | Infinite, and **no** such list exists | $\mathbb{R}$, $[-1,1]$, $(0,1)$ |

**Infinite vs. uncountable.** *Infinite* only means "not finite". *Uncountable* is stronger: the set is infinite **and** too big to be listed. Every uncountable set is infinite, but not every infinite set is uncountable.

**Infinite sets can still be countable.** For $\mathbb{Z}$, use the ordering

$$0,\ 1,\ -1,\ 2,\ -2,\ 3,\ -3,\ \dots$$

Every integer appears exactly once, so $\mathbb{Z}$ is countable.

**Why $\mathbb{R}$ is not countable (Cantor's diagonal argument).**
Suppose $(0,1)$ could be listed as $x_1, x_2, x_3, \dots$ with decimal expansions

$$x_1 = 0.a_{11}a_{12}a_{13}\dots,\quad x_2 = 0.a_{21}a_{22}a_{23}\dots,\quad \dots$$

Build a new number $y = 0.b_1 b_2 b_3 \dots$ with

$$b_n = \begin{cases} 5 & \text{if } a_{nn} \neq 5, \\ 4 & \text{if } a_{nn} = 5. \end{cases}$$

Then $y$ differs from $x_n$ in the $n$-th digit for every $n$, so $y$ is not on the list, yet $y \in (0,1)$. Contradiction: no such list exists. (Using only the digits 4 and 5 avoids the ambiguity $0.4999\dots = 0.5$.) Since $(0,1) \subset \mathbb{R}$, $\mathbb{R}$ is uncountable too.

**Why this matters for probability.**

- **Countable $\Omega$:** we can define $P$ by giving a probability to each single outcome (the *discrete* case).
- **Uncountable $\Omega$:** each single point typically has probability $0$, and $\mathcal{F}$ can no longer be the power set. This is treated later in the course.

---

## 5. Probability measure and probability space

**Definition 1.7.** Let $\Omega$ be a countable set (not necessarily finite) and $\mathcal{F}$ the family of all subsets of $\Omega$. A function

$$P : \mathcal{F} \to [0,1]$$

is called a **probability measure** if:

1. **Normalization:** $P(\Omega) = 1$.
2. **Countable additivity:** for any sequence of **pairwise disjoint** events $A_1, A_2, \dots$ (that is, $A_i \cap A_j = \emptyset$ for $i \ne j$),

$$P\left(\bigcup_{n=1}^{\infty} A_n\right) = \sum_{n=1}^{\infty} P(A_n).$$

The triple $(\Omega, \mathcal{F}, P)$ is called a **probability space**.

**Consequences of the axioms**

- $P(\emptyset) = 0$.
- **Finite additivity:** for disjoint $A, B$: $P(A \cup B) = P(A) + P(B)$.
- **Complement:** $P(A^c) = 1 - P(A)$.
- **Discrete case:** for any event $A$,

$$P(A) = \sum_{\omega \in A} P(\{\omega\}).$$

---

## 6. Structure of F (Remark 1.8)

Because $\mathcal{F}$ is the family of *all* subsets of $\Omega$, it satisfies:

1. $\Omega \in \mathcal{F}$.
2. **Closed under complement:** if $A \in \mathcal{F}$, then $A^c = \Omega \setminus A \in \mathcal{F}$.
3. **Closed under countable unions:** if $A_1, A_2, \dots \in \mathcal{F}$, then $\bigcup_{n=1}^\infty A_n \in \mathcal{F}$.

**Why they hold.** $\Omega$ is a subset of itself; the complement of a subset of $\Omega$ is a subset of $\Omega$; a union of subsets of $\Omega$ is a subset of $\Omega$.

**In words.** Whatever operations we perform on events ("not $A$", "$A$ or $B$ or $C$ or ..."), we stay inside $\mathcal{F}$, so we can always ask for the probability of the result.

**Further consequences.** A family satisfying (1) to (3) is also closed under:

- $\emptyset \in \mathcal{F}$, since $\emptyset = \Omega^c$.
- **Finite unions**, by taking $A_n = \emptyset$ for large $n$.
- **Countable intersections**, by De Morgan: $\bigcap_n A_n = \left(\bigcup_n A_n^c\right)^c$.
- **Differences:** $A \setminus B = A \cap B^c$.

**Example (coin).** $\mathcal{F} = \{\emptyset, \{H\}, \{T\}, \{H,T\}\}$:

- $\{H,T\} = \Omega \in \mathcal{F}$
- $\{H\}^c = \{T\} \in \mathcal{F}$
- $\{H\} \cup \{T\} = \{H,T\} \in \mathcal{F}$

**Why this is marked (\*).** Properties (1) to (3) are exactly the definition of a **σ-algebra**. For countable $\Omega$ the power set works automatically. For uncountable $\Omega$ (like $\mathbb{R}$) the power set is too large for a probability measure to be defined on all of it, so one chooses a smaller family satisfying (1) to (3) and requires those properties by definition. This is why a probability space is written as the triple $(\Omega, \mathcal{F}, P)$.

---

## 7. Example: rolling a die, unions and "or"

$$\Omega = \{1,2,3,4,5,6\}, \qquad \mathcal{F} = \text{all subsets of } \Omega.$$

Take a **fair die**: $P(\{\omega\}) = \tfrac16$ for each outcome.

**Events** (note: $A_1$ and $A_2$ are events, i.e. subsets of $\Omega$; the probabilities are $P(A_1)$ and $P(A_2)$)

- $A_1$ = "the result is odd" $= \{1,3,5\}$
- $A_2$ = "the result is 4" $= \{4\}$

**Probabilities of each event**

$$P(A_1) = \tfrac16 + \tfrac16 + \tfrac16 = \tfrac12, \qquad P(A_2) = \tfrac16.$$

**Union = "or".** $A_1 \cup A_2$ means "$A_1$ occurs **or** $A_2$ occurs (or both)":

$$A_1 \cup A_2 = \{1,3,4,5\}.$$

The events are disjoint ($A_1 \cap A_2 = \emptyset$, since 4 is not odd), so additivity applies:

$$P(A_1 \cup A_2) = P(A_1) + P(A_2) = \tfrac12 + \tfrac16 = \tfrac23.$$

Check by counting: $\{1,3,4,5\}$ has 4 outcomes, so $\tfrac46 = \tfrac23$.

**What if the events are not disjoint?** Let $B$ = "the result is at least 4" $= \{4,5,6\}$. Then $A_1 \cap B = \{5\}$, and

$$P(A_1 \cup B) = P(A_1) + P(B) - P(A_1 \cap B) = \tfrac12 + \tfrac12 - \tfrac16 = \tfrac56.$$

Check: $A_1 \cup B = \{1,3,4,5,6\}$ has 5 outcomes, so $\tfrac56$.

**Why the formula works.** $A \cup B$ splits into three disjoint pieces: $A \setminus B$, $A \cap B$, $B \setminus A$. Adding $P(A) + P(B)$ counts $A \cap B$ twice, so we subtract it once.

---

## 8. Preview: an uncountable sample space

*(A short preview only. This is treated properly later in the semester.)*

Let $\Omega = [-1,1]$ (uncountable) and pick a number uniformly at random.

- $P(\{0.7\}) = 0$: any single point has probability $0$.
- $P(x < 0.7) = \dfrac{\text{length of } [-1, 0.7)}{\text{length of } [-1,1]} = \dfrac{1.7}{2} = 0.85$.

The natural probability here is *length divided by total length*.

---

## 9. Equally likely outcomes

The simplest case is a **finite** sample space ($|\Omega| < \infty$, where $|\Omega|$ is the number of elements) with equally likely outcomes:

$$P(\{\omega\}) = \frac{1}{|\Omega|} \qquad \forall\, \omega \in \Omega.$$

This is called the **uniform probability measure** on $\Omega$.

**Why $P(A) = |A|/|\Omega|$ follows.** Any event $A$ is a finite union of disjoint single-outcome events, $A = \bigcup_{\omega \in A} \{\omega\}$. By additivity,

$$P(A) = \sum_{\omega \in A} P(\{\omega\}) = |A| \cdot \frac{1}{|\Omega|} = \frac{|A|}{|\Omega|} \qquad \forall\, A \in \mathcal{F}.$$

**In words:** the probability of an event is the number of favorable outcomes divided by the total number of possible outcomes.

**Properties** (each follows by counting elements)

| Property | Why |
|---|---|
| $P(\emptyset) = 0$ | $\lvert\emptyset\rvert = 0$ |
| $A \subseteq B \Rightarrow P(A) \le P(B)$ | $A \subseteq B$ implies $\lvert A\rvert \le \lvert B\rvert$ |
| $A \cap B = \emptyset \Rightarrow P(A \cup B) = P(A) + P(B)$ | For disjoint sets, $\lvert A \cup B\rvert = \lvert A\rvert + \lvert B\rvert$ |
| $P(A \cup B) = P(A) + P(B) - P(A \cap B)$ | $\lvert A \cup B\rvert = \lvert A\rvert + \lvert B\rvert - \lvert A \cap B\rvert$ (the overlap is counted twice) |
| $P(A \cup B) \le P(A) + P(B)$ | From the previous line, since $P(A \cap B) \ge 0$ |

These properties hold for **every** probability measure; the uniform case just makes them easy to see by counting.

**Checking that $P$ is a probability measure.** $P(\Omega) = \frac{|\Omega|}{|\Omega|} = 1$, and for disjoint events $A_1, \dots, A_n$,

$$P\left(\bigcup_{k=1}^{n} A_k\right) = \frac{\left|A_1 \cup \dots \cup A_n\right|}{|\Omega|} = \sum_{k=1}^{n} \frac{|A_k|}{|\Omega|} = \sum_{k=1}^{n} P(A_k).$$

Also $0 \le |A| \le |\Omega|$ gives $P(A) \in [0,1]$.

**Warning: "equally likely" is an assumption.** The formula is only valid when all outcomes really are equally likely.

*Counterexample.* Toss two fair coins and record only the number of heads: $\Omega = \{0,1,2\}$. The formula would give $P(\text{exactly 1 head}) = \tfrac13$, but the true value is $\tfrac24 = \tfrac12$, since it corresponds to 2 of the 4 equally likely sequences $\{HT, TH\}$. The outcomes $0,1,2$ are not equally likely, so the uniform measure does not apply on that $\Omega$. The fix is to choose a sample space whose outcomes are equally likely (the full sequences).

**Why this case matters.** With equally likely outcomes, computing $P(A)$ reduces to **counting** $|A|$ and $|\Omega|$. This is why combinatorics (permutations, combinations) comes next.

---

## 10. Worked examples: die and cards

### Example 1.9: fair die

$\Omega = \{1,\dots,6\}$, $P(\{i\}) = \tfrac16$ for $i = 1,\dots,6$.

- $P(\text{even}) = P(\{2,4,6\}) = \tfrac36 = \tfrac12$
- $P(\text{outcome} \le 5) = P(\{1,\dots,5\}) = \tfrac56$. Shortcut: $1 - P(\{6\}) = 1 - \tfrac16$.

### Example 1.10: one card from a deck of 52

A deck has 4 suits (hearts, diamonds, clubs, spades) with 13 ranks each, so $|\Omega| = 52$.

- $A$ = {pick the queen of hearts}: $|A| = 1$, so $P(A) = \tfrac{1}{52}$.
- $B$ = {pick a Diamond **or** a Jack}. There are 13 diamonds and 4 jacks, but the jack of diamonds is in both. By inclusion-exclusion, $|B| = 13 + 4 - 1 = 16$, so $P(B) = \tfrac{16}{52}$. (Simply adding $13 + 4 = 17$ would overcount.)
- $C$ = {don't pick an ace}: $C$ is the complement of "pick an ace", so $|C| = 52 - 4 = 48$ and $P(C) = \tfrac{48}{52}$.

### Example 1.11: two cards from a deck of 52

$\Omega$ is the set of all **ordered pairs** of distinct cards (drawing without replacement). The first card has 52 choices and the second has 51, so by the multiplication principle

$$|\Omega| = 52 \cdot 51 = 2652.$$

"Ordered" means (K of spades, 2 of diamonds) and (2 of diamonds, K of spades) are different outcomes.

**$A$ = {pick an ace, then a 2}.** There are 4 aces for the first card and 4 twos for the second: $|A| = 4 \cdot 4 = 16$.

$$P(A) = \frac{16}{2652} = \frac{4}{663} \approx 0.0060$$

**$B$ = {pick two diamonds}.** There are 13 choices for the first diamond and 12 remaining for the second: $|B| = 13 \cdot 12 = 156$.

$$P(B) = \frac{156}{2652} = \frac{1}{17} \approx 0.0588$$

**$C$ = {the first card is a jack}.** There are 4 jacks for the first card, and the second card is any of the other 51: $|C| = 4 \cdot 51 = 204$.

$$P(C) = \frac{204}{2652} = \frac{1}{13} \approx 0.0769$$

**Sanity checks**

- For $C$: the second card is unrestricted, so $P(C) = \frac{4}{52} = \frac{1}{13}$, the same as getting a jack when picking one card.
- For $B$: $\frac{13}{52} \cdot \frac{12}{51} = \frac14 \cdot \frac{4}{17} = \frac{1}{17}$. This "first card, then second card given the first" idea is a preview of conditional probability.
