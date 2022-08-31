# Chem 274A - Lab 1

In this lab, you will be using the molecular simulation code we wrote in Chem 280 - Foundations of Molecular Modelling and Software Engineering.

## Exercises

### Section 1 - Makefile (Spend 30 minutes max on this)
1. Use the `makefile` to create an environment for this lab.
    ```
    cd mcsim_python
    make environment
    ```
2. Activate the environment created by the `makefile`
    ```
    conda activate chem274A_lab1
    ```
3. Use the `makefile` to install `mcsim`
    ```
    make install
    ```

4. Review the Makefile in `mcsim_python`. Write a comment above each target explaining what the target does.

### Section 2 - Runnning Simulations
1. Use the notebook `run_mcsim.ipynb` to run Monte Carlo simulations. Follow the instructions in the notebook.

1. Run the simulation with the current parameters. You shouldn't have to modify any code to do this. Take note of the comments and the graphs generated. The starting parameters are:
 - num_atoms = 500
 - reduced_temperature = 0.9
 - density = 0.9
 - 100000 steps for equilibration (freq = 10000)
 - 100000 steps for production (freq = 10000)
 
 2. Run a simulation with the following parameters:
 - num_atoms = 500
 - reduced_temperature = 0.9
 - density = 0.9
 - 1 step for equilibration (freq = 1)
 - 1000 steps for production (freq = 100)
 
 3. The main difference between these two simulations is that the first simulation runs for 100,000 steps which is more than enough time to reach equilibrium, whereas the second simulation only runs for 1 step, meaning that the initial configuration is very close to the congfiguration as it started. This second simulation results in a very high energy calculated, as well as a very high pressure. This is plotted as a single point using pandas, reading from equilibrium.csv. 
 
 The production simulation is then run for 1000 steps, and the energy per particle and pressure calculated can be seen to decrease as the system approaces equilibrium, yet does not reach it. There are differences in the RDF values calculcated after running the production simulation. In the first simulation we see that g(r) reaches a maximum at the value of r/sigma = 1.0, meaning that most particles are within one radius away from each other. As r/sigma increases the function oscillates around the value of g(r) = 1.0. This plot indicates a liquid phase when compared to known RDF plots for the liquid phase.
 
 In the second simulation, because the particles have not reached equilibrium, a large portion of the atoms are closer than 1 radius from each other, as exemplified by the high energy per particle, and high pressure calculated. The value of g(r) reaches a maximum at a radius of less than one, which we can conclude is not natural because the particles have been initialized yet have not reached equilibrium. 
 
 4. By changing the density to 0.009 and running the simulation with 100,000 steps for equilibration and 100000 steps for production we see that the RDF plotted seems to represent a gaseous phase. This is corroborated by a lower value for energy and pressure, and is reflected in the RDF plot which tells us that the probabiity of finding particles at a distance of 1 r/sigma is the most common.
 
 5. Running the simulation from (4) with a reduced temperature of 1.5 results in a higher initial energy per particle and a higher  pressure, which converges to a higher temperature than the previous simulation after equilibrium has been reached. This is in accordance with the ideal gas laws. Again the RDF plot reflects a gaseous phase, with a peak occuring at 1.0 r/sigma, although the value for g(r) is lower (1.75 at the peak, compared to 3.0 for the simulation in (4)) meaning that the particles are more spread out and less likely to be found within one radius of distance.
 
 6. Using the function generate_cubic_lattice() we create an initial configuration in a lattice. This configuration takes more steps to reach equilibrium and could even continue to equilibrate after 100,000 steps. The pressure is larger than the other simulations and the RDF seems to reflect a solid or a dense liquid (i'm not sure of the difference). Again the peak value of g(r) at r/sigma = 1.0 tells us that the particles are most likely to be found within one radius of each other, and this value for g(r) oscillates with maximums at values that are constant multiples of 1.0. 