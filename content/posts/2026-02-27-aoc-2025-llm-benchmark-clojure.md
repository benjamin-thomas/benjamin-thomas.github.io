+++
title = "Benchmarking LLMs on Advent of Code 2025 (Clojure)"
description = "10 LLMs, AoC 2025 Days 1–5 in Clojure. Nine of ten survive — one ejection on Day 1 Part 2."

[taxonomies]
tags = ["Clojure", "AI", "Advent of Code"]
+++

Following up on the [Haskell](@/posts/2026-02-24-aoc-2025-llm-benchmark-haskell.md),
[OCaml](@/posts/2026-02-25-aoc-2025-llm-benchmark-ocaml.md),
[Python](@/posts/2026-02-25-aoc-2025-llm-benchmark-python.md),
[ReScript](@/posts/2026-02-26-aoc-2025-llm-benchmark-rescript.md),
[Ruby](@/posts/2026-02-26-aoc-2025-llm-benchmark-ruby.md),
[Elixir](@/posts/2026-02-26-aoc-2025-llm-benchmark-elixir.md),
[Java](@/posts/2026-02-26-aoc-2025-llm-benchmark-java.md),
[Elm](@/posts/2026-02-26-aoc-2025-llm-benchmark-elm.md),
[Rust](@/posts/2026-02-27-aoc-2025-llm-benchmark-rust.md), and
[Racket](@/posts/2026-02-27-aoc-2025-llm-benchmark-racket.md) benchmarks, I ran the same
AoC 2025 Days 1–5 setup in **Clojure**.

Clojure is a Lisp dialect that runs on the JVM. It's known for its persistent data
structures, REPL-driven development, and strong concurrency primitives. For this benchmark,
models needed to write standalone scripts runnable via `clj`. The JVM startup cost is real —
one model got trapped in repeated slow `clj` invocations on a single part, ballooning its
wall-clock time — but the language itself posed no conceptual difficulty. No scaffolding was
provided.

The result: 9 of 10 models completed all 10 parts. One ejection on Day 1 Part 2.

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

**1 ejection:**
- `alibaba/qwen3-coder-next` — Day 1 Part 2: wrong answer on all 3 clean attempts
  (2132, 5637, 5637). Ejected.

Three retries succeeded across the remaining 90 model-parts:
- `anthropic/claude-haiku-4-5` — Day 1 Part 2 (wrong answer, fixed on 3rd try)
- `mistral/devstral-2512` — Day 1 Part 2 (wrong answer, fixed on 3rd try)
- `minimax/MiniMax-M2.5` — Day 2 Part 2 (wrong answer, fixed on 2nd try)

## Results (Days 1–5)

### Per-task leaderboards

<br>

#### Day 1 Part 1 — Dial rotation counting

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 35s |
| openai-codex/gpt-5.3-codex | 35s |
| mistral/devstral-2512 | 41s |
| anthropic/claude-opus-4-6 | 44s |
| alibaba/qwen3.5-plus | 45s |
| anthropic/claude-sonnet-4-6 | 46s |
| alibaba/qwen3-coder-next | 54s |
| kimi-coding/k2p5 | 58s |
| minimax/MiniMax-M2.5 | 67s |
| zai/glm-5 | 72s |

<br><br>

#### Day 1 Part 2 — Counting zero-crossings during dial rotation

| Model | Time | Result |
| ------:| ----:| :--: |
| openai-codex/gpt-5.3-codex | 22s | ✓ |
| anthropic/claude-opus-4-6 | 27s | ✓ |
| anthropic/claude-sonnet-4-6 | 40s | ✓ |
| alibaba/qwen3.5-plus | 55s | ✓ |
| kimi-coding/k2p5 | 83s | ✓ |
| minimax/MiniMax-M2.5 | 111s | ✓ |
| zai/glm-5 | 141s | ✓ |
| mistral/devstral-2512 | 344s | ✓ (3rd try) |
| anthropic/claude-haiku-4-5 | 365s | ✓ (3rd try) |
| alibaba/qwen3-coder-next | — | ✗ (ejected, 3/3 failed) |

<br><br>

