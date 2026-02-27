+++
title = "Benchmarking LLMs on Advent of Code 2025 (ReScript)"
description = "Three runs, three strategies: brute force, overflow warnings, and a ReScript system prompt. The completion rate went from 1/10 to 2/10 to 7/10. Teaching models the language was the biggest lever."

[taxonomies]
tags = ["ReScript", "AI", "Advent of Code"]
+++

Following up on [the Haskell benchmark](@/posts/2026-02-24-aoc-2025-llm-benchmark-haskell.md), [the OCaml
benchmark](@/posts/2026-02-25-aoc-2025-llm-benchmark-ocaml.md), and [the Python
benchmark](@/posts/2026-02-25-aoc-2025-llm-benchmark-python.md), I ran AoC 2025 Days 1–5 in
**ReScript** — a typed functional language that compiles to JavaScript with a lean
standard library, a distinct syntax, and very limited LLM training data.

This post covers three runs of the same benchmark, each adding a different intervention
to see what helps models cope with an unfamiliar language:

1. **Run 1** — no help at all. 3-minute timeout. 1 completer out of 10.
2. **Run 2** — overflow warning + longer timeout. 2 completers.
3. **Run 3** — a ReScript system prompt teaching syntax, stdlib, and types. **7 completers.**

<!-- more -->

## The contestants

Same 10 models across all three runs:

| # | Model |
| -:| ------:|
| 1 | `anthropic/claude-haiku-4-5` |
| 2 | `anthropic/claude-sonnet-4-6` |
| 3 | `anthropic/claude-opus-4-6` |
| 4 | `openai-codex/gpt-5.3-codex` |
| 5 | `zai/glm-5` |
| 6 | `minimax/MiniMax-M2.5` |
| 7 | `kimi-coding/k2p5` |
| 8 | `mistral/devstral-2512` |
| 9 | `alibaba/qwen3.5-plus` |
| 10 | `alibaba/qwen3-coder-next` |

---

# Run 2 — overflow warning + longer timeout

The first run was rough: 7 of 10 models ejected, `claude-haiku-4-5` the sole completer,
integer overflow the root cause of most failures. Two things changed for run 2:

1. **Overflow warning baked into every prompt.** ReScript's `int` type is 32 bits on the
   JavaScript runtime. Several puzzles produce answers in the tens of billions or hundreds
   of trillions — well beyond that ceiling. No warning was given in run 1. In run 2 every
   prompt includes an explicit note that large answers require `float` or `BigInt`.

2. **Timeout increased from 3 to 5 minutes per attempt.** ReScript project setup
   (initialising npm, configuring the build system, first compile) is non-trivial for
   models unfamiliar with the ecosystem. Three minutes left very little room for the actual
   solving.

## The rules (Run 2)

**Part 1** runs up to 3 attempts, each with a 5-minute window:

- Attempt 1: plain prompt + overflow warning
- Attempt 2 (on failure): "YOU MUST read `llm-small.txt` before starting"
- Attempt 3 (still failing): "YOU MUST read `llm-full.txt` before starting"
- Fail all three → ejected

The working directory contains two versions of the official ReScript `llms.txt`
documentation: a 5,578-line condensed version and a 14,405-line full API reference.
Models are not told about them on the first attempt.

**Part 2** gets exactly one attempt. Any failure — wrong answer, timeout, or API error —
means immediate ejection. No llms.txt hints.

API errors (quota limits, network failures) count as free retries and are not charged
against the attempt limit.

---

## Ejections (Run 2)

| Model | Ejected at | Reason |
| ------| ----------| ------|
| `mistral/devstral-2512` | D1P1 | Filled ~75% of its 200k context window with no answer |
| `openai-codex/gpt-5.3-codex` | D1P1 | Entered a loop of echoing prompts back as "DONE" without doing any work |
| `anthropic/claude-haiku-4-5` | D1P2 | Wrong answer |
| `anthropic/claude-sonnet-4-6` | D1P2 | Wrong answer |
| `zai/glm-5` | D1P2 | Wrong answer |
| `minimax/MiniMax-M2.5` | D1P2 | Wrong answer |
| `alibaba/qwen3-coder-next` | D2P1 | 40+ minutes in a compile loop, 45% of context consumed — ejected on excessive cost |
| `alibaba/qwen3.5-plus` | D5P2 | 32-bit integer overflow on the final puzzle |

**Two models completed all 10 parts:** `claude-opus-4-6` and `kimi-coding/k2p5`.

---

## Did the overflow warning make a difference?

Yes — but with an asterisk.

In run 1, both `claude-opus-4-6` and `claude-sonnet-4-6` overflowed on Day 5 Part 2 and
were ejected. In run 2, `opus` answered correctly and completed the benchmark. The warning
worked exactly as intended for it.

`alibaba/qwen3.5-plus` tells a more complicated story. In run 1 it timed out on Day 2
Part 1 and was ejected. In run 2 it sailed through Days 2, 3, and 4 — even detecting and
self-correcting an overflow mid-run on Day 2 Part 2. Then on Day 5 Part 2 it overflowed
anyway and was ejected. The warning helped it reach six extra puzzle parts; it wasn't
enough to protect it at the end.

The four models ejected on Day 1 Part 2 — `haiku`, `sonnet`, `glm-5`, `minimax` — gave
algorithmically wrong answers rather than overflow answers. The overflow warning had
nothing to do with their ejection. (In run 1, different models fell at Day 1 Part 2 —
it's a tricky boundary-condition puzzle that catches different models in different
sessions.)

---

## Results (Run 2)

### Day 1 Part 1 — Dial rotation counting

