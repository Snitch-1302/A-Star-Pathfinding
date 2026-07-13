# A* Pathfinding Visualizer

An interactive Python + Pygame visualization of the A* search algorithm — draw walls, set a start and end point, and watch the algorithm find the shortest path in real time.

![Python](https://img.shields.io/badge/Python-3.x-blue) ![Pygame](https://img.shields.io/badge/Pygame-2.x-green) ![License](https://img.shields.io/badge/License-MIT-lightgrey)

## Overview

This project implements the A* pathfinding algorithm from scratch on a 50x50 interactive grid. Rather than just running the algorithm on hardcoded input, you build the maze yourself with the mouse — placing a start node, an end node, and walls — then watch A* explore the grid, expanding the search frontier and settling on the optimal path.

## Features

- **Interactive grid** — left-click to place start/end nodes and draw walls, right-click to erase
- **Live visualization** — see the algorithm's open set (frontier) and closed set (visited nodes) update in real time as it searches
- **Shortest path rendering** — once the end node is reached, the optimal path is traced and highlighted
- **Manhattan distance heuristic** — guides the search toward the goal instead of exploring blindly (like Dijkstra's algorithm would)
- **Reset support** — clear the grid and start over without restarting the program

## How It Works

The grid is made of `Cube` objects, each aware of its position, its walkable neighbors, and its current state (empty, wall, start, end, open, closed, or path).

The search itself is a straightforward A* implementation:

- A `PriorityQueue` holds nodes ordered by `f(n) = g(n) + h(n)`, where `g(n)` is the cost from the start node and `h(n)` is the estimated cost to the goal
- `h(n)` is computed using **Manhattan distance**, appropriate for a grid where movement is restricted to up/down/left/right
- On each step, the algorithm pops the lowest-`f(n)` node, checks its neighbors, and updates their scores if a shorter path is found
- Once the end node is popped, the path is reconstructed by walking backward through a `came_from` map

**Controls:**
| Action | Effect |
|---|---|
| Left-click | Place start → end → walls |
| Right-click | Erase a node |
| `Space` | Run the algorithm |
| `C` | Clear the grid |

## What I Learned / What I'd Improve

Building this from scratch (rather than following a pre-built visualizer) forced me to actually understand *why* A* is faster than plain Dijkstra — the heuristic prunes the search space instead of exploring uniformly in every direction, which matters a lot as the grid scales up.

Things I'd improve with more time:
- Decouple the algorithm logic from the Pygame rendering so the core search could be unit-tested independently
- Add support for diagonal movement and alternate heuristics (Euclidean, Chebyshev) to compare search behavior
- Allow configurable grid size and weighted terrain instead of binary walkable/wall
- Add a step counter / nodes-explored stat on screen to make algorithm efficiency visible, not just the end result

## How to Run

**Requirements:** Python 3.x and Pygame

```bash
pip install pygame
```

Clone the repo and run:

```bash
git clone https://github.com/Snitch-1302/A-Star-Pathfinding.git
cd A-Star-Pathfinding
python project.py
```

Make sure `ufo.jpg` (used as the window icon) stays in the same directory as `project.py`.

## Why This Matters Beyond the Project Itself

A* and graph search aren't just an algorithms-class exercise — the same core idea (traversing nodes and edges to find optimal or shortest paths) shows up directly in security-relevant contexts: mapping network topology, modeling attacker lateral-movement paths through a network, and route/cost optimization in routing protocols. This project was where I built the underlying intuition for graph traversal that those problems rely on.
