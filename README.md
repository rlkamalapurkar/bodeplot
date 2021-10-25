# bodeplot
LaTeX package to plot Bode, Nichols, and Nyquist diagrams.

Inspired by the `bodegraph` package.

Limitation: Phase plots from TF commands are wrapped between 0 and 360 degrees.

Added functionality:
 - New `\BodeZPK` and `BodeTF` commands to generate Bode plots of any transfer function given either poles, zeros, gain, and delay, or numerator and denominator coefficients and delay
 - Support for unstable poles and zeros.
 - Support for complex poles and zeros.
 - Support for general stable and unstable second order transfer functions.
 - Support for both `gnuplot` and `pgfplots`.
 - Support for linear and asymptotic approximation of magnitude and phase plots of any transfer function given poles, zeros, and gain.

Main Bode/Nyquist/Nichols commands:
Given Zeros, Poles, Gain, and Delay (Bode plots support asymptotic and linear approximation for systems without delays):
 - `\BodeZPK[{{magnitude_plot_options},{phase_plot_options}},{{magnitude_axis_options},{phase_axis_options}},{group_options},approximation_type]{{zeros},{poles},gain,delay}{min_frequency}{max_frequency}`
 - `\NicholsZPK[{plot_options},{axis_options}]{{zeros},{poles},gain,delay}{min_frequency}{max_frequency}`
 - `\NyquistZPK[{plot_options},{axis_options}]{{zeros},{poles},gain,delay}{min_frequency}{max_frequency}`

Given Numerator and denominator coefficients and delay (does not support approximation yet):
 - `\BodeTF[{{magnitude_plot_options},{phase_plot_options}},{{magnitude_axis_options},{phase_axis_options}},{group_options}]{{numerator coefficients},{denominator coefficients},delay}{min_frequency}{max_frequency}`
 - `\NicholsTF[{plot_options},{axis_options}]{{numerator coefficients},{denominator coefficients},delay}`
 - `\NyquistTF[{plot_options},{axis_options}]{{numerator coefficients},{denominator coefficients},delay}`
 
Other new environments and associated commands:
 - `BodePlot` environment
    - `\addBodeZPKPlots[{approximation_1/{plot_options_1}},{approximation_2/{plot_options_2}},...]{plot_type (phase or magnitude)}{{zeros},{poles},gain,delay}`
    - `\addBodeTFPlot[plot_options]{plot_type (phase or magnitude)}{{numerator coefficients},{denominator coefficients},delay}`
    - `\addBodeComponentPlot[plot_options]{basic_component_plot_command}`
      - Basic component plot commands: ***(append `Lin` to get linear approximation and `Asymp` to get asymptotic approximation)*** ***(change `Pole` to `Zero` to get inverse plots)*** ***(change `Mag` to `Ph` to get phase plots)***
      - `\MagK{a}` - Pure gain, G(s) = a.
      - `\MagPole{a}{b}` - Single pole at s = a+bi, G(s) = 1/(s - a-bi).
      - `\MagCSPoles{z}{w}` - Cannonical Second order system, G(s) = 1/(s^2 + 2zws + w^2).
      - `\MagSOPoles{a}{b}` - Second Order system, G(s) = 1/(s^2 + as + b).
      - `\MagDel{T}` - Pure delay, G(s) = exp(-Ts) (does not admit asymptotic approximation).
 - `NicholsChart` environment
    - `\addNicholsZPKChart[plot_options]{{zeros},{poles},gain,delay}`
    - `\addNicholsTFChart[plot_options]{{numerator coefficients},{denominator coefficients},delay}`
 - `NyquistPlot` environment
    - `\addNyquistZPKPlot[plot_options]{{zeros},{poles},gain,delay}`
    - `\addNyquistTFPlot[plot_options]{{numerator coefficients},{denominator coefficients},delay}`