| Model | Time | Output tokens | Cost |
| ------| ----| ------| ----|
| `claude-opus-4-6` | 52s | 2,613 | $0.23 |
| `claude-sonnet-4-6` | 109s | 6,335 | $0.29 |
| `zai/glm-5` | 150s | 3,495 | $0.08 |
| `claude-haiku-4-5` | 183s | 16,079 | $0.32 |
| `alibaba/qwen3.5-plus` | 337s | 18,512 | $1.06 |
| `kimi-coding/k2p5` | 365s | 7,636 | $0.14 |
| `alibaba/qwen3-coder-next` | 894s | 54,900 | $6.47 |
| `minimax/MiniMax-M2.5` | 1,404s | 14,027 | $0.45 |
| `mistral/devstral-2512` | — | 50,158 | $3.46 | **EJECTED** (context full) |
| `openai-codex/gpt-5.3-codex` | — | 3,599 | $0.22 | **EJECTED** (brain-dead) |

All 8 surviving models passed on attempt 1 — nobody needed the llms.txt reference this
time. In run 1, three models only cleared Day 1 Part 1 by reading `llm-full.txt` on their
third attempt. The extra two minutes made the difference.

`mistral` consumed most of its 200k context window without producing an answer — a
different failure mode from run 1 (where it overflowed on every attempt), same outcome.

`gpt-5.3-codex` compiled a project, hit errors, then entered a loop of echoing each nudge
back and responding "DONE" without doing any work.

<br>

### Day 1 Part 2 — Counting zero-crossings during dial rotation

| Model | Time | Output tokens | Cost | Result |
| ------| ----| ------| ----| ------|
| `claude-opus-4-6` | 39s | 2,329 | $0.11 | ✓ |
| `kimi-coding/k2p5` | 92s | 682 | $0.02 | ✓ |
| `alibaba/qwen3.5-plus` | 108s | 8,560 | $0.16 | ✓ |
| `alibaba/qwen3-coder-next` | 247s | 14,616 | $1.09 | ✓ |
| `claude-sonnet-4-6` | 16s | 2,118 | $0.08 | ✗ wrong answer → **EJECTED** |
| `zai/glm-5` | 22s | 1,323 | $0.05 | ✗ wrong answer → **EJECTED** |
| `claude-haiku-4-5` | 46s | 5,253 | $0.15 | ✗ wrong answer → **EJECTED** |
| `minimax/MiniMax-M2.5` | 446s | 17,084 | $0.56 | ✗ wrong answer → **EJECTED** |

Day 1 Part 2 ejected four models in this run.
`k2p5` flipped from a wrong answer in run 1 to correct in run 2; the extra time appears
to have made the difference. `haiku`, which was run 1's sole winner, went out here.

<br>

### Day 2 Part 1 — Summing repeated-digit IDs in ranges

The puzzle answer is an 11-digit number — the first real overflow test.

| Model | Time | Output tokens | Cost | Result |
| ------| ----| ------| ----| ------|
| `claude-opus-4-6` | 142s | 6,918 | $0.47 | ✓ |
| `kimi-coding/k2p5` | 146s | 5,413 | $0.03 | ✓ |
| `alibaba/qwen3.5-plus` | 910s | 24,027 | $2.29 | ✓ |
| `alibaba/qwen3-coder-next` | >2,500s | 70,017 | $3.80 | ✗ **EJECTED** (cost/time) |

`qwen3.5-plus` passed where it timed out in run 1 — the overflow warning appears to have
steered it toward `float` arithmetic. Slow, but correct.

`qwen3-coder-next` spent over 40 minutes in a compile-debug loop and was ejected on cost
grounds. Its total across Days 1–2: $11.36.

<br>

### Day 2 Part 2 — Repeated-pattern IDs (any repeat count)

Another 11-digit answer.

| Model | Time | Output tokens | Cost |
| ------| ----| ------| ----|
| `claude-opus-4-6` | 33s | 2,126 | $0.13 |
| `alibaba/qwen3.5-plus` | 142s | 8,758 | $0.60 |
| `kimi-coding/k2p5` | 854s | 1,397 | $0.02 |

`qwen3.5-plus` detected an overflowed intermediate result mid-run, switched to `float`
arithmetic, and corrected itself — all within the same attempt.

<br>

### Day 3 Part 1 — Maximizing 2-digit joltage from battery banks

| Model | Time | Output tokens | Cost |
| ------| ----| ------| ----|
| `claude-opus-4-6` | 80s | 2,966 | $0.29 |
| `kimi-coding/k2p5` | 85s | 3,188 | $0.04 |
| `alibaba/qwen3.5-plus` | 847s | 24,097 | $1.32 |

<br>

### Day 3 Part 2 — Maximizing 12-digit joltage from battery banks

| Model | Time | Output tokens | Cost |
| ------| ----| ------| ----|
| `claude-opus-4-6` | 17s | 1,315 | $0.09 |
| `kimi-coding/k2p5` | 23s | 1,351 | $0.02 |
| `alibaba/qwen3.5-plus` | 155s | 3,478 | $0.26 |

The answer is a 15-digit number. All three passed.

<br>

### Day 4 Part 1 — Grid neighbour counting (accessible paper rolls)

| Model | Time | Output tokens | Cost |
| ------| ----| ------| ----|
| `claude-opus-4-6` | 59s | 2,770 | $0.26 |
| `kimi-coding/k2p5` | 64s | 3,544 | $0.03 |
| `alibaba/qwen3.5-plus` | 280s | 9,930 | $0.37 |

<br>

### Day 4 Part 2 — Iterative grid removal simulation

| Model | Time | Output tokens | Cost |
| ------| ----| ------| ----|
| `claude-opus-4-6` | 19s | 1,399 | $0.10 |
| `alibaba/qwen3.5-plus` | 65s | 2,878 | $0.20 |
| `kimi-coding/k2p5` | 79s | 4,193 | $0.06 |

<br>

### Day 5 Part 1 — Range membership checking

