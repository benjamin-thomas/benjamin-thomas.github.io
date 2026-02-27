+++
title = "Benchmarking LLMs on Advent of Code 2025 (Python)"
description = "10 LLMs, AoC 2025 Days 1–5 in Python. First benchmark with full token and cost tracking — and the first one where nobody gets ejected."

[taxonomies]
tags = ["Python", "AI", "Advent of Code"]
+++

Following up on [the Haskell benchmark](@/posts/2026-02-24-aoc-2025-llm-benchmark-haskell.md) and [the OCaml
benchmark](@/posts/2026-02-25-aoc-2025-llm-benchmark-ocaml.md), I ran the same orchestration setup on
the same AoC 2025 Days 1–5 puzzles — this time in **Python**.

This is also the first run with full **token usage and API cost tracking** per part, which
adds a new angle beyond raw wall-clock time.

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

A wrong model ID (`claude-3-5-haiku-latest`) was accidentally in the enabled model list at
the start. It was caught immediately, killed, and `claude-haiku-4-5` was launched as a
replacement, missing only Day 1 Part 1 of the original session. Its D1P1 was run separately
and produced the right answer in 9s.

## Ejections

**None.** All 10 models solved all 10 parts correctly on the first attempt. This is the
first benchmark in this series with a perfect sweep.

## Results (Days 1–5)

### Per-task leaderboards

<br>

#### Day 1 Part 1 — Dial rotation counting

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 9s |
| mistral/devstral-2512 | 23s |
| kimi-coding/k2p5 | 27s |
| alibaba/qwen3-coder-next | 28s |
| anthropic/claude-sonnet-4-6 | 29s |
| anthropic/claude-opus-4-6 | 30s |
| alibaba/qwen3.5-plus | 30s |
| openai-codex/gpt-5.3-codex | 36s |
| zai/glm-5 | 37s |
| minimax/MiniMax-M2.5 | 60s |

<br><br>

#### Day 1 Part 2 — Counting zero-crossings during dial rotation

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 13s |
| anthropic/claude-haiku-4-5 | 18s |
| openai-codex/gpt-5.3-codex | 20s |
| kimi-coding/k2p5 | 21s |
| anthropic/claude-sonnet-4-6 | 26s |
| anthropic/claude-opus-4-6 | 26s |
| alibaba/qwen3-coder-next | 42s |
| zai/glm-5 | 56s |
| alibaba/qwen3.5-plus | 73s |
| minimax/MiniMax-M2.5 | 81s |

<br><br>

#### Day 2 Part 1 — Summing repeated-digit IDs in ranges

| Model | Time |
| ------:| ----:|
| alibaba/qwen3-coder-next | 22s |
| mistral/devstral-2512 | 23s |
| anthropic/claude-haiku-4-5 | 24s |
| openai-codex/gpt-5.3-codex | 26s |
| kimi-coding/k2p5 | 28s |
| alibaba/qwen3.5-plus | 30s |
| zai/glm-5 | 38s |
| anthropic/claude-sonnet-4-6 | 43s |
| anthropic/claude-opus-4-6 | 50s |
| minimax/MiniMax-M2.5 | 67s |

<br><br>

#### Day 2 Part 2 — Repeated-pattern IDs (any repeat count)

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 14s |
| alibaba/qwen3-coder-next | 17s |
| anthropic/claude-haiku-4-5 | 18s |
| kimi-coding/k2p5 | 24s |
| anthropic/claude-sonnet-4-6 | 25s |
| openai-codex/gpt-5.3-codex | 27s |
| zai/glm-5 | 30s |
| minimax/MiniMax-M2.5 | 33s |
| anthropic/claude-opus-4-6 | 41s |
| alibaba/qwen3.5-plus | 48s |

<br><br>

#### Day 3 Part 1 — Maximizing 2-digit joltage from battery banks

| Model | Time |
| ------:| ----:|
| kimi-coding/k2p5 | 21s |
| mistral/devstral-2512 | 24s |
| alibaba/qwen3-coder-next | 25s |
| anthropic/claude-sonnet-4-6 | 28s |
| anthropic/claude-haiku-4-5 | 30s |
| anthropic/claude-opus-4-6 | 31s |
| openai-codex/gpt-5.3-codex | 31s |
| alibaba/qwen3.5-plus | 31s |
| zai/glm-5 | 71s |
| minimax/MiniMax-M2.5 | 72s |

