# Aegis

**Deterministic Execution-Time Authority for Confidential AI Systems**

Aegis formalizes a missing systems layer in AI deployments: execution-time authority arbitration.

Large language models can generate structured plans, tool calls, and state-modifying commands. Trusted Execution Environments (TEEs) protect confidentiality and integrity of computation. However, neither model alignment nor enclave isolation determines whether a generated action is *authorized* to execute.

Aegis enforces a strict invariant:

> No action executes without explicit, valid, and scoped authority at the moment of execution.

The model may propose actions.  
It does not authorize them.

## Motivation

As AI systems gain the ability to:

- call external APIs  
- access credentials  
- modify state  
- move value  
- orchestrate autonomous workflows  

the primary risk surface shifts from model output to action execution.

Prompt filtering and alignment heuristics operate at the reasoning layer.  
Risk materializes at the execution boundary.

Confidential computing ensures that data cannot be inspected.  
It does not define who is allowed to execute which operations.

Execution is the trust boundary.

## Execution Invariant

Every proposed action must satisfy three conditions before execution:

1. **Explicit Authority** — Authority must be declared and machine-verifiable.  
2. **Valid Authority** — Authority must be cryptographically or policy-valid.  
3. **Scoped Authority** — Authority must be within defined capability bounds.

If any condition fails, execution is denied.

The language model has no control over this decision path.

Authorization logic is isolated from model reasoning and evaluated deterministically.

## System Model

Aegis introduces an execution-time authorization fork:

1. The model emits a structured action proposal.
2. The proposal is intercepted before side effects occur.
3. A deterministic authority engine evaluates:
   - identity
   - capability scope
   - contextual policy constraints
4. The system returns one of:
   - allow
   - escalate
   - block

The enforcement layer is model-agnostic and compatible with TEE deployment.

## Security Position

Aegis assumes:

- Models are capable of hallucination.
- Models may emit invalid or unsafe commands.
- TEEs protect computation but do not encode authorization semantics.

Aegis does not attempt to improve model alignment.

Instead, it removes the model’s ability to self-authorize execution.

By separating reasoning from authority, prompt injection and hallucinated commands become structurally irrelevant at the execution boundary.

## Research Direction

This repository explores:

- Deterministic execution-time governance inside TEEs
- Capability-scoped authority models for AI agents
- Separation of reasoning and authorization
- Formalization of execution invariants for autonomous systems

Confidential AI requires more than data protection.

It requires enforceable authority at the moment action occurs.

