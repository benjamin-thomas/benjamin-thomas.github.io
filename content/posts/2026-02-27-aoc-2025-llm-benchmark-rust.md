+++
title = "Benchmarking LLMs on Advent of Code 2025 (Rust)"
description = "10 LLMs, AoC 2025 Days 1–5 in Rust. Two needed second tries on Day 1, but nobody gets ejected."

[taxonomies]
tags = ["Rust", "AI", "Advent of Code"]
+++

Following up on the [Haskell](@/posts/2026-02-24-aoc-2025-llm-benchmark-haskell.md),
[OCaml](@/posts/2026-02-25-aoc-2025-llm-benchmark-ocaml.md),
[Python](@/posts/2026-02-25-aoc-2025-llm-benchmark-python.md),
[Elixir](@/posts/2026-02-26-aoc-2025-llm-benchmark-elixir.md),
[Elm](@/posts/2026-02-26-aoc-2025-llm-benchmark-elm.md),
[Java](@/posts/2026-02-26-aoc-2025-llm-benchmark-java.md),
[ReScript](@/posts/2026-02-26-aoc-2025-llm-benchmark-rescript.md), and
[Ruby](@/posts/2026-02-26-aoc-2025-llm-benchmark-ruby.md) benchmarks, I ran the same
orchestration setup on the same AoC 2025 Days 1–5 puzzles — this time in **Rust**.

Rust is a compiled systems language with strict ownership rules and a demanding compiler.
Models have to deal with borrow-checking, lifetime annotations, and explicit error handling
just to get a solution that compiles.

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

**None.** All 10 models solved all 10 parts and survived the full benchmark. Two models
needed a second attempt on Day 1 Part 2, but nobody was ejected.

## Results (Days 1–5)

### Per-task leaderboards

<br>

#### Day 1 Part 1 — Dial rotation counting

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 12s |
| anthropic/claude-haiku-4-5 | 16s |
| openai-codex/gpt-5.3-codex | 16s |
| anthropic/claude-sonnet-4-6 | 17s |
| anthropic/claude-opus-4-6 | 19s |
| alibaba/qwen3.5-plus | 22s |
| zai/glm-5 | 31s |
| kimi-coding/k2p5 | 31s |
| alibaba/qwen3-coder-next | 52s |
| minimax/MiniMax-M2.5 | 63s |

<br><br>

#### Day 1 Part 2 — Counting zero-crossings during dial rotation

`glm-5` and `qwen3.5-plus` both gave wrong answers on their first attempt. Both
got it right on the second try.

| Model | Time | Note |
| ------:| ----:| ----:|
| anthropic/claude-haiku-4-5 | 10s | |
| openai-codex/gpt-5.3-codex | 15s | |
| mistral/devstral-2512 | 18s | |
| anthropic/claude-opus-4-6 | 21s | |
| anthropic/claude-sonnet-4-6 | 28s | |
| kimi-coding/k2p5 | 60s | |
| alibaba/qwen3-coder-next | 86s | |
| minimax/MiniMax-M2.5 | 93s | |
| alibaba/qwen3.5-plus | 206s | 2nd try |
| zai/glm-5 | 212s | 2nd try |

<br><br>

#### Day 2 Part 1 — Summing repeated-digit IDs in ranges

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 16s |
| kimi-coding/k2p5 | 18s |
| openai-codex/gpt-5.3-codex | 20s |
| alibaba/qwen3.5-plus | 20s |
| anthropic/claude-sonnet-4-6 | 30s |
| zai/glm-5 | 30s |
| mistral/devstral-2512 | 30s |
| anthropic/claude-opus-4-6 | 32s |
| minimax/MiniMax-M2.5 | 36s |
| alibaba/qwen3-coder-next | 197s |

<br><br>

#### Day 2 Part 2 — Repeated-pattern IDs (any repeat count)

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 10s |
| mistral/devstral-2512 | 11s |
| alibaba/qwen3-coder-next | 14s |
| openai-codex/gpt-5.3-codex | 16s |
| alibaba/qwen3.5-plus | 21s |
| kimi-coding/k2p5 | 22s |
| zai/glm-5 | 33s |
| anthropic/claude-sonnet-4-6 | 37s |
| anthropic/claude-opus-4-6 | 43s |
| minimax/MiniMax-M2.5 | 51s |

<br><br>

#### Day 3 Part 1 — Maximizing 2-digit joltage from battery banks

