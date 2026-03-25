# Ptah Protocol Specification

**Version:** 1.0.0
**Namespace:** `world.ptah.*`
**Status:** Production schemas published and live on the ATProto network.

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
- Log content: 102,400 bytes / 10,000 graphemes

**Categorical fields** use `knownValues` (open sets), not `enum` (closed sets). Clients must handle unknown values gracefully. New values can be added without breaking the schema.

**Record keys** use `tid` (timestamp-based identifier) for all records except Flax, which uses the literal key `self`.

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

The foundational record. Everything else references it. A world must exist before characters, events, or logs can exist inside it.

| Field | Type | Required | Description |
|---|---|---|---|
| `name` | string | ✦ | What the world is called. Max 640 bytes / 64 graphemes. |
| `creatorDID` | string (did) | ✦ | Permanent identity of whoever seeded this world. |
| `createdAt` | string (datetime) | ✦ | Timestamp of creation. |
| `description` | string | | What kind of world this is. Max 10,240 bytes / 1,024 graphemes. |
| `sourceType` | string | | `knownValues`: `sourceTypeOriginalIP`, `sourceTypePublicDomain`, `sourceTypeCollaborativeCommons` (fully-qualified defs tokens). |
| `sourceReference` | string | | If public domain, the specific source material. Max 2,560 bytes / 256 graphemes. |
| `governanceMode` | string | | `knownValues`: `sandbox` (anything goes), `governed` (originator rules), or `constitutional` (community governance). |
| `canonicalStatus` | string | | References `world.ptah.defs#canonicalStatus*` tokens. |
| `coverImage` | blob | | Cover image for the world. Accepts PNG, JPEG, WebP. Max 1 MB. |
| `renderingHints` | ref → `#renderingHints` | | Metadata for visual rendering layers. See below. |

### renderingHints object

| Field | Type | Description |
|---|---|---|
| `tone` | string | Narrative tone. Max 640 bytes / 64 graphemes. |
| `era` | string | Time period. Max 640 bytes / 64 graphemes. |
| `genre` | string | Genre classification. Max 640 bytes / 64 graphemes. |
| `aesthetic` | string | Visual character. Max 640 bytes / 64 graphemes. |

---

## Character · `world.ptah.character`

A person, creature, or entity that exists inside a specific world. The character is not the user — the character is the world's inhabitant.

| Field | Type | Required | Description |
|---|---|---|---|
| `name` | string | ✦ | What the character is called. Max 640 bytes / 64 graphemes. |
| `creatorDID` | string (did) | ✦ | Who created this character. |
| `worldReference` | string (at-uri) | ✦ | The world this character belongs to. |
| `createdAt` | string (datetime) | ✦ | Timestamp. |
| `templateReference` | string (at-uri) | | If present, the Template this character is an instance of. |
| `description` | string | | Who this character is. Max 10,240 bytes / 1,024 graphemes. |
| `characterProperties` | ref → `#characterProperties` | | Flexible fields. See below. |
| `originType` | string | | `knownValues`: `originalIP`, `publicDomain`, `collaborativeCommons`. |
| `controlType` | string | | `knownValues`: `exclusive` (creator only), `open` (anyone can act as), or `contested` (multiple claimants). |
| `authorshipRecord` | string (did) | | The DID of the original author if different from creator. |
| `avatar` | blob | | Avatar image for the character. Accepts PNG, JPEG, WebP. Max 1 MB. |
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

## Template · `world.ptah.template`

A shared identity template that multiple characters can embody. The type, not the instance. Hamlet is a Template — each performance of Hamlet is a Character instance.

| Field | Type | Required | Description |
|---|---|---|---|
| `name` | string | ✦ | What this template is called. Max 640 bytes / 64 graphemes. |
| `creatorDID` | string (did) | ✦ | Who defined this template. |
| `worldReference` | string (at-uri) | ✦ | Which world this template exists in. |
| `createdAt` | string (datetime) | ✦ | Timestamp. |
| `description` | string | | What this template represents. Max 10,240 bytes / 1,024 graphemes. |
| `originType` | string | | `knownValues`: `originalIP`, `publicDomain`, `collaborativeCommons`. |
| `canonicalCharacterReference` | string (at-uri) | | The single Character designated as the authoritative expression of this template. |
| `canonicalReferencePolicy` | string | | `knownValues`: `fixed` (never changes), `updatable` (originator can update), or `community` (community consensus). |
| `instancePolicy` | string | | `knownValues`: `open` (anyone can create instances), `restricted` (with approval), or `closed` (no new instances). |
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
| `actionType` | string | | `knownValues`: `narrative`, `dialogue`, `witness`, `competitive`, `administrative`. |
| `content` | string | | What happened. Max 30,720 bytes / 3,000 graphemes. |
| `locationReference` | string (at-uri) | | Where the action took place. |
| `visibility` | string | | `knownValues`: `canon`, `community`, `experimental`. |
| `narrativeWeight` | integer | | Optional importance scoring hook. Null by default. Populated by AppView or originator when needed. |
| `parentAction` | string (at-uri) | | Reference to the action this is responding to (for threading). |
| `eventReference` | string (at-uri) | | Reference to the event this action is part of. |

