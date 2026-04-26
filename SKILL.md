---
name: rpa-requirements-analyst
description: Analyze early-stage RPA automation ideas and turn vague business requests into structured requirement analysis, feasibility judgment, process boundaries, inputs/outputs, platform assumptions, happy path steps, exception branches, Mermaid swimlane diagrams, missing-information questions, and guidance for humans writing the final RPA requirement document. Use when users ask to assess, clarify, decompose, diagram, or prepare an RPA requirement before formal documentation. Do not use to directly fill Word templates, insert screenshots, or operate business/RPA platforms.
---

# RPA Requirements Analyst

## Purpose

Help the agent turn a vague RPA idea into a structured analysis package that a human can use to write the final requirement document.

Do not promise to complete the final requirement document. Screenshots, page-element confirmation, platform-specific operations, credentials, verification codes, and real-system behavior must be confirmed by humans or external tools.

## Operating Boundary

Perform:

- Clarify the automation target and business context.
- Judge whether the request is suitable for RPA.
- Identify start/end boundaries, triggers, and completion markers.
- Identify input data, output results, working platforms, accounts, verification, permissions, and stability risks.
- Build the happy path.
- Design exception branches and human handoff points.
- Generate Mermaid swimlane flow code when useful.
- Produce requirement-document writing guidance and known risk notes.

Do not perform:

- Do not fill `.docx` requirement templates.
- Do not insert screenshots.
- Do not claim to know exact UI elements of business systems unless the user provides screenshots or tool output.
- Do not operate Feishu, DingTalk, ERP, tax systems, Yingdao, UiBot, Power Automate, or other platforms unless the user explicitly provides tools and asks for operation.
- Do not treat the analysis as final development acceptance.

## Workflow

1. Parse the user's business description.
2. If key information is missing, ask concise clarifying questions. If enough information exists, proceed with explicit assumptions.
3. Evaluate RPA feasibility using `references/feasibility-checklist.md`.
4. Extract process boundaries using `references/workflow.md`.
5. Decompose the happy path into action-oriented steps. Prefer "verb + precise qualifier" phrasing.
6. Identify exception branches, including no data, multiple data, login failure, permission failure, verification-code intervention, network/system failure, retry limit, logging, notification, and manual handling.
7. Generate a Mermaid swimlane diagram when the user asks for a diagram or when the process has multiple roles/systems. Follow `references/mermaid-swimlane-guide.md`.
8. Produce requirement-document writing guidance using `references/requirement-writing-guide.md`.
9. If a structured artifact is requested, output JSON compatible with `schemas/rpa_requirement_analysis.schema.json`.

## Default Output

Use this structure unless the user requests another format:

1. Requirement one-liner
2. Feasibility judgment
3. Start and end boundaries
4. Inputs, outputs, and platforms
5. Happy path
6. Exception branches
7. Mermaid swimlane diagram
8. Missing information
9. Requirement document writing guidance
10. Human confirmation checklist

## Quality Rules

- Keep analysis implementation-oriented, not course-like.
- Separate facts provided by the user from assumptions.
- Mark each risk as `low`, `medium`, or `high`.
- When platform details are unknown, say what must be checked instead of inventing UI steps.
- For every decision branch, include both success and failure handling.
- For every output, identify where it is written, sent, stored, or displayed.
- Treat verification codes, CAPTCHAs, face recognition, and dynamic login as human-intervention or tool-risk items.
- For document-writing guidance, tell the human what screenshots and field descriptions to collect, not that the agent has collected them.

## Reference Selection

- Read `references/workflow.md` for the main RPA requirement analysis procedure.
- Read `references/feasibility-checklist.md` when judging whether an automation idea is suitable for RPA.
- Read `references/mermaid-swimlane-guide.md` before generating Mermaid swimlane code.
- Read `references/requirement-writing-guide.md` before producing final writing guidance for a human document owner.
- Read `references/logistics-intercept-example.md` when an example is needed or the user asks how the method applies to a concrete case.
