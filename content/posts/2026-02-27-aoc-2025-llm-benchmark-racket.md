+++
title = "Benchmarking LLMs on Advent of Code 2025 (Racket)"
description = "10 LLMs, AoC 2025 Days 1–5 in Racket. All ten complete every part — the fifth perfect-completion language in the series."

[taxonomies]
tags = ["Racket", "AI", "Advent of Code"]
+++

Following up on the [Haskell](@/posts/2026-02-24-aoc-2025-llm-benchmark-haskell.md),
[OCaml](@/posts/2026-02-25-aoc-2025-llm-benchmark-ocaml.md),
[Python](@/posts/2026-02-25-aoc-2025-llm-benchmark-python.md),
[ReScript](@/posts/2026-02-26-aoc-2025-llm-benchmark-rescript.md),
[Ruby](@/posts/2026-02-26-aoc-2025-llm-benchmark-ruby.md),
[Elixir](@/posts/2026-02-26-aoc-2025-llm-benchmark-elixir.md),
[Java](@/posts/2026-02-26-aoc-2025-llm-benchmark-java.md),
[Elm](@/posts/2026-02-26-aoc-2025-llm-benchmark-elm.md), and
[Rust](@/posts/2026-02-27-aoc-2025-llm-benchmark-rust.md) benchmarks, I ran the same
AoC 2025 Days 1–5 setup in **Racket**.

Racket is a Lisp dialect from the Scheme family. It's well-known in the programming
languages community and widely used in education (How to Design Programs, SICP variants),
but it's not a mainstream production language. Models need to handle S-expressions,
`#lang racket` conventions, and functional idioms with mutable state available but
discouraged. No scaffolding was provided — each model started from scratch.

The result: another clean sweep. Every model solved every part.

<!-- more -->

## The contestants

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

## Ejections

None. **All 10 models completed all 10 parts.**

Only four retries were needed across all 100 model-parts:
- `kimi-coding/k2p5` — Day 1 Part 2 (wrong answer, fixed on 2nd try)
- `alibaba/qwen3-coder-next` — Day 1 Part 2 (wrong answer, fixed on 2nd try)
- `anthropic/claude-haiku-4-5` — Day 3 Part 1 (wrong answer, fixed on 2nd try)
- `minimax/MiniMax-M2.5` — Day 5 Part 1 (API timeout, dirty restart) and Day 5 Part 2
  (wrong answer, fixed on 2nd try)

## Results (Days 1–5)

### Per-task leaderboards

<br>

#### Day 1 Part 1 — Dial rotation counting

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 39s |
| anthropic/claude-sonnet-4-6 | 40s |
| kimi-coding/k2p5 | 40s |
| openai-codex/gpt-5.3-codex | 41s |
| anthropic/claude-opus-4-6 | 44s |
| zai/glm-5 | 44s |
| mistral/devstral-2512 | 44s |
| alibaba/qwen3-coder-next | 50s |
| alibaba/qwen3.5-plus | 62s |
| minimax/MiniMax-M2.5 | 78s |

<br><br>

#### Day 1 Part 2 — Counting zero-crossings during dial rotation

| Model | Time | Result |
| ------:| ----:| :--: |
| anthropic/claude-haiku-4-5 | 11s | ✓ |
| openai-codex/gpt-5.3-codex | 16s | ✓ |
| anthropic/claude-sonnet-4-6 | 20s | ✓ |
| anthropic/claude-opus-4-6 | 23s | ✓ |
| zai/glm-5 | 25s | ✓ |
| mistral/devstral-2512 | 49s | ✓ |
| alibaba/qwen3.5-plus | 70s | ✓ |
| minimax/MiniMax-M2.5 | 386s | ✓ |
| kimi-coding/k2p5 | 492s | ✓ (2nd try) |
| alibaba/qwen3-coder-next | 540s | ✓ (2nd try) |

<br><br>

#### Day 2 Part 1 — Summing repeated-digit IDs in ranges

