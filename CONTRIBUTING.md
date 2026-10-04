# Contributing to ANOS

ANOS architecture should evolve deliberately.

## Rule for accepted fundamentals

An idea becomes canonical only when it is either:

1. recorded in `docs/foundations/FOUNDATIONS.md`, or
2. accepted through an ADR under `docs/decisions/`.

## Rule for unresolved ideas

Unresolved concepts belong in `docs/open-questions/OPEN_QUESTIONS.md` or a dedicated design note. They must not silently become architectural assumptions.

## Rule for superseding decisions

Do not erase historical decisions. Add a new ADR that supersedes the old decision and link the two.

## Design discipline

For every major ANOS feature, ask:

- Is this truly native to the operating system architecture?
- Could this be removed as an application without changing ANOS itself?
- What deterministic system mechanism enforces it?
- How does it interact with ordinary non-agent workloads?
- What is the security boundary?
- What is observable and attributable?