| Model | Time | Output tokens | Cost |
| ------| ----| ------| ----|
| `claude-opus-4-6` | 52s | 2,426 | $0.24 |
| `kimi-coding/k2p5` | 236s | 4,345 | $0.05 |
| `alibaba/qwen3.5-plus` | 400s | 18,712 | $1.29 |

<br>

### Day 5 Part 2 — Counting total fresh IDs from overlapping ranges

The answer is a 15-digit number — the final overflow test.

| Model | Time | Output tokens | Cost | Result |
| ------| ----| ------| ----| ------|
| `claude-opus-4-6` | 16s | 1,419 | $0.09 | ✓ **COMPLETE** |
| `kimi-coding/k2p5` | 71s | 1,798 | $0.03 | ✓ **COMPLETE** |
| `alibaba/qwen3.5-plus` | 215s | 11,300 | $0.96 | ✗ overflow → **EJECTED** |

`opus` answered in 16 seconds. In run 1, it overflowed the same puzzle. The overflow
warning was the difference.

`qwen3.5-plus` fell to the pattern it had avoided on Days 2 and 3 — despite the warning
and its earlier self-correction, it overflowed here and was ejected.

---

## Full summary (Run 2) — all 10 models

Wall-clock seconds. `✗` = ejected at that part.

<table>
  <thead>
    <tr>
      <th style="text-align: left">Model</th>
      <th style="text-align: right">D1P1</th>
      <th style="text-align: right">D1P2</th>
      <th style="text-align: right">D2P1</th>
      <th style="text-align: right">D2P2</th>
      <th style="text-align: right">D3P1</th>
      <th style="text-align: right">D3P2</th>
      <th style="text-align: right">D4P1</th>
      <th style="text-align: right">D4P2</th>
      <th style="text-align: right">D5P1</th>
      <th style="text-align: right">D5P2</th>
      <th style="text-align: right">Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>claude-opus-4-6</td>
      <td style="text-align: right">52</td>
      <td style="text-align: right">39</td>
      <td style="text-align: right">142</td>
      <td style="text-align: right">33</td>
      <td style="text-align: right">80</td>
      <td style="text-align: right">17</td>
      <td style="text-align: right">59</td>
      <td style="text-align: right">19</td>
      <td style="text-align: right">52</td>
      <td style="text-align: right">16</td>
      <td style="text-align: right"><strong>509s</strong></td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">365</td>
      <td style="text-align: right">92</td>
      <td style="text-align: right">146</td>
      <td style="text-align: right">854</td>
      <td style="text-align: right">85</td>
      <td style="text-align: right">23</td>
      <td style="text-align: right">64</td>
      <td style="text-align: right">79</td>
      <td style="text-align: right">236</td>
      <td style="text-align: right">71</td>
      <td style="text-align: right"><strong>2,015s</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">337</td>
      <td style="text-align: right">108</td>
      <td style="text-align: right">910</td>
      <td style="text-align: right">142</td>
      <td style="text-align: right">847</td>
      <td style="text-align: right">155</td>
      <td style="text-align: right">280</td>
      <td style="text-align: right">65</td>
      <td style="text-align: right">400</td>
      <td style="text-align: right">✗</td>
      <td style="text-align: right"><strong>DNF</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">894</td>
      <td style="text-align: right">247</td>
      <td style="text-align: right">✗</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right"><strong>DNF</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">1,404</td>
      <td style="text-align: right">✗</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right"><strong>DNF</strong></td>
    </tr>
    <tr>
      <td>claude-haiku-4-5</td>
      <td style="text-align: right">183</td>
      <td style="text-align: right">✗</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right"><strong>DNF</strong></td>
    </tr>
    <tr>
      <td>claude-sonnet-4-6</td>
      <td style="text-align: right">109</td>
      <td style="text-align: right">✗</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right"><strong>DNF</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">150</td>
      <td style="text-align: right">✗</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right"><strong>DNF</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">✗</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right"><strong>DNF</strong></td>
    </tr>
    <tr>
      <td>openai-codex/gpt-5.3-codex</td>
      <td style="text-align: right">✗</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right"><strong>DNF</strong></td>
    </tr>
  </tbody>
</table>

<br>

Token and cost breakdown for the completers and qwen3.5-plus. *Costs are rough
approximations based on published per-token pricing. I use subscription plans, so my
actual spending is capped regardless.*

<table>
  <thead>
    <tr>
      <th style="text-align: left">Model</th>
      <th style="text-align: right">D1P1</th>
      <th style="text-align: right">D1P2</th>
      <th style="text-align: right">D2P1</th>
      <th style="text-align: right">D2P2</th>
      <th style="text-align: right">D3P1</th>
      <th style="text-align: right">D3P2</th>
      <th style="text-align: right">D4P1</th>
      <th style="text-align: right">D4P2</th>
      <th style="text-align: right">D5P1</th>
      <th style="text-align: right">D5P2</th>
      <th style="text-align: right">Total tokens</th>
      <th style="text-align: right">Total cost</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>claude-opus-4-6</td>
      <td style="text-align: right">2,613</td>
      <td style="text-align: right">2,329</td>
      <td style="text-align: right">6,918</td>
      <td style="text-align: right">2,126</td>
      <td style="text-align: right">2,966</td>
      <td style="text-align: right">1,315</td>
      <td style="text-align: right">2,770</td>
      <td style="text-align: right">1,399</td>
      <td style="text-align: right">2,426</td>
      <td style="text-align: right">1,419</td>
      <td style="text-align: right"><strong>26,281</strong></td>
      <td style="text-align: right"><strong>$2.01</strong></td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">7,636</td>
      <td style="text-align: right">682</td>
      <td style="text-align: right">5,413</td>
      <td style="text-align: right">1,397</td>
      <td style="text-align: right">3,188</td>
      <td style="text-align: right">1,351</td>
      <td style="text-align: right">3,544</td>
      <td style="text-align: right">4,193</td>
      <td style="text-align: right">4,345</td>
      <td style="text-align: right">1,798</td>
      <td style="text-align: right"><strong>33,547</strong></td>
      <td style="text-align: right"><strong>$0.46</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus †</td>
      <td style="text-align: right">18,512</td>
      <td style="text-align: right">8,560</td>
      <td style="text-align: right">24,027</td>
      <td style="text-align: right">8,758</td>
      <td style="text-align: right">24,097</td>
      <td style="text-align: right">3,478</td>
      <td style="text-align: right">9,930</td>
      <td style="text-align: right">2,878</td>
      <td style="text-align: right">18,712</td>
      <td style="text-align: right">11,300</td>
      <td style="text-align: right"><strong>130,252</strong></td>
      <td style="text-align: right"><strong>$8.49</strong></td>
    </tr>
  </tbody>