| Model | Time |
| ------:| ----:|
| alibaba/qwen3-coder-next | 11s |
| anthropic/claude-haiku-4-5 | 12s |
| kimi-coding/k2p5 | 14s |
| openai-codex/gpt-5.3-codex | 18s |
| anthropic/claude-sonnet-4-6 | 23s |
| mistral/devstral-2512 | 25s |
| zai/glm-5 | 28s |
| anthropic/claude-opus-4-6 | 30s |
| alibaba/qwen3.5-plus | 31s |
| minimax/MiniMax-M2.5 | 37s |

<br><br>

#### Day 2 Part 2 — Repeated-pattern IDs (any repeat count)

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 21s |
| anthropic/claude-haiku-4-5 | 24s |
| openai-codex/gpt-5.3-codex | 26s |
| kimi-coding/k2p5 | 27s |
| alibaba/qwen3-coder-next | 30s |
| alibaba/qwen3.5-plus | 34s |
| anthropic/claude-sonnet-4-6 | 36s |
| anthropic/claude-opus-4-6 | 41s |
| zai/glm-5 | 50s |
| minimax/MiniMax-M2.5 | 94s |

<br><br>

#### Day 3 Part 1 — Maximizing 2-digit joltage from battery banks

| Model | Time | Result |
| ------:| ----:| :--: |
| anthropic/claude-sonnet-4-6 | 32s | ✓ |
| anthropic/claude-opus-4-6 | 32s | ✓ |
| alibaba/qwen3.5-plus | 34s | ✓ |
| zai/glm-5 | 37s | ✓ |
| mistral/devstral-2512 | 38s | ✓ |
| kimi-coding/k2p5 | 40s | ✓ |
| openai-codex/gpt-5.3-codex | 48s | ✓ |
| alibaba/qwen3-coder-next | 50s | ✓ |
| minimax/MiniMax-M2.5 | 110s | ✓ |
| anthropic/claude-haiku-4-5 | 229s | ✓ (2nd try) |

<br><br>

#### Day 3 Part 2 — Maximizing 12-digit joltage from battery banks

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 24s |
| alibaba/qwen3-coder-next | 29s |
| anthropic/claude-sonnet-4-6 | 31s |
| anthropic/claude-opus-4-6 | 34s |
| openai-codex/gpt-5.3-codex | 38s |
| kimi-coding/k2p5 | 40s |
| alibaba/qwen3.5-plus | 86s |
| mistral/devstral-2512 | 156s |
| zai/glm-5 | 171s |
| minimax/MiniMax-M2.5 | 229s |

<br><br>

#### Day 4 Part 1 — Grid neighbor counting (accessible paper rolls)

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 13s |
| anthropic/claude-sonnet-4-6 | 17s |
| openai-codex/gpt-5.3-codex | 17s |
| anthropic/claude-opus-4-6 | 21s |
| kimi-coding/k2p5 | 22s |
| zai/glm-5 | 24s |
| alibaba/qwen3-coder-next | 40s |
| alibaba/qwen3.5-plus | 41s |
| minimax/MiniMax-M2.5 | 63s |
| mistral/devstral-2512 | 255s |

<br><br>

#### Day 4 Part 2 — Iterative grid removal simulation

| Model | Time |
| ------:| ----:|
| openai-codex/gpt-5.3-codex | 27s |
| anthropic/claude-sonnet-4-6 | 30s |
| alibaba/qwen3.5-plus | 30s |
| anthropic/claude-opus-4-6 | 31s |
| kimi-coding/k2p5 | 33s |
| zai/glm-5 | 41s |
| anthropic/claude-haiku-4-5 | 49s |
| minimax/MiniMax-M2.5 | 64s |
| mistral/devstral-2512 | 84s |
| alibaba/qwen3-coder-next | 290s |

<br><br>

#### Day 5 Part 1 — Range membership checking

| Model | Time | Result |
| ------:| ----:| :--: |
| openai-codex/gpt-5.3-codex | 14s | ✓ |
| anthropic/claude-haiku-4-5 | 15s | ✓ |
| mistral/devstral-2512 | 16s | ✓ |
| anthropic/claude-sonnet-4-6 | 17s | ✓ |
| zai/glm-5 | 18s | ✓ |
| alibaba/qwen3-coder-next | 19s | ✓ |
| anthropic/claude-opus-4-6 | 21s | ✓ |
| alibaba/qwen3.5-plus | 21s | ✓ |
| kimi-coding/k2p5 | 28s | ✓ |
| minimax/MiniMax-M2.5 | —* | ✓ (dirty retry) |

