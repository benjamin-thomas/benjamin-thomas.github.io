+++
title = "Benchmarking LLMs on Advent of Code 2025 (OCaml)"
description = "Same 9 LLMs, same AoC 2025 puzzles — this time in OCaml. How does the leaderboard compare?"

[taxonomies]
tags = ["OCaml", "AI", "Advent of Code"]
+++

Following up on [the Haskell benchmark](@/posts/2026-02-24-aoc-2025-llm-benchmark-haskell.md), I ran the same
orchestration setup on the same AoC 2025 Days 1–5 puzzles — this time requiring solutions in
**OCaml**. The methodology is identical: each model gets an isolated directory, a puzzle
description, and must write its final answer to `ANSWER.txt`. Wrong answer or no answer = ejection.

<!-- more -->

## The contestants

9 models from my enabled model list this run, plus one added retroactively:

| # | Model |
| -:| ------:|
| 1 | `anthropic/claude-opus-4-6` |
| 2 | `anthropic/claude-sonnet-4-6` |
| 3 | `openai-codex/gpt-5.3-codex` |
| 4 | `zai/glm-5` |
| 5 | `minimax/MiniMax-M2.5` |
| 6 | `kimi-coding/k2p5` |
| 7 | `mistral/devstral-2512` |
| 8 | `alibaba/qwen3.5-plus` |
| 9 | `alibaba/qwen3-coder-next` |
| 10 ★ | `anthropic/claude-haiku-4-5` |

★ Added in a separate session after the main benchmark. Since inference is remote, the
timings are directly comparable.

## Ejections

All 5 casualties happened at Day 1 Part 2:

| Model | Ejected at |
| ------:| ----------:|
| `mistral/devstral-2512` | D1P2 |
| `alibaba/qwen3.5-plus` | D1P2 |
| `alibaba/qwen3-coder-next` | D1P2 |
| `kimi-coding/k2p5` | D1P2 |
| `minimax/MiniMax-M2.5` | D1P2 |

Notably, `mistral/devstral-2512` was the fastest model on Day 1 Part 1 (19s) but
failed Part 2. Same thing happened in the Haskell run.

## Results (Days 1–5)

The 4 original survivors, plus `claude-haiku-4-5` (★), went on a perfect streak. All correct, all 10 parts.

<br>

### Per-task leaderboards

<br>

#### Day 1 Part 1 — Dial rotation counting

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 ★ | 13s |
| mistral/devstral-2512 | 19s |
| alibaba/qwen3-coder-next | 20s |
| openai-codex/gpt-5.3-codex | 24s |
| kimi-coding/k2p5 | 24s |
| anthropic/claude-sonnet-4-6 | 26s |
| alibaba/qwen3.5-plus | 34s |
| zai/glm-5 | 35s |
| anthropic/claude-opus-4-6 | 50s |
| minimax/MiniMax-M2.5 | 59s |

<br><br>

#### Day 1 Part 2 — Counting zero-crossings during dial rotation

| Model | Time | |
| ------:| ----:| :-: |
| anthropic/claude-haiku-4-5 ★ | 12s | ✓ |
| anthropic/claude-sonnet-4-6 | 34s | ✓ |
| openai-codex/gpt-5.3-codex | 35s | ✓ |
| anthropic/claude-opus-4-6 | 36s | ✓ |
| zai/glm-5 | 62s | ✓ |
| mistral/devstral-2512 | 51s | ✗ |
| alibaba/qwen3.5-plus | 38s | ✗ |
| alibaba/qwen3-coder-next | 40s | ✗ |
| kimi-coding/k2p5 | 68s | ✗ |
| minimax/MiniMax-M2.5 | 248s | ✗ |

<br><br>

#### Day 2 Part 1 — Summing repeated-digit IDs in ranges

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 ★ | 11s |
| openai-codex/gpt-5.3-codex | 26s |
| anthropic/claude-sonnet-4-6 | 54s |
| anthropic/claude-opus-4-6 | 56s |
| zai/glm-5 | 110s |