</table>

† ejected on D5P2; D5P2 cost includes the final wrong attempt.

---

## Run 1 vs Run 2

| | Run 1 | Run 2 |
| --| ------| ------|
| Timeout per attempt | 3 min | 5 min |
| Overflow warning in prompt | ✗ | ✓ |
| Full completers | 1 (`claude-haiku-4-5`) | 2 (`claude-opus-4-6`, `kimi-coding/k2p5`) |
| `claude-opus-4-6` on D5P2 | ✗ overflow | ✓ |
| `kimi-coding/k2p5` overall | ejected D1P2 | all 10 parts ✓ |
| Session cost data | partial (Day 5 only for finalists) | complete |

The overflow warning made a real difference for `opus`. The longer timeout saved `k2p5`.
But six models out of ten still couldn't produce correct answers even with those helps.
The bottleneck wasn't overflow — it was the language itself.

---

# Run 3 — ReScript system prompt

Run 2 left an obvious question: if the problem is unfamiliarity with ReScript, what
happens when you *teach* the model the language?

For run 3 I wrote a concise ReScript system prompt — roughly 150 lines covering project
setup, syntax essentials, the type system (including the fact that `int` is 32-bit and
`bigint` exists), common stdlib functions, and file I/O patterns.

### How it was injected

The agent harness ([pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent))
supports `--append-system-prompt`, which adds content to the default system prompt
without replacing it. Each model was launched with:

```bash
pi --model <model> --thinking off \
   --append-system-prompt rescript-system-prompt.md \
   --session-dir . \
   '<puzzle prompt>'
```

This means every model saw pi's standard coding-agent instructions *plus* the ReScript
reference below, before receiving the puzzle. No other hints — no overflow warning, no
llms.txt documentation files.

### The system prompt

<details>
<summary>Click to expand the full system prompt (rescript-system-prompt.md)</summary>

````markdown
## ReScript v12

ReScript is a typed functional language that compiles to JavaScript.
Think of it as **functional TypeScript** — if you can solve a problem in TypeScript,
you can solve it in ReScript using the same logic, just with different syntax.

### Project setup

**package.json**:
```json
{ "name": "my-project", "dependencies": { "rescript": "^12.1.0" } }
```

**rescript.json** (NOT bsconfig.json):
```json
{
  "name": "my-project",
  "sources": [{ "dir": "src", "subdirs": true }],
  "package-specs": [{ "module": "esmodule", "in-source": true }],
  "suffix": ".res.js"
}
```

Then: `npm install && npx rescript && node src/MyModule.res.js`

### Syntax essentials

```rescript
// Pipe operator (not |>)
[1, 2, 3]->Array.map(x => x * 2)->Array.filter(x => x > 2)

// Let bindings, no semicolons needed
let x = 42
let greet = (name) => "Hello " ++ name  // ++ for string concat

// Pattern matching
switch myValue {
| Some(x) => Console.log(x)
| None => Console.log("nothing")
}

// String operations
let lines = text->String.split("\n")
let trimmed = line->String.trim
let parts = line->String.split(",")
```

### Type system

```rescript
// Primitive types
let n: int = 42              // 32-bit signed integer
let f: float = 3.14          // 64-bit IEEE 754
let b: bigint = 99999999999n // arbitrary precision
let s: string = "hello"      // UTF-8 string
let c: char = 'a'            // single byte, no Unicode — prefer string
let ok: bool = true

// Float arithmetic uses distinct operators
let sum = 1.0 +. 2.5         // +.  -.  *.  /.
let converted = Int.toFloat(n)

// Modulo is a function call, not an infix operator
mod(7, 3)             // int modulo — NOT 7 mod 3, NOT 7 % 3
Float.mod(7.0, 3.0)  // float modulo

// Mutable values use ref
let counter = ref(0)
counter := counter.contents + 1  // := to set, .contents to read

// Records
type point = { x: float, y: float }
let p = { x: 1.0, y: 2.0 }

// Variants
type shape = Circle(float) | Rect(float, float)

// Option and Result
let found: option<int> = Some(42)
let parsed: result<int, string> = Ok(42)

// Arrays — main ordered data structure (like JS arrays)
let a = ["hello", "world"]
let first = a[0]              // Some("hello") — access returns option!
a[0] = "hey"                  // mutation
let b = [1, 2, ...a]          // spread

// List — immutable singly linked list
let l = list{1, 2, 3}
let l2 = list{0, ...l}        // prepend
```

### File I/O (Node.js bindings)

```rescript
@module("fs") external readFileSync: (string, string) => string = "readFileSync"

let content = readFileSync("input.txt", "utf8")
```

### Common stdlib

