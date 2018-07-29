# zams_tidal_coupling

T_[mass].csv: Tabulated (l=2) tidal coupling constants for ZAMS, solar metallicity stars between 0.1 and 100 solar masses. We follow the formalism of Press&Teukolsky 1977 (see also Lee&Ostriker 1986), and simply recalculate their overlap integrals (eq. 38 in Press & Teukolsky) using MESA models and the GYRE stellar oscillation code (v. 9793 and 5.0 respectively; sample in-lists are included in the repo). Each file contains two columns: the left column is eta, and the right column is the tidal coupling constant. The masses in the grid are listed in masses.txt.

Note that Press&Teukolsky implicitly assume that the star is on a parabolic orbit. 

The two plots below show how the tidal coupling constants vary with stellar mass. For comparison, I also plot the tidal coupling constants for n=3 and n=3/2 polytropes as dash-dotted, green lines.

![tc1](tc1.png?raw=true)

![tc2](tc2.png?raw=true)

**Validation**

1) Tidal coupling constants are robust to changes in the spatial grid in MESA. For our models we set mesh_delta_coeff=0.2. Using MESA's default grid (which reduces the number of grid points by a factor of a few), changes the tidal coupling constants by at most 10%. 

2) The overlap integrals have to satisfy the following summation rule:<br/>
  <img src="https://latex.codecogs.com/gif.latex?\Sigma\,Q^2=10\int_{0}^1\rho(r)r^4dr" />. <br/>
  Rho is the stellar density and the sum on the left-hand side is over all of the modes.
  This summation is satisfied within 2% (and the agreement is often much better, especially for sub-solar models;    error_sum.csv enumerates the fractional disagreement for all masses).<br/>
 

**Potential issues**

For high mass stars (>~2 solar masses), the overlap integrals do not vary smoothly between consecutive, low frequency modes. 

20 Msun (overlap integral vs. mode frequency). The oscillations in the overlap integral are insensitive to the resolution. Also tried different treatments of the convective/radiative boundary in MESA (conv_bdy_mix_softening_f0 = 0.003, conv_bdy_mix_softening_f = 0.001, conv_bdy_mix_softening_min_D_mix = 0), but this has no effect

![prob3](prob3.png?raw=true)

100 Msun (overlap integral vs. mode frequency)
![prob4](prob4.png?raw=true)




