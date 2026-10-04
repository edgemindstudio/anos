# ANOS Threat Model — Initial Skeleton

## Fundamental assumption

ANOS must assume that an autonomous agent may become confused, maliciously influenced, compromised, or simply wrong.

System safety must therefore not depend on model alignment or agent obedience alone.

## Initial threats

- Prompt injection through files, web content, messages, tool outputs, or other agents.
- Agent attempting to exceed delegated authority.
- Child agent attempting privilege amplification.
- Recursive or uncontrolled agent spawning.
- Excessive token/API/compute/resource consumption.
- Unauthorized data exfiltration.
- Confused-deputy behavior.
- Agent impersonation or identity spoofing.
- Delegation-chain forgery.
- Cross-agent memory leakage.
- Policy bypass through ordinary processes launched by an agent.
- Audit/provenance tampering.
- Stale capabilities after revocation.

## Security principle

> Assume the agent can be compromised; protect the system anyway.
