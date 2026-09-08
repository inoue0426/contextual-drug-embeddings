# AGENTS.md

This repository is operated as a falsification-first research project.

## Read first

Before doing substantial work, read:

1. `README.md`
2. `RESEARCH_PLAN.md`
3. `EXPERIMENT_LOG.md`
4. `OVERNIGHT_STATUS.md`

Then inspect the current repository and local data before proposing new downloads or model development.

## Operating principle

The goal is not to build the most sophisticated contextual drug embedding model.

The goal is to determine, as cheaply and rigorously as possible, whether biological context changes the useful representation of a drug in a way that is not already captured by simpler baselines.

Prefer:

`data -> experiment -> metrics -> controls -> failure analysis -> next cheapest experiment`

over

`architecture -> tuning -> benchmark expansion`.

## Core claim under test

> Context-conditioned drug representations provide predictive or representational information beyond drug identity and simple categorical context encoding, especially under compositional or OOD generalization.

Natural-language conditioning is not assumed to be useful. It must earn its complexity.

## Research discipline

- Test identifiability and dataset structure before training models.
- Use the simplest interpretable baseline first.
- Explicitly compare natural-language conditioning against categorical conditioning.
- Prefer grouped / compositional / OOD splits over random splits.
- Guard against drug leakage, cell-line leakage, biomarker leakage, and duplicated context descriptions.
- Do not tune prompts, architectures, or hyperparameters merely to rescue a weak result.
- Treat negative results as valid.
- When results look implausibly strong, actively search for leakage or structural shortcuts.
- Preserve contradictory findings.

## Required status block

Keep `OVERNIGHT_STATUS.md` current with:

```text
CURRENT CLAIM:
STRONGEST EVIDENCE:
STRONGEST ALTERNATIVE EXPLANATION:
FALSIFICATION ATTEMPT:
DECISION: GO / PIVOT / KILL
NEXT EXPERIMENT:
ESTIMATED COST:
```

## Logging

For each meaningful experiment, append to `EXPERIMENT_LOG.md`:

- question tested;
- data subset and split;
- method / baseline;
- metrics;
- controls;
- what became stronger or weaker;
- decision;
- next cheapest discriminating experiment.

## Autonomy

Implement, execute, evaluate, add controls, document, and commit coherent checkpoints.

Do not stop after code generation if the experiment can reasonably be executed locally.

Stop when:

- there is a genuine blocker requiring human input;
- the project reaches a defensible KILL decision;
- the next step would require major scope expansion rather than another discriminating experiment.
