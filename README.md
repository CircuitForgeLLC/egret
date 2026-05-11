# Egret — Privacy Rights & Data Request Management

> *Part of the Circuit Forge LLC "AI for the tasks you hate most" suite.*

**Status:** Backlog — not yet started. Peregrine must prove the model first.

## What it does

Egret manages your privacy rights across companies worldwide: submitting Data Subject Access Requests (DSARs), Right to Erasure requests, data portability requests, opt-out-of-sale notices, and escalating to regulatory bodies when companies stonewall or miss their legal deadlines.

The name is intentional: *egret* sounds like *egress* — data flowing out of companies' systems and back under your control. Egrets are patient, methodical, and precise. White, clean. That's the goal.

## Legal frameworks supported

| Regulation | Region | Key rights |
|---|---|---|
| GDPR | EU / EEA | Access, erasure, portability, rectification, restrict processing |
| CCPA / CPRA | California, USA | Know, delete, opt-out of sale/sharing, correct, limit sensitive use |
| PIPEDA | Canada | Access, correction, withdrawal of consent |
| LGPD | Brazil | Access, deletion, portability, correction, anonymization |
| PDPA | Thailand / Singapore | Access, correction, deletion, portability |
| UK GDPR | United Kingdom | Post-Brexit GDPR equivalent |
| State privacy laws | USA (VA, CO, CT, TX, OR, MT, +) | Access, deletion, opt-out (varies by state) |
| APPI | Japan | Disclosure, correction, use limitation |

## Why it's hard

Privacy rights exist on paper but are designed to be abandoned:
- Companies have no incentive to make DSAR submission easy — most bury the form or require accounts
- Legal deadlines are short but enforcement is weak for individuals (30 days GDPR, 45 days CCPA)
- Responses are often partial, evasive, or in formats designed to be unreadable
- Escalation paths (DPAs, state AGs, FTC) require formal complaints with specific formats
- Identity verification requirements vary and are sometimes used as gatekeeping

## Core pipeline

```
Inventory data exposures (companies with your data + what category)
→ Generate tailored DSAR / erasure / opt-out letter per company
→ Submit via verified channel (email / web form / certified mail)
→ Track deadline (GDPR: 30 days; CCPA: 45 days; grace periods)
→ Monitor for response → Review compliance of response
→ If non-compliant / no response: draft DPA / state AG complaint
→ Track escalation status
```

## Key differentiators vs. other products

- Multi-jurisdiction: the correct legal framing, citation, and deadline vary by company location AND your location
- Identity verification workflow: guide user through what to submit (and what NOT to overshare)
- Partial response detection: AI reviews company response for completeness vs. legal requirements
- Escalation chain: ICO → CNIL → Datatilsynet → state AG → FTC → small claims, based on jurisdiction and response

## Response handling

When a company responds, Egret:
1. Parses the response (email / PDF / portal export)
2. Checks against your original request — what was addressed, what was dodged
3. Flags if the response doesn't meet legal minimums
4. Drafts a follow-up or escalation letter as needed

## Company database

A structured, community-maintained database of:
- DSAR submission endpoints (email, web form URL, or postal address) per company
- Average response time (crowdsourced)
- Compliance rating (historically responsive / stonewalls / partial)
- Required identity verification documents

MIT-licensed, like the job board scrapers in Peregrine — the community maintains it because company policies change constantly.

## Product code (license key)

`CFG-EGRT-XXXX-XXXX-XXXX`

## Tech notes

- Shared `circuitforge-core` scaffold
- Jurisdiction detection: user location + company HQ → applicable law
- Letter template library: per-regulation, per-right, per-escalation-level
- Email sync: monitor company responses, flag when deadline approaches
- Response analysis: LLM review of company responses against legal checklists
- Vision module: scan physical mail responses, PDF exports from companies
- ⚠️ Sensitive data handling: DSAR responses may include PII — local-only processing, never routed through cloud LLM without explicit consent
