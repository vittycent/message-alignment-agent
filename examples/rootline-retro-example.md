# W34 retro (1 Oct 2026, reader spec v1.4, adjudicator v1.2, all agents on Opus 5.5 medium)

## What ran

| Step | Result | Cost |
|---|---|---|
| Readers A1 and A2, two halves each | A1 328 rows, A2 329 rows, all 11 calls | about 795k tokens in total with the adjudicator (estimate was 1.1 to 1.4M) |
| Check (no agents) | Call level claim recall 86% (A1) and 81% (A2). Exclusive and shared recall 93% and 90%. Same (turn, claim) pairs in both readers: 125 of 205 = 61%; reader agreement at call level 71% | none |
| Adjudicator | 39 items: 28 accept, 2 event only, 9 reject, 0 unsure | inside the total above |
| **Week total** | **W34 = pairs both readers found + 28 adjudicated accepts + 2 event only** | |

Low precision against the key (28 and 29%) is the key again: it holds the documented moments only, and 52 and 55 call level extras are mostly real.

## Medium effort guardrail (D-52)

Exclusive and shared recall 93% and 90%, above the 85% floor. **Medium stays.** W33 under the corrected key was 97% for both, so there is a small drop. Spec changes (F1 in W33) and effort changed together, so the drop cannot be pinned on effort alone.

## What moved since W33

| Measure | W33 | W34 | Read |
|---|---|---|---|
| Adjudicator rejects | 18 of 42 (43%) | 9 of 39 (23%) | F1 (generic claim rule in the reader spec) worked: far fewer topic only claims |
| Reader agreement | 69% | 71% | Barely moved |
| Generic claim recall | not tracked | 67% and 58% | Both readers miss the same ones |
| Gap and field born score | 4 of 4 | 3 of 8 (scorer) | See F6: scorer artefact, now 7 of 7 |
| Distinct labels | 22 vs 33 between readers | 69 label groups after pairing, 21 matched the list | The list covered under a third of what W34 said; most new labels were W34's new call types (discovery, exit) |

## Findings, tagged (D-49)

### Fix now (applied 1 Oct, proposed as diffs, logged D-59)

| # | Finding | Evidence | Change made | Check in W35 |
|---|---|---|---|---|
| F1 | No event for a gap spoken by a Rootline rep | A2 H2 note 1; the event list has no gap event, and `field born` already covers "never carried by any asset" | Reader spec v1.5: a rep spoken gap is `field born` with the gap label, fidelity `n/a` | Both readers code it the same way |
| F2 | Paraphrased or win back renewal question: spec silent | Both readers counted Karin's "would you talk to us in a year?" (Aalborg) as asked, and "what would keep you?" (Bergstrand) as `asked, unclear`; the adjudicator rejected C106 `drifted` for the Bergstrand question | Reader spec v1.5: win back and "what would keep you?" count as asked; C106 is only the would you renew today check, so no C106 `drifted` for them | No C106 `drifted` rows on renewal conditions questions |
| F3 | May a gap row reuse a label listed under another type | A2 H1 note 1 reused "export in a customer's format" (a feature request) on a gap row; the review script then counted it as new | Reader spec v1.5: yes, any label whose meaning fits. `label_review.py` checks across types for gap rows | Fewer false "new" labels |
| F4 | Renewal reason prefixes had no place for "still here but no value" | Aalborg left, but A1 wrote `not renew: no ongoing use` because `unsure:` did not fit; your ruling on #8 | `at risk:` added as a fourth prefix | Prefix use is consistent |
| F5 | Reader aliases (your request for W35) | The two readers wrote near twin labels for the same turn (for example "suppliers refuse to share" and "suppliers refuse to share data") | `labels.csv` has an `also_called` column; the reader spec says to write the main label, never the old name; `label_review.py` treats aliases as known. Aliases cover your rulings on #6 to #10 and the both reader items below | Distinct labels per week fall |
| F6 | Adjudicator filled the asset on `field born` rows | Adjudicator note 1: it filled TPL 1.1, SCRIPT 2.0 and WHN; the reader spec (F4 in W33) leaves them empty | Adjudicator spec v1.3: same rule as the readers | Field born rows with an asset filled are 0 |
| F7 | **Tool, not spec:** the gap score of 3 of 8 | One key row sits in an internal call the readers never get; two rows were found one or two turns away from the key turn | `score_run.py`: internal calls not scored for gaps; a gap counts within 2 turns. W34 is now 7 of 7 for both readers; W33 unchanged at 4 of 4 | none needed |

### Needs your call (these change what a metric means, or touch your data)

