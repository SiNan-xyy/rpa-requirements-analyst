# Requirement Document Writing Guide

This skill does not fill the final Word requirement document. Generate writing guidance that helps a human complete it.

## Suggested Document Sections

### Process Basic Information

Tell the human to fill:

- Process name.
- Owning department.
- Business scenario description.
- Single operation time.
- Daily/monthly volume.
- Trigger method.
- Notes and assumptions.

### Application Systems

Tell the human to list each platform:

- System name.
- Type: browser website, desktop client, Excel/WPS/Office, API, database, RPA platform, messaging app.
- Account/password requirement.
- Verification type: SMS, CAPTCHA, app approval, face recognition, none.
- Upgrade plan or known instability.
- Permission owner and access path.

### Detailed Steps

For each happy-path and exception step, tell the human to provide:

- Step number.
- Step name.
- Screenshot.
- Exact page/field/button name.
- Data source.
- Operation rule.
- Expected result.
- Failure behavior.
- Notes for developers.

Use "action + precise qualifier":

- "Click the logistics interception navigation button."
- "Enter the Feishu logistics number into the interception input field."
- "Send the interception result to the Feishu robot conversation."

### Data Transmission

Tell the human to specify:

- Runtime inputs.
- Runtime outputs.
- File paths or message sources.
- Field mapping.
- Success output.
- Failure output.
- Log and notification destination.

### Exception Handling

Tell the human to write explicit handling for:

- No matching data.
- Multiple matching records.
- Login expired.
- Verification code appears.
- Permission denied.
- Page timeout.
- Required field missing.
- Output write/send failure.
- Retry limit reached.

For each exception, specify:

- Condition.
- Robot action.
- Log content.
- Notification recipient.
- Whether human intervention is required.

## Human Confirmation Checklist

Before the requirement document is considered ready for RPA development, the human owner should confirm:

- Key screenshots are complete and readable.
- Page elements are named consistently.
- Test data examples are provided.
- Accounts and permissions are available.
- Verification-code handling is agreed.
- Every decision branch has success and failure handling.
- Output location and notification recipient are explicit.
- Development scope exclusions are written down.
