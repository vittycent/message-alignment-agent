# What it can and cannot do (the honest version)

Victor's rule: say these before anyone asks.

## What it can do

- **Find where your messages show up in real calls,** turn by turn, with the speaker, the time, a fidelity grade and a one line reason quoting the words.
- **Find what is said that no document covers.** This is the part you cannot get from a keyword tracker, because it needs to see the whole conversation.
- **Show drift and contradictions:** where a rep stretches a claim, or says the opposite of the document.
- **Show which vehicles are used at which buying stage,** and which messages the field says first.
- **Capture what customers tell you:** their goals, feature requests, feedback, constraints, value, renewal questions and reasons, and the signals that matter around churn and win back.
- **Rank what to review** (label review and spot check) so a human spends about an hour a week, not a day.
- **Get better each week,** because the retro turns errors into spec changes.

## What it cannot do (yet)

| Limit | What it means for you |
|---|---|
| **Tested on fictional data only.** A made up company, with calls written by Claude | Real calls have transcription errors, crosstalk, mixed languages and wrong speaker labels. Expect more noise. Nothing here has been tested on a real company's calls yet. You are an early tester |
| **The data and the answer key were written by the same Claude session that built the agent** | The fictional calls were written with realistic messiness (tangents, speaker quirks, talking speed), but some patterns were deliberately made findable, and about a quarter of the moments were kept unattributed so the gap report has a real job. What reduces the risk: the readers are fresh agents that never see the key or the build notes, the first 45 calls were written before any asset existed and never edited, and a human rules on the uncertain items. It is still a test on data that is easier to read than real calls |
| **Only 3 of 8 planned weeks run so far** | The findings in the examples are direction, not measurement |
| **It does not measure deal outcomes or win rate** | Different question, different agent. Used is not the same as works |
| **It is not a distribution tracker** | Who opened or sent a document (which Drive already tells you) is not the same as what was said on a call |
| **Pricing is out of scope in Victor's build** | Price claims and price talk are left out. You can bring them in, but it changes what the readers need to know |
| **Claims table quality decides everything** | If the claims are wrong or missing, the reader looks in the wrong place. This is the single most valuable place to spend your time |
| **No answer key for your data** | You will build a small one by hand. Without it you cannot measure recall |
| **Swedish and other languages are untested** | The embedding model is multilingual and Claude reads many languages, but Victor has not tested it on non English calls |
| **Not a packaged agent yet** | This kit is the specs and the process you use to produce your own agent and command. It takes some credits and a few sessions to build |
| **Models change the results** | A different model, or a different effort level, changes recall and agreement. Change one thing at a time |

## What is still being tested

- **Sonnet 5.5 at medium effort** against Opus 5.5 for the readers. Victor's plan is to calibrate on a week where the right answers are already known, with pass bars set in advance: recall on the best measured claims at or above 85%, generic claim recall at or above 60%, customer signals within 70% of what the stronger model found, and fewer than 2% bad rows.
- **How well it reads generic claims** (messages carried by many assets). Recall for these dipped when effort moved from high to medium.
- **Reader agreement.** Two readers agreed on 69 to 71% of pairs in the harder weeks. The adjudicator accepted most of what only one reader found, which means each reader misses real moments and the design catches them. Whether a cheaper model changes this is part of the test.
- **Whether a claims proposal loop works** (Claude proposing claims, you ruling). It is a draft in this kit and has not been run end to end.

## Numbers from the fictional data, so far

| Measure | Week 33 | Week 34 | Week 37 |
|---|---|---|---|
| Calls | 10 | 11 | 9 |
| Share of planted moments found, call level (reader 1 and reader 2) | 95% and 95% (after fixing two wrong key rows) | 86% and 81% | 96% and 96% |
| Reader agreement | 69% | 71% | 89% |
| Adjudicator: accept, event only, reject | 21, 2, 19 | 28, 2, 9 | 10, 3, 1 |
| Model and effort | Opus 5.5, high | Opus 5.5, medium | Opus 5.5, default |

These are on made up data. Use them to understand the process, not to predict your own numbers.

## Be thoughtful when you change something

If you change the model, the effort level and a spec in the same week, you will not know which one moved the numbers. The kit's habit is **one change at a time, with a pass bar written first**.