\* API timeout forced a fresh relaunch.

<br><br>

#### Day 5 Part 2 — Counting total fresh IDs from overlapping ranges

| Model | Time | Result |
| ------:| ----:| :--: |
| kimi-coding/k2p5 | 21s | ✓ |
| alibaba/qwen3-coder-next | 24s | ✓ |
| openai-codex/gpt-5.3-codex | 27s | ✓ |
| anthropic/claude-opus-4-6 | 29s | ✓ |
| anthropic/claude-haiku-4-5 | 30s | ✓ |
| anthropic/claude-sonnet-4-6 | 32s | ✓ |
| zai/glm-5 | 36s | ✓ |
| alibaba/qwen3.5-plus | 44s | ✓ |
| mistral/devstral-2512 | 59s | ✓ |
| minimax/MiniMax-M2.5 | 789s | ✓ (2nd try) |

<br>

### Summary tables

#### Wall-clock time (seconds)

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
      <td>openai-codex/gpt-5.3-codex</td>
      <td style="text-align: right">41s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">26s</td>
      <td style="text-align: right">48s</td>
      <td style="text-align: right">38s</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right"><strong>272s</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">40s</td>
      <td style="text-align: right">20s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right">36s</td>
      <td style="text-align: right">32s</td>
      <td style="text-align: right">31s</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">32s</td>
      <td style="text-align: right"><strong>278s</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">44s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">41s</td>
      <td style="text-align: right">32s</td>
      <td style="text-align: right">34s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">31s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">29s</td>
      <td style="text-align: right"><strong>306s</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">39s</td>
      <td style="text-align: right">11s</td>
      <td style="text-align: right">12s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">229s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">13s</td>
      <td style="text-align: right">49s</td>
      <td style="text-align: right">15s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right"><strong>446s</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">62s</td>
      <td style="text-align: right">70s</td>
      <td style="text-align: right">31s</td>
      <td style="text-align: right">34s</td>
      <td style="text-align: right">34s</td>
      <td style="text-align: right">86s</td>
      <td style="text-align: right">41s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">44s</td>
      <td style="text-align: right"><strong>453s</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">44s</td>
      <td style="text-align: right">25s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">50s</td>
      <td style="text-align: right">37s</td>
      <td style="text-align: right">171s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">41s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">36s</td>
      <td style="text-align: right"><strong>474s</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">44s</td>
      <td style="text-align: right">49s</td>
      <td style="text-align: right">25s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">38s</td>
      <td style="text-align: right">156s</td>
      <td style="text-align: right">255s</td>
      <td style="text-align: right">84s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">59s</td>
      <td style="text-align: right"><strong>747s</strong></td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">40s</td>
      <td style="text-align: right">492s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">40s</td>
      <td style="text-align: right">40s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">33s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right"><strong>757s</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">50s</td>
      <td style="text-align: right">540s</td>
      <td style="text-align: right">11s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">50s</td>
      <td style="text-align: right">29s</td>
      <td style="text-align: right">40s</td>
      <td style="text-align: right">290s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right"><strong>1,083s</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">78s</td>
      <td style="text-align: right">386s</td>
      <td style="text-align: right">37s</td>
      <td style="text-align: right">94s</td>
      <td style="text-align: right">110s</td>
      <td style="text-align: right">229s</td>
      <td style="text-align: right">63s</td>
      <td style="text-align: right">64s</td>
      <td style="text-align: right">—*</td>
      <td style="text-align: right">789s</td>
      <td style="text-align: right"><strong>1,850s*</strong></td>
    </tr>
  </tbody>
</table>

\* MiniMax D5P1 required a dirty restart after API timeout; wall-clock time not captured
cleanly. Total excludes D5P1.

<br>

