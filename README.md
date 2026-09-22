# Pathfinder

An **expedition pathfinding studio** — not another colored-grid tutorial.

You generate a Himalayan-style elevation field, carve roads and crevasses, then watch search algorithms race across real slope-weighted terrain. Lighting is hillshaded from the heightmap so ridges actually look like ridges.

## Why this is different

Most visualizers treat every empty cell as cost `1`. Pathfinder treats the map as geography:

- **Elevation noise** builds ridgelines and valleys (seeded, so a seed is a shareable map).
- **Movement cost** is `1 + slope penalty`. Climbing a steep face is expensive; following a contour is cheap. Dijkstra and A* feel *different* here, which is the whole point.
- **Hillshade** renders the terrain instead of flat pastel squares.
- **Race mode** runs two algorithms on the same map and scores nodes expanded, path cost, and wall-clock time.

## Algorithms

| Algorithm | What it actually does |
| --- | --- |
| BFS | Unweighted. Ignores slope. Finds fewest *steps*, not the cheapest climb. |
| DFS | Stack walk. Good for seeing why DFS is a terrible expedition planner. |
| Dijkstra | True weighted shortest path on slope costs. |
| A* | Dijkstra + Manhattan heuristic (admissible on 4-direction, still useful on 8). |
| Greedy Best-First | Heuristic only. Fast, often ugly. |
| Bidirectional BFS | Search from basecamp *and* summit until the fronts meet. |

## Terrain tools

- **Basecamp / Summit** — start and goal
- **Crevasse** — impassable
- **Road** — flattens elevation locally so cost drops
- **Ridge** — raises elevation
- **Erase** — restore generated ground
- Generators: ridgeline noise, recursive-backtracker maze, Prim maze, recursive division, random crevasses

## Run

No build step. Open `index.html` in a browser, or from this folder:

```bash
npx --yes serve .
```

## Keyboard

| Key | Action |
| --- | --- |
| `Space` | Run / pause |
| `R` | Reset search (keep terrain) |
| `N` | New elevation seed |
| `1–6` | Algorithms |
| `D` | Toggle 4 / 8 direction |

Built as a portfolio piece for Pranaya Simkhada — HTML, CSS, and vanilla JS, no frameworks.
