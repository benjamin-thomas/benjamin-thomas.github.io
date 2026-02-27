+++
title = "Benchmarking a Local LLM on Advent of Code 2025 (Ollama)"
description = "Can a 14B-parameter local model solve AoC puzzles? Testing qwen2.5-coder:14b via Ollama on Day 1 in Python and Haskell — with up to 10 retries."

[taxonomies]
tags = ["Python", "Haskell", "AI", "Advent of Code", "Ollama"]
+++

The previous benchmarks in this series ([Haskell](@/posts/2026-02-24-aoc-2025-llm-benchmark-haskell.md),
[OCaml](@/posts/2026-02-25-aoc-2025-llm-benchmark-ocaml.md),
[Python](@/posts/2026-02-25-aoc-2025-llm-benchmark-python.md),
[ReScript](@/posts/2026-02-26-aoc-2025-llm-benchmark-rescript.md),
[Ruby](@/posts/2026-02-26-aoc-2025-llm-benchmark-ruby.md),
[Elixir](@/posts/2026-02-26-aoc-2025-llm-benchmark-elixir.md),
[Java](@/posts/2026-02-26-aoc-2025-llm-benchmark-java.md),
[Elm](@/posts/2026-02-26-aoc-2025-llm-benchmark-elm.md)) all used cloud API models — big,
frontier-class LLMs served by Anthropic, OpenAI, and others. But what about a **local
model**? Can a 14-billion-parameter model running on a single machine solve the same puzzles?

