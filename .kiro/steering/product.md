# Product: Voter Assistant

## What it is
A multilingual AI voter assistant that lives inside the chat apps people already use
(Telegram, WhatsApp, and a web chat). It helps citizens go from "I want to vote" to
polling day without confusing portals, long queues, or language barriers.

Built for Nigeria first, designed for anywhere: each country is a "country pack"
(languages, election body links, FAQs, key dates) that can be added without code changes.

## The problem
In 2023 the founder registered to vote but never collected his voter's card. Not because
of apathy or money, but because of friction. Millions of eligible voters drop off at the
same point: they don't know their card status, where to collect it, or where their
polling unit is, and the official information is not in the language they speak.

## Who it is for
- First-time and young voters who live on their phones
- Voters more comfortable in Pidgin, Yorùbá, Hausa or Igbo than English
- Election bodies who want a cheaper, wider channel to reach voters

## Core jobs (MVP)
1. Pick a language, and switch language at any time mid-conversation
2. Check voter card (PVC) status
3. Find the card collection centre and polling unit, with a map link
4. Set reminders (card collection, election day)
5. Answer voter questions using only official information from the country pack

## Product principles
- **Nonpartisan, always.** Never recommend, rank, or comment on candidates or parties.
  Questions about who to vote for get a polite, neutral decline.
- **Grounded, never invented.** Answers come only from the country pack's official
  content. If the answer is not there, say so and link the official source.
- **Honest about data.** There is no public INEC API. Status lookups use clearly
  labelled sample data in the demo, and always link to the official INEC portal.
- **Privacy first.** Never ask for or store BVN, NIN, biometrics or passwords. Store the
  minimum needed for reminders, and hash phone numbers / chat IDs.
- **Short and warm.** Chat-sized replies, plain language, no jargon.

## Country packs
- `ng` Nigeria (first): English, Nigerian Pidgin, Yorùbá, Hausa, Igbo
- `ke` Kenya (second, to prove portability): English, Swahili
