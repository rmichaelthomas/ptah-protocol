# World 2: The Marvel Cinematic Universe — Franchise as World

## Why This World

The MCU is the Template/Character showcase. Iron Man is not Tony Stark. Iron Man is the mantle — the identity that exists independent of who wears it. Tony Stark is one Character instance of that Template. Rhodey as War Machine is another. The MCU tests what happens when intellectual property operates at franchise scale — hundreds of characters, dozens of films, a shared continuity, and a corporate originator whose attribution chain runs through decades of comics creators.

This world demonstrates all fourteen record types, with particular emphasis on Template, Collection, Trace, and Version.

## What This Chain Contains

- 1 World record
- 1 Template record (Iron Man)
- 2 Character records (Tony Stark, Pepper Potts)
- 2 Location records (Avengers Tower, Stark Industries R&D Lab)
- 1 Action record ("I Am Iron Man")
- 1 Event record (The Battle of New York)
- 1 Log record (The Avengers Chronicle)
- 1 Origin record (Stan Lee → Iron Man)
- 1 Collection record (MCU Phase One)
- 1 Trace record (Comics to Film)
- 1 Usage record (MCU Franchise Terms)
- 1 Version record (Phase One Release)

Total: 14 records across all 14 record types.

---

### Record 1 — World: The Marvel Cinematic Universe

```json
{
  "$type": "world.ptah.world",
  "name": "The Marvel Cinematic Universe",
  "creatorDID": "did:plc:mcu01",
  "description": "A shared cinematic universe built from sixty years of comics. One continuity. Dozens of films. Hundreds of characters. A single corporate originator controlling canon across every medium. The MCU is what happens when world-building becomes an industrial process — and the industry is worth billions.",
  "sourceType": "originalIP",
  "governanceMode": "governed",
  "renderingHints": {
    "tone": "heroic, quippy, high-stakes",
    "era": "contemporary Earth with advanced technology",
    "genre": "superhero, science fiction, action",
    "aesthetic": "repulsor glow, vibranium sheen, New York skylines, third-act beam in the sky"
  },
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:00:00Z"
}
```

**AT URI:** `at://did:plc:mcu01/world.ptah.world/mcu`

`governanceMode: governed` — Marvel Studios controls what is and isn't canon. This is not a sandbox. You don't get to add an Avenger without approval.

---

### Record 2 — Template: Iron Man

The mantle. The identity. Not Tony Stark — the concept of Iron Man. The suit, the name, the role in the Avengers. Tony Stark is one person who wore it. He won't be the last.

```json
{
  "$type": "world.ptah.template",
  "name": "Iron Man",
  "creatorDID": "did:plc:mcu01",
  "worldReference": "at://did:plc:mcu01/world.ptah.world/mcu",
  "description": "The armored Avenger. A mantle defined by the suit, not the wearer. The identity has outlived its first bearer in the comics and will outlive him in the films. Iron Man is a role — genius, billionaire, or otherwise — that someone steps into.",
  "originType": "originalIP",
  "canonicalCharacterReference": "at://did:plc:mcu01/world.ptah.character/tony-stark",
  "canonicalReferencePolicy": "updatable",
  "instancePolicy": "restricted",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:01:00Z"
}
```

**AT URI:** `at://did:plc:mcu01/world.ptah.template/iron-man`

`instancePolicy: restricted` — Marvel decides who wears the suit. `canonicalReferencePolicy: updatable` because the canonical Iron Man can change — and in the comics, it already has.

---

### Record 3 — Character: Tony Stark

The first and canonical instance of the Iron Man template. The man who built the suit in a cave.

