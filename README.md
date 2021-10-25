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

Main Bode plot commands:
Given Zeros, Poles, Gain, and Delay 
 - `\BodeZPK[plot_type,{{Magnitude_axis_options},{Phase_axis_options}},{{Magnitude_plot_options},{Phase_plot_options}}]{{zeros},{poles},gain,delay}{min_frequency}{max_frequency}`

Given Numerator and denominator coefficients and delay:
 - `\BodeTF[{{Magnitude_axis_options},{Phase_axis_options}},{{Magnitude_plot_options},{Phase_plot_options}}]{{numerator coefficients},{denominator coefficients},delay}{min_frequency}{max_frequency}`

Other new environments and associated commands:
 - `BodePlot` environment
    - `\addBodeZPKPlots[{approximation_1/{plot_options_1}},{approximation_2/{plot_options_2}},...]{plot_type (phase or magnitude)}{{zeros},{poles},gain,delay}`
    - `\addBodeTFPlot[plot_options]{plot_type (phase or magnitude)}{{numerator coefficients},{denominator coefficients},delay}`
    - `\addBodeComponentPlot[plot_options]{basic_component_plot_command}`
      - Basic component plot commands: ***(append `Lin` to get linear approximation and `Asymp` to get asymptotic approximation)*** ***(change `Pole` to `Zero` to get inverse plots)*** ***(change `Mag` to `Ph` to get phase plots)***
      - `\MagK{a}`
      - `\MagPole{a}{b}`
      - `\MagCSPoles{z}{w}`
      - `\MagSOPoles{a}{b}`
      - `\MagDel{T}` (does not admit asymptotic approximation)
 - `NicholsChart` environment
    - `\addNicholsZPKChart[plot_options]{{zeros},{poles},gain,delay}`
    - `\addNicholsTFChart[plot_options]{{numerator coefficients},{denominator coefficients},delay}`
 - `NyquistPlot` environment
    - `\addNyquistZPKPlot[plot_options]{{zeros},{poles},gain,delay}`
    - `\addNyquistTFPlot[plot_options]{{numerator coefficients},{denominator coefficients},delay}`
