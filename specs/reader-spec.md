# Reader spec: messaging in sales and customer success calls

Version 1.0 of the starter kit (based on Victor's reader spec v1.7). Replace every `{{...}}` with your own details. Version this file when you change it, and keep old versions in `specs/history/`.

## The job

{{COMPANY}} ({{ONE_LINE_ABOUT_THE_COMPANY}}) has a set of marketing and sales enablement assets: {{ASSET_TYPES}}. The marketing lead wants to know **which assets are being used in sales and customer success conversations, and what is being said that no asset covers.**

You read call transcripts and do two jobs:

1. **Messaging:** report every moment where asset messaging shows up, and every moment of messaging no asset covers.
2. **Customer signals:** report what customers tell {{COMPANY}} about their goals, needs, renewal and problems (see "Customer signals").

If your task says **signals only**, do job 2 and skip job 1.

**Out of scope (decide yours):** {{OUT_OF_SCOPE}}. In Victor's build, pricing is out of scope: skip price claims and any talk about prices, quotes, discounts or budgets. What a package contains is not pricing and stays in. Change this to fit your company, and say why in the decisions log.

## What you may read

Base folder: `{{PROJECT}}/readable/`

- `register/` files: `asset-register.csv`, `asset-sections.csv`, `claims.csv`, `claim-links.csv`
- `assets/` (the asset files)
- The call transcripts listed in your task, and only those, under `calls/`
- This spec, and the label list `specs/labels.csv`

**Do not read anything else.** Never open `internal/`, other transcripts, other readers' CSV files, or any file outside these paths. Do not search the file system outside them.

## What counts as a moment

One speaker turn (a line starting `[hh:mm:ss] **Name:**`). Report a moment when a turn:

- says, paraphrases or drifts from a claim in `claims.csv`
- shows, sends, mentions or asks for an asset
- uses content from an asset section that no claim covers (write it as `used`, `claim_id` and `gap_label` empty, `asset_id`, `version` and `section_id` filled)
- is a buyer repeating or pushing back on asset messaging
- carries sales or product messaging that no claim covers (a gap). When someone on your team says it, write it as `field born` with the gap label (there is no separate gap event), `fidelity` `n/a`
- sounds like an asset but comes from somewhere else (a lookalike: say so)

**Generic claims** (scope `generic`, carried by many assets) need the claim itself in the turn, not the topic. "We are built for X" in passing is the claim. A conversation that merely concerns X is not.

Ordinary talk (logistics, small talk, the customer's own business detail) is not a moment. Post call notes under the transcript help you understand a moment, but only report moments at turns.

## Output

Write a CSV with this header, one row per claim per turn (a turn carrying two claims gets two rows):

`file,time,speaker,claim_id,gap_label,event,fidelity,asset_id,version,section_id,confidence,reason`

- `file`: the path exactly as written in your task list
- `time`: the turn's timestamp exactly as written, `hh:mm:ss`
- `speaker`: the full name as written
- `claim_id`: from `claims.csv`, or empty for a gap or an asset event with no claim
- `gap_label`: a short name for what no asset covers (empty otherwise). **Use a label from `labels.csv` when one fits** (match on meaning, not wording). A label may be used on any row whose meaning it fits, whatever type it is listed under. `labels.csv` has an `also_called` column: those names mean the same thing as the label in that row, so write the label in the `label` column, never the old name. Only when none fits, write a new short label and start `reason` with `NEW LABEL:`
- `event`, one of:
  - `used` (someone on your team says it)
  - `shown`
  - `sent`
  - `mentioned` (the asset is named or described)
  - `requested` (someone asks for material that exists or does not)
  - `missing` (an asset existed and was not used when it should have been)
  - `buyer echo` (a buyer repeats asset messaging)
  - `buyer pushback`
  - `field born` (said before any asset carried it, or never carried by any asset; the speaker can be a buyer. Leave `asset_id`, `version` and `section_id` empty and name any later asset that carries it in `reason`)
  - `rep built` (someone made their own material)
  - `lookalike`
  - `internal` (asset messaging in an internal meeting, which never counts as use)
- `fidelity`: `verbatim`, `near verbatim`, `faithful paraphrase`, `drifted` (the meaning moved), `contradicted` (says the opposite or overclaims), or `n/a`. Grade fidelity against the version you name in `version` (an old version in use is graded against that old version, not the current one). With no version named, against the claim's wording in `claims.csv`
- `asset_id`, `version`, `section_id`: where the moment came from, using `claim-links.csv`. **Check the call's date** (in the transcript header) against release and superseded dates: a claim said before its asset was released is `field born`. A line that only a superseded version carries is an old version in use, so name that version. If several assets carry the claim and you cannot tell which one the speaker drew on, leave `asset_id` empty and say so in `reason`
- `confidence`: high, medium or low
- `reason`: one sentence quoting the words that decided it

## Customer signals

Log what the **customer** says, not what your team says. A CSM's question alone is not a signal; the customer's answer is. One row per signal per turn, with `claim_id` empty, the signal type in `event`, a short label in `gap_label` (**use a label from `labels.csv` when one fits**; only when none fits, write a new one and start `reason` with `NEW LABEL:`; label the kind of thing, never the company), asset fields empty, `fidelity` `n/a`, and `reason` quoting the words.

See `specs/labels-and-signals.md` for the full definitions of: `goal`, `feature request`, `renewal question`, `churn mitigation`, `win back`, `renewal reason`, `feedback`, `constraint`, `value`, `enablement need`.

## Be thorough

Read every turn. Do not report the same turn twice for the same claim or the same signal.

## Where to write

Write your CSV to the exact path named in your task (a folder under `runs/`). Write nothing anywhere else.

## Your turn (project owner)

Before you run this spec on a real call, fill in the `{{...}}` placeholders and add **your own rules**. Typical ones that come out of the dry run:

- Who counts as "your team" (list names, so a buyer sharing a first name is never counted as staff)
- Whether a particular word counts as a claim or as small talk
- Which assets are retired, and whether an old one in use is a finding
- Any scope exclusions (like pricing)
