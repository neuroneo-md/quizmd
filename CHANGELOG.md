# Changelog

All notable changes to the QuizMD specification are documented here.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).
Versioning follows [Semantic Versioning](https://semver.org/).

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
