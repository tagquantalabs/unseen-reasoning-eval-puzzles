<p align="center">
  <img src="images/fulllogo_transparent_nobuffer.png" alt="Quanta Labs" width="280"/>
</p>

# Unseen Reasoning Eval Datasets and Puzzles

Fresh reasoning evaluation puzzles in ARC-AGI format. Human-designed, human-verified, never published anywhere. If your model scores well on these, it earned it.

## Why we do this

Public benchmarks are leaking into training data, and it's affecting scores. The ARC Prize 2025 report found that leading labs use [correct ARC color mappings in their reasoning without being told the format](https://arxiv.org/abs/2601.10904),suggesting these models have seen ARC data during training. ARC-AGI-2 shows signs of knowledge-dependent overfitting as well.

ARC-AGI-3 is now entirely new and interactive, where the best AIs are hitting <1%, so essentially just random (could be different tomorrow, I am not having a Clawbot check leaderboards constantly).

**These puzzles are clearly held out.** They don't exist in any public dataset, any crawl, or any training corpus. Every task is designed from scratch by human experts and independently verified before release. No LLM was involved in creating them.

## What we are sharing

One sample puzzle and a drop-in browser viewer. Standard ARC-AGI format. Grids are N×M integer matrices (0–9). Compatible with existing ARC tooling out of the box.

## Sample: Signal Propagation with Arithmetic Gates

![Train pair 1](images/train_pair_1.png)
![Train pair 2](images/train_pair_2.png)
![Train pair 3](images/train_pair_3.png)

Four emitter types fire beams in fixed directions (blue → up, red → right, green → down, yellow → left). Orange gates deflect beams 90° clockwise. When beams of different colors collide, they mix (magenta for 2 colors, azure for 3+). Emitters whose trail cells are fully overwritten get marked dead.

The puzzle requires applying all rules in sequence across grids of increasing size. Full rule spec and color map are in the JSON.

## Format

```json
{
  "id": "ql-signal-propagation-001",
  "type": "spatial_logic",
  "difficulty": "medium",
  "rules": {
    "description": "...",
    "elements": { "0": "empty", "1": "blue — emitter, fires UP", "..." : "..." },
    "steps": [ "Rule 1 — Fire: ...", "Rule 2 — Propagation: ...", "..." ],
    "notes": [ "..." ]
  },
  "train": [
    { "input": [[0,1,...], ...], "output": [[0,5,...], ...] }
  ],
  "test": [
    { "input": [[...]], "output": [[...]] }
  ],
  "coverage": {
    "features_exercised": ["all_4_beam_directions", "gate_deflection", "..."]
  }
}
```

The `rules` and `coverage` fields are our additions to the standard ARC format — they document exactly what reasoning each puzzle tests and what each training pair covers. To get vanilla ARC compatibility, use only the input/output grids. The rules and coverage fields are there for your own analysis.

## How we build these

Each puzzle goes through a simple pipeline: a human expert designs the rule system and grids from scratch, a separate person solves it without seeing the intended answer to confirm it's unambiguous, and we validate that training pairs cover the full rule set and edge cases.

## More puzzles

This is a sample from a larger library. Different difficulties, different grid sizes, custom noise levels and edge cases. Custom eval sets available on request. We build tasks across spatial logic, constraint propagation, multi-step transformations, and pattern completion families.

## License

CC BY-NC 4.0. Free for research and evaluation with attribution. 

## Contact

**tag@quanta-labs.ai** · [quanta-labs.ai](https://quanta-labs.ai)

Ran your model on these? We'd love to hear how it did and what surprised you.

---

<p align="center">Built by <a href="https://quanta-labs.ai">Quanta Labs</a> · Munich, Germany</p>