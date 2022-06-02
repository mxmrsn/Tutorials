# Sliding Mode Control of Steerable Needles

This tutorial should be completed after you have completed the 'NeedleModelSimulation' tutorial.

This tutorial is based on the publication from [Rucker 2013](http://research.vuse.vanderbilt.edu/MEDLab/sites/default/files/RuckerSlidingTRO13.pdf).

After we have a working model that describes how the needle moves as we apply control inputs to the system, we want to use this for the purposes of closed loop control. We typically embed an EM sensor into the tip of the needle so that we can provide feedback to the robotic actuation system to hone in on a target or follow a desired trajectory. It is non-intuitive to actuate the needle (especially without line-of-sight) so as to accurately follow a trajectory. Note that the trajectory or target point must be feasible for the needle-tissue pair.

Recall that the workspace of the needle is bounded by a trumpet defined by the needle's maximum radius of curvature. We solved for this radius in the 'NeedleCalibration' tutorial.

Therefore, if we take a target point that lies inside of the trumpet, we can use sliding mode control (more on that in nonlinear control **TODO: add link**) to steer to this target using our two control inputs: insertion and rotation of the needle base (actuator).

If we directly sense the pose of the needle tip (i.e. with an EM sensor), we can steer with this sensor information. Alternatively, and usually worse performance, we can use a model that describes that transmission of motion from the base to the needle tip and have a model that predicts the needle tip pose (**TODO: cite Efe's and my work**).
