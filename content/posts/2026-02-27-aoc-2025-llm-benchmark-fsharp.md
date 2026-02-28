+++
title = "Benchmarking LLMs on Advent of Code 2025 (F#)"
description = "10 LLMs, AoC 2025 Days 1–5 in F#. All ten models completed every part — the fourth perfect-completion language alongside Python, Ruby, and Elm."

[taxonomies]
tags = ["F#", "AI", "Advent of Code"]
+++

Following up on [the Haskell benchmark](@/posts/2026-02-24-aoc-2025-llm-benchmark-haskell.md), [the OCaml
benchmark](@/posts/2026-02-25-aoc-2025-llm-benchmark-ocaml.md), [the Python
benchmark](@/posts/2026-02-25-aoc-2025-llm-benchmark-python.md), [the ReScript
benchmark](@/posts/2026-02-26-aoc-2025-llm-benchmark-rescript.md), [the Ruby
benchmark](@/posts/2026-02-26-aoc-2025-llm-benchmark-ruby.md), [the Elixir
benchmark](@/posts/2026-02-26-aoc-2025-llm-benchmark-elixir.md), [the Java
benchmark](@/posts/2026-02-26-aoc-2025-llm-benchmark-java.md), and [the Elm
benchmark](@/posts/2026-02-26-aoc-2025-llm-benchmark-elm.md), I ran the same AoC 2025 Days 1–5
setup in **F#**.

F# occupies an interesting middle ground. It's a functional-first language on .NET — strongly
typed with type inference, pattern matching, and pipelines, but with full access to the
imperative .NET ecosystem when needed. It sees real production use but isn't anywhere near as
common as C# or Python in training data. No scaffold was provided; each model had to figure
out `dotnet fsi` scripting or full project setup on its own.

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

None. **All 10 models completed all 10 parts.** F# joins Python, Ruby, and Elm as the
fourth language with a perfect completion rate.

Day 1 Part 2 was the only real trouble spot. Four models needed retries there —
`gpt-5.3-codex`, `devstral-2512`, and `MiniMax-M2.5` each needed two attempts, while
`qwen3-coder-next` took three. Beyond that, `glm-5` had a dirty retry on Day 3 Part 1
(it wrote a premature answer while still working). Every other part was a clean first-try
solve across the board.

## Results (Days 1–5)

### Per-task leaderboards

<br>

#### Day 1 Part 1 — Dial rotation counting

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 12s |
| anthropic/claude-sonnet-4-6 | 17s |
| anthropic/claude-haiku-4-5 | 19s |
| openai-codex/gpt-5.3-codex | 20s |
| kimi-coding/k2p5 | 24s |
| anthropic/claude-opus-4-6 | 27s |
| zai/glm-5 | 40s |
| alibaba/qwen3-coder-next | 42s |
| minimax/MiniMax-M2.5 | 83s |
| alibaba/qwen3.5-plus | 86s |

<br><br>

#### Day 1 Part 2 — Counting zero-crossings during dial rotation

| Model | Time | Result |
| ------:| ----:| :--: |
| anthropic/claude-haiku-4-5 | 10s | ✓ |
| anthropic/claude-sonnet-4-6 | 28s | ✓ |
| zai/glm-5 | 30s | ✓ |
| anthropic/claude-opus-4-6 | 33s | ✓ |
| kimi-coding/k2p5 | 65s | ✓ |
| alibaba/qwen3.5-plus | 73s | ✓ |
| openai-codex/gpt-5.3-codex | 315s | ✓ (2nd try) |
| mistral/devstral-2512 | 342s | ✓ (2nd try) |
| minimax/MiniMax-M2.5 | 547s | ✓ (2nd try) |
| alibaba/qwen3-coder-next | 625s | ✓ (3rd try) |

<br><br>

