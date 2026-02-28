+++
title = "Benchmarking LLMs on Advent of Code 2025 (Elm)"
description = "10 LLMs, AoC 2025 Days 1–5 in Elm. All ten models completed every part — the third perfect-completion language alongside Python and Ruby."

[taxonomies]
tags = ["Elm", "AI", "Advent of Code"]
+++

Following up on [the Haskell benchmark](@/posts/2026-02-24-aoc-2025-llm-benchmark-haskell.md), [the OCaml
benchmark](@/posts/2026-02-25-aoc-2025-llm-benchmark-ocaml.md), [the Python
benchmark](@/posts/2026-02-25-aoc-2025-llm-benchmark-python.md), [the ReScript
benchmark](@/posts/2026-02-26-aoc-2025-llm-benchmark-rescript.md), [the Ruby
benchmark](@/posts/2026-02-26-aoc-2025-llm-benchmark-ruby.md), [the Elixir
benchmark](@/posts/2026-02-26-aoc-2025-llm-benchmark-elixir.md), and [the Java
benchmark](@/posts/2026-02-26-aoc-2025-llm-benchmark-java.md), I ran the same AoC 2025 Days 1–5
setup in **Elm**.

Elm is the most niche language in this series. It's a pure functional language that compiles
to JavaScript, has no native CLI story, and sees relatively little use outside its frontend
niche. Each model received a pre-built scaffold — `run.mjs`, `elm.json`, and a
`Day00.elm` template — that compiles and runs Elm modules via Node.js. The question was
whether models would handle Elm's strict type system, lack of escape hatches, and unfamiliar
idioms (e.g. `Debug.log` for output, `Platform.worker` for headless programs).

The answer: every single one of them did.

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

None. **All 10 models completed all 10 parts.** This ties Elm with Python and Ruby for the
best completion rate in the series.

That said, the path was rocky for some. Several models needed multiple retries, and two
(`devstral-2512` on Day 3 Part 1, `MiniMax-M2.5` on Day 3 Part 2) went through costly
runaway loops requiring dirty restarts.

## Results (Days 1–5)

### Per-task leaderboards

<br>

#### Day 1 Part 1 — Dial rotation counting

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 43s |
| openai-codex/gpt-5.3-codex | 52s |
| alibaba/qwen3-coder-next | 52s |
| anthropic/claude-opus-4-6 | 53s |
| anthropic/claude-sonnet-4-6 | 54s |
| alibaba/qwen3.5-plus | 58s |
| kimi-coding/k2p5 | 60s |
| mistral/devstral-2512 | 65s |
| zai/glm-5 | 66s |
| minimax/MiniMax-M2.5 | 97s |

<br><br>

#### Day 1 Part 2 — Counting zero-crossings during dial rotation

| Model | Time | Result |
| ------:| ----:| :--: |
| anthropic/claude-haiku-4-5 | 22s | ✓ |
| openai-codex/gpt-5.3-codex | 23s | ✓ |
| anthropic/claude-opus-4-6 | 41s | ✓ |
| anthropic/claude-sonnet-4-6 | 44s | ✓ |
| alibaba/qwen3-coder-next | 52s | ✓ |
| alibaba/qwen3.5-plus | 86s | ✓ |
| minimax/MiniMax-M2.5 | 127s | ✓ |
| zai/glm-5 | 137s | ✓ |
| kimi-coding/k2p5 | 239s | ✓ (2nd try) |
| mistral/devstral-2512 | 364s | ✓ (3rd try) |

<br><br>

#### Day 2 Part 1 — Summing repeated-digit IDs in ranges

| Model | Time | Result |
| ------:| ----:| :--: |
| kimi-coding/k2p5 | 32s | ✓ |
| openai-codex/gpt-5.3-codex | 33s | ✓ |
| anthropic/claude-haiku-4-5 | 37s | ✓ |
| alibaba/qwen3-coder-next | 39s | ✓ |
| anthropic/claude-sonnet-4-6 | 49s | ✓ |
| zai/glm-5 | 54s | ✓ |
| mistral/devstral-2512 | 61s | ✓ |
| anthropic/claude-opus-4-6 | 80s | ✓ |
| minimax/MiniMax-M2.5 | 213s | ✓ (2nd try) |
| alibaba/qwen3.5-plus | 363s | ✓ (2nd try) |

<br><br>

