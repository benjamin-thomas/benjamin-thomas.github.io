+++
title = "Benchmarking LLMs on Advent of Code 2025 — The Recap"
description = "12 languages, 10 models, 120 puzzle parts each. Two models went flawless. Most didn't. Here's what happened."

[taxonomies]
tags = ["AI", "Advent of Code"]
+++

Over the past week I ran the same 10 AoC 2025 puzzles (Days 1–5, Parts 1 and 2) across
**12 programming languages**, pitting **10 LLMs** against each other in complete
isolation. Each model got the same puzzle, the same inputs, and had to produce a correct
answer — or be ejected.

This post pulls together the results from all 12 individual benchmark posts and applies a
stricter scoring rule: **a retry counts as a failure**. Only first-try correct answers
count as passes.

I am an AI reviewer assisting with this recap. I also reviewed the generated code in the
benchmark directories for indicators such as language-idiomatic usage, raw JavaScript
injection in ReScript, and general implementation quality. These quality checks are
heuristic and should be interpreted as qualitative signal, not ground truth.

<!-- more -->

## The languages

| Language | Paradigm | Post |
| --------| --------| ----|
| Haskell | Pure FP, compiled | [results](@/posts/2026-02-24-aoc-2025-llm-benchmark-haskell.md) |
| OCaml | FP, compiled | [results](@/posts/2026-02-25-aoc-2025-llm-benchmark-ocaml.md) |
| Python | Dynamic, imperative | [results](@/posts/2026-02-25-aoc-2025-llm-benchmark-python.md) |
| Ruby | Dynamic, OO | [results](@/posts/2026-02-26-aoc-2025-llm-benchmark-ruby.md) |
| Elixir | FP, dynamic (BEAM) | [results](@/posts/2026-02-26-aoc-2025-llm-benchmark-elixir.md) |
| Elm | Pure FP, compiles to JS | [results](@/posts/2026-02-26-aoc-2025-llm-benchmark-elm.md) |
| Java | OO, compiled (JVM) | [results](@/posts/2026-02-26-aoc-2025-llm-benchmark-java.md) |
| ReScript | FP, compiles to JS | [results](@/posts/2026-02-26-aoc-2025-llm-benchmark-rescript.md) |
| F# | FP-first (.NET) | [results](@/posts/2026-02-27-aoc-2025-llm-benchmark-fsharp.md) |
| Rust | Systems, compiled | [results](@/posts/2026-02-27-aoc-2025-llm-benchmark-rust.md) |
| Clojure | Lisp (JVM) | [results](@/posts/2026-02-27-aoc-2025-llm-benchmark-clojure.md) |
| Racket | Lisp (Scheme family) | [results](@/posts/2026-02-27-aoc-2025-llm-benchmark-racket.md) |

ReScript was benchmarked three times with escalating interventions (no help → overflow
warning → system prompt teaching the language). Only **run 3** (with the system prompt)
is used in this recap.

A separate post covers a [local Ollama model](@/posts/2026-02-27-aoc-2025-llm-benchmark-local-ollama.md)
on Day 1 only — not included in the cross-language results.

## The models

| # | Model |
| -:| ------:|
| 1 | `anthropic/claude-opus-4-6` |
| 2 | `anthropic/claude-sonnet-4-6` |
| 3 | `openai-codex/gpt-5.3-codex` |
| 4 | `anthropic/claude-haiku-4-5` |
| 5 | `kimi-coding/k2p5` |
| 6 | `zai/glm-5` |
| 7 | `alibaba/qwen3.5-plus` |
| 8 | `mistral/devstral-2512` |
| 9 | `minimax/MiniMax-M2.5` |
| 10 | `alibaba/qwen3-coder-next` |

## Scoring rules

- **First-try correct** = pass. Anything else = failure.
- **Retry then correct** = failure (the model got it wrong at least once).
- **Ejection** = failure on that part and all subsequent parts in that language.
- Each model faces 10 parts × 12 languages = **120 total parts**.

---

## The results

### Global model ranking

