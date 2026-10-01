# Lessons learned (what worked, what we got wrong)

Victor's honest list, from building version 2 on fictional data. Right means "the evidence still backs it", not "proven".

## What worked

| Decision | Why it looks right |
|---|---|
| **Stop after every step** | It caught a bad asset at step 3, not step 20. After a failed launch, one week at a time with a retro turned each week into a chance to improve the agent |
| **Fresh agents as readers and adjudicators** | They broke the closed loop (the agent that builds the data should not judge it), and they found things the builder would not have, such as a data error and gaps in the claims table |
| **Two readings plus an adjudicator** | Agreement predicts truth. In one repair, items found by all four runs were accepted 26 of 29 times, and items found by one run 5 of 10. It also works in production, where there is no answer key |
| **Claude reads the whole call** | It beat a search shortlist on recall with no cost penalty at about a dozen calls a week |
| **Never edit the original data** | Calibration went into new assets and new weeks, so earlier work and everything built on it stayed intact |
| **Claims as the evidence unit** | Even after the question changed, claims stayed the base. Messages and vehicles are roll ups of claims |
| **Bug triage: fix now, watch, no change** | One week of data gave 5 fixes and 6 watch items instead of 11 spec changes. Do not over rotate or under rotate on one week |
| **Check what a rebuild reproduces before changing it** | A data fix was checked against the old files first, so the diff was exactly one link |
| **Pricing out of scope** | Kept a noisy, different kind of question out of the first version. When one price quote slipped through, the adjudicator caught it |
| **Pair the two readers' labels before ranking them** | The first label review had 78 entries and the top ten were duplicates. After pairing, 48, and the top ten were real decisions |
| **Let the human rename the concept** | The owner's rulings turned one question (the renewal question) into three signals (renewal question, churn mitigation, win back). The data alone would not have done that |

## What we got wrong, and what changed

| What we thought | What happened | Lesson |
|---|---|---|
| Deal outcomes and win rate belong in this agent | Removed. Win rate by rep was tangled with segment, and the question is "used", not "succeeded" | Different questions belong in different agents |
| Message latency (release to first use) is the headline | Demoted twice, then the question itself changed | Pick the headline after seeing data, not before |
| Start from "which of my assets are used?" | Reframed to message alignment. Messages are measurable and assets often are not | Unused assets are a symptom. The cause is assets not carrying the messaging that drives value |
| The answer key is complete | Readers found 46 real extras that both agreed on | Treat any hand built key as a floor. Adjudicate before measuring |
| A first draft asset lifted rep lines to raise coverage | Rewritten in the real author's voice | Authenticity beats coverage |
| The gap score of 3 of 8 was an agent failure | It was the scoring script, which counted a call the readers never get and wanted the exact turn when gaps spread over two | **When a number looks bad, check the ruler before blaming the agent** |
| The label review tool was fine | It counted each reader's labels separately and filled the top ten with duplicates | Test a review tool on a real week before asking a human to rely on it |
| "What would keep you?" is the renewal question | The owner ruled it is churn mitigation, and a win back question after an exit is a third thing | Define a signal by the action it leads to, not by the words |
| Launch several readers in parallel | All six died at the weekly usage limit and left no output | State the agent count and a token estimate first. Start small |
| Save outputs wherever is convenient | A scratchpad folder vanished with the session, and a file had to be rewritten from memory | Outputs go in the project folder, with an exact path |
| Roles by first name | A buyer who shared a first name with a rep was counted as staff | Match staff by full name. Sanity check every roll up against the text |
| Count an asset as used before its release | A new asset was counted before it existed | A mention before release is demand, not use |
| Leave generic claims out of adjudication | A headline claim had an unconfirmed moment | Adjudicate generic claims too |
| Reader spec and adjudicator spec define a "hit" differently | The readers logged what the adjudicator was always going to reject | With agents, most "AI errors" are instruction errors. Copy a rule word for word between specs |

## Habits worth copying

- Write the pass bar **before** a test, so the result is not argued afterwards.
- Change **one thing at a time**: the model, the effort or a spec.
- Keep **old outputs** when you change something.
- Log every change with a version number and who decided.
- Cap human review at about ten items. Spend your attention on the most uncertain ones.

## What is still not solved

- A packaged one command agent, and a claims proposal loop that is tested end to end
- Whether a cheaper model reads as well as a stronger one (a calibration is planned)
- Real calls: transcription errors, crosstalk, mixed languages, wrong speaker labels
- Who keeps the claims table up to date when assets change
