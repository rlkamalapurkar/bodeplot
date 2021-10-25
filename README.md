# bodeplot
LaTeX package to plot Bode, Nichols, and Nyquist diagrams.
Based on the `bodegraph` package.
Added functionality:
 - New `\BodeZPK` and `BodeTF` commands to generate Bode plots of any transfer function given either poles, zeros, gain, and delay, or numerator and denominator coefficients and delay
 - Support for unstable poles and zeros.
 - Support for complex poles and zeros.
 - Support for general stable and unstable second order transfer functions.
 - Support for both `gnuplot` and `pgfplots`.
 - Support for linear and asymptotic approximation of magnitude and phase plots of any transfer function given poles, zeros, and gain.

Bode plots
 - `\BodeZPK[plot_type,{{Magnitude_axis_options},{Phase_axis_options}},{{Magnitude_plot_options},{Phase_plot_options}}]{{zeros},{poles},gain,delay}{min_frequency}{max_frequency}`
 - `\BodeTF[{{Magnitude_axis_options},{Phase_axis_options}},{{Magnitude_plot_options},{Phase_plot_options}}]{{numerator coefficients},{denominator coefficients},delay}{min_frequency}{max_frequency}`

Basic components of Bode plots:

***(append `Lin` to get linear approximation and `Asymp` to get asymptotic approximation)***

***(change `Pole` to `Zero` to get inverse plots)***

***(change `Mag` to `Ph` to get phase plots)***
 - `\MagK{a}`
 - `\MagPole{a}{b}`
 - `\MagCSPoles{z}{w}`
 - `\MagSOPoles{a}{b}`
 
The following commands for delay transfer functions do not admit asymptotic approximation
 - `\MagDel{T}`
 - `\PhDel{T}`

New environments and corresponding commands:
 - `BodePlot`
    - `\addBodeZPKPlots[{approximation_1/{plot_options_1}},{approximation_2/{plot_options_2}},...]{plot_type (phase or magnitude)}{{zeros},{poles},gain,delay}`
    - `\addBodeTFPlot[plot_options]{plot_type (phase or magnitude)}{{numerator coefficients},{denominator coefficients},delay}`
    - `\addBodeComponentPlot[plot_options]{basic_component_plot_command}`
 - `NicholsChart`
    - `\addNicholsZPKChart[plot_options]{{zeros},{poles},gain,delay}`
    - `\addNicholsTFChart[plot_options]{{numerator coefficients},{denominator coefficients},delay}`
 - `NyquistPlot`
    - `\addNyquistZPKPlot[plot_options]{{zeros},{poles},gain,delay}`
    - `\addNyquistTFPlot[plot_options]{{numerator coefficients},{denominator coefficients},delay}`
