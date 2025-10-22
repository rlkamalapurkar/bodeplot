# bodeplot
LaTeX package to plot Bode, Nichols, and Nyquist diagrams.
Inspired by the `bodegraph` package.

Author: Rushikesh Kamalapurkar ([rlkamalapurkar@gmail.com](mailto:rlkamalapurkar@gmail.com))

License: [LPPL-1.3c](https://github.com/rlkamalapurkar/bodeplot/blob/main/LICENSE)

## Limitations
 1. Before version 1.2, in `pgf` mode, the package set `trig format plots` to `rad` globally. Version 1.2 onwards, this option is passed to each `addplot` command individually so it does not affect non-`bodeplot` plots. To roll back to pre-v1.2 behavior, load the package with `\usepackage[pgf]{bodeplot}[=2024-02-06]`.
 2. TF commands are wrapped between -180 and 180 degrees in `pgf` mode.
 3. Version 1.0.8 and newer store `gnuplot` temporary files in the working directory. Use class option `declutter` to restore pre-v1.0.8 behavior. Option `declutter` can cause errors if used with a `tikzexternalize` prefix.

## Compilation instructions
1) `latex bodeplot.ins` to generate `bodeplot.sty`
2) To compile documentation (needs `gnuplot` on system PATH):
```
pdflatex --shell-escape bodeplot.dtx
makeindex -s gind.ist bodeplot.idx
makeindex -s gglo.ist -o bodeplot.gls bodeplot.glo
pdflatex --shell-escape bodeplot.dtx
pdflatex --shell-escape bodeplot.dtx
```
## Added functionality over `bodegraph`
 - New `\BodeZPK` and `\BodeTF` commands to generate Bode plots of any transfer function given either poles, zeros, gain, and delay, or numerator and denominator coefficients and delay
 - All plots are fully customizable using `pgf` options (see package documentation for a full list of commands, environments, and options)
 - Support for unstable poles and zeros.
 - Support for complex poles and zeros.
 - Support for general stable and unstable second order transfer functions.
 - Support for both `gnuplot` (default) and `pgfplots` (package option `pgf`).
 - Support for `rad/s` (default) and `Hz` (package option `Hz` or `pgf` key `frequency unit=Hz` for per-plot change) frequency units.
 - Support for `deg` (default) and `rad` (package option `rad` or `pgf` key `phase unit=rad` for per-plot change) phase units.
 - Support for linear and asymptotic approximation of magnitude and phase plots of any transfer function given poles, zeros, and gain.

## Basic Bode/Nyquist/Nichols commands
*See package documentation for the complete key reference, command list, and environment options.*

Starting v3.0, all plotting commands use a simplified PGF-style key/value syntax. 

- Zeros–poles–gain (ZPK) form with optional delay:
```latex
\BodeZPK[%
  domain=0.01:100,
  samples=1000,
  mag plot={blue, thick},
  ph plot={green, thick},
  phase unit=rad%
]{%
  zeros={0,-0.1-0.5i,-0.1+0.5i},
  poles={-0.5-10i,-0.5+10i},
  gain=10,
  delay=0.01%
}
```
  Use the same interface with `\NicholsZPK[...]` or `\NyquistZPK[...]` to generate Nichols and Nyquist plots. Approximation options ( `linear`, `asymptotic`) are available for systems without delays through the `approx=...` key.

- Transfer-function (TF) form:
```latex
\BodeTF[%
  domain=0.001:100,
  samples=1000,
  frequency unit=Hz%
]{%
  numerator={10,2,2.6,0},
  denominator={1,1,100.25},
  delay=0.01%
}
```
  The TF syntax is shared by `\NicholsTF[...]` and `\NyquistTF[...]`.

## Basic pole-zero map commands (v3.0 interface)
*See package documentation for the full list of keys.*

- Given zeros and poles (gain and delay are ignored by the plot):
```latex
\PoleZeroMapZPK[%
  axes={width=6cm, height=6cm},
  plot={blue, thick}%
]{%
  zeros={0,-0.1-0.5i,-0.1+0.5i},
  poles={-0.5-10i,-0.5+10i},
  gain=10,
  delay=0.01%
}
```