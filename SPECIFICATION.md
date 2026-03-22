# Ptah Protocol Specification

**Version:** 0.1.0 (experimental)
**Namespace:** `world.ptah.*` (production) · `world.ptah.temp.*` (experimental)
**Status:** Experimental schemas published. Production promotion pending.

This document is the field-level technical reference for the Ptah Protocol. It covers every record type, every field, types, constraints, and how records reference each other.

For a conceptual overview, see the [README](README.md). For a hands-on walkthrough, see the [Getting Started guide](GETTING_STARTED.md).

---

## Conventions

**Required fields** are marked with ✦. Everything else is optional.

**AT URI references** follow the format `at://{DID}/{NSID}/{rkey}` and point to a specific record on the network.

**DID fields** store a Decentralized Identifier — the permanent, portable identity of a user on ATProto.

**String limits** use a ~10:1 byte-to-grapheme ratio:
- Names/titles: 640 bytes / 64 graphemes
- Descriptions and medium text: 2,560 bytes / 256 graphemes
- Long text (stakes, results, descriptions): 10,240 bytes / 1,024 graphemes
- Action content: 30,720 bytes / 3,000 graphemes
- Lore content: 102,400 bytes / 10,000 graphemes

**Categorical fields** use `knownValues` (open sets), not `enum` (closed sets). Clients must handle unknown values gracefully. New values can be added without breaking the schema.

**Record keys** use `tid` (timestamp-based identifier) for all records except Declaration, which uses the literal key `self`.

---

## Shared Definitions · `world.ptah.defs`

Reusable tokens referenced across multiple record types.

### Source Types

| Token | Meaning |
|---|---|
| `sourceTypeOriginalIP` | Created by the world originator with full authorship control |
| `sourceTypePublicDomain` | Derived from public domain source material |
| `sourceTypeCollaborativeCommons` | Created under a collaborative framework with shared governance |

### Canonical Status Tiers

| Token | Meaning |
|---|---|
| `canonicalStatusOfficial` | Designated as official canon by the world originator |
| `canonicalStatusCommunity` | Accepted by community consensus but not originator-designated |
| `canonicalStatusApocryphal` | Exists in the record but outside accepted canon |

These tokens are referenced as fully-qualified strings in `knownValues` arrays, e.g. `"world.ptah.defs#canonicalStatusOfficial"`.

---

## World · `world.ptah.world`

The foundational record. Everything else references it. A world must exist before characters, events, or lore can exist inside it.

| Field | Type | Required | Description |
|---|---|---|---|
| `name` | string | ✦ | What the world is called. Max 640 bytes / 64 graphemes. |
| `creatorDID` | string (did) | ✦ | Permanent identity of whoever seeded this world. |
| `createdAt` | string (datetime) | ✦ | Timestamp of creation. |
| `description` | string | | What kind of world this is. Max 10,240 bytes / 1,024 graphemes. |
| `sourceType` | string | | `knownValues`: `sourceTypeOriginalIP`, `sourceTypePublicDomain`, `sourceTypeCollaborativeCommons` (fully-qualified defs tokens). |
| `sourceReference` | string | | If public domain, the specific source material. Max 10,240 bytes / 1,024 graphemes. |
| `governanceMode` | string | | `sandbox` (anything goes), `governed` (originator rules), or `constitutional` (community governance). |
| `canonicalStatus` | string | | References `world.ptah.defs#canonicalStatus*` tokens. |
| `renderingHints` | ref → `#renderingHints` | | Metadata for visual rendering layers. See below. |

### renderingHints object

| Field | Type | Description |
|---|---|---|
| `tone` | string | Narrative tone. Max 2,560 bytes / 256 graphemes. |
| `era` | string | Time period. Max 2,560 bytes / 256 graphemes. |
| `genre` | string | Genre classification. Max 2,560 bytes / 256 graphemes. |
| `aesthetic` | string | Visual character. Max 2,560 bytes / 256 graphemes. |

---

## Character · `world.ptah.character`

A person, creature, or entity that exists inside a specific world. The character is not the user — the character is the world's inhabitant.