| Model | Time |
| ------:| ----:|
| kimi-coding/k2p5 | 15s |
| anthropic/claude-haiku-4-5 | 16s |
| anthropic/claude-sonnet-4-6 | 20s |
| alibaba/qwen3.5-plus | 23s |
| openai-codex/gpt-5.3-codex | 24s |
| anthropic/claude-opus-4-6 | 28s |
| zai/glm-5 | 30s |
| mistral/devstral-2512 | 35s |
| minimax/MiniMax-M2.5 | 67s |
| alibaba/qwen3-coder-next | 103s |

<br><br>

#### Day 3 Part 2 — Maximizing 12-digit joltage from battery banks

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 13s |
| openai-codex/gpt-5.3-codex | 15s |
| kimi-coding/k2p5 | 16s |
| alibaba/qwen3.5-plus | 18s |
| anthropic/claude-sonnet-4-6 | 19s |
| anthropic/claude-opus-4-6 | 24s |
| zai/glm-5 | 28s |
| alibaba/qwen3-coder-next | 29s |
| anthropic/claude-haiku-4-5 | 33s |
| minimax/MiniMax-M2.5 | 41s |

<br><br>

#### Day 4 Part 1 — Grid neighbor counting (accessible paper rolls)

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 16s |
| openai-codex/gpt-5.3-codex | 17s |
| kimi-coding/k2p5 | 17s |
| anthropic/claude-haiku-4-5 | 19s |
| anthropic/claude-sonnet-4-6 | 19s |
| anthropic/claude-opus-4-6 | 20s |
| alibaba/qwen3-coder-next | 20s |
| alibaba/qwen3.5-plus | 21s |
| zai/glm-5 | 38s |
| minimax/MiniMax-M2.5 | 64s |

<br><br>

#### Day 4 Part 2 — Iterative grid removal simulation

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 12s |
| anthropic/claude-sonnet-4-6 | 16s |
| alibaba/qwen3.5-plus | 16s |
| kimi-coding/k2p5 | 17s |
| mistral/devstral-2512 | 18s |
| anthropic/claude-opus-4-6 | 22s |
| openai-codex/gpt-5.3-codex | 22s |
| alibaba/qwen3-coder-next | 28s |
| minimax/MiniMax-M2.5 | 31s |
| zai/glm-5 | 34s |

<br><br>

#### Day 5 Part 1 — Range membership checking

`qwen3-coder-next` initially wrote a stale answer from the previous day while still working.
After the dirty stop was cleared, it produced the correct answer.

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 14s |
| anthropic/claude-sonnet-4-6 | 18s |
| openai-codex/gpt-5.3-codex | 18s |
| kimi-coding/k2p5 | 18s |
| anthropic/claude-haiku-4-5 | 19s |
| anthropic/claude-opus-4-6 | 22s |
| alibaba/qwen3.5-plus | 33s |
| zai/glm-5 | 35s |
| minimax/MiniMax-M2.5 | 39s |
| alibaba/qwen3-coder-next | 162s |

<br><br>

#### Day 5 Part 2 — Counting total fresh IDs from overlapping ranges

| Model | Time |
| ------:| ----:|
| kimi-coding/k2p5 | 14s |
| anthropic/claude-sonnet-4-6 | 16s |
| anthropic/claude-haiku-4-5 | 17s |
| openai-codex/gpt-5.3-codex | 18s |
| anthropic/claude-opus-4-6 | 19s |
| mistral/devstral-2512 | 25s |
| minimax/MiniMax-M2.5 | 29s |
| alibaba/qwen3.5-plus | 30s |
| zai/glm-5 | 47s |
| alibaba/qwen3-coder-next | 60s |

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
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">10s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">10s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">33s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">12s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right"><strong>168s</strong></td>
    </tr>
    <tr>
      <td>openai-codex/gpt-5.3-codex</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">15s</td>
      <td style="text-align: right">20s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">15s</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right"><strong>181s</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">12s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">11s</td>
      <td style="text-align: right">35s</td>
      <td style="text-align: right">13s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">25s</td>
      <td style="text-align: right"><strong>192s</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">37s</td>
      <td style="text-align: right">20s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right"><strong>220s</strong></td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">31s</td>
      <td style="text-align: right">60s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">15s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right"><strong>228s</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">32s</td>
      <td style="text-align: right">43s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">20s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right"><strong>250s</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">206s</td>
      <td style="text-align: right">20s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">33s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right"><strong>410s</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">63s</td>
      <td style="text-align: right">93s</td>
      <td style="text-align: right">36s</td>
      <td style="text-align: right">51s</td>
      <td style="text-align: right">67s</td>
      <td style="text-align: right">41s</td>
      <td style="text-align: right">64s</td>
      <td style="text-align: right">31s</td>
      <td style="text-align: right">39s</td>
      <td style="text-align: right">29s</td>
      <td style="text-align: right"><strong>514s</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">31s</td>
      <td style="text-align: right">212s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">33s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">38s</td>
      <td style="text-align: right">34s</td>
      <td style="text-align: right">35s</td>
      <td style="text-align: right">47s</td>
      <td style="text-align: right"><strong>518s</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">52s</td>
      <td style="text-align: right">86s</td>
      <td style="text-align: right">197s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">103s</td>
      <td style="text-align: right">29s</td>
      <td style="text-align: right">20s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">162s</td>
      <td style="text-align: right">60s</td>
      <td style="text-align: right"><strong>751s</strong></td>
    </tr>
  </tbody>
