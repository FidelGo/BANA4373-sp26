# ECON 4370 — Potential Outcomes & The Causal Inference Problem

**Dr. Fidel Gonzalez**  
**Department of Economics and International Business**  
**Sam Houston State University**

---

## Overview

This lecture introduces the formal language of causal inference. The central idea is simple:

A causal effect compares two potential outcomes for the **same unit**:

- what happens if the unit is treated,
- and what happens if the same unit is not treated.

The difficulty is that we only ever observe **one** of those outcomes. The other one is the missing counterfactual.

---

## Learning Objectives

After this lecture, you should be able to:

1. **State the fundamental problem of causal inference.** Explain why we cannot observe both the treated and untreated outcomes for the same unit at the same time.
2. **Use potential outcomes notation correctly.** Interpret \(Y_i^1\), \(Y_i^0\), \(D_i\), and \(\delta_i\).
3. **Define the switching equation.** Show how observed outcomes depend on treatment status.
4. **Distinguish ATE, ATT, and ATU.** Explain which causal question each one answers.
5. **Decompose the simple difference in outcomes.** Understand why the raw treated-minus-untreated comparison is usually not the causal effect.
6. **Interpret selection bias and HTE bias.** Explain how baseline differences and heterogeneous effects distort naive comparisons.
7. **Explain why randomization is the gold standard.** Connect independence to the disappearance of bias.
8. **Understand the role of SUTVA.** Recognize the assumptions needed for the potential outcomes framework to make sense.

---

## The Fundamental Problem of Causal Inference

A causal effect compares two states of the world for the same unit.

- **Actual world:** patient takes aspirin, headache severity = 2
- **Counterfactual world:** same patient does **not** take aspirin, headache severity = ?

The problem is that we only ever observe **one** of these two states.

---

## Potential Outcomes Notation

Each unit \(i\) has two potential outcomes:

\[
Y_i^1 = \text{outcome if unit } i \text{ receives treatment}
\]

\[
Y_i^0 = \text{outcome if unit } i \text{ does not receive treatment}
\]

The individual treatment effect is:

\[
\delta_i = Y_i^1 - Y_i^0
\]

We never observe both \(Y_i^1\) and \(Y_i^0\) for the same unit.

---

## The Switching Equation

\[
Y_i = D_iY_i^1 + (1-D_i)Y_i^0
\]

where:

- \(D_i = 1\) if treated
- \(D_i = 0\) if untreated

If \(D_i=1\), then \(Y_i = Y_i^1\).  
If \(D_i=0\), then \(Y_i = Y_i^0\).

---

## Three Causal Parameters of Interest

### Average Treatment Effect (ATE)

\[
ATE = E[Y_i^1] - E[Y_i^0]
\]

### Average Treatment Effect on the Treated (ATT)

\[
ATT = E[Y_i^1 \mid D=1] - E[Y_i^0 \mid D=1]
\]

### Average Treatment Effect on the Untreated (ATU)

\[
ATU = E[Y_i^1 \mid D=0] - E[Y_i^0 \mid D=0]
\]

### Weighted-average relationship

\[
ATE = \pi \cdot ATT + (1-\pi)\cdot ATU
\]

where \(\pi\) is the share treated.

In the lecture example:

- \(ATE = 0.6\)
- \(ATT = 4.4\)
- \(ATU = -3.2\)

---

## The Simple Difference in Outcomes (SDO)

\[
SDO = E[Y \mid D=1] - E[Y \mid D=0]
\]

Using potential outcomes notation:

\[
SDO = E[Y_i^1 \mid D=1] - E[Y_i^0 \mid D=0]
\]

### First decomposition

\[
SDO =
\Big(E[Y_i^1 \mid D=1] - E[Y_i^0 \mid D=1]\Big)
+
\Big(E[Y_i^0 \mid D=1] - E[Y_i^0 \mid D=0]\Big)
\]

So:

\[
SDO = ATT + \text{Selection Bias}
\]

### Full decomposition

\[
SDO = ATE + \text{Selection Bias} + \text{HTE Bias}
\]

---

## Selection Bias

\[
\text{Selection Bias} = E[Y_i^0 \mid D=1] - E[Y_i^0 \mid D=0]
\]

This measures the baseline difference between treated and untreated groups that would exist even if neither group were treated.

---

## Heterogeneous Treatment Effect Bias

\[
\text{HTE Bias} = ATT - ATE = (1-\pi)(ATT-ATU)
\]

Even if selection bias were zero, the simple comparison would still fail to recover the population ATE whenever \(ATT \neq ATU\).

---

## Putting It Together

In the lecture example:

- \(ATE = 0.6\)
- Selection Bias \(= -4.8\)
- HTE Bias \(= 3.8\)

So:

\[
SDO = 0.6 + (-4.8) + 3.8 = -0.4
\]

The true average effect is positive, but the raw treated-minus-untreated comparison is negative.

---

## The Independence Assumption

\[
(Y_i^1, Y_i^0) \perp D_i
\]

Under independence:

- Selection bias = 0
- HTE bias = 0
- therefore:

\[
SDO = ATE
\]

---

## Randomization: The Gold Standard

Randomization makes treatment assignment independent of potential outcomes.

Because treatment is assigned by chance, treated and untreated groups are statistically identical on average in both observed and unobserved dimensions.

---

## SUTVA: The Fine Print

The Stable Unit Treatment Value Assumption (SUTVA) requires:

1. **No variation in treatment doses**
2. **No spillovers / externalities**
3. **No general equilibrium effects**

---

## Quick Reference

\[
Y_i^1,\quad Y_i^0,\quad D_i,\quad \delta_i = Y_i^1 - Y_i^0
\]

\[
Y_i = D_iY_i^1 + (1-D_i)Y_i^0
\]

\[
ATE = E[Y_i^1] - E[Y_i^0]
\]

\[
ATT = E[Y_i^1 \mid D=1] - E[Y_i^0 \mid D=1]
\]

\[
ATU = E[Y_i^1 \mid D=0] - E[Y_i^0 \mid D=0]
\]

\[
ATE = \pi \cdot ATT + (1-\pi)\cdot ATU
\]

\[
SDO = ATE + \text{Selection Bias} + \text{HTE Bias}
\]

\[
\text{Selection Bias} = E[Y^0 \mid D=1] - E[Y^0 \mid D=0]
\]

\[
\text{HTE Bias} = ATT - ATE = (1-\pi)(ATT-ATU)
\]

\[
(Y^1, Y^0) \perp D
\]

---

*ECON 4370 · Potential Outcomes & The Causal Inference Problem · Dr. Fidel Gonzalez*
