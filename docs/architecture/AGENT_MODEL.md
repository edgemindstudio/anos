# ANOS Native Agent Model

## Status

Draft architecture specification under active review.

This document captures the current ANOS native-agent model. Canonical foundations and accepted Architecture Decision Records take precedence if a conflict is discovered. Provisional mechanisms in this document must not be treated as a stable ABI or implementation commitment unless separately accepted.

This document defines the native agent abstraction of ANOS. It builds upon the canonical principles recorded in `docs/foundations/FOUNDATIONS.md`.

---

# 1. Definition

An ANOS agent is a goal-directed computational principal capable of autonomously selecting actions and initiating system operations within explicitly delegated authority and system-enforced resource constraints. Its identity and state may persist independently of any individual process.

An agent is a native operating-system entity.

An agent is not merely:

- a process,
- a thread,
- an LLM session,
- a chatbot,
- a service,
- a container,
- a workflow,
- or metadata maintained by an application-level orchestration framework.

ANOS recognizes the agent itself as a computational principal.

---

# 2. Fundamental distinction

A process answers:

> What execution context is running?

An agent answers:

> Which autonomous computational principal is responsible for pursuing this goal?

Processes execute instructions.

Agents pursue goals under delegated authority.

An agent may own, create, coordinate, or invoke multiple processes and may delegate work to child agents.

---

# 3. Native execution coexistence

ANOS natively supports both conventional and autonomous execution.

```text
                         ANOS
                          |
                Native Execution Model
                          |
             +------------+------------+
             |                         |
             v                         v
     Conventional                 Autonomous
      Execution                    Execution
             |                         |
          Process                     Agent
             |                         |
          Threads          +-----------+-----------+
                           |           |           |
                       Processes     Tools     Sub-agents
```

Conventional software does not need to become agentic in order to execute on ANOS.

Agentic execution extends the operating-system execution model rather than replacing process-based computation.

---

# 4. Agent identity

Every native ANOS agent has a system-recognized identity.

Working identifier:

```text
AID — Agent Identifier
```

An AID is conceptually distinct from:

```text
UID — user identity
GID — group identity
PID — process identity
TID — thread identity
AID — agent identity
```

The existence of an AID does not imply that its implementation must resemble Unix identifiers.

The identifier exists so that ANOS can attribute execution, authority, resources, communication, delegation, and audit events to a specific autonomous principal.

---

# 5. Agent principal

An agent is a principal rather than merely an execution container.

A principal is an entity to which ANOS may attach:

- identity,
- authority,
- capabilities,
- resource ownership,
- policy,
- accountability,
- communication rights,
- and lifecycle state.

An agent may act on behalf of another principal while retaining its own distinct identity.

Example:

```text
Human Principal
UID 1000
    |
    | delegates
    v
Development Agent
AID 20
    |
    | delegates subset
    v
Compiler Agent
AID 27
```

ANOS must preserve the distinction between the authorizing principal and the autonomous agent performing the work.

---

# 6. Delegation lineage

Every delegated agent should have an attributable authority lineage.

Example:

```text
Human
  |
  +-- DevelopmentAgent
        |
        +-- CompilerAgent
              |
              +-- BenchmarkAgent
```

A system operation initiated by `BenchmarkAgent` should be attributable through the complete chain when required:

```text
UID 1000
 -> AID 20
 -> AID 27
 -> AID 31
 -> PID 9124
 -> requested operation
```

Delegation lineage is part of native ANOS accountability.

---

# 7. Authority invariant

Authority does not originate from the agent itself.

Authority must be granted by an authorized principal or by an ANOS policy permitted to make such grants.

For ordinary hierarchical delegation, the intended invariant is:

```text
ChildCapabilities ⊆ ParentCapabilities
```

A child agent must not acquire authority solely because it requests or reasons that the authority is useful.

Authority must remain:

- explicit,
- scoped,
- revocable,
- attributable,
- auditable,
- and system-enforced.

---

# 8. Autonomy without sovereignty

Agents possess autonomy but not sovereignty.

