# bodeplot
LaTeX package to plot Bode, Nichols, and Nyquist diagrams.
Based on the `bodegraph` package.
Bug fixes and added functionality:
 - Support for unstable poles and zeros.
 - Support for complex poles and zeros.
 - Support for general stable and unstable second order transfer functions.
 - Moved from `gnuplot` to `pgfplots`.
 - Fixed a bug where `\POAmpAsymp{a}{b}` generates a blank plot for b >= 2.
 - Support for linear and asymptotic approximation of magnitude and phase plots

Basic components of Bode plots:

***(append `Lin` to get linear approximation and `Asymp` to get asymptotic approximation)***

***(change `Pole` to `Zero` to get inverse plots)***

***(change `Mag` to `Ph` to get phase plots)***
 - `\MagK{a}`
 - `\MagPole{a}{b}`
 - `\MagRePole{a}`
 - `\MagCCPoles{a}{b}`
 - `\MagKSOPoles{z}{w}`
 - `\MagInt{a}`
 - `\MagDiff{a}`
 
 The following commands for delay transfer functions do not admit asymptotic approximation
 - `\MagDel{T}`
 - `\PhDel{T}`

New environments and corresponding commands:
 - `MagBodePlot` 
 - `PhBodePlot`
 - `BodePlots`
    - `addBodePlot`
 - `NicholsChart`
    - `addNicholsPlot`
 - `NyquistPlot`
    - `addNyquistPlot`