This post answers that question using **`qwen2.5-coder:14b`** via
[Ollama](https://ollama.com/), tested on AoC 2025 Day 1 in both Python and Haskell.

<!-- more -->

## The hardware

| | |
|-:|-:|
| Laptop | TUXEDO Pulse 14 Gen4 |
| CPU | AMD Ryzen 7 8845HS (8 cores / 16 threads, up to 5.1 GHz) |
| RAM | 26 GB DDR5 |
| GPU | AMD Radeon 780M (integrated — no dedicated GPU) |
| OS | TUXEDO OS 3 (Ubuntu-based), kernel 6.11 |

This is a general-purpose laptop — not a machine you'd pick for local AI inference.
No dedicated GPU means Ollama probably falls back to CPU, which makes generation obviously slow.

## The model

| | |
|-:|-:|
| Model | `qwen2.5-coder:14b` |
| Released | [November 2024](https://qwenlm.github.io/blog/qwen2.5-coder-family/) |
| Parameters | ~14B |
| Size on disk | ~9 GB |
| Runtime | Ollama 0.4.1 (CPU inference most likely) |
| Generation speed | Very slow (~40–90s per response) |

For comparison, the cloud models in previous benchmarks typically solve Day 1 in 10–50
seconds _total_ — including reading the puzzle, writing code, running it, verifying, and
producing the answer. The local model takes that long just to generate a single response.

## Why not use pi?

The first thing I tried was running the model through
[pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent), the same agent
harness used for all the other benchmarks. That failed immediately.

I assumed Ollama's OpenAI-compatible API would let pi drive the model the same way it drives
cloud models. It didn't work — instead of making actual tool calls, the model output
JSON-shaped text with placeholder values and immediately said "DONE" — without reading the
puzzle, writing any code, or running anything. I didn't investigate further.

```
{"name": "read", "arguments": {"path": "./PART_1.description"}}
{"name": "bash", "arguments": {"command": "timeout 5 python solution.py < ..."}}
{"name": "write", "arguments": {"path": "./ANSWER.txt", "content": "<paste the output here>"}}
DONE
```

Even if tool calls had worked, pi's background work (reading files, running commands) was
very slow through Ollama on this hardware. This ruled out using pi as-is and led me to a
completely different methodology.

## Methodology

Instead of having the local model use pi directly, I used raw Ollama CLI calls orchestrated by
a separate cloud-hosted pi instance acting as a manual agent loop:

1. **Write a prompt** containing the full puzzle description, example input, and expected output
2. **Send it to ollama** via `ollama run qwen2.5-coder:14b < prompt.txt`
3. **Extract the code** from the response (stripping markdown fences)
4. **Run it** against the example input, then the real input
5. **If wrong**: build a new prompt with the puzzle description + the actual error output, retry
6. **Up to 10 attempts** per part

Each Ollama call is **stateless** — the model has no memory of previous attempts. Every retry
includes the full puzzle context plus the error feedback from the previous attempt.

### Error feedback rules

The feedback given on retries was deliberately minimal — similar to what a human would see:

- **Compile/runtime error** → include the actual error output (traceback, compiler message)
- **Wrong answer on example** → "Your code outputs X but the expected answer is Y"
- **Wrong answer on real input** → "That's not the right answer"

No debugging hints, no solution suggestions, no explanation of _why_ the code was wrong.

### Timing

Each Ollama call was timed independently (wall-clock, generation only). The reported time is
for the **successful attempt** — the one that produced the correct answer. Total cumulative
time across all attempts is also noted.

### Key differences from the cloud benchmarks

| | Cloud benchmarks | This test |
|--:|:--:|:--:|
| Agent harness | pi (autonomous) | Manual loop (pi as orchestrator) |
| Tool use | Full (read, write, bash) | None — one-shot code generation |
| Self-correction | Model can run & debug its own code | Orchestrator runs code, sends error back |
| Memory | Full conversation context | Stateless (each attempt is fresh) |
| Retries | 3 max | 10 max |
| Concurrency | Up to 11 models in parallel | 1 model, sequential |

## Results

### Python

#### Day 1 Part 1 — Dial rotation counting

| Attempt | Time | Result | Issue |
| ------:| ----:| :----:| :-----|
| 1 | 62s | ✗ | Parsing bug |
| 2 | 48s | ✗ | Parsing bug |
| 3 | 34s | ✗ | Parsing bug |
| 4 | 50s | ✗ | Parsing bug |
| 5 | 45s | ✗ | Parsing bug |
| **6** | **41s** | **✓** | — |

<br>

#### Day 1 Part 2 — Counting zero-crossings during dial rotation

| Attempt | Time | Result | Issue |
| ------:| ----:| :----:| :-----|
| **1** | **59s** | **✓** | — |

<br>

### Haskell

#### Day 1 Part 1 — Dial rotation counting

| Attempt | Time | Result | Issue |
| ------:| ----:| :----:| :-----|
| 1 | 78s | ✗ | Compiled, ran, wrong answer — `normalize` only adds 100 once |
| 2 | 69s | ✗ | Type error: `Int` vs `String` |
| 3 | 48s | ✗ | Type error: `Char` vs `String` |
| 4 | 62s | ✗ | Non-exhaustive pattern match |
| **5** | **54s** | **✓** | Correct — used `mod` properly |

<br>

#### Day 1 Part 2 — Counting zero-crossings during dial rotation

| Attempt | Time | Result | Issue |
| ------:| ----:| :----:| :-----|
| 1 | 68s | ✗ | Wrong answer (5) — `iterate` includes start position |
| 2 | 44s | ✗ | Wrong answer (5) — same off-by-one |
| 3 | 60s | ✗ | Type error: variable not in scope |
| 4 | 61s | ✗ | Wrong answer (5) |
| 5 | 73s | ✗ | Type errors: wrong accumulator type in fold |
| 6 | 96s | ✗ | Same type error |
| 7 | 54s | ✗ | Wrong answer (5) — resets position to 50 each rotation |
| 8 | 62s | ✗ | Type error: `Int` vs `String` |
| 9 | 59s | ✗ | Shadowed `lines` function |
| **10** | **66s** | **✓** | Correct — on the very last attempt |

<br>

### Summary

<table>
  <thead>
    <tr>
      <th style="text-align: left"></th>
      <th style="text-align: right">D1P1</th>
      <th style="text-align: right">D1P2</th>
      <th style="text-align: right">Attempts</th>
      <th style="text-align: right">Total gen time</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Python</strong></td>
      <td style="text-align: right">✓ (6th try, 41s)</td>
      <td style="text-align: right">✓ (1st try, 59s)</td>
      <td style="text-align: right">7</td>
      <td style="text-align: right">~339s</td>
    </tr>
    <tr>
      <td><strong>Haskell</strong></td>
      <td style="text-align: right">✓ (5th try, 54s)</td>
      <td style="text-align: right">✓ (10th try, 66s)</td>
      <td style="text-align: right">15</td>
      <td style="text-align: right">~954s</td>
    </tr>
  </tbody>
</table>

<br>

## Observations

**The most visible weakness was input parsing.** In Python, the model kept making the same
parsing mistake for 5 attempts in a row, despite receiving the error output each time. It
took 6 attempts to find a correct approach.

**The algorithmic logic seemed mostly sound.** When the code compiled and parsed input correctly,
the core algorithm was often right. The Part 1 logic (modular arithmetic) and Part 2 logic
(click-by-click simulation) were correct in most attempts — the model just couldn't always wire
them up with correct parsing and types.

**Haskell was significantly harder.** 15 attempts vs. 7 for Python. The model struggled with
Haskell's type system — confusing `Char` with `String`, `Int` with `[Char]`, shadowing the
`lines` function, and getting accumulator types wrong in folds.

**Haskell Part 2 barely made it.** The model solved it on attempt 10 of 10. Four attempts
compiled and ran but produced the wrong answer (5 instead of 6) — a consistent off-by-one
error where `iterate` included the start position in the click list. Five attempts didn't
compile at all. One attempt out of ten got everything right.

**Python Part 2 worked on the first try.** First-try success on Part 2 — the part that ejected
4 of 11 cloud models in the Haskell benchmark and 5 of 9 in the OCaml benchmark.

**Cost: $0.** The entire benchmark cost nothing in API fees. The only cost is electricity
and patience. For a hobbyist or someone learning, being able to get _eventual_ correct answers
for free is meaningful — even if it takes 10 tries.

## Conclusion

A 14B local model **can** solve AoC Day 1 — but it needs patience. Where cloud models solve
both parts in under a minute with zero retries, `qwen2.5-coder:14b` needed 7 attempts for
Python and 15 for Haskell, with a total generation time of ~22 minutes.

Whether that's useful depends on your tolerance for iteration. At $0 per attempt, with a
local setup you control entirely, there's a case to be made — especially for easier puzzles
or languages the model handles well (Python >> Haskell).

*Benchmarked on 2026-02-27 using [Ollama](https://ollama.com/) 0.4.1 for local inference and
[pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent) as the
orchestrator.*

## Discussion

Join the conversation on the [Haskell Discourse](https://discourse.haskell.org/t/benchmarking-haskell-llm-proficiency-with-aoc-puzzles/13736/4).

---

*This post was written with AI assistance.*
