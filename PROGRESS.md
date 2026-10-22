# Development progress

This log records work actually completed and checks actually run. Dates use Asia/Almaty. See [PLAN.md](PLAN.md) for the scheduled milestones.

| Day | Date | Milestone | Status |
| --- | --- | --- | --- |
| 1 | 22 Oct 2026 | Project setup and weighted graph model | Complete |
| 2 | 23 Oct 2026 | Disjoint set union | Planned |
| 3 | 24 Oct 2026 | Kruskal MST | Planned |
| 4 | 25 Oct 2026 | Prim MST and comparison | Planned |
| 5 | 26 Oct 2026 | Topological ordering | Planned |
| 6 | 27 Oct 2026 | Strongly connected components | Planned |
| 7 | 28 Oct 2026 | Dijkstra shortest paths | Planned |
| 8 | 29 Oct 2026 | Graph generation and benchmarks | Planned |
| 9 | 30 Oct 2026 | Plots and report | Planned |
| 10 | 31 Oct 2026 | Final verification and submission preparation | Planned |

## 22 October 2026 — Day 1

Completed:

- Recorded the ten-day plan and configured a daily run in this chat at 18:00, ending on 31 October. Commits are made when changes are ready; they have no fixed time of day.
- Added the package structure, an immutable `Edge` record, and `WeightedGraph` with directed and undirected adjacency lists.
- Defined behavior for edge counting, parallel edges, self-loops, invalid vertices, and read-only collection access.
- Replaced the starter output with a four-district graph demonstration.
- Added JDK-only build, run, and assertion-test scripts, plus ignore rules for build output and IDE files.
- Started the README report with graph design, representation complexity, commands, and clearly marked future work.

Checks performed:

- `bash scripts/test.sh`: all **11 graph tests passed**; compilation with `--release 17 -Xlint:all` produced no warnings.
- `bash scripts/run.sh`: printed **4 districts and 4 roads**, with the expected endpoints and weights.
- Runtime available: Eclipse Temurin OpenJDK **17.0.20.1**. Maven is not installed, so the project uses the JDK directly and requires no Java dependencies.

Decision: keep the shared graph model general enough for all three tasks. Negative weights remain representable for MST inputs; Dijkstra will validate its non-negative-weight requirement when implemented. Tests verify that an invalid edge cannot partially modify the graph.

Next step: on 23 October, implement DSU with path compression and union by size, add its correctness tests, and document its complexity. Later algorithms and benchmarks have not been implemented yet.
