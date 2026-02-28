+++
title = "Benchmarking LLMs on Advent of Code 2025 (Java)"
description = "10 LLMs, AoC 2025 Days 1–5 in Java. Nine models completed all 10 parts; one was ejected on Day 1 Part 2."

[taxonomies]
tags = ["Java", "AI", "Advent of Code"]
+++

Following up on [the Haskell benchmark](@/posts/2026-02-24-aoc-2025-llm-benchmark-haskell.md), [the OCaml
benchmark](@/posts/2026-02-25-aoc-2025-llm-benchmark-ocaml.md), [the Python
benchmark](@/posts/2026-02-25-aoc-2025-llm-benchmark-python.md), [the ReScript
benchmark](@/posts/2026-02-26-aoc-2025-llm-benchmark-rescript.md), [the Ruby
benchmark](@/posts/2026-02-26-aoc-2025-llm-benchmark-ruby.md), and [the Elixir
benchmark](@/posts/2026-02-26-aoc-2025-llm-benchmark-elixir.md), I ran the same AoC 2025 Days 1–5
setup in **Java**.

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

| Model | Ejected at | Reason |
| ------| ----------| ------|
| `alibaba/qwen3-coder-next` | D1P2 | Wrong answer after 3 clean retries |

The remaining **9 models solved all 10 parts**, though two needed retries on Day 1 Part 2:
`glm-5` passed on its 2nd attempt and `MiniMax-M2.5` on its 3rd.

## Results (Days 1–5)

### Per-task leaderboards

<br>

#### Day 1 Part 1 — Dial rotation counting

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 11s |
| mistral/devstral-2512 | 11s |
| alibaba/qwen3-coder-next | 12s |
| anthropic/claude-sonnet-4-6 | 14s |
| openai-codex/gpt-5.3-codex | 15s |
| kimi-coding/k2p5 | 16s |
| alibaba/qwen3.5-plus | 16s |
| anthropic/claude-opus-4-6 | 17s |
| zai/glm-5 | 26s |
| minimax/MiniMax-M2.5 | 44s |

<br><br>

#### Day 1 Part 2 — Counting zero-crossings during dial rotation

| Model | Time | Result |
| ------:| ----:| :--: |
| anthropic/claude-haiku-4-5 | 10s | ✓ |
| anthropic/claude-opus-4-6 | 16s | ✓ |
| anthropic/claude-sonnet-4-6 | 19s | ✓ |
| openai-codex/gpt-5.3-codex | 27s | ✓ |
| kimi-coding/k2p5 | 36s | ✓ |
| alibaba/qwen3.5-plus | 47s | ✓ |
| mistral/devstral-2512 | 111s | ✓ |
| zai/glm-5 | 282s | ✓ (2nd try) |
| minimax/MiniMax-M2.5 | 816s | ✓ (3rd try) |
| alibaba/qwen3-coder-next | — | ✗ (ejected) |

<br><br>

#### Day 2 Part 1 — Summing repeated-digit IDs in ranges

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 11s |
| mistral/devstral-2512 | 12s |
| kimi-coding/k2p5 | 13s |
| openai-codex/gpt-5.3-codex | 23s |
| anthropic/claude-sonnet-4-6 | 25s |
| anthropic/claude-opus-4-6 | 27s |
| minimax/MiniMax-M2.5 | 32s |
| zai/glm-5 | 34s |
| alibaba/qwen3.5-plus | 48s |

<br><br>

#### Day 2 Part 2 — Repeated-pattern IDs (any repeat count)

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 9s |
| anthropic/claude-haiku-4-5 | 10s |
| kimi-coding/k2p5 | 13s |
| openai-codex/gpt-5.3-codex | 16s |
| alibaba/qwen3.5-plus | 23s |
| anthropic/claude-opus-4-6 | 25s |
| minimax/MiniMax-M2.5 | 31s |
| zai/glm-5 | 39s |
| anthropic/claude-sonnet-4-6 | 62s |

<br><br>

#### Day 3 Part 1 — Maximizing 2-digit joltage from battery banks

| Model | Time |
| ------:| ----:|
| kimi-coding/k2p5 | 14s |
| openai-codex/gpt-5.3-codex | 16s |
| anthropic/claude-sonnet-4-6 | 20s |
| anthropic/claude-opus-4-6 | 21s |
| mistral/devstral-2512 | 21s |
| anthropic/claude-haiku-4-5 | 36s |
| alibaba/qwen3.5-plus | 39s |
| zai/glm-5 | 83s |
| minimax/MiniMax-M2.5 | 110s |

<br><br>

