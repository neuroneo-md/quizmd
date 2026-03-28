# QuizMD — Format Specification v0.2

## Core principle: YAML everywhere

QuizMD uses **YAML as its single configuration syntax**, applied across three progressive and backward-compatible levels. Keys are the same at every level — one mental model to learn.

| Level | Mechanism | Purpose |
|-------|-----------|---------|
| 0 | Plain `.quiz.md`, no configuration | Minimal quiz, human-readable |
| 1 | YAML frontmatter at top of file | Global metadata, behavior, scoring |
| 2 | Per-question ` ```quiz ` fenced block | Per-question overrides (points, timer, hint) |

A Level 0 file is valid at Level 1 and 2. A Level 1 file is valid at Level 2. Each level is a strict superset of the previous one.

---

## Level 0 — Base Markdown syntax

### Conventions

| Syntax | Meaning |
|--------|---------|
| `## Qn` or `## Qn · Title` | Start of a question |
| `- [x]` | Correct answer choice |
| `- [ ]` | Incorrect answer choice |
| `___` | Open-answer field (short answer / fill-in-the-blank) |
| `---` | Question separator (optional when `##` is used) |
| `> text` | Feedback / explanation (shown after the answer is submitted) |
| `!import ./file.quiz.md` | Include questions from a sub-quiz file |
| `$...$` | Inline LaTeX math formula |
| `$$...$$` | Block (display) LaTeX math formula |

### Question body

