# Granularity Guide

Use this guide to avoid producing a business-level process that looks complete but is not executable by an RPA developer.

## Core Principle

An RPA process is not development-ready just because the business loop is closed. A phrase like "query the order" often contains many browser or desktop actions: open page, locate input, fill field, click button, wait for result, handle verification, read result area, judge no-result or multi-result cases, and write or send output.

Always distinguish three layers:

- Business flow: what the business wants to accomplish.
- System operation flow: which systems, pages, modules, and fields are involved.
- RPA atomic action flow: what the robot clicks, types, waits for, reads, judges, logs, and sends.

## Staged Inquiry Layers

Do not ask all questions at once. Pick the current layer and ask only the next 3 to 5 questions needed to advance.

### L1 Business Intent

Goal: confirm what should be automated.

Ask about:

- Business goal.
- Trigger.
- Input.
- Output.
- Recipient or destination.

Move on when the agent can summarize the business goal without inventing facts.

### L2 Boundary And Data

Goal: confirm process scope and data contract.

Ask about:

- Start condition and stop condition.
- Processing unit: one message, one order, one row, one file, or a batch.
- Required input fields and one masked example.
- Output fields and success definition.
- Basic no-data or invalid-data handling.

Move on when the input/output boundary is clear.

### L3 System Operation

Goal: confirm where the robot operates.

Ask about:

- Query or operation channel: API, browser page, desktop client, spreadsheet, database, or messaging platform.
- System/page/module names.
- Login, permission, VPN, verification, or CAPTCHA requirements.
- Main page path: where to enter, where to search, where to read result.
- Whether screenshots or page annotations are available.

Move on when the operation path is known at page/module level.

### L4 RPA Atomic Actions

Goal: confirm what the robot does step by step.

Ask about:

- Exact input fields, buttons, tabs, filters, and result areas.
- Wait condition after each click or submit.
- Data extraction fields.
- Judgment rules, such as unique result, no result, multiple result, timeout, or stale update.
- Retry count, log content, notification recipient, and human handoff condition.

Move on when the robot's action sequence can be written as click/type/wait/read/judge/send/log steps.

## RPA Granularity Score

Score the request from 0 to 5:

- `0`: Only the business goal is known.
- `1`: Involved systems are known, but operation path is unknown.
- `2`: Page or module level operation is known, but specific actions are missing.
- `3`: Main click, fill, read, and send actions are known, but waits, judgments, and exceptions are incomplete.
- `4`: Atomic actions, waits, judgments, outputs, and common exceptions are mostly clear; screenshots and exact selectors may still need human confirmation.
- `5`: Atomic actions, page elements, screenshots, field names, waits, exceptions, logs, notifications, and human handoff rules are all confirmed.

Use inquiry mode for scores `0` to `2`.

For score `3`, generate only a draft analysis if the information sufficiency score is at least `4`; mark page details and exception rules as pending.

For scores `4` to `5`, generate a full analysis with layered flows.

## Layered Output Rules

When generating analysis, output all three layers:

### Business Flow

Use 3 to 8 high-level business steps. Example:

- Receive logistics order number from Feishu.
- Query logistics status.
- Reply result to the original Feishu conversation.

### System Operation Flow

Use page/module-level steps. Example:

- Open the logistics query channel.
- Enter the order number in the query page.
- Submit the query.
- Read the latest logistics status area.
- Return the result to Feishu.

### RPA Atomic Action Flow

Use robot-level actions. Example:

- Open browser and navigate to the query URL.
- Wait for the query input box to appear.
- Type the order number into the query input box.
- Click the query button.
- Wait for the result area or error message.
- Judge whether a verification challenge appears.
- Judge whether the result is empty, unique, or ambiguous.
- Read the latest status text and latest update time.
- Compare the latest update time with the 24-hour threshold.
- Compose the reply text.
- Send the reply to the Feishu conversation.
- Write processing log.

## Anti-Patterns

Avoid these outputs:

- "Query order" without page, field, button, wait, and result details.
- "Process data" without field mapping.
- "Handle exception" without condition, robot action, log, notification, and handoff.
- "Reply result" without recipient, channel, and message template.
- "Open system" without login and verification assumptions.
