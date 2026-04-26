# RPA Feasibility Checklist

Judge feasibility before designing detailed steps.

## Strong Fit

An RPA request is usually suitable when:

- The process is repetitive and rule-based.
- Input and output are structured or semi-structured.
- The operation frequency or volume justifies automation.
- Systems are accessible through stable UI or API.
- The process has clear start and end points.
- Exceptions are enumerable.
- Business rules can be expressed as explicit conditions.
- Required accounts and permissions can be provided.

## Medium Fit

Use caution when:

- Some input fields are unstructured text.
- Screens change occasionally.
- Human judgment is needed for a minority of cases.
- Login includes SMS or app verification that can be handled manually at startup.
- Data volume fluctuates strongly.
- Multiple systems must stay synchronized.

Design a human-in-the-loop plan for these cases.

## Poor Fit

The request may not be suitable for RPA when:

- The decision depends on subjective human judgment.
- The system blocks automation through frequent CAPTCHA, face recognition, or device binding.
- The UI changes frequently and no API is available.
- Required data is not available in a stable source.
- The process has many unbounded exceptions.
- The platform forbids automation or violates compliance rules.
- The operation requires risky irreversible actions without review.

## Risk Categories

Classify risks as:

- `low`: Known rule, stable platform, clear data, limited exception handling.
- `medium`: Some unclear rules, multiple platforms, occasional human intervention, or moderate data-quality risk.
- `high`: Unknown UI behavior, unstable login, CAPTCHA/face recognition, unclear business rule, compliance concern, or irreversible action.

## Required Feasibility Output

Provide:

- Overall feasibility: `suitable`, `conditionally suitable`, or `not currently suitable`.
- Rationale.
- Blocking questions.
- Risks and mitigation.
- Minimum proof needed before development.

## Minimum Proof Before Development

Ask the human owner to provide or confirm:

- Example input data.
- Expected output examples.
- Screenshots of key pages.
- Account and permission availability.
- Verification-code handling method.
- Exception examples.
- Whether the target system has upcoming upgrades.