<br><br>

#### Day 3 Part 2 — Maximizing 12-digit joltage from battery banks

| Model | Time |
| ------:| ----:|
| kimi-coding/k2p5 | 19s |
| anthropic/claude-haiku-4-5 | 21s |
| mistral/devstral-2512 | 21s |
| alibaba/qwen3-coder-next | 21s |
| alibaba/qwen3.5-plus | 24s |
| anthropic/claude-sonnet-4-6 | 25s |
| openai-codex/gpt-5.3-codex | 25s |
| anthropic/claude-opus-4-6 | 28s |
| zai/glm-5 | 33s |
| minimax/MiniMax-M2.5 | 56s |

<br><br>

#### Day 4 Part 1 — Grid neighbor counting (accessible paper rolls)

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 21s |
| mistral/devstral-2512 | 22s |
| alibaba/qwen3-coder-next | 23s |
| kimi-coding/k2p5 | 27s |
| anthropic/claude-opus-4-6 | 29s |
| openai-codex/gpt-5.3-codex | 31s |
| zai/glm-5 | 31s |
| alibaba/qwen3.5-plus | 40s |
| anthropic/claude-sonnet-4-6 | 51s |
| minimax/MiniMax-M2.5 | 59s |

<br><br>

#### Day 4 Part 2 — Iterative grid removal simulation

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 14s |
| alibaba/qwen3-coder-next | 18s |
| anthropic/claude-haiku-4-5 | 19s |
| openai-codex/gpt-5.3-codex | 21s |
| anthropic/claude-sonnet-4-6 | 23s |
| anthropic/claude-opus-4-6 | 23s |
| kimi-coding/k2p5 | 30s |
| alibaba/qwen3.5-plus | 47s |
| minimax/MiniMax-M2.5 | 52s |
| zai/glm-5 | 217s |

<br><br>

#### Day 5 Part 1 — Range membership checking

| Model | Time |
| ------:| ----:|
| kimi-coding/k2p5 | 22s |
| mistral/devstral-2512 | 22s |
| openai-codex/gpt-5.3-codex | 23s |
| anthropic/claude-haiku-4-5 | 25s |
| anthropic/claude-sonnet-4-6 | 25s |
| alibaba/qwen3.5-plus | 26s |
| anthropic/claude-opus-4-6 | 27s |
| alibaba/qwen3-coder-next | 27s |
| zai/glm-5 | 43s |
| minimax/MiniMax-M2.5 | 53s |

<br><br>

