# Probability Distributions Study Sheet

Oct 21, 2026 · @ennoura hiba

Five distributions cover most exam questions, and you pick one by asking what the question counts or measures.

## Which one do I use?

First ask: am I counting whole things (discrete) or measuring something that can be 2.37 (continuous)? Then match the key phrase.

| The question says... | Use | Possible values |
| --- | --- | --- |
| One yes/no event | Bernoulli(p) | 0 or 1 |
| Number of successes in n trials | Binomial(n, p) | 0, 1, ..., n |
| How many trials until the first success | Geometric(p) | 1, 2, 3, ... |
| Chosen at random, all equally likely | Uniform | any value in the range |
| Waiting time, lifetime, time between arrivals | Exponential(rate) | any x ≥ 0 |

## 1. Bernoulli: one trial

One trial with two outcomes: success (1) with probability p, failure (0) with probability 1 - p. It is the building block of the next three distributions.

```latex
P(X=1)=p,\qquad P(X=0)=1-p
```

```latex
\mathbb{E}[X]=p,\qquad \mathrm{Var}(X)=p(1-p)
```

**Spot it:** a single coin flip, one part defective or not, one student pass or fail.

**Example.** A part is defective with probability 0.1, and X = 1 if it is defective.

- P(X=1) = 0.1 and P(X=0) = 0.9
- Mean = 0.1
- Variance = 0.1 × 0.9 = 0.09

## 2. Binomial: successes in n trials

Repeat n independent Bernoulli(p) trials and count the successes. The binomial coefficient counts the ways to place k successes among n trials.

```latex
P(X=k)=\binom{n}{k}\,p^{k}(1-p)^{n-k},\qquad k=0,1,\dots,n
```

```latex
\mathbb{E}[X]=np,\qquad \mathrm{Var}(X)=np(1-p)
```

**Spot it:** "exactly k successes in n trials", with a fixed n and the same p every time.

**Example.** A student guesses on 5 multiple-choice questions with 4 options each, so p = 0.25. What is the chance of exactly 2 correct?

1. Identify: n = 5, p = 0.25, k = 2
2. Plug in: C(5,2) × 0.25² × 0.75³
3. Compute: 10 × 0.0625 × 0.421875 ≈ **0.264**
4. Mean = 5 × 0.25 = 1.25 correct answers on average

## 3. Geometric: trial of the first success

Keep running independent Bernoulli(p) trials and record which trial gives the first success. That means n - 1 failures, then one success.

```latex
P(X=n)=(1-p)^{\,n-1}\,p,\qquad n=1,2,3,\dots
```

```latex
\mathbb{E}[X]=\frac{1}{p},\qquad \mathrm{Var}(X)=\frac{1-p}{p^{2}}
```

**Tail shortcut:** the chance of needing more than n trials is the chance of n failures in a row.

```latex
P(X>n)=(1-p)^{n}
```

**Memoryless:** past failures do not change the future. After 10 failures you are no closer to success.

```latex
P(X>s+t\mid X>s)=P(X>t)
```

**Spot it:** "first success", "how many tries until".

**Example.** Roll a fair die until you get a 6, so p = 1/6.

1. First 6 on exactly roll 3: (5/6)² × 1/6 = 25/216 ≈ **0.116**
2. More than 3 rolls needed: (5/6)³ ≈ **0.579**
3. Expected number of rolls: 1/p = **6**

## 4. Uniform: all values equally likely

No value is favored. It comes in a discrete version (a finite set) and a continuous version (an interval).

**Discrete, on a finite set S**

```latex
P(X=x)=\frac{1}{|S|},\qquad x\in S
```

**Continuous, on \[a, b\]**

```latex
f(x)=\frac{1}{b-a}\ \ (a\le x\le b),\qquad \mathbb{E}[X]=\frac{a+b}{2},\qquad \mathrm{Var}(X)=\frac{(b-a)^{2}}{12}
```

For a continuous uniform, the probability of an interval is its length divided by the total length. The probability of any single exact value is 0.

