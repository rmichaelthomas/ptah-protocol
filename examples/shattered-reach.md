# World 4: The Shattered Reach — A Tabletop RPG Campaign

## Why This World

Spades shows structured competition with concrete outcomes. A tabletop RPG campaign shows the opposite end of the competitive spectrum — open-ended collaborative storytelling where a Game Master runs sessions, players control persistent characters, outcomes are driven by dice and decisions, and history accumulates over weeks or months of play.

This world tests: characters with progression (abilities, affiliations that change over time), a GM as a distinct participant type, sessions as Events rather than competitions, Actions driven by gameplay mechanics rather than pure narrative, and Log entries that serve as a campaign journal — the living memory of a group's shared adventure.

The core mechanics reference the D&D 5th Edition SRD, which was released under Creative Commons (CC BY 4.0) in 2023, making the game system itself open for use.

## What This Chain Contains

- 1 World record
- 3 Character records (two player characters, one GM-controlled NPC)
- 1 Location record (The Shattered Reach)
- 2 Action records (a player action, a GM ruling)
- 1 Event record (Session 1)
- 1 Log record (Campaign journal entry)
- 1 Origin record (a new player joining the campaign)

Total: 10 records.

---

### Record 1 — World: The Shattered Reach

```json
{
  "$type": "world.ptah.world",
  "name": "The Shattered Reach",
  "creatorDID": "did:plc:gm01",
  "description": "A homebrew campaign world. The northern coast was shattered by a magical cataclysm a century ago. The islands that remain are connected by unstable bridges of frozen arcane energy. Three factions fight for control of the bridges. The party landed on the wrong island at the wrong time.",
  "sourceType": "collaborativeCommons",
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
  "originType": "originalIP",
  "characterProperties": {
    "species": "Half-elf",
    "role": "Ranger",
    "abilities": "Favored terrain: coastal. Fighting style: archery. Carries a longbow named Tide.",
    "affiliation": "Unaffiliated — arrived as an outsider"
  },
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:01:00Z"
}
```

**AT URI:** `at://did:plc:player05/world.ptah.character/kael`

The `characterProperties` object gets real use here — species, class, abilities, and affiliation all matter for gameplay.

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
  "originType": "originalIP",
  "characterProperties": {
    "species": "Tiefling",
    "role": "Warlock",
    "abilities": "Eldritch blast. Pact of the Tome. Patron: unknown (GM secret).",
    "affiliation": "Unaffiliated — won't say where she came from"
  },
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
  "originType": "originalIP",
  "characterProperties": {
    "species": "Human (probably)",
    "role": "NPC — quest giver, gatekeeper",
    "abilities": "Unknown. The bridge obeys her. That's enough.",
    "affiliation": "The Bridge — no faction, no allegiance"
  },
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
  "locationType": "territory",
  "depthIndex": 0,
  "locationProperties": {
    "climate": "Cold coastal. Permanent fog at sea level. Clear and biting wind above the bridge line.",
    "population": "Scattered settlements on the larger islands. Maybe 3,000 total.",
    "controllingFaction": "Contested — three factions, none dominant",
    "notableHistory": "The Shattering occurred roughly 100 years ago. No one agrees on the cause."
  },
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
  "actionType": "narrative",
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
  "actionType": "dialogue",
  "content": "The Bridge Keeper steps out of the fog. 'You saw the runes.' It's not a question. She looks at Kael, then at Senna. 'The bridge is dying. Someone is killing it on purpose. I'll let you cross for free — if you find out who.' She holds out two iron tokens. 'One crossing each. Don't lose them.'",
  "locationReference": "at://did:plc:gm01/world.ptah.location/shattered-reach-region",
  "visibility": "canon",
  "createdAt": "2026-04-08T19:35:00Z"
}
```

**AT URI:** `at://did:plc:gm01/world.ptah.action/bridge-keeper-offer`

The GM acts through the NPC. The `actorDID` is the GM. The `characterReference` is the Bridge Keeper. The distinction between player and character is preserved.

---

### Record 8 — Origin: A New Player Joins

A third player joins the campaign in session 2.

```json
{
  "$type": "world.ptah.origin",
  "contributorDID": "did:plc:player07",
  "worldReference": "at://did:plc:gm01/world.ptah.world/shattered-reach",
  "contributionType": "contributor",
  "targetReference": "at://did:plc:player07/world.ptah.character/new-pc",
  "originatorApproval": "approved",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "attributionChain": [
    {
      "contributorDID": "did:plc:gm01",
      "role": "originator"
    }
  ],
  "publicDomainCompliance": "notApplicable",
  "createdAt": "2026-04-15T00:00:00Z"
}
```

**AT URI:** `at://did:plc:player07/world.ptah.origin/join-campaign`

`originatorApproval: approved` — unlike RENAISSANCE where the originator curates featured artists, a tabletop campaign requires the GM to approve new players. The GM governs the world.

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
  "startTime": "2026-04-08T19:00:00Z",
  "endTime": "2026-04-08T22:00:00Z",
  "createdAt": "2026-04-08T19:00:00Z"
}
```

**AT URI:** `at://did:plc:gm01/world.ptah.event/session-1`

`witnesses: []` — an empty array. This is a private campaign session, not a public tournament. No spectators. The protocol handles both cases — witnessed events and unwitnessed events — without breaking.

---

### Record 10 — Log: Campaign Journal — Session 1

```json
{
  "$type": "world.ptah.log",
  "title": "Session 1 — The Bridge Keeper's Bargain",
  "worldReference": "at://did:plc:gm01/world.ptah.world/shattered-reach",
  "creatorDID": "did:plc:gm01",
  "logType": "entry",
  "summary": "The party reaches the last stable bridge, discovers sabotage, and accepts the Bridge Keeper's bargain.",
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
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-08T23:00:00Z"
}
```

**AT URI:** `at://did:plc:gm01/world.ptah.log/session-1-journal`

The campaign journal is a Log entry — traceable back to the specific actions and events of the session. Next week's session builds on this. The history accumulates. The campaign becomes a world with a permanent, verifiable record of everything that happened in it.

---
