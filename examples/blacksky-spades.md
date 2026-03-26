# World 3: Blacksky Spades — A Competitive Tournament

## Why This World

RENAISSANCE and the MCU demonstrate world-building with complex attribution and franchise-scale IP. Spades demonstrates the other half of what the protocol was built for — structured competitive events with brackets, rounds, winners, and results that become permanent history.

This world tests: the full `status` lifecycle (`scheduled` → `active` → `completed`), multiple Events chaining into a tournament arc, witnesses as real attestation records during competitive play, and Log entries that read like a season record rather than a narrative.

Spades is culturally aligned with Blacksky, where the protocol lives. It's a game people already play online. The tournament structure is immediately recognizable.

## What This Chain Contains

- 1 World record
- 4 Character records (four players forming two teams)
- 1 Location record (The Table)
- 3 Action records (a bid, a play, a witness)
- 1 Event record (Championship Match)
- 1 Log record (Season record)

Total: 11 records. No Template record — Spades players are themselves, not instances of a shared identity.

---

### Record 1 — World: Blacksky Spades

```json
{
  "$type": "world.ptah.world",
  "name": "Blacksky Spades",
  "creatorDID": "did:plc:spadeshost01",
  "description": "Competitive Spades on the open network. Partners, bids, books, and Boston. Every hand is recorded. Every result is permanent. Talk your trash — it's on the record too.",
  "sourceType": "originalIP",
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
  "originType": "originalIP",
  "characterProperties": {
    "affiliation": "Team North"
  },
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
  "originType": "originalIP",
  "characterProperties": {
    "affiliation": "Team North"
  },
  "createdAt": "2026-04-01T00:02:00Z"
}
```

**AT URI:** `at://did:plc:player02/world.ptah.character/deuce`

---

### Record 4 — Character: Player 3 (Team South)

```json
{
  "$type": "world.ptah.character",
  "name": "Blitz",
  "creatorDID": "did:plc:player03",
  "worldReference": "at://did:plc:spadeshost01/world.ptah.world/blacksky-spades",
  "description": "Team South. Overbids every round. Somehow makes it work.",
  "controlType": "exclusive",
  "originType": "originalIP",
  "characterProperties": {
    "affiliation": "Team South"
  },
  "createdAt": "2026-04-01T00:03:00Z"
}
```

**AT URI:** `at://did:plc:player03/world.ptah.character/blitz`

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
  "originType": "originalIP",
  "characterProperties": {
    "affiliation": "Team South"
  },
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
  "locationType": "virtual",
  "depthIndex": 1,
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:05:00Z"
}
```

**AT URI:** `at://did:plc:spadeshost01/world.ptah.location/the-table`

`locationType: virtual` — the table isn't a physical place. It's wherever the game happens.

---

### Record 7 — Action: The Bid

```json
{
  "$type": "world.ptah.action",
  "actorDID": "did:plc:player01",
  "characterReference": "at://did:plc:player01/world.ptah.character/ace",
  "worldReference": "at://did:plc:spadeshost01/world.ptah.world/blacksky-spades",
  "actionType": "dialogue",
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
  "characterReference": "at://did:plc:player03/world.ptah.character/blitz",
  "worldReference": "at://did:plc:spadeshost01/world.ptah.world/blacksky-spades",
  "actionType": "competitive",
  "content": "Blitz cuts with the Queen of Spades on a Heart lead. Takes the book. Team South now has 7 — one over their bid. Sandbag watch is on.",
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
  "eventType": "competition",
  "participants": [
    "at://did:plc:player01/world.ptah.character/ace",
    "at://did:plc:player02/world.ptah.character/deuce",
    "at://did:plc:player03/world.ptah.character/blitz",
    "at://did:plc:player04/world.ptah.character/shadow"
  ],
  "stakes": "Season title. Bragging rights. Your name in the permanent record.",
  "status": "completed",
  "result": "Team South wins 502–380. Blitz went nil in the final round and made it. Shadow counted every card to cover. Team North went set trying to block the nil.",
  "witnesses": [
    "at://did:plc:spectator01/world.ptah.action/witness-championship"
  ],
  "locationReference": "at://did:plc:spadeshost01/world.ptah.location/the-table",
  "startTime": "2026-04-05T19:00:00Z",
  "endTime": "2026-04-05T22:00:00Z",
  "createdAt": "2026-04-05T19:00:00Z"
}
```

**AT URI:** `at://did:plc:spadeshost01/world.ptah.event/championship-spring-2026`

`eventType: competition` — the same record type that holds franchise conflicts also holds tournament matches. The `stakes` and `result` fields do the heavy lifting.

---

### Record 11 — Log: The Spring 2026 Season Record

```json
{
  "$type": "world.ptah.log",
  "title": "Spring 2026 Season — The Nil That Won It",
  "worldReference": "at://did:plc:spadeshost01/world.ptah.world/blacksky-spades",
  "creatorDID": "did:plc:spadeshost01",
  "logType": "article",
  "summary": "Spring 2026 Championship final — Team South wins on a nil bid in the last round.",
  "content": "The Spring 2026 Championship came down to one call. Team South was up 40 points going into the final round. Blitz bid nil — the first nil bid of the entire match. Shadow counted the remaining spades and covered every lead. Team North tried to force a spade onto Blitz three times. Three times Shadow cut in front. Final score: 502–380. The nil held. The season belongs to Team South.",
  "sourceReferences": [
    "at://did:plc:player01/world.ptah.action/bid-round1",
    "at://did:plc:player03/world.ptah.action/play-round1",
    "at://did:plc:spadeshost01/world.ptah.event/championship-spring-2026"
  ],
  "characters": [
    "at://did:plc:player01/world.ptah.character/ace",
    "at://did:plc:player02/world.ptah.character/deuce",
    "at://did:plc:player03/world.ptah.character/blitz",
    "at://did:plc:player04/world.ptah.character/shadow"
  ],
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-05T23:00:00Z"
}
```

**AT URI:** `at://did:plc:spadeshost01/world.ptah.log/spring-2026-season`

The `sourceReferences` trace the season record back to the specific actions and events that produced it. The log isn't a narrative someone made up — it's a record of what happened, verifiable against the action records.

---
