# FestFixaren

**Plan a Swedish bachelorette or bachelor party without the group chat chaos.**

**Live at [festfixaren.fredskvist.com](https://festfixaren.fredskvist.com)** · Free, no account needed · In Swedish

<img width="1454" height="1311" alt="Skärmavbild 2026-07-13 kl  10 47 53" src="https://github.com/user-attachments/assets/36569d44-9641-43f7-a25c-8565bc426ebc" />## The problem

Every möhippa (bachelorette) and svensexa (bachelor party) starts the same way: a group chat with twenty ideas, forty unread messages and zero decisions. Someone has to chase everyone for dates, keep the plan secret from the guest of honor, coordinate the day and then untangle who owes whom afterwards.

FestFixaren replaces that with one shared page.

## What it does

- **Date voting.** The group votes on dates that work. The best one wins. No more chasing people one by one.
- **A shareable program page.** Schedule, meeting points and activities on one link, with proper link previews when shared in chats. Visible to guests, hidden from the guest of honor.
- **Expense splitting via Swish.** One or two people pay up front, the app calculates who swishes whom afterwards. No receipts, no spreadsheet.
- **Post-party reviews.** Guests rate the day afterwards. Names and cities are only ever shown with active consent, and nothing is published without moderation.
- **City guides.** Curated activity and restaurant tips for Gothenburg and Stockholm, by party type.

## How it's built

React 18 + Vite frontend, Cloudflare Pages Functions backend, Cloudflare D1 (SQLite) database. Fully serverless, deploys automatically from this repo.

A few decisions worth mentioning:

- **Privacy by design.** No accounts, no tracking. Rate limiting hashes visitor IPs (SHA-256, salted per party) before anything touches the database, so raw IPs are never stored. Review names require explicit opt-in consent, and consent alone is not enough for publication: an approval step gates the public feed.
- **Token-based access.** Organizers and guests get capability URLs with 128-bit random tokens instead of logins. Less friction for a product people use once, smaller attack surface.
- **Staging before production.** A separate branch and D1 database mirror production. Schema migrations always run before code deploys, never after.

## How it was built

FestFixaren is developed with AI coding agents (Claude Code) under human direction, with the discipline you'd expect from a production system:

- Adversarial code reviews run in separate agent sessions that haven't seen the code being written. Findings are triaged by severity and fixed before anything ships.
- The production database is never touched by an agent. All production migrations are run manually, by a human, after staging verification.
- Every release path: build on staging branch → independent review → staging deploy and manual test → production migration → merge to main.

The interesting part isn't that AI wrote code. It's that the process around it (reviews, staging, migration ordering, least-privilege rules for agents) is what made it safe to ship fast.

## Roadmap

- Review approval flow for organizers
- More cities and party types
- Partner-tagged recommendations (structure in place, intentionally unused until there's traffic to justify it)

## About this repo

The application source lives in a private repository. This repo is the public showcase: product overview, screenshots and documentation. Curious about the code or the process? Get in touch.

## Contact

Built by Dennis Fredin. Questions, feedback or party disasters averted: hej@fredskvist.com
