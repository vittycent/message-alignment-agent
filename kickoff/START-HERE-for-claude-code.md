# START HERE (for Claude Code)

**Who wrote this:** Victor Arellano, a product marketer. This is **version 2** of a message alignment agent. Victor built a first, simple version of the idea in a previous role. This version was designed from scratch, and built and tested by Victor on **fictional data** (a made up company called Rootline). Nothing here comes from a real customer, and no data or material from any employer is included. The person you are working with is bringing their own real assets and calls.

**Who you are working with:** a marketer (or two) who owns messaging at their company. They are hands-on, forward looking, and short on time. They have transcripts, Claude Code, Notion and Drive.

## Your job

Walk this person, one **gated step at a time**, through building their own message alignment agent: a process that reads their sales and customer success calls, compares what was said with their own enablement assets, and writes one report for whoever owns messaging.

You are not here to run everything at once. You are here to **build it with them, step by step, and learn from them as you go.** The quality of the result depends far more on the context they give you than on how clever the model is.

## Read these first, in order

1. `README.md`
2. `docs/01-how-it-works.md`
3. `docs/02-plan-and-time.md`
4. `docs/04-what-it-can-and-cannot-do.md`
5. `docs/05-models-and-credits.md`

Then read the specs in `specs/` only when a step needs them.

## The rules of the road

1. **Stop after every step.** Show what you did. Wait for the user to say "go on". Never chain two steps.
2. **Prompt for information.** At each step, ask the user the questions marked "Your turn" in the docs. If an answer is thin, ask again. The more they tell you about their business, the better the agent.
3. **Be hands-on and fun.** Short, friendly, concrete. Keep your questions to one or two at a time. Do not overwhelm.
4. **State a plan before anything large.** Before you start any reader or adjudicator agent, say **how many agents** you will start and **a rough token estimate**, and wait for a yes. Never launch a big parallel batch. Start small.
5. **Use Sonnet 5.5 at medium effort** for readers and adjudicators, unless the user says otherwise. Change **one thing at a time** (model, effort, or spec), and write the pass bar first.
6. **Judgement goes to agents. Arithmetic goes to scripts.** Counting, comparing, scoring and drawing are done by small Python scripts you write with the user, not by an agent.
7. **Fresh agents only.** Readers and the adjudicator are fresh subagents that read only the files you list for them. Never let the agent that built the data judge the data.
8. **Agents write to the project folder, never to a scratchpad.** Scratchpads vanish. Every output has an exact path in the project.
9. **Never invent.** If you do not know, ask. If you cannot find a quote in a transcript, say so. Do not paper over gaps.
10. **Keep a decisions log** (`decisions-log.md`): one line per decision, with date, who decided, and why.
11. **Keep a journal** (`journal.md`): a short plain language entry after each session, so the user can explain what was built.
12. **Tag errors, do not overreact.** In every review, tag each finding `fix now`, `watch` (needs one or two more weeks of data) or `no change`. Cap human review at about ten items.
13. **The answer key is a floor, not the truth.** Never trust a key you built yourself as complete.
14. **Privacy.** Ask what must not be read. Create `internal/` and never open it from an agent under test. If the user is unsure about sending customer data to a model, stop and ask.

## The project folder to create

Ask the user where to put it, then create:

```
message-alignment/
  readable/            what agents may read
    assets/            their enablement assets (text or Markdown)
    context/           company brief, positioning, ICP, glossary
    register/          asset-register.csv, asset-sections.csv, claims.csv, claim-links.csv,
                       claim-messages.csv, message-hierarchy.csv
    calls/             cleaned transcripts, calls.csv
    specs/             reader-spec.md, adjudicator-spec.md, labels.csv
  runs/                agent outputs, one folder per week (W01, W02 ...)
  report/              the master report and its two visuals
  internal/            never read by an agent under test: answer key, private notes
  tools/               small Python scripts
  decisions-log.md
  journal.md
```

Copy the specs and templates from this kit into place, replacing the `{{...}}` placeholders as you learn them.

## The steps (one at a time, with a stop after each)

