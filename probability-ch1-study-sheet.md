# Discrete Probability: Study Sheet (Chapter 1, sections 1-12)

> Goal: be able to solve the exercises alone. Easy things are kept short; the parts that trip people up are in **bold** or marked ⚠️.

---

## 📌 What you must know (checklist)

- [ ] Sample space, outcome, event; probability measure; equally likely outcomes
- [ ] Counting toolbox (4 cases, permutations, groups, stars and bars)
- [ ] Basic properties, De Morgan, inclusion-exclusion (2 and 3 events), union bound
- [ ] Independence (2 events, $n$ events, pairwise ≠ independent)
- [ ] Conditional probability and the product formula
- [ ] Law of total probability (cases / tree)
- [ ] Bayes' theorem
- [ ] Which tool to use from the wording of the exercise (Section 8)

---

## 1. Basics

| Word | Meaning | Example (die) |
|---|---|---|
| Sample space $\Omega$ | set of all outcomes | $\{1,\dots,6\}$ |
| Outcome $\omega$ | one element of $\Omega$ | $5$ |
| Event $A$ | subset of $\Omega$ | $A=\{2,4,6\}$ (even) |
| $\mathcal F$ | all subsets of $\Omega$ (for countable $\Omega$) | $\lvert\mathcal F\rvert=2^{\lvert\Omega\rvert}$ |

**Probability measure** $P:\mathcal F\to[0,1]$ with
1. $P(\Omega)=1$
2. disjoint events $A_1,A_2,\dots$: $P\left(\bigcup A_n\right)=\sum P(A_n)$

**Equally likely outcomes** (finite $\Omega$):
$$P(A)=\frac{|A|}{|\Omega|}$$

**How to start any exercise:** write down $\Omega$ (is it ordered pairs? sequences? subsets?), compute $|\Omega|$, then count $|A|$ **with the same model**.

Typical sample spaces:

| Experiment | $\Omega$ | $\lvert\Omega\rvert$ |
|---|---|---|
| Two dice | ordered pairs $\{1..6\}^2$ | 36 |
| Two cards (one after the other) | ordered pairs of distinct cards | $52\cdot51$ |
| Arrange $n$ books | orderings (permutations) | $n!$ |
| Pick 3 cards of 5, arranged left to right | ordered, no repetition | $5\cdot4\cdot3$ |
| Pick 3 cards of 5, kept in hand | subsets | $\binom{5}{3}$ |
| $k$ draws with replacement from $n$ | sequences | $n^k$ |

Countable $\Omega$ can be infinite (e.g. $\mathbb N$); uncountable (e.g. $[0,1]$) is not treated in this part.

---

## 2. Counting (recap of the combinatorics lecture)

**Before any formula ask: are objects distinguishable? does order matter? is repetition allowed?**

|  | Order matters | Order does NOT matter |
|---|---|---|
| **No repetition** | $\dfrac{n!}{(n-k)!}$ | $\dbinom{n}{k}$ |
| **Repetition** | $n^k$ | $\dbinom{n+k-1}{k}$ (stars and bars) |

Other tools:

| Tool | Formula | When |
|---|---|---|
| Multiplication rule | $n_1 n_2\cdots n_N$ | step-by-step choices |
| Addition rule | add counts | disjoint cases |
| Permutations | $n!$ | order all $n$ objects |
| Anagrams (identical objects) | $\dfrac{n!}{n_1!\cdots n_k!}$ | repeated letters |
| Groups of sizes $n_1..n_k$ | $\dfrac{n!}{n_1!\cdots n_k!}$ | split people/cards into groups |
| Unlabelled groups of equal size | divide by (number of equal groups)! | e.g. 3 pairs: $\div3!$ |
| Subsets of an $n$-set | $2^n$ | |
| Glued objects | block count! × inside! | "must be together" |

**Stars and bars:** non-negative solutions of $x_1+\dots+x_n=k$: $\binom{n+k-1}{k}$.
Each $x_i\ge1$: $\binom{k-1}{n-1}$. Each $x_i\ge m_i$: subtract the minimums from $k$ first.

### Counting functions $f:\{1..k\}\to\{1..n\}$ (appears in exercises)

