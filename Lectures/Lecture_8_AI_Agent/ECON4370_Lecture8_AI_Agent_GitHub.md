# ECON 4370 — Building AI Economic Data Agents

**Dr. Fidel Gonzalez**  
**Department of Economics and International Business**  
**Sam Houston State University**

---

## Overview

This lecture connects the course’s core data skills to the next layer: **automation**. The goal is not just to run code, but to build a system that can interpret a question, choose the right steps, and return an economic answer.

In this course, an AI agent is not magic. It is a structured system that converts a natural-language question into an economic workflow.

---

## Learning Objectives

After this lecture, you should be able to:

1. **Explain what an AI agent is.**  
   Distinguish an agent from a regular script: a script follows fixed instructions, while an agent uses decision logic to choose which instructions to run.

2. **Describe the basic agent pipeline.**  
   Trace the full flow from user question to planner to tools to final output, including data pull, transformation, plot, and narrative.

3. **Understand why structure matters.**  
   Explain why JSON plans, approved tools, and restricted series menus make classroom agents more reliable and safer.

4. **Compare baseline and intermediate agents.**  
   Identify what changes when the model starts selecting series, transformations, and tasks more autonomously.

5. **Apply data engineering discipline.**  
   Recognize why frequency mismatches, date alignment, and resampling matter before computing correlations or plotting time series.

6. **Use API keys responsibly.**  
   Know what an API key is, why ChatGPT Plus is not the same as API access, and how to protect secrets in notebooks and shared projects.

7. **Interpret practical business value.**  
   Connect AI agents to dashboards, executive questions, automated reporting, and decision support inside organizations.

8. **See the next step in the course.**  
   Understand that solid economics + clean data + controlled tool use is the foundation for richer systems like regression agents, forecasting modules, and dashboards.

---

## Where This Fits in the Course

You already know how to:

- Pull data from APIs
- Clean and merge datasets
- Compute transformations
- Create visualizations
- Compute correlations

Today’s addition is:

\[
\text{Automation} + \text{Decision Logic} = \text{AI Agent}
\]

The agent sits **on top of** your existing data skills. It does not replace them.

---

## Traditional Script vs AI Agent

| Traditional Python Script | AI Agent |
|---|---|
| Static | Interprets natural language |
| Hard-coded variables | Chooses tools dynamically |
| User must know Python | Executes multi-step workflow |
| Limited flexibility | Generates interpretation |

### Main idea

A regular script is useful, but rigid.  
An AI agent feels more flexible because it can translate a user question into a sequence of approved actions.

---

## What Is an AI Agent?

A simple way to think about an AI agent is:

```text
User Question
    ↓
LLM Planner (structured JSON plan)
    ↓
Python Tools (data + analysis)
    ↓
Plot + Statistics + Narrative
```

### Why this matters

The system is not just answering with words. It is:

- deciding what data to use,
- deciding what transformation is needed,
- deciding what analysis to run,
- and returning evidence plus interpretation.

---

## Agent Architecture

A typical pipeline looks like this:

1. **User asks a question**  
   Example: “Did wages keep up with inflation after COVID?”

2. **Planner creates a structured plan**  
   The model decides which series, transformations, and tasks are needed.

3. **Python tools execute the work**  
   Pull data, clean it, merge it, calculate statistics, and generate plots.

4. **System returns output**  
   A chart, summary statistics, and an economic interpretation.

### Example planner output

```json
{
  "tool": "build_dataset",
  "series_ids": ["UNRATE", "CPIAUCSL"],
  "start_date": "2000-01-01",
  "transformations": ["compute_cpi_yoy"],
  "tasks": ["plot", "correlation"],
  "interpretation_goal": "Check whether inflation and unemployment move together"
}
```

### Why use a structured planner?

- **Reliability:** JSON reduces ambiguity.
- **Control:** The model only chooses from approved tools and approved series.
- **Teaching value:** Students can inspect the logic and debug it more easily.

---

## Two Versions of the Agent

### Version 1: Baseline Agent

**Characteristics:**

- Structured planner
- Limited decision space
- Reliable and controlled
- Good for learning architecture

**Goal:** understand how the LLM and tools interact.

### Version 2: Intermediate / More Autonomous Agent

**Upgrades:**

- Maps concepts to FRED series
- Chooses transformations such as levels vs. year-over-year
- Selects tasks like plotting or correlation
- Adapts to new questions

**Still safe because:**

- Approved series dictionary
- Structured JSON schema
- Controlled tool set