#### Day 5 Part 2 — Counting total fresh IDs from overlapping ranges

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 21s |
| kimi-coding/k2p5 | 21s |
| anthropic/claude-sonnet-4-6 | 22s |
| anthropic/claude-opus-4-6 | 23s |
| openai-codex/gpt-5.3-codex | 26s |
| alibaba/qwen3-coder-next | 28s |
| mistral/devstral-2512 | 29s |
| alibaba/qwen3.5-plus | 30s |
| minimax/MiniMax-M2.5 | 41s |
| zai/glm-5 | 46s |

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
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right">13s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">29s</td>
      <td style="text-align: right"><strong>205s</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">9s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">25s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right"><strong>206s</strong></td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right"><strong>240s</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">42s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">25s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right"><strong>251s</strong></td>
    </tr>
    <tr>
      <td>openai-codex/gpt-5.3-codex</td>
      <td style="text-align: right">36s</td>
      <td style="text-align: right">20s</td>
      <td style="text-align: right">26s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">31s</td>
      <td style="text-align: right">25s</td>
      <td style="text-align: right">31s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right">26s</td>
      <td style="text-align: right"><strong>266s</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">29s</td>
      <td style="text-align: right">26s</td>
      <td style="text-align: right">43s</td>
      <td style="text-align: right">25s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">25s</td>
      <td style="text-align: right">51s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right">25s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right"><strong>297s</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">26s</td>
      <td style="text-align: right">50s</td>
      <td style="text-align: right">41s</td>
      <td style="text-align: right">31s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">29s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right"><strong>308s</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">73s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">48s</td>
      <td style="text-align: right">31s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">40s</td>
      <td style="text-align: right">47s</td>
      <td style="text-align: right">26s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right"><strong>379s</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">60s</td>
      <td style="text-align: right">81s</td>
      <td style="text-align: right">67s</td>
      <td style="text-align: right">33s</td>
      <td style="text-align: right">72s</td>
      <td style="text-align: right">56s</td>
      <td style="text-align: right">59s</td>
      <td style="text-align: right">52s</td>
      <td style="text-align: right">53s</td>
      <td style="text-align: right">41s</td>
      <td style="text-align: right"><strong>574s</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">37s</td>
      <td style="text-align: right">56s</td>
      <td style="text-align: right">38s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">71s</td>
      <td style="text-align: right">33s</td>
      <td style="text-align: right">31s</td>
      <td style="text-align: right">217s</td>
      <td style="text-align: right">43s</td>
      <td style="text-align: right">46s</td>
      <td style="text-align: right"><strong>602s</strong></td>
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
      <td style="text-align: right">420</td>
      <td style="text-align: right">560</td>
      <td style="text-align: right">482</td>
      <td style="text-align: right">476</td>
      <td style="text-align: right">563</td>
      <td style="text-align: right">617</td>
      <td style="text-align: right">583</td>
      <td style="text-align: right">807</td>
      <td style="text-align: right">417</td>
      <td style="text-align: right">501</td>
      <td style="text-align: right"><strong>5,426</strong></td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">582</td>
      <td style="text-align: right">798</td>
      <td style="text-align: right">550</td>
      <td style="text-align: right">583</td>
      <td style="text-align: right">438</td>
      <td style="text-align: right">571</td>
      <td style="text-align: right">511</td>
      <td style="text-align: right">612</td>
      <td style="text-align: right">500</td>
      <td style="text-align: right">568</td>
      <td style="text-align: right"><strong>5,713</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">454</td>
      <td style="text-align: right">1,316</td>
      <td style="text-align: right">603</td>
      <td style="text-align: right">536</td>
      <td style="text-align: right">1,626</td>
      <td style="text-align: right">507</td>
      <td style="text-align: right">521</td>
      <td style="text-align: right">576</td>
      <td style="text-align: right">788</td>
      <td style="text-align: right">785</td>
      <td style="text-align: right"><strong>7,712</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">528</td>
      <td style="text-align: right">849</td>
      <td style="text-align: right">683</td>
      <td style="text-align: right">539</td>
      <td style="text-align: right">860</td>
      <td style="text-align: right">988</td>
      <td style="text-align: right">664</td>
      <td style="text-align: right">826</td>
      <td style="text-align: right">728</td>
      <td style="text-align: right">1,460</td>
      <td style="text-align: right"><strong>8,125</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">671</td>
      <td style="text-align: right">897</td>
      <td style="text-align: right">1,508</td>
      <td style="text-align: right">1,031</td>
      <td style="text-align: right">780</td>
      <td style="text-align: right">776</td>
      <td style="text-align: right">783</td>
      <td style="text-align: right">794</td>
      <td style="text-align: right">682</td>
      <td style="text-align: right">658</td>
      <td style="text-align: right"><strong>8,580</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">592</td>
      <td style="text-align: right">852</td>
      <td style="text-align: right">2,165</td>
      <td style="text-align: right">1,882</td>
      <td style="text-align: right">728</td>
      <td style="text-align: right">763</td>
      <td style="text-align: right">737</td>
      <td style="text-align: right">742</td>
      <td style="text-align: right">663</td>
      <td style="text-align: right">650</td>
      <td style="text-align: right"><strong>9,774</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">843</td>
      <td style="text-align: right">798</td>
      <td style="text-align: right">1,034</td>
      <td style="text-align: right">897</td>
      <td style="text-align: right">1,940</td>
      <td style="text-align: right">1,099</td>
      <td style="text-align: right">907</td>
      <td style="text-align: right">970</td>
      <td style="text-align: right">1,410</td>
      <td style="text-align: right">1,365</td>
      <td style="text-align: right"><strong>11,263</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">956</td>
      <td style="text-align: right">4,823</td>
      <td style="text-align: right">1,152</td>
      <td style="text-align: right">953</td>
      <td style="text-align: right">800</td>
      <td style="text-align: right">737</td>
      <td style="text-align: right">907</td>
      <td style="text-align: right">1,019</td>
      <td style="text-align: right">718</td>
      <td style="text-align: right">1,022</td>
      <td style="text-align: right"><strong>13,087</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">1,305</td>
      <td style="text-align: right">2,853</td>
      <td style="text-align: right">1,333</td>
      <td style="text-align: right">947</td>
      <td style="text-align: right">1,973</td>
      <td style="text-align: right">2,249</td>
      <td style="text-align: right">1,068</td>
      <td style="text-align: right">1,046</td>
      <td style="text-align: right">1,049</td>
      <td style="text-align: right">940</td>
      <td style="text-align: right"><strong>14,763</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">1,388</td>
      <td style="text-align: right">7,840</td>
      <td style="text-align: right">1,537</td>
      <td style="text-align: right">3,484</td>
      <td style="text-align: right">2,188</td>
      <td style="text-align: right">1,031</td>
      <td style="text-align: right">1,414</td>
      <td style="text-align: right">1,056</td>
      <td style="text-align: right">1,141</td>
      <td style="text-align: right">1,582</td>
      <td style="text-align: right"><strong>22,661</strong></td>
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
      <td style="text-align: right">.0049</td>
      <td style="text-align: right">.0019</td>
      <td style="text-align: right">.0020</td>
      <td style="text-align: right">.0017</td>
      <td style="text-align: right">.0015</td>
      <td style="text-align: right">.0015</td>
      <td style="text-align: right">.0016</td>
      <td style="text-align: right">.0018</td>
      <td style="text-align: right">.0016</td>
      <td style="text-align: right">.0015</td>
      <td style="text-align: right"><strong>$0.02</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">.0079</td>
      <td style="text-align: right">.0092</td>
      <td style="text-align: right">.0078</td>
      <td style="text-align: right">.0093</td>
      <td style="text-align: right">.0072</td>
      <td style="text-align: right">.0092</td>
      <td style="text-align: right">.0064</td>
      <td style="text-align: right">.0104</td>
      <td style="text-align: right">.0076</td>
      <td style="text-align: right">.0155</td>
      <td style="text-align: right"><strong>$0.09</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">.0060</td>
      <td style="text-align: right">.0132</td>
      <td style="text-align: right">.0072</td>
      <td style="text-align: right">.0074</td>
      <td style="text-align: right">.0385</td>
      <td style="text-align: right">.0226</td>
      <td style="text-align: right">.0055</td>
      <td style="text-align: right">.0074</td>
      <td style="text-align: right">.0072</td>
      <td style="text-align: right">.0087</td>
      <td style="text-align: right"><strong>$0.12</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">.0224</td>
      <td style="text-align: right">.0297</td>
      <td style="text-align: right">.0060</td>
      <td style="text-align: right">.0065</td>
      <td style="text-align: right">.0234</td>
      <td style="text-align: right">.0491</td>
      <td style="text-align: right">.0053</td>
      <td style="text-align: right">.0089</td>
      <td style="text-align: right">.0168</td>
      <td style="text-align: right">.0211</td>
      <td style="text-align: right"><strong>$0.19</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">.0224</td>
      <td style="text-align: right">.0122</td>
      <td style="text-align: right">.0273</td>
      <td style="text-align: right">.0092</td>
      <td style="text-align: right">.0288</td>
      <td style="text-align: right">.0116</td>
      <td style="text-align: right">.0233</td>
      <td style="text-align: right">.0179</td>
      <td style="text-align: right">.0330</td>
      <td style="text-align: right">.0172</td>
      <td style="text-align: right"><strong>$0.20</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">.0110</td>
      <td style="text-align: right">.0308</td>
      <td style="text-align: right">.0119</td>
      <td style="text-align: right">.0273</td>
      <td style="text-align: right">.0127</td>
      <td style="text-align: right">.0141</td>
      <td style="text-align: right">.0336</td>
      <td style="text-align: right">.0425</td>
      <td style="text-align: right">.0094</td>
      <td style="text-align: right">.0161</td>
      <td style="text-align: right"><strong>$0.21</strong></td>
    </tr>
    <tr>
      <td>openai-codex/gpt-5.3-codex</td>
      <td style="text-align: right">.0178</td>
      <td style="text-align: right">.0185</td>
      <td style="text-align: right">.0163</td>
      <td style="text-align: right">.0167</td>
      <td style="text-align: right">.0518</td>
      <td style="text-align: right">.0240</td>
      <td style="text-align: right">.0340</td>
      <td style="text-align: right">.0465</td>
      <td style="text-align: right">.0153</td>
      <td style="text-align: right">.0124</td>
      <td style="text-align: right"><strong>$0.25</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">.0340</td>
      <td style="text-align: right">.0272</td>
      <td style="text-align: right">.0519</td>
      <td style="text-align: right">.0311</td>
      <td style="text-align: right">.0349</td>
      <td style="text-align: right">.0243</td>
      <td style="text-align: right">.0348</td>
      <td style="text-align: right">.0272</td>
      <td style="text-align: right">.0323</td>
      <td style="text-align: right">.0207</td>
      <td style="text-align: right"><strong>$0.32</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">.0273</td>
      <td style="text-align: right">.0560</td>
      <td style="text-align: right">.0104</td>
      <td style="text-align: right">.0123</td>
      <td style="text-align: right">.0482</td>
      <td style="text-align: right">.0599</td>
      <td style="text-align: right">.0261</td>
      <td style="text-align: right">.0344</td>
      <td style="text-align: right">.0525</td>
      <td style="text-align: right">.0741</td>
      <td style="text-align: right"><strong>$0.40</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">.1090</td>
      <td style="text-align: right">.0809</td>
      <td style="text-align: right">.1351</td>
      <td style="text-align: right">.0803</td>
      <td style="text-align: right">.1089</td>
      <td style="text-align: right">.0942</td>
      <td style="text-align: right">.1088</td>
      <td style="text-align: right">.0794</td>
      <td style="text-align: right">.1029</td>
      <td style="text-align: right">.1030</td>
      <td style="text-align: right"><strong>$1.00</strong></td>
    </tr>
  </tbody>
