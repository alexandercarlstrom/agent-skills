---
name: prd-creator
description: "Guide the user through creating a Product Requirements Document (PRD) for a new product or feature. Use this skill whenever the user mentions writing a PRD, product requirements, product spec, feature spec, product brief, or wants to define requirements for a new product, feature, or tool. Also trigger when the user says things like 'I have an idea for a product', 'I want to spec out a feature', 'help me think through requirements', or 'I need to write up what we're building'. Works for SaaS apps, internal tools, APIs, and integrations. The skill conducts an interactive interview to gather context, then generates a structured PRD document."
---

# PRD Creator

Create well-structured Product Requirements Documents through an interactive interview process, then generate a polished deliverable.

## How It Works

The process has two phases:

1. **Interview** — Ask targeted questions across key PRD dimensions to understand the product/feature
2. **Generate** — Produce a structured PRD document based on the answers

Do NOT try to generate the PRD immediately. The interview phase is essential — it surfaces edge cases, forces clarity, and produces a much better document than working from a vague brief.

## Phase 1: The Interview

### Getting Started

Begin by understanding the scope. Ask the user:

> What are you building? Give me the elevator pitch — a couple of sentences on what it is and who it's for.

Based on their answer, determine the **product type** to tailor follow-up questions:

- **SaaS / web application** — focus on users, workflows, integrations, billing
- **Internal tool** — focus on internal users, existing systems, data access, operational constraints
- **API / service** — focus on consumers, contracts, performance, versioning
- **Feature within an existing product** — focus on context within the larger product, migration, backward compatibility

### Interview Dimensions

Work through these dimensions conversationally. Don't dump all questions at once — group them into 2-3 per message, and adapt based on answers. Skip questions that aren't relevant to the product type.

**1. Problem & Context**
- What problem does this solve? What's the current workaround?
- Why now? What's the trigger or business driver?
- Who are the primary users/personas? Are there secondary users?
- What does success look like? How will you measure it?

**2. Scope & Requirements**
- What are the must-have features for v1? What's explicitly out of scope?
- Walk me through the core user journey or workflow — what happens step by step?
- Are there specific business rules or logic that need to be captured?
- What are the key decisions the user makes along the way?

**3. Technical Context**
- What's the existing tech stack this needs to integrate with?
- Are there any APIs, services, or data sources involved?
- Are there performance requirements (latency, throughput, data volume)?
- Any security, compliance, or data privacy considerations?

**4. Design & UX** (skip for pure APIs/backend services)
- Are there existing UI patterns or design systems to follow?
- Any reference products or inspiration for how this should feel?
- Key screens or states to account for (empty states, errors, loading)?

**5. Constraints & Risks**
- What's the timeline? Any hard deadlines?
- Who needs to be involved (stakeholders, dependencies on other teams)?
- What are the biggest risks or unknowns?
- Are there any regulatory or legal constraints?

**6. Release & Operations**
- How will this be rolled out (big bang, phased, feature flag)?
- What monitoring, alerting, or support needs exist?
- Is there a migration path from the current solution?

### Interview Tips

- If the user gives a brief, high-level answer, probe deeper: "Can you walk me through what happens when a user actually does X?"
- Reflect back your understanding before moving on: "So if I'm understanding correctly, the main flow is..."
- It's OK to suggest things: "Most products like this also need Y — should we include that?"
- When you have enough to work with (usually 4-8 exchanges), summarize what you've gathered and ask if anything is missing before generating.

### Pre-Generation Summary

Before generating, present a brief summary of what you've captured:

