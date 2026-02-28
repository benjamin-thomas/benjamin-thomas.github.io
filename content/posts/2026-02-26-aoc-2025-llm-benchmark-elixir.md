+++
title = "Benchmarking LLMs on Advent of Code 2025 (Elixir)"
description = "10 LLMs, AoC 2025 Days 1–5 in Elixir. Seven models completed all 10 parts; three were ejected in costly early failures."

[taxonomies]
tags = ["Elixir", "AI", "Advent of Code"]
+++

Following up on [the Haskell benchmark](@/posts/2026-02-24-aoc-2025-llm-benchmark-haskell.md), [the OCaml
benchmark](@/posts/2026-02-25-aoc-2025-llm-benchmark-ocaml.md), [the Python
benchmark](@/posts/2026-02-25-aoc-2025-llm-benchmark-python.md), [the ReScript benchmark](@/posts/2026-02-26-aoc-2025-llm-benchmark-rescript.md),
and [the Ruby benchmark](@/posts/2026-02-26-aoc-2025-llm-benchmark-ruby.md), I ran the same AoC 2025
Days 1–5 setup in **Elixir**.

Elixir is dynamic like Ruby/Python, but with its own ecosystem and idioms that models don't
always handle cleanly.

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
| `mistral/devstral-2512` | D1P1 | Wrong answer after 3 clean retries |
| `alibaba/qwen3-coder-next` | D1P2 | Wrong answer after 3 clean retries |
| `openai-codex/gpt-5.3-codex` | D3P1 | Brain-dead/no-progress loop after retry nudge |

So this run finished with **7/10 full completers**.

## Results (Days 1–5)

### Per-task leaderboards

<br>

#### Day 1 Part 1 — Dial rotation counting

| Model | Time | Result |
| ------:| ----:| :--: |
| anthropic/claude-haiku-4-5 | 24s | ✓ |
| openai-codex/gpt-5.3-codex | 24s | ✓ |
| anthropic/claude-opus-4-6 | 26s | ✓ |
| alibaba/qwen3.5-plus | 39s | ✓ |
| kimi-coding/k2p5 | 44s | ✓ |
| alibaba/qwen3-coder-next | 79s | ✓ |
| minimax/MiniMax-M2.5 | 109s | ✓ |
| anthropic/claude-sonnet-4-6 | 135s | ✓ |
| zai/glm-5 | 172s | ✓ |
| mistral/devstral-2512 | 416s | ✗ (ejected) |

<br><br>

#### Day 1 Part 2 — Counting zero-crossings during dial rotation

| Model | Time | Result |
| ------:| ----:| :--: |
| openai-codex/gpt-5.3-codex | 13s | ✓ |
| anthropic/claude-opus-4-6 | 25s | ✓ |
| anthropic/claude-sonnet-4-6 | 31s | ✓ |
| kimi-coding/k2p5 | 49s | ✓ |
| alibaba/qwen3.5-plus | 78s | ✓ |
| anthropic/claude-haiku-4-5 | 403s | ✓ (2nd try) |
| minimax/MiniMax-M2.5 | 477s | ✓ (2nd try) |
| zai/glm-5 | 526s | ✓ (2nd try) |
| alibaba/qwen3-coder-next | 870s | ✗ (ejected) |

<br><br>

#### Day 2 Part 1 — Summing repeated-digit IDs in ranges

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 12s |
| kimi-coding/k2p5 | 21s |
| alibaba/qwen3.5-plus | 24s |
| openai-codex/gpt-5.3-codex | 27s |
| anthropic/claude-sonnet-4-6 | 33s |
| anthropic/claude-opus-4-6 | 45s |
| minimax/MiniMax-M2.5 | 50s |
| zai/glm-5 | 92s |

<br><br>

#### Day 2 Part 2 — Repeated-pattern IDs (any repeat count)

| Model | Time |
| ------:| ----:|
| openai-codex/gpt-5.3-codex | 11s |
| anthropic/claude-opus-4-6 | 33s |
| anthropic/claude-sonnet-4-6 | 35s |
| anthropic/claude-haiku-4-5 | 36s |
| kimi-coding/k2p5 | 36s |
| alibaba/qwen3.5-plus | 85s |
| zai/glm-5 | 106s |
| minimax/MiniMax-M2.5 | 112s |

<br><br>

#### Day 3 Part 1 — Maximizing 2-digit joltage from battery banks

| Model | Time | Result |
| ------:| ----:| :--: |
| anthropic/claude-haiku-4-5 | 19s | ✓ |
| alibaba/qwen3.5-plus | 27s | ✓ |
| anthropic/claude-sonnet-4-6 | 29s | ✓ |
| kimi-coding/k2p5 | 29s | ✓ |
| anthropic/claude-opus-4-6 | 31s | ✓ |
| minimax/MiniMax-M2.5 | 39s | ✓ |
| zai/glm-5 | 125s | ✓ |
| openai-codex/gpt-5.3-codex | — | ✗ (ejected) |

