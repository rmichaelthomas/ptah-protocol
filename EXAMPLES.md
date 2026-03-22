# Example World Record Chains

Two complete example worlds demonstrating how the Ptah Protocol's eight record types connect, reference each other via AT URIs, and express different kinds of creative worlds. Two additional competitive examples demonstrate the protocol handling structured tournament play and collaborative tabletop RPG campaigns.

For field-level details, see the [Specification](SPECIFICATION.md). For a hands-on walkthrough, see [Getting Started](GETTING_STARTED.md).

---

## AT URI Convention

All AT URIs follow the standard ATProto format:

```
at://{DID}/{NSID}/{rkey}
```

Where:
- `{DID}` is a placeholder Decentralized Identifier (e.g., `did:plc:worldseeder01`)
- `{NSID}` is the Namespaced Identifier for the record type (e.g., `world.ptah.world`)
- `{rkey}` is a unique record key (e.g., `hamlet-world`)

Placeholder DIDs are human-readable for clarity. On a live network, DIDs are opaque alphanumeric strings. The structure is identical.

---

# World 1: The World of Hamlet

## Why This World

Hamlet is the hardest test for the public domain pattern. It is universally known. The Role/Instance split matters immediately — multiple people can play the same character. Canon is contested by four centuries of interpretation. The `controlType`, `roleReference`, and `canonicalCharacterReference` fields are all load-bearing from the first record.

If the schema holds Hamlet, it holds any public domain world.

## What This Chain Contains

