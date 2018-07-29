# zams_tidal_coupling

T_[mass].csv: Tabulated (l=2) tidal coupling constants for ZAMS, solar metallicity stars between 0.1 and 100 solar masses following the formalism of Press&Teukolsky 1977 (and Lee&Ostriker 1986). We simply recalculate their overlap integrals (eq. 38 in Press & Teukolsky) using MESA models and the GYRE stellar oscillation code (v. 9793 and 5.0 respectively; sample in-lists are included in the repo). Each file contains two columns: the right column lists the value of eta, while the left column lists the tidal coupling constant. 

Note that Press&Teukolsky implicitly assume that the star is on a parabolic orbit. The masses in the grid are listed in masses.txt.

The two plots below show how the tidal coupling constants vary with stellar mass. For comparison, I also plot the tidal coupling constants for n=3 and n=3/2 polytropes as dash-dotted, green lines.

[!tc1](https://github.com/alekseygenerozov/zams_tidal_coupling/blob/master/tc1.png)

[!tc2](https://github.com/alekseygenerozov/zams_tidal_coupling/blob/master/tc2.png)

#Validation
The tidal coupling constants are robust to variations in the numerical resolution of the stellar model (i.e. decreasing mesh_delta_coeff to 0.2). 

The overlap integrals have to satisfy the following summation rule:

$\Sum Q^2 10 \int_{0}^1 rho(r) r^4 dr$,

This summation is generally satisfied to within 2% (and the agreement is often much better, especially for sub-solar models--error_sum.csv lists the errors for all models). 

where rho is the stellar denstiy; all masses and lengths are in units of the stellar mass and radius. 

#Potential issues

For high mass stars (>~2 solar masses), the overlap integrals does not vary smoothly between successive modes.  

20 Msun (overlap integral vs. mode frequency)
[prob1](https://github.com/alekseygenerozov/zams_tidal_coupling/prob1.png)

100 Msun (overlap integral vs. mode frequency)
[prob2](https://github.com/alekseygenerozov/zams_tidal_coupling/prob2.png)