```rescript
// String
String.length: string => int
String.get: (string, int) => option<string>    // None if out of bounds
String.charAt: (string, int) => string        // "" if out of bounds
String.slice: (string, ~start: int, ~end: int=?) => string
String.split: (string, string) => array<string>
String.trim: string => string
String.includes: (string, string) => bool
String.startsWith: (string, string) => bool
String.replaceAll: (string, string, string) => string
String.make: 'a => string               // convert anything to string

// Array
Array.map: (array<'a>, 'a => 'b) => array<'b>
Array.filter: (array<'a>, 'a => bool) => array<'a>
Array.reduce: (array<'a>, 'b, ('b, 'a) => 'b) => 'b
Array.forEach: (array<'a>, 'a => unit) => unit
Array.length: array<'a> => int
Array.get: (array<'a>, int) => option<'a>

// Option — use getOrThrow, NOT getExn (deprecated)
Option.getOrThrow: (option<'a>, ~message: string=?) => 'a  // throws if None
Option.getOr: (option<'a>, 'a) => 'a           // default if None
Option.map: (option<'a>, 'a => 'b) => option<'b>
Option.flatMap: (option<'a>, 'a => option<'b>) => option<'b>
Option.isSome: option<'a> => bool
Option.isNone: option<'a> => bool
Option.forEach: (option<'a>, 'a => unit) => unit

// Result — use getOrThrow, NOT getExn (deprecated)
Result.getOrThrow: (result<'a, 'b>, ~message: string=?) => 'a  // throws if Error
Result.getOr: (result<'a, 'b>, 'a) => 'a
Result.map: (result<'a, 'c>, 'a => 'b) => result<'b, 'c>
Result.isOk: result<'a, 'b> => bool
Result.isError: result<'a, 'b> => bool

// Conversions
Int.fromString: (string, ~radix: int=?) => option<int>
Int.toString: (int, ~radix: int=?) => string
Int.toFloat: int => float
Float.fromString: string => option<float>
Float.toString: (float, ~radix: int=?) => string

// Output
Console.log: 'a => unit
Console.log2: ('a, 'b) => unit
```
````

</details>

## The rules (Run 3)

Same retry logic as run 2 (up to 3 attempts on wrong answers), but:

- **No overflow warning** in the puzzle prompt — the system prompt documents `int` as
  32-bit and `bigint` as arbitrary precision; models have to connect those dots themselves.
- **No llms.txt escalation** — models either know enough from the system prompt or they
  don't.
- **15-minute timeout** per part (increased from the polling window, not per-attempt).

---

## Ejections (Run 3)

| Model | Ejected at | Reason |
| ------| ----------| ------|
| `mistral/devstral-2512` | D1P2 | Wrong answer on all 3 attempts |
| `openai-codex/gpt-5.3-codex` | D2P1 | Brain-dead — echoed prompts as "DONE" without working |
| `alibaba/qwen3-coder-next` | D5P1 | Brain-dead — froze mid-sentence after dumping the input file |

**Seven models completed all 10 parts.**

---

## Results (Run 3)

### Day 1 Part 1 — Dial rotation counting

| Model | Time | Output tokens | Cost |
| ------| ----| ------| ----|
| `alibaba/qwen3.5-plus` | 49s | 1,350 | $0.02 |
| `anthropic/claude-haiku-4-5` | 59s | 2,256 | $0.03 |
| `mistral/devstral-2512` | 59s | 1,488 | $0.03 |
| `openai-codex/gpt-5.3-codex` | 62s | 899 | $0.04 |
| `anthropic/claude-sonnet-4-6` | 68s | 1,915 | $0.08 |
| `anthropic/claude-opus-4-6` | 69s | 1,722 | $0.13 |
| `kimi-coding/k2p5` | 73s | 1,118 | $0.03 |
| `minimax/MiniMax-M2.5` | 120s | 2,728 | $0.06 |
| `alibaba/qwen3-coder-next` | 122s | 3,905 | $0.22 |
| `zai/glm-5` | 133s | 1,515 | $0.04 |

**10/10 correct on first attempt.** In run 2, two models were ejected here (`devstral`
for filling its context window, `codex` for going brain-dead). The system prompt got
them through.

<br>

### Day 1 Part 2 — Counting zero-crossings during dial rotation

| Model | Time | Output tokens | Cost | Result |
| ------| ----| ------| ----| ------|
| `openai-codex/gpt-5.3-codex` | 26s | 752 | $0.02 | ✓ |
| `anthropic/claude-sonnet-4-6` | 39s | 1,559 | $0.05 | ✓ |
| `anthropic/claude-opus-4-6` | 46s | 1,809 | $0.09 | ✓ |
| `zai/glm-5` | 65s | 1,244 | $0.03 | ✓ |
| `alibaba/qwen3.5-plus` | 90s | 9,100 | $0.04 | ✓ |
| `anthropic/claude-haiku-4-5` | 327s | 11,607 | $0.13 | ✓ (2nd try) |
| `alibaba/qwen3-coder-next` | 330s | 9,936 | $0.29 | ✓ (2nd try) |
| `kimi-coding/k2p5` | 335s | 2,078 | $0.05 | ✓ (2nd try) |
| `minimax/MiniMax-M2.5` | 615s | 19,746 | $0.22 | ✓ (2nd try) |
| `mistral/devstral-2512` | — | 24,404 | $0.58 | ✗ wrong 3/3 → **EJECTED** |

**9/10 survived.** In run 2, this puzzle ejected four models (`sonnet`, `haiku`, `glm-5`,
`minimax`). With the system prompt, all four completed it. Only `devstral` couldn't
solve it — it gave three different wrong answers across three
attempts, each algorithmically different but each wrong.

<br>

### Day 2 Part 1 — Summing repeated-digit IDs in ranges

The puzzle answer is an 11-digit number — the first real overflow test.