Note: Action uses `actorDID` instead of `creatorDID` — the actor is the person performing, not abstractly "creating."

---

## Event · `world.ptah.event`

Where competition becomes history. A competition, gathering, milestone, ceremony, or conflict where characters compete or convene.

| Field | Type | Required | Description |
|---|---|---|---|
| `name` | string | ✦ | What the event is called. Max 640 bytes / 64 graphemes. |
| `creatorDID` | string (did) | ✦ | Who organized this event. |
| `worldReference` | string (at-uri) | ✦ | Which world this event belongs to. |
| `createdAt` | string (datetime) | ✦ | Timestamp of event creation. |
| `description` | string | | What this event is about. Max 10,240 bytes / 1,024 graphemes. |
| `eventType` | string | | `knownValues`: `competition`, `gathering`, `milestone`, `ceremony`, `conflict`. |
| `status` | string | | `knownValues`: `scheduled`, `active`, `completed`, `cancelled`. |
| `startTime` | string (datetime) | | When the event begins. |
| `endTime` | string (datetime) | | When the event ends. |
| `stakes` | string | | What's at stake. Max 10,240 bytes / 1,024 graphemes. |
| `result` | string | | What happened. Populated when status moves to completed. Max 10,240 bytes / 1,024 graphemes. |
| `participants` | array of string (at-uri) | | Character records participating. |
| `witnesses` | array of string (at-uri) | | Action records that serve as witness attestations. Not a count — verifiable records. |
| `locationReference` | string (at-uri) | | Where the event takes place. |
| `canonicalStatus` | string | | References `world.ptah.defs#canonicalStatus*` tokens. |

---

## Log · `world.ptah.log`

The world's history book. What separates the protocol from a game or a social feed. Logs trace back through source references to the actions and events that generated them.

| Field | Type | Required | Description |
|---|---|---|---|
| `title` | string | ✦ | What this log entry is called. Max 640 bytes / 64 graphemes. |
| `creatorDID` | string (did) | ✦ | Who authored this log entry. |
| `worldReference` | string (at-uri) | ✦ | Which world this log belongs to. |
| `createdAt` | string (datetime) | ✦ | Timestamp. |
| `content` | string | | The narrative content. Max 102,400 bytes / 10,000 graphemes. |
| `summary` | string | | A brief summary of the log content. Max 2,560 bytes / 256 graphemes. |
| `logType` | string | | `knownValues`: `history`, `chronicle`, `essay`, `chapter`, `article`, `entry`. |
| `sourceReferences` | array of string (at-uri) | | Actions, events, or other logs this log derives from. The field that makes history verifiable. |
| `characters` | array of string (at-uri) | | Character records mentioned or involved. |
| `locationReference` | string (at-uri) | | The primary location of this log's narrative. |
| `canonicalStatus` | string | | References `world.ptah.defs#canonicalStatus*` tokens. |
| `coverImage` | blob | | Cover image for this log entry. Accepts PNG, JPEG, WebP. Max 1 MB. |
| `media` | array of ref → `#mediaItem` | | Media attachments. See below. |
| `humanAuthored` | boolean | | Declaration by the author that this work was written by a human, not generated by AI. |

Note: Log uses `title` instead of `name` — log entries are narrative texts, not entities.

### mediaItem object

| Field | Type | Description |
|---|---|---|
| `blob` | blob | The media file. Accepts PNG, JPEG, WebP, MP3, WAV, MP4. Max 50 MB. |
| `mimeType` | string | The MIME type of the media. Max 128 bytes. |
| `alt` | string | Alt text for accessibility. Max 1,000 bytes. |
| `caption` | string | Caption for the media. Max 500 bytes. |
| `duration` | integer | Duration in seconds for audio/video. |

---

## Origin · `world.ptah.origin`

The attribution and permission layer. Tracks who contributed what and under what terms.

