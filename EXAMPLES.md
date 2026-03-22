# Example World Record Chains

Two complete example worlds demonstrating how the Ptah Protocol's eight record types connect, reference each other via AT URIs, and express different kinds of creative worlds.

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

## What These Two Worlds Demonstrate Together

**Hamlet** tests the protocol's hardest public domain problem: a universally known work with contested interpretations, where multiple people need to embody the same character simultaneously. The Role/Instance split, `controlType`, and `canonicalCharacterReference` are all exercised.

**Gatsby** tests a different kind of world: social performance rather than political violence, gatherings rather than battles, lore built from unreliable narration rather than witnessed combat. The same eight record types express both worlds without modification.

Both worlds show:
- A world originator seeding the foundation
- A contributor adding their own interpretation
- Multiple Character instances of the same Role, attributed to different creators
- Actions generating history that becomes verifiable Lore
- Events with witnesses — real action records, not just a count
- The `attributionChain` tracing provenance through every contribution

The schema holds both worlds. It will hold yours.