#### Day 2 Part 2 — Repeated-pattern IDs (any repeat count)

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 11s |
| kimi-coding/k2p5 | 16s |
| alibaba/qwen3-coder-next | 16s |
| anthropic/claude-haiku-4-5 | 19s |
| openai-codex/gpt-5.3-codex | 23s |
| anthropic/claude-opus-4-6 | 29s |
| zai/glm-5 | 48s |
| minimax/MiniMax-M2.5 | 79s |
| anthropic/claude-sonnet-4-6 | 239s |
| alibaba/qwen3.5-plus | 260s |

<br><br>

#### Day 3 Part 1 — Maximizing 2-digit joltage from battery banks

| Model | Time | Result |
| ------:| ----:| :--: |
| anthropic/claude-sonnet-4-6 | 19s | ✓ |
| openai-codex/gpt-5.3-codex | 19s | ✓ |
| alibaba/qwen3.5-plus | 22s | ✓ |
| anthropic/claude-opus-4-6 | 27s | ✓ |
| alibaba/qwen3-coder-next | 27s | ✓ |
| kimi-coding/k2p5 | 30s | ✓ |
| anthropic/claude-haiku-4-5 | 53s | ✓ |
| zai/glm-5 | 63s | ✓ |
| minimax/MiniMax-M2.5 | 67s | ✓ |
| mistral/devstral-2512 | 1164s | ✓ (dirty retry) |

<br><br>

#### Day 3 Part 2 — Maximizing 12-digit joltage from battery banks

| Model | Time | Result |
| ------:| ----:| :--: |
| kimi-coding/k2p5 | 16s | ✓ |
| anthropic/claude-sonnet-4-6 | 32s | ✓ |
| anthropic/claude-haiku-4-5 | 45s | ✓ |
| zai/glm-5 | 45s | ✓ |
| anthropic/claude-opus-4-6 | 48s | ✓ |
| alibaba/qwen3.5-plus | 62s | ✓ |
| mistral/devstral-2512 | 163s | ✓ |
| alibaba/qwen3-coder-next | 216s | ✓ |
| openai-codex/gpt-5.3-codex | 952s | ✓ (nudge) |
| minimax/MiniMax-M2.5 | — | ✓ (dirty retry ×3) |

<br><br>

#### Day 4 Part 1 — Grid neighbor counting (accessible paper rolls)

| Model | Time | Result |
| ------:| ----:| :--: |
| anthropic/claude-haiku-4-5 | 15s | ✓ |
| kimi-coding/k2p5 | 17s | ✓ |
| anthropic/claude-sonnet-4-6 | 21s | ✓ |
| anthropic/claude-opus-4-6 | 22s | ✓ |
| mistral/devstral-2512 | 22s | ✓ |
| alibaba/qwen3-coder-next | 23s | ✓ |
| zai/glm-5 | 28s | ✓ |
| alibaba/qwen3.5-plus | 37s | ✓ |
| minimax/MiniMax-M2.5 | 53s | ✓ |
| openai-codex/gpt-5.3-codex | — | ✓ (2nd try) |

<br><br>

#### Day 4 Part 2 — Iterative grid removal simulation

| Model | Time | Result |
| ------:| ----:| :--: |
| anthropic/claude-sonnet-4-6 | 24s | ✓ |
| anthropic/claude-opus-4-6 | 24s | ✓ |
| kimi-coding/k2p5 | 38s | ✓ |
| mistral/devstral-2512 | 47s | ✓ |
| alibaba/qwen3.5-plus | 48s | ✓ |
| minimax/MiniMax-M2.5 | 58s | ✓ |
| zai/glm-5 | 68s | ✓ |
| anthropic/claude-haiku-4-5 | 245s | ✓ |
| alibaba/qwen3-coder-next | 272s | ✓ |
| openai-codex/gpt-5.3-codex | 971s | ✓ (2nd try) |

<br><br>

#### Day 5 Part 1 — Range membership checking

| Model | Time |
| ------:| ----:|
| anthropic/claude-sonnet-4-6 | 16s |
| openai-codex/gpt-5.3-codex | 17s |
| alibaba/qwen3.5-plus | 19s |
| anthropic/claude-haiku-4-5 | 20s |
| mistral/devstral-2512 | 20s |
| anthropic/claude-opus-4-6 | 21s |
| zai/glm-5 | 24s |
| minimax/MiniMax-M2.5 | 30s |
| kimi-coding/k2p5 | 44s |
| alibaba/qwen3-coder-next | 47s |

