# ANOS Open Questions

These questions are intentionally unresolved. They should remain visible until ANOS reaches an explicit architectural decision.

## Agent abstraction
- What minimum state makes an entity an ANOS agent?
- Is an agent always persistent, or may ephemeral agents exist?
- Which parts of an Agent Control Block belong in kernel space versus user space?

## Identity
- What guarantees must an AID provide?
- How are human, system, service, and agent principals represented and related?
- How is agent identity authenticated across machines?

## Delegation
- What is the precise capability algebra?
- How are capabilities attenuated when delegated?
- How are delegation chains represented, validated, and revoked?

## Security
- What is the default-deny boundary for agents?
- How does ANOS remain safe when an agent is compromised by prompt injection or malicious input?
- Which security operations require human approval?

## Goals and policy
- How should semantic goals be represented?
- What, if anything, should the OS understand about goal semantics?
- How do we guarantee that natural-language reasoning never becomes the sole authority for security decisions?

## Scheduling and resources
- Is there a separate agent scheduler or a hierarchical resource manager above process scheduling?
- How should token, inference, API, cost, and model resources be represented?

## Memory
- What constitutes protected agent memory?
- Can agent semantic memory be shared using capability-based access?
- How are agents checkpointed and restored?

## Communication
- What native Agent-to-Agent Communication (AAC/AIPC) primitives are required?
- How are task delegation and result return distinguished from ordinary IPC?

## Compatibility
- What compatibility layer should ANOS provide for POSIX/Linux software?
- Should the first system be Linux-kernel-based, microkernel-based, or begin as an experimental substrate?

## Compiler/runtime integration
- Which compiler/runtime functions become agent-native?
- How can probabilistic optimization proposals be combined with deterministic compiler verification?