<table>
  <thead>
    <tr>
      <th style="text-align: right">Rank</th>
      <th style="text-align: left">Model</th>
      <th style="text-align: right">Perfect langs</th>
      <th style="text-align: right">Retries</th>
      <th style="text-align: right">Ejections</th>
      <th style="text-align: right">Failure incidents<br>(retry + ejection)</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align: right"><strong>🥇 1</strong></td>
      <td><strong>claude-opus-4-6</strong></td>
      <td style="text-align: right"><strong>12/12</strong></td>
      <td style="text-align: right"><strong>0</strong></td>
      <td style="text-align: right"><strong>0</strong></td>
      <td style="text-align: right"><strong>0</strong></td>
    </tr>
    <tr>
      <td style="text-align: right"><strong>🥇 1</strong></td>
      <td><strong>claude-sonnet-4-6</strong></td>
      <td style="text-align: right"><strong>12/12</strong></td>
      <td style="text-align: right"><strong>0</strong></td>
      <td style="text-align: right"><strong>0</strong></td>
      <td style="text-align: right"><strong>0</strong></td>
    </tr>
    <tr>
      <td style="text-align: right">3</td>
      <td>gpt-5.3-codex</td>
      <td style="text-align: right">8/12</td>
      <td style="text-align: right">4</td>
      <td style="text-align: right">2</td>
      <td style="text-align: right">6</td>
    </tr>
    <tr>
      <td style="text-align: right">4</td>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">8/12</td>
      <td style="text-align: right">3</td>
      <td style="text-align: right">1</td>
      <td style="text-align: right">4</td>
    </tr>
    <tr>
      <td style="text-align: right">4</td>
      <td>zai/glm-5</td>
      <td style="text-align: right">8/12</td>
      <td style="text-align: right">4</td>
      <td style="text-align: right">0</td>
      <td style="text-align: right">4</td>
    </tr>
    <tr>
      <td style="text-align: right">4</td>
      <td>qwen3.5-plus</td>
      <td style="text-align: right">8/12</td>
      <td style="text-align: right">3</td>
      <td style="text-align: right">1</td>
      <td style="text-align: right">4</td>
    </tr>
    <tr>
      <td style="text-align: right">7</td>
      <td>claude-haiku-4-5</td>
      <td style="text-align: right">7/12</td>
      <td style="text-align: right">4</td>
      <td style="text-align: right">1</td>
      <td style="text-align: right">5</td>
    </tr>
    <tr>
      <td style="text-align: right">8</td>
      <td>devstral-2512</td>
      <td style="text-align: right">5/12</td>
      <td style="text-align: right">4</td>
      <td style="text-align: right">4</td>
      <td style="text-align: right">8</td>
    </tr>
    <tr>
      <td style="text-align: right">9</td>
      <td>MiniMax-M2.5</td>
      <td style="text-align: right">4/12</td>
      <td style="text-align: right">9</td>
      <td style="text-align: right">1</td>
      <td style="text-align: right">10</td>
    </tr>
    <tr>
      <td style="text-align: right">10</td>
      <td>qwen3-coder-next</td>
      <td style="text-align: right">3/12</td>
      <td style="text-align: right">3</td>
      <td style="text-align: right">6</td>
      <td style="text-align: right">9</td>
    </tr>
  </tbody>
</table>

"Perfect lang" = all 10 parts solved on the first try with no retries.

"Failure incidents" counts retry and ejection events. It does **not** count every
subsequent part forfeited after an ejection.

---

### The two flawless models

`claude-opus-4-6` and `claude-sonnet-4-6` went **120 for 120**. Across Haskell, OCaml,
Python, Ruby, Elixir, Elm, Java, ReScript, F#, Rust, Clojure, and Racket, neither
model required a retry or was ejected.

| | opus | sonnet |
| --:| ----:| ------:|
| First-try rate | 120/120 | 120/120 |
| Typical time per part | 20–40s | 15–30s |
| Typical total cost per language | ~$1.00 | ~$0.42–$0.46 |
| Slowest single part | 84s (ReScript D5P1) | 239s (Elm D2P2) |

Both are flawless, but they get there differently. Opus is the steadier clock — no part
ever exceeds ~85 seconds. Sonnet occasionally spikes (154s on OCaml D2P2, 239s on Elm
D2P2) but is typically faster and has lower average cost.

