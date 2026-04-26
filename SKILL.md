---
name: rpa-requirements-analyst
description: Analyze early-stage RPA automation ideas by first entering an inquiry phase, asking structured clarification questions until enough executable information exists, then turning the confirmed request into feasibility judgment, process boundaries, inputs/outputs, platform assumptions, happy path steps, exception branches, Mermaid swimlane diagrams, missing-information notes, and guidance for humans writing the final RPA requirement document. Use when users ask to assess, clarify, decompose, diagram, or prepare an RPA requirement before formal documentation. Do not guess a requirement one-liner from insufficient information, directly fill Word templates, insert screenshots, or operate business/RPA platforms.
---

# RPA Requirements Analyst

## Purpose

Help the agent turn a vague RPA idea into a structured analysis package that a human can use to write the final requirement document.

Do not promise to complete the final requirement document. Screenshots, page-element confirmation, platform-specific operations, credentials, verification codes, and real-system behavior must be confirmed by humans or external tools.

Default to inquiry before generation. When information is insufficient, ask targeted questions instead of producing a requirement definition, happy path, feasibility conclusion, or diagram.

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
2. Run the information sufficiency gate in `references/inquiry-guide.md`.
3. If the request is below the minimum executable threshold, enter inquiry mode. Ask only the next 3 to 7 high-value questions, using multiple-choice options when choices are predictable. Do not generate the default analysis package.
4. After each user answer, update the known facts, assumptions, and unresolved gaps. Continue inquiry until the minimum threshold is met or the user explicitly asks for a rough draft.
5. Only after the threshold is met, evaluate RPA feasibility using `references/feasibility-checklist.md`.
6. Extract process boundaries using `references/workflow.md`.
7. Decompose the happy path into action-oriented steps. Prefer "verb + precise qualifier" phrasing.
8. Identify exception branches, including no data, multiple data, login failure, permission failure, verification-code intervention, network/system failure, retry limit, logging, notification, and manual handling.
9. Generate a Mermaid swimlane diagram when the user asks for a diagram or when the process has multiple roles/systems. Follow `references/mermaid-swimlane-guide.md`.
10. Produce requirement-document writing guidance using `references/requirement-writing-guide.md`.
11. If a structured artifact is requested, output JSON compatible with `schemas/rpa_requirement_analysis.schema.json`.

## Inquiry Mode Output

Use this structure when information is insufficient:

1. Current understanding
2. Information sufficiency score
3. Blocking gaps
4. Questions for this round
5. What will be generated after confirmation

Do not include a requirement one-liner, feasibility conclusion, happy path, exception table, or Mermaid diagram in inquiry mode unless the user explicitly requests a rough assumption draft.

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
- Do not invent facts to satisfy the default output structure.
- Do not write a "requirement one-liner" until trigger, input, target platform, business action, output, and recipient/destination are confirmed or explicitly assumed by the user.
- If more than two core fields are unknown, stay in inquiry mode.
- Prefer one round of 3 to 7 targeted questions over a long questionnaire.
- Use multiple-choice questions when the user may not know how to phrase the answer, but include a free-text option.
- Mark each risk as `low`, `medium`, or `high`.
- When platform details are unknown, say what must be checked instead of inventing UI steps.
- For every decision branch, include both success and failure handling.
- For every output, identify where it is written, sent, stored, or displayed.
- Treat verification codes, CAPTCHAs, face recognition, and dynamic login as human-intervention or tool-risk items.
- For document-writing guidance, tell the human what screenshots and field descriptions to collect, not that the agent has collected them.

## Reference Selection

- Read `references/workflow.md` for the main RPA requirement analysis procedure.
- Read `references/inquiry-guide.md` before deciding whether to ask questions or generate analysis.
- Read `references/feasibility-checklist.md` when judging whether an automation idea is suitable for RPA.
- Read `references/mermaid-swimlane-guide.md` before generating Mermaid swimlane code.
- Read `references/requirement-writing-guide.md` before producing final writing guidance for a human document owner.
- Read `references/logistics-intercept-example.md` when an example is needed or the user asks how the method applies to a concrete case.
