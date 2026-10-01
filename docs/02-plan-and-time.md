# The plan: short sessions, a stop after each

You do not need a free week. You need about **eight short sessions over roughly two weeks**. Each one has a clear start, a clear finish, and a **stop**: Claude Code finishes, shows you what it did, and waits for you to say "go on". That is how you stay in control, and it is how the agent gets better.

> **Time estimates are Victor's.** They come from building this once, on fictional data, with a lot of experience of the problem. Your first run will likely be a bit slower, and your second a lot faster. Treat them as a guide, not a promise.

## The shape of it

| # | Session | You | Claude Code | Time (estimate) | What you have at the end |
|---|---|---|---|---|---|
| 0 | **Talk it out** | Talk, with a colleague if you can | Takes notes and writes your company brief | **60 min** | A company brief |
| 1 | **Inventory your assets** | List and point to them | Builds the asset register and section list | 60 to 90 min | Asset register |
| 2 | **Claims workshop** | Rule on proposed claims | Proposes claims, links, messages | **2 sessions of 60 to 90 min** | Claims table |
| 3 | **Prepare your calls** | Choose and export calls | Cleans transcripts, builds the call list | 45 to 60 min | Call list, clean transcripts |
| 4 | **Dry run on one call, by hand** | Read along and correct | Reads one call with the specs and shows its work | 60 min | Tuned specs |
| 5 | **First full week** | Review | Runs two readers, the check and the adjudicator | 30 min of yours, plus the run | First readings |
| 6 | **Reviews** | Label review, spot check, retro | Prepares each and applies your rulings | 60 min | Better specs, a first report |
| 7 | **Make it repeatable** | Choose a name and a day | Turns it into a command or skill | 45 min | A weekly command |

**Total about 8 to 11 hours, spread over about two weeks.** You can stop after session 4 and already have something useful: you will have read one real call against your own messages, which is eye opening.

## How to use the sessions

- **Book them in your calendar now**, as short blocks. Sessions 0 to 3 can be done in two or three days.
- **Do session 0 with a colleague** who sells or runs customer success. One hour of two people disagreeing about what the company says is worth more than a day alone.
- **Never run two sessions back to back without reading what Claude produced.** The gate is the point.
- **Keep a decisions log.** Claude Code will keep one for you (the kickoff file asks it to). One line per decision, with who decided.

## Session 0: Talk it out (60 minutes)

This is where you give the agent your business. **Come prepared to talk, and make it fun.** Pour a coffee. Record it if you like, or ask Claude Code to take notes as you go.

**Your turn.** Talk through these out loud. Claude Code will ask them one at a time:

1. Who do you sell to, and who do you *not* sell to?
2. What are the three messages you want every rep to say?
3. Which assets do reps actually use? Which ones do you suspect they have stopped using?
4. What do reps say that is not in any document, and is it good?
5. How do you describe your buying stages? Where do customers get stuck?
6. What is a renewal conversation at your company? Who asks the question, and when?
7. What words do you use that a stranger would misread?
8. What would you act on first if the report told you?

**What you have at the end:** `context/company-brief.md`, written by Claude Code in your words, and approved by you.

## Session 1: Inventory your assets (60 to 90 minutes)

You point Claude Code at where your assets live (Drive, Notion or a folder) and it builds a register: one row per asset **version**, with release date, date replaced, owner, audience, buying stage and who uses it.

**Your turn.**
- Say which assets are **alive**, which are **old but still circulating**, and which are **dead**. Old versions in circulation are one of the best findings this agent produces.
- Fill in release dates, even approximate ones. They decide what counts as "said before the asset existed".
- Say who each asset is for (rep, CS, customer) and at which buying stage.

**Stop:** you review the register. Fix anything that is wrong. Do not move on with guesses in it.

## Session 2: Claims workshop (two sessions, 60 to 90 minutes each)

This is the part that makes or breaks the quality, and it is the part people enjoy most. Claude Code reads your assets and **proposes claims**: the individual messages inside each asset, in short form, with a scope, and links to the sections that carry them. **You rule on them.** You say "yes", "merge these two", "that is not a message, it is filler", or "that one is the real headline".

