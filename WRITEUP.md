## Answers of all the given 5 questions:

Design principle: AI reads, code decides, humans approve.

1. AI vs. rules

AI (two steps only):
- Extraction: turns each free-text proposal into facts, each with an exact quote, or "not stated". Proposals are written in many styles, so fixed rules cannot read them reliably.
- Rating "Team and approach" (0-5): against the admin's rubric. It is the only criterion that needs judgment.

Plain code and rules:
- PDF text extraction
- A scan for text that tries to instruct the reviewer or AI
- Checking the AI's output (format, and that each quote really exists in the source)
- Mandatory pass/fail gates, the budget ceiling and the 16-week limit
- Formulas for price, timeline, warranty and experience
- Weighted total, sorting, tie-breaks
- The reason text, built from stored evidence

Where I drew the line: AI where the input is messy language, rules where the output is a decision someone must defend. Gates are compliance decisions, so they must be identical every time. Reasons are built from what was actually scored, so they cannot say something that was not.

2. Consistency and explainability

Repeatable:
All numbers come from code using a saved copy of the criteria and weights.
The AI runs with the selected model and prompt versions.
Extraction results are stored with the file key, criteria version and prompt version. A re-run reuses them, so the same proposals give the same ranking. A fresh extraction that differs from the stored one is flagged, not silently accepted.
A fixed tie-break order: score rounded to one decimal, then experience score, then lower price, then a shared rank with a note.

Explainable:
For each proposal the reviewer sees: gate results, each criterion's raw value (for example "12 weeks"), score, weight and contribution, plus the quoted evidence. The one-line reason is generated from that breakdown so nothing is being hided.

3. Human in the loop

A person acts at five points:
1. Confirms the category and criteria version before a run.
2. Resolves every flag: clear it, ask the bidder to clarify, or disqualify. Nothing flagged is ranked automatically. In the samples this covers C (instructions aimed at the AI) and D (no completion time).
3. Reviews ineligible bids and can override, with a written reason.
4. Can correct an extracted value after seeing its quote. Scores then recalculate.
5. Makes the final award decision. The tool only suggests an order.

Audit log:
Audit logs will checks who did what and when. Criteria snapshot and weights, prompt versions and model, an ID of uploaded file, raw AI outputs, validation results, every flag and the rule that triggered it, benchmark values,  scores, the ranking, and every human action with before/after values and the reviewer's note.

4. Changing criteria

Every run is tied to a saved criteria version, so old results never change silently. If an admin edits criteria after scoring:
- The results screen shows a notice: "scored under v3, current is v4".
- Code recalculates from stored facts. No AI call is needed.
- Only that criterion is re-extracted.
- Gates re-run and statuses may change.
- Re-scoring is a reviewer action that creates a new run. The old run is saved for comparison.

The log records who changed what and when, so criteria cannot be quietly adjusted to favour a bidder after results are seen. I would also lock criteria once proposals are opened, if the client's policy allows.

5. Risks & Safeguard:

Risk: Wrong extraction
Safeguard: Every value needs a word-for-word quote, which code verifies. A failed check means one retry, then a flag. The reviewer sees quotes beside values.

Risk: Made-up facts
Safeguard: The AI may answer "not stated". Missing information is flagged and never becomes a guessed value or a silent zero (see D).

Risk: Manipulation
Safeguard: Proposal text is treated as data only. A rule scan runs before the AI and unique markers fence off the text. The AI reports instructions instead of obeying them. Code, not the AI, sets the rank. The rating step sees only validated evidence. The proposal goes to a human.

Risk: Vague promises
Safeguard: Future or unconfirmed statements are marked "conditional". For mandatory criteria, "held now" is required (see B's subcontractor).

Risk: Bias
Safeguard: Scores rest on criteria and evidence, not company size, name or location. Bidder names are not passed to the rating step. The rubric defines each score. Overrides are logged and can be reviewed.

Risk: Over-trust in the tool
Safeguard: Flagged and ineligible bids stay visible with reasons. The decision stays with a person. 

Risk: Cost
Safeguard: One extraction call per proposal and one small rating call for eligible bids. Everything else is code, and results are cached.

Risk: Confidential data
Safeguard: Proposals hold commercial information. Use a provider with no-training terms, restrict access and set a retention period.

Risk: Fake licence numbers
Safeguard: The tool checks that a licence is stated, not that it is genuine. The reviewer verifies it with the regulator. Automating that is a future improvement.

Risk: Known limitations
Safeguard: "best bid = 100" scoring means scores can shift if the bid set changes (benchmarks are logged and the run is repeatable). The Team rubric tops out at 5, so it cannot separate A and E.

## Assumptions:

- I flagged C rather than ranking it with a warning, because a person should judge an apparent manipulation attempt. Ranking it on merit with a warning would also be defensible.
