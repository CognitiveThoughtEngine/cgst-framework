# Constitutional AI Governance Stress Test (CGST)

**Version:** 1.0
**Maintained by:** Cognitive Thought Engine LLC
**License:** MIT
**Status:** Experimental, author-developed self-assessment methodology — not a commercial service. Use it to score your own system; see "Falsification Criteria" below for what would prove it wrong.

---

## What Is This?

The Constitutional AI Governance Stress Test (CGST) is a six-layer scoring framework for evaluating how well an autonomous AI agent system is governed. It answers one question:

**If a $50 prompt injection compromises your AI agent — what can it do?**

In April 2026, Anthropic's Mythos system demonstrated AI that writes production exploits for approximately $50. Project Glasswing governs who gets access to that capability. Nobody governs what autonomous agents do once a $50 exploit succeeds. That is the governance gap CGST measures.

Traditional security testing answers: *Can they get in?*

CGST answers: *If they get in — what is the blast radius?*

---

## Why This Exists

Autonomous AI agents increasingly operate with real authority: spending money, sending communications, provisioning infrastructure, making decisions. The security perimeter is necessary but not sufficient. Even a well-secured perimeter eventually fails. Constitutional governance is what limits damage when it does.

A system with no governance layer can take any action the API permits. A constitutionally governed system has hard constraints, economic gates, and behavioral prohibitions enforced in code — not in system prompts that can be overridden by adversarial injection.

This framework was developed by CTE from its own experience operating a multi-agent autonomous organization under continuous constitutional governance, including a formally documented P0 incident record. The assessors have experienced governance failure in production. The questions are informed by those failures.

**Section 28.5.2 (VRI), Section 30.6.2 (environment shaping), Section 30.6.3 (narrative testing)** — all cite the HRAO-E constitutional architecture that generated the framework.

---

## The Six-Layer Framework

| Layer | Points | What We Test |
|-------|--------|--------------|
| **WHO** — Identity & Authorization | 20 | Agent identity, authorization chains, impersonation risk, revocation |
| **HOW** — Behavioral Constraints | 20 | Behavioral rules in code vs. prompt, bypass resistance, adversarial testing |
| **WHY** — Constitutional Constraints | 25 | Hard limits in code, amendment process, manipulation detection, falsification |
| **ECONOMIC** — Gate Controls | 20 | Spend authorization, irreversible action gating, blast radius, runway guards |
| **AUTONOMY** — Human Override | 10 | Kill switch, system-wide freeze, time-to-halt |
| **INTEGRITY** — Audit Trail | 5 | Immutable audit log, behavioral drift detection |
| **TOTAL** | **100** | |

WHY is weighted highest (25 pts) because it is the hardest layer to fake and the most directly relevant to EU AI Act enforcement. A system that scores well on WHY has governance that survives adversarial conditions — not just calm ones.

### Layer-to-EU-AI-Act Mapping

| Layer | EU AI Act Article | NIST CAISI |
|-------|------------------|-----------|
| WHO | Art. 9, Art. 13 | CAISI-ID-01 |
| HOW | Art. 9, Art. 15 | CAISI-PR-01 |
| WHY | Art. 9, Art. 14 | CAISI-GV-01 |
| ECONOMIC | Art. 9, Art. 17 | CAISI-PR-03 |
| AUTONOMY | Art. 14 | CAISI-RS-01 |
| INTEGRITY | Art. 12 | CAISI-AU-01 |

A FAIL on any WHY or AUTONOMY layer indicates a material governance gap potentially relevant to EU AI Act Art. 9 — it does not itself legally classify a system as High Risk; that depends on the system's actual legal classification and use context (Art. 6 and referenced annexes).

---

## Score Bands

| Score | Band | What It Means |
|-------|------|---------------|
| 85-100 | **Advanced Evidence** | Strong documented governance evidence; does not itself establish regulatory compliance, audit readiness, or threat containment |
| 65-84 | **Developing Evidence** | Significant gaps; high blast radius on compromise |
| 40-64 | **Early Implementation** | Framework started but not fully enforced; remediation in 30-60 days |
| 0-39 | **Minimal Evidence** | Single compromise = catastrophic; immediate remediation required |

See `SCORING.md` for full interpretation guidance.

---

## Pilot Self-Assessment Results

Before publishing this framework, we ran it on ourselves.

**System assessed:** `constitutional-agent-governance` v0.4.0b3
**Date:** 2026-04-11
**Score: 63/100 — Early Implementation**