The body of a question is all Markdown content between the `## Qn` heading (and its optional ` ```quiz ` block) and the first answer choice (`- [ ]` / `- [x]`) or the `___` marker. The body may contain multiple paragraphs, lists, tables, math formulas, and images — any valid Markdown.

This mechanism supports **passage-based questions** (reading comprehension, physics problems, legal cases) without any additional syntax:

```markdown
## Q3 · Text analysis

Read the following passage carefully:

> "Freedom consists in being able to do anything that does not harm others."
> — Declaration of the Rights of Man and of the Citizen, Article 4 (1789)

This definition of freedom is called **negative liberty**: it delimits freedom by the absence of constraint rather than by the effective capacity to act. It contrasts with the **positive** conception of liberty (Isaiah Berlin, 1958), which emphasizes the real conditions enabling individuals to exercise their autonomy.

According to this passage, which statement is correct?

- [x] Negative liberty is defined by the absence of interference from others.
- [ ] Negative liberty guarantees the material means to act freely.
```

### Minimal example

```markdown
# My first quiz

## Q1 · What is the capital of France?

- [ ] London
- [x] Paris
- [ ] Berlin

> Paris has been the capital since the 10th century.

## Q2 · True or false: The Earth is flat.

- [ ] True
- [x] False

## Q3 · Fill in the blank: The sun is a ___.

**Answer:** star
```

---

## Question types

### MCQ — Single correct answer

One `- [x]` marks the correct choice. All other choices use `- [ ]`.

```markdown
## Q1 · Which composer wrote "The Four Seasons"?

- [ ] Johann Sebastian Bach
- [ ] George Frideric Handel
- [x] Antonio Vivaldi
- [ ] Arcangelo Corelli

> "The Four Seasons" (1725) is a set of four violin concertos by Vivaldi.
```

### Multi-select — Multiple correct answers

Two or more `- [x]` marks indicate multiple correct choices. Renderers should display checkboxes rather than radio buttons.

```markdown
## Q2 · Which of the following are characteristics of Baroque music?

- [x] Basso continuo
- [x] Terraced dynamics
- [ ] Twelve-tone serialism
- [x] Elaborate ornamentation
- [x] Counterpoint and polyphony
- [ ] Minimalist texture

> Serialism is 20th-century; minimalism is post-1960.
```

### Open answer — Fill in the blank

The `___` marker signals a free-text input field. The expected answer follows on a `**Answer:**` line.

```markdown
## Q3 · Fill in the blank: Bach's 30 keyboard variations are known as the ___ Variations.

**Answer:** Goldberg

> Named after the harpsichordist Johann Gottlieb Goldberg.
```

Multiple blanks in a single question are supported by repeating `___`:

```markdown
## Q4 · Complete: ___ was born in ___, Germany.

**Answer:** Handel | Halle
```

### True / False

A True/False question is an MCQ with exactly two choices labeled `True` and `False` (or their language equivalents).

```markdown
## Q5 · True or false: Handel was born in England.

- [ ] True
- [x] False

> Handel was born in Halle, Germany in 1685.
```

### Match pairs

A match question associates items from two columns. Declared with `type: match` in the per-question ` ```quiz ` block. Syntax uses a Markdown table:

````markdown
## Q6 · Match each composer with their nationality.

```quiz
type: match
points: 4
```

| Composer | Nationality |
|----------|-------------|
| Bach | German |
| Vivaldi | Italian |
| Handel | German |
| Rameau | French |
````

### Order

An order question asks the learner to sort items into the correct sequence. Declared with `type: order`. The correct order is the order in which items appear in the list:

````markdown
## Q7 · Place these Baroque composers in chronological order of birth (earliest first).

```quiz
type: order
points: 3
```

1. Claudio Monteverdi (1567)
2. Heinrich Schütz (1585)
3. Jean-Baptiste Lully (1632)
4. Henry Purcell (1659)
5. Antonio Vivaldi (1678)
````

---

## Feedback syntax

QuizMD supports four levels of feedback, freely combinable within a single question:

| Syntax | Scope | When displayed |
|--------|-------|----------------|
| `  > text` (indented under a choice) | Per-choice | Only when that choice is selected |
| `> [!correct] text` | Global | Only when the answer is correct |
| `> [!incorrect] text` | Global | Only when the answer is incorrect |
| `> text` | Global | Always (general explanation) |

### Full example

```markdown
## Q1 · What is the capital of France?

- [x] Paris
  > Correct — Paris has been the capital since the 10th century.
- [ ] London
  > No, London is the capital of the United Kingdom.
- [ ] Berlin
  > No, Berlin is the capital of Germany.

> [!correct] Excellent! Paris has been the capital since the reign of Hugh Capet.
> [!incorrect] The correct answer was Paris, France's capital since the 10th century.
> Paris is home to the French government and national institutions.
```

### Display priority rules

1. Per-choice feedback (indented) is displayed **inline**, below the option, **only if the learner selected it** — not for options that are simply revealed after submission.
2. `[!correct]` or `[!incorrect]` appears in the result banner according to the outcome.
3. Global `>` feedback always appears in the result banner, after the targeted feedback.
4. For open-answer questions (`___`), only `> [!correct]`, `> [!incorrect]`, and `> text` apply — per-choice feedback is not supported.

---

## The `!import` directive

The `!import` directive includes questions from another `.quiz.md` file directly into the current quiz. It is the primary mechanism for **composing quizzes from independent modules**.

### Syntax

```markdown
!import ./path/to/sub-quiz.quiz.md
```

The directive must appear alone on its line. The path is **relative** to the file that contains the directive.

### Behavior

- Questions from the sub-quiz are **inserted at the position of the directive** in the question stream.
- Questions are **renumbered sequentially** (Q1, Q2, … across the full assembled quiz).
- The **frontmatter of the sub-quiz is ignored** — only its questions are imported. Global metadata (title, language, scoring) come from the parent file.
- Imports are **recursive**: a sub-quiz may itself contain `!import` directives.
- **Circular import protection** is guaranteed: a file already being processed is silently skipped.
- Missing files are **ignored without error**, allowing partial assemblies.
- Multiple `!import` directives may coexist in a single file, in any order, interleaved with local questions.

### Example

```markdown
---
title: History of France — Complete course
lang: en
domain: academic
passing_score: 0.6
---

# History of France — Complete course

!import ./frankish-kingdom.quiz.md

!import ./french-revolution.quiz.md

!import ./napoleon.quiz.md
```

---

## Reveal and feedback modes

QuizMD supports two independent display-control axes, configurable in the frontmatter:

### `reveal` — question display

| Value | Behavior |
|-------|----------|
| `all` (default) | All questions are displayed at once |
| `sequential` | Questions are revealed one at a time; a **Next →** button advances after each answer |

### `feedback_mode` — when corrections appear

| Value | Behavior |
|-------|----------|
| `immediate` (default) | Correction (correct/incorrect, feedback) is shown immediately after submission |
| `deferred` | Answers are recorded without revealing corrections; a **See results** button reveals everything at the end |

### Typical combinations

| `reveal` | `feedback_mode` | Use case |
|----------|-----------------|----------|
| `all` | `immediate` | Practice mode (default behavior) |
| `sequential` | `immediate` | Guided progression, one question at a time |
| `all` | `deferred` | Paper-style exam: everything visible, corrections at the end |
| `sequential` | `deferred` | **Exam mode**: one question at a time, global results at the end |

---

## Level 1 — YAML frontmatter

A YAML block at the top of the `.quiz.md` file, between two `---` lines. Defines **global** quiz parameters.

```yaml
---
# Identity
title: string               # required
description: string
author: string | {name, email, url}
version: semver             # e.g. "1.0.0"
lang: BCP-47                # e.g. "fr", "en", "en-US"
tags: [string]
license: SPDX               # e.g. "CC-BY-4.0", "MIT"

# Domain
domain: recreational | academic | corporate | certification

# Behavior
reveal: all | sequential            # default: all
feedback_mode: immediate | deferred # default: immediate
shuffle_questions: bool             # default: false
shuffle_answers: bool               # default: true
passing_score: float                # 0.0–1.0
time_limit: int                     # seconds, applies to the whole quiz

# Scoring
scoring:
  correct: int              # points per correct answer
  incorrect: int            # may be negative (penalty scoring)
---
```

### Frontmatter field reference

| Field | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| `title` | string | Yes | — | Quiz title |
| `description` | string | No | — | Short description |
| `author` | string or object | No | — | Author name, or `{name, email, url}` |
| `lang` | BCP-47 | No | — | Language code (`en`, `fr`, `en-US`) |
| `tags` | string[] | No | `[]` | Thematic tags |
| `domain` | enum | No | — | `recreational`, `academic`, `corporate`, `certification` |
| `reveal` | enum | No | `all` | `all` or `sequential` |
| `feedback_mode` | enum | No | `immediate` | `immediate` or `deferred` |
| `shuffle_questions` | bool | No | `false` | Randomize question order |
| `shuffle_answers` | bool | No | `true` | Randomize answer choice order |
| `passing_score` | float | No | — | Minimum ratio to pass (0.0–1.0) |
| `time_limit` | int | No | — | Total time limit in seconds |
| `scoring.correct` | int | No | 1 | Points awarded per correct answer |
| `scoring.incorrect` | int | No | 0 | Points deducted per incorrect answer |
| `spec_version` | string | No | — | QuizMD spec version this file targets (e.g. `"0.2"`) |

### Level 1 example

```markdown
---
title: Baroque Music
description: Composers, works and characteristics of the Baroque era (c. 1600–1750)
lang: en
tags: [music, baroque, history]
domain: recreational
shuffle_answers: true
passing_score: 0.6
reveal: sequential
feedback_mode: deferred
scoring:
  correct: 2
  incorrect: 0
---

# Baroque Music

## Q1 · Which composer wrote "The Four Seasons"?

- [ ] Johann Sebastian Bach
- [x] Antonio Vivaldi
- [ ] George Frideric Handel
```

---

## Level 2 — Per-question fenced block

A ` ```quiz ` block placed **immediately after the question heading** overrides global parameters for that specific question. The content is YAML using the same keys as the rest of the format.

````markdown
## Q5 · What is the speed of light?

```quiz
id: q-light-speed
points: 10
timer: 30
difficulty: easy
tags: [physics]
hint: "Approximately 300,000 km/s"
type: mcq
```

- [ ] 150,000 km/s
- [x] 299,792 km/s
- [ ] 1,000,000 km/s
````

### Per-question block field reference

| Field | Type | Description |
|-------|------|-------------|
| `id` | string | Stable unique identifier for this question |
| `points` | int | Points for this question (overrides `scoring.correct`) |
| `timer` | int | Per-question time limit in seconds (overrides `time_limit`) |
| `hint` | string | Hint shown on demand before the answer is submitted |
| `difficulty` | enum | `easy`, `medium`, or `hard` |
| `tags` | string[] | Per-question thematic tags |
| `type` | enum | `mcq`, `multi`, `open`, `tf`, `match`, or `order` |
| `bloom` | enum | Bloom's taxonomy level: `remember`, `understand`, `apply`, `analyze`, `evaluate`, `create` |
| `depends_on` | string | ID of a question this one is conditional on |

The `type` field is inferred automatically from the answer syntax when omitted:
- One `- [x]` → `mcq`
- Two or more `- [x]` → `multi`
- `___` present → `open`
- Exactly two choices `True` / `False` → `tf`

Use `type` explicitly only to override inference or to declare `match` and `order` questions.

---

## Math support

QuizMD natively supports **LaTeX** math syntax, rendered via KaTeX in compatible renderers. Math may appear in question bodies, answer choices, feedback, and hints.

### Syntax

| Form | Syntax | Rendering |
|------|--------|-----------|
| Inline | `$E = mc^2$` | Embedded in the line of text |
| Block (display) | `$$\int_0^\infty e^{-x}\,dx = 1$$` | Centered on its own line |

Math is **auto-detected**: if a `.quiz.md` file contains `$` or `$$` delimiters, KaTeX is loaded automatically. No frontmatter flag is required.

### Example

```markdown
## Q1 · Kinetic energy

An object of mass $m = 2\,\text{kg}$ moves at $v = 10\,\text{m·s}^{-1}$.
What is its kinetic energy $E_k$?

- [x] $E_k = 100\,\text{J}$
  > $E_k = \frac{1}{2}mv^2 = \frac{1}{2} \times 2 \times 100 = 100\,\text{J}$
- [ ] $E_k = 20\,\text{J}$
  > You computed $mv$, not $\frac{1}{2}mv^2$.

> Recall: $$E_k = \frac{1}{2}mv^2$$
```

### Constraints

- LaTeX inside ` ```quiz ` YAML blocks must be quoted to avoid parsing conflicts: `hint: '$E = mc^2$'`
- The supported subset is **KaTeX** (see [katex.org/docs/support_table](https://katex.org/docs/support_table.html)). `\newcommand` macros and complex environments (`tikz`, `pgfplots`) are not supported.

---

## ABC music notation

QuizMD supports **ABC notation** for rendering sheet music inline in question bodies. Compatible renderers (e.g. neuroneo.md) use [abcjs](https://www.abcjs.net/) to produce SVG output directly in the browser — no server required.

### Syntax

Use a fenced code block with the language identifier `abc`:

````markdown
```abc
X:1
T:Scale of C major
M:4/4
L:1/4
K:C
CDEF|GABC|
```
````

### Rendering

- Compatible renderers replace the `abc` block with an inline SVG score.
- Non-compatible renderers (e.g. GitHub) display the raw ABC text as a code block — the format degrades gracefully.
- ABC notation may appear in question bodies. It is **not** supported inside answer choices, feedback, or hints.

### Example

```markdown
## Q1 · Which of these is a C major scale?

Listen to the following musical example:

\`\`\`abc
X:1
T:Example
M:4/4
L:1/4
K:C
CDEF|GABC|
\`\`\`

- [x] C D E F G A B C
- [ ] C D Eb F G Ab Bb C
```

---

## Partial scoring

When `partial_scoring: true` (default), **match** and **order** questions award a proportional score rather than all-or-nothing.

### `type: match` — pair score

```
score = correct_pairs / total_pairs   ∈ [0, 1]
```

### `type: order` — Kendall's tau

The quality of a ranking is measured by **Kendall's tau** (τ): the ratio of concordant pairs (in the same relative order as the solution) to all possible pairs.

```
τ = concordant_pairs / (n × (n−1) / 2)   ∈ [0, 1]
score = τ
```

| Submitted ranking | τ | Interpretation |
|-------------------|----|----------------|
| Identical to the answer key | 1.0 | Perfect |
| One adjacent swap | ≈ 0.93 (n=5) | Near-perfect |
| Random order (on average) | ≈ 0.5 | Chance |
| Fully reversed | 0.0 | Completely wrong |

To disable: set `partial_scoring: false` in the frontmatter. This reverts to binary scoring (full points or zero).

---

## Syntax reference table

| Element | Syntax | Level |
|---------|--------|-------|
| Quiz title | `# Title` | 0 |
| Question heading | `## Q1` or `## Q1 · Title` | 0 |
| Correct choice | `- [x] text` | 0 |
| Incorrect choice | `- [ ] text` | 0 |
| Open answer marker | `___` | 0 |
| Expected answer | `**Answer:** value` | 0 |
| Per-choice feedback | `  > text` (indented 2 spaces) | 0 |
| Correct-only feedback | `> [!correct] text` | 0 |
| Incorrect-only feedback | `> [!incorrect] text` | 0 |
| General feedback | `> text` | 0 |
| Sub-quiz import | `!import ./file.quiz.md` | 0 |
| Inline math | `$formula$` | 0 |
| Block math | `$$formula$$` | 0 |
| Frontmatter | `---` YAML `---` | 1 |
| Per-question config | ` ```quiz ` YAML ` ``` ` | 2 |
| ABC music notation | ` ```abc ` ABC text ` ``` ` | 0 |

---

## Validation

QuizMD validators operate in two modes:

### Lenient mode (default)

| Condition | Level |
|-----------|-------|
| No correct answer (`- [x]`) in an MCQ | Warning |
| `title` absent from frontmatter | Warning |
| `lang` absent from frontmatter | Warning |
| Unclosed ` ```quiz ` block | Error |
| `!import` pointing to a missing file | Warning |
| Frontmatter YAML parse error | Error |

### Strict mode (`--strict`)

| Condition | Level |
|-----------|-------|
| `title` absent | Error |
| `lang` absent | Error |
| No correct answer in any question | Error |
| All lenient-mode errors | Error |

Strict mode is recommended for CI pipelines and production publishing. Lenient mode is appropriate during authoring.

---

## Complete example — Level 2

````markdown
---
title: Physics Exam — Mechanics
lang: en
domain: academic
tags: [physics, mechanics, exam]
passing_score: 0.6
reveal: sequential
feedback_mode: deferred
scoring:
  correct: 2
  incorrect: 0
---

# Physics Exam — Mechanics

## Q1 · What is the speed of light in a vacuum?

```quiz
id: q-speed-of-light
points: 2
difficulty: easy
hint: "Approximately 3 × 10⁸ m/s"
```

- [ ] 150,000 km/s
- [x] 299,792 km/s
- [ ] 1,000,000 km/s
- [ ] 3,000 km/s

> The speed of light in a vacuum is c ≈ 2.998 × 10⁸ m/s, a fundamental constant of physics.

## Q2 · True or false: The mass of an object increases when heated.

```quiz
id: q-mass-heat
points: 2
difficulty: medium
```

- [ ] True
- [x] False

> Mass is invariant in classical physics. It is volume that increases with temperature, not mass.

## Q3 · State Newton's second law: F = ___.

```quiz
id: q-newton-2
points: 2
difficulty: medium
```

**Answer:** ma

> F = ma: the net force equals the product of mass and acceleration.

## Q4 · Which of the following are examples of diffraction?

```quiz
id: q-diffraction
points: 3
difficulty: hard
type: multi
```

- [x] Light passing through a narrow slit
- [ ] Refraction through a prism
- [x] Sound bending around an obstacle
- [x] Radio waves passing through an aperture
- [ ] Reflection off a mirror

> Diffraction is the bending of a wave around obstacles or through openings. Refraction and reflection are distinct phenomena.

## Q5 · Match each unit with the quantity it measures.

```quiz
id: q-units
type: match
points: 4
difficulty: easy
```

| Unit | Quantity |
|------|----------|
| Newton | Force |
| Joule | Energy |
| Watt | Power |
| Pascal | Pressure |
````

---

## MCP integration

QuizMD provides a reference MCP server that exposes the format to compatible AI assistants.

### Exposed tools

| Tool | Input | Output |
|------|-------|--------|
| `list_samples` | — | List of samples with metadata |
| `get_sample` | `name: string` | Raw `.quiz.md` file content |
| `parse_quiz` | `content: string` | JSON structure (title, questions, imports, meta) |
| `validate_quiz` | `content: string` | List of errors and warnings |
| `check_open_answer` | `student_answer, correct_answer` | `{correct: bool, matched_alternative: string}` |
| `upload_quiz` | `content, api_key, title` | Hosted quiz URL on neuroneo.md |

The `parse_quiz` output includes, for each question, `source_file` and `source_title` when the question originates from an imported sub-quiz. The `imports` field lists all sub-quiz paths declared in the file.