| Field | Type | Required | Description |
|---|---|---|---|
| `name` | string | ✦ | What the character is called. Max 640 bytes / 64 graphemes. |
| `creatorDID` | string (did) | ✦ | Who created this character. |
| `worldReference` | string (at-uri) | ✦ | The world this character belongs to. |
| `createdAt` | string (datetime) | ✦ | Timestamp. |
| `roleReference` | string (at-uri) | | If present, the Role this character is an instance of. |
| `description` | string | | Who this character is. Max 10,240 bytes / 1,024 graphemes. |
| `properties` | ref → `#characterProperties` | | Flexible fields. See below. |
| `originType` | string | | `knownValues`: `sourceTypeOriginalIP`, `sourceTypePublicDomain` (defs tokens), `contributed`. |
| `sourceReference` | string | | Source material for public domain characters. Max 10,240 bytes / 1,024 graphemes. |
| `controlType` | string | | `exclusive` (one DID controls), `open` (anyone can act as), or `delegated` (specific DIDs granted permission). |
| `authorshipRecord` | string (did) | | Permanent provenance link. Never changes. |
| `canonicalStatus` | string | | References `world.ptah.defs#canonicalStatus*` tokens. |

### characterProperties object

| Field | Type | Description |
|---|---|---|
| `species` | string | Species or kind. Max 640 bytes / 64 graphemes. |
| `age` | string | Age or age range. Max 640 bytes / 64 graphemes. |
| `affiliation` | string | Faction, group, or allegiance. Max 640 bytes / 64 graphemes. |
| `abilities` | string | Capabilities or powers. Max 2,560 bytes / 256 graphemes. |
| `role` | string | Narrative function in the world. Max 640 bytes / 64 graphemes. |

---

## Role · `world.ptah.role`

A shared identity template. Multiple Character instances can embody one Role. Hamlet is a Role — each performance of Hamlet is a Character instance.

| Field | Type | Required | Description |
|---|---|---|---|
| `name` | string | ✦ | What this role is called. Max 640 bytes / 64 graphemes. |
| `creatorDID` | string (did) | ✦ | Who defined this role. |
| `worldReference` | string (at-uri) | ✦ | Which world this role exists in. |
| `createdAt` | string (datetime) | ✦ | Timestamp. |
| `description` | string | | Narrative function and archetypal weight. Max 10,240 bytes / 1,024 graphemes. |
| `sourceType` | string | | `knownValues`: `sourceTypeOriginalIP`, `sourceTypePublicDomain` (defs tokens). |
| `sourceReference` | string | | Source material if public domain. Max 10,240 bytes / 1,024 graphemes. |
| `canonicalCharacterReference` | string (at-uri) | | The single Character designated as the authoritative expression of this role. |
| `canonicalReferencePolicy` | string | | `fixed` (locked forever), `updatable` (originator can reassign), or `community` (follows consensus). |
| `instancePolicy` | string | | `openInstance` (anyone can create instances), `approvedInstance` (requires approval), or `singleInstance` (one canonical instance only). |
| `authorshipRecord` | string (did) | | Permanent provenance link. |
| `canonicalStatus` | string | | References `world.ptah.defs#canonicalStatus*` tokens. |

---

## Action · `world.ptah.action`

The heartbeat. Every time someone acts inside a world, they create one of these.

| Field | Type | Required | Description |
|---|---|---|---|
| `actorDID` | string (did) | ✦ | Who performed the action. The person behind the character. |
| `worldReference` | string (at-uri) | ✦ | Which world this action happened in. |
| `createdAt` | string (datetime) | ✦ | Timestamp. |
| `characterReference` | string (at-uri) | | The character performing the action. |
| `actionType` | string | | `knownValues`: `movement`, `speech`, `conflict`, `creation`, `witness`. Max 640 bytes / 64 graphemes. |
| `content` | string | | What happened. Max 30,720 bytes / 3,000 graphemes. |
| `locationReference` | string (at-uri) | | Where the action took place. |
| `targetReference` | string (at-uri) | | If directed at another character or object. |
| `visibility` | string | | `knownValues`: `canon`, `community`, `experimental`. |
| `narrativeWeight` | integer | | Optional importance scoring hook. Minimum 0. Null by default. Populated by AppView or originator when needed. |

