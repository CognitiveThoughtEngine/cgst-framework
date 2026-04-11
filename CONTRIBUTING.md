# Contributing to the CGST Framework

**Version:** 1.0
**Framework:** Constitutional AI Governance Stress Test

---

## Philosophy

The CGST rubric is a governance artifact, not a software module. Changes to the scoring methodology -- adding questions, changing point weights, modifying PASS/HOLD/FAIL criteria -- are governance decisions. They affect the validity of assessments that have already been conducted and the comparability of scores across time.

This repository follows the same formal amendment philosophy as the `constitutional-agent-governance` library: amendments require justification, review, and explicit maintainer ratification. Pull requests that change rubric content are not merged by a thumbs-up -- they go through an amendment review process.

---

## What You Can Contribute Without a Formal Amendment

The following contributions are welcome via standard pull request:

- **Bug fixes in YAML:** Typos, formatting errors, field naming inconsistencies in `rubric/cgst_rubric.yaml`
- **Clarifications in rubric text:** Improving the clarity of evidence descriptions or PASS/HOLD/FAIL language without changing the underlying criteria
- **New examples:** Additional self-assessment case studies following the format in `examples/constitutional_agent_2026-04-11.md` -- these enrich the framework without changing its scoring rules
- **Tooling:** Scripts, CI integrations, or parsers that consume `cgst_rubric.yaml` -- these extend utility without affecting the rubric itself
- **Translation:** The rubric in languages other than English -- translations that do not change meaning

For these contributions: open a pull request with a clear description of what changed and why. The description should be specific enough that a reviewer can verify the change does not inadvertently alter scoring criteria.

---

## What Requires a Formal Amendment

The following require a GitHub Issue before a pull request:

- Adding a new question to any layer
- Changing the point value of any existing question
- Changing the point allocation between layers (e.g., increasing WHY from 25 to 30)
- Changing PASS/HOLD/FAIL criteria in ways that would change scores for assessed systems
- Adding or removing a score band
- Changing the N/A documentation requirement
- Changing the EU AI Act article mappings
- Adding a new layer

### Amendment Process

1. **Open a GitHub Issue** titled "Amendment Proposal: [brief description]" using the template below
2. The issue is reviewed by the maintainer (Michael Saleme, Cognitive Thought Engine LLC)
3. If the proposal passes review, the maintainer will ratify it and assign an amendment number (e.g., Amendment 2)
4. The proposer then opens a pull request implementing the ratified amendment, citing the issue number
5. The pull request is merged after a final review confirming it matches the ratified proposal exactly

**Why this process?** A scoring rubric that changes without governance creates retroactive score invalidation. If a question's PASS criteria tighten after assessments have been conducted, those prior assessments become incomparable. The amendment process creates a traceable record of what the rubric said at any point in time, enabling assessments from different dates to be correctly contextualized.

---

## Amendment Issue Template

Open a GitHub Issue with the following structure:

```
Title: Amendment Proposal: [one-line description]

## What I am proposing to change
[Be specific: which layer, which question, which field, what the change is]

## Current text
[Copy the exact current text from the rubric]

## Proposed text
[The exact replacement text]

## Rationale
[Why this change improves the framework. What governance gap does it close? What
evidence from assessments or literature supports the change?]

## Impact on existing scores
[Which question(s) would change PASS/HOLD/FAIL for systems already assessed?
Would this change invalidate any published assessment results?]

## Falsification criteria
[What would prove this proposed change is wrong? Under what conditions should
this amendment be reverted?]
```

The falsification criteria field is required. Following the Section 28.8 standard of the HRAO-E constitution, an amendment proposal that cannot state what would prove it wrong is not ready for ratification.

---

## Known Planned Amendments

The following framework improvements were identified during the pilot self-assessment (2026-04-11) and are planned for a future ratified version:

**Amendment 1 -- WHO N/A pathway for governance libraries:** Add a formal `N/A (library -- WHO delegated to caller)` scoring option for governance libraries that explicitly document WHO delegation. Currently, a library correctly scores FAIL on WHO even when the design is intentional. This creates misleading risk perception for well-designed libraries.

**Amendment 2 -- I3: FRIA evidence generation:** Add a seventh question to the INTEGRITY layer: "Does the system produce structured EU AI Act Article 27 FRIA evidence programmatically?" (0-2 pts). This capability was present in constitutional-agent but not captured by the current I1/I2 questions. Adding I3 would bring the total to /102.

**Amendment 3 -- Version tracking on assessments:** Add a `rubric_version` field to the report template, making explicit which version of the rubric a given assessment used. This enables correct comparison of assessments conducted at different points in the framework's evolution.

If you are interested in contributing to any of these, open an issue referencing the planned amendment by number.

---

## Report Contributions

Completed self-assessments following the format in `examples/constitutional_agent_2026-04-11.md` are welcome as pull requests to the `examples/` directory. Requirements:

- The assessment must cite specific evidence for each PASS/HOLD/FAIL determination (not assertions)
- FAIL findings must explain the gap, not just state the score
- The assessor must be named (CTE does not publish anonymous assessments)
- The system being assessed must consent to publication if it is not the assessor's own system
- Scores must be reproducible from the evidence cited -- a reviewer should be able to verify the score from the described evidence

Self-assessments are preferred for the examples directory. Third-party assessments may be published with the assessed organization's written consent.

---

## Scope Clarification

This repository contains the open-source scoring rubric and methodology. It does not contain:

- The Tier 2 assessment methodology (internal use -- how CTE assessors conduct the 2-hour session)
- Client assessment reports (confidential to clients)
- CTE's internal lessons-learned from assessments

The rubric itself is fully open. The professional judgment applied during a Tier 2 assessment -- which evidence is credible, how to probe claims, how to score ambiguous situations -- is CTE's expertise and is not fully encodable in a rubric document.

---

## Code of Conduct

This project follows a simple standard: be honest about what evidence you have seen, do not overclaim, and do not penalize systems for governance gaps that are genuinely out of scope (with documentation). These are the same standards the framework holds for the assessors.

---

*Constitutional AI Governance Stress Test Framework v1.0*
*Cognitive Thought Engine LLC -- research@cognitivethoughtengine.com*