| Model | Time | Output tokens | Cost |
| ------| ----| ------| ----|
| `anthropic/claude-haiku-4-5` | 50s | 4,585 | $0.05 |
| `kimi-coding/k2p5` | 65s | 2,201 | $0.01 |
| `anthropic/claude-opus-4-6` | 70s | 2,680 | $0.16 |
| `anthropic/claude-sonnet-4-6` | 71s | 3,349 | $0.12 |
| `minimax/MiniMax-M2.5` | 210s | 5,421 | $0.06 |
| `alibaba/qwen3-coder-next` | 226s | 9,925 | $0.38 |
| `zai/glm-5` | 580s | 11,880 | $0.17 |
| `alibaba/qwen3.5-plus` | 840s | 29,837 | $1.06 |
| `openai-codex/gpt-5.3-codex` | — | 1,987 | $0.11 | ✗ brain-dead → **EJECTED** |

**8/8 surviving models correct on first try.** `codex` compiled a solution but it timed
out on even the example input. After two dirty-stop retries it went brain-dead — echoing
nudges and saying "DONE" without doing any work.

<br>

### Day 2 Part 2 — Repeated-pattern IDs (any repeat count)

Another 11-digit answer.

| Model | Time | Output tokens | Cost |
| ------| ----| ------| ----|
| `anthropic/claude-haiku-4-5` | 18s | 1,104 | $0.02 |
| `anthropic/claude-sonnet-4-6` | 54s | 2,935 | $0.08 |
| `anthropic/claude-opus-4-6` | 54s | 2,713 | $0.12 |
| `kimi-coding/k2p5` | 68s | 1,109 | $0.01 |
| `minimax/MiniMax-M2.5` | 75s | 2,912 | $0.04 |
| `zai/glm-5` | 338s | 6,442 | $0.14 |
| `alibaba/qwen3-coder-next` | 365s | 13,194 | $0.51 |
| `alibaba/qwen3.5-plus` | 394s | 15,365 | $1.20 |

All 8 correct. `haiku` was fastest at 18 seconds.

<br>

### Day 3 Part 1 — Maximizing 2-digit joltage from battery banks

| Model | Time | Output tokens | Cost |
| ------| ----| ------| ----|
| `anthropic/claude-sonnet-4-6` | 39s | 1,370 | $0.06 |
| `alibaba/qwen3.5-plus` | 50s | 2,648 | $0.03 |
| `anthropic/claude-opus-4-6` | 57s | 1,697 | $0.12 |
| `anthropic/claude-haiku-4-5` | 62s | 5,251 | $0.06 |
| `minimax/MiniMax-M2.5` | 127s | 3,704 | $0.05 |
| `alibaba/qwen3-coder-next` | 158s | 5,835 | $0.40 |
| `zai/glm-5` | 291s | 5,600 | $0.11 |
| `kimi-coding/k2p5` | 299s | 1,865 | $0.03 |

<br>

### Day 3 Part 2 — Maximizing 12-digit joltage from battery banks

The answer is a 15-digit number.

| Model | Time | Output tokens | Cost |
| ------| ----| ------| ----|
| `kimi-coding/k2p5` | 31s | 937 | $0.01 |
| `anthropic/claude-opus-4-6` | 34s | 1,252 | $0.07 |
| `anthropic/claude-sonnet-4-6` | 44s | 2,013 | $0.08 |
| `zai/glm-5` | 106s | 1,978 | $0.06 |
| `minimax/MiniMax-M2.5` | 110s | 3,173 | $0.09 |
| `anthropic/claude-haiku-4-5` | 144s | 14,461 | $0.17 |
| `alibaba/qwen3-coder-next` | 248s | 4,409 | $0.47 |
| `alibaba/qwen3.5-plus` | 265s | 10,304 | $0.23 |

All 8 correct. All handled the 15-digit answer — no overflow.

<br>

### Day 4 Part 1 — Grid neighbour counting (accessible paper rolls)

| Model | Time | Output tokens | Cost |
| ------| ----| ------| ----|
| `anthropic/claude-sonnet-4-6` | 33s | 1,307 | $0.05 |
| `kimi-coding/k2p5` | 33s | 974 | $0.01 |
| `anthropic/claude-haiku-4-5` | 44s | 3,673 | $0.05 |
| `anthropic/claude-opus-4-6` | 44s | 1,409 | $0.11 |
| `minimax/MiniMax-M2.5` | 89s | 2,759 | $0.03 |
| `alibaba/qwen3.5-plus` | 147s | 6,383 | $0.11 |
| `zai/glm-5` | 162s | 2,968 | $0.04 |
| `alibaba/qwen3-coder-next` | 769s | 19,731 | $0.73 |

<br>

### Day 4 Part 2 — Iterative grid removal simulation

| Model | Time | Output tokens | Cost |
| ------| ----| ------| ----|
| `anthropic/claude-opus-4-6` | 22s | 1,320 | $0.08 |
| `anthropic/claude-sonnet-4-6` | 24s | 1,243 | $0.04 |
| `anthropic/claude-haiku-4-5` | 25s | 2,423 | $0.03 |
| `kimi-coding/k2p5` | 28s | 1,340 | $0.02 |
| `alibaba/qwen3.5-plus` | 65s | 3,829 | $0.12 |
| `alibaba/qwen3-coder-next` | 213s | 4,696 | $0.29 |
| `zai/glm-5` | 221s | 3,976 | $0.09 |
| `minimax/MiniMax-M2.5` | 237s | 7,399 | $0.12 |

<br>

### Day 5 Part 1 — Range membership checking

| Model | Time | Output tokens | Cost |
| ------| ----| ------| ----|
| `anthropic/claude-sonnet-4-6` | 67s | 2,632 | $0.10 |
| `kimi-coding/k2p5` | 74s | 3,287 | $0.03 |
| `anthropic/claude-haiku-4-5` | 82s | 7,079 | $0.09 |
| `anthropic/claude-opus-4-6` | 84s | 3,399 | $0.22 |
| `alibaba/qwen3.5-plus` | 172s | 8,297 | $0.09 |
| `minimax/MiniMax-M2.5` | 293s | 8,600 | $0.27 |
| `zai/glm-5` | 361s | 6,021 | $0.23 |
| `alibaba/qwen3-coder-next` | — | 160 | $0.01 | ✗ brain-dead → **EJECTED** |