| Type of function | Count | Why |
|---|---|---|
| any | $n^k$ | $n$ choices for each of the $k$ inputs |
| injective (all values distinct) | $\dfrac{n!}{(n-k)!}$ | ordered, no repetition |
| strictly increasing | $\dbinom{n}{k}$ | choose the $k$ values, order is forced |
| non-decreasing | $\dbinom{n+k-1}{k}$ | choose values with repetition, order is forced |
| constant | $n$ | |

Also: functions $\{1..k\}\to\{0,1\}$: $2^k$. Handing out distinct toys to children = functions (toy → child), or injective if each child gets at most one.

### Balls and boxes
- $n$ **distinct** balls into $n$ **distinct** boxes: each ball picks a box → $n^n$ outcomes.
- "No box empty" with $n$ balls and $n$ boxes: every box gets exactly one ball → permutations.
- "All in the same box": choose the box.

### Probability patterns from counting
- **Good group × bad group** (lottery, committee with 2 women...): $\dfrac{\binom{g}{a}\binom{b}{c}}{\binom{N}{a+c}}$
- **"At least one" / "all different"**: use the complement (birthday problem: $1-\frac{n\text{ distinct}}{365^k}$).
- Matching a lottery ticket **with** order: $1/\frac{n!}{(n-k)!}$; **without** order: $1/\binom nk$.

⚠️ **Same model top and bottom.** Never put ordered counting in the numerator and unordered in the denominator.
⚠️ **Unordered draws with replacement** (multisets) are NOT equally likely: use ordered sequences ($n^k$) for probabilities. Two dice: use the 36 ordered pairs, not the 21 unordered.

---

## 3. Properties of probability

For any events:

| Property | Formula |
|---|---|
| Range | $0\le P(A)\le1$, $P(\emptyset)=0$ |
| Complement | $P(A^c)=1-P(A)$ |
| Disjoint | $A\cap B=\emptyset\Rightarrow P(A\cup B)=P(A)+P(B)$ |
| Monotone | $A\subseteq B\Rightarrow P(A)\le P(B)$ and $P(B\setminus A)=P(B)-P(A)$ |
| Union (2 events) | $P(A\cup B)=P(A)+P(B)-P(A\cap B)$ |
| Union bound (Boole) | $P(\bigcup A_k)\le\sum P(A_k)$ |

### Inclusion-exclusion (you must know $n=2,3$)

$$P(A\cup B\cup C)=P(A)+P(B)+P(C)-P(A\cap B)-P(A\cap C)-P(B\cap C)+P(A\cap B\cap C)$$

Pattern: **add singles, subtract pairs, add triple.** Use it when you see "or" with overlapping events (e.g. divisible by 3 or 5, card is a heart or ≤ 5).

Counting version (same idea): numbers in $\{1..500\}$ divisible by 3 or 5 = $\lfloor500/3\rfloor+\lfloor500/5\rfloor-\lfloor500/15\rfloor$.

### Set language (to express events in symbols)

| In words | Symbols |
|---|---|
| $A$ or $B$ (at least one) | $A\cup B$ |
| $A$ and $B$ | $A\cap B$ |
| not $A$ | $A^c$ |
| $A$ but not $B$ | $A\cap B^c=A\setminus B$ |
| only $A$ occurs (of $A,B,C$) | $A\cap B^c\cap C^c$ |
| none occurs | $A^c\cap B^c\cap C^c$ |
| exactly one occurs | $(A\cap B^c\cap C^c)\cup(A^c\cap B\cap C^c)\cup(A^c\cap B^c\cap C)$ |
| at least one occurs | $A\cup B\cup C$ |

**De Morgan:** $(A\cup B)^c=A^c\cap B^c$ and $(A\cap B)^c=A^c\cup B^c$.

Useful: $P(A^c\cap(B\cup C))=P(B\cup C)-P(A\cap(B\cup C))$, or draw a Venn diagram and sum the regions.

### Continuity (short)
- Increasing events $A_1\subseteq A_2\subseteq\cdots$: $P\left(\bigcup A_n\right)=\lim P(A_n)$
- Decreasing events $B_1\supseteq B_2\supseteq\cdots$: $P\left(\bigcap B_n\right)=\lim P(B_n)$
- Example: $A_n=\{1..n\}$ in $\mathbb N$ grows to $\Omega$, so the limit is $1$; $B_n=\{n,n+1,\dots\}$ shrinks to $\emptyset$, so the limit is $0$.
- Consequence: if $P(A_n)\to p$ for increasing $A_n$, then $P(\bigcup A_n)=p$ and $P(\bigcap A_n^c)=1-p$.

