# Roadmap

The Ptah Protocol is in active development. Here's where things stand and where they're going.

---

## Now — Schema Complete

**Done:**
- Fourteen record types defined and formalized as Lexicon JSON
- Shared definitions file (world.ptah.defs)
- Two complete example world chains (Hamlet + Freedmen Universe) pressure-tested against seven failure modes
- Production schemas published to the ATProto network under `world.ptah.*`
- Schemas promoted from `world.ptah.temp.*` to production `world.ptah.*` namespace
- Domain, DNS, Blacksky account, and website live
- GitHub repository public with full documentation

**In progress:**
- Community engagement via ATmosphereConf 2026 and ATProto developer ecosystem

---

## Next — AppView & First Client

The schemas define the data. The AppView is what makes it queryable and navigable.

**Planned:**
- AppView architecture design — namespace-scoped indexing of `world.ptah.*` records from the ATProto firehose
- First rendering client — a way to browse worlds, characters, and accumulated history
- Conversation brief for ecosystem partners and early collaborators
- Schema refinement based on ATmosphereConf learnings and early builder feedback

**Open questions being explored:**
- AppView hosting model — lightweight namespace-scoped indexer vs. full network relay
- Rendering architecture — single reference client vs. multi-client ecosystem from day one
- Integration patterns with existing ATProto infrastructure (Smoke Signal events, location data, feeds)

---

## Later — V2 Protocol Extensions

Identified during pressure testing as real needs that don't belong in v1:

- **Dispute Record** — a formal mechanism for contesting canon, attribution, or governance decisions within a world
- **Canon Branching Vocabulary** — structured language for how a world's canon can fork, merge, or diverge
- **World Governance Document** — the actual constitution that `governanceMode: constitutional` points to
- **Geographic Analytics** — world-level spatial data derived from Location records
- **Cross-World References** — how characters, logs, or events can span multiple worlds

---

## Principles

The roadmap follows a few commitments:

**Schemas shipped. Now build the view.** The record types are defined and published to the ATProto network under the production `world.ptah.*` namespace. The priority has shifted to building the AppView and rendering layer that makes this data queryable and navigable.

**Open by default.** The protocol is MIT/Apache-2.0 dual-licensed. Anyone can build on it. The roadmap is public. Feedback shapes direction.

**Don't overpromise.** Items move from "later" to "next" when there's a real reason and real capacity, not when it sounds impressive on a roadmap.

---

## Get Involved

This is early. If you're building on ATProto and any of this intersects with your work, reach out.

- **GitHub:** [github.com/rmichaelthomas/ptah-protocol](https://github.com/rmichaelthomas/ptah-protocol)
- **Blacksky:** [@ptah.world](https://blacksky.community/profile/ptah.world)
- **Email:** protocol@ptah.world
