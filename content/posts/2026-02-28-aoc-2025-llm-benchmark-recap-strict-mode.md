+++
title = "Benchmarking LLMs on Advent of Code 2025 — Recap Strict Mode"
description = "Same 10 models, same 12 languages, but no retries and no scaffolding. No model achieved a perfect score."

[taxonomies]
tags = ["AI", "Advent of Code"]
+++

This is a second run of the [AoC 2025 LLM benchmark](@/posts/2026-02-28-aoc-2025-llm-benchmark-recap.md),
with stricter rules. The same 10 models solved the same 5 days (10 parts) across the same
12 programming languages, but with two changes:

1. **No retries.** A wrong answer or timeout results in immediate ejection from that
   language. No nudges, no second chances.
2. **No language-specific scaffolding.** No system prompts teaching syntax (as was done
   for ReScript run 3 in the previous benchmark). Every model receives the same prompt
   regardless of language.

The previous benchmark allowed retries during the run, then applied strict scoring
retroactively in the recap. This run enforces strict mode at execution time — ejected
models never get the chance to try again.

<!-- more -->

## Setup

| Parameter | Value |
|:--|:--|
| Puzzles | AoC 2025 Days 1–5, Parts 1 and 2 |
| Languages | 12 (see below) |
| Models | 10 (see below) |
| Per-model timeout | 120 seconds |
| Extended thinking | off |
| Execution timeout | 5 seconds per solution run |
| Retries | none |
| Language-specific prompts | none |

Each model faces 10 parts × 12 languages = **120 total parts**.

Ejection is language-local: failing in Haskell does not affect participation in OCaml.

The full run took **3 hours wall-clock** (11:49–14:49 CET), processing 1,200 model-part
slots at a combined API cost of **$24.50**.

## The models

| # | Model |
| -:| :------|
| 1 | `anthropic/claude-opus-4-6` |
| 2 | `anthropic/claude-sonnet-4-6` |
| 3 | `anthropic/claude-haiku-4-5` |
| 4 | `openai-codex/gpt-5.3-codex` |
| 5 | `zai/glm-5` |
| 6 | `minimax/MiniMax-M2.5` |
| 7 | `kimi-coding/k2p5` |
| 8 | `mistral/devstral-2512` |
| 9 | `alibaba/qwen3.5-plus` |
| 10 | `alibaba/qwen3-coder-next` |

## The languages

| # | Language | Paradigm |
| -:| :--------| :--------|
| 1 | Haskell | Pure FP, compiled |
| 2 | OCaml | FP, compiled |
| 3 | Python | Dynamic, imperative |
| 4 | Ruby | Dynamic, OO |
| 5 | Elixir | FP, dynamic (BEAM) |
| 6 | Elm | Pure FP, compiles to JS |
| 7 | Java | OO, compiled (JVM) |
| 8 | ReScript | FP, compiles to JS |
| 9 | F# | FP-first (.NET) |
| 10 | Rust | Systems, compiled |
| 11 | Clojure | Lisp (JVM) |
| 12 | Racket | Lisp (Scheme family) |

---

## The results

### Global ranking

| Rank | Model | Score | Perfect langs | Total time | Total cost |
| :---:| :------| ----:| :---:| ----:| ----:|
| 1 | claude-opus-4-6 | 93/120 | 9/12 | 2456s | $10.20 |
| 2 | claude-sonnet-4-6 | 91/120 | 9/12 | 2299s | $3.98 |
| 3 | claude-haiku-4-5 | 71/120 | 6/12 | 1234s | $2.00 |
| 4 | gpt-5.3-codex | 69/120 | 5/12 | 1239s | $1.74 |
| 5 | qwen3.5-plus | 66/120 | 5/12 | 2792s | $1.72 |
| 6 | devstral-2512 | 53/120 | 4/12 | 1383s | $1.78 |
| 7 | kimi-coding/k2p5 | 52/120 | 4/12 | 1861s | $0.56 |
| 8 | zai/glm-5 | 51/120 | 4/12 | 2156s | $0.82 |
| 9 | qwen3-coder-next | 23/120 | 1/12 | 683s | $1.39 |
| 10 | MiniMax-M2.5 | 9/120 | 0/12 | 470s | $0.31 |

