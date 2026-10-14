# IAI_SLE4
# SLE-4: Final Viva & Architecture Decision Record (ADR)

**Course:** 02AML204 – Introduction to Artificial Intelligence
**PRN:** 25UAM021
**Name:** Shravani Mahadev Asawale
**Division:** A
**Date:** 11 October 2026

---

## 📌 Overview

This repository contains the **Architecture Decision Record (ADR)** for the 8-Puzzle Solver System, along with the final viva preparation notes and a summary of the complete SLE journey (SLE-1 → SLE-4).

The central decision documented here is:

> **Use Breadth-First Search (BFS) over Depth-First Search (DFS) for optimal 8-Puzzle solving.**

This decision is backed by real profiling data collected in SLE-2 and the modular C4 architecture designed in SLE-3.

---

## 📂 Contents

| File | Description |
|---|---|
| `SLE4_25UAM021.docx` | Original Word document (full ADR + viva notes) |
| `README.md` | This file |

---

## 🧩 The Decision at a Glance

**Context:** The 8-Puzzle Solver needs a search algorithm to find a path from a scrambled state to the goal state.

**Decision:** BFS is used as the **primary solver**. DFS is kept only as a **secondary comparison algorithm** for profiling and educational purposes.

**Why:** BFS guarantees the shortest path and, in the profiled puzzle, was dramatically faster and more memory-efficient.

---

## 📊 Evidence (from SLE-2 Profiling)

Same start state `(1,2,3,4,0,6,7,5,8)` and goal state `(1,2,3,4,5,6,7,8,0)` were used for both algorithms.

| Criterion | BFS | DFS |
|---|---|---|
| **Data structure** | FIFO queue | LIFO stack |
| **Execution time** | 0.0763 ms | 543.56 ms |
| **Nodes expanded** | 9 | 135,586 |
| **Max frontier size** | 8 | 42,912 |
| **Solution path length** | 3 moves (optimal) | 49,285 moves (non-optimal) |
| **Optimality guarantee** | ✅ Yes | ❌ No |

**Result:** BFS was ~7,126× faster and expanded ~15,000× fewer nodes than DFS.

---

## 🔄 Alternatives Considered

1. **Breadth-First Search (BFS)** ✅ *Chosen* — FIFO queue, level-by-level, guaranteed shortest path.
2. **Depth-First Search (DFS)** ❌ *Rejected as default* — LIFO stack, memory-efficient but non-optimal.
3. **A\* Search with Manhattan Distance Heuristic** 🔮 *Future work* — not implemented in SLE-1/SLE-2, but a natural next step for larger puzzles.

---

## ⚖️ Consequences

**Positive**
- Guarantees the shortest possible solution path.
- Completes shallow puzzles in under 0.1 ms.
- Small frontier keeps memory usage low.
- Easy to verify (BFS is a standard, well-understood algorithm).

**Negative / Trade-offs**
- Memory grows exponentially with depth — not suitable for very deep puzzles (e.g., 15-puzzle).
- DFS is still retained for comparison and memory-constrained cases.

**Review Trigger**
Revisit this decision if:
- The system is extended to a larger puzzle (e.g., 15-puzzle),
- Memory limits become a constraint,
- A\* is implemented and profiled with better results.

---

## 🛠️ SLE Journey Summary

| Stage | Focus | What Was Done |
|---|---|---|
| **SLE-1** | Build | Implemented BFS & DFS search code, Contribution Log, README |
| **SLE-2** | Measure | Profiled BFS vs DFS on the same puzzle (time, nodes, frontier, path length) |
| **SLE-3** | Design | Created C4 architecture (Context, Container, Component, Code) with PlantUML & draw.io |
| **SLE-4** | Decide | Recorded the BFS-over-DFS decision as an ADR using SLE-2 evidence and SLE-3 design |

**Takeaway:** A good engineering decision comes from *building* something that works, *measuring* it, *designing* it clearly, and then *explaining* the choice with evidence.

---

## 🤖 AI Contribution Note

- **AI tool used:** DeepSeek (web interface)
- **AI helped with:** Structuring the ADR format, phrasing the rationale, and suggesting viva questions.
- **Done by me:** Ran all BFS/DFS experiments, collected the actual numbers, drew the C4 diagrams, made the BFS-vs-DFS decision, and verified every number against the SLE-2 report and code.

------

## 🔗 Links

- **GitHub Profile:** [https://github.com/Shravaniasawale15](https://github.com/Shravaniasawale15)

---

## 📜 References

- SLE-2 Report: Algorithms Profiled — BFS vs DFS on 8-Puzzle
- SLE-3 Report: C4 Architecture of the 8-Puzzle Solver
- SLE-2 GitHub Repository: [IAI_SLE2](https://github.com/Shravaniasawale15/IAI_SLE2)