#### Day 2 Part 1 — Summing repeated-digit IDs in ranges

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 30s |
| anthropic/claude-sonnet-4-6 | 30s |
| anthropic/claude-opus-4-6 | 32s |
| openai-codex/gpt-5.3-codex | 37s |
| zai/glm-5 | 38s |
| mistral/devstral-2512 | 39s |
| alibaba/qwen3-coder-next | 43s |
| minimax/MiniMax-M2.5 | 79s |
| alibaba/qwen3.5-plus | 85s |
| kimi-coding/k2p5 | 155s |

<br><br>

#### Day 2 Part 2 — Repeated-pattern IDs (any repeat count)

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 13s |
| openai-codex/gpt-5.3-codex | 16s |
| alibaba/qwen3.5-plus | 17s |
| alibaba/qwen3-coder-next | 21s |
| mistral/devstral-2512 | 28s |
| anthropic/claude-sonnet-4-6 | 29s |
| anthropic/claude-opus-4-6 | 33s |
| zai/glm-5 | 36s |
| minimax/MiniMax-M2.5 | 48s |
| kimi-coding/k2p5 | 76s |

<br><br>

#### Day 3 Part 1 — Maximizing 2-digit joltage from battery banks

| Model | Time | Result |
| ------:| ----:| :--: |
| anthropic/claude-sonnet-4-6 | 18s | ✓ |
| kimi-coding/k2p5 | 18s | ✓ |
| anthropic/claude-opus-4-6 | 25s | ✓ |
| openai-codex/gpt-5.3-codex | 26s | ✓ |
| alibaba/qwen3-coder-next | 29s | ✓ |
| anthropic/claude-haiku-4-5 | 30s | ✓ |
| alibaba/qwen3.5-plus | 45s | ✓ |
| minimax/MiniMax-M2.5 | 51s | ✓ |
| mistral/devstral-2512 | 64s | ✓ |
| zai/glm-5 | 178s | ✓ (dirty retry) |

<br><br>

#### Day 3 Part 2 — Maximizing 12-digit joltage from battery banks

| Model | Time |
| ------:| ----:|
| openai-codex/gpt-5.3-codex | 14s |
| kimi-coding/k2p5 | 18s |
| anthropic/claude-sonnet-4-6 | 20s |
| alibaba/qwen3.5-plus | 22s |
| anthropic/claude-opus-4-6 | 24s |
| alibaba/qwen3-coder-next | 25s |
| zai/glm-5 | 33s |
| minimax/MiniMax-M2.5 | 37s |
| anthropic/claude-haiku-4-5 | 40s |
| mistral/devstral-2512 | 44s |

<br><br>

#### Day 4 Part 1 — Grid neighbor counting (accessible paper rolls)

| Model | Time |
| ------:| ----:|
| alibaba/qwen3-coder-next | 10s |
| alibaba/qwen3.5-plus | 17s |
| openai-codex/gpt-5.3-codex | 18s |
| anthropic/claude-sonnet-4-6 | 20s |
| mistral/devstral-2512 | 21s |
| anthropic/claude-haiku-4-5 | 24s |
| anthropic/claude-opus-4-6 | 29s |
| kimi-coding/k2p5 | 29s |
| zai/glm-5 | 37s |
| minimax/MiniMax-M2.5 | 82s |

<br><br>

#### Day 4 Part 2 — Iterative grid removal simulation

| Model | Time |
| ------:| ----:|
| alibaba/qwen3-coder-next | 8s |
| anthropic/claude-haiku-4-5 | 14s |
| alibaba/qwen3.5-plus | 17s |
| anthropic/claude-sonnet-4-6 | 18s |
| openai-codex/gpt-5.3-codex | 19s |
| anthropic/claude-opus-4-6 | 22s |
| mistral/devstral-2512 | 24s |
| kimi-coding/k2p5 | 34s |
| zai/glm-5 | 37s |
| minimax/MiniMax-M2.5 | 69s |

<br><br>

#### Day 5 Part 1 — Range membership checking