```latex
P(c\le X\le d)=\frac{d-c}{b-a}
```

**Spot it:** "chosen at random", "equally likely", "arrives at a random time within...".

**Example (discrete).** Roll a fair die. S = {1,...,6}, so P(X=4) = 1/6.

**Example (continuous).** A bus arrives at a random time within the next 20 minutes, so X \~ Uniform\[0, 20\].

1. Wait at most 5 minutes: (5 - 0) / 20 = **0.25**
2. Average wait: (0 + 20) / 2 = **10 minutes**
3. Variance: 20² / 12 ≈ **33.3**

## 5. Exponential: waiting time

The continuous waiting time until the first event, when events happen at a constant average rate λ > 0 (events per unit of time).

```latex
f(x)=\lambda e^{-\lambda x},\qquad x\ge 0
```

```latex
P(X\le x)=1-e^{-\lambda x},\qquad P(X>x)=e^{-\lambda x}
```

```latex
\mathbb{E}[X]=\frac{1}{\lambda},\qquad \mathrm{Var}(X)=\frac{1}{\lambda^{2}}
```

**Memoryless:** if you have already waited s, the remaining wait has the same distribution as a fresh one.

```latex
P(X>s+t\mid X>s)=P(X>t)
```

**Spot it:** "waiting time", "lifetime", "time between arrivals".

**Example.** A customer arrives every 4 minutes on average, so the rate is λ = 1/4 = 0.25 per minute.

1. Wait more than 6 minutes: e^(-0.25 × 6) = e^(-1.5) ≈ **0.223**
2. Wait at most 2 minutes: 1 - e^(-0.5) ≈ **0.393**
3. Average wait: 1/λ = **4 minutes**, variance 1/λ² = **16**
4. Already waited 3 minutes, chance of waiting 6 more: still **0.223**, by memorylessness

## How they connect

The distributions are variations of one idea, repeated Bernoulli trials, so learn the links.

- **Bernoulli is Binomial with n = 1.** One trial, counting successes.
- **Binomial is a sum of Bernoullis.** Add n independent Bernoulli(p) variables and you get Bin(n, p). That is why the mean is n × p and the variance is n × p(1 - p).
- **Geometric is the other way to read the same trials.** Binomial fixes the number of trials and counts successes. Geometric fixes the success and counts trials.
- **Exponential is the continuous cousin of Geometric.** Both measure waiting for the first event, and they are the only two memoryless distributions.
- **Uniform stands alone.** It describes a lack of preference, not a repeated process.

## Cheat sheet

| Distribution | Type | Models | Probability / density | Mean | Variance |
| --- | --- | --- | --- | --- | --- |
| Bernoulli(p) | Discrete | One yes/no trial | P(X=1) = p | p | p(1-p) |
| Binomial(n, p) | Discrete | Successes in n trials | C(n,k) p^k (1-p)^(n-k) | np | np(1-p) |
| Geometric(p) | Discrete | Trial of the first success | (1-p)^(n-1) p | 1/p | (1-p)/p² |
| Uniform\[a, b\] | Continuous | All values equally likely | 1/(b-a) | (a+b)/2 | (b-a)²/12 |
| Exponential(λ) | Continuous | Waiting time to first event | λ e^(-λx), x ≥ 0 | 1/λ | 1/λ² |

## Common mistakes

- **Rate vs mean.** If a question gives the average wait (4 minutes), the exponential rate is λ = 1/4, not 4.
- **Geometric starts at 1.** It counts the trial that succeeds, so the smallest value is 1, not 0.
- **Binomial needs independence and a constant p.** Drawing cards without replacement breaks both.
- **Continuous means intervals.** For a uniform or exponential variable, P(X = exact value) = 0, so ask about ranges.
- **"At least one" success.** Use the complement: 1 - (1-p)^n for n trials.
- **Memoryless is rare.** Only Geometric and Exponential have it; Binomial and Uniform do not.
