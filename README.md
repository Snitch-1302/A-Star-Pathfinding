# A* Pathfinding Visualizer

An interactive Python + Pygame visualization of the A* search algorithm — draw walls, set a start and end point, and watch the algorithm find the shortest path in real time.

![Python](https://img.shields.io/badge/Python-3.x-blue) ![Pygame](https://img.shields.io/badge/Pygame-2.x-green) ![License](https://img.shields.io/badge/License-MIT-lightgrey)

## Overview

This project implements the A* pathfinding algorithm from scratch on a 50x50 interactive grid. Build the maze yourself with the mouse — placing a start node, an end node, and walls — then watch A* explore the grid, expanding the search frontier and settling on the optimal path.

## Tech Stack

- Python 3.x
- Pygame (rendering + interaction)

## Features

- **Interactive grid** — left-click to place start/end nodes and draw walls, right-click to erase
- **Live visualization** — see the open set (frontier) and closed set (visited nodes) update in real time
- **Shortest path rendering** — once the end node is reached, the optimal path is traced and highlighted
- **Manhattan distance heuristic** — guides the search toward the goal instead of exploring blindly (like Dijkstra's would)
- **Reset support** — clear the grid and start over without restarting the program

## How It Works

- The grid is made of `Cube` objects, each aware of its position, walkable neighbors, and current state (empty, wall, start, end, open, closed, path)
- A `PriorityQueue` holds nodes ordered by `f(n) = g(n) + h(n)`, where `g(n)` is cost from the start node and `h(n)` is estimated cost to the goal (Manhattan distance)
- On each step, the algorithm pops the lowest-`f(n)` node, checks neighbors, and updates scores if a shorter path is found
- Once the end node is popped, the path is reconstructed via a `came_from` map

## Controls

| Action | Effect |
|---|---|
| Left-click | Place start → end → walls |
| Right-click | Erase a node |
| Space | Run the algorithm |
| C | Clear the grid |

## Setup & Run

```bash
git clone https://github.com/Snitch-1302/A-Star-Pathfinding.git
cd A-Star-Pathfinding
pip install -r requirements.txt
python astar_visualizer.py
```

**Note:** keep `ufo.jpg` (window icon) in the same directory as `astar_visualizer.py`.

## Full write-up

A detailed breakdown of the design decisions and what I learned building this: [link to Hashnode article]
