# Assumptions, and how to test a model change

Two habits make this process trustworthy: **write your assumptions down**, and **set the pass bar before you test**. This page shows how, with real examples from Victor's build.

## 1. The assumptions register

For each thing you are betting on, write one row: the assumption, its status (**holding**, **broken**, **untested**), and the evidence so far. Revisit it after every week. Never delete a broken row; it is the most useful one.

Examples from Victor's build (adapt them):

| # | Assumption | Status | Evidence so far |
|---|---|---|---|
| A1 | Reps paraphrase messages more than they name assets, so matching must be by meaning | Holding | No call named an asset by title or version. Keyword hits were mostly noise |
| A2 | A claim level register lets us name the asset | Partly broken | Claims were found well. Naming the asset was weaker, because many moments had no single right asset |
| A3 | Claude reading the whole call is enough at about 10 to 12 calls a week | Holding | It beat a search shortlist at the same cost |
| A4 | Two independent readings make a usable confidence tier | Holding | Acceptance followed agreement in a repair |
| A5 | Medium effort is enough for readers | Holding, with a watch | Recall on the best measured claims stayed above 85%. Generic claim recall fell |
| A6 | The answer key is complete | Broken | Readers found many real extras the key did not list |
| A7 | Themes should anchor to the positioning document, not free clusters | Holding | It exposed themes the documents carry that positioning lacks |
| A8 | Synthetic calls behave enough like real ones | Untested | Real calls have transcription errors, crosstalk, mixed languages, wrong speaker labels |
| A9 | A small company can keep the claims table current | Untested, doubtful | Building it by hand took a day. A proposal loop is the planned answer |
| A10 | Customer signals belong in this agent | Holding | They gave some of the strongest findings |
| A11 | "Renewal" is three different conversations, and each is its own signal | Holding | The renewal question, churn mitigation and win back lead to different assets |

**Your turn.** Write your own five assumptions before your first full week. For example: "Our reps say our headline in discovery calls", "Our old deck is still in use", "Customers ask about X before they buy". Then check them against the report.

## 2. Changing the model or the effort: the method

1. **Change one thing at a time.** The model, the effort level, or a spec, never two together.
2. **Pick a test week where you already know the right answers.** Use a week you have already run, read and ruled on.
3. **Write the pass bars first.** Numbers, not feelings.
4. **List your assumptions about what will go wrong, with a tripwire for each.** The point is to look for the failure you expect.
5. **Run a small calibration** (one reader on one half of the week) before you commit to a full run.
6. **Decide with the numbers.** Pass all bars: switch. Pass some: try a hybrid (one stronger reader and one cheaper reader). Fail on recall: stay.
7. **Keep the old outputs and log the result.**

## 3. A worked example: Sonnet 5.5 at medium effort

> **Status (1 October 2026):** this plan is written and approved. The calibration **has not been run yet**. Victor will add the result to this repo.

**The question:** can the readers move from Opus 5.5 (medium) to Sonnet 5.5 (medium) to save credits? **One variable changes** (the model). The adjudicator stays on the stronger model for the test, so a weak reading cannot hide behind a weak adjudication.

**The design:** one Sonnet reader on one half of a week that has already been read and ruled on, scored against the known right answers. If it passes, run the next week with two Sonnet readers and a stronger adjudicator.

**The pass bars (set first):**

- Recall on exclusive and shared claims at or above 85% (the existing guardrail)
- Call level recall within 5 points of the stronger model on the same half
- Generic claim recall at or above 60%
- Customer signals at or above 70% of what both stronger readers agreed on, and the renewal question present on every business review
- Fewer than 2% of rows failing the format checks, and no fabricated quote

**The assumptions, with tripwires:**

| # | Assumption | What I expect | How I identify it | Tripwire |
|---|---|---|---|---|
| S1 | Recall falls on subtle claims (drifted paraphrases, buyer echoes, generic claims) | Recall of 80 to 90% on the best measured claims, generic recall lower | Score against the key and the settled truth, by claim scope and by fidelity | Recall under 85% |
| S2 | Recall decays later in long transcripts | More misses in the second half of long calls | Bucket the right answers by position in the call | Last third more than 10 points below the first |
| S3 | Fewer rows, not more | 10 to 25% fewer rows than the stronger model | Row count per call against the stronger model | Over 25% fewer |
| S4 | Two cheaper readers agree with each other more, and that proves nothing | Their misses correlate, so the adjudicator never sees them | Do not use agreement as the pass bar. The bar is recall against the truth | Agreement over 80% with recall under 85% |
| S5 | More label list slippage: new labels coined when one fits, aliases ignored | A higher rate of new labels and near twins | Count new labels and run the label review | Under half of labels match the list |
| S6 | Customer signals are the weakest part | 70 to 85% of what the stronger pair found | Compare to the union of the two stronger readers' agreed signals | Under 70%, or a renewal question row missing |
| S7 | Format and spec errors rise | A few per run | Automatic checks: CSV parses, every time exists, every quote appears in the transcript | Over 2% bad rows, or any fabricated quote |
| S8 | Scope slips more (for example a price row when pricing is out of scope) | One or two rows | Search for out of scope claims | More than 2 rows |
| S9 | Cost: tokens per half similar, price per token lower | Cheaper per run, only if S1 to S8 hold | Record tokens, minutes and adjudicator items | The adjudicator needs over 50% more items |
| S10 | "Medium" on one model is not the same effort as "medium" on another | Cannot be assumed equal | If S1 fails narrowly, try the cheaper model at high on the same half | A narrow fail on S1 only |
| S11 | New or subtle rules (for example renewal question against churn mitigation) get confused | Confusion on the newest rules | Check the exact turns where you know the answer | Any of them wrong |

**Your turn.** When you switch models, copy this table and rewrite the "what I expect" column for *your* data. The act of writing it down tells you what to look for.