`qwen3-coder-next` read the real input file, dumped it into the context, started writing
"I understand the problem now. The task is to: 1. Parse Ingredi—" and froze mid-sentence.
No recovery.

<br>

### Day 5 Part 2 — Counting total fresh IDs from overlapping ranges

The answer is a 15-digit number — the final overflow test.

| Model | Time | Output tokens | Cost | Result |
| ------| ----| ------| ----| ------|
| `anthropic/claude-sonnet-4-6` | 25s | 1,360 | $0.06 | ✓ **COMPLETE** |
| `anthropic/claude-opus-4-6` | 31s | 1,269 | $0.10 | ✓ **COMPLETE** |
| `kimi-coding/k2p5` | 73s | 4,663 | $0.04 | ✓ **COMPLETE** |
| `anthropic/claude-haiku-4-5` | 76s | 7,877 | $0.11 | ✓ **COMPLETE** |
| `zai/glm-5` | 171s | 3,382 | $0.15 | ✓ **COMPLETE** |
| `minimax/MiniMax-M2.5` | 211s | 6,854 | $0.34 | ✓ **COMPLETE** |
| `alibaba/qwen3.5-plus` | 551s | 15,764 | $0.60 | ✓ **COMPLETE** |

**Seven out of seven.** In run 2, `qwen3.5-plus` overflowed this exact puzzle. With
the system prompt documenting that `int` is 32-bit and `bigint` exists, it used `bigint`
from the start and answered correctly. No explicit warning needed.

---

## Full summary (Run 3) — all 10 models

Wall-clock seconds. `✗` = ejected at that part.

<table>
  <thead>
    <tr>
      <th style="text-align: left">Model</th>
      <th style="text-align: right">D1P1</th>
      <th style="text-align: right">D1P2</th>
      <th style="text-align: right">D2P1</th>
      <th style="text-align: right">D2P2</th>
      <th style="text-align: right">D3P1</th>
      <th style="text-align: right">D3P2</th>
      <th style="text-align: right">D4P1</th>
      <th style="text-align: right">D4P2</th>
      <th style="text-align: right">D5P1</th>
      <th style="text-align: right">D5P2</th>
      <th style="text-align: right">Total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>claude-sonnet-4-6</td>
      <td style="text-align: right">68</td>
      <td style="text-align: right">39</td>
      <td style="text-align: right">71</td>
      <td style="text-align: right">54</td>
      <td style="text-align: right">39</td>
      <td style="text-align: right">44</td>
      <td style="text-align: right">33</td>
      <td style="text-align: right">24</td>
      <td style="text-align: right">67</td>
      <td style="text-align: right">25</td>
      <td style="text-align: right"><strong>464s</strong></td>
    </tr>
    <tr>
      <td>claude-opus-4-6</td>
      <td style="text-align: right">69</td>
      <td style="text-align: right">46</td>
      <td style="text-align: right">70</td>
      <td style="text-align: right">54</td>
      <td style="text-align: right">57</td>
      <td style="text-align: right">34</td>
      <td style="text-align: right">44</td>
      <td style="text-align: right">22</td>
      <td style="text-align: right">84</td>
      <td style="text-align: right">31</td>
      <td style="text-align: right"><strong>511s</strong></td>
    </tr>
    <tr>
      <td>claude-haiku-4-5</td>
      <td style="text-align: right">59</td>
      <td style="text-align: right">327</td>
      <td style="text-align: right">50</td>
      <td style="text-align: right">18</td>
      <td style="text-align: right">62</td>
      <td style="text-align: right">144</td>
      <td style="text-align: right">44</td>
      <td style="text-align: right">25</td>
      <td style="text-align: right">82</td>
      <td style="text-align: right">76</td>
      <td style="text-align: right"><strong>887s</strong></td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">73</td>
      <td style="text-align: right">335</td>
      <td style="text-align: right">65</td>
      <td style="text-align: right">68</td>
      <td style="text-align: right">299</td>
      <td style="text-align: right">31</td>
      <td style="text-align: right">33</td>
      <td style="text-align: right">28</td>
      <td style="text-align: right">74</td>
      <td style="text-align: right">73</td>
      <td style="text-align: right"><strong>1,079s</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">120</td>
      <td style="text-align: right">615</td>
      <td style="text-align: right">210</td>
      <td style="text-align: right">75</td>
      <td style="text-align: right">127</td>
      <td style="text-align: right">110</td>
      <td style="text-align: right">89</td>
      <td style="text-align: right">237</td>
      <td style="text-align: right">293</td>
      <td style="text-align: right">211</td>
      <td style="text-align: right"><strong>2,087s</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">133</td>
      <td style="text-align: right">65</td>
      <td style="text-align: right">580</td>
      <td style="text-align: right">338</td>
      <td style="text-align: right">291</td>
      <td style="text-align: right">106</td>
      <td style="text-align: right">162</td>
      <td style="text-align: right">221</td>
      <td style="text-align: right">361</td>
      <td style="text-align: right">171</td>
      <td style="text-align: right"><strong>2,428s</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">49</td>
      <td style="text-align: right">90</td>
      <td style="text-align: right">840</td>
      <td style="text-align: right">394</td>
      <td style="text-align: right">50</td>
      <td style="text-align: right">265</td>
      <td style="text-align: right">147</td>
      <td style="text-align: right">65</td>
      <td style="text-align: right">172</td>
      <td style="text-align: right">551</td>
      <td style="text-align: right"><strong>2,623s</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">122</td>
      <td style="text-align: right">330</td>
      <td style="text-align: right">226</td>
      <td style="text-align: right">365</td>
      <td style="text-align: right">158</td>
      <td style="text-align: right">248</td>
      <td style="text-align: right">769</td>
      <td style="text-align: right">213</td>
      <td style="text-align: right">✗</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right"><strong>DNF</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">59</td>
      <td style="text-align: right">✗</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right"><strong>DNF</strong></td>
    </tr>
    <tr>
      <td>openai-codex/gpt-5.3-codex</td>
      <td style="text-align: right">62</td>
      <td style="text-align: right">26</td>
      <td style="text-align: right">✗</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right"><strong>DNF</strong></td>
    </tr>
  </tbody>