Note: Action uses `actorDID` instead of `creatorDID` — the actor is the person performing, not abstractly "creating."

---

## Event · `world.ptah.event`

Where competition becomes history. A tournament, battle, gathering, or any occasion where characters compete or convene.

| Field | Type | Required | Description |
|---|---|---|---|
| `name` | string | ✦ | What the event is called. Max 640 bytes / 64 graphemes. |
| `creatorDID` | string (did) | ✦ | Who organized this event. |
| `worldReference` | string (at-uri) | ✦ | Which world this event belongs to. |
| `createdAt` | string (datetime) | ✦ | Timestamp of event creation. |
| `eventType` | string | | `knownValues`: `tournament`, `battle`, `gathering`, `contest`, `ritual`. Max 640 bytes / 64 graphemes. |
| `format` | string | | Competitive or structural format. `knownValues`: `bracket`, `roundRobin`, `openChallenge`, `singleElimination`. Max 640 bytes / 64 graphemes. |
| `participants` | array of string (at-uri) | | Character records participating. |
| `stakes` | string | | What's at stake. Max 10,240 bytes / 1,024 graphemes. |
| `status` | string | | `knownValues`: `upcoming`, `active`, `completed`. |
| `result` | string | | What happened. Populated when status moves to completed. Max 10,240 bytes / 1,024 graphemes. |
| `witnesses` | array of string (at-uri) | | Action records that serve as witness attestations. Not a count — verifiable records. |
| `locationReference` | string (at-uri) | | Where the event takes place. |
| `loreStatus` | string | | Narrative standing of this event. `knownValues`: `canonicalStatusOfficial`, `canonicalStatusCommunity` (defs tokens), `pending`. |
| `completedAt` | string (datetime) | | Timestamp of when the event concluded. |

---

## Lore · `world.ptah.lore`

The world's history book. What separates the protocol from a game or a social feed. Lore traces back through source references to the actions and events that generated it.

| Field | Type | Required | Description |
|---|---|---|---|
| `title` | string | ✦ | What this piece of history is called. Max 640 bytes / 64 graphemes. |
| `creatorDID` | string (did) | ✦ | Who authored this lore entry. |
| `worldReference` | string (at-uri) | ✦ | Which world this lore belongs to. |
| `createdAt` | string (datetime) | ✦ | Timestamp. |
| `content` | string | | The actual narrative. Max 102,400 bytes / 10,000 graphemes. |
| `sourceReferences` | array of string (at-uri) | | Action and Event records this lore was generated from. The field that makes history verifiable. |
| `characters` | array of string (at-uri) | | Character records involved. |
| `timelinePosition` | string | | Where this sits in the world's chronology. Max 2,560 bytes / 256 graphemes. |
| `canonicalStatus` | string | | References `world.ptah.defs#canonicalStatus*` tokens. |
| `authorshipRecord` | string (did) | | Permanent provenance link. |
| `contributionType` | string | | `knownValues`: `originator`, `community`. Both valid. Both attributed differently. |

Note: Lore uses `title` instead of `name` — lore entries are narrative texts, not entities.

---

## Contribution · `world.ptah.contribution`

The permission and attribution layer. Governs how someone who didn't create a world adds to it.

| Field | Type | Required | Description |
|---|---|---|---|
| `contributorDID` | string (did) | ✦ | Who is making the contribution. |
| `worldReference` | string (at-uri) | ✦ | Which world they're contributing to. |
| `createdAt` | string (datetime) | ✦ | Timestamp. |
| `contributionType` | string | | `knownValues`: `character`, `role`, `action`, `event`, `lore`, `location`. Max 640 bytes / 64 graphemes. |
| `recordReference` | string (at-uri) | | The actual record being contributed. |
| `originatorApproval` | string | | `knownValues`: `approved`, `preApproved`, `communityCanon`. |
| `canonicalStatus` | string | | References `world.ptah.defs#canonicalStatus*` tokens. |
| `attributionChain` | array of string (at-uri) | | AT URIs tracing every hand a contribution passed through. Provenance travels with the work. |
| `publicDomainCompliance` | boolean | | Whether this contribution complies with public domain source terms. |