### limsup / liminf (optional, but the exercises use them)
- $\limsup A_n$ = "$A_n$ happens **infinitely often**" $=\bigcap_n\bigcup_{m\ge n}A_m$
- $\liminf A_n$ = "$A_n$ happens **eventually** (from some point on)" $=\bigcup_n\bigcap_{m\ge n}A_m$
- $(\limsup A_n)^c=\liminf A_n^c$
- If $A_n$ is monotone, both equal the union (increasing) or the intersection (decreasing).

---

## 4. Independence

**Definition:** $A,B$ independent $\iff P(A\cap B)=P(A)P(B)$.

**How to check:** compute $P(A)$, $P(B)$, $P(A\cap B)$ and compare. That's all.

Facts:
- $A,B$ independent ⇒ so are $(A,B^c)$, $(A^c,B)$, $(A^c,B^c)$. (Proof idea: $P(A\cap B^c)=P(A)-P(A\cap B)=P(A)(1-P(B))$.)
- Independent ⇒ $P(A|B)=P(A)$: knowing $B$ tells nothing about $A$.
- ⚠️ Independent ≠ disjoint. Disjoint events with positive probability are **never** independent.

**$n$ events** $A_1..A_n$ are independent if the product rule holds for **every** sub-collection (all pairs, all triples, ..., all $n$).

⚠️ **Pairwise independent does NOT imply independent.** Classic example: two coins, $A$ = first is T, $B$ = second is T, $C$ = exactly one T. All pairs are independent, but $P(A\cap B\cap C)=0\neq\frac18$.

Checking 3 events $A,B,C$: verify 3 pairs **and** the triple $P(A\cap B\cap C)=P(A)P(B)P(C)$.

Typical dice checks: "first die = 4" and "sum = 7" are independent; "first die = 4" and "sum = 6" are not (sum 6 depends on the first die).

---

## 5. Conditional probability

$$P(A|B)=\frac{P(A\cap B)}{P(B)}\qquad(P(B)>0)$$

Meaning: probability of $A$ **when we know $B$ happened**. Equally likely case: $P(A|B)=\dfrac{|A\cap B|}{|B|}$ (just restrict the sample space to $B$).

**Product formula** (rearranged):
$$P(A\cap B)=P(A|B)P(B)=P(B|A)P(A)$$

Chain version for sequential experiments:
$$P(A\cap B\cap C)=P(A)\,P(B|A)\,P(C|A\cap B)$$

Properties:
- $P(B|B)=1$
- $A\subseteq B\Rightarrow P(A|B)=\dfrac{P(A)}{P(B)}$; if $A\subsetneq B$ then $P(A|B)<1$
- If $A\cap B=\emptyset$ then $P(A|B)=0$
- $A,B$ independent ⇔ $P(A|B)=P(A)$
- ⚠️ In general $P(A|B)\neq P(B|A)$ (but $P(A|B)P(B)=P(B|A)P(A)$ always)
- "$B$ attracts $A$" ($P(A|B)>P(A)$) ⇒ "$A$ attracts $B$" (symmetric, by the product formula)

---

## 6. Law of total probability (the "cases" tool)

**Partition:** events $B_1,B_2,\dots$ that are **disjoint** and whose **union is $\Omega$**. Then for any $A$:

$$P(A)=\sum_n P(A|B_n)P(B_n)$$

Simplest version: $P(A)=P(A|B)P(B)+P(A|B^c)P(B^c)$.

**Recognize it:** the experiment has a **first stage** (coin, die, which urn, which type, did the student misread...) that changes what happens in the **second stage**. Ask "what are the possible first-stage cases?", those are the $B_n$.

**Method (tree):**
1. List first-stage cases $B_n$ and their probabilities $P(B_n)$ (they must sum to 1).
2. For each case, compute $P(A|B_n)$ (usually an easy counting problem).
3. Multiply along each branch, then add the branches.

