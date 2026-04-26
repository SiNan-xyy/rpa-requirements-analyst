# Inquiry Guide

Use this guide before generating any requirement analysis. The agent must first decide whether the request contains enough confirmed information to produce an executable RPA analysis.

## Core Principle

Do not convert a vague idea into a confident requirement by guessing. If the user has not provided enough information, enter inquiry mode and ask targeted questions.

## Minimum Executable Threshold

Only generate the full analysis package when these core fields are known or explicitly accepted as assumptions:

- Trigger: what starts the robot.
- Input: what data the robot receives, where it comes from, and an example.
- Target platform: which system, page, file, app, API, or message channel the robot operates on.
- Business action: what the robot must actually do.
- Output: what result the robot returns, writes, sends, stores, or displays.
- Recipient/destination: where the output goes and who receives it.
- Processing unit: whether one run handles one item, one message, one file, or a batch.
- Success definition: what counts as completed successfully.
- Known failure conditions: at least the obvious no-data, duplicate-data, login/permission, and output-failure cases.

If more than two core fields are missing, do not generate a requirement one-liner, feasibility conclusion, happy path, exception table, or Mermaid diagram.

## Information Sufficiency Score

Score each request from 0 to 5:

- `0`: Only an automation topic is known.
- `1`: Goal is known, but trigger/input/output/platform are mostly unknown.
- `2`: Some core fields are known, but process boundary and output are unclear.
- `3`: Most core fields are known, but exceptions or platform constraints are unclear.
- `4`: Enough for a draft analysis with marked assumptions.
- `5`: Enough for implementation-oriented analysis and document-writing guidance.

Use inquiry mode for scores `0` to `3`. Use full analysis for scores `4` to `5`.

## Inquiry Mode Behavior

In inquiry mode:

- Summarize only confirmed facts.
- List blocking gaps.
- Ask the next 3 to 7 questions.
- Put the highest-risk question first.
- Use multiple-choice options when useful.
- Avoid asking for everything at once.
- Tell the user what will be generated after confirmation.

Do not:

- Do not write a polished requirement one-liner.
- Do not assert feasibility as suitable or high.
- Do not create a detailed happy path from assumptions.
- Do not invent API availability, message format, time rules, or exception handling.
- Do not generate Mermaid diagrams unless the user asks for a rough sketch.

## Question Types

Prefer these question categories:

1. Trigger
   - What starts the process?
   - Options: real-time message, scheduled scan, manual click, file upload, API event, other.

2. Input
   - What data does the robot receive?
   - Ask for one real or masked example.

3. Platform
   - Which systems are involved?
   - Options: browser website, desktop client, Excel/WPS file, API, Feishu/DingTalk/WeCom, internal ERP, other.

4. Action
   - What should the robot do after receiving the input?
   - Ask for the business rule, not just the system name.

5. Output
   - What should the robot return or write?
   - Options: message reply, spreadsheet row, system status update, downloaded file, log only, other.

6. Success
   - What is the exact success condition?

7. Exceptions
   - What should happen when data is not found, multiple records exist, login fails, verification appears, or output fails?

## Inquiry Output Template

```markdown
## Current Understanding

- Confirmed: ...
- Not confirmed: ...

## Information Sufficiency

Score: 2/5
Reason: ...

## Blocking Gaps

- ...

## Questions For This Round

1. ...
   - A. ...
   - B. ...
   - C. ...
   - Other: ...

## After You Confirm

I can generate: feasibility judgment, process boundary, input/output/platform table, happy path, exception branches, Mermaid swimlane code, and requirement-document writing guidance.
```
