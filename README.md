# zams_tidal_coupling

T_[mass].csv: Tabulated (l=2) tidal coupling constants for ZAMS, solar metallicity stars between 0.1 and 100 solar masses following the formalism of Press&Teukolsky 1977 (and Lee&Ostriker 1986). We simply recalculate their overlap integrals (eq. 38 in Press & Teukolsky) using MESA models and the GYRE stellar oscillation code (v. 9793 and 5.0 respectively; sample in-lists are included in the repo). Each file contains two columns: the left column is eta, and the right column is the tidal coupling constant. 

Note that Press&Teukolsky implicitly assume that the star is on a parabolic orbit. The masses in the grid are listed in masses.txt.

The two plots below show how the tidal coupling constants vary with stellar mass. For comparison, I also plot the tidal coupling constants for n=3 and n=3/2 polytropes as dash-dotted, green lines.

![tc1](tc1.png?raw=true)

![tc2](tc2.png?raw=true)

**Validation**

1) Tidal coupling constants are robust to changes in the numerical grid. Decreasing mesh_delta_coeff to 0.2 (which increases the number of grid points by a factor of a few), changes the tidal coupling constant by at most ~10%.

2) The overlap integrals have to satisfy the following summation rule:
  
  <img src="https://latex.codecogs.com/gif.latex?\Sigma\,Q^2=10\int_{0}^1\rho(r)r^4dr" />  
  
  This summation is generally satisfied to within 2% (and the agreement is often much better, especially for sub-          solar models--error_sum.csv lists the errors for all models). 

  where rho is the stellar denstiy; all masses and lengths are in units of the stellar mass and radius. 

**Potential issues**

For high mass stars (>~2 solar masses), the overlap integrals does not vary smoothly between successive modes.  

20 Msun (overlap integral vs. mode frequency)
![prob3](prob3.png?raw=true)

100 Msun (overlap integral vs. mode frequency)
![prob4](prob4.png?raw=true)




