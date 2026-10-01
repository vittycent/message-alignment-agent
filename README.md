# Message Alignment Agent: starter kit (version 2)

**From Victor Arellano, product marketer.** Built and tested on **fictional data** (a made up company called Rootline). Nothing in this kit comes from a real customer, and you will not need any of Victor's files to use it. You bring your own assets and your own calls.

## What this is, in one minute

Marketing writes decks, one pagers, blogs, scripts and playbooks. Hardly anyone knows which of those messages sales and customer success really say on calls, or what they say that no document covers.

This kit shows you how to build an agent, in your own Claude Code, that:

1. reads your recorded calls
2. compares what people said with your own documents
3. writes one report for the person who owns messaging

The report covers **what is landing, what is not, what the field says that your documents lack, how reps drift from the documents, and what customers tell you** about their goals, problems and renewal. Every finding comes with quotes and a confidence level.

## Where this comes from (version 1 and version 2)

**This is version 2.** Victor built a first, simple version of this process in a previous role (see [Provenance and data](#provenance-and-data) below). That earlier version was a register of every sales asset and a weekly heat map of which assets showed up in call transcripts. It taught him two things:

- Reps almost never name the asset ("the deck"), so matching has to be by meaning.
- A keyword search cannot see what is *missing*, and what is missing is where the best evidence usually is.

Version 2 is a rebuild around **claims**, the individual messages inside each asset, with two independent AI readers per call and a third agent to settle disagreements. Victor designed it from scratch on fictional data so that he could share it, measure it against an answer key, and keep improving it in the open.

## Provenance and data

- **Everything in this repo was created for this repo.** It was written by Victor with Claude.
- **Rootline, and every call, asset, name, customer, quote and number in the examples, is invented.** Nothing in the examples is real.
- **No data, documents, transcripts, customer information, code or prompts from any current or previous employer are used or included here.** Nothing confidential is in this repo.
- The idea of an earlier, simpler process came from Victor's own experience in a previous role. This version was designed from scratch and tested only on invented data.
- Rootline is a made up carbon accounting company. The industry choice reflects the author's general field knowledge, not any company's data.
- The kit is licensed under CC BY 4.0 (see below).

## The most important thing to know: this is hands-on

The agent is only as good as the context you give it. Expect to **review data and explain your business along the way**. That is not a flaw in the process, it is the process. Every hour you spend telling it how to interpret things pays back many times:

- what your company means by words like "customer", "champion" or "renewal"
- which of your assets are alive, which are dead, and which reps still use the old ones
- which messages matter and which are filler
- what a good call looks like to you

Every file in this kit asks you for information at the right moment. Look for the boxes that say **Your turn**. Please do not skip them. The more of yourself you put in, the better your report.

**It does not have to be scary.** Most people do this in short, friendly sessions with a colleague, a coffee, and a Claude Code window. See [docs/02-plan-and-time.md](docs/02-plan-and-time.md) for how to chunk it. Plan to come prepared to talk for about an hour at the start, and to share what you know. That conversation is the single best investment.

## Who does what

The marketer owns the problem, the question and every judgement call. Claude does the engineering and proposes options. Victor did it that way and so can you: you do not need to be an engineer.

## What you will end up with

- A folder with your asset register, your claims table and your call list
- A set of written instructions (specs) for a reader agent and an adjudicator agent, tuned to your company
- A first report on your own calls
- A weekly command or skill in your Claude Code that repeats the process on new calls

## What is in this repo

| Where | What |
|---|---|
| [docs/01-how-it-works.md](docs/01-how-it-works.md) | The architecture, in detail, and how it works right now |
| [docs/02-plan-and-time.md](docs/02-plan-and-time.md) | The setup in short sessions, with a stop after each |
| [docs/03-prepare-your-inputs.md](docs/03-prepare-your-inputs.md) | What to gather before you start: transcripts, assets, context, access |
| [docs/04-what-it-can-and-cannot-do.md](docs/04-what-it-can-and-cannot-do.md) | The honest version, including what is still being tested |
| [docs/05-models-and-credits.md](docs/05-models-and-credits.md) | Which model to use, and what it cost in Victor's build |
| [docs/06-lessons-learned.md](docs/06-lessons-learned.md) | What worked, what we got wrong, and what changed |
| [docs/07-assumptions-and-model-tests.md](docs/07-assumptions-and-model-tests.md) | How to write assumptions and test a model change, with a worked example |
| [docs/00-explain-it-to-your-team.md](docs/00-explain-it-to-your-team.md) | 30 second and 2 minute versions, and the questions you will get |
| [docs/glossary.md](docs/glossary.md) | The terms used in this kit |
| [kickoff/START-HERE-for-claude-code.md](kickoff/START-HERE-for-claude-code.md) | **The file you give Claude Code to begin.** It walks you through everything, one gated step at a time |
| [specs/](specs/) | The specs that produce the agent: reader, adjudicator, labels and signals, claims builder, report, helper scripts |
| [templates/](templates/) | Empty versions of every file you will fill in |
| [examples/](examples/) | A small sample of the fictional Rootline data, what the agent produced, and a retro, spot check and label review |
| [agents/](agents/) | The agent definition for the reader (Sonnet 5.5, medium effort) |

## How to get started (today)

1. Read this page and [docs/01-how-it-works.md](docs/01-how-it-works.md). Fifteen minutes.
2. Skim [docs/03-prepare-your-inputs.md](docs/03-prepare-your-inputs.md) and start gathering.
3. Put this folder somewhere Claude Code can see it, open Claude Code in your project folder, and give it `kickoff/START-HERE-for-claude-code.md`.
4. Say: "Follow this file. Stop after each step and ask me before you go on."

## Honest status and a note on models

- It has been **run on three of eight planned weeks** of fictional calls so far. It works, with known limits ([docs/04](docs/04-what-it-can-and-cannot-do.md)).
- Part of it was built with **Claude Opus 5.5 at high effort**, then moved to medium, and Victor is now testing **Claude Sonnet 5.5 at medium effort** to save credits. **For this kit, use Sonnet 5.5 at medium effort.** Be thoughtful if you switch models: a different model or effort level changes the results, so change one thing at a time and watch the numbers.
- **Building this uses credits**, for example for writing the helper scripts, proposing claims, and reading your first calls. Start small. See [docs/05-models-and-credits.md](docs/05-models-and-credits.md).
- Victor will **publish updates to this repo** as he improves it. Check back here before you start a new round, and compare the changelog (in this repo's commit history).

## A note on the open source tools

The process uses a few open source Python libraries, run locally on your machine: a keyword search library, a fuzzy text matching library, and a small multilingual text embedding model. They are well known, widely used libraries and they are optional at the size most teams start at. [docs/01-how-it-works.md](docs/01-how-it-works.md) explains what each one does in plain language.

## Licence

This kit is licensed under [Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE). You may share and adapt it, including commercially, as long as you give credit to Victor Arellano and note any changes. All company names, people, calls and numbers in the examples are fictional.

## Credit

Built by Victor Arellano with Claude. Everything in this repo is built on fictional data, and nothing from any employer is included (see Provenance and data).

Questions, wins and surprises are welcome. If something in this kit did not work for you, that is useful information. Tell Victor.
