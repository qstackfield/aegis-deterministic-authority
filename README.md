# Aegis
**Deterministic Execution-Time Authority for Confidential AI Systems**

> Shape Rotator Virtual Hackathon — Track: TEE & AI-Enabled Applications  
> Challenges: NDAI Agreements · Conditional Recall

---

## The Problem

The NDAI paper (Stephenson, Miller et al., 2025) proves something important: TEEs combined with AI agents can solve Arrow's disclosure-expropriation paradox. An inventor can safely reveal their idea inside a TEE, bargain with a buyer's agent, and receive payment — all without risking theft.

But the paper explicitly acknowledges a structural gap:

> *"Recognizing that real AI agents are imperfect, we model 'agent errors' in payments or disclosures."*

Their solution to imperfect agents is budget caps and acceptance thresholds — mechanical guardrails that contain errors after they occur.

**Aegis addresses the gap before errors occur.**

The NDAI model assumes agents operate faithfully inside the TEE. It does not define who authorized the agent to act, what the agent is permitted to do, or how to prove at the moment of execution that the action was within authorized bounds.

A TEE protects data confidentiality.  
Budget caps contain overpayment errors.  
**Neither answers: was this agent authorized to execute this action?**

That is the missing governance layer. That is what Aegis provides.

---

## The Principle

> No AI agent action executes without explicit, valid, and scoped authority at the moment of execution.

This is not error tolerance. It is enforcement.

The model proposes. It does not authorize.  
Authorization is resolved deterministically, before side effects occur, by a layer the model cannot influence.

**The TEE protects the data. Aegis governs whether the agent is authorized to act on it.**

This is Zero Trust applied to AI execution:  
Never trust the agent's intent. Always verify authority at the commit point.

---

## The Execution Invariant

Every proposed agent action must satisfy three conditions before execution proceeds:

1. **Explicit Authority** — Authority must be declared and machine-verifiable.
2. **Valid Authority** — Authority must be cryptographically or policy-valid at the moment of execution.
3. **Scoped Authority** — Authority must fall within defined capability bounds for this agent, this context, this action.

If any condition fails, execution is denied.  
Not delayed. Not logged for review. Denied.

The model has no control over this decision path.

---

## How Aegis Extends NDAI

The NDAI paper establishes three key conditions for secure disclosure via TEE:

| NDAI Condition | What It Provides | What's Still Missing |
|----------------|-----------------|----------------------|
| TEE security | Data confidentiality during bargaining | Whether agent was authorized to act |
| Budget cap | Contains buyer overpayment errors | Doesn't govern action scope |
| Acceptance threshold | Seller rejects low offers | Doesn't verify agent identity or authority |

Aegis adds the enforcement layer beneath all three:

```
Seller Agent / Buyer Agent (inside TEE)
        ↓
Action Proposal (payment, disclosure, transfer)
        ↓
Aegis Authority Engine
   ├── Is this agent authorized to make this action?
   ├── Is the authority valid at this moment?
   └── Is the action within scoped capability bounds?
        ↓
Decision: allow / escalate / block
        ↓
TEE-Attested Execution (if allowed)
        ↓
Append-only Audit DAG — replayable compliance evidence
```

The NDAI paper's error robustness result holds within this framework.  
Aegis makes it structurally enforceable, not just probabilistically contained.

---

## How Aegis Extends Conditional Recall

Conditional Recall (Sun, Flashbots) solves brokered credential delegation via TEE — users can delegate access to credentials without exposing secrets.

The same gap exists: TEE protects the credential. It does not define what the delegated agent is authorized to do with it, under what conditions, or with what scope.

Aegis provides the authority layer for delegated execution:
- Identity verification at the moment of use
- Capability scope enforcement per delegation contract
- Audit DAG proving what was authorized vs. what executed

---

## Architecture

```
NDA-Protected Data / Delegated Credential (inside TEE)
        ↓
AI Agent Action Proposal
        ↓
Aegis Execution Intercept Layer
        ↓
Authority Engine (deterministic, model-agnostic)
   ├── Identity verification
   ├── Capability scope check
   ├── Policy evaluation (NDA terms / delegation contract)
   └── Contextual constraints
        ↓
Decision: allow / escalate / block
        ↓
TEE-Attested Execution (if allowed)
        ↓
Append-only Audit DAG
        ↓
Replayable Compliance Evidence
```

---

## Security Assumptions

Aegis assumes:
- Models are capable of hallucination
- Models may emit invalid, unsafe, or injected commands
- TEEs protect computation but do not encode authorization semantics
- Prompt injection and alignment failures are structural, not edge cases
- Budget caps and acceptance thresholds contain errors — they do not prevent unauthorized execution

Aegis does not attempt to improve model alignment or replace TEE security.

It removes the model's ability to self-authorize execution.  
Prompt injection and hallucinated commands become structurally irrelevant at the execution boundary — because the model never had authorization authority to begin with.

---

## Why This Matters Beyond NDAI

The NDAI paper's disclosure-expropriation framework applies across any high-stakes AI agent deployment:

- Financial transactions (payment authorization)
- IP licensing and technology transfer
- Healthcare data sharing
- Legal document execution
- Autonomous procurement and contracting

In every case, the same gap exists. TEEs protect the data. Agents handle the logic. Nobody governs whether the agent's specific action was authorized at the moment it executed.

Aegis is the governance primitive that makes TEE-resident AI agents trustworthy — not by assuming they behave correctly, but by enforcing that they can only execute what they were authorized to execute.

---

## Hackathon Deliverables

- [ ] Aegis authority engine core — deterministic allow/escalate/block evaluation
- [ ] LCAC policy layer — capability-scoped context access control
- [ ] TEE integration — execution intercept inside confidential compute boundary
- [ ] NDAI demo — seller and buyer agents attempting authorized and unauthorized disclosure/payment actions, with full enforcement and audit trail
- [ ] Conditional Recall demo — delegated credential access with scoped authority enforcement

---

## Production Validation

The Authority-Before-Execution framework underlying Aegis has been running in production for one year inside VANTA OS — an autonomous capital intelligence system operating across equity, options, and cryptocurrency markets.

Key production metrics:
- 100% pre-execution authority resolution
- 28–43ms governance overhead
- Shadow governance catching behavioral drift before live execution
- Kill switch verified across all execution paths
- 100% audit DAG completeness

Capital markets represent the highest-stakes proving ground for AI governance. The framework works at production scale.

---

## Research Foundation

- Stephenson, Miller, Sun et al. (2025). NDAI: AI Agents and TEEs as Ironclad NDAs. arXiv:2502.07924
- Sun, Flashbots (2025). Conditional Recall: Brokered Credential Delegation via TEE.
- Stackfield, Q. (2026). Authority-Before-Execution: A Pre-Authorization Architecture for Enterprise AI Governance. DOI: 10.13140/RG.2.2.33692.76163
- Stackfield, Q. (2026). Never Trust, Always Govern: The Zero Trust Parallel for Enterprise AI Governance. DOI: 10.13140/RG.2.2.14199.07843
- Saltzer & Schroeder (1975). The Protection of Information in Computer Systems.
- NIST SP 800-207. Zero Trust Architecture.
- Patent Pending: Pre-Execution AI Governance Systems (US 63/958,209)

---

*Atom Labs | Quinton Stackfield | ORCID: 0009-0002-7377-4165*  
*github.com/qstackfield | researchgate.net/profile/Quinton-Stackfield*