Note: Contribution uses `contributorDID` instead of `creatorDID` — the contributor is the person adding, distinct from the world originator.

---

## Location · `world.ptah.location`

A place inside a world. Gives events and actions an address. Locations nest infinitely via parent references.

| Field | Type | Required | Description |
|---|---|---|---|
| `name` | string | ✦ | What this place is called. Max 640 bytes / 64 graphemes. |
| `creatorDID` | string (did) | ✦ | Who named and defined this place. |
| `worldReference` | string (at-uri) | ✦ | Which world this location exists in. |
| `createdAt` | string (datetime) | ✦ | Timestamp. |
| `description` | string | | What kind of place. Max 10,240 bytes / 1,024 graphemes. |
| `locationType` | string | | `knownValues`: `city`, `region`, `building`, `territory`, `landmark`, `vessel`, `abstractSpace`. Max 640 bytes / 64 graphemes. |
| `parentLocation` | string (at-uri) | | If this location exists inside a larger one. Enables infinite nesting. |
| `depthIndex` | integer | | How deep in the geographic hierarchy. Minimum 0. World-level=0, continent=1, country=2, city=3, etc. |
| `properties` | ref → `#locationProperties` | | Flexible fields. See below. |
| `authorshipRecord` | string (did) | | Permanent provenance link. |
| `canonicalStatus` | string | | References `world.ptah.defs#canonicalStatus*` tokens. |

### locationProperties object

| Field | Type | Description |
|---|---|---|
| `climate` | string | Environmental conditions. Max 2,560 bytes / 256 graphemes. |
| `population` | string | Size or density. Max 2,560 bytes / 256 graphemes. |
| `controllingFaction` | string | Who controls this place. Max 2,560 bytes / 256 graphemes. |
| `notableHistory` | string | Significant events tied to this location. Max 10,240 bytes / 1,024 graphemes. |

---

## Declaration · `world.ptah.declaration`

A signaling record indicating an account participates in the Ptah Protocol. One per account. Used by AppViews for participant discovery.

| Field | Type | Required | Description |
|---|---|---|---|
| `createdAt` | string (datetime) | ✦ | When this account declared participation. |
| `displayName` | string | | How this participant wants to be identified in Ptah contexts. Max 640 bytes / 64 graphemes. |
| `description` | string | | What this participant does in the ecosystem. Max 2,560 bytes / 256 graphemes. |

**Record key:** `self` (literal, singleton — one per account).

No `creatorDID` field. The account's DID is implicit from the repository — the AT URI itself (`at://{DID}/world.ptah.declaration/self`) identifies the account.

---

## How Records Reference Each Other

The dependency chain:

```
World
├── Role (references World)
│   └── Character (references Role + World)
├── Character (references World, optionally Role)
├── Location (references World, optionally parent Location)
├── Action (references World, Character, optionally Location)
├── Event (references World, Location, Characters as participants, Actions as witnesses)
├── Lore (references World, Actions + Events as sources, Characters)
└── Contribution (references World + any record being contributed)
```

A World must exist first. Everything else references it via AT URI. Records reference each other laterally — an Action points to a Character, an Event points to a Location, Lore points to the Actions and Events that generated it. The entire graph is traversable from any node.

---

## Network Resolution

When ATProto software encounters a `world.ptah.*` NSID:

1. Read the domain from the NSID → `ptah.world`
2. Look up `_lexicon.ptah.world` TXT record → returns DID
3. Fetch `com.atproto.lexicon.schema` record from that DID's repository
4. The schema definition is returned

**Production DNS:** `_lexicon.ptah.world` → `did=did:plc:l45z35sxxjuobp5q65a5vu22`
**Experimental DNS:** `_lexicon.temp.ptah.world` → `did=did:plc:l45z35sxxjuobp5q65a5vu22`
**PDS:** Blacksky (`blacksky.app`)
