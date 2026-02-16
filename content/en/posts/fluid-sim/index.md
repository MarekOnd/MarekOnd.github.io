---
title: "Fluid simulation using LBM"
date: 2026-02-16T18:19:08+01:00
draft: true
cover:
    image: "streamlines-desaturated.png"
    alt: ""
    caption: "Streamlines from a simulation of flow around a cylinder in a 3D channel."
    relative: false
---

I have been working in the area of LBM for my [bachelor project](https://dspace.cvut.cz/entities/publication/ed8a03a2-cdf0-451b-8a34-fa6ba8e272e3) and for my diploma thesis. Here is a very simple overview of it.

Consider a model D$d$Q$q$ with discrete velocities $\vec{c}_i$ for $i\in\{1,2,\ldots,q\}$.


$$
\rho(\vec{x},t) = \sum_i f_i(\vec{x},t)
$$
$$
\rho(\vec{x},t) \vec{u}(\vec{x},t) = \sum_i f_i(\vec{x},t) \vec{c}_i
$$

$$
f_i(\vec{x}+\vec{c}_i,t+1) - f_i(\vec{x},t)  = \frac{1}{\tau} (f_i^{\mathrm{eq}}(\rho,\vec{u}) - f_i(\vec{x},t)) 
$$

