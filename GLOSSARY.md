# Glossary

Terms used across the Ptah Protocol documentation, covering protocol infrastructure, ATProto concepts, and the creative domains the protocol supports.

---

## Protocol & ATProto Terms

**AppView** — A service that indexes and serves ATProto records for a specific application or use case. The Ptah Protocol will need its own AppView to index `world.ptah.*` records from the network and make them queryable. Think of it as the search engine and database layer that sits between the raw records and whatever client displays them.

**AT URI** — The address of a specific record on the ATProto network. Format: `at://{DID}/{NSID}/{rkey}`. Every cross-reference in the protocol — a character pointing to its world, log pointing to its source events — uses an AT URI. It's how the record graph stays connected and traversable.

**audienceTier** — Who gets access under a Cadence record's temporal rules. Four known values: `public` (everyone), `supporters` (paid/supporting audience), `early` (early access window before public release), and `private` (specific audience only). Determines who sees what, when.

**Attribution Chain** — An array of structured `attributionEntry` objects on the Origin record. Each entry records a contributor's DID, role, timestamp, and optional split percentage. If person A created a world, person B added a character, and person C built on that character, the chain records all three. Provenance travels with the work.

**Cadence** — A record that controls when and how works surface inside a world. The temporal orchestration primitive — release schedules, gated access, sequential unlocks, ritualized drops. Each cadence targets one or more works and defines the rules for when they become available.

**cadenceType** — The temporal orchestration mode on a Cadence record. Four known values: `scheduled` (fixed dates/times), `sequential` (ordered progression where the next unlocks after the previous), `gated` (conditional access based on criteria), and `ritualized` (irregular, unpredictable drops designed to break habituation).

**Canonical Status** — Where a record stands in its world's accepted history. Three tiers: Official (originator-designated), Community (community-accepted but not originator-designated), and Apocryphal (exists but outside accepted canon). Clients can filter or display differently based on tier.

**channelHints** — An array on the Cadence record indicating preferred delivery surfaces for content releases. Known values include `calendar`, `wallet`, `notification`, and `feed`. Presence in the array signals preference. The field is extensible — new surfaces can be added without schema changes.

**Collection** — A record that bundles multiple works together. An album, anthology, season, or any curated set of related works. Items can be ordered sequentially, chronologically, or left unordered.

**DID (Decentralized Identifier)** — A permanent, portable identity on ATProto. It doesn't change even if the user changes their handle or moves to a different server. Every record that tracks authorship uses a DID. Think of it as a permanent ID number for the open web.

**Flax** — A signaling record indicating an account participates in the Ptah Protocol. Named for the twisted flax glyph (𓉔), the H in Ptah — the attribution chain thread. One per account, fixed key. AppViews use it to discover participants.

**Governance Mode** — How a world handles contributions and canon. Three modes: Sandbox (anything goes), Governed (originator sets rules), Constitutional (community governance with published rules). Declared on the World record before anyone contributes.

**knownValues** — ATProto's open-ended value sets. Unlike enums (closed lists), knownValues can be extended without breaking the schema. Every categorical field in the protocol uses knownValues so new types can be added over time.

**Lexicon** — ATProto's schema language. It defines the shape of records — what fields exist, what types they are, which are required. The Ptah Protocol's fifteen record types are expressed as Lexicon schemas. Think of a Lexicon as a blank form. Each record is a filled-out version of that form.

**NSID (Namespaced Identifier)** — The unique address of a Lexicon schema across the entire ATProto network. Read right to left: `world.ptah.character` means the Character record type, from the Ptah protocol, at the domain ptah.world.

**PDS (Personal Data Server)** — Where your ATProto data lives. Your records, your identity, your repository. Blacksky runs a PDS. Bluesky runs a PDS. You can run your own. The protocol doesn't care which PDS hosts the data — records are portable.

**Record** — A single piece of structured data in an ATProto repository. A Bluesky post is a record. A Ptah World is a record. A Ptah Character is a record. Records are signed, timestamped, and attributed to the DID that created them.

**Trace** — A record tracking lineage between works. The paper trail from one work to another — cover, remix, adaptation, translation, sample, interpolation, response, sequel, spinoff, excerpt, remake, or fork. Includes clearance status for rights management.

**unlockCondition** — A human-readable description on a Cadence record of what triggers the next release or access change. Used with `gated` and `sequential` cadence types to describe conditions like "complete chapter 3 to unlock chapter 4" or "reach 1,000 supporters to release the bonus track."

**Usage** — A record governing terms and permissions for a work. Covers what's allowed (commercial use, derivatives, performance), where (territories), for how long (expiration), and under what license type (all rights reserved, Creative Commons, public domain, custom).

**Version** — A record tracking edit history within a work. Each version links to its predecessor and carries a label (draft, published, revised, corrected, final) and status (active, superseded, retracted, archived). The protocol's mechanism for tracking how works evolve.