| Model | Time |
| ------:| ----:|
| openai-codex/gpt-5.3-codex | 16s |
| anthropic/claude-sonnet-4-6 | 23s |
| anthropic/claude-opus-4-6 | 27s |
| zai/glm-5 | 29s |
| kimi-coding/k2p5 | 30s |
| mistral/devstral-2512 | 31s |
| alibaba/qwen3.5-plus | 31s |
| anthropic/claude-haiku-4-5 | 44s |
| minimax/MiniMax-M2.5 | 45s |
| alibaba/qwen3-coder-next | 58s |

<br><br>

#### Day 5 Part 2 — Counting total fresh IDs from overlapping ranges

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 11s |
| openai-codex/gpt-5.3-codex | 12s |
| anthropic/claude-sonnet-4-6 | 13s |
| anthropic/claude-haiku-4-5 | 15s |
| anthropic/claude-opus-4-6 | 18s |
| kimi-coding/k2p5 | 21s |
| alibaba/qwen3.5-plus | 27s |
| alibaba/qwen3-coder-next | 27s |
| zai/glm-5 | 37s |
| minimax/MiniMax-M2.5 | 37s |

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
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">29s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">20s</td>
      <td style="text-align: right">20s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right">13s</td>
      <td style="text-align: right"><strong>216s</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">10s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">13s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">40s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">44s</td>
      <td style="text-align: right">15s</td>
      <td style="text-align: right"><strong>239s</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">33s</td>
      <td style="text-align: right">32s</td>
      <td style="text-align: right">33s</td>
      <td style="text-align: right">25s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">29s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right"><strong>270s</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">86s</td>
      <td style="text-align: right">73s</td>
      <td style="text-align: right">85s</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">45s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">31s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right"><strong>420s</strong></td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">65s</td>
      <td style="text-align: right">155s</td>
      <td style="text-align: right">76s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">29s</td>
      <td style="text-align: right">34s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right"><strong>470s</strong></td>
    </tr>
    <tr>
      <td>openai-codex/gpt-5.3-codex</td>
      <td style="text-align: right">20s</td>
      <td style="text-align: right">315s</td>
      <td style="text-align: right">37s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">26s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">12s</td>
      <td style="text-align: right"><strong>493s</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">40s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">38s</td>
      <td style="text-align: right">36s</td>
      <td style="text-align: right">178s</td>
      <td style="text-align: right">33s</td>
      <td style="text-align: right">37s</td>
      <td style="text-align: right">37s</td>
      <td style="text-align: right">29s</td>
      <td style="text-align: right">37s</td>
      <td style="text-align: right"><strong>495s</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">12s</td>
      <td style="text-align: right">342s</td>
      <td style="text-align: right">39s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">64s</td>
      <td style="text-align: right">44s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">31s</td>
      <td style="text-align: right">11s</td>
      <td style="text-align: right"><strong>616s</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">42s</td>
      <td style="text-align: right">625s</td>
      <td style="text-align: right">43s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">29s</td>
      <td style="text-align: right">25s</td>
      <td style="text-align: right">10s</td>
      <td style="text-align: right">8s</td>
      <td style="text-align: right">58s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right"><strong>888s</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">83s</td>
      <td style="text-align: right">547s</td>
      <td style="text-align: right">79s</td>
      <td style="text-align: right">48s</td>
      <td style="text-align: right">51s</td>
      <td style="text-align: right">37s</td>
      <td style="text-align: right">82s</td>
      <td style="text-align: right">69s</td>
      <td style="text-align: right">45s</td>
      <td style="text-align: right">37s</td>
      <td style="text-align: right"><strong>1078s</strong></td>
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
      <td style="text-align: right">709</td>
      <td style="text-align: right">1,248</td>
      <td style="text-align: right">1,205</td>
      <td style="text-align: right">553</td>
      <td style="text-align: right">758</td>
      <td style="text-align: right">533</td>
      <td style="text-align: right">547</td>
      <td style="text-align: right">803</td>
      <td style="text-align: right">543</td>
      <td style="text-align: right">517</td>
      <td style="text-align: right"><strong>7,416</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">861</td>
      <td style="text-align: right">609</td>
      <td style="text-align: right">841</td>
      <td style="text-align: right">767</td>
      <td style="text-align: right">3,630</td>
      <td style="text-align: right">648</td>
      <td style="text-align: right">777</td>
      <td style="text-align: right">666</td>
      <td style="text-align: right">609</td>
      <td style="text-align: right">823</td>
      <td style="text-align: right"><strong>10,231</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">750</td>
      <td style="text-align: right">1,279</td>
      <td style="text-align: right">1,404</td>
      <td style="text-align: right">1,503</td>
      <td style="text-align: right">859</td>
      <td style="text-align: right">932</td>
      <td style="text-align: right">855</td>
      <td style="text-align: right">873</td>
      <td style="text-align: right">1,184</td>
      <td style="text-align: right">695</td>
      <td style="text-align: right"><strong>10,334</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">1,054</td>
      <td style="text-align: right">1,736</td>
      <td style="text-align: right">1,438</td>
      <td style="text-align: right">1,429</td>
      <td style="text-align: right">961</td>
      <td style="text-align: right">1,015</td>
      <td style="text-align: right">1,122</td>
      <td style="text-align: right">899</td>
      <td style="text-align: right">1,030</td>
      <td style="text-align: right">806</td>
      <td style="text-align: right"><strong>11,490</strong></td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">639</td>
      <td style="text-align: right">2,636</td>
      <td style="text-align: right">4,824</td>
      <td style="text-align: right">2,640</td>
      <td style="text-align: right">677</td>
      <td style="text-align: right">868</td>
      <td style="text-align: right">903</td>
      <td style="text-align: right">1,225</td>
      <td style="text-align: right">850</td>
      <td style="text-align: right">616</td>
      <td style="text-align: right"><strong>15,878</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">1,559</td>
      <td style="text-align: right">898</td>
      <td style="text-align: right">2,339</td>
      <td style="text-align: right">1,037</td>
      <td style="text-align: right">2,560</td>
      <td style="text-align: right">3,326</td>
      <td style="text-align: right">1,962</td>
      <td style="text-align: right">1,131</td>
      <td style="text-align: right">3,864</td>
      <td style="text-align: right">1,139</td>
      <td style="text-align: right"><strong>19,815</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">618</td>
      <td style="text-align: right">5,672</td>
      <td style="text-align: right">3,459</td>
      <td style="text-align: right">2,511</td>
      <td style="text-align: right">4,324</td>
      <td style="text-align: right">2,710</td>
      <td style="text-align: right">1,560</td>
      <td style="text-align: right">3,129</td>
      <td style="text-align: right">2,437</td>
      <td style="text-align: right">790</td>
      <td style="text-align: right"><strong>27,210</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">4,919</td>
      <td style="text-align: right">7,012</td>
      <td style="text-align: right">6,106</td>
      <td style="text-align: right">1,138</td>
      <td style="text-align: right">3,165</td>
      <td style="text-align: right">1,430</td>
      <td style="text-align: right">1,198</td>
      <td style="text-align: right">1,160</td>
      <td style="text-align: right">2,158</td>
      <td style="text-align: right">2,161</td>
      <td style="text-align: right"><strong>30,447</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">2,481</td>
      <td style="text-align: right">18,006</td>
      <td style="text-align: right">2,230</td>
      <td style="text-align: right">1,060</td>
      <td style="text-align: right">1,720</td>
      <td style="text-align: right">993</td>
      <td style="text-align: right">2,007</td>
      <td style="text-align: right">2,514</td>
      <td style="text-align: right">991</td>
      <td style="text-align: right">1,482</td>
      <td style="text-align: right"><strong>33,484</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">3,355</td>
      <td style="text-align: right">31,718</td>
      <td style="text-align: right">2,426</td>
      <td style="text-align: right">2,066</td>
      <td style="text-align: right">1,391</td>
      <td style="text-align: right">1,300</td>
      <td style="text-align: right">819</td>
      <td style="text-align: right">803</td>
      <td style="text-align: right">4,027</td>
      <td style="text-align: right">1,547</td>
      <td style="text-align: right"><strong>49,452</strong></td>
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
      <td style="text-align: right">.0091</td>
      <td style="text-align: right">.0122</td>
      <td style="text-align: right">.0228</td>
      <td style="text-align: right">.0165</td>
      <td style="text-align: right">.0100</td>
      <td style="text-align: right">.0095</td>
      <td style="text-align: right">.0117</td>
      <td style="text-align: right">.0114</td>
      <td style="text-align: right">.0040</td>
      <td style="text-align: right">.0037</td>
      <td style="text-align: right"><strong>$0.11</strong></td>
    </tr>
    <tr>
      <td>openai-codex/gpt-5.3-codex</td>
      <td style="text-align: right">.0291</td>
      <td style="text-align: right">.0363</td>
      <td style="text-align: right">.0408</td>
      <td style="text-align: right">.0168</td>
      <td style="text-align: right">.0352</td>
      <td style="text-align: right">.0158</td>
      <td style="text-align: right">.0187</td>
      <td style="text-align: right">.0284</td>
      <td style="text-align: right">.0220</td>
      <td style="text-align: right">.0133</td>
      <td style="text-align: right"><strong>$0.26</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">.0279</td>
      <td style="text-align: right">.0186</td>
      <td style="text-align: right">.0092</td>
      <td style="text-align: right">.0086</td>
      <td style="text-align: right">.0720</td>
      <td style="text-align: right">.0226</td>
      <td style="text-align: right">.0304</td>
      <td style="text-align: right">.0219</td>
      <td style="text-align: right">.0408</td>
      <td style="text-align: right">.0283</td>
      <td style="text-align: right"><strong>$0.28</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">.0352</td>
      <td style="text-align: right">.0098</td>
      <td style="text-align: right">.0402</td>
      <td style="text-align: right">.0114</td>
      <td style="text-align: right">.0469</td>
      <td style="text-align: right">.0337</td>
      <td style="text-align: right">.0372</td>
      <td style="text-align: right">.0134</td>
      <td style="text-align: right">.0638</td>
      <td style="text-align: right">.0175</td>
      <td style="text-align: right"><strong>$0.31</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">.0355</td>
      <td style="text-align: right">.0349</td>
      <td style="text-align: right">.0489</td>
      <td style="text-align: right">.0458</td>
      <td style="text-align: right">.0361</td>
      <td style="text-align: right">.0275</td>
      <td style="text-align: right">.0362</td>
      <td style="text-align: right">.0288</td>
      <td style="text-align: right">.0455</td>
      <td style="text-align: right">.0214</td>
      <td style="text-align: right"><strong>$0.36</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">.0081</td>
      <td style="text-align: right">.0528</td>
      <td style="text-align: right">.0502</td>
      <td style="text-align: right">.0463</td>
      <td style="text-align: right">.0828</td>
      <td style="text-align: right">.0538</td>
      <td style="text-align: right">.0171</td>
      <td style="text-align: right">.0327</td>
      <td style="text-align: right">.0268</td>
      <td style="text-align: right">.0141</td>
      <td style="text-align: right"><strong>$0.38</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">.0892</td>
      <td style="text-align: right">.0583</td>
      <td style="text-align: right">.0928</td>
      <td style="text-align: right">.0345</td>
      <td style="text-align: right">.0453</td>
      <td style="text-align: right">.0255</td>
      <td style="text-align: right">.0116</td>
      <td style="text-align: right">.0179</td>
      <td style="text-align: right">.0261</td>
      <td style="text-align: right">.0318</td>
      <td style="text-align: right"><strong>$0.43</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">.0696</td>
      <td style="text-align: right">.1855</td>
      <td style="text-align: right">.0209</td>
      <td style="text-align: right">.0132</td>
      <td style="text-align: right">.0171</td>
      <td style="text-align: right">.0192</td>
      <td style="text-align: right">.0435</td>
      <td style="text-align: right">.0555</td>
      <td style="text-align: right">.0166</td>
      <td style="text-align: right">.0282</td>
      <td style="text-align: right"><strong>$0.47</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">.1711</td>
      <td style="text-align: right">.0743</td>
      <td style="text-align: right">.1466</td>
      <td style="text-align: right">.0668</td>
      <td style="text-align: right">.1185</td>
      <td style="text-align: right">.0873</td>
      <td style="text-align: right">.1628</td>
      <td style="text-align: right">.0737</td>
      <td style="text-align: right">.1520</td>
      <td style="text-align: right">.0798</td>
      <td style="text-align: right"><strong>$1.13</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">.0991</td>
      <td style="text-align: right">1.1932</td>
      <td style="text-align: right">.0505</td>
      <td style="text-align: right">.0435</td>
      <td style="text-align: right">.0997</td>
      <td style="text-align: right">.1027</td>
      <td style="text-align: right">.0210</td>
      <td style="text-align: right">.0280</td>
      <td style="text-align: right">.2615</td>
      <td style="text-align: right">.1149</td>
      <td style="text-align: right"><strong>$2.01</strong></td>
    </tr>
  </tbody>
