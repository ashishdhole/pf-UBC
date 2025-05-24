<div style="display: flex; align-items: center; gap: 20px; justify-content: left;">
  <img src="./images/logo.png" alt="pf-UBC Logo" class="float-glow-img" width="100">
  <h1 style="margin: 0; font-size: 3em; color: #000000; font-weight: bold;">pf-UBC</h1>
</div>

##<span style="font-size: 1.2em; color: #000000;">Grain Growth Model</span>
<p style="text-align: justify; text-indent: 2em;">
The movement of grain boundaries (GBs) plays a fundamental role in the microstructural evolution of materials, as it enables the system to lower its total free energy. This energy reduction is influenced by several factors, including internal stresses, dislocation structures, and the energy associated with the grain boundaries themselves. To understand and predict this behavior, researchers have employed a variety of computational models.

Among the available techniques, the phase-field method stands out for its ability to simulate complex boundary interactions and morphological changes without explicitly tracking interfaces. Leveraging this approach, pf-UBC incorporates a multiphase grain growth model rooted in the pioneering studies by <a href="#chen_yang_1994">Chen and Yang (1994)</a>, <a href="#chen_1995">Chen (1995)</a>, and refined further by <a href="#moelans_2008">Moelans et al. (2008)</a>. In this formulation, each grain is represented by an evolving order parameter that responds to energy gradients in the system. The temporal evolution of these parameters follows the Allen–Cahn equation, capturing the physics of grain boundary motion, given by :

<div class="small-math">
$$
\frac{\partial \eta_i}{\partial t} = -L \frac{\delta F}{\delta \eta_i}
$$
</div>

where $F$ is the free energy functional, $L$ is the order parameter mobility, and the $\delta$ operator represents a variational derivative.

<div class="small-math">
$$
F = \int_{V}^{} f_{loc}(\eta_0, \eta_1,..., \eta_N) + f_{add}+\kappa\sum_{i}^{N}\left| \nabla \eta_i \right|^2
$$
</div>

where $N$ is the total number of order parameters, $f_{loc}$​ represents the local free energy density, and $f_{add}$​ represents any additional sources of energy density. $f_{loc}$ consists of two parts: (i) variation of local energy across the interface ($f_0$) and (ii) a contribution due to the internal bulk energy of the grains ($f_d$).

<div class="small-math">
$$
f_{loc} = f_{0} + f_{d}
$$
</div>

Here f0 is chosen to have a minimum of 0 inside each grain and a maximum at the interface resembling a double-well shape. 
Based on the formulation of <a href="#chen_yang_1994">Chen and Yang (1994)</a>, $f_0$ is proposed as:

<div class="small-math">
$$
f_0 = m\left( \sum_{i=1}^{N}\frac{{\eta_i}^4}{4} - \sum_{i=1}^{N}\frac{{\eta_i}^2}{2} + \frac{3}{2}\sum_{i=1}^{N}\sum_{j\neq 1}^{N}{\eta_i}^2 {\eta_j}^2 + \frac{1}{4}\right)
$$
</div>

where $m$ is a constant that determines the height of the energy peaks between each minima.
Following Allen-Cahn dynamics, the evolution of the system results in a set of partial differential equation (PDEs):

<div class="small-math">
$$
\frac{\partial{\eta_i}}{\partial t} = -L\frac{\delta{F}}{\delta{\eta_i}} = -L\left( \frac{\partial{f_0}}{\partial \eta_i} - \kappa\nabla^2\eta_i \right)
\\[1.5em]
\frac{\partial{\eta_i}}{\partial t} = -L\left[ m\left( {\eta_i}^3 - {\eta_i} + 3\eta_i \sum_{j\neq i}^{N} {\eta_j}^2\right) - \kappa\nabla^2 \eta_i\right]
$$
</div>
</p>