<br><br>

#### Day 2 Part 2 — Repeated-pattern IDs (any repeat count)

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 ★ | 14s |
| openai-codex/gpt-5.3-codex | 20s |
| anthropic/claude-opus-4-6 | 39s |
| anthropic/claude-sonnet-4-6 | 154s |
| zai/glm-5 | 236s |

<br><br>

#### Day 3 Part 1 — Maximizing 2-digit joltage from battery banks

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 ★ | 13s |
| openai-codex/gpt-5.3-codex | 24s |
| anthropic/claude-sonnet-4-6 | 30s |
| anthropic/claude-opus-4-6 | 37s |
| zai/glm-5 | 162s |

<br><br>

#### Day 3 Part 2 — Maximizing 12-digit joltage from battery banks

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 ★ | 13s |
| openai-codex/gpt-5.3-codex | 18s |
| anthropic/claude-sonnet-4-6 | 24s |
| anthropic/claude-opus-4-6 | 28s |
| zai/glm-5 | 161s |

<br><br>

#### Day 4 Part 1 — Grid neighbor counting (accessible paper rolls)

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 ★ | 12s |
| anthropic/claude-sonnet-4-6 | 26s |
| openai-codex/gpt-5.3-codex | 26s |
| anthropic/claude-opus-4-6 | 31s |
| zai/glm-5 | 34s |

<br><br>

#### Day 4 Part 2 — Iterative grid removal simulation

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 ★ | 11s |
| openai-codex/gpt-5.3-codex | 18s |
| anthropic/claude-opus-4-6 | 23s |
| anthropic/claude-sonnet-4-6 | 28s |
| zai/glm-5 | 37s |

<br><br>

#### Day 5 Part 1 — Range membership checking

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 ★ | 12s |
| anthropic/claude-sonnet-4-6 | 29s |
| openai-codex/gpt-5.3-codex | 32s |
| anthropic/claude-opus-4-6 | 33s |
| zai/glm-5 | 108s |

<br><br>

#### Day 5 Part 2 — Counting total fresh IDs from overlapping ranges

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 ★ | 13s |
| openai-codex/gpt-5.3-codex | 18s |
| anthropic/claude-sonnet-4-6 | 23s |
| anthropic/claude-opus-4-6 | 24s |
| zai/glm-5 | 82s |

### Speed vs accuracy

<div style="height:480px"><canvas id="speed-accuracy"></canvas></div>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script src="https://cdn.jsdelivr.net/npm/chartjs-plugin-datalabels@2"></script>
<script>
Chart.register(ChartDataLabels);
const models = [
  { name: 'haiku',      t: 124,  s: 10, cost: 0 },
  { name: 'codex',      t: 241,  s: 10, cost: 0 },
  { name: 'opus',       t: 357,  s: 10, cost: 0 },
  { name: 'sonnet',     t: 428,  s: 10, cost: 0 },
  { name: 'glm-5',      t: 1027, s: 10, cost: 0 },
  { name: 'devstral',   t: 19,   s:  1, cost: 0 },
  { name: 'coder-next', t: 20,   s:  1, cost: 0 },
  { name: 'k2p5',       t: 24,   s:  1, cost: 0 },
  { name: 'qwen3.5+',   t: 34,   s:  1, cost: 0 },
  { name: 'MiniMax',    t: 59,   s:  1, cost: 0 },
];
new Chart(document.getElementById('speed-accuracy'), {
  type: 'bubble',
  data: { datasets: models.map(m => ({ label: m.name, data: [{ x: +(m.t/m.s).toFixed(1), y: m.s, r: 6 }] })) },
  options: {
    maintainAspectRatio: false,
    scales: { x: { title: { display: true, text: 'Seconds per passed part — lower is better' }}, y: { title: { display: true, text: 'Parts passed (/10)' }, min: 0, max: 11 } },
    plugins: {
      datalabels: { anchor: 'end', align: 'end', offset: 1, font: { size: 11 }, formatter: (_, ctx) => models[ctx.datasetIndex].name },
      tooltip: { callbacks: { label: (ctx) => { const m = models[ctx.datasetIndex]; return `${m.name}: ${m.s}/10, ${(m.t/m.s).toFixed(1)}s/part`; } } }
    }
  }
});
</script>