| Field | Type | Required | Description |
|---|---|---|---|
| `contributorDID` | string (did) | ✦ | Who is making the contribution. |
| `worldReference` | string (at-uri) | ✦ | Which world they're contributing to. |
| `createdAt` | string (datetime) | ✦ | Timestamp. |
| `targetReference` | string (at-uri) | | The specific record being contributed to. |
| `contributionType` | string | | `knownValues`: `originator`, `coauthor`, `contributor`, `editor`, `translator`, `illustrator`. |
| `description` | string | | Description of what was contributed. Max 10,240 bytes / 1,024 graphemes. |
| `originatorApproval` | string | | `knownValues`: `approved`, `pending`, `rejected`, `notRequired`. |
| `publicDomainCompliance` | string | | `knownValues`: `compliant`, `pending`, `disputed`, `notApplicable`. |
| `attributionChain` | array of ref → `#attributionEntry` | | Structured attribution chain. Each entry records a contributor's DID, role, timestamp, and optional split. See below. |
| `splitPercentage` | integer | | Contribution share in basis points (100 = 1%). Min 0, max 10,000. |

Note: Origin uses `contributorDID` instead of `creatorDID` — the contributor is the person adding, distinct from the world originator.

### attributionEntry object

| Field | Type | Required | Description |
|---|---|---|---|
| `contributorDID` | string (did) | ✦ | The contributor's permanent identity. |
| `role` | string | ✦ | What role they played. Max 640 bytes / 64 graphemes. |
| `timestamp` | string (datetime) | | When this attribution was recorded. |
| `splitPercentage` | integer | | Contribution share in basis points. Min 0, max 10,000. |

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
| `locationType` | string | | `knownValues`: `territory`, `city`, `building`, `room`, `landmark`, `wilderness`, `vessel`, `virtual`. |
| `parentLocation` | string (at-uri) | | If this location exists inside a larger one. Enables infinite nesting. |
| `depthIndex` | integer | | How deep in the geographic hierarchy. Minimum 0. World-level=0, continent=1, country=2, city=3, etc. |
| `locationProperties` | ref → `#locationProperties` | | Flexible fields. See below. |
| `canonicalStatus` | string | | References `world.ptah.defs#canonicalStatus*` tokens. |

### locationProperties object

| Field | Type | Description |
|---|---|---|
| `climate` | string | Environmental conditions. Max 640 bytes / 64 graphemes. |
| `population` | string | Size or density. Max 640 bytes / 64 graphemes. |
| `controllingFaction` | string | Who controls this place. Max 640 bytes / 64 graphemes. |
| `notableHistory` | string | Significant events tied to this location. Max 2,560 bytes / 256 graphemes. |

---

## Collection · `world.ptah.collection`

Bundles multiple works together. An album, anthology, season, or any curated set of related works.

| Field | Type | Required | Description |
|---|---|---|---|
| `name` | string | ✦ | What the collection is called. Max 640 bytes / 64 graphemes. |
| `creatorDID` | string (did) | ✦ | Who created this collection. |
| `worldReference` | string (at-uri) | ✦ | Which world this collection belongs to. |
| `createdAt` | string (datetime) | ✦ | Timestamp. |
| `items` | array of string (at-uri) | ✦ | References to the works in this collection. |
| `description` | string | | What this collection is about. Max 10,240 bytes / 1,024 graphemes. |
| `ordering` | string | | `knownValues`: `sequential`, `unordered`, `chronological`. |
| `coverImage` | blob | | Cover artwork. Accepts PNG, JPEG, WebP. Max 1 MB. |
| `canonicalStatus` | string | | References `world.ptah.defs#canonicalStatus*` tokens. |

---

## Trace · `world.ptah.trace`

Tracks lineage between works. The paper trail from one work to another.

| Field | Type | Required | Description |
|---|---|---|---|
| `creatorDID` | string (did) | ✦ | Who created this trace record. |
| `worldReference` | string (at-uri) | ✦ | Which world this trace belongs to. |
| `createdAt` | string (datetime) | ✦ | Timestamp. |
| `sourceWork` | string (at-uri) | ✦ | Reference to the original work. |
| `derivedWork` | string (at-uri) | ✦ | Reference to the work that came from the source. |
| `relationship` | string | ✦ | `knownValues`: `cover`, `remix`, `adaptation`, `translation`, `sample`, `interpolation`, `response`, `sequel`, `spinoff`, `excerpt`, `remake`, `fork`. |
| `description` | string | | Context about the relationship. Max 10,240 bytes / 1,024 graphemes. |
| `clearanceStatus` | string | | `knownValues`: `cleared`, `pending`, `disputed`, `notRequired`. |

