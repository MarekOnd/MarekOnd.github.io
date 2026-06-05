---
title: "Programmable Cubes"
date: 2026-06-05T16:36:15+02:00
draft: true
cover:
    image: "jwst.png"
---

This is an overview of my solution to the [SpOC 3: Programmable Cubes challenge](https://optimize.esa.int/challenge/spoc-3-programmable-cubes/About) by ESA ACT.

The goal is to reconfigure modular cube structure from a scrambled configuration to an object (ISS, JWST or Enterprise in the challenge) in as few steps as possible. Cubes need to roll over each other and collide with each other which makes it difficult to find even a feasible solution.

## Solution

[My solution](https://github.com/MarekOnd/SpOC3-solution) uses these concepts:

- A* on the cube structure with customizable heuristics (it was sometimes better to use Dijkstra or different norms)
- cube unstucking using bridges
- A* with few random modification to the neighbourhood of target cube and target position (another unstucking measure)
- branch and bound metaheuristic to find best combination of previous algorithms

It would be useful to create an A* modification that has also the moves of currently adjacent cubes as the neighbourhood and can be much more reliable than the currect implementation. The amount of branches in this case grows exponentially and it is difficult to track all configurations.

## Preview

An example of how unstucking using bridge works (object should be a "wand" with blue cube on the top):

<video src="enterprise.mp4" autoplay="true" loop="true" style="width:40vw"></video>

Best chromosome for the largest problem with the Enterprise ship:

{{< youtube id=93BuoOowUbA  loading=lazy mute=true >}}

