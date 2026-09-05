# Contributing

Thanks for helping keep this list useful. Read this before opening a PR — submissions that don't meet the criteria are closed without review.

## What belongs here

A project must meet **all** of these:

1. **Resilience is the core design.** The project must keep communication working under at least one of: internet shutdowns, censorship, infrastructure failure, disasters, off-grid operation, or intermittent/high-latency connectivity — by architecture, not as a feature or a marketing claim. Using encryption is not resilience; needing an always-on server disqualifies a tool from the off-grid sections.
2. **Open source with a working implementation.** OSI-approved license for software; open specifications qualify for hardware. Specs and protocols are welcome if they have at least one real implementation. Rare exceptions with non-OSI source-available licenses (e.g., Reticulum) are flagged explicitly in the entry.
3. **Alive or stable.** Meaningful activity (commits, releases, community) within the last 24 months, or mature software that is quiet because it is finished — still working and still used. Projects that go quiet *after* being listed are not removed; they are marked **Dormant** (see the removal policy below).
4. **Adopted.** Some evidence people actually use it: real deployments, distro/F-Droid packaging, an active community, or roughly 100+ stars. This list is not a launch platform for brand-new projects.
5. **Honest about security.** Entries must not claim a tool is anonymous, metadata-resistant, or safe for high-risk users without evidence. Name independent audits (auditor and year) where they exist; where none exists, the entry may say so. Known serious vulnerabilities must be mentioned.

Note: an encrypted messenger is not automatically resilient — otherwise this would become a directory of every chat app. Ask instead: does it still work when the internet is off, filtered, or the servers are gone? For general privacy-messenger coverage see the dedicated lists under *Other Related Lists*.

## What does not belong here

These are closed without review, regardless of technical merit:

- **Cryptocurrency- and token-dependent projects** — including otherwise-relevant mesh or connectivity projects whose operation depends on a token or payment chain (e.g., token-incentivized bandwidth networks).
- **AI tools and agent frameworks.**
- **Closed-source commercial products** and conventional VPN services.
- **Encrypted messengers that depend on centralized infrastructure** (Signal-style apps): good tools, wrong list.
- **Military-only technology.**
- **AI-generated ("vibe-coded") projects without demonstrated adoption** — a working demo is not adoption; see the criteria above.

## How to submit

- One project per pull request.
- Entry format: `- [Name](https://example.org/) - Short, factual description that starts with a capital letter and ends with punctuation.`
- Add the entry to the correct section, in alphabetical order.
- Do not add your project to the *Resilience at a Glance* matrix — it holds a small fixed set of representative examples, not every entry.
- If the project's main link is not its GitHub repository, add a mapping (or an `exempt` reason) in `.github/data/repos.json` so the status audit can monitor it — CI enforces this.
- In the PR description, explain **why resilience is core to the project's architecture**, what infrastructure it actually requires (servers, relays, gateways, subscriptions, licenses), and how it meets the criteria above. The PR template asks for this — PRs that skip it are closed.

## Removal policy

- Projects with no meaningful development activity for roughly 2 years, whose software still works, are marked **Dormant**.
- Dormant projects move to the **Graveyard** section when they stop working, archive their repository, shut down, or lose their domain (we keep the historical record).
- Projects whose security claims are disproven (a published break, a serious unfixed vulnerability) get the finding added to their entry immediately; removal is decided case by case.
- Links whose domains are squatted, hijacked, or repurposed for spam are removed or repointed to archived copies immediately. If you spot one, please open an issue, or a PR if issue creation is unavailable to you.