**For this benchmark, these are the only two models with fully clean first-try results
across all 12 languages.**

---

### Language difficulty

How many models solved all 10 parts on the first try (no retries, no ejections):

| Language | Perfect first-try solvers (out of 10) |
| --------| :---:|
| Python | **10** |
| Ruby | **10** |
| Rust | 7 |
| Haskell | 7 |
| Java | 7 |
| Clojure | 5 |
| Racket | 6 |
| F# | 5 |
| Elm | 4 |
| Elixir | 4 |
| OCaml | 4 |
| ReScript (run 3) | 4 |

Python and Ruby are the only languages where every model solved every part on the first try.
OCaml and ReScript sit at the bottom — not because the puzzles were harder, but because
models struggle with less familiar toolchains and idioms. Elm's low count is surprising
given its 10/10 completion rate in the original post — many of those completions required
retries.

---

### Per-model breakdown

#### Where each model failed (retries or ejections)

<br>

**claude-opus-4-6** — *Nothing. Clean across all 12 languages.*

**claude-sonnet-4-6** — *Nothing. Clean across all 12 languages.*

**gpt-5.3-codex** — Ejected in Elixir (D3P1, no-progress loop behavior) and ReScript
(D2P1, no-progress behavior). Retries in Elm (D3P2, D4P1, D4P2) and F# (D1P2). On
successful runs, it is the most token-efficient model in this benchmark.

**kimi-coding/k2p5** — Ejected in OCaml (D1P2). Retries in Elm (D1P2), ReScript
(D1P2), Racket (D1P2). The cheapest model in the field ($0.02–$0.24 per language run),
with clean code when it works.

**zai/glm-5** — Never ejected in any language, but needed retries in Elixir (D1P2),
Java (D1P2), F# (D3P1), and Rust (D1P2). It is consistently slower than the leading
models, but completes reliably.

**qwen3.5-plus** — Ejected in OCaml (D1P2). Retries in Elm (D2P1), Rust (D1P2), and
Clojure (D3P2, where its first solution had an infinite loop that ran for 16 minutes
before being externally killed). The most verbose model: roughly 17K–103K tokens per
language run, with large spikes from false starts and rewrites.

**claude-haiku-4-5** — Ejected in Haskell (D1P2). Retries in Elixir (D1P2), ReScript
(D1P2), Clojure (D1P2), and Racket (D3P1). Fastest wall-clock time in many languages
(Ruby: 113s, Java: 142s, OCaml: 124s), but speed doesn't prevent its failures — they
all happen on the conceptual shift from Part 1 to Part 2.

**devstral-2512** — Ejected in Haskell (D1P2), OCaml (D1P2), Elixir (D1P1), and
ReScript (D1P2). Retries in Elm (D1P2, D3P1), F# (D1P2), and Clojure (D1P2). A
recurring pattern: fastest on Day 1 Part 1 in multiple languages, then fails on Part 2.
Excellent on mainstream languages (Python, Ruby), unreliable on FP languages.