---

## World-Building Terms

**Canon** — The accepted history and facts of a world. What "really happened" within the world's narrative. The protocol doesn't enforce canon — it tracks it. Multiple versions can coexist, each attributed and traceable.

**Character** — A person, creature, or entity inside a world. Not the user — the world's inhabitant. A user controls a character through their DID, but the character is a separate object with its own record.

**Character Instance** — A specific performance or embodiment of a shared Template. If Iron Man is the Template, then Tony Stark is a Character Instance of that Template. Multiple instances of the same Template can coexist, each attributed to a different creator.

**Origin** — A record tracking who contributed what, under what terms, and with what role. Carries a structured attribution chain where each entry records the contributor's DID, role, and optional split percentage. The protocol's mechanism for collaborative world-building with provenance.

**Control Type** — How a character is governed. Exclusive (one DID controls it), Open (anyone can act as it), or Contested (multiple claimants). Solves the problem of shared characters in public domain or collaborative worlds.

**Log** — A world's accumulated history. What separates the protocol from a game or a social feed. Log records trace back through source references to the actions and events that generated them. Supports typed entries (history, chronicle, essay, chapter, article, entry) and a human-authored declaration flag.

**Ritualized** — A cadence mode (`cadenceType: ritualized`) for irregular, unpredictable content drops designed to break habituation. Unlike scheduled or sequential cadences, ritualized drops have no fixed pattern — the irregularity is the point. Useful for surprise releases, limited-time events, or content strategies that reward attention over routine.

**Rendering Hints** — Metadata on a World record that tells visual rendering layers what kind of world it is — tone, era, genre, aesthetic. The world has to feel like something before anything has happened in it yet.

**Template** — A shared identity template that multiple characters can embody. The type, not the instance. Iron Man is a Template — Tony Stark is a Character Instance. Templates govern how many instances can exist (open, restricted, closed) and who can create them.

**Source Type** — The intellectual property origin of a world or character. Three types: Original IP (created by the originator), Public Domain (derived from public domain source material), Collaborative Commons (created under a shared framework).

**World** — The foundational record. Everything else references it. A world must exist before characters, events, or log can exist inside it. Defines the world's name, creator, IP origin, governance mode, and rendering hints.

---

## Competitive & Gaming Terms

**Bid** — In Spades, a declaration of how many tricks (books) a player or team expects to win in a round. Bids are commitments — going under (set) or over (sandbags) has consequences.

**Book** — A single trick in Spades. Four cards played, one from each player. The highest card (or highest spade if spades were played) takes the book.

**Boston** — In Spades, winning all 13 books in a single round. Rare and devastating.

**Bracket** — A tournament structure where losers are eliminated and winners advance. Single elimination means one loss and you're out.

**Format** — The competitive structure of an event. The protocol supports known formats including bracket, round robin, open challenge, and single elimination. The field is extensible — any format can be added.

**GM (Game Master)** — The person who runs a tabletop RPG. They control the world, the non-player characters, the story, and the rules. In Dungeons & Dragons specifically called a Dungeon Master (DM). In other systems: Storyteller, Keeper, Referee. The GM's DID creates the World record and NPC Character records. Player DIDs create their own Character records.

**Nil** — In Spades, a bid of zero — the player commits to winning no books at all. High risk, high reward. A successful nil scores bonus points. A failed nil costs them.

**NPC (Non-Player Character)** — A character controlled by the GM, not by a player. In the protocol, an NPC's `creatorDID` is the GM's DID and its `controlType` is exclusive to the GM.

**Round Robin** — A tournament format where every participant plays every other participant. No elimination — standings are determined by overall record.

**Sandbag** — In Spades, winning more books than you bid. Accumulating too many sandbags results in a point penalty.

**Session** — A single sitting of a tabletop RPG campaign, typically lasting 2–4 hours. In the protocol, each session is an Event record with participants, stakes, status, and a result summarizing what happened.

**Set** — In Spades, failing to make your bid — winning fewer books than you committed to. Results in a point penalty.

**SRD (System Reference Document)** — The openly licensed core rules of a tabletop RPG system. The D&D 5th Edition SRD was released under Creative Commons (CC BY 4.0) in 2023, making the base game mechanics free to use.

**Tabletop RPG** — A collaborative storytelling game played with dice, character sheets, and a Game Master. Players control individual characters. The GM controls the world. Outcomes are determined by dice rolls, character abilities, and group decisions. Dungeons & Dragons is the most well-known tabletop RPG, but hundreds of systems exist.

**Witness** — In the protocol, a witness is someone who creates an action record attesting to their presence at an event. Witnesses are verifiable — each one is a real record created by a real DID at a real timestamp. A thousand witnesses don't make an event good. They make it witnessed.
