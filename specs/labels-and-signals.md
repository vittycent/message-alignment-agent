# Customer signals and the labels list

Readers log what customers say, as well as what your team says. These are the signal types and the rules. The **labels list** (`labels.csv`) keeps the names consistent from week to week.

## The signal types

Each is one row per signal per turn: `claim_id` empty, the type in `event`, a short label in `gap_label`, `fidelity` `n/a`, `reason` quoting the words.

| Type | What it is | Rules |
|---|---|---|
| `goal` | A goal the customer states or confirms, and what sits under it (the consequence behind a deadline, who they need to convince) | Label the goal *type*, for example `answer a customer's data request` |
| `feature request` | The customer needs a capability you lack or only have on the roadmap, often tied to a date or an internal goal | Label the capability. A buyer asking whether something is coming because they need it is a feature request, not use of a roadmap claim |
| `renewal question` | Only in business reviews and renewal calls, one row per call. Whether your team asked **would you renew**, and how the customer answered | Labels: `asked, clear yes`, `asked, clear no`, `asked, unclear`, or `not asked` (logged at the call's last turn, even if the customer volunteers an answer; log what they volunteer as a `renewal reason`). Exit interviews get no renewal question row. Kickoffs and onboarding are too early |
| `churn mitigation` | Someone on your team asks what it would take to keep a customer who may stop using the product ("what would keep you?", "what would you need to see?") | **Not the renewal question.** Label the condition the customer names ("something for the board"). Quote the answer in `reason` |
| `win back` | The customer has already decided to leave, and your team asks whether they would come back | Labels: `win back: clear yes`, `win back: clear no`, `win back: unclear` |
| `renewal reason` | From an existing customer, a reason for renewing, not renewing, being unsure or being at risk | Start the label with `renew:`, `not renew:`, `unsure:` or `at risk:`. `at risk:` is for a customer who stays for now but shows no ongoing value or use |
| `feedback` | Something the customer says is not working **in your product, data or service** | Label the thing, so the same problem groups across calls. The customer's own limits are a `constraint` |
| `constraint` | The customer's own bandwidth or limits you have to work around (two hours a week, one person doing it all, their own data gaps, internal politics) | Label the limit |
| `value` | A benefit the customer reports, especially money or time saved | Money saved is `value`, even if pricing is out of scope |
| `enablement need` | The customer, often the champion, lacks the material or skills to bring colleagues or leadership along | Label the need |

> These definitions came out of Victor's real review sessions. The renewal question, churn mitigation and win back are three different conversations that lead to three different assets. Define a signal by the action it leads to, not by the words. **Your turn:** change these definitions to match your company.

## The labels list

`labels.csv` has these columns: `type, label, means, first_seen, also_called`.

- `type`: one of the signal types above, or `gap`
- `label`: the short, consistent name readers must use
- `means`: one line, so a reader can match on meaning
- `first_seen`: the week it was first used
- `also_called`: other names that mean the same thing, separated by `;`. Readers write the main label, never an alias

**How it grows:** readers may coin a new label when none fits, starting `reason` with `NEW LABEL:`. The weekly **label review** shows you the ten labels the system is least sure about (new, from one reader only, low confidence). You keep, merge (turn into an alias), rename or drop each one. Approved changes go into `labels.csv` before the next week.

**Pair the two readers' labels before you rank them.** Two readers describing the same turn with different words should be one entry, or the top ten fills with duplicates. A good rule: link labels that are in the same call and of the same type, either within about 60 seconds of each other or with nearly identical wording.

## Seed list

Start with an empty `labels.csv` (header only) and let the first week fill it. After the first label review you will have 30 to 50 labels, and later weeks will need far fewer new ones.
