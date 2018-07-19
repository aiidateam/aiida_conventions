# Data type for forces
We want to have a datatype for forces.

At the moment, we agreed that the best approach is to have a single data node
that contains both the elements/coordinates and the forces.

Units will be `eV/angstrom`.

We decided to extend `TrajectoryData` to have an optional forces array (`3xN`) with the forces, similar to what we already do for velocities.
