# poredewet_SI
Gromacs and Plumed files used in metadynamics sims of water fluctuation in nanopores

These files correspond to the publication:
Nordquist E#, Schultz S#, Chen J. Using metadynamics to explore the free energy of dewetting in biologically-relevant nanopores. J. Phys. Chem. B 2022, 126 (34), 6428-6437 DOI: [10.1021/acs.jpcb.2c04157](https://doi.org/10.1021/acs.jpcb.2c04157)

We learned a lot about the efficiency of using metadynamics for this purpose while employing this method to study dewetting in a much larger system: the BK channel (KCa1.1), see below publication:
 Nordquist E, Jia Z, Chen J. Inner pore hydration free energy controls the activation of big potassium channels. Biophys. J. 2023, 122, 1158-1167. DOI: [10.1016/j.bpj.2023.02.005](https://doi.org/10.1016/j.bpj.2023.02.005)
We employed umbrella sampling, but also compared the convergence speed to metadynamics in that paper. Ultimately, UB was a lot more straightforward and converged ~3-5x faster.
Note that we used a different plumed COLVAR, [https://www.plumed.org/doc-v2.7/user-doc/html/_c_o_o_r_d_i_n_a_t_i_o_n_n_u_m_b_e_r.html](COORDINATIONNUMBER) to define the region to dewet. 
This CV has two key advantages:
1. The region switching region, wherein waters experience bias, is much broader and better aligned with mouth of the pore than incylinder (which only applies bias along walls of cylinder, not top/bottom)
2. This CV has neighbor list implemented, which gave us ~3x faster sampling. For a big system, this makes a big difference.

Pressure fluctuations can result when using the Parrinello-Rahman barostat with harmonic restraints. We tried adjusting tau_p and the compressibility, but eventually
switched to the Berendsen barostat for the small systems (70 Angstrom cubic). For the larger system (BK channel CoreMT construct, 160x160x100 Angstrom cubic), we did not have this issue.
