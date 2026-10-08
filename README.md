# Q-RELIABLE

### Noise-Aware Reliability Engineering for Quantum Circuits

Q-RELIABLE is a Qiskit-based noise-aware quantum reliability workflow designed to evaluate how circuit complexity affects task-level fidelity and automatically determine when mitigation should be applied.

Instead of blindly applying mitigation to every circuit, Q-RELIABLE follows an engineering workflow:

**Circuit Characterization → Controlled Noise Injection → Reliability Measurement → Mitigation Decision → ZNE Mitigation → Reliability Report**

---

## 1. Problem Statement

Quantum circuits executed on noisy quantum hardware or realistic simulators can produce results that deviate from their expected outcomes.

A practical quantum software engineer therefore needs to answer:

- How sensitive is a circuit to noise?
- How does circuit complexity affect reliability?
- When should mitigation be applied?
- Does mitigation actually improve the result?
- What is the measurement overhead of mitigation?

Q-RELIABLE addresses these questions using a controlled Qiskit Aer noise model and a configurable reliability threshold.

---

## 2. Key Idea

Q-RELIABLE treats quantum error mitigation as a **reliability engineering problem** rather than simply applying mitigation blindly.

The workflow is:

```text
Input Circuit
     ↓
Circuit Analyzer
     ↓
Circuit + Noise Metrics
     ↓
Reliability Score
     ↓
Is Fidelity < Threshold?
    /              \
  No                Yes
  │                  │
  ▼                  ▼
Keep Result       Apply ZNE
  │                  │
  └────────┬─────────┘
           ▼
    Final Reliability
           │
           ▼
    Reliability Report