#### Day 2 Part 1 — Summing repeated-digit IDs in ranges

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 29s |
| openai-codex/gpt-5.3-codex | 36s |
| mistral/devstral-2512 | 42s |
| kimi-coding/k2p5 | 47s |
| anthropic/claude-opus-4-6 | 57s |
| anthropic/claude-sonnet-4-6 | 64s |
| alibaba/qwen3.5-plus | 68s |
| zai/glm-5 | 72s |
| minimax/MiniMax-M2.5 | 84s |

<br><br>

#### Day 2 Part 2 — Repeated-pattern IDs (any repeat count)

| Model | Time | Result |
| ------:| ----:| :--: |
| openai-codex/gpt-5.3-codex | 21s | ✓ |
| mistral/devstral-2512 | 21s | ✓ |
| zai/glm-5 | 23s | ✓ |
| anthropic/claude-haiku-4-5 | 28s | ✓ |
| alibaba/qwen3.5-plus | 33s | ✓ |
| anthropic/claude-sonnet-4-6 | 34s | ✓ |
| anthropic/claude-opus-4-6 | 39s | ✓ |
| kimi-coding/k2p5 | 62s | ✓ |
| minimax/MiniMax-M2.5 | 190s | ✓ (2nd try) |

<br><br>

#### Day 3 Part 1 — Maximizing 2-digit joltage from battery banks

| Model | Time |
| ------:| ----:|
| openai-codex/gpt-5.3-codex | 27s |
| kimi-coding/k2p5 | 27s |
| anthropic/claude-opus-4-6 | 35s |
| anthropic/claude-haiku-4-5 | 42s |
| anthropic/claude-sonnet-4-6 | 48s |
| alibaba/qwen3.5-plus | 53s |
| mistral/devstral-2512 | 55s |
| zai/glm-5 | 70s |
| minimax/MiniMax-M2.5 | 103s |

<br><br>

#### Day 3 Part 2 — Maximizing 12-digit joltage from battery banks

| Model | Time |
| ------:| ----:|
| openai-codex/gpt-5.3-codex | 24s |
| kimi-coding/k2p5 | 25s |
| anthropic/claude-sonnet-4-6 | 26s |
| anthropic/claude-opus-4-6 | 31s |
| anthropic/claude-haiku-4-5 | 47s |
| mistral/devstral-2512 | 50s |
| zai/glm-5 | 116s |
| minimax/MiniMax-M2.5 | 183s |
| alibaba/qwen3.5-plus | 1,069s* |

\* `qwen3.5-plus`'s first solution had an infinite loop that ran for over 16 minutes
before being externally killed. After rewriting and fixing several subsequent bugs
(runtime errors, unmatched parens), it eventually produced the correct answer.

<br><br>

#### Day 4 Part 1 — Grid neighbor counting (accessible paper rolls)

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 29s |
| kimi-coding/k2p5 | 34s |
| anthropic/claude-opus-4-6 | 36s |
| mistral/devstral-2512 | 36s |
| alibaba/qwen3.5-plus | 38s |
| openai-codex/gpt-5.3-codex | 43s |
| anthropic/claude-sonnet-4-6 | 44s |
| minimax/MiniMax-M2.5 | 54s |
| zai/glm-5 | 69s |

<br><br>

#### Day 4 Part 2 — Iterative grid removal simulation

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 14s |
| anthropic/claude-haiku-4-5 | 19s |
| openai-codex/gpt-5.3-codex | 20s |
| alibaba/qwen3.5-plus | 22s |
| anthropic/claude-sonnet-4-6 | 23s |
| zai/glm-5 | 30s |
| anthropic/claude-opus-4-6 | 32s |
| minimax/MiniMax-M2.5 | 35s |
| kimi-coding/k2p5 | 37s |

<br><br>

#### Day 5 Part 1 — Range membership checking

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 26s |
| kimi-coding/k2p5 | 27s |
| mistral/devstral-2512 | 32s |
| anthropic/claude-sonnet-4-6 | 34s |
| anthropic/claude-opus-4-6 | 35s |
| openai-codex/gpt-5.3-codex | 38s |
| alibaba/qwen3.5-plus | 41s |
| zai/glm-5 | 60s |
| minimax/MiniMax-M2.5 | 84s |

<br><br>

#### Day 5 Part 2 — Counting total fresh IDs from overlapping ranges