</table>

## Observations

**10/10 completers — zero ejections.** F# joins Python, Ruby, and Elm as the only languages
in this series where every model solved every part.

**`claude-sonnet-4-6`** — fastest overall at 216s. No single part over 30s, never needed a
retry. The most consistent performer in this run, never once stumbling. ~$0.36 total.

**`claude-haiku-4-5`** — second fastest at 239s and remarkably cheap at ~$0.31. Hit a 10s
solve on D1P2 — the single fastest part solve in the entire benchmark. Never needed a
retry.

**`claude-opus-4-6`** — the steadiest clock in the field. Every single part between 18s and
33s, never needed a retry. No part was a blowout but none was slow either. The most expensive
Anthropic model at ~$1.13.

**`kimi-coding/k2p5`** — cheapest at ~$0.11. That's roughly 10× cheaper than Opus for
comparable results. Slow on D2P1 (155s) and D2P2 (76s) but otherwise quick.

**`gpt-5.3-codex`** — fewest tokens: 7,416 total for 10 parts. Incredibly concise. Would
have been a top-3 finisher on time if not for the 315s D1P2 retry that dragged its total
to 493s.

**Day 1 Part 2 was the filter.** Six models solved it instantly; four needed retries. This
was the only part in the entire F# benchmark where any model gave a wrong answer. Whatever
the conceptual shift between Part 1 and Part 2 was, it tripped up the same models that
struggle with Part 2 pivots in other languages.

