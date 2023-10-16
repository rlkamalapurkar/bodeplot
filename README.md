# bodeplot
LaTeX package to plot Bode, Nichols, and Nyquist diagrams.
Inspired by the `bodegraph` package.

Author: Rushikesh Kamalapurkar ([rlkamalapurkar@gmail.com](mailto:rlkamalapurkar@gmail.com))

License: [LPPL-1.3c](https://github.com/rlkamalapurkar/bodeplot/blob/main/LICENSE)

## Limitations
 1. TF commands are wrapped between -180 and 180 degrees in `pgf` mode.
 2. Version 1.0.8 and newer store `gnuplot` temporary files in the working directory. Use class option `declutter` to restore pre-v1.0.8 behavior. Option `declutter` can cause errors if used with a `tikzexternalize` prefix.

## Compilation instructions
1) `latex bodeplot.ins` to generate `bodeplot.sty`
2) To compile documentation (needs `gnuplot` on system PATH):
```
pdflatex bodeplot.dtx --shell-escape
makeindex -s gind.ist bodeplot.idx
makeindex -s gglo.ist -o bodeplot.gls bodeplot.glo
pdflatex bodeplot.dtx --shell-escape
pdflatex bodeplot.dtx --shell-escape
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
*See package documentation for a full list of commands, environments, and options.*
 - Given Zeros, Poles, Gain, and Delay (asymptotic and linear approximation available for systems without delay):
```
\BodeZPK % (OR \NicholsZPK[samples=1000] OR NyquistZPK[samples=1000])
{% 
  z/{0,{-0.1,-0.5},{-0.1,0.5}}, % zeros at s = 0, s = -0.1 - 0.5j, and s = -0.1 + 0.5j
  p/{{-0.5,-10},{-0.5,10}}, % poles at s = -0.5 - 10j, and s = -0.5 + 10j
  k/10, % gain
  d/0.01, % delay
}
{0.01} % frequency range start
{100} % frequency range end
```

 - Given Numerator and denominator coefficients and delay (does not support approximation):
```
\BodeTF % (OR \NicholsTF[samples=1000] OR NyquistTF[samples=1000])
{%
  num/{10,2,2.6,0}, % numerator coefficients
  den/{1,1,100.25}, % denominator coefficients
  d/0.01, % delay
}
{0.001} % frequency range start
{100} % frequency range end
```
