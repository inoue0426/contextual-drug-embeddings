# Research Plan

## Working hypothesis

A useful drug representation may depend on biological context:

\[
z(d,c) = E(\text{drug}, \text{context})
\]

rather than being fixed as `z(d)`.

The stronger claim is not merely that context improves drug-response prediction. The stronger claim is that **context changes the representation of the intervention in a way that supports generalization to unseen biological combinations**.

## Main alternative explanations

1. Context conditioning is just ordinary categorical covariate modeling.
2. Natural-language context descriptions merely re-encode known labels.
3. Gains arise from drug identity or cell-line leakage.
4. Random train/test splits reward memorization rather than compositional generalization.
5. Context-dependent response exists, but a simple interaction model captures it completely.
6. Any language benefit comes from external factual leakage rather than compositional semantics.

## Phase 1 — Identifiability audit

Before model training, characterize the candidate dataset(s):

- number of drugs;
- number of biological contexts;
- observations per drug and per context;
- number of drugs shared across contexts;
- within-drug response variance across contexts;
- context definitions available (cell line, tissue, mutations, biomarkers, pathway states, etc.);
- missingness and imbalance;
- repeated measures / duplicate observations;
- degree of drug × context crossing;
- feasibility of grouped and compositional OOD splits.

### Gate 1

Proceed only if there is enough crossed structure to distinguish a contextual effect from drug or context identity.

## Phase 2 — Cheapest contextual-signal test

Without building a language-conditioned model, compare simple baselines such as:

1. drug-only;
2. context-only;
3. drug + context additive;
4. drug × context interaction / simple bilinear model;
5. response-history or nearest-context baselines where scientifically valid.

Evaluate on grouped splits that prevent trivial memorization.

### Gate 2

If simple context modeling does not materially outperform drug-only prediction, the contextual-embedding premise is weak for the chosen dataset.

If a simple interaction model completely captures the signal, natural-language conditioning needs a stronger motivation before proceeding.

## Phase 3 — Language necessity test

Only after Gates 1–2 pass, test whether natural-language conditioning offers information beyond categorical context encoding.

Critical comparisons:

- fixed drug representation;
- categorical context conditioning;
- structured biomarker conditioning;
- natural-language context conditioning;
- shuffled / semantically corrupted context descriptions.

The natural-language model must be evaluated under conditions where simple category memorization is insufficient.

## Phase 4 — Compositional OOD

Prefer evaluation such as:

- held-out drug × biomarker combinations;
- held-out biomarker combinations within known drugs;
- held-out molecular subtypes;
- held-out context families;
- zero-shot descriptions composed from known biological attributes.

The exact split must be leakage-safe and prospectively computable.

## Phase 5 — Representation diagnostics

If predictive evidence survives, ask whether the learned embedding itself behaves contextually in a biologically meaningful way.

Potential diagnostics:

- same drug moves systematically across contexts;
- embedding shifts align with response changes;
- similar biological contexts induce similar representation shifts;
- context shifts recover known mechanism / resistance relationships;
- representations generalize rather than merely cluster by label.

## Success criterion

A strong result would show that context-conditioned drug representations provide reproducible gains over drug identity and categorical/structured context baselines on a genuinely compositional or OOD task, with appropriate leakage controls.

## Kill criterion

Stop or pivot if:

- the dataset lacks sufficient crossed drug × context structure;
- contextual effects disappear under grouped splits;
- simple categorical / interaction models explain the full signal;
- natural-language conditioning does not outperform strong structured controls;
- gains vanish under semantic corruption or leakage controls.

## First autonomous task

Perform Phase 1 and the cheapest feasible part of Phase 2. Do not begin by implementing a large language-conditioned architecture.

End the first run with an explicit `GO`, `PIVOT`, or `KILL` decision and the cheapest next experiment that could change that decision.