### Core comparison

| Feature | Version 1 | Version 2 |
|---|---|---|
| Planner | Simple and constrained | More adaptive |
| Series choice | Mostly pre-specified | Selected from approved dictionary |
| Transformations | More explicit | Can choose among approved options |
| Strength | Reliable and easy to teach | More flexible and realistic |
| Risk | Lower | Higher unless guarded |

### Main takeaway

\[
\text{Baseline} = \text{Structured Automation}
\qquad
\text{Intermediate} = \text{Adaptive Intelligence}
\]

---

## API Keys, Billing, and Security

### What is an API key?

An API key is:

- a secret string tied to your account,
- used for authentication,
- and used for billing.

It identifies your account for every API request.

Example format:

```text
sk-xxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

### ChatGPT Plus vs API

| ChatGPT Plus | OpenAI API |
|---|---|
| Subscription for chat interface | Separate billing |
| Used in the ChatGPT app/site | Usage-based pricing |
| Not the same as API access | Required for programmatic access |

### Security best practices

- Never hard-code API keys in shared notebooks
- Never upload keys to GitHub
- Use environment variables
- Revoke keys if exposed

Preferred pattern:

```python
import os
OPENAI_API_KEY = os.environ.get("OPENAI_API_KEY")
FRED_API_KEY = os.environ.get("FRED_API_KEY")
```

### Professional lesson

Security is part of professional data workflow.  
A system is not production-ready if it mishandles secrets.

---

## Data Engineering Lesson: Frequency Mismatch

One of the most useful ideas from the lecture is that many “AI failures” are actually **data failures**.

### Example

- CPI is often **monthly**
- Oil prices are often **daily**

If you merge them directly:

- most dates will not match,
- you will get many missing values,
- correlations may be `NaN`,
- and plots may be misleading.

### Correct solution

Resample the higher-frequency series first.

For example:

- convert daily oil prices to a monthly average,
- then merge with monthly CPI.

### Monthly aggregation formula

\[
\bar{X}_m = \frac{1}{N_m}\sum_{d \in m} X_d
\]

### Key principle

Good analysis requires **frequency alignment before comparison**.

---

## Useful Transformations and Statistics

### Year-over-year growth

\[
\text{YoY}_t = \left(\frac{X_t}{X_{t-12}} - 1\right)\times 100
\]

This is often the right transformation for price levels or wages when you want growth rates rather than raw levels.

### Correlation

\[
\rho_{XY} = \frac{\operatorname{Cov}(X,Y)}{\sigma_X \sigma_Y}
\]

Correlation helps summarize co-movement, but only after the series are aligned and cleaned properly.

---

## Interactive Visualization: Why Plotly?

Plotly is useful because it is:

- zoomable,
- interactive,
- easy to inspect with hover values,
- and better for demos and dashboards.

This makes economic analysis more engaging and easier to communicate.

---

## Live Demo Questions

Examples of questions the agent can answer:

- “Is there evidence of a Phillips Curve since 1990?”
- “Compare oil prices and inflation after 2015.”
- “Did wages keep up with inflation after COVID?”
- “Compare federal funds rate and inflation since 2000.”

### What students should observe

- which series the agent selects,
- which transformations it applies,
- how the plot is generated,
- and how the interpretation is written.

---

## Why This Matters for Business

Agents allow:

- executives to ask natural-language questions,
- automated economic dashboards,
- AI-assisted decision systems,
- workflow automation.

This is how AI becomes useful inside organizations: it lowers the friction between a question and a usable answer.

---

## Final Takeaway

A script follows instructions.  
An agent decides which instructions to follow.

That is the conceptual shift of the lecture.

But both still rely on:

- clean data,
- sensible transformations,
- sound economic reasoning,
- and careful interpretation.

---

## Next Steps

Possible future enhancements include:

- automatic regression tool,
- forecasting module,
- dashboard interface,
- multi-step economic reasoning.

You are now moving from running analysis manually to building systems that can help perform analysis.

---

## Quick Reference

### Core workflow

```text
Question → Planner → Tools → Evidence → Interpretation
```

### Safe design principles

- Use an approved series dictionary
- Use a controlled tool set
- Use structured planner output
- Handle keys securely
- Align data before analysis

### Most important message

AI agents are most useful when they combine:

\[
\text{Economics} + \text{Data Skills} + \text{Controlled Automation}
\]

---

*ECON 4370 · Building AI Economic Data Agents · Dr. Fidel Gonzalez*