An agent may autonomously determine how to pursue a goal within its authorized operating envelope.

An agent cannot autonomously redefine that operating envelope.

Therefore:

```text
Agent:
    chooses actions

ANOS:
    determines whether those actions are permitted
```

The operating system remains the ultimate enforcement authority.

---

# 9. Agent Control State

ANOS requires native state associated with every agent.

The working architectural concept is an:

```text
ACB — Agent Control Block
```

The ACB is conceptually analogous in importance to process-control state, but represents an agent rather than a process.

A conceptual ACB may contain:

```text
Agent Control Block
|
+-- AID
+-- principal / owner
+-- parent AID
+-- delegation lineage
+-- lifecycle state
+-- goals
+-- capabilities
+-- policies
+-- resource budgets
+-- process membership
+-- child agents
+-- communication endpoints
+-- agent memory references
+-- audit/provenance references
+-- creation metadata
+-- checkpoint state
```

This structure is architectural, not yet an implementation specification.

Whether all ACB state belongs in the kernel is intentionally unresolved.

---

# 10. Agent-to-process relationship

An agent may own zero, one, or many processes.

Example:

```text
AID 42 — CompilerAgent
|
+-- PID 3110 — clang
+-- PID 3118 — linker
+-- PID 3131 — benchmark
|
+-- AID 46 — ProfileAgent
      |
      +-- PID 3160 — perf
```

Processes associated with an agent remain ordinary executable contexts.

The presence of an owning agent adds agent-level identity, authority, resource, provenance, and lifecycle semantics.

A process must not automatically become an agent merely because it is started by one.

---

# 11. Agent-to-tool relationship

A tool is not necessarily an agent.

A compiler agent may invoke:

```text
clang
cmake
make
perf
git
```

without those programs becoming autonomous principals.

ANOS must distinguish:

```text
agent
```

from:

```text
tool used by agent
```

This distinction preserves compatibility with deterministic software.

---

# 12. Agent-to-model relationship

An agent is not synonymous with an AI model.

The reasoning mechanism used by an agent may include:

- large language models,
- small language models,
- symbolic planners,
- rule systems,
- search algorithms,
- compiler analyses,
- learned policies,
- robotics controllers,
- hybrid systems,
- or future computational mechanisms.

ANOS defines agency through system semantics rather than model technology.

The operating system should not require knowledge of the internal reasoning architecture unless that knowledge is necessary for resource management, policy, or security.

---

# 13. Goal-directed execution

Agents are goal-directed entities.

A goal represents what an agent is attempting to accomplish.

A goal is not equivalent to authority.

For example:

```text
Goal:
    Build and optimize project

Authority:
    read /project/src
    write /project/build
    execute clang
    execute cmake
    no network access
```

The semantic goal may be expressed flexibly.

The enforceable authority envelope must remain machine-verifiable.

ANOS must not grant authority merely because an operation appears semantically related to an agent's natural-language goal.

---

# 14. Probabilistic reasoning boundary

Agent reasoning may be probabilistic.

System enforcement must not depend upon probabilistic compliance.

The architectural boundary is:

```text
      Autonomous Agent
   probabilistic reasoning
             |
             | requests action
             v
    -----------------------
      TRUST BOUNDARY
    -----------------------
             |
             v
 Deterministic ANOS Policy
             |
        allow / deny
```

Examples of deterministic enforcement include:

- capability checks,
- resource limits,
- isolation,
- delegation restrictions,
- access-control rules,
- lifecycle controls,
- revocation,
- and mandatory approval boundaries.

---

# 15. Native lifecycle

Agent lifecycle is distinct from process lifecycle.

Candidate native lifecycle operations include:

```text
create
authorize
activate
delegate
checkpoint
suspend
resume
complete
revoke
terminate
```

A suspended agent may have no active processes while still existing as an ANOS principal.

An agent may therefore outlive any individual process associated with it.

---

# 16. Candidate agent states

Initial conceptual states include:

```text
CREATED
AUTHORIZED
RUNNABLE
RUNNING
WAITING
SUSPENDED
AWAITING_APPROVAL
POLICY_BLOCKED
BUDGET_EXHAUSTED
COMPLETED
FAILED
REVOKED
TERMINATED
```

These states are provisional and require later lifecycle design.

They must not yet be treated as a stable ABI.

---

# 17. Resource ownership

An agent may own or be charged for resources independently of individual process lifetimes.

Potential resources include:

Traditional resources:

- CPU
- memory
- storage
- network
- GPU
- devices

Agent-related resources:

- model inference
- tokens
- API expenditure
- action count
- wall-clock lifetime
- delegation depth
- child-agent count
- tool invocations
- persistent agent memory

Resource accounting must be attributable to the responsible agent.

---

# 18. Agent memory

ANOS distinguishes ordinary computational memory from persistent agent state.

Potential agent state includes:

- working context,
- goal state,
- execution history,
- semantic memory,
- artifacts,
- tool state,
- delegation state,
- checkpoints,
- and persistent task state.

Agent memory requires native isolation and authorization semantics.

One agent must not automatically receive access to another agent's persistent state merely because both execute under the same human user.

The precise ANOS agent-memory architecture remains an open design area.

---

# 19. Agent communication

Agents require native communication semantics beyond ordinary byte transport.

Candidate operations include:

```text
send message
request task
delegate task
return result
request capability
grant capability
revoke capability
cancel task
report failure
request human approval
```

The implementation may reuse ordinary IPC mechanisms, but ANOS must preserve agent identity, authority, provenance, and policy semantics across the communication.

---

# 20. Agent observability

ANOS must make autonomous activity inspectable.

The system should eventually be able to answer:

```text
Which agent is running?
Who authorized it?
What goal is it pursuing?
What authority does it possess?
What processes belong to it?
What resources has it consumed?
What agents has it created?
What operations has it attempted?
Which actions were denied?
What is its delegation lineage?
What state is it currently in?
```

Agent observability is part of the operating system, not merely application logging.

---

# 21. Accountability

ANOS must support attribution beyond process identity.

A consequential operation should be attributable, where applicable, through:

```text
authorizing principal
       |
delegation lineage
       |
responsible agent
       |
executing process
       |
system operation
```

This supports audit, debugging, security analysis, policy enforcement, and human oversight.

---

# 22. Compatibility principle

ANOS must not require deterministic applications to adopt agent semantics.

Existing software should remain usable as conventional process-based workloads wherever technically compatible.

An ordinary C program should be able to remain an ordinary C program.

An ordinary compiler should be able to remain an ordinary compiler.

An ordinary shell command should be able to remain an ordinary shell command.

Agents may invoke these programs without transforming them into agents.

---

# 23. Native-agent test

A proposed ANOS design is not considered agent-native merely because agents can execute on it.

For each major agent feature, ask:

1. Does ANOS itself recognize the agent principal?
2. Does the system know the agent identity?
3. Can authority be attached directly to the agent?
4. Can resources be attributed directly to the agent?
5. Can delegation be represented and enforced?
6. Can the agent lifecycle exist independently of a single process?
7. Can operations be traced back to the responsible agent?
8. Would removing an application-level agent framework leave these semantics intact?

If the answer to these questions is no, the design may be agent-aware or agent-integrated rather than agent-native.

---

# 24. Non-goals of this document

This document does not yet decide:

- monolithic kernel vs microkernel vs hybrid kernel,
- whether ACBs reside wholly or partially in kernel space,
- exact system-call interfaces,
- exact AID representation,
- exact scheduler algorithms,
- exact agent memory implementation,
- exact agent IPC protocol,
- exact model-runtime architecture,
- exact compatibility strategy with Linux binaries,
- or whether the first ANOS prototype uses Linux as a bootstrap kernel.

Those decisions require separate architecture work and ADRs.

---

# 25. Core invariant

The defining invariant of the ANOS agent model is:

> An autonomous agent is a first-class computational principal whose identity, authority, execution, resources, lifecycle, delegation, communication, observability, and accountability are recognized and governed natively by ANOS.
