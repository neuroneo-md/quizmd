# QuizMD

**QuizMD** is an open, Markdown-based format for writing quizzes and assessments.

A `.quiz.md` file is valid Markdown — readable by humans, versionable in Git, and playable by any compatible player. No proprietary format, no lock-in, just text.

## Quick example

```markdown
# Capital cities

## Q1 · Capital of France?

- [ ] London
- [x] Paris
- [ ] Berlin

> Paris has been the capital since the 10th century.

## Q2 · Complete: The sun is a ___.

**Answer:** star
```

## Key features

- **Progressive levels** — minimal quiz needs zero config; scoring, timer, math unlocked via YAML frontmatter
- **All question types** — MCQ, multi-select, open answer, true/false, match, order
- **Math support** — LaTeX via KaTeX, auto-detected
- **AI-native** — designed to be generated and validated by AI assistants via MCP
- **Works standalone** — certifications, exams, knowledge checks without any other tooling
- **Embeddable** — integrates inside [LearnMD](https://github.com/neuroneo-md/learnmd) lessons as checkpoints

## Specification

See [SPEC.md](./SPEC.md) for the full format specification.

## Implementations

| Project | Type | Link |
|---------|------|------|
| neuroneo.md | Web player + API + MCP server | [neuroneo.md](https://www.neuroneo.md) |

> Built an implementation? Open a PR to add it here.

## Repository structure

```
quizmd/
├── SPEC.md              # Full format specification
├── CHANGELOG.md         # Version history
├── samples/             # Example .quiz.md files
├── schema/
│   └── quizmd.schema.json   # JSON Schema for frontmatter validation
├── tests/
│   ├── valid/           # Files that must parse successfully
│   └── invalid/         # Files that must fail validation
└── CONTRIBUTING.md
```

## Related

- [LearnMD](https://github.com/neuroneo-md/learnmd) — companion format for learning content
- [neuroneo.md](https://www.neuroneo.md) — community platform and reference implementation

## License

MIT — see [LICENSE](./LICENSE)