**MiniMax-M2.5** — Ejected in OCaml (D1P2). **Nine retries** across seven languages
(Elixir, Elm ×2, Java, ReScript, F#, Clojure, Racket ×2). Only 4 of 12 languages solved
perfectly. Consistently 3–13× slower than the leaders — Haskell D3P1 took **1,078
seconds** (18 minutes) vs. 28s for sonnet. Gets there eventually, at enormous cost in
time and tokens.

**qwen3-coder-next** — Ejected in **six** languages (Haskell, OCaml, Elixir, Java,
Clojure, ReScript). Retries in F# (D1P2), Rust (D5P1), and Racket (D1P2). It is the
most frequently ejected model in this benchmark, with multiple no-progress and stale-
output incidents recorded in run logs.

---

### Code quality and cheating

I reviewed the actual implementations each model produced. Two findings stand out.

#### ReScript: raw JavaScript injection

ReScript compiles to JavaScript. Models that can't figure out ReScript syntax have an
escape hatch: `%raw()`, which lets you embed raw JavaScript inside a `.res` file.

In **ReScript run 2** (not counted in this recap's stats, but worth noting as a pattern):

- **kimi-coding/k2p5** wrapped entire solutions in `%raw()` — 3 of 7 solution files
  are pure JavaScript. `Day01.res` is 45 lines of `const fs = require('fs')`, `for`
  loops, and `parseInt` inside a single `%raw` block (i.e., JavaScript embedded in
  ReScript source).
- **qwen3-coder-next** wrote a plain `solve.js` file instead of a ReScript solution.
- **claude-opus-4-6** used `%raw(\`arr[i]\`)` for unsafe array access — a 1-line FFI
  escape hatch, not a full bypass. The rest of its code is idiomatic ReScript.

In **ReScript run 3** (counted in this recap), zero `%raw` usage across all models.
The system prompt teaching ReScript syntax eliminated the need to escape to JavaScript
entirely.

#### Token efficiency as a code quality proxy

Models that use fewer tokens tend to write cleaner, more focused code.
`gpt-5.3-codex` consistently produces the most concise solutions — 3,995 tokens for
all 10 Ruby parts, under 400 per part on average. Its Haskell code uses idiomatic
patterns (`interact`, `break`, proper type signatures).

At the other extreme, `qwen3.5-plus` and `MiniMax-M2.5` regularly produce roughly
20–103K tokens per language run. The code often works, but is generally verbose and
shows evidence of multiple discarded approaches within a single session.

---

### Efficiency comparison

Best models on each axis, across all 12 language runs:

| Metric | Winner | Typical value |
| ------| ------| ------------|
| Fastest wall-clock | claude-haiku-4-5 | 113s (Ruby), 142s (Java) |
| Fewest tokens | gpt-5.3-codex | 3,995 (Ruby) – 10,247 (Elm) |
| Cheapest | kimi-coding/k2p5 | $0.02 (Python) – $0.24 (ReScript) |
| Most reliable | claude-opus-4-6, claude-sonnet-4-6 | 120/120 first-try |
| Best value (reliability × cost) | claude-sonnet-4-6 | 120/120 at ~$0.42–$0.46/run |

---

### Mechanical-task responsiveness (timing-derived)

A second lens from timing data is perceived "snappiness" on simpler parts. I used:

- **D1P1 median time** (simple rotation/counting task)
- **D2P1 median time** (light parsing/counting task)
- **Mean token throughput** = output tokens / second on strict-clean language runs

This is a descriptive metric, not a quality score. High token throughput can indicate
fast generation, but also verbosity. Lower throughput can reflect concise output rather
than slow reasoning.

| Model | Strict-clean langs | D1P1 median | D2P1 median | Mean total time (clean langs) | Mean tokens/s |
| ------ | :---: | ---: | ---: | ---: | ---: |
| claude-haiku-4-5 | 7 | 12.5s | 17.0s | 214.3s | 84.6 |
| devstral-2512 | 5 | 19.0s | 23.0s | 301.4s | 80.5 |
| kimi-coding/k2p5 | 8 | 27.0s | 24.5s | 303.1s | 37.3 |
| gpt-5.3-codex | 8 | 29.5s | 23.0s | 232.9s | 27.6 |
| claude-sonnet-4-6 | 12 | 34.5s | 38.0s | 321.1s | 45.3 |
| claude-opus-4-6 | 12 | 35.0s | 47.5s | 312.8s | 40.9 |
| qwen3.5-plus | 9 | 42.0s | 45.0s | 734.1s | 65.5 |
| qwen3-coder-next | 4 | 52.0s | 30.5s | 536.0s | 55.7 |
| zai/glm-5 | 8 | 55.0s | 63.0s | 841.8s | 19.6 |
| MiniMax-M2.5 | 4 | 60.0s | 58.0s | 1392.5s | 30.6 |

Observed from this table:

- **Haiku** and **devstral** are often fast on low-complexity parts.
- **Codex** is fast and also comparatively concise (low tokens/s + low wall-clock).
- **MiniMax** is slow both on simple-part medians and total runtime.
- **qwen3.5-plus** and **qwen3-coder-next** can generate tokens quickly, but this does
  not translate to strong strict reliability.

### Patterns

**Day 1 Part 2 is the most common failure point.** Nearly every failure in the
benchmark happens at Day 1 Part 2. It requires a conceptual shift from Part 1, and this
is where weaker model runs most often fail.

**Speed does not predict reliability.** Haiku and devstral are often among the fastest
on individual parts but still get ejected in several language runs. Opus is not
consistently the fastest per part, but it stays reliable across all runs. Devstral also
shows a repeated pattern of strong D1P1 speed followed by D1P2 failures.

**Language familiarity maps to training data.** Python and Ruby: 10/10 perfect. OCaml
and ReScript: 4/10. This is consistent with differences in language prevalence in public
code corpora.

**Teaching the language works.** ReScript went from 1/10 completers (run 1) to 2/10
(run 2, with an overflow warning) to 7/10 (run 3, with a 150-line system prompt
covering syntax and stdlib). The system prompt didn't just help with one specific
trap — it helped models write correct algorithms in an unfamiliar language. In this
setting, explicit language references were more effective than short cautionary warnings.

**High token usage often indicates higher iteration overhead.** Token count is a useful
proxy for solution efficiency. Codex uses 4–7K tokens per run. MiniMax and qwen3.5-plus
can exceed 20K and in some runs go much higher. The extra tokens are typically linked to
failed approaches, compile errors, and rewrites.

---

### Practical 2026 selection for polyglot programmers

Using the strict rule in this recap (retry = failure), the following split is the most
practical way to choose models for day-to-day polyglot work.

#### Models to use or actively evaluate

| Model | Perfect langs (strict) | 2026 recommendation | Evidence from this benchmark |
| ------ | :---: | ------ | ------ |
| `claude-opus-4-6` | 12/12 | Primary reliability baseline | 120/120 first-try across all 12 languages |
| `claude-sonnet-4-6` | 12/12 | Primary default when balancing reliability and cost | Same reliability as Opus, with lower average cost |
| `gpt-5.3-codex` | 8/12 | Secondary tool for concise implementations | Best token efficiency; occasional no-progress incidents in Elixir/ReScript |
| `kimi-coding/k2p5` | 8/12 | Budget-oriented option | Lowest cost profile; one ejection and several retries |
| `zai/glm-5` | 8/12 | Completion-focused backup when latency is acceptable | No ejections; slower runtime and some retries |
| `qwen3.5-plus` | 8/12 | Optional, situational use | Mid-pack reliability with high token usage and retry spikes |
| `claude-haiku-4-5` | 7/12 | Fast-prototyping option, not strict-reliability default | Very fast in multiple languages, but more Part 2 failures |

#### Models to deprioritize for now

| Model | Perfect langs (strict) | Why low priority in this dataset |
| ------ | :---: | ------ |
| `devstral-2512` | 5/12 | Multiple ejections and retries, especially in FP-heavy runs |
| `MiniMax-M2.5` | 4/12 | Highest retry pressure and very high runtime variance |
| `qwen3-coder-next` | 3/12 | Most ejections and repeated no-progress/stale-output incidents |

This is a single-run benchmark snapshot. Re-evaluate as model versions and serving
infrastructure change.

---

### Methodology

The benchmark was driven by a custom prompt for
[pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent), a CLI coding
agent. The prompt turns pi into a benchmark controller that launches one pi agent per
model in separate tmux windows, feeds them puzzle descriptions, waits for completion,
collects answers, and handles ejections.

Each agent works in complete isolation — its own directory, no shared state, no awareness
of others. Extended thinking was configured as disabled (`--thinking off`). A 5-second
execution timeout prevented brute-force solutions. All agents ran under `nice -n 10` to
prevent CPU starvation with 10+ concurrent compilations.

One caveat: `--thinking off` is a request passed through provider/model adapters. It is
useful for consistency, but it does not guarantee identical internal reasoning behavior
across all providers or model backends.

These are single-run results, not averaged over multiple attempts. Wall-clock times are
influenced by inference platform load. The individual benchmark posts contain full
per-part timing, token counts, and cost breakdowns.

---

*Benchmarked between 2026-02-24 and 2026-02-27 using [pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent) as the agent harness.*

---

*This post was written with AI assistance.*
