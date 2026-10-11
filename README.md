# Home Credit LAP Qualification - AI Voice Agent

An AI voice agent for **Home Credit** that calls existing customers about a pre-approved **Loan Against Property (LAP)** offer of up to ₹75 lakh, runs a 7-point preliminary eligibility check, and hands qualified customers to a senior loan expert.

Built for the SalesAgents AI - AI Intern (Prompt Engineer) assignment. Platform: **Retell AI** (single-prompt voice agent, English, female voice).

## Submission contents

| File | What it is |
|---|---|
| [`system_prompt.md`](system_prompt.md) | The complete system prompt (uses all required variables) |
| [`test_scenarios.md`](test_scenarios.md) | Every scenario tested, what was said, and the expected result |
| [`transcripts.md`](transcripts.md) | Transcripts of the test calls |
| [`iteration_log.md`](iteration_log.md) | Issues found in testing and the prompt fixes made |

Call recordings (audio) and Retell call logs: **[ADD YOUR GOOGLE DRIVE FOLDER LINK HERE]**
Screen recording of the test session: **[ADD YOUR GOOGLE DRIVE LINK HERE]**

## Approach

1. **Requirements to rules.** The assignment was turned into an explicit rule table (property type, ownership, documents, loan amount, occupation and income mode, market value, tenure) so nothing is left to guesswork.
2. **Silent memory.** The agent keeps 7 facts plus a callback time in an internal state, updated after every customer reply.
3. **Core logic: Extract, Validate, Update, Ask.** After each reply the agent extracts every fact given (even out of order), checks the rules, updates memory, then asks only the earliest unanswered question. This is how out-of-order answers are handled without re-asking.
4. **Separate branches** for busy customers (callback time), wrong person, existing loan or EMI reduction (loan-transfer specialist), and loan amounts above 75 lakh (explain the cap, offer 75 lakh).
5. **Safety rules.** The agent never invents interest rates, fees, branch details or a minimum market value. Product facts come only from `additional_context_from_rag`. Ambiguous answers get one clarifying question rather than an assumption.
6. **Voice rules.** Short turns, one question at a time, Indian number style (lakh and crore), strict agent gender and language, and a spoken closing line before every hang-up.

## Key design decisions

| Decision | Reason |
|---|---|
| Loan above 75 lakh is not a disqualification | The assignment says to explain the limit and offer the maximum |
| Joint ownership is never rejected | Explicitly eligible |
| No minimum market value | None is given in the assignment, so none is invented |
| Transfer overrides disqualification | Existing-loan customers belong to a different specialist flow |
| Ambiguous answer: clarify once | Avoids wrongly rejecting or wrongly accepting a customer |
| Handoff only after all 7 items | Required handoff gate |

## Test results summary

| Scenario | Result |
|---|---|
| Happy path (full handoff) | Pass |
| Joint ownership | Pass |
| Out-of-order answers | Pass |
| Agricultural property (2 calls) | Pass |
| Cash income | Pass |
| No original documents | Pass |
| Tenure too short (2 years) | Pass |
| Tenure too long (20 years) | Pass |
| Existing loan on property | Pass |
| EMI reduction | Pass |
| Busy customer, callback captured | Pass |
| Diversions (interest rate, branch) | Pass, no invented answers |
| Loan above 75 lakh, customer agrees | Fixed in v2 - see iteration log. **[UPDATE after your redo call A]** |
| Loan above 75 lakh, customer declines | **[UPDATE after your redo call B]** |

Full details: [`test_scenarios.md`](test_scenarios.md) and [`iteration_log.md`](iteration_log.md).