| # | Question | My recommendation |
|---|---|---|
| C1 | **W1, reader agreement is 71%, still under the 80% bar we set.** The cause is not the spec: the adjudicator accepted 28 of 39 one reader items, so most disagreements are real moments one reader missed (my inference). Options: (a) keep medium and let the second reader plus the adjudicator catch them, (b) go back to high effort for readers | (a). The guardrail passes, medium saves credits, and the two reader design is doing its job. Revisit if W35 recall falls under 85% |
| C2 | F2 makes "what would keep you?" count as a renewal question asked. Both readers already did this, but it feeds your "renewal question asked or not" insight | Keep, because the question asks about staying. Tell me if you want only a direct would you renew question to count |
| C3 | Some merges may be too loose: "lost trust in the numbers" took in two unit conversion labels; "file drop for disconnected entities" took in "unsourced customer stat" (a proof number, not a file feature) | Splitting "unsourced customer stat" back out is the one I would do |
| C4 | #4 "replace an unexplained estimate": your answer described a request arriving by email or phone, which does not obviously match | Tell me what you meant and I will fix the means line |

### Watch (one or two more weeks)

| # | Finding | Why not fix yet | Promote if |
|---|---|---|---|
| W1 | Reader agreement 71% | See C1 | W35 is under 80% again and recall is under 85% |
| W2 | `missing` rules: the C103 and C104 `missing` items both came back `event only`; C106 `missing` at Nordkost was agreed by both readers | No disagreement this week | Readers disagree on a `missing` row |
| W4 | `lookalike` for the adjudicator: it accepted one this week (item 16, with an asset filled), after rejecting all four in W33 | One item | It decides another and gives a different answer |
| W5 | Generic recall 67% and 58%, both readers missing the same ones | F1 and effort changed together, cannot separate | Still under 70% in W35 |
| W6 | `missing` against "no turn twice" | Not in the W34 reader notes | Recurs |
| N1 | One pricing leak: a reader logged C89 `contradicted` on the price quote ("eighteen thousand euros a year"); the adjudicator rejected it as pricing | One row, caught downstream | A second row, then add a check to `scope.py` |
| N2 | Nearby idea rejects on exclusive claims: 6 of the 9 rejects (C97, C18, C81, C11, C62, C88) | Already down from 43% to 23% | Rejects go back over 30% |
| N3 | Borderline adjudicator accepts: buyers using a claim as a yardstick on a competitor (items 18, 21, 35) and one turn carrying one item of a list claim (items 8, 28) | The adjudicator was consistent: accepted as buyer echo or drifted | You disagree in the spot check |
| N4 | Possible claim link gaps in `share/`: QBR S04 carries a coverage line near C54 but is linked only to BLOG-2; Sales Engineer days in OP-PKG H3 for C124 are linked only to WHN | Two cases, and it touches your data | Same asset section used with no claim again |

### No change

- Kärnhuset repeats timestamps (00:18:36 and 00:19:33 or 00:19:40 for different speakers). W33 to W36 files are never edited. Both readers used time plus speaker.
- A2 H1 note 3 (a claim carried only by two superseded versions): the existing rule already answers it, leave `asset_id` empty and say so in `reason`.
- Low precision against the key: the key is incomplete by design (D-39).

## Labels (label review plus retro)

- Your rulings on the top 10 are in (D-58). Items 44 to 46 (renewal question `not asked`, `asked, unclear`, `asked, clear no`) are added with `asked, clear yes`, so all four are on the list.
- Both reader items (25 to 43 and 47 in the first review) are added as labels, each with the other reader's wording as an alias. Where both readers described the same moment in different words, the main label is the more general one.
- "Navigation too complex for occasional users" and "not built for occasional users" are one label with an alias.
- One reader only items (about 14) stay off the list this week. If a second reader or a second call uses one, it comes in. `label-review-W34.md` now shows the 18 that are still open.
- The list is now 73 labels.

## Model and effort

Keep Opus 5.5 medium for W35. The one risk to watch is generic recall (W5), because the fix and the effort change landed together.

## Next

Spot check for you (about 10 adjudicated items), then the master report update, then the journal entry. W35 only after that, and only on your go.

## Update after Victor's rulings (1 Oct 2026)

- **C2 is reversed.** He ruled that "what would keep you?" is churn mitigation, not a renewal question (spot check S7). Reader spec v1.6 adds a `churn mitigation` signal; F2 above is superseded for that case. Win back questions after an exit still count as a renewal question asked (open, not yet ruled).
- C1 (keep medium), C3 (split the stat label) and C4 (product gap meaning) were answered as proposed.
- Spot check: S1 to S5, S9, S10 agreed, S6 unanswered, S8 comment read as about S7. All 39 adjudicator decisions stand. Details in `spot-check-W34-rulings.md`.
- Label review items 1 to 18 approved; `labels.csv` has 87 labels.