</table>

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
      <td style="text-align: right">448</td>
      <td style="text-align: right">689</td>
      <td style="text-align: right">575</td>
      <td style="text-align: right">667</td>
      <td style="text-align: right">562</td>
      <td style="text-align: right">630</td>
      <td style="text-align: right">627</td>
      <td style="text-align: right">975</td>
      <td style="text-align: right">617</td>
      <td style="text-align: right">638</td>
      <td style="text-align: right"><strong>6,428</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">636</td>
      <td style="text-align: right">1,251</td>
      <td style="text-align: right">720</td>
      <td style="text-align: right">783</td>
      <td style="text-align: right">547</td>
      <td style="text-align: right">695</td>
      <td style="text-align: right">896</td>
      <td style="text-align: right">745</td>
      <td style="text-align: right">774</td>
      <td style="text-align: right">837</td>
      <td style="text-align: right"><strong>7,884</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">732</td>
      <td style="text-align: right">1,038</td>
      <td style="text-align: right">1,658</td>
      <td style="text-align: right">2,416</td>
      <td style="text-align: right">1,112</td>
      <td style="text-align: right">1,064</td>
      <td style="text-align: right">979</td>
      <td style="text-align: right">979</td>
      <td style="text-align: right">933</td>
      <td style="text-align: right">850</td>
      <td style="text-align: right"><strong>11,761</strong></td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">766</td>
      <td style="text-align: right">4,725</td>
      <td style="text-align: right">1,026</td>
      <td style="text-align: right">1,307</td>
      <td style="text-align: right">585</td>
      <td style="text-align: right">793</td>
      <td style="text-align: right">692</td>
      <td style="text-align: right">1,076</td>
      <td style="text-align: right">723</td>
      <td style="text-align: right">743</td>
      <td style="text-align: right"><strong>12,436</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">1,023</td>
      <td style="text-align: right">1,575</td>
      <td style="text-align: right">1,984</td>
      <td style="text-align: right">2,522</td>
      <td style="text-align: right">1,024</td>
      <td style="text-align: right">1,121</td>
      <td style="text-align: right">1,135</td>
      <td style="text-align: right">1,094</td>
      <td style="text-align: right">993</td>
      <td style="text-align: right">952</td>
      <td style="text-align: right"><strong>13,423</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">1,583</td>
      <td style="text-align: right">3,010</td>
      <td style="text-align: right">1,172</td>
      <td style="text-align: right">1,449</td>
      <td style="text-align: right">1,913</td>
      <td style="text-align: right">1,140</td>
      <td style="text-align: right">1,359</td>
      <td style="text-align: right">1,041</td>
      <td style="text-align: right">1,094</td>
      <td style="text-align: right">923</td>
      <td style="text-align: right"><strong>14,684</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">1,315</td>
      <td style="text-align: right">1,150</td>
      <td style="text-align: right">1,692</td>
      <td style="text-align: right">937</td>
      <td style="text-align: right">1,339</td>
      <td style="text-align: right">3,084</td>
      <td style="text-align: right">1,544</td>
      <td style="text-align: right">1,547</td>
      <td style="text-align: right">1,667</td>
      <td style="text-align: right">1,559</td>
      <td style="text-align: right"><strong>15,834</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">610</td>
      <td style="text-align: right">2,746</td>
      <td style="text-align: right">2,625</td>
      <td style="text-align: right">1,574</td>
      <td style="text-align: right">2,616</td>
      <td style="text-align: right">1,298</td>
      <td style="text-align: right">1,225</td>
      <td style="text-align: right">1,709</td>
      <td style="text-align: right">568</td>
      <td style="text-align: right">1,752</td>
      <td style="text-align: right"><strong>16,723</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">1,198</td>
      <td style="text-align: right">5,507</td>
      <td style="text-align: right">1,693</td>
      <td style="text-align: right">1,550</td>
      <td style="text-align: right">2,044</td>
      <td style="text-align: right">1,506</td>
      <td style="text-align: right">1,244</td>
      <td style="text-align: right">1,231</td>
      <td style="text-align: right">1,447</td>
      <td style="text-align: right">1,400</td>
      <td style="text-align: right"><strong>18,820</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">1,500</td>
      <td style="text-align: right">8,238</td>
      <td style="text-align: right">7,040</td>
      <td style="text-align: right">808</td>
      <td style="text-align: right">3,046</td>
      <td style="text-align: right">1,948</td>
      <td style="text-align: right">1,203</td>
      <td style="text-align: right">1,265</td>
      <td style="text-align: right">5,264</td>
      <td style="text-align: right">1,991</td>
      <td style="text-align: right"><strong>32,303</strong></td>
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
      <td style="text-align: right">.0236</td>
      <td style="text-align: right">.0299</td>
      <td style="text-align: right">.0042</td>
      <td style="text-align: right">.0059</td>
      <td style="text-align: right">.0099</td>
      <td style="text-align: right">.0104</td>
      <td style="text-align: right">.0112</td>
      <td style="text-align: right">.0111</td>
      <td style="text-align: right">.0111</td>
      <td style="text-align: right">.0100</td>
      <td style="text-align: right"><strong>$0.13</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">.0201</td>
      <td style="text-align: right">.0292</td>
      <td style="text-align: right">.0086</td>
      <td style="text-align: right">.0095</td>
      <td style="text-align: right">.0062</td>
      <td style="text-align: right">.0084</td>
      <td style="text-align: right">.0105</td>
      <td style="text-align: right">.0105</td>
      <td style="text-align: right">.0342</td>
      <td style="text-align: right">.0279</td>
      <td style="text-align: right"><strong>$0.17</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">.0101</td>
      <td style="text-align: right">.0245</td>
      <td style="text-align: right">.0320</td>
      <td style="text-align: right">.0274</td>
      <td style="text-align: right">.0310</td>
      <td style="text-align: right">.0161</td>
      <td style="text-align: right">.0111</td>
      <td style="text-align: right">.0276</td>
      <td style="text-align: right">.0077</td>
      <td style="text-align: right">.0187</td>
      <td style="text-align: right"><strong>$0.21</strong></td>
    </tr>
    <tr>
      <td>openai-codex/gpt-5.3-codex</td>
      <td style="text-align: right">.0205</td>
      <td style="text-align: right">.0251</td>
      <td style="text-align: right">.0262</td>
      <td style="text-align: right">.0196</td>
      <td style="text-align: right">.0220</td>
      <td style="text-align: right">.0173</td>
      <td style="text-align: right">.0219</td>
      <td style="text-align: right">.0235</td>
      <td style="text-align: right">.0193</td>
      <td style="text-align: right">.0169</td>
      <td style="text-align: right"><strong>$0.21</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">.0257</td>
      <td style="text-align: right">.0492</td>
      <td style="text-align: right">.0047</td>
      <td style="text-align: right">.0080</td>
      <td style="text-align: right">.0259</td>
      <td style="text-align: right">.0295</td>
      <td style="text-align: right">.0290</td>
      <td style="text-align: right">.0321</td>
      <td style="text-align: right">.0169</td>
      <td style="text-align: right">.0212</td>
      <td style="text-align: right"><strong>$0.24</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">.0301</td>
      <td style="text-align: right">.0163</td>
      <td style="text-align: right">.0284</td>
      <td style="text-align: right">.0099</td>
      <td style="text-align: right">.0361</td>
      <td style="text-align: right">.0352</td>
      <td style="text-align: right">.0438</td>
      <td style="text-align: right">.0237</td>
      <td style="text-align: right">.0410</td>
      <td style="text-align: right">.0205</td>
      <td style="text-align: right"><strong>$0.29</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">.0158</td>
      <td style="text-align: right">.0454</td>
      <td style="text-align: right">.0140</td>
      <td style="text-align: right">.0195</td>
      <td style="text-align: right">.0170</td>
      <td style="text-align: right">.0194</td>
      <td style="text-align: right">.0141</td>
      <td style="text-align: right">.0191</td>
      <td style="text-align: right">.0909</td>
      <td style="text-align: right">.0940</td>
      <td style="text-align: right"><strong>$0.35</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">.0415</td>
      <td style="text-align: right">.0447</td>
      <td style="text-align: right">.0600</td>
      <td style="text-align: right">.0633</td>
      <td style="text-align: right">.0407</td>
      <td style="text-align: right">.0331</td>
      <td style="text-align: right">.0426</td>
      <td style="text-align: right">.0337</td>
      <td style="text-align: right">.0394</td>
      <td style="text-align: right">.0271</td>
      <td style="text-align: right"><strong>$0.43</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">.1148</td>
      <td style="text-align: right">.0888</td>
      <td style="text-align: right">.1203</td>
      <td style="text-align: right">.1003</td>
      <td style="text-align: right">.1430</td>
      <td style="text-align: right">.0911</td>
      <td style="text-align: right">.1193</td>
      <td style="text-align: right">.0904</td>
      <td style="text-align: right">.1305</td>
      <td style="text-align: right">.0964</td>
      <td style="text-align: right"><strong>$1.09</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">.0725</td>
      <td style="text-align: right">.1456</td>
      <td style="text-align: right">.1978</td>
      <td style="text-align: right">.0586</td>
      <td style="text-align: right">.2160</td>
      <td style="text-align: right">.1075</td>
      <td style="text-align: right">.0421</td>
      <td style="text-align: right">.0488</td>
      <td style="text-align: right">.4686</td>
      <td style="text-align: right">.1493</td>
      <td style="text-align: right"><strong>$1.51</strong></td>
    </tr>
  </tbody>
