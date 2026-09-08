# Contextual Drug Embeddings

Research code for testing whether a drug should have a **context-dependent representation** rather than a single fixed embedding.

## Core question

> Does conditioning drug representations on biological context capture response-relevant information that cannot be explained by ordinary drug identity or categorical context encoding?

We are especially interested in the hypothesis that the meaning of an intervention depends on the biological state in which it is applied:

\[
z(d, c) \neq z(d)
\]

where `d` is a drug and `c` is a biological context such as a cell line, molecular subtype, mutation, pathway state, or biomarker-defined condition.

## Scientific priority

This repository is **falsification-first**.

Before building a contextual embedding model, test whether the available data support a non-trivial context-dependent signal and whether natural-language conditioning has any plausible advantage over simpler categorical conditioning.

The first phase should answer:

1. Are the same drugs observed across sufficiently diverse biological contexts?
2. Does response vary enough within drug across contexts to justify context-dependent representations?
3. Are there held-out context / biomarker combinations suitable for compositional OOD evaluation?
4. Can a simple drug + categorical-context baseline already explain the apparent signal?
5. Is there any realistic test where language semantics could help beyond verbose categorical encoding?

If not, stop or pivot before training a complex model.

## Initial evaluation ladder

Only advance as evidence justifies it:

1. Data / identifiability audit
2. Fixed drug representation baseline
3. Drug + categorical context baseline
4. Simple interaction baseline
5. Natural-language-conditioned representation
6. Compositional OOD / held-out biomarker evaluation
7. Strong leakage and shortcut controls

Do not jump directly to step 5.

## Decision rule

Every major run should end with one of:

- **GO** — central claim survives and merits the next experiment
- **PIVOT** — interesting signal exists, but the original claim is not supported
- **KILL** — current data / hypothesis do not justify further investment

Negative results are valid outcomes.

## Repository structure

```text
.
├── AGENTS.md
├── EXPERIMENT_LOG.md
├── OVERNIGHT_STATUS.md
├── RESEARCH_PLAN.md
├── data/
├── results/
├── scripts/
└── src/
```

Raw or large datasets should remain local and be ignored by Git.