---

## Usage · `world.ptah.usage`

Terms and permissions for a work. What's allowed, where, for how long, and under what conditions.

| Field | Type | Required | Description |
|---|---|---|---|
| `creatorDID` | string (did) | ✦ | Who created this usage record. |
| `worldReference` | string (at-uri) | ✦ | Which world this usage record belongs to. |
| `createdAt` | string (datetime) | ✦ | Timestamp. |
| `workReference` | string (at-uri) | ✦ | Reference to the work these terms apply to. |
| `allowCommercial` | boolean | | Whether commercial use is permitted. |
| `allowDerivatives` | boolean | | Whether derivative works are permitted. |
| `allowPerformance` | boolean | | Whether public performance is permitted. |
| `requireAttribution` | boolean | | Whether attribution is required. |
| `territories` | array of string | | Geographic territories where these terms apply. Empty = worldwide. Max 128 bytes per entry. |
| `validUntil` | string (datetime) | | When these terms expire. Empty = perpetual. |
| `terms` | string | | Human-readable terms description. Max 10,240 bytes / 1,024 graphemes. |
| `licenseType` | string | | `knownValues`: `allRightsReserved`, `creativeCommons`, `publicDomain`, `custom`. |

---

## Version · `world.ptah.version`

Edit history within a work. Tracks the evolution from draft to published to revised — every version, every change.

| Field | Type | Required | Description |
|---|---|---|---|
| `creatorDID` | string (did) | ✦ | Who created this version. |
| `worldReference` | string (at-uri) | ✦ | Which world this version belongs to. |
| `createdAt` | string (datetime) | ✦ | Timestamp. |
| `workReference` | string (at-uri) | ✦ | Reference to the work this is a version of. |
| `previousVersion` | string (at-uri) | | Reference to the version this replaced. Empty = first version. |
| `versionLabel` | string | | `knownValues`: `draft`, `published`, `revised`, `corrected`, `final`. Max 640 bytes / 64 graphemes. |
| `changeDescription` | string | | What changed in this version. Max 10,240 bytes / 1,024 graphemes. |
| `isCurrent` | boolean | | Whether this is the current/active version. |
| `status` | string | | `knownValues`: `active`, `superseded`, `retracted`, `archived`. |

---

## Flax · `world.ptah.flax`

A signaling record indicating an account participates in the Ptah Protocol. Named for the twisted flax glyph (𓉔), the H in Ptah — the attribution chain thread. One per account. Used by AppViews for participant discovery.

| Field | Type | Required | Description |
|---|---|---|---|
| `createdAt` | string (datetime) | ✦ | When this account joined the Ptah Protocol. |
| `displayName` | string | | How this participant wants to be identified in Ptah contexts. Max 640 bytes / 64 graphemes. |
| `bio` | string | | Short biography for this creator. Max 2,560 bytes / 256 graphemes. |

**Record key:** `self` (literal, singleton — one per account).

No `creatorDID` field. The account's DID is implicit from the repository — the AT URI itself (`at://{DID}/world.ptah.flax/self`) identifies the account.

---

## How Records Reference Each Other

The dependency chain:

```
World
├── Template (references World)
│   └── Character (references Template + World)
├── Character (references World, optionally Template)
├── Location (references World, optionally parent Location)
├── Action (references World, Character, optionally Location, Event, parent Action)
├── Event (references World, Location, Characters as participants, Actions as witnesses)
├── Log (references World, Actions + Events + Logs as sources, Characters, Location)
├── Origin (references World + any record being contributed to)
├── Collection (references World + array of work items)
├── Trace (references World + source work + derived work)
├── Usage (references World + work)
└── Version (references World + work + previous version)
```

A World must exist first. Everything else references it via AT URI. Records reference each other laterally — an Action points to a Character, an Event points to a Location, a Log points to the Actions and Events that generated it. The entire graph is traversable from any node.

---

## Network Resolution

When ATProto software encounters a `world.ptah.*` NSID:

1. Read the domain from the NSID → `ptah.world`
2. Look up `_lexicon.ptah.world` TXT record → returns DID
3. Fetch `com.atproto.lexicon.schema` record from that DID's repository
4. The schema definition is returned

**DNS:** `_lexicon.ptah.world` → `did=did:plc:l45z35sxxjuobp5q65a5vu22`
**PDS:** Blacksky (`blacksky.app`)
