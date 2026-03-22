# The Ptah Protocol

**Open world infrastructure for the AT Protocol.**

The Ptah Protocol is a set of [Lexicon](https://atproto.com/specs/lexicon) schemas that bring collaborative world-building, narrative provenance, and creative attribution to the [AT Protocol](https://atproto.com) network. It defines eight record types that let anyone create a world, inhabit it with characters, act inside it, accumulate history, and trace every contribution back to the person who made it.

The namespace is `world.ptah.*`. Experimental schemas are published to the network under `world.ptah.temp.*`.

**Status:** Active Development — Schema Complete

**Website:** [ptah.world](https://ptah.world)
**Account:** [@ptah.world](https://blacksky.community/profile/ptah.world)
**Contact:** protocol@ptah.world

---

## Documentation

- **[Getting Started](GETTING_STARTED.md)** — build your first world in five minutes
- **[Specification](SPECIFICATION.md)** — field-level reference for every record type
- **[Examples](EXAMPLES.md)** — four complete world record chains (Hamlet, Gatsby, Spades, tabletop RPG)
- **[Roadmap](ROADMAP.md)** — where the protocol is and where it's going

---

## Record Types

The protocol defines eight foundational record types plus a shared definitions file and a declaration companion record.

### World · `world.ptah.world`
The foundational record. Everything else references it. A world must exist before characters, events, or lore can exist inside it. Declares the world's name, creator, intellectual property origin, governance mode, and rendering hints.

### Character · `world.ptah.character`
A person, creature, or entity that exists inside a specific world. The character is not the user — the character is the world's inhabitant. Can be an original creation or an instance of a shared Role.

### Role · `world.ptah.role`
The template that sits between the World and the Character. A shared identity that multiple Character instances can embody. Hamlet is a Role — each performance of Hamlet is a Character instance. Governs instance policy and canonical reference.

### Action · `world.ptah.action`
The heartbeat of the protocol. Every time someone acts inside a world, they create one of these. Captures who acted, as which character, in which world, at which location, and what happened.

### Event · `world.ptah.event`
Where competition becomes history. A tournament, battle, gathering, or any occasion where characters compete or convene. Tracks participants, stakes, status, result, and witnesses. Witnesses are verifiable action records, not just a count.

### Lore · `world.ptah.lore`
The world's history book. What separates the protocol from a game or a social feed. Lore traces back through source references to the actions and events that generated it. The history is attributable, permanent, and verifiable.

### Contribution · `world.ptah.contribution`
The permission and attribution layer. Governs how someone who didn't create a world adds something to it. Carries an attribution chain — an array tracing every hand a contribution passed through. Provenance travels with the work.

### Location · `world.ptah.location`
A place inside a world. Gives events and actions an address. Locations nest infinitely via parent references and carry a depth index for efficient rendering without traversing the full hierarchy.

### Supporting schemas

- **Defs** · `world.ptah.defs` — Shared token definitions (source types, canonical status tiers) referenced across all record types.
- **Declaration** · `world.ptah.declaration` — A signaling record indicating that an account participates in the Ptah Protocol. One per account, fixed key. Used by AppViews for participant discovery.

---

## Design Principles

**Attribution is infrastructure, not metadata.** Every record carries a permanent, immutable link to its creator. The `authorshipRecord` field never changes, even if the record is contributed to, built on, or rendered a thousand different ways.

**The protocol records; clients render.** The schemas define the data. How that data is displayed — which canon tier to show, how to weight narrative significance, what visual style to use — belongs to the rendering layer. Multiple clients can read the same records and produce meaningfully different world experiences.

**Witnessing is presence, not endorsement.** A thousand witnesses do not make an event good. They make it witnessed. The distinction is preserved at every layer.

**Lore is rhetoric, not truth.** The protocol makes narrative attributable and permanent. It does not make narrative true. Any piece of lore can be traced back to its sources, but the interpretation belongs to the author.

---

## Schema Design Decisions

- **`knownValues` over `enum` everywhere.** Fields use open-ended known value sets rather than closed enumerations, allowing extensibility without breaking changes.
- **Consistent required fields.** Most records require who created it, what world it belongs to, when it was created, and what it's called. Deliberate exceptions: Action uses `actorDID` instead of `creatorDID`, Contribution uses `contributorDID`, Declaration requires only `createdAt`, and Action has no `name` field. Everything else is optional.
- **Typed flexible properties.** Freeform metadata (rendering hints, character properties, location properties) uses named object definitions with explicit optional fields rather than untyped key-value pairs.
- **String length limits.** Names: 640 bytes / 64 graphemes. Descriptions: 10,240 bytes / 1,024 graphemes. Lore content: 102,400 bytes / 10,000 graphemes. Byte-to-grapheme ratio approximately 10:1.
- **AT URI references throughout.** All cross-record references use the `at-uri` format, making every relationship in the record chain resolvable on the network.

---

## Network Publication

Experimental schemas are published as `com.atproto.lexicon.schema` records in the [@ptah.world](https://blacksky.community/profile/ptah.world) repository under the `world.ptah.temp.*` namespace.

Lexicon resolution is wired via DNS TXT records:
- `_lexicon.ptah.world` → production namespace (`world.ptah.*`)
- `_lexicon.temp.ptah.world` → experimental namespace (`world.ptah.temp.*`)

DID: `did:plc:l45z35sxxjuobp5q65a5vu22`
PDS: [Blacksky](https://blacksky.app)

---

## Intellectual Property Model

The protocol supports three source types for worlds and their contents:

- **Original IP** — created by the world originator, with full authorship control.
- **Public Domain** — derived from public domain source material, with the Role/Character instance split enabling multiple performances of shared identities.
- **Collaborative Commons** — created under a collaborative framework with shared governance.

The `controlType` field on characters (exclusive, open, delegated) and the `instancePolicy` field on roles (openInstance, approvedInstance, singleInstance) govern how creative control flows through the system.

---

## Repository Structure

```
ptah-protocol/
├── README.md
├── SPECIFICATION.md
├── GETTING_STARTED.md
├── EXAMPLES.md
├── ROADMAP.md
├── LICENSE
└── lexicons/
    ├── world.ptah.action.json
    ├── world.ptah.character.json
    ├── world.ptah.contribution.json
    ├── world.ptah.declaration.json
    ├── world.ptah.defs.json
    ├── world.ptah.event.json
    ├── world.ptah.location.json
    ├── world.ptah.lore.json
    ├── world.ptah.role.json
    └── world.ptah.world.json
```

---

## License

MIT OR Apache-2.0, at your discretion. Following the dual-license convention used by the AT Protocol reference implementation.

---

## About

The Ptah Protocol is created by [R. Michael Thomas](https://blacksky.community/profile/rmichaelthomas.com).

Named for Ptah, the Egyptian god of craftsmen and architects — the one who conceived the world in his heart and spoke it into existence. The protocol's three-letter hieroglyphic name maps to its architecture: 𓊪 (P) is the foundation layer, 𓏏 (T) is the record layer, 𓉔 (H) is the attribution chain.
