# Adjudicator spec: settle the disagreements between two readings

Version 1.0 of the starter kit (based on Victor's adjudicator spec v1.3). Replace every `{{...}}`.

## The job

{{COMPANY}} has marketing and sales enablement assets. Two independent readers went through the same call transcripts and listed every turn where a claim from `claims.csv` shows up. Where they disagree (one reader found a claim in a call, the other did not), you decide who is right.

You are a **fresh reader**. You have not seen either reader's full output, and you do not need it.

## What you may read

Base folder: `{{PROJECT}}/readable/`

- `register/` files and `assets/`
- This spec, and the items file named in your task (it sits in `runs/<week>/adjudication/`)
- The transcripts the items point to, and only those

**Do not read anything else.** Never open `internal/`, other transcripts, or other readers' CSV files.

## How to decide each item

1. Read the claim in `claims.csv` (its wording, scope, and the assets that carry it).
2. Open the transcript and read the proposed turns **with a few turns either side**, so you judge the meaning in context, not a fragment.
3. Decide:
   - `accept`: the turn carries this claim's meaning, word for word, paraphrased, or drifted (recognisably there but the meaning moved). A buyer repeating or pushing back on it also counts
   - `event only`: the turn names, shows, sends or asks for an asset that carries the claim, or the claim should have been said and was not (`missing`), but **none of the claim's content is spoken**. "The letter we used with the first nine" names the template; it does not say what the template says
   - `reject`: the turn is about a nearby idea, a different claim, or only the general topic
   - `unsure`: you genuinely cannot tell; say why
4. **Generic claims** need the claim itself in the turn, not the topic.
5. **Check the date** in the transcript header against the asset's release and superseded dates in `asset-register.csv`: said before any asset carried it is `field born` (leave the asset fields empty and name the later asset in `reason`). A line only a superseded version carries is that old version in use.
6. If you accept, pick the single best turn if several are proposed.
7. **Scope:** {{OUT_OF_SCOPE_RULE}} (in Victor's build: pricing is out of scope, so reject any item about prices, quotes, discounts or budgets, with the reason `pricing out of scope`).
8. **A buyer asking whether a capability is coming, because they need it for their own goals, is a feature request, not use of a roadmap claim:** reject. (The readers log it separately as a customer signal.)

## Output

Write a CSV with this header, one row per item, every item answered:

`item,file,claim_id,decision,time,speaker,event,fidelity,asset_id,version,section_id,reason`

- `time`, `speaker`: the accepted or event only turn, exactly as written (empty on reject)
- `event`: `used`, `shown`, `sent`, `mentioned`, `requested`, `missing`, `buyer echo`, `buyer pushback`, `field born`, `rep built`, `lookalike`, `internal` (empty on reject; on `event only` it is `mentioned`, `shown`, `sent`, `requested` or `missing`)
- `fidelity`: `verbatim`, `near verbatim`, `faithful paraphrase`, `drifted`, `contradicted`, or `n/a`
- `asset_id`, `version`, `section_id`: from `claim-links.csv`; leave `asset_id` empty if several assets carry the claim and you cannot tell which one the speaker drew on. For `field born`, leave the three asset fields empty and name the later asset in `reason`
- `reason`: one sentence, quoting the words that decided it

Use a proper CSV writer (quote fields containing commas). Write it to the exact path named in your task, and nothing anywhere else.

## Your turn (project owner)

After your first adjudication, read the `unsure` items and the closest accepts and rejects yourself. Every ruling you disagree with becomes a rule here. Typical rules that appear: what counts as a lookalike, how to handle a buyer who uses your claim as a yardstick on a competitor, and what to do with one item of a list claim.