#### Output tokens per part

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
      <td>openai-codex/gpt-5.3-codex</td>
      <td style="text-align: right">427</td>
      <td style="text-align: right">570</td>
      <td style="text-align: right">674</td>
      <td style="text-align: right">540</td>
      <td style="text-align: right">1,109</td>
      <td style="text-align: right">893</td>
      <td style="text-align: right">656</td>
      <td style="text-align: right">740</td>
      <td style="text-align: right">561</td>
      <td style="text-align: right">541</td>
      <td style="text-align: right"><strong>6,711</strong></td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">575</td>
      <td style="text-align: right">2,515</td>
      <td style="text-align: right">782</td>
      <td style="text-align: right">830</td>
      <td style="text-align: right">614</td>
      <td style="text-align: right">774</td>
      <td style="text-align: right">636</td>
      <td style="text-align: right">793</td>
      <td style="text-align: right">886</td>
      <td style="text-align: right">585</td>
      <td style="text-align: right"><strong>7,990</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">465</td>
      <td style="text-align: right">518</td>
      <td style="text-align: right">660</td>
      <td style="text-align: right">766</td>
      <td style="text-align: right">489</td>
      <td style="text-align: right">4,134</td>
      <td style="text-align: right">560</td>
      <td style="text-align: right">671</td>
      <td style="text-align: right">475</td>
      <td style="text-align: right">505</td>
      <td style="text-align: right"><strong>8,243</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">704</td>
      <td style="text-align: right">1,158</td>
      <td style="text-align: right">1,453</td>
      <td style="text-align: right">1,435</td>
      <td style="text-align: right">797</td>
      <td style="text-align: right">958</td>
      <td style="text-align: right">901</td>
      <td style="text-align: right">930</td>
      <td style="text-align: right">865</td>
      <td style="text-align: right">813</td>
      <td style="text-align: right"><strong>10,014</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">718</td>
      <td style="text-align: right">1,045</td>
      <td style="text-align: right">1,318</td>
      <td style="text-align: right">1,414</td>
      <td style="text-align: right">902</td>
      <td style="text-align: right">947</td>
      <td style="text-align: right">990</td>
      <td style="text-align: right">1,096</td>
      <td style="text-align: right">807</td>
      <td style="text-align: right">844</td>
      <td style="text-align: right"><strong>10,081</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">1,172</td>
      <td style="text-align: right">1,040</td>
      <td style="text-align: right">1,125</td>
      <td style="text-align: right">1,074</td>
      <td style="text-align: right">5,350</td>
      <td style="text-align: right">1,092</td>
      <td style="text-align: right">1,332</td>
      <td style="text-align: right">5,061</td>
      <td style="text-align: right">1,274</td>
      <td style="text-align: right">2,823</td>
      <td style="text-align: right"><strong>21,343</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">1,053</td>
      <td style="text-align: right">6,960</td>
      <td style="text-align: right">768</td>
      <td style="text-align: right">1,421</td>
      <td style="text-align: right">1,345</td>
      <td style="text-align: right">1,679</td>
      <td style="text-align: right">4,761</td>
      <td style="text-align: right">10,162</td>
      <td style="text-align: right">1,430</td>
      <td style="text-align: right">818</td>
      <td style="text-align: right"><strong>30,397</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">2,831</td>
      <td style="text-align: right">9,323</td>
      <td style="text-align: right">3,407</td>
      <td style="text-align: right">1,790</td>
      <td style="text-align: right">2,579</td>
      <td style="text-align: right">6,137</td>
      <td style="text-align: right">1,926</td>
      <td style="text-align: right">1,177</td>
      <td style="text-align: right">1,654</td>
      <td style="text-align: right">2,102</td>
      <td style="text-align: right"><strong>32,926</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">1,005</td>
      <td style="text-align: right">6,380</td>
      <td style="text-align: right">1,392</td>
      <td style="text-align: right">3,668</td>
      <td style="text-align: right">3,208</td>
      <td style="text-align: right">7,825</td>
      <td style="text-align: right">2,038</td>
      <td style="text-align: right">1,184</td>
      <td style="text-align: right">1,316</td>
      <td style="text-align: right">29,365</td>
      <td style="text-align: right"><strong>57,381</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">2,215</td>
      <td style="text-align: right">7,035</td>
      <td style="text-align: right">2,306</td>
      <td style="text-align: right">800</td>
      <td style="text-align: right">2,344</td>
      <td style="text-align: right">14,380</td>
      <td style="text-align: right">23,047</td>
      <td style="text-align: right">6,962</td>
      <td style="text-align: right">1,368</td>
      <td style="text-align: right">5,165</td>
      <td style="text-align: right"><strong>65,622</strong></td>
    </tr>
  </tbody>
