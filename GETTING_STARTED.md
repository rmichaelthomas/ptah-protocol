# Getting Started with the Ptah Protocol

This guide walks you through creating your first chain of records on the Ptah Protocol. By the end, you'll have a World, a Character, an Action, and an understanding of how records connect.

No AppView exists yet — these records live in ATProto repositories and are resolvable on the network, but there is no dedicated rendering client. You're building on infrastructure that's being constructed. That's the point.

---

## Prerequisites

You need an ATProto account. Any PDS works — [Blacksky](https://blacksky.community), [bsky.app](https://bsky.app), or your own. You'll need your DID and an app password.

Find your DID:
```
https://bsky.social/xrpc/com.atproto.identity.resolveHandle?handle=YOUR_HANDLE
```

Create an app password in your account settings under **App Passwords**.

---

## Step 1: Declare Participation

Before creating world records, signal that your account participates in the Ptah Protocol. This is how AppViews discover participants.

```json
{
  "$type": "world.ptah.declaration",
  "displayName": "Your Builder Name",
  "description": "World-builder. Here to create.",
  "createdAt": "2026-03-22T00:00:00Z"
}
```

This record uses the fixed key `self` — one per account.

To write it to your repository:

```bash
curl -X POST "https://YOUR_PDS/xrpc/com.atproto.repo.putRecord" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "repo": "YOUR_DID",
    "collection": "world.ptah.declaration",
    "rkey": "self",
    "record": {
      "$type": "world.ptah.declaration",
      "displayName": "Your Builder Name",
      "description": "World-builder. Here to create.",
      "createdAt": "2026-03-22T00:00:00Z"
    }
  }'
```

Replace `YOUR_PDS`, `YOUR_DID`, and `YOUR_ACCESS_TOKEN` with your actual values. To get an access token, authenticate via `com.atproto.server.createSession`.

---

## Step 2: Create a World

Everything starts here. A World must exist before anything else can exist inside it.

```json
{
  "$type": "world.ptah.world",
  "name": "The World of Gatsby",
  "creatorDID": "did:plc:your-did-here",
  "description": "Long Island, 1922. New money and old money separated by a bay. A man built an empire to win back a woman. The empire was a performance. The woman was a memory.",
  "sourceType": "publicDomain",
  "sourceReference": "F. Scott Fitzgerald, The Great Gatsby, 1925. Public domain (U.S.) as of January 1, 2021.",
  "governanceMode": "governed",
  "renderingHints": {
    "tone": "elegiac, seductive, doomed",
    "era": "Jazz Age, 1920s America",
    "genre": "literary fiction, social tragedy",
    "aesthetic": "gold light, green water, white linen, broken glass"
  },
  "createdAt": "2026-03-22T00:01:00Z"
}
```

Write it:

```bash
curl -X POST "https://YOUR_PDS/xrpc/com.atproto.repo.createRecord" \
  -H "Authorization: Bearer YOUR_ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "repo": "YOUR_DID",
    "collection": "world.ptah.world",
    "record": {
      "$type": "world.ptah.world",
      "name": "The World of Gatsby",
      "creatorDID": "did:plc:your-did-here",
      "description": "Long Island, 1922. New money and old money separated by a bay. A man built an empire to win back a woman. The empire was a performance. The woman was a memory.",
      "sourceType": "publicDomain",
      "sourceReference": "F. Scott Fitzgerald, The Great Gatsby, 1925. Public domain (U.S.) as of January 1, 2021.",
      "governanceMode": "governed",
      "renderingHints": {
        "tone": "elegiac, seductive, doomed",
        "era": "Jazz Age, 1920s America",
        "genre": "literary fiction, social tragedy",
        "aesthetic": "gold light, green water, white linen, broken glass"
      },
      "createdAt": "2026-03-22T00:01:00Z"
    }
  }'
```

The response includes a `uri` field — that's the AT URI you'll reference from every other record. Save it. It looks like:

```
at://did:plc:your-did-here/world.ptah.world/3lr2example
```

---

## Step 3: Create a Character

A character lives inside a world. It references the World via AT URI.

```json
{
  "$type": "world.ptah.character",
  "name": "Jay Gatsby",
  "creatorDID": "did:plc:your-did-here",
  "worldReference": "at://did:plc:your-did-here/world.ptah.world/3lr2example",
  "roleReference": "at://did:plc:your-did-here/world.ptah.role/ROLE_RKEY",
  "description": "The self-made man. Born James Gatz. Invented himself out of nothing and longing. Throws parties for a woman across the bay.",
  "controlType": "exclusive",
  "originType": "world.ptah.defs#sourceTypePublicDomain",
  "authorshipRecord": "did:plc:your-did-here",
  "createdAt": "2026-03-22T00:02:00Z"
}
```

Write it the same way, using `world.ptah.character` as the collection. Replace `ROLE_RKEY` with the record key if you created a Role first (optional for this quickstart). Save the returned AT URI.

---

## Step 4: Create a Location

Give your world a place where things happen.

```json
{
  "$type": "world.ptah.location",
  "name": "The Mansion at West Egg",
  "creatorDID": "did:plc:your-did-here",
  "worldReference": "at://did:plc:your-did-here/world.ptah.world/3lr2example",
  "description": "Gatsby's house. An imitation of a French Hôtel de Ville. Forty acres of lawn. A marble swimming pool. The whole thing is a stage set for an audience of one.",
  "locationType": "building",
  "depthIndex": 2,
  "properties": {
    "climate": "Long Island summers — humid, golden, lit by lanterns",
    "controllingFaction": "Jay Gatsby, sole owner"
  },
  "createdAt": "2026-03-22T00:03:00Z"
}
```

---

## Step 5: Create an Action

Something happens. A character acts inside the world.

```json
{
  "$type": "world.ptah.action",
  "actorDID": "did:plc:your-did-here",
  "characterReference": "at://did:plc:your-did-here/world.ptah.character/CHAR_RKEY",
  "worldReference": "at://did:plc:your-did-here/world.ptah.world/3lr2example",
  "actionType": "creation",
  "content": "The lights go on across the lawn. The orchestra arrives. Gatsby stands at the window and watches the green light across the bay. The party is not for the guests. It has never been for the guests.",
  "locationReference": "at://did:plc:your-did-here/world.ptah.location/LOC_RKEY",
  "visibility": "canon",
  "createdAt": "2026-03-22T00:04:00Z"
}
```

Replace `CHAR_RKEY` and `LOC_RKEY` with the record keys from the responses in Steps 3 and 4.

---

## What You've Built

Four records. A chain that looks like this:

```
World: The World of Gatsby
  └── Location: The Mansion at West Egg
  └── Character: Jay Gatsby
        └── Action: The lights go on across the lawn.
```

Every record references the World. The Action references both the Character and the Location. The entire chain is traversable — start at any record and follow the AT URIs to reconstruct the full context.

This is the fundamental pattern. Everything else in the protocol — Roles, Events, Lore, Contributions — builds on this same structure of typed records referencing each other through AT URIs.

---

## What Comes Next

**Add an Event.** Create a `world.ptah.event` record where characters compete or convene. Reference participants and a location.

**Write Lore.** After actions and events accumulate, create a `world.ptah.lore` record that traces back to the actions and events that generated it. This is where play becomes history.

**Invite a Contributor.** When someone else wants to add to your world, they create a `world.ptah.contribution` record with an `attributionChain` that traces back to you. Provenance travels with every addition.

**Use Roles for shared characters.** In public domain worlds (or worlds with open characters), create a `world.ptah.role` as a template, then let multiple people create Character instances of that Role. This is how a world scales without losing coherence.

---

## Reading Records

Fetch any record from the network:

```bash
curl "https://public.api.bsky.app/xrpc/com.atproto.repo.getRecord?repo=YOUR_DID&collection=world.ptah.world&rkey=RECORD_KEY"
```

List all records of a type in a repository:

```bash
curl "https://public.api.bsky.app/xrpc/com.atproto.repo.listRecords?repo=YOUR_DID&collection=world.ptah.world"
```

These work for any collection — `world.ptah.character`, `world.ptah.action`, etc.

---

## Resources

- **Specification:** [SPECIFICATION.md](SPECIFICATION.md) — full field-level reference
- **Example Worlds:** [EXAMPLES.md](EXAMPLES.md) — Hamlet, Gatsby, Spades tournament, and tabletop RPG campaign
- **ATProto Lexicon Spec:** [atproto.com/specs/lexicon](https://atproto.com/specs/lexicon)
- **Lexicon Schemas:** [`lexicons/`](lexicons/) directory in this repository
- **Contact:** protocol@ptah.world
