# Assignment 3: 10-day development plan

Working dates: 22–31 October 2026. Assumed deadline: 1 November 2026; verify the exact submission time in the course system. If the deadline is earlier, shift the dates so the final check still happens before submission.

Starting point before work on 22 October: `Main.java` prints `Hello, World!`; the repository has no commits. This plan schedules the remaining work from that date. Budget approximately 2–3 focused hours per day, with extra time available for benchmarking and the report.

The daily Codex automation is scheduled at **18:00 Asia/Almaty**, through **31 October 2026**, in this chat. Each run checks `PROGRESS.md` and the Git history, completes the current milestone and unfinished prerequisites, and commits verified changes with their actual timestamps. A milestone already completed earlier that day is skipped. Work is committed locally until a GitHub remote is connected; after that, finished commits can be pushed. The schedule is recorded in the Codex app; this file documents it without creating a separate scheduler.

The three assignment tasks are MST, connectivity, and shortest paths. Benchmarking, analysis, testing, and the README report apply across them.

## Daily milestones

| Day | Date | Work | Evidence that the milestone is complete | Suggested commit subject |
| --- | --- | --- | --- | --- |
| 1 | 22 Oct | Set up the Java project and test runner. Establish the required packages and a weighted graph representation supporting directed and undirected edges. Start the README, `.gitignore`, and work log. | A documented build/test command works; graph tests cover edge insertion, direction, weights, and a single vertex. | `Set up project structure and weighted graph model` |
| 2 | 23 Oct | **Task 1:** implement DSU with path compression and union by size. Explain the approach and complexity in the README. | Tests cover separate sets, repeated unions, transitive connectivity, and merging vertices already in the same set. | `Implement disjoint sets with path compression and union by size` |
| 3 | 24 Oct | **Task 1:** implement Kruskal using DSU. Return selected edges, total weight, and whether all vertices are connected. | A hand-calculated example has the expected MST weight; disconnected input, equal weights, multiple valid MSTs, and a single vertex are covered. | `Implement Kruskal MST and connectivity detection` |
| 4 | 25 Oct | **Task 1:** implement Prim with a priority queue. Compare it with Kruskal and complete the MST explanation. | Both implementations return the same total weight on connected graphs, including graphs with multiple valid MSTs. Disconnected inputs are handled explicitly. | `Implement Prim MST and compare spanning tree weights` |
| 5 | 26 Oct | **Task 2:** implement topological ordering using Kahn's algorithm. Return a clear cycle result when a complete ordering is impossible. | Tests validate every directed edge against the returned order, and cover a DAG, disconnected DAG, directed cycle, and single vertex. | `Implement topological ordering with cycle detection` |
| 6 | 27 Oct | **Task 2:** implement SCC using Kosaraju's algorithm. Document its two passes and complexity. | Known graphs produce the expected component sets; every vertex occurs exactly once. Include isolated vertices, one large SCC, and several SCCs. | `Implement Kosaraju strongly connected components` |
| 7 | 28 Oct | **Task 3:** implement Dijkstra with a priority queue and predecessor tracking for path reconstruction. Reject negative weights and explain the algorithm's non-negative-weight assumption. | Tests verify expected distances and actual paths, including an unreachable vertex, zero-weight edges, equal-distance alternatives, and a single vertex. | `Implement Dijkstra distances and path reconstruction` |
| 8 | 29 Oct | Build reproducible graph generators and the benchmark runner. Run every applicable algorithm on all required sizes, five measured repetitions per experiment, and save timing and operation-count tables. | Results can be regenerated with one documented command. Tables include seed, V, E, average nanoseconds, operation counts, and graph type. MST generators always produce connected graphs; topological benchmarks include DAGs and cyclic graphs. | `Add reproducible graph benchmarks and operation counts` |
| 9 | 30 Oct | Create both required plots. Complete the README's analysis and discussion, using the measured results. Review all required report sections. | Plots show execution time against vertices and against edges. README includes tables, embedded plots, all time/space complexities, implementation assumptions, and explanations of observed differences. | `Document benchmark results, plots, and complexity analysis` |
| 10 | 31 Oct | Check the complete project from a fresh checkout, rerun the tests, verify reproducibility, fix remaining issues, and prepare submission. Keep this day as a buffer if earlier work slips. | Build and test commands succeed; benchmark/plot instructions work; README images render on GitHub; required files are tracked and pushed; the repository link is ready before the deadline. | `Finalize run instructions and submission checks` |