<br><br>

#### Day 3 Part 2 — Maximizing 12-digit joltage from battery banks

| Model | Time |
| ------:| ----:|
| kimi-coding/k2p5 | 15s |
| alibaba/qwen3.5-plus | 18s |
| anthropic/claude-sonnet-4-6 | 19s |
| anthropic/claude-opus-4-6 | 22s |
| minimax/MiniMax-M2.5 | 34s |
| anthropic/claude-haiku-4-5 | 59s |
| zai/glm-5 | 229s |

<br><br>

#### Day 4 Part 1 — Grid neighbor counting (accessible paper rolls)

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 13s |
| anthropic/claude-sonnet-4-6 | 15s |
| kimi-coding/k2p5 | 17s |
| alibaba/qwen3.5-plus | 23s |
| anthropic/claude-opus-4-6 | 28s |
| minimax/MiniMax-M2.5 | 38s |
| zai/glm-5 | 56s |

<br><br>

#### Day 4 Part 2 — Iterative grid removal simulation

| Model | Time |
| ------:| ----:|
| kimi-coding/k2p5 | 13s |
| anthropic/claude-sonnet-4-6 | 17s |
| alibaba/qwen3.5-plus | 17s |
| anthropic/claude-opus-4-6 | 18s |
| anthropic/claude-haiku-4-5 | 19s |
| zai/glm-5 | 34s |
| minimax/MiniMax-M2.5 | 51s |

<br><br>

#### Day 5 Part 1 — Range membership checking

| Model | Time |
| ------:| ----:|
| alibaba/qwen3.5-plus | 13s |
| anthropic/claude-sonnet-4-6 | 15s |
| anthropic/claude-haiku-4-5 | 18s |
| kimi-coding/k2p5 | 21s |
| anthropic/claude-opus-4-6 | 28s |
| minimax/MiniMax-M2.5 | 34s |
| zai/glm-5 | 65s |

<br><br>

#### Day 5 Part 2 — Counting total fresh IDs from overlapping ranges

| Model | Time |
| ------:| ----:|
| anthropic/claude-haiku-4-5 | 13s |
| anthropic/claude-sonnet-4-6 | 13s |
| kimi-coding/k2p5 | 15s |
| anthropic/claude-opus-4-6 | 16s |
| minimax/MiniMax-M2.5 | 27s |
| alibaba/qwen3.5-plus | 32s |
| zai/glm-5 | 71s |

<br>

### Speed vs accuracy

<div style="height:480px"><canvas id="speed-accuracy"></canvas></div>
<script src="https://cdn.jsdelivr.net/npm/chart.js"></script>
<script src="https://cdn.jsdelivr.net/npm/chartjs-plugin-datalabels@2"></script>
<script>
Chart.register(ChartDataLabels);
const models = [
  { name: 'k2p5',       t: 260,  s: 10, cost: 0.14 },
  { name: 'opus',       t: 272,  s: 10, cost: 1.14 },
  { name: 'sonnet',     t: 342,  s: 10, cost: 0.42 },
  { name: 'qwen3.5+',   t: 356,  s: 10, cost: 0.21 },
  { name: 'haiku',      t: 616,  s: 10, cost: 0.35 },
  { name: 'MiniMax',    t: 971,  s: 10, cost: 0.34 },
  { name: 'glm-5',      t: 1476, s: 10, cost: 0.35 },
  { name: 'codex',      t: 75,   s:  4, cost: 0.13 },
  { name: 'coder-next', t: 79,   s:  1, cost: 1.09 },
  { name: 'devstral',   t: 416,  s:  0, cost: 0.25 },
];
new Chart(document.getElementById('speed-accuracy'), {
  type: 'bubble',
  data: { datasets: models.map(m => ({ label: m.name, data: [{ x: m.s > 0 ? +(m.t/m.s).toFixed(1) : m.t, y: m.s, r: 3+Math.sqrt(m.cost)*4 }] })) },
  options: {
    maintainAspectRatio: false,
    scales: { x: { title: { display: true, text: 'Seconds per passed part — lower is better' }}, y: { title: { display: true, text: 'Parts passed (/10)' }, min: -1, max: 11 } },
    plugins: {
      datalabels: { anchor: 'end', align: 'end', offset: 1, font: { size: 11 }, formatter: (_, ctx) => models[ctx.datasetIndex].name },
      tooltip: { callbacks: { label: (ctx) => { const m = models[ctx.datasetIndex]; return `${m.name}: ${m.s}/10, ${m.t}s total, $${m.cost}`; } } }
    }
  }
});
</script>

