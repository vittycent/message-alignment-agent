# Helper scripts to build

Small Python scripts that do the **counting, checking and drawing**. Ask Claude Code to write them one at a time with you, and test each one on your dry run. Keep them deterministic: the same input always gives the same output. Put them in `tools/`.

## Set up Python once

Use `uv` and a virtual environment inside the project. Python 3.12 is a good choice. Install what you need as you go (for example `rapidfuzz`). Nothing here touches your machine's own Python.

## The scripts

| Script | What it does | Inputs | Output |
|---|---|---|---|
| `ingest.py` | Reads the readers' CSV files for a week (and halves, if split), checks the header, merges halves into one file per reader, and **verifies every quote in `reason` exists in the transcript** (RapidFuzz is good for this) | `runs/<week>/parts/*.csv`, transcripts | `runs/<week>/run-A1.csv`, `run-A2.csv`, a list of rows that failed a check |
| `check.py` | Compares reader 1 and reader 2 per (call, claim). Both found it: **high**. Only one: goes to the adjudicator. Reports reader agreement | the two run files | counts, and `adjudication/items.csv` |
| `build_adjudication.py` | Writes the adjudicator's items file (claim wording, the proposed turns with context, the earlier reader's reasons) | `items.csv`, claims, transcripts | `adjudication/items.md` |
| `score.py` | Scores each reader against your **mini answer key**: recall at turn level and call level, asset right where scored, lookalikes not misattributed | run files, `internal/answer-key.csv` | `score.txt` |
| `asset_use.py` | Counts, per call and per asset, where both readers find two or more claims (at least one exclusive) or someone naming the asset. Counts every version released by the call date | run files, register, claim links | `alignment-data/asset-use-by-call.csv` |
| `visuals.py` | Draws the two visuals: assets by stage, and the week over week heat map, as SVG, plus the numbers behind them | `asset-use-by-call.csv`, `calls.csv`, register | `report/*.svg`, `visual-numbers.md` |
| `evidence.py` | Rolls up all weeks into tables: messages by week, stage and role; discovery calls only; drift; gap labels; asset events; old versions in use; customer signals by type and label | run files, adjudication decisions, claims, messages | printed tables for the report |
| `label_review.py` | Lists every gap and signal label against `labels.csv` and ranks the ones that need your eyes: new, one reader, low confidence first. **Pairs the two readers' labels** (same call and type, within 60 seconds, or near twin wording) before ranking | run files, `labels.csv` | `label-review-<week>.md` |

## Settings to give every script

- A `scope` module that lists out of scope claims and the signal event types
- Staff matched by **full name**, from `calls.csv` (the `team_speakers` column)
- Paths relative to the project root, so the folder can move

## Order to build them

1. `ingest.py` and `check.py` (needed for the first week)
2. `build_adjudication.py`
3. `score.py` (once you have the mini key)
4. `label_review.py`
5. `asset_use.py` and `visuals.py` (once the first week is done)
6. `evidence.py` (when you start writing the report)

## Your turn (project owner)

Run each script on a small example and read the output yourself. If a number looks wrong, **check the script and the key before blaming the agent**. In Victor's build the first gap score looked terrible. It was the scoring script, which was counting a call the readers were never given.
