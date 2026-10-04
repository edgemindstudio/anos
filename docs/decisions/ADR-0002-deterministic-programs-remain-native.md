# ADR-0002: Conventional deterministic programs remain native workloads

- Status: Accepted
- Date: 2026-10-04

## Context

Making agents first-class must not imply that every workload has to become agentic.

## Decision

ANOS will natively support conventional deterministic programs, processes, threads, services, and applications alongside native agents.

Agentic execution extends the traditional process model; it does not replace deterministic computing.

## Consequence

Ordinary software such as compilers, databases, shells, utilities, servers, and GUI programs can run without being modeled as autonomous agents. Agents may invoke and coordinate these deterministic tools.
