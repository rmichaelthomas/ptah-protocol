# Example World Record Chains

Four example worlds demonstrating how the Ptah Protocol's fourteen record types connect, reference each other via AT URIs, and express different kinds of creative worlds. RENAISSANCE and the MCU showcase the full protocol including all new production types. Spades and The Shattered Reach demonstrate competitive tournament play and collaborative tabletop RPG campaigns.

For field-level details, see the [Specification](SPECIFICATION.md). For a hands-on walkthrough, see [Getting Started](GETTING_STARTED.md).

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

## What All Four Worlds Demonstrate Together

| World | Type | Tests |
|---|---|---|
| **RENAISSANCE** | Music, original IP | Complex attribution chains, sampling lineage, all 14 record types, commercial licensing |
| **MCU** | Franchise, original IP | Template/Instance split at scale, corporate attribution, adaptation lineage, phase-based versioning |
| **Blacksky Spades** | Structured competition | Competition events, scoring, competitive witnesses, season records |
| **The Shattered Reach** | Collaborative RPG campaign | GM/player dynamics, character progression, sessions as events, campaign journals as log entries |

The same fourteen record types express all four worlds without modification. Music production. Franchise IP. Competitive card games. Tabletop RPG campaigns. The protocol doesn't care what kind of world you're building. It cares that authorship travels, history is verifiable, and every contribution traces back to the person who made it.

The schema holds all four worlds. It will hold yours.
