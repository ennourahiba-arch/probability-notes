# Probability Distributions Study Sheet

## 1) Bernoulli Distribution

A Bernoulli random variable models **one trial** with two outcomes:

- success (1) with probability \(p\)
- failure (0) with probability \(1-p\)

\[
X\sim \mathrm{Bernoulli}(p),\qquad P(X=1)=p,\; P(X=0)=1-p
\]

- Support: \(\{0,1\}\)
- Mean: \(\mathbb E[X]=p\)
- Variance: \(\mathrm{Var}(X)=p(1-p)\)

**Use when:** one yes/no event (pass/fail, head/tail, defective/not defective).

---

## 2) Uniform Distribution

A random variable is uniform when all values are equally likely.

### Discrete uniform on \(\{1,\dots,n\}\)

\[
P(X=k)=\frac{1}{n},\quad k=1,\dots,n
\]

More generally, on finite set \(S\):

\[
P(X=x)=\frac{1}{|S|},\quad x\in S
\]

### Continuous uniform on \([a,b]\)

\[
f(x)=\frac{1}{b-a},\quad a\le x\le b
\]

- Mean: \(\frac{a+b}{2}\)
- Variance: \(\frac{(b-a)^2}{12}\)

**Use when:** “chosen at random”, “equally likely”, or no value is favored.

---

## 3) Binomial Distribution

A binomial random variable counts successes in **\(n\) independent Bernoulli(\(p\)) trials**.

\[
X\sim \mathrm{Bin}(n,p),\qquad
P(X=k)=\binom{n}{k}p^k(1-p)^{n-k},\; k=0,\dots,n
\]

- Mean: \(\mathbb E[X]=np\)
- Variance: \(\mathrm{Var}(X)=np(1-p)\)

**Use when:** “exactly \(k\) successes in \(n\) trials”.

---

## 4) Geometric Distribution

A geometric random variable is the trial number of the **first success** in repeated independent Bernoulli(\(p\)) trials.

\[
X\sim \mathrm{Geom}(p),\qquad
P(X=n)=(1-p)^{n-1}p,\; n=1,2,\dots
\]

- Mean: \(\mathbb E[X]=\frac{1}{p}\)
- Variance: \(\mathrm{Var}(X)=\frac{1-p}{p^2}\)

Memoryless property:

\[
P(X>s+t\mid X>s)=P(X>t)
\]

**Use when:** “first success”, “how many trials until success”.

---

## 5) Exponential Distribution

An exponential random variable models **continuous waiting time** until the first event (rate \(\lambda>0\)).

\[
X\sim \mathrm{Exp}(\lambda)
\]

Density:

\[
f(x)=\lambda e^{-\lambda x},\quad x\ge0
\]

CDF:

\[
F(x)=P(X\le x)=1-e^{-\lambda x},\quad x\ge0
\]

Tail:

\[
P(X>x)=e^{-\lambda x}
\]

- Mean: \(\mathbb E[X]=\frac{1}{\lambda}\)
- Variance: \(\mathrm{Var}(X)=\frac{1}{\lambda^2}\)

Memoryless property:

\[
P(X>s+t\mid X>s)=P(X>t)
\]

**Use when:** waiting time, lifetime, time between arrivals.

---

## 6) Quick Comparison

| Distribution | Type | What it models | Key formula |
|---|---|---|---|
| Bernoulli | Discrete | One success/failure trial | \(P(X=1)=p\) |
| Uniform | Discrete/Continuous | All values equally likely | \(P(X=x)=1/|S|\) or \(f(x)=1/(b-a)\) |
| Binomial | Discrete | Number of successes in \(n\) trials | \(\binom{n}{k}p^k(1-p)^{n-k}\) |
| Geometric | Discrete | Trial of first success | \((1-p)^{n-1}p\) |
| Exponential | Continuous | Waiting time to first event | \(\lambda e^{-\lambda x}\) |
