# Mercury_StarCluster

This is a modified version of John Chambers' MERCURY integrator.

The base of the algorithm is the 'WB' integrator that accounts for a single wide binary stellar companion to a planetary system as described in Chambers et al. (2002). 

This extension includes the ability to add an arbitrary number of additional stellar mass bodies (the max number limited by run time and hardware considerations).

These additional stellar bodies are integrated in a symplectic T+V algorithm within a center-fo-mass coordinate system as described in Kaib et al. (2018). 

An additional effect in this extension is that a gaseous component to the cluster is also included. It is modeled as a background Plummer sphere whose center is fixed at the simulation particles' center-of-mass. This approach is similar to that of Levison et al. (2010). 


