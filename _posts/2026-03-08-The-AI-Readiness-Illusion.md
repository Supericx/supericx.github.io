---
layout: post
title: The Foundation Problem
description: Why 95% of enterprise AI projects fail, and why the fix has nothing to do with better models.
---

I've been sitting in on a lot of enterprise AI conversations lately. The energy is always the same. Someone senior watched a demo, got excited, and now there's a mandate: we need to be doing AI. A task force gets assembled. Vendors get called. A proof-of-concept spins up. The demo goes well. Everyone claps.

Then six months pass, and the project is quietly shelved. Or it launches and nobody uses it. Or it works in the meeting room but falls apart the moment real data touches it.

I used to think this was a technology problem. Models hallucinate. Context windows are too short. Inference is expensive. All true. But the more I see these projects up close, the less I think the models are the issue.

MIT recently put out a number that's been rattling around in my head: 95% of generative AI business initiatives fail to produce meaningful revenue impact. RAND says over 80% of AI projects fail overall—double the rate of regular IT projects. When I first read that, it felt exaggerated. Now it feels about right.

The pattern I keep seeing is this: companies try to build something smart on top of something broken.

Take internal documents. Every company I've worked with has the same problem. Fifteen years of accumulated files, spread across SharePoint, Confluence, Google Drive, a couple legacy databases, and at least one person's desktop. Half are duplicates. A third are outdated. Nobody's sure which version of the expense policy is current, because both the 2022 and 2025 versions are sitting in the same folder, unmarked.

This is fine when humans run the show. People develop this incredible implicit knowledge—they know who to ask, which folder to trust, which document to ignore even though it shows up first in search. The whole thing holds together through tribal knowledge and hallway conversations.

But AI doesn't have hallway conversations.

You point a RAG pipeline at this mess, and it'll retrieve the wrong expense policy with absolute confidence. Not because the retrieval algorithm is bad, but because nothing in the system distinguishes current from deprecated. The metadata isn't there. The versioning isn't there. So you end up with answers that are well-structured, articulate, and wrong. Which is arguably worse than no answer at all, because people trust them.

I heard someone at Microsoft say something that stuck: "Without a solid, curated data stack, you won't have good AI." This was their internal team, talking about what they did before rolling Copilot out across the company. They didn't start with the AI. They started with the plumbing—consolidating data sources, deduplicating, enforcing access controls, building metadata. The boring stuff. The stuff that doesn't make a good demo.

And this is where it gets hard. Not technically hard. Organizationally hard. Cleaning up data means getting departments to agree on a single source of truth. It means asking people to give up the private spreadsheets they've maintained for years. It means touching systems that everyone has silently agreed to never touch. I've watched this process stall more over turf wars than technical limitations.

The same thing applies to workflows. McKinsey found that companies seeing the highest returns from AI were three times more likely to have restructured their core processes first—not just added AI on top. This tracks with what I've observed. Most business processes have these pockets of ambiguity that humans navigate instinctively but machines can't parse. When should this get escalated? It depends. Who approves exceptions? Whoever's around. What counts as urgent? You kind of know it when you see it.

These "you know it when you see it" moments are everywhere in enterprise operations. They work because experienced people fill in the gaps. But you can't automate a gap. You have to close it first—make the implicit rules explicit, turn judgment calls into decision trees. Only then can you hand it to an agent.

Here's the number that really gets me: only 1% of enterprise leaders consider their organization mature in AI deployment. One percent. And 92% of companies are planning to increase AI spending. That's a staggering gap between ambition and readiness, and I don't think shipping better models closes it.

There's a historical parallel I find useful. When factories first got electric power, they literally just replaced the steam engine with an electric motor and kept everything else the same. Same layout, same drive shaft, same workflow. It took a full generation to realize that electricity changed the physics of the whole thing—you could put a motor on every machine, redesign the floor plan, rethink production from scratch. The technology arrived decades before the organizational thinking caught up.

That feels like where we are. The models are already remarkable. But most organizations are still wiring the electric motor into the steam engine's spot and wondering why nothing feels different.

I don't have a neat conclusion for this. I just keep noticing that the companies making real progress with AI aren't the ones chasing the latest model release. They're the ones doing the deeply unglamorous work of getting their house in order first. Fixing the data. Rewriting the processes. Having the uncomfortable conversations about who owns what.

It's not fun. It doesn't look good on a slide. But it might be the only thing that actually matters.