```json
{
  "$type": "world.ptah.character",
  "name": "Tony Stark",
  "creatorDID": "did:plc:mcu01",
  "worldReference": "at://did:plc:mcu01/world.ptah.world/mcu",
  "templateReference": "at://did:plc:mcu01/world.ptah.template/iron-man",
  "description": "Genius. Billionaire. The man who built the first suit in a cave in Afghanistan with a box of scraps, then spent a decade upgrading it. Founding Avenger. Died closing a portal. The MCU started with him and ended its first saga with him.",
  "controlType": "exclusive",
  "originType": "originalIP",
  "characterProperties": {
    "species": "human",
    "affiliation": "Avengers, Stark Industries",
    "abilities": "genius-level intellect, powered armor, arc reactor technology",
    "role": "founding Avenger, Iron Man (primary)"
  },
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:02:00Z"
}
```

**AT URI:** `at://did:plc:mcu01/world.ptah.character/tony-stark`

This is the character that `canonicalCharacterReference` on the Iron Man Template points to. Tony Stark is Iron Man — for now. The `updatable` policy on the Template means this pointer can change.

---

### Record 4 — Character: Pepper Potts

No `templateReference` — Pepper Potts is not an instance of a shared mantle. She is her own character. Not every character needs the Template/Instance split.

```json
{
  "$type": "world.ptah.character",
  "name": "Pepper Potts",
  "creatorDID": "did:plc:mcu01",
  "worldReference": "at://did:plc:mcu01/world.ptah.world/mcu",
  "description": "CEO of Stark Industries. The person who kept the company running while Tony was in the suit. Wore the Rescue armor once. Didn't need it to be the most important person in the room.",
  "controlType": "exclusive",
  "originType": "originalIP",
  "characterProperties": {
    "species": "human",
    "affiliation": "Stark Industries",
    "abilities": "corporate leadership, Extremis exposure (temporary), Rescue armor (temporary)",
    "role": "CEO, Tony Stark's partner"
  },
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:03:00Z"
}
```

**AT URI:** `at://did:plc:mcu01/world.ptah.character/pepper-potts`

Pepper briefly wore armor, but she's not an instance of the Iron Man Template. Wearing a suit once doesn't make you the mantle. The Template pattern is for persistent shared identities, not borrowed equipment.

---

### Record 5 — Location: Avengers Tower, Manhattan

```json
{
  "$type": "world.ptah.location",
  "name": "Avengers Tower",
  "creatorDID": "did:plc:mcu01",
  "worldReference": "at://did:plc:mcu01/world.ptah.world/mcu",
  "description": "Originally Stark Tower. Rebuilt after the Battle of New York with a giant A on the side. The operational headquarters of the Avengers during Phase One and Two. Midtown Manhattan. Ninety-three floors of glass, steel, and arc reactor power.",
  "locationType": "building",
  "depthIndex": 2,
  "locationProperties": {
    "climate": "Manhattan — four seasons, rooftop wind, helicopter noise",
    "population": "Avengers roster plus Stark Industries staff",
    "controllingFaction": "Stark Industries / The Avengers",
    "notableHistory": "Formerly Stark Tower. Damaged during the Chitauri invasion. Rebuilt as Avengers HQ."
  },
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:04:00Z"
}
```

**AT URI:** `at://did:plc:mcu01/world.ptah.location/avengers-tower`

---

### Record 6 — Location: Stark Industries R&D Lab

Nested inside Avengers Tower via `parentLocation`. This is where the suits get built.

```json
{
  "$type": "world.ptah.location",
  "name": "Stark Industries R&D Lab",
  "creatorDID": "did:plc:mcu01",
  "worldReference": "at://did:plc:mcu01/world.ptah.world/mcu",
  "description": "Sub-level workshop inside Avengers Tower. Holographic displays, robotic assembly arms, a fleet of Iron Man suits on the walls. JARVIS runs the room. Tony talks to the machines and the machines talk back.",
  "locationType": "room",
  "parentLocation": "at://did:plc:mcu01/world.ptah.location/avengers-tower",
  "depthIndex": 3,
  "locationProperties": {
    "controllingFaction": "Tony Stark, personal access only",
    "notableHistory": "Where the Mark suits were designed and built. Where Ultron was born."
  },
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:05:00Z"
}
```

