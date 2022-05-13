# How to build a 6DOF Sensorized Steerable Needle

There are two styles of needle that we build:
 - NIH style that contains a larger head to house the sensor, with a smaller backbone to reduce bending stiffness and thus maximize the steerability of the needle
 - Unibody design made of larger tube, typically with a laser-patterning on the backbone to reduce the bending stiffness.

1. Locate Superelastic Nitinol stock. The minimum ID requirement is 1.0 mm, as the sensor size is 0.9mm x 9mm. Make sure that the wall thickness is at least 0.1mm thick, as thinner wall nitinol is prone to buckling/kinking/failure. We typically use a smaller backbone of 0.7mm OD. If the needle is to be deployed through an endoscope, we must ensure that the total length of the prototype is long enough to satisfy:

```
Needle Length = 2*(Max Insertion Length) + Scope Length + Distance Between Actuation Unit and Scope + Buffer
```

Typically, we manufacture a needle to be ~ 1.3m long, for a 0.9m long scope, capable of a 100mm insertion length, accounting for 50mm distance between the scope and robot, with 50mm buffer.

2. After locating the Nitinol stock, we must decide which style of needle we are going to build. It is advantageous to have as few individual pieces of Nitinol composing the needle as possible, as the needle can fail at the bonded glue-joint interfaces.
- NIH style: 3 pieces - Needle tip, Needle Shaft, Connector Tube
- Unibody style: 3 pieces - Lasercut Needle, Needle Shaft, Connector Tube

Note: especially with the smaller backbone on the NIH style needle, the backbone can buckle when inserting with the actuation unit depending on the tissue forces. We need to support the needle during insertion to prevent it from breaking and/or abort the steer if we see that the tissue forces are high enough to buckle the needle. In the case of the lung, this typically means that we are colliding with anatomy such as the bronchial airways or blood vessels.

3. 
