# Contributing to QuizMD

Thank you for your interest in improving the QuizMD specification.

## Ways to contribute

### Report an ambiguity or bug in the spec
Open a [GitHub Issue](https://github.com/neuroneo-md/quizmd/issues) describing:
- The section of the spec that is unclear or incorrect
- Your interpretation and the alternative interpretation
- A concrete `.quiz.md` example that demonstrates the ambiguity

### Propose a new feature
Open an issue with the label `proposal` and describe:
- **Problem** — what use case is not covered by the current spec?
- **Proposed syntax** — a concrete `.quiz.md` example of the new feature
- **Impact on existing files** — is it backward-compatible?
- **Impact on implementations** — what does a parser need to do?

Proposals are discussed openly. A feature is added to the spec once:
1. There is clear consensus on the syntax
2. At least one implementation (e.g. neuroneo.md) has validated it in practice
3. Sample files and tests are provided

### Add a sample file
Add a `.quiz.md` file to `samples/` that demonstrates a feature or use case not yet covered. Open a PR with a brief description.

### Add a test case
- `tests/valid/` — files that any conforming parser **must** accept
- `tests/invalid/` — files that any conforming parser **must** reject, with a comment explaining why

Each test file should have a companion `.md` or comment explaining the expected behaviour.

### Add your implementation
Edit `README.md` to add your parser, player, or tooling to the implementations table.

## Versioning

The spec follows [Semantic Versioning](https://semver.org/):
- **Patch** (0.1.x) — clarifications, typo fixes, no behaviour change
- **Minor** (0.x.0) — new backward-compatible features
- **Major** (x.0.0) — breaking changes (rare, requires strong justification)

## Code of conduct

Be respectful and constructive. This is a technical specification — discussions should focus on the format, not personalities.
