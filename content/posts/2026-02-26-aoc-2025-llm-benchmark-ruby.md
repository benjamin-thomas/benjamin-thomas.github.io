+++
title = "Benchmarking LLMs on Advent of Code 2025 (Ruby)"
description = "10 LLMs, AoC 2025 Days 1–5 in Ruby. All 10 solved every part — a clean sweep matching Python."

[taxonomies]
tags = ["Ruby", "AI", "Advent of Code"]
+++

Following up on [the Haskell benchmark](@/posts/2026-02-24-aoc-2025-llm-benchmark-haskell.md), [the OCaml
benchmark](@/posts/2026-02-25-aoc-2025-llm-benchmark-ocaml.md), [the Python
benchmark](@/posts/2026-02-25-aoc-2025-llm-benchmark-python.md), and [the ReScript
benchmark](@/posts/2026-02-26-aoc-2025-llm-benchmark-rescript.md), I ran the same AoC 2025 Days 1–5
puzzles in **Ruby**.

Same setup as before — the question is whether the leaderboard reshuffles when the
target language changes.

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

**None.** All 10 models solved all 10 parts correctly on the first attempt.

`zai/glm-5` was originally ejected on D1P1 due to persistent HTTP 429 errors from ZAI's
API. It was re-run solo after the API stabilized and completed all 10 parts without issues.
Its results are included below.

## Results (Days 1–5)

### Per-task leaderboards

<br>

#### Day 1 Part 1 — Dial rotation counting

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 8s |
| anthropic/claude-haiku-4-5 | 9s |
| alibaba/qwen3-coder-next | 11s |
| kimi-coding/k2p5 | 12s |
| openai-codex/gpt-5.3-codex | 12s |
| anthropic/claude-sonnet-4-6 | 13s |
| anthropic/claude-opus-4-6 | 18s |
| alibaba/qwen3.5-plus | 18s |
| zai/glm-5 | 27s |
| minimax/MiniMax-M2.5 | 48s |

<br><br>

#### Day 1 Part 2 — Counting zero-crossings during dial rotation

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 8s |
| openai-codex/gpt-5.3-codex | 10s |
| anthropic/claude-sonnet-4-6 | 17s |
| mistral/devstral-2512 | 22s |
| anthropic/claude-opus-4-6 | 26s |
| alibaba/qwen3.5-plus | 29s |
| kimi-coding/k2p5 | 35s |
| zai/glm-5 | 63s |
| alibaba/qwen3-coder-next | 164s |
| minimax/MiniMax-M2.5 | 187s |

<br><br>

#### Day 2 Part 1 — Summing repeated-digit IDs in ranges

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 10s |
| alibaba/qwen3-coder-next | 10s |
| openai-codex/gpt-5.3-codex | 13s |
| kimi-coding/k2p5 | 14s |
| anthropic/claude-haiku-4-5 | 17s |
| anthropic/claude-sonnet-4-6 | 21s |
| alibaba/qwen3.5-plus | 23s |
| zai/glm-5 | 25s |
| anthropic/claude-opus-4-6 | 27s |
| minimax/MiniMax-M2.5 | 49s |

<br><br>

#### Day 2 Part 2 — Repeated-pattern IDs (any repeat count)

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 7s |
| anthropic/claude-haiku-4-5 | 11s |
| kimi-coding/k2p5 | 13s |
| alibaba/qwen3.5-plus | 17s |
| openai-codex/gpt-5.3-codex | 20s |
| anthropic/claude-opus-4-6 | 25s |
| zai/glm-5 | 26s |
| anthropic/claude-sonnet-4-6 | 27s |
| alibaba/qwen3-coder-next | 28s |
| minimax/MiniMax-M2.5 | 31s |

<br><br>

#### Day 3 Part 1 — Maximizing 2-digit joltage from battery banks

| Model | Time |
| ------:| ----:|
| openai-codex/gpt-5.3-codex | 11s |
| anthropic/claude-haiku-4-5 | 14s |
| anthropic/claude-sonnet-4-6 | 17s |
| anthropic/claude-opus-4-6 | 24s |
| alibaba/qwen3.5-plus | 27s |
| alibaba/qwen3-coder-next | 28s |
| zai/glm-5 | 34s |
| kimi-coding/k2p5 | 36s |
| mistral/devstral-2512 | 48s |
| minimax/MiniMax-M2.5 | 165s |

