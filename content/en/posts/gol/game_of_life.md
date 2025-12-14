---
title: "Game of life"
date: 2025-12-14T20:44:02+01:00
draft: false
cover:
    image: "gol_preview.png"
    alt: "Result example"
    caption: "Result example"
    relative: false
---

Overview of my <a href="https://github.com/MarekOnd/Game-of-Life-in-Python">repository</a>.

Repository contains an implementation of the <a href="https://en.wikipedia.org/wiki/Conway%27s_Game_of_Life">Conway's Game of Life</a> in Python with output in OpenCV2 using various methods. Namely:
<ul>
<li> vectorization with Numpy
<li> basic nested for loops
<li> nested for loops with <a href="https://en.wikipedia.org/wiki/Just-in-time_compilation"> Just-in-time compilation </a>
<li> integration with CUDA GPU computation (works only on NVIDIA GPUs) using <a href="https://numba.pydata.org/">Numba</a>
</ul>

<img src="gol_preview.png">