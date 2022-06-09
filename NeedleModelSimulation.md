# Needle Model Simulation

This tutorial aims to guide you through simulating a standard unicycle needle model. We will be simulating the model using MATLAB. Refer to [Webster 2006](http://research.vuse.vanderbilt.edu/MEDLab/sites/default/files/papers/WebsterJRR2006.pdf) for an in-depth discussion of the nonholonomic unicycle model.

The model makes an analogy to a unicycle wheel rolling on a plane. The nonholonomic constraint of a wheel rolling on a plane means that the wheel can only roll without slip, and that it can only precess about the tangent direction of the rolling (i.e. it cannot slip laterally).

The bending plane of the needle is determined by the orientation of the bevel. The bending plane changes instantaneously as the body of the needle rotates. In the case of the unicycle model, the needle always bends with a constant curvature with radius r. The radius r is the only model parameter in the model and is calibrated for a given needle in a given tissue given a minimum insertion length.

**TODO: add pics**

## Assumptions

The model neglects any and all tissue interactions that occur along the needle backbone.

The model is purely kinematic and assumes that velocity of insertion and rotation does not change the radius of curvature.

The model assumes that the control inputs are transmitted instantaneously without lag to the tip of the needle. This assumption is circumnavigated by putting a 6DOF sensor in the tip of the needle where we can directly sense the spatial and angular velocity of the needle body.

## Model Formulation

The state of the needle is parameterized by the position and orientation of the tip frame. There is a choice of parameterization of the orientation - we typically choose to use rotation matrices or quaternions.

The inputs to the model are 1) the spatial insertion velocity of the needle ```v```, and 2) the angular/rotational velocity of the needle ```w```.

We use a state-space representation to describe the state of the needle, as well as the inputs to the model.

```
X = [p_n; q_n];
U = [v; w];
```

The needle model evolution can be written as a markov model (discrete model that only depends on the prior state and current control inputs):

```
x_dot = f(x,u)
```

We can integrate the model with standard Euler integration, as long as the timestep is small

```
dt = 0.01; % sec
x_kp1 = x_k + x_dot*dt;
```

For a control input profile, we can loop through a simulation:

```
x(1) = [0;0;0; 1;0;0;0]; % [p; q]
for ii = 2:length(u)
    x_dot = f(x(:,ii-1), u(:,ii));
    x(:,ii) = x(:,ii-1) + x_dot*dt;
end
```


## Code Homework

The tasks for simulation are two scripts:
1. Needle Model function that implements the equations above ``` x_dot = f(x,u) ```
2. Generate control inputs for a set simulation length
3. Script to integrate the model with different control input profiles (u1(t) and u2(t))
