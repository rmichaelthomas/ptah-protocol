# Contributing to the Ptah Protocol

The Ptah Protocol is open infrastructure. Contributions are welcome at every layer — schema feedback, documentation improvements, example worlds, and tooling.

---

## Ways to Contribute

**Documentation fixes** are the easiest path in. If something in the spec is unclear, wrong, or outdated — fix it. No ceremony required.

**Example worlds** live in `examples/`. Each demonstrates a different use case (music, film franchise, competitive play, tabletop RPG). If you've built a world on the protocol and want to document it here, open a PR. Follow the existing file format.

**Lexicon corrections** — typos, incorrect field types, missing `knownValues` entries. Straightforward and always welcome.

**Schema feedback and proposals** — If you've implemented against the schemas and found something missing, ambiguous, or structurally wrong, open an issue. Protocol-level changes go through discussion before implementation. See the [Roadmap](ROADMAP.md) for what's already planned.

---

## Getting Started

Clone the repository:

```bash
git clone https://github.com/rmichaelthomas/ptah-protocol.git
cd ptah-protocol
```

No build step. No dependencies. The `lexicons/` directory contains JSON schema files. The `examples/` directory contains Markdown. Edit directly.

To validate a lexicon change:

```bash
python3 -m json.tool lexicons/world.ptah.your-file.json
```

To test your changes against the live network, follow [GETTING_STARTED.md](GETTING_STARTED.md) to write records against the schemas using your ATProto account.

---

## Pull Request Process

1. Fork the repository and create a branch from `main`
2. Make your changes
3. Validate any modified JSON with `python3 -m json.tool`
4. If you're proposing a schema change, include a brief rationale in the PR description
5. Open the PR against `main`

One logical change per PR where possible. If you're touching multiple unrelated things, split them.

---

## Issues

Use the issue templates. If nothing fits, open a blank issue. Be specific — "this field name is ambiguous because X" is more actionable than "the spec is confusing."

---

## Code of Conduct

This project follows the [Contributor Covenant](CODE_OF_CONDUCT.md). Be direct, be constructive, be kind.

---

## Questions

- **GitHub:** open an issue
- **Blacksky:** [@ptah.world](https://blacksky.community/profile/ptah.world)
- **Email:** protocol@ptah.world
