# World 1: RENAISSANCE — Music as World-Building

## Why This World

RENAISSANCE is the attribution showcase. A modern album with over a hundred contributors — producers, writers, sampled artists, featured performers. The protocol's Origin, Trace, and Usage records exist for exactly this kind of complexity. Every sample is traceable. Every contribution is attributed. Every permission is documented.

This world demonstrates every record type in the protocol, including the six new production types: Collection, Trace, Usage, Version, Flax, and Defs (referenced throughout).

## What This Chain Contains

- 1 World record
- 1 Template record (The Featured Artist)
- 3 Character records (Beyoncé, Big Freedia, Donna Summer)
- 2 Location records (The Studio, The Stage)
- 2 Action records (BREAK MY SOUL Drops, Big Freedia's Call)
- 2 Event records (Album Release, Grammy Performance)
- 1 Log record (How House Music Shaped RENAISSANCE)
- 1 Origin record (Attribution Chain)
- 1 Collection record (RENAISSANCE the album)
- 2 Trace records (Show Me Love sample, I Feel Love sample)
- 1 Usage record (Album Licensing Terms)
- 1 Version record (Album Release Version)

Total: 18 records across all 14 record types.

---

### Record 1 — World: RENAISSANCE

```json
{
  "$type": "world.ptah.world",
  "name": "RENAISSANCE",
  "creatorDID": "did:plc:renaissance01",
  "description": "The album as a world. RENAISSANCE is a house music cathedral built by Beyoncé and over a hundred collaborators — producers, writers, sampled artists, featured vocalists. It traces a lineage from Chicago house to Detroit techno to New York ballroom to Houston bounce. Every track is an act of attribution. Every sample is a citation. The dancefloor is the canon.",
  "sourceType": "originalIP",
  "governanceMode": "governed",
  "renderingHints": {
    "tone": "joyful, defiant, ancestral",
    "era": "2022, drawing from 1970s–1990s dance music",
    "genre": "house, dance, Afrofuturist pop",
    "aesthetic": "silver chrome, disco mirrors, sweat, strobe light, the four-on-the-floor kick"
  },
  "createdAt": "2022-07-29T00:00:00Z"
}
```

**AT URI:** `at://did:plc:renaissance01/world.ptah.world/renaissance`

`sourceType: originalIP` — this is an original commercial work. `governanceMode: governed` because one person controls the world, even with a hundred contributors. Beyoncé is the architect. Everyone else is credited, but the world is hers.

---

### Record 2 — Template: The Featured Artist

The archetype. RENAISSANCE has featured artists on multiple tracks — Big Freedia, Grace Jones, Tems. This template defines what a featured artist is within the world: a voice invited into a track, credited and compensated, but not the world's originator.

```json
{
  "$type": "world.ptah.template",
  "name": "The Featured Artist",
  "worldReference": "at://did:plc:renaissance01/world.ptah.world/renaissance",
  "creatorDID": "did:plc:renaissance01",
  "description": "A guest voice on the record. Featured artists bring their own identity into the world but operate within the album's architecture. They are invited, not self-appointed. Their contributions are credited, cleared, and compensated.",
  "originType": "originalIP",
  "canonicalReferencePolicy": "fixed",
  "instancePolicy": "restricted",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2022-07-29T00:01:00Z"
}
```

**AT URI:** `at://did:plc:renaissance01/world.ptah.template/featured-artist`

`instancePolicy: restricted` — not anyone can be a featured artist on RENAISSANCE. You get invited. This is a governed world with curated access.

---

### Record 3 — Character: Beyoncé

The world's originator. Not an instance of the Featured Artist template — she is the architect, not a guest.

```json
{
  "$type": "world.ptah.character",
  "name": "Beyoncé",
  "creatorDID": "did:plc:renaissance01",
  "worldReference": "at://did:plc:renaissance01/world.ptah.world/renaissance",
  "description": "Singer, writer, producer, world-builder. RENAISSANCE is her seventh studio album and her most collaborative — but the vision is singular. She controls the world. Every featured artist, every sample, every four-on-the-floor kick exists because she put it there.",
  "controlType": "exclusive",
  "originType": "originalIP",
  "characterProperties": {
    "role": "world originator, lead artist, executive producer",
    "affiliation": "Parkwood Entertainment"
  },
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2022-07-29T00:02:00Z"
}
```

**AT URI:** `at://did:plc:renaissance01/world.ptah.character/beyonce`

No `templateReference`. Beyoncé is not a featured artist on her own album. She is the world itself.

---

### Record 4 — Character: Big Freedia

Featured on BREAK MY SOUL. The bounce queen from New Orleans. Her vocal is the track's call to action.

```json
{
  "$type": "world.ptah.character",
  "name": "Big Freedia",
  "creatorDID": "did:plc:bigfreedia01",
  "worldReference": "at://did:plc:renaissance01/world.ptah.world/renaissance",
  "templateReference": "at://did:plc:renaissance01/world.ptah.template/featured-artist",
  "description": "New Orleans bounce artist. Featured on BREAK MY SOUL. Her vocal commands the dancefloor — part sermon, part directive. She brought the bounce tradition into the house framework and made them shake hands.",
  "controlType": "exclusive",
  "originType": "originalIP",
  "characterProperties": {
    "role": "featured artist, vocalist",
    "affiliation": "New Orleans bounce"
  },
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2022-07-29T00:03:00Z"
}
```

**AT URI:** `at://did:plc:bigfreedia01/world.ptah.character/big-freedia`

`templateReference` points to the Featured Artist template. Big Freedia is an instance of that archetype — an invited voice with full attribution.

---

### Record 5 — Character: Donna Summer (Sampled)

Not a living participant. A presence carried forward through a sample. Her voice on "I Feel Love" appears in SUMMER RENAISSANCE — the album's closing track and direct tribute.

```json
{
  "$type": "world.ptah.character",
  "name": "Donna Summer (Sampled)",
  "creatorDID": "did:plc:renaissance01",
  "worldReference": "at://did:plc:renaissance01/world.ptah.world/renaissance",
  "description": "The Queen of Disco. Her 1977 track 'I Feel Love,' produced by Giorgio Moroder, is sampled on SUMMER RENAISSANCE. She is not a living collaborator but a credited ancestor — her voice is the foundation the closing track is built on. The sample is the citation. The protocol makes it permanent.",
  "controlType": "open",
  "originType": "originalIP",
  "characterProperties": {
    "role": "sampled artist",
    "affiliation": "Disco, electronic dance music origins"
  },
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2022-07-29T00:04:00Z"
}
```

**AT URI:** `at://did:plc:renaissance01/world.ptah.character/donna-summer`

`controlType: open` — Donna Summer died in 2012. Her legacy is performed by the sample, not controlled by a living person. The protocol still credits her.

---

### Record 6 — Location: The Studio

```json
{
  "$type": "world.ptah.location",
  "name": "The Studio",
  "creatorDID": "did:plc:renaissance01",
  "worldReference": "at://did:plc:renaissance01/world.ptah.world/renaissance",
  "description": "Where RENAISSANCE was built. Sessions in Los Angeles, New York, London — wherever the collaborators gathered. The studio is singular in the world even though the physical rooms were many. One creative space, distributed across cities.",
  "locationType": "building",
  "depthIndex": 1,
  "locationProperties": {
    "climate": "controlled, isolated, nocturnal",
    "notableHistory": "Three years of sessions across multiple cities, 2019–2022"
  },
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2022-07-29T00:05:00Z"
}
```

**AT URI:** `at://did:plc:renaissance01/world.ptah.location/the-studio`

---

### Record 7 — Location: The Stage

```json
{
  "$type": "world.ptah.location",
  "name": "The Stage",
  "creatorDID": "did:plc:renaissance01",
  "worldReference": "at://did:plc:renaissance01/world.ptah.world/renaissance",
  "description": "The live performance space. The Renaissance World Tour, the Grammy stage, every venue where the album became a physical experience. The studio made the record. The stage made it a world.",
  "locationType": "building",
  "depthIndex": 1,
  "locationProperties": {
    "climate": "heat, volume, crowd energy",
    "notableHistory": "Renaissance World Tour, 2023. 56 shows. Grammy performance, February 2023."
  },
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2022-07-29T00:06:00Z"
}
```

**AT URI:** `at://did:plc:renaissance01/world.ptah.location/the-stage`

No `parentLocation` — The Studio and The Stage are parallel spaces, not nested. The album is made in one and realized in the other.

---

### Record 8 — Action: BREAK MY SOUL Drops

```json
{
  "$type": "world.ptah.action",
  "actorDID": "did:plc:renaissance01",
  "characterReference": "at://did:plc:renaissance01/world.ptah.character/beyonce",
  "worldReference": "at://did:plc:renaissance01/world.ptah.world/renaissance",
  "actionType": "narrative",
  "content": "The lead single arrives. June 20, 2022 — five weeks before the album. A four-on-the-floor house beat, a Robin S. vocal sample, a Big Freedia bounce call. The thesis statement: the dancefloor as liberation. The world announces itself.",
  "locationReference": "at://did:plc:renaissance01/world.ptah.location/the-studio",
  "visibility": "canon",
  "createdAt": "2022-06-20T00:00:00Z"
}
```

**AT URI:** `at://did:plc:renaissance01/world.ptah.action/break-my-soul-drops`

---

### Record 9 — Action: Big Freedia's Call

```json
{
  "$type": "world.ptah.action",
  "actorDID": "did:plc:bigfreedia01",
  "characterReference": "at://did:plc:bigfreedia01/world.ptah.character/big-freedia",
  "worldReference": "at://did:plc:renaissance01/world.ptah.world/renaissance",
  "actionType": "dialogue",
  "content": "Big Freedia's vocal on BREAK MY SOUL — the bounce call that drives the track. A New Orleans tradition dropped into a Chicago house framework. The collaboration is the point: two Black music lineages meeting on the same four-count.",
  "locationReference": "at://did:plc:renaissance01/world.ptah.location/the-studio",
  "visibility": "canon",
  "createdAt": "2022-06-20T00:01:00Z"
}
```

**AT URI:** `at://did:plc:bigfreedia01/world.ptah.action/freedia-call`

`actorDID` is Big Freedia's DID — the action belongs to the person who performed it, not the world creator. This is how the protocol distinguishes the architect from the collaborator.

---

### Record 10 — Event: Album Release

```json
{
  "$type": "world.ptah.event",
  "name": "RENAISSANCE Album Release",
  "creatorDID": "did:plc:renaissance01",
  "worldReference": "at://did:plc:renaissance01/world.ptah.world/renaissance",
  "description": "The album drops. July 29, 2022. Sixteen tracks. Act I of a planned trilogy. The world goes live.",
  "eventType": "milestone",
  "status": "completed",
  "startTime": "2022-07-29T00:00:00Z",
  "endTime": "2022-07-29T23:59:00Z",
  "stakes": "The return. Beyoncé's first solo album in six years. A bet on house music in the streaming era.",
  "result": "Debuted at number one. Grammy for Best Dance/Electronic Album. The house revival it triggered is still ongoing.",
  "participants": [
    "at://did:plc:renaissance01/world.ptah.character/beyonce"
  ],
  "locationReference": "at://did:plc:renaissance01/world.ptah.location/the-studio",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2022-07-29T00:07:00Z"
}
```

**AT URI:** `at://did:plc:renaissance01/world.ptah.event/album-release`

---

### Record 11 — Event: Grammy Performance

```json
{
  "$type": "world.ptah.event",
  "name": "Grammy Performance — RENAISSANCE",
  "creatorDID": "did:plc:renaissance01",
  "worldReference": "at://did:plc:renaissance01/world.ptah.world/renaissance",
  "description": "The 65th Grammy Awards. Beyoncé opens the show. The stage becomes the world — chrome, light, movement. The studio record becomes a live experience. She wins four awards that night, becoming the most awarded artist in Grammy history.",
  "eventType": "ceremony",
  "status": "completed",
  "startTime": "2023-02-05T20:00:00Z",
  "endTime": "2023-02-05T23:30:00Z",
  "stakes": "Legacy. The record book. Whether RENAISSANCE translates from headphones to the room.",
  "result": "Four wins including Best Dance/Electronic Album. Most awarded artist in Grammy history with 32 total.",
  "participants": [
    "at://did:plc:renaissance01/world.ptah.character/beyonce"
  ],
  "locationReference": "at://did:plc:renaissance01/world.ptah.location/the-stage",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2023-02-05T20:00:00Z"
}
```

**AT URI:** `at://did:plc:renaissance01/world.ptah.event/grammy-performance`

---

### Record 12 — Log: How House Music Shaped RENAISSANCE

```json
{
  "$type": "world.ptah.log",
  "title": "How House Music Shaped RENAISSANCE",
  "creatorDID": "did:plc:renaissance01",
  "worldReference": "at://did:plc:renaissance01/world.ptah.world/renaissance",
  "logType": "essay",
  "summary": "The album's debt to house music, Black queer dance culture, and the Chicago/Detroit/New York lineage that made it possible.",
  "content": "RENAISSANCE did not come from nowhere. It came from the Warehouse in Chicago where Frankie Knuckles played. From the Paradise Garage in New York where Larry Levan mixed. From Detroit where Juan Atkins and Derrick May built techno from Kraftwerk and funk. From the ballroom scene where vogueing and house music fused into a culture of survival and style. The album samples Robin S., Donna Summer, Giorgio Moroder. It features Big Freedia from the New Orleans bounce tradition. Every track is a citation — a line drawn from the present back to the source. The protocol makes those lines permanent. The Origin record names every contributor. The Trace records map every sample. The dancefloor has a bibliography now.",
  "sourceReferences": [
    "at://did:plc:renaissance01/world.ptah.action/break-my-soul-drops",
    "at://did:plc:bigfreedia01/world.ptah.action/freedia-call",
    "at://did:plc:renaissance01/world.ptah.event/album-release",
    "at://did:plc:renaissance01/world.ptah.event/grammy-performance"
  ],
  "characters": [
    "at://did:plc:renaissance01/world.ptah.character/beyonce",
    "at://did:plc:bigfreedia01/world.ptah.character/big-freedia",
    "at://did:plc:renaissance01/world.ptah.character/donna-summer"
  ],
  "humanAuthored": true,
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2022-08-01T00:00:00Z"
}
```

**AT URI:** `at://did:plc:renaissance01/world.ptah.log/house-music-shaped-renaissance`

The `sourceReferences` array traces this essay back to the actions and events that generated it. The `characters` array names every person discussed. The history is verifiable — follow the AT URIs to the source.

---

### Record 13 — Origin: Attribution Chain

This is the record that justifies the Origin type's existence. RENAISSANCE has over a hundred contributors. This Origin record shows a representative slice — the attribution chain for BREAK MY SOUL, with featured artists, sampled artists, roles, and split percentages.

```json
{
  "$type": "world.ptah.origin",
  "contributorDID": "did:plc:renaissance01",
  "worldReference": "at://did:plc:renaissance01/world.ptah.world/renaissance",
  "targetReference": "at://did:plc:renaissance01/world.ptah.action/break-my-soul-drops",
  "contributionType": "coauthor",
  "description": "Attribution chain for BREAK MY SOUL. Multiple contributors across performance, writing, sampling, and production. Each entry represents a credited role with a split percentage in basis points.",
  "originatorApproval": "approved",
  "publicDomainCompliance": "notApplicable",
  "attributionChain": [
    {
      "contributorDID": "did:plc:renaissance01",
      "role": "lead artist, writer, producer",
      "timestamp": "2022-06-20T00:00:00Z",
      "splitPercentage": 3000
    },
    {
      "contributorDID": "did:plc:bigfreedia01",
      "role": "featured artist, vocalist",
      "timestamp": "2022-06-20T00:00:00Z",
      "splitPercentage": 1500
    },
    {
      "contributorDID": "did:plc:robins01",
      "role": "sampled artist — Show Me Love vocal",
      "timestamp": "2022-06-20T00:00:00Z",
      "splitPercentage": 2000
    },
    {
      "contributorDID": "did:plc:donnasummer01",
      "role": "sampled artist — I Feel Love",
      "timestamp": "2022-06-20T00:00:00Z",
      "splitPercentage": 1500
    },
    {
      "contributorDID": "did:plc:tricky01",
      "role": "producer",
      "timestamp": "2022-06-20T00:00:00Z",
      "splitPercentage": 2000
    }
  ],
  "splitPercentage": 3000,
  "createdAt": "2022-07-29T00:08:00Z"
}
```

**AT URI:** `at://did:plc:renaissance01/world.ptah.origin/break-my-soul-attribution`

Five entries in the `attributionChain`. Split percentages in basis points (100 = 1%, so 3000 = 30%). The chain is representative, not exhaustive — the real BREAK MY SOUL has even more credited writers and producers. But the structure scales. Add entries to the array. The protocol holds them all.

---

### Record 14 — Collection: RENAISSANCE (The Album)

The album itself, structured as a collection of tracks. Each item references an action record representing a key track.

```json
{
  "$type": "world.ptah.collection",
  "name": "RENAISSANCE",
  "creatorDID": "did:plc:renaissance01",
  "worldReference": "at://did:plc:renaissance01/world.ptah.world/renaissance",
  "description": "The album as a sequenced collection. Sixteen tracks, each a discrete creative work, ordered as released. The collection is the world's spine — everything else references into it.",
  "items": [
    "at://did:plc:renaissance01/world.ptah.action/break-my-soul-drops",
    "at://did:plc:bigfreedia01/world.ptah.action/freedia-call"
  ],
  "ordering": "sequential",
  "canonicalStatus": "world.ptah.defs#canonicalStatusOfficial",
  "createdAt": "2022-07-29T00:09:00Z"
}
```

**AT URI:** `at://did:plc:renaissance01/world.ptah.collection/renaissance-album`

The `items` array here shows two representative tracks. A full implementation would list all sixteen. `ordering: sequential` — track order matters. This is an album, not a playlist.

---

### Record 15 — Trace: "Show Me Love" Sample

```json
{
  "$type": "world.ptah.trace",
  "creatorDID": "did:plc:renaissance01",
  "worldReference": "at://did:plc:renaissance01/world.ptah.world/renaissance",
  "sourceWork": "at://did:plc:robins01/world.ptah.action/show-me-love-original",
  "derivedWork": "at://did:plc:renaissance01/world.ptah.action/break-my-soul-drops",
  "relationship": "sample",
  "description": "BREAK MY SOUL samples the vocal hook from Robin S.'s 'Show Me Love' (1993). The sample is the emotional core of the track — a 1990s house vocal threaded into a 2022 production. Cleared and credited.",
  "clearanceStatus": "cleared",
  "createdAt": "2022-07-29T00:10:00Z"
}
```

**AT URI:** `at://did:plc:renaissance01/world.ptah.trace/show-me-love-sample`

`sourceWork` points to the original. `derivedWork` points to the new track. `relationship: sample`. `clearanceStatus: cleared`. The paper trail is complete.

---

### Record 16 — Trace: "I Feel Love" Sample

```json
{
  "$type": "world.ptah.trace",
  "creatorDID": "did:plc:renaissance01",
  "worldReference": "at://did:plc:renaissance01/world.ptah.world/renaissance",
  "sourceWork": "at://did:plc:donnasummer01/world.ptah.action/i-feel-love-original",
  "derivedWork": "at://did:plc:renaissance01/world.ptah.action/summer-renaissance",
  "relationship": "sample",
  "description": "SUMMER RENAISSANCE samples Donna Summer and Giorgio Moroder's 'I Feel Love' (1977). The closing track of the album built on the opening statement of electronic dance music. The lineage is the point.",
  "clearanceStatus": "cleared",
  "createdAt": "2022-07-29T00:11:00Z"
}
```

**AT URI:** `at://did:plc:renaissance01/world.ptah.trace/i-feel-love-sample`

Two Trace records, two samples, two lineages. Each one links a source work to a derived work with a named relationship and clearance status. This is what Trace was built for.

---

### Record 17 — Usage: Album Licensing Terms

```json
{
  "$type": "world.ptah.usage",
  "creatorDID": "did:plc:renaissance01",
  "worldReference": "at://did:plc:renaissance01/world.ptah.world/renaissance",
  "workReference": "at://did:plc:renaissance01/world.ptah.collection/renaissance-album",
  "licenseType": "allRightsReserved",
  "allowCommercial": true,
  "allowDerivatives": false,
  "allowPerformance": true,
  "requireAttribution": true,
  "territories": [],
  "terms": "All rights reserved. Commercial release via Columbia Records and Parkwood Entertainment. Performance rights administered through ASCAP/BMI. Sampling requires clearance — see individual Trace records for sample-level permissions. Attribution is non-negotiable.",
  "createdAt": "2022-07-29T00:12:00Z"
}
```

**AT URI:** `at://did:plc:renaissance01/world.ptah.usage/album-licensing`

`licenseType: allRightsReserved` — this is a commercial release, not a Creative Commons project. `allowDerivatives: false` — you cannot remix the album without clearance. `requireAttribution: true` — you must credit the artists. `territories` is empty, meaning worldwide.

---

### Record 18 — Version: Album Release Version

```json
{
  "$type": "world.ptah.version",
  "creatorDID": "did:plc:renaissance01",
  "worldReference": "at://did:plc:renaissance01/world.ptah.world/renaissance",
  "workReference": "at://did:plc:renaissance01/world.ptah.collection/renaissance-album",
  "versionLabel": "published",
  "changeDescription": "Initial commercial release. Sixteen tracks. Act I of a planned trilogy.",
  "isCurrent": true,
  "status": "active",
  "createdAt": "2022-07-29T00:13:00Z"
}
```

**AT URI:** `at://did:plc:renaissance01/world.ptah.version/album-v1`

`versionLabel: published`, `status: active`, `isCurrent: true`. No `previousVersion` — this is the first and current release. When Act II drops, a new Version record supersedes this one, and `isCurrent` flips to `false`. The edit history is permanent.

---

## What This World Demonstrates

**Complex attribution.** The Origin record's `attributionChain` holds five contributors with roles and split percentages. The real album has over a hundred. The array scales — add entries, the structure holds.

**Sampling lineage.** Two Trace records map two samples from source to derived work. Every sample has a named relationship (`sample`), a clearance status (`cleared`), and a description. The paper trail is machine-readable and permanent.

**All 14 record types.** RENAISSANCE uses every record type in the protocol: World, Template, Character, Location, Action, Event, Log, Origin, Collection, Trace, Usage, Version — plus Flax and Defs referenced throughout via `canonicalStatus` values. No other example world exercises the full schema.

**The difference between originator and collaborator.** Beyoncé has no `templateReference` — she is the world, not an instance of it. Big Freedia has a `templateReference` pointing to the Featured Artist template. Donna Summer has `controlType: open` because she is a sampled presence, not a living participant. Three characters, three different relationships to the world.

**Commercial licensing.** The Usage record makes rights explicit: all rights reserved, attribution required, derivatives require clearance. This is not a public domain world. The protocol handles both.

**Version tracking.** The Version record establishes the album's release as the current active version of the collection, with a structure ready to track future revisions or new acts in the trilogy.

---