- 1 World record
- 1 Role record (Hamlet)
- 3 Character records (Canonical Hamlet, a contributor's Hamlet instance, Claudius)
- 1 Location record (The Battlements of Elsinore)
- 3 Action records (The Ghost Speaks, The Burning Court Hamlet Acts, A Witness Action)
- 1 Event record (The Throne Room Confrontation)
- 1 Lore record (The Day the Court Heard the Truth)
- 1 Contribution record (governing the contributor's additions)

Total: 12 records across all 8 record types.

---

### Record 1 — World: The World of Hamlet

```json
{
  "$type": "world.ptah.world",
  "name": "The World of Hamlet",
  "creatorDID": "did:plc:worldseeder01",
  "description": "A world seeded from Shakespeare's Hamlet. Denmark in crisis. A dead king. A usurper on the throne. A prince caught between action and paralysis.",
  "sourceType": "publicDomain",
  "sourceReference": "William Shakespeare, The Tragedy of Hamlet, Prince of Denmark, c. 1600–1601. Public domain.",
  "governanceMode": "governed",
  "renderingHints": {
    "tone": "dark, political, psychological",
    "era": "late medieval / early Renaissance",
    "genre": "tragedy",
    "aesthetic": "stone, torchlight, fog, cold sea"
  },
  "createdAt": "2026-04-01T00:00:00Z"
}
```

**AT URI:** `at://did:plc:worldseeder01/world.ptah.world/hamlet-world`

---

### Record 2 — Role: Hamlet, Prince of Denmark

The template. The shared identity. Not a specific performance — the Role itself.

```json
{
  "$type": "world.ptah.role",
  "name": "Hamlet, Prince of Denmark",
  "worldReference": "at://did:plc:worldseeder01/world.ptah.world/hamlet-world",
  "creatorDID": "did:plc:worldseeder01",
  "description": "The Prince. Son of the murdered King. The most performed role in the English language.",
  "sourceType": "world.ptah.defs#sourceTypePublicDomain",
  "sourceReference": "William Shakespeare, Hamlet, Prince of Denmark character.",
  "canonicalCharacterReference": "at://did:plc:worldseeder01/world.ptah.character/hamlet-canonical",
  "canonicalReferencePolicy": "updatable",
  "instancePolicy": "openInstance",
  "authorshipRecord": "did:plc:worldseeder01",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:01:00Z"
}
```

**AT URI:** `at://did:plc:worldseeder01/world.ptah.role/hamlet-role`

The Role exists. `instancePolicy: openInstance` means anyone can create a Character instance of Hamlet. This is a public domain world — Hamlet belongs to everyone.

---

### Record 3 — Character: Canonical Hamlet

The specific character the world originator designated as the authoritative expression of the Hamlet role.

```json
{
  "$type": "world.ptah.character",
  "name": "Hamlet (Canonical)",
  "creatorDID": "did:plc:worldseeder01",
  "worldReference": "at://did:plc:worldseeder01/world.ptah.world/hamlet-world",
  "roleReference": "at://did:plc:worldseeder01/world.ptah.role/hamlet-role",
  "description": "The canonical Hamlet. The originator's definitive expression of the prince.",
  "controlType": "exclusive",
  "originType": "world.ptah.defs#sourceTypePublicDomain",
  "authorshipRecord": "did:plc:worldseeder01",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:02:00Z"
}
```

**AT URI:** `at://did:plc:worldseeder01/world.ptah.character/hamlet-canonical`

This is the character that `canonicalCharacterReference` on the Role record points to.

---

### Record 4 — Character: Claudius

An open character — anyone can act as Claudius within the world's rules.

```json
{
  "$type": "world.ptah.character",
  "name": "Claudius, King of Denmark",
  "creatorDID": "did:plc:worldseeder01",
  "worldReference": "at://did:plc:worldseeder01/world.ptah.world/hamlet-world",
  "description": "The usurper. Brother of the dead king. Now wears the crown and the queen.",
  "controlType": "open",
  "originType": "world.ptah.defs#sourceTypePublicDomain",
  "authorshipRecord": "did:plc:worldseeder01",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:03:00Z"
}
```

**AT URI:** `at://did:plc:worldseeder01/world.ptah.character/claudius`

No `roleReference` — Claudius doesn't need the Role/Instance split because there's only one Claudius. The role pattern is used when multiple people need to embody the same identity.

---

### Record 5 — Location: The Battlements of Elsinore

```json
{
  "$type": "world.ptah.location",
  "name": "The Battlements of Elsinore",
  "creatorDID": "did:plc:worldseeder01",
  "worldReference": "at://did:plc:worldseeder01/world.ptah.world/hamlet-world",
  "description": "The high walls of the castle. Where the ghost walks. Where the watch keeps vigil. Cold stone and colder wind.",
  "locationType": "landmark",
  "depthIndex": 2,
  "properties": {
    "climate": "North Sea wind, perpetual damp, winter fog",
    "controllingFaction": "The Crown — currently Claudius"
  },
  "authorshipRecord": "did:plc:worldseeder01",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:04:00Z"
}
```

**AT URI:** `at://did:plc:worldseeder01/world.ptah.location/battlements`

---

### Record 6 — Action: The Ghost Speaks

```json
{
  "$type": "world.ptah.action",
  "actorDID": "did:plc:worldseeder01",
  "characterReference": "at://did:plc:worldseeder01/world.ptah.character/hamlet-canonical",
  "worldReference": "at://did:plc:worldseeder01/world.ptah.world/hamlet-world",
  "actionType": "speech",
  "content": "The ghost of King Hamlet appears on the battlements and speaks to his son. He names his murderer. He demands revenge. The prince listens. The prince does not act.",
  "locationReference": "at://did:plc:worldseeder01/world.ptah.location/battlements",
  "visibility": "canon",
  "createdAt": "2026-04-01T00:05:00Z"
}
```

**AT URI:** `at://did:plc:worldseeder01/world.ptah.action/ghost-speaks`

---

### Record 7 — Contribution: A Contributor Enters the World

A second person wants to add to the World of Hamlet.

```json
{
  "$type": "world.ptah.contribution",
  "contributorDID": "did:plc:contributor01",
  "worldReference": "at://did:plc:worldseeder01/world.ptah.world/hamlet-world",
  "contributionType": "character",
  "recordReference": "at://did:plc:contributor01/world.ptah.character/hamlet-instance-01",
  "originatorApproval": "preApproved",
  "canonicalStatus": "world.ptah.defs#canonicalStatusCommunity",
  "attributionChain": [
    "at://did:plc:worldseeder01/world.ptah.world/hamlet-world"
  ],
  "publicDomainCompliance": true,
  "createdAt": "2026-04-02T00:00:00Z"
}
```

**AT URI:** `at://did:plc:contributor01/world.ptah.contribution/hamlet-contrib-01`

`originatorApproval: preApproved` because the world is public domain with `instancePolicy: openInstance`. The contributor doesn't need individual permission — the world's design already grants it.

---

### Record 8 — Character: A Contributor's Hamlet Instance

```json
{
  "$type": "world.ptah.character",
  "name": "Hamlet (The Burning Court)",
  "creatorDID": "did:plc:contributor01",
  "worldReference": "at://did:plc:worldseeder01/world.ptah.world/hamlet-world",
  "roleReference": "at://did:plc:worldseeder01/world.ptah.role/hamlet-role",
  "description": "A Hamlet who chose fire over hesitation. This is the prince who acts immediately — and burns the court down around him.",
  "controlType": "exclusive",
  "originType": "contributed",
  "authorshipRecord": "did:plc:contributor01",
  "canonicalStatus": "world.ptah.defs#canonicalStatusCommunity",
  "createdAt": "2026-04-02T00:01:00Z"
}
```

**AT URI:** `at://did:plc:contributor01/world.ptah.character/hamlet-instance-01`

This character references the same Role as the canonical Hamlet but is a different instance — a different performance. `canonicalStatus: communityCanon` distinguishes it from the originator's version.

---

### Record 9 — Action: The Burning Court Hamlet Acts

```json
{
  "$type": "world.ptah.action",
  "actorDID": "did:plc:contributor01",
  "characterReference": "at://did:plc:contributor01/world.ptah.character/hamlet-instance-01",
  "worldReference": "at://did:plc:worldseeder01/world.ptah.world/hamlet-world",
  "actionType": "conflict",
  "content": "This Hamlet does not wait. He draws his sword in the throne room and names Claudius murderer before the entire court. The court fractures. The kingdom splinters. The ghost watches from the battlements and says nothing.",
  "locationReference": "at://did:plc:worldseeder01/world.ptah.location/battlements",
  "visibility": "community",
  "createdAt": "2026-04-02T00:02:00Z"
}
```

**AT URI:** `at://did:plc:contributor01/world.ptah.action/burning-court-acts`

---

### Record 10 — Action: A Witness

A third person witnesses the event. This action record becomes evidence in the Event's witnesses array.

```json
{
  "$type": "world.ptah.action",
  "actorDID": "did:plc:witness01",
  "worldReference": "at://did:plc:worldseeder01/world.ptah.world/hamlet-world",
  "actionType": "witness",
  "content": "I was present when the court confrontation occurred. The prince acted. The king fell.",
  "visibility": "canon",
  "createdAt": "2026-04-02T00:03:00Z"
}
```

**AT URI:** `at://did:plc:witness01/world.ptah.action/witness-throne-room`

---

### Record 11 — Event: The Throne Room Confrontation

```json
{
  "$type": "world.ptah.event",
  "name": "The Throne Room Confrontation",
  "creatorDID": "did:plc:worldseeder01",
  "worldReference": "at://did:plc:worldseeder01/world.ptah.world/hamlet-world",
  "eventType": "battle",
  "participants": [
    "at://did:plc:worldseeder01/world.ptah.character/hamlet-canonical",
    "at://did:plc:worldseeder01/world.ptah.character/claudius"
  ],
  "stakes": "The crown. The truth. The future of Denmark.",
  "status": "completed",
  "result": "The prince spoke. The court heard. The kingdom will never be the same.",
  "witnesses": [
    "at://did:plc:witness01/world.ptah.action/witness-throne-room"
  ],
  "locationReference": "at://did:plc:worldseeder01/world.ptah.location/battlements",
  "loreStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-02T00:04:00Z",
  "completedAt": "2026-04-02T00:05:00Z"
}
```

**AT URI:** `at://did:plc:worldseeder01/world.ptah.event/throne-room`

---

### Record 12 — Lore: The Day the Court Heard the Truth

```json
{
  "$type": "world.ptah.lore",
  "title": "The Day the Court Heard the Truth",
  "worldReference": "at://did:plc:worldseeder01/world.ptah.world/hamlet-world",
  "creatorDID": "did:plc:worldseeder01",
  "content": "On the day the prince finally spoke, the court learned what the battlements had known since the ghost first walked. The king was a murderer. The crown was stolen. And the prince — whether he hesitated for weeks or acted in an instant — changed Denmark forever. Two versions of this moment exist in the record. In one, the prince deliberated. In the other, he burned. Both are true. Both are attributed. The world holds both.",
  "sourceReferences": [
    "at://did:plc:worldseeder01/world.ptah.action/ghost-speaks",
    "at://did:plc:contributor01/world.ptah.action/burning-court-acts",
    "at://did:plc:worldseeder01/world.ptah.event/throne-room"
  ],
  "characters": [
    "at://did:plc:worldseeder01/world.ptah.character/hamlet-canonical",
    "at://did:plc:worldseeder01/world.ptah.character/claudius"
  ],
  "timelinePosition": "Act III — The Confrontation",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "authorshipRecord": "did:plc:worldseeder01",
  "contributionType": "originator",
  "createdAt": "2026-04-02T00:06:00Z"
}
```

**AT URI:** `at://did:plc:worldseeder01/world.ptah.lore/court-heard-truth`

The `sourceReferences` array traces this lore back to the action records and event record that generated it. The history is verifiable — follow the AT URIs to the source.

---

# World 2: The World of Gatsby

## Why This World

Gatsby tests what Hamlet doesn't. Where Hamlet is a world of political violence and succession, Gatsby is a world of social performance — wealth as identity, parties as power, narration as an unreliable act. The characters' public selves diverge from their private selves. The events are social gatherings, not battles. The lore is gossip elevated to history.

This world entered the U.S. public domain in 2021 and has already spawned a wave of creative reworkings. It's one of the most recognized stories in the English language.

## What This Chain Contains

- 1 World record
- 1 Role record (Gatsby)
- 2 Character records (Canonical Gatsby, a contributor's Gatsby reinterpretation)
- 1 Location record (The Mansion at West Egg)
- 2 Action records (The Party Begins, A Witness Observes)
- 1 Event record (The Last Party)
- 1 Lore record (What the Green Light Meant)
- 1 Contribution record

Total: 10 records across all 8 record types.

---

### Record 1 — World: The World of Gatsby

```json
{
  "$type": "world.ptah.world",
  "name": "The World of Gatsby",
  "creatorDID": "did:plc:worldseeder02",
  "description": "Long Island, 1922. New money and old money separated by a bay. A man built an empire to win back a woman. The empire was a performance. The woman was a memory. The narrator watched it all and told you a story — but narrators choose what to tell.",
  "sourceType": "publicDomain",
  "sourceReference": "F. Scott Fitzgerald, The Great Gatsby, 1925. Public domain (U.S.) as of January 1, 2021.",
  "governanceMode": "governed",
  "renderingHints": {
    "tone": "elegiac, seductive, doomed",
    "era": "Jazz Age, 1920s America",
    "genre": "literary fiction, social tragedy",
    "aesthetic": "gold light, green water, white linen, broken glass"
  },
  "createdAt": "2026-04-01T00:00:00Z"
}
```

**AT URI:** `at://did:plc:worldseeder02/world.ptah.world/gatsby-world`

---

### Record 2 — Role: Jay Gatsby

```json
{
  "$type": "world.ptah.role",
  "name": "Jay Gatsby",
  "worldReference": "at://did:plc:worldseeder02/world.ptah.world/gatsby-world",
  "creatorDID": "did:plc:worldseeder02",
  "description": "The self-made man. Born James Gatz. Invented himself out of nothing and longing. Throws parties for a woman across the bay. The performance is the person — or the person is the performance. The role invites that question.",
  "sourceType": "world.ptah.defs#sourceTypePublicDomain",
  "sourceReference": "F. Scott Fitzgerald, The Great Gatsby, Jay Gatsby character.",
  "canonicalCharacterReference": "at://did:plc:worldseeder02/world.ptah.character/gatsby-canonical",
  "canonicalReferencePolicy": "updatable",
  "instancePolicy": "openInstance",
  "authorshipRecord": "did:plc:worldseeder02",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:01:00Z"
}
```

**AT URI:** `at://did:plc:worldseeder02/world.ptah.role/gatsby-role`

---

### Record 3 — Character: Canonical Gatsby

```json
{
  "$type": "world.ptah.character",
  "name": "Jay Gatsby (Canonical)",
  "creatorDID": "did:plc:worldseeder02",
  "worldReference": "at://did:plc:worldseeder02/world.ptah.world/gatsby-world",
  "roleReference": "at://did:plc:worldseeder02/world.ptah.role/gatsby-role",
  "description": "The originator's Gatsby. Faithful to Fitzgerald's portrait — the romantic who built a cathedral of lights to reach one person.",
  "controlType": "exclusive",
  "originType": "world.ptah.defs#sourceTypePublicDomain",
  "authorshipRecord": "did:plc:worldseeder02",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:02:00Z"
}
```

**AT URI:** `at://did:plc:worldseeder02/world.ptah.character/gatsby-canonical`

---

### Record 4 — Location: The Mansion at West Egg

```json
{
  "$type": "world.ptah.location",
  "name": "The Mansion at West Egg",
  "creatorDID": "did:plc:worldseeder02",
  "worldReference": "at://did:plc:worldseeder02/world.ptah.world/gatsby-world",
  "description": "Gatsby's house. An imitation of a French Hôtel de Ville. Forty acres of lawn. A marble swimming pool. A tower on one side. The whole thing is a stage set for an audience of one — Daisy, across the bay.",
  "locationType": "building",
  "depthIndex": 2,
  "properties": {
    "climate": "Long Island summers — humid, golden, lit by lanterns",
    "controllingFaction": "Jay Gatsby, sole owner"
  },
  "authorshipRecord": "did:plc:worldseeder02",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:03:00Z"
}
```

**AT URI:** `at://did:plc:worldseeder02/world.ptah.location/west-egg-mansion`

---

### Record 5 — Action: The Party Begins

```json
{
  "$type": "world.ptah.action",
  "actorDID": "did:plc:worldseeder02",
  "characterReference": "at://did:plc:worldseeder02/world.ptah.character/gatsby-canonical",
  "worldReference": "at://did:plc:worldseeder02/world.ptah.world/gatsby-world",
  "actionType": "creation",
  "content": "The lights go on across the lawn. The orchestra arrives. The caterers lay tables for hundreds. Gatsby stands at the window and watches the green light across the bay. The party is not for the guests. It has never been for the guests.",
  "locationReference": "at://did:plc:worldseeder02/world.ptah.location/west-egg-mansion",
  "visibility": "canon",
  "createdAt": "2026-04-01T00:04:00Z"
}
```

**AT URI:** `at://did:plc:worldseeder02/world.ptah.action/party-begins`

---

### Record 6 — Contribution: A Contributor Reimagines Gatsby

```json
{
  "$type": "world.ptah.contribution",
  "contributorDID": "did:plc:contributor02",
  "worldReference": "at://did:plc:worldseeder02/world.ptah.world/gatsby-world",
  "contributionType": "character",
  "recordReference": "at://did:plc:contributor02/world.ptah.character/gatsby-instance-01",
  "originatorApproval": "preApproved",
  "canonicalStatus": "world.ptah.defs#canonicalStatusCommunity",
  "attributionChain": [
    "at://did:plc:worldseeder02/world.ptah.world/gatsby-world"
  ],
  "publicDomainCompliance": true,
  "createdAt": "2026-04-02T00:00:00Z"
}
```

**AT URI:** `at://did:plc:contributor02/world.ptah.contribution/gatsby-contrib-01`

---

### Record 7 — Character: A Contributor's Gatsby

```json
{
  "$type": "world.ptah.character",
  "name": "Jay Gatsby (The Hollow Empire)",
  "creatorDID": "did:plc:contributor02",
  "worldReference": "at://did:plc:worldseeder02/world.ptah.world/gatsby-world",
  "roleReference": "at://did:plc:worldseeder02/world.ptah.role/gatsby-role",
  "description": "A Gatsby who knows the performance is empty and keeps performing anyway. Not a romantic — a nihilist wearing a romantic's suit. The parties get louder because the silence underneath gets worse.",
  "controlType": "exclusive",
  "originType": "contributed",
  "authorshipRecord": "did:plc:contributor02",
  "canonicalStatus": "world.ptah.defs#canonicalStatusCommunity",
  "createdAt": "2026-04-02T00:01:00Z"
}
```

**AT URI:** `at://did:plc:contributor02/world.ptah.character/gatsby-instance-01`

Same Role, different instance. Fitzgerald's Gatsby is a romantic. This contributor's Gatsby is a nihilist. Both reference the same Role record. Both are valid. Both are attributed to different creators.

---

### Record 8 — Action: A Witness Observes

```json
{
  "$type": "world.ptah.action",
  "actorDID": "did:plc:witness02",
  "worldReference": "at://did:plc:worldseeder02/world.ptah.world/gatsby-world",
  "actionType": "witness",
  "content": "I attended the last party. I saw Gatsby standing alone on the dock after everyone left. The green light was still on across the bay.",
  "locationReference": "at://did:plc:worldseeder02/world.ptah.location/west-egg-mansion",
  "visibility": "canon",
  "createdAt": "2026-04-02T00:02:00Z"
}
```

**AT URI:** `at://did:plc:witness02/world.ptah.action/witness-last-party`

---

### Record 9 — Event: The Last Party

```json
{
  "$type": "world.ptah.event",
  "name": "The Last Party at West Egg",
  "creatorDID": "did:plc:worldseeder02",
  "worldReference": "at://did:plc:worldseeder02/world.ptah.world/gatsby-world",
  "eventType": "gathering",
  "participants": [
    "at://did:plc:worldseeder02/world.ptah.character/gatsby-canonical"
  ],
  "stakes": "Everything Gatsby built. Every light he turned on. The question of whether any of it was real.",
  "status": "completed",
  "result": "The guests left. The lights went dark. Gatsby stood on the dock alone. The green light was still there. It was always going to be there.",
  "witnesses": [
    "at://did:plc:witness02/world.ptah.action/witness-last-party"
  ],
  "locationReference": "at://did:plc:worldseeder02/world.ptah.location/west-egg-mansion",
  "loreStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-02T00:03:00Z",
  "completedAt": "2026-04-02T00:04:00Z"
}
```

**AT URI:** `at://did:plc:worldseeder02/world.ptah.event/last-party`

---

### Record 10 — Lore: What the Green Light Meant

```json
{
  "$type": "world.ptah.lore",
  "title": "What the Green Light Meant",
  "worldReference": "at://did:plc:worldseeder02/world.ptah.world/gatsby-world",
  "creatorDID": "did:plc:worldseeder02",
  "content": "After the last party ended and the mansion went dark, the question remained: what was the green light? To the canonical Gatsby, it was Daisy — the real person, the recoverable past. To the Hollow Empire Gatsby, it was the performance itself — the light you stare at because looking away means admitting there's nothing behind you. Both readings trace back to the same event. Both are sourced. Both are permanent. The world holds both, and the green light stays on.",
  "sourceReferences": [
    "at://did:plc:worldseeder02/world.ptah.action/party-begins",
    "at://did:plc:worldseeder02/world.ptah.event/last-party"
  ],
  "characters": [
    "at://did:plc:worldseeder02/world.ptah.character/gatsby-canonical",
    "at://did:plc:contributor02/world.ptah.character/gatsby-instance-01"
  ],
  "timelinePosition": "Summer's End — After the Last Party",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "authorshipRecord": "did:plc:worldseeder02",
  "contributionType": "originator",
  "createdAt": "2026-04-02T00:05:00Z"
}
```

**AT URI:** `at://did:plc:worldseeder02/world.ptah.lore/green-light`

---

## What These Two Literary Worlds Demonstrate

**Hamlet** tests the protocol's hardest public domain problem: a universally known work with contested interpretations, where multiple people need to embody the same character simultaneously. The Role/Instance split, `controlType`, and `canonicalCharacterReference` are all exercised.

**Gatsby** tests a different kind of world: social performance rather than political violence, gatherings rather than battles, lore built from unreliable narration rather than witnessed combat. The same eight record types express both worlds without modification.

Both worlds show:
- A world originator seeding the foundation
- A contributor adding their own interpretation
- Multiple Character instances of the same Role, attributed to different creators
- Actions generating history that becomes verifiable Lore
- Events with witnesses — real action records, not just a count
- The `attributionChain` tracing provenance through every contribution

---

# World 3: Blacksky Spades — A Competitive Tournament

## Why This World

Hamlet and Gatsby demonstrate literary world-building. Spades demonstrates the other half of what the protocol was built for — structured competitive events with brackets, rounds, winners, and results that become permanent history.

This world tests: the `format` field on Events, the full `status` lifecycle (`upcoming` → `active` → `completed`), multiple Events chaining into a tournament arc, witnesses as real attestation records during competitive play, and Lore that reads like a season record rather than a narrative.

Spades is culturally aligned with Blacksky, where the protocol lives. It's a game people already play online. The tournament structure is immediately recognizable.

## What This Chain Contains

- 1 World record
- 4 Character records (four players forming two teams)
- 1 Location record (The Table)
- 3 Action records (a bid, a play, a witness)
- 1 Event record (Championship Match)
- 1 Lore record (Season record)

Total: 11 records. No Role record — Spades players are themselves, not instances of a shared identity.

---

### Record 1 — World: Blacksky Spades

```json
{
  "$type": "world.ptah.world",
  "name": "Blacksky Spades",
  "creatorDID": "did:plc:spadeshost01",
  "description": "Competitive Spades on the open network. Partners, bids, books, and Boston. Every hand is recorded. Every result is permanent. Talk your trash — it's on the record too.",
  "sourceType": "world.ptah.defs#sourceTypeOriginalIP",
  "governanceMode": "governed",
  "renderingHints": {
    "tone": "competitive, social, sharp",
    "era": "present day",
    "genre": "card game, tournament play",
    "aesthetic": "green felt, four chairs, house rules posted on the wall"
  },
  "createdAt": "2026-04-01T00:00:00Z"
}
```

**AT URI:** `at://did:plc:spadeshost01/world.ptah.world/blacksky-spades`

`sourceType: originalIP` — this isn't a public domain adaptation. It's an original competitive world built on the protocol.

---

### Record 2 — Character: Player 1 (Team North)

```json
{
  "$type": "world.ptah.character",
  "name": "Ace",
  "creatorDID": "did:plc:player01",
  "worldReference": "at://did:plc:spadeshost01/world.ptah.world/blacksky-spades",
  "description": "Team North. Bids conservative. Plays aggressive. Never goes nil unless it's match point.",
  "controlType": "exclusive",
  "originType": "world.ptah.defs#sourceTypeOriginalIP",
  "properties": {
    "affiliation": "Team North"
  },
  "authorshipRecord": "did:plc:player01",
  "createdAt": "2026-04-01T00:01:00Z"
}
```

**AT URI:** `at://did:plc:player01/world.ptah.character/ace`

---

### Record 3 — Character: Player 2 (Team North)

```json
{
  "$type": "world.ptah.character",
  "name": "Deuce",
  "creatorDID": "did:plc:player02",
  "worldReference": "at://did:plc:spadeshost01/world.ptah.world/blacksky-spades",
  "description": "Team North. The nil specialist. Reads the table like a book.",
  "controlType": "exclusive",
  "originType": "world.ptah.defs#sourceTypeOriginalIP",
  "properties": {
    "affiliation": "Team North"
  },
  "authorshipRecord": "did:plc:player02",
  "createdAt": "2026-04-01T00:02:00Z"
}
```

**AT URI:** `at://did:plc:player02/world.ptah.character/deuce`

---

### Record 4 — Character: Player 3 (Team South)

```json
{
  "$type": "world.ptah.character",
  "name": "Spook",
  "creatorDID": "did:plc:player03",
  "worldReference": "at://did:plc:spadeshost01/world.ptah.world/blacksky-spades",
  "description": "Team South. Overbids every round. Somehow makes it work.",
  "controlType": "exclusive",
  "originType": "world.ptah.defs#sourceTypeOriginalIP",
  "properties": {
    "affiliation": "Team South"
  },
  "authorshipRecord": "did:plc:player03",
  "createdAt": "2026-04-01T00:03:00Z"
}
```

**AT URI:** `at://did:plc:player03/world.ptah.character/spook`

---

### Record 5 — Character: Player 4 (Team South)

```json
{
  "$type": "world.ptah.character",
  "name": "Shadow",
  "creatorDID": "did:plc:player04",
  "worldReference": "at://did:plc:spadeshost01/world.ptah.world/blacksky-spades",
  "description": "Team South. Counts every card. Doesn't talk until the hand is over. Then talks too much.",
  "controlType": "exclusive",
  "originType": "world.ptah.defs#sourceTypeOriginalIP",
  "properties": {
    "affiliation": "Team South"
  },
  "authorshipRecord": "did:plc:player04",
  "createdAt": "2026-04-01T00:04:00Z"
}
```

**AT URI:** `at://did:plc:player04/world.ptah.character/shadow`

---

### Record 6 — Location: The Table

```json
{
  "$type": "world.ptah.location",
  "name": "The Table",
  "creatorDID": "did:plc:spadeshost01",
  "worldReference": "at://did:plc:spadeshost01/world.ptah.world/blacksky-spades",
  "description": "Four seats. One deck. House rules: no blind nil before round 5, jokers are high, talk all the trash you want.",
  "locationType": "abstractSpace",
  "depthIndex": 1,
  "authorshipRecord": "did:plc:spadeshost01",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:05:00Z"
}
```

**AT URI:** `at://did:plc:spadeshost01/world.ptah.location/the-table`

`locationType: abstractSpace` — the table isn't a physical place. It's wherever the game happens.

---

### Record 7 — Action: The Bid

```json
{
  "$type": "world.ptah.action",
  "actorDID": "did:plc:player01",
  "characterReference": "at://did:plc:player01/world.ptah.character/ace",
  "worldReference": "at://did:plc:spadeshost01/world.ptah.world/blacksky-spades",
  "actionType": "speech",
  "content": "Ace bids 4. Looks at Deuce across the table. Deuce nods. Team North is at 6 combined.",
  "locationReference": "at://did:plc:spadeshost01/world.ptah.location/the-table",
  "visibility": "canon",
  "createdAt": "2026-04-05T20:00:00Z"
}
```

**AT URI:** `at://did:plc:player01/world.ptah.action/bid-round1`

---

### Record 8 — Action: The Play

```json
{
  "$type": "world.ptah.action",
  "actorDID": "did:plc:player03",
  "characterReference": "at://did:plc:player03/world.ptah.character/spook",
  "worldReference": "at://did:plc:spadeshost01/world.ptah.world/blacksky-spades",
  "actionType": "conflict",
  "content": "Spook cuts with the Queen of Spades on a Heart lead. Takes the book. Team South now has 7 — one over their bid. Sandbag watch is on.",
  "locationReference": "at://did:plc:spadeshost01/world.ptah.location/the-table",
  "visibility": "canon",
  "createdAt": "2026-04-05T20:15:00Z"
}
```

**AT URI:** `at://did:plc:player03/world.ptah.action/play-round1`

---

### Record 9 — Action: A Witness

```json
{
  "$type": "world.ptah.action",
  "actorDID": "did:plc:spectator01",
  "worldReference": "at://did:plc:spadeshost01/world.ptah.world/blacksky-spades",
  "actionType": "witness",
  "content": "Watched the championship match. Team North went set in round 3 trying to cover a nil. Team South ran the table from there.",
  "visibility": "canon",
  "createdAt": "2026-04-05T21:30:00Z"
}
```

**AT URI:** `at://did:plc:spectator01/world.ptah.action/witness-championship`

---

### Record 10 — Event: Championship Match

```json
{
  "$type": "world.ptah.event",
  "name": "Blacksky Spades Championship — Spring 2026",
  "creatorDID": "did:plc:spadeshost01",
  "worldReference": "at://did:plc:spadeshost01/world.ptah.world/blacksky-spades",
  "eventType": "tournament",
  "format": "singleElimination",
  "participants": [
    "at://did:plc:player01/world.ptah.character/ace",
    "at://did:plc:player02/world.ptah.character/deuce",
    "at://did:plc:player03/world.ptah.character/spook",
    "at://did:plc:player04/world.ptah.character/shadow"
  ],
  "stakes": "Season title. Bragging rights. Your name in the permanent record.",
  "status": "completed",
  "result": "Team South wins 502–380. Spook went nil in the final round and made it. Shadow counted every card to cover. Team North went set trying to block the nil.",
  "witnesses": [
    "at://did:plc:spectator01/world.ptah.action/witness-championship"
  ],
  "locationReference": "at://did:plc:spadeshost01/world.ptah.location/the-table",
  "loreStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-05T19:00:00Z",
  "completedAt": "2026-04-05T22:00:00Z"
}
```

**AT URI:** `at://did:plc:spadeshost01/world.ptah.event/championship-spring-2026`

`format: singleElimination` — this field hasn't been exercised in either literary world. Here it defines the tournament structure.

---

### Record 11 — Lore: The Spring 2026 Season Record

```json
{
  "$type": "world.ptah.lore",
  "title": "Spring 2026 Season — The Nil That Won It",
  "worldReference": "at://did:plc:spadeshost01/world.ptah.world/blacksky-spades",
  "creatorDID": "did:plc:spadeshost01",
  "content": "The Spring 2026 Championship came down to one call. Team South was up 40 points going into the final round. Spook bid nil — the first nil bid of the entire match. Shadow counted the remaining spades and covered every lead. Team North tried to force a spade onto Spook three times. Three times Shadow cut in front. Final score: 502–380. The nil held. The season belongs to Team South.",
  "sourceReferences": [
    "at://did:plc:player01/world.ptah.action/bid-round1",
    "at://did:plc:player03/world.ptah.action/play-round1",
    "at://did:plc:spadeshost01/world.ptah.event/championship-spring-2026"
  ],
  "characters": [
    "at://did:plc:player01/world.ptah.character/ace",
    "at://did:plc:player02/world.ptah.character/deuce",
    "at://did:plc:player03/world.ptah.character/spook",
    "at://did:plc:player04/world.ptah.character/shadow"
  ],
  "timelinePosition": "Spring 2026 Season — Championship",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "authorshipRecord": "did:plc:spadeshost01",
  "contributionType": "originator",
  "createdAt": "2026-04-05T23:00:00Z"
}
```

**AT URI:** `at://did:plc:spadeshost01/world.ptah.lore/spring-2026-season`

The `sourceReferences` trace the season record back to the specific actions and events that produced it. The lore isn't a narrative someone made up — it's a record of what happened, verifiable against the action records.

---

# World 4: The Shattered Reach — A Tabletop RPG Campaign

## Why This World

Spades shows structured competition with concrete outcomes. A tabletop RPG campaign shows the opposite end of the competitive spectrum — open-ended collaborative storytelling where a Game Master runs sessions, players control persistent characters, outcomes are driven by dice and decisions, and history accumulates over weeks or months of play.

This world tests: characters with progression (abilities, affiliations that change over time), a GM as a distinct participant type, sessions as Events rather than tournaments, Actions driven by gameplay mechanics rather than pure narrative, and Lore that serves as a campaign journal — the living memory of a group's shared adventure.

The core mechanics reference the D&D 5th Edition SRD, which was released under Creative Commons (CC BY 4.0) in 2023, making the game system itself open for use.

## What This Chain Contains

- 1 World record
- 3 Character records (two player characters, one GM-controlled NPC)
- 1 Location record (The Shattered Reach)
- 2 Action records (a player action, a GM ruling)
- 1 Event record (Session 1)
- 1 Lore record (Campaign journal entry)
- 1 Contribution record (a new player joining the campaign)

Total: 10 records.

---

### Record 1 — World: The Shattered Reach

```json
{
  "$type": "world.ptah.world",
  "name": "The Shattered Reach",
  "creatorDID": "did:plc:gm01",
  "description": "A homebrew campaign world. The northern coast was shattered by a magical cataclysm a century ago. The islands that remain are connected by unstable bridges of frozen arcane energy. Three factions fight for control of the bridges. The party landed on the wrong island at the wrong time.",
  "sourceType": "world.ptah.defs#sourceTypeCollaborativeCommons",
  "governanceMode": "governed",
  "renderingHints": {
    "tone": "epic, dangerous, weird",
    "era": "post-cataclysm fantasy",
    "genre": "tabletop RPG, high fantasy",
    "aesthetic": "shattered coastline, frozen magic, rope bridges, lantern light"
  },
  "createdAt": "2026-04-01T00:00:00Z"
}
```

**AT URI:** `at://did:plc:gm01/world.ptah.world/shattered-reach`

`sourceType: collaborativeCommons` — a tabletop campaign is inherently collaborative. The GM creates the world but the players shape it through play. `governanceMode: governed` — the GM has final say on canon.

---

### Record 2 — Character: Player Character — Kael

```json
{
  "$type": "world.ptah.character",
  "name": "Kael Thornwood",
  "creatorDID": "did:plc:player05",
  "worldReference": "at://did:plc:gm01/world.ptah.world/shattered-reach",
  "description": "Half-elf ranger. Survived the crossing from the mainland. Doesn't talk about what happened on the boat. Tracks everything. Trusts nothing.",
  "controlType": "exclusive",
  "originType": "world.ptah.defs#sourceTypeOriginalIP",
  "properties": {
    "species": "Half-elf",
    "role": "Ranger",
    "abilities": "Favored terrain: coastal. Fighting style: archery. Carries a longbow named Tide.",
    "affiliation": "Unaffiliated — arrived as an outsider"
  },
  "authorshipRecord": "did:plc:player05",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:01:00Z"
}
```

**AT URI:** `at://did:plc:player05/world.ptah.character/kael`

The `properties` object gets real use here — species, class, abilities, and affiliation all matter for gameplay.

---

### Record 3 — Character: Player Character — Senna

```json
{
  "$type": "world.ptah.character",
  "name": "Senna Ashveil",
  "creatorDID": "did:plc:player06",
  "worldReference": "at://did:plc:gm01/world.ptah.world/shattered-reach",
  "description": "Tiefling warlock. Made a pact she won't explain. The magic works. The cost is unclear. She smiles too much for someone carrying that kind of debt.",
  "controlType": "exclusive",
  "originType": "world.ptah.defs#sourceTypeOriginalIP",
  "properties": {
    "species": "Tiefling",
    "role": "Warlock",
    "abilities": "Eldritch blast. Pact of the Tome. Patron: unknown (GM secret).",
    "affiliation": "Unaffiliated — won't say where she came from"
  },
  "authorshipRecord": "did:plc:player06",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:02:00Z"
}
```

**AT URI:** `at://did:plc:player06/world.ptah.character/senna`

---

### Record 4 — Character: NPC — The Bridge Keeper

```json
{
  "$type": "world.ptah.character",
  "name": "The Bridge Keeper of Voss",
  "creatorDID": "did:plc:gm01",
  "worldReference": "at://did:plc:gm01/world.ptah.world/shattered-reach",
  "description": "Nobody knows her real name. She controls the last stable bridge between the outer islands and the mainland fragment. Charges a toll — not in gold. In favors. The favors always come due at the worst possible time.",
  "controlType": "exclusive",
  "originType": "world.ptah.defs#sourceTypeOriginalIP",
  "properties": {
    "species": "Human (probably)",
    "role": "NPC — quest giver, gatekeeper",
    "abilities": "Unknown. The bridge obeys her. That's enough.",
    "affiliation": "The Bridge — no faction, no allegiance"
  },
  "authorshipRecord": "did:plc:gm01",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:03:00Z"
}
```

**AT URI:** `at://did:plc:gm01/world.ptah.character/bridge-keeper`

Created by the GM's DID, not a player. The `controlType: exclusive` means only the GM controls this NPC.

---

### Record 5 — Location: The Shattered Reach (Region)

```json
{
  "$type": "world.ptah.location",
  "name": "The Shattered Reach",
  "creatorDID": "did:plc:gm01",
  "worldReference": "at://did:plc:gm01/world.ptah.world/shattered-reach",
  "description": "What used to be a continuous northern coastline is now an archipelago of jagged islands connected by bridges of frozen arcane energy. The bridges hum. Some of them flicker. The locals say the flickering ones are dying.",
  "locationType": "region",
  "depthIndex": 0,
  "properties": {
    "climate": "Cold coastal. Permanent fog at sea level. Clear and biting wind above the bridge line.",
    "population": "Scattered settlements on the larger islands. Maybe 3,000 total.",
    "controllingFaction": "Contested — three factions, none dominant",
    "notableHistory": "The Shattering occurred roughly 100 years ago. No one agrees on the cause."
  },
  "authorshipRecord": "did:plc:gm01",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:04:00Z"
}
```

**AT URI:** `at://did:plc:gm01/world.ptah.location/shattered-reach-region`

`depthIndex: 0` — this is the top-level region. Future locations (specific islands, the bridge, towns) would nest under it via `parentLocation`.

---

### Record 6 — Action: Kael Makes a Perception Check

```json
{
  "$type": "world.ptah.action",
  "actorDID": "did:plc:player05",
  "characterReference": "at://did:plc:player05/world.ptah.character/kael",
  "worldReference": "at://did:plc:gm01/world.ptah.world/shattered-reach",
  "actionType": "creation",
  "content": "Kael rolls Perception at the bridge approach. Natural 18 + 5 modifier = 23. He spots runes carved into the underside of the bridge supports — they're not part of the original construction. Someone added them recently. They pulse faintly in the same rhythm as the bridge's hum.",
  "locationReference": "at://did:plc:gm01/world.ptah.location/shattered-reach-region",
  "visibility": "canon",
  "createdAt": "2026-04-08T19:30:00Z"
}
```

**AT URI:** `at://did:plc:player05/world.ptah.action/perception-check-bridge`

The action content includes the mechanical roll and the narrative result. Both are part of the permanent record.

---

### Record 7 — Action: The GM Rules

```json
{
  "$type": "world.ptah.action",
  "actorDID": "did:plc:gm01",
  "characterReference": "at://did:plc:gm01/world.ptah.character/bridge-keeper",
  "worldReference": "at://did:plc:gm01/world.ptah.world/shattered-reach",
  "actionType": "speech",
  "content": "The Bridge Keeper steps out of the fog. 'You saw the runes.' It's not a question. She looks at Kael, then at Senna. 'The bridge is dying. Someone is killing it on purpose. I'll let you cross for free — if you find out who.' She holds out two iron tokens. 'One crossing each. Don't lose them.'",
  "locationReference": "at://did:plc:gm01/world.ptah.location/shattered-reach-region",
  "visibility": "canon",
  "createdAt": "2026-04-08T19:35:00Z"
}
```

**AT URI:** `at://did:plc:gm01/world.ptah.action/bridge-keeper-offer`

The GM acts through the NPC. The `actorDID` is the GM. The `characterReference` is the Bridge Keeper. The distinction between player and character is preserved.

---

### Record 8 — Contribution: A New Player Joins

A third player joins the campaign in session 2.

```json
{
  "$type": "world.ptah.contribution",
  "contributorDID": "did:plc:player07",
  "worldReference": "at://did:plc:gm01/world.ptah.world/shattered-reach",
  "contributionType": "character",
  "recordReference": "at://did:plc:player07/world.ptah.character/new-pc",
  "originatorApproval": "approved",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "attributionChain": [
    "at://did:plc:gm01/world.ptah.world/shattered-reach"
  ],
  "createdAt": "2026-04-15T00:00:00Z"
}
```

**AT URI:** `at://did:plc:player07/world.ptah.contribution/join-campaign`

`originatorApproval: approved` — unlike the public domain worlds where contribution is pre-approved, a tabletop campaign requires the GM to approve new players. The GM governs the world.

---

### Record 9 — Event: Session 1 — The Bridge

```json
{
  "$type": "world.ptah.event",
  "name": "Session 1 — The Bridge",
  "creatorDID": "did:plc:gm01",
  "worldReference": "at://did:plc:gm01/world.ptah.world/shattered-reach",
  "eventType": "gathering",
  "participants": [
    "at://did:plc:player05/world.ptah.character/kael",
    "at://did:plc:player06/world.ptah.character/senna",
    "at://did:plc:gm01/world.ptah.character/bridge-keeper"
  ],
  "stakes": "Free passage across the last stable bridge. The party needs to reach the inner islands. The Bridge Keeper's price: find out who's killing the bridges.",
  "status": "completed",
  "result": "The party accepted the Bridge Keeper's offer. Kael took both iron tokens. Senna tried to Insight check the Bridge Keeper and rolled a 4. The Keeper smiled. Session ended at the bridge crossing.",
  "witnesses": [],
  "locationReference": "at://did:plc:gm01/world.ptah.location/shattered-reach-region",
  "loreStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-08T19:00:00Z",
  "completedAt": "2026-04-08T22:00:00Z"
}
```

**AT URI:** `at://did:plc:gm01/world.ptah.event/session-1`

`witnesses: []` — an empty array. This is a private campaign session, not a public tournament. No spectators. The protocol handles both cases — witnessed events and unwitnessed events — without breaking.

---

### Record 10 — Lore: Campaign Journal — Session 1

```json
{
  "$type": "world.ptah.lore",
  "title": "Session 1 — The Bridge Keeper's Bargain",
  "worldReference": "at://did:plc:gm01/world.ptah.world/shattered-reach",
  "creatorDID": "did:plc:gm01",
  "content": "The party arrived at the last stable bridge in the Shattered Reach. Kael spotted sabotage runes on the supports — someone is deliberately destabilizing the bridges. The Bridge Keeper offered free passage in exchange for finding the saboteur. The party accepted. Kael holds both crossing tokens. Senna failed to read the Keeper's intentions. The Keeper knows more than she's saying. The bridge hummed under their feet as they crossed. It flickered once.",
  "sourceReferences": [
    "at://did:plc:player05/world.ptah.action/perception-check-bridge",
    "at://did:plc:gm01/world.ptah.action/bridge-keeper-offer",
    "at://did:plc:gm01/world.ptah.event/session-1"
  ],
  "characters": [
    "at://did:plc:player05/world.ptah.character/kael",
    "at://did:plc:player06/world.ptah.character/senna",
    "at://did:plc:gm01/world.ptah.character/bridge-keeper"
  ],
  "timelinePosition": "Campaign Week 1 — Arrival at the Reach",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "authorshipRecord": "did:plc:gm01",
  "contributionType": "originator",
  "createdAt": "2026-04-08T23:00:00Z"
}
```

**AT URI:** `at://did:plc:gm01/world.ptah.lore/session-1-journal`

The campaign journal is Lore — traceable back to the specific actions and events of the session. Next week's session builds on this. The history accumulates. The campaign becomes a world with a permanent, verifiable record of everything that happened in it.

---

## What All Four Worlds Demonstrate Together

| World | Type | Tests |
|---|---|---|
| **Hamlet** | Literary, public domain | Role/Instance split, contested canon, multiple embodiments of shared characters |
| **Gatsby** | Literary, public domain | Social performance, unreliable narration, gatherings as events |
| **Blacksky Spades** | Structured competition | Tournament format, scoring, brackets, competitive witnesses, season records |
| **The Shattered Reach** | Collaborative RPG campaign | GM/player dynamics, character progression, sessions as events, campaign journals as lore |

The same eight record types express all four worlds without modification. Literary world-building. Social narrative. Competitive card games. Tabletop RPG campaigns. The protocol doesn't care what kind of world you're building. It cares that authorship travels, history is verifiable, and every contribution traces back to the person who made it.

The schema holds all four worlds. It will hold yours.
