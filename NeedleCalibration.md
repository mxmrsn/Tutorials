# Needle Calibration Process

In this section we aim to calibrate the rotational offset of 6DOF sensor to bevel plane of the needle. We have to do this because we have no way of accurately orienting the 6DOF sensor when mounting/gluing it into the needle tip.

## Rotational Offset Calibration

We formulate the calibration by considering a pure insertion of the needle. We know that when we perform this insertion, the needle will deflect in the direction of the bevel plane and roughly trace out a circle. Therefore, it is reasonable to say that we want to fit a circle in a plane to the sensor position data as the needle is inserted.

Considering the position measurements of the sensor as the needle is inserted, we have:

```
pts = sensor(1:3,:); % position of 6DOF sensor
```

We can parameterize a circle in a plane by three parameters: the center point of the circle ([1 x 3]), the normal vector of the plane it resides in ([1 x 3]) and the radius of the circle (r - simply a scalar value).

Using this parameterization, we aim to find these 3 parameters (2 vectors and a scalar) by minimizing some objective function that is performing the fit of the needle position data to the circle residing in the plane.