<br><br>

#### Day 3 Part 2 — Maximizing 12-digit joltage from battery banks

| Model | Time |
| ------:| ----:|
| openai-codex/gpt-5.3-codex | 11s |
| mistral/devstral-2512 | 11s |
| anthropic/claude-haiku-4-5 | 13s |
| anthropic/claude-sonnet-4-6 | 14s |
| kimi-coding/k2p5 | 15s |
| anthropic/claude-opus-4-6 | 19s |
| zai/glm-5 | 20s |
| alibaba/qwen3-coder-next | 23s |
| alibaba/qwen3.5-plus | 24s |
| minimax/MiniMax-M2.5 | 36s |

<br><br>

#### Day 4 Part 1 — Grid neighbor counting (accessible paper rolls)

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 10s |
| anthropic/claude-haiku-4-5 | 11s |
| anthropic/claude-sonnet-4-6 | 14s |
| openai-codex/gpt-5.3-codex | 15s |
| kimi-coding/k2p5 | 15s |
| anthropic/claude-opus-4-6 | 19s |
| alibaba/qwen3.5-plus | 22s |
| alibaba/qwen3-coder-next | 25s |
| minimax/MiniMax-M2.5 | 29s |
| zai/glm-5 | 32s |

<br><br>

#### Day 4 Part 2 — Iterative grid removal simulation

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 8s |
| anthropic/claude-haiku-4-5 | 12s |
| anthropic/claude-sonnet-4-6 | 14s |
| openai-codex/gpt-5.3-codex | 14s |
| kimi-coding/k2p5 | 14s |
| anthropic/claude-opus-4-6 | 16s |
| alibaba/qwen3.5-plus | 19s |
| zai/glm-5 | 25s |
| minimax/MiniMax-M2.5 | 27s |
| alibaba/qwen3-coder-next | 35s |

<br><br>

#### Day 5 Part 1 — Range membership checking

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 8s |
| anthropic/claude-haiku-4-5 | 10s |
| kimi-coding/k2p5 | 12s |
| openai-codex/gpt-5.3-codex | 12s |
| alibaba/qwen3-coder-next | 13s |
| anthropic/claude-sonnet-4-6 | 14s |
| anthropic/claude-opus-4-6 | 15s |
| alibaba/qwen3.5-plus | 16s |
| zai/glm-5 | 28s |
| minimax/MiniMax-M2.5 | 34s |

<br><br>

#### Day 5 Part 2 — Counting total fresh IDs from overlapping ranges

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 6s |
| anthropic/claude-haiku-4-5 | 8s |
| anthropic/claude-sonnet-4-6 | 12s |
| kimi-coding/k2p5 | 12s |
| openai-codex/gpt-5.3-codex | 12s |
| anthropic/claude-opus-4-6 | 15s |
| zai/glm-5 | 29s |
| minimax/MiniMax-M2.5 | 34s |
| alibaba/qwen3.5-plus | 36s |
| alibaba/qwen3-coder-next | 39s |

<br>

### Speed vs accuracy

<div style="height:480px"><canvas id="speed-accuracy"></canvas></div>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script src="https://cdn.jsdelivr.net/npm/chartjs-plugin-datalabels@2"></script>
<script>
Chart.register(ChartDataLabels);
const models = [
  { name: 'haiku',      t: 113,  s: 10, cost: 0.22 },
  { name: 'codex',      t: 130,  s: 10, cost: 0.19 },
  { name: 'devstral',   t: 138,  s: 10, cost: 0.12 },
  { name: 'sonnet',     t: 163,  s: 10, cost: 0.30 },
  { name: 'k2p5',       t: 178,  s: 10, cost: 0.04 },
  { name: 'opus',       t: 204,  s: 10, cost: 0.94 },
  { name: 'qwen3.5+',   t: 231,  s: 10, cost: 0.14 },
  { name: 'glm-5',      t: 309,  s: 10, cost: 0.16 },
  { name: 'coder-next', t: 376,  s: 10, cost: 0.48 },
  { name: 'MiniMax',    t: 640,  s: 10, cost: 0.25 },
];
new Chart(document.getElementById('speed-accuracy'), {
  type: 'bubble',
  data: { datasets: models.map(m => ({ label: m.name, data: [{ x: +(m.t/m.s).toFixed(1), y: m.s, r: 3+Math.sqrt(m.cost)*4 }] })) },
  options: {
    maintainAspectRatio: false,
    scales: { x: { title: { display: true, text: 'Seconds per passed part — lower is better' }}, y: { title: { display: true, text: 'Parts passed (/10)' }, min: 0, max: 11 } },
    plugins: {
      datalabels: { anchor: 'end', align: 'end', offset: 1, font: { size: 11 }, formatter: (_, ctx) => models[ctx.datasetIndex].name },
      tooltip: { callbacks: { label: (ctx) => { const m = models[ctx.datasetIndex]; return `${m.name}: ${m.s}/10, ${(m.t/m.s).toFixed(1)}s/part, $${m.cost}`; } } }
    }
  }
});
</script>

