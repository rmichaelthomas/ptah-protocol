# Glossary

Terms used across the Ptah Protocol documentation, covering protocol infrastructure, ATProto concepts, and the creative domains the protocol supports.

---

## Protocol & ATProto Terms

**AppView** — A service that indexes and serves ATProto records for a specific application or use case. The Ptah Protocol will need its own AppView to index `world.ptah.*` records from the network and make them queryable. Think of it as the search engine and database layer that sits between the raw records and whatever client displays them.

**AT URI** — The address of a specific record on the ATProto network. Format: `at://{DID}/{NSID}/{rkey}`. Every cross-reference in the protocol — a character pointing to its world, lore pointing to its source events — uses an AT URI. It's how the record graph stays connected and traversable.

**Attribution Chain** — An array on the Contribution record that traces every hand a contribution passed through. If person A created a world, person B added a character, and person C built on that character, the chain records all three. Provenance travels with the work.

**Canonical Status** — Where a record stands in its world's accepted history. Three tiers: Official (originator-designated), Community (community-accepted but not originator-designated), and Apocryphal (exists but outside accepted canon). Clients can filter or display differently based on tier.

**DID (Decentralized Identifier)** — A permanent, portable identity on ATProto. It doesn't change even if the user changes their handle or moves to a different server. Every record that tracks authorship uses a DID. Think of it as a permanent ID number for the open web.

**Declaration** — A lightweight signaling record that tells the network an account participates in the Ptah Protocol. One per account, fixed key. AppViews use it to discover participants.

**Governance Mode** — How a world handles contributions and canon. Three modes: Sandbox (anything goes), Governed (originator sets rules), Constitutional (community governance with published rules). Declared on the World record before anyone contributes.

**knownValues** — ATProto's open-ended value sets. Unlike enums (closed lists), knownValues can be extended without breaking the schema. Every categorical field in the protocol uses knownValues so new types can be added over time.

**Lexicon** — ATProto's schema language. It defines the shape of records — what fields exist, what types they are, which are required. The Ptah Protocol's eight record types are expressed as Lexicon schemas. Think of a Lexicon as a blank form. Each record is a filled-out version of that form.

**NSID (Namespaced Identifier)** — The unique address of a Lexicon schema across the entire ATProto network. Read right to left: `world.ptah.character` means the Character record type, from the Ptah protocol, at the domain ptah.world.

**PDS (Personal Data Server)** — Where your ATProto data lives. Your records, your identity, your repository. Blacksky runs a PDS. Bluesky runs a PDS. You can run your own. The protocol doesn't care which PDS hosts the data — records are portable.

**Record** — A single piece of structured data in an ATProto repository. A Bluesky post is a record. A Ptah World is a record. A Ptah Character is a record. Records are signed, timestamped, and attributed to the DID that created them.

---

## World-Building Terms

**Canon** — The accepted history and facts of a world. What "really happened" within the world's narrative. The protocol doesn't enforce canon — it tracks it. Multiple versions can coexist, each attributed and traceable.

**Character** — A person, creature, or entity inside a world. Not the user — the world's inhabitant. A user controls a character through their DID, but the character is a separate object with its own record.

**Character Instance** — A specific performance or interpretation of a shared Role. If Hamlet is the Role, then "Hamlet as played by contributor X" is a Character Instance. Multiple instances of the same Role can coexist, each attributed to a different creator.

**Contribution** — A record governing how someone who didn't create a world adds to it. Carries the attribution chain, approval status, and canonical standing. The protocol's mechanism for collaborative world-building with provenance.

**Control Type** — How a character is governed. Exclusive (one DID controls it), Open (anyone can act as it), or Delegated (specific DIDs are granted permission). Solves the problem of shared characters in public domain or collaborative worlds.

**Lore** — A world's accumulated history. What separates the protocol from a game or a social feed. Lore records trace back through source references to the actions and events that generated them. The history is attributable, permanent, and verifiable.

**Rendering Hints** — Metadata on a World record that tells visual rendering layers what kind of world it is — tone, era, genre, aesthetic. The world has to feel like something before anything has happened in it yet.

**Role** — A shared identity template that sits between the World and the Character. Hamlet is a Role. Each performance of Hamlet is a Character Instance. Roles govern how many instances can exist and who can create them.

**Source Type** — The intellectual property origin of a world or character. Three types: Original IP (created by the originator), Public Domain (derived from public domain source material), Collaborative Commons (created under a shared framework).

**World** — The foundational record. Everything else references it. A world must exist before characters, events, or lore can exist inside it. Defines the world's name, creator, IP origin, governance mode, and rendering hints.

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
