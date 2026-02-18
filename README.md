# Aegis

Deterministic execution-time authority for confidential AI systems.

---

Most AI safety work focuses on prompts.

That’s the wrong layer.

The real risk starts when an AI-generated action leaves the model and touches the outside world. An API call, a transaction, a robot instruction, a secret retrieval.

That’s where execution happens.
That’s where damage happens.

Aegis enforces a simple invariant:

No action executes without explicit, scoped, and valid authority at the moment of execution.

The model can plan.
It cannot approve itself.

---

## What This Is

A deterministic authority engine designed to run inside a Trusted Execution Environment (TEE).

It intercepts structured actions proposed by an AI system and evaluates them against hard authority rules before anything executes.

The decision is binary and verifiable:
- Allow
- Escalate
- Block

If it’s not explicitly authorized, it does not run.

No prompt filtering.
No heuristic alignment tricks.
No trusting the model to behave.

---

## Why a TEE

Authority enforcement must be isolated from model reasoning.

Running arbitration inside a TEE gives us:

- Tamper resistance
- Cryptographic attestation
- Secret protection
- Deterministic policy enforcement

The model cannot override the enclave.
The host cannot forge a decision.
Execution requires a valid signed result.

---

## Core Idea

Separate reasoning from authorization.

AI systems are probabilistic.
Authority decisions should not be.

Aegis makes execution a deterministic boundary.

---

## Status

Research prototype focused on:
- Structured action interception
- Enclave-based authority evaluation
- Signed execution gating
- Verifiable decision flow

---

Safe autonomy requires governance at execution time.

That is the layer Aegis enforces.