# ANOS Foundations

This file records architectural principles that have been explicitly agreed upon. These are considered canonical unless superseded through an Architecture Decision Record (ADR).

## F-001 — Autonomous agency is fundamental

Autonomous agency is a fundamental execution paradigm of ANOS from the beginning. It is not a long-term optional feature, application, framework, plugin, assistant, or service layered over an otherwise conventional operating system.

## F-002 — ANOS is a general-purpose operating system

ANOS is intended to be an operating system in the same categorical sense that Linux, Windows, and macOS are operating systems—not merely an agent framework installed on another operating system.

Early prototypes may use an existing kernel or host platform to validate ANOS semantics, but the ANOS architecture is conceptually independent of that bootstrap implementation.

## F-003 — Agents are first-class computational principals

Autonomous agents are native ANOS entities with explicit system-recognized identity, lifecycle, authority, resource ownership, delegation relationships, communication semantics, memory/state, observability, and accountability.

An agent must not exist only as metadata maintained by an application-level orchestration framework.

## F-004 — Deterministic programs remain native

Conventional deterministic programs remain native first-class workloads.

ANOS does not require every program, process, application, service, compiler, database, shell utility, or GUI application to become an agent.

Agentic execution extends rather than replaces conventional process-based computing.

## F-005 — Agent is not synonymous with LLM

ANOS defines agents by their execution semantics and authority model rather than by a particular model technology.

An ANOS agent may be implemented using an LLM, symbolic planner, compiler analysis engine, rule-based system, hybrid architecture, robotics controller, or future computational model.

## F-006 — Process and agent are distinct abstractions

A process answers: **what execution context is running?**

An agent answers: **which autonomous computational principal is responsible for pursuing this goal?**

An agent may own or coordinate multiple processes, tools, services, and child agents.

Processes execute instructions. Agents pursue goals under delegated authority.

## F-007 — Agent identity is distinct

Human identity, system identity, process identity, and agent identity are distinct concepts.

ANOS should provide a native agent identifier (working term: **AID**) analogous in importance—but not necessarily implementation—to PID, UID, and GID.

## F-008 — Authority is explicitly delegated

Agent authority is explicitly delegated, scoped, revocable, auditable, and attributable.

A child agent cannot receive authority that its parent agent does not possess.

The intended invariant is:

`ChildCapabilities ⊆ ParentCapabilities`

subject to delegation policy defined by ANOS.

## F-009 — Autonomy without sovereignty

Agents may autonomously determine how to pursue authorized goals, but they do not determine the authority they possess.

ANOS remains the ultimate enforcement authority.

## F-010 — Probabilistic reasoning does not replace deterministic enforcement

Agents may reason probabilistically and request operations. Security policy, capability enforcement, isolation, resource limits, and other system guarantees must be enforced by deterministic mechanisms.

The operating system must not rely on an agent or language model behaving correctly for system safety.

## F-011 — Native agentic concerns permeate the OS

Agentic semantics belong inside the native operating-system architecture, including:

- identity
- execution
- authority
- delegation
- security
- scheduling
- resource management
- memory and persistent agent state
- communication
- lifecycle
- observability
- accountability

There should not be a detachable "AI layer" whose removal leaves an otherwise complete conventional OS claiming to be ANOS.

## F-012 — Conventional and autonomous execution coexist

ANOS supports at least two native forms of workload execution:

1. Conventional deterministic execution through processes/threads.
2. Autonomous goal-directed execution through agents, which may themselves own processes, tools, and sub-agents.

Neither form requires the other to disappear.

## F-013 — Responsibility must be attributable

ANOS must be able to determine not only which process performed an operation but also which agent caused it, which principal authorized that agent, and through what delegation chain the authority flowed.

## F-014 — Agent lifecycle is distinct from process lifecycle

Agent creation, authorization, activation, delegation, checkpointing, suspension, resumption, completion, revocation, and termination are conceptually distinct from process start/stop/exit semantics.

## F-015 — Agent resources are first-class system resources

ANOS should account for resources relevant to autonomous execution, including traditional resources such as CPU, RAM, storage, network, and GPU, as well as agent-specific budgets such as model usage, tokens, cost, action count, delegation depth, child count, time, and other bounded resources.
