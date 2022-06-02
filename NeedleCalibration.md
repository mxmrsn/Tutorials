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

```
param = [cx cy cz nx ny nz r]';
```

The error (objective) function that we want to minimize:

```
for ii = 1:N
  % e(:,ii) = distance of pts(:,ii) from closest point on circle arc with params
end
E = e(:); % this stacks all error components into tall vector
```

After solving for the best parameters using a MATLAB or Google CERES (C++) solver, we want to compute the offset angle.

The angle can be described as the angle applied about the z-axis of the base sensor that aligns the x-axis of the sensor with the normal vector. Put otherwise:

```
  Rz = axang2rotm([0 0 1 theta])
  Rm = Rs*Rz;
  Rmx = Rm(:,1:3);
  n = [nx; ny; nz];
```

We want to find the angle theta that minimizes the angle between ```Rmx``` and the normal vector of the plane ```n```.

We can relate the projection of these two vectors through the definition of the [dot product](https://en.wikipedia.org/wiki/Dot_product) of two vectors. We can solve for theta using a cosine inverse. However, we need to be careful of a few things:
1. Convention of the pure insertion direction (I'm not sure this is enough - basically make sure that the fit circle normal is always in the same direction w.r.t. the EM tracker frame, otherwise sometimes it is reversed w.r.t. the plane)
2. Cosine inverse is not great, as it can produce a reversed result. Instead, define stheta and ctheta and use ```atan2()``` to solve for theta.

![circle_fit](/imgs/NeedleCalibration/circle_fit.png)
