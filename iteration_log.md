# Iteration Log - Issues Found in Testing and Fixes

## v1 test findings

| # | Issue | Evidence | Fix in v2 |
|---|---|---|---|
| 1 | The call ended without the handoff message | In the over-limit call (customer asked for 90 lakh, agreed to 75 lakh, then gave all answers), `end_call` fired right after "Ten years" and the senior-expert handoff was never spoken | Added to `# CALL TERMINATION`: speak the full closing line first, then call `end_call`; never end the call straight after the customer's answer |
| 2 | The agent did not always hang up by itself | Some call logs show the customer hanging up instead of the agent | Same fix, plus an explicit rule not to wait for the customer to hang up |
| 3 | Offer sounded unsure | In two calls the agent said "you may have a pre-approved offer" | STEP 3 now says to state the offer with confidence and never say "may have" |
| 4 | Numbers without units caused extra questions | In the out-of-order call, "one point two" led to a repeated question about the unit | Added a rule to infer lakh or crore from context when obvious |

## What worked well in v1

- The agent never re-asked a question the customer had already answered.
- It never invented an interest rate or a branch address; it deferred to the senior loan expert and returned to the checklist.
- Every disqualifier (agricultural, cash income, missing original documents, tenure outside 3 to 15 years) stopped the flow immediately and politely.
- Existing-loan and EMI-reduction cases went straight to the transfer message.
- Busy customers were not pitched to; the callback time was repeated back.

## Notes on transcripts

Speech-to-text sometimes mishears the caller (for example "residence lounge" for "residential house"). The agent handled this by asking a short clarifying question rather than guessing, which is the intended behaviour.
