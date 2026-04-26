# RPA Requirement Analysis Workflow

Use this workflow to transform vague business experience into logic that RPA developers can discuss and implement.

## 1. Define The Request

Create a one-sentence definition:

`When [trigger], the robot should use [input] on [platform/system] to complete [business action], then produce [output/result].`

Keep the sentence concrete. Avoid phrases like "process data", "handle exceptions", or "sync information" without specifying which data, which exception, and which target.

## 2. Find Start And End Boundaries

Clarify:

- Start trigger: scheduled time, received message, uploaded file, manual click, API event, queue item, or batch list.
- Start condition: what exact data or signal must exist before the robot starts.
- End marker: what proves the robot has finished.
- Stop condition: no remaining tasks, result sent, table updated, file archived, or human handoff created.

If the boundary is unclear, ask:

- What tells the robot to start?
- What tells the robot to stop?
- What should happen if there is nothing to process?
- Does one run process one item or many items?

## 3. Identify Inputs, Outputs, And Platforms

For every process, list:

- Input data: source, format, required fields, optional fields, examples, and validation rules.
- Output result: destination, format, success/failure message, logs, files, database rows, notifications, and reports.
- Platforms: browser websites, desktop clients, Excel/WPS/Office files, APIs, RPA platform, internal systems, messaging platforms.
- Access needs: account/password, MFA, CAPTCHA, SMS code, mobile approval, permissions, VPN, IP whitelist.
- Stability factors: planned upgrades, UI changes, slow pages, rate limits, data volume, locked files, concurrent users.

## 4. Build The Happy Path

The happy path assumes:

- Input is complete and valid.
- Network and system are available.
- Login state is normal.
- Data can be found.
- No permission, verification, or business-rule exception occurs.

Write 5 to 15 action steps. Use "verb + precise qualifier" phrasing:

- Good: "Read the logistics order number from the Feishu robot message."
- Good: "Enter the order number into the logistics interception search box."
- Weak: "Process the order."

Skip retries and exception branches in the happy path, but do not ignore them; capture them in the exception section.

## 5. Add Decision Branches

For each branch, define:

- Decision condition.
- Success path.
- Failure path.
- Retry count, if applicable.
- Log content.
- Notification recipient and message.
- Manual handoff condition.

Common RPA branches:

- Login required or already logged in.
- Verification code or CAPTCHA appears.
- Target data exists once, does not exist, or appears multiple times.
- Required field is missing.
- Platform timeout or page load failure.
- Permission denied.
- Business rule blocks operation.
- Output write fails.

## 6. Prepare Human Document Guidance

Do not fill the final requirement document automatically. Instead, produce guidance that tells the document owner:

- Which screenshots are needed.
- Which page elements require naming and annotation.
- Which accounts, permissions, and verification methods must be confirmed.
- Which fields and business rules must be listed.
- Which exception branches need explicit handling.
- Which outputs and notifications must be specified.

## 7. Suggested Final Analysis Shape

Return:

- Requirement one-liner.
- Feasibility judgment.
- Process boundary.
- Inputs/outputs/platforms table.
- Happy path.
- Exception branches.
- Mermaid swimlane code.
- Missing information.
- Requirement document writing guidance.
- Human confirmation checklist.