No model achieved 120/120. In the [previous benchmark's recap](@/posts/2026-02-28-aoc-2025-llm-benchmark-recap.md),
`claude-opus-4-6` and `claude-sonnet-4-6` both went 120/120 using strict retroactive
scoring. The difference here is the absence of language-specific scaffolding (the
ReScript system prompt) and the enforcement of ejection at runtime (no recovery from
near-misses that retries would have caught).

---

### Cross-language score matrix

<div style="overflow-x: auto">

| Model | HS | ML | PY | RB | EX | ELM | JV | RS | F# | RUST | CLJ | RKT |
|:------|---:|---:|---:|---:|---:|----:|---:|---:|---:|-----:|----:|----:|
| claude-opus-4-6 | 10 | 10 | 10 | 10 | 10 | 10 | 10 | 0 | 0 | 10 | 3 | 10 |
| claude-sonnet-4-6 | 10 | 10 | 10 | 10 | 10 | 10 | 10 | 0 | 0 | 10 | 10 | 1 |
| claude-haiku-4-5 | 1 | 10 | 10 | 10 | 10 | 4 | 10 | 0 | 0 | 10 | 1 | 5 |
| gpt-5.3-codex | 1 | 10 | 10 | 10 | 2 | 0 | 4 | 4 | 10 | 4 | 10 | 4 |
| qwen3.5-plus | 5 | 10 | 10 | 10 | 10 | 0 | 1 | 0 | 10 | 3 | 2 | 5 |
| devstral-2512 | 3 | 1 | 1 | 10 | 1 | 1 | 10 | 0 | 10 | 10 | 1 | 5 |
| kimi-coding/k2p5 | 10 | 1 | 10 | 1 | 0 | 4 | 1 | 2 | 2 | 10 | 1 | 10 |
| zai/glm-5 | 10 | 1 | 10 | 10 | 1 | 0 | 10 | 0 | 4 | 1 | 3 | 1 |
| qwen3-coder-next | 5 | 0 | 1 | 10 | 1 | 0 | 1 | 0 | 2 | 1 | 1 | 1 |
| MiniMax-M2.5 | 1 | 1 | 1 | 1 | 1 | 0 | 1 | 0 | 1 | 1 | 0 | 1 |

</div>

Legend: HS=Haskell, ML=OCaml, PY=Python, RB=Ruby, EX=Elixir, ELM=Elm, JV=Java,
RS=ReScript, F#=F#, RUST=Rust, CLJ=Clojure, RKT=Racket.

---

### Language difficulty

Models achieving a perfect 10/10 per language:

| Language | Perfect solvers (out of 10) | Which models |
|:---------|:---:|:------|
| Ruby | 8 | opus, sonnet, haiku, codex, glm-5, devstral, qwen3.5-plus, qwen3-coder-next |
| Python | 7 | opus, sonnet, haiku, codex, glm-5, k2p5, qwen3.5-plus |
| Java | 5 | opus, sonnet, haiku, glm-5, devstral |
| Rust | 5 | opus, sonnet, haiku, k2p5, devstral |
| Haskell | 4 | opus, sonnet, glm-5, k2p5 |
| OCaml | 5 | opus, sonnet, haiku, codex, qwen3.5-plus |
| Elixir | 4 | opus, sonnet, haiku, qwen3.5-plus |
| F# | 3 | codex, devstral, qwen3.5-plus |
| Elm | 2 | opus, sonnet |
| Clojure | 2 | sonnet, codex |
| Racket | 2 | opus, k2p5 |
| ReScript | 0 | (none) |

ReScript was the only language where no model achieved 10/10. The highest score was
`gpt-5.3-codex` with 4/10.

---

### ReScript and F#: total failure for Anthropic models

All three Anthropic models (`claude-opus-4-6`, `claude-sonnet-4-6`, `claude-haiku-4-5`)
scored **0/10 on both ReScript and F#**. All six failures were timeouts on Day 01
Part 1 — the models did not produce an answer within 120 seconds on the first puzzle.

These two languages require specific toolchain setup (`dotnet` for F#, `npm`/`rescript`
for ReScript). The 120-second timeout includes environment setup time. In the previous
benchmark, the ReScript run 3 used a system prompt that taught the language syntax,
which eliminated toolchain friction. No such scaffolding was provided here.

The models that succeeded on these languages — `gpt-5.3-codex`, `devstral-2512`,
`qwen3.5-plus`, `kimi-coding/k2p5` — produced working solutions within the timeout.

---

### Where each model failed

**claude-opus-4-6** (93/120) — Scored 0/10 on ReScript and F# (timeout D01P1 on both).
Wrong answer on Clojure D02P2. Perfect on the remaining 9 languages.

**claude-sonnet-4-6** (91/120) — Scored 0/10 on ReScript and F# (same timeout issue).
Wrong answer on Racket D01P2. Perfect on the remaining 9 languages.

**claude-haiku-4-5** (71/120) — Scored 0/10 on ReScript and F#. Wrong answers on
Haskell D01P2, Elm D03P1, and Clojure D01P2. Perfect on OCaml, Python, Ruby, Elixir,
Java, and Rust.

**gpt-5.3-codex** (69/120) — Scored 0/10 on Elm (timeout D01P1). Failed on Haskell
D01P2 (timeout), Elixir D02P1 (timeout), Java D03P1 (wrong answer), Rust D03P1
(wrong answer), Racket D03P1 (wrong answer), ReScript D03P1 (timeout). Perfect on
OCaml, Python, Ruby, F#, and Clojure.

**qwen3.5-plus** (66/120) — Scored 0/10 on Elm and ReScript (both timeout D01P1).
Ejected from Haskell D03P2 by code review. Failed on Java D01P2 (timeout), Rust D02P2
(timeout), Clojure D02P1 (timeout), Racket D03P2 (timeout). Perfect on OCaml, Python,
Ruby, Elixir, and F#.

**devstral-2512** (53/120) — Scored 0/10 on ReScript (timeout D01P1). Failed on
Haskell D02P2 (ejected by code review), OCaml D01P2 (wrong answer), Python D01P2
(timeout), Elixir D01P2 (wrong answer), Elm D01P2 (wrong answer), Clojure D01P2
(timeout), Racket D03P2 (timeout). Perfect on Ruby, Java, F#, and Rust.

**kimi-coding/k2p5** (52/120) — Scored 0/10 on Elixir (timeout D01P1). Failed on
OCaml D01P2 (timeout), Ruby D01P2 (timeout), Elm D03P1 (timeout), Java D01P2 (wrong
answer), ReScript D02P1 (timeout), F# D02P1 (timeout), Clojure D01P2 (wrong answer).
Perfect on Haskell, Python, Rust, and Racket.

**zai/glm-5** (51/120) — Scored 0/10 on Elm and ReScript (both timeout D01P1). Failed
on OCaml D01P2 (timeout), Elixir D01P2 (timeout), F# D03P1 (wrong answer — output a
different day's answer), Rust D01P2 (timeout), Clojure D02P2 (timeout), Racket D01P2
(timeout). Perfect on Haskell, Python, Ruby, and Java.

**qwen3-coder-next** (23/120) — Scored 0/10 on OCaml, Elm, and ReScript (all timeout
D01P1). Ejected from Haskell D03P2 by code review. Failed early (D01P2) in Python,
Elixir, Java, Clojure, and Racket. Perfect only on Ruby.

**MiniMax-M2.5** (9/120) — Scored 0/10 on Elm, ReScript, and Clojure. Failed on D01P2
in 7 other languages. Scored only 1/10 (D01P1 only) in every other language. Perfect on
no language.

---

### Cost per model

| Model | Total cost | Cost per passed part |
|:------|----:|----:|
| claude-opus-4-6 | $10.20 | $0.110 |
| claude-sonnet-4-6 | $3.98 | $0.044 |
| claude-haiku-4-5 | $2.00 | $0.028 |
| devstral-2512 | $1.78 | $0.034 |
| openai-codex/gpt-5.3-codex | $1.74 | $0.025 |
| alibaba/qwen3.5-plus | $1.72 | $0.026 |
| alibaba/qwen3-coder-next | $1.39 | $0.060 |
| zai/glm-5 | $0.82 | $0.016 |
| kimi-coding/k2p5 | $0.56 | $0.011 |
| minimax/MiniMax-M2.5 | $0.31 | $0.034 |

---

### Code review ejections (flawed)

The benchmark included a code review phase after each part for the Haskell language.
Two independent reviewer agents (`claude-opus-4-6` and `gpt-5.3-codex`) read the source
code produced by each model and checked whether it was written in the target language and
actually solved the stated problem.

Three models were ejected from Haskell due to code review findings. In all three cases,
the ejections were **false positives** — the models had produced the correct answer by
solving the correct problem. The reviewers disagreed, and the reconciliation rule
(either reviewer flags `lang_ok=false` → ejection) allowed one reviewer's error to
override the other's correct assessment.

**devstral-2512** (Haskell D02P2): `opus` found the correct solution file and rated
it 5/10. `codex` looked at leftover Day 1 files in the workspace and concluded the
model was solving a different problem. Reconciled: 2.5/10, ejected.

**qwen3.5-plus** (Haskell D03P2): `opus` found the correct greedy-subsequence solution
and rated it 5/10. `codex` flagged leftover Day 2 code (invalid-ID ranges) as the
primary implementation. Reconciled: 2.5/10, ejected.

**qwen3-coder-next** (Haskell D03P2): Same pattern. `opus` rated the correct solution
5/10. `codex` flagged leftover files from earlier days. Reconciled: 2.5/10, ejected.

The common factor: all three models left `.hs` files from previous days in their
workspace. One reviewer evaluated the workspace holistically and misidentified
leftover code as the primary solution. The other reviewer correctly identified the
actual solution file.

Code reviews were not run for languages after Haskell (the streamlined run script did
not include the review phase). Given the false positive rate observed in Haskell,
this is not a significant loss.

---

### Comparison to the previous benchmark

The previous benchmark applied strict scoring retroactively: retries counted as
failures, but models still had the opportunity to retry during execution, meaning their
context and code were preserved even after a wrong answer. Additionally, ReScript run 3
used a 150-line system prompt teaching the language.

Key differences in outcomes:

| Metric | Previous (strict retroactive) | This run (strict enforced) |
|:-------|----:|----:|
| Top score | 120/120 (opus, sonnet) | 93/120 (opus) |
| Models with ≥100/120 | 2 | 0 |
| ReScript perfect solvers | 4 | 0 |
| F# perfect solvers | 5 | 3 |
| Languages with ≥8 perfect solvers | 2 (Python, Ruby) | 2 (Python, Ruby) |

The gap between retroactive strict scoring and enforced strict mode is 27 points for
opus and 29 for sonnet. Most of the gap comes from ReScript (0 vs 10) and F# (0 vs 10),
where the absence of scaffolding caused immediate timeout.

---

### Patterns in the data

**Day 01 Part 2 is the most common single-part failure point.** Of the models that
passed D01P1 in a given language, the D01P2 step was where the majority of ejections
occurred. In OCaml, 9 models passed D01P1 but only 5 passed D01P2. In Java, all 10
passed D01P1 but only 6 passed D01P2.

**Once a model passes Day 01, it tends to complete the language.** Models that survived
both parts of Day 01 had high completion rates for the remaining days. The exceptions
were Elm (haiku failed D03P1, k2p5 timed out D03P1), Clojure (opus wrong on D02P2,
glm-5 timed out D02P2), and Racket (several models failed on Day 03).

**Toolchain setup consumes a significant portion of the 120-second timeout.** Languages
requiring project scaffolding (ReScript, F#, Elm) had higher timeout rates on D01P1 than
languages with simpler toolchains (Python, Ruby, Java). All three Anthropic models timed
out on ReScript D01P1 and F# D01P1.

**The same wrong answer for Day 01 Part 2 appeared across multiple models and
languages.** Haiku (Haskell, Clojure), k2p5 (Java, Clojure), and sonnet (Racket) all
produced the identical incorrect value. This suggests a common algorithmic error in the
Day 01 Part 2 solution logic rather than language-specific bugs.

---

## Methodology

The benchmark was orchestrated by a prompt for
[pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent), a CLI coding
agent. The prompt turns pi into a benchmark controller that:

- Launches one pi agent per model in separate tmux windows
- Feeds puzzle descriptions and input file paths
- Polls for `ANSWER.txt` completion
- Compares answers against a pre-computed reference table
- Ejects failing models immediately
- Collects timing, token counts, and API costs from session JSONL files

Each agent works in complete isolation — its own directory, no shared state, no awareness
of other models. Part 2 reuses the Part 1 session (agents keep their code and context).

Models were launched with a 3-second stagger to avoid settings-file lock contention.
Elapsed time is measured from each model's launch time, not the global start. All agents
ran under `nice -n 10`.

The Haskell language included a code review phase after each part, using two independent
reviewer agents. This was not included for subsequent languages.

These are single-run results. Wall-clock times are influenced by inference platform load
and concurrent system activity. The raw CSV data is available in the benchmark working
directory.

---

## Orchestration prompt

The full prompt used to orchestrate this benchmark is included below for reproducibility.
This prompt is passed as the initial user message to a pi agent running
`anthropic/claude-sonnet-4-6`. It can be reused with different model lists by updating
`~/.pi/agent/settings.json`.

<details>
<summary>Click to expand the full orchestration prompt (~800 lines)</summary>

~~~text
You are the **Benchmark AOC 2025 (strict)** orchestrator. You run all enabled models in
parallel across every target language, one language at a time, collecting timing, tokens,
and cost. No retries, no nudges — one shot per model per part.

## Hardcoded defaults

- **Year**: `2025` (fixed)
- **Thinking level**: `off`
- **Timeout**: `120` seconds
- **End day**: `5`
- **Start language**: Haskell (first in list)

## Optional arguments

The user may have provided overrides:

Parse positionally (all optional):

1. **Thinking level** (`off`, `minimal`, `low`, `medium`, `high`, `xhigh`)
2. **Timeout** (seconds)
3. **End day** (e.g. `5`)
4. **Start language** — allows resuming after a crash (e.g. `Python` to skip Haskell and OCaml)

If no arguments are provided, use all defaults above and proceed immediately — never ask.

Example invocations:

- `/benchmark-aoc-2025` — all defaults: thinking:off, 120s timeout, days 1–5, all languages
- `/benchmark-aoc-2025 off 180 5 OCaml` — resume from OCaml, 180s timeout

---

## Fixed language set (run in order)

1. Haskell
2. OCaml
3. Python
4. Ruby
5. Elixir
6. Elm
7. Java
8. ReScript
9. F#
10. Rust
11. Clojure
12. Racket

Each language is a full independent run (days 1–`end_day`). All models start fresh for each
language. Ejection is **language-local** — failing in Haskell does not affect Python.

---

## Strict rules

1. **One attempt only** per model per part — no nudges, no retries, no escalation
2. **Hard timeout** — if ANSWER.txt is not written within `timeout` seconds (measured from
   that model's launch/inject time), the model fails immediately
3. **Wrong answer = immediate ejection** for that language run
4. **No ANSWER.txt at timeout = immediate ejection** for that language run
5. **Ejection is language-local** — the model participates in subsequent languages
6. **No language-specific scaffolding** — no templates, no system prompts, no tutoring
7. **Part 2 reuses the Part 1 session** — agents keep their Part 1 code and context

---

## Reference implementation

Used at setup to pre-populate the correct-answers table, enabling fully autonomous operation.

**Default path (try automatically before asking):**
```
~/code/github.com/benjamin-thomas/multi-playground/aoc/2025/haskell/
```

If that path exists, use it without asking. If not, ask the user.

### How to run the Haskell reference implementation

The reference lives at `~/code/github.com/benjamin-thomas/multi-playground/aoc/2025/haskell/`
and inputs at `~/code/github.com/benjamin-thomas/multi-playground/aoc/2025/inputs/`.

Input filenames follow the pattern `DayNN.txt` (e.g. `Day01.txt`, `Day02.txt`).

Two patterns exist in the codebase — detect per file:

**Pattern A — file has a `main` function:**
```bash
cd ~/code/github.com/benjamin-thomas/multi-playground/aoc/2025/haskell/
timeout 120 runghc DayNN.hs 2>&1
```
Parse stdout for lines matching `solve1 (real)` / `solve2 (real)`. The answer appears after
`✓` in the output:
```
solve1 (real)  ✓ 28146997880
solve2 (real)  ✓ 40028128307
```
Strip any `Right ` prefix.

**Pattern B — no `main` function:**
Scan for GHCi-style answer comments:
```haskell
{-
*Main> readFile "../inputs/Day01.txt" >>= print . solve1 . lines
1064
-}
```
Extract the answer that follows the `readFile` line inside the comment block.

**Neither pattern** → inspect more carefully. If still can't extract, leave blank and ask
the user when that day is reached.

Display the table before starting:
```
Reference answers extracted:
  Day01  Part1: 1064              Part2: 6122
  Day02  Part1: 28146997880       Part2: 40028128307
  ...
```

---

## Required filesystem layout

Inputs: `/home/benjamin/benchmark/aoc-inputs/2025/inputs/`

```
DayNN/
  input.example
  input.real
```

Description archive: `/home/benjamin/benchmark/aoc-descriptions/2025/`

```
DayNN/
  PART_1.description
  PART_2.description
```

When the orchestrator needs a description:
1. Check if it exists in the archive
2. If yes → copy it to each active model's subdirectory
3. If no → ask the user to paste it, then save to the archive for future runs

Descriptions are never placed in model subdirs until the orchestrator reaches that part.

Zero-pad day numbers everywhere: `Day01`, `Day02`, ..., `Day09`, `Day10`, etc.
Use `printf '%02d'` (NOT `seq -w`, which doesn't pad single-digit ranges).

---

## Directory structure

```
<work_dir>/
  results/
    part_results.csv
    language_summary.csv
    global_summary.csv
    reviews.csv
  reviews/
    <Language>/
      Day<NN>P<P>/
        reviewer-opus/
          REVIEW.json
          DONE
        reviewer-codex/
          REVIEW.json
          DONE
  Haskell/
    anthropic__claude-opus-4-6/
    anthropic__claude-sonnet-4-6/
    ...
  OCaml/
    anthropic__claude-opus-4-6/
    ...
  ...
```

Model subdir naming — sanitize the full model name:
- `/` → `__`
- `.` → `_`

Examples:
- `anthropic/claude-opus-4-6` → `anthropic__claude-opus-4-6`
- `alibaba/qwen3.5-plus` → `alibaba__qwen3_5-plus`
- `openai-codex/gpt-5.3-codex` → `openai-codex__gpt-5_3-codex`

---

## Main loop — language iteration

For each language in the fixed set (or starting from `start_language`):

1. Print banner: `═══ Starting language: <Language> ═══`
2. Reset `active_models` to `all_models`
3. **Clean previous run data** for this language
4. Create fresh subdirectories for each model
5. Run the **day loop** for days 1–`end_day`
6. After all days: display the **per-language summary tables**
7. Append rows to `language_summary.csv`
8. Move to next language

After the last language: display **cross-language summary**, write `global_summary.csv`.

---

## Day loop (within a language)

For each day, parts 1 then 2.

### Phase A — Launch Part 1

1. Distribute description to each active model's subdir
2. Clear stale ANSWER.txt
3. Record start time
4. Launch tmux windows (3-second stagger between models)
5. Poll for completion every 15 seconds

### Phase B — Collect and eject

1. Read ANSWER.txt (or note absence)
2. Collect tokens and cost from session JSONL
3. Compare against reference answers
4. Classify: pass, fail_wrong, fail_timeout
5. Display leaderboard
6. Eject failing models (kill tmux window, mark remaining parts as forfeit)
7. Append to CSV

### Phase B½ — Code Review (Haskell only in this run)

Two reviewer agents evaluate code quality of all active models. Models flagged for wrong
language, hardcoded answers, or reconciled rating < 3 are ejected.

### Phase C — Advance

- Part 1 → inject Part 2 into surviving windows
- Part 2 → archive JSONL files, kill windows, advance to next day

---

## Rules

- NEVER solve puzzles yourself
- NEVER give nudges, retries, or second chances
- NEVER delete session JSONL files — archive them
- ALWAYS launch all active models in parallel
- ALWAYS use 3-second stagger between launches
- ALWAYS subtract per-model launch offsets when computing elapsed time
- ALWAYS trim whitespace when comparing answers
- ALWAYS collect token and cost data after every part
- ALWAYS reset active_models to full list when starting a new language
~~~

</details>

---

*Benchmarked on 2026-02-28 using [pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent)
as the agent harness. This post was written with AI assistance.*
