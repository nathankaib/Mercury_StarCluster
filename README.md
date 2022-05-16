# Mercury_StarCluster

This is a modified version of John Chambers' MERCURY integrator.

The base of the algorithm is the 'WB' integrator that accounts for a single wide binary stellar companion to a planetary system as described in Chambers et al. (2002). 

This extension includes the ability to add an arbitrary number of additional stellar mass bodies (the max number of which is limited by run time and hardware considerations).

These additional stellar bodies are integrated in a symplectic T+V algorithm within a center-of-mass coordinate system as described in Kaib et al. (2018). 

An additional effect in this extension is that a gaseous component to the cluster is also included. It is modeled as a background Plummer sphere whose center is fixed at the simulation particles' center-of-mass. This approach is similar to that of Levison et al. (2010). 

To run this code, you can largely refer to the standard Mercury documentation written by John Chambers (which can be found at https://github.com/smirik/mercury), but there are a few key changes:

param.in file: On line 6, the algorithm must be set to 'WB'. The code will not recognize any other of the algorithms in the standard version of Mercury. On line 33, there is now a prompt requiring users to set the 'number of bound bodies.' Set this equal to the number of bodies gravitationally bound to the primary star that hosts planetary mass bodies. This number includes the primary star as well as any bodies in orbit about it, including a wide binary companion. These are the bodies that will be integrated in a Wisdom-Holman mixed variable symplectic scheme as described in Chambers et al. (2002). 

big.in file: On line 4, the coordinate style must be set to Cartesian, since orbital elements are not ideal for unbound cluster stars. These Cartesian coordinates are in a coordinate system whose origin is at the primary star's center. The first object listed in this file is hard-coded to be a wide binary companion in orbit about a primary and planetary bodies. Set this body's mass to some extremely small value if you are not interested in a wide binary companion. The next set of bodies listed are all of the other planetary bodies in orbit about the primary. These bodies will be integrated in democratic heliocentric coordinates with MERCURY's hybrid algorithm. Following the planetary bodies, the big.in file will contain all of the other stellar mass bodies in the simulation. The final body in the simulation should be a 'SUN' particle to act as a tracer particle for the primary star as it moves through phase space under the perturbation of the background potential and the massive bodies. Its mass should be set to a very small value (10^-81 in the example), and its initial position and velocity should be zero (since all coordinates are centered on the primary).  

cluster.in file: This is a new file that is not part of the standard version of MERCURY. It contains the parameters of the cluster Plummer background potential. The first line is the mass of the Plummer sphere (in simulation mass units such that 1 solar mass is ~2.96e-4). The second line is the Plummer radius in AU. The third line is the time (in days) at which the Plummer potential is instantaneously dispersed. 

files.in file: This is a new files.in that is designed to recognize the existance of cluster.in as well as its corresponding dumpfiles.




Example directory: This contains the input files for a simulation that will evolve the Sun, 4 giant planets, and a 0.5 solar-mass binary companion with a=800 AU and e=0.5 for 10 Myrs within a 508-star cluster. This cluster also includes a 1364 solar-mass Plummer potential (with Plummer radius of 285598 AU) to represent the cluster's gas potential. This potential disperses instantaneously after 5 Myrs. 
