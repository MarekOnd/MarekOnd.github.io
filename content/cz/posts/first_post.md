---
title: "První zpráva"
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
Toto je varování.
{{</warning>}}

{{<note>}}
Toto je poznámka.
{{</note>}}

{{<tip>}}
Toto je užitečný tip!
{{</tip>}}

{{<danger>}}
Obávej se tohohle.
{{</danger>}}

Extrakt z kódu Hry života v Pythonu

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

## Matematické bloky

{{<definition "Tvrzení">}}
Tvrzení je výrok, který je buď pravdivý nebo nepravdivý.
{{</definition>}}

{{<lemma "Zakladní pozorování">}}
Tvrzení je pravdivé $\Rightarrow$ je pravdivé
{{</lemma>}}

{{<theorem "Co je pravda">}}
Tvrzení je pravdivé $\Leftrightarrow$ je pravdivé
{{</theorem>}}

{{<proof>}}
$\square$
{{</proof>}}