</table>

<br>

Token and cost breakdown for all models. *Costs are rough approximations based on
published per-token pricing. I use subscription plans, so my actual spending is capped
regardless.*

<table>
  <thead>
    <tr>
      <th style="text-align: left">Model</th>
      <th style="text-align: right">Total tokens</th>
      <th style="text-align: right">Total cost</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right"><strong>102,877</strong></td>
      <td style="text-align: right"><strong>$3.50</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right"><strong>63,296</strong></td>
      <td style="text-align: right"><strong>$1.28</strong></td>
    </tr>
    <tr>
      <td>claude-opus-4-6</td>
      <td style="text-align: right"><strong>19,270</strong></td>
      <td style="text-align: right"><strong>$1.20</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right"><strong>45,006</strong></td>
      <td style="text-align: right"><strong>$1.06</strong></td>
    </tr>
    <tr>
      <td>claude-haiku-4-5</td>
      <td style="text-align: right"><strong>60,316</strong></td>
      <td style="text-align: right"><strong>$0.74</strong></td>
    </tr>
    <tr>
      <td>claude-sonnet-4-6</td>
      <td style="text-align: right"><strong>19,683</strong></td>
      <td style="text-align: right"><strong>$0.72</strong></td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right"><strong>19,572</strong></td>
      <td style="text-align: right"><strong>$0.24</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next †</td>
      <td style="text-align: right"><strong>71,791</strong></td>
      <td style="text-align: right"><strong>$3.30</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512 †</td>
      <td style="text-align: right"><strong>25,892</strong></td>
      <td style="text-align: right"><strong>$0.61</strong></td>
    </tr>
    <tr>
      <td>openai-codex/gpt-5.3-codex †</td>
      <td style="text-align: right"><strong>3,638</strong></td>
      <td style="text-align: right"><strong>$0.17</strong></td>
    </tr>
  </tbody>
</table>

† ejected before completing all parts.

---

## Across all three runs

| | Run 1 | Run 2 | Run 3 |
| --| ------| ------| ------|
| Intervention | none | overflow warning | system prompt |
| Timeout | 3 min | 5 min | 15 min |
| Full completers | 1/10 | 2/10 | **7/10** |
| D1P1 first-try pass rate | 7/10 | 8/10 | **10/10** |
| D1P2 survivors | 3/10 | 4/10 | **9/10** |
| `claude-opus-4-6` | ejected D5P2 | ✓ all 10 | ✓ all 10 |
| `claude-sonnet-4-6` | ejected D1P2 | ejected D1P2 | **✓ fastest (464s)** |
| `claude-haiku-4-5` | ✓ sole completer | ejected D1P2 | **✓ all 10** |
| `kimi-coding/k2p5` | ejected D1P2 | ✓ all 10 | ✓ all 10 |
| `zai/glm-5` | ejected D1P2 | ejected D1P2 | **✓ all 10** |
| `minimax/MiniMax-M2.5` | ejected D1P2 | ejected D1P2 | **✓ all 10** |
| `alibaba/qwen3.5-plus` | ejected D2P1 | ejected D5P2 | **✓ all 10** |
| `alibaba/qwen3-coder-next` | ejected D1P2 | ejected D2P1 | ejected D5P1 |
| `mistral/devstral-2512` | ejected D1P1 | ejected D1P1 | ejected D1P2 |
| `openai-codex/gpt-5.3-codex` | ejected D1P1 | ejected D1P1 | ejected D2P1 |

---

## Observations

**Teaching the language was the biggest lever.** The system prompt — 150 lines of
syntax, types, and stdlib — took the completion rate from 2/10 to 7/10. The overflow
warning in run 2 helped exactly one model (`opus`). The system prompt helped *five
more* (`sonnet`, `haiku`, `glm-5`, `minimax`, `qwen3.5-plus`).

**The overflow problem was a documentation problem.** In run 2, `qwen3.5-plus`
overflowed on Day 5 Part 2 despite an explicit overflow warning. In run 3, it used
`bigint` from the start and answered correctly — because the system prompt documented
`int` as 32-bit and `bigint` as arbitrary precision. Models don't need warnings; they
need language specs.

**`claude-sonnet-4-6` went from run 2's Day 1 Part 2 casualty to run 3's fastest
completer (464s).** In run 2 it gave a wrong answer on the boundary-condition puzzle
and was ejected. In run 3 it completed all 10 parts and beat `opus` on total time. The
system prompt didn't just help with overflow — it helped models write correct algorithms
in an unfamiliar language.

**`kimi-coding/k2p5` remains the value champion: $0.24 for all 10 parts.** Down from
$0.46 in run 2. The system prompt cut its token usage almost in half — fewer compile
errors, fewer false starts.

**Three models remain unreachable.** `devstral` got further (past D1P1) but still
couldn't solve D1P2. `gpt-5.3-codex` got further (past D1) but went brain-dead on
D2P1. `qwen3-coder-next` got the furthest (8 parts) but froze mid-thought on D5P1.
The system prompt can't fix models that go catatonic.

**The llms.txt files were never needed.** In run 2, no model proactively consulted
them. In run 3, they weren't even offered. A concise system prompt covering the
essentials was more effective than 14,000 lines of API reference sitting in the
working directory.

---

*Benchmarked on 2026-02-26 (run 2) and 2026-02-27 (run 3) using [pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent) as the agent harness.*

---

*This post was written with AI assistance.*