> Here's what I've gathered — let me know if anything is off or missing before I write it up:
>
> **Product:** [name/description]
> **Users:** [who]
> **Core problem:** [what]
> **Key features:** [list]
> **Tech context:** [stack/integrations]
> **Success metrics:** [how we'll know it works]
> **Timeline:** [if discussed]

## Phase 2: Generate the PRD

### Output Format Decision

Choose the format based on context:
- **Markdown (.md)** — default for developer-audience PRDs, internal tools, API specs, or when the user will paste it into a wiki/repo
- **Word document (.docx)** — when the user asks for it, when it's going to stakeholders/leadership, or when professional formatting matters. If generating a .docx, follow the `/mnt/skills/public/docx/SKILL.md` skill instructions for document creation.

If unsure, ask: "Should I generate this as a markdown file or a Word doc?"

### PRD Template

Use this structure. Adapt section depth based on the product's complexity — a small internal tool doesn't need the same depth as a customer-facing SaaS feature. Omit sections that aren't relevant.

```
# [Product/Feature Name] — Product Requirements Document

**Author:** [user's name if known]
**Date:** [today's date]
**Status:** Draft
**Version:** 1.0

---

## 1. Overview

### 1.1 Summary
[2-3 sentence description of what this is and why it matters]

### 1.2 Background & Motivation
[The problem, current state, and why we're building this now]

### 1.3 Goals & Success Metrics
[What success looks like, with measurable outcomes where possible]

| Metric | Target | How Measured |
|--------|--------|--------------|
| ...    | ...    | ...          |

### 1.4 Non-Goals
[What this project is explicitly NOT trying to solve]

---

## 2. Users & Personas

### 2.1 Primary Users
[Who they are, what they care about, relevant context]

### 2.2 Secondary Users
[Other stakeholders or user types affected]

---

## 3. Requirements

### 3.1 Functional Requirements

#### 3.1.1 [Feature/Capability Area]
- **FR-001:** [Requirement description]
- **FR-002:** [Requirement description]

[Repeat for each feature area. Use the FR-XXX numbering so requirements are referenceable.]

### 3.2 Non-Functional Requirements
- **NFR-001:** [Performance, security, scalability, accessibility, etc.]

### 3.3 Out of Scope
[Explicitly listed to prevent scope creep]

---

## 4. User Flows & Workflows

### 4.1 [Primary Flow Name]
[Step-by-step description of the core user journey. Use numbered steps.]

1. User does X
2. System responds with Y
3. ...

### 4.2 [Secondary Flow / Edge Cases]
[Additional flows, error handling, edge cases]

---

## 5. Technical Considerations

### 5.1 Architecture & Integration
[How this fits into the existing system, key integrations]

### 5.2 Data Model
[Key entities, relationships, storage considerations]

### 5.3 API Design
[If applicable — key endpoints, contracts, versioning]

### 5.4 Security & Compliance
[Auth, authorization, data privacy, regulatory needs]

---

## 6. Design & UX

### 6.1 Design Principles
[Guiding principles for the UI/UX]

### 6.2 Key Screens / States
[Description of main views, including empty, loading, and error states]

### 6.3 References & Inspiration
[Links or descriptions of reference products]

---

## 7. Release & Rollout

### 7.1 Rollout Strategy
[Phased, feature flag, beta, etc.]

### 7.2 Migration Plan
[If replacing an existing solution]

### 7.3 Monitoring & Support
[What to watch, alerting, support playbook]

---

## 8. Timeline & Milestones

| Milestone | Target Date | Description |
|-----------|-------------|-------------|
| ...       | ...         | ...         |

---

## 9. Open Questions & Risks

| # | Question / Risk | Owner | Status |
|---|----------------|-------|--------|
| 1 | ...            | ...   | Open   |

---

## 10. Appendix

[Glossary, reference links, related documents, diagrams]
```

### Writing Guidelines

- Write requirements as clear, testable statements: "The system shall..." or "Users can..."
- Number requirements (FR-001, NFR-001) so they can be referenced in discussions and tickets
- Be specific about behavior: "returns results within 200ms" not "should be fast"
- Include edge cases and error states — these are where PRDs earn their keep
- Use tables for structured data (metrics, timelines, risks)
- Keep the tone professional but not stiff — this document should be easy to read and act on
- If something came up as uncertain during the interview, capture it in the Open Questions section rather than guessing

### After Generation

Once the PRD is generated:
1. Save to the appropriate output format
2. Remind the user that this is a living document — suggest they review with their team and iterate
3. Offer to help refine specific sections, add user stories, create follow-up tickets, or break the PRD into implementation tasks