**`qwen3-coder-next`** — the most extreme profile. Produced the fastest D4P1 (10s) and
D4P2 (8s) solves, but also the most expensive D1P2 at $1.19 and 31,718 tokens after
needing three attempts. Total cost: $2.01, the highest in the field.

**`MiniMax-M2.5`** — slowest overall at 1,078s. D1P2 alone took 547s after a retry. But it
got there in the end, and its per-token pricing kept costs moderate at ~$0.47.

## Cross-language snapshot

| Language | Models completing all 10 parts |
| --------| ------|
| Python | 10/10 |
| Ruby | 10/10 |
| Elm | 10/10 |
| **F#** | **10/10** |
| Java | 9/10 |
| Elixir | 7/10 |
| Haskell | 7/11 |
| OCaml | 5/9 |
| ReScript (run 2) | 2/10 |

F#'s 10/10 was expected more than Elm's — it's a .NET language with decent representation
in training data thanks to the broader .NET ecosystem. Models could reach for imperative
patterns when functional ones didn't work, and `dotnet fsi` provides a frictionless scripting
experience. Still, zero ejections across 10 models and 10 parts is a strong result for a
language that isn't Python or JavaScript.

*Benchmarked on 2026-02-27 using [pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent) as the agent harness.*

---

*This post was written with AI assistance.*