</table>

<br>

#### API cost per part (approximate USD)

*Costs are rough approximations based on published per-token pricing. I use subscription plans, so my actual spending is capped regardless.*

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
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">.0084</td>
      <td style="text-align: right">.0165</td>
      <td style="text-align: right">.0035</td>
      <td style="text-align: right">.0043</td>
      <td style="text-align: right">.0090</td>
      <td style="text-align: right">.0081</td>
      <td style="text-align: right">.0029</td>
      <td style="text-align: right">.0042</td>
      <td style="text-align: right">.0040</td>
      <td style="text-align: right">.0040</td>
      <td style="text-align: right"><strong>$0.06</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">.0061</td>
      <td style="text-align: right">.0068</td>
      <td style="text-align: right">.0072</td>
      <td style="text-align: right">.0104</td>
      <td style="text-align: right">.0271</td>
      <td style="text-align: right">.0761</td>
      <td style="text-align: right">.0222</td>
      <td style="text-align: right">.0190</td>
      <td style="text-align: right">.0052</td>
      <td style="text-align: right">.0073</td>
      <td style="text-align: right"><strong>$0.19</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">.0347</td>
      <td style="text-align: right">.0104</td>
      <td style="text-align: right">.0245</td>
      <td style="text-align: right">.0104</td>
      <td style="text-align: right">.0664</td>
      <td style="text-align: right">.0137</td>
      <td style="text-align: right">.0292</td>
      <td style="text-align: right">.0469</td>
      <td style="text-align: right">.0317</td>
      <td style="text-align: right">.0231</td>
      <td style="text-align: right"><strong>$0.29</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">.0237</td>
      <td style="text-align: right">.0460</td>
      <td style="text-align: right">.0213</td>
      <td style="text-align: right">.0185</td>
      <td style="text-align: right">.0137</td>
      <td style="text-align: right">.0538</td>
      <td style="text-align: right">.0553</td>
      <td style="text-align: right">.0388</td>
      <td style="text-align: right">.0108</td>
      <td style="text-align: right">.0216</td>
      <td style="text-align: right"><strong>$0.30</strong></td>
    </tr>
    <tr>
      <td>openai-codex/gpt-5.3-codex</td>
      <td style="text-align: right">.0155</td>
      <td style="text-align: right">.0220</td>
      <td style="text-align: right">.0271</td>
      <td style="text-align: right">.0171</td>
      <td style="text-align: right">.0340</td>
      <td style="text-align: right">.0352</td>
      <td style="text-align: right">.0386</td>
      <td style="text-align: right">.0410</td>
      <td style="text-align: right">.0389</td>
      <td style="text-align: right">.0390</td>
      <td style="text-align: right"><strong>$0.31</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">.0349</td>
      <td style="text-align: right">.0303</td>
      <td style="text-align: right">.0457</td>
      <td style="text-align: right">.0377</td>
      <td style="text-align: right">.0373</td>
      <td style="text-align: right">.0279</td>
      <td style="text-align: right">.0388</td>
      <td style="text-align: right">.0335</td>
      <td style="text-align: right">.0348</td>
      <td style="text-align: right">.0246</td>
      <td style="text-align: right"><strong>$0.35</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">.1142</td>
      <td style="text-align: right">.0926</td>
      <td style="text-align: right">.1286</td>
      <td style="text-align: right">.0646</td>
      <td style="text-align: right">.1117</td>
      <td style="text-align: right">.0834</td>
      <td style="text-align: right">.1160</td>
      <td style="text-align: right">.0879</td>
      <td style="text-align: right">.1117</td>
      <td style="text-align: right">.0939</td>
      <td style="text-align: right"><strong>$1.00</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">.0360</td>
      <td style="text-align: right">.1663</td>
      <td style="text-align: right">.0092</td>
      <td style="text-align: right">.0198</td>
      <td style="text-align: right">.0993</td>
      <td style="text-align: right">.0962</td>
      <td style="text-align: right">.1017</td>
      <td style="text-align: right">.4650</td>
      <td style="text-align: right">.0828</td>
      <td style="text-align: right">.0647</td>
      <td style="text-align: right"><strong>$1.14</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">.0144</td>
      <td style="text-align: right">.0334</td>
      <td style="text-align: right">.0057</td>
      <td style="text-align: right">.0259</td>
      <td style="text-align: right">.0356</td>
      <td style="text-align: right">.1261</td>
      <td style="text-align: right">.0452</td>
      <td style="text-align: right">.0395</td>
      <td style="text-align: right">.0208</td>
      <td style="text-align: right">.8727</td>
      <td style="text-align: right"><strong>$1.22</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">.0233</td>
      <td style="text-align: right">.0987</td>
      <td style="text-align: right">.0171</td>
      <td style="text-align: right">.0147</td>
      <td style="text-align: right">.0286</td>
      <td style="text-align: right">.3224</td>
      <td style="text-align: right">.5733</td>
      <td style="text-align: right">.1688</td>
      <td style="text-align: right">.0142</td>
      <td style="text-align: right">.0667</td>
      <td style="text-align: right"><strong>$1.33</strong></td>
    </tr>
  </tbody>