**Your turn.**
- Tell Claude which claims are your **core messages** and which are supporting.
- Tell it which claims are **old and retired** so it does not count them as live.
- Point out when two assets say the same thing in different words. That is one claim, carried twice.
- Group the claims into the **messages and themes** your team is trained on, anchored to your positioning document.

A good starting size is **50 to 150 claims** across **15 to 40 asset versions**. Do not try to be perfect. The retro finds what is missing.

**Stop:** you review the claims table, the links and the message hierarchy.

> Victor's honest note: building the claims table by hand for his 24 asset versions took a day of careful work. Having Claude propose claims and you rule on them should be much faster, but it is the least tested part of the kit. Expect to fix things. Time you spend here comes back to you in better reports.

## Session 3: Prepare your calls (45 to 60 minutes)

You choose the calls, export the transcripts, and Claude Code cleans them into a shared format and builds the call list (file, date, stage, type).

**Your turn.**
- Pick **8 to 12 calls for the first week**, with a mix of stages if you can.
- Tell Claude the **buying stage** of each call, and who on the call is on your team.
- Remove anything private you do not want to send to a model. See the privacy notes in [03-prepare-your-inputs.md](03-prepare-your-inputs.md).

**Stop:** you check three transcripts yourself against the originals.

## Session 4: Dry run on one call, by hand (60 minutes)

Before running anything at scale, Claude Code reads **one call** with the reader spec, and shows you its rows. You read along with the transcript. This is where you teach it the most.

**Your turn.**
- For each row, say: right, wrong, or "right but you missed another".
- When you disagree, **say why**. Claude writes your reason into the spec as a rule.
- Pick **10 to 20 moments you are certain about** across your first calls. This is your **mini answer key**. It lets the agent show you recall on your own data.

**Stop:** you approve the reader spec. Everything after this uses it.

## Session 5: First full week (30 minutes of yours)

Claude Code starts the two readers on a week of calls. If the week is long it splits each reader's job into two halves. Then it runs the check script, builds the adjudicator's list and starts the adjudicator.

**Your turn.** While it works, write down what you **expect** the report to find. Compare when it finishes. The places where you are surprised are the interesting ones.

**Stop:** you review the numbers (recall against your mini key, agreement between readers, how many items the adjudicator accepted and rejected).

## Session 6: Reviews (60 minutes)

Three short reviews, in this order:

1. **Label review.** The ten labels Claude is least sure about. You keep, merge, rename or drop. Use your own words.
2. **Spot check.** About ten items the adjudicator ruled on, led by anything it marked unsure. Agree or rule.
3. **Retro.** Claude groups the week's errors by cause and tags each `fix now`, `watch` or `no change`. You approve or reject each fix. Specs get a version number.

**Your turn.** For each ruling, tell Claude **what you would do about it**. If a finding would make you change an asset, say so. Findings you would never act on can be dropped from the report.

**Stop:** you read the first version of the report. It will have a first screen of three findings and a table of fixes.

## Session 7: Make it repeatable (45 minutes)

Claude Code turns the process into a **command or skill** in your Claude Code (for example `/message-alignment-weekly`). It points at your specs, your register, your claims table and the call folder. You choose a day of the week.

**Your turn.** Decide who reviews each week, and how long you will give it (about 60 minutes is a good target).

**Stop:** you run it once on a new week and read the result.

## Credits, and starting small

Building this uses credits. The big costs are Claude reading calls (a ten call week cost on the order of 800,000 tokens per run at Victor's first settings) and the one time cost of Claude writing your helper scripts and proposing claims. **Start with a small trial** (sessions 0 to 4 on two or three calls) before you run a full week. See [05-models-and-credits.md](05-models-and-credits.md).

## If you only have a day

Do sessions 0 and 4 on **one asset type and five calls**. You will have a tiny claims table of ten claims, one dry run, and a feel for the whole thing. That is a good way to decide whether to invest the rest.