| Model | Time |
| ------:| ----:|
| openai-codex/gpt-5.3-codex | 18s |
| kimi-coding/k2p5 | 18s |
| anthropic/claude-sonnet-4-6 | 19s |
| anthropic/claude-haiku-4-5 | 22s |
| alibaba/qwen3.5-plus | 23s |
| mistral/devstral-2512 | 24s |
| anthropic/claude-opus-4-6 | 27s |
| minimax/MiniMax-M2.5 | 30s |
| zai/glm-5 | 31s |

<br>

### Speed vs accuracy

<div style="height:480px"><canvas id="speed-accuracy"></canvas></div>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script src="https://cdn.jsdelivr.net/npm/chartjs-plugin-datalabels@2"></script>
<script>
Chart.register(ChartDataLabels);
const models = [
  { name: 'codex',      t: 284,  s: 10, cost: 0.27 },
  { name: 'opus',       t: 363,  s: 10, cost: 1.03 },
  { name: 'sonnet',     t: 378,  s: 10, cost: 0.48 },
  { name: 'k2p5',       t: 418,  s: 10, cost: 0.11 },
  { name: 'haiku',      t: 642,  s: 10, cost: 0.32 },
  { name: 'devstral',   t: 659,  s: 10, cost: 0.33 },
  { name: 'glm-5',      t: 684,  s: 10, cost: 0.35 },
  { name: 'MiniMax',    t: 941,  s: 10, cost: 0.33 },
  { name: 'qwen3.5+',   t: 1447, s: 10, cost: 0.32 },
  { name: 'coder-next', t: 54,   s:  1, cost: 0.53 },
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
  { name: 'codex',      tok: 5650,   s: 10, cost: 0.27 },
  { name: 'opus',       tok: 11047,  s: 10, cost: 1.03 },
  { name: 'k2p5',       tok: 11814,  s: 10, cost: 0.11 },
  { name: 'sonnet',     tok: 14307,  s: 10, cost: 0.48 },
  { name: 'glm-5',      tok: 18212,  s: 10, cost: 0.35 },
  { name: 'haiku',      tok: 22007,  s: 10, cost: 0.32 },
  { name: 'devstral',   tok: 29274,  s: 10, cost: 0.33 },
  { name: 'qwen3.5+',   tok: 31714,  s: 10, cost: 0.32 },
  { name: 'MiniMax',    tok: 31967,  s: 10, cost: 0.33 },
  { name: 'coder-next', tok: 17589,  s:  1, cost: 0.53 },
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
      <td>openai-codex/gpt-5.3-codex</td>
      <td style="text-align: right">35s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">36s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">43s</td>
      <td style="text-align: right">20s</td>
      <td style="text-align: right">38s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right"><strong>284s</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">44s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">57s</td>
      <td style="text-align: right">39s</td>
      <td style="text-align: right">35s</td>
      <td style="text-align: right">31s</td>
      <td style="text-align: right">36s</td>
      <td style="text-align: right">32s</td>
      <td style="text-align: right">35s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right"><strong>363s</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">46s</td>
      <td style="text-align: right">40s</td>
      <td style="text-align: right">64s</td>
      <td style="text-align: right">34s</td>
      <td style="text-align: right">48s</td>
      <td style="text-align: right">26s</td>
      <td style="text-align: right">44s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right">34s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right"><strong>378s</strong></td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">58s</td>
      <td style="text-align: right">83s</td>
      <td style="text-align: right">47s</td>
      <td style="text-align: right">62s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">25s</td>
      <td style="text-align: right">34s</td>
      <td style="text-align: right">37s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">18s</td>
      <td style="text-align: right"><strong>418s</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">35s</td>
      <td style="text-align: right">365s</td>
      <td style="text-align: right">29s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">42s</td>
      <td style="text-align: right">47s</td>
      <td style="text-align: right">29s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">26s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right"><strong>642s</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">41s</td>
      <td style="text-align: right">344s</td>
      <td style="text-align: right">42s</td>
      <td style="text-align: right">21s</td>
      <td style="text-align: right">55s</td>
      <td style="text-align: right">50s</td>
      <td style="text-align: right">36s</td>
      <td style="text-align: right">14s</td>
      <td style="text-align: right">32s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right"><strong>659s</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">72s</td>
      <td style="text-align: right">141s</td>
      <td style="text-align: right">72s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right">70s</td>
      <td style="text-align: right">116s</td>
      <td style="text-align: right">69s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">60s</td>
      <td style="text-align: right">31s</td>
      <td style="text-align: right"><strong>684s</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">67s</td>
      <td style="text-align: right">111s</td>
      <td style="text-align: right">84s</td>
      <td style="text-align: right">190s</td>
      <td style="text-align: right">103s</td>
      <td style="text-align: right">183s</td>
      <td style="text-align: right">54s</td>
      <td style="text-align: right">35s</td>
      <td style="text-align: right">84s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right"><strong>941s</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">45s</td>
      <td style="text-align: right">55s</td>
      <td style="text-align: right">68s</td>
      <td style="text-align: right">33s</td>
      <td style="text-align: right">53s</td>
      <td style="text-align: right">1,069s</td>
      <td style="text-align: right">38s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">41s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right"><strong>1,447s</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">54s</td>
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
      <td style="text-align: right">474</td>
      <td style="text-align: right">491</td>
      <td style="text-align: right">608</td>
      <td style="text-align: right">569</td>
      <td style="text-align: right">451</td>
      <td style="text-align: right">632</td>
      <td style="text-align: right">526</td>
      <td style="text-align: right">473</td>
      <td style="text-align: right">945</td>
      <td style="text-align: right">481</td>
      <td style="text-align: right"><strong>5,650</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">764</td>
      <td style="text-align: right">839</td>
      <td style="text-align: right">2,161</td>
      <td style="text-align: right">1,753</td>
      <td style="text-align: right">825</td>
      <td style="text-align: right">971</td>
      <td style="text-align: right">869</td>
      <td style="text-align: right">1,165</td>
      <td style="text-align: right">866</td>
      <td style="text-align: right">834</td>
      <td style="text-align: right"><strong>11,047</strong></td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">1,081</td>
      <td style="text-align: right">3,243</td>
      <td style="text-align: right">758</td>
      <td style="text-align: right">2,433</td>
      <td style="text-align: right">501</td>
      <td style="text-align: right">1,008</td>
      <td style="text-align: right">593</td>
      <td style="text-align: right">1,069</td>
      <td style="text-align: right">558</td>
      <td style="text-align: right">570</td>
      <td style="text-align: right"><strong>11,814</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">1,277</td>
      <td style="text-align: right">1,872</td>
      <td style="text-align: right">2,274</td>
      <td style="text-align: right">1,528</td>
      <td style="text-align: right">1,782</td>
      <td style="text-align: right">980</td>
      <td style="text-align: right">1,865</td>
      <td style="text-align: right">872</td>
      <td style="text-align: right">1,165</td>
      <td style="text-align: right">692</td>
      <td style="text-align: right"><strong>14,307</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">1,413</td>
      <td style="text-align: right">4,696</td>
      <td style="text-align: right">1,663</td>
      <td style="text-align: right">557</td>
      <td style="text-align: right">1,645</td>
      <td style="text-align: right">4,361</td>
      <td style="text-align: right">1,677</td>
      <td style="text-align: right">594</td>
      <td style="text-align: right">1,024</td>
      <td style="text-align: right">582</td>
      <td style="text-align: right"><strong>18,212</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">970</td>
      <td style="text-align: right">5,811</td>
      <td style="text-align: right">1,061</td>
      <td style="text-align: right">971</td>
      <td style="text-align: right">3,058</td>
      <td style="text-align: right">4,781</td>
      <td style="text-align: right">1,467</td>
      <td style="text-align: right">1,204</td>
      <td style="text-align: right">1,234</td>
      <td style="text-align: right">1,450</td>
      <td style="text-align: right"><strong>22,007</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">1,791</td>
      <td style="text-align: right">10,105</td>
      <td style="text-align: right">2,342</td>
      <td style="text-align: right">886</td>
      <td style="text-align: right">2,956</td>
      <td style="text-align: right">4,798</td>
      <td style="text-align: right">2,192</td>
      <td style="text-align: right">820</td>
      <td style="text-align: right">1,163</td>
      <td style="text-align: right">2,221</td>
      <td style="text-align: right"><strong>29,274</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">1,948</td>
      <td style="text-align: right">6,586</td>
      <td style="text-align: right">6,076</td>
      <td style="text-align: right">2,183</td>
      <td style="text-align: right">3,467</td>
      <td style="text-align: right">4,784</td>
      <td style="text-align: right">1,972</td>
      <td style="text-align: right">1,152</td>
      <td style="text-align: right">2,126</td>
      <td style="text-align: right">1,420</td>
      <td style="text-align: right"><strong>31,714</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">1,928</td>
      <td style="text-align: right">5,000</td>
      <td style="text-align: right">2,511</td>
      <td style="text-align: right">6,304</td>
      <td style="text-align: right">2,254</td>
      <td style="text-align: right">7,516</td>
      <td style="text-align: right">1,900</td>
      <td style="text-align: right">1,157</td>
      <td style="text-align: right">2,539</td>
      <td style="text-align: right">858</td>
      <td style="text-align: right"><strong>31,967</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">2,158</td>
      <td style="text-align: right">15,431</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right"><strong>17,589</strong></td>
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
      <td style="text-align: right">.0142</td>
      <td style="text-align: right">.0181</td>
      <td style="text-align: right">.0038</td>
      <td style="text-align: right">.0112</td>
      <td style="text-align: right">.0087</td>
      <td style="text-align: right">.0108</td>
      <td style="text-align: right">.0097</td>
      <td style="text-align: right">.0122</td>
      <td style="text-align: right">.0097</td>
      <td style="text-align: right">.0082</td>
      <td style="text-align: right"><strong>$0.11</strong></td>
    </tr>
    <tr>
      <td>openai-codex/gpt-5.3-codex</td>
      <td style="text-align: right">.0168</td>
      <td style="text-align: right">.0190</td>
      <td style="text-align: right">.0252</td>
      <td style="text-align: right">.0191</td>
      <td style="text-align: right">.0213</td>
      <td style="text-align: right">.0193</td>
      <td style="text-align: right">.0169</td>
      <td style="text-align: right">.0200</td>
      <td style="text-align: right">.0664</td>
      <td style="text-align: right">.0416</td>
      <td style="text-align: right"><strong>$0.27</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-haiku-4-5</td>
      <td style="text-align: right">.0268</td>
      <td style="text-align: right">.0693</td>
      <td style="text-align: right">.0276</td>
      <td style="text-align: right">.0179</td>
      <td style="text-align: right">.0367</td>
      <td style="text-align: right">.0404</td>
      <td style="text-align: right">.0297</td>
      <td style="text-align: right">.0125</td>
      <td style="text-align: right">.0339</td>
      <td style="text-align: right">.0204</td>
      <td style="text-align: right"><strong>$0.32</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">.0164</td>
      <td style="text-align: right">.0363</td>
      <td style="text-align: right">.0479</td>
      <td style="text-align: right">.0284</td>
      <td style="text-align: right">.0331</td>
      <td style="text-align: right">.0831</td>
      <td style="text-align: right">.0170</td>
      <td style="text-align: right">.0163</td>
      <td style="text-align: right">.0245</td>
      <td style="text-align: right">.0166</td>
      <td style="text-align: right"><strong>$0.32</strong></td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">.0238</td>
      <td style="text-align: right">.0444</td>
      <td style="text-align: right">.0151</td>
      <td style="text-align: right">.0574</td>
      <td style="text-align: right">.0334</td>
      <td style="text-align: right">.0808</td>
      <td style="text-align: right">.0083</td>
      <td style="text-align: right">.0110</td>
      <td style="text-align: right">.0337</td>
      <td style="text-align: right">.0239</td>
      <td style="text-align: right"><strong>$0.33</strong></td>
    </tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">.0175</td>
      <td style="text-align: right">.1344</td>
      <td style="text-align: right">.0222</td>
      <td style="text-align: right">.0120</td>
      <td style="text-align: right">.0325</td>
      <td style="text-align: right">.0522</td>
      <td style="text-align: right">.0188</td>
      <td style="text-align: right">.0098</td>
      <td style="text-align: right">.0123</td>
      <td style="text-align: right">.0199</td>
      <td style="text-align: right"><strong>$0.33</strong></td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">.0402</td>
      <td style="text-align: right">.0527</td>
      <td style="text-align: right">.0227</td>
      <td style="text-align: right">.0105</td>
      <td style="text-align: right">.0387</td>
      <td style="text-align: right">.0483</td>
      <td style="text-align: right">.0397</td>
      <td style="text-align: right">.0201</td>
      <td style="text-align: right">.0518</td>
      <td style="text-align: right">.0236</td>
      <td style="text-align: right"><strong>$0.35</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">.0498</td>
      <td style="text-align: right">.0480</td>
      <td style="text-align: right">.0805</td>
      <td style="text-align: right">.0439</td>
      <td style="text-align: right">.0671</td>
      <td style="text-align: right">.0316</td>
      <td style="text-align: right">.0622</td>
      <td style="text-align: right">.0309</td>
      <td style="text-align: right">.0453</td>
      <td style="text-align: right">.0225</td>
      <td style="text-align: right"><strong>$0.48</strong></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">.0746</td>
      <td style="text-align: right">.4550</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right">—</td>
      <td style="text-align: right"><strong>$0.53</strong></td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">.1160</td>
      <td style="text-align: right">.0827</td>
      <td style="text-align: right">.1362</td>
      <td style="text-align: right">.0767</td>
      <td style="text-align: right">.1125</td>
      <td style="text-align: right">.0841</td>
      <td style="text-align: right">.1141</td>
      <td style="text-align: right">.1015</td>
      <td style="text-align: right">.1117</td>
      <td style="text-align: right">.0966</td>
      <td style="text-align: right"><strong>$1.03</strong></td>
    </tr>
  </tbody>
</table>

## Observations

**9/10 completers — one ejection.** `qwen3-coder-next` fell on Day 1 Part 2 after three
wrong answers, while the other nine models finished all 10 parts.

**`gpt-5.3-codex`** — fastest overall at 284s, fewest tokens at 5,650, and never needed
a retry. No single part over 43s. Consistent dominance, same as in Racket.

**`claude-opus-4-6`** — second fastest at 363s, zero retries, rock-solid. The premium
pricing ($1.03 total) remains its only weakness.

**`kimi-coding/k2p5`** — cheapest at $0.11 total, with a respectable 418s. The best
value proposition in the field.

**Day 1 Part 2 was the graveyard.** Three models needed retries and one was ejected.
`claude-haiku-4-5` and `devstral-2512` both needed all three attempts, pushing their
Day 1 Part 2 times past 340s. After clearing that hurdle, both ran clean for the
remaining 8 parts.

**The 17-minute outlier.** `qwen3.5-plus`'s first Day 3 Part 2 solution had an infinite
loop that ran for over 16 minutes before being externally killed. The model then
recognized the issue ("likely an infinite loop"), rewrote the algorithm, but hit
several more bugs (runtime exceptions, unmatched parens) before finally producing the
correct answer. Total wall-clock: 1,069s. Excluding that one disastrous part,
`qwen3.5-plus` was a mid-pack performer.

**`MiniMax-M2.5`** — completed everything but was consistently the slowest or
second-slowest. Day 2 Part 2 required a retry (190s), and several other parts crossed
the 100s mark. Total: 941s.

**No Clojure-specific struggles.** No model got stuck on S-expression syntax, Clojure's
threading macros, or JVM interop beyond the startup cost. The language was accessible
to all models.

## Cross-language snapshot

| Language | Models completing all 10 parts |
| --------| ------|
| Python | 10/10 |
| Ruby | 10/10 |
| Elm | 10/10 |
| Rust | 10/10 |
| Racket | 10/10 |
| Java | 9/10 |
| **Clojure** | **9/10** |
| Elixir | 7/10 |
| Haskell | 7/11 |
| OCaml | 5/9 |
| ReScript (run 2) | 2/10 |

Clojure slots in alongside Java — one ejection, strong overall. The Lisp syntax was
no barrier. The only real friction was runtime: JVM startup latency penalized models
that didn't plan their execution strategy. As with Racket, these are languages that
LLMs clearly *know* — the training data coverage is sufficient for correct solutions
even if the languages aren't mainstream.

*Benchmarked on 2026-02-27 using [pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent) as the agent harness.*

---

*This post was written with AI assistance.*