**AT URI:** `at://did:plc:mcu01/world.ptah.location/stark-rd-lab`

`parentLocation` creates the nesting. The R&D Lab is inside Avengers Tower. `depthIndex: 3` reflects the hierarchy: world (0) → city (1) → building (2) → room (3).

---

### Record 7 — Action: "I Am Iron Man"

The press conference at the end of Iron Man (2008). The moment Tony Stark threw out the prepared cover story and told the world who he was. Every other superhero kept the secret. Stark held a press conference.

```json
{
  "$type": "world.ptah.action",
  "actorDID": "did:plc:mcu01",
  "worldReference": "at://did:plc:mcu01/world.ptah.world/mcu",
  "characterReference": "at://did:plc:mcu01/world.ptah.character/tony-stark",
  "actionType": "dialogue",
  "content": "Tony Stark stands at the podium. Agent Coulson's cover story is on the cards in front of him. He looks at the press corps, sets the cards down, and says it: 'I am Iron Man.' No secret identity. No mask. The MCU starts here — with a man who refuses to hide.",
  "visibility": "canon",
  "narrativeWeight": 10,
  "createdAt": "2026-04-01T00:06:00Z"
}
```

**AT URI:** `at://did:plc:mcu01/world.ptah.action/i-am-iron-man`

`narrativeWeight: 10` — this is the defining action of the entire franchise. It set the tone for twenty-three films.

---

### Record 8 — Event: The Battle of New York

The Avengers assemble for the first time. The Chitauri pour through a portal over Manhattan. Six people hold the line.

```json
{
  "$type": "world.ptah.event",
  "name": "The Battle of New York",
  "creatorDID": "did:plc:mcu01",
  "worldReference": "at://did:plc:mcu01/world.ptah.world/mcu",
  "description": "The Chitauri invasion of Manhattan. Loki opens a portal above Stark Tower using the Tesseract. The Avengers — assembled for the first time — hold the city block by block. Stark flies a nuclear missile through the portal and closes it from the other side.",
  "eventType": "conflict",
  "locationReference": "at://did:plc:mcu01/world.ptah.location/avengers-tower",
  "participants": [
    "at://did:plc:mcu01/world.ptah.character/tony-stark"
  ],
  "status": "completed",
  "stakes": "Manhattan. Earth. The first public confirmation that humanity is not alone in the universe.",
  "result": "Portal closed. Chitauri defeated. Stark survived the fall. The Avengers became a symbol. The world changed permanently.",
  "witnesses": [
    "at://did:plc:viewer01/world.ptah.action/witness-new-york"
  ],
  "startTime": "2026-04-01T12:00:00Z",
  "endTime": "2026-04-01T15:00:00Z",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:07:00Z"
}
```

**AT URI:** `at://did:plc:mcu01/world.ptah.event/battle-of-new-york`

The `participants` array here shows only Tony Stark for brevity — a full implementation would include all six original Avengers as Character records.

---

### Record 9 — Log: The Avengers Chronicle

```json
{
  "$type": "world.ptah.log",
  "title": "The Avengers Chronicle — How Six People Held New York",
  "creatorDID": "did:plc:mcu01",
  "worldReference": "at://did:plc:mcu01/world.ptah.world/mcu",
  "logType": "chronicle",
  "summary": "The narrative account of the first Avengers team-up: from Loki's arrival to the Battle of New York to the shawarma.",
  "content": "They were never supposed to work together. A billionaire in a suit. A soldier out of time. A god. A spy. Another spy. A rage monster. Fury's gamble was that the crisis would be bigger than the egos. He was barely right. Loki opened a portal over Manhattan and the Chitauri came through. The team held the perimeter. Stark flew the nuke through the portal. The portal closed. Stark fell. The Hulk caught him. Then they ate shawarma. The Avengers Initiative was no longer theoretical.",
  "sourceReferences": [
    "at://did:plc:mcu01/world.ptah.action/i-am-iron-man",
    "at://did:plc:mcu01/world.ptah.event/battle-of-new-york"
  ],
  "characters": [
    "at://did:plc:mcu01/world.ptah.character/tony-stark"
  ],
  "locationReference": "at://did:plc:mcu01/world.ptah.location/avengers-tower",
  "humanAuthored": true,
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:08:00Z"
}
```

