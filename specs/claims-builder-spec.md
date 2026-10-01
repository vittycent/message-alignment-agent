# Claims builder spec (draft, untested end to end)

> **Honest status:** In Victor's build the claims table was written by hand, with scripts, over about a day. This spec is the *proposed* way to make it faster: Claude proposes claims from your assets and you rule on them. It has not been run end to end. Expect to fix things, and tell Victor what breaks.

The claims table is the most valuable file in the whole process. Every reader looks claims up in it. Spend your time here.

## What is a claim?

A **claim** is one distinct message inside an asset, in short form, that a rep could say out loud. Examples (from the fictional company):

- "Every number traces back to source, vintage and geography"
- "Restatements are split by cause: factor update, activity correction, methodology"
- "Start with the top twelve suppliers, not all of them"

A claim is **not**: a heading, a decorative sentence, a logistics line, or a fact about the document itself.

## The files you build

| File | One row per | Columns |
|---|---|---|
| `claims.csv` | claim | `claim_id, claim, cluster, era, first_released, status, scope, assets_full, assets_family, n_links, notes` |
| `claim-links.csv` | claim and where it appears | `claim_id, asset_id, version, section_id, strength, released, superseded_on, heading` |
| `claim-messages.csv` | claim | `claim_id, message_id` |
| `message-hierarchy.csv` | message | `message_id, theme_id, theme, message, in_positioning, positioning_ref, n_claims, claim_ids` |

- `strength` is `full` (the asset carries the claim in full) or `family` (a softened or early form).
- `scope` is **exclusive** (one asset carries it), **shared** (two or three) or **generic** (four or more), counted on full links.
- `cluster` is a short theme code you choose.
- `era` groups claims by the period of your messaging (for example four periods since the company started).
- `status` is `current` if any current asset version carries the claim, otherwise `retired`.

## The process (one asset batch at a time)

1. **Pick a batch** of 3 to 6 assets (start with your positioning document, then the pitch deck, then the one pagers).
2. For each asset, **read it section by section** and propose claims. Number the claim ids `C01`, `C02`, ... in the order you first meet them.
3. **Link each claim to its sections** with `claim-links.csv`. If a claim already exists in another asset, **link it, do not duplicate it**. A different wording of the same message is one claim carried twice.
4. **Mark strength** (`full` or `family`) and the version's release and replaced dates from the asset register.
5. **Show the batch to the owner.** Ask them to rule on each claim: keep, merge with another, drop, or rename. Ask which are core messages and which are supporting.
6. Apply the rulings. **Never silently renumber a claim that has been used.**
7. After all batches, **compute scope** and **status** with a script, not by hand.
8. **Group claims into messages and themes** the way the owner trains the team, anchored to the positioning document. Mark which messages are in the positioning document and which are not (these are findings in themselves).
9. Write a short **README-data.md** describing the files.

## Your turn (project owner)

Claude Code will ask you, batch by batch:

- Which of these claims are your headline messages?
- Which of these are filler?
- Which two claims are really the same?
- Which claims do you want the agent to watch for, even if they appear in only one asset?
- Which claims are old and retired?

Do not rush this. A better claims table gives a better report, every week.

## Sizing guide

| Size | Use it for |
|---|---|
| 10 to 20 claims, 5 assets | A trial, to feel the process |
| 50 to 150 claims, 15 to 40 asset versions | A full first run |
| Over 150 claims | Possible, but expect to need the optional shortlist from `docs/01-how-it-works.md` |

## Checks (scripts, not agents)

- Every `claim_id` in `claim-links.csv` exists in `claims.csv`, and the reverse
- Every `asset_id`, `version` and `section_id` in `claim-links.csv` exists in the register and section files
- Every claim has at least one link
- `scope` and `status` match the links
