## Abbreviated User Guide:  milm_mle.m


[x_hat,k_hat,pre] = milm_mle(Ac,yc,Mc,V,Prec,Ns,pre)

* David Tucker, Ohio State University (tucker.431@osu.edu)
* Shen Zhao, Stanford University (shenzhao@stanford.edu)
* Lee C. Potter, Ohio State University (potter.36@osu.edu)

This is the main routine for solving maximum likelihood estimation in mixed integer linear models,
$$y=Ax + Mk + u$$
where $y \in \mathbb{R}^m$ is a vector of noisy observations, $x\in\mathbb{R}^n$ are real-valued unknowns, $k \in \mathbb{Z}^m$ are integer-valued unknowns, and $u$ is zero-mean additive noise with inverse covariance matrix given by Prec. The matrix $A$ has full column rank, and $M$ is invertible; both $A$ and $M$ are assumed to have rational entries in this code.

The input $V$ is an $n \times n$ real-valued matrix providing a basis for the fundamental parallelotope describing the un-aliased values for $x$.  From $A$ and $M$, a basis $V$ is constructed by the utility routine, form_Lambda_basis.m.

Multiple values of $x$ and $k$ providing large likelihood scores are returned by choosing integer-valued input, Ns, greater than 1.

For applications in which an estimator is sought for many instances with the same $A$, $M$, $V$, and Prec, an input data structure, pre, is computed only once via milm_mle_precompute.m then re-used for all calls to milm_mle.


A special case of the problem occurs for multi-variate congruence equations 
$$y_1  \equiv a_{11} x_1 + a_{12} x_2 + a{1n} x_n \mod b_1$$
$$y_2  \equiv a_{21} x_1 + a_{22} x_2 + a{2n} x_n \mod b_2$$ 
$$\vdots$$
$$y_m \equiv a_{m1} x_1 + a_{m2} x_2 + a{mn} x_n \mod b_m$$
The matrix $A$ above is formed as $[a_{ij}]$;  $M$ is the diagonal matrix of rational moduli, $b_1, ..., b_m$.  The remainders, $y_1, ... , y_m$ are available only as noisy versions in the column vector, $y$. The perturbations in $y$ are assumed zero-mean Gaussian, but may have unequal variance and may be correlated.


The following is an annotated list of the routines in the package.
* milm_mle.m			Main routine
* Figure3_DoA.simulation.m	Reproduces direction of arrival estimation example found in Figure 3 of the referenced IEEE Signal Processing Letters paper.
  * doa_pue.m			Estimator from phase of the data covariance matrix
  * doa_mle.m			Maximum likelihood estimator from raw IQ data
* form_Lambda_basis.m		Computes lattice bases given $A$ and $M$
* sils_reduction_Q.m		For sphere decoding; redistributed, with modification, from X-C Wang, et al. 
* sils_search.m			For sphere decoding: redistributed from X-C Wang, et al. 
* Selected utilities
  * lcms.m			Finds column-wise positive least common multiple of the non-infinity, non-zero elements in a rational matrix.
  * LLLReduce.m			Implementation of lattice reduction algorithm described in  Wubben et al., 2004. 
  * awgn_phase_covariance.m	Constructs the approximate covariance matrix for phase-difference pairs of L complex-valued observation with iid complex-Gaussian noise
  * lenum.m			Find the shortest vector of a lattice using the method by Schnorr & Euchner 1994, as implemented by Christian Chapman 2018.
  * milm_mle_precompute.m	Pre-compute quantities used by milm_mle
  * tril_vec.m			Returns vector of the lower triangular elements of a square matrix.
  * wrapping_error_bounds.m	Computes upper and lower bounds on the probably of incorrectly detecting the integer unknowns, k.
		

Copyright (c) 2023, David Tucker, Shen Zhao, Lee C. Potter
All rights reserved.

This source code is licensed under the MIT license found in the LICENSE file in the root directory of this source tree. 
