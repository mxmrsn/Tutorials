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

3. If the needle is not lasercut with the desired needle tip geometry, we usually fabricate this manually. Using a dremel mounted in the bench vise, and observing proper safety measures (tied up hair, no long sleeves, safety glasses, etc.), we grind the bevel geometry into the Nitinol tube. We have an aluminum jig that can help with grinding the correct bevel angle - I usually just do this freehand, checking frequently to make sure that I don't remove too much material and overshoot the desired geometry.

4. Deburring - using a fresh, sharp Xacto knife blade, make sure to de-burr the edge of the tube where the cut was made to ensure that the ID/OD geometry is preserved and that the sensor can fit through. You can also use needle files and the dissection microscope to aide in this process. In all of these steps, be sure to take your time, otherwise you have to start over.

5. Assemble the needle. TODO: add pics and diagrams of how this goes together

6. Glue the sensor into the needle, and glue the bevel face closed. Loctite gap-filling super glue works best with accelerant. Note that applying accelerant creates a lower-strength bond with more brittle material properties. This is not recommended for the connections of the needle to the shaft or connector tube. The best glue for those bonds is rubberized/flexible superglue or epoxy.

7. Put a plastic sheath over the exposed sensor wires, ensuring that there is adequate overlap of the sheath onto the Nitinol tube backend (not too much though to make sure that the collet can be mounted at the appropriate spot for coupling to the actuation unit).

8. Soldering the sensor wires into the connector. TODO: add picture of pinout. Glue the sensor wires to the SROM chip to strain-relief them, make sure that the sheath is inside of the plastic collet when securing them down. The sensor wires should not be in tension or strained - the sheath should provide the mechanical attachment of the Nitinol tube to the plastic connector.

9. Programming the SROM. Using NDI 6D Architect, upload the .ROM file onto the SROM chip. The .ROM files can be obtained through the NDI Support site - you need to have an account to login to access these resources.

10. Open NDI Track and ensure that the sensor gives good readings and does not give 'BROKEN_SENSOR' or 'MISSING_TOOL' error codes.

You now have a sensorized steerable needle! Keep in mind that in order to steer this under closed-loop control the needle rotational offset must be calibrated, as we have no way of orienting the sensor roll angle with respect to the bevel. This will be covered in [NeedleCalibration](NeedleCalibration.md).