</table>



## Observations

**All 10 models passed all 10 parts on the first attempt.** In the OCaml run, 5 of 9 models
failed at Day 1 Part 2. Here, nobody failed anything — no retries needed across the board.

**`devstral-2512` is the fastest overall at 205s.** Fastest or joint-fastest on 6 of 10
parts. 8,125 output tokens total.

**`claude-haiku-4-5`** — 206s total, close behind. Higher token count (11,263) relative
to its speed.

**`gpt-5.3-codex`** — fewest output tokens: 5,426 total across 10 parts. $0.25 total
cost, 266s total time.

**`kimi-coding/k2p5`** — cheapest at ~$0.02. 5,713 tokens, 240s total.

**`qwen3.5-plus`** — most tokens: 22,661 total. The D1P2 spike (7,840 tokens for a
single part) stands out. Total cost of $0.21, kept low by per-token pricing.

**`glm-5`** — 217s on D4P2, while others solved it in 14–52s. Token usage on that part
(576 tok) was normal, so the time was spent elsewhere (execution retries, perhaps).

**`claude-opus-4-6`** — $1.00 total across all 10 parts. Not the slowest (308s), not the
most verbose (9,774 tok), but the most expensive at roughly $0.10 per part.

**`qwen3-coder-next`** — 251s total, but $0.40 (second-highest cost). The D1P2 token
spike (4,823) accounts for much of that.

## What's next

Future runs in other languages should show whether these results hold or whether the
leaderboard reshuffles when the target language changes.

Token and cost tracking will continue across all future benchmarks.

*Benchmarked on 2026-02-25 using [pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent) as the agent harness.*

---

*This post was written with AI assistance.*