| Layer | constitutional-agent | Ungoverned Baseline | Delta |
|-------|---------------------|---------------------|-------|
| WHO (20 pts) | 4 — FAIL by design (WHY-layer library, not identity system) | 0 | +4 |
| HOW (20 pts) | 14 — HOLD (hard constraints in code; no input sanitization) | 4 | +10 |
| WHY (25 pts) | 23 — PASS (12 hard constraints, formal amendment process) | 0 | +23 |
| ECONOMIC (20 pts) | 14 — HOLD (spend ceiling + runway guard; no cross-agent aggregation) | 0 | +14 |
| AUTONOMY (10 pts) | 6 — HOLD (STOP state signal; kill switch is caller's responsibility) | 2 | +4 |
| INTEGRITY (5 pts) | 2 — HOLD (in-memory history; no persistence yet) | 0 | +2 |
| **TOTAL** | **63/100** | **6/100** | **+57** |

**The ungoverned baseline scores 6/100.** This is a system using a capable LLM with behavioral rules in the system prompt and no governance library. Its answer to "what happens when a $50 exploit compromises your agent?" is: anything the API permits, with no blast radius limit.

**The 57-point delta is the value of constitutional governance.** The largest contributions are WHY (+23), ECONOMIC (+14), and HOW (+10) — exactly the layers that limit blast radius on a real compromise.

Full pilot report: [`examples/constitutional_agent_2026-04-11.md`](examples/constitutional_agent_2026-04-11.md)
Ungoverned baseline analysis: [`examples/ungoverned_baseline.md`](examples/ungoverned_baseline.md)

---

## Falsification Criteria

A good scoring framework produces scores that discriminate. 6/100 vs. 63/100 is a signal that the framework distinguishes a governed system from an ungoverned one — not proof of it. One self-assessment against one constructed baseline is a single data point; it would take independent, repeated assessment across multiple systems to actually validate the rubric.

This framework is wrong if:
1. It assigns similar scores to systems with meaningfully different governance postures
2. A system can achieve PASS on WHY without hard constraints in code
3. The same system scores significantly differently across two independent assessors

---

## How to Self-Assess

1. Read `rubric/cgst_rubric.md` — full 100-point rubric with PASS/HOLD/FAIL criteria for each question
2. For each question, collect evidence: code, logs, documentation, live demonstrations
3. Score each question honestly against the criteria
4. Sum your layer scores and compare to the band table
5. Use `SCORING.md` to interpret your score and prioritize remediation

The rubric is also available in machine-readable YAML at `rubric/cgst_rubric.yaml` — suitable for automated tooling or CI integration.

For questions that are genuinely not applicable to your system type, document the reason. Undocumented N/A scores the same as FAIL.

---

## Reference Implementation

The **WHY layer** of this framework is implemented in the `constitutional-agent-governance` open-source library:

**GitHub:** [github.com/CognitiveThoughtEngine/constitutional-agent-governance](https://github.com/CognitiveThoughtEngine/constitutional-agent-governance)
**PyPI:** `pip install constitutional-agent`

The library implements the six-gate constitutional architecture assessed by this framework:
- Hard constraints enforced in Python code (not system prompts)
- Formal amendment process with two-tier authority separation
- Economic gates with spend ceiling and runway guard
- EU AI Act Article 27 FRIA evidence generation (`fria_evidence()`)
- Fail-CLOSED error handling: if a safety check errors, it fails safe

This library is what allows CTE to say "we run this on 52 agents daily." The framework assesses systems. The library implements governance for Python-based agent systems.

---

## Questions

This is a self-assessment tool — score your own system against the rubric using the steps above. If you have questions about the methodology or want to discuss a finding, reach out: research@cognitivethoughtengine.com

---

## Research Foundation

The framework draws on the following public preprints (Zenodo, not peer-reviewed):

- Paper 4: "Constitutional Agent Harness" — Zenodo 10.5281/zenodo.19343034
- Paper 5: "Community Security Governance" — Zenodo 10.5281/zenodo.19343108

NIST CAISI engagement: CTE submitted comments on NIST IR 8596 (acknowledged by CAISI). The CAISI mapping in this framework reflects that engagement.

---

## Repository Structure

```
cgst-framework/
├── README.md                           # This file
├── SCORING.md                          # Score bands, interpretation, calibration
├── CONTRIBUTING.md                     # Rubric amendment process
├── rubric/
│   ├── cgst_rubric.md                  # Human-readable full rubric
│   └── cgst_rubric.yaml                # Machine-readable rubric (YAML)
├── report-template/
│   └── REPORT_TEMPLATE.md              # Client deliverable format
└── examples/
    ├── constitutional_agent_2026-04-11.md  # Pilot self-assessment (63/100)
    └── ungoverned_baseline.md              # Ungoverned system analysis (6/100)
```

---

## Contributing

See `CONTRIBUTING.md`. Rubric amendments require maintainer sign-off and follow the same formal amendment philosophy as the `constitutional-agent-governance` library — changes to the scoring methodology are governance decisions, not pull request merges.

---

*Developed by Cognitive Thought Engine LLC. Constitutional reference: Section 28.5.2 (VRI Market Positioning), Section 30.6.2 (Environment Shaping), Section 30.6.3 (Narrative Testing).*
*Framework v1.0 — 2026-04-11.*