</table>

## Observations

**10/10 completers — zero ejections.** Racket joins Python, Ruby, Elm, and Rust as the
fifth language in this series where every model solved every part.

**`gpt-5.3-codex`** — fastest overall at 272s. Also the most token-efficient at 6,711
tokens total. Never needed a retry. No single part over 48s.

**`claude-sonnet-4-6`** — second fastest at 278s, remarkably consistent. Every part
between 17–40s.

**`kimi-coding/k2p5`** — cheapest at $0.06 total, second fewest tokens at 7,990. The
Day 1 Part 2 retry inflated its total time to 757s, but on 9 of 10 parts it was under
40s.

**`minimax/MiniMax-M2.5`** — slowest overall at 1,850s. Hit an API timeout on Day 5
Part 1, then gave a wrong answer on Day 5 Part 2 that took 789s and 29K tokens to fix.
Day 1 Part 2 also took 386s. The model completed everything, but was consistently the
bottleneck.

**`devstral-2512`** — spiked on two parts: D3P2 (156s, 14K tokens) and D4P1 (255s,
23K tokens, $0.57). Every other part was routine.

**Day 1 Part 2 was the stumbling block.** Two models (`k2p5`, `qwen3-coder-next`)
needed a second try, and `MiniMax-M2.5` took 386s on its first try. Part 2 was otherwise
straightforward — most first-try solves landed under 50s.

**No Racket-specific struggles.** No model got stuck on S-expression syntax,
`#lang racket` conventions, or Racket-specific library APIs. The parentheses didn't slow
anyone down.

## Cross-language snapshot

| Language | Models completing all 10 parts |
| --------| ------|
| Python | 10/10 |
| Ruby | 10/10 |
| Elm | 10/10 |
| Rust | 10/10 |
| **Racket** | **10/10** |
| Java | 9/10 |
| Elixir | 7/10 |
| Haskell | 7/11 |
| OCaml | 5/9 |
| ReScript (run 2) | 2/10 |

Racket's perfect completion rate is notable. It's not a mainstream language, but it has
clear semantics, good documentation, and a REPL-friendly workflow. Unlike Elm (which
needed a scaffold) or Rust (which demands borrow-checking), Racket lets you write a
quick script with `#lang racket` and go — and that simplicity may have helped.

*Benchmarked on 2026-02-27 using [pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent) as the agent harness.*

---

*This post was written with AI assistance.*
