# Example World Record Chains

Four example worlds demonstrating how the Ptah Protocol's fourteen record types connect, reference each other via AT URIs, and express different kinds of creative worlds.

For field-level details, see the [Specification](../SPECIFICATION.md). For a hands-on walkthrough, see [Getting Started](../GETTING_STARTED.md).

---

## AT URI Convention

All AT URIs follow the standard ATProto format:

```
at://{DID}/{NSID}/{rkey}
```

Where:
- `{DID}` is a placeholder Decentralized Identifier (e.g., `did:plc:renaissance01`)
- `{NSID}` is the Namespaced Identifier for the record type (e.g., `world.ptah.world`)
- `{rkey}` is a unique record key (e.g., `renaissance`)

Placeholder DIDs are human-readable for clarity. On a live network, DIDs are opaque alphanumeric strings. The structure is identical.

---

## Worlds

| World | Type | File | Tests |
|---|---|---|---|
| **RENAISSANCE** | Music, original IP | [renaissance.md](renaissance.md) | Complex attribution chains, sampling lineage, all 14 record types, commercial licensing |
| **MCU** | Franchise, original IP | [mcu.md](mcu.md) | Template/Instance split at scale, corporate attribution, adaptation lineage, phase-based versioning |
| **Blacksky Spades** | Structured competition | [blacksky-spades.md](blacksky-spades.md) | Competition events, scoring, competitive witnesses, season records |
| **The Shattered Reach** | Collaborative RPG campaign | [shattered-reach.md](shattered-reach.md) | GM/player dynamics, character progression, sessions as events, campaign journals as log entries |

---

## What All Four Worlds Demonstrate Together

The same fourteen record types express all four worlds without modification. Music production. Franchise IP. Competitive card games. Tabletop RPG campaigns. The protocol doesn't care what kind of world you're building. It cares that authorship travels, history is verifiable, and every contribution traces back to the person who made it.

The schema holds all four worlds. It will hold yours.
