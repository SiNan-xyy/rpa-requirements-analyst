# Source Confidence Guide

Use this guide to prevent detailed but guessed RPA steps from being presented as development-ready facts.

## Core Principle

Fine-grained steps are dangerous when their source is unclear. A coarse guess is easy to spot; a detailed guess can look true and mislead RPA development.

Every step in business flow, system operation flow, and RPA atomic action flow must include a source status.

## Source Status Values

- `confirmed_by_user`: The user explicitly provided this fact in the conversation.
- `confirmed_by_artifact`: The fact comes from an artifact the agent inspected, such as a screenshot, requirement document, webpage observation, API documentation, exported log, or template.
- `inferred`: The agent inferred this from context or common patterns. It may be useful as a candidate path, but it is not confirmed.
- `needs_confirmation`: The step cannot be trusted until the user provides confirmation, screenshot, document, page observation, or tool output.

## Hard Rules

- Do not mark UI actions as `confirmed_by_user` unless the user explicitly described the page, field, button, module, or navigation path.
- Do not mark UI actions as `confirmed_by_artifact` unless an artifact proves the page, field, button, module, or navigation path.
- Do not place `inferred` or `needs_confirmation` UI actions in a development-ready RPA atomic action flow.
- Put guessed UI actions in a "candidate operation paths" section.
- Convert guessed UI actions into the next inquiry questions.
- If a system operation says "enter query page", confirm how to enter it: direct URL, homepage entry, menu path, workbench module, popup, tab, or embedded search box.
- If a step says "click query", confirm the button name, page state before click, expected page state after click, and wait condition.
- If a step says "read result", confirm the result field, result region, no-result message, loading behavior, and error message.

## UI Action Confirmation Gate

For browser and desktop-client work, these action types require source confirmation:

- Open a specific URL or system.
- Navigate from one page/module to another.
- Click a menu, button, tab, link, or icon.
- Fill an input box, filter, dropdown, or form field.
- Wait for page load, popup, table, toast, file download, or result region.
- Read a status, time, amount, table row, error message, or notification.
- Judge no result, multiple results, verification challenge, timeout, or permission failure.

If any of these are not confirmed, label them as `needs_confirmation` or `inferred`, then ask a question.

## Candidate Operation Path

When a likely path exists but is not confirmed, write it as:

```markdown
Candidate path: From the homepage, enter the waybill query page.
Source status: inferred
Cannot be used as development-ready step.
Questions:
- Is the query entry on the homepage, a logged-in workbench, a direct URL, or another page?
- What is the exact menu/button name?
- After clicking, does it navigate to a new page, open a popup, or expand a search area on the same page?
- Can you provide a screenshot of the entry and query page?
```

## Development-Ready Atomic Action Rule

An RPA atomic action can be considered development-ready only when:

- `source_status` is `confirmed_by_user` or `confirmed_by_artifact`.
- The action uses a clear verb: open, click, type, select, wait, read, judge, send, write, log, notify, or handoff.
- The target is specific enough: page, field, button, result area, message window, file, API endpoint, or table.
- The expected result or wait condition is known.
- Failure handling is defined or listed as a blocking gap.

## Inquiry Prompts For Unconfirmed Navigation

When the path between pages is unknown, ask:

1. How does the robot reach the target page?
   - A. Direct URL
   - B. Homepage menu/button
   - C. Logged-in workbench/module
   - D. Search box on current page
   - Other: provide the path

2. What is the exact entry name?
   - A. Query
   - B. Waybill tracking
   - C. Order search
   - D. Unknown; needs screenshot confirmation
   - Other: provide the label

3. What happens after clicking the entry?
   - A. New page opens
   - B. Same page expands a query area
   - C. Popup/modal opens
   - D. Unknown

4. Can you provide screenshots for the entry page and result page?