These are milestones, not a quota of commits. Use one commit for a coherent change or separate implementation, tests, and documentation when they are independently useful. Choose the final subject to describe the actual diff. Commit fixes when they arise, and record only checks that were really performed.

## Daily development routine

1. Read the previous work-log entry and choose the day's concrete outcome.
2. Implement that increment and check it with a small example and appropriate tests.
3. Update the relevant README explanation while the design decisions are fresh.
4. Review the diff, commit coherent changes, and push the day's finished work to GitHub.
5. Add a short work-log entry describing what changed, what was tested, what was learned, and what remains.

Keep the commit timestamps and work log aligned with the work actually done. The development record should show how the project evolved. Do not fill earlier dates with invented activity or split finished work into empty commits merely to increase the count.

Suggested work-log entry, starting on the actual date work is performed:

```text
Date:
Completed:
Tests/checks and outcomes:
Decision, issue, or finding:
Next step:
```

## Benchmark requirements for Day 8

| Configuration | Vertices | Edges |
| --- | ---: | ---: |
| Small | 10 | 30 |
| Medium | 100 | 500 |
| Large | 1,000 | 5,000 |

- Use a documented fixed random seed and the exact graph sizes above. Prefer no self-loops or duplicate endpoint pairs in generated benchmark graphs so the edge count is unambiguous; duplicate weights are valid.
- Generate a connected undirected graph by first building a spanning tree and then adding edges until the required count is reached. Use the same graph for Kruskal and Prim.
- Generate DAGs by choosing a vertex order and adding edges only forward in that order. Generate a separate cyclic directed graph with a guaranteed directed cycle. Document the procedure for SCC and Dijkstra inputs as well.
- Use non-negative weights for Dijkstra. Include unreachable vertices in correctness tests even if a benchmark instance happens to be fully reachable.
- Perform any JVM warm-up separately, then record five measured repetitions per algorithm and configuration. Explain the warm-up procedure in the report.
- Use `System.nanoTime()` around algorithm work. Keep generation, file writing, and console output outside the timed section. State whether essential setup such as Kruskal's edge sorting is included; include work required by the algorithm consistently.
- Use fresh mutable algorithm state on each repetition, and check result correctness outside the timed section. Define which operations are counted for each implementation; different counter definitions do not represent equal units of work.
- Record the Java version and execution environment. Preserve the measured tables and plot-generation instructions in the repository.

## README completion checklist

- Overview: city scenario and graph representation.
- Implementation: data structures, main design choices, and how to build/run.
- Complexity Analysis: time and space for DSU find/union, Kruskal, Prim, SCC, topological ordering, and Dijkstra; state representation and heap assumptions.
- Experimental Setup: graph sizes, seeds, directed/undirected generation, cycle guarantees, repetitions, timing, operation counters, and environment.
- Results: measured tables and at least the two required plots.
- Comparison and Discussion: Kruskal versus Prim, DSU optimizations, SCC and Dijkstra growth, topological ordering on DAGs/cyclic graphs, and theory versus measurements. With these three fixed configurations, V and E change together; discuss trends without claiming the plots isolate their independent effects.
- Testing: concrete cases, commands, expected outcomes, and correctness checks.
- Conclusion: findings and which algorithms suit which tasks, including why Dijkstra is unsuitable for negative weights.

## Submission checklist

- Java source is organized under packages for graph, DSU, MST, connectivity, and shortest paths.
- Tests cover small graphs, disconnected graphs, cycles, multiple valid MSTs, unreachable vertices, duplicate weights, and a single vertex.
- Results tables and plots are stored under `results/tables/` and `results/plots/`.
- README contains the complete report and reproducible build, test, benchmark, and plotting instructions.
- GitHub contains the actual development history and all required files, without generated build directories or machine-specific configuration.
- Submit the GitHub repository link by the confirmed deadline.