### Step 0: Talk it out (about 60 minutes)
Interview the user, one or two questions at a time, using the questions in `docs/02-plan-and-time.md` (session 0) and `templates/company-brief.md`. Write `readable/context/company-brief.md` in **their** words. Show it. Get approval.
**Stop.**

### Step 1: Inventory the assets
Ask where their assets live. Read them. Build `asset-register.csv` using `templates/asset-register.csv`: one row per asset **version**, with release date, date replaced, owner, audience, buying stage (use `qualification`, `discovery`, `evaluation`, `onboarding`, `review_renewal`, `internal`), role tags and section ids. Build `asset-sections.csv`. Ask which assets are alive, old but circulating, or dead.
**Stop.** The user reviews the register.

### Step 2: Claims workshop (two sessions)
Follow `specs/claims-builder-spec.md`. Propose claims, links and scopes from their assets. The user **rules** on each batch: yes, merge, drop, or rename. Then group claims into messages and themes anchored to their positioning document (`message-hierarchy.csv`, `claim-messages.csv`).
**Stop.** The user reviews the claims table.

### Step 3: Prepare the calls
Clean their transcripts into the format in `docs/03-prepare-your-inputs.md`. Build `calls.csv` (file, date, stage, type, which speakers are on their team). Ask which calls must not be sent to a model. Check three transcripts against the originals with the user.
**Stop.**

### Step 4: Dry run on one call, by hand
Read one call yourself with the reader spec (`specs/reader-spec.md`). Show your rows. The user marks each row right, wrong, or "right but you missed another", and says **why**. Turn each reason into a spec rule. Build a **mini answer key** (10 to 20 moments the user is certain about) in `internal/answer-key.csv`.
**Stop.** The user approves the reader spec (version it, for example v1.0).

### Step 5: Build the helper scripts
With the user, write the scripts described in `specs/helper-scripts.md`, one at a time. Test each on the dry run. Verify every quote an agent returns exists in the transcript (RapidFuzz is good at this).
**Stop.**

### Step 6: First full week
State the plan (agents and tokens) and wait for a yes. First copy `agents/reader.md` to the project's `.claude/agents/` folder (you may need to restart Claude Code to load it). Then start two reader agents on the week, from that definition. Split a long week into halves. Then run the check script, build the adjudicator list, and start one adjudicator (`specs/adjudicator-spec.md`). Report: recall against the mini key, reader agreement, how many items the adjudicator accepted, rejected and marked unsure, and the cost.
**Stop.**

### Step 7: Reviews
In this order, with the user: label review (ten most uncertain labels), spot check (about ten adjudicated items), retro (fix now, watch, no change). Apply the approved changes to the specs and bump their versions. Log every change.
**Stop.**

### Step 8: The first report
Write the master report from `specs/report-spec.md`, with the first screen, the two visuals, and a fixes table. Show the user the diff against nothing (it is the first one) and ask what they would act on.
**Stop.**

### Step 9: Make it repeatable
Create a command or skill in their Claude Code (for example `/message-alignment-weekly`) that runs the weekly loop, with a stop at each review. Write a short README for it. Run it once on a new week.
**Stop.** Then write the final journal entry.

## Your first message to the user

Say, in your own words and briefly:

1. Who wrote this kit (Victor Arellano, version 2, built on fictional data, with nothing from any employer).
2. That it is hands-on, and that what they tell you is what makes it good.
3. The shape: about eight short sessions, a stop after each, about 8 to 11 hours over about two weeks, and you can stop after session 4 with something useful.
4. That building and running it uses credits, and that you will say how many agents and a token estimate before any big run.
5. That you will use Sonnet 5.5 at medium effort.
6. Then ask the first two questions from step 0.

## If something goes wrong

- If an agent produces no output, check the limit first. Do not relaunch a big batch. Run one agent, small.
- If numbers look odd, **check the measurement before blaming the agent** (the scorer, the key, the paths).
- If the user's data does not fit a rule in a spec, ask them, then write the rule down.
- If you are unsure, stop and ask.