</table>



## Observations

**All 10 models solved all 10 parts.** Two needed a second attempt on Day 1 Part 2, and
one had a dirty stop on Day 5 Part 1, but nobody was ejected.

**`claude-haiku-4-5`** — fastest overall at 168s. Five parts solved in ≤16s. In the
Python benchmark it placed second (206s); here it placed first.

**`gpt-5.3-codex`** — 181s total, 6,428 tokens. Fewest output tokens of any model
(next lowest: glm-5 at 7,884). Also the most token-efficient in the Python run.

**`devstral-2512`** — 192s, third place. Won the Python benchmark (205s). Tied with
gpt-5.3-codex for cheapest at $0.21.

**`kimi-coding/k2p5`** — $0.13 total cost, 228s total time. Cheapest model. Was also
cheapest in Python ($0.02).

**`qwen3-coder-next`** — most expensive at $1.51, slowest at 751s. D5P1 alone cost
$0.47 due to a dirty stop. 32,303 total output tokens — 5× more than gpt-5.3-codex.

**`claude-opus-4-6`** — $1.09, second-most expensive. Per-part cost consistently
around $0.10. 250s total.

**Day 1 Part 2** was the only part where any model needed a retry. Both `glm-5` and
`qwen3.5-plus` recovered on the second try, but the retries added 200+ seconds each.

**No model got stuck on Rust-specific issues.** No borrow-checker loops, no lifetime
annotation struggles across the full 10 parts.

## Comparison with Python

| Model | Python time | Rust time | Δ |
| ------:| ----:| ----:| ----:|
| claude-haiku-4-5 | 206s | 168s | −38s |
| gpt-5.3-codex | 266s | 181s | −85s |
| devstral-2512 | 205s | 192s | −13s |
| claude-sonnet-4-6 | 297s | 220s | −77s |
| k2p5 | 240s | 228s | −12s |
| claude-opus-4-6 | 308s | 250s | −58s |
| qwen3.5-plus | 379s | 410s | +31s |
| MiniMax-M2.5 | 574s | 514s | −60s |
| glm-5 | 602s | 518s | −84s |
| qwen3-coder-next | 251s | 751s | +500s |

8 of 10 models were faster in Rust than Python. The two exceptions — `qwen3.5-plus`
and `qwen3-coder-next` — both lost time to retries and dirty stops.

## What's next

The benchmark stopped at Day 5 because Day 6+ inputs and descriptions weren't available yet.

*Benchmarked on 2026-02-27 using [pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent) as the agent harness.*

---

*This post was written with AI assistance.*
