# Changelog

All notable changes to the QuizMD specification are documented here.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).
Versioning follows [Semantic Versioning](https://semver.org/).

---

## [0.3.0] — 2026-05-10

### Context
QuizMD becomes part of the broader **LearnSpec** suite. Many additions align with universal LearnSpec conventions defined in the [Architecture Charter](https://github.com/learnspec/.github/blob/main/profile/README.md).

### Added
- `!ref` directive — declares a MediaMD or GlossaryMD context without inline rendering
- `!import` now supports `.diagram.md` files (DiagramMD reusable diagram bundles)
- `media:slug` image syntax with mandatory fallback URL — resolves to MediaMD entries
- Explicit support for DiagramMD Level 0 blocks in question bodies
- Frontmatter fields: `created`, `updated`, `license` (SPDX) — universal LearnSpec fields
- Principle: "LearnSpec-interoperable"

### Changed
- `lang` frontmatter field promoted from optional to **required** (warning in lenient mode, error in strict)
- `title` frontmatter field demoted from required to **optional** — inferred from the first `# H1` if absent
- ABC notation section removed — delegated to the [DiagramMD spec](https://github.com/learnspec/diagrammd)

### Breaking
- `lang` is now required (lenient: warning; strict: error)
- `title` is no longer required (parsers may need to derive it from H1)

---

## [0.2.0] — 2026-03-26

### Added
- `match` question type — pair matching with drag-and-drop support
- `order` question type — reorder items, scored with Kendall's tau
- `true_false` question type as a shorthand MCQ variant
- Per-choice feedback (indented `>` under each `- [x]` / `- [ ]` item)
- `> [!correct]` and `> [!incorrect]` differentiated global feedback
- Math auto-detection — `$...$` and `$$...$$` trigger KaTeX rendering automatically; `math:` frontmatter field removed
- `hint:` per-question frontmatter field (Level 2)
- `shuffle_questions` and `shuffle_answers` frontmatter flags

### Changed
- `math: boolean` frontmatter field replaced by auto-detection
- Scoring formula for `order` type now uses Kendall's tau τ

### Removed
- `math:` frontmatter field (auto-detected)

---

## [0.1.0] — 2025-09-01

### Added
- Initial specification draft
- Three progressive levels (0, 1, 2)
- Question types: MCQ, multi-select, open answer
- YAML frontmatter: `title`, `description`, `lang`, `domain`, `tags`, `reveal`, `feedback_mode`, `passing_score`, `time_limit`
- `!import` directive for composing quizzes from multiple files
- `reveal: all | sequential` display modes
- `feedback_mode: immediate | deferred` modes
- Global feedback via `>` blockquote
- `validate_quiz` strict and lenient modes
