# Needle Calibration Process

In this section we aim to calibrate the rotational offset of 6DOF sensor to bevel plane of the needle. We have to do this because we have no way of accurately orienting the 6DOF sensor when mounting/gluing it into the needle tip.

## Rotational Offset Calibration

We formulate the calibration by considering a pure insertion of the needle. We know that when we perform this insertion, the needle will deflect in the direction of the bevel plane and roughly trace out a circle. Therefore, it is reasonable to say that we want to fit a circle in a plane to the sensor position data as the needle is inserted (for a minimum insertion length).

Considering the position measurements of the sensor as the needle is inserted, we have:

```
sensor_pose = [px; py; pz; qw; qx; qy; qz];
pts = sensor_pose(1:3,:); % position of 6DOF sensor
```

We can parameterize a circle in a plane by three parameters: the center point of the circle ([3 x 1]), the normal vector of the plane it resides in ([4 x 1]), and the radius of the circle (r - simply a scalar value).

Using this parameterization, we aim to find these 3 parameters (2 vectors and a scalar) by minimizing some objective function that is performing the fit of the needle position data to the circle residing in the plane.

More explicitly, we have a parameter vector:

<img src="https://render.githubusercontent.com/render/math?math=\t \lVertc_x \hspace{1mm} c_y \hspace{1mm} c_z \hspace{1mm} n_x \hspace{1mm} n_y \hspace{1mm} n_z \hspace{1mm} r}">

We aim to minimize the following objective function:

<img src="https://render.githubusercontent.com/render/math?math=f{\sum_{i=1}^(N) d_p}">


<img src="https://render.githubusercontent.com/render/math?math={\min_{T \in SE(3), C} \sum_{i=1}^{N_s} \sum_{j=1}^{N_m} C_{ij} \hspace{1mm} \lVert Tp^{m_j} - p^{s_i} \rVert^2}">
