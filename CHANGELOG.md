# Changelog

All notable changes to the Ptah Protocol are documented here.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

---

## [Unreleased]

### Added

- `world.ptah.cadence` — temporal orchestration primitive (15th record type). Controls when and how works surface: release schedules, gated access, sequential unlocks, ritualized drops. Supports RRULE scheduling, audience tiering, unlock conditions, and multi-surface channel hints.
- Four complete example world chains: RENAISSANCE (hip-hop collective), MCU (franchise universe), Blacksky Spades (competitive tournament), The Shattered Reach (tabletop RPG campaign).
- `GLOSSARY.md` — terms from protocol infrastructure, world-building, and competitive play.
- `ROADMAP.md` — current development status and planned next steps.
- `SPECIFICATION.md` — field-level reference for all fifteen record types.
- `GETTING_STARTED.md` — five-minute quickstart guide: declare participation, create a world, create a character, create an action.
- Domain, DNS TXT record for lexicon resolution, Blacksky account, and website at [ptah.world](https://ptah.world).

### Changed

- All schemas promoted from `world.ptah.temp.*` to production `world.ptah.*` namespace.
- Production schemas published to the ATProto network as `com.atproto.lexicon.schema` records under `did:plc:l45z35sxxjuobp5q65a5vu22`.
- Examples updated from Hamlet/Gatsby to RENAISSANCE and MCU for production v2.
- Examples split from a single file into individual world files in `examples/`.

### Fixed

- Required fields documentation clarified across record types.
- Author profile and account links updated to Blacksky community.

---

## [0.1.0] — Initial Release

### Added

- Fourteen initial record types defined as ATProto Lexicon JSON: `world`, `character`, `template`, `action`, `event`, `log`, `origin`, `location`, `collection`, `trace`, `usage`, `version`, `flax`, and shared `defs`.
- Schemas published to the ATProto network under initial `world.ptah.temp.*` namespace.
- README with full record type documentation and design principles.
