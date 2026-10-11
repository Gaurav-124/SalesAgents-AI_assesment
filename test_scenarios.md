# Test Scenarios

Every call opens the same way: the customer confirms their name, says it is a good time, and shows interest. Unless a scenario says otherwise, the customer gives these answers: residential flat, sole owner, original documents at home, around 40 lakh, salaried with salary in the bank, about 80 lakh property value, 10 years.

| # | Scenario | Customer says | Expected result |
|---|---|---|---|
| 1 | Perfect customer | Standard answers (50 lakh, 1 crore, 10 years) | All 7 asked, then senior-expert handoff |
| 2 | Out-of-order answers | "Residential house, jointly owned with my wife, worth about 1.2 crore" in one sentence | Agent asks documents next; does not re-ask type, ownership or value |
| 3 | Existing loan | "I already have a loan on this property" | Loan-transfer specialist message, call ends |
| 4 | EMI reduction | "I actually want to reduce my EMI" | Loan-transfer specialist message, call ends |
| 5 | Agricultural property | "It's agricultural land" | Polite not-eligible message, call ends, no more questions |
| 6 | Cash income | "Self-employed, income comes in cash" | Not eligible, call ends |
| 7 | No original documents | "I only have photocopies" | Not eligible, call ends |
| 8 | Tenure too short | "Two years" | Not eligible, call ends |
| 9 | Tenure too long | "Twenty years" | Not eligible, call ends |
| 10 | Loan above limit, agrees | "I need ninety lakh", then "Yes, seventy-five is fine" | Cap explained, flow continues, full handoff |
| 11 | Loan above limit, declines | "I need ninety lakh", then "No, I'm not interested" | Polite goodbye, no handoff |
| 12 | Busy customer | "I'm in a meeting, call later", then "Tomorrow around 5 PM" | No pitch, time repeated back, call ends |
| 13 | Diversions | Asks the interest rate and nearest branch mid-flow | No invented rate or branch; agent returns to the next question |
| 14 | Joint ownership | "Jointly owned with my brother" | Continues, not rejected |
| 15 | Different loan amount | "Nineteen lakh" | Accepted, full handoff |