<div style="height:480px"><canvas id="token-efficiency"></canvas></div>
<script>
{
const models = [
  { name: 'codex',      tok: 3995,   s: 10, cost: 0.19 },
  { name: 'k2p5',       tok: 5293,   s: 10, cost: 0.04 },
  { name: 'glm-5',      tok: 5788,   s: 10, cost: 0.16 },
  { name: 'sonnet',     tok: 7622,   s: 10, cost: 0.30 },
  { name: 'opus',       tok: 8921,   s: 10, cost: 0.94 },
  { name: 'haiku',      tok: 9600,   s: 10, cost: 0.22 },
  { name: 'devstral',   tok: 12575,  s: 10, cost: 0.12 },
  { name: 'coder-next', tok: 14276,  s: 10, cost: 0.48 },
  { name: 'qwen3.5+',   tok: 17152,  s: 10, cost: 0.14 },
  { name: 'MiniMax',    tok: 23914,  s: 10, cost: 0.25 },
];
new Chart(document.getElementById('token-efficiency'), {
  type: 'bubble',
  data: { datasets: models.map(m => ({ label: m.name, data: [{ x: +(m.tok/m.s).toFixed(0), y: m.s, r: 3+Math.sqrt(m.cost)*4 }] })) },
  options: {
    maintainAspectRatio: false,
    scales: { x: { title: { display: true, text: 'Tokens per passed part — lower is better' }}, y: { title: { display: true, text: 'Parts passed (/10)' }, min: 0, max: 11 } },
    plugins: {
      datalabels: { anchor: 'end', align: 'end', offset: 1, font: { size: 11 }, formatter: (_, ctx) => models[ctx.datasetIndex].name },
      tooltip: { callbacks: { label: (ctx) => { const m = models[ctx.datasetIndex]; return `${m.name}: ${m.s}/10, ${m.tok} tokens, $${m.cost}`; } } }
    }
  }
});
}
</script>

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
      <td style="text-align: right">9s</td>
      <td style="text-align: right">8s</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">11s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">13s</td>
      <td style="text-align: right">11s</td>
      <td style="text-align: right">12s</td>
      <td style="text-align: right">10s</td>
      <td style="text-align: right">8s</td>
      <td style="text-align: right"><strong>113s</strong></td>
    </tr>
    <tr>
      <td>openai-codex/gpt-5.3-codex</td>
      <td style="text-align: right">12s</td>
      <td style="text-align: right">10s</td>
      <td style="text-align: right">13s</td>
      <td style="text-align: right">20s</td>
      <td style="text-align: right">11s</td>
      <td style="text-align: right">11s</td>
      <td style="text-align: right">15s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">12s</td>
      <td style="text-align: right">12s</td>
      <td style="text-align: right"><strong>130s</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">8s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">10s</td>
      <td style="text-align: right">7s</td>
      <td style="text-align: right">48s</td>
      <td style="text-align: right">11s</td>
      <td style="text-align: right">10s</td>
      <td style="text-align: right">8s</td>
      <td style="text-align: right">8s</td>
      <td style="text-align: right">6s</td>
      <td style="text-align: right"><strong>138s</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">13s</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">12s</td>
      <td style="text-align: right"><strong>163s</strong></td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">12s</td>
      <td style="text-align: right">35s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">13s</td>
      <td style="text-align: right">36s</td>
      <td style="text-align: right">15s</td>
      <td style="text-align: right">15s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">12s</td>
      <td style="text-align: right">12s</td>
      <td style="text-align: right"><strong>178s</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">26s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">25s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">15s</td>
      <td style="text-align: right">15s</td>
      <td style="text-align: right"><strong>204s</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">29s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">36s</td>
      <td style="text-align: right"><strong>231s</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">63s</td>
      <td style="text-align: right">25s</td>
      <td style="text-align: right">26s</td>
      <td style="text-align: right">34s</td>
      <td style="text-align: right">20s</td>
      <td style="text-align: right">32s</td>
      <td style="text-align: right">25s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">29s</td>
      <td style="text-align: right"><strong>309s</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">11s</td>
      <td style="text-align: right">164s</td>
      <td style="text-align: right">10s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right">25s</td>
      <td style="text-align: right">35s</td>
      <td style="text-align: right">13s</td>
      <td style="text-align: right">39s</td>
      <td style="text-align: right"><strong>376s</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">48s</td>
      <td style="text-align: right">187s</td>
      <td style="text-align: right">49s</td>
      <td style="text-align: right">31s</td>
      <td style="text-align: right">165s</td>
      <td style="text-align: right">36s</td>
      <td style="text-align: right">29s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">34s</td>
      <td style="text-align: right">34s</td>
      <td style="text-align: right"><strong>640s</strong></td>
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
      <td style="text-align: right">319</td>
      <td style="text-align: right">382</td>
      <td style="text-align: right">367</td>
      <td style="text-align: right">377</td>
      <td style="text-align: right">337</td>
      <td style="text-align: right">396</td>
      <td style="text-align: right">437</td>
      <td style="text-align: right">671</td>
      <td style="text-align: right">330</td>
      <td style="text-align: right">379</td>
      <td style="text-align: right"><strong>3,995</strong></td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">408</td>
      <td style="text-align: right">837</td>
      <td style="text-align: right">522</td>
      <td style="text-align: right">621</td>
      <td style="text-align: right">406</td>
      <td style="text-align: right">532</td>
      <td style="text-align: right">542</td>
      <td style="text-align: right">583</td>
      <td style="text-align: right">398</td>
      <td style="text-align: right">444</td>
      <td style="text-align: right"><strong>5,293</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">543</td>
      <td style="text-align: right">1,291</td>
      <td style="text-align: right">485</td>
      <td style="text-align: right">507</td>
      <td style="text-align: right">605</td>
      <td style="text-align: right">379</td>
      <td style="text-align: right">542</td>
      <td style="text-align: right">498</td>
      <td style="text-align: right">464</td>
      <td style="text-align: right">474</td>
      <td style="text-align: right"><strong>5,788</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">598</td>
      <td style="text-align: right">823</td>
      <td style="text-align: right">1,049</td>
      <td style="text-align: right">1,197</td>
      <td style="text-align: right">658</td>
      <td style="text-align: right">743</td>
      <td style="text-align: right">689</td>
      <td style="text-align: right">698</td>
      <td style="text-align: right">577</td>
      <td style="text-align: right">590</td>
      <td style="text-align: right"><strong>7,622</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">565</td>
      <td style="text-align: right">1,221</td>
      <td style="text-align: right">1,349</td>
      <td style="text-align: right">1,405</td>
      <td style="text-align: right">958</td>
      <td style="text-align: right">828</td>
      <td style="text-align: right">732</td>
      <td style="text-align: right">725</td>
      <td style="text-align: right">566</td>
      <td style="text-align: right">572</td>
      <td style="text-align: right"><strong>8,921</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">915</td>
      <td style="text-align: right">792</td>
      <td style="text-align: right">1,384</td>
      <td style="text-align: right">1,000</td>
      <td style="text-align: right">1,295</td>
      <td style="text-align: right">906</td>
      <td style="text-align: right">903</td>
      <td style="text-align: right">837</td>
      <td style="text-align: right">813</td>
      <td style="text-align: right">755</td>
      <td style="text-align: right"><strong>9,600</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">538</td>
      <td style="text-align: right">3,040</td>
      <td style="text-align: right">608</td>
      <td style="text-align: right">510</td>
      <td style="text-align: right">4,973</td>
      <td style="text-align: right">730</td>
      <td style="text-align: right">600</td>
      <td style="text-align: right">651</td>
      <td style="text-align: right">428</td>
      <td style="text-align: right">497</td>
      <td style="text-align: right"><strong>12,575</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">688</td>
      <td style="text-align: right">6,720</td>
      <td style="text-align: right">744</td>
      <td style="text-align: right">719</td>
      <td style="text-align: right">766</td>
      <td style="text-align: right">768</td>
      <td style="text-align: right">802</td>
      <td style="text-align: right">1,135</td>
      <td style="text-align: right">707</td>
      <td style="text-align: right">1,227</td>
      <td style="text-align: right"><strong>14,276</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">1,364</td>
      <td style="text-align: right">3,504</td>
      <td style="text-align: right">2,031</td>
      <td style="text-align: right">1,031</td>
      <td style="text-align: right">2,150</td>
      <td style="text-align: right">1,980</td>
      <td style="text-align: right">1,266</td>
      <td style="text-align: right">1,121</td>
      <td style="text-align: right">1,117</td>
      <td style="text-align: right">1,588</td>
      <td style="text-align: right"><strong>17,152</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">822</td>
      <td style="text-align: right">9,448</td>
      <td style="text-align: right">1,390</td>
      <td style="text-align: right">868</td>
      <td style="text-align: right">6,678</td>
      <td style="text-align: right">1,102</td>
      <td style="text-align: right">809</td>
      <td style="text-align: right">820</td>
      <td style="text-align: right">788</td>
      <td style="text-align: right">1,189</td>
      <td style="text-align: right"><strong>23,914</strong></td>
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
      <td style="text-align: right">.0028</td>
      <td style="text-align: right">.0047</td>
      <td style="text-align: right">.0031</td>
      <td style="text-align: right">.0036</td>
      <td style="text-align: right">.0025</td>
      <td style="text-align: right">.0032</td>
      <td style="text-align: right">.0097</td>
      <td style="text-align: right">.0085</td>
      <td style="text-align: right">.0024</td>
      <td style="text-align: right">.0028</td>
      <td style="text-align: right"><strong>$0.04</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">.0063</td>
      <td style="text-align: right">.0217</td>
      <td style="text-align: right">.0069</td>
      <td style="text-align: right">.0065</td>
      <td style="text-align: right">.0308</td>
      <td style="text-align: right">.0206</td>
      <td style="text-align: right">.0044</td>
      <td style="text-align: right">.0094</td>
      <td style="text-align: right">.0061</td>
      <td style="text-align: right">.0080</td>
      <td style="text-align: right"><strong>$0.12</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">.0108</td>
      <td style="text-align: right">.0194</td>
      <td style="text-align: right">.0129</td>
      <td style="text-align: right">.0145</td>
      <td style="text-align: right">.0125</td>
      <td style="text-align: right">.0160</td>
      <td style="text-align: right">.0101</td>
      <td style="text-align: right">.0146</td>
      <td style="text-align: right">.0093</td>
      <td style="text-align: right">.0188</td>
      <td style="text-align: right"><strong>$0.14</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">.0177</td>
      <td style="text-align: right">.0227</td>
      <td style="text-align: right">.0056</td>
      <td style="text-align: right">.0066</td>
      <td style="text-align: right">.0071</td>
      <td style="text-align: right">.0063</td>
      <td style="text-align: right">.0225</td>
      <td style="text-align: right">.0180</td>
      <td style="text-align: right">.0295</td>
      <td style="text-align: right">.0221</td>
      <td style="text-align: right"><strong>$0.16</strong></td>
    </tr>
    <tr>
      <td>openai-codex/gpt-5.3-codex</td>
      <td style="text-align: right">.0146</td>
      <td style="text-align: right">.0254</td>
      <td style="text-align: right">.0162</td>
      <td style="text-align: right">.0120</td>
      <td style="text-align: right">.0131</td>
      <td style="text-align: right">.0148</td>
      <td style="text-align: right">.0356</td>
      <td style="text-align: right">.0262</td>
      <td style="text-align: right">.0138</td>
      <td style="text-align: right">.0151</td>
      <td style="text-align: right"><strong>$0.19</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">.0228</td>
      <td style="text-align: right">.0122</td>
      <td style="text-align: right">.0331</td>
      <td style="text-align: right">.0106</td>
      <td style="text-align: right">.0333</td>
      <td style="text-align: right">.0140</td>
      <td style="text-align: right">.0317</td>
      <td style="text-align: right">.0164</td>
      <td style="text-align: right">.0261</td>
      <td style="text-align: right">.0155</td>
      <td style="text-align: right"><strong>$0.22</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">.0138</td>
      <td style="text-align: right">.0945</td>
      <td style="text-align: right">.0080</td>
      <td style="text-align: right">.0147</td>
      <td style="text-align: right">.0443</td>
      <td style="text-align: right">.0251</td>
      <td style="text-align: right">.0034</td>
      <td style="text-align: right">.0058</td>
      <td style="text-align: right">.0159</td>
      <td style="text-align: right">.0207</td>
      <td style="text-align: right"><strong>$0.25</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">.0325</td>
      <td style="text-align: right">.0257</td>
      <td style="text-align: right">.0406</td>
      <td style="text-align: right">.0331</td>
      <td style="text-align: right">.0325</td>
      <td style="text-align: right">.0235</td>
      <td style="text-align: right">.0330</td>
      <td style="text-align: right">.0252</td>
      <td style="text-align: right">.0302</td>
      <td style="text-align: right">.0192</td>
      <td style="text-align: right"><strong>$0.30</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">.0243</td>
      <td style="text-align: right">.1128</td>
      <td style="text-align: right">.0081</td>
      <td style="text-align: right">.0117</td>
      <td style="text-align: right">.0502</td>
      <td style="text-align: right">.0599</td>
      <td style="text-align: right">.0258</td>
      <td style="text-align: right">.0409</td>
      <td style="text-align: right">.0506</td>
      <td style="text-align: right">.0945</td>
      <td style="text-align: right"><strong>$0.48</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">.1078</td>
      <td style="text-align: right">.0927</td>
      <td style="text-align: right">.1421</td>
      <td style="text-align: right">.0628</td>
      <td style="text-align: right">.1359</td>
      <td style="text-align: right">.0827</td>
      <td style="text-align: right">.1080</td>
      <td style="text-align: right">.0786</td>
      <td style="text-align: right">.0985</td>
      <td style="text-align: right">.1340</td>
      <td style="text-align: right"><strong>$0.94</strong></td>
    </tr>
  </tbody>