**AT URI:** `at://did:plc:mcu01/world.ptah.log/avengers-chronicle`

`humanAuthored: true` — this chronicle was written by a person, not generated. The `sourceReferences` trace every claim back to specific action and event records.

---

### Record 10 — Origin: Stan Lee → Iron Man

The attribution record. Iron Man didn't appear out of nowhere — he was created in 1963 by four people. The protocol tracks all of them.

```json
{
  "$type": "world.ptah.origin",
  "contributorDID": "did:plc:stanlee01",
  "worldReference": "at://did:plc:mcu01/world.ptah.world/mcu",
  "targetReference": "at://did:plc:mcu01/world.ptah.template/iron-man",
  "contributionType": "originator",
  "description": "Iron Man was created for Tales of Suspense #39 (March 1963). Stan Lee conceived the character, Larry Lieber wrote the script, Don Heck designed the initial artwork, and Jack Kirby designed the original gray armor. The attribution chain preserves all four contributions.",
  "originatorApproval": "approved",
  "publicDomainCompliance": "notApplicable",
  "attributionChain": [
    {
      "contributorDID": "did:plc:stanlee01",
      "role": "creator",
      "timestamp": "1963-03-01T00:00:00Z",
      "splitPercentage": 4000
    },
    {
      "contributorDID": "did:plc:larrylieber01",
      "role": "scripter",
      "timestamp": "1963-03-01T00:00:00Z",
      "splitPercentage": 2000
    },
    {
      "contributorDID": "did:plc:donheck01",
      "role": "artist",
      "timestamp": "1963-03-01T00:00:00Z",
      "splitPercentage": 2000
    },
    {
      "contributorDID": "did:plc:jackkirby01",
      "role": "designer",
      "timestamp": "1963-03-01T00:00:00Z",
      "splitPercentage": 2000
    }
  ],
  "createdAt": "2026-04-01T00:09:00Z"
}
```

**AT URI:** `at://did:plc:stanlee01/world.ptah.origin/iron-man-creation`

Four creators, each with a role and a split percentage (in basis points — 4000 = 40%). The protocol doesn't just say "Stan Lee created Iron Man." It says who did what.

---

### Record 11 — Collection: MCU Phase One

The six films that launched the franchise, bundled as a collection.

```json
{
  "$type": "world.ptah.collection",
  "name": "MCU Phase One",
  "creatorDID": "did:plc:mcu01",
  "worldReference": "at://did:plc:mcu01/world.ptah.world/mcu",
  "description": "The six films of Phase One: Iron Man through The Avengers. The origin story of the shared universe itself — six solo introductions converging into one team.",
  "items": [
    "at://did:plc:mcu01/world.ptah.action/i-am-iron-man",
    "at://did:plc:mcu01/world.ptah.event/battle-of-new-york",
    "at://did:plc:mcu01/world.ptah.log/avengers-chronicle"
  ],
  "ordering": "chronological",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2026-04-01T00:10:00Z"
}
```

**AT URI:** `at://did:plc:mcu01/world.ptah.collection/phase-one`

`ordering: chronological` — the films have a release order that matters.

---

### Record 12 — Trace: Comics to Film

The lineage record. Iron Man didn't start in the MCU — he started in a comic book in 1963. The Trace tracks the adaptation.