Patterns:
- **Coin decides how many dice** → cases H / T, then "max ≤ 4" with 1 die $\frac46$ or 2 dice $\frac{4\cdot4}{6\cdot6}$.
- **Die value $k$ decides a coin's bias** → cases $B_k$, $P(\text{head}|B_k)=k/6$, sum over $k$.
- **Urn, second ball** → cases "first ball black / not black". (Shortcut: the second draw has the same distribution as the first.)

---

## 7. Bayes' theorem (the "reverse" tool)

$$P(A|B)=\frac{P(B|A)\,P(A)}{P(B)}$$

with the denominator computed by total probability:

$$P(B_i|A)=\frac{P(A|B_i)\,P(B_i)}{\sum_n P(A|B_n)P(B_n)}$$

**Recognize it:** you know "cause → effect" probabilities, and the question is "**given the effect, what was the cause?**"
(given the coin gave head, which coin was it? given max ≤ 2, was the coin head? given the student got a B, did he read the question?)

**Method:**
1. Name the cases (causes) $B_i$ and the observed fact $A$.
2. Compute numerator $P(A|B_i)P(B_i)$ for the cause asked.
3. Compute the denominator $P(A)$ with total probability (the same tree as Section 6).
4. Divide.

⚠️ Don't confuse $P(A|B)$ with $P(B|A)$: write clearly which one is given.

---

## 8. Which tool? (wording → method)

| Wording in the exercise | Tool |
|---|---|
| "uniformly / at random / fair", all outcomes equal | $\lvert A\rvert/\lvert\Omega\rvert$ + counting |
| "at least one", "not all", "none" | complement |
| "A or B" with overlap | inclusion-exclusion |
| "is it independent?" | check $P(A\cap B)=P(A)P(B)$ (all subsets for 3 events) |
| "given that...", "knowing that..." | conditional probability |
| "first ... then ..." (stages) | product formula / tree |
| "probability of $A$" where the experiment has stages with different cases | total probability |
| "given the result, what was the cause?" | Bayes |
| repeated independent trials, each with success prob. $p$ | multiply probabilities (see below) |

### Repeated independent trials (games, rounds, weekly experiments)
- Probability $q$ that the game ends in one round. It lasts **exactly $n$ rounds**: $(1-q)^{n-1}q$ (fail $n-1$ times, then end).
- **No success in the first $n$ trials**: $(1-p)^n$. **At least one**: $1-(1-p)^n$.
- **Exactly $k$ successes in $n$ trials**: $\dbinom nk p^k(1-p)^{n-k}$ (choose which trials succeed).
- **First success exactly at trial $n$**: $(1-p)^{n-1}p$.
- Seeing $n$ heads in a row with a fair coin: $(1/2)^n$.
- Dice game with simultaneous players: count the outcomes of the round (e.g. nobody gets a 6: $\frac56\cdot\frac56$; ties allowed means both can get a 6).

---

## 9. Common mistakes

| ❌ Mistake | ✅ Fix |
|---|---|
| Ordered numerator, unordered denominator | Same model for both |
| Using the 21 unordered dice pairs | Use the 36 ordered pairs |
| Forgetting to subtract the intersections in $P(A\cup B)$ | Inclusion-exclusion |
| Calling events independent because they "look unrelated" | Check the product formula |
| Checking only pairs for 3 events | Check the triple too |
| Confusing disjoint with independent | Disjoint with positive probability ⇒ NOT independent |
| $P(A|B)$ used as $P(B|A)$ | Write "given" explicitly |
| Bayes without computing the denominator by total probability | Denominator = sum over all cases |
| Case probabilities $P(B_n)$ that don't sum to 1 | Partition must cover $\Omega$ and be disjoint |
| Forgetting $0!=1$, $\binom n0=1$ | |

---

## 10. Mini-checklist for ANY exercise

1. Write $\Omega$ and the events in symbols.
2. Uniform case? → count $|A|/|\Omega|$ with one consistent model.
3. Look for keywords: *at least* → complement; *or* → inclusion-exclusion; *given* → conditional; *stages* → tree; *reverse* → Bayes.
4. Compute, then **sanity-check** (probability between 0 and 1, tree branches sum to 1, try a tiny case).
