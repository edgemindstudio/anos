# ADR-0001: ANOS is agentic-native, not merely agent-aware

- Status: Accepted
- Date: 2026-10-04

## Context

The project must distinguish a true agentic-native operating-system architecture from a conventional operating system with an agent framework, AI assistant, daemon, plugin, or orchestration service installed on top.

## Decision

ANOS will treat autonomous agents as first-class computational principals within the operating system's native architectural model.

Agent semantics must participate in identity, execution, authority, security, scheduling, memory, communication, resource management, lifecycle, observability, and accountability.

## Consequence

A design in which all agent semantics live only inside an ordinary user-space orchestration application is insufficient to satisfy the ANOS architecture, even if such a layer is used temporarily for prototyping individual ideas.