```json
{
  "$type": "world.ptah.trace",
  "creatorDID": "did:plc:mcu01",
  "worldReference": "at://did:plc:mcu01/world.ptah.world/mcu",
  "sourceWork": "at://did:plc:stanlee01/world.ptah.origin/iron-man-creation",
  "derivedWork": "at://did:plc:mcu01/world.ptah.template/iron-man",
  "relationship": "adaptation",
  "description": "The MCU Iron Man is adapted from the Marvel Comics character who first appeared in Tales of Suspense #39 (March 1963). The film version retains the core identity — genius inventor builds powered armor — while updating the origin from Vietnam-era to Afghanistan. The adaptation is substantial but the lineage is direct.",
  "clearanceStatus": "cleared",
  "createdAt": "2026-04-01T00:11:00Z"
}
```

**AT URI:** `at://did:plc:mcu01/world.ptah.trace/comics-to-film`

`relationship: adaptation` — not a remake, not a sequel, not a fork. An adaptation: same character, different medium, updated context. `clearanceStatus: cleared` because Marvel owns both the source and the derived work.

---

### Record 13 — Usage: MCU Franchise Terms

```json
{
  "$type": "world.ptah.usage",
  "creatorDID": "did:plc:mcu01",
  "worldReference": "at://did:plc:mcu01/world.ptah.world/mcu",
  "workReference": "at://did:plc:mcu01/world.ptah.world/mcu",
  "allowCommercial": true,
  "allowDerivatives": false,
  "allowPerformance": false,
  "requireAttribution": true,
  "territories": ["worldwide"],
  "terms": "All Marvel Cinematic Universe characters, names, likenesses, and related indicia are trademarks of and copyrighted by Marvel Entertainment, LLC and The Walt Disney Company. No derivative works, fan films, or public performances without explicit written license.",
  "licenseType": "allRightsReserved",
  "createdAt": "2026-04-01T00:12:00Z"
}
```

**AT URI:** `at://did:plc:mcu01/world.ptah.usage/mcu-franchise-terms`

`allowDerivatives: false` and `allowPerformance: false` — nobody else gets to without a license. This is the opposite of an open public domain world — corporate IP locked down at every level.

---

### Record 14 — Version: Phase One Release

```json
{
  "$type": "world.ptah.version",
  "creatorDID": "did:plc:mcu01",
  "worldReference": "at://did:plc:mcu01/world.ptah.world/mcu",
  "workReference": "at://did:plc:mcu01/world.ptah.collection/phase-one",
  "versionLabel": "published",
  "changeDescription": "Phase One complete. Six films released: Iron Man (2008), The Incredible Hulk (2008), Iron Man 2 (2010), Thor (2011), Captain America: The First Avenger (2011), The Avengers (2012). Shared continuity established.",
  "isCurrent": false,
  "status": "active",
  "createdAt": "2026-04-01T00:13:00Z"
}
```

**AT URI:** `at://did:plc:mcu01/world.ptah.version/phase-one-release`

`isCurrent: false` because Phase One has been superseded by later phases. `status: active` because the content is still canonical — it hasn't been retracted or archived.

---

## What This World Demonstrates

**Template/Instance split at franchise scale.** Iron Man is a Template. Tony Stark is a Character instance of that Template. Pepper Potts is her own character — no template needed. `instancePolicy: restricted` shows how corporate IP differs from public domain: Marvel controls who gets to be Iron Man.

**Corporate attribution chains.** The Origin record traces Iron Man back to four creators with explicit roles and split percentages. The protocol preserves the full chain — creator, scripter, artist, designer — because attribution at this scale is never simple.

**Adaptation lineage from comics to film.** The Trace record draws a direct line from Tales of Suspense #39 to the MCU Iron Man Template. The relationship type (`adaptation`) and clearance status (`cleared`) make the lineage explicit and verifiable.

**Phase-based versioning.** The Version record tracks Phase One as a published version of the franchise. The Collection bundles the phase's key records. Together, they model how a franchise evolves in discrete, labeled stages.

---