No cost data was tracked for this benchmark run.

### Summary table

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
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>anthropic/claude-haiku-4-5 ★</td>
      <td style="text-align: right">13s</td>
      <td style="text-align: right">12s</td>
      <td style="text-align: right">11s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">13s</td>
      <td style="text-align: right">13s</td>
      <td style="text-align: right">12s</td>
      <td style="text-align: right">11s</td>
      <td style="text-align: right">12s</td>
      <td style="text-align: right">13s</td>
    </tr>
    <tr>
      <td>openai-codex/gpt-5.3-codex</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">35s</td>
      <td style="text-align: right">26s</td>
      <td style="text-align: right">20s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">26s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">32s</td>
      <td style="text-align: right">18s</td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">26s</td>
      <td style="text-align: right">34s</td>
      <td style="text-align: right">54s</td>
      <td style="text-align: right">154s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">26s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">29s</td>
      <td style="text-align: right">23s</td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">50s</td>
      <td style="text-align: right">36s</td>
      <td style="text-align: right">56s</td>
      <td style="text-align: right">39s</td>
      <td style="text-align: right">37s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">31s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right">33s</td>
      <td style="text-align: right">24s</td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">35s</td>
      <td style="text-align: right">62s</td>
      <td style="text-align: right">110s</td>
      <td style="text-align: right">236s</td>
      <td style="text-align: right">162s</td>
      <td style="text-align: right">161s</td>
      <td style="text-align: right">34s</td>
      <td style="text-align: right">37s</td>
      <td style="text-align: right">108s</td>
      <td style="text-align: right">82s</td>
    </tr>
    <tr><td colspan="11" style="text-align: center; font-style: italic; opacity: 0.6">— ejected at Day 1 Part 2 —</td></tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">✗</td>
      <td colspan="8"></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">34s</td>
      <td style="text-align: right">✗</td>
      <td colspan="8"></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">20s</td>
      <td style="text-align: right">✗</td>
      <td colspan="8"></td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">✗</td>
      <td colspan="8"></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">59s</td>
      <td style="text-align: right">✗</td>
      <td colspan="8"></td>
    </tr>
  </tbody>
</table>

## Observations

**OCaml is harder** — 5 of 9 models failed Part 2 of Day 1, vs. 4 of 11 in the Haskell run.
The survivors were exactly the same top-tier models: the two Anthropic models, GPT-5.3-Codex,
and GLM-5.

**`gpt-5.3-codex` led among the original 9 models** — fastest on 7 of
the 10 parts, with a consistent 18–35s range.

**`claude-haiku-4-5` (★ retroactive)** — fastest on all 10 parts,
never exceeding 14s.

**`glm-5`** — always correct, almost always last. Its times were often
3–6× those of the leaders, particularly in Days 2 and 3 (110–236s). Later benchmarks
with token tracking showed `glm-5` uses roughly 2–3× more output tokens per part.

**`claude-sonnet-4-6`** — 154s on D2P2 stands out against its otherwise
23–54s range. A single run doesn't tell the full story — averaging over multiple runs
would give a cleaner signal.

**`mistral/devstral-2512`** — same pattern as in the Haskell run: fast on Part
1 (19s), wrong answer on Part 2, ejected.

## What's next

Token usage and API cost tracking are now part of the benchmark. Future runs will report
output token counts and per-part cost alongside wall-clock times — giving a clearer picture
of solution complexity and value-for-money across models.

*Benchmarked on 2026-02-25 using [pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent) as the agent harness.*

---

*This post was written with AI assistance.*
