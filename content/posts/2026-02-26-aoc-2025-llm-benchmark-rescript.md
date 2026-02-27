+++
title = "Benchmarking LLMs on Advent of Code 2025 (ReScript) — Run 2"
description = "A redo of the ReScript benchmark with an overflow warning baked in and a longer timeout. Two models finish cleanly. The hint saved opus — but not qwen3.5-plus."

[taxonomies]
tags = ["ReScript", "AI", "Advent of Code"]
+++

Following up on [the Haskell benchmark](@/posts/2026-02-24-aoc-2025-llm-benchmark-haskell.md), [the OCaml
benchmark](@/posts/2026-02-25-aoc-2025-llm-benchmark-ocaml.md), and [the Python
benchmark](@/posts/2026-02-25-aoc-2025-llm-benchmark-python.md), I ran AoC 2025 Days 1–5 in
**ReScript** — a typed functional language that compiles to JavaScript with a lean
standard library, a distinct syntax, and very limited LLM training data.

The first run was rough: 7 of 10 models ejected, `claude-haiku-4-5` the sole completer,
integer overflow the root cause of most failures. Two things changed for this run:

1. **Overflow warning baked into every prompt.** ReScript's `int` type is 32 bits on the
   JavaScript runtime. Several puzzles produce answers in the tens of billions or hundreds
   of trillions — well beyond that ceiling. No warning was given in run 1. In run 2 every
   prompt includes an explicit note that large answers require `float` or `BigInt`.

2. **Timeout increased from 3 to 5 minutes per attempt.** ReScript project setup
   (initialising npm, configuring the build system, first compile) is non-trivial for
   models unfamiliar with the ecosystem. Three minutes left very little room for the actual
   solving.

<!-- more -->

## The contestants

Same 10 models as run 1:

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

## The rules

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

## Ejections

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

## Results

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

## Full summary — all 10 models

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

## Observations

**The overflow warning made a real difference — for `opus`.** In run 1 both `opus` and
`sonnet` overflowed on Day 5 Part 2. In run 2 `opus` completed the benchmark. The
warning did its job. `qwen3.5-plus` got further than in run 1 and even self-corrected
an overflow mid-run, but eventually fell to the same bug on the hardest puzzle. A
runtime hint helps but isn't a guarantee.

**`kimi-coding/k2p5`** — $0.46 for all 10 parts. In run 1 it was ejected on Day 1 Part 2.
With 5 minutes it completed every puzzle correctly. One part (Day 2 Part 2) took 854
seconds; every other part was under 4 minutes.

**`claude-opus-4-6`** — fastest completer at 509 seconds total. In run 1 it overflowed
on the final puzzle; the warning fixed that.

**Day 1 Part 2 ejected four models in run 2** (different four from run 1). The puzzle
has a subtle boundary condition that produced wrong answers from multiple models.

**`qwen3-coder-next`** — cost $11.36 and completed 2.5 parts. On Day 2 Part 1 it ran
for over 40 minutes, consumed nearly half its 262k context window, and produced no answer.

**No model proactively consulted the documentation.** Neither llms.txt file was opened
on any first attempt — same as run 1.

**Complete token and cost data is available for the first time.** Run 1 lost
session data by wiping working directories between days. This run archives them instead,
enabling the full per-day breakdowns above.

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

---

## What's next

One open question: would enabling `thinking` mode help models catch the 32-bit overflow?
Rust or Go would also be interesting — those languages require explicit integer-width
choices, which might surface the issue at compile time rather than silently.

*Benchmarked on 2026-02-26 using [pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent) as the agent harness.*

---

*This post was written with AI assistance.*
