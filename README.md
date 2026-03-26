<p align="center">
  <img src="images/fulllogo_transparent_nobuffer.png" alt="Quanta Labs" width="280"/>
</p>

# Unseen Reasoning Eval Puzzles

**Reasoning evaluation puzzles no model has ever seen.**

Public benchmarks get contaminated. Models train on them. Scores go up, but reasoning ability does not. ARC-AGI's 2025 technical report documented this as "knowledge-dependent overfitting": models memorize surface patterns rather than learning to reason ([Chollet et al., 2025](https://arxiv.org/abs/2601.10904)). The newly launched [ARC Prize 2026](https://arcprize.org/competitions/2026) ($2M in prizes) raises the bar further with ARC-AGI-3, an interactive benchmark where agents must learn from experience inside novel environments with no instructions and no stated goals. The best AI so far scores 12.58% against a human baseline of 100%.

The problem is clear: we need harder, private, uncontaminated evaluation tasks.

We build exactly that. Rule-based reasoning puzzles generated from scratch, with formal specifications, training pairs (input/output grids), and held-out test pairs. None of this data has appeared in any training corpus. This repo is a single sample from our evaluation suite, along with a browser-based viewer to explore it.

---

## Sample: Signal Propagation with Arithmetic Gates

| | |
|---|---|
| **Type** | Spatial logic |
| **Difficulty** | Medium |
| **Rules** | 6 |
| **Training pairs** | 6 |
| **Test pairs** | 1 |
| **Grid sizes** | 12x12 to 20x20 |

Four types of directional emitters fire beams simultaneously. Gates deflect beams 90 degrees clockwise. When beams from different emitter colors collide on a cell, the collision is marked (2-color = magenta, 3+ = azure). Emitters whose beams leave no unique trace are flagged as dead. Solving this requires tracking multiple beams across the grid, resolving intersections, and reasoning about second-order effects.

![Train pair 1](images/train_pair_1.png)
![Train pair 2](images/train_pair_2.png)
![Train pair 3](images/train_pair_3.png)

### Rules

| # | Rule |
|---|------|
| 1 | **Fire.** Each emitter fires a beam in a fixed direction: blue = up, red = right, green = down, yellow = left. All beams fire simultaneously. |
| 2 | **Propagation.** Beams travel cell by cell through empty (black) cells. A beam stops before the grid boundary, a wall (grey), or any emitter. Beams do not interact with each other during propagation. |
| 3 | **Gate deflection.** When a beam reaches an orange gate, it enters the gate, rotates 90 degrees clockwise, and continues in the new direction. Gates can be chained. A beam stops if it would re-enter a gate it already visited. |
| 4 | **Marking.** Each empty cell reached by exactly one beam takes the color of that beam's emitter. |
| 5 | **Collision.** If a cell is reached by beams from 2 distinct emitter colors, it becomes magenta (6). If reached by 3 or more distinct colors, it becomes azure (8). |
| 6 | **Dead emitter.** After all marking and collisions are resolved, any emitter whose color appears in zero trail cells is replaced with maroon (9). Dead emitters' beams still count toward collisions. |

### Color map

| Value | Color | Role |
|-------|-------|------|
| 0 | Black | Empty cell |
| 1 | Blue | Emitter (fires up) |
| 2 | Red | Emitter (fires right) |
| 3 | Green | Emitter (fires down) |
| 4 | Yellow | Emitter (fires left) |
| 5 | Grey | Wall (blocks beams) |
| 6 | Magenta | 2-color collision (output only) |
| 7 | Orange | Gate (deflects 90 degrees clockwise) |
| 8 | Azure | 3+-color collision (output only) |
| 9 | Maroon | Dead emitter (output only) |

---

## Viewer

Open `viewer/arc_puzzle_viewer.html` in any browser to explore the puzzle interactively. Load any puzzle JSON in this format, resize cells, toggle color labels, and inspect training and test pairs.

---

## Puzzle format

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

Grids are NxN matrices of integers 0-9. Grid sizes scale with difficulty. The format is compatible with standard ARC-AGI tooling.

---

## Want more?

This is one puzzle from one family. We currently maintain a large number of distinct puzzle families, each targeting different reasoning capabilities: spatial logic, recursive pattern application, constraint propagation, multi-agent simulation, and more. Every puzzle is generated programmatically with verified solutions, so we can produce new instances at any scale.

We also build custom evaluation sets on request. If you are benchmarking a reasoning system and need uncontaminated tasks with specific properties, we can help.

**Contact:** tag@quanta-labs.ai
**Website:** [quanta-labs.ai](https://quanta-labs.ai)

---

<p align="center">Built by <a href="https://quanta-labs.ai">Quanta Labs</a> &middot; Munich, Germany</p>