<br><br>
##<span style="font-size: 1.2em; color: #000000;">Friction Pressure</span>
<p style="text-align: justify; text-indent: 2em;">
Second phase particles and solute atoms have been used as an important constituent to design materials and processes due to their ability to control motion of grain boundaries. These particles limit motion of grain boundaries by the particle pinning mechanism. in pf-UBC, a model on an energetic approach to include the drag pressure (Friction Pressure) directly into the phase-field equation. It avoids the phenomenological modification of the grain-boundary kinetics through mobility.
</p>
<p style="text-align: justify; text-indent: 2em;">
The bulk energy of grain $i$, $G_i$ is considered in comparison with a standard state. In a case where bulk energy of all grains is equal ($G_i = G_j$), $f_d = const$. and the driving pressure for grain-boundary movement is only due to its <a href="#chen_yang_1994">curvature</a>. However, in a case of different bulk energies, $G_i \neq G_j$ , there is an additional driving pressure of $\Delta G_{ij} = G_j − G_i$ on the grain boundaries. In this situation, $f_d$ interpolates the bulk energy of each grain across the grain boundary. For two order parameters the contribution to the local energy density due to the bulk energy is written as: 
</p>

<div class="small-math">
$$
f_d = 3\sum_{i=1}^{2}\sum_{j \neq i}^{2}\left( \frac{\phi^2_{ij}}{2} - \frac{\phi^3_{ij}}{3}\right) \Delta G_{ij} + \frac{1}{2}\sum_{i=1}^{2} G_i
\\[2em]
\phi_{ij} = \frac{\eta_i - \eta_j +1}{2}
$$
</div>

<p style="text-align: justify; text-indent: 2em;">
The derivation of $f_d$ can be simplified as 

<div class="small-math">
$$
\frac{\partial f_d}{\partial eta_i} = 3 \eta_i \eta_j \Delta G_{ij}
$$
</div>

Each pair of order parameters between ηi and ηj has a contribution to the $\frac{\partial f_d}{\partial eta_i}$ term. Therefore, a set of evolution PDEs are obtained by generalizing equation over all order parameter pairs:

<div class="small-math">
$$
\frac{\partial{\eta_i}}{\partial t} = -L\frac{\delta{F}}{\delta{\eta_i}} = -L\left( \frac{\partial{f_0}}{\partial \eta_i} + \frac{\partial{f_d}}{\partial \eta_i}- \kappa\nabla^2\eta_i \right)
\\[1.5em]
\frac{\partial{\eta_i}}{\partial t} = -L\left[ m\left( {\eta_i}^3 - {\eta_i} + 3\eta_i \sum_{j\neq i}^{N} {\eta_j}^2\right) - 3 \eta_i \sum_{j \neq i}^{N} \eta_j \Delta G_{ij} - \kappa\nabla^2 \eta_i\right]
$$
</div>

The detailed literature on friction pressure was presented by <a href="#chen_yang_1994">S. Shahandeh et al. (2012)</a> 
</p>

<br><br><br><br>
## References
<p style="text-align: justify; font-size: 1em">
- <span id="chen_yang_1994">Chen, Long-Qing, and Wei Yang. "Computer simulation of the domain dynamics of a quenched system with a large number of nonconserved order parameters: The grain-growth kinetics." Physical Review B 50, no. 21 (1994): 15752.</span>
<br><br>
- <span id="chen_1995">Chen, Long-Qing. "A novel computer simulation for modeling grain growth." Scripta Metallurgica et Materialia;(United States) 32, no. 1 (1995).</span>
<br><br>
- <span id="moelans_2008">Moelans, Nele, Bart Blanpain, and Patrick Wollants. "Quantitative analysis of grain boundary properties in a generalized phase field model for grain growth in anisotropic systems." Physical Review B—Condensed Matter and Materials Physics 78, no. 2 (2008): 024113.</span>
- <br><br>
- <span id="fan_chen_1997">Fan, Danan, and Long-Qing Chen. "Diffuse-interface description of grain boundary motion." Philosophical Magazine Letters 75, no. 4 (1997): 187-196.</span>
- <br><br>
- <span id="Shahandeh_2012">Shahandeh, S., M. Greenwood, and Matthias Militzer. "Friction pressure method for simulating solute drag and particle pinning in a multiphase-field model." Modelling and Simulation in Materials Science and Engineering 20, no. 6 (2012): 065008.</span>
</p>