<div style="height:480px"><canvas id="token-efficiency"></canvas></div>
<script>
{
const models = [
  { name: 'k2p5',       tok: 12268,  s: 10, cost: 0.14 },
  { name: 'sonnet',     tok: 12068,  s: 10, cost: 0.42 },
  { name: 'opus',       tok: 12957,  s: 10, cost: 1.14 },
  { name: 'glm-5',      tok: 17588,  s: 10, cost: 0.35 },
  { name: 'haiku',      tok: 24937,  s: 10, cost: 0.35 },
  { name: 'qwen3.5+',   tok: 30683,  s: 10, cost: 0.21 },
  { name: 'MiniMax',    tok: 31228,  s: 10, cost: 0.34 },
  { name: 'codex',      tok: 3331,   s:  4, cost: 0.13 },
  { name: 'coder-next', tok: 34945,  s:  1, cost: 1.09 },
  { name: 'devstral',   tok: 12277,  s:  0, cost: 0.25 },
];
new Chart(document.getElementById('token-efficiency'), {
  type: 'bubble',
  data: { datasets: models.map(m => ({ label: m.name, data: [{ x: m.s > 0 ? +(m.tok/m.s).toFixed(0) : m.tok, y: m.s, r: 3+Math.sqrt(m.cost)*4 }] })) },
  options: {
    maintainAspectRatio: false,
    scales: { x: { title: { display: true, text: 'Tokens per passed part — lower is better' }}, y: { title: { display: true, text: 'Parts passed (/10)' }, min: -1, max: 11 } },
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

| Model | D1P1 | D1P2 | D2P1 | D2P2 | D3P1 | D3P2 | D4P1 | D4P2 | D5P1 | D5P2 | Total |
| ------ | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| kimi-coding/k2p5 | 44s | 49s | 21s | 36s | 29s | 15s | 17s | 13s | 21s | 15s | **260s** |
| anthropic/claude-opus-4-6 | 26s | 25s | 45s | 33s | 31s | 22s | 28s | 18s | 28s | 16s | **272s** |
| anthropic/claude-sonnet-4-6 | 135s | 31s | 33s | 35s | 29s | 19s | 15s | 17s | 15s | 13s | **342s** |
| alibaba/qwen3.5-plus | 39s | 78s | 24s | 85s | 27s | 18s | 23s | 17s | 13s | 32s | **356s** |
| anthropic/claude-haiku-4-5 | 24s | 403s | 12s | 36s | 19s | 59s | 13s | 19s | 18s | 13s | **616s** |
| minimax/MiniMax-M2.5 | 109s | 477s | 50s | 112s | 39s | 34s | 38s | 51s | 34s | 27s | **971s** |
| zai/glm-5 | 172s | 526s | 92s | 106s | 125s | 229s | 56s | 34s | 65s | 71s | **1476s** |
| mistral/devstral-2512 | ✗ | — | — | — | — | — | — | — | — | — | DNF |
| alibaba/qwen3-coder-next | 79s | ✗ | — | — | — | — | — | — | — | — | DNF |
| openai-codex/gpt-5.3-codex | 24s | 13s | 27s | 11s | ✗(—) | — | — | — | — | — | DNF |

<br>

#### Output tokens per part

| Model | D1P1 | D1P2 | D2P1 | D2P2 | D3P1 | D3P2 | D4P1 | D4P2 | D5P1 | D5P2 | Total |
| ------ | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| kimi-coding/k2p5 | 1,219 | 3,300 | 949 | 1,839 | 1,371 | 812 | 764 | 804 | 616 | 594 | **12,268** |
| anthropic/claude-opus-4-6 | 1,022 | 1,139 | 2,355 | 1,858 | 1,360 | 1,122 | 1,183 | 952 | 1,153 | 813 | **12,957** |
| anthropic/claude-sonnet-4-6 | 1,320 | 1,513 | 1,787 | 2,050 | 1,368 | 967 | 790 | 883 | 686 | 704 | **12,068** |
| alibaba/qwen3.5-plus | 2,456 | 9,866 | 1,935 | 6,754 | 2,413 | 1,540 | 1,824 | 1,146 | 899 | 1,850 | **30,683** |
| anthropic/claude-haiku-4-5 | 2,008 | 4,244 | 1,007 | 3,508 | 2,106 | 6,349 | 1,322 | 1,780 | 1,602 | 1,011 | **24,937** |
| minimax/MiniMax-M2.5 | 2,994 | 13,508 | 2,118 | 5,278 | 1,709 | 1,323 | 1,037 | 1,347 | 1,040 | 874 | **31,228** |
| zai/glm-5 | 753 | 3,728 | 1,594 | 1,847 | 2,338 | 4,327 | 775 | 662 | 531 | 1,033 | **17,588** |
| mistral/devstral-2512 | 12,277 | — | — | — | — | — | — | — | — | — | 12,277 |
| alibaba/qwen3-coder-next | 2,100 | 32,845 | — | — | — | — | — | — | — | — | 34,945 |
| openai-codex/gpt-5.3-codex | 691 | 482 | 864 | 359 | 935 | — | — | — | — | — | 3,331 |

<br>

#### API cost per part (approximate USD)

*Costs are rough approximations based on published per-token pricing. I use subscription plans, so my actual spending is capped regardless.*

| Model | D1P1 | D1P2 | D2P1 | D2P2 | D3P1 | D3P2 | D4P1 | D4P2 | D5P1 | D5P2 | Total |
| ------ | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| kimi-coding/k2p5 | 0.0371 | 0.0242 | 0.0050 | 0.0091 | 0.0150 | 0.0090 | 0.0101 | 0.0092 | 0.0100 | 0.0082 | **0.1370** |
| anthropic/claude-opus-4-6 | 0.1569 | 0.0554 | 0.1720 | 0.0933 | 0.1478 | 0.0552 | 0.1732 | 0.0526 | 0.1868 | 0.0421 | **1.1352** |
| anthropic/claude-sonnet-4-6 | 0.0546 | 0.0419 | 0.0615 | 0.0602 | 0.0552 | 0.0306 | 0.0350 | 0.0290 | 0.0324 | 0.0216 | **0.4220** |
| alibaba/qwen3.5-plus | 0.0315 | 0.0418 | 0.0133 | 0.0310 | 0.0172 | 0.0162 | 0.0152 | 0.0167 | 0.0088 | 0.0202 | **0.2119** |
| anthropic/claude-haiku-4-5 | 0.0392 | 0.0437 | 0.0247 | 0.0435 | 0.0330 | 0.0667 | 0.0284 | 0.0178 | 0.0351 | 0.0151 | **0.3472** |
| minimax/MiniMax-M2.5 | 0.0579 | 0.1287 | 0.0128 | 0.0450 | 0.0056 | 0.0077 | 0.0185 | 0.0290 | 0.0165 | 0.0206 | **0.3425** |
| zai/glm-5 | 0.0315 | 0.0486 | 0.0151 | 0.0191 | 0.0516 | 0.0787 | 0.0282 | 0.0193 | 0.0298 | 0.0322 | **0.3542** |
| mistral/devstral-2512 | 0.2548 | — | — | — | — | — | — | — | — | — | 0.2548 |
| alibaba/qwen3-coder-next | 0.1052 | 0.9827 | — | — | — | — | — | — | — | — | 1.0878 |
| openai-codex/gpt-5.3-codex | 0.0220 | 0.0202 | 0.0351 | 0.0121 | 0.0422 | — | — | — | — | — | 0.1316 |

## Observations

**7/10 completers.** Fewer than Python (10/10) and Ruby (10/10), but more than
ReScript run 2 (2/10).

**`kimi-coding/k2p5` wins the full-completion speed race.** 260s total across all 10 parts,
beating `claude-opus-4-6` by 12 seconds.

**`claude-opus-4-6` is fast but expensive.**
272s total (second place), but **$1.1352** total cost — more than 8× `k2p5`.

**`claude-sonnet-4-6` is the token-efficiency winner among completers.**
12,068 output tokens total, slightly lower than `k2p5`'s 12,268.

**`qwen3.5-plus` is fast-ish but verbose.** 356s total is solid (4th), but 30,683 output
tokens is over 2.5× `sonnet` and `k2p5`.

**Day 1 Part 2 was the slowest part overall.** Three models eventually passed only on a
second clean attempt (`haiku`, `glm-5`, `MiniMax-M2.5`), producing 403–526s times.

**`gpt-5.3-codex`** — fast early (D1P2: 13s, D2P2: 11s), then ejected on D3P1 for
no-progress behavior after a retry nudge.

**`qwen3-coder-next`** — spent ~$0.98 on one failed puzzle part (D1P2). Solved D1P1 in
79s, then failed D1P2 retries and was ejected.

## Cross-language snapshot

| Language | Models completing all 10 parts |
| -------- | ------------------------------ |
| Python | 10/10 |
| Ruby | 10/10 |
| Elixir | 7/10 |
| Haskell | 7/11 |
| OCaml | 5/9 |
| ReScript (run 2) | 2/10 |

Elixir lands very close to Haskell in completion rate on this benchmark, but with a very
different shape of failures (more behavioral/retry-loop failures, fewer pure language/tooling
barriers).

## What's next

If I extend this Elixir run beyond Day 5 in a follow-up benchmark, it'll be interesting to
see whether the same seven-model pack holds through later, trickier puzzles — or whether
another wave of ejections appears.

*Benchmarked on 2026-02-26 using [pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent) as the agent harness.*

---

*This post was written with AI assistance.*
