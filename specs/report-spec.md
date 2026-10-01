# Report spec: the master alignment report

One master report, **updated each week**, written for the person who owns messaging, positioning and go to market (at a small company often one or two people). It is a hand written document, drafted by Claude from the week's evidence and reviewed by you. Show changes as a **diff**, not a rewrite.

## Evidence rules

- **High** confidence: both readers found it.
- **Adjudicated:** one reader found it and the adjudicator accepted it.
- **Medium:** one reading, not adjudicated, or a small sample.
- Say which weeks and how many calls the evidence covers. Early weeks are **direction, not measurement**.
- Every finding carries a quote, with the call and the time.
- Out of scope topics are left out (in Victor's build, pricing).

## Structure

1. **First screen: three findings.** Each with its confidence tier. The first screen is what the owner reads if they read nothing else.
2. **Vehicles by stage and role.** Two visuals (below), and a grid of stages: calls, vehicles in use, missing or unused. Include old versions still in circulation and which roles use which assets.
3. **What is landing.** The messages said most, how many calls, who says them, what stands out.
4. **What the field says that the documents lack.** Messages said by your team (and by buyers) that no asset carries.
5. **What is not landing, and why.** Messages the assets carry that nobody says. Drift and contradiction (where a rep stretches or contradicts the document). Assets that existed and were not used.
6. **What customers are telling you.** Goals, enablement needs, feedback, feature requests, constraints, value, and renewal (the renewal question, churn mitigation, win back, and renewal reasons). A signal becomes a pattern only when it recurs.
7. **Fixes.** A table: the fix, the vehicle, the stage, the owner, the evidence, the status.
8. **Method and limits.** Weeks run, number of calls, specs and model used, what changed since last time.

## The two visuals

1. **Assets grouped by type, by buying stage.** Assets grouped as decks, one pagers, scripts and templates, blogs and guides, webinars. Each cell counts the calls where the asset was used or named, from 0 (white) to 5 or more (full green). Outline the stages the asset was written for.
2. **A week over week heat map.** The same assets by week, with a marker on the week a new asset or version shipped. A call counts for an asset when both readers find two or more of its claims (at least one carried by no other asset), or when both find someone naming it.

Draw them with a script (see `helper-scripts.md`), as SVG files, so they can sit in the report.

## Counting rules (learned the hard way)

- Count claims for **every version released by the call date**, old versions included, so a rep on a superseded deck still counts for the deck.
- **Before an asset's first release, nothing counts as use.** Mentions and requests then are **demand**, not use.
- Count only rows that **say** the claim: `missing`, `requested`, `lookalike` and bare mentions do not count as the claim being said.
- Match staff by **full name**. A buyer who shares a first name with a rep must not be counted as staff.
- Pair the two readers' labels before ranking them.

## Your turn (project owner)

After each draft, tell Claude Code:

- Which of the three first screen findings you would act on, and which are noise.
- Which fixes you would assign, and to whom.
- Which findings you do not believe, and why. These become `watch` items for next week.

You are the person who knows what a finding means for your business. The agent finds patterns; you decide which ones matter.
