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
 - Support for unstable poles and zeros.
 - Support for complex poles and zeros.
 - Support for general stable and unstable second order transfer functions.
 - Support for both `gnuplot` (default) and `pgfplots` (package option `pgf`).
 - Support for `rad/s` (default) and `Hz` (package option `Hz` or `pgf` key `frequency unit=Hz` for per-plot change) frequency units.
 - Support for `deg` (default) and `rad` (package option `rad` or `pgf` key `phase unit=rad` for per-plot change) phase units.
 - Support for linear and asymptotic approximation of magnitude and phase plots of any transfer function given poles, zeros, and gain.

## Main Bode/Nyquist/Nichols commands
Given Zeros, Poles, Gain, and Delay (Bode plots support asymptotic and linear approximation for systems without delays):
 - `\BodeZPK[object1/type1/{options1},object2/type2/{options2},...]{z/{zeros},p/{poles},k/gain,d/delay}{min-frequency}{max-frequency}`
 - `\NicholsZPK[plot/{options},axes/{options}]{z/{zeros},p/{poles},k/gain,d/delay}{min-frequency}{max-frequency}`
 - `\NyquistZPK[plot/{options},axes/{options}]{z/{zeros},p/{poles},k/gain,d/delay}{min-frequency}{max-frequency}`

Given Numerator and denominator coefficients and delay (does not support approximation yet):
 - `\BodeTF[object1/type1/{options1},object2/type2/{options2},...]{num/{coeff},den/{coeff},d/delay}{min-frequency}{max-frequency}`
 - `\NicholsTF[plot/{options},axes/{options}]{num/{coeff},den/{coeff},d/delay}{min-frequency}{max-frequency}`
 - `\NyquistTF[plot/{options},axes/{options}]{num/{coeff},den/{coeff},d/delay}{min-frequency}{max-frequency}`
 
## Other new environments and associated commands
 - `BodeMagPlot` and `BodePhPlot` environments
    - The `addBodeZPKPlots` command

          \begin{BodeMagPlot (or BodePhPlot)}{min-frequency}{max-frequency}
            \addBodeZPKPlots[{approximation1/{plot-options1}},{approximation2/{plot-options2}},...]{magnitude(or phase)}{z/{zeros},p/{poles},k/gain,d/delay}
          \end{BodeMagPlot (or BodePhPlot)}
    - The `addBodeTFPlot` command

          \begin{BodePhPlot (or BodeMagPlot)}{min-frequency}{max-frequency}
            \addBodeTFPlot[plot-options]{phase(or magnitude)}{num/{coeff},den/{coeff},d/delay}
          \end{BodePhPlot (or BodeMagPlot)}
    - The `addBodeComponentPlot` command

          \begin{BodeMagPlot (or BodePhPlot)}{min-frequency}{max-frequency}
            \addBodeComponentPlot[plot-options]{component_plot_command}
          \end{BodeMagPlot (or BodePhPlot)}
      where the component plot commands are variations of the following five commands ***(append `Lin` to get linear approximation and `Asymp` to get asymptotic approximation)*** ***(change `Pole` to `Zero` to get inverse plots)*** ***(change `Mag` to `Ph` to get phase plots)***
      - `\MagK{a}` - Pure gain, G(s) = a.
      - `\MagPole{a}{b}` - Single pole at s = a+bi, G(s) = 1/(s - a-bi).
      - `\MagCSPoles{z}{w}` - Cannonical Second order system, G(s) = 1/(s^2 + 2zws + w^2).
      - `\MagSOPoles{a}{b}` - Second Order system, G(s) = 1/(s^2 + as + b).
      - `\MagDel{T}` - Pure delay, G(s) = exp(-Ts) (does not admit asymptotic approximation).
 - `NicholsChart` environment
    - The `addNicholsZPKChart` command

          \begin{NicholsChart}{min-frequency}{max-frequency}
            \addNicholsZPKChart[plot-options]{z/{zeros},p/{poles},k/gain,d/delay}
          \end{NicholsChart}
    - The `addNicholsTFChart` command

          \begin{NicholsChart}{min-frequency}{max-frequency}
            \addNicholsTFChart[plot-options]{num/{coeff},den/{coeff},d/delay}
          \end{NicholsChart}
 - `NyquistPlot` environment
    - The `addNyquistZPKPlot` command

          \begin{NyquistPlot}{min-frequency}{max-frequency}
            \addNyquistZPKPlot[plot-options]{z/{zeros},p/{poles},k/gain,d/delay}
          \end{NyquistPlot}
    - The `addNyquistTFPlot` command

          \begin{NyquistPlot}{min-frequency}{max-frequency}
            \addNyquistTFPlot[plot-options]{num/{coeff},den/{coeff},d/delay}
          \end{NyquistPlot}