<br><br>

#### Day 5 Part 2 — Counting total fresh IDs from overlapping ranges

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 9s |
| mistral/devstral-2512 | 11s |
| anthropic/claude-sonnet-4-6 | 13s |
| alibaba/qwen3.5-plus | 14s |
| openai-codex/gpt-5.3-codex | 15s |
| kimi-coding/k2p5 | 22s |
| alibaba/qwen3-coder-next | 22s |
| anthropic/claude-opus-4-6 | 24s |
| zai/glm-5 | 31s |
| minimax/MiniMax-M2.5 | 108s |

<br>

### Speed vs accuracy

<div style="height:480px"><canvas id="speed-accuracy"></canvas></div>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script src="https://cdn.jsdelivr.net/npm/chartjs-plugin-datalabels@2"></script>
<script>
Chart.register(ChartDataLabels);
const models = [
  { name: 'opus',       t: 369,  s: 10, cost: 1.02 },
  { name: 'haiku',      t: 508,  s: 10, cost: 0.51 },
  { name: 'sonnet',     t: 511,  s: 10, cost: 0.81 },
  { name: 'k2p5',       t: 514,  s: 10, cost: 0.13 },
  { name: 'glm-5',      t: 564,  s: 10, cost: 0.14 },
  { name: 'coder-next', t: 766,  s: 10, cost: 1.89 },
  { name: 'MiniMax',    t: 832,  s: 10, cost: 1.93 },
  { name: 'qwen3.5+',   t: 969,  s: 10, cost: 0.79 },
  { name: 'devstral',   t: 1928, s: 10, cost: 2.82 },
  { name: 'codex',      t: 2105, s: 10, cost: 0.31 },
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
  { name: 'codex',      tok: 10247,  s: 10, cost: 0.31 },
  { name: 'glm-5',      tok: 13401,  s: 10, cost: 0.14 },
  { name: 'k2p5',       tok: 15732,  s: 10, cost: 0.13 },
  { name: 'opus',       tok: 15785,  s: 10, cost: 1.02 },
  { name: 'sonnet',     tok: 28892,  s: 10, cost: 0.81 },
  { name: 'haiku',      tok: 42230,  s: 10, cost: 0.51 },
  { name: 'coder-next', tok: 68636,  s: 10, cost: 1.89 },
  { name: 'qwen3.5+',   tok: 71538,  s: 10, cost: 0.79 },
  { name: 'MiniMax',    tok: 111871, s: 10, cost: 1.93 },
  { name: 'devstral',   tok: 158759, s: 10, cost: 2.82 },
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
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">53s</td>
      <td style="text-align: right">41s</td>
      <td style="text-align: right">80s</td>
      <td style="text-align: right">29s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">48s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right"><strong>369s</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">43s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">37s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">53s</td>
      <td style="text-align: right">45s</td>
      <td style="text-align: right">15s</td>
      <td style="text-align: right">245s</td>
      <td style="text-align: right">20s</td>
      <td style="text-align: right">9s</td>
      <td style="text-align: right"><strong>508s</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">54s</td>
      <td style="text-align: right">44s</td>
      <td style="text-align: right">49s</td>
      <td style="text-align: right">239s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">32s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">13s</td>
      <td style="text-align: right"><strong>511s</strong></td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">60s</td>
      <td style="text-align: right">239s</td>
      <td style="text-align: right">32s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">38s</td>
      <td style="text-align: right">44s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right"><strong>514s</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">66s</td>
      <td style="text-align: right">137s</td>
      <td style="text-align: right">54s</td>
      <td style="text-align: right">48s</td>
      <td style="text-align: right">63s</td>
      <td style="text-align: right">45s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">68s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">31s</td>
      <td style="text-align: right"><strong>564s</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">52s</td>
      <td style="text-align: right">52s</td>
      <td style="text-align: right">39s</td>
      <td style="text-align: right">16s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">216s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right">272s</td>
      <td style="text-align: right">47s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right"><strong>766s</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">97s</td>
      <td style="text-align: right">127s</td>
      <td style="text-align: right">213s</td>
      <td style="text-align: right">79s</td>
      <td style="text-align: right">67s</td>
      <td style="text-align: right">—*</td>
      <td style="text-align: right">53s</td>
      <td style="text-align: right">58s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">108s</td>
      <td style="text-align: right"><strong>832s*</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">58s</td>
      <td style="text-align: right">86s</td>
      <td style="text-align: right">363s</td>
      <td style="text-align: right">260s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">62s</td>
      <td style="text-align: right">37s</td>
      <td style="text-align: right">48s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right"><strong>969s</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">65s</td>
      <td style="text-align: right">364s</td>
      <td style="text-align: right">61s</td>
      <td style="text-align: right">11s</td>
      <td style="text-align: right">1164s</td>
      <td style="text-align: right">163s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">47s</td>
      <td style="text-align: right">20s</td>
      <td style="text-align: right">11s</td>
      <td style="text-align: right"><strong>1928s</strong></td>
    </tr>
    <tr>
      <td>openai-codex/gpt-5.3-codex</td>
      <td style="text-align: right">52s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right">33s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">952s</td>
      <td style="text-align: right">—†</td>
      <td style="text-align: right">971s</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">15s</td>
      <td style="text-align: right"><strong>2105s†</strong></td>
    </tr>
  </tbody>
</table>

\* MiniMax D3P2 required three dirty restarts; wall-clock time not directly comparable.
Total excludes D3P2.<br>
† Codex D4P1 needed a retry; time for that part not captured cleanly.

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
      <td style="text-align: right">750</td>
      <td style="text-align: right">486</td>
      <td style="text-align: right">774</td>
      <td style="text-align: right">1,074</td>
      <td style="text-align: right">746</td>
      <td style="text-align: right">1,015</td>
      <td style="text-align: right">1,039</td>
      <td style="text-align: right">3,042</td>
      <td style="text-align: right">779</td>
      <td style="text-align: right">542</td>
      <td style="text-align: right"><strong>10,247</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">853</td>
      <td style="text-align: right">4,144</td>
      <td style="text-align: right">970</td>
      <td style="text-align: right">950</td>
      <td style="text-align: right">1,442</td>
      <td style="text-align: right">979</td>
      <td style="text-align: right">919</td>
      <td style="text-align: right">1,618</td>
      <td style="text-align: right">817</td>
      <td style="text-align: right">709</td>
      <td style="text-align: right"><strong>13,401</strong></td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">978</td>
      <td style="text-align: right">4,470</td>
      <td style="text-align: right">923</td>
      <td style="text-align: right">736</td>
      <td style="text-align: right">1,904</td>
      <td style="text-align: right">863</td>
      <td style="text-align: right">1,009</td>
      <td style="text-align: right">2,505</td>
      <td style="text-align: right">1,676</td>
      <td style="text-align: right">668</td>
      <td style="text-align: right"><strong>15,732</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">1,246</td>
      <td style="text-align: right">1,600</td>
      <td style="text-align: right">2,627</td>
      <td style="text-align: right">1,876</td>
      <td style="text-align: right">1,328</td>
      <td style="text-align: right">2,061</td>
      <td style="text-align: right">1,282</td>
      <td style="text-align: right">1,390</td>
      <td style="text-align: right">1,024</td>
      <td style="text-align: right">1,351</td>
      <td style="text-align: right"><strong>15,785</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">1,325</td>
      <td style="text-align: right">1,673</td>
      <td style="text-align: right">2,143</td>
      <td style="text-align: right">16,394</td>
      <td style="text-align: right">1,207</td>
      <td style="text-align: right">1,980</td>
      <td style="text-align: right">1,393</td>
      <td style="text-align: right">939</td>
      <td style="text-align: right">1,068</td>
      <td style="text-align: right">770</td>
      <td style="text-align: right"><strong>28,892</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">1,299</td>
      <td style="text-align: right">1,197</td>
      <td style="text-align: right">1,808</td>
      <td style="text-align: right">1,964</td>
      <td style="text-align: right">6,141</td>
      <td style="text-align: right">5,755</td>
      <td style="text-align: right">1,764</td>
      <td style="text-align: right">19,336</td>
      <td style="text-align: right">2,006</td>
      <td style="text-align: right">960</td>
      <td style="text-align: right"><strong>42,230</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">2,224</td>
      <td style="text-align: right">6,930</td>
      <td style="text-align: right">1,955</td>
      <td style="text-align: right">1,855</td>
      <td style="text-align: right">1,610</td>
      <td style="text-align: right">22,069</td>
      <td style="text-align: right">2,055</td>
      <td style="text-align: right">25,465</td>
      <td style="text-align: right">3,080</td>
      <td style="text-align: right">1,393</td>
      <td style="text-align: right"><strong>68,636</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">2,169</td>
      <td style="text-align: right">7,427</td>
      <td style="text-align: right">32,452</td>
      <td style="text-align: right">14,674</td>
      <td style="text-align: right">2,194</td>
      <td style="text-align: right">4,576</td>
      <td style="text-align: right">2,852</td>
      <td style="text-align: right">2,267</td>
      <td style="text-align: right">1,622</td>
      <td style="text-align: right">1,305</td>
      <td style="text-align: right"><strong>71,538</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">1,877</td>
      <td style="text-align: right">4,445</td>
      <td style="text-align: right">5,885</td>
      <td style="text-align: right">3,525</td>
      <td style="text-align: right">2,606</td>
      <td style="text-align: right">87,094</td>
      <td style="text-align: right">1,972</td>
      <td style="text-align: right">2,260</td>
      <td style="text-align: right">1,063</td>
      <td style="text-align: right">1,144</td>
      <td style="text-align: right"><strong>111,871</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">3,825</td>
      <td style="text-align: right">16,758</td>
      <td style="text-align: right">1,418</td>
      <td style="text-align: right">1,074</td>
      <td style="text-align: right">115,225</td>
      <td style="text-align: right">13,010</td>
      <td style="text-align: right">2,255</td>
      <td style="text-align: right">2,811</td>
      <td style="text-align: right">1,576</td>
      <td style="text-align: right">807</td>
      <td style="text-align: right"><strong>158,759</strong></td>
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
      <td style="text-align: right">.0096</td>
      <td style="text-align: right">.0273</td>
      <td style="text-align: right">.0043</td>
      <td style="text-align: right">.0049</td>
      <td style="text-align: right">.0164</td>
      <td style="text-align: right">.0112</td>
      <td style="text-align: right">.0109</td>
      <td style="text-align: right">.0178</td>
      <td style="text-align: right">.0152</td>
      <td style="text-align: right">.0116</td>
      <td style="text-align: right"><strong>$0.13</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">.0196</td>
      <td style="text-align: right">.0330</td>
      <td style="text-align: right">.0097</td>
      <td style="text-align: right">.0104</td>
      <td style="text-align: right">.0121</td>
      <td style="text-align: right">.0136</td>
      <td style="text-align: right">.0083</td>
      <td style="text-align: right">.0170</td>
      <td style="text-align: right">.0073</td>
      <td style="text-align: right">.0096</td>
      <td style="text-align: right"><strong>$0.14</strong></td>
    </tr>
    <tr>
      <td>openai-codex/gpt-5.3-codex</td>
      <td style="text-align: right">.0300</td>
      <td style="text-align: right">.0158</td>
      <td style="text-align: right">.0197</td>
      <td style="text-align: right">.0389</td>
      <td style="text-align: right">.0260</td>
      <td style="text-align: right">.0277</td>
      <td style="text-align: right">.0296</td>
      <td style="text-align: right">.0864</td>
      <td style="text-align: right">.0190</td>
      <td style="text-align: right">.0199</td>
      <td style="text-align: right"><strong>$0.31</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">.0289</td>
      <td style="text-align: right">.0119</td>
      <td style="text-align: right">.0272</td>
      <td style="text-align: right">.0186</td>
      <td style="text-align: right">.0650</td>
      <td style="text-align: right">.0586</td>
      <td style="text-align: right">.0253</td>
      <td style="text-align: right">.2179</td>
      <td style="text-align: right">.0413</td>
      <td style="text-align: right">.0155</td>
      <td style="text-align: right"><strong>$0.51</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">.0200</td>
      <td style="text-align: right">.0603</td>
      <td style="text-align: right">.2671</td>
      <td style="text-align: right">.2750</td>
      <td style="text-align: right">.0138</td>
      <td style="text-align: right">.0658</td>
      <td style="text-align: right">.0228</td>
      <td style="text-align: right">.0339</td>
      <td style="text-align: right">.0125</td>
      <td style="text-align: right">.0161</td>
      <td style="text-align: right"><strong>$0.79</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">.0517</td>
      <td style="text-align: right">.0512</td>
      <td style="text-align: right">.0590</td>
      <td style="text-align: right">.4163</td>
      <td style="text-align: right">.0406</td>
      <td style="text-align: right">.0567</td>
      <td style="text-align: right">.0443</td>
      <td style="text-align: right">.0325</td>
      <td style="text-align: right">.0374</td>
      <td style="text-align: right">.0251</td>
      <td style="text-align: right"><strong>$0.81</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">.0988</td>
      <td style="text-align: right">.0736</td>
      <td style="text-align: right">.1614</td>
      <td style="text-align: right">.0856</td>
      <td style="text-align: right">.1123</td>
      <td style="text-align: right">.0998</td>
      <td style="text-align: right">.1273</td>
      <td style="text-align: right">.0692</td>
      <td style="text-align: right">.1338</td>
      <td style="text-align: right">.0607</td>
      <td style="text-align: right"><strong>$1.02</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">.0518</td>
      <td style="text-align: right">.0644</td>
      <td style="text-align: right">.0302</td>
      <td style="text-align: right">.0319</td>
      <td style="text-align: right">.0715</td>
      <td style="text-align: right">.7594</td>
      <td style="text-align: right">.0249</td>
      <td style="text-align: right">.5769</td>
      <td style="text-align: right">.1729</td>
      <td style="text-align: right">.1039</td>
      <td style="text-align: right"><strong>$1.89</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">.0192</td>
      <td style="text-align: right">.0346</td>
      <td style="text-align: right">.0445</td>
      <td style="text-align: right">.0290</td>
      <td style="text-align: right">.0285</td>
      <td style="text-align: right">1.6985</td>
      <td style="text-align: right">.0095</td>
      <td style="text-align: right">.0160</td>
      <td style="text-align: right">.0205</td>
      <td style="text-align: right">.0262</td>
      <td style="text-align: right"><strong>$1.93</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">.0487</td>
      <td style="text-align: right">.2439</td>
      <td style="text-align: right">.0254</td>
      <td style="text-align: right">.0204</td>
      <td style="text-align: right">2.0172</td>
      <td style="text-align: right">.3556</td>
      <td style="text-align: right">.0190</td>
      <td style="text-align: right">.0525</td>
      <td style="text-align: right">.0198</td>
      <td style="text-align: right">.0131</td>
      <td style="text-align: right"><strong>$2.82</strong></td>
    </tr>
  </tbody>
</table>

## Observations

**10/10 completers — zero ejections.** Elm joins Python and Ruby as the only languages in
this series where every model solved every part.

**`claude-opus-4-6`** — fastest at 369s total. No single part over 80s, never needed a
retry. ~$1.02 total.

**`kimi-coding/k2p5`** — cheapest at ~$0.13. Fourth fastest at 514s. On 8 of 10 parts
it was under 44s.

**Day 3 was rough for two models.** `devstral-2512` on D3P1 (runaway loop, ~$1.91 and
105K tokens before being killed) and `MiniMax-M2.5` on D3P2 (three dirty restarts, 87K
tokens, ~$1.70).

**`gpt-5.3-codex`** — fewest tokens: 10,247 total. But also the slowest overall (2,105s),
due to D3P2 (952s) and D4P2 (971s).

**`claude-sonnet-4-6`** — 239s and 16,394 tokens on D2P2. Every other part was 13–54s.

**`qwen3.5-plus`** — 32,452 tokens on D2P1 alone. Both Alibaba models completed
everything but used a lot of tokens getting there.

**`glm-5`** — second cheapest at ~$0.14, fifth fastest at 564s, 13,401 tokens. No dirty
retries needed.

## Cross-language snapshot

| Language | Models completing all 10 parts |
| --------| ------|
| Python | 10/10 |
| Ruby | 10/10 |
| **Elm** | **10/10** |
| Java | 9/10 |
| Elixir | 7/10 |
| Haskell | 7/11 |
| OCaml | 5/9 |
| ReScript (run 2) | 2/10 |

Elm's 10/10 completion was unexpected — it has a smaller training corpus than any other
language tested. The provided template (`Day00.elm` with `Platform.worker` and `Debug.log`)
may have helped by giving every model a clear starting point.

ReScript (2/10) is also a niche compile-to-JS functional language, but its toolchain gave
models a much harder time. The scaffold and Elm's stable API may explain the difference.

*Benchmarked on 2026-02-26 using [pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent) as the agent harness.*

---

*This post was written with AI assistance.*