</table>

## Observations

**All 10 models solved all 10 parts correctly on the first attempt** — matching
Python's clean sweep.

**`claude-haiku-4-5`** — fastest overall at 113s. Fastest or near-fastest on 7 of 10 parts.

**`devstral-2512`** — fastest on individual parts (six sub-10s), but a 48-second D3P1
spike pushes its total to 138s. The token data shows 4,973 output tokens on D3P1 vs.
a 428–651 range on most other parts.

**`gpt-5.3-codex`** — fewest tokens: 3,995 total, under 400 per part on average.

**`kimi-coding/k2p5`** — cheapest at $0.04 for all 10 parts. Fifth in speed (178s),
second in token count (5,293).

**`claude-opus-4-6`** — $0.94 total, the most expensive at ~$0.09 per part. 204s total,
8,921 tokens.

**`qwen3-coder-next`** — 164 seconds on D1P2, with 6,720 output tokens on that single
part. Every other part was 10–39s.

**`minimax/MiniMax-M2.5`** — 640s total, slowest but correct on every part across all
benchmarks so far.

**`zai/glm-5` completed all 10 parts in a solo re-run (309s total).** Originally ejected
due to API 429 errors, it was re-run after ZAI's service stabilized. 5,788 tokens and $0.16
total — mid-pack on speed, but third in token efficiency behind `codex` and `k2p5`.

## Cross-language comparison

With five benchmarks now complete, some patterns are emerging:

| Language | Models completing all 10 parts |
| --------| ------|
| Python | 10/10 |
| Ruby | 10/10 |
| Haskell | 7/11 |
| OCaml | 5/9 |
| ReScript (run 2) | 2/10 |

Completion rates may correlate with how widely each language is represented in public codebases.

The speed rankings shift across languages. `haiku` is fastest in Ruby (113s) and OCaml
(124s). `devstral` was fastest in Python (205s) but gets ejected in Haskell and OCaml.
`opus` is the only model that completed the ReScript benchmark.

## What's next

With multiple scripting-language benchmarks now showing the same pattern (all models pass,
differences mainly in cost and token efficiency), the next runs in other languages should
show whether the leaderboard reshuffles with different target languages.

*Benchmarked on 2026-02-26 using [pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent) as the agent harness.*

---

*This post was written with AI assistance.*