#### Day 3 Part 2 — Maximizing 12-digit joltage from battery banks

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 10s |
| anthropic/claude-haiku-4-5 | 14s |
| anthropic/claude-sonnet-4-6 | 15s |
| kimi-coding/k2p5 | 18s |
| anthropic/claude-opus-4-6 | 19s |
| openai-codex/gpt-5.3-codex | 20s |
| minimax/MiniMax-M2.5 | 25s |
| zai/glm-5 | 43s |
| alibaba/qwen3.5-plus | 68s |

<br><br>

#### Day 4 Part 1 — Grid neighbor counting (accessible paper rolls)

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 13s |
| openai-codex/gpt-5.3-codex | 16s |
| mistral/devstral-2512 | 16s |
| anthropic/claude-sonnet-4-6 | 19s |
| anthropic/claude-opus-4-6 | 20s |
| alibaba/qwen3.5-plus | 20s |
| zai/glm-5 | 30s |
| kimi-coding/k2p5 | 45s |
| minimax/MiniMax-M2.5 | 53s |

<br><br>

#### Day 4 Part 2 — Iterative grid removal simulation

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 9s |
| anthropic/claude-haiku-4-5 | 13s |
| alibaba/qwen3.5-plus | 17s |
| anthropic/claude-opus-4-6 | 18s |
| anthropic/claude-sonnet-4-6 | 21s |
| openai-codex/gpt-5.3-codex | 21s |
| kimi-coding/k2p5 | 32s |
| minimax/MiniMax-M2.5 | 38s |
| zai/glm-5 | 41s |

<br><br>

#### Day 5 Part 1 — Range membership checking

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 14s |
| mistral/devstral-2512 | 17s |
| anthropic/claude-opus-4-6 | 18s |
| openai-codex/gpt-5.3-codex | 21s |
| anthropic/claude-sonnet-4-6 | 24s |
| alibaba/qwen3.5-plus | 28s |
| kimi-coding/k2p5 | 29s |
| zai/glm-5 | 41s |
| minimax/MiniMax-M2.5 | 66s |

<br><br>

#### Day 5 Part 2 — Counting total fresh IDs from overlapping ranges

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 9s |
| anthropic/claude-haiku-4-5 | 10s |
| kimi-coding/k2p5 | 13s |
| anthropic/claude-sonnet-4-6 | 15s |
| openai-codex/gpt-5.3-codex | 15s |
| anthropic/claude-opus-4-6 | 17s |
| alibaba/qwen3.5-plus | 19s |
| zai/glm-5 | 41s |
| minimax/MiniMax-M2.5 | 56s |

<br>

### Speed vs accuracy

<div style="height:480px"><canvas id="speed-accuracy"></canvas></div>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script src="https://cdn.jsdelivr.net/npm/chartjs-plugin-datalabels@2"></script>
<script>
Chart.register(ChartDataLabels);
const models = [
  { name: 'haiku',      t: 142,  s: 10, cost: 0.26 },
  { name: 'codex',      t: 190,  s: 10, cost: 0.21 },
  { name: 'opus',       t: 198,  s: 10, cost: 1.02 },
  { name: 'devstral',   t: 225,  s: 10, cost: 0.28 },
  { name: 'k2p5',       t: 229,  s: 10, cost: 0.08 },
  { name: 'sonnet',     t: 234,  s: 10, cost: 0.43 },
  { name: 'qwen3.5+',   t: 325,  s: 10, cost: 0.19 },
  { name: 'glm-5',      t: 660,  s: 10, cost: 0.20 },
  { name: 'MiniMax',    t: 1271, s: 10, cost: 0.45 },
  { name: 'coder-next', t: 12,   s:  1, cost: 0.27 },
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
  { name: 'codex',      tok: 6525,   s: 10, cost: 0.21 },
  { name: 'glm-5',      tok: 9244,   s: 10, cost: 0.20 },
  { name: 'k2p5',       tok: 10085,  s: 10, cost: 0.08 },
  { name: 'opus',       tok: 10410,  s: 10, cost: 1.02 },
  { name: 'sonnet',     tok: 14097,  s: 10, cost: 0.43 },
  { name: 'haiku',      tok: 15283,  s: 10, cost: 0.26 },
  { name: 'devstral',   tok: 21822,  s: 10, cost: 0.28 },
  { name: 'qwen3.5+',   tok: 31597,  s: 10, cost: 0.19 },
  { name: 'MiniMax',    tok: 41717,  s: 10, cost: 0.45 },
  { name: 'coder-next', tok: 11215,  s:  1, cost: 0.27 },
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
      <td style="text-align: right">11s</td>
      <td style="text-align: right">10s</td>
      <td style="text-align: right">11s</td>
      <td style="text-align: right">10s</td>
      <td style="text-align: right">36s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">13s</td>
      <td style="text-align: right">13s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">10s</td>
      <td style="text-align: right"><strong>142s</strong></td>
    </tr>
    <tr>
      <td>openai-codex/gpt-5.3-codex</td>
      <td style="text-align: right">15s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">20s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">15s</td>
      <td style="text-align: right"><strong>190s</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">25s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">20s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right"><strong>198s</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">11s</td>
      <td style="text-align: right">111s</td>
      <td style="text-align: right">12s</td>
      <td style="text-align: right">9s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">10s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">9s</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">9s</td>
      <td style="text-align: right"><strong>225s</strong></td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">36s</td>
      <td style="text-align: right">13s</td>
      <td style="text-align: right">13s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right">45s</td>
      <td style="text-align: right">32s</td>
      <td style="text-align: right">29s</td>
      <td style="text-align: right">13s</td>
      <td style="text-align: right"><strong>229s</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">25s</td>
      <td style="text-align: right">62s</td>
      <td style="text-align: right">20s</td>
      <td style="text-align: right">15s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">15s</td>
      <td style="text-align: right"><strong>234s</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">47s</td>
      <td style="text-align: right">48s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right">39s</td>
      <td style="text-align: right">68s</td>
      <td style="text-align: right">20s</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right"><strong>325s</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">26s</td>
      <td style="text-align: right">282s</td>
      <td style="text-align: right">34s</td>
      <td style="text-align: right">39s</td>
      <td style="text-align: right">83s</td>
      <td style="text-align: right">43s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">41s</td>
      <td style="text-align: right">41s</td>
      <td style="text-align: right">41s</td>
      <td style="text-align: right"><strong>660s</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">44s</td>
      <td style="text-align: right">816s</td>
      <td style="text-align: right">32s</td>
      <td style="text-align: right">31s</td>
      <td style="text-align: right">110s</td>
      <td style="text-align: right">25s</td>
      <td style="text-align: right">53s</td>
      <td style="text-align: right">38s</td>
      <td style="text-align: right">66s</td>
      <td style="text-align: right">56s</td>
      <td style="text-align: right"><strong>1271s</strong></td>
    </tr>
    <tr><td colspan="12" style="text-align: center; font-style: italic; opacity: 0.6">— ejected —</td></tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">12s</td>
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
      <td style="text-align: right">525</td>
      <td style="text-align: right">654</td>
      <td style="text-align: right">621</td>
      <td style="text-align: right">576</td>
      <td style="text-align: right">555</td>
      <td style="text-align: right">573</td>
      <td style="text-align: right">584</td>
      <td style="text-align: right">855</td>
      <td style="text-align: right">899</td>
      <td style="text-align: right">683</td>
      <td style="text-align: right"><strong>6,525</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">620</td>
      <td style="text-align: right">1,638</td>
      <td style="text-align: right">771</td>
      <td style="text-align: right">653</td>
      <td style="text-align: right">1,590</td>
      <td style="text-align: right">830</td>
      <td style="text-align: right">704</td>
      <td style="text-align: right">744</td>
      <td style="text-align: right">945</td>
      <td style="text-align: right">749</td>
      <td style="text-align: right"><strong>9,244</strong></td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">673</td>
      <td style="text-align: right">3,081</td>
      <td style="text-align: right">636</td>
      <td style="text-align: right">745</td>
      <td style="text-align: right">582</td>
      <td style="text-align: right">814</td>
      <td style="text-align: right">825</td>
      <td style="text-align: right">932</td>
      <td style="text-align: right">1,112</td>
      <td style="text-align: right">685</td>
      <td style="text-align: right"><strong>10,085</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">793</td>
      <td style="text-align: right">755</td>
      <td style="text-align: right">1,541</td>
      <td style="text-align: right">1,586</td>
      <td style="text-align: right">957</td>
      <td style="text-align: right">918</td>
      <td style="text-align: right">985</td>
      <td style="text-align: right">1,083</td>
      <td style="text-align: right">870</td>
      <td style="text-align: right">922</td>
      <td style="text-align: right"><strong>10,410</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">772</td>
      <td style="text-align: right">1,071</td>
      <td style="text-align: right">1,703</td>
      <td style="text-align: right">4,317</td>
      <td style="text-align: right">923</td>
      <td style="text-align: right">919</td>
      <td style="text-align: right">997</td>
      <td style="text-align: right">1,042</td>
      <td style="text-align: right">1,495</td>
      <td style="text-align: right">858</td>
      <td style="text-align: right"><strong>14,097</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">1,030</td>
      <td style="text-align: right">1,023</td>
      <td style="text-align: right">1,061</td>
      <td style="text-align: right">994</td>
      <td style="text-align: right">4,382</td>
      <td style="text-align: right">1,540</td>
      <td style="text-align: right">1,391</td>
      <td style="text-align: right">1,378</td>
      <td style="text-align: right">1,271</td>
      <td style="text-align: right">1,213</td>
      <td style="text-align: right"><strong>15,283</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">548</td>
      <td style="text-align: right">12,994</td>
      <td style="text-align: right">794</td>
      <td style="text-align: right">687</td>
      <td style="text-align: right">1,547</td>
      <td style="text-align: right">815</td>
      <td style="text-align: right">942</td>
      <td style="text-align: right">1,043</td>
      <td style="text-align: right">1,549</td>
      <td style="text-align: right">903</td>
      <td style="text-align: right"><strong>21,822</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">1,329</td>
      <td style="text-align: right">6,333</td>
      <td style="text-align: right">4,610</td>
      <td style="text-align: right">1,791</td>
      <td style="text-align: right">4,252</td>
      <td style="text-align: right">7,334</td>
      <td style="text-align: right">1,314</td>
      <td style="text-align: right">1,129</td>
      <td style="text-align: right">1,980</td>
      <td style="text-align: right">1,525</td>
      <td style="text-align: right"><strong>31,597</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">1,091</td>
      <td style="text-align: right">28,159</td>
      <td style="text-align: right">1,273</td>
      <td style="text-align: right">1,336</td>
      <td style="text-align: right">3,970</td>
      <td style="text-align: right">928</td>
      <td style="text-align: right">1,123</td>
      <td style="text-align: right">1,071</td>
      <td style="text-align: right">1,866</td>
      <td style="text-align: right">900</td>
      <td style="text-align: right"><strong>41,717</strong></td>
    </tr>
    <tr><td colspan="12" style="text-align: center; font-style: italic; opacity: 0.6">— ejected —</td></tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">608</td>
      <td style="text-align: right">10,607</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">11,215</td>
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
      <td style="text-align: right">.0086</td>
      <td style="text-align: right">.0118</td>
      <td style="text-align: right">.0030</td>
      <td style="text-align: right">.0038</td>
      <td style="text-align: right">.0089</td>
      <td style="text-align: right">.0151</td>
      <td style="text-align: right">.0139</td>
      <td style="text-align: right">.0100</td>
      <td style="text-align: right">.0049</td>
      <td style="text-align: right">.0039</td>
      <td style="text-align: right"><strong>$0.08</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">.0108</td>
      <td style="text-align: right">.0272</td>
      <td style="text-align: right">.0272</td>
      <td style="text-align: right">.0200</td>
      <td style="text-align: right">.0178</td>
      <td style="text-align: right">.0294</td>
      <td style="text-align: right">.0086</td>
      <td style="text-align: right">.0121</td>
      <td style="text-align: right">.0171</td>
      <td style="text-align: right">.0158</td>
      <td style="text-align: right"><strong>$0.19</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">.0181</td>
      <td style="text-align: right">.0314</td>
      <td style="text-align: right">.0070</td>
      <td style="text-align: right">.0079</td>
      <td style="text-align: right">.0387</td>
      <td style="text-align: right">.0239</td>
      <td style="text-align: right">.0063</td>
      <td style="text-align: right">.0085</td>
      <td style="text-align: right">.0317</td>
      <td style="text-align: right">.0240</td>
      <td style="text-align: right"><strong>$0.20</strong></td>
    </tr>
    <tr>
      <td>openai-codex/gpt-5.3-codex</td>
      <td style="text-align: right">.0199</td>
      <td style="text-align: right">.0199</td>
      <td style="text-align: right">.0233</td>
      <td style="text-align: right">.0179</td>
      <td style="text-align: right">.0212</td>
      <td style="text-align: right">.0164</td>
      <td style="text-align: right">.0176</td>
      <td style="text-align: right">.0257</td>
      <td style="text-align: right">.0274</td>
      <td style="text-align: right">.0163</td>
      <td style="text-align: right"><strong>$0.21</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">.0293</td>
      <td style="text-align: right">.0153</td>
      <td style="text-align: right">.0286</td>
      <td style="text-align: right">.0178</td>
      <td style="text-align: right">.0556</td>
      <td style="text-align: right">.0153</td>
      <td style="text-align: right">.0365</td>
      <td style="text-align: right">.0222</td>
      <td style="text-align: right">.0315</td>
      <td style="text-align: right">.0117</td>
      <td style="text-align: right"><strong>$0.26</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">.0084</td>
      <td style="text-align: right">.1834</td>
      <td style="text-align: right">.0090</td>
      <td style="text-align: right">.0096</td>
      <td style="text-align: right">.0103</td>
      <td style="text-align: right">.0109</td>
      <td style="text-align: right">.0101</td>
      <td style="text-align: right">.0112</td>
      <td style="text-align: right">.0137</td>
      <td style="text-align: right">.0115</td>
      <td style="text-align: right"><strong>$0.28</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">.0359</td>
      <td style="text-align: right">.0308</td>
      <td style="text-align: right">.0527</td>
      <td style="text-align: right">.0949</td>
      <td style="text-align: right">.0376</td>
      <td style="text-align: right">.0274</td>
      <td style="text-align: right">.0390</td>
      <td style="text-align: right">.0324</td>
      <td style="text-align: right">.0508</td>
      <td style="text-align: right">.0248</td>
      <td style="text-align: right"><strong>$0.43</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">.0170</td>
      <td style="text-align: right">.2968</td>
      <td style="text-align: right">.0060</td>
      <td style="text-align: right">.0076</td>
      <td style="text-align: right">.0257</td>
      <td style="text-align: right">.0231</td>
      <td style="text-align: right">.0059</td>
      <td style="text-align: right">.0082</td>
      <td style="text-align: right">.0342</td>
      <td style="text-align: right">.0261</td>
      <td style="text-align: right"><strong>$0.45</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">.1174</td>
      <td style="text-align: right">.0803</td>
      <td style="text-align: right">.1318</td>
      <td style="text-align: right">.0694</td>
      <td style="text-align: right">.1188</td>
      <td style="text-align: right">.0841</td>
      <td style="text-align: right">.1196</td>
      <td style="text-align: right">.0938</td>
      <td style="text-align: right">.1118</td>
      <td style="text-align: right">.0974</td>
      <td style="text-align: right"><strong>$1.02</strong></td>
    </tr>
    <tr><td colspan="12" style="text-align: center; font-style: italic; opacity: 0.6">— ejected —</td></tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">.0241</td>
      <td style="text-align: right">.2475</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">$0.27</td>
    </tr>
  </tbody>
</table>



## Observations

**`claude-haiku-4-5` is the fastest overall at 142s.** It never needed a retry, and 8 of
its 10 parts came in under 15 seconds. The D3P1 spike (36s, 4,382 tokens) is the only
outlier — still not slow, but notably wordier than its usual output.

**`gpt-5.3-codex` is the most token-efficient: 6,525 tokens total.** Under 900 tokens per
part across the board. This matches the pattern from previous benchmarks — `codex`
consistently writes the most compact solutions.

**`devstral-2512`** — 111 seconds and 12,994 tokens on D1P2 alone — over half its total
token output. On the remaining 9 parts it averaged about 10 seconds.

**`sonnet-4-6`** — 62 seconds and 4,317 tokens on D2P2. Every other part was 14–25s.

**`MiniMax-M2.5` needed three attempts on Day 1 Part 2.** 816 seconds and 28,159 tokens
on that single part — 67% of its total token output across all 10 parts. It then solved
Days 2–5 without trouble, though consistently slower than other models (25–110s per part).

**`qwen3.5-plus`** — most tokens among completers: 31,597. The D3P2 spike (7,334 tokens,
68s) stands out. Total cost ~$0.19.

**`claude-opus-4-6`** — ~$1.02 total. Third fastest at 198s, 10,410 tokens.

**`kimi-coding/k2p5`** — cheapest at ~$0.08. Fifth in speed (229s), third in tokens
(10,085).

**`qwen3-coder-next` was the only ejection.** It solved D1P1 fast (12s) but couldn't
produce the correct D1P2 answer in three clean attempts, spending 10,607 tokens and $0.25
in the process. The same model was also ejected on D1P2 in the Haskell run and the Elixir
run.

## Cross-language snapshot

| Language | Models completing all 10 parts |
| --------| ------|
| Python | 10/10 |
| Ruby | 10/10 |
| Java | 9/10 |
| Elixir | 7/10 |
| Haskell | 7/11 |
| OCaml | 5/9 |
| ReScript (run 2) | 2/10 |

Java sits alongside Python and Ruby in the high-completion tier. The single ejection
(`qwen3-coder-next` on D1P2) matches a pattern — the same model also failed D1P2 in
Haskell and Elixir.

*Benchmarked on 2026-02-26 using [pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent) as the agent harness.*

---

*This post was written with AI assistance.*
