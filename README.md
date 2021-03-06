# zams_tidal_coupling

T_[mass]_l[23].csv: Tabulated (l=2 and 3) tidal coupling constants for ZAMS, solar metallicity stars between 0.1 and 100 solar masses. We follow the formalism of Press&Teukolsky 1977 (see also Lee&Ostriker 1986), and simply recalculate their overlap integrals (eq. 38 in Press & Teukolsky) using MESA models and the GYRE stellar oscillation code (v. 9793 and 5.0 respectively; sample in-lists are included in the repo). Each file contains two columns: the left column is eta, and the right column is the tidal coupling constant. The masses in the grid are listed in masses.txt. 

T_[mass]_z0.001_l[23].csv: Same as above except for a metallicity of 0.001. Lowering the metallicity decreases the tidal coupling constants small for stellar masses (<~1.3 Msun). Conversely, lower metallicity enhances the tidal coupling constants for higher mass stars. 

T_grid.h5: hdf5 file containing all of the tabulated data. Example python code to obtain l=2 tidal coupling constant for 10 solar mass, solar metallicity (Z=0.02) star. 

```
import h5py
f=h5py.File('T_grid.h5')
MM=10
f['{0}_0.02_2'.format(MM)][...]
```


Note that Press&Teukolsky (PT) implicitly assume that the star is on a parabolic orbit. 

The two plots below show how the tidal coupling constants vary with stellar mass. For comparison, I also plot the tidal coupling constants for n=3 and n=3/2 polytropes as dash-dotted, green lines.

![tc1](tc1.png?raw=true)

![tc2](tc2.png?raw=true)


**Validation and numerics**

1) Tidal coupling constants are robust to changes in the spatial grid in MESA. For our models we set
mesh_delta_coeff=0.2. Using MESA's default grid (which reduces the number of grid points by a factor of a few),
changes the tidal coupling constants by at most 10% (the only exception is 1.3 solar masses, but further checks at
intermediate grid sizes indicate that the high resolution run is converged). <br />
There are between 650 and 1000 grid points in our lower resolution runs, and between 2500 and 5000 grid points in
our high resolution runs. 

2) The overlap integrals have to satisfy the following summation rule:<br/>
  <img src="https://latex.codecogs.com/gif.latex?\Sigma\,Q^2=\ell(2\ell+1)\int_{0}^1\rho(r)r^{2\ell}dr" />. <br/>
  Rho is the stellar density and the sum on the left-hand side is over all of the modes.
  This summation is satisfied within 3% (and the agreement is often much better, especially for sub-solar models;       error_sum.csv enumerates the fractional disagreement for all masses). The second column and third columns are the the percent errors for the l=2 and l=3 modes.<br/>
  
3) For higher order g-modes (g3 and beyond), we use the following equation for the overlap integral 
(see eq. 78 in [Ivanov et al. 2013](https://ui.adsabs.harvard.edu/#abs/2013MNRAS.432.2339I/abstract)).<br />
<img src="https://latex.codecogs.com/gif.latex?Q%3D%5Comega%5E2%5Cint%5C%2Cdr%5Crho%5C%2Cr%5E%7Bl&plus;2%7D%5Cleft%5B%5Cfrac%7B%5Cxi_r%28r%29%7D%7Bg%7D&plus;%5Cfrac%7B%5Cxi_t%28r%29%7D%7Br%5E%7B%5Cell&plus;1%7D%7D%20%5Cleft%28%5Cfrac%7Br%5E%7B%5Cell&plus;2%7D%7D%7Bg%7D%5Cright%29%27%5Cright%5D" />, (a)<br/>
xi_r and xi_t are the radial and tangential components of the normal mode, omega is its frequency, rho is the stellar density, and g is the local gravitational acceleration. Equation a is more numerically stable than the standard expression from PT, as the integrand is less oscillatory. (However, equation assumes the Cowling approximation, which neglects variations in the stellar potential. So this expression cannot be used for all modes).<br />
The plot below shows the overlap integrals of the g3, g4, g5,... modes in our 1 solar mass models. The red points are calculated using the standard PT integral, while the black points are calculating using equation a. The latter do not depend on the resolution of the stellar model, while the former does. As the resolution is increased, the two formulations of the overlap integral converge.<br/>

![conv](conv.png?raw=true)

For our (default) high resolution models, using the standard PT integral for all modes changes the tidal coupling constants by <~10%.

**Potential issues**

For high mass stars (>~2 solar masses), the overlap integrals do not vary smoothly between consecutive, low frequency modes. 

20 Msun (overlap integral vs. mode frequency). The oscillations in the overlap integral are insensitive to the resolution. Also tried different treatments of the convective/radiative boundary in MESA (conv_bdy_mix_softening_f0 = 0.003, conv_bdy_mix_softening_f = 0.001, conv_bdy_mix_softening_min_D_mix = 0), but this has no effect. Finally I tried varying the grid parameters in the GYRE inlist (e.g. chaning alpha_osc from 10 to 100), but the oscillations remain.

![prob3](prob3.png?raw=true)

100 Msun (overlap integral vs. mode frequency)
![prob4](prob4.png?raw=true)




