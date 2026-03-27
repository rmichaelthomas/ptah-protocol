# The Ptah Protocol

**Open infrastructure for creative authorship on the AT Protocol.**

The Ptah Protocol is a set of [Lexicon](https://atproto.com/specs/lexicon) schemas for the [AT Protocol](https://atproto.com) network. It defines fifteen record types that handle attribution, lineage, permissions, and history for creative work — from albums and franchise universes to competitive tournaments and collaborative campaigns. Create a world. Track who contributed what. Trace every sample, adaptation, and remix back to its source. Accumulate history that's permanent and verifiable.

The namespace is `world.ptah.*`. Production schemas are published and live on the ATProto network.

**Status:** Active Development — Schema Complete

**Website:** [ptah.world](https://ptah.world)
**Account:** [@ptah.world](https://blacksky.community/profile/ptah.world)
**Contact:** protocol@ptah.world

---

## Documentation

- **[Getting Started](GETTING_STARTED.md)** — build your first world in five minutes
- **[Specification](SPECIFICATION.md)** — field-level reference for every record type
- **[Examples](examples/)** — four complete world record chains (RENAISSANCE, MCU, Spades, tabletop RPG)
- **[Glossary](GLOSSARY.md)** — terms from protocol infrastructure, world-building, and competitive play
- **[Roadmap](ROADMAP.md)** — where the protocol is and where it's going

---

## Record Types

The protocol defines fifteen record types plus a shared definitions file.

### World · `world.ptah.world`
The foundational record. Everything else references it. A world must exist before characters, events, or logs can exist inside it. Declares the world's name, creator, intellectual property origin, governance mode, and rendering hints.

### Character · `world.ptah.character`
A person, creature, or entity that exists inside a specific world. The character is not the user — the character is the world's inhabitant. Can be an original creation or an instance of a shared Template.

### Template · `world.ptah.template`
A shared identity template that multiple characters can embody. The type, not the instance. Iron Man is a Template — Tony Stark is a Character instance of that Template. Governs instance policy and canonical reference.

### Action · `world.ptah.action`
The heartbeat of the protocol. Every time someone acts inside a world, they create one of these. Captures who acted, as which character, in which world, at which location, and what happened. Supports threading via parent action references.

### Event · `world.ptah.event`
A structured occurrence — competition, gathering, milestone, ceremony, or conflict. Tracks participants, stakes, status, result, and witnesses. An album release is an event. A tournament match is an event. A battle is an event. Witnesses are verifiable action records, not just a count.

### Log · `world.ptah.log`
The world's history book. What separates the protocol from a game or a social feed. Logs trace back through source references to the actions and events that generated them. The history is attributable, permanent, and verifiable. Supports a human-authored declaration flag.

### Origin · `world.ptah.origin`
The attribution and permission layer. Tracks who contributed what, under what terms, and with what role. Carries a structured attribution chain where each entry records the contributor's DID, role, and optional split percentage. Provenance travels with the work.

### Location · `world.ptah.location`
A place inside a world. Gives events and actions an address. Locations nest infinitely via parent references and carry a depth index for efficient rendering without traversing the full hierarchy.

### Collection · `world.ptah.collection`
Bundles multiple works together. An album, anthology, season, or any curated set of related works. Items are ordered sequentially, chronologically, or unordered.

### Cadence · `world.ptah.cadence`
Temporal orchestration for content delivery. Controls when and how works surface — release schedules, gated access, sequential unlocks, ritualized drops. Supports RRULE scheduling, audience tiering, unlock conditions, and multi-surface channel hints. The world's clock.

### Trace · `world.ptah.trace`
Tracks lineage between works. The paper trail from one work to another — cover, remix, adaptation, translation, sample, interpolation, response, sequel, spinoff, excerpt, remake, or fork. Includes clearance status.

### Usage · `world.ptah.usage`
Terms and permissions for a work. What's allowed, where, for how long, and under what conditions. Covers commercial use, derivatives, performance rights, attribution requirements, territories, and license type.

### Version · `world.ptah.version`
Edit history within a work. Tracks the evolution from draft to published to revised to final — every version, every change. Versions link to their predecessors and carry status (active, superseded, retracted, archived).

### Flax · `world.ptah.flax`
Signaling record indicating an account participates in the Ptah Protocol. One per account, fixed key `self`. Named for the twisted flax glyph (𓉔), the H in Ptah — the attribution chain thread. Used by AppViews for participant discovery.

### Supporting schemas

- **Defs** · `world.ptah.defs` — Shared token definitions (source types, canonical status tiers) referenced across all record types.

---

## Design Principles

**Attribution is infrastructure, not metadata.** Every record carries a permanent link to its creator. The creator's DID is immutable — it doesn't change even if the record is contributed to, built on, or rendered a thousand different ways.

**The protocol records; clients render.** The schemas define the data. How that data is displayed — which canon tier to show, how to weight narrative significance, what visual style to use — belongs to the rendering layer. Multiple clients can read the same records and produce meaningfully different world experiences.

**Witnessing is presence, not endorsement.** A thousand witnesses do not make an event good. They make it witnessed. The distinction is preserved at every layer.

**The log is rhetoric, not truth.** The protocol makes narrative attributable and permanent. It does not make narrative true. Any log entry can be traced back to its sources, but the interpretation belongs to the author.

---

## Schema Design Decisions

- **`knownValues` over `enum` everywhere.** Fields use open-ended known value sets rather than closed enumerations, allowing extensibility without breaking changes.
- **Consistent required fields.** Core records require a creator DID, a world reference, and a creation timestamp. Most also require a name or title. Everything else is optional.
- **Typed flexible properties.** Freeform metadata (rendering hints, character properties, location properties) uses named object definitions with explicit optional fields rather than untyped key-value pairs.
- **String length limits.** Names: 640 bytes / 64 graphemes. Descriptions: 10,240 bytes / 1,024 graphemes. Log content: 102,400 bytes / 10,000 graphemes. Byte-to-grapheme ratio approximately 10:1.
- **AT URI references throughout.** All cross-record references use the `at-uri` format, making every relationship in the record chain resolvable on the network.

---

## Network Publication

Production schemas are published as `com.atproto.lexicon.schema` records in the [@ptah.world](https://blacksky.community/profile/ptah.world) repository under the `world.ptah.*` namespace. All fifteen schemas are live and resolvable on the ATProto network.

Lexicon resolution is wired via DNS TXT record:
- `_lexicon.ptah.world` → `did=did:plc:l45z35sxxjuobp5q65a5vu22`

DID: `did:plc:l45z35sxxjuobp5q65a5vu22`
PDS: [Blacksky](https://blacksky.app)

---

## Intellectual Property Model

The protocol supports three source types for worlds and their contents:

- **Original IP** — created by the world originator, with full authorship control.
- **Public Domain** — derived from public domain source material, with the Template/Character instance split enabling multiple performances of shared identities.
- **Collaborative Commons** — created under a collaborative framework with shared governance.

The `controlType` field on characters (exclusive, open, contested) and the `instancePolicy` field on templates (open, restricted, closed) govern how creative control flows through the system.

---

## Repository Structure

```
ptah-protocol/
├── README.md
├── SPECIFICATION.md
├── GETTING_STARTED.md
├── examples/
│   ├── README.md
│   ├── renaissance.md
│   ├── mcu.md
│   ├── blacksky-spades.md
│   └── shattered-reach.md
├── GLOSSARY.md
├── ROADMAP.md
├── LICENSE
└── lexicons/
    ├── world.ptah.action.json
    ├── world.ptah.cadence.json
    ├── world.ptah.character.json
    ├── world.ptah.collection.json
    ├── world.ptah.defs.json
    ├── world.ptah.event.json
    ├── world.ptah.flax.json
    ├── world.ptah.location.json
    ├── world.ptah.log.json
    ├── world.ptah.origin.json
    ├── world.ptah.template.json
    ├── world.ptah.trace.json
    ├── world.ptah.usage.json
    ├── world.ptah.version.json
    └── world.ptah.world.json
```

---

## License

MIT OR Apache-2.0, at your discretion. Following the dual-license convention used by the AT Protocol reference implementation.

---

## About

The Ptah Protocol is created by [R. Michael Thomas](https://blacksky.community/profile/rmichaelthomas.com).

Named for Ptah, the Egyptian god of craftsmen and architects — the one who conceived the world in his heart and spoke it into existence. The protocol's three-letter hieroglyphic name maps to its architecture: 𓊪 (P) is the foundation layer, 𓏏 (T) is the record layer, 𓉔 (H) is the attribution chain.
