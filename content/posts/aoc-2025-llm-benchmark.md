+++
title = "Benchmarking LLMs on Advent of Code 2025 (Haskell)"
date = 2025-02-24T19:30:00+01:00
description = "Pitting 11 LLMs against each other on AoC 2025 puzzles, solved in Haskell — tracking correctness and speed"

[taxonomies]
tags = ["Haskell", "AI", "Advent of Code"]
+++

I benchmarked 11 LLMs on [Advent of Code 2025](https://adventofcode.com/2025) Days 1–5, each solving independently in **Haskell**. The goal: see which models can reliably produce correct, working solutions — and how fast.

<!-- more -->

## How it works

I built a custom orchestration prompt for [pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent), a CLI coding agent. The prompt acts as a benchmark controller: it launches one `pi` agent per model in separate tmux windows, feeds them the puzzle description, waits for them to finish, collects their answers, scores them for correctness and time-to-solution, and maintains a leaderboard. Models that fail a puzzle get ejected from the competition.

Each agent works in complete isolation — its own directory, no shared state, no awareness of the others. They all get the same puzzle description and input files. The orchestrator never solves anything itself; it just dispatches, collects, and scores.

## The contestants

All 11 models came from my enabled model list:

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
| 9 | `alibaba/qwen3-max-2026-01-23` |
| 10 | `alibaba/qwen3-coder-next` |
| 11 | `alibaba/qwen3-coder-plus` |

## Ejections

Models that failed a puzzle were offered for ejection. Four models didn't survive past Day 1:

| Model | Ejected at | Reason |
| ------:| ---------:| ------:|
| `alibaba/qwen3-coder-plus` | D1P1 | No answer (never wrote ANSWER.txt) |
| `mistral/devstral-2512` | D1P2 | Wrong answer |
| `alibaba/qwen3-coder-next` | D1P2 | Wrong answer |
| `alibaba/qwen3-max-2026-01-23` | D1P2 | No answer (got the right answer but stopped before writing the file!) |

The `qwen3-max` case was particularly painful — the model computed the correct answer, said "Now I'll write the answer to ANSWER.txt:" and then... just stopped generating. The answer was right there. 😩

## Results (Days 1–5)

The surviving 7 models went on a perfect streak through Days 1–5, all producing correct answers for every part. Here's the full timing breakdown:

<br>

### Per-task leaderboards

<br>

#### Day 1 Part 1 — Dial rotation counting

| Model | Time |
| ------:| ----:|
| mistral/devstral-2512 | 33s |
| anthropic/claude-opus-4-6 | 40s |
| anthropic/claude-sonnet-4-6 | 41s |
| kimi-coding/k2p5 | 42s |
| alibaba/qwen3.5-plus | 45s |
| openai-codex/gpt-5.3-codex | 50s |
| zai/glm-5 | 70s |
| alibaba/qwen3-coder-next | 74s |
| alibaba/qwen3-max-2026-01-23 | 78s |
| minimax/MiniMax-M2.5 | 111s |

<br><br>
#### Day 1 Part 2 — Counting zero-crossings during dial rotation

| Model | Time |
| ------:| ----:|
| anthropic/claude-opus-4-6 | 32s |
| anthropic/claude-sonnet-4-6 | 39s |
| openai-codex/gpt-5.3-codex | 53s |
| kimi-coding/k2p5 | 70s |
| alibaba/qwen3.5-plus | 85s |
| zai/glm-5 | 130s |
| minimax/MiniMax-M2.5 | 972s |

<br><br>
#### Day 2 Part 1 — Summing repeated-digit IDs in ranges

| Model | Time |
| ------:| ----:|
| openai-codex/gpt-5.3-codex | 17s |
| kimi-coding/k2p5 | 41s |
| alibaba/qwen3.5-plus | 45s |
| anthropic/claude-sonnet-4-6 | 53s |
| anthropic/claude-opus-4-6 | 54s |
| zai/glm-5 | 72s |
| minimax/MiniMax-M2.5 | 113s |

<br><br>
#### Day 2 Part 2 — Repeated-pattern IDs (any repeat count)

| Model | Time |
| ------:| ----:|
| openai-codex/gpt-5.3-codex | 22s |
| kimi-coding/k2p5 | 22s |
| alibaba/qwen3.5-plus | 25s |
| anthropic/claude-sonnet-4-6 | 31s |
| minimax/MiniMax-M2.5 | 38s |
| anthropic/claude-opus-4-6 | 41s |
| zai/glm-5 | 63s |

<br><br>
#### Day 3 Part 1 — Maximizing 2-digit joltage from battery banks

| Model | Time |
| ------:| ----:|
| anthropic/claude-sonnet-4-6 | 28s |
| kimi-coding/k2p5 | 30s |
| anthropic/claude-opus-4-6 | 32s |
| zai/glm-5 | 39s |
| openai-codex/gpt-5.3-codex | 41s |
| alibaba/qwen3.5-plus | 42s |
| minimax/MiniMax-M2.5 | 1078s |

<br><br>
#### Day 3 Part 2 — Maximizing 12-digit joltage from battery banks

| Model | Time |
| ------:| ----:|
| openai-codex/gpt-5.3-codex | 19s |
| alibaba/qwen3.5-plus | 24s |
| anthropic/claude-sonnet-4-6 | 27s |
| anthropic/claude-opus-4-6 | 30s |
| zai/glm-5 | 37s |
| kimi-coding/k2p5 | 71s |
| minimax/MiniMax-M2.5 | 473s |

<br><br>
#### Day 4 Part 1 — Grid neighbor counting (accessible paper rolls)

| Model | Time |
| ------:| ----:|
| openai-codex/gpt-5.3-codex | 27s |
| alibaba/qwen3.5-plus | 27s |
| anthropic/claude-sonnet-4-6 | 28s |
| anthropic/claude-opus-4-6 | 33s |
| kimi-coding/k2p5 | 36s |
| zai/glm-5 | 70s |
| minimax/MiniMax-M2.5 | 707s |

<br><br>
#### Day 4 Part 2 — Iterative grid removal simulation

| Model | Time |
| ------:| ----:|
| openai-codex/gpt-5.3-codex | 23s |
| anthropic/claude-sonnet-4-6 | 24s |
| alibaba/qwen3.5-plus | 24s |
| anthropic/claude-opus-4-6 | 28s |
| kimi-coding/k2p5 | 37s |
| zai/glm-5 | 39s |
| minimax/MiniMax-M2.5 | 166s |

<br><br>
#### Day 5 Part 1 — Range membership checking

| Model | Time |
| ------:| ----:|
| openai-codex/gpt-5.3-codex | 27s |
| anthropic/claude-sonnet-4-6 | 28s |
| alibaba/qwen3.5-plus | 28s |
| anthropic/claude-opus-4-6 | 32s |
| kimi-coding/k2p5 | 33s |
| zai/glm-5 | 72s |
| minimax/MiniMax-M2.5 | 140s |

<br><br>
#### Day 5 Part 2 — Counting total fresh IDs from overlapping ranges

| Model | Time |
| ------:| ----:|
| openai-codex/gpt-5.3-codex | 20s |
| kimi-coding/k2p5 | 20s |
| anthropic/claude-sonnet-4-6 | 23s |
| anthropic/claude-opus-4-6 | 24s |
| alibaba/qwen3.5-plus | 28s |
| minimax/MiniMax-M2.5 | 44s |
| zai/glm-5 | 54s |

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
      <td>openai-codex/gpt-5.3-codex</td>
      <td style="text-align: right">50s</td>
      <td style="text-align: right">53s</td>
      <td style="text-align: right">17s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">41s</td>
      <td style="text-align: right">19s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">23s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">20s</td>
    </tr>
    <tr>
      <td>anthropic/claude-sonnet-4-6</td>
      <td style="text-align: right">41s</td>
      <td style="text-align: right">39s</td>
      <td style="text-align: right">53s</td>
      <td style="text-align: right">31s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">23s</td>
    </tr>
    <tr>
      <td>anthropic/claude-opus-4-6</td>
      <td style="text-align: right">40s</td>
      <td style="text-align: right">32s</td>
      <td style="text-align: right">54s</td>
      <td style="text-align: right">41s</td>
      <td style="text-align: right">32s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">33s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">32s</td>
      <td style="text-align: right">24s</td>
    </tr>
    <tr>
      <td>kimi-coding/k2p5</td>
      <td style="text-align: right">42s</td>
      <td style="text-align: right">70s</td>
      <td style="text-align: right">41s</td>
      <td style="text-align: right">22s</td>
      <td style="text-align: right">30s</td>
      <td style="text-align: right">71s</td>
      <td style="text-align: right">36s</td>
      <td style="text-align: right">37s</td>
      <td style="text-align: right">33s</td>
      <td style="text-align: right">20s</td>
    </tr>
    <tr>
      <td>alibaba/qwen3.5-plus</td>
      <td style="text-align: right">45s</td>
      <td style="text-align: right">85s</td>
      <td style="text-align: right">45s</td>
      <td style="text-align: right">25s</td>
      <td style="text-align: right">42s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">27s</td>
      <td style="text-align: right">24s</td>
      <td style="text-align: right">28s</td>
      <td style="text-align: right">28s</td>
    </tr>
    <tr>
      <td>zai/glm-5</td>
      <td style="text-align: right">70s</td>
      <td style="text-align: right">130s</td>
      <td style="text-align: right">72s</td>
      <td style="text-align: right">63s</td>
      <td style="text-align: right">39s</td>
      <td style="text-align: right">37s</td>
      <td style="text-align: right">70s</td>
      <td style="text-align: right">39s</td>
      <td style="text-align: right">72s</td>
      <td style="text-align: right">54s</td>
    </tr>
    <tr>
      <td>minimax/MiniMax-M2.5</td>
      <td style="text-align: right">111s</td>
      <td style="text-align: right">972s</td>
      <td style="text-align: right">113s</td>
      <td style="text-align: right">38s</td>
      <td style="text-align: right">1078s</td>
      <td style="text-align: right">473s</td>
      <td style="text-align: right">707s</td>
      <td style="text-align: right">166s</td>
      <td style="text-align: right">140s</td>
      <td style="text-align: right">44s</td>
    </tr>
    <tr><td colspan="11" style="text-align: center; font-style: italic; opacity: 0.6">— ejected —</td></tr>
    <tr>
      <td>mistral/devstral-2512</td>
      <td style="text-align: right">33s</td>
      <td style="text-align: right">✗</td>
      <td colspan="8"></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-next</td>
      <td style="text-align: right">74s</td>
      <td style="text-align: right">✗</td>
      <td colspan="8"></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-max-2026-01-23</td>
      <td style="text-align: right">78s</td>
      <td style="text-align: right">✗(—)</td>
      <td colspan="8"></td>
    </tr>
    <tr>
      <td>alibaba/qwen3-coder-plus</td>
      <td style="text-align: right">✗(—)</td>
      <td colspan="9"></td>
    </tr>
  </tbody>
</table>

## Observations

**The top tier** — `openai-codex/gpt-5.3-codex`, `anthropic/claude-sonnet-4-6`, and `anthropic/claude-opus-4-6` were consistently fast and correct. GPT-5.3-Codex was often the fastest, with the Anthropic models close behind.

**Solid mid-pack** — `kimi-coding/k2p5` and `alibaba/qwen3.5-plus` were reliable and reasonably quick, occasionally matching the top performers.

**Consistent but slow** — `zai/glm-5` always got the right answer but typically took 2–3x longer than the leaders.

**The outlier** — `minimax/MiniMax-M2.5` always got the right answer eventually, but with wildly inconsistent timing. It ranged from 38s (competitive) to 1078s (18 minutes!) for puzzles others solved in under a minute. Something about its approach leads to very expensive wrong turns before converging.

**Early casualties** — The four ejected models all failed on the very first day. `mistral/devstral-2512` was actually the _fastest_ on D1P1 (33s!) but got Part 2 wrong. `qwen3-max` was the most frustrating: it computed the correct answer and then stopped generating before writing it to disk.

**Haskell competency** — All surviving models demonstrated solid Haskell knowledge. They correctly used standard libraries, handled I/O, parsed input, and produced clean, compilable code. The early AoC puzzles are not algorithmically complex, so the real test will come with later days.

## Methodology

### Orchestration

The whole benchmark is driven by a custom `pi` prompt that acts as a controller. It:

- Reads the enabled model list from pi's settings
- Creates an isolated working directory per model
- Launches each model as a separate `pi` agent in its own tmux window
- Feeds puzzle descriptions (pasted by the operator) into each model's directory
- Waits for agents to finish, then reads their `ANSWER.txt` files
- Compares answers, displays leaderboards, and handles ejections
- For Part 2, reuses the same tmux sessions so agents keep their Part 1 context (since AoC Part 2 typically builds on Part 1)

The orchestrator never reads puzzle descriptions itself and never solves anything — it only dispatches and scores.

### Timing

- Elapsed time = `ANSWER.txt` file modification time − launch time − stagger offset
- Agents are launched with a **3-second stagger** between each to avoid a lock file race condition in pi's settings. Each model's offset is subtracted from its raw time
- Times include the full cycle: reading the puzzle, writing Haskell code, compiling with GHC, testing against example input, running against real input, and writing the answer

### Fairness controls

- **Thinking/reasoning disabled** (`--thinking off`) — keeps things fair across models that support extended thinking differently
- **5-second execution timeout** — prevents runaway brute-force solutions from locking up the machine
- **`nice -n 10`** on all agent processes — prevents CPU starvation with 7+ concurrent compilations and executions
- **No shared state** — each model works in its own directory with no awareness of others
- **Same prompt for all** — every agent receives identical instructions and input paths

### Caveats

- This is a single run, not averaged over multiple attempts. Results may vary on repeated runs
- Day 1 Part 1 ran without the `--thinking off` flag and without stagger offset correction (those improvements were introduced mid-session)
- Day 1 used a 10s execution timeout; this was reduced to 5s from Day 2 onward
- The benchmark is ongoing — results will be updated as we progress through more days
- Network latency to different API providers may contribute to timing differences

*Benchmarked on 2025-02-24 using [pi](https://github.com/badlogic/pi-mono/tree/main/packages/coding-agent) as the agent harness.*

## The full orchestration prompt

The prompt below is what drives the entire benchmark. It's a pi "skill" — a markdown file that turns the agent into a benchmark controller. I paste puzzle descriptions into the chat, and the orchestrator handles everything else.

<details>
<summary>Click to expand the full prompt (~280 lines of markdown)</summary>

````markdown
You are the **Benchmark AOC** orchestrator. You guide the user through benchmarking
multiple LLMs on Advent of Code puzzles, one part at a time. You dispatch work to agents,
collect results, maintain a leaderboard, and eject underperforming models as you go.

## Arguments

Parse:
- **Year** (e.g. `2025`) — required, ask if not provided
- **Language** (e.g. `Haskell`, `Ruby`, `Go`) — required, ask if not provided
- **Thinking level** (`off`, `minimal`, `low`, `medium`, `high`, `xhigh`) — optional, ask if
  not provided. This sets the `--thinking` flag uniformly for all models, keeping the
  benchmark fair. If a model doesn't support extended thinking, pi handles it gracefully.

Example invocations: `/benchmark-aoc 2025 Haskell high`, `/benchmark-aoc 2025 Ruby medium`

---

## Required filesystem layout

The inputs base is: `/home/benjamin/benchmark/aoc-inputs/<year>/inputs/`

Each day has a subdirectory:

    DayNN/
      input.example       ← small example input (can be pre-staged for all days)
      input.real          ← the actual puzzle input (can be pre-staged for all days)

Puzzle descriptions are **not** stored in the shared inputs directory. Instead, the user
pastes them directly into the chat, and the orchestrator writes them to each active model's
subdirectory as `PART_<P>.description`. This prevents stale descriptions from leaking across
re-runs and ensures no agent sees a description before it's time.

Zero-pad the day number: `Day01`, `Day02`, ..., `Day09`, `Day10`, etc.

---

## State (track across the session)

- `active_models`: list of model names still in the benchmark (starts as all enabled models)
- `windows`: map of `model → tmux window name`
- `subdirs`: map of `model → absolute path of its work subdirectory`
- `work_dir`: the directory the prompt was launched from (captured at setup)
- `inputs_base`: `/home/benjamin/benchmark/aoc-inputs/<year>/inputs`
- `language`: target language
- `thinking`: thinking level (e.g. `high`)
- `current_day`: integer, starts at 1
- `leaderboard`: accumulated results across all days and parts

---

## Setup (once per session)

### 1. Get model list

    cat ~/.pi/agent/settings.json | jq -r '.enabledModels[]'

This is the starting `active_models` list. Show it to the user.

### 2. Set work directory

The work directory is wherever the user launched this prompt from. Store it as `work_dir`.
Model subdirectories will be created inside this directory.

### 3. Create subdirectory per model

For each model, create `<work_dir>/<model-subdir>/` where the subdir name is the full model
name with `/` replaced by `__`.

Example: `anthropic/claude-opus-4-6` → `anthropic__claude-opus-4-6/`

---

## Main loop

Repeat for each day (1–25), parts 1 then 2, until all models are ejected or day 25 part 2
is complete.

---

### Phase A — Launch

**1. Verify input files and collect description**

Check that `input.example` and `input.real` exist. If input files are missing, tell the user
and wait.

Then ask the user to paste the puzzle description. When the user pastes it, write the
description to `<subdir>/PART_<P>.description` for **each active model's subdirectory**.
This keeps descriptions scoped per-model and per-run — no shared files that could leak
across re-runs.

**2. Clear stale ANSWER.txt files**

For each model in `active_models`:

    rm -f <subdir>/ANSWER.txt

**3. Record start time**

    date +%s

Store as `start_time`.

**4. Launch tmux windows**

For each model in `active_models`, open a new tmux window with a **3-second delay** between
each launch. Multiple `pi` instances starting simultaneously will fight over the global
settings lock file and crash. The stagger gives each instance time to acquire the lock, read
config, and release it.

Because of the stagger, **subtract each model's launch offset** when computing elapsed time.
Model #0 (launched first) gets 0s subtracted, model #1 gets 3s, model #2 gets 6s, etc.

    tmux new-window -n <window-name> -c <subdir> \
      "nice -n 10 pi --model <model> --thinking <thinking> '<prompt>'"
    sleep 3

The agent prompt tells the model to:
- Read the puzzle description from `./PART_<P>.description`
- Read example and real inputs from the shared inputs directory
- Verify against the example input first, then run against the real input
- Always run solutions with a 5-second timeout
- Write ONLY the final answer to `ANSWER.txt`
- Say DONE when finished

Window name = full model name with `/` replaced by `__` and `.` replaced by `_`.
The `.` replacement prevents tmux from interpreting `.` as a pane separator in `-t` targets.

**5. Tell the user**

Report how many agents were launched. Then wait for the user to type `done`.

---

### Phase B — Collect results

When the user types `done`:

**1. Read results**

For each model, read `ANSWER.txt` and compute elapsed time (file mtime − start_time).

**2. Ask for the correct answer**

Wait for the user's reply. Trim whitespace from both answers before comparing.

**3. Display leaderboard for this task**

Sort passing models by elapsed time (fastest first), then failing models below.

**4. Eject failing models**

For each model that gave a wrong or missing answer, ask the user whether to eject it.
For each confirmed ejection, kill its tmux window and remove it from `active_models`.

If no models remain, show the final leaderboard and stop.

---

### Phase C — Advance

#### If this was Part 1 → move to Part 2

Part 2 reuses the same tmux sessions. This is intentional — the agents keep their Part 1
context, which helps since AoC Part 2 typically builds on Part 1.

1. Ask the user to paste the Part 2 description. Write it to each surviving model's subdir.
2. Clear ANSWER.txt in each surviving model's subdir.
3. Record new `start_time`.
4. Inject Part 2 into surviving tmux windows via `tmux send-keys`.
5. Tell the user and wait for `done`. → Go to Phase B.

#### If this was Part 2 → move to next day

1. Increment `current_day`. If > 25, show the final leaderboard and stop.
2. Kill all surviving tmux windows. Fresh windows will be created by Phase A.
3. Go to Phase A.

---

## Final leaderboard

When all models are ejected or day 25 part 2 is complete, display a full summary table
showing times for passing cells and ✗ for failing cells.

---

## Rules

- NEVER solve puzzles yourself
- NEVER read puzzle descriptions — only write them to model subdirs and point agents there
- NEVER ask the user for a description for a part they haven't reached yet
- NEVER kill a tmux window without telling the user first
- ALWAYS write descriptions to each active model's subdir before launching
- ALWAYS clear ANSWER.txt before each new launch
- ALWAYS trim whitespace when comparing answers
````

</details>

---

<br>

## Disclaimer

*This post was written with AI assistance to maximize efficiency given my time constraints.*
