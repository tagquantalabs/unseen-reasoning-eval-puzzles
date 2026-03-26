<p align="center">
  <img src="images/fulllogo_transparent_nobuffer.png" alt="Quanta Labs" width="280"/>
</p>

# Unseen Reasoning Eval Puzzles

Private reasoning evaluation puzzles for AI models. Multi-step, rule-based grid tasks. Unseen by any model.

## Why

Public benchmarks leak into training data. Models overfit to them. ARC-AGI's 2025 report covers this in detail ([Chollet et al., 2025](https://arxiv.org/abs/2601.10904)). [ARC Prize 2026](https://arcprize.org/competitions/2026) responds with ARC-AGI-3, where the best AI scores 12.58% against a 100% human baseline.

These puzzles are held out. They do not exist in any public dataset. Every puzzle is crafted by human experts with verified solutions.

## What's here

One puzzle, one viewer.

- `puzzles/signal_propagation.json` — spatial logic, 6 rules, 6 training pairs, 1 test pair, grids from 12x12 to 20x20
- `viewer/arc_puzzle_viewer.html` — browser-based, works with any puzzle JSON in this format

## Signal Propagation with Arithmetic Gates

![Train pair 1](images/train_pair_1.png)
![Train pair 2](images/train_pair_2.png)
![Train pair 3](images/train_pair_3.png)

Four emitter types fire beams in fixed directions (blue=up, red=right, green=down, yellow=left). Orange gates deflect beams 90° clockwise. Collisions between beam colors produce magenta (2 colors) or azure (3+). Emitters with no surviving trail cells are marked dead.

Full rules and color map are in the JSON.

## Format

```json
{
  "id": "ql-signal-propagation-001",
  "type": "spatial_logic",
  "difficulty": "medium",
  "rules": {
    "description": "...",
    "elements": { "0": "empty", "1": "blue — emitter, fires UP", ... },
    "steps": [ "Rule 1 — Fire: ...", "Rule 2 — Propagation: ...", ... ],
    "notes": [ "..." ]
  },
  "train": [
    { "input": [[0,1,...], ...], "output": [[0,5,...], ...] }
  ],
  "test": [
    { "input": [[...]], "output": [[...]] }
  ],
  "coverage": {
    "features_exercised": ["all_4_beam_directions", "gate_deflection", ...]
  }
}
```

Grids are NxN integer matrices (0-9). Compatible with ARC-AGI tooling.

## More puzzles

We maintain additional puzzle families covering spatial logic, constraint propagation, and multi-step transformation tasks. Custom evaluation sets available on request.

**tag@quanta-labs.ai** | [quanta-labs.ai](https://quanta-labs.ai)

---

<p align="center">Built by <a href="https://quanta-labs.ai">Quanta Labs</a> &middot; Munich, Germany</p>
