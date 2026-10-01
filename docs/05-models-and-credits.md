# Models and credits

## What to use

**Use Claude Sonnet 5.5 at medium effort** for the readers and the adjudicator while you get going. It is the setting Victor is testing now, and it is the easiest on credits.

## How Victor got here (so you know what changed)

- The first runs, and part of the specs, were built with **Claude Opus 5.5 at high effort**.
- A ten call week at those settings cost on the order of **800,000 tokens** for the readers and adjudicator, plus a second pass for customer signals.
- To save credits he moved the readers to **Opus 5.5 at medium effort**. Recall on the best measured claims stayed above the 85% floor, but recall on generic claims dipped.
- He is now **testing Sonnet 5.5 at medium effort**, on a week where the right answers are already known.

**Be honest with yourself about the trade.** A smaller model or lower effort can miss subtler moments (paraphrases, buyers repeating your messages, messages carried by many assets). That is why the kit uses two readers and an adjudicator, and why the retro exists. If your numbers look weak, the first thing to try is **more context from you** (a better claims table, a better company brief), and only then a bigger model.

## Switching models

- Change **one thing at a time**: the model, the effort level or the spec, never two together.
- Write the **pass bar first**: what recall, what agreement, what share of rejects, what cost.
- Keep the **old outputs** so you can compare.
- The reader agent definition lives in [`agents/reader.md`](../agents/reader.md). The `model` and `effort` lines are the ones you change.

## What costs credits

| Step | What happens | Rough size |
|---|---|---|
| Building helper scripts | Claude writes a few small Python scripts for you | One time, small |
| Proposing claims | Claude reads your assets and proposes claims | One time per asset batch, moderate |
| Dry run on one call | Claude reads one call | Small |
| A weekly run | Two readers read the week, then an adjudicator | The biggest cost, on the order of hundreds of thousands of tokens for a ten call week |
| Reviews and reports | Claude drafts the retro, the spot check list and the report | Small |

**Ways to keep it small**

1. Start with 2 to 3 calls and 5 assets.
2. Split a long week into halves (the kit does this for you).
3. Run one week at a time, with a stop after each.
4. Let the check script do arithmetic, not an agent.
5. Run the full week only after the dry run is right.

## Before you start

- Know your Claude Code usage limits and when they reset.
- State the plan to Claude Code first: **how many agents, and roughly how many tokens**. The kickoff file asks it to do this before it starts anything large.
- Do not start a big run near the end of your limit window. A run that hits the limit produces no output.

## What it cost in Victor's build (fictional data)

| When | What | Cost |
|---|---|---|
| Test week | Four readers on one test week (a whole call vs a search shortlist) | About 217,000 to 248,000 tokens each |
| First eight week launch | Six readers started at once | Hit the weekly usage limit. All six died, **no output** |
| Week 33 (10 calls) | Two readers, Opus 5.5 at high effort | About 309,000 and 292,000 tokens, 13 to 14 minutes each |
| Week 33 | One adjudicator on 42 items | About 190,000 tokens, 5 minutes |
| Week 33 | A second pass for customer signals, two readers | About 155,000 tokens each, about 3 minutes |
| Week 33 total | | About 790,000 tokens for the main run, about 1.1 million with signals |
| Week 34 (11 calls) | Four readers (two readings, two halves each), one adjudicator, signals included, Opus 5.5 at medium | About 795,000 tokens in total, about 72,000 tokens per call, against about 110,000 per call for week 33 with its signals pass |
| Reviews, retro and report | Main session, no agents | No reader tokens |

Two things to take from this: **splitting a long week into halves** keeps each reader's context smaller, and doing messaging and signals in **one pass** came out cheaper per call than two passes. That second comparison is not clean, because the effort level changed in the same week, so treat it as a hint, not a rule.
