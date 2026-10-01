# Explain it to your team

Short versions you can adapt, and the questions you will get. Replace the placeholders with your own company.

## In 30 seconds

Marketing writes decks, one pagers, blogs and scripts. Nobody knows which of those messages sales and customer success actually say on calls, or what they say that no document covers. This agent reads every recorded call, compares what was said with our own documents, and writes one report for the person who owns messaging. It covers what is landing, what is not, what the field says that the documents lack, and what customers are asking for. Each finding has quotes and a confidence level.

## In 2 minutes

The idea started as a simple register of every sales asset plus a weekly heat map of which assets showed up in call transcripts. It had two problems. Reps almost never name the asset ("the deck"), and a keyword search cannot see what is *missing*, which is where the best evidence usually is.

So it was rebuilt around **claims**, the individual messages inside each asset. An AI reader goes through each call, turn by turn, and logs every moment a claim is said, drifts, or is contradicted, and every moment someone says something no claim covers. **Two readers** read each call independently. What both find is high confidence. What only one finds goes to a third agent that rules on it. A person spot checks the ten most uncertain items each week.

Everything rolls up into one report: which types of assets are used at which buying stage, which messages land, which never get said, where reps drift from the documents, and what customers tell us about their goals, problems and renewal.

It was built and tested on fictional data first (a made up company and made up calls, with an answer key so it could be measured). On that data it found 81 to 96% of the known message uses, depending on the week and setting. It has not been tested on real calls yet. We are the early testers.

## In 10 minutes

Use the 2 minute version, then walk through [01-how-it-works.md](01-how-it-works.md) and one real example row. Close with three things that surprised the builder:

1. The pitch deck's headline was said by no rep. The practical messages (how supplier data actually gets collected) were the most said, and they lived in customer success documents, not the positioning.
2. Search tools turned out to be optional at this size. Letting Claude read the whole call beat a pipeline that searches first and then judges.
3. The hardest part was not the AI. It was deciding what question the report should answer, and that changed three times.

## Questions you will probably get

| Question | Short answer |
|---|---|
| Why not just use a conversation intelligence tool? | Those track messages you define in advance and train one by one. This starts from your own documents, reports what is said that none of them cover, and links messages to vehicles and stages. And not every team has one |
| Why not paste the calls into a chat? | That is roughly what one reader does. The difference is the claims table to match against, two independent readings, an adjudicator, a small answer key to measure against, and a weekly loop that improves the instructions |
| How accurate is it? | On fictional data it found 81 to 96% of the planted moments. On your data, you will measure it with your own small answer key |
| What does it cost? | Credits. Start with 2 or 3 calls and 5 assets. A ten call week at the first settings was about 800,000 tokens for the readers and adjudicator. See [05-models-and-credits.md](05-models-and-credits.md) |
| How long does setup take? | About eight short sessions over about two weeks, 8 to 11 hours. You can stop after session 4 with something useful. Those are estimates |
| Does it work in other languages? | Untested |
| Where does the data go? | The files stay on your machine. What each agent reads is sent to Claude to be processed, like any Claude Code work. Check your company's rules on customer data first |
| Did the builder or the AI build it? | The marketer made the product decisions: the audience, what to remove, what the question is, and the judgement calls on every review. Claude did the engineering and proposed options |
| What if our assets are slides? | Export them to text, one slide per section |
| What if we have no positioning document? | Use a messaging document or a pitch deck as the anchor, and say so in your company brief |
| What if the agent gets it wrong? | That is what the reviews are for. Every error becomes a rule in the spec |
