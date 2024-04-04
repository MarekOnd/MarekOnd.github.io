---
title: "Siunitx_tables"
date: 2024-04-04T20:14:02+02:00
draft: true
---

## Example

An *siunitx* table for a experimental order of convergence summary can look like this.

```tex
\begin{table}
    \centering
    \sisetup{
        separate-uncertainty = true,
        table-alignment-mode=marker,
        round-mode=places,
        round-precision=3,
        scientific-notation=true}
    \begin{tabular}{
        S[table-format=0.0, scientific-notation=false, round-mode=none]
        S[table-format = 2.3e1]
        S[table-format = 2.3e1]
        S[table-format = 2.3e1]
        S[table-format = 2.3]
        }
        \toprule
         {res} & {$\delta_x$ [\unit{\metre}]} & {$E_{\delta_x}^{(1)}$} & {$\mathrm{EOC}_1$}\\
        \midrule[\heavyrulewidth]
        60 $\times$ 32 & 6.666667000e-02 & 1.663076419e-03 & \\
        124 $\times$ 64 & 3.225806000e-02 & 3.875007840e-04 & 2.006656460e+00\\
        252 $\times$ 128 & 1.587302000e-02 & 9.181369774e-05 & 2.030546734e+00\\
    \end{tabular}
\end{table}
```

Whole `.tex` file can look like this

```tex
\documentclass{article}

\usepackage{siunitx}
\usepackage{booktabs}

\begin{document}
% table here
\end{document}
```

## Explanation of arguments

- `table-alignment-mode=marker`: aligns the first columns at symbol $\times$
- `round-mode=places`: round the numbers to places after decimal dot (alternatively `figures` for total number of *figures/digits*)
- `round-precision=3`: sets the number of places to round to
- `scientific-notation=true`: mantissa is in the format with one non-zero digit before decimal point and it is multiplied by a power of 10 according to the notation
$$\mathrm{e}\plusmn X\equiv \cdot 10^{\plusmn X}$$ (see [Scientific notation on Wikipedia](https://en.wikipedia.org/wiki/Scientific_notation))
- `table-format = 2.3e1`: in this example, numbers 2, 3 and 1 specify number of digits before decimal dot, after decimal dot (*end of mantissa*) and in the exponent respectively
- `\unit{\metre}`: writes the unit, easier than using `\mathrm{}` in math mode

{{<tip>}}
The parameter `scientific-notation` has to be turned of to display integers in normal style. This is shown in the first column.
{{</tip>}}


{{<warning>}}
The first row needs to have each element enclose in curly brackets `{}` so that it doesn`t register as a number which should be formatted.
{{</warning>}}
