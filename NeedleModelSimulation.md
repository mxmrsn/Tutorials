# Needle Model Simulation

This tutorial aims to guide you through simulating a standard unicycle needle model. We will be simulating the model using MATLAB. Refer to []() for an in-depth discussion of the nonholonomic unicycle model.

The model makes an analogy to a unicycle wheel rolling on a plane. The nonholonomic constraint of a wheel rolling on a plane means that the wheel can only roll without slip, and that it can only precess about the tangent direction of the rolling (i.e. it cannot slip laterally).

The bending plane of the needle is determined by the orientation of the bevel. The bending plane changes instantaneously as the body of the needle rotates. In the case of the unicycle model, the needle always bends with a constant curvature with radius r. The radius r is the only model parameter in the model and is calibrated for a given needle in a given tissue.

## Assumptions

The model neglects any and all tissue interactions that occur along the needle backbone.
The model is purely kinematic and assumes that velocity of insertion and rotation does not change the radius of curvature.
The model assumes that the control inputs are transmitted instantaneously without lag to the tip of the needle. This assumption is circumnavigated by putting a 6DOF sensor in the tip of the needle where we can directly sense the spatial and angular velocity of the needle body.

## Model Formulation

The state of the needle is parameterized by the position and orientation of the tip frame. There is a choice of parameterization of the orientation - we typically choose to use rotation matrices or quaternions.

The inputs to the model are 1) the spatial insertion velocity of the needle, and 2) the angular/rotational velocity of the needle.

We use a state-space representation to describe the state of the needle, as well as the inputs to the model.

```
X = [p_n; q_n];
U = [v; w];
```

The needle model evolution can be written as a markov model:


## Code

The tasks for simulation are two scripts:
1. Needle Model
2. Script to integrate the model with different control input profiles
