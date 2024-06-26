---
title: "First post"
date: 2024-03-30T17:32:59+01:00
tags: ['test']
cover:
    image: "/mandelbrot.png"
    alt: "Mandelbrot set"
    caption: "Mandelbrot set"
    relative: false
showtoc: false
---
$$
e = \sum_{n=0}^\infty \frac{1}{n!}
$$

{{<warning>}}
This is a warning.
{{</warning>}}

{{<note>}}
This is a note which is not being built as markdown (one with %% around instead of <> doesn't work for some reason)
{{</note>}}
{{<note>}}
UPDATE: it is now being **built** as markdown because of an argument `| markdownify`.
{{</note>}}
{{<danger>}}
UPDATE: But this removes the ability to have more a shortcode in a shortcode.
{{</danger>}}


{{<tip>}}
A useful tip!
{{</tip>}}

{{<danger>}}
Beware this.
{{</danger>}}

An extract from Game of Life in Python code

```python
@cuda.jit
def update_board(gridInput:np.ndarray, gridOutput:np.ndarray):
    x,y = cuda.grid(2)
    if x < gridInput.shape[0] and y < gridInput.shape[1]:
        z = 0
        val = 0
        # go through all the neigbouring cells and add 1 for each life
        while z < VECTORS.shape[0]:
            xZ = x + VECTORS[z,0]
            yZ = y + VECTORS[z,1]
            val += gridInput[xZ,yZ]
            z+=1
        # different scenarios for cases with and without life
        if gridInput[x,y]:
            # will it survive?
            if val >= COUNT_TO_LIVE and val < COUNT_TO_OVERCROWD:
                gridOutput[x,y] = True
            else:
                gridOutput[x,y] = False
        else:
            # will it revive
            if val == COUNT_TO_REVIVE:
                gridOutput[x,y] = True
            else:
                gridOutput[x,y] = False
```

{{<youtube d6iQrh2TK98>}}

## Math blocks

{{<theorem "What is true">}}
A statement is true when it is true.
{{</theorem>}}
{{<proof>}}
$\square$
{{</proof>}}
