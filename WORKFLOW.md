# WORKFLOW.md — AI-Assisted Workflow Drill

## Feature
Email validation on a signup form (`index.html`), built twice using two 
different prompting approaches on separate branches.

## Round 1 — Vague Prompt
**Prompt:** "Add email validation to this form"

**What was built:** The AI added only the `required` attribute to the email 
input. This relies entirely on the browser's default HTML5 validation, which 
just blocks empty submissions — it does not check whether the value is 
actually a valid email format (e.g. "test" or "test@test" would still be 
rejected by the browser natively, but there's no custom error message, no 
styling, and no control over the validation logic at all).

**Issues:**
- No real format checking beyond what the browser does by default
- No custom inline error message — just the browser's native tooltip
- No control over edge cases (e.g. "test@test" without a domain extension)
- Not testable or extendable — validation logic doesn't actually exist in code

## Round 2 — Precise Prompt
**Prompt:** Specified the exact field IDs, required a custom regex-based email 
format check, a required inline red error message below the field, a specific 
"Email is required" message for empty submission, submission blocking on 
invalid input, plain JavaScript only, and asked the AI to self-test against 
four specific cases (empty, "test", "test@test", "test@test.com") before 
returning the result.

**What was built:** Actual JavaScript validation logic with a regex check, 
custom error messages rendered inline below the field, and submission 
properly blocked on invalid input. All four test cases passed on the first 
attempt — no fixes were needed.

## Key diff
Round 1 has zero custom validation logic — it's a single HTML attribute. 
Round 2 added a JavaScript function that checks the email pattern, inserts/ 
removes an error `<span>`, and calls `preventDefault()` on invalid submit. 
This is the core difference: Round 1 outsources correctness to the browser 
and gets it wrong; Round 2 defines correctness explicitly and verifies it.

## AI mistake caught
In Round 1, the AI presented `required` as if it were "email validation," 
which is misleading — it validates presence, not format. Without specifying 
what "validation" actually meant, the AI picked the minimum-effort 
interpretation.

## Lesson
Round 2 took longer to prompt (writing out constraints and test cases), but 
needed zero review/fix time since it was self-tested. Round 1 was fast to 
prompt but produced something that looked done while not actually solving 
the problem — the vagueness let the AI silently substitute a much weaker 
solution.